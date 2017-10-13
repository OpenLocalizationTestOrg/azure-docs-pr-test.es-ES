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
ms.date: 08/22/2017
ms.author: sngun
ms.openlocfilehash: 914f2e5d10aa341cea5eba8c24c7c37610e6b626
ms.sourcegitcommit: 90e2cced6a773b1b52f999ba73cd8877305d270b
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/13/2017
---
# <a name="connect-to-azure-stack"></a><span data-ttu-id="d1314-103">Conexión a Azure Stack</span><span class="sxs-lookup"><span data-stu-id="d1314-103">Connect to Azure Stack</span></span>

<span data-ttu-id="d1314-104">Para administrar recursos, debe conectarse a Azure Stack Development Kit.</span><span class="sxs-lookup"><span data-stu-id="d1314-104">To manage resources, you must connect to the Azure Stack Development Kit.</span></span> <span data-ttu-id="d1314-105">Este tema detalla los pasos necesarios para conectar con el kit de desarrollo.</span><span class="sxs-lookup"><span data-stu-id="d1314-105">This topic details the steps required to connect to the development kit.</span></span> <span data-ttu-id="d1314-106">Puede utilizar cualquiera de las siguientes opciones de conexión:</span><span class="sxs-lookup"><span data-stu-id="d1314-106">You can use either of the following connection options:</span></span>

