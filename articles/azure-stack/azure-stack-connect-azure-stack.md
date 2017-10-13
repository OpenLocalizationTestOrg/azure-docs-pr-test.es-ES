---
title: "Conexión a Azure Stack | Microsoft Docs"
description: "Obtenga información acerca de cómo conectar a Azure Stack"
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
ms.date: 09/25/2017
ms.author: sngun
ms.openlocfilehash: 09c626e97832821009ce2da360ceea2b54273ffa
ms.sourcegitcommit: 90e2cced6a773b1b52f999ba73cd8877305d270b
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/13/2017
---
# <a name="connect-to-azure-stack"></a><span data-ttu-id="c3ac7-103">Conexión a Azure Stack</span><span class="sxs-lookup"><span data-stu-id="c3ac7-103">Connect to Azure Stack</span></span>

<span data-ttu-id="c3ac7-104">*Se aplica a: Azure Stack Development Kit*</span><span class="sxs-lookup"><span data-stu-id="c3ac7-104">*Applies to: Azure Stack Development Kit*</span></span>

<span data-ttu-id="c3ac7-105">Para administrar recursos, debe conectarse a Azure Stack Development Kit.</span><span class="sxs-lookup"><span data-stu-id="c3ac7-105">To manage resources, you must connect to the Azure Stack Development Kit.</span></span> <span data-ttu-id="c3ac7-106">Este tema detalla los pasos necesarios para conectar con el kit de desarrollo.</span><span class="sxs-lookup"><span data-stu-id="c3ac7-106">This topic details the steps required to connect to the development kit.</span></span> <span data-ttu-id="c3ac7-107">Puede utilizar cualquiera de las siguientes opciones de conexión:</span><span class="sxs-lookup"><span data-stu-id="c3ac7-107">You can use either of the following connection options:</span></span>

