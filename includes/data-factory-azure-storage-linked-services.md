### <a name="azure-storage-linked-service"></a>Servicio vinculado de Almacenamiento de Azure
Hola **servicio vinculado de almacenamiento de Azure** permite toolink un generador de datos de Azure de tooan de cuenta de almacenamiento de Azure mediante el uso de hello **clave de cuenta**, lo que proporciona la factoría de datos de hello con acceso global toohello Azure Almacenamiento de información. Hello en la tabla siguiente proporciona una descripción para JSON elementos específico tooAzure servicio vinculado de almacenamiento.

| Propiedad | Descripción | Obligatorio |
|:--- |:--- |:--- |
| type |propiedad de tipo Hello debe establecerse en: **azurestorage.** |Sí |
| connectionString |Especifique la información necesaria tooconnect tooAzure almacenamiento para la propiedad connectionString de Hola. |Sí |

Vea Hola artículo clave de cuenta de hello tooview/copia de pasos siguiente para un almacenamiento de Azure: [ver, copiar y regenerar las claves de acceso de almacenamiento](../articles/storage/common/storage-create-storage-account.md#manage-your-storage-account).

**Ejemplo:**  

```json
{  
    "name": "StorageLinkedService",  
    "properties": {  
        "type": "AzureStorage",  
        "typeProperties": {  
            "connectionString": "DefaultEndpointsProtocol=https;AccountName=<accountname>;AccountKey=<accountkey>"  
        }  
    }  
}  
```

### <a name="azure-storage-sas-linked-service"></a>Servicio vinculado de SAS Azure Storage
Una firma de acceso compartido (SAS) proporciona acceso delegado tooresources en su cuenta de almacenamiento. Permite toogrant un cliente limitada tooobjects permisos en su cuenta de almacenamiento en un periodo de tiempo y con un conjunto especificado de permisos, sin necesidad de tooshare las claves de acceso de cuenta. Hola SAS es un URI que abarca el proceso en sus parámetros de consulta toda la información de hello necesaria para el recurso de almacenamiento de tooa de acceso autenticado. recursos de almacenamiento de tooaccess con hello SAS, cliente hello solo necesita toopass en el método o constructor adecuado de hello SAS toohello. Para obtener información detallada sobre SAS, consulte [firmas de acceso compartido: Hola descripción modelo SAS](../articles/storage/common/storage-dotnet-shared-access-signature-part-1.md)

> [!IMPORTANT]
> Ahora Azure Data Factory solo admite **SAS de servicio**, pero no SAS de cuenta. Vea [tipos de firmas de acceso compartido](../articles/storage/common/storage-dotnet-shared-access-signature-part-1.md#types-of-shared-access-signatures) para obtener más información acerca de estos dos tipos y cómo tooconstruct. Tenga en cuenta Hola URL de SAS generable desde portal de Azure o el Explorador de almacenamiento es una SAS de cuenta, que no es compatible.
> 

Hola SAS de almacenamiento de Azure vinculada servicio permite toolink un generador de datos de Azure tooan cuenta de almacenamiento de Azure mediante una firma de acceso compartido (SAS). Proporciona factoría de datos de hello con acceso restringido tiempo enlazadas a recursos de tooall/específicos (blob o el contenedor) en el almacenamiento de Hola. Hello en la tabla siguiente proporciona la descripción de JSON elementos específico tooAzure servicio vinculado de SAS de almacenamiento. 

| Propiedad | Descripción | Obligatorio |
|:--- |:--- |:--- |
| type |propiedad de tipo Hello debe establecerse en: **AzureStorageSas** |Sí |
| sasUri |Especificar recursos de almacenamiento de Azure de toohello de URI de firma de acceso compartido como blob, contenedor o tabla.  |Sí |

**Ejemplo:**

```json
{  
    "name": "StorageSasLinkedService",  
    "properties": {  
        "type": "AzureStorageSas",  
        "typeProperties": {  
            "sasUri": "<Specify SAS URI of hello Azure Storage resource>"   
        }  
    }  
}  
```

Al crear un **URI de SAS**, tenga en cuenta Hola siguientes:  

* Establecer lectura/escritura adecuados **permisos** en objetos en función de cómo Hola vinculadas servicio (lectura, escritura, lectura/escritura) se utilizan en la factoría de datos.
* Establezca la **hora de expiración** adecuadamente. Asegúrese de que no caducan los objetos de almacenamiento de hello acceso tooAzure dentro del periodo activo de Hola de canalización de Hola.
* URI debe crearse en el contenedor/blob derecho Hola o nivel de tabla en función de hello necesario. Un blob de Azure de Uri de SAS tooan permite tooaccess de servicio de factoría de datos de hello ese blob determinado. Un contenedor de blobs de Azure de Uri de SAS tooan permite hello tooiterate de servicio de factoría de datos a través de blobs del contenedor. Si necesita acceso de tooprovide más/menos objetos más tarde o actualización Hola SAS URI, recuerde tooupdate Hola vinculado servicio con Hola nuevo URI.   

