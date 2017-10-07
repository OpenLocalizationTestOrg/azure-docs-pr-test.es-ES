---
title: aaaBefore implementar el servicio de aplicaciones en la pila de Azure | Documentos de Microsoft
description: Pasos toocomplete antes de implementar el servicio de aplicaciones en la pila de Azure
services: azure-stack
documentationcenter: 
author: apwestgarth
manager: stefsch
editor: 
ms.assetid: 
ms.service: azure-stack
ms.workload: app-service
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 7/3/2017
ms.author: anwestg
ms.openlocfilehash: fad758232ef2795105036640c2a26abf3fa2c3c8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="before-you-get-started-with-app-service-on-azure-stack"></a><span data-ttu-id="8a789-103">Antes de empezar a trabajar con App Service en Azure Stack</span><span class="sxs-lookup"><span data-stu-id="8a789-103">Before you get started with App Service on Azure Stack</span></span>

<span data-ttu-id="8a789-104">Necesita unos elementos tooinstall servicio de aplicaciones de Azure en la pila de Azure:</span><span class="sxs-lookup"><span data-stu-id="8a789-104">You need a few items tooinstall Azure App Service on Azure Stack:</span></span>

- <span data-ttu-id="8a789-105">Una implementación completa de hello [kit de desarrollo de Azure pila](azure-stack-run-powershell-script.md).</span><span class="sxs-lookup"><span data-stu-id="8a789-105">A completed deployment of hello [Azure Stack development kit](azure-stack-run-powershell-script.md).</span></span>
- <span data-ttu-id="8a789-106">Suficiente espacio en el sistema de Azure Stack para una implementación pequeña de App Service en Azure Stack.</span><span class="sxs-lookup"><span data-stu-id="8a789-106">Enough space in your Azure Stack system for a small deployment of App Service on Azure Stack.</span></span>  <span data-ttu-id="8a789-107">Hola se requiere espacio en aproximadamente 20 GB de espacio en disco.</span><span class="sxs-lookup"><span data-stu-id="8a789-107">hello required space is roughly 20 GB of disk space.</span></span>
- <span data-ttu-id="8a789-108">Una imagen de máquina virtual de Windows Server para usarla al crear máquinas virtuales para App Service en Azure Stack.</span><span class="sxs-lookup"><span data-stu-id="8a789-108">A Windows Server VM image for use when you create virtual machines for App Service on Azure Stack.</span></span>
- <span data-ttu-id="8a789-109">[Un servidor que ejecute SQL Server](#SQL-Server).</span><span class="sxs-lookup"><span data-stu-id="8a789-109">[A server that's running SQL Server](#SQL-Server).</span></span>

>[!NOTE] 
> <span data-ttu-id="8a789-110">Hola lo siguiente *todos los* tienen lugar en la máquina de host de hello pila de Azure.</span><span class="sxs-lookup"><span data-stu-id="8a789-110">hello following steps *all* take place on hello Azure Stack host machine.</span></span>

<span data-ttu-id="8a789-111">toodeploy un proveedor de recursos, debe ejecutar Hola entorno de Scripting integrado (ISE) de PowerShell como administrador.</span><span class="sxs-lookup"><span data-stu-id="8a789-111">toodeploy a resource provider, you must run hello PowerShell Integrated Scripting Environment (ISE) as an administrator.</span></span> <span data-ttu-id="8a789-112">Por esta razón, necesita tooallow cookies y JavaScript de perfil de Internet Explorer de Hola que usas toosign en tooAzure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="8a789-112">For this reason, you need tooallow cookies and JavaScript in hello Internet Explorer profile that you use toosign in tooAzure Active Directory.</span></span>

## <a name="turn-off-internet-explorer-enhanced-security"></a><span data-ttu-id="8a789-113">Desactivación de la seguridad mejorada de Internet Explorer</span><span class="sxs-lookup"><span data-stu-id="8a789-113">Turn off Internet Explorer enhanced security</span></span>

1.  <span data-ttu-id="8a789-114">Inicie sesión en el equipo de kit de desarrollo de pila de Azure de toohello como **AzureStack/administrador**y, a continuación, abra **el administrador del servidor**.</span><span class="sxs-lookup"><span data-stu-id="8a789-114">Sign in toohello Azure Stack development kit machine as **AzureStack/administrator**, and then open **Server Manager**.</span></span>

2.  <span data-ttu-id="8a789-115">Desactive la **Configuración de seguridad mejorada de Internet Explorer** para los administradores y usuarios.</span><span class="sxs-lookup"><span data-stu-id="8a789-115">Turn off **Internet Explorer Enhanced Security Configuration** for both admins and users.</span></span>

3.  <span data-ttu-id="8a789-116">Inicie sesión en el equipo de kit de desarrollo de toohello pila de Azure como administrador y, a continuación, abra **el administrador del servidor**.</span><span class="sxs-lookup"><span data-stu-id="8a789-116">Sign in toohello Azure Stack development kit machine as an administrator, and then open **Server Manager**.</span></span>

4.  <span data-ttu-id="8a789-117">Desactive la **Configuración de seguridad mejorada de Internet Explorer** para los administradores y usuarios.</span><span class="sxs-lookup"><span data-stu-id="8a789-117">Turn off **Internet Explorer Enhanced Security Configuration** for both admins and users.</span></span>

## <a name="enable-cookies"></a><span data-ttu-id="8a789-118">Habilitación de las cookies</span><span class="sxs-lookup"><span data-stu-id="8a789-118">Enable cookies</span></span>

1.  <span data-ttu-id="8a789-119">Seleccione **Inicio** > **Todas las aplicaciones** > **Accesorios de Windows**.</span><span class="sxs-lookup"><span data-stu-id="8a789-119">Select **Start** > **All apps** > **Windows accessories**.</span></span> <span data-ttu-id="8a789-120">Haga clic con el botón derecho en **Internet Explorer** > **Más** > **Ejecutar como administrador**.</span><span class="sxs-lookup"><span data-stu-id="8a789-120">Right-click **Internet Explorer** > **More** > **Run as an administrator**.</span></span>

2.  <span data-ttu-id="8a789-121">Si se le pide, seleccione **Use recommended security** (Usar seguridad recomendada) y, a continuación, seleccione **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="8a789-121">If you're prompted, select **Use recommended security**, and then select **OK**.</span></span>

3.  <span data-ttu-id="8a789-122">En Internet Explorer, seleccione **herramientas** (icono de engranaje de hello) > **opciones de Internet** > **privacidad** > **avanzadas**.</span><span class="sxs-lookup"><span data-stu-id="8a789-122">In Internet Explorer, select **Tools** (hello gear icon) > **Internet Options** > **Privacy** > **Advanced**.</span></span>

4.  <span data-ttu-id="8a789-123">Seleccione **Advanced** (Avanzadas).</span><span class="sxs-lookup"><span data-stu-id="8a789-123">Select **Advanced**.</span></span> <span data-ttu-id="8a789-124">Asegúrese de que las dos casillas **Aceptar** estén activadas.</span><span class="sxs-lookup"><span data-stu-id="8a789-124">Make sure that both **Accept** check boxes are selected.</span></span> <span data-ttu-id="8a789-125">Seleccione **Aceptar** dos veces.</span><span class="sxs-lookup"><span data-stu-id="8a789-125">Select **OK** twice.</span></span>

5.  <span data-ttu-id="8a789-126">Cierre Internet Explorer y reinicie Hola PowerShell ISE como administrador.</span><span class="sxs-lookup"><span data-stu-id="8a789-126">Close Internet Explorer, and restart hello PowerShell ISE as an administrator.</span></span>

## <a name="install-powershell-for-azure-stack"></a><span data-ttu-id="8a789-127">Instalación de PowerShell para Azure Stack</span><span class="sxs-lookup"><span data-stu-id="8a789-127">Install PowerShell for Azure Stack</span></span>

<span data-ttu-id="8a789-128">tooinstall PowerShell para la pila de Azure, siga los pasos de hello en [instale PowerShell](azure-stack-powershell-install.md).</span><span class="sxs-lookup"><span data-stu-id="8a789-128">tooinstall PowerShell for Azure Stack, follow hello steps in [Install PowerShell](azure-stack-powershell-install.md).</span></span>

## <a name="use-visual-studio-with-azure-stack"></a><span data-ttu-id="8a789-129">Uso de Visual Studio con Azure Stack</span><span class="sxs-lookup"><span data-stu-id="8a789-129">Use Visual Studio with Azure Stack</span></span>

<span data-ttu-id="8a789-130">toouse Visual Studio con la pila de Azure, siga los pasos de hello en [instalar Visual Studio](azure-stack-install-visual-studio.md).</span><span class="sxs-lookup"><span data-stu-id="8a789-130">toouse Visual Studio with Azure Stack, follow hello steps in [Install Visual Studio](azure-stack-install-visual-studio.md).</span></span>

## <a name="add-a-windows-server-2016-vm-image-tooazure-stack"></a><span data-ttu-id="8a789-131">Agregar un tooAzure de imagen de máquina virtual de Windows Server 2016 pila</span><span class="sxs-lookup"><span data-stu-id="8a789-131">Add a Windows Server 2016 VM image tooAzure Stack</span></span>

<span data-ttu-id="8a789-132">Puesto que App Service implementa varias máquinas virtuales, requiere una imagen de máquina virtual de Windows Server 2016 en Azure Stack.</span><span class="sxs-lookup"><span data-stu-id="8a789-132">Because App Service deploys a number of virtual machines, it requires a Windows Server 2016 VM image in Azure Stack.</span></span> <span data-ttu-id="8a789-133">tooinstall una imagen de máquina virtual, siga los pasos de hello en [agregar una imagen de máquina virtual predeterminada](azure-stack-add-default-image.md).</span><span class="sxs-lookup"><span data-stu-id="8a789-133">tooinstall a VM image, follow hello steps in [Add a default virtual machine image](azure-stack-add-default-image.md).</span></span>

## <span data-ttu-id="8a789-134"><a name="SQL-Server"></a>SQL Server</span><span class="sxs-lookup"><span data-stu-id="8a789-134"><a name="SQL-Server"></a>SQL Server</span></span>

<span data-ttu-id="8a789-135">Servicio de aplicaciones en la pila de Azure requiere acceso tooa SQL Server instancia toocreate y host dos bases de datos toorun Hola proveedor de recursos de servicio de aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="8a789-135">App Service on Azure Stack requires access tooa SQL Server instance toocreate and host two databases toorun hello App Service resource provider.</span></span>  <span data-ttu-id="8a789-136">Si decide toodeploy una VM de SQL Server en la pila de Azure debe tener el nivel de conectividad SQL Hola establecido demasiado**público**.</span><span class="sxs-lookup"><span data-stu-id="8a789-136">Should you choose toodeploy a SQL Server VM on Azure Stack it must have hello SQL connectivity level set too**Public**.</span></span>  <span data-ttu-id="8a789-137">Puede elegir toouse de instancia de SQL Server de hello al completar las opciones de Hola Hola servicio de aplicaciones en el instalador de la pila de Azure.</span><span class="sxs-lookup"><span data-stu-id="8a789-137">You can choose hello SQL Server instance toouse when you complete hello options in hello App Service on Azure Stack installer.</span></span>

## <a name="next-steps"></a><span data-ttu-id="8a789-138">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="8a789-138">Next steps</span></span>

- <span data-ttu-id="8a789-139">[Instalar el proveedor de recursos de servicio de aplicaciones de hello](azure-stack-app-service-deploy.md).</span><span class="sxs-lookup"><span data-stu-id="8a789-139">[Install hello App Service resource provider](azure-stack-app-service-deploy.md).</span></span>

<!--Image references-->
[1]: ./media/azure-stack-app-service-before-you-get-started/PSGallery.png
[2]: ./media/azure-stack-app-service-before-you-get-started/WebPI_InstalledProducts.png
