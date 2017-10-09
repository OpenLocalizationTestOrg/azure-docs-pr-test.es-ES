---
title: "aaaDesired la configuración de estado para información general de Azure | Documentos de Microsoft"
description: "Información general para usar el controlador de extensión de Microsoft Azure hello para la configuración de estado deseado de PowerShell. Incluidos los requisitos previos, arquitectura, cmdlets, etc."
services: virtual-machines-windows
documentationcenter: 
author: zjalexander
manager: timlt
editor: 
tags: azure-service-management,azure-resource-manager
keywords: 
ms.assetid: bbacbc93-1e7b-4611-a3ec-e3320641f9ba
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: na
ms.date: 01/09/2017
ms.author: zachal
ms.openlocfilehash: b0337a2f1124f35e5e40c1478bd7530427e59d44
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="introduction-toohello-azure-desired-state-configuration-extension-handler"></a>Controlador de extensión de configuración de estado deseado de Azure de introducción toohello
[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-both-include.md)]

Hola agente de máquina virtual de Azure y las extensiones asociadas forman parte del programa Hola a servicios de infraestructura de Microsoft Azure. Las extensiones de VM son componentes de software que amplían la funcionalidad de máquina virtual de Hola y simplifican varias operaciones de administración de máquinas virtuales. Por ejemplo, hello extensión VMAccess puede ser tooreset usa una contraseña de administrador u Hola Script personalizado extensión puede ser tooexecute usa un script de Hola máquina virtual.

Este artículo presenta Hola extensión de configuración de estado deseado (DSC) de PowerShell para máquinas virtuales de Azure como parte del SDK de Azure PowerShell Hola. Puede utilizar tooupload de cmdlets nuevos y aplicar una configuración de DSC de PowerShell en una máquina virtual de Azure habilitada con hello extensión de DSC de PowerShell. llamadas de extensión de DSC de PowerShell de Hello en hello tooenact de DSC de PowerShell reciben una configuración de DSC en hello máquina virtual. Esta funcionalidad también está disponible a través de hello portal de Azure.

## <a name="prerequisites"></a>Requisitos previos
**Equipo local** toointeract con Hola extensión de máquina virtual de Azure, necesita toouse cualquier portal de Azure de Hola u Hola SDK de Azure PowerShell. 