* <span data-ttu-id="d1314-107">[Escritorio remoto](#connect-with-remote-desktop): permite a un solo usuario simultáneo conectarse rápidamente al kit de desarrollo.</span><span class="sxs-lookup"><span data-stu-id="d1314-107">[Remote Desktop](#connect-with-remote-desktop): lets a single concurrent user quickly connect from the development kit.</span></span>
* <span data-ttu-id="d1314-108">[Red privada virtual (VPN)](#connect-with-vpn): permite que varios usuarios simultáneos se conecten desde clientes fuera de la infraestructura de Azure Stack (requiere configuración).</span><span class="sxs-lookup"><span data-stu-id="d1314-108">[Virtual Private Network (VPN)](#connect-with-vpn): lets multiple concurrent users connect from clients outside of the Azure Stack infrastructure (requires configuration).</span></span>

## <a name="connect-to-azure-stack-with-remote-desktop"></a><span data-ttu-id="d1314-109">Conexión a Azure Stack con Escritorio remoto</span><span class="sxs-lookup"><span data-stu-id="d1314-109">Connect to Azure Stack with Remote Desktop</span></span>
<span data-ttu-id="d1314-110">Con una conexión a Escritorio remoto, un único usuario simultáneo puede trabajar con el portal para administrar los recursos.</span><span class="sxs-lookup"><span data-stu-id="d1314-110">With a Remote Desktop connection, a single concurrent user can work with the portal to manage resources.</span></span>

1. <span data-ttu-id="d1314-111">Abra una conexión a Escritorio remoto y conecte con el kit de desarrollo.</span><span class="sxs-lookup"><span data-stu-id="d1314-111">Open a Remote Desktop Connection and connect to the development kit.</span></span> <span data-ttu-id="d1314-112">Escriba **AzureStack\AzureStackAdmin** como nombre de usuario y la contraseña de administrador que proporcionó durante la instalación de Azure Stack.</span><span class="sxs-lookup"><span data-stu-id="d1314-112">Enter **AzureStack\AzureStackAdmin** as the username, and the administrative password that you provided during Azure Stack setup.</span></span>  

2. <span data-ttu-id="d1314-113">En el equipo del kit de desarrollo, abra el Administrador del servidor, haga clic en **Servidor local**, desactive la opción de seguridad mejorada de Internet Explorer y, a continuación, cierre el Administrador del servidor.</span><span class="sxs-lookup"><span data-stu-id="d1314-113">From the development kit computer, open Server Manager, click **Local Server**, turn off Internet Explorer Enhanced Security, and then close Server Manager.</span></span>

3. <span data-ttu-id="d1314-114">Para abrir el portal, vaya a (https://portal.local.azurestack.external/) e inicie sesión con las credenciales de usuario.</span><span class="sxs-lookup"><span data-stu-id="d1314-114">To open the  portal, navigate to (https://portal.local.azurestack.external/) and sign in using user credentials.</span></span>


## <a name="connect-to-azure-stack-with-vpn"></a><span data-ttu-id="d1314-115">Conexión a Azure Stack con VPN</span><span class="sxs-lookup"><span data-stu-id="d1314-115">Connect to Azure Stack with VPN</span></span>

<span data-ttu-id="d1314-116">Puede establecer un túnel de conexión de red privada virtual (VPN) a Azure Stack Development Kit.</span><span class="sxs-lookup"><span data-stu-id="d1314-116">You can establish a split tunnel Virtual Private Network (VPN) connection to an Azure Stack Development Kit.</span></span> <span data-ttu-id="d1314-117">A través de la conexión VPN, puede tener acceso al portal de administrador, al portal de usuario y a las herramientas instaladas localmente, como Visual Studio y PowerShell, para administrar los recursos de Azure Stack.</span><span class="sxs-lookup"><span data-stu-id="d1314-117">Through the VPN connection, you can access the administrator portal, user portal, and locally installed tools such as Visual Studio and PowerShell to manage Azure Stack resources.</span></span> <span data-ttu-id="d1314-118">Se admite la conectividad VPN en implementaciones basadas en Azure Active Directory (AAD) y en los Servicios de federación de Active Directory (AD FS).</span><span class="sxs-lookup"><span data-stu-id="d1314-118">VPN connectivity is supported in both Azure Active Directory(AAD) and Active Directory Federation Services(AD FS) based deployments.</span></span> <span data-ttu-id="d1314-119">Las conexiones VPN permiten que varios clientes puedan conectarse a Azure Stack al mismo tiempo.</span><span class="sxs-lookup"><span data-stu-id="d1314-119">VPN connections enable multiple clients to connect to Azure Stack at the same time.</span></span> 

> [!NOTE] 
> <span data-ttu-id="d1314-120">Esta conexión VPN no proporciona conectividad a las máquinas virtuales de infraestructura de Azure Stack.</span><span class="sxs-lookup"><span data-stu-id="d1314-120">This VPN connection does not provide connectivity to Azure Stack infrastructure VMs.</span></span> 

### <a name="prerequisites"></a><span data-ttu-id="d1314-121">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="d1314-121">Prerequisites</span></span>

* <span data-ttu-id="d1314-122">Instale [Azure PowerShell compatible con Azure Stack](azure-stack-powershell-install.md) en el equipo local.</span><span class="sxs-lookup"><span data-stu-id="d1314-122">Install [Azure Stack compatible Azure PowerShell](azure-stack-powershell-install.md) on your local computer.</span></span>  
* <span data-ttu-id="d1314-123">Descargue las [herramientas necesarias para trabajar con Azure Stack](azure-stack-powershell-download.md).</span><span class="sxs-lookup"><span data-stu-id="d1314-123">Download the [tools required to work with Azure Stack](azure-stack-powershell-download.md).</span></span> 

### <a name="configure-vpn-connectivity"></a><span data-ttu-id="d1314-124">Configuración de la conectividad VPN</span><span class="sxs-lookup"><span data-stu-id="d1314-124">Configure VPN connectivity</span></span>

<span data-ttu-id="d1314-125">Para crear una conexión VPN con el kit de desarrollo, abra una sesión de PowerShell con privilegios elevados desde el equipo local basado en Windows y ejecute el script siguiente (asegúrese de actualizar los valores de dirección IP y contraseña para su entorno):</span><span class="sxs-lookup"><span data-stu-id="d1314-125">To create a VPN connection to the development kit, open an elevated PowerShell session from your local Windows-based computer and run the following script (make sure to update the the IP address and password values for your environment):</span></span>

```PowerShell 
# Configure winrm if it's not already configured
winrm quickconfig  

Set-ExecutionPolicy RemoteSigned

# Import the Connect module
Import-Module .\Connect\AzureStack.Connect.psm1 

# Add the development kit computer’s host IP address & certificate authority (CA) to the list of trusted hosts. Make sure to update the the IP address and password values for your environment. 

$hostIP = "<Azure Stack host IP address>"

$Password = ConvertTo-SecureString `
  "<Administrator password provided when deploying Azure Stack>" `
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

<span data-ttu-id="d1314-126">Si la configuración se realiza correctamente, debería ver **azurestack** en la lista de conexiones VPN.</span><span class="sxs-lookup"><span data-stu-id="d1314-126">If the set up succeeds, you should see **azurestack** in your list of VPN connections.</span></span>

![Conexiones de red](media/azure-stack-connect-azure-stack/image3.png)  

### <a name="connect-to-azure-stack"></a><span data-ttu-id="d1314-128">Conexión a Azure Stack</span><span class="sxs-lookup"><span data-stu-id="d1314-128">Connect to Azure Stack</span></span>

<span data-ttu-id="d1314-129">Conéctese a la instancia de Azure Stack mediante cualquiera de los dos métodos siguientes:</span><span class="sxs-lookup"><span data-stu-id="d1314-129">Connect to the Azure Stack instance by using either of the following two methods:</span></span>  

* <span data-ttu-id="d1314-130">Mediante el uso del comando `Connect-AzsVpn `:</span><span class="sxs-lookup"><span data-stu-id="d1314-130">By using the `Connect-AzsVpn ` command:</span></span> 
    
  ```PowerShell
  Connect-AzsVpn `
    -Password $Password
  ```

  <span data-ttu-id="d1314-131">Cuando se le solicite, confíe en el host de Azure Stack e instale el certificado de **AzureStackCertificateAuthority** en el almacén de certificados del equipo local.</span><span class="sxs-lookup"><span data-stu-id="d1314-131">When prompted, trust the Azure Stack host and install the certificate from **AzureStackCertificateAuthority** onto your local computer’s certificate store.</span></span> <span data-ttu-id="d1314-132">(el símbolo del sistema podría aparecer detrás de la ventana de sesión de PowerShell).</span><span class="sxs-lookup"><span data-stu-id="d1314-132">(the prompt might appear behind the PowerShell session window).</span></span> 

* <span data-ttu-id="d1314-133">En el equipo local, abra **Configuración de red** > **VPN** > haga clic en **azurestack** > **Conectar**.</span><span class="sxs-lookup"><span data-stu-id="d1314-133">Open your local computer’s **Network Settings** > **VPN** > click **azurestack** > **connect**.</span></span> <span data-ttu-id="d1314-134">En el símbolo del sistema de inicio de sesión, escriba el nombre de usuario (AzureStack\AzureStackAdmin) y la contraseña.</span><span class="sxs-lookup"><span data-stu-id="d1314-134">At the sign-in prompt, enter the username (AzureStack\AzureStackAdmin) and the password.</span></span>

### <a name="test-the-vpn-connectivity"></a><span data-ttu-id="d1314-135">Prueba de la conectividad VPN</span><span class="sxs-lookup"><span data-stu-id="d1314-135">Test the VPN connectivity</span></span>

<span data-ttu-id="d1314-136">Para probar la conexión del portal, abra un explorador de Internet y navegue hasta el portal de usuario (https://portal.local.azurestack.external/), inicie sesión y cree recursos.</span><span class="sxs-lookup"><span data-stu-id="d1314-136">To test the portal connection, open an Internet browser and navigate to the user portal (https://portal.local.azurestack.external/), sign in and create resources.</span></span>  

## <a name="next-steps"></a><span data-ttu-id="d1314-137">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="d1314-137">Next steps</span></span>



