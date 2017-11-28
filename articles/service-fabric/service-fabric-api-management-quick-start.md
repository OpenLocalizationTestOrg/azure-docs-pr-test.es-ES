---
title: "aaaAzure Service Fabric con inicio rápido de administración de API | Documentos de Microsoft"
description: "Esta guía le mostrará cómo tooquickly comenzar con la administración de API de Azure y el tejido de servicio."
services: service-fabric
documentationcenter: .net
author: vturecek
manager: timlt
editor: 
ms.assetid: 96176149-69bb-4b06-a72e-ebbfea84454b
ms.service: service-fabric
ms.devlang: dotNet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/01/2017
ms.author: vturecek
ms.openlocfilehash: f76f3f39a92f89892d6a02ecaab1ec3d343fe2a0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="service-fabric-with-azure-api-management-quick-start"></a><span data-ttu-id="24e10-103">Inicio rápido de Service Fabric con Azure API Management</span><span class="sxs-lookup"><span data-stu-id="24e10-103">Service Fabric with Azure API Management Quick Start</span></span>

<span data-ttu-id="24e10-104">Esta guía le mostrará cómo tooset una copia de seguridad administración de API de Azure con Service Fabric y configurar los primeros servicios de API operación toosend tráfico tooback-end de Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="24e10-104">This guide shows you how tooset up Azure API Management with Service Fabric and configure your first API operation toosend traffic tooback-end services in Service Fabric.</span></span> <span data-ttu-id="24e10-105">toolearn más información acerca de los escenarios de administración de API de Azure con Service Fabric, vea hello [Introducción](service-fabric-api-management-overview.md) artículo.</span><span class="sxs-lookup"><span data-stu-id="24e10-105">toolearn more about Azure API Management scenarios with Service Fabric, see hello [overview](service-fabric-api-management-overview.md) article.</span></span> 

## <a name="deploy-api-management-and-service-fabric-tooazure"></a><span data-ttu-id="24e10-106">Implementar la administración de API y el tejido de servicio tooAzure</span><span class="sxs-lookup"><span data-stu-id="24e10-106">Deploy API Management and Service Fabric tooAzure</span></span>

<span data-ttu-id="24e10-107">Hola primer paso es toodeploy administración de API y un tooAzure de clúster de Service Fabric en una red Virtual compartida.</span><span class="sxs-lookup"><span data-stu-id="24e10-107">hello first step is toodeploy API Management and a Service Fabric cluster tooAzure in a shared Virtual Network.</span></span> <span data-ttu-id="24e10-108">Esto permite toocommunicate de administración de API directamente con el tejido de servicio para que pueda realizar la detección de servicios, resolución de la partición de servicio y reenvíe el tráfico directamente tooany back-end del servicio de Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="24e10-108">This allows API Management toocommunicate directly with Service Fabric so it can perform service discovery, service partition resolution, and forward traffic directly tooany backend service in Service Fabric.</span></span>

### <a name="topology"></a><span data-ttu-id="24e10-109">Topología</span><span class="sxs-lookup"><span data-stu-id="24e10-109">Topology</span></span>

<span data-ttu-id="24e10-110">Esta guía implementa siguiente hello tooAzure topología en la que administración de API y el tejido de servicio están en subredes de Hola misma red Virtual:</span><span class="sxs-lookup"><span data-stu-id="24e10-110">This guide deploys hello following topology tooAzure in which API Management and Service Fabric are in subnets of hello same Virtual Network:</span></span>

 ![Leyenda de la imagen][sf-apim-topology-overview]

<span data-ttu-id="24e10-112">tooget a trabajar rápidamente, plantillas de administrador de recursos se proporcionan para cada paso de implementación:</span><span class="sxs-lookup"><span data-stu-id="24e10-112">tooget started quickly, Resource Manager templates are provided for each deployment step:</span></span>

 - <span data-ttu-id="24e10-113">Topología de red:</span><span class="sxs-lookup"><span data-stu-id="24e10-113">Network topology:</span></span>
    - <span data-ttu-id="24e10-114">[network.json][network-arm]</span><span class="sxs-lookup"><span data-stu-id="24e10-114">[network.json][network-arm]</span></span>
    - <span data-ttu-id="24e10-115">[network.parameters.json][network-parameters-arm]</span><span class="sxs-lookup"><span data-stu-id="24e10-115">[network.parameters.json][network-parameters-arm]</span></span>
 - <span data-ttu-id="24e10-116">Clúster de Service Fabric:</span><span class="sxs-lookup"><span data-stu-id="24e10-116">Service Fabric cluster:</span></span>
    - <span data-ttu-id="24e10-117">[cluster.json][cluster-arm]</span><span class="sxs-lookup"><span data-stu-id="24e10-117">[cluster.json][cluster-arm]</span></span>
    - <span data-ttu-id="24e10-118">[cluster.parameters.json][cluster-parameters-arm]</span><span class="sxs-lookup"><span data-stu-id="24e10-118">[cluster.parameters.json][cluster-parameters-arm]</span></span>
 - <span data-ttu-id="24e10-119">API Management:</span><span class="sxs-lookup"><span data-stu-id="24e10-119">API Management:</span></span>
    - <span data-ttu-id="24e10-120">[apim.json][apim-arm]</span><span class="sxs-lookup"><span data-stu-id="24e10-120">[apim.json][apim-arm]</span></span>
    - <span data-ttu-id="24e10-121">[apim.parameters.json][apim-parameters-arm]</span><span class="sxs-lookup"><span data-stu-id="24e10-121">[apim.parameters.json][apim-parameters-arm]</span></span>

### <a name="sign-in-tooazure-and-select-your-subscription"></a><span data-ttu-id="24e10-122">Inicie sesión en tooAzure y seleccione su suscripción</span><span class="sxs-lookup"><span data-stu-id="24e10-122">Sign in tooAzure and select your subscription</span></span>

<span data-ttu-id="24e10-123">En esta guía se usa [Azure PowerShell][azure-powershell].</span><span class="sxs-lookup"><span data-stu-id="24e10-123">This guide uses [Azure PowerShell][azure-powershell].</span></span> <span data-ttu-id="24e10-124">Cuando se inicia una nueva sesión de PowerShell, inicie sesión en tooyour cuenta de Azure y seleccione su suscripción antes de ejecutar comandos de Azure.</span><span class="sxs-lookup"><span data-stu-id="24e10-124">When you start a new PowerShell session, sign in tooyour Azure account and select your subscription before you execute Azure commands.</span></span>
 
<span data-ttu-id="24e10-125">Inicie sesión en tooyour cuenta de Azure:</span><span class="sxs-lookup"><span data-stu-id="24e10-125">Sign in tooyour Azure account:</span></span>

```powershell
PS > Login-AzureRmAccount
```

<span data-ttu-id="24e10-126">Seleccione su suscripción:</span><span class="sxs-lookup"><span data-stu-id="24e10-126">Select your subscription:</span></span>

```powershell
PS > Get-AzureRmSubscription
PS > Set-AzureRmContext -SubscriptionId <guid>
```

### <a name="create-a-resource-group"></a><span data-ttu-id="24e10-127">Crear un grupo de recursos</span><span class="sxs-lookup"><span data-stu-id="24e10-127">Create a resource group</span></span>

<span data-ttu-id="24e10-128">Cree un grupo de recursos para la implementación.</span><span class="sxs-lookup"><span data-stu-id="24e10-128">Create a new resource group for your deployment.</span></span> <span data-ttu-id="24e10-129">Asígnele un nombre y una ubicación.</span><span class="sxs-lookup"><span data-stu-id="24e10-129">Give it a name and a location.</span></span>

