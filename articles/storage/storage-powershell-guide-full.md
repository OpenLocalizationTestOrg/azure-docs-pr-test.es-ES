---
title: aaaUsing PowerShell de Azure con el almacenamiento de Azure | Documentos de Microsoft
description: "Obtenga información acerca de cómo toouse Hola cmdlets de PowerShell de Azure para el almacenamiento de Azure toocreate y administrar las cuentas de almacenamiento; trabajar con blobs, tablas, colas y archivos; Configurar análisis de almacenamiento de la consulta y crear firmas de acceso compartido."
services: storage
documentationcenter: na
author: robinsh
manager: timlt
ms.assetid: f4704f58-abc6-4f89-8b6d-1b1659746f5a
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/03/2017
ms.author: robinsh
ms.openlocfilehash: befe7adda2384f8bcdb8b9f1a063e4eafc158271
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="using-azure-powershell-with-azure-storage"></a>Usar Azure PowerShell con Almacenamiento de Azure
## <a name="overview"></a>Información general
Azure PowerShell es un módulo que proporciona cmdlets toomanage Azure a través de Windows PowerShell. Es un Shell de línea de comandos y un lenguaje de scripting basados en tareas y diseñados especialmente para la administración del sistema. Fácilmente con PowerShell, puede controlar y automatizar la administración de Hola de sus aplicaciones y servicios de Azure. Por ejemplo, puede usar Hola cmdlets tooperform Hola mismo las tareas que puede realizar a través de hello [portal de Azure](https://portal.azure.com).

En esta guía, exploraremos cómo hello toouse [Cmdlets de almacenamiento de Azure](/powershell/module/azurerm.storage/#storage) tooperform una serie de tareas de desarrollo y la administración con el almacenamiento de Azure.

En esta guía se considera que ya tiene experiencia previa en el uso de [Azure Storage](https://azure.microsoft.com/documentation/services/storage/) y [Windows PowerShell](http://technet.microsoft.com/library/bb978526.aspx). Guía de Hola proporciona a una serie de secuencias de comandos de uso de hello toodemonstrate de PowerShell con el almacenamiento de Azure. Debe actualizar las variables de script de Hola según la configuración antes de ejecutar cada script.

Hola primera sección de esta guía proporciona una vista rápida en el almacenamiento de Azure y PowerShell. Para obtener información detallada e instrucciones, iniciar desde hello [requisitos previos para usar PowerShell de Azure con el almacenamiento de Azure](#prerequisites-for-using-azure-powershell-with-azure-storage).

## <a name="getting-started-with-azure-storage-and-powershell-in-5-minutes"></a>Introducción de 5 minutos a Almacenamiento de Azure y PowerShell
Esta sección muestra cómo tooaccess el almacenamiento de Azure a través de PowerShell en 5 minutos.

**Nueva tooAzure:** obtener una suscripción de Microsoft Azure y una cuenta de Microsoft asociadas a esa suscripción. Para más información sobre las opciones de compra de Azure, consulte [Evaluación gratuita](https://azure.microsoft.com/pricing/free-trial/), [Opciones de compra](https://azure.microsoft.com/pricing/purchase-options/) y [Ofertas para miembros](https://azure.microsoft.com/pricing/member-offers/) (para miembros de MSDN, Microsoft Partner Network, BizSpark y otros programas de Microsoft).

Para obtener más información sobre las suscripciones a Azure, consulte [Asignación de roles de administrador en Azure Active Directory (Azure AD)](https://msdn.microsoft.com/library/azure/hh531793.aspx) .

**Después de crear una suscripción y una cuenta de Microsoft Azure:**

1. Descargue e instale hello más reciente [Azure PowerShell](https://github.com/Azure/azure-powershell/releases/latest).
2. Iniciar Windows PowerShell Integrated Scripting Environment (ISE): En el equipo local, vaya toohello **iniciar** menú. Tipo de **herramientas administrativas** y haga clic en toorun se. Hola **herramientas administrativas** ventana, haga clic en **Windows PowerShell ISE**, haga clic en **ejecutar como administrador**.
3. En **Windows PowerShell ISE**, haga clic en **archivo** > **New** toocreate un nuevo archivo de script.
4. Ahora, le ofreceremos una secuencia de comandos simple que muestra básica tooaccess de comandos de PowerShell almacenamiento de Azure. script de Hola primero le preguntará la tooadd de las credenciales de cuenta de Azure el entorno de PowerShell local toohello de cuenta de Azure. A continuación, el script de Hola establezca el valor predeterminado de hello suscripción de Azure y crear una nueva cuenta de almacenamiento de Azure. A continuación, el script de Hola creará un nuevo contenedor en esta nueva cuenta de almacenamiento y cargar un contenedor de toothat de archivo (blob) de imagen existente. Después de script de Hola enumera todos los blobs en ese contenedor, creará un nuevo directorio de destino en el equipo local y descargar el archivo de imagen de Hola.
5. Hola pasos de la sección de código, seleccione el script de Hola entre comentarios de Hola **#begin** y **#end**. Presione CTRL + C toocopy se toohello Portapapeles.

    ```powershell
    # begin
    # Update with hello name of your subscription.
    $SubscriptionName = "YourSubscriptionName"
       
    # Give a name tooyour new storage account. It must be lowercase!
    $StorageAccountName = "yourstorageaccountname"
       
    # Choose "West US" as an example.
    $Location = "West US"
       
    # Give a name tooyour new container.
    $ContainerName = "imagecontainer"
       
    # Have an image file and a source directory in your local computer.
    $ImageToUpload = "C:\Images\HelloWorld.png"
       
    # A destination directory in your local computer.
    $DestinationFolder = "C:\DownloadImages"
       
    # Add your Azure account toohello local PowerShell environment.
    Add-AzureAccount
       
    # Set a default Azure subscription.
    Select-AzureSubscription -SubscriptionName $SubscriptionName –Default
       
    # Create a new storage account.
    New-AzureStorageAccount –StorageAccountName $StorageAccountName -Location $Location
       
    # Set a default storage account.
    Set-AzureSubscription -CurrentStorageAccountName $StorageAccountName -SubscriptionName $SubscriptionName
       
    # Create a new container.
    New-AzureStorageContainer -Name $ContainerName -Permission Off
       
    # Upload a blob into a container.
    Set-AzureStorageBlobContent -Container $ContainerName -File $ImageToUpload
       
    # List all blobs in a container.
    Get-AzureStorageBlob -Container $ContainerName
       
    # Download blobs from hello container:
    # Get a reference tooa list of all blobs in a container.
    $blobs = Get-AzureStorageBlob -Container $ContainerName
       
    # Create hello destination directory.
    New-Item -Path $DestinationFolder -ItemType Directory -Force  
       
    # Download blobs into hello local destination directory.
    $blobs | Get-AzureStorageBlobContent –Destination $DestinationFolder
       
    # end
    ```

6. En **Windows PowerShell ISE**, presione script de Hola toocopy CTRL+V. Haga clic en **archivo** > **Guardar**. Hola **Guardar como** cuadro de diálogo, escriba un nombre Hola Hola del archivo de script, como "mystoragescript." Haga clic en **Guardar**.
7. Ahora, necesita las variables de script de Hola tooupdate basadas en las opciones de configuración. Debe actualizar hello **$SubscriptionName** variable con su propia suscripción. Puede mantener Hola otras variables como se especifica en el script de Hola o actualizarlos como desee.
   
   * **$SubscriptionName:** debe actualizar esta variable con su propia suscripción. Siga uno de hello después de tres maneras toolocate Hola nombre de la suscripción:
     
    a. En **Windows PowerShell ISE**, haga clic en **archivo** > **New** toocreate un nuevo archivo de script. Siguiente de hello copia toohello nuevo archivo de script de secuencia de comandos y haga clic en **depurar** > **ejecutar**. Hello script siguiente solicitar su entorno de PowerShell local de cuenta de Azure toohello su tooadd de credenciales de cuenta de Azure y, a continuación, muestra todas las suscripciones de Hola que están conectados toohello sesión de PowerShell local. Tome nota del nombre de Hola de suscripción de Hola que desea toouse mientras sigue este tutorial:
     
    ```powershell
    Add-AzureAccount 
      Get-AzureSubscription | Format-Table SubscriptionName, IsDefault, IsCurrent, CurrentStorageAccountName
    ```

    b. toolocate y copiar nombre de la suscripción en hello [portal de Azure](https://portal.azure.com), en el menú del concentrador en hello deja de Hola, haga clic en **suscripciones**. Copiar nombre Hola de suscripción que desea toouse durante la ejecución de secuencias de comandos de hello en esta guía.
     
     ![Azure Portal](./media/storage-powershell-guide-full/Subscription_Previewportal.png)

    c. toolocate y copiar nombre de la suscripción en hello [Portal clásico de Azure](https://manage.windowsazure.com/), desplácese hacia abajo y haga clic en **configuración** en hello izquierda del portal de Hola. Haga clic en **suscripciones** toosee una lista de las suscripciones. Copiar nombre Hola de suscripción que desee toouse mientras se ejecuta scripts Hola proporcionados en esta guía.
     
     ![Portal de Azure clásico](./media/storage-powershell-guide-full/Subscription_currentportal.png)

   * **$StorageAccountName:** usar hello según el nombre de script de Hola o escriba un nombre nuevo para la cuenta de almacenamiento. **Importante:** Hola nombre de cuenta de almacenamiento de hello debe ser único en Azure. También debe estar en minúscula.
   * **$Location:** usar Hola dado "West US" en el script de Hola o elegir otras ubicaciones de Azure, como este de EE., Europa del Norte y así sucesivamente.
   * **$ContainerName:** usar hello según el nombre de script de Hola o escriba un nombre nuevo para el contenedor.
   * **$ImageToUpload:** escriba una imagen de tooa de ruta de acceso en el equipo local, como por ejemplo: "C:\Images\HelloWorld.png".
   * **$DestinationFolder:** ENTRAR archivos toostore en el directorio local de tooa de una ruta de acceso se descargan desde el almacenamiento de Azure, como: "C:\DownloadImages".
8. Después de actualizar las variables de script de hello en el archivo de "mystoragescript.ps1" hello, haga clic en **archivo** > **guardar**. A continuación, haga clic en **depurar** > **ejecutar** o presione **F5** secuencia de comandos de toorun Hola.  

Después de ejecutar el script de Hola, debe tener una carpeta de destino local que incluye el archivo de imagen de hello descargado. Hola siguiente captura de pantalla muestra una salida de ejemplo:

![blobs](./media/storage-powershell-guide-full/Blobdownload.png)

> [!NOTE]
> Hello "Introducción a almacenamiento de Azure y PowerShell en 5 minutos" sección proporciona una introducción rápida acerca de cómo toouse PowerShell de Azure con el almacenamiento de Azure. Para obtener información detallada e instrucciones, le recomendamos hello tooread las secciones siguientes.
> 

## <a name="prerequisites-for-using-azure-powershell-with-azure-storage"></a>requisitos previos para usar Azure PowerShell con Almacenamiento de Azure
Necesita una suscripción y cuenta toorun Hola cmdlets de Azure PowerShell proporcionado en esta guía, como se describió anteriormente.

Azure PowerShell es un módulo que proporciona cmdlets toomanage Azure a través de Windows PowerShell. Para obtener información sobre cómo instalar y configurar Azure PowerShell, consulte [cómo tooinstall y configurar Azure PowerShell](/powershell/azure/overview). Se recomienda descargar e instalar o actualizar toohello última versión del módulo Azure PowerShell antes de utilizar a esta guía.

Puede ejecutar los cmdlets de hello en la consola de Windows PowerShell estándar de Hola o hello Windows PowerShell Integrated Scripting Environment (ISE). Por ejemplo, tooopen **Windows PowerShell ISE**, vaya el menú de inicio de toohello, escriba herramientas administrativas y haga clic en toorun se. En la ventana de herramientas administrativas de hello, haga clic en Windows PowerShell ISE, haga clic en Ejecutar como administrador.

## <a name="how-toomanage-storage-accounts-in-azure"></a>Cómo las cuentas de almacenamiento de toomanage en Azure

Veamos la administración de cuentas de almacenamiento en Azure con PowerShell.

### <a name="how-tooset-a-default-azure-subscription"></a>¿Cómo tooset un suscripción de Azure predeterminado
toomanage almacenamiento de Azure con Azure PowerShell, necesita tooauthenticate el entorno de cliente con Azure a través de la autenticación de Azure Active Directory o la autenticación basada en certificados. Para obtener información detallada, vea [cómo tooinstall y configurar Azure PowerShell](/powershell/azure/overview) tutorial. Esta guía usa la autenticación de Azure Active Directory Hola.

1. En Windows PowerShell ISE, escriba Hola después tooadd de comando su entorno de PowerShell local de cuenta de Azure toohello:

    ```powershell
    Add-AzureAccount
    ```

2. En la ventana de "Iniciar sesión en Azure tooMicrosoft" hello, dirección de correo electrónico de tipo hello y contraseña asociada a su cuenta. Azure autentica y guarda la información de credenciales de hello y, a continuación, cierra la ventana hello.

3. A continuación, ejecute hello después comando tooview hello Azure cuentas en su entorno de PowerShell local y compruebe que aparece la cuenta:
   
    ```powershell
    Get-AzureAccount
    ```
4. A continuación, ejecute hello siguiente cmdlet tooview todas las suscripciones de Hola que están conectados toohello sesión de PowerShell local y compruebe que aparece su suscripción:

    ```powershell
    Get-AzureSubscription | Format-Table SubscriptionName, IsDefault, IsCurrent, CurrentStorageAccountName`
    ```
5. tooset una suscripción de Azure, de forma predeterminada al ejecutar el cmdlet Select-AzureSubscription hello:

    ```powershell
    $SubscriptionName = 'Your subscription Name'
    Select-AzureSubscription -SubscriptionName $SubscriptionName –Default
    ```

6. Comprobar nombre de Hola de suscripción de hello predeterminada mediante la ejecución del cmdlet Get-AzureSubscription hello:

    ```powershell
    Get-AzureSubscription -Default
    ```

7. toosee todos los cmdlets de PowerShell disponibles hello para el almacenamiento de Azure, ejecute:
    
    ```powershell
    Get-Command -Module Azure -Noun *Storage*`
    ```

### <a name="how-toocreate-a-new-azure-storage-account"></a>¿Cómo toocreate una nueva cuenta de almacenamiento de Azure
toouse almacenamiento de Azure, necesitará una cuenta de almacenamiento. Puede crear una nueva cuenta de almacenamiento de Azure después de haber configurado la suscripción de tooyour tooconnect de equipo.

1. Ejecutar toofind de cmdlet Get-AzureLocation Hola Hola todas las ubicaciones de centro de datos disponibles:

    ```powershell
    Get-AzureLocation | Format-Table -Property Name, AvailableServices, StorageAccountTypes
    ```

2. A continuación, ejecute hello AzureStorageAccount nuevo cmdlet toocreate una nueva cuenta de almacenamiento. Hello en el ejemplo siguiente se crea una nueva cuenta de almacenamiento en el centro de datos de Hola "West US".
   
    ```powershell
    $location = "West US"
    $StorageAccountName = "yourstorageaccount"
    New-AzureStorageAccount –StorageAccountName $StorageAccountName -Location $location
    ```

> [!IMPORTANT]
> nombre de Hello de la cuenta de almacenamiento debe ser único dentro de Azure y debe estar en minúscula. Para las convenciones de nomenclatura y otras restricciones, consulte [Acerca de las cuentas de Azure Storage](storage-create-storage-account.md) y [Convenciones de nomenclatura y referencia de contenedores, blobs y metadatos](http://msdn.microsoft.com/library/azure/dd135715.aspx).
> 
> 

### <a name="how-tooset-a-default-azure-storage-account"></a>¿Cómo tooset una cuenta de almacenamiento de Azure de forma predeterminada
Puede tener varias cuentas de almacenamiento en su suscripción. Puede elegir uno de ellos y establézcalo como cuenta de almacenamiento predeterminada de Hola para almacenamiento Hola a todos los comandos de hello misma sesión de PowerShell. Esto le permite comandos de almacenamiento de Azure PowerShell de hello toorun sin especificar explícitamente el contexto de almacenamiento de Hola.

1. tooset una cuenta de almacenamiento predeterminada para su suscripción, puede ejecutar el cmdlet Set-AzureSubscription de Hola.

    ```powershell
    $SubscriptionName = "Your subscription name"
    $StorageAccountName = "yourstorageaccount"  
    Set-AzureSubscription -CurrentStorageAccountName $StorageAccountName -SubscriptionName $SubscriptionName
    ```

2. A continuación, ejecute Get-AzureSubscription Hola cmdlet tooverify que cuenta de almacenamiento de hello está asociado a su cuenta de suscripción de manera predeterminada. Este comando devuelve las propiedades de suscripción de Hola de suscripción actual Hola incluida su cuenta de almacenamiento actual.

    ```powershell
    Get-AzureSubscription –Current
    ```

### <a name="how-toolist-all-azure-storage-accounts-in-a-subscription"></a>Cómo toolist cuentas de todo el almacenamiento de Azure en una suscripción
Cada suscripción de Azure puede tener hasta too100 cuentas de almacenamiento. Para hello información más actualizada acerca de los límites, consulte [suscripción de Azure y límites de servicio, cuotas y restricciones](../azure-subscription-service-limits.md).

Ejecute hello después toofind cmdlet out Hola nombre y el estado de las cuentas de almacenamiento de hello en la suscripción actual de hello:

```powershell
Get-AzureStorageAccount | Format-Table -Property StorageAccountName, Location, AccountType, StorageAccountStatus
```

### <a name="how-toocreate-an-azure-storage-context"></a>¿Cómo toocreate un contexto de almacenamiento de Azure
Contexto de almacenamiento de Azure es un objeto de credenciales de almacenamiento de PowerShell tooencapsulate Hola. Usando un contexto de almacenamiento durante la ejecución de cualquier cmdlet posterior permite tooauthenticate la solicitud sin especificar cuenta de almacenamiento de Hola y su clave de acceso explícitamente. Puede crear un contexto de almacenamiento de muchas formas; por ejemplo, mediante el uso de la clave de acceso y el nombre de la cuenta de almacenamiento, el token de firma de acceso compartido (SAS), la cadena de conexión o de forma anónima. Para obtener más información, consulte [New-AzureStorageContext](/powershell/module/azure.storage/new-azurestoragecontext).  

Use uno de hello después toocreate de tres maneras un contexto de almacenamiento:

* Ejecute hello [AzureStorageKey Get](/powershell/module/azure.storage/get-azurestoragekey) toofind cmdlet out clave de acceso de almacenamiento principal de Hola para su cuenta de almacenamiento de Azure. A continuación, llame a hello [AzureStorageContext New](/powershell/module/azure.storage/new-azurestoragecontext) cmdlet toocreate un contexto de almacenamiento:

    ```powershell
    $StorageAccountName = "yourstorageaccount"
    $StorageAccountKey = Get-AzureStorageKey -StorageAccountName $StorageAccountName
    $Ctx = New-AzureStorageContext $StorageAccountName -StorageAccountKey $StorageAccountKey.Primary
    ```

* Generar un token de firma de acceso compartido para un contenedor de almacenamiento de Azure y usarlo toocreate un contexto de almacenamiento:

    ```powershell
    $sasToken = New-AzureStorageContainerSASToken -Container abc -Permission rl
    $Ctx = New-AzureStorageContext -StorageAccountName $StorageAccountName -SasToken $sasToken
    ```

    Para más información, consulte [New-AzureStorageContainerSASToken](/powershell/module/azure.storage/new-azurestoragecontainersastoken) y [Uso de Firmas de acceso compartido (SAS)](storage-dotnet-shared-access-signature-part-1.md).

* En algunos casos, puede que desee los extremos de servicio de hello toospecify cuando se crea un nuevo contexto de almacenamiento. Esto podría ser necesario si ha registrado un nombre de dominio personalizado para su cuenta de almacenamiento con el servicio de blobs de Hola o desea toouse una firma de acceso compartido para tener acceso a los recursos de almacenamiento. Establecer puntos de conexión de servicio de hello en una cadena de conexión y usarlo toocreate un nuevo contexto de almacenamiento, tal y como se muestra a continuación:

    ```powershell
    $ConnectionString = "DefaultEndpointsProtocol=http;BlobEndpoint=<blobEndpoint>;QueueEndpoint=<QueueEndpoint>;TableEndpoint=<TableEndpoint>;AccountName=<AccountName>;AccountKey=<AccountKey>"
    $Ctx = New-AzureStorageContext -ConnectionString $ConnectionString
    ```

Para obtener más información acerca de cómo tooconfigure una cadena de conexión de almacenamiento, consulte [configurar cadenas de conexión](storage-configure-connection-string.md).

Ahora que ha configurado el equipo y ha aprendido cómo toomanage suscripciones y cuentas de almacenamiento con PowerShell de Azure, vaya toohello siguiente sección toolearn cómo toomanage Azure blobs y las instantáneas de blob.

### <a name="how-tooretrieve-and-regenerate-azure-storage-keys"></a>¿Cómo tooretrieve y regenerar claves de almacenamiento de Azure
Una cuenta de almacenamiento de Azure incluye dos claves de cuenta. Puede usar Hola siguiente cmdlet tooretrieve sus claves.

```powershell
Get-AzureStorageKey -StorageAccountName "yourstorageaccount"
```

Usar hello siguiente cmdlet tooretrieve una clave específica. Los valores válidos son: Principal y Secundaria.  

```powershell
(Get-AzureStorageKey -StorageAccountName $StorageAccountName).Primary
    
(Get-AzureStorageKey -StorageAccountName $StorageAccountName).Secondary
```

Si desea que tooregenerate sus claves, use Hola siguiente cmdlet. Los valores válidos para -KeyType -son "Principal" y "Secundaria".

```powershell
New-AzureStorageKey -StorageAccountName $StorageAccountName -KeyType "Primary"
    
New-AzureStorageKey -StorageAccountName $StorageAccountName -KeyType "Secondary"
```

## <a name="how-toomanage-azure-blobs"></a>¿Cómo toomanage Azure blobs
Almacenamiento de blobs de Azure es un servicio para almacenar grandes cantidades de datos no estructurados, como texto o binario, que puede tener acceso desde cualquier lugar Hola mundo a través de HTTP o HTTPS. En esta sección se da por supuesto que ya está familiarizado con los conceptos de servicio de almacenamiento de blobs de Azure de Hola. Para más información, consulte [Introducción a Blob Storage mediante .NET](storage-dotnet-how-to-use-blobs.md) y [Conceptos de Blob service](http://msdn.microsoft.com/library/azure/dd179376.aspx).

### <a name="how-toocreate-a-container"></a>¿Cómo toocreate un contenedor
Todos los blobs del almacenamiento de Azure han de estar en un contenedor. Puede crear un contenedor privado mediante el cmdlet New-AzureStorageContainer hello:

```powershell
$StorageContainerName = "yourcontainername"
New-AzureStorageContainer -Name $StorageContainerName -Permission Off
```

> [!NOTE]
> Existen tres niveles de acceso de lectura anónimo: **Desactivado**, **Blob** y **Contenedor**. tooprevent anónimo tener acceso a tooblobs, parámetro del conjunto de permisos Hola demasiado**desactivar**. De forma predeterminada, el nuevo contenedor de hello es privado y son accesibles solo por el propietario de la cuenta de hello. público anónimo tooallow lee tooblob acceder a los recursos, pero no toocontainer metadatos o toohello lista de blobs en el contenedor de hello, establezca el parámetro de permiso de hello demasiado**Blob**. tooallow completa público de lectura tooblob acceder a los recursos, metadatos del contenedor y lista de Hola de blobs en el contenedor de Hola, establezca el parámetro de permiso de hello demasiado**contenedor**. Para obtener más información, consulte [administrar toocontainers de acceso de lectura anónimo y los blobs](storage-manage-access-to-resources.md).
> 
> 

### <a name="how-tooupload-a-blob-into-a-container"></a>¿Cómo tooupload un blob en un contenedor
El almacenamiento de blobs de Azure admite blobs en bloques y en páginas. Para más información, consulte [Introducción a los blobs en bloques, los blobs de anexión y los blobs en páginas](http://msdn.microsoft.com/library/azure/ee691964.aspx).

blobs tooupload tooa contenedor, puede usar hello [Set-AzureStorageBlobContent](/powershell/module/azure.storage/set-azurestorageblobcontent) cmdlet. De forma predeterminada, este comando carga blob en bloques tooa Hola archivos locales. tipo de hello toospecify para blob hello, puede usar hello - BlobType parámetro.

Hello en el ejemplo siguiente se ejecuta hello [Get-ChildItem](http://technet.microsoft.com/library/hh849800.aspx) cmdlet tooget Hola todos los archivos en la carpeta especificada de hello y pasa ellos toohello siguiente cmdlet utilizando el operador de canalización de Hola. Hola [Set-AzureStorageBlobContent](/powershell/module/azure.storage/set-azurestorageblobcontent) cmdlet carga contenedor tooyour de hello archivos locales:

```powershell
Get-ChildItem –Path C:\Images\* | Set-AzureStorageBlobContent -Container "yourcontainername"
```

### <a name="how-toodownload-blobs-from-a-container"></a>¿Cómo toodownload blobs de un contenedor
Hola siguiente ejemplo muestra cómo toodownload blobs de un contenedor. ejemplo de Hola establece en primer lugar un almacenamiento de conexión tooAzure utilizando el contexto de cuenta de almacenamiento de hello, que incluye el nombre de cuenta de almacenamiento de Hola y su clave de acceso principal. A continuación, ejemplo de Hola recupera una referencia de blob mediante hello [AzureStorageBlob Get](/powershell/module/azure.storage/get-azurestorageblob) cmdlet. A continuación, ejemplo de Hola usa hello [Get-AzureStorageBlobContent](/powershell/module/azure.storage/get-azurestorageblobcontent) blobs toodownload de cmdlet en la carpeta de destino local Hola.

```powershell
#Define hello variables.
$ContainerName = "yourcontainername"
$DestinationFolder = "C:\DownloadImages"

#Define hello storage account and context.
$StorageAccountName = "yourstorageaccount"
$StorageAccountKey = "Storage key for yourstorageaccount ends with =="
$Ctx = New-AzureStorageContext -StorageAccountName $StorageAccountName -StorageAccountKey $StorageAccountKey

#List all blobs in a container.
$blobs = Get-AzureStorageBlob -Container $ContainerName -Context $Ctx

#Download blobs from a container.
New-Item -Path $DestinationFolder -ItemType Directory -Force
$blobs | Get-AzureStorageBlobContent -Destination $DestinationFolder -Context $Ctx
```

### <a name="how-toocopy-blobs-from-one-storage-container-tooanother"></a>¿Cómo toocopy blobs desde una tooanother de contenedor de almacenamiento
Puede copiar blobs entre cuentas de almacenamiento y regiones de forma asincrónica. Hello en el ejemplo siguiente se muestra cómo toocopy blobs de almacenamiento de un contenedor tooanother en dos diferentes cuentas de almacenamiento. ejemplo de Hola primero establece las variables para las cuentas de almacenamiento de origen y de destino y, a continuación, crea un contexto de almacenamiento para cada cuenta. A continuación, ejemplo de Hola copia blobs de hello origen toohello destino contenedor mediante hello [AzureStorageBlobCopy inicio](/powershell/module/azure.storage/start-azurestorageblobcopy) cmdlet. ejemplo de Hola se da por supuesto que ya existen cuentas de almacenamiento de origen y destino de Hola y de contenedores.

```powershell
#Define hello source storage account and context.
$SourceStorageAccountName = "yoursourcestorageaccount"
$SourceStorageAccountKey = "Storage key for yoursourcestorageaccount"
$SrcContainerName = "yoursrccontainername"
$SourceContext = New-AzureStorageContext -StorageAccountName $SourceStorageAccountName -StorageAccountKey $SourceStorageAccountKey

#Define hello destination storage account and context.
$DestStorageAccountName = "yourdeststorageaccount"
$DestStorageAccountKey = "Storage key for yourdeststorageaccount"
$DestContainerName = "destcontainername"
$DestContext = New-AzureStorageContext -StorageAccountName $DestStorageAccountName -StorageAccountKey $DestStorageAccountKey

#Get a reference tooblobs in hello source container.
$blobs = Get-AzureStorageBlob -Container $SrcContainerName -Context $SourceContext

#Copy blobs from one container tooanother.
$blobs| Start-AzureStorageBlobCopy -DestContainer $DestContainerName -DestContext $DestContext
```

Tenga en cuenta que este ejemplo realiza una copia asincrónica. Puede supervisar el estado de Hola de cada copia ejecutando hello [AzureStorageBlobCopyState Get](/powershell/module/azure.storage/start-azurestorageblobcopystate) cmdlet.

### <a name="how-toocopy-blobs-from-a-secondary-location"></a>¿Cómo toocopy blobs desde una ubicación secundaria
Puede copiar blobs desde la ubicación secundaria de Hola de una cuenta habilitada para RA GRS.

```powershell
#define secondary storage context using a connection string constructed from secondary endpoints.
$SrcContext = New-AzureStorageContext -ConnectionString "DefaultEndpointsProtocol=https;AccountName=***;AccountKey=***;BlobEndpoint=http://***-secondary.blob.core.windows.net;FileEndpoint=http://***-secondary.file.core.windows.net;QueueEndpoint=http://***-secondary.queue.core.windows.net; TableEndpoint=http://***-secondary.table.core.windows.net;"
Start-AzureStorageBlobCopy –Container *** -Blob *** -Context $SrcContext –DestContainer *** -DestBlob *** -DestContext $DestContext
```

### <a name="how-toodelete-a-blob"></a>¿Cómo toodelete un blob
toodelete un blob, primero hay que obtener una referencia de blob y, a continuación, llame al cmdlet Remove-AzureStorageBlob de hello en él. Hola siguiente ejemplo elimina todos los blobs de hello en un contenedor determinado. ejemplo de Hola primero establece variables para una cuenta de almacenamiento y, a continuación, crea un contexto de almacenamiento. A continuación, ejemplo de Hola recupera una referencia de blob mediante hello [Get AzureStorageBlob](/powershell/module/azure.storage/get-azurestorageblob) Hola de cmdlet y se ejecuta [Remove-AzureStorageBlob](/powershell/module/azure.storage/remove-azurestorageblob) cmdlet tooremove blobs de un contenedor de almacenamiento de Azure.

```powershell
#Define hello storage account and context.
$StorageAccountName = "yourstorageaccount"
$StorageAccountKey = "Storage key for yourstorageaccount ends with =="
$ContainerName = "containername"
$Ctx = New-AzureStorageContext -StorageAccountName $StorageAccountName -StorageAccountKey $StorageAccountKey

#Get a reference tooall hello blobs in hello container.
$blobs = Get-AzureStorageBlob -Container $ContainerName -Context $Ctx

#Delete blobs in a specified container.
$blobs| Remove-AzureStorageBlob
```

## <a name="how-toomanage-azure-blob-snapshots"></a>Cómo las instantáneas de blob toomanage Azure
Azure permite crear una instantánea de un blob. Una instantánea es una versión de solo lectura de un blob que se ha realizado en un momento dado. Una vez se crea la instantánea, puede leerla, copiarla o eliminarla, pero no modificarla. Las instantáneas proporcionan una tooback forma de un blob tal y como aparece en un momento determinado. Para obtener más información, consulte [Crear una instantánea de un blob](http://msdn.microsoft.com/library/azure/hh488361.aspx).

### <a name="how-toocreate-a-blob-snapshot"></a>¿Cómo toocreate una instantánea de blob
toocreate una instantánea de un blob, primero hay que obtener una referencia de blob y, a continuación, llamar a hello `ICloudBlob.CreateSnapshot` método en él. Hello en el ejemplo siguiente se establece primero las variables para una cuenta de almacenamiento y, a continuación, crea un contexto de almacenamiento. A continuación, ejemplo de Hola recupera una referencia de blob mediante hello [Get AzureStorageBlob](/powershell/module/azure.storage/get-azurestorageblob) Hola de cmdlet y se ejecuta [ICloudBlob.CreateSnapshot](http://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.blob.icloudblob.aspx) método toocreate una instantánea.

```powershell
#Define hello storage account and context.
$StorageAccountName = "yourstorageaccount"
$StorageAccountKey = "Storage key for yourstorageaccount ends with =="
$ContainerName = "yourcontainername"
$BlobName = "yourblobname"
$Ctx = New-AzureStorageContext -StorageAccountName $StorageAccountName -StorageAccountKey $StorageAccountKey

#Get a reference tooa blob.
$blob = Get-AzureStorageBlob -Context $Ctx -Container $ContainerName -Blob $BlobName

#Create a snapshot of hello blob.
$snap = $blob.ICloudBlob.CreateSnapshot()
```

### <a name="how-toolist-a-blobs-snapshots"></a>Cómo las instantáneas del toolist un blob
Puede crear tantas instantáneas como desee para un blob. Puede enumerar instantáneas de hello asociadas con su tootrack blob las instantáneas actuales. Hello en el ejemplo siguiente se usa un Hola predefinido de blob y llamadas [AzureStorageBlob Get](/powershell/module/azure.storage/get-azurestorageblob) instantáneas de hello toolist de cmdlet del blob.  

```powershell
#Define hello blob name.
$BlobName = "yourblobname"

#List hello snapshots of a blob.
Get-AzureStorageBlob –Context $Ctx -Prefix $BlobName -Container $ContainerName  | Where-Object  { $_.ICloudBlob.IsSnapshot -and $_.Name -eq $BlobName }
```

### <a name="how-toocopy-a-snapshot-of-a-blob"></a>¿Cómo toocopy una instantánea de un blob
Puede copiar una instantánea de una instantánea de blob toorestore Hola. Para obtener más información y detalles acerca de las restricciones, consulte [Crear una instantánea de un blob](http://msdn.microsoft.com/library/azure/hh488361.aspx). Hello en el ejemplo siguiente se establece primero las variables para una cuenta de almacenamiento y, a continuación, crea un contexto de almacenamiento. A continuación, ejemplo de Hola define variables de nombre de contenedor y blob Hola. ejemplo de Hola recupera una referencia de blob mediante hello [Get AzureStorageBlob](/powershell/module/azure.storage/get-azurestorageblob) Hola de cmdlet y se ejecuta [ICloudBlob.CreateSnapshot](http://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.blob.icloudblob.aspx) método toocreate una instantánea. A continuación, ejemplo de Hola ejecuta hello [AzureStorageBlobCopy inicio](/powershell/module/azure.storage/start-azurestorageblobcopy) instantánea de hello toocopy de cmdlet de un blob con objeto de ICloudBlob de hello para el blob de origen de Hola. Estar seguro de que las variables de hello tooupdate según la configuración antes de ejemplo Hola. Tenga en cuenta que Hola siguiente ejemplo se da por supuesto que Hola contenedores de origen y de destino y blob de origen Hola ya existe.

```powershell
#Define hello storage account and context.
$StorageAccountName = "yourstorageaccount"
$StorageAccountKey = "Storage key for yourstorageaccount ends with =="
$Ctx = New-AzureStorageContext -StorageAccountName $StorageAccountName -StorageAccountKey $StorageAccountKey

#Define hello variables.
$SrcContainerName = "yoursourcecontainername"
$DestContainerName = "yourdestcontainername"
$SrcBlobName = "yourblobname"
$DestBlobName = "CopyBlobName"

#Get a reference tooa blob.
$blob = Get-AzureStorageBlob -Context $Ctx -Container $SrcContainerName -Blob $SrcBlobName

#Create a snapshot of a blob.
$snap = $blob.ICloudBlob.CreateSnapshot()

#Copy hello snapshot tooanother container.
Start-AzureStorageBlobCopy –Context $Ctx -ICloudBlob $snap -DestBlob $DestBlobName -DestContainer $DestContainerName
```

Ahora que ha aprendido cómo toomanage Azure blobs y las instantáneas con Azure PowerShell de blob, vaya toohello siguiente sección toolearn cómo toomanage tablas, colas y archivos.

## <a name="how-toomanage-azure-tables-and-table-entities"></a>¿Cómo toomanage Azure tablas y entidades de tabla
Servicio de almacenamiento de tabla de Azure es un almacén de datos NoSQL, que se puede utilizar toostore y consulta los conjuntos grandes de datos estructurados no relacionales. componentes principales de Hello del servicio de hello son tablas, entidades y propiedades. Una tabla es una colección de entidades. Una entidad es un conjunto de propiedades. Cada entidad puede tener hasta too252 propiedades, que son todos los pares de nombre y valor. En esta sección se da por supuesto que ya está familiarizado con conceptos de servicio de almacenamiento de tabla de Azure de Hola. Para obtener información detallada, vea [Hola de entender el modelo de datos del servicio de tabla](http://msdn.microsoft.com/library/azure/dd179338.aspx) y [Introducción al almacenamiento de tabla de Azure mediante .NET](storage-dotnet-how-to-use-tables.md).

Hola siguientes subsecciones, obtendrá información sobre cómo toomanage almacenamiento de tabla de Azure service con Azure PowerShell. Hello escenarios descritos se incluyen **crear**, **eliminar**, y **recuperar** **tablas**, así como **agregar**, **consultar**, y **eliminar entidades de tabla**.

### <a name="how-toocreate-a-table"></a>¿Cómo toocreate una tabla
Todas las tablas deberán estar en una cuenta de almacenamiento de Azure. Hello ejemplo siguiente se muestra cómo toocreate una tabla en el almacenamiento de Azure. ejemplo de Hola establece en primer lugar un almacenamiento de conexión tooAzure utilizando el contexto de cuenta de almacenamiento de hello, que incluye el nombre de cuenta de almacenamiento de Hola y su clave de acceso. A continuación, usa hello [AzureStorageTable New](/powershell/module/azure.storage/new-azurestoragetable) cmdlet toocreate una tabla en el almacenamiento de Azure.

```powershell
#Define hello storage account and context.
$StorageAccountName = "yourstorageaccount"
$StorageAccountKey = "Storage key for yourstorageaccount ends with =="
$Ctx = New-AzureStorageContext $StorageAccountName -StorageAccountKey $StorageAccountKey

#Create a new table.
$tabName = "yourtablename"
New-AzureStorageTable –Name $tabName –Context $Ctx
```

### <a name="how-tooretrieve-a-table"></a>¿Cómo tooretrieve una tabla
Puede consultar y recuperar una o todas las tablas de una cuenta de almacenamiento. Hello en el ejemplo siguiente se muestra cómo tooretrieve una tabla dada mediante Hola [AzureStorageTable Get](/powershell/module/azure.storage/get-azurestoragetable) cmdlet.

```powershell
#Retrieve a table.
$tabName = "yourtablename"
Get-AzureStorageTable –Name $tabName –Context $Ctx
```

Si llama al cmdlet Get-AzureStorageTable de hello sin ningún parámetro, obtiene todas las tablas de almacenamiento para una cuenta de almacenamiento.

### <a name="how-toodelete-a-table"></a>¿Cómo toodelete una tabla
Puede eliminar una tabla de una cuenta de almacenamiento mediante el uso de hello [Remove-AzureStorageTable](/powershell/module/azure.storage/remove-azurestoragetable) cmdlet.  

```powershell
#Delete a table.
$tabName = "yourtablename"
Remove-AzureStorageTable –Name $tabName –Context $Ctx
```

### <a name="how-toomanage-table-entities"></a>Cómo toomanage tabla entidades
Actualmente, PowerShell de Azure no proporciona directamente cmdlets toomanage en entidades de tabla. tooperform operaciones en entidades de tabla, puede utilizar clases de hello en hello [biblioteca de cliente de almacenamiento de Azure para .NET](http://msdn.microsoft.com/library/azure/wa_storage_30_reference_home.aspx).

#### <a name="how-tooadd-table-entities"></a>Cómo tooadd tabla entidades
tooadd una tabla de tooa de entidad, primero cree un objeto que define las propiedades de entidad. Una entidad puede tener hasta too255 propiedades, incluidas las 3 propiedades del sistema: **PartitionKey**, **RowKey**, y **marca de tiempo**. Usted es responsable de insertar y actualizar valores de hello de **PartitionKey** y **RowKey**. servidor Hello administra valo hello **marca de tiempo**, que no se puede modificar. Hola junto **PartitionKey** y **RowKey** identificar de forma exclusiva todas las entidades dentro de una tabla.

* **PartitionKey**: determina la partición de Hola Hola entidad se almacena en.
* **RowKey**: identifica de forma única entidad de hello en partición de Hola.

Puede definir las propiedades personalizadas de too252 para una entidad. Para obtener más información, consulte [Hola de entender el modelo de datos del servicio de tabla](http://msdn.microsoft.com/library/azure/dd179338.aspx).

Hello ejemplo siguiente se muestra cómo tabla tooa de tooadd entidades. ejemplo de Hola muestra cómo tooretrieve Hola tabla de empleados y agregar varias entidades en él. En primer lugar, establece un almacenamiento de conexión tooAzure utilizando el contexto de cuenta de almacenamiento de hello, que incluye el nombre de cuenta de almacenamiento de Hola y su clave de acceso. A continuación, recupera Hola dada tabla mediante hello [AzureStorageTable Get](/powershell/module/azure.storage/get-azurestoragetable) cmdlet. Si no existe la tabla de hello, Hola [AzureStorageTable New](/powershell/module/azure.storage/new-azurestoragetable) cmdlet es toocreate usa una tabla de almacenamiento de Azure. A continuación, ejemplo de Hola define una función personalizada tabla toohello de Agregar entidad tooadd entidades mediante la especificación de cada partición y una clave de fila. Hola de llamadas de función Hello Agregar entidad [New-Object](http://technet.microsoft.com/library/hh849885.aspx) cmdlet en hello [Microsoft.WindowsAzure.Storage.Table.DynamicTableEntity](http://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.table.dynamictableentity.aspx) toocreate clase un objeto de entidad. Más adelante, ejemplo de Hola llama hello [Microsoft.WindowsAzure.Storage.Table.TableOperation.Insert](http://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.table.tableoperation.insert.aspx) método en este tooadd de objeto de entidad se tooa tabla.

```powershell
#Function Add-Entity: Adds an employee entity tooa table.
function Add-Entity() {
    [CmdletBinding()]
    param(
       $table,
       [String]$partitionKey,
       [String]$rowKey,
       [String]$name,
       [Int]$id
    )

  $entity = New-Object -TypeName Microsoft.WindowsAzure.Storage.Table.DynamicTableEntity -ArgumentList $partitionKey, $rowKey
  $entity.Properties.Add("Name", $name)
  $entity.Properties.Add("ID", $id)

  $result = $table.CloudTable.Execute([Microsoft.WindowsAzure.Storage.Table.TableOperation]::Insert($entity))
}

#Define hello storage account and context.
$StorageAccountName = "yourstorageaccount"
$StorageAccountKey = Get-AzureStorageKey -StorageAccountName $StorageAccountName
$Ctx = New-AzureStorageContext $StorageAccountName -StorageAccountKey $StorageAccountKey.Primary
$TableName = "Employees"

#Retrieve hello table if it already exists.
$table = Get-AzureStorageTable –Name $TableName -Context $Ctx -ErrorAction Ignore

#Create a new table if it does not exist.
if ($table -eq $null)
{
   $table = New-AzureStorageTable –Name $TableName -Context $Ctx
}

#Add multiple entities tooa table.
Add-Entity -Table $table -PartitionKey Partition1 -RowKey Row1 -Name Chris -Id 1
Add-Entity -Table $table -PartitionKey Partition1 -RowKey Row2 -Name Jessie -Id 2
Add-Entity -Table $table -PartitionKey Partition2 -RowKey Row1 -Name Christine -Id 3
Add-Entity -Table $table -PartitionKey Partition2 -RowKey Row2 -Name Steven -Id 4
```

#### <a name="how-tooquery-table-entities"></a>Cómo tooquery tabla entidades
tooquery una tabla, utilice hello [Microsoft.WindowsAzure.Storage.Table.TableQuery](http://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.table.tablequery.aspx) clase. Hello en el ejemplo siguiente se supone que ya ha ejecutado el script de Hola facilitado en hello cómo tooadd sección de entidades de esta guía. ejemplo de Hola establece en primer lugar un almacenamiento de conexión tooAzure utilizando el contexto de almacenamiento de hello, que incluye el nombre de cuenta de almacenamiento de Hola y su clave de acceso. A continuación, lo intenta de tabla de hello creado anteriormente "Employees" tooretrieve con hello [AzureStorageTable Get](/powershell/module/azure.storage/get-azurestoragetable) cmdlet. Llamar a hello [New-Object](http://technet.microsoft.com/library/hh849885.aspx) cmdlet en hello Microsoft.WindowsAzure.Storage.Table.TableQuery clase crea un nuevo objeto de consulta. ejemplo de Hola busca las entidades de Hola que tienen una columna 'ID' cuyo valor es 1, como se especifica en un filtro de cadena. Para obtener información detallada, vea [Consultar tablas y entidades](http://msdn.microsoft.com/library/azure/dd894031.aspx). Al ejecutar esta consulta, devuelve todas las entidades que coinciden con los criterios de filtro de Hola.

```powershell
#Define hello storage account and context.
$StorageAccountName = "yourstorageaccount"
$StorageAccountKey = Get-AzureStorageKey -StorageAccountName $StorageAccountName
$Ctx = New-AzureStorageContext –StorageAccountName $StorageAccountName -StorageAccountKey $StorageAccountKey.Primary
$TableName = "Employees"

#Get a reference tooa table.
$table = Get-AzureStorageTable –Name $TableName -Context $Ctx

#Create a table query.
$query = New-Object Microsoft.WindowsAzure.Storage.Table.TableQuery

#Define columns tooselect.
$list = New-Object System.Collections.Generic.List[string]
$list.Add("RowKey")
$list.Add("ID")
$list.Add("Name")

#Set query details.
$query.FilterString = "ID gt 0"
$query.SelectColumns = $list
$query.TakeCount = 20

#Execute hello query.
$entities = $table.CloudTable.ExecuteQuery($query)

#Display entity properties with hello table format.
$entities  | Format-Table PartitionKey, RowKey, @{ Label = "Name"; Expression={$_.Properties["Name"].StringValue}}, @{ Label = "ID"; Expression={$_.Properties["ID"].Int32Value}} -AutoSize
```

#### <a name="how-toodelete-table-entities"></a>Cómo toodelete tabla entidades
Puede eliminar una entidad usando sus claves de partición y fila. Hello en el ejemplo siguiente se supone que ya ha ejecutado el script de Hola facilitado en hello cómo tooadd sección de entidades de esta guía. ejemplo de Hola establece en primer lugar un almacenamiento de conexión tooAzure utilizando el contexto de almacenamiento de hello, que incluye el nombre de cuenta de almacenamiento de Hola y su clave de acceso. A continuación, lo intenta de tabla de hello creado anteriormente "Employees" tooretrieve con hello [AzureStorageTable Get](/powershell/module/azure.storage/get-azurestoragetable) cmdlet. Si existe en la tabla de hello, ejemplo de Hola llama hello [Microsoft.WindowsAzure.Storage.Table.TableOperation.Retrieve](http://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.table.tableoperation.retrieve.aspx) tooretrieve método una entidad en función de sus valores de clave de partición y fila. A continuación, pase Hola entidad toohello [Microsoft.WindowsAzure.Storage.Table.TableOperation.Delete](http://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.table.tableoperation.delete.aspx) toodelete de método.

```powershell
#Define hello storage account and context.
$StorageAccountName = "yourstorageaccount"
$StorageAccountKey = Get-AzureStorageKey -StorageAccountName $StorageAccountName
$Ctx = New-AzureStorageContext –StorageAccountName $StorageAccountName -StorageAccountKey $StorageAccountKey.Primary

#Retrieve hello table.
$TableName = "Employees"
$table = Get-AzureStorageTable -Name $TableName -Context $Ctx -ErrorAction Ignore

#If hello table exists, start deleting its entities.
if ($table -ne $null) 
{
    #Together hello PartitionKey and RowKey uniquely identify every  
    #entity within a table.
    $tableResult = $table.CloudTable.Execute([Microsoft.WindowsAzure.Storage.Table.TableOperation]::Retrieve("Partition2", "Row1"))
    $entity = $tableResult.Result
    if ($entity -ne $null)
    {
        #Delete hello entity.
        $table.CloudTable.Execute([Microsoft.WindowsAzure.Storage.Table.TableOperation]::Delete($entity))
    }
}
```

## <a name="how-toomanage-azure-queues-and-queue-messages"></a>¿Cómo toomanage Azure pone en cola y cola de mensajes
Almacenamiento de la cola de Azure es un servicio para almacenar grandes cantidades de mensajes que pueden tener acceso desde cualquier lugar Hola mundo a través de llamadas autenticadas mediante HTTP o HTTPS. En esta sección se da por supuesto que ya está familiarizado con conceptos de servicio de almacenamiento de cola de Azure de Hola. Para más información, consulte [Introducción al Almacenamiento en cola de Azure mediante .NET](storage-dotnet-how-to-use-queues.md).

Esta sección le mostrará cómo toomanage almacenamiento de cola de Azure service con Azure PowerShell. Hello escenarios descritos se incluyen **insertar** y **eliminar** cola los mensajes, así como **crear**, **eliminar**y **recuperar colas**.

### <a name="how-toocreate-a-queue"></a>¿Cómo toocreate una cola
Hello en el ejemplo siguiente se establece en primer lugar un almacenamiento de conexión tooAzure utilizando el contexto de cuenta de almacenamiento de hello, que incluye el nombre de cuenta de almacenamiento de Hola y su clave de acceso. A continuación, llama a [AzureStorageQueue New](/powershell/module/azure.storage/new-azurestoragequeue) cmdlet toocreate una cola denominada 'queuename'.

```powershell
#Define hello storage account and context.
$StorageAccountName = "yourstorageaccount"
$StorageAccountKey = Get-AzureStorageKey -StorageAccountName $StorageAccountName
$Ctx = New-AzureStorageContext –StorageAccountName $StorageAccountName -StorageAccountKey $StorageAccountKey.Primary
$QueueName = "queuename"
$Queue = New-AzureStorageQueue –Name $QueueName -Context $Ctx
```

Para obtener información sobre las convenciones de nomenclatura del servicio Cola de Azure, consulte [Nomenclatura de colas y metadatos](http://msdn.microsoft.com/library/azure/dd179349.aspx).

### <a name="how-tooretrieve-a-queue"></a>¿Cómo tooretrieve una cola
Puede consultar y recuperar una cola específica o una lista de todas las colas de hello en una cuenta de almacenamiento. Hello en el ejemplo siguiente se muestra cómo tooretrieve una cola especificada utilizando Hola [AzureStorageQueue Get](/powershell/module/azure.storage/get-azurestoragequeue) cmdlet.

```powershell
#Retrieve a queue.
$QueueName = "queuename"
$Queue = Get-AzureStorageQueue –Name $QueueName –Context $Ctx
```

Si se llama a hello [AzureStorageQueue Get](/powershell/module/azure.storage/get-azurestoragequeue) cmdlet sin parámetros, obtiene una lista de todas las colas de Hola.

### <a name="how-toodelete-a-queue"></a>¿Cómo toodelete una cola
toodelete una cola y todos los mensajes de Hola contenidas en ella, llamada Hola Remove-AzureStorageQueue cmdlet. Hola de ejemplo siguiente muestra cómo toodelete una cola especificada utilizando Hola cmdlet Remove-AzureStorageQueue.

```powershell
#Delete a queue.
$QueueName = "yourqueuename"
Remove-AzureStorageQueue –Name $QueueName –Context $Ctx
```

#### <a name="how-tooinsert-a-message-into-a-queue"></a>¿Cómo tooinsert un mensaje en una cola
tooinsert un mensaje en una cola existente, primero cree una nueva instancia de hello [Microsoft.WindowsAzure.Storage.Queue.CloudQueueMessage](http://msdn.microsoft.com/library/azure/jj732474.aspx) clase. A continuación, llame a hello [AddMessage](http://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.queue.cloudqueue.addmessage.aspx) método. Se puede crear un CloudQueueMessage a partir de una cadena (en formato UTF-8) o de una matriz de bytes.

Hola siguiente ejemplo muestra cómo tooadd tooa cola de mensajes. ejemplo de Hola establece en primer lugar un almacenamiento de conexión tooAzure utilizando el contexto de cuenta de almacenamiento de hello, que incluye el nombre de cuenta de almacenamiento de Hola y su clave de acceso. A continuación, recupera mediante Hola de cola especificado hello [AzureStorageQueue Get](https://msdn.microsoft.com/library/azure/dn806377.aspx) cmdlet. Si la cola de hello existe, hello [New-Object](http://technet.microsoft.com/library/hh849885.aspx) cmdlet es toocreate usa una instancia de hello [Microsoft.WindowsAzure.Storage.Queue.CloudQueueMessage](http://msdn.microsoft.com/library/azure/jj732474.aspx) clase. Más adelante, ejemplo de Hola llama hello [AddMessage](http://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.queue.cloudqueue.addmessage.aspx) método en este tooadd del objeto de mensaje se tooa cola. Este es el código que recupera una cola e inserta el mensaje de bienvenida de 'MessageInfo':

```powershell
#Define hello storage account and context.
$StorageAccountName = "yourstorageaccount"
$StorageAccountKey = Get-AzureStorageKey -StorageAccountName $StorageAccountName
$Ctx = New-AzureStorageContext –StorageAccountName $StorageAccountName -StorageAccountKey $StorageAccountKey.Primary

#Retrieve hello queue.
$QueueName = "queuename"
$Queue = Get-AzureStorageQueue -Name $QueueName -Context $ctx

#If hello queue exists, add a new message.
if ($Queue -ne $null) {
   # Create a new message using a constructor of hello CloudQueueMessage class.
   $QueueMessage = New-Object -TypeName Microsoft.WindowsAzure.Storage.Queue.CloudQueueMessage -ArgumentList MessageInfo

   # Add a new message toohello queue.
   $Queue.CloudQueue.AddMessage($QueueMessage)
}
```

#### <a name="how-toode-queue-at-hello-next-message"></a>¿Cómo toode a la cola en hello mensaje siguiente
El código quita un mensaje de una cola en dos pasos. Cuando se llama a hello [Microsoft.WindowsAzure.Storage.Queue.CloudQueue.GetMessage](http://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.queue.cloudqueue.getmessage.aspx) (método), obtendrá los mensajes de bienvenida del siguiente en una cola. Un mensaje devuelto de **GetMessage** se convierte en invisible tooany otro código que lee mensajes de esta cola. toofinish al quitar el mensaje de saludo de cola de hello, también debe llamar a hello [Microsoft.WindowsAzure.Storage.Queue.CloudQueue.DeleteMessage](http://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.queue.cloudqueue.deletemessage.aspx) método. Este proceso de dos pasos de la eliminación de un mensaje garantiza que si se produce un error en el código tooprocess que puede obtener un mensaje debido a un error toohardware o software, otra instancia del código Hola mismo mensaje y vuelva a intentarlo. Las llamadas de código **DeleteMessage** justo después de que se ha procesado el mensaje de bienvenida.

```powershell
# Define hello storage account and context.
$StorageAccountName = "yourstorageaccount"
$StorageAccountKey = Get-AzureStorageKey -StorageAccountName $StorageAccountName
$Ctx = New-AzureStorageContext –StorageAccountName $StorageAccountName -StorageAccountKey $StorageAccountKey.Primary

# Retrieve hello queue.
$QueueName = "queuename"
$Queue = Get-AzureStorageQueue -Name $QueueName -Context $ctx

$InvisibleTimeout = [System.TimeSpan]::FromSeconds(10)

# Get hello message object from hello queue.
$QueueMessage = $Queue.CloudQueue.GetMessage($InvisibleTimeout)
# Delete hello message.
$Queue.CloudQueue.DeleteMessage($QueueMessage)
```

## <a name="how-toomanage-azure-file-shares-and-files"></a>¿Cómo toomanage archivo Azure comparte y archivos
Almacenamiento de archivos de Azure ofrece almacenamiento compartido para las aplicaciones que usan el protocolo SMB estándar de Hola. Máquinas virtuales de Microsoft Azure y servicios en la nube pueden compartir datos de archivos a través de los componentes de la aplicación a través de recursos compartidos montados y aplicaciones locales pueden tener acceso a los datos de archivo en un recurso compartido a través de API de almacenamiento de archivos de Hola o Azure PowerShell.

Para más información sobre Azure File Storage, consulte [Introducción a Azure File Storage en Windows](storage-dotnet-how-to-use-files.md) y [API de REST del servicio de archivos](http://msdn.microsoft.com/library/azure/dn167006.aspx).

## <a name="how-tooset-and-query-storage-analytics"></a>¿Cómo tooset y consulta de análisis de almacenamiento
Puede usar [análisis de almacenamiento de Azure](storage-analytics.md) toocollect métricas para los datos del registro acerca de las solicitudes y las cuentas de almacenamiento de Azure envían tooyour cuenta de almacenamiento. Puede utilizar Mantenimiento de almacenamiento métricas toomonitor Hola de una cuenta de almacenamiento y almacenamiento toodiagnose de registro y solucionar los problemas de la cuenta de almacenamiento. Puede configurar la supervisión mediante Hola portal de Azure o Windows PowerShell o mediante programación con la biblioteca de cliente de almacenamiento de Hola. El registro de almacenamiento del servidor produce y permite toorecord detalles para las solicitudes correctas e incorrectas en la cuenta de almacenamiento. Estos registros permiten toosee detalles de operaciones de lectura, escritura y eliminación con sus tablas, colas y blobs, así como los motivos de Hola para solicitudes con error.

toolearn tooenable y ver de los datos de las métricas de almacenamiento con PowerShell, vea [cómo tooenable las métricas de almacenamiento con PowerShell](http://msdn.microsoft.com/library/azure/dn782843.aspx#HowtoenableStorageMetricsusingPowerShell).

toolearn tooenable y recuperar datos del registro de almacenamiento con PowerShell, vea [cómo tooenable almacenamiento registrar mediante PowerShell](http://msdn.microsoft.com/library/azure/dn782840.aspx#HowtoenableStorageLoggingusingPowerShell) y [buscar los datos de registro del registro de almacenamiento](http://msdn.microsoft.com/library/azure/dn782840.aspx#FindingyourStorageLogginglogdata).
Para obtener información detallada sobre el uso de las métricas de almacenamiento y el registro de problemas de almacenamiento de tootroubleshoot de almacenamiento, consulte [Monitoring, Diagnosing and Troubleshooting Microsoft Azure Storage](storage-monitoring-diagnosing-troubleshooting.md).

## <a name="how-toomanage-shared-access-signature-sas-and-stored-access-policy"></a>Cómo compartir toomanage firma de acceso (SAS) y la directiva de acceso almacenada
Las firmas de acceso compartido son una parte importante del modelo de seguridad de Hola para las aplicaciones que utilizan el almacenamiento de Azure. Son útiles para proporcionar permisos limitados tooclients de cuenta de almacenamiento de tooyour que no se debería tener la clave de la cuenta de hello. De forma predeterminada, sólo el propietario de Hola de cuenta de almacenamiento de hello puede tener acceso a blobs, tablas y colas en esa cuenta. Si el servicio o la aplicación necesita toomake estos clientes tooother disponibles de recursos sin compartir la clave de acceso, tiene tres opciones:

* Establecer el acceso de lectura anónimo toohello contenedor de un contenedor permisos toopermit y sus blobs. Esto no se permite para tablas o colas.
* Utilizar una firma de acceso compartido que concede toocontainers de derechos de acceso restringido, blobs, colas y tablas para un intervalo de tiempo específico.
* Utilice un tooobtain de directiva de acceso almacenada un nivel adicional de control sobre las firmas de acceso compartido para un contenedor o sus blobs, para una cola o para una tabla. Hello directiva de acceso almacenada permite la hora de inicio de hello toochange, la hora de expiración o permisos de una firma o toorevoke después de se ha emitido.

Una firma de acceso compartido puede presentar una de estas dos formas:

* **Ad hoc SAS**: cuando se crea un SAS ad hoc, la hora de inicio de hello, la hora de expiración y permisos para hello SAS se especifican en hello URI de SAS. Este tipo de SAS puede crearse en un contenedor, blob, tabla o cola y no se puede revocar.
* **Asociaciones de seguridad con la directiva de acceso almacenada**: se define una directiva de acceso almacenada en un contenedor de recursos un contenedor de blob, tabla o cola - y se pueden usar restricciones de toomanage para una o varias firmas de acceso compartido. Al asociar una SAS con una directiva de acceso almacenada, Hola SAS hereda las restricciones de hello: Hola hora de inicio, la hora de expiración y permisos - definidos para la directiva de acceso de hello almacenado. Este tipo de SAS se puede revocar.

Para obtener más información, consulte [utilizando firmas de acceso compartido (SAS)](storage-dotnet-shared-access-signature-part-1.md) y [administrar toocontainers de acceso de lectura anónimo y los blobs](storage-manage-access-to-resources.md).

En las secciones siguientes de hello, aprenderá cómo toocreate una directiva de acceso almacenado y token de firma de acceso compartido para las tablas de Azure. Azure PowerShell también proporciona cmdlets similares para contenedores, blobs y colas. secuencias de comandos de toorun hello en esta sección, descargue hello [Azure PowerShell versión 0.8.14](http://go.microsoft.com/?linkid=9811175&clcid=0x409) o una versión posterior.

### <a name="how-toocreate-a-policy-based-shared-access-signature-token"></a>El token de firma de acceso compartido toocreate basada en directivas
Utilice hello AzureStorageTableStoredAccessPolicy nuevo cmdlet toocreate una nueva directiva de acceso almacenada. A continuación, llamar a hello [AzureStorageTableSASToken New](/powershell/module/azure.storage/new-azurestoragetablesastoken) cmdlet toocreate un nuevo token de firma de acceso compartido basada en directivas para una tabla de almacenamiento de Azure.

```powershell
$policy = "policy1"
New-AzureStorageTableStoredAccessPolicy -Name $tableName -Policy $policy -Permission "rd" -StartTime "2015-01-01" -ExpiryTime "2016-01-01" -Context $Ctx
New-AzureStorageTableSASToken -Name $tableName -Policy $policy -Context $Ctx
```

### <a name="how-toocreate-an-ad-hoc-non-revocable-shared-access-signature-token"></a>¿Cómo toocreate un token de firma de acceso compartido ad hoc (no revocable)
Hola de uso [AzureStorageTableSASToken New](/powershell/module/azure.storage/new-azurestoragetablesastoken) cmdlet toocreate un nuevo token de firma de acceso compartido (no revocable) ad hoc para una tabla de almacenamiento de Azure:

```powershell
New-AzureStorageTableSASToken -Name $tableName -Permission "rqud" -StartTime "2015-01-01" -ExpiryTime "2015-02-01" -Context $Ctx
```
    
### <a name="how-toocreate-a-stored-access-policy"></a>¿Cómo toocreate una directiva de acceso almacenada
Use hello AzureStorageTableStoredAccessPolicy nuevo cmdlet toocreate una nueva directiva de acceso almacenada en una tabla de almacenamiento de Azure:

```powershell
$policy = "policy1"
New-AzureStorageTableStoredAccessPolicy -Name $tableName -Policy $policy -Permission "rd" -StartTime "2015-01-01" -ExpiryTime "2016-01-01" -Context $Ctx
```
    
### <a name="how-tooupdate-a-stored-access-policy"></a>¿Cómo tooupdate una directiva de acceso almacenada
Use Hola conjunto AzureStorageTableStoredAccessPolicy cmdlet tooupdate una directiva de acceso almacenada existente para una tabla de almacenamiento de Azure:

```powershell
Set-AzureStorageTableStoredAccessPolicy -Policy $policy -Table $tableName -Permission "rd" -NoExpiryTime -NoStartTime -Context $Ctx
```

### <a name="how-toodelete-a-stored-access-policy"></a>¿Cómo toodelete una directiva de acceso almacenada
Usar Hola Remove-AzureStorageTableStoredAccessPolicy cmdlet toodelete una directiva de acceso almacenada en una tabla de almacenamiento de Azure:

```powershell
Remove-AzureStorageTableStoredAccessPolicy -Policy $policy -Table $tableName -Context $Ctx
```

## <a name="how-toouse-azure-storage-for-us-government-and-azure-china"></a>Cómo toouse el almacenamiento de Azure para el gobierno de Estados Unidos y Azure China
Un entorno de Azure es una implementación independiente de Microsoft Azure como, por ejemplo, [Azure Government para el gobierno de EE. UU.](https://azure.microsoft.com/features/gov/), [AzureCloud para el servicio global de Azure](https://portal.azure.com) y [AzureChinaCloud para el servicio de Azure operado por 21Vianet en China](http://www.windowsazure.cn/). Puede implementar el nuevo entorno de Azure para el gobierno de los EE. UU. y Azure para China.

Almacenamiento de Azure con AzureChinaCloud toouse, deberá toocreate un contexto de almacenamiento que está asociado a AzureChinaCloud. Siga estos tooget pasos que se ha iniciado:

1. Ejecute hello [AzureEnvironment Get](/powershell/module/azure/get-azureenvironment?view=azuresmps-3.7.0) toosee cmdlet Hola entornos de Azure disponibles:
   
    ```powershell
    Get-AzureEnvironment
    ```

2. Agregue un tooWindows de cuenta de Azure China PowerShell:
   
    ```powershell
    Add-AzureAccount –Environment AzureChinaCloud
    ```

3. Cree un contexto de almacenamiento para una cuenta AzureChinaCloud:
   
    ```powershell
    $Ctx = New-AzureStorageContext -StorageAccountName $AccountName -StorageAccountKey $AccountKey> -Environment AzureChinaCloud
    ```

toouse almacenamiento de Azure con [EE. UU. Government para EE. UU.](https://azure.microsoft.com/features/gov/), deberá precisar un nuevo entorno y crear un nuevo contexto de almacenamiento con este entorno:

1. Ejecute hello [AzureEnvironment Get](/powershell/module/azure/get-azureenvironment?view=azuresmps-3.7.0) toosee cmdlet Hola entornos de Azure disponibles:

    ```powershell
    Get-AzureEnvironment
    ```

2. Agregue un tooWindows de cuenta de Azure US Government PowerShell:
   
    ```powershell
    Add-AzureAccount –Environment AzureUSGovernment
    ```

3. Cree un contexto de almacenamiento para una cuenta de AzureUSGovernment:
   
    ```powershell
    $Ctx = New-AzureStorageContext -StorageAccountName $AccountName -StorageAccountKey $AccountKey> -Environment AzureUSGovernment
    ```
     
Para más información, consulte:

* [Guía para desarrolladores de Microsoft Azure Government](../azure-government-developer-guide.md).
* [Información general de las diferencias en la creación de una aplicación de servicio de China](https://msdn.microsoft.com/library/azure/dn578439.aspx)

## <a name="next-steps"></a>Pasos siguientes
En esta guía, ha aprendido cómo toomanage el almacenamiento de Azure con Azure PowerShell. A continuación encontrará algunos artículos relacionados y recursos para obtener más información acerca de estos servicios.

* [Documentación de Almacenamiento de Azure](https://azure.microsoft.com/documentation/services/storage/)
* [Cmdlets de PowerShell de Almacenamiento de Azure.](/powershell/module/azurerm.storage/#storage)
* [Referencia de Windows PowerShell](https://msdn.microsoft.com/library/ms714469.aspx)

[Getting started with Azure Storage and PowerShell in 5 minutes]: #getstart
[Prerequisites for using Azure PowerShell with Azure Storage]: #pre
[How toomanage storage accounts in Azure]: #manageaccount
[How tooset a default Azure subscription]: #setdefsub
[How toocreate a new Azure storage account]: #createaccount
[How tooset a default Azure storage account]: #defaultaccount
[How toolist all Azure storage accounts in a subscription]: #listaccounts
[How toocreate an Azure storage context]: #createctx
[How toomanage Azure blobs and blob snapshots]: #manageblobs
[How toocreate a container]: #container
[How tooupload a blob into a container]: #uploadblob
[How toodownload blobs from a container]: #downblob
[How toocopy blobs from one storage container tooanother]: #copyblob
[How toodelete a blob]: #deleteblob
[How toomanage Azure blob snapshots]: #manageshots
[How toocreate a blob snapshot]: #createshot
[How toolist snapshots of a blob]: #listshot
[How toocopy a snapshot of a blob]: #copyshot
[How toomanage Azure tables and table entities]: #managetables
[How toocreate a table]: #createtable
[How tooretrieve a table]: #gettable
[How toodelete a table]: #remtable
[How toomanage table entities]: #mngentity
[How tooadd table entities]: #addentity
[How tooquery table entities]: #queryentity
[How toodelete table entities]: #deleteentity
[How toomanage Azure queues and queue messages]: #managequeues
[How toocreate a queue]: #createqueue
[How tooretrieve a queue]: #getqueue
[How toodelete a queue]: #remqueue
[How toomanage queue messages]: #mngqueuemsg
[How tooinsert a message into a queue]: #addqueuemsg
[How toode-queue at hello next message]: #dequeuemsg
[How toomanage Azure file shares and files]: #files
[How tooset and query storage analytics]: #stganalytics
[How toomanage Shared Access Signature (SAS) and Stored Access Policy]: #sas
[How toouse Azure Storage for U.S. government and Azure China]: #gov
[Next Steps]: #next
