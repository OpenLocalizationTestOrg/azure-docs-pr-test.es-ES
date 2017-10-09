---
title: "aaaImport y exportación de base de datos de Azure para MySQL | Documentos de Microsoft"
description: "Este artículo explica maneras tooimport y exportación de bases de datos comunes en la base de datos de Azure para MySQL, mediante herramientas como MySQL Workbench."
services: mysql
author: v-chenyh
ms.author: v-chenyh
manager: jhubbard
editor: jasonwhowell
ms.service: mysql-database
ms.topic: article
ms.date: 06/13/2017
ms.openlocfilehash: e2c036773d975df2eea2a59d166ea10567218a41
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="migrate-your-mysql-database-by-using-import-and-export"></a>Migración de la base de datos de MySQL mediante importación y exportación
Este artículo explica dos tooimporting de enfoques comunes y exportar datos tooan base de datos de MySQL server mediante el uso de MySQL Workbench. 

## <a name="before-you-begin"></a>Antes de empezar
toostep a través de este tooguide cómo, necesita:
- Un servidor de Azure Database for MySQL, que puede obtener después de consultar [Creación de un servidor de Azure Database for MySQL con Azure Portal](quickstart-create-mysql-server-database-using-azure-portal.md).
- MySQL Workbench [descargado](https://dev.mysql.com/downloads/workbench/), o MySQL herramienta tooimport y exportación de otro.

## <a name="use-common-tools"></a>Uso de herramientas comunes
Usar herramientas comunes como MySQL Workbench, Toad o Navicat tooremotely conectar importar o exportar datos a la base de datos de MySQL. 

Use estas herramientas en el equipo cliente con un tooAzure tooconnect de conexión de Internet base de datos de MySQL. Use una conexión cifrada SSL para aprovechar los procedimientos recomendados de seguridad tal y como se describe en [Conectividad SSL de Azure Database for MySQL](concepts-ssl-connection-security.md).

No necesita toomove la importación y exportación ubicación de archivos tooany nube especiales al migrar tooAzure base de datos de MySQL. 

## <a name="create-a-database-on-hello-azure-database-for-mysql-server"></a>Crear una base de datos en hello base de datos de MySQL server
Crear una base de datos vacía en hello base de datos de MySQL server donde desea toomigrate Hola datos. Usar una herramienta como MySQL Workbench, Toad o Navicat base de datos de la hello toocreate. base de datos de Hello puede tener Hola mismo nombre de base de datos de Hola que contenga los datos de hello el volcado o puede crear una base de datos con un nombre diferente.

tooget conectado, encontrar la información de conexión de hello en hello **propiedades** panel en la base de datos de Azure para MySQL.

![Buscar información de conexión de Hola Hola portal de Azure](./media/concepts-migrate-import-export/1_server-properties-name-login.png)

Agregar tooMySQL de información de conexión de hello Workbench.

![Cadena de conexión de MySQL Workbench](./media/concepts-migrate-import-export/2_setup-new-connection.png)

## <a name="determine-when-toouse-import-and-export-techniques-instead-of-a-dump-and-restore"></a>Determinar cuándo toouse importar y exportar técnicas en lugar de un volcado de memoria y la restauración
Usar MySQL herramientas tooimport y exportar bases de datos en la base de datos de MySQL de Azure en hello los escenarios siguientes. En otros escenarios, puede beneficiarse del uso de hello [dump y restore](concepts-migrate-dump-restore.md) enfocar en su lugar. 

- Cuando necesite tooselectively elija tooimport algunas de las tablas de base de datos MySQL existente en la base de datos de MySQL de Azure, es mejor toouse Hola importar y exportar técnica.  Al hacerlo, puede omitir cualquier tablas innecesarias de hello migración toosave tiempo y recursos. Por ejemplo, usar hello `--include-tables` o `--exclude-tables` cambiar con [mysqlpump](https://dev.mysql.com/doc/refman/5.7/en/mysqlpump.html#option_mysqlpump_include-tables) hello y `--tables` cambiar con [mysqldump](https://dev.mysql.com/doc/refman/5.7/en/mysqldump.html#option_mysqldump_tables).
- Cuando se mueven los objetos de base de datos de Hola que no sean tablas, créelas explícitamente. Incluir restricciones (clave principal, clave externa, índices), vistas, funciones, procedimientos, desencadenadores, y los objetos de otras bases de datos que desea toomigrate.
- Si va a migrar datos desde orígenes de datos externos que no sean una base de datos de MySQL, cree archivos planos e impórtelos mediante el uso de [mysqlimport](https://dev.mysql.com/doc/refman/5.7/en/mysqlimport.html).

Asegúrese de que todas las tablas de base de datos de hello usan motor de almacenamiento de hello InnoDB cuando se carga datos en la base de datos de MySQL. Base de datos de Azure para MySQL admite solo Hola InnoDB motor de almacenamiento, por lo que no es compatible con los motores de almacenamiento alternativa. Si las tablas requieren motores de almacenamiento alternativo, que seguro tooconvert ellos formato del motor toouse Hola InnoDB antes de hello migración tooAzure base de datos de MySQL. 

Por ejemplo, si tiene una aplicación web o WordPress que utiliza el motor de MyISAM hello, primero convertir Hola tablas mediante la migración de datos de hello en tablas InnoDB. A continuación, restaure tooAzure base de datos de MySQL. Cláusula de uso hello `ENGINE=INNODB` tooset Hola motor para la creación de una tabla y, a continuación, transfiera los datos de Hola a tabla compatible de hello antes de la migración de Hola. 

   ```sql
   INSERT INTO innodb_table SELECT * FROM myisam_table ORDER BY primary_key_columns
   ```

## <a name="performance-recommendations-for-import-and-export"></a>Recomendaciones de rendimiento para la importación y exportación
-   Cree los índices agrupados y las claves principales antes de cargar los datos. Cargue los datos en el orden de la clave principal. 
-   Retrase la creación de índices secundarios hasta después de que se hayan cargado los datos. Cree todos los índices secundarios después de la carga. 
-   Deshabilite las restricciones de las claves externas antes de la carga. El hecho de deshabilitar las comprobaciones de las claves externas favorece un aumento significativo del rendimiento. Habilitar las restricciones de Hola y comprobar los datos de hello después de la integridad referencial de hello carga tooensure.
-   Cargue los datos en paralelo. Evite demasiada paralelismo que podría provocar toohit un límite de recursos y supervisar los recursos mediante el uso de las métricas de hello disponibles en hello portal de Azure. 
-   Use tablas con particiones cuando sea necesario.

## <a name="import-and-export-by-using-mysql-workbench"></a>Importación y exportación mediante MySQL Workbench
Hay dos maneras de tooexport e importar datos en el área de trabajo de MySQL. Cada una de ellas sirve para un propósito diferente. 

### <a name="table-data-export-and-import-wizards-from-hello-object-browsers-context-menu"></a>Datos de la tabla exportación e importación a asistentes desde el menú contextual del Examinador de objetos de Hola
![Asistentes de MySQL Workbench en el menú contextual del Examinador de objetos de Hola](./media/concepts-migrate-import-export/p1.png)

asistentes de Hola para datos de la tabla admiten la importación y las operaciones de exportación mediante el uso de archivos CSV y JSON. Incluyen varias opciones de configuración, como separadores, selección de columnas y selección de codificación. Puede ejecutar cada asistente en servidores locales o servidores de MySQL conectados de forma remota. acción de importación de Hello incluye la tabla, columna y asignación de tipos. 

Para tener acceso a estos asistentes desde el menú contextual del Examinador de objetos de hello haciendo clic en una tabla. A continuación, elija **Asistente para exportación de datos de tabla** o **Asistente para importación de datos de tabla**. 

#### <a name="table-data-export-wizard"></a>Asistente para exportación de datos de tabla
Hello en el ejemplo siguiente se exporta archivo CSV de hello tabla tooa: 
1. Haga clic en tabla de Hola de hello toobe de base de datos exportado. 
2. Seleccione **Table Data Export Wizard** (Asistente para exportación de datos de tabla). Seleccione Hola columnas toobe exportado, desplazamiento de fila (si existe) y cuenta (si existe). 
3. En hello **seleccionar datos para exportar** página, haga clic en **siguiente**. Seleccione la ruta de acceso de archivo hello, CSV o JSON tipo de archivo. También selecciona separador de línea de hello, método de inclusión de cadenas y el separador de campos. 
4. En hello **ubicación del archivo de salida seleccione** página, haga clic en **siguiente**. 
5. En hello **exportar datos** página, haga clic en **siguiente**.

#### <a name="table-data-import-wizard"></a>Asistente para importación de datos de tabla
Hello en el ejemplo siguiente se importa Hola tabla desde un archivo CSV:
1. Haga clic en tabla de Hola de hello toobe de base de datos importado. 
2. Examinar tooand seleccione Hola toobe de archivo CSV importado y, a continuación, haga clic en **siguiente**. 
3. Seleccione la tabla de destino de hello (nuevo o existente) y Active o desactive hello **truncar tabla antes de importar** casilla de verificación. Haga clic en **Siguiente**.
4. Seleccione hello y codificación toobe columnas importado y, a continuación, haga clic en **siguiente**. 
5. En hello **importar datos** página, haga clic en **siguiente**. Asistente de Hello importa datos hello en consecuencia.

### <a name="sql-data-export-and-import-wizards-from-hello-navigator-pane"></a>Datos de SQL exportación e importación a asistentes desde el panel del navegador de Hola
Utilizar un asistente tooexport o importar SQL generado a partir de MySQL Workbench o generado a partir de comando de mysqldump Hola. Obtener acceso a estos asistentes de hello **navegador** panel o seleccionando **Server** desde el menú principal de Hola. A continuación, seleccione **Exportación de datos** o **Importación de datos**. 

#### <a name="data-export"></a>Exportación de datos
![Exportación de datos de MySQL Workbench usando el panel de navegación de Hola](./media/concepts-migrate-import-export/p2.png)

Puede usar hello **exportar datos** ficha tooexport los datos de MySQL. 
1. Seleccione cada esquema que desee tooexport, opcionalmente, elija los objetos o tablas de esquema específico de cada esquema y generar exportación Hola. Opciones de configuración son independientes SQL de archivo o carpeta de proyecto de exportación tooa, volcado de eventos y las rutinas almacenadas u omitir los datos de la tabla. 
 
   O bien, usar **exportar un conjunto de resultados** tooexport un resultado concreto establecido en hello SQL tooanother formato del editor, como CSV, JSON, HTML y XML. 
3. Seleccione tooexport de objetos de base de datos de Hola y configurar opciones relacionadas con Hola.
4. Haga clic en **actualizar** objetos de tooload Hola actuales.
5. Si lo desea, abra hello **opciones avanzadas** ficha operación de exportación de toorefine Hola. Por ejemplo, agregue bloqueos de tabla, utilice instrucciones replace en lugar de insert y entrecomille los identificadores con caracteres de acento grave.
6. Haga clic en **iniciar exportación** proceso de exportación de toobegin Hola.


#### <a name="data-import"></a>Importación de datos
![Importación de los datos en MySQL Workbench mediante Management Navigator](./media/concepts-migrate-import-export/p3.png)

Puede usar hello **importación de datos** ficha tooimport o restaurar los datos exportados de operación de exportación de datos de Hola o de comando de hello mysqldump. 
1. Elija la carpeta de proyecto de Hola o un archivo SQL independiente, elija tooimport de esquema de hello en o elija **New** toodefine un nuevo esquema. 
2. Haga clic en **iniciar importar** proceso de importación de toobegin Hola.

## <a name="next-steps"></a>Pasos siguientes
Para conocer otro método de migración, consulte [Migración de la Base de datos MySQL mediante el volcado y la restauración en Azure Database for MySQL](concepts-migrate-dump-restore.md). 
