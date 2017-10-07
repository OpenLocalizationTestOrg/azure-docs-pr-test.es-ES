---
title: emulador de almacenamiento de Azure de hello aaaUse para desarrollo y pruebas | Documentos de Microsoft
description: "emulador de almacenamiento de Azure de Hello proporciona un entorno de desarrollo local disponible para desarrollar y probar las aplicaciones de almacenamiento de Azure. Obtenga información acerca de cómo se autentican las solicitudes, cómo tooconnect toohello emulador desde la aplicación y cómo toouse Hola herramienta de línea de comandos."
services: storage
documentationcenter: 
author: mmacy
manager: timlt
editor: tysonn
ms.assetid: f480b059-df8a-4a63-b05a-7f2f5d1f5c2a
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/08/2017
ms.author: marsma
ms.openlocfilehash: 42637dcd9f476069e6ecd19ed04e7ed93fe38ff7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-azure-storage-emulator-for-development-and-testing"></a>Usar el emulador de almacenamiento de Azure de Hola para desarrollo y pruebas

emulador de almacenamiento de Microsoft Azure Hola proporciona un entorno local que emula los servicios de Azure Blob, cola y tabla de Hola para fines de desarrollo. Mediante el emulador de almacenamiento de hello, puede probar la aplicación en servicios de almacenamiento de hello localmente, sin crear una suscripción de Azure o incurrir en los costos. Cuando esté satisfecho con cómo funciona la aplicación en el emulador de hello, puede cambiar una cuenta de almacenamiento de Azure en la nube de hello toousing.

