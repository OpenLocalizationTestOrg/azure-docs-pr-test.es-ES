---
title: aaaEnable FTP en el servicio de aplicaciones en la pila de Azure | Documentos de Microsoft
description: Pasos toocomplete tooenable FTP en el servicio de aplicaciones en la pila de Azure
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
ms.date: 4/6/2017
ms.author: anwestg
ms.openlocfilehash: 9c02da6362085fdd9f8d285da04efe85cf352398
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="enable-ftp-in-app-service-on-azure-stack"></a><span data-ttu-id="270da-103">Habilitación del FTP en App Service en Azure Stack</span><span class="sxs-lookup"><span data-stu-id="270da-103">Enable FTP in App Service on Azure Stack</span></span>

<span data-ttu-id="270da-104">Una vez que ha implementado correctamente el servicio de aplicaciones en la pila de Azure si desea que la publicación tooenable FTP, para que los inquilinos pueden cargar sus archivos de la aplicación y el contenido, hay algunos pasos adicionales que necesitan toobe completado.</span><span class="sxs-lookup"><span data-stu-id="270da-104">Once you have successfully deployed App Service on Azure Stack if you wish tooenable FTP publishing, so that your tenants can upload their application files and content, there are some additional steps that need toobe completed.</span></span>  <span data-ttu-id="270da-105">Estos pasos se automatizarán en futuras versiones.</span><span class="sxs-lookup"><span data-stu-id="270da-105">In future releases these steps will be automated.</span></span>

> [!NOTE]
> <span data-ttu-id="270da-106">Además, están dirigidos a los administradores de empresas o servicios que configuran una instancia de App Service en el proveedor de recursos de Azure Stack.</span><span class="sxs-lookup"><span data-stu-id="270da-106">These steps are for Service or Enterprise Administrators configuring an App Service on Azure Stack Resource Provider.</span></span>

## <a name="enable-ftp"></a><span data-ttu-id="270da-107">Habilitación del FTP</span><span class="sxs-lookup"><span data-stu-id="270da-107">Enable FTP</span></span>

1.  <span data-ttu-id="270da-108">Inicie sesión en el portal de Azure pila toohello como administrador de servicios de Hola.</span><span class="sxs-lookup"><span data-stu-id="270da-108">Log in toohello Azure Stack portal as hello service administrator.</span></span>
2.  <span data-ttu-id="270da-109">Examinar demasiado**interfaces de red** seleccione hello y **FTP NIC** en **grupo de recursos** - **AppService LOCAL**.</span><span class="sxs-lookup"><span data-stu-id="270da-109">Browse too**Network interfaces** and select hello **FTP-NIC** under **Resource Group** - **AppService-LOCAL**.</span></span> <span data-ttu-id="270da-110">![Interfaces de red de Azure Stack][1]</span><span class="sxs-lookup"><span data-stu-id="270da-110">![Azure Stack Network Interfaces][1]</span></span>
3.  <span data-ttu-id="270da-111">Hola Nota **dirección IP pública** de hello **FTP NIC**.</span><span class="sxs-lookup"><span data-stu-id="270da-111">Note hello **Public IP Address** of hello **FTP-NIC**.</span></span> 
<span data-ttu-id="270da-112">![Detalles de la interfaz de red de Azure Stack][2]</span><span class="sxs-lookup"><span data-stu-id="270da-112">![Azure Stack Network Interface Details][2]</span></span>
4.  <span data-ttu-id="270da-113">A continuación vaya demasiado**máquinas virtuales** y seleccione hello **FTP0-VM**.</span><span class="sxs-lookup"><span data-stu-id="270da-113">Next Browse too**Virtual Machines** and select hello **FTP0-VM**.</span></span> <span data-ttu-id="270da-114">![Máquinas virtuales de Azure Stack][3]</span><span class="sxs-lookup"><span data-stu-id="270da-114">![Azure Stack Virtual Machines][3]</span></span>
5.  <span data-ttu-id="270da-115">Abra una VM de toohello de sesión de escritorio remoto con hello **conectar** sesión de toohello botón e inicie sesión con credenciales de administrador de hello establecido durante la implementación del servicio de aplicación.</span><span class="sxs-lookup"><span data-stu-id="270da-115">Open a remote desktop session toohello VM using hello **Connect** button and login toohello session using hello Administrator credentials you set during App Service deployment.</span></span>  
<span data-ttu-id="270da-116">![Detalles de la máquina virtual de Azure Stack][4]</span><span class="sxs-lookup"><span data-stu-id="270da-116">![Azure Stack Virtual Machine Details][4]</span></span>
6.  <span data-ttu-id="270da-117">Abra **servicios de Internet Information Server (IIS) Manager** en hello FTP VM (FTP0-VM).</span><span class="sxs-lookup"><span data-stu-id="270da-117">Open **Internet Information Service (IIS) Manager** on hello FTP VM (FTP0-VM).</span></span>
7.  <span data-ttu-id="270da-118">En **Sitios**, seleccione **Hospedaje de sitio FTP**.</span><span class="sxs-lookup"><span data-stu-id="270da-118">Under **Sites** select **Hosting FTP Site**.</span></span>
8.  <span data-ttu-id="270da-119">Abra **Compatibilidad con el FTP Firewall**.</span><span class="sxs-lookup"><span data-stu-id="270da-119">Open **FTP Firewall Support**.</span></span> <span data-ttu-id="270da-120">![Administrador de IIS en la máquina virtual FTP0-VM de App Service][5]</span><span class="sxs-lookup"><span data-stu-id="270da-120">![IIS Manager on App Service FTP0-VM][5]</span></span>
9.  <span data-ttu-id="270da-121">Escriba Hola dirección IP pública de hello NIC de FTP y haga clic en **aplicar** ![soporte de Firewall de FTP de IIS Manager][6]</span><span class="sxs-lookup"><span data-stu-id="270da-121">Enter hello Public IP Address of hello FTP-NIC and click **Apply** ![IIS Manager FTP Firewall Support][6]</span></span>

