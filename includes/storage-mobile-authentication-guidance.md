## <a name="configure-your-application-tooaccess-azure-storage"></a>Configurar el almacenamiento de Azure tooaccess de aplicación
Los servicios de almacenamiento de aplicación tooaccess no hay tooauthenticate de dos maneras:

* Clave compartida: la clave compartida solo se usa para realizar pruebas.
* Firma de acceso compartido (SAS): SAS para aplicaciones de producción.

### <a name="shared-key"></a>Clave compartida
La autenticación de clave compartida significa que la aplicación usará el nombre de cuenta y tooaccess clave de cuenta de servicios de almacenamiento. Para los fines de Hola de rápidamente que muestra cómo toouse esta biblioteca, vamos a usar autenticación Shared Key en esta introducción a.

> [!WARNING] 
> **Use la autenticación de clave compartida solamente para las pruebas.** El nombre de cuenta y la clave de cuenta, que le ofrecen toohello de acceso completo de lectura/escritura asociados de cuenta de almacenamiento, será persona tooevery distribuida que permite descargar la aplicación. Esta práctica **no** se recomienda, ya que se corre el riesgo de que los clientes en los que no se confía pongan la clave en peligro.
> 
> 

Si se usa la autenticación de clave compartida, se creará una [cadena de conexión](../articles/storage/common/storage-configure-connection-string.md). cadena de conexión de Hello consta de:  

* Hola **DefaultEndpointsProtocol** -puede elegir HTTP o HTTPS. De todos modos, se recomienda encarecidamente el uso de HTTPS.
* Hola **nombre de la cuenta** : hello nombre de la cuenta de almacenamiento
* Hola **clave de cuenta** - en hello [Portal de Azure](https://portal.azure.com), desplácese tooyour cuenta de almacenamiento y haga clic en hello **claves** icono toofind esta información.
* (Opcional) **EndpointSuffix** : se usa para servicios de almacenamiento en regiones con distintos sufijos de punto de conexión, como Azure China o Azure Governance.

Este es un ejemplo de cadena de conexión que usa la autenticación de clave compartida.

`"DefaultEndpointsProtocol=https;AccountName=your_account_name_here;AccountKey=your_account_key_here"`

### <a name="shared-access-signatures-sas"></a>Firmas de acceso compartido (SAS)
Para una aplicación móvil, Hola recomendada método para autenticar una solicitud de un cliente contra Hola servicio de almacenamiento de Azure consiste en usar una firma de acceso compartido (SAS). SAS permite toogrant un recurso de tooa de acceso de cliente para un periodo de tiempo, con un conjunto de permisos especificado.
Como propietario de la cuenta de almacenamiento de hello, necesitará toogenerate una SAS para su tooconsume clientes móviles. toogenerate Hola SAS, probablemente deseará toowrite un servicio independiente que genera Hola SAS toobe distribuida tooyour clientes. Para realizar pruebas, puede usar hello [Microsoft Azure Storage Explorer](http://storageexplorer.com) o hello [Portal de Azure](https://portal.azure.com) toogenerate una SAS. Cuando creas Hola SAS, puede especificar el intervalo de tiempo de Hola durante qué Hola SAS es válida y permisos Hola Hola SAS concede toohello cliente.

Hola de ejemplo siguiente muestra cómo toouse Hola toogenerate de Microsoft Azure Storage Explorer una SAS.

1. Si no lo ha hecho ya, [Hola instalar Microsoft Azure Storage Explorer](http://storageexplorer.com)
2. Conectar tooyour suscripción.
3. Haga clic en la cuenta de almacenamiento y haga clic en la pestaña Hola "acciones" final Hola izquierda. Haga clic en "Obtener firma de acceso compartido" toogenerate una "cadena de conexión" de la SAS.
4. Este es un ejemplo de una cadena de conexión de SAS que concede permisos lectura y escritura en el servicio de hello, contenedor y nivel de objeto de servicio de blob de Hola de cuenta de almacenamiento de Hola.
   
   `"SharedAccessSignature=sv=2015-04-05&ss=b&srt=sco&sp=rw&se=2016-07-21T18%3A00%3A00Z&sig=3ABdLOJZosCp0o491T%2BqZGKIhafF1nlM3MzESDDD3Gg%3D;BlobEndpoint=https://youraccount.blob.core.windows.net"`

Como puede ver, cuando usa una SAS, no expone su clave de cuenta en la aplicación. Puede aprender más acerca de SAS y prácticas recomendadas para utilizar SAS consultando [firmas de acceso compartido: modelo de descripción Hola SAS](../articles/storage/common/storage-dotnet-shared-access-signature-part-1.md).

