>[!NOTE]
> Puede dejar comentarios en esta página para proporcionar información o a través del [foro de comentarios acerca de Azure](https://feedback.azure.com/forums/216843-virtual-machines) con la etiqueta #azerrormessage.

## <a name="error-response-format"></a>Formato de respuestas de error 
Máquinas virtuales de Azure usan hello siguiendo el formato JSON para la respuesta de error:

```json
{
  "status": "status code",
  "error": {
    "code":"Top level error code",
    "message":"Top level error message",
    "details":[
     {
      "code":"Inner evel error code",
      "message":"Inner level error message"
     }
    ]
   }
}
```

Una respuesta de error siempre incluye un código de estado y un objeto de error. Cada objeto de error contiene siempre un código de error y un mensaje. Si hello se crea la VM con una plantilla, el objeto de error de hello también contiene una sección de detalles que contiene un nivel interno de códigos de error y el mensaje. Normalmente, hello mayoría interna nivel de mensaje de error es Error de raíz de Hola.


## <a name="common-virtual-machine-management-errors"></a>Errores habituales en la administración de máquinas virtuales

Esta sección enumeran los mensajes de error comunes Hola que pueden producirse al administrar las máquinas virtuales:

|  Código de error  |  Mensaje de error  |  
|  :------| :-------------|  
|  AcquireDiskLeaseFailed  |  No se pudo tooacquire concesión al crear el disco '{0}' con blob {1} URI. El blob ya está en uso.  |  
|  AllocationFailed  |  Error en la asignación. Por favor, reduzca el tamaño de la máquina virtual de Hola o número de máquinas virtuales, vuelva a intentar más tarde o intente implementar tooa conjunto de disponibilidad diferente o en otra ubicación de Azure.  |  
|  AllocationFailed  |  no se pudo Hola asignación de máquina virtual debido a error interno de tooan. Vuelva a intentarlo más tarde o intente implementar tooa otra ubicación.  |
|  ArtifactNotFound  |  Hola extensión de máquina virtual con el publicador '{0}' y el tipo '{1}' no se encontró en la ubicación '{2}'.  |
|  ArtifactNotFound  |  Tipo de extensión con el publicador '{0}', '{1}' y versión de controlador de tipo '{2}' no se encontró en el repositorio de extensión de Hola.  |
|  ArtifactVersionNotFound  |  Ninguna versión encontrada en el repositorio de artefactos Hola que satisface Hola solicitado versión '{0}'.  |
|  ArtifactVersionNotFound  |  Ninguna versión encontrada en el repositorio de artefactos Hola que satisface Hola solicitado versión '{0}' para la extensión de máquina virtual con el publicador '{1}' y tipo '{2}'.  |
|  AttachDiskWhileBeingDetached  |  No se puede adjuntar datos disco '{0}' tooVM '{1}' porque actualmente se va a separar disco Hola. Espere hasta que el disco de hello esté completamente desasociado y, a continuación, vuelva a intentarlo.  |
|  BadRequest  |  En esta región aún no se admiten conjuntos de disponibilidad alineados.  |
|  BadRequest  |  Adición de una máquina virtual con discos administrados toonon administrado por un conjunto de disponibilidad o adición de una máquina virtual con el blob según discos toomanaged conjunto de disponibilidad no se admite. Cree un conjunto de disponibilidad con la propiedad 'administrado' establecida en orden tooadd una máquina virtual con discos administrados tooit.  |
|  BadRequest  |  En esta región no se admiten discos administrados.  |
|  BadRequest  |  No se admiten varias instancias de VMExtension por controlador para un OS del tipo "{0}". VMExtension "{1}" con el controlador "{2}" ya se ha agregado o se ha especificado en la entrada.  |
|  BadRequest  |  La operación "{0}" no se admite en el recurso "{1}" con discos administrados.  |
|  CertificateImproperlyFormatted  |  representación de JSON del secreto recuperado de {0} Hello tiene un campo de datos que no es un archivo PFX con el formato correcto o contraseña Hola proporcionada no decodifica archivo PFX de hello correctamente.  |
|  CertificateImproperlyFormatted  |  datos de Hello recuperados de {0} no están pueden deserializar en JSON.  |
|  Conflicto  |  Tamaño de los discos se permite sólo cuando se crea una máquina virtual o cuando Hola VM está desasignada.  |
|  ConflictingUserInput  |  No se puede adjuntar el disco '{0}' como disco Hola ya pertenece a la máquina virtual '{1}'.  |
|  ConflictingUserInput  |  Grupos de recursos de origen y destino son Hola mismo.  |
|  ConflictingUserInput  |  Las cuentas de almacenamiento de origen y de destino del disco {0} son distintas.  |
|  ContainerAlreadyOnLease  |  Ya hay una concesión en el contenedor de almacenamiento de Hola que contiene el blob de hello con el URI {0}.  |
|  CrossSubscriptionMoveWithKeyVaultResources  |  solicitud de Hello mover recursos contiene recursos de KeyVault que hace referencia a uno o más {0} s en la solicitud de Hola. En la actualidad, esto no se admite en la instancia de Move entre suscripciones. Compruebe los detalles de error de Hola para hello Id. de recurso de KeyVault.  |
|  DiagnosticsOperationInternalError  |  Se produjo un error interno al procesar el perfil de diagnóstico de la máquina virtual {0}.  |
|  DiskBlobAlreadyInUseByAnotherDisk  |  {0} del BLOB ya está en uso por otro disco que pertenece tooVM '{1}'. Puede examinar los metadatos de blob de Hola Hola disco como información de referencia.  |
|  DiskBlobNotFound  |  No se puede toofind VHD blob con {0} URI para el disco '{1}'.  |
|  DiskBlobNotFound  |  No se puede toofind VHD blob con URI {0}.  |
|  DiskEncryptionKeySecretMissingTags  |  secreto de {0} no tiene etiquetas de hello {1}. Actualizar la versión de secreto de hello, agregar etiquetas de hello necesario y vuelva a intentar.  |
|  DiskEncryptionKeySecretUnwrapFailed  |  Error al realizar el desajuste del valor {0} del secreto mediante la clave {1}.  |
|  DiskImageNotReady  |  La imagen de disco {0} está en estado {1}. Vuelva a intentarlo cuando la imagen esté lista.  |
|  DiskPreparationError  |  Se produjeron uno o varios errores al preparar los discos de la máquina virtual. Para más información, consulte la vista de la instancia del disco.  |
|  DiskProcessingError  |  Procesamiento de disco se detiene cuando Hola VM tenga otros discos en discos con errores.  |
|  ImageBlobNotFound  |  No se puede toofind VHD blob con {0} URI para el disco '{1}'.  |
|  ImageBlobNotFound  |  No se puede toofind VHD blob con URI {0}.  |
|  IncorrectDiskBlobType  |  Los blobs de disco solo pueden ser del tipo blob en páginas. El blob {0} disco "{1}" es del tipo blob en bloques.  |
|  IncorrectDiskBlobType  |  Los blobs de disco solo pueden ser del tipo blob en páginas. El blob {0} es del tipo "{1}".  |
|  IncorrectImageBlobType  |  Los blobs de disco solo pueden ser del tipo blob en páginas. El blob {0} disco "{1}" es del tipo blob en bloques.  |
|  IncorrectImageBlobType  |  Los blobs de disco solo pueden ser del tipo blob en páginas. El blob {0} es del tipo "{1}".  |
|  InternalOperationError  |  No se pudo resolver la cuenta de almacenamiento "{0}". Asegúrese de que se creó mediante Hola proveedor de recursos de almacenamiento en hello mismo recurso de proceso de ubicación como Hola.  |
|  InternalOperationError  |  Error en las tareas de búsqueda del objetivo de {0}.  |
|  InternalOperationError  |  Se ha producido un error en la validación de perfil de red de saludo de la máquina virtual '{0}'.  |
|  InvalidAccountType  |  {0} de Hello AccountType no es válido.  |
|  InvalidParameter  |  valor de Hola de parámetro {0} no es válido.  |
|  InvalidParameter  |  no se permite la contraseña de administrador de Hello especificada.  |
|  InvalidParameter  |  "Hola proporcionado contraseña debe tener entre {0}-\ {1\\} caracteres y debe cumplir al menos {2} de requisitos de complejidad de contraseña desde siguientes hello: <ol><li> Contiene una letra mayúscula</li><li>Contiene una letra minúscula</li><li>Contiene un dígito numérico</li><li>Contiene un carácter especial</li></ol>  |
|  InvalidParameter  |  Hola, nombre de usuario de administrador especificado no está permitido.  |
|  InvalidParameter  |  No se puede adjuntar un disco de sistema operativo existente si VM hello se crea a partir de una imagen de plataforma o del usuario.  |
|  InvalidParameter  |  El nombre de contenedor {0} no es válido. Los nombres de contenedor deben tener una longitud de entre 3 y 63 caracteres, y pueden contener solo caracteres alfanuméricos en minúscula y el signo de guion. Antes y después del guion debe ir un carácter alfanumérico.  |
|  InvalidParameter  |  El nombre del contenedor {0} de la dirección URL {1} no es válido. Los nombres de contenedor deben tener una longitud de entre 3 y 63 caracteres, y pueden contener solo caracteres alfanuméricos en minúscula y el signo de guion. Antes y después del guion debe ir un carácter alfanumérico.  |
|  InvalidParameter  |  nombre de blob de Hello en la dirección URL {0} contiene una barra diagonal. Actualmente esto es algo que no se admite en discos.  |
|  InvalidParameter  |  URI de Hola {0} no parece toobe URI de blob correcto.  |
|  InvalidParameter  |  Un disco con el nombre '{0}' ya usa Hola mismo LUN: {1}.  |
|  InvalidParameter  |  Ya existe un disco llamado "{0}".  |
|  InvalidParameter  |  No se puede especificar la imagen de usuario invalidaciones para un disco ya definido en hello especificada la imagen de referencia.  |
|  InvalidParameter  |  Un disco con el nombre '{0}' ya usa Hola la misma dirección URL del VHD {1}.  |
|  InvalidParameter  |  Hola {0} el recuento de dominio de error especificado debe estar incluida en hello intervalo {1} too\ {2\}.  |
|  InvalidParameter  |  tipo de licencia de Hola {0} no es válido. Los tipos de licencia válidos son: Windows_Client o Windows_Server, con distinción de mayúsculas y minúsculas.  |
|  InvalidParameter  |  Nombre de host de Linux no puede superar {0} caracteres de longitud ni contener los caracteres siguientes de hello: {1}.  |
|  InvalidParameter  |  Ruta de acceso de destino para claves públicas Ssh está actualmente limitado tooits predeterminado valor {0} due tooa un problema conocido en el agente de aprovisionamiento de Linux.  |
|  InvalidParameter  |  Ya existe un disco en LUN {0}.  |
|  InvalidParameter  |  Suscripción {0} de solicitud de hello debe coincidir con {1} de suscripción de hello contenidos en el Id. de disco administrado Hola.  |
|  InvalidParameter  |  Los datos personalizados de OSProfile deben estar codificados en Base64 y su longitud máxima debe ser de {0} caracteres.  |
|  InvalidParameter  |  El nombre del blob en la dirección URL {0} debe terminar con la extensión "{1}".  |
|  InvalidParameter  |  {0}" no es un prefijo de nombre de blob VHD capturado válido. Los prefijos válidos coincide con regex "{1}".  |
|  InvalidParameter  |  No se pueden agregar certificados tooyour VM si no se ha aprovisionado el agente de máquina virtual de Hola.  |
|  InvalidParameter  |  Ya existe un disco en LUN {0}.  |
|  InvalidParameter  |  No se puede toocreate Hola VM porque Hola solicitado {0} de tamaño no está disponible en clúster Hola donde esté asignado actualmente conjunto de disponibilidad de Hola. Hola los tamaños disponibles son: {1}. Para más información acerca de la estrategia de cambio de tamaño de máquinas virtuales, consulte https://aka.ms/azure-resizevm.  |
|  InvalidParameter  |  Hola solicitado {0} de tamaño de máquina virtual no está disponible en la región actual de Hola. Hola tamaños disponibles en la región actual de hello son: {1}. Conozca más sobre los tamaños VM disponibles hello en cada región en https://aka.ms/azure-regions.  |
|  InvalidParameter  |  Hola solicitado {0} de tamaño de máquina virtual no está disponible en la región actual de Hola. Conozca más sobre los tamaños VM disponibles hello en cada región en https://aka.ms/azure-regions.  |
|  InvalidParameter  |  Nombre de usuario de administrador de Windows no puede ser más de {0} caracteres largos, terminan con un punto o contengan los caracteres siguientes de hello: {1}.  |
|  InvalidParameter  |  Nombre de equipo de Windows no puede ser más de {0} caracteres largos, contener únicamente números o contengan los caracteres siguientes de hello: {1}.  |
|  MissingMoveDependentResources  |  Hola mover la solicitud de recursos no contiene todos los recursos dependientes de Hola. Consulte los detalles del error para conocer los identificadores de recursos que faltan.  |
|  MoveResourcesHaveInvalidState  |  solicitud de Hello mover recursos contiene máquinas virtuales que están asociadas a las cuentas de almacenamiento no es válida. Consulte la información relativa a estos identificadores de recursos y nombres de cuenta de almacenamiento de referencia.  |
|  MoveResourcesHavePendingOperations  |  Hola mover la solicitud de recursos contiene recursos para los que está pendiente una operación. Consulte la información relativa a estos identificadores de recursos. Vuelva a intentar la operación cuando se haya completado hello las operaciones pendientes.  |
|  MoveResourcesNotFound  |  Hola mover recursos solicitud contiene los recursos que no se encuentra. Consulte la información relativa a estos identificadores de recursos.  |
|  NetworkingInternalOperationError  |  Error de asignación de red desconocido.  |
|  NetworkingInternalOperationError  |  Error de asignación de red desconocido  |
|  NetworkingInternalOperationError  |  Se produjo un error interno en el procesamiento de perfil de red de VM de Hola.  |
|  NotFound  |  no se encuentra {0} el conjunto de disponibilidad de Hola.  |
|  NotFound  |  Máquina Virtual de origen especificado en la solicitud de hello ' {0}' no existe en esta ubicación de Azure.  |
|  NotFound  |  No se encuentra el inquilino con el identificador {0}.  |
|  NotFound  |  no se encuentra la imagen de Hola {0}.  |
|  NotSupported  |  tipo de licencia de Hello es {0}, pero {1} de blob de imagen de hello no es local.  |
|  OperationNotAllowed  |  El conjunto de disponibilidad {0} no se puede eliminar. Antes de eliminar un conjunto de disponibilidad asegúrese de que no contiene ninguna máquina virtual.  |
|  OperationNotAllowed  |  Cambiar la disponibilidad del conjunto de SKU de 'Alineado' too'Classic' no está permitido.  |
|  OperationNotAllowed  |  No se puede modificar las extensiones de hello VM cuando Hola VM no se está ejecutando.  |
|  OperationNotAllowed  |  Hola acción de captura solo se admite en una máquina Virtual con discos de blob según. Use hello 'Image' recurso API toocreate una imagen de una máquina Virtual administrado.  |
|  OperationNotAllowed  |  no se puede crear el recurso de Hola {0} de {1} de la imagen hasta que la imagen se ha creado correctamente.  |
|  OperationNotAllowed  |  TooencryptionSettings de actualizaciones no se permite cuando se asigna VM, vuelva a intentarlo después de que se cancela la asignación de máquina virtual  |
|  OperationNotAllowed  |  No se admite la adición de un tooa de disco administrado máquina virtual con discos de blob según.  |
|  OperationNotAllowed  |  número máximo de Hola de discos de datos permitido toobe adjuntada tooa VM de este tamaño es {0}.  |
|  OperationNotAllowed  |  No se admite la adición de un tooVM de disco de blob según con discos administrados.  |
|  OperationNotAllowed  |  La operación '{0}' no se permite en la imagen '{1}' desde Hola que imagen está marcada para su eliminación. Sólo puede volver a intentar la operación de eliminación de hello (o esperar un toocomplete en curso de una).  |
|  OperationNotAllowed  |  No se permite la operación '{0}' en la máquina virtual '{1}' desde la máquina virtual es generalizada de Hola.  |
|  OperationNotAllowed  |  La operación "{0}" no se permite, ya que la colección de puntos de restauración "{1}" está marcada para su eliminación.  |
|  OperationNotAllowed  |  La operación "{0}" no se permite en la extensión de la máquina virtual "{1}", ya que está marcada para su eliminación. Sólo puede volver a intentar la operación de eliminación de hello (o esperar un toocomplete en curso de una).  |
|  OperationNotAllowed  |  No se permite la operación '{0}' ya que se van a aprovisionar máquinas virtuales de hello '{1}' con la imagen de hello '{2}'.  |
|  OperationNotAllowed  |  La operación '{0}' no se permite porque hello ScaleSet '{1}' de máquina Virtual está usando hello '{2}' de la imagen.  |
|  OperationNotAllowed  |  No se permite la operación '{0}' en la máquina virtual '{1}' desde Hola que máquina virtual está marcada para su eliminación. Sólo puede volver a intentar la operación de eliminación de hello (o esperar un toocomplete en curso de una).  |
|  OperationNotAllowed  |  La operación '{0}' no se permite en la máquina virtual '{1}' porque Hola VM está desasignada o está marcado toobe desasignado.  |
|  OperationNotAllowed  |  No se permite la operación '{0}' en la máquina virtual '{1}' desde Hola que VM se esté ejecutando. Póngase apagar explícitamente en caso de que apague Hola VM desde dentro de hello sistema operativo.  |
|  OperationNotAllowed  |  La operación '{0}' no se permite en la máquina virtual '{1}' desde la VM no se cancela la asignación de Hola.  |
|  OperationNotAllowed  |  La operación "{0}" no se permite en la máquina virtual "{1}" porque la extensión "{2}" de la misma está en estado de error.  |
|  OperationNotAllowed  |  La operación "{0}" no se permite en la máquina virtual "{1}", ya que hay otra operación en curso.  |
|  OperationNotAllowed  |  operación de Hello '{0}' requiere '{1}' toobe generalizado de hello Máquina Virtual.  |
|  OperationNotAllowed  |  operación de Hello requiere Hola VM toobe ejecutando (o establece toorun).  |
|  OperationNotAllowed  |  Disco con tamaño de {0} GB, que es más pequeño que Hola tamaño {1}GB del disco correspondiente en la imagen, no se permite.  |
|  OperationNotAllowed  |  Pueden agregarse extensiones del conjunto de escalado de VM del controlador '{0}' solo en el momento de Hola de creación de un conjunto de escala de máquinas virtuales.  |
|  OperationNotAllowed  |  Extensiones del conjunto de escalado de VM del controlador '{0}' se pueden eliminar solo en el momento de Hola de eliminación del conjunto de escala de máquinas virtuales.  |
|  OperationNotAllowed  |  La máquina virtual "{0}" ya usa discos administrados.  |
|  OperationNotAllowed  |  Máquina virtual '{0}' pertenece too'Classic' '{1}' del conjunto de disponibilidad. Disponibilidad de actualización de hello establezca toouse 'Aligned' SKU y, a continuación, vuelva a intentar Hola conversión.  |
|  OperationNotAllowed  |  La máquina virtual creada a partir de la imagen no puede tener discos basados en blobs. Todos los discos tienen discos toobe administrado.  |
|  OperationNotAllowed  |  Capturar no se puede completar la operación porque hello VM no es generalizada.  |
|  OperationNotAllowed  |  No se permiten las operaciones de administración en la máquina virtual '{0}' porque los discos de máquina virtual se va a convertir toomanaged discos.  |
|  OperationNotAllowed  |  Una operación en curso está cambiando el estado de energía de la máquina Virtual {0} too\ {1\\}. Realice la operación {2} después de un tiempo.  |
|  OperationNotAllowed  |  No se puede tooadd o actualización hello máquina virtual. Hola solicitado no estén disponibles en la unidad de asignación existente de Hola {0} de tamaño de máquina virtual. Para más información acerca de la estrategia de cambio de tamaño de máquinas virtuales, consulte https://aka.ms/azure-resizevm.  |
|  OperationNotAllowed  |  No se puede tooresize Hola VM porque Hola solicitado {0} de tamaño no está disponible en clúster Hola donde esté asignado actualmente conjunto de disponibilidad de Hola. Hola los tamaños disponibles son: {1}. Para más información acerca de la estrategia de cambio de tamaño de máquinas virtuales, consulte https://aka.ms/azure-resizevm.  |
|  OperationNotAllowed  |  No se puede tooresize Hola VM porque Hola solicitado {0} de tamaño no está disponible en clúster Hola donde hello VM está actualmente asignada. tooresize, cancelar la asignación de su too\ VM {1\\} (es decir, la operación de detención en hello portal de Azure) e inténtelo de nuevo la operación de cambio de tamaño de Hola. Para más información acerca de la estrategia de cambio de tamaño de máquinas virtuales, consulte https://aka.ms/azure-resizevm.  |
|  OSProvisioningClientError  |  Aprovisionamiento de SO no se pudo para máquina virtual '{0}' porque actualmente se está aprovisionando SO invitado de Hola.  |
|  OSProvisioningClientError  |  Error de aprovisionamiento de SO para la máquina virtual "{0}". Detalles del error: {1} Asegúrese de imagen de hello seguro se ha preparado correctamente (generalizado). <ul><li>Instrucciones para Windows: https://azure.microsoft.com/documentation/articles/virtual-machines-windows-upload-image/  </li></ul> |
|  OSProvisioningClientError  |  Error de generación de claves del host SSH. Detalles del error: {0}. tooresolve este problema, compruebe si el agente de Linux está configurado correctamente. <ul><li>Puede comprobar las instrucciones de hello en: https://azure.microsoft.com/documentation/articles/virtual-machines-linux-agent-user-guide/ </li></ul> |
|  OSProvisioningClientError  |  Nombre de usuario especificado para hello que VM no es válida para esta distribución de Linux. Detalles del error: {0}.  |
|  OSProvisioningInternalError  |  Aprovisionamiento de SO no se pudo para máquina virtual '{0}' debido a error interno de tooan.  |
|  OSProvisioningTimedOut  |  Aprovisionamiento de SO para la máquina virtual '{0}' no finalizó en hello asignada tiempo. Hola VM aún puede finalizar satisfactoriamente el aprovisionamiento. Compruebe el estado de aprovisionamiento posteriormente.  |
|  OSProvisioningTimedOut  |  Aprovisionamiento de SO para la máquina virtual '{0}' no finalizó en hello asignada tiempo. Hola VM aún puede finalizar satisfactoriamente el aprovisionamiento. Compruebe el estado de aprovisionamiento posteriormente. Asegúrese también de que se preparó correctamente imagen hello (generalizado).   <ul><li>Instrucciones para Windows: https://azure.microsoft.com/documentation/articles/virtual-machines-windows-upload-image/ </li><li> Instrucciones para Linux: https://azure.microsoft.com/documentation/articles/virtual-machines-linux-capture-image/</li></ul>  |
|  OSProvisioningTimedOut  |  Aprovisionamiento de SO para la máquina virtual '{0}' no finalizó en hello asignada tiempo. Sin embargo, el agente de Invitado VM de hello detectó ejecutando. Esto sugiere invitado hello no se estableció correctamente el sistema operativo preparado toobe utilizado como una imagen de máquina virtual (con CreateOption = FromImage). tooresolve este problema, cualquier Hola utilice VHD con CreateOption = adjuntar o prepararla correctamente para su uso como una imagen:   <ul><li>Instrucciones para Windows: https://azure.microsoft.com/documentation/articles/virtual-machines-windows-upload-image/ </li><li> Instrucciones para Linux: https://azure.microsoft.com/documentation/articles/virtual-machines-linux-capture-image/</li></ul>  |
|  OverConstrainedAllocationRequest  |  Hola necesario tamaño de máquina virtual no está disponible actualmente en la ubicación de hello seleccionado.  |
|  ResourceUpdateBlockedOnPlatformUpdate  |  No se puede actualizar el recurso en este momento debido tooongoing actualización de la plataforma. Inténtelo de nuevo más tarde.  |
|  StorageAccountLimitation  |  Cuenta de almacenamiento '{0}' no es compatible con blobs en páginas que son necesarios toocreate discos.  |
|  StorageAccountLimitation  |  La cuenta de almacenamiento "{0}" ha superado su cuota asignada.  |
|  StorageAccountLocationMismatch  |  No se pudo resolver la cuenta de almacenamiento "{0}". Asegúrese de que se creó mediante Hola proveedor de recursos de almacenamiento en hello mismo recurso de proceso de ubicación como Hola.  |
|  StorageAccountNotFound  |  No se encontró la cuenta de almacenamiento {0}. Asegúrese de cuenta de almacenamiento no se elimina y pertenece toohello misma ubicación como Hola VM de Azure.  |
|  StorageAccountNotRecognized  |  Use una cuenta de almacenamiento administrada por el proveedor de recursos de almacenamiento. El uso de "{0}" no se admite.  |
|  StorageAccountOperationInternalError  |  Error interno al obtener acceso a la cuenta de almacenamiento {0}.  |
|  StorageAccountSubscriptionMismatch  |  Cuenta de almacenamiento {0} no pertenece {1} toosubscription.  |
|  StorageAccountTooBusy  |  La cuenta de almacenamiento "{0}" está demasiado ocupada actualmente. Considere la posibilidad de usar otra cuenta.  |
|  StorageAccountTypeNotSupported  |  El disco {0} usa {1}, que es una cuenta de Blob Storage. Reinténtelo con una cuenta de Storage con fines generales.  |
|  StorageAccountTypeNotSupported  |  La cuenta de almacenamiento {0} es del tipo {1}. Diagnósticos de arranque admite {2} tipos de cuenta de almacenamiento.  |
|  SubscriptionNotAuthorizedForImage  |  suscripción de Hello no está autorizada.  |
|  TargetDiskBlobAlreadyExists  |  El blob {0} ya existe. Proporcione un toocreate URI de blob distinto de un disco de datos en blanco nueva '{1}'.  |
|  TargetDiskBlobAlreadyExists  |  Captura de operación no puede continuar porque ya existe {0} el blob de imagen de destino y blobs de disco duro virtual de hello marca toooverwrite no está establecida. Ya sea eliminar el blob de Hola o establecer marca de hello toooverwrite blobs de disco duro virtual y vuelva a intentar.  |
|  TargetDiskBlobAlreadyExists  |  La operación de captura no puede continuar porque el blob de imagen de destino {0} tiene una concesión activa.   |
|  TargetDiskBlobAlreadyExists  |  El blob {0} ya existe. Especifique un identificador URI de blob distinto como destino del disco "{1}".  |
|  TooManyVMRedeploymentRequests  |  Se recibieron demasiadas solicitudes de reimplementación para máquina virtual '{0}' o máquinas virtuales de hello en Hola mismo conjunto de disponibilidad con esta máquina virtual. Inténtelo de nuevo más tarde.  |
|  VHDSizeInvalid  |  Hola especifica el valor de tamaño de disco de {0} para el disco '{1}' con {2} de blob no es válido. El tamaño del disco estar entre {3} y {4}.  |
|  VMAgentStatusCommunicationError  |  La máquina virtual "{0}" no ha indicado el estado del agente o de las extensiones de máquina virtual. Compruebe Hola máquina virtual tiene un agente de máquina virtual en ejecución y puede establecer el almacenamiento de información de las conexiones salientes tooAzure.  |
|  VMArtifactRepositoryInternalError  |  Se produjo un error al comunicarse con los detalles del artefacto de hello artefacto repositorio tooretrieve máquina virtual.  |
|  VMArtifactRepositoryInternalError  |  Se produjo un error interno al recuperar datos del artefacto VM Hola del repositorio de artefactos de Hola.  |
|  VMExtensionHandlerNonTransientError  |  El controlador "{0}" informó de un error en la extensión de máquina virtual "{1}" con el código de error terminal "{2}" y el mensaje de error: "{3}"  |
|  VMExtensionManagementInternalError  |  Error interno al procesar la extensión de máquina virtual "{0}".  |
|  VMExtensionManagementInternalError  |  Se produjeron varios errores al preparar las extensiones de VM de Hola. Para más información, consulte la vista de instancia de extensión de máquina virtual.  |
|  VMExtensionProvisioningError  |  La máquina virtual indicó un error al procesar la extensión "{0}". Mensaje de error: "{1}".  |
|  VMExtensionProvisioningError  |  Varias extensiones de máquina virtual no pudo toobe aprovisionado en hello máquina virtual. Consulte la vista de instancia de extensión de máquina virtual de Hola para obtener más información.  |
|  VMExtensionProvisioningTimeout  |  Se ha agotado el tiempo de espera del aprovisionamiento de la extensión de máquina virtual "{0}". Puede que la instalación de la extensión esté tardando demasiado o que no se haya podido obtener el estado de la extensión.  |
|  VMMarketplaceInvalidInput  |  Crear una máquina virtual desde una imagen de Marketplace no no necesita información del Plan, quite Hola información del Plan en la solicitud de saludo. El nombre del disco de SO es {0}.  |
|  VMMarketplaceInvalidInput  |  información de compra de Hello no coincide. No se puede toodeploy desde una imagen de Marketplace Hola. El nombre del disco de SO es {0}.  |
|  VMMarketplaceInvalidInput  |  Crear una máquina virtual desde una imagen de Marketplace requiere información del Plan en la solicitud de saludo. El nombre del disco de SO es {0}.  |
|  VMNotFound  |  VM Hello '{0}' no se encuentra.  |
|  VMRedeploymentFailed  |  No se pudo volver a implementar máquina virtual '{0}' debido a error interno de tooan. Inténtelo de nuevo más tarde.  |
|  VMRedeploymentTimedOut  |  Nueva implementación de máquina virtual '{0}' no finalizó en hello asignada tiempo. Puede terminar correctamente en algún momento. En caso contrario, puede reintentar la solicitud de saludo.  |
|  VMStartTimedOut  |  Máquina virtual '{0}' no se inició en hello asignada tiempo. Hola VM pero aún puede iniciarse correctamente. Compruebe el estado de energía de hello más tarde.  |


## <a name="next-steps"></a>Pasos siguientes
Si necesita más ayuda, puede ponerse en contacto con hello Azure expertos en [Hola foros de Azure de MSDN y el desbordamiento de la pila](https://azure.microsoft.com/support/forums/). Como alternativa, puede registrar un incidente de soporte técnico de Azure. Vaya toohello [sitio de soporte técnico de Azure](https://azure.microsoft.com/support/options/) y seleccione **obtener admiten**.
