---
title: puerta de enlace de datos de aaaInstall local | Documentos de Microsoft
description: "Obtenga información acerca de cómo tooinstall y configurar una puerta de enlace de datos local."
services: analysis-services
documentationcenter: 
author: minewiskan
manager: erikre
editor: 
tags: 
ms.assetid: 
ms.service: analysis-services
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: na
ms.date: 08/22/2017
ms.author: owend
ms.openlocfilehash: e2878bf765c82910d452ae2cdd9264a343ec1990
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="install-and-configure-an-on-premises-data-gateway"></a><span data-ttu-id="4a9c9-103">Instalación y configuración de una puerta de enlace de datos local</span><span class="sxs-lookup"><span data-stu-id="4a9c9-103">Install and configure an on-premises data gateway</span></span>
<span data-ttu-id="4a9c9-104">Se requiere una puerta de enlace de datos local cuando uno o varios servidores de servicios de análisis de Azure en Hola mismo región conectarse a orígenes de datos locales de tooon.</span><span class="sxs-lookup"><span data-stu-id="4a9c9-104">An on-premises data gateway is required when one or more Azure Analysis Services servers in hello same region connect tooon-premises data sources.</span></span> <span data-ttu-id="4a9c9-105">toolearn más información acerca de la puerta de enlace de hello, consulte [puerta de enlace de datos local](analysis-services-gateway.md).</span><span class="sxs-lookup"><span data-stu-id="4a9c9-105">toolearn more about hello gateway, see [On-premises data gateway](analysis-services-gateway.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="4a9c9-106">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="4a9c9-106">Prerequisites</span></span>
<span data-ttu-id="4a9c9-107">**Requisitos mínimos:**</span><span class="sxs-lookup"><span data-stu-id="4a9c9-107">**Minimum Requirements:**</span></span>

* <span data-ttu-id="4a9c9-108">.NET Framework 4.5</span><span class="sxs-lookup"><span data-stu-id="4a9c9-108">.NET 4.5 Framework</span></span>
* <span data-ttu-id="4a9c9-109">versión de 64 bits de Windows 7 o Windows Server 2008 R2 (o posterior)</span><span class="sxs-lookup"><span data-stu-id="4a9c9-109">64-bit version of Windows 7 / Windows Server 2008 R2 (or later)</span></span>

<span data-ttu-id="4a9c9-110">**Se recomienda que use:**</span><span class="sxs-lookup"><span data-stu-id="4a9c9-110">**Recommended:**</span></span>

* <span data-ttu-id="4a9c9-111">CPU de 8 núcleos</span><span class="sxs-lookup"><span data-stu-id="4a9c9-111">8 Core CPU</span></span>
* <span data-ttu-id="4a9c9-112">8 GB de memoria</span><span class="sxs-lookup"><span data-stu-id="4a9c9-112">8 GB Memory</span></span>
* <span data-ttu-id="4a9c9-113">versión de 64 bits de Windows 2012 R2 (o posterior)</span><span class="sxs-lookup"><span data-stu-id="4a9c9-113">64-bit version of Windows 2012 R2 (or later)</span></span>

<span data-ttu-id="4a9c9-114">**Consideraciones importantes:**</span><span class="sxs-lookup"><span data-stu-id="4a9c9-114">**Important considerations:**</span></span>

* <span data-ttu-id="4a9c9-115">Durante la instalación, al registrar la puerta de enlace con Azure, se selecciona región predeterminados de Hola para su suscripción.</span><span class="sxs-lookup"><span data-stu-id="4a9c9-115">During setup, when registering your gateway with Azure, hello default region for your subscription is selected.</span></span> <span data-ttu-id="4a9c9-116">Puede elegir otra región.</span><span class="sxs-lookup"><span data-stu-id="4a9c9-116">You can choose a different region.</span></span> <span data-ttu-id="4a9c9-117">Si tiene servidores en varias regiones, debe instalar una puerta de enlace en cada una de ellas.</span><span class="sxs-lookup"><span data-stu-id="4a9c9-117">If you have servers in more than one region, you must install a gateway for each region.</span></span> 
* <span data-ttu-id="4a9c9-118">no se puede instalar la puerta de enlace de Hello en un controlador de dominio.</span><span class="sxs-lookup"><span data-stu-id="4a9c9-118">hello gateway cannot be installed on a domain controller.</span></span>
* <span data-ttu-id="4a9c9-119">Solo se puede instalar una puerta de enlace en un equipo.</span><span class="sxs-lookup"><span data-stu-id="4a9c9-119">Only one gateway can be installed on a single computer.</span></span>
* <span data-ttu-id="4a9c9-120">Instalar la puerta de enlace de hello en un equipo que permanece en y no queda toosleep.</span><span class="sxs-lookup"><span data-stu-id="4a9c9-120">Install hello gateway on a computer that remains on and does not go toosleep.</span></span>
* <span data-ttu-id="4a9c9-121">No instale la puerta de enlace de hello en un equipo de la red de forma inalámbrica conectado tooyour.</span><span class="sxs-lookup"><span data-stu-id="4a9c9-121">Do not install hello gateway on a computer wirelessly connected tooyour network.</span></span> <span data-ttu-id="4a9c9-122">Puede disminuir el rendimiento.</span><span class="sxs-lookup"><span data-stu-id="4a9c9-122">Performance can be diminished.</span></span>


## <span data-ttu-id="4a9c9-123"><a name="download"></a>Descarga</span><span class="sxs-lookup"><span data-stu-id="4a9c9-123"><a name="download"></a>Download</span></span>
 [<span data-ttu-id="4a9c9-124">Descargar la puerta de enlace de Hola</span><span class="sxs-lookup"><span data-stu-id="4a9c9-124">Download hello gateway</span></span>](https://aka.ms/azureasgateway)

## <span data-ttu-id="4a9c9-125"><a name="install"></a>Instalación</span><span class="sxs-lookup"><span data-stu-id="4a9c9-125"><a name="install"></a>Install</span></span>

1. <span data-ttu-id="4a9c9-126">Ejecute la configuración.</span><span class="sxs-lookup"><span data-stu-id="4a9c9-126">Run setup.</span></span>

2. <span data-ttu-id="4a9c9-127">Seleccione una ubicación, acepte los términos de Hola y, a continuación, haga clic en **instalar**.</span><span class="sxs-lookup"><span data-stu-id="4a9c9-127">Select a location, accept hello terms, and then click **Install**.</span></span>

   ![Ubicación de instalación y términos de la licencia](media/analysis-services-gateway-install/aas-gateway-installer-accept.png)

3. <span data-ttu-id="4a9c9-129">Seleccione **Puerta de enlace de datos local (se recomienda)**.</span><span class="sxs-lookup"><span data-stu-id="4a9c9-129">Select **On-premises data gateway (recommended)**.</span></span> <span data-ttu-id="4a9c9-130">Azure Analysis Services no admite el modo personal.</span><span class="sxs-lookup"><span data-stu-id="4a9c9-130">Azure Analysis Services does not support personal mode.</span></span>

   ![Elección del tipo de puerta de enlace](media/analysis-services-gateway-install/aas-gateway-installer-shared.png)

4. <span data-ttu-id="4a9c9-132">Escriba una cuenta toosign en tooAzure.</span><span class="sxs-lookup"><span data-stu-id="4a9c9-132">Enter an account toosign in tooAzure.</span></span> <span data-ttu-id="4a9c9-133">cuenta de Hello debe estar en de Azure Active Directory su inquilino.</span><span class="sxs-lookup"><span data-stu-id="4a9c9-133">hello account must be in your tenant's Azure Active Directory.</span></span> <span data-ttu-id="4a9c9-134">Esta cuenta se usa para el Administrador de puerta de enlace de Hola.</span><span class="sxs-lookup"><span data-stu-id="4a9c9-134">This account is used for hello gateway administrator.</span></span> 

   ![Escriba una cuenta toosign en tooAzure](media/analysis-services-gateway-install/aas-gateway-installer-account.png)

   > [!NOTE]
   > <span data-ttu-id="4a9c9-136">Si inicia sesión con una cuenta de dominio, será asignado tooyour de cuenta profesional en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="4a9c9-136">If you sign in with a domain account, it will be mapped tooyour organizational account in Azure AD.</span></span> <span data-ttu-id="4a9c9-137">Se utilizará la cuenta de su organización como administrador de puerta de enlace de Hola Hola.</span><span class="sxs-lookup"><span data-stu-id="4a9c9-137">Your organizational account will be used as hello hello gateway administrator.</span></span>

## <span data-ttu-id="4a9c9-138"><a name="register"></a>Registro</span><span class="sxs-lookup"><span data-stu-id="4a9c9-138"><a name="register"></a>Register</span></span>
<span data-ttu-id="4a9c9-139">En orden toocreate un recurso de puerta de enlace de Azure, debe registrar instancia local de hello instalada con hello puerta de enlace de servicio en la nube.</span><span class="sxs-lookup"><span data-stu-id="4a9c9-139">In order toocreate a gateway resource in Azure, you must register hello local instance you installed with hello Gateway Cloud Service.</span></span> 

1.  <span data-ttu-id="4a9c9-140">Seleccione **Registrar una nueva puerta de enlace en este equipo**.</span><span class="sxs-lookup"><span data-stu-id="4a9c9-140">Select **Register a new gateway on this computer**.</span></span>

    ![Registro](media/analysis-services-gateway-install/aas-gateway-register-new.png)

2. <span data-ttu-id="4a9c9-142">Escriba el nombre y la clave de recuperación de la puerta de enlace.</span><span class="sxs-lookup"><span data-stu-id="4a9c9-142">Type a name and recovery key for your gateway.</span></span> <span data-ttu-id="4a9c9-143">De forma predeterminada, la puerta de enlace de hello usa región predeterminados de la suscripción.</span><span class="sxs-lookup"><span data-stu-id="4a9c9-143">By default, hello gateway uses your subscription's default region.</span></span> <span data-ttu-id="4a9c9-144">Si necesita tooselect una región distinta, seleccione **cambiar región**.</span><span class="sxs-lookup"><span data-stu-id="4a9c9-144">If you need tooselect a different region, select **Change Region**.</span></span>

   ![Registro](media/analysis-services-gateway-install/aas-gateway-register-name.png)


## <span data-ttu-id="4a9c9-146"><a name="create-resource"></a>Creación de un recurso de puerta de enlace de Azure</span><span class="sxs-lookup"><span data-stu-id="4a9c9-146"><a name="create-resource"></a>Create an Azure gateway resource</span></span>
<span data-ttu-id="4a9c9-147">Una vez que ha instalado y registrado la puerta de enlace, deberá toocreate un recurso de puerta de enlace en su suscripción de Azure.</span><span class="sxs-lookup"><span data-stu-id="4a9c9-147">After you've installed and registered your gateway, you need toocreate a gateway resource in your Azure subscription.</span></span> <span data-ttu-id="4a9c9-148">Inicie sesión en tooAzure con hello misma cuenta que usó al registrar la puerta de enlace de Hola.</span><span class="sxs-lookup"><span data-stu-id="4a9c9-148">Sign in tooAzure with hello same account you used when registering hello gateway.</span></span>

1. <span data-ttu-id="4a9c9-149">En Azure Portal, haga clic en **Crear un nuevo servicio** > **Enterprise Integration** > **Puerta de enlace de datos local** > **Crear**.</span><span class="sxs-lookup"><span data-stu-id="4a9c9-149">In Azure portal, click **Create a new service** > **Enterprise Integration** > **On-premises data gateway** > **Create**.</span></span>

   ![Creación de un recurso de puerta de enlace](media/analysis-services-gateway-install/aas-gateway-new-azure-resource.png)

2. <span data-ttu-id="4a9c9-151">En **Crear puerta de enlace de conexión**, escriba estos valores:</span><span class="sxs-lookup"><span data-stu-id="4a9c9-151">In **Create connection gateway**, enter these settings:</span></span>

    * <span data-ttu-id="4a9c9-152">**Nombre**: escriba un nombre para el recurso de puerta de enlace.</span><span class="sxs-lookup"><span data-stu-id="4a9c9-152">**Name**: Enter a name for your gateway resource.</span></span> 

    * <span data-ttu-id="4a9c9-153">**Suscripción**: seleccione Hola tooassociate de suscripción de Azure con su recurso de puerta de enlace.</span><span class="sxs-lookup"><span data-stu-id="4a9c9-153">**Subscription**: Select hello Azure subscription tooassociate with your gateway resource.</span></span> 
    <span data-ttu-id="4a9c9-154">Esta suscripción debe ser Hola misma suscripción que los servidores están en.</span><span class="sxs-lookup"><span data-stu-id="4a9c9-154">This subscription should be hello same subscription your servers are in.</span></span>
   
      <span data-ttu-id="4a9c9-155">suscripción de Hello predeterminada se basa en hello cuenta de Azure que usan toosign en.</span><span class="sxs-lookup"><span data-stu-id="4a9c9-155">hello default subscription is based on hello Azure account that you used toosign in.</span></span>

    * <span data-ttu-id="4a9c9-156">**Grupo de recursos**: cree un grupo de recursos o seleccione uno existente.</span><span class="sxs-lookup"><span data-stu-id="4a9c9-156">**Resource group**: Create a resource group or select an existing resource group.</span></span>

    * <span data-ttu-id="4a9c9-157">**Ubicación**: región Hola seleccione registrado la puerta de enlace.</span><span class="sxs-lookup"><span data-stu-id="4a9c9-157">**Location**: Select hello region you registered your gateway in.</span></span>

    * <span data-ttu-id="4a9c9-158">**Nombre de la instalación**: si la instalación de puerta de enlace no está seleccionada, la puerta de enlace de hello seleccione registrado.</span><span class="sxs-lookup"><span data-stu-id="4a9c9-158">**Installation Name**: If your gateway installation isn't already selected, select hello gateway registered.</span></span> 

    <span data-ttu-id="4a9c9-159">Cuando haya terminado, haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="4a9c9-159">When you're done, click **Create**.</span></span>

## <span data-ttu-id="4a9c9-160"><a name="connect-servers"></a>Conectarse a recursos de puerta de enlace de toohello de servidores</span><span class="sxs-lookup"><span data-stu-id="4a9c9-160"><a name="connect-servers"></a>Connect servers toohello gateway resource</span></span>

1. <span data-ttu-id="4a9c9-161">En la introducción al servidor de Azure Analysis Services, haga clic en **Puerta de enlace de datos local**.</span><span class="sxs-lookup"><span data-stu-id="4a9c9-161">In your Azure Analysis Services server overview, click **On-Premises Data Gateway**.</span></span>

   ![Conectar a servidor toogateway](media/analysis-services-gateway-install/aas-gateway-connect-server.png)

2. <span data-ttu-id="4a9c9-163">En **elegir una puerta de enlace de datos de On-Premises tooconnect**, seleccione el recurso de puerta de enlace y, a continuación, haga clic en **conectar la puerta de enlace seleccionado**.</span><span class="sxs-lookup"><span data-stu-id="4a9c9-163">In **Pick an On-Premises Data Gateway tooconnect**, select your gateway resource, and then click **Connect selected gateway**.</span></span>

   ![Conectarse a recursos de servidor toogateway](media/analysis-services-gateway-install/aas-gateway-connect-resource.png)

    > [!NOTE]
    > <span data-ttu-id="4a9c9-165">Si la puerta de enlace no aparece en la lista de hello, el servidor es probable que no está en Hola la misma región como región Hola que especificó al registrar la puerta de enlace de Hola.</span><span class="sxs-lookup"><span data-stu-id="4a9c9-165">If your gateway does not appear in hello list, your server is likely not in hello same region as hello region you specified when registering hello gateway.</span></span> 

<span data-ttu-id="4a9c9-166">Eso es todo.</span><span class="sxs-lookup"><span data-stu-id="4a9c9-166">That's it.</span></span> <span data-ttu-id="4a9c9-167">Si necesita tooopen puertos o realice cualquier solución de problemas, que seguro toocheck out [puerta de enlace de datos local](analysis-services-gateway.md).</span><span class="sxs-lookup"><span data-stu-id="4a9c9-167">If you need tooopen ports or do any troubleshooting, be sure toocheck out [On-premises data gateway](analysis-services-gateway.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="4a9c9-168">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="4a9c9-168">Next steps</span></span>
* [<span data-ttu-id="4a9c9-169">Administración de Analysis Services</span><span class="sxs-lookup"><span data-stu-id="4a9c9-169">Manage Analysis Services</span></span>](analysis-services-manage.md)   
* [<span data-ttu-id="4a9c9-170">Obtención de datos de Azure Analysis Services</span><span class="sxs-lookup"><span data-stu-id="4a9c9-170">Get data from Azure Analysis Services</span></span>](analysis-services-connect.md)
