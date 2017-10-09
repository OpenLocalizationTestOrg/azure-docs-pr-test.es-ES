## <a name="repeatability-during-copy"></a>Repetibilidad durante la copia
Cuando copia tooAzure de datos SQL o SQL Server de otros datos almacena una necesidades tookeep repetibilidad en mente tooavoid resultados imprevistos. 

Al copiar datos tooAzure base de datos SQL o SQL Server, actividad de copia aparecerá por tabla del conjunto de datos toohello receptor de predeterminado ANEXAR Hola de forma predeterminada. Por ejemplo, al copiar datos de un origen de archivo CSV (datos de valores separados por comas) que contiene dos registros tooAzure base de datos SQL o SQL Server, esto es qué tabla Hola aspecto:

```
ID    Product        Quantity    ModifiedDate
...    ...            ...            ...
6    Flat Washer    3            2015-05-01 00:00:00
7     Down Tube    2            2015-05-01 00:00:00
```

Suponga que encontró errores en el archivo de código fuente y la cantidad de Hola actualizada de Tube hacia abajo desde too4 2 en el archivo de código fuente de Hola. Si vuelve a ejecutar el segmento de datos de Hola durante ese período, encontrará dos nuevos registros anexan tooAzure base de datos SQL o SQL Server. Hola siguiente se da por supuesto que ninguna de las columnas de hello en la tabla de Hola tiene restricción de clave principal de Hola.

```
ID    Product        Quantity    ModifiedDate
...    ...            ...            ...
6    Flat Washer    3            2015-05-01 00:00:00
7     Down Tube    2            2015-05-01 00:00:00
6    Flat Washer    3            2015-05-01 00:00:00
7     Down Tube    4            2015-05-01 00:00:00
```

tooavoid esto, necesitará una semántica UPSERT toospecify mediante el aprovechamiento de uno de Hola por debajo de 2 mecanismos indicadas a continuación.

> [!NOTE]
> Un segmento se puede volver a ejecutar automáticamente en Data Factory de Azure según la directiva de reintento de hello especificada.
> 
> 

### <a name="mechanism-1"></a>Mecanismo 1
Puede aprovechar **sqlWriterCleanupScript** toofirst propiedad realizar la acción de limpieza cuando se ejecuta un segmento. 

```json
"sink":  
{ 
  "type": "SqlSink", 
  "sqlWriterCleanupScript": "$$Text.Format('DELETE FROM table WHERE ModifiedDate >= \\'{0:yyyy-MM-dd HH:mm}\\' AND ModifiedDate < \\'{1:yyyy-MM-dd HH:mm}\\'', WindowStart, WindowEnd)"
}
```

Hello script de limpieza se ejecutaría primera durante la copia de un sector determinado que podría eliminar datos de Hola de segmento de toothat Hola tabla SQL correspondiente. actividad Hello posteriormente insertará los datos de hello en hello Table de SQL. 

Si el segmento de hello es ahora vuelva a ejecutar; a continuación, encontrará Hola cantidad se actualiza como se desea.

```
ID    Product        Quantity    ModifiedDate
...    ...            ...            ...
6    Flat Washer    3            2015-05-01 00:00:00
7     Down Tube    4            2015-05-01 00:00:00
```

Imagine Hola registro arandela sin formato se quita de hello original csv. A continuación, volver a ejecutar segmento Hola generaría Hola siguiente resultado: 

```
ID    Product        Quantity    ModifiedDate
...    ...            ...            ...
7     Down Tube    4            2015-05-01 00:00:00
```
Nada nuevo tenía toobe realiza. actividad de copia de Hello ejecutó Hola limpieza script toodelete Hola datos correspondientes para dicho sector. A continuación, debe leer Hola entrada desde archivo csv de hello (que, a continuación, incluidos 1 sólo registro) y se inserta en hello tabla. 

### <a name="mechanism-2"></a>Mecanismo 2
> [!IMPORTANT]
> sliceIdentifierColumnName no se admite en este momento para Almacenamiento de datos SQL de Azure. 

Capacidad de repetición de otro mecanismo tooachieve es tener una columna dedicada (**sliceIdentifierColumnName**) en hello la tabla de destino. Esta columna se usaría por factoría de datos de Azure tooensure Hola origen y destino permanecen sincronizadas. Este enfoque funciona cuando se produce la flexibilidad de cambiar o definir el esquema de tabla SQL de destino de Hola. 

Esta columna se usaría por factoría de datos de Azure para fines de capacidad de repetición y en proceso de hello Data Factory de Azure no realizará ningún esquema cambia toohello tabla. Forma toouse este enfoque:

1. Definir una columna de tipo binary (32) en el destino de hello Table de SQL. No debería haber ninguna restricción en esta columna. Llamemos a esta columna 'ColumnForADFuseOnly' para este ejemplo.
2. Usarlo en la actividad de copia de hello como sigue:
   
    ```json
    "sink":  
    { 
   
        "type": "SqlSink", 
        "sliceIdentifierColumnName": "ColumnForADFuseOnly"
    }
    ```

Factoría de datos de Azure se llenará esta columna según su necesidad tooensure Hola origen y destino están sincronizadas. valores de Hello de esta columna no deben usarse fuera de este contexto de usuario de Hola. 

Toomechanism similar 1, se de actividad de copia automáticamente primera limpiar los datos de Hola para hello proporcionadas segmento desde el destino de hello Table de SQL y, a continuación, ejecute actividad de copia de hello normalmente datos de hello tooinsert de toodestination de origen para dicho sector. 