```powershell
PS > New-AzureRmResourceGroup -Name <my-resource-group> -Location westus
```

### <a name="deploy-hello-network-topology"></a><span data-ttu-id="24e10-130">Implementar la topología de red de Hola</span><span class="sxs-lookup"><span data-stu-id="24e10-130">Deploy hello network topology</span></span>

<span data-ttu-id="24e10-131">Hola primer paso es tooset una toowhich de topología de red de hello administración de API y clúster de Service Fabric Hola se va a implementar.</span><span class="sxs-lookup"><span data-stu-id="24e10-131">hello first step is tooset up hello network topology toowhich API Management and hello Service Fabric cluster will be deployed.</span></span> <span data-ttu-id="24e10-132">Hola [network.json] [ network-arm] plantilla de administrador de recursos es toocreate configurado una red Virtual (VNET) con dos subredes y dos grupos de seguridad de red (NSG).</span><span class="sxs-lookup"><span data-stu-id="24e10-132">hello [network.json][network-arm] Resource Manager template is configured toocreate a Virtual Network (VNET) with two subnets and two Network Security Groups (NSG).</span></span> 

<span data-ttu-id="24e10-133">Hola [network.parameters.json] [ network-parameters-arm] archivo de parámetros contiene nombres de Hola de subredes de Hola y NSG que se implementará en administración de API y el tejido de servicio.</span><span class="sxs-lookup"><span data-stu-id="24e10-133">hello [network.parameters.json][network-parameters-arm] parameters file contains hello names of hello subnets and NSGs that API Management and Service Fabric will be deployed to.</span></span> <span data-ttu-id="24e10-134">En esta guía, los valores de parámetro hello no es necesario toobe cambiado.</span><span class="sxs-lookup"><span data-stu-id="24e10-134">For this guide, hello parameter values do not need toobe changed.</span></span> <span data-ttu-id="24e10-135">plantillas de administración de API y el servicio Administrador de recursos del tejido de Hello utilizan estos valores, por lo que si se modifican aquí, debe modificar otras plantillas de administrador de recursos en hello en consecuencia.</span><span class="sxs-lookup"><span data-stu-id="24e10-135">hello API Management and Service Fabric Resource Manager templates use these values, so if they are modified here, you must modify them in hello other Resource Manager templates accordingly.</span></span> 

 1. <span data-ttu-id="24e10-136">Descargar Hola siguiente archivo de plantilla y los parámetros del Administrador de recursos:</span><span class="sxs-lookup"><span data-stu-id="24e10-136">Download hello following Resource Manager template and parameters file:</span></span>

    - <span data-ttu-id="24e10-137">[network.json][network-arm]</span><span class="sxs-lookup"><span data-stu-id="24e10-137">[network.json][network-arm]</span></span>
    - <span data-ttu-id="24e10-138">[network.parameters.json][network-parameters-arm]</span><span class="sxs-lookup"><span data-stu-id="24e10-138">[network.parameters.json][network-parameters-arm]</span></span>

 2. <span data-ttu-id="24e10-139">Usar hello siguiendo PowerShell toodeploy Hola Administrador de recursos plantilla y parámetros archivos de comandos para el programa de instalación de red de hello:</span><span class="sxs-lookup"><span data-stu-id="24e10-139">Use hello following PowerShell command toodeploy hello Resource Manager template and parameter files for hello network setup:</span></span>

    ```powershell
    PS > New-AzureRmResourceGroupDeployment -ResourceGroupName <my-resource-group> -TemplateFile .\network.json -TemplateParameterFile .\network.parameters.json -Verbose
    ```

### <a name="deploy-hello-service-fabric-cluster"></a><span data-ttu-id="24e10-140">Implementar el clúster de Service Fabric Hola</span><span class="sxs-lookup"><span data-stu-id="24e10-140">Deploy hello Service Fabric cluster</span></span>

<span data-ttu-id="24e10-141">Una vez que han terminado de recursos de red de hello implementar, Hola siguiente paso es toodeploy toohello de clúster de Service Fabric red virtual en la subred de Hola y NSG designado para el clúster de Service Fabric Hola.</span><span class="sxs-lookup"><span data-stu-id="24e10-141">Once hello network resources have finished deploying, hello next step is toodeploy a Service Fabric cluster toohello VNET in hello subnet and NSG designated for hello Service Fabric cluster.</span></span> <span data-ttu-id="24e10-142">Para este tutorial, plantilla de servicio Administrador de recursos de tejido de hello es toouse preconfigurada Hola nombres de hello red virtual, subred y NSG que configuró en el paso anterior de Hola.</span><span class="sxs-lookup"><span data-stu-id="24e10-142">For this tutorial, hello Service Fabric Resource Manager template is pre-configured toouse hello names of hello VNET, subnet, and NSG that you set up in hello previous step.</span></span> 

<span data-ttu-id="24e10-143">plantilla de administrador de recursos de clúster de Service Fabric Hello es toocreate configurado un clúster segura con seguridad de certificado.</span><span class="sxs-lookup"><span data-stu-id="24e10-143">hello Service Fabric cluster Resource Manager template is configured toocreate a secure cluster with certificate security.</span></span> <span data-ttu-id="24e10-144">certificado de Hello es comunicación de nodo a nodo toosecure usado para el clúster y toomanage usuario acceso tooyour Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="24e10-144">hello certificate is used toosecure node-to-node communication for your cluster and toomanage user access tooyour Service Fabric cluster.</span></span> <span data-ttu-id="24e10-145">Administración de API usa este Hola de tooaccess servicio de nomenclatura de tejido de servicio de certificado para la detección de servicios.</span><span class="sxs-lookup"><span data-stu-id="24e10-145">API Management uses this certificate tooaccess  hello Service Fabric Naming Service for service discovery.</span></span>

<span data-ttu-id="24e10-146">Este paso requiere un certificado en Key Vault para la seguridad del clúster.</span><span class="sxs-lookup"><span data-stu-id="24e10-146">This step requires having a certificate in Key Vault for cluster security.</span></span> <span data-ttu-id="24e10-147">Para más información sobre cómo configurar un clúster seguro en Key Vault, consulte [esta guía sobre la creación de un clúster de Azure con Resource Manager](service-fabric-cluster-creation-via-arm.md).</span><span class="sxs-lookup"><span data-stu-id="24e10-147">For more information on setting up a secure cluster with Key Vault, see [this guide on creating a cluster in Azure using Resource Manager](service-fabric-cluster-creation-via-arm.md)</span></span>

