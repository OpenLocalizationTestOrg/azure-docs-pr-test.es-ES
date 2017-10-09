---
title: aaaConnect tooAzure pila | Documentos de Microsoft
description: "Obtenga información acerca de cómo tooconnect la pila de Azure"
services: azure-stack
documentationcenter: 
author: SnehaGunda
manager: byronr
editor: 
ms.assetid: 3cebbfa6-819a-41e3-9f1b-14ca0a2aaba3
ms.service: azure-stack
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 08/22/2017
ms.author: sngun
ms.openlocfilehash: 8a940245fbcc8795d26b694df66824f0eb1dc3ea
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="connect-tooazure-stack"></a><span data-ttu-id="52582-103">Conectar tooAzure pila</span><span class="sxs-lookup"><span data-stu-id="52582-103">Connect tooAzure Stack</span></span>

<span data-ttu-id="52582-104">toomanage recursos, debe conectarse toohello Kit de desarrollo de pila de Azure.</span><span class="sxs-lookup"><span data-stu-id="52582-104">toomanage resources, you must connect toohello Azure Stack Development Kit.</span></span> <span data-ttu-id="52582-105">Este tema se detallan Hola los pasos necesarios kit de desarrollo de tooconnect toohello.</span><span class="sxs-lookup"><span data-stu-id="52582-105">This topic details hello steps required tooconnect toohello development kit.</span></span> <span data-ttu-id="52582-106">Puede usar cualquiera de las siguientes opciones de conexión de hello:</span><span class="sxs-lookup"><span data-stu-id="52582-106">You can use either of hello following connection options:</span></span>

