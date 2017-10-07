---
title: aaaPassing credenciales tooAzure con DSC | Documentos de Microsoft
description: "Información general sobre cómo pasar de forma segura credenciales tooAzure de máquinas virtuales con la configuración de estado deseado de PowerShell"
services: virtual-machines-windows
documentationcenter: 
author: zjalexander
manager: timlt
editor: 
tags: azure-service-management,azure-resource-manager
keywords: 
ms.assetid: ea76b7e8-b576-445a-8107-88ea2f3876b9
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: na
ms.date: 09/15/2016
ms.author: zachal
ms.openlocfilehash: 306ecd3fd481f49a0beca5052fc7531a52999330
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="passing-credentials-toohello-azure-dsc-extension-handler"></a>Pasar el controlador de extensión de credenciales toohello DSC de Azure
[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-both-include.md)]

Este artículo trata la extensión de configuración de estado deseado de Hola para Azure. Información general sobre el controlador de extensión de hello DSC puede encontrarse en [controlador de extensión de configuración de estado deseado de Azure de introducción toohello](extensions-dsc-overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json). 

## <a name="passing-in-credentials"></a>Transmisión de credenciales
Como parte del proceso de configuración de hello, puede que necesite tooset las cuentas de usuario, obtener acceso a servicios o instalar un programa en un contexto de usuario. toodo estas cosas, necesita credenciales de tooprovide. 

DSC permite configuraciones con parámetros en la que las credenciales se pasan en configuración de Hola y almacenan de forma segura en los archivos MOF. Hola controlador de extensión de Azure simplifica la administración de credenciales al proporcionar la administración automática de certificados. 

Considere la posibilidad de hello siguiente secuencia de comandos de configuración de DSC que crea una cuenta de usuario local con la contraseña especificada hello:

*user_configuration.ps1*

```
configuration Main
{
    param(
        [Parameter(Mandatory=$true)]
        [ValidateNotNullorEmpty()]
        [PSCredential]
        $Credential
    )    
    Node localhost {       
        User LocalUserAccount
        {
            Username = $Credential.UserName
            Password = $Credential
            Disabled = $false
            Ensure = "Present"
            FullName = "Local User Account"
            Description = "Local User Account"
            PasswordNeverExpires = $true
        } 
    }  
} 
```

Es importante tooinclude *nodo localhost* como parte de la configuración de Hola. Si falta esta declaración, hello estos pasos no funcionan como controlador de extensión de hello específicamente busca la instrucción de host local del nodo de Hola. También es importante convertir el tipo de hello tooinclude *[PsCredential]*, tal y como credencial de hello extensión tooencrypt Hola desencadena este tipo específico. 

Publicar este almacenamiento tooblob de secuencia de comandos:

`Publish-AzureVMDscConfiguration -ConfigurationPath .\user_configuration.ps1`

Establezca la extensión de DSC de Azure de Hola y proporcione las credenciales de hello:

```
$configurationName = "Main"
$configurationArguments = @{ Credential = Get-Credential }
$configurationArchive = "user_configuration.ps1.zip"
$vm = Get-AzureVM "example-1"

$vm = Set-AzureVMDSCExtension -VM $vm -ConfigurationArchive $configurationArchive 
-ConfigurationName $configurationName -ConfigurationArgument @configurationArguments

$vm | Update-AzureVM
```
## <a name="how-credentials-are-secured"></a>¿Cómo se protegen las credenciales?
Al ejecutar este código, se solicita una credencial. Una vez proporcionada, se almacena brevemente en la memoria. Cuando se publica con `Set-AzureVmDscExtension` cmdlet, se transmite a través de HTTPS toohello VM, donde Azure almacena cifrar en el disco, mediante certificados de máquina virtual local de Hola. Es brevemente descifrado en memoria y volver a cifrar toopass lo tooDSC.

Este comportamiento es diferente al [con configuraciones seguras sin controlador de extensión de hello](https://msdn.microsoft.com/powershell/dsc/securemof). Hola entorno de Azure ofrece un datos de configuración de tootransmit de manera segura a través de certificados. Cuando se utiliza el controlador de extensión de hello DSC, no hay ninguna necesidad tooprovide $CertificatePath o un $CertificateID / entrada $Thumbprint en ConfigurationData.

## <a name="next-steps"></a>Pasos siguientes
Para obtener más información sobre el controlador de extensión de DSC de Azure de hello, consulte [controlador de extensión de configuración de estado deseado de Azure de introducción toohello](extensions-dsc-overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json). 

Examinar hello [plantilla de administrador de recursos de Azure para la extensión de hello DSC](extensions-dsc-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).

Para obtener más información sobre PowerShell DSC, [visite el centro de documentación de PowerShell de hello](https://msdn.microsoft.com/powershell/dsc/overview). 

toofind funcionalidad adicional que puede administrar con PowerShell DSC, [examinar la Galería de PowerShell de hello](https://www.powershellgallery.com/packages?q=DscResource&x=0&y=0) más recursos de DSC.