> [!NOTE]
> <span data-ttu-id="24e10-148">Autenticación de Azure Active Directory se puede agregar en suma toohello certificado utilizado para el acceso al clúster.</span><span class="sxs-lookup"><span data-stu-id="24e10-148">You may add Azure Active Directory authentication in addition toohello certificate used for cluster access.</span></span> <span data-ttu-id="24e10-149">Azure Active Directory es hello recomendada clúster Service Fabric de tooyour de acceso de usuario de manera toomanage, pero es toocomplete no es necesario en este tutorial.</span><span class="sxs-lookup"><span data-stu-id="24e10-149">Azure Active Directory is hello recommended way toomanage user access tooyour Service Fabric cluster, but is not necessary toocomplete this tutorial.</span></span> <span data-ttu-id="24e10-150">En cualquier caso, se necesita un certificado para la seguridad de nodo a nodo del clúster y para la autenticación de Azure API Management, que actualmente no admite la autenticación con Azure Active Directory para el back-end de Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="24e10-150">A certificate is required either way for cluster node-to-node security and for Azure API Management authentication, which currently does not support authenticating with Azure Active Directory for a Service Fabric backend.</span></span>

 1. <span data-ttu-id="24e10-151">Descargar Hola siguiente archivo de plantilla y los parámetros del Administrador de recursos:</span><span class="sxs-lookup"><span data-stu-id="24e10-151">Download hello following Resource Manager template and parameters file:</span></span>
 
    - <span data-ttu-id="24e10-152">[cluster.json][cluster-arm]</span><span class="sxs-lookup"><span data-stu-id="24e10-152">[cluster.json][cluster-arm]</span></span>
    - <span data-ttu-id="24e10-153">[cluster.parameters.json][cluster-parameters-arm]</span><span class="sxs-lookup"><span data-stu-id="24e10-153">[cluster.parameters.json][cluster-parameters-arm]</span></span>

 2. <span data-ttu-id="24e10-154">Rellenar parámetros vacía de hello en hello `cluster.parameters.json` archivo para la implementación, incluyendo hello [información del almacén de claves](service-fabric-cluster-creation-via-arm.md#set-up-a-key-vault) para el certificado de clúster.</span><span class="sxs-lookup"><span data-stu-id="24e10-154">Fill in hello empty parameters in hello `cluster.parameters.json` file for your deployment, including hello [Key Vault information](service-fabric-cluster-creation-via-arm.md#set-up-a-key-vault) for your cluster certificate.</span></span>

 3. <span data-ttu-id="24e10-155">Usar hello después PowerShell comando toodeploy Hola Administrador de recursos plantilla y parámetros archivos toocreate Hola clúster de Service Fabric:</span><span class="sxs-lookup"><span data-stu-id="24e10-155">Use hello following PowerShell command toodeploy hello Resource Manager template and parameter files toocreate hello Service Fabric cluster:</span></span>

    ```powershell
    PS > New-AzureRmResourceGroupDeployment -ResourceGroupName <my-resource-group> -TemplateFile .\cluster.json -TemplateParameterFile .\cluster.parameters.json -Verbose
    ```

### <a name="deploy-api-management"></a><span data-ttu-id="24e10-156">Implementación de API Management</span><span class="sxs-lookup"><span data-stu-id="24e10-156">Deploy API Management</span></span>

<span data-ttu-id="24e10-157">Por último, implementar la administración de API toohello red virtual en la subred de Hola y NSG designado para la administración de API.</span><span class="sxs-lookup"><span data-stu-id="24e10-157">Finally, deploy API Management toohello VNET in hello subnet and NSG designated for API Management.</span></span> <span data-ttu-id="24e10-158">No es necesario toowait para toofinish de implementación de clúster de Service Fabric Hola antes de implementar la administración de API.</span><span class="sxs-lookup"><span data-stu-id="24e10-158">You do not need toowait for hello Service Fabric cluster deployment toofinish before deploying API Management.</span></span> 

<span data-ttu-id="24e10-159">Para este tutorial, plantilla de administrador de recursos de administración de API de hello es toouse preconfigurada Hola nombres de hello red virtual, subred y NSG que configuró en el paso anterior de Hola.</span><span class="sxs-lookup"><span data-stu-id="24e10-159">For this tutorial, hello API Management Resource Manager template is pre-configured toouse hello names of hello VNET, subnet, and NSG that you set up in hello previous step.</span></span> 

 1. <span data-ttu-id="24e10-160">Descargar Hola siguiente archivo de plantilla y los parámetros del Administrador de recursos:</span><span class="sxs-lookup"><span data-stu-id="24e10-160">Download hello following Resource Manager template and parameters file:</span></span>
 
    - <span data-ttu-id="24e10-161">[apim.json][apim-arm]</span><span class="sxs-lookup"><span data-stu-id="24e10-161">[apim.json][apim-arm]</span></span>
    - <span data-ttu-id="24e10-162">[apim.parameters.json][apim-parameters-arm]</span><span class="sxs-lookup"><span data-stu-id="24e10-162">[apim.parameters.json][apim-parameters-arm]</span></span>

 2. <span data-ttu-id="24e10-163">Rellenar parámetros vacía de hello en hello `apim.parameters.json` para su implementación.</span><span class="sxs-lookup"><span data-stu-id="24e10-163">Fill in hello empty parameters in hello `apim.parameters.json` for your deployment.</span></span>

 3. <span data-ttu-id="24e10-164">Usar hello siguientes PowerShell comando toodeploy Hola Administrador de recursos plantilla y parámetros archivos para la administración de API:</span><span class="sxs-lookup"><span data-stu-id="24e10-164">Use hello following PowerShell command toodeploy hello Resource Manager template and parameter files for API Management:</span></span>

    ```powershell
    PS > New-AzureRmResourceGroupDeployment -ResourceGroupName <my-resource-group> -TemplateFile .\apim.json -TemplateParameterFile .\apim.parameters.json -Verbose
    ```

## <a name="configure-api-management"></a><span data-ttu-id="24e10-165">Configuración de API Management</span><span class="sxs-lookup"><span data-stu-id="24e10-165">Configure API Management</span></span>

<span data-ttu-id="24e10-166">Una vez implementados API Management y el clúster de Service Fabric, puede configurar un back-end de Service Fabric en API Management.</span><span class="sxs-lookup"><span data-stu-id="24e10-166">Once your API Management and Service Fabric cluster are deployed, you can configure a Service Fabric backend in API Management.</span></span> <span data-ttu-id="24e10-167">Esto le permite toocreate una directiva de servicio de back-end que envía el clúster de Service Fabric tooyour de tráfico.</span><span class="sxs-lookup"><span data-stu-id="24e10-167">This allows you toocreate a backend service policy that sends traffic tooyour Service Fabric cluster.</span></span>

### <a name="api-management-security"></a><span data-ttu-id="24e10-168">Seguridad de API Management</span><span class="sxs-lookup"><span data-stu-id="24e10-168">API Management Security</span></span>

<span data-ttu-id="24e10-169">tooconfigure Hola Service Fabric back-end, primero debe tooconfigure configuración de seguridad de administración de API.</span><span class="sxs-lookup"><span data-stu-id="24e10-169">tooconfigure hello Service Fabric backend, you first need tooconfigure API Management security settings.</span></span> <span data-ttu-id="24e10-170">configuración de seguridad de tooconfigure, vaya a servicio de administración de API tooyour de hello portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="24e10-170">tooconfigure security settings, go tooyour API Management service in hello Azure portal.</span></span>

#### <a name="enable-hello-api-management-rest-api"></a><span data-ttu-id="24e10-171">Habilitar Hola API de REST de administración</span><span class="sxs-lookup"><span data-stu-id="24e10-171">Enable hello API Management REST API</span></span>

<span data-ttu-id="24e10-172">Hola API de REST de administración está actualmente tooconfigure de forma única un servicio back-end de Hola.</span><span class="sxs-lookup"><span data-stu-id="24e10-172">hello API Management REST API is currently hello only way tooconfigure a backend service.</span></span> <span data-ttu-id="24e10-173">primer paso de Hello es tooenable hello API de REST de administración y protegerla.</span><span class="sxs-lookup"><span data-stu-id="24e10-173">hello first step is tooenable hello API Management REST API and secure it.</span></span>

 1. <span data-ttu-id="24e10-174">En el servicio de administración de API de hello, seleccione **API de administración - versión preliminar** en **seguridad**.</span><span class="sxs-lookup"><span data-stu-id="24e10-174">In hello API Management service, select **Management API - PREVIEW** under **Security**.</span></span>
 2. <span data-ttu-id="24e10-175">Comprobar hello **habilitar API de REST de administración de API** casilla de verificación.</span><span class="sxs-lookup"><span data-stu-id="24e10-175">Check hello **Enable API Management REST API** checkbox.</span></span>
 3. <span data-ttu-id="24e10-176">Tenga en cuenta Hola URL de la API de administración; éste es dirección URL de hello usaremos tooset posterior de back-end de hello Service Fabric</span><span class="sxs-lookup"><span data-stu-id="24e10-176">Note hello Management API URL - this is hello URL we'll use later tooset up hello Service Fabric backend</span></span>
 4. <span data-ttu-id="24e10-177">Generar un **Token de acceso** al seleccionar una fecha de expiración y una clave, a continuación, haga clic en hello **generar** botón hacia la parte inferior de Hola de página de Hola.</span><span class="sxs-lookup"><span data-stu-id="24e10-177">Generate an **access Token** by selecting an expiry date and a key, then click hello **Generate** button toward hello bottom of hello page.</span></span>
 5. <span data-ttu-id="24e10-178">Hola copia **token de acceso** y guárdelo: vamos a usar en hello pasos.</span><span class="sxs-lookup"><span data-stu-id="24e10-178">Copy hello **access token** and save it - we'll use this in hello following steps.</span></span> <span data-ttu-id="24e10-179">Tenga en cuenta que esto es diferente de la clave principal de Hola y la clave secundaria.</span><span class="sxs-lookup"><span data-stu-id="24e10-179">Note this is different from hello primary key and secondary key.</span></span>

#### <a name="upload-a-service-fabric-client-certificate"></a><span data-ttu-id="24e10-180">Carga de un certificado de cliente de Service Fabric</span><span class="sxs-lookup"><span data-stu-id="24e10-180">Upload a Service Fabric client certificate</span></span>

<span data-ttu-id="24e10-181">Administración de API debe autenticarse con el clúster de Service Fabric para la detección de servicio utilizando un certificado de cliente que tiene acceso tooyour clúster.</span><span class="sxs-lookup"><span data-stu-id="24e10-181">API Management must authenticate with your Service Fabric cluster for service discovery using a client certificate that has access tooyour cluster.</span></span> <span data-ttu-id="24e10-182">Por simplicidad, este tutorial se utiliza Hola mismo certificado que se especificó al crear el clúster de Service Fabric hello, que puede ser tooaccess usados de forma predeterminada el clúster.</span><span class="sxs-lookup"><span data-stu-id="24e10-182">For simplicity, this tutorial uses hello same certificate specified when creating hello Service Fabric cluster, which by default can be used tooaccess your cluster.</span></span>

 1. <span data-ttu-id="24e10-183">En el servicio de administración de API de hello, seleccione **certificados de cliente - vista previa** en **seguridad**.</span><span class="sxs-lookup"><span data-stu-id="24e10-183">In hello API Management service, select **Client certificates - PREVIEW** under **Security**.</span></span>
 2. <span data-ttu-id="24e10-184">Haga clic en hello **+ agregar** botón</span><span class="sxs-lookup"><span data-stu-id="24e10-184">Click hello **+ Add** button</span></span>
 2. <span data-ttu-id="24e10-185">Hola Seleccione archivo de clave privada (.pfx) del certificado de clúster de Hola que especificó al crear el clúster de Service Fabric, asígnele un nombre y proporcionar la contraseña de clave privada de Hola.</span><span class="sxs-lookup"><span data-stu-id="24e10-185">Select hello private key file (.pfx) of hello cluster certificate that you specified when creating your Service Fabric cluster, give it a name, and provide hello private key password.</span></span>

> [!NOTE]
> <span data-ttu-id="24e10-186">Este tutorial usa Hola mismo certificado para la seguridad de cliente autenticación y clúster de nodo a nodo.</span><span class="sxs-lookup"><span data-stu-id="24e10-186">This tutorial uses hello same certificate for client authentication and cluster node-to-node security.</span></span> <span data-ttu-id="24e10-187">Puede utilizar un certificado de cliente independiente si tienes un tooaccess configurado el clúster de Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="24e10-187">You may use a separate client certificate if you have one configured tooaccess your Service Fabric cluster.</span></span>

### <a name="configure-hello-backend"></a><span data-ttu-id="24e10-188">Configurar Hola back-end</span><span class="sxs-lookup"><span data-stu-id="24e10-188">Configure hello backend</span></span>

<span data-ttu-id="24e10-189">Ahora que se configura la seguridad de administración de API, puede configurar el back-end de hello Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="24e10-189">Now that API Management security is configured, you can configure hello Service Fabric backend.</span></span> <span data-ttu-id="24e10-190">Para servidores backend de Service Fabric, clúster de Service Fabric hello es Hola back-end, en lugar de un servicio de Service Fabric específico.</span><span class="sxs-lookup"><span data-stu-id="24e10-190">For Service Fabric backends, hello Service Fabric cluster is hello backend, rather than a specific Service Fabric service.</span></span> <span data-ttu-id="24e10-191">Esto permite un toomore de tooroute de directiva único que un servicio en clúster de Hola.</span><span class="sxs-lookup"><span data-stu-id="24e10-191">This allows a single policy tooroute toomore than one service in hello cluster.</span></span>

<span data-ttu-id="24e10-192">Este paso requiere Hola token de acceso que ha generado anteriormente y Hola huella digital para el certificado de clúster que se cargó tooAPI administración en el paso anterior de Hola.</span><span class="sxs-lookup"><span data-stu-id="24e10-192">This step requires hello access token you generated earlier and hello thumbprint for your cluster certificate you uploaded tooAPI Management in hello previous step.</span></span>

> [!NOTE]
> <span data-ttu-id="24e10-193">Si utiliza un certificado de cliente independiente en el paso anterior de hello para la administración de API, deberá huella digital de hello certificado de cliente de hello en suma toohello clúster huella digital del certificado en este paso.</span><span class="sxs-lookup"><span data-stu-id="24e10-193">If you used a separate client certificate in hello previous step for API Management, you need hello thumbprint for hello client certificate in addition toohello cluster certificate thumbprint in this step.</span></span>

<span data-ttu-id="24e10-194">Enviar Hola después toohello de solicitud HTTP PUT URL de la API de administración de API que anotó anteriormente al habilitar el servicio de back-end de hello API de REST de administración tooconfigure Hola Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="24e10-194">Send hello following HTTP PUT request toohello API Management API URL you noted earlier when enabling hello API Management REST API tooconfigure hello Service Fabric backend service.</span></span> <span data-ttu-id="24e10-195">Debería ver un `HTTP 201 Created` en la respuesta al comando Hola se ejecuta correctamente.</span><span class="sxs-lookup"><span data-stu-id="24e10-195">You should see an `HTTP 201 Created` response when hello command succeeds.</span></span> <span data-ttu-id="24e10-196">Para obtener más información sobre cada campo, consulte Administración de API de hello [documentación de referencia de API de back-end](https://docs.microsoft.com/rest/api/apimanagement/apimanagementrest/azure-api-management-rest-api-contract-reference#a-namebackenda-backend).</span><span class="sxs-lookup"><span data-stu-id="24e10-196">For more information on each field, see hello API Management [backend API reference documentation](https://docs.microsoft.com/rest/api/apimanagement/apimanagementrest/azure-api-management-rest-api-contract-reference#a-namebackenda-backend).</span></span>

<span data-ttu-id="24e10-197">Comando HTTP y dirección URL:</span><span class="sxs-lookup"><span data-stu-id="24e10-197">HTTP command and URL:</span></span>
```http
PUT https://your-apim.management.azure-api.net/backends/servicefabric?api-version=2016-10-10
```

<span data-ttu-id="24e10-198">Encabezados de solicitud:</span><span class="sxs-lookup"><span data-stu-id="24e10-198">Request headers:</span></span>
```http
Authorization: SharedAccessSignature <your access token>
Content-Type: application/json
```

<span data-ttu-id="24e10-199">Cuerpo de la solicitud:</span><span class="sxs-lookup"><span data-stu-id="24e10-199">Request body:</span></span>
```http
{
    "description": "<description>",
    "url": "<fallback service name>",
    "protocol": "http",
    "resourceId": "<cluster HTTP management endpoint>",
    "properties": {
        "serviceFabricCluster": {
            "managementEndpoints": [ "<cluster HTTP management endpoint>" ],
            "clientCertificateThumbprint": "<client cert thumbprint>",
            "serverCertificateThumbprints": [ "<cluster cert thumbprint>" ],
            "maxPartitionResolutionRetries" : 5
        }
    }
}
```

<span data-ttu-id="24e10-200">Hola **url** parámetro aquí es un nombre de servicio de acceso completa de un servicio en el clúster que todas las solicitudes enruta tooby predeterminado si se especifica ningún nombre de servicio en una directiva de back-end.</span><span class="sxs-lookup"><span data-stu-id="24e10-200">hello **url** parameter here is a fully-qualified service name of a service in your cluster that all requests are routed tooby default if no service name is specified in a backend policy.</span></span> <span data-ttu-id="24e10-201">Puede usar un nombre de servicio falsa, como "fabric: / falsa/servicio" Si no piensa toohave un servicio de reserva.</span><span class="sxs-lookup"><span data-stu-id="24e10-201">You may use a fake service name, such as "fabric:/fake/service" if you do not intend toohave a fallback service.</span></span>

<span data-ttu-id="24e10-202">Consulte administración de API de toohello [documentación de referencia de API de back-end](https://docs.microsoft.com/rest/api/apimanagement/apimanagementrest/azure-api-management-rest-api-contract-reference#a-namebackenda-backend) para obtener más detalles sobre cada campo.</span><span class="sxs-lookup"><span data-stu-id="24e10-202">Refer toohello API Management [backend API reference documentation](https://docs.microsoft.com/rest/api/apimanagement/apimanagementrest/azure-api-management-rest-api-contract-reference#a-namebackenda-backend) for more details on each field.</span></span>

#### <a name="example"></a><span data-ttu-id="24e10-203">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="24e10-203">Example</span></span>

```http
PUT https://your-apim.management.azure-api.net/backends/servicefabric?api-version=2016-10-10
Authorization: SharedAccessSignature 230948023984&Ld93cRGcNU6KZ4uVz7JlfTec4eX43Q9Nu8ndatOgBzs6+f559Pkf3iHX2cSge+r42pn35qGY3TitjrIl13hwcQ==
Content-Type: application/json

{
    "description": "My Service Fabric backend",
    "url": "fabric:/myapp/myservice",
    "protocol": "http",
    "resourceId": "https://your-cluster.westus.cloudapp.azure.com:19080",
    "properties": {
        "serviceFabricCluster": {
            "managementEndpoints": ["https://your-cluster.westus.cloudapp.azure.com:19080"],
            "clientCertificateThumbprint": "57bc463aba3aea3a12a18f36f44154f819f0fe32",
            "serverCertificateThumbprints": ["57bc463aba3aea3a12a18f36f44154f819f0fe32"],
            "maxPartitionResolutionRetries" : 5
        }
    }
}
```

## <a name="deploy-a-service-fabric-back-end-service"></a><span data-ttu-id="24e10-204">Implementación de un servicio de back-end de Service Fabric</span><span class="sxs-lookup"><span data-stu-id="24e10-204">Deploy a Service Fabric back-end service</span></span>

<span data-ttu-id="24e10-205">Ahora que tiene Hola que Service Fabric configurado como un tooAPI de back-end administración, puede crear directivas de back-end para las API que envían tráfico tooyour servicios de Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="24e10-205">Now that you have hello Service Fabric configured as a backend tooAPI Management, you can author backend policies for your APIs that send traffic tooyour Service Fabric services.</span></span> <span data-ttu-id="24e10-206">Pero primero necesita un servicio que se ejecuta en las solicitudes de tooaccept de Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="24e10-206">But first you need a service running in Service Fabric tooaccept requests.</span></span>

### <a name="create-a-service-fabric-service-with-an-http-endpoint"></a><span data-ttu-id="24e10-207">Creación de un servicio de Service Fabric con un punto de conexión HTTP</span><span class="sxs-lookup"><span data-stu-id="24e10-207">Create a Service Fabric service with an HTTP endpoint</span></span>

<span data-ttu-id="24e10-208">Para este tutorial, vamos a crear un básica sin estado ASP.NET confiable servicio principal con plantilla de proyecto de API Web de hello predeterminada.</span><span class="sxs-lookup"><span data-stu-id="24e10-208">For this tutorial, we'll create a basic stateless ASP.NET Core Reliable Service using hello default Web API project template.</span></span> <span data-ttu-id="24e10-209">Así se crea un punto de conexión HTTP para el servicio que se expondrá en Azure API Management:</span><span class="sxs-lookup"><span data-stu-id="24e10-209">This creates an HTTP endpoint for your service, which you'll expose through Azure API Management:</span></span>

```
/api/values
```

<span data-ttu-id="24e10-210">Empiece por [configurar el entorno de desarrollo para ASP.NET Core](service-fabric-add-a-web-frontend.md#set-up-your-environment-for-aspnet-core).</span><span class="sxs-lookup"><span data-stu-id="24e10-210">Start by [setting up your development environment for ASP.NET Core development](service-fabric-add-a-web-frontend.md#set-up-your-environment-for-aspnet-core).</span></span>

<span data-ttu-id="24e10-211">Una vez configurado el entorno de desarrollo, inicie Visual Studio como administrador y cree un servicio ASP.NET Core:</span><span class="sxs-lookup"><span data-stu-id="24e10-211">Once your development environment is set up, start Visual Studio as Administrator and create an ASP.NET Core service:</span></span>

 1. <span data-ttu-id="24e10-212">En Visual Studio, seleccione Archivo -> Nuevo proyecto.</span><span class="sxs-lookup"><span data-stu-id="24e10-212">In Visual Studio, select File -> New Project.</span></span>
 2. <span data-ttu-id="24e10-213">Seleccione la plantilla de aplicación de servicio Fabric hello en la nube y asígnele el nombre **"ApiApplication"**.</span><span class="sxs-lookup"><span data-stu-id="24e10-213">Select hello Service Fabric Application template under Cloud and name it **"ApiApplication"**.</span></span>
 3. <span data-ttu-id="24e10-214">Seleccione Hola plantilla de servicio de ASP.NET Core y proyecto de hello name **"WebApiService"**.</span><span class="sxs-lookup"><span data-stu-id="24e10-214">Select hello ASP.NET Core service template and name hello project **"WebApiService"**.</span></span>
 4. <span data-ttu-id="24e10-215">Seleccione la plantilla de proyecto de hello Web API de ASP.NET Core 1.1.</span><span class="sxs-lookup"><span data-stu-id="24e10-215">Select hello Web API ASP.NET Core 1.1 project template.</span></span>
 5. <span data-ttu-id="24e10-216">Una vez creado el proyecto de hello, abra `PackageRoot\ServiceManifest.xml` y quitar hello `Port` atributo de configuración de recurso del extremo de hello:</span><span class="sxs-lookup"><span data-stu-id="24e10-216">Once hello project is created, open `PackageRoot\ServiceManifest.xml` and remove hello `Port` attribute from hello endpoint resource configuration:</span></span>
 
    ```xml
    <Resources>
      <Endpoints>
        <Endpoint Protocol="http" Name="ServiceEndpoint" Type="Input" />
      </Endpoints>
    </Resources>
    ```

    <span data-ttu-id="24e10-217">Esto permite que un puerto de forma dinámica a partir de intervalo de puertos de aplicación hello, que se abría mediante Hola grupo de seguridad de red en la plantilla de administrador de recursos de clúster de hello, lo que permite el tráfico tooflow tooit de la API de administración de Service Fabric toospecify.</span><span class="sxs-lookup"><span data-stu-id="24e10-217">This allows Service Fabric toospecify a port dynamically from hello application port range, which we opened through hello Network Security Group in hello cluster Resource Manager template, allowing traffic tooflow tooit from API Management.</span></span>
 
 6. <span data-ttu-id="24e10-218">Presione F5 en web de Visual Studio tooverify Hola API está disponible localmente.</span><span class="sxs-lookup"><span data-stu-id="24e10-218">Press F5 in Visual Studio tooverify hello web API is available locally.</span></span> 

    <span data-ttu-id="24e10-219">Abra el Explorador de Service Fabric y explorar en profundidad tooa instancia concreta de hello ASP.NET Core toosee Hola dirección base Hola servicio está escuchando en.</span><span class="sxs-lookup"><span data-stu-id="24e10-219">Open Service Fabric Explorer and drill down tooa specific instance of hello ASP.NET Core service toosee hello base address hello service is listening on.</span></span> <span data-ttu-id="24e10-220">Agregar `/api/values` toohello dirección base y ábralo en un explorador.</span><span class="sxs-lookup"><span data-stu-id="24e10-220">Add `/api/values` toohello base address and open it in a browser.</span></span> <span data-ttu-id="24e10-221">Esto invoca el método Get en hello ValuesController en la plantilla de la API Web de Hola Hola.</span><span class="sxs-lookup"><span data-stu-id="24e10-221">This invokes hello Get method on hello ValuesController in hello Web API template.</span></span> <span data-ttu-id="24e10-222">Devuelve respuesta predeterminada de hello proporcionada por la plantilla de hello, una matriz JSON que contiene dos cadenas:</span><span class="sxs-lookup"><span data-stu-id="24e10-222">It returns hello default response that is provided by hello template, a JSON array that contains two strings:</span></span>

    ```json
    ["value1", "value2"]`
    ```

    <span data-ttu-id="24e10-223">Se trata de punto de conexión de Hola que quedará expuesto a través de la API de administración de Azure.</span><span class="sxs-lookup"><span data-stu-id="24e10-223">This is hello endpoint that you'll expose through API Management in Azure.</span></span>

 7. <span data-ttu-id="24e10-224">Por último, implementar clústeres de tooyour de aplicación hello en Azure.</span><span class="sxs-lookup"><span data-stu-id="24e10-224">Finally, deploy hello application tooyour cluster in Azure.</span></span> <span data-ttu-id="24e10-225">[Con Visual Studio](service-fabric-publish-app-remote-cluster.md#to-publish-an-application-using-the-publish-service-fabric-application-dialog-box), haga clic en proyecto de aplicación de Hola y seleccione **publicar**.</span><span class="sxs-lookup"><span data-stu-id="24e10-225">[Using Visual Studio](service-fabric-publish-app-remote-cluster.md#to-publish-an-application-using-the-publish-service-fabric-application-dialog-box), right-click hello Application project and select **Publish**.</span></span> <span data-ttu-id="24e10-226">Proporciona el punto de conexión de clúster (por ejemplo, `mycluster.westus.cloudapp.azure.com:19000`) toodeploy Hola aplicación tooyour tejido de servicio de clúster en Azure.</span><span class="sxs-lookup"><span data-stu-id="24e10-226">Provide your cluster endpoint (for example, `mycluster.westus.cloudapp.azure.com:19000`) toodeploy hello application tooyour Service Fabric cluster in Azure.</span></span>

<span data-ttu-id="24e10-227">En el clúster de Service Fabric en Azure ahora se ejecutará un servicio sin estado ASP.NET Core denominado `fabric:/ApiApplication/WebApiService`.</span><span class="sxs-lookup"><span data-stu-id="24e10-227">An ASP.NET Core stateless service named `fabric:/ApiApplication/WebApiService` should now be running in your Service Fabric cluster in Azure.</span></span>

## <a name="create-an-api-operation"></a><span data-ttu-id="24e10-228">Creación de una operación de API</span><span class="sxs-lookup"><span data-stu-id="24e10-228">Create an API operation</span></span>

<span data-ttu-id="24e10-229">Ahora estamos listo toocreate una operación de administración de API que toocommunicate de uso de los clientes externos con Hola servicio sin estado ASP.NET Core se ejecuta en el clúster de Service Fabric Hola.</span><span class="sxs-lookup"><span data-stu-id="24e10-229">Now we're ready toocreate an operation in API Management that external clients use toocommunicate with hello ASP.NET Core stateless service running in hello Service Fabric cluster.</span></span>

 1. <span data-ttu-id="24e10-230">Inicie sesión en toohello portal de Azure y navegar por la implementación del servicio de administración de API de tooyour.</span><span class="sxs-lookup"><span data-stu-id="24e10-230">Log in toohello Azure portal and navigate tooyour API Management service deployment.</span></span>
 2. <span data-ttu-id="24e10-231">En la hoja de servicio de administración de API de hello, seleccione **API - vista previa**</span><span class="sxs-lookup"><span data-stu-id="24e10-231">In hello API Management service blade, select **APIs - Preview**</span></span>
 3. <span data-ttu-id="24e10-232">Agregar una nueva API haciendo clic en hello **API en blanco** cuadro y rellenar el cuadro de diálogo de hello:</span><span class="sxs-lookup"><span data-stu-id="24e10-232">Add a new API by clicking hello **Blank API** box and filling out hello dialog box:</span></span>

     - <span data-ttu-id="24e10-233">**URL de servicio Web**: para los back-end de Service Fabric, no se utiliza.</span><span class="sxs-lookup"><span data-stu-id="24e10-233">**Web service URL**: For Service Fabric backends, this URL value is not used.</span></span> <span data-ttu-id="24e10-234">Puede escribir aquí cualquier valor.</span><span class="sxs-lookup"><span data-stu-id="24e10-234">You can put any value here.</span></span> <span data-ttu-id="24e10-235">Para este tutorial usaremos `http://servicefabric`.</span><span class="sxs-lookup"><span data-stu-id="24e10-235">For this tutorial, use: `http://servicefabric`.</span></span>
     - <span data-ttu-id="24e10-236">**Nombre**: proporcione cualquier nombre para la API.</span><span class="sxs-lookup"><span data-stu-id="24e10-236">**Name**: Provide any name for your API.</span></span> <span data-ttu-id="24e10-237">Para este tutorial usaremos `Service Fabric App`.</span><span class="sxs-lookup"><span data-stu-id="24e10-237">For this tutorial, use `Service Fabric App`.</span></span>
     - <span data-ttu-id="24e10-238">**Esquema URL**: seleccione HTTP, HTTPS o ambos.</span><span class="sxs-lookup"><span data-stu-id="24e10-238">**URL scheme**: Select either HTTP, HTTPS, or both.</span></span> <span data-ttu-id="24e10-239">Para este tutorial usaremos `both`.</span><span class="sxs-lookup"><span data-stu-id="24e10-239">For this tutorial, use `both`.</span></span>
     - <span data-ttu-id="24e10-240">**API URL Suffix** (Sufijo de URL para API): proporcione un sufijo para la API.</span><span class="sxs-lookup"><span data-stu-id="24e10-240">**API URL Suffix**: Provide a suffix for our API.</span></span> <span data-ttu-id="24e10-241">Para este tutorial usaremos `myapp`.</span><span class="sxs-lookup"><span data-stu-id="24e10-241">For this tutorial, use `myapp`.</span></span>
 
 4. <span data-ttu-id="24e10-242">Una vez que se crea Hola API, haga clic en **+ Agregar operación** operación tooadd una API de front-end.</span><span class="sxs-lookup"><span data-stu-id="24e10-242">Once hello API is created, click **+ Add operation** tooadd a front-end API operation.</span></span> <span data-ttu-id="24e10-243">Rellene los valores de hello:</span><span class="sxs-lookup"><span data-stu-id="24e10-243">Fill out hello values:</span></span>
    
     - <span data-ttu-id="24e10-244">**Dirección URL**: seleccione `GET` y proporcione una ruta de acceso de dirección URL para hello API.</span><span class="sxs-lookup"><span data-stu-id="24e10-244">**URL**: Select `GET` and provide a URL path for hello API.</span></span> <span data-ttu-id="24e10-245">Para este tutorial usaremos `/api/values`.</span><span class="sxs-lookup"><span data-stu-id="24e10-245">For this tutorial, use `/api/values`.</span></span>
     
       <span data-ttu-id="24e10-246">De forma predeterminada, la ruta de acceso de dirección URL de hello especificado aquí se ruta de acceso de dirección URL de hello envía el servicio de Service Fabric toohello back-end.</span><span class="sxs-lookup"><span data-stu-id="24e10-246">By default, hello URL path specified here is hello URL path sent toohello backend Service Fabric service.</span></span> <span data-ttu-id="24e10-247">Si usas Hola misma dirección URL aquí que utiliza el servicio, en este caso `/api/values`, a continuación, la operación de hello funciona sin modificaciones adicionales.</span><span class="sxs-lookup"><span data-stu-id="24e10-247">If you use hello same URL path here that your service uses, in this case `/api/values`, then hello operation works without further modification.</span></span> <span data-ttu-id="24e10-248">También puede especificar una ruta de acceso URL aquí que es diferente de la ruta de acceso de dirección URL de hello utilizado por el servicio de Service Fabric, de back-end en cuyo caso tendrá que también toospecify necesidad de volver a escribir una ruta de acceso en la directiva de la operación más tarde.</span><span class="sxs-lookup"><span data-stu-id="24e10-248">You may also specify a URL path here that is different from hello URL path used by your backend Service Fabric service, in which case you will also need toospecify a path rewrite in your operation policy later.</span></span>
     - <span data-ttu-id="24e10-249">**Nombre para mostrar**: proporcionar un nombre para hello API.</span><span class="sxs-lookup"><span data-stu-id="24e10-249">**Display name**: Provide any name for hello API.</span></span> <span data-ttu-id="24e10-250">Para este tutorial usaremos `Values`.</span><span class="sxs-lookup"><span data-stu-id="24e10-250">For this tutorial, use `Values`.</span></span>

## <a name="configure-a-backend-policy"></a><span data-ttu-id="24e10-251">Configuración de una directiva de back-end</span><span class="sxs-lookup"><span data-stu-id="24e10-251">Configure a backend policy</span></span>

<span data-ttu-id="24e10-252">Directiva de back-end de Hello agrupa todos los componentes.</span><span class="sxs-lookup"><span data-stu-id="24e10-252">hello backend policy ties everything together.</span></span> <span data-ttu-id="24e10-253">Esto es donde se configura Hola back-end se enrutan las solicitudes de servicio toowhich de Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="24e10-253">This is where you configure hello backend Service Fabric service toowhich requests are routed.</span></span> <span data-ttu-id="24e10-254">Puede aplicar esta operación de API de tooany de directiva.</span><span class="sxs-lookup"><span data-stu-id="24e10-254">You can apply this policy tooany API operation.</span></span> <span data-ttu-id="24e10-255">Hola [configuración de back-end de Service Fabric](https://docs.microsoft.com/azure/api-management/api-management-transformation-policies#SetBackendService) proporciona controles de enrutamientos de solicitud de siguiente de hello:</span><span class="sxs-lookup"><span data-stu-id="24e10-255">hello [backend configuration for Service Fabric](https://docs.microsoft.com/azure/api-management/api-management-transformation-policies#SetBackendService) provides hello following request routing controls:</span></span> 
 - <span data-ttu-id="24e10-256">Selección de instancia de servicio mediante la especificación de un nombre de instancia de servicio de Service Fabric, ya sea codificado de forma rígida (por ejemplo, `"fabric:/myapp/myservice"`) o generarse a partir de la solicitud de hello HTTP (por ejemplo, `"fabric:/myapp/users/" + context.Request.MatchedParameters["name"]`).</span><span class="sxs-lookup"><span data-stu-id="24e10-256">Service instance selection by specifying a Service Fabric service instance name, either hardcoded (for example, `"fabric:/myapp/myservice"`) or generated from hello HTTP request (for example, `"fabric:/myapp/users/" + context.Request.MatchedParameters["name"]`).</span></span>
 - <span data-ttu-id="24e10-257">Resolución de la partición mediante la generación de una clave de partición a partir de cualquier esquema de partición de Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="24e10-257">Partition resolution by generating a partition key using any Service Fabric partitioning scheme.</span></span>
 - <span data-ttu-id="24e10-258">Selección de réplicas para los servicios con estado.</span><span class="sxs-lookup"><span data-stu-id="24e10-258">Replica selection for stateful services.</span></span>
 - <span data-ttu-id="24e10-259">Resolución vuelva a intentar las condiciones que permiten las condiciones de hello toospecify para volver a resolver una ubicación de servicio y volver a enviar una solicitud.</span><span class="sxs-lookup"><span data-stu-id="24e10-259">Resolution retry conditions that allow you toospecify hello conditions for re-resolving a service location and resending a request.</span></span>

<span data-ttu-id="24e10-260">Para este tutorial, cree una directiva de back-end que las rutas de las solicitudes directamente toohello servicio sin estado ASP.NET Core implementó anteriormente:</span><span class="sxs-lookup"><span data-stu-id="24e10-260">For this tutorial, create a backend policy that routes requests directly toohello ASP.NET Core stateless service deployed earlier:</span></span>

 1. <span data-ttu-id="24e10-261">Seleccionar y editar hello **entrada directivas** para hello `Values` operación haciendo clic en el icono de edición de hello y, a continuación, seleccione **en la vista código**.</span><span class="sxs-lookup"><span data-stu-id="24e10-261">Select and edit hello **inbound policies** for hello `Values` operation by clicking hello edit icon, and then selecting **Code View**.</span></span>
 2. <span data-ttu-id="24e10-262">En el editor de código de directiva de hello, agregue un `set-backend-service` directiva en las directivas de entrada tal y como se muestra a continuación y haga clic en hello **guardar** botón:</span><span class="sxs-lookup"><span data-stu-id="24e10-262">In hello policy code editor, add a `set-backend-service` policy under inbound policies as shown here and click hello **Save** button:</span></span>
    
    ```xml
    <policies>
      <inbound>
        <base/>
        <set-backend-service 
           backend-id="servicefabric"
           sf-service-instance-name="fabric:/ApiApplication/WebApiService"
           sf-resolve-condition="@((int)context.Response.StatusCode != 200)" />
      </inbound>
      <backend>
        <base/>
      </backend>
      <outbound>
        <base/>
      </outbound>
    </policies>
    ```

<span data-ttu-id="24e10-263">Para obtener un conjunto completo de atributos de directiva de back-end de Service Fabric, consulte toohello [documentación de back-end de administración de API](https://docs.microsoft.com/azure/api-management/api-management-transformation-policies#SetBackendService)</span><span class="sxs-lookup"><span data-stu-id="24e10-263">For a full set of Service Fabric back-end policy attributes, refer toohello [API Management back-end documentation](https://docs.microsoft.com/azure/api-management/api-management-transformation-policies#SetBackendService)</span></span>

### <a name="add-hello-api-tooa-product"></a><span data-ttu-id="24e10-264">Agregar Hola API tooa producto.</span><span class="sxs-lookup"><span data-stu-id="24e10-264">Add hello API tooa product.</span></span> 

<span data-ttu-id="24e10-265">Antes de poder llamar a las API de hello, deben agregarse como producto tooa donde puede conceder acceso toousers.</span><span class="sxs-lookup"><span data-stu-id="24e10-265">Before you can call hello API, it must be added tooa product where you can grant access toousers.</span></span> 

 1. <span data-ttu-id="24e10-266">En el servicio de administración de API de hello, seleccione **productos - vista previa**.</span><span class="sxs-lookup"><span data-stu-id="24e10-266">In hello API Management service, select **Products - PREVIEW**.</span></span>
 2. <span data-ttu-id="24e10-267">De forma predeterminada, API Management ofrece dos productos: Starter y Unlimited.</span><span class="sxs-lookup"><span data-stu-id="24e10-267">By default, API Management providers two products: Starter and Unlimited.</span></span> <span data-ttu-id="24e10-268">Seleccione el producto de un número ilimitado de Hola.</span><span class="sxs-lookup"><span data-stu-id="24e10-268">Select hello Unlimited product.</span></span>
 3. <span data-ttu-id="24e10-269">Seleccione las API.</span><span class="sxs-lookup"><span data-stu-id="24e10-269">Select APIs.</span></span>
 4. <span data-ttu-id="24e10-270">Haga clic en hello **+ agregar** botón.</span><span class="sxs-lookup"><span data-stu-id="24e10-270">Click hello **+ Add** button.</span></span>
 5. <span data-ttu-id="24e10-271">Seleccione hello `Service Fabric App` API que creó en los pasos anteriores de Hola y haga clic en hello **seleccione** botón.</span><span class="sxs-lookup"><span data-stu-id="24e10-271">Select hello `Service Fabric App` API you created in hello previous steps and click hello **Select** button.</span></span>

### <a name="test-it"></a><span data-ttu-id="24e10-272">Pruébelo.</span><span class="sxs-lookup"><span data-stu-id="24e10-272">Test it</span></span>

<span data-ttu-id="24e10-273">Ahora puede intentar enviar un servicio de back-end de solicitud tooyour en Service Fabric a través de la API de administración directamente desde el portal de Azure Hola.</span><span class="sxs-lookup"><span data-stu-id="24e10-273">You can now try sending a request tooyour back-end service in Service Fabric through API Management directly from hello Azure portal.</span></span>

 1. <span data-ttu-id="24e10-274">En el servicio de administración de API de hello, seleccione **API - vista previa**.</span><span class="sxs-lookup"><span data-stu-id="24e10-274">In hello API Management service, select **API - PREVIEW**.</span></span>
 2. <span data-ttu-id="24e10-275">Hola `Service Fabric App` API que creó en los pasos anteriores de hello, seleccione hello **prueba** ficha.</span><span class="sxs-lookup"><span data-stu-id="24e10-275">In hello `Service Fabric App` API you created in hello previous steps, select hello **Test** tab.</span></span>
 3. <span data-ttu-id="24e10-276">Haga clic en hello **enviar** botón toosend un servicio de back-end de toohello de solicitud de prueba.</span><span class="sxs-lookup"><span data-stu-id="24e10-276">Click hello **Send** button toosend a test request toohello backend service.</span></span>

## <a name="next-steps"></a><span data-ttu-id="24e10-277">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="24e10-277">Next steps</span></span>

<span data-ttu-id="24e10-278">Llegados a este punto, debe tener una configuración básica de Service Fabric y API Management.</span><span class="sxs-lookup"><span data-stu-id="24e10-278">At this point, you should have a basic setup with Service Fabric and API Management.</span></span>

<span data-ttu-id="24e10-279">Este tutorial utiliza la autenticación de usuario básica basada en certificados para su tooget de clúster de Service Fabric que preparar rápidamente.</span><span class="sxs-lookup"><span data-stu-id="24e10-279">This tutorial uses basic certificate-based user authentication for your Service Fabric cluster tooget you set up quickly.</span></span> <span data-ttu-id="24e10-280">aunque para el clúster de Service Fabric es preferible una autenticación de usuarios más avanzada con [autenticación de Azure Active Directory](service-fabric-cluster-creation-via-arm.md#set-up-azure-active-directory-for-client-authentication).</span><span class="sxs-lookup"><span data-stu-id="24e10-280">More advanced user authentication for your Service Fabric cluster is preferable with [Azure Active Directory authentication](service-fabric-cluster-creation-via-arm.md#set-up-azure-active-directory-for-client-authentication).</span></span> 

<span data-ttu-id="24e10-281">Después, [crear y configurar opciones de producto avanzadas en la administración de API de Azure](https://docs.microsoft.com/azure/api-management/api-management-howto-product-with-rules) tooprepare la aplicación para el tráfico del mundo real.</span><span class="sxs-lookup"><span data-stu-id="24e10-281">Next, [create and configure advanced product settings in Azure API Management](https://docs.microsoft.com/azure/api-management/api-management-howto-product-with-rules) tooprepare your application for real world traffic.</span></span>

<!-- links -->
[azure-powershell]:https://azure.microsoft.com/documentation/articles/powershell-install-configure/

[network-arm]:https://github.com/Azure-Samples/service-fabric-api-management/blob/master/network.json
[network-parameters-arm]:https://github.com/Azure-Samples/service-fabric-api-management/blob/master/network.parameters.json

[apim-arm]:https://github.com/Azure-Samples/service-fabric-api-management/blob/master/apim.json
[apim-parameters-arm]:https://github.com/Azure-Samples/service-fabric-api-management/blob/master/apim.parameters.json

[cluster-arm]:https://github.com/Azure-Samples/service-fabric-api-management/blob/master/cluster.json
[cluster-parameters-arm]:https://github.com/Azure-Samples/service-fabric-api-management/blob/master/cluster.parameters.json


<!-- pics -->
[sf-apim-topology-overview]: ./media/service-fabric-api-management-quickstart/sf-apim-topology-overview.png