* <span data-ttu-id="52582-107">[Escritorio remoto](#connect-with-remote-desktop): permite a los usuarios simultáneos único conectarse rápidamente desde el kit de desarrollo de Hola.</span><span class="sxs-lookup"><span data-stu-id="52582-107">[Remote Desktop](#connect-with-remote-desktop): lets a single concurrent user quickly connect from hello development kit.</span></span>
* <span data-ttu-id="52582-108">[Red privada virtual (VPN)](#connect-with-vpn): permite que varios usuarios simultáneos conectan desde los clientes fuera de la infraestructura de Azure pila hello (necesita la configuración).</span><span class="sxs-lookup"><span data-stu-id="52582-108">[Virtual Private Network (VPN)](#connect-with-vpn): lets multiple concurrent users connect from clients outside of hello Azure Stack infrastructure (requires configuration).</span></span>

## <a name="connect-tooazure-stack-with-remote-desktop"></a><span data-ttu-id="52582-109">Conectar tooAzure pila con Escritorio remoto</span><span class="sxs-lookup"><span data-stu-id="52582-109">Connect tooAzure Stack with Remote Desktop</span></span>
<span data-ttu-id="52582-110">Con una conexión a Escritorio remoto, un único usuario simultáneo puede trabajar con recursos de hello toomanage portal.</span><span class="sxs-lookup"><span data-stu-id="52582-110">With a Remote Desktop connection, a single concurrent user can work with hello portal toomanage resources.</span></span>

1. <span data-ttu-id="52582-111">Abra una conexión a Escritorio remoto y conéctese toohello kit de desarrollo.</span><span class="sxs-lookup"><span data-stu-id="52582-111">Open a Remote Desktop Connection and connect toohello development kit.</span></span> <span data-ttu-id="52582-112">Escriba **AzureStack\AzureStackAdmin** como nombre de usuario de Hola y contraseña administrativa Hola que proporcionó durante la instalación de la pila de Azure.</span><span class="sxs-lookup"><span data-stu-id="52582-112">Enter **AzureStack\AzureStackAdmin** as hello username, and hello administrative password that you provided during Azure Stack setup.</span></span>  

2. <span data-ttu-id="52582-113">En el equipo de kit de desarrollo de hello, abra Administrador del servidor, haga clic en **servidor Local**, desactive la opción de seguridad mejorada de Internet Explorer y, a continuación, cierre el administrador del servidor.</span><span class="sxs-lookup"><span data-stu-id="52582-113">From hello development kit computer, open Server Manager, click **Local Server**, turn off Internet Explorer Enhanced Security, and then close Server Manager.</span></span>

3. <span data-ttu-id="52582-114">usuario de hello tooopen [portal](azure-stack-key-features.md#portal), navegue demasiado (https://portal.local.azurestack.external/) e inicie sesión con las credenciales de usuario.</span><span class="sxs-lookup"><span data-stu-id="52582-114">tooopen hello user [portal](azure-stack-key-features.md#portal), navigate too(https://portal.local.azurestack.external/) and sign in using user credentials.</span></span> <span data-ttu-id="52582-115">Administrador de hello tooopen [portal](azure-stack-key-features.md#portal), navegue demasiado (https://adminportal.local.azurestack.external/) y Hola de inicio de sesión utilizando credenciales de Azure Active Directory especificadas durante la instalación.</span><span class="sxs-lookup"><span data-stu-id="52582-115">tooopen hello administrator [portal](azure-stack-key-features.md#portal), navigate too(https://adminportal.local.azurestack.external/) and sign in using hello Azure Active Directory credentials specified during installation.</span></span>

## <a name="connect-tooazure-stack-with-vpn"></a><span data-ttu-id="52582-116">Conectar tooAzure pila con VPN</span><span class="sxs-lookup"><span data-stu-id="52582-116">Connect tooAzure Stack with VPN</span></span>

<span data-ttu-id="52582-117">Puede establecer una tooan de conexión de red privada Virtual (VPN) de túnel dividido Kit de desarrollo de pila de Azure.</span><span class="sxs-lookup"><span data-stu-id="52582-117">You can establish a split tunnel Virtual Private Network (VPN) connection tooan Azure Stack Development Kit.</span></span> <span data-ttu-id="52582-118">A través de hello conexión VPN, puede acceder al portal de administrador de hello, portal de usuarios y herramientas como Visual Studio y recursos de pila de Azure PowerShell toomanage, instalado localmente.</span><span class="sxs-lookup"><span data-stu-id="52582-118">Through hello VPN connection, you can access hello administrator portal, user portal, and locally installed tools such as Visual Studio and PowerShell toomanage Azure Stack resources.</span></span> <span data-ttu-id="52582-119">Se admite la conectividad VPN en implementaciones basadas en Azure Active Directory (AAD) y en los Servicios de federación de Active Directory (AD FS).</span><span class="sxs-lookup"><span data-stu-id="52582-119">VPN connectivity is supported in both Azure Active Directory(AAD) and Active Directory Federation Services(AD FS) based deployments.</span></span> <span data-ttu-id="52582-120">Las conexiones VPN permiten a varios clientes tooconnect tooAzure pila en hello mismo tiempo.</span><span class="sxs-lookup"><span data-stu-id="52582-120">VPN connections enable multiple clients tooconnect tooAzure Stack at hello same time.</span></span> 

> [!NOTE] 
> <span data-ttu-id="52582-121">Esta conexión VPN no proporciona la infraestructura de pila conectividad tooAzure de máquinas virtuales.</span><span class="sxs-lookup"><span data-stu-id="52582-121">This VPN connection does not provide connectivity tooAzure Stack infrastructure VMs.</span></span> 

### <a name="prerequisites"></a><span data-ttu-id="52582-122">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="52582-122">Prerequisites</span></span>

* <span data-ttu-id="52582-123">Instale [Azure PowerShell compatible con Azure Stack](azure-stack-powershell-install.md) en el equipo local.</span><span class="sxs-lookup"><span data-stu-id="52582-123">Install [Azure Stack compatible Azure PowerShell](azure-stack-powershell-install.md) on your local computer.</span></span>  
* <span data-ttu-id="52582-124">Descargar hello [toowork necesarios de herramientas con la pila de Azure](azure-stack-powershell-download.md).</span><span class="sxs-lookup"><span data-stu-id="52582-124">Download hello [tools required toowork with Azure Stack](azure-stack-powershell-download.md).</span></span> 

### <a name="configure-vpn-connectivity"></a><span data-ttu-id="52582-125">Configuración de la conectividad VPN</span><span class="sxs-lookup"><span data-stu-id="52582-125">Configure VPN connectivity</span></span>

<span data-ttu-id="52582-126">toocreate un kit de desarrollo de toohello de conexión VPN, abra una sesión de PowerShell con privilegios elevados desde el equipo local basado en Windows y ejecución Hola siguiente secuencia de comandos (asegúrese de tooupdate seguro Hola Hola IP dirección y la contraseña valores para su entorno):</span><span class="sxs-lookup"><span data-stu-id="52582-126">toocreate a VPN connection toohello development kit, open an elevated PowerShell session from your local Windows-based computer and run hello following script (make sure tooupdate hello hello IP address and password values for your environment):</span></span>

```PowerShell 
# Configure winrm if it's not already configured
winrm quickconfig  

Set-ExecutionPolicy RemoteSigned

# Import hello Connect module
Import-Module .\Connect\AzureStack.Connect.psm1 

# Add hello development kit computer’s host IP address & certificate authority (CA) toohello list of trusted hosts. Make sure tooupdate hello hello IP address and password values for your environment. 

$hostIP = "<Azure Stack host IP address>"

$Password = ConvertTo-SecureString `
  "<Administrator password provided when deploying Azure Stack>" `
  -AsPlainText `
  -Force

Set-Item wsman:\localhost\Client\TrustedHosts `
  -Value $hostIP `
  -Concatenate

# Create a VPN connection entry for hello local user
Add-AzsVpnConnection `
  -ServerAddress $hostIP `
  -Password $Password

```

<span data-ttu-id="52582-127">Si Hola configurar se realiza correctamente, debería ver **azurestack** en la lista de conexiones VPN.</span><span class="sxs-lookup"><span data-stu-id="52582-127">If hello set up succeeds, you should see **azurestack** in your list of VPN connections.</span></span>

![Conexiones de red](media/azure-stack-connect-azure-stack/image3.png)  

### <a name="connect-tooazure-stack"></a><span data-ttu-id="52582-129">Conectar tooAzure pila</span><span class="sxs-lookup"><span data-stu-id="52582-129">Connect tooAzure Stack</span></span>

<span data-ttu-id="52582-130">Conectar la instancia de la pila de Azure de toohello mediante el uso de hello siguiendo dos métodos:</span><span class="sxs-lookup"><span data-stu-id="52582-130">Connect toohello Azure Stack instance by using either of hello following two methods:</span></span>  

* <span data-ttu-id="52582-131">Mediante el uso de hello `Connect-AzsVpn ` comando:</span><span class="sxs-lookup"><span data-stu-id="52582-131">By using hello `Connect-AzsVpn ` command:</span></span> 
    
  ```PowerShell
  Connect-AzsVpn `
    -Password $Password
  ```

  <span data-ttu-id="52582-132">Cuando se le solicite, confiar hello Azure pila host e instalar certificado de Hola de **AzureStackCertificateAuthority** en el almacén de certificados del equipo local.</span><span class="sxs-lookup"><span data-stu-id="52582-132">When prompted, trust hello Azure Stack host and install hello certificate from **AzureStackCertificateAuthority** onto your local computer’s certificate store.</span></span> <span data-ttu-id="52582-133">(mensaje de Hola puede aparecer detrás de la ventana de sesión de PowerShell de hello).</span><span class="sxs-lookup"><span data-stu-id="52582-133">(hello prompt might appear behind hello PowerShell session window).</span></span> 

* <span data-ttu-id="52582-134">En el equipo local, abra **Configuración de red** > **VPN** > haga clic en **azurestack** > **Conectar**.</span><span class="sxs-lookup"><span data-stu-id="52582-134">Open your local computer’s **Network Settings** > **VPN** > click **azurestack** > **connect**.</span></span> <span data-ttu-id="52582-135">En hello inicio de sesión de símbolo del sistema, escriba Hola username (AzureStack\AzureStackAdmin) y la contraseña de Hola.</span><span class="sxs-lookup"><span data-stu-id="52582-135">At hello sign-in prompt, enter hello username (AzureStack\AzureStackAdmin) and hello password.</span></span>

### <a name="test-hello-vpn-connectivity"></a><span data-ttu-id="52582-136">Hola de prueba la conectividad VPN</span><span class="sxs-lookup"><span data-stu-id="52582-136">Test hello VPN connectivity</span></span>

<span data-ttu-id="52582-137">conexión de portal de hello tootest, abra un explorador de Internet y vaya portal de usuarios de hello tooeither (https://portal.local.azurestack.external/) o el portal de administrador de hello (https://adminportal.local.azurestack.external/), inicie sesión y crear recursos.</span><span class="sxs-lookup"><span data-stu-id="52582-137">tootest hello portal connection, open an Internet browser and navigate tooeither hello user portal (https://portal.local.azurestack.external/) or hello administrator portal (https://adminportal.local.azurestack.external/), sign in and create resources.</span></span>  

## <a name="next-steps"></a><span data-ttu-id="52582-138">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="52582-138">Next steps</span></span>

[<span data-ttu-id="52582-139">Hacer tooyour disponibles de máquinas virtuales que los usuarios de la pila de Azure</span><span class="sxs-lookup"><span data-stu-id="52582-139">Make virtual machines available tooyour Azure Stack users</span></span>](azure-stack-tutorial-tenant-vm.md)