* <span data-ttu-id="c3ac7-108">[Escritorio remoto](#connect-with-remote-desktop): permite a un solo usuario simultáneo conectarse rápidamente al kit de desarrollo.</span><span class="sxs-lookup"><span data-stu-id="c3ac7-108">[Remote Desktop](#connect-with-remote-desktop): lets a single concurrent user quickly connect from the development kit.</span></span>
* <span data-ttu-id="c3ac7-109">[Red privada virtual (VPN)](#connect-with-vpn): permite que varios usuarios simultáneos se conecten desde clientes fuera de la infraestructura de Azure Stack (requiere configuración).</span><span class="sxs-lookup"><span data-stu-id="c3ac7-109">[Virtual Private Network (VPN)](#connect-with-vpn): lets multiple concurrent users connect from clients outside of the Azure Stack infrastructure (requires configuration).</span></span>

## <a name="connect-to-azure-stack-with-remote-desktop"></a><span data-ttu-id="c3ac7-110">Conexión a Azure Stack con Escritorio remoto</span><span class="sxs-lookup"><span data-stu-id="c3ac7-110">Connect to Azure Stack with Remote Desktop</span></span>
<span data-ttu-id="c3ac7-111">Con una conexión a Escritorio remoto, un único usuario simultáneo puede trabajar con el portal para administrar los recursos.</span><span class="sxs-lookup"><span data-stu-id="c3ac7-111">With a Remote Desktop connection, a single concurrent user can work with the portal to manage resources.</span></span>

1. <span data-ttu-id="c3ac7-112">Abra una conexión a Escritorio remoto y conecte con el kit de desarrollo.</span><span class="sxs-lookup"><span data-stu-id="c3ac7-112">Open a Remote Desktop Connection and connect to the development kit.</span></span> <span data-ttu-id="c3ac7-113">Escriba **AzureStack\AzureStackAdmin** como nombre de usuario y la contraseña del operador que proporcionó durante la instalación de Azure Stack.</span><span class="sxs-lookup"><span data-stu-id="c3ac7-113">Enter **AzureStack\AzureStackAdmin** as the username, and the operator's password that you provided during Azure Stack setup.</span></span>  

2. <span data-ttu-id="c3ac7-114">En el equipo del kit de desarrollo, abra el Administrador del servidor, haga clic en **Servidor local**, desactive la opción de seguridad mejorada de Internet Explorer y, a continuación, cierre el Administrador del servidor.</span><span class="sxs-lookup"><span data-stu-id="c3ac7-114">From the development kit computer, open Server Manager, click **Local Server**, turn off Internet Explorer Enhanced Security, and then close Server Manager.</span></span>

3. <span data-ttu-id="c3ac7-115">Para abrir el [portal](azure-stack-key-features.md#portal) de usuario, vaya a (https://portal.local.azurestack.external/) e inicie sesión con las credenciales de usuario.</span><span class="sxs-lookup"><span data-stu-id="c3ac7-115">To open the user [portal](azure-stack-key-features.md#portal), navigate to (https://portal.local.azurestack.external/) and sign in using user credentials.</span></span> <span data-ttu-id="c3ac7-116">Para abrir el [portal](azure-stack-key-features.md#portal) de administrador de Azure Stack, vaya a (https://adminportal.local.azurestack.external/) e inicie sesión con las credenciales de Azure Active Directory especificadas durante la instalación.</span><span class="sxs-lookup"><span data-stu-id="c3ac7-116">To open the Azure Stack operator's [portal](azure-stack-key-features.md#portal), navigate to (https://adminportal.local.azurestack.external/) and sign in using the Azure Active Directory credentials specified during installation.</span></span>

## <a name="connect-to-azure-stack-with-vpn"></a><span data-ttu-id="c3ac7-117">Conexión a Azure Stack con VPN</span><span class="sxs-lookup"><span data-stu-id="c3ac7-117">Connect to Azure Stack with VPN</span></span>

<span data-ttu-id="c3ac7-118">Puede establecer un túnel de conexión de red privada virtual (VPN) a Azure Stack Development Kit.</span><span class="sxs-lookup"><span data-stu-id="c3ac7-118">You can establish a split tunnel Virtual Private Network (VPN) connection to an Azure Stack Development Kit.</span></span> <span data-ttu-id="c3ac7-119">A través de la conexión VPN, puede tener acceso al portal del operador de Azure Stack, al portal de usuario y a las herramientas instaladas localmente como Visual Studio y PowerShell para administrar los recursos de Azure Stack.</span><span class="sxs-lookup"><span data-stu-id="c3ac7-119">Through the VPN connection, you can access the Azure Stack operator's portal, user portal, and locally installed tools such as Visual Studio and PowerShell to manage Azure Stack resources.</span></span> <span data-ttu-id="c3ac7-120">Se admite la conectividad VPN en implementaciones basadas en Azure Active Directory (AAD) y en los Servicios de federación de Active Directory (AD FS).</span><span class="sxs-lookup"><span data-stu-id="c3ac7-120">VPN connectivity is supported in both Azure Active Directory(AAD) and Active Directory Federation Services(AD FS) based deployments.</span></span> <span data-ttu-id="c3ac7-121">Las conexiones VPN permiten que varios clientes puedan conectarse a Azure Stack al mismo tiempo.</span><span class="sxs-lookup"><span data-stu-id="c3ac7-121">VPN connections enable multiple clients to connect to Azure Stack at the same time.</span></span> 

> [!NOTE] 
> <span data-ttu-id="c3ac7-122">Esta conexión VPN no proporciona conectividad a las máquinas virtuales de infraestructura de Azure Stack.</span><span class="sxs-lookup"><span data-stu-id="c3ac7-122">This VPN connection does not provide connectivity to Azure Stack infrastructure VMs.</span></span> 

### <a name="prerequisites"></a><span data-ttu-id="c3ac7-123">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="c3ac7-123">Prerequisites</span></span>

* <span data-ttu-id="c3ac7-124">Instale [Azure PowerShell compatible con Azure Stack](azure-stack-powershell-install.md) en el equipo local.</span><span class="sxs-lookup"><span data-stu-id="c3ac7-124">Install [Azure Stack compatible Azure PowerShell](azure-stack-powershell-install.md) on your local computer.</span></span>  
* <span data-ttu-id="c3ac7-125">Descargue las [herramientas necesarias para trabajar con Azure Stack](azure-stack-powershell-download.md).</span><span class="sxs-lookup"><span data-stu-id="c3ac7-125">Download the [tools required to work with Azure Stack](azure-stack-powershell-download.md).</span></span> 

### <a name="configure-vpn-connectivity"></a><span data-ttu-id="c3ac7-126">Configuración de la conectividad VPN</span><span class="sxs-lookup"><span data-stu-id="c3ac7-126">Configure VPN connectivity</span></span>

<span data-ttu-id="c3ac7-127">Para crear una conexión VPN con el kit de desarrollo, abra una sesión de PowerShell con privilegios elevados desde el equipo local basado en Windows y ejecute el script siguiente (asegúrese de actualizar los valores de dirección IP y contraseña para su entorno):</span><span class="sxs-lookup"><span data-stu-id="c3ac7-127">To create a VPN connection to the development kit, open an elevated PowerShell session from your local Windows-based computer and run the following script (make sure to update the the IP address and password values for your environment):</span></span>

```PowerShell 
# Configure winrm if it's not already configured
winrm quickconfig  

Set-ExecutionPolicy RemoteSigned

# Import the Connect module
Import-Module .\Connect\AzureStack.Connect.psm1 

# Add the development kit computer’s host IP address & certificate authority (CA) to the list of trusted hosts. Make sure to update the the IP address and password values for your environment. 

$hostIP = "<Azure Stack host IP address>"

$Password = ConvertTo-SecureString `
  "<operator's password provided when deploying Azure Stack>" `
  -AsPlainText `
  -Force

Set-Item wsman:\localhost\Client\TrustedHosts `
  -Value $hostIP `
  -Concatenate

# Create a VPN connection entry for the local user
Add-AzsVpnConnection `
  -ServerAddress $hostIP `
  -Password $Password

```

<span data-ttu-id="c3ac7-128">Si la configuración se realiza correctamente, debería ver **azurestack** en la lista de conexiones VPN.</span><span class="sxs-lookup"><span data-stu-id="c3ac7-128">If the set up succeeds, you should see **azurestack** in your list of VPN connections.</span></span>

![Conexiones de red](media/azure-stack-connect-azure-stack/image3.png)  

### <a name="connect-to-azure-stack"></a><span data-ttu-id="c3ac7-130">Conexión a Azure Stack</span><span class="sxs-lookup"><span data-stu-id="c3ac7-130">Connect to Azure Stack</span></span>

<span data-ttu-id="c3ac7-131">Conéctese a la instancia de Azure Stack mediante cualquiera de los dos métodos siguientes:</span><span class="sxs-lookup"><span data-stu-id="c3ac7-131">Connect to the Azure Stack instance by using either of the following two methods:</span></span>  

* <span data-ttu-id="c3ac7-132">Mediante el uso del comando `Connect-AzsVpn `:</span><span class="sxs-lookup"><span data-stu-id="c3ac7-132">By using the `Connect-AzsVpn ` command:</span></span> 
    
  ```PowerShell
  Connect-AzsVpn `
    -Password $Password
  ```

  <span data-ttu-id="c3ac7-133">Cuando se le solicite, confíe en el host de Azure Stack e instale el certificado de **AzureStackCertificateAuthority** en el almacén de certificados del equipo local.</span><span class="sxs-lookup"><span data-stu-id="c3ac7-133">When prompted, trust the Azure Stack host and install the certificate from **AzureStackCertificateAuthority** onto your local computer’s certificate store.</span></span> <span data-ttu-id="c3ac7-134">(el símbolo del sistema podría aparecer detrás de la ventana de sesión de PowerShell).</span><span class="sxs-lookup"><span data-stu-id="c3ac7-134">(the prompt might appear behind the PowerShell session window).</span></span> 

* <span data-ttu-id="c3ac7-135">En el equipo local, abra **Configuración de red** > **VPN** > haga clic en **azurestack** > **Conectar**.</span><span class="sxs-lookup"><span data-stu-id="c3ac7-135">Open your local computer’s **Network Settings** > **VPN** > click **azurestack** > **connect**.</span></span> <span data-ttu-id="c3ac7-136">En el símbolo del sistema de inicio de sesión, escriba el nombre de usuario (AzureStack\AzureStackAdmin) y la contraseña.</span><span class="sxs-lookup"><span data-stu-id="c3ac7-136">At the sign-in prompt, enter the username (AzureStack\AzureStackAdmin) and the password.</span></span>

### <a name="test-the-vpn-connectivity"></a><span data-ttu-id="c3ac7-137">Prueba de la conectividad VPN</span><span class="sxs-lookup"><span data-stu-id="c3ac7-137">Test the VPN connectivity</span></span>

<span data-ttu-id="c3ac7-138">Para probar la conexión del portal, abra un explorador de Internet y navegue hasta el portal de usuario (https://portal.local.azurestack.external/) o el portal del operador (https://adminportal.local.azurestack.external/), inicie sesión y cree recursos.</span><span class="sxs-lookup"><span data-stu-id="c3ac7-138">To test the portal connection, open an Internet browser and navigate to either the user portal (https://portal.local.azurestack.external/) or the operator portal (https://adminportal.local.azurestack.external/), sign in and create resources.</span></span>  

## <a name="next-steps"></a><span data-ttu-id="c3ac7-139">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="c3ac7-139">Next steps</span></span>

[<span data-ttu-id="c3ac7-140">Máquinas virtuales disponibles para los usuarios de Azure Stack</span><span class="sxs-lookup"><span data-stu-id="c3ac7-140">Make virtual machines available to your Azure Stack users</span></span>](azure-stack-tutorial-tenant-vm.md)