## <a name="validate-hello-enabling-of-ftp"></a><span data-ttu-id="270da-122">Validar Hola habilitación de FTP</span><span class="sxs-lookup"><span data-stu-id="270da-122">Validate hello enabling of FTP</span></span>

1.  <span data-ttu-id="270da-123">Inicie sesión en toohello portal de Azure pila como cualquier administrador de servicios de Hola o como un inquilino.</span><span class="sxs-lookup"><span data-stu-id="270da-123">Log in toohello Azure Stack portal as either hello service administrator or as a tenant.</span></span>
2.  <span data-ttu-id="270da-124">Examinar demasiado**servicios de aplicaciones** y seleccione una Web, móviles o App API que haya creado.</span><span class="sxs-lookup"><span data-stu-id="270da-124">Browse too**App Services** and select a Web, Mobile, or API App you have created.</span></span> <span data-ttu-id="270da-125">![App Services][7]</span><span class="sxs-lookup"><span data-stu-id="270da-125">![App Services][7]</span></span>
3.  <span data-ttu-id="270da-126">En la aplicación hello detalles Observe hello **nombre de host FTP** y **nombre de usuario FTP e implementación**.</span><span class="sxs-lookup"><span data-stu-id="270da-126">In hello application details note hello **FTP Hostname** and **FTP/deployment username**.</span></span> <span data-ttu-id="270da-127">![Detalles de la aplicación de App Service][8]</span><span class="sxs-lookup"><span data-stu-id="270da-127">![App Service App Details][8]</span></span>
> [!NOTE]
> <span data-ttu-id="270da-128">Si no ve una entrada en **nombre de usuario FTP e implementación**, necesita las credenciales de implementación de hello tooset usar primero Hola **las credenciales de implementación** hoja.</span><span class="sxs-lookup"><span data-stu-id="270da-128">If you do not see an entry under **FTP/deployment username**, you need tooset hello Deployment credentials first using hello **Deployment Credentials** Blade.</span></span>

4.  <span data-ttu-id="270da-129">Abra el Explorador de Windows, escriba el nombre de host de hello FTP en dirección del archivo hello barra ftp://ftp.appservice.azurestack.local por ejemplo,</span><span class="sxs-lookup"><span data-stu-id="270da-129">Open Windows Explorer, enter hello FTP hostname into hello file address bar for example, ftp://ftp.appservice.azurestack.local</span></span>
5.  <span data-ttu-id="270da-130">Cuando se le solicite escribir hello **las credenciales de implementación** que anotó en el paso 3, si se ha habilitado la característica de hello, verá una lista de directorios de contenido de la aplicación de servicio de aplicación Hola.</span><span class="sxs-lookup"><span data-stu-id="270da-130">When prompted enter hello **Deployment credentials** you noted in step 3, if hello feature has been enabled you will see a directory listing of hello app service application's contents.</span></span> <span data-ttu-id="270da-131">![Lista de archivos de FTP][9]</span><span class="sxs-lookup"><span data-stu-id="270da-131">![FTP File Listing][9]</span></span>
<!--Image references-->
[1]: ./media/azure-stack-app-service-enable-ftp/azure-stack-app-service-enable-ftp-network-interfaces.png
[2]: ./media/azure-stack-app-service-enable-ftp/azure-stack-app-service-enable-ftp-network-interface-details.png
[3]: ./media/azure-stack-app-service-enable-ftp/azure-stack-app-service-enable-ftp-virtual-machines.png
[4]: ./media/azure-stack-app-service-enable-ftp/azure-stack-app-service-enable-ftp-virtual-machines-FTP0-VM.png
[5]: ./media/azure-stack-app-service-enable-ftp/azure-stack-app-service-enable-ftp-IIS-Manager.png
[6]: ./media/azure-stack-app-service-enable-ftp/azure-stack-app-service-enable-ftp-IIS-Manager-FTP-Firewall-Support.png
[7]: ./media/azure-stack-app-service-enable-ftp/azure-stack-app-service-enable-ftp-validate-app-services.png
[8]: ./media/azure-stack-app-service-enable-ftp/azure-stack-app-service-enable-ftp-validate-app-service-app-detail.png
[9]: ./media/azure-stack-app-service-enable-ftp/azure-stack-app-service-enable-ftp-validate-ftp-file-listing.png
