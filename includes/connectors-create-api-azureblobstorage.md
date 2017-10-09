### <a name="prerequisites"></a>Requisitos previos
* Una cuenta de Azure; puede crear una [gratuita](https://azure.microsoft.com/free)
* Un [cuenta de almacenamiento de blobs de Azure](../articles/storage/common/storage-create-storage-account.md) como nombre de cuenta de almacenamiento de Hola y su clave de acceso. Esta información se muestra en las propiedades de Hola de cuenta de almacenamiento de Hola Hola portal de Azure. Más información sobre [Azure Storage](../articles/storage/common/storage-introduction.md).

Antes de usar su cuenta de almacenamiento de blobs de Azure en una aplicación de lógica, conectarse a tooyour cuenta de almacenamiento de blobs de Azure. Puede hacerlo fácilmente dentro de la aplicación lógica en hello portal de Azure.  

Conectar tooyour cuenta de almacenamiento de blobs de Azure con hello pasos:  

1. Cree una aplicación lógica. En el Diseñador de aplicaciones de la lógica de hello, agregar un desencadenador y, a continuación, agregue una acción. Seleccione **API administradas de Microsoft mostrar** Hola lista desplegable y, a continuación, escriba "blob" en el cuadro de búsqueda de Hola. Seleccione una de las acciones de hello:  
   
    ![paso de creación de la conexión de Almacenamiento de blobs de Azure](./media/connectors-create-api-azureblobstorage/azureblobstorage-1.png)  
2. Si anteriormente no ha creado ninguna conexión almacenamiento tooAzure, le pediremos detalles de la conexión de hello:   
   
    ![paso de creación de la conexión de Almacenamiento de blobs de Azure](./media/connectors-create-api-azureblobstorage/connection-details.png)  
3. Escriba los detalles de cuenta de almacenamiento de Hola. Aquellas propiedades con un asterisco son obligatorias.
   
   | Propiedad | Detalles |
   | --- | --- |
   | Nombre de la conexión * |Escriba cualquier nombre para la conexión. |
   | Nombre de la cuenta de Almacenamiento de Azure * |Escriba el nombre de cuenta de almacenamiento de Hola. nombre de cuenta de almacenamiento de Hola se muestra en las propiedades de almacenamiento de Hola Hola portal de Azure. |
   | Clave de acceso de la cuenta de Almacenamiento de Azure * |Escriba la clave de cuenta de almacenamiento de Hola. se muestran las claves de acceso de Hello en Propiedades del almacenamiento Hola Hola portal de Azure. |
   
    Estas credenciales son tooauthorize usa su tooconnect de aplicación lógica y obtener acceso a los datos. 
4. Seleccione **Crear**.
5. Se ha creado la conexión de anuncio Hola. Ahora, proceda con hello otro pasos de la aplicación lógica: 
   
    ![paso de creación de la conexión de Almacenamiento de blobs de Azure](./media/connectors-create-api-azureblobstorage/azureblobstorage-3.png)  