## <a name="get-hello-storage-emulator"></a>Obtener el emulador de almacenamiento de Hola
Hello emulador de almacenamiento está disponible como parte del programa Hola a [SDK de Microsoft Azure](https://azure.microsoft.com/downloads/). También puede instalar el emulador de almacenamiento de hello mediante hello [instalador independiente de](https://go.microsoft.com/fwlink/?linkid=717179&clcid=0x409) (descarga directa). emulador de almacenamiento de tooinstall hello, debe tener privilegios administrativos en el equipo.

emulador de almacenamiento de Hello actualmente sólo se ejecuta en Windows. Para quienes estén pensando en un emulador de almacenamiento para Linux, una opción es la Comunidad de hello mantenida, emulador de almacenamiento de código abierto [Azurite](https://github.com/arafato/azurite).

> [!NOTE]
> Datos que se crean en una versión de emulador de almacenamiento de hello no está garantizados toobe accesible cuando se usa una versión diferente. Si necesita toopersist los datos para a largo plazo de hello, se recomienda que almacene esos datos en una cuenta de almacenamiento de Azure, en lugar de en el emulador de almacenamiento de Hola.
> <p/>
> emulador de almacenamiento de Hello depende de versiones específicas de las bibliotecas de OData de Hola. Reemplazar archivos DLL de OData de hello usa Hola emulador del almacenamiento de información con otras versiones no se admite y puede provocar un comportamiento inesperado. Sin embargo, cualquier versión de OData compatible con el servicio de almacenamiento de hello puede ser usado toosend solicitudes toohello emulador.
>

## <a name="how-hello-storage-emulator-works"></a>Cómo funciona el emulador de almacenamiento de Hola
emulador de almacenamiento de Hello usa una instancia local de Microsoft SQL Server y servicios de almacenamiento de Azure de tooemulate del sistema de archivos local de Hola. De forma predeterminada, el emulador de almacenamiento de hello utiliza una base de datos de Microsoft SQL Server 2012 Express LocalDB. Puede elegir tooconfigure Hola almacenamiento emulador tooaccess una instancia local de SQL Server en lugar de la instancia de LocalDB Hola. Para obtener más información, vea hello [inicio e inicialice Hola emulador de almacenamiento](#start-and-initialize-the-storage-emulator) sección más adelante en este artículo.

emulador de almacenamiento de Hello conecta tooSQL Server o LocalDB mediante la autenticación de Windows.

Existen algunas diferencias de funcionalidad entre el emulador de almacenamiento de Hola y servicios de almacenamiento de Azure. Para obtener más información sobre estas diferencias, vea hello [diferencias entre el emulador de almacenamiento de Hola y el almacenamiento de Azure](#differences-between-the-storage-emulator-and-azure-storage) sección más adelante en este artículo.

## <a name="start-and-initialize-hello-storage-emulator"></a>Iniciar e inicializar el emulador de almacenamiento de Hola
emulador de almacenamiento de Azure de Hola toostart:
1. Seleccione hello **iniciar** Hola o presionen **Windows** clave.
1. Comience a escribir `Azure Storage Emulator`.
1. Seleccione emulador de hello en lista de Hola de aplicaciones mostradas.

Cuando se inicia el emulador de almacenamiento de hello, aparecerá una ventana de símbolo del sistema. Puede utilizar esta consola ventana toostart y detener Hola emulador de almacenamiento, borrar los datos, obtener el estado e inicializar Hola emulador. Para obtener más información, vea hello [referencia de la herramienta de línea de comandos del emulador de almacenamiento](#storage-emulator-command-line-tool-reference) sección más adelante en este artículo.

Cuando se ejecuta el emulador de hello, verá un icono en el área de notificación de barra de tareas de Windows hello.

Cuando se cierra la ventana de símbolo del sistema del emulador de almacenamiento de hello, emulador de almacenamiento de hello seguirá toorun. toobring una ventana de consola del emulador de almacenamiento de Hola de nuevo, siga Hola pasos anteriores como si iniciar emulador de almacenamiento de Hola.

Hello primera vez que ejecuta el emulador de almacenamiento de hello, entorno de almacenamiento local de Hola se inicializa automáticamente. proceso de inicialización de Hello crea una base de datos en LocalDB y reserva puertos HTTP para cada servicio de almacenamiento local.

emulador de almacenamiento de Hola se instala de forma predeterminada demasiado`C:\Program Files (x86)\Microsoft SDKs\Azure\Storage Emulator`.

> [!TIP]
> Puede usar hello [Microsoft Azure Storage Explorer](http://storageexplorer.com) toowork con recursos de emulador de almacenamiento local. Busque "(desarrollo)" en "Cuentas de almacenamiento" en el árbol de recursos del explorador de almacenamiento de hello después de que se ha instalado e iniciado el emulador de almacenamiento de Hola.
>

### <a name="initialize-hello-storage-emulator-toouse-a-different-sql-database"></a>Inicializar Hola almacenamiento emulador toouse otra base de datos SQL
Puede utilizar Hola almacenamiento emulador herramienta de línea de comandos tooinitialize Hola almacenamiento emulador toopoint tooa SQL base de datos instancia distinta a instancia de LocalDB Hola predeterminada:

1. Ventana de consola de emulador de almacenamiento abierto Hola tal y como se describe en hello [inicio e inicialice Hola emulador de almacenamiento](#start-and-initialize-the-storage-emulator) sección.
1. En la ventana de la consola de hello, escriba Hola siguiente comando, donde `<SQLServerInstance>` es Hola nombre de instancia de SQL Server de Hola. toouse LocalDB, especifique `(localdb)\MSSQLLocalDb` como instancia de SQL Server de Hola.

  `AzureStorageEmulator.exe init /server <SQLServerInstance>`

  También puede usar Hola siguiente comando, que indica la instancia de SQL Server de hello emulador toouse Hola predeterminada:

  `AzureStorageEmulator.exe init /server .\\`

  O bien, puede usar Hola siguiente comando, que se reinicializa la instancia de LocalDB de hello base de datos toohello predeterminada:

  `AzureStorageEmulator.exe init /forceCreate`

Para más información sobre estos comandos, consulte la sección [Referencia de la herramienta de la línea de comandos del emulador de almacenamiento](#storage-emulator-command-line-tool-reference).

> [!TIP]
> Puede usar hello [Microsoft SQL Server Management Studio](/sql/ssms/download-sql-server-management-studio-ssms) toomanage (SSMS) instancias de SQL Server, incluida la instalación de LocalDB Hola. Hola SMSS **conectar tooServer** cuadro de diálogo, especifique `(localdb)\MSSQLLocalDb` en hello **nombre del servidor:** instancia del campo tooconnect toohello LocalDB.

## <a name="authenticating-requests-against-hello-storage-emulator"></a>Autenticar solicitudes en el emulador de almacenamiento de Hola
Una vez que haya instalado e iniciado el emulador de almacenamiento de hello, puede probar el código en él. Al igual que con el almacenamiento de Azure en la nube de hello, todas las solicitudes que realice en el emulador de almacenamiento de hello deben autenticarse, a menos que sea una solicitud anónima. Puede autenticar las solicitudes en el emulador de almacenamiento de hello mediante la autenticación de clave compartida o con una firma de acceso compartido (SAS).

### <a name="authenticate-with-shared-key-credentials"></a>Autenticación con credenciales de clave compartida
[!INCLUDE [storage-emulator-connection-string-include](../../includes/storage-emulator-connection-string-include.md)]

Para más información sobre las cadenas de conexión, consulte [Configuración de las cadenas de conexión de Azure Storage](storage-configure-connection-string.md).

### <a name="authenticate-with-a-shared-access-signature"></a>Autenticación con una firma de acceso compartido
Algunas bibliotecas de cliente de almacenamiento de Azure, como Xamarin hello, solo admiten la autenticación con un token de firma (SAS) de acceso compartido. Se puede crear el token SAS de hello mediante una herramienta como hello [Explorador de almacenamiento](http://storageexplorer.com/) u otra aplicación que admita la autenticación de clave compartida.

También puede generar un token de SAS mediante Azure PowerShell. Hello en el ejemplo siguiente se genera un token SAS con el contenedor de blobs de tooa todos los permisos:

1. Instalar Azure PowerShell si no lo ha hecho ya (versión más reciente de Hola de hello cmdlets de PowerShell de Azure se recomienda usar). Para ver las instrucciones de instalación, consulte [Instalación y configuración de Azure PowerShell](/powershell/azure/install-azurerm-ps).
2. Abrir Azure PowerShell y ejecute hello siga los comandos, reemplazando `ACCOUNT_NAME` y `ACCOUNT_KEY==` con sus propias credenciales, y `CONTAINER_NAME` con un nombre de su elección:

```powershell
$context = New-AzureStorageContext -StorageAccountName "ACCOUNT_NAME" -StorageAccountKey "ACCOUNT_KEY=="

New-AzureStorageContainer CONTAINER_NAME -Permission Off -Context $context

$now = Get-Date

New-AzureStorageContainerSASToken -Name CONTAINER_NAME -Permission rwdl -ExpiryTime $now.AddDays(1.0) -Context $context -FullUri
```

firma de acceso compartido resultante de Hello URI para el nuevo contenedor de hello debe ser similar al:

```
https://storageaccount.blob.core.windows.net/sascontainer?sv=2012-02-12&se=2015-07-08T00%3A12%3A08Z&sr=c&sp=wl&sig=t%2BbzU9%2B7ry4okULN9S0wst%2F8MCUhTjrHyV9rDNLSe8g%3Dsss
```

firma de acceso compartido de Hello creada con este ejemplo es válida durante un día. firma de Hello concede acceso completo (lectura, escritura, eliminación, lista) tooblobs dentro de contenedor de Hola.

Para más información sobre las firmas de acceso compartido, consulte [Uso de firmas de acceso compartido (SAS) en Azure Storage](storage-dotnet-shared-access-signature-part-1.md).

## <a name="addressing-resources-in-hello-storage-emulator"></a>Abordar los recursos en el emulador de almacenamiento de Hola
extremos de servicio de Hello para el emulador de almacenamiento de hello son diferentes de los de una cuenta de almacenamiento de Azure. diferencia de Hello es porque el equipo local de hello no realiza la resolución de nombres de dominio, que requieren direcciones locales del toobe de puntos de conexión de emulador de almacenamiento para hello.

Al direccionar un recurso en una cuenta de almacenamiento de Azure, use Hola después de esquema. nombre de la cuenta de Hello es parte del nombre de host URI de Hola y recurso de Hola que se redirige forma parte de ruta de acceso URI de hello:

`<http|https>://<account-name>.<service-name>.core.windows.net/<resource-path>`

Por ejemplo, hello siguiente URI es una dirección válida para un blob en una cuenta de almacenamiento de Azure:

`https://myaccount.blob.core.windows.net/mycontainer/myblob.txt`

Sin embargo, Hola emulador de almacenamiento, porque el equipo local de hello no lleva a cabo la resolución de nombres de dominio, nombre de la cuenta de hello forma parte de la ruta de acceso URI de hello en lugar del nombre de host de Hola. Usar hello siguiendo el formato URI para un recurso en el emulador de almacenamiento de hello:

`http://<local-machine-address>:<port>/<account-name>/<resource-path>`

Por ejemplo, hello dirección siguiente podría utilizarse para obtener acceso a un blob en el emulador de almacenamiento de hello:

`http://127.0.0.1:10000/myaccount/mycontainer/myblob.txt`

extremos de servicio de Hello para el emulador de almacenamiento de hello son:

* Blob service: `http://127.0.0.1:10000/<account-name>/<resource-path>`
* Queue service: `http://127.0.0.1:10001/<account-name>/<resource-path>`
* Table service: `http://127.0.0.1:10002/<account-name>/<resource-path>`

### <a name="addressing-hello-account-secondary-with-ra-grs"></a>Cuenta de hello direccionamiento secundaria con RA-GRS
A partir de la versión 3.1, emulador de almacenamiento de hello admite la replicación con redundancia geográfica con acceso de lectura (RA-GRS). Para los recursos de almacenamiento en nube de Hola y en un emulador local hello, puede tener acceso a ubicación secundaria Hola por anexar - nombre de la cuenta secundaria toohello. Por ejemplo, podría utilizarse Hola siguiente dirección para tener acceso a un blob usando secundaria de solo lectura de hello en el emulador de almacenamiento de hello:

`http://127.0.0.1:10000/myaccount-secondary/mycontainer/myblob.txt`

> [!NOTE]
> Para el acceso mediante programación toohello secundaria con el emulador de almacenamiento de hello, utilice Hola biblioteca cliente de almacenamiento para .NET versión 3.2 o posterior. Vea hello [biblioteca de cliente de almacenamiento de Microsoft Azure para .NET](https://msdn.microsoft.com/library/azure/dn261237.aspx) para obtener más información.
>
>

## <a name="storage-emulator-command-line-tool-reference"></a>Referencia de la herramienta de la línea de comandos del emulador de almacenamiento
A partir de la versión 3.0, se muestra una ventana de consola cuando se inicia Hola emulador de almacenamiento. Usar línea de comandos de hello en hello consola ventana toostart y detener Hola emulador, así como consultas de estado y realizar otras operaciones.

> [!NOTE]
> Si tienes Hola instalación del emulador de proceso de Microsoft Azure, aparece un icono de bandeja del sistema al iniciar Hola emulador de almacenamiento. Haga doble clic en hello icono tooreveal un menú que proporciona una manera gráfica toostart y detener Hola emulador de almacenamiento.
>
>

### <a name="command-line-syntax"></a>Sintaxis de la línea de comandos
`AzureStorageEmulator.exe [start] [stop] [status] [clear] [init] [help]`

### <a name="options"></a>Opciones
lista de hello tooview de opciones, tipo `/help` en línea de comandos de Hola.

| Opción | Description | Comando | Argumentos |
| --- | --- | --- | --- |
| **Iniciar** |Se inicia el emulador de almacenamiento de Hola. |`AzureStorageEmulator.exe start [-inprocess]` |*-inprocess*: iniciar el emulador de hello en el proceso actual de hello en lugar de crear un nuevo proceso. |
| **Detención** |Emulador de almacenamiento de Hola se detiene. |`AzureStorageEmulator.exe stop` | |
| **Estado** |Imprime Hola estado Hola del emulador de almacenamiento. |`AzureStorageEmulator.exe status` | |
| **Borrar** |Borra los datos de hello en todos los servicios especificados en la línea de comandos de Hola. |`AzureStorageEmulator.exe clear [blob] [table] [queue] [all]                                                    ` |*blob*: borra datos del blob. <br/>*queue*: borra datos de cola. <br/>*table*: borra datos de tabla. <br/>*all*: borra todos los datos de todos los servicios. |
| **Init** |Realiza una inicialización tooset emulador Hola. |<code>AzureStorageEmulator.exe init [-server serverName] [-sqlinstance instanceName] [-forcecreate&#124;-skipcreate] [-reserveports&#124;-unreserveports] [-inprocess]</code> |*-nombreDeServidor ombreDeInstancia server*: especifica el servidor hello hospeda la instancia de SQL Hola. <br/>*-sqlinstance nombreDeInstancia*: especifica el nombre de Hola de hello SQL instancia toobe utilizado en la instancia predeterminada del servidor de Hola. <br/>*-forcecreate*: fuerza la creación de base de datos SQL de hello, incluso si ya existe. <br/>*-skipcreate*: omite la creación de la base de datos SQL de Hola. Esto tiene prioridad sobre -forcecreate.<br/>*-reserveports*: intentos de puertos de hello HTTP tooreserve asociados con los servicios de Hola.<br/>*-unreserveports*: intenta tooremove reservas para los puertos de hello HTTP asociados con los servicios de Hola. Esto tiene prioridad sobre -reserveports.<br/>*-inprocess*: realiza la inicialización en el proceso actual de hello en lugar de abrir un nuevo proceso. proceso actual de Hello debe iniciarse con permisos elevados si cambiar las reservas de puerto. |

## <a name="differences-between-hello-storage-emulator-and-azure-storage"></a>Diferencias entre el emulador de almacenamiento de Hola y el almacenamiento de Azure
Dado que el emulador de almacenamiento de hello es un entorno emulado que se ejecuta en una instancia local de SQL, existen diferencias de funcionalidad entre el emulador de hello y una cuenta de almacenamiento de Azure en la nube de hello:

* emulador de almacenamiento de Hello admite solo una cuenta única fija y una clave de autenticación conocido.
* emulador de almacenamiento de Hello no es un servicio de almacenamiento escalable y no admite un gran número de usuarios simultáneos.
* Como se describe en [abordar los recursos en el emulador de almacenamiento de hello](#addressing-resources-in-the-storage-emulator), recursos se tratan de forma diferente en el emulador de almacenamiento de hello frente a una cuenta de almacenamiento de Azure. Esta diferencia es porque la resolución de nombres de dominio está disponible en la nube de hello pero no en equipo local de Hola.
* A partir de la versión 3.1, cuenta del emulador de almacenamiento Hola admite replicación con redundancia geográfica con acceso de lectura (RA-GRS). En el emulador de Windows hello, todas las cuentas tienen RA-GRS habilitada y nunca hay ningún retraso entre réplicas principales y secundarias de Hola. Hola obtener estadísticas del servicio Blob obtener estadísticas del servicio cola, operaciones y obtener estadísticas del servicio tabla son compatibles con la cuenta de hello secundaria y siempre devolverá el valor de Hola de hello `LastSyncTime` elemento de respuesta como Hola subyacente de actual tiempo toohello correspondiente Base de datos SQL.
* Hola servicio de archivos y los extremos del servicio de protocolo SMB no se admiten actualmente en el emulador de almacenamiento de Hola.
* Si usa una versión de servicios de almacenamiento de Hola que todavía no se admite con el emulador de hello, emulador de almacenamiento de hello devuelve un error de VersionNotSupportedByEmulator (código de estado HTTP 400 - Solicitud incorrecta).

### <a name="differences-for-blob-storage"></a>Diferencias en el almacenamiento de blobs
Hola siguiendo las diferencias aplica tooBlob almacenamiento en el emulador de hello:

* emulador de almacenamiento de Hello solo admite tamaños de blob too2 GB.
* Copia incremental permite que las instantáneas de blobs sobrescribe toobe copiados, y que devuelva un error en el servicio de Hola.
* Get Page Ranges Diff no funciona entre instantáneas copiadas con el blob de copia incremental.
* Una operación Put Blob puede realizarse correctamente con un blob que resida en el emulador de almacenamiento de hello con una concesión activa, incluso si no se ha especificado el identificador de concesión de hello en solicitud de Hola.
* Anexar Blob no se admiten las operaciones de emulador de Hola. Intentando realizar una operación en un blob en anexos, devuelve un error FeatureNotSupportedByEmulator (código de estado HTTP 400 - Solicitud incorrecta).

### <a name="differences-for-table-storage"></a>Diferencias en el almacenamiento de tabla
Hola siguiendo las diferencias aplica tooTable almacenamiento en el emulador de hello:

* Propiedades de fecha en el servicio de tabla en el emulador de almacenamiento de Hola Hola soportar solo amplia gama de hello compatible con SQL Server 2005 (son necesaria toobe a más tardar el 1 de enero de 1753). Se cambian todas las fechas anteriores al 1 de enero de 1753 toothis valor. precisión de las fechas Hello es precisión toohello limitada de SQL Server 2005, lo que significa que las fechas son precisas too1/300 de segundo.
* emulador de almacenamiento de Hello es compatible con los valores de propiedad de clave de partición clave y fila de menos de 512 bytes. Además, tamaño total de Hola de nombre de la cuenta de hello, nombre de la tabla y nombres de propiedad de clave juntos no puede superar 900 bytes.
* tamaño total de Hola de una fila de una tabla en el emulador de almacenamiento de hello es limitada que no requiere herramientas de 1 MB.
* En el emulador de almacenamiento de hello, propiedades de datos, escriba `Edm.Guid` o `Edm.Binary` compatibilidad solo Hola `Equal (eq)` y `NotEqual (ne)` cadenas de filtro de operadores de comparación en consultas.

### <a name="differences-for-queue-storage"></a>Diferencias en el almacenamiento de cola
No hay ningún almacenamiento tooQueue específicos de las diferencias en el emulador de Hola.

## <a name="storage-emulator-release-notes"></a>Notas de la versión del emulador de almacenamiento
### <a name="version-52"></a>Versión 5.2
* emulador de almacenamiento de Hello ahora admite la versión de 2017-04-17 de servicios de almacenamiento de hello en los extremos de servicio Blob, cola y tabla.
* Se ha corregido un error por el que no se codificaban correctamente los valores de propiedad de tabla.

### <a name="version-51"></a>Versión 5.1
* Se ha corregido un error donde emulador de almacenamiento de hello devolvía hello `DataServiceVersion` encabezado en algunas respuestas donde hello el servicio no está.

### <a name="version-50"></a>Versión 5.0
* instalador de emulador de almacenamiento de Hello ya no comprueba MSSQL existente e instala .NET Framework.
* instalador de emulador de almacenamiento de Hello ya no crea la base de datos de hello como parte de la instalación. Se seguirá creando la base de datos si se necesita como parte del proceso de inicio.
* La creación de la base de datos ya no requiere elevación.
* Las reservas de puertos ya no son necesarias para el inicio.
* Agrega las siguientes opciones demasiado de hello`init`: `-reserveports` (requiere elevación), `-unreserveports` (requiere elevación), `-skipcreate`.
* Hola la opción de IU del emulador en el icono de bandeja del sistema de hello ahora inicia la interfaz de línea de comandos de Hola. Hola antigua interfaz gráfica de usuario ya no está disponible.
* Algunos archivos DLL se han quitado o se han cambiado de nombre.

### <a name="version-46"></a>Versión 4.6
* emulador de almacenamiento de Hello ahora admite la versión 2016-05-31 de servicios de almacenamiento de hello en los extremos de servicio Blob, cola y tabla.

### <a name="version-45"></a>Versión 4.5
* Se ha corregido un error que provocó la inicialización y la instalación de toofail de emulador de almacenamiento de hello cuando se cambia el nombre hello realizar una copia de la base de datos.

### <a name="version-44"></a>Version 4.4
* emulador de almacenamiento de Hello ahora admite la versión 2015-12-11 de servicios de almacenamiento de hello en los extremos de servicio Blob, cola y tabla.
* Hello recolección del emulador de almacenamiento de datos blob es ahora más eficaz cuando se trabaja con un gran número de blobs.
* Se ha corregido un error que provocó el contenedor toobe de ACL XML que se validen de forma ligeramente diferente de cómo lo hace el servicio de almacenamiento de Hola.
* Se ha corregido un error que se produce a veces máx. y toobe de valores de fecha y hora de min notifica en la zona horaria incorrecta de Hola.

### <a name="version-43"></a>Versión 4.3
* emulador de almacenamiento de Hello ahora admite la versión 2015-07-08 de servicios de almacenamiento de hello en los extremos de servicio Blob, cola y tabla.

### <a name="version-42"></a>Versión 4.2
* emulador de almacenamiento de Hello ahora admite la versión 2015-04-05 de servicios de almacenamiento de hello en los extremos de servicio Blob, cola y tabla.

### <a name="version-41"></a>Versión 4.1
* emulador de almacenamiento de Hello ahora admite la versión 2015-02-21 de servicios de almacenamiento de hello en los extremos de servicio Blob, cola y tabla, excepto las nuevas características de anexar Blob Hola.
* Si usa una versión de servicios de almacenamiento de Hola que todavía no se admite con el emulador de hello, emulador Hola devuelve un mensaje de error significativo. Se recomienda utilizar la versión más reciente de Hola de emulador de Hola. Si se produce un error de VersionNotSupportedByEmulator (código de estado HTTP 400 - Solicitud incorrecta), descargue la versión más reciente de Hola Hola del emulador de almacenamiento.
* Se corrige un error en el que una carrera provocada tabla entidad datos toobe incorrecta durante las operaciones de mezcla simultáneos.

### <a name="version-40"></a>Versión 4.0
* emulador de almacenamiento de Hello ejecutable ha cambiado de nombre demasiado*AzureStorageEmulator.exe*.

### <a name="version-32"></a>Versión 3.2
* emulador de almacenamiento de Hello ahora admite la versión 2014-02-14 de servicios de almacenamiento de hello en los extremos de servicio Blob, cola y tabla. Los extremos de servicio de archivos no se admiten actualmente en el emulador de almacenamiento de Hola. Vea [control de versiones para servicios de almacenamiento de Azure hello](/rest/api/storageservices/Versioning-for-the-Azure-Storage-Services) para obtener más información acerca de la versión 2014-02-14.

### <a name="version-31"></a>Versión 3.1
* Almacenamiento con redundancia geográfica con acceso de lectura (RA-GRS) ahora es compatible con el emulador de almacenamiento de Hola. Estadísticas del servicio Blob Hola obtener, obtener estadísticas del servicio cola y obtener las API de estadísticas de servicio de tabla son compatibles con la cuenta de hello secundaria y siempre devolverá el valor de Hola de elemento de respuesta de hello LastSyncTime como Hola actual toohello correspondiente de tiempo subyacente SQL base de datos. Para el acceso mediante programación toohello secundaria con el emulador de almacenamiento de hello, utilice Hola biblioteca cliente de almacenamiento para .NET versión 3.2 o posterior. Para obtener más información, vea Hola biblioteca de cliente de almacenamiento de Microsoft Azure para .NET Reference.

### <a name="version-30"></a>Versión 3.0
* emulador de almacenamiento de Azure Hola ya no se incluye en hello mismo empaquetar como emulador de proceso de Hola.
* interfaz de usuario gráfica del emulador de almacenamiento de Hello está en desuso en favor de una interfaz de línea de comandos que permiten ejecutar scripts. Para obtener detalles sobre la interfaz de línea de comandos de hello, consulte referencia emulador de almacenamiento de la herramienta de línea de comandos. interfaz gráfica de Hello seguirán toobe presente en la versión 3.0, pero solo puede obtenerse cuando se instala Hola emulador de proceso, haga doble clic en el icono de bandeja del sistema de Hola y seleccione Mostrar IU del emulador de almacenamiento.
* La versión 2013-08-15 de servicios de almacenamiento de Azure Hola ahora es totalmente compatible. (Anteriormente esta versión solo era compatible con versión la versión 2.2.1 Preview del emulador de almacenamiento.)

## <a name="next-steps"></a>Pasos siguientes

* Evaluar el emulador de almacenamiento entre plataformas, mantiene a la Comunidad de código abierto de hello [Azurite](https://github.com/arafato/azurite). 
* [Ejemplos de almacenamiento de Azure mediante .NET](storage-samples-dotnet.md) contiene ejemplos de código de tooseveral vínculos puede usar al desarrollar la aplicación.
* Puede usar hello [Microsoft Azure Storage Explorer](http://storageexplorer.com) toowork con recursos en la nube de la cuenta de almacenamiento y en el emulador de almacenamiento de Hola.
