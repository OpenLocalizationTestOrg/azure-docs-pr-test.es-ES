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
# <a name="passing-credentials-toohello-azure-dsc-extension-handler"></a><span data-ttu-id="c1930-103">Pasar el controlador de extensión de credenciales toohello DSC de Azure</span><span class="sxs-lookup"><span data-stu-id="c1930-103">Passing credentials toohello Azure DSC extension handler</span></span>
[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-both-include.md)]

<span data-ttu-id="c1930-104">Este artículo trata la extensión de configuración de estado deseado de Hola para Azure.</span><span class="sxs-lookup"><span data-stu-id="c1930-104">This article covers hello Desired State Configuration extension for Azure.</span></span> <span data-ttu-id="c1930-105">Información general sobre el controlador de extensión de hello DSC puede encontrarse en [controlador de extensión de configuración de estado deseado de Azure de introducción toohello](extensions-dsc-overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="c1930-105">An overview of hello DSC extension handler can be found at [Introduction toohello Azure Desired State Configuration extension handler](extensions-dsc-overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span> 

## <a name="passing-in-credentials"></a><span data-ttu-id="c1930-106">Transmisión de credenciales</span><span class="sxs-lookup"><span data-stu-id="c1930-106">Passing in credentials</span></span>
<span data-ttu-id="c1930-107">Como parte del proceso de configuración de hello, puede que necesite tooset las cuentas de usuario, obtener acceso a servicios o instalar un programa en un contexto de usuario.</span><span class="sxs-lookup"><span data-stu-id="c1930-107">As a part of hello configuration process, you may need tooset up user accounts, access services, or install a program in a user context.</span></span> <span data-ttu-id="c1930-108">toodo estas cosas, necesita credenciales de tooprovide.</span><span class="sxs-lookup"><span data-stu-id="c1930-108">toodo these things, you need tooprovide credentials.</span></span> 

<span data-ttu-id="c1930-109">DSC permite configuraciones con parámetros en la que las credenciales se pasan en configuración de Hola y almacenan de forma segura en los archivos MOF.</span><span class="sxs-lookup"><span data-stu-id="c1930-109">DSC allows for parameterized configurations in which credentials are passed into hello configuration and securely stored in MOF files.</span></span> <span data-ttu-id="c1930-110">Hola controlador de extensión de Azure simplifica la administración de credenciales al proporcionar la administración automática de certificados.</span><span class="sxs-lookup"><span data-stu-id="c1930-110">hello Azure Extension Handler simplifies credential management by providing automatic management of certificates.</span></span> 

<span data-ttu-id="c1930-111">Considere la posibilidad de hello siguiente secuencia de comandos de configuración de DSC que crea una cuenta de usuario local con la contraseña especificada hello:</span><span class="sxs-lookup"><span data-stu-id="c1930-111">Consider hello following DSC configuration script that creates a local user account with hello specified password:</span></span>

<span data-ttu-id="c1930-112">*user_configuration.ps1*</span><span class="sxs-lookup"><span data-stu-id="c1930-112">*user_configuration.ps1*</span></span>

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

<span data-ttu-id="c1930-113">Es importante tooinclude *nodo localhost* como parte de la configuración de Hola.</span><span class="sxs-lookup"><span data-stu-id="c1930-113">It is important tooinclude *node localhost* as part of hello configuration.</span></span> <span data-ttu-id="c1930-114">Si falta esta declaración, hello estos pasos no funcionan como controlador de extensión de hello específicamente busca la instrucción de host local del nodo de Hola.</span><span class="sxs-lookup"><span data-stu-id="c1930-114">If this statement is missing, hello following steps do not work as hello extension handler specifically looks for hello node localhost statement.</span></span> <span data-ttu-id="c1930-115">También es importante convertir el tipo de hello tooinclude *[PsCredential]*, tal y como credencial de hello extensión tooencrypt Hola desencadena este tipo específico.</span><span class="sxs-lookup"><span data-stu-id="c1930-115">It is also important tooinclude hello typecast *[PsCredential]*, as this specific type triggers hello extension tooencrypt hello credential.</span></span> 

<span data-ttu-id="c1930-116">Publicar este almacenamiento tooblob de secuencia de comandos:</span><span class="sxs-lookup"><span data-stu-id="c1930-116">Publish this script tooblob storage:</span></span>

`Publish-AzureVMDscConfiguration -ConfigurationPath .\user_configuration.ps1`

<span data-ttu-id="c1930-117">Establezca la extensión de DSC de Azure de Hola y proporcione las credenciales de hello:</span><span class="sxs-lookup"><span data-stu-id="c1930-117">Set hello Azure DSC extension and provide hello credential:</span></span>

```
$configurationName = "Main"
$configurationArguments = @{ Credential = Get-Credential }
$configurationArchive = "user_configuration.ps1.zip"
$vm = Get-AzureVM "example-1"

$vm = Set-AzureVMDSCExtension -VM $vm -ConfigurationArchive $configurationArchive 
-ConfigurationName $configurationName -ConfigurationArgument @configurationArguments

$vm | Update-AzureVM
```
## <a name="how-credentials-are-secured"></a><span data-ttu-id="c1930-118">¿Cómo se protegen las credenciales?</span><span class="sxs-lookup"><span data-stu-id="c1930-118">How credentials are secured</span></span>
<span data-ttu-id="c1930-119">Al ejecutar este código, se solicita una credencial.</span><span class="sxs-lookup"><span data-stu-id="c1930-119">Running this code prompts for a credential.</span></span> <span data-ttu-id="c1930-120">Una vez proporcionada, se almacena brevemente en la memoria.</span><span class="sxs-lookup"><span data-stu-id="c1930-120">Once it is provided, it is stored in memory briefly.</span></span> <span data-ttu-id="c1930-121">Cuando se publica con `Set-AzureVmDscExtension` cmdlet, se transmite a través de HTTPS toohello VM, donde Azure almacena cifrar en el disco, mediante certificados de máquina virtual local de Hola.</span><span class="sxs-lookup"><span data-stu-id="c1930-121">When it is published with `Set-AzureVmDscExtension` cmdlet, it is transmitted over HTTPS toohello VM, where Azure stores it encrypted on disk, using hello local VM certificate.</span></span> <span data-ttu-id="c1930-122">Es brevemente descifrado en memoria y volver a cifrar toopass lo tooDSC.</span><span class="sxs-lookup"><span data-stu-id="c1930-122">Then it is briefly decrypted in memory and re-encrypted toopass it tooDSC.</span></span>

<span data-ttu-id="c1930-123">Este comportamiento es diferente al [con configuraciones seguras sin controlador de extensión de hello](https://msdn.microsoft.com/powershell/dsc/securemof).</span><span class="sxs-lookup"><span data-stu-id="c1930-123">This behavior is different than [using secure configurations without hello extension handler](https://msdn.microsoft.com/powershell/dsc/securemof).</span></span> <span data-ttu-id="c1930-124">Hola entorno de Azure ofrece un datos de configuración de tootransmit de manera segura a través de certificados.</span><span class="sxs-lookup"><span data-stu-id="c1930-124">hello Azure environment gives a way tootransmit configuration data securely via certificates.</span></span> <span data-ttu-id="c1930-125">Cuando se utiliza el controlador de extensión de hello DSC, no hay ninguna necesidad tooprovide $CertificatePath o un $CertificateID / entrada $Thumbprint en ConfigurationData.</span><span class="sxs-lookup"><span data-stu-id="c1930-125">When using hello DSC extension handler, there is no need tooprovide $CertificatePath or a $CertificateID / $Thumbprint entry in ConfigurationData.</span></span>

## <a name="next-steps"></a><span data-ttu-id="c1930-126">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="c1930-126">Next steps</span></span>
<span data-ttu-id="c1930-127">Para obtener más información sobre el controlador de extensión de DSC de Azure de hello, consulte [controlador de extensión de configuración de estado deseado de Azure de introducción toohello](extensions-dsc-overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="c1930-127">For more information on hello Azure DSC extension handler, see [Introduction toohello Azure Desired State Configuration extension handler](extensions-dsc-overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span> 

<span data-ttu-id="c1930-128">Examinar hello [plantilla de administrador de recursos de Azure para la extensión de hello DSC](extensions-dsc-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="c1930-128">Examine hello [Azure Resource Manager template for hello DSC extension](extensions-dsc-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

<span data-ttu-id="c1930-129">Para obtener más información sobre PowerShell DSC, [visite el centro de documentación de PowerShell de hello](https://msdn.microsoft.com/powershell/dsc/overview).</span><span class="sxs-lookup"><span data-stu-id="c1930-129">For more information about PowerShell DSC, [visit hello PowerShell documentation center](https://msdn.microsoft.com/powershell/dsc/overview).</span></span> 

<span data-ttu-id="c1930-130">toofind funcionalidad adicional que puede administrar con PowerShell DSC, [examinar la Galería de PowerShell de hello](https://www.powershellgallery.com/packages?q=DscResource&x=0&y=0) más recursos de DSC.</span><span class="sxs-lookup"><span data-stu-id="c1930-130">toofind additional functionality you can manage with PowerShell DSC, [browse hello PowerShell gallery](https://www.powershellgallery.com/packages?q=DscResource&x=0&y=0) for more DSC resources.</span></span>

