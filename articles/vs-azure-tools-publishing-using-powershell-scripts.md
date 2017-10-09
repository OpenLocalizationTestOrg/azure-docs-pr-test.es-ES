---
title: aaaUsing entornos de prueba y los Scripts de Windows PowerShell tooPublish tooDev | Documentos de Microsoft
description: "Obtenga información acerca de cómo toouse Windows PowerShell scripts de entornos de prueba y toodevelopment de toopublish de Visual Studio."
services: visual-studio-online
documentationcenter: na
author: kraigb
manager: ghogen
editor: 
ms.assetid: 5fff1301-5469-4d97-be88-c85c30f837c1
ms.service: multiple
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: multiple
ms.date: 11/11/2016
ms.author: kraigb
ms.openlocfilehash: 491a058f96255576afa74f6156f20ae9559bb9f7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="using-windows-powershell-scripts-toopublish-toodev-and-test-environments"></a>Uso de Windows PowerShell scripts de entornos de prueba y toodev de toopublish
Cuando crea una aplicación web en Visual Studio, puede generar un script de Windows PowerShell que puede utilizar la publicación de hello tooautomate posterior de su sitio Web tooAzure como una aplicación Web en el servicio de aplicaciones de Azure o una máquina virtual. Puede editar y ampliar sus requisitos de script de Windows PowerShell de hello en toosuit de editor de Visual Studio de Hola o integrar script de Hola con compilación existente, prueba y scripts de publicación.

Mediante estos scripts, puede aprovisionar versiones personalizadas (también conocidos como entornos de desarrollo y pruebas) de su sitio para uso temporal. Por ejemplo, podría configurar una versión concreta de su sitio Web en una máquina virtual de Azure o en hello ensayo ranura en un sitio Web toorun un conjunto de pruebas, reproducir un error, realizar una corrección de errores, probar un cambio propuesto o configurar un entorno personalizado para una demostración o presentación. Después de crear un script que publique su proyecto, puede volver a crear entornos idénticos volviendo a ejecutar script de Hola según sea necesario, o ejecutar script de Hola con su propia compilación de su toocreate de aplicación web de un entorno de pruebas personalizado.