**Agente invitado** Hola VM de Azure que se configura mediante la configuración de hello DSC necesita toobe un sistema operativo que soporta Windows Management Framework (WMF) 4.0 o 5.0. Hola lista completa de las versiones compatibles de sistema operativo puede encontrarse en hello [historial de versiones de extensión de DSC](https://blogs.msdn.microsoft.com/powershell/2014/11/20/release-history-for-the-azure-dsc-extension/).

## <a name="terms-and-concepts"></a>Términos y conceptos
Esta guía presupone que está familiarizado con los siguientes conceptos de hello:

Configuración: un documento de configuración de DSC. 

Nodo: un destino para una configuración de DSC. En este documento, "node" siempre hace referencia tooan máquina virtual de Azure.

Datos de configuración: un archivo .psd1 que contiene datos del entorno de una configuración

## <a name="architectural-overview"></a>Información general acerca de la arquitectura
Hola extensión de DSC de Azure usa hello Azure VM Agent framework toodeliver, establecer e informar sobre las configuraciones de DSC que se ejecutan en máquinas virtuales de Azure. Hola extensión de DSC espera un archivo .zip que contiene al menos un documento de configuración y proporciona un conjunto de parámetros a través de hello SDK de Azure PowerShell u Hola portal de Azure.

Cuando se llama a la extensión de Hola para hello primera vez, se ejecuta un proceso de instalación. Este proceso instala una versión de Hola Windows Management Framework (WMF) mediante Hola siguiendo la lógica:

1. Si hello SO de la máquina virtual de Azure es Windows Server 2016, se realiza ninguna acción. Windows Server 2016 ya tiene la versión más reciente de Hola de PowerShell instalado.
2. Si hello `wmfVersion` se especifica la propiedad, esa versión de hello WMF se instalará a menos que no es compatible con un sistema operativo de la máquina virtual de Hola.
3. Si no hay ningún `wmfVersion` propiedad se especifica, se instala Hola última versión concreta de hello WMF.

Instalación de hello WMF requiere un reinicio. Después del reinicio, extensión de hello descargas de archivo .zip de hello especificado en hello `modulesUrl` propiedad. Si esta ubicación está en almacenamiento de blobs de Azure, se puede especificar un token de SAS en hello `sasToken` tooaccess propiedad Hola archivo. Después de hello .zip se descarga y desempaquetar, Hola definido en función de la configuración `configurationFunction` se ejecuta el archivo MOF de toogenerate Hola. a continuación, se ejecuta la extensión de Hello `Start-DscConfiguration -Force` de archivo MOF de hello generado. extensión de Hello captura el resultado y lo escribe volver toohello canal de estado de Azure. Desde este punto, Hola LCM de DSC controla la supervisión y la corrección de forma habitual. 

## <a name="powershell-cmdlets"></a>Cmdlets de PowerShell
Cmdlets de PowerShell puede usarse con el Administrador de recursos de Azure u Hola toopackage de modelo de implementación clásica, publicar y supervisar las implementaciones de extensión de DSC. Hello siguientes cmdlets figuran aquí son módulos de implementación clásica de hello, pero "Azure" puede reemplazarse con el modelo de "AzureRm" toouse hello Azure Resource Manager. Por ejemplo, `Publish-AzureVMDscConfiguration` usa Hola modelo de implementación clásico, donde `Publish-AzureRmVMDscConfiguration` usa Azure Resource Manager. 

`Publish-AzureVMDscConfiguration`toma un archivo de configuración, busca los recursos DSC dependientes y crea un archivo .zip que contiene la configuración de Hola y configuración de Hola de tooenact necesaria de recursos de DSC. También puede crear paquete de hello localmente mediante hello `-ConfigurationArchivePath` parámetro. De lo contrario, publica el almacenamiento de blobs de hello .zip archivo tooAzure y lo protege con un token de SAS.

archivo .zip de Hello creado por este cmdlet tiene el script de configuración de Hola. ps1 en raíz de Hola de carpeta para archivar faxes Hola. Los recursos tienen carpeta del módulo de hello coloca en la carpeta para archivar faxes Hola. 

`Set-AzureVMDscExtension`Inserta la configuración de Hola que necesita Hola extensión de DSC de PowerShell en un objeto de configuración de máquina virtual. En el modelo de implementación clásica de hello, los cambios VM de hello deben tener aplicado tooan máquina virtual de Azure con `Update-AzureVM`. 

`Get-AzureVMDscExtension`Recupera el estado de extensión de DSC Hola de una máquina virtual concreta. 

`Get-AzureVMDscExtensionStatus`Recupera el estado de Hola de configuración de DSC de hello establecida por el controlador de extensión de DSC de Hola. Esta acción puede realizarse en una sola máquina virtual o en un grupo de máquinas virtuales.

`Remove-AzureVMDscExtension`Quita el controlador de extensión de Hola de una máquina virtual dada. Este cmdlet no hace **no** quitar la configuración de hello, desinstalar Hola WMF o cambiar la configuración de hello aplicado en la máquina virtual de Hola. Solo se quita el controlador de extensión de Hola. 

**Principales diferencias clave en los cmdlets de ASM y Azure Resource Manager**

* Los cmdlets de Azure Resource Manager son sincrónicos. Los cmdlets de ASM son asincrónicos.
* ResourceGroupName, VMName, ArchiveStorageAccountName, Version y Location son todos parámetros necesarios en Azure Resource Manager.
* ArchiveResourceGroupName es un nuevo parámetro opcional de Azure Resource Manager. Puede especificar este parámetro cuando la cuenta de almacenamiento pertenece tooa otro grupo de recursos que Hola uno donde se crea la máquina virtual de Hola.
* ConfigurationArchive se denomina ArchiveBlobName en Azure Resource Manager
* ContainerName se denomina ArchiveContainerName en Azure Resource Manager
* StorageEndpointSuffix se denomina ArchiveStorageEndpointSuffix en Azure Resource Manager
* conmutador de actualización automática de Hola se ha agregado tooAzure tooenable de administrador de recursos de hello extensión controlador toohello versión más reciente como y cuando esté disponible la actualización automática. Tenga en cuenta que este parámetro no tiene reinicios toocause potencial de hello en hello VM cuando hay una nueva versión de hello que WMF se libera. 

## <a name="azure-portal-functionality"></a>Funcionalidad del Portal de Azure
Examinar tooa máquina virtual. En Configuración -> General, haga clic en "Extensiones". Se crea un nuevo panel. Haga clic en "Agregar" y seleccione DSC de PowerShell.

portal de Hello necesita entrada.
**Script o módulos de configuración**: este campo es obligatorio. Requiere un archivo. ps1, que contiene un script de configuración o un archivo .zip con un script de configuración. ps1 en raíz de Hola y todos los recursos dependientes en carpetas de módulo dentro de .zip Hola. Pueden crearse con hello `Publish-AzureVMDscConfiguration -ConfigurationArchivePath` cmdlet incluido en hello SDK de Azure PowerShell. archivo de .zip Hola se carga en el almacenamiento de blobs de usuario protegido por un token de SAS. 

**Archivo PSD1 de datos de configuración**: este campo es opcional. Si la configuración requiere un archivo de datos de configuración en. psd1, utilice este campo tooselect y la carga de almacenamiento de blobs de usuario de tooyour, donde se está protegida por un token de SAS. 

**Nombre completo del módulo de configuración**: los archivos .ps1 pueden tener varias funciones de configuración. Escriba Hola nombre de script. ps1 de configuración de hello seguido por un '\' y el nombre de Hola de función de la configuración de Hola. Por ejemplo, si el script. ps1 tiene nombre hello "configuration.ps1" y configuración de hello es "IisInstall", escriba:`configuration.ps1\IisInstall`

**Argumentos de configuración**: si la función de la configuración de hello tiene argumentos, escriba aquí en formato de hello `argumentName1=value1,argumentName2=value2`. Tenga en cuenta que se trata de un formato distinto a cómo se aceptan argumentos de configuración a través de los cmdlets de PowerShell o las plantillas de Resource Manager. 

## <a name="getting-started"></a>Introducción
Hola extensión de DSC de Azure se toma en documentos de configuración de DSC y aplica a ellos en máquinas virtuales de Azure. A continuación encontrará un ejemplo sencillo de una configuración. Guárdelo localmente como "IisInstall.ps1":

```powershell
configuration IISInstall 
{ 
    node "localhost"
    { 
        WindowsFeature IIS 
        { 
            Ensure = "Present" 
            Name = "Web-Server"                       
        } 
    } 
}
```

Hola seguir pasos lugar hello IisInstall.ps1 script de Hola había especificado VM, ejecutamos configuración hello e informar sobre el estado.
###<a name="classic-model"></a>Modelo clásico
```powershell
#Azure PowerShell cmdlets are required
Import-Module Azure

#Use an existing Azure Virtual Machine, 'DscDemo1'
$demoVM = Get-AzureVM DscDemo1

#Publish hello configuration script into user storage.
Publish-AzureVMDscConfiguration -ConfigurationPath ".\IisInstall.ps1" -StorageContext $storageContext -Verbose -Force

#Set hello VM toorun hello DSC configuration
Set-AzureVMDscExtension -VM $demoVM -ConfigurationArchive "IisInstall.ps1.zip" -StorageContext $storageContext -ConfigurationName "IisInstall" -Verbose

#Update hello configuration of an Azure Virtual Machine
$demoVM | Update-AzureVM -Verbose

#check on status
Get-AzureVMDscExtensionStatus -VM $demovm -Verbose
```
###<a name="azure-resource-manager-model"></a>Modelo de Azure Resource Manager

```powershell
$resourceGroup = "dscVmDemo"
$location = "westus"
$vmName = "myVM"
$storageName = "demostorage"
#Publish hello configuration script into user storage
Publish-AzureRmVMDscConfiguration -ConfigurationPath .\iisInstall.ps1 -ResourceGroupName $resourceGroup -StorageAccountName $storageName -force
#Set hello VM toorun hello DSC configuration
Set-AzureRmVmDscExtension -Version 2.21 -ResourceGroupName $resourceGroup -VMName $vmName -ArchiveStorageAccountName $storageName -ArchiveBlobName iisInstall.ps1.zip -AutoUpdate:$true -ConfigurationName "IISInstall"

```

## <a name="logging"></a>Registro
Los registros se colocan en:

C:\WindowsAzure\Logs\Plugins\Microsoft.Powershell.DSC\[número de versión]

## <a name="next-steps"></a>Pasos siguientes
Para obtener más información sobre PowerShell DSC, [visite el centro de documentación de PowerShell de hello](https://msdn.microsoft.com/powershell/dsc/overview). 

Examinar hello [plantilla de administrador de recursos de Azure para la extensión de hello DSC](extensions-dsc-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json). 

toofind funcionalidad adicional que puede administrar con PowerShell DSC, [examinar la Galería de PowerShell de hello](https://www.powershellgallery.com/packages?q=DscResource&x=0&y=0) más recursos de DSC.

Para obtener más información sobre cómo pasar los parámetros confidenciales a las configuraciones, vea [administrar credenciales de forma segura con el controlador de extensión de hello DSC](extensions-dsc-credentials.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).