## <a name="what-you-need"></a>Lo que necesita
* SDK de Azure 2.3 o posterior. Vea [Descargas de Visual Studio](http://go.microsoft.com/fwlink/?LinkID=624384) para obtener más información.

No es necesario secuencias de comandos de hello Azure SDK toogenerate Hola para proyectos web. Esta característica es para proyectos web, no para los roles web de servicios en la nube.

* Azure PowerShell 0.7.4 o posterior. Vea [cómo tooinstall y configurar Azure PowerShell](/powershell/azure/overview) para obtener más información.
* [Windows PowerShell 3.0](http://go.microsoft.com/?linkid=9811175) o posterior.

## <a name="additional-tools"></a>Herramientas adicionales
Tiene a su disposición herramientas y recursos adicionales para trabajar con PowerShell en Visual Studio para el desarrollo de Azure. Vea [Herramientas de PowerShell para Visual Studio](http://go.microsoft.com/fwlink/?LinkId=404012).

## <a name="generating-hello-publish-scripts"></a>Hola de generar scripts de publicación
Puede generar Hola scripts de publicación para una máquina virtual que hospeda el sitio Web cuando se crea un nuevo proyecto siguiendo [estas instrucciones](virtual-machines/windows/classic/web-app-visual-studio.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json). También puede [generar scripts de publicación para aplicaciones web en Azure App Service](app-service-web/app-service-web-get-started-dotnet.md).

## <a name="scripts-that-visual-studio-generates"></a>Scripts que genera Visual Studio
Visual Studio genera una carpeta de nivel de solución denominada **PublishScripts** que contiene dos archivos de Windows PowerShell, un script de publicación de la máquina virtual o sitio Web y un módulo que contiene funciones que puede usar en hello secuencias de comandos. Visual Studio también genera un archivo en formato JSON de Hola que especifica los detalles de hello del proyecto de Hola que va a implementar.

### <a name="windows-powershell-publish-script"></a>Script de publicación de Windows PowerShell
script de publicación de Hello contiene específico publicar los pasos para implementar la máquina virtual o sitio Web de tooa. Visual Studio ofrece color de sintaxis para el desarrollo de Windows PowerShell. Ayuda para las funciones hello está disponible y puede editarlas libremente las funciones hello en hello script toosuit sus distintas necesidades.

### <a name="windows-powershell-module"></a>Módulo de Windows PowerShell
Windows PowerShell módulo que genera Visual Studio contiene funciones que Hola Hola publicar de script se utiliza. Estas son funciones de PowerShell de Azure y no son toobe previsto modificado. Vea [cómo tooinstall y configurar Azure PowerShell](/powershell/azure/overview) para obtener más información.

### <a name="json-configuration-file"></a>Archivo de configuración de JSON
se crea el archivo JSON de Hola Hola **configuraciones** carpeta y contiene los datos de configuración que especifica exactamente qué tooAzure toodeploy de recursos. Hola de archivo hello que genera Visual Studio se denomina proyecto-nombre-WAWS-dev.json si ha creado un sitio Web o proyecto nombre-VM-dev.json si ha creado una máquina virtual. Este es un ejemplo de un archivo de configuración de JSON que se genera al crear un sitio web. La mayoría de los valores de hello es autoexplicativo. nombre del sitio Web de Hello lo genera Azure, por lo que quizás no coincida con el nombre del proyecto.

```json
{
    "environmentSettings": {
        "webSite": {
            "name": "WebApplication26632",
            "location": "West US"
        },
        "databases": [{
            "connectionStringName": "DefaultConnection",
            "databaseName": "WebApplication26632_db",
            "serverName": "YourDatabaseServerName",
            "user": "sqluser2",
            "password": "",
            "edition": "",
            "size": "",
            "collation": "",
            "location": "West US"
        }]
    }
}
```
Cuando se crea una máquina virtual, archivo de configuración de JSON de hello parece similar siguiente toohello. Tenga en cuenta que un servicio de nube se crea como un contenedor para la máquina virtual de Hola. máquina virtual de Hello contiene extremos habituales de hello para el acceso web a través de HTTP y HTTPS, así como los extremos de Web Deploy, que permite publicar el sitio Web de toohello desde el equipo local, escritorio remoto y Windows PowerShell.

```json
{
    "environmentSettings": {
        "cloudService": {
            "name": "myusernamevm1",
            "affinityGroup": "",
            "location": "West US",
            "virtualNetwork": "",
            "subnet": "",
            "availabilitySet": "",
            "virtualMachine": {
                "name": "myusernamevm1",
                "vhdImage": "a699494373c04fc0bc8f2bb1389d6106__Win2K8R2SP1-Datacenter-201403.01-en.us-127GB.vhd",
                "size": "Small",
                "user": "vmuser1",
                "password": "",
                "enableWebDeployExtension": true,
                "endpoints": [{
                        "name": "Http",
                        "protocol": "TCP",
                        "publicPort": "80",
                        "privatePort": "80"
                    },
                    {
                        "name": "Https",
                        "protocol": "TCP",
                        "publicPort": "443",
                        "privatePort": "443"
                    },
                    {
                        "name": "WebDeploy",
                        "protocol": "TCP",
                        "publicPort": "8172",
                        "privatePort": "8172"
                    },
                    {
                        "name": "Remote Desktop",
                        "protocol": "TCP",
                        "publicPort": "3389",
                        "privatePort": "3389"
                    },
                    {
                        "name": "Powershell",
                        "protocol": "TCP",
                        "publicPort": "5986",
                        "privatePort": "5986"
                    }
                ]
            }
        },
        "databases": [{
            "connectionStringName": "",
            "databaseName": "",
            "serverName": "",
            "user": "",
            "password": ""
        }],
        "webDeployParameters": {
            "iisWebApplicationName": "Default Web Site"
        }
    }
}
```

Puede editar Hola JSON configuración toochange lo que sucede al ejecutar Hola scripts de publicación. Hola `cloudService` y `virtualMachine` secciones resultan necesarias, pero se puede eliminar hello `databases` sección si no lo necesita. propiedades de Hola que están vacías en el archivo de configuración predeterminado de Hola que genera Visual Studio son opcionales; los que tienen valores en el archivo de configuración predeterminado de hello son necesarios.

Si tiene un sitio Web con varios entornos de implementación (conocidos como espacios) en lugar de un único sitio de producción en Azure, puede incluir nombre de la ranura de hello en nombre de hello del sitio Web de hello en el archivo de configuración de JSON de Hola. Por ejemplo, si tiene un sitio Web que se denomina **misitio** y un espacio llamado **probar** , a continuación, Hola URI es misitio test.cloudapp.net, pero toouse nombre correcto de hello en el archivo de configuración de hello es mysite (Test) . Sólo puede hacerlo si las ranuras y sitio Web de hello ya existen en la suscripción. Si no existen, crear sitio Web de hello mediante la ejecución de script de Hola sin especificar la ranura de Hola y luego crear ranura Hola Hola [portal de Azure clásico](http://go.microsoft.com/fwlink/?LinkID=213885), y posteriormente, ejecute el script de Hola con el nombre de sitio Web modificado Hola. Para más información sobre las ranuras de implementación para las aplicaciones web, consulte [Configuración de entornos de ensayo para aplicaciones web en Azure App Service](app-service-web/web-sites-staged-publishing.md).

## <a name="how-toorun-hello-publish-scripts"></a>Cómo toorun Hola publicar scripts
Si nunca ha ejecutado un script de Windows PowerShell antes, debe establecer primero Hola ejecución directiva tooenable scripts toorun. Se trata de una seguridad característica tooprevent usuarios ejecuten scripts de Windows PowerShell si son vulnerable toomalware o virus que implican la ejecución de scripts.

### <a name="run-hello-script"></a>Ejecutar script de Hola
1. Crear paquete de Web Deploy de hello para el proyecto. Un paquete de Web Deploy es un archivo comprimido (.zip) que contienen archivos que desea que sitio Web de tooyour toocopy o una máquina virtual. Puede crear paquetes de implementación web en Visual Studio para cualquier aplicación web.

![Crear paquete de implementación web](./media/vs-azure-tools-publishing-using-powershell-scripts/IC767885.png)

Para obtener más información, vea [Cómo crear un paquete de implementación web en Visual Studio](https://msdn.microsoft.com/library/dd465323.aspx). También puede automatizar la creación de hello de su paquete de Web Deploy, tal y como se describe en la sección de hello **personalizar y extender Hola publican scripts** más adelante en este tema.

1. En **el Explorador de soluciones**, abra el menú contextual de Hola para script de Hola y, a continuación, elija **abrir con PowerShell ISE**.
2. Si se trata de hello primera vez que ejecuta scripts de Windows PowerShell en este equipo, abra una ventana de símbolo del sistema con privilegios de administrador y Hola de tipo siguiente comando:

    ```powershell
    Set-ExecutionPolicy RemoteSigned
    ```

3. Inicie sesión en tooAzure utilizando el siguiente comando de Hola.

    ```powershell
    Add-AzureAccount
    ```

    Cuando se le solicite, escriba su nombre de usuario y su contraseña.

    Tenga en cuenta que cuando automatiza el script de Hola, este método para proporcionar las credenciales de Azure no funcionará. En su lugar, debe usar las credenciales de hello .publishsettings archivos tooprovide. Una vez únicamente, use comandos de hello **Get-AzurePublishSettingsFile** hello toodownload de archivos de Azure y, posteriormente, use **importación-AzurePublishSettingsFile** archivo de hello tooimport. Para obtener instrucciones detalladas, consulte [cómo tooinstall y configurar Azure PowerShell](/powershell/azure/overview).

4. (Opcional) Si desea que toocreate Azure recursos como Hola virtual machine, base de datos y sitios Web sin publicar la aplicación web, utilizan hello **Publish-WebApplication.ps1** comando con hello **-configuración** establecido toohello archivo de configuración de JSON. Esta línea de comandos usa toodetermine del archivo de configuración de hello JSON que toocreate de recursos. Porque utiliza la configuración predeterminada de Hola para otros argumentos de línea de comandos, crea recursos de hello, pero no publica la aplicación web. Hello: opción detallada proporciona más información sobre lo que está sucediendo.

    ```powershell
    Publish-WebApplication.ps1 -Verbose –Configuration C:\Path\WebProject-WAWS-dev.json
    ```

5. Hola de uso **Publish-WebApplication.ps1** comando tal como se muestra en uno de la siguiente secuencia de comandos de ejemplos tooinvoke Hola de Hola y publicar la aplicación web. Si necesita toooverride Hola una configuración predeterminada para cualquiera de Hola otros argumentos, como el nombre de la suscripción de Hola, nombre del paquete, las credenciales de la máquina virtual o las credenciales del servidor de base de datos de publicación, puede especificar esos parámetros. Hola de uso **– Verbose** opción toosee obtener más información sobre el progreso de Hola de hello proceso de publicación.

    ```powershell
    Publish-WebApplication.ps1 –Configuration C:\Path\WebProject-WAWS-dev-json `
    –SubscriptionName Contoso `
    -WebDeployPackage C:\Documents\Azure\ADWebApp.zip `
    -DatabaseServerPassword @{Name="dbServerName";Password="adminPassword"} `
    -Verbose
    ```

    Si va a crear una máquina virtual, comando Hola Hola siguiente aspecto. Este ejemplo también muestra cómo toospecify hello las credenciales para varias bases de datos. Para las máquinas virtuales de Hola que crean estos scripts, certificado SSL de hello no es de una entidad emisora raíz de confianza. Por lo tanto, debe hello toouse **– AllowUntrusted** opción.

    ```powershell
    Publish-WebApplication.ps1 `
    -Configuration C:\Path\ADVM-VM-test.json `
    -SubscriptionName Contoso `
    -WebDeployPackage C:\Path\ADVM.zip `
    -AllowUntrusted `
    -VMPassword @{name = "vmUserName"; password = "YourPasswordHere"} `
    -DatabaseServerPassword @{Name="server1";Password="adminPassword1"}, @{Name="server2";Password="adminPassword2"} `
    -Verbose
    ```

    script de Hola puede crear bases de datos, pero no crea servidores de base de datos. Si desea que toocreate un servidor de base de datos, puede usar hello **New-AzureSqlDatabaseServer** función Hola módulo de Azure.

## <a name="customizing-and-extending-hello-publish-scripts"></a>Personalizar y ampliar Hola publican scripts
Puede personalizar Hola publicar script y el archivo de configuración de JSON. Hola funciones de módulo de Windows PowerShell de hello **AzureWebAppPublishModule.psm1** no está previsto toobe modificado. Si solo desea toospecify otra base de datos o cambiar algunas de las propiedades de Hola de máquina virtual de hello, edite el archivo de configuración de JSON de Hola. Si desea tooextend Hola de hello script tooautomate compilar y probar el proyecto, puede implementar códigos auxiliares de función en **Publish-WebApplication.ps1**.

tooautomate compilar el proyecto, agregue código que llame a MSBuild demasiado`New-WebDeployPackage` tal y como se muestra en este ejemplo de código. Hola ruta de acceso toohello comando MSBuild es diferente según la versión de Hola de Visual Studio que tenga instalada. ruta de acceso correcta de tooget hello, puede usar la función hello **Get-MSBuildCmd**, tal y como se muestra en este ejemplo.

### <a name="tooautomate-building-your-project"></a>tooautomate compilar el proyecto
1. Agregar hello `$ProjectFile` parámetro en la sección de parámetros globales de Hola.

    ```powershell
    [Parameter(Mandatory = $false)]
    [ValidateScript({Test-Path $_ -PathType Leaf})]
    [String]
    $ProjectFile,
    ```

2. Copiar función hello `Get-MSBuildCmd` en el archivo de script.

    ```powershell
    function Get-MSBuildCmd
    {
            process
    {

                $path =  Get-ChildItem "HKLM:\SOFTWARE\Microsoft\MSBuild\ToolsVersions\" |
                                    Sort-Object {[double]$_.PSChildName} -Descending |
                                    Select-Object -First 1 |
                                    Get-ItemProperty -Name MSBuildToolsPath |
                                    Select -ExpandProperty MSBuildToolsPath

                $path = (Join-Path -Path $path -ChildPath 'msbuild.exe')

            return Get-Item $path
        }
    }
    ```

3. Reemplace `New-WebDeployPackage` con hello código siguiente y reemplace los marcadores de posición de hello en la creación de la línea de hello `$msbuildCmd`. Este código es para Visual Studio 2015. Si está utilizando Visual Studio 2013, cambie hello **VisualStudioVersion** la propiedad siguiente demasiado`12.0`.

    ```powershell
    function New-WebDeployPackage
    {
        #Write a function toobuild and package your web application
    ```

    toobuild su aplicación web, use MsBuild.exe. Para obtener ayuda, consulte la referencia de la línea de comandos de MSBuild en: [http://go.microsoft.com/fwlink/?LinkId=391339](http://go.microsoft.com/fwlink/?LinkId=391339)

    ```powershell
    Write-VerboseWithTime 'Build-WebDeployPackage: Start'

    $msbuildCmd = '"{0}" "{1}" /T:Rebuild;Package /P:VisualStudioVersion=14.0 /p:OutputPath="{2}\MSBuildOutputPath" /flp:logfile=msbuild.log,v=d' -f (Get-MSBuildCmd), $ProjectFile, $scriptDirectory

    Write-VerboseWithTime ('Build-WebDeployPackage: ' + $msbuildCmd)
    ```

### <a name="start-execution-of-hello-build-command"></a>Inicia la ejecución del comando de generación de Hola

```powershell
$job = Start-Process cmd.exe -ArgumentList('/C "' + $msbuildCmd + '"') -WindowStyle Normal -Wait -PassThru

if ($job.ExitCode -ne 0) {
    throw('MsBuild exited with an error. ExitCode:' + $job.ExitCode)
}

#Obtain hello project name
$projectName = (Get-Item $ProjectFile).BaseName

#Construct hello path tooweb deploy zip package
$DeployPackageDir =  '.\MSBuildOutputPath\_PublishedWebsites\{0}_Package\{0}.zip' -f $projectName

#Get hello full path for hello web deploy zip package. This is required for MSDeploy toowork
$WebDeployPackage = Resolve-Path –LiteralPath $DeployPackageDir

Write-VerboseWithTime 'Build-WebDeployPackage: End'

return $WebDeployPackage
}
```

1. Llamar a hello `New-WebDeployPackage` función antes de esta línea: `$Config = Read-ConfigFile $Configuration` para las aplicaciones web o `$Config = Read-ConfigFile $Configuration -HasWebDeployPackage:([Bool]$WebDeployPackage)` para las máquinas virtuales.

    ```powershell
    if($ProjectFile)
    {
    $WebDeployPackage = New-WebDeployPackage
    }
    ```

2. Invocar el script de Hola personalizado desde la línea de comandos mediante el paso de Hola `$Project` argumento, como en la siguiente línea de comandos de ejemplo de Hola.

    ```powershell
    .\Publish-WebApplicationVM.ps1 -Configuration .\Configurations\WebApplication5-VM-dev.json `
    -ProjectFile ..\WebApplication5\WebApplication5.csproj `
    -VMPassword @{Name="VMUser";Password="Test.123"} `
    -AllowUntrusted `
    -Verbose
    ```

    tooautomate pruebas de la aplicación, agregue código demasiado`Test-WebApplication`. Estar seguro de toouncomment líneas de hello en **Publish-WebApplication.ps1** donde se llaman a estas funciones. Si no proporciona una implementación, puede crear manualmente el proyecto con Visual Studio y, a continuación, ejecución Hola publicar script toopublish tooAzure.

## <a name="publishing-function-summary"></a>Publicación del resumen de la función
Ayuda de tooget para las funciones que puede usar en línea de comandos de Windows PowerShell de hello, use el comando de hello `Get-Help function-name`. Ayuda de Hello incluye la ayuda sobre parámetros y ejemplos. Hola mismo texto de ayuda también está en archivos de origen de la secuencia de comandos de hello, **AzureWebAppPublishModule.psm1** y **Publish-WebApplication.ps1**. Ayuda y script de Hola está localizado en el idioma de Visual Studio.

**AzureWebAppPublishModule**

| Nombre de función | Description |
| --- | --- |
| Add-AzureSQLDatabase |Crea una nueva base de datos SQL de Azure. |
| Add-AzureSQLDatabases |Crea las bases de datos de SQL Azure a partir de valores de hello en el archivo de configuración de JSON de Hola que genera Visual Studio. |
| Add-AzureVM |Crea una máquina virtual de Azure y devuelve la que dirección URL de Hola de hello implementa VM. Hello función configura los requisitos previos de hello y, a continuación, Hola llamadas **New-AzureVM** función toocreate (módulo de Azure) una nueva máquina virtual. |
| Add-AzureVMEndpoints |Agrega la nueva máquina virtual de tooa los extremos de entrada y devuelve la máquina virtual de hello con nuevo extremo de Hola. |
| Add-AzureVMStorage |Crea una nueva cuenta de almacenamiento de Azure en la suscripción actual de Hola. nombre de Hola de cuenta de hello comienza por "devtest" seguido de una cadena alfanumérica única. función Hello devuelve nombre de Hola de hello nueva cuenta de almacenamiento. Debe especificar una ubicación o un grupo de afinidad para la nueva cuenta de almacenamiento Hola. |
| Add-AzureWebsite |Crea un sitio Web con la ubicación y el nombre especificado de Hola. Esta función llama hello **New-AzureWebsite** función Hola módulo de Azure. Si la suscripción de hello ya no incluye un sitio Web con el nombre especificado de hello, esta función crea el sitio Web de Hola y devuelve un objeto de sitio Web. De lo contrario, devuelve `$null`. |
| Backup-Subscription |Guarda Hola suscripción de Azure actual en hello `$Script:originalSubscription` variable en el ámbito del script. Esta función guarda la suscripción actual de Azure hello (obtenida por `Get-AzureSubscription -Current`) y su cuenta de almacenamiento y Hola suscripción cambiada por este script (almacenada en la variable de hello `$UserSpecifiedSubscription`) y su cuenta de almacenamiento, en el ámbito del script. Al guardar los valores de hello, puede usar una función, como `Restore-Subscription`, toorestore Hola original suscripción y almacenamiento cuenta toocurrent estado actual si ha cambiado el estado actual de Hola. |
| Find-AzureVM |Hola obtiene especifica la máquina virtual de Azure. |
| Format-DevTestMessageWithTime |Antepone el mensaje de tooa de fecha y hora de saludo. Esta función está diseñada para mensajes escritos toohello flujos de Error y detallado. |
| Get-AzureSQLDatabaseConnectionString |Ensambla una base de datos de SQL Azure de conexión cadena tooconnect tooan. |
| Get-AzureVMStorage |Devuelve Hola nombre de cuenta de almacenamiento primera Hola con patrón de nombre de Hola "devtest*" (entre mayúsculas y minúsculas) Hola ubicación o la afinidad del grupo especificado. Si hello "devtest*" cuenta de almacenamiento no coincide con la ubicación de Hola o el grupo de afinidad, función hello pasa por alto. Debe especificar una ubicación o un grupo de afinidad. |
| Get-MSDeployCmd |Devuelve una herramienta de comando toorun hello MsDeploy.exe. |
| New-AzureVMEnvironment |Busca o crea una máquina virtual en la suscripción de Hola que coincide con los valores de hello en el archivo de configuración de JSON de Hola. |
| Publish-WebPackage |Utiliza MsDeploy.exe y un servidor web publican el paquete. ZIP archivo toodeploy recursos tooa el sitio Web. Esta función no genera ninguna salida. Si se produce un error en hello llamada tooMSDeploy.exe, función hello produce una excepción. tooget más detallados de salida, use hello **-Verbose** opción. |
| Publish-WebPackageToVM |Comprueba los valores de parámetro hello y, a continuación, llama a hello **Publish-WebPackage** función. |
| Read-ConfigFile |Valida el archivo de configuración de JSON de Hola y devuelve una tabla hash de valores seleccionados. |
| Restore-Subscription |Restablece la suscripción original de hello actual suscripción toohello. |
| Test-AzureModule |Devuelve `$true` si la versión del módulo de Azure de hello instalado es 0.7.4 o posterior. Devuelve `$false` si el módulo de hello no está instalado o tiene una versión anterior. Esta función no tiene parámetros. |
| Test-AzureModuleVersion |Devuelve `$true` si la versión de Hola de hello módulo de Azure es 0.7.4 o posterior. Devuelve `$false` si el módulo de hello no está instalado o tiene una versión anterior. Esta función no tiene parámetros. |
| Test-HttpsUrl |Convierte el objeto de hello entrada URL tooa System.Uri. Devuelve `$True` si Hola URL es absoluta y su esquema es https. Devuelve `$false` si hello es relativa, su esquema no es HTTPS o cadena de entrada de hello no puede ser la dirección URL de tooa convertido. |
| Test-Member |Devuelve `$true` si una propiedad o método es un miembro del objeto de Hola. De lo contrario, devuelve `$false`. |
| Write-ErrorWithTime |Escribe un mensaje de error prefijado con hello hora actual. Esta función llama hello **Format-DevTestMessageWithTime** tiempo de función tooprepend Hola antes de escribir la secuencia de Error de toohello de mensajes de Hola. |
| Write-HostWithTime |Escribe un programa de host de mensaje toohello (**Write-Host**) como prefijo Hola hora actual. efecto de Hello de la escritura de programa de host toohello varía. Mayoría de los programas que hospedan Windows PowerShell escribe estos mensajes toostandard salida. |
| Write-VerboseWithTime |Escribe un mensaje detallado prefijado con hello hora actual. Dado que llama **Write-Verbose**, mensajes de bienvenida muestra solo cuando se ejecuta el script de Hola con hello **detallado** parámetro o cuando Hola **VerbosePreference** preferencia es establecer demasiado**continuar**. |

**Publish-WebApplication**

| Nombre de función | Description |
| --- | --- |
| New-AzureWebApplicationEnvironment |Crea recursos de Azure, como un sitio web o una máquina virtual. |
| New-WebDeployPackage |Esta función no está implementada. Puede agregar comandos en esta función toobuild el proyecto. |
| Publish-AzureWebApplication |Publica un tooAzure de aplicación web. |
| Publish-WebApplication |Crea e implementa aplicaciones web, máquinas virtuales, bases de datos SQL y cuentas de almacenamiento para un proyecto web de Visual Studio. |
| Test-WebApplication |Esta función no está implementada. Puede agregar comandos en esta tootest de función de la aplicación. |

## <a name="next-steps"></a>Pasos siguientes
Más información acerca de los scripts de PowerShell leyendo [Scripting con Windows PowerShell](https://technet.microsoft.com/library/bb978526.aspx) y ver otras secuencias de comandos de PowerShell de Azure en hello [centro de scripts de](https://azure.microsoft.com/documentation/scripts/).
