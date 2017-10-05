---
title: "Inicio rápido de Azure Service Fabric con API Management | Microsoft Docs"
description: "En esta guía se muestra cómo empezar a usar rápidamente Azure API Management y Service Fabric."
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
ms.openlocfilehash: e9f44d8a43d274768f43261fea68f0da9c681ae1
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/03/2017
---
# <a name="service-fabric-with-azure-api-management-quick-start"></a><span data-ttu-id="a9fab-103">Inicio rápido de Service Fabric con Azure API Management</span><span class="sxs-lookup"><span data-stu-id="a9fab-103">Service Fabric with Azure API Management Quick Start</span></span>

<span data-ttu-id="a9fab-104">Esta guía muestra cómo configurar Azure API Management con Service Fabric y la primera operación de API para enviar tráfico a los servicios de back-end de Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="a9fab-104">This guide shows you how to set up Azure API Management with Service Fabric and configure your first API operation to send traffic to back-end services in Service Fabric.</span></span> <span data-ttu-id="a9fab-105">Para más información sobre escenarios de Azure API Management con Service Fabric, consulte el artículo de [introducción](service-fabric-api-management-overview.md).</span><span class="sxs-lookup"><span data-stu-id="a9fab-105">To learn more about Azure API Management scenarios with Service Fabric, see the [overview](service-fabric-api-management-overview.md) article.</span></span> 

## <a name="deploy-api-management-and-service-fabric-to-azure"></a><span data-ttu-id="a9fab-106">Implementación de API Management y Service Fabric en Azure</span><span class="sxs-lookup"><span data-stu-id="a9fab-106">Deploy API Management and Service Fabric to Azure</span></span>

<span data-ttu-id="a9fab-107">El primer paso es implementar API Management y un clúster de Service Fabric en Azure, en una red virtual compartida.</span><span class="sxs-lookup"><span data-stu-id="a9fab-107">The first step is to deploy API Management and a Service Fabric cluster to Azure in a shared Virtual Network.</span></span> <span data-ttu-id="a9fab-108">Esto permite a API Management comunicarse directamente con Service Fabric para que realice la detección de servicios, la resolución de la partición de servicio y que reenvíe el tráfico directamente a cualquier servicio de back-end de Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="a9fab-108">This allows API Management to communicate directly with Service Fabric so it can perform service discovery, service partition resolution, and forward traffic directly to any backend service in Service Fabric.</span></span>

### <a name="topology"></a><span data-ttu-id="a9fab-109">Topología</span><span class="sxs-lookup"><span data-stu-id="a9fab-109">Topology</span></span>

<span data-ttu-id="a9fab-110">Esta guía distribuye en Azure la topología siguiente, donde API Management y Service Fabric se encuentran en subredes de la misma red virtual:</span><span class="sxs-lookup"><span data-stu-id="a9fab-110">This guide deploys the following topology to Azure in which API Management and Service Fabric are in subnets of the same Virtual Network:</span></span>

 ![Leyenda de la imagen][sf-apim-topology-overview]

<span data-ttu-id="a9fab-112">Para empezar a trabajar rápidamente, se proporcionan plantillas de Resource Manager para cada paso de la implementación:</span><span class="sxs-lookup"><span data-stu-id="a9fab-112">To get started quickly, Resource Manager templates are provided for each deployment step:</span></span>

 - <span data-ttu-id="a9fab-113">Topología de red:</span><span class="sxs-lookup"><span data-stu-id="a9fab-113">Network topology:</span></span>
    - <span data-ttu-id="a9fab-114">[network.json][network-arm]</span><span class="sxs-lookup"><span data-stu-id="a9fab-114">[network.json][network-arm]</span></span>
    - <span data-ttu-id="a9fab-115">[network.parameters.json][network-parameters-arm]</span><span class="sxs-lookup"><span data-stu-id="a9fab-115">[network.parameters.json][network-parameters-arm]</span></span>
 - <span data-ttu-id="a9fab-116">Clúster de Service Fabric:</span><span class="sxs-lookup"><span data-stu-id="a9fab-116">Service Fabric cluster:</span></span>
    - <span data-ttu-id="a9fab-117">[cluster.json][cluster-arm]</span><span class="sxs-lookup"><span data-stu-id="a9fab-117">[cluster.json][cluster-arm]</span></span>
    - <span data-ttu-id="a9fab-118">[cluster.parameters.json][cluster-parameters-arm]</span><span class="sxs-lookup"><span data-stu-id="a9fab-118">[cluster.parameters.json][cluster-parameters-arm]</span></span>
 - <span data-ttu-id="a9fab-119">API Management:</span><span class="sxs-lookup"><span data-stu-id="a9fab-119">API Management:</span></span>
    - <span data-ttu-id="a9fab-120">[apim.json][apim-arm]</span><span class="sxs-lookup"><span data-stu-id="a9fab-120">[apim.json][apim-arm]</span></span>
    - <span data-ttu-id="a9fab-121">[apim.parameters.json][apim-parameters-arm]</span><span class="sxs-lookup"><span data-stu-id="a9fab-121">[apim.parameters.json][apim-parameters-arm]</span></span>

### <a name="sign-in-to-azure-and-select-your-subscription"></a><span data-ttu-id="a9fab-122">Inicio de sesión en Azure y selección de la suscripción</span><span class="sxs-lookup"><span data-stu-id="a9fab-122">Sign in to Azure and select your subscription</span></span>

<span data-ttu-id="a9fab-123">En esta guía se usa [Azure PowerShell][azure-powershell].</span><span class="sxs-lookup"><span data-stu-id="a9fab-123">This guide uses [Azure PowerShell][azure-powershell].</span></span> <span data-ttu-id="a9fab-124">Al iniciar una nueva sesión de PowerShell, inicie sesión en su cuenta de Azure y seleccione su suscripción antes de ejecutar comandos de Azure.</span><span class="sxs-lookup"><span data-stu-id="a9fab-124">When you start a new PowerShell session, sign in to your Azure account and select your subscription before you execute Azure commands.</span></span>
 
<span data-ttu-id="a9fab-125">Inicio de sesión en la cuenta de Azure</span><span class="sxs-lookup"><span data-stu-id="a9fab-125">Sign in to your Azure account:</span></span>

```powershell
PS > Login-AzureRmAccount
```

<span data-ttu-id="a9fab-126">Seleccione su suscripción:</span><span class="sxs-lookup"><span data-stu-id="a9fab-126">Select your subscription:</span></span>

```powershell
PS > Get-AzureRmSubscription
PS > Set-AzureRmContext -SubscriptionId <guid>
```

### <a name="create-a-resource-group"></a><span data-ttu-id="a9fab-127">Crear un grupo de recursos</span><span class="sxs-lookup"><span data-stu-id="a9fab-127">Create a resource group</span></span>

<span data-ttu-id="a9fab-128">Cree un grupo de recursos para la implementación.</span><span class="sxs-lookup"><span data-stu-id="a9fab-128">Create a new resource group for your deployment.</span></span> <span data-ttu-id="a9fab-129">Asígnele un nombre y una ubicación.</span><span class="sxs-lookup"><span data-stu-id="a9fab-129">Give it a name and a location.</span></span>

```powershell
PS > New-AzureRmResourceGroup -Name <my-resource-group> -Location westus
```

### <a name="deploy-the-network-topology"></a><span data-ttu-id="a9fab-130">Implementación de la topología de red</span><span class="sxs-lookup"><span data-stu-id="a9fab-130">Deploy the network topology</span></span>

<span data-ttu-id="a9fab-131">El primer paso es configurar la topología de la red de implementación de API Management y el clúster de Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="a9fab-131">The first step is to set up the network topology to which API Management and the Service Fabric cluster will be deployed.</span></span> <span data-ttu-id="a9fab-132">La plantilla de Resource Manager [network.json][network-arm] está configurada para crear una red Virtual (VNET) con dos subredes y dos grupos de seguridad de red (NSG).</span><span class="sxs-lookup"><span data-stu-id="a9fab-132">The [network.json][network-arm] Resource Manager template is configured to create a Virtual Network (VNET) with two subnets and two Network Security Groups (NSG).</span></span> 

<span data-ttu-id="a9fab-133">El archivo de parámetros [network.parameters.json][network-parameters-arm] contiene los nombres de las subredes y los grupos de seguridad de red donde se implementarán API Management y Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="a9fab-133">The [network.parameters.json][network-parameters-arm] parameters file contains the names of the subnets and NSGs that API Management and Service Fabric will be deployed to.</span></span> <span data-ttu-id="a9fab-134">En esta guía, los valores de los parámetros no deben cambiarse.</span><span class="sxs-lookup"><span data-stu-id="a9fab-134">For this guide, the parameter values do not need to be changed.</span></span> <span data-ttu-id="a9fab-135">Las plantillas de Resource Manager para API Management y Service Fabric usan estos valores, por lo que, si los modifica aquí, debe modificarlos también en las demás plantillas de Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="a9fab-135">The API Management and Service Fabric Resource Manager templates use these values, so if they are modified here, you must modify them in the other Resource Manager templates accordingly.</span></span> 

 1. <span data-ttu-id="a9fab-136">Descargue la plantilla de Resource Manager y el archivo de parámetros siguientes:</span><span class="sxs-lookup"><span data-stu-id="a9fab-136">Download the following Resource Manager template and parameters file:</span></span>

    - <span data-ttu-id="a9fab-137">[network.json][network-arm]</span><span class="sxs-lookup"><span data-stu-id="a9fab-137">[network.json][network-arm]</span></span>
    - <span data-ttu-id="a9fab-138">[network.parameters.json][network-parameters-arm]</span><span class="sxs-lookup"><span data-stu-id="a9fab-138">[network.parameters.json][network-parameters-arm]</span></span>

 2. <span data-ttu-id="a9fab-139">Use el siguiente comando de PowerShell para implementar la plantilla de Resource Manager y los archivos de parámetros para la configuración de la red:</span><span class="sxs-lookup"><span data-stu-id="a9fab-139">Use the following PowerShell command to deploy the Resource Manager template and parameter files for the network setup:</span></span>

    ```powershell
    PS > New-AzureRmResourceGroupDeployment -ResourceGroupName <my-resource-group> -TemplateFile .\network.json -TemplateParameterFile .\network.parameters.json -Verbose
    ```

### <a name="deploy-the-service-fabric-cluster"></a><span data-ttu-id="a9fab-140">Implementación del clúster de Service Fabric</span><span class="sxs-lookup"><span data-stu-id="a9fab-140">Deploy the Service Fabric cluster</span></span>

<span data-ttu-id="a9fab-141">Una vez implementados los recursos de red, el siguiente paso es implementar un clúster de Service Fabric a la red virtual, en la subred y el grupo de seguridad de red designados para el clúster de Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="a9fab-141">Once the network resources have finished deploying, the next step is to deploy a Service Fabric cluster to the VNET in the subnet and NSG designated for the Service Fabric cluster.</span></span> <span data-ttu-id="a9fab-142">Para este tutorial, la plantilla de Resource Manager para Service Fabric está preconfigurada para los nombres de la red virtual, la subred y el grupo de seguridad de red que configuró en el paso anterior.</span><span class="sxs-lookup"><span data-stu-id="a9fab-142">For this tutorial, the Service Fabric Resource Manager template is pre-configured to use the names of the VNET, subnet, and NSG that you set up in the previous step.</span></span> 

<span data-ttu-id="a9fab-143">La plantilla de Resource Manager para el clúster de Service Fabric está configurada para crear un clúster con certificado seguro.</span><span class="sxs-lookup"><span data-stu-id="a9fab-143">The Service Fabric cluster Resource Manager template is configured to create a secure cluster with certificate security.</span></span> <span data-ttu-id="a9fab-144">El certificado se utiliza para proteger la comunicación de nodo a nodo del clúster y para administrar el acceso de los usuarios al clúster de Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="a9fab-144">The certificate is used to secure node-to-node communication for your cluster and to manage user access to your Service Fabric cluster.</span></span> <span data-ttu-id="a9fab-145">API Management usa este certificado para acceder al servicio de nomenclatura de Service Fabric para detectar servicios.</span><span class="sxs-lookup"><span data-stu-id="a9fab-145">API Management uses this certificate to access  the Service Fabric Naming Service for service discovery.</span></span>

<span data-ttu-id="a9fab-146">Este paso requiere un certificado en Key Vault para la seguridad del clúster.</span><span class="sxs-lookup"><span data-stu-id="a9fab-146">This step requires having a certificate in Key Vault for cluster security.</span></span> <span data-ttu-id="a9fab-147">Para más información sobre cómo configurar un clúster seguro en Key Vault, consulte [esta guía sobre la creación de un clúster de Azure con Resource Manager](service-fabric-cluster-creation-via-arm.md).</span><span class="sxs-lookup"><span data-stu-id="a9fab-147">For more information on setting up a secure cluster with Key Vault, see [this guide on creating a cluster in Azure using Resource Manager](service-fabric-cluster-creation-via-arm.md)</span></span>

> [!NOTE]
> <span data-ttu-id="a9fab-148">Puede agregar la autenticación de Azure Active Directory además del certificado de acceso al clúster.</span><span class="sxs-lookup"><span data-stu-id="a9fab-148">You may add Azure Active Directory authentication in addition to the certificate used for cluster access.</span></span> <span data-ttu-id="a9fab-149">Azure Active Directory es la manera recomendada para administrar el acceso de usuario al clúster de Service Fabric, pero esto no es necesario para completar el tutorial.</span><span class="sxs-lookup"><span data-stu-id="a9fab-149">Azure Active Directory is the recommended way to manage user access to your Service Fabric cluster, but is not necessary to complete this tutorial.</span></span> <span data-ttu-id="a9fab-150">En cualquier caso, se necesita un certificado para la seguridad de nodo a nodo del clúster y para la autenticación de Azure API Management, que actualmente no admite la autenticación con Azure Active Directory para el back-end de Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="a9fab-150">A certificate is required either way for cluster node-to-node security and for Azure API Management authentication, which currently does not support authenticating with Azure Active Directory for a Service Fabric backend.</span></span>

 1. <span data-ttu-id="a9fab-151">Descargue la plantilla de Resource Manager y el archivo de parámetros siguientes:</span><span class="sxs-lookup"><span data-stu-id="a9fab-151">Download the following Resource Manager template and parameters file:</span></span>
 
    - <span data-ttu-id="a9fab-152">[cluster.json][cluster-arm]</span><span class="sxs-lookup"><span data-stu-id="a9fab-152">[cluster.json][cluster-arm]</span></span>
    - <span data-ttu-id="a9fab-153">[cluster.parameters.json][cluster-parameters-arm]</span><span class="sxs-lookup"><span data-stu-id="a9fab-153">[cluster.parameters.json][cluster-parameters-arm]</span></span>

 2. <span data-ttu-id="a9fab-154">Rellene los parámetros vacíos del archivo `cluster.parameters.json` para la implementación, incluida la [información del almacén de claves](service-fabric-cluster-creation-via-arm.md#set-up-a-key-vault) para el certificado del clúster.</span><span class="sxs-lookup"><span data-stu-id="a9fab-154">Fill in the empty parameters in the `cluster.parameters.json` file for your deployment, including the [Key Vault information](service-fabric-cluster-creation-via-arm.md#set-up-a-key-vault) for your cluster certificate.</span></span>

 3. <span data-ttu-id="a9fab-155">Use el siguiente comando de PowerShell para implementar la plantilla de Resource Manager y los archivos de parámetros para crear el clúster de Service Fabric:</span><span class="sxs-lookup"><span data-stu-id="a9fab-155">Use the following PowerShell command to deploy the Resource Manager template and parameter files to create the Service Fabric cluster:</span></span>

    ```powershell
    PS > New-AzureRmResourceGroupDeployment -ResourceGroupName <my-resource-group> -TemplateFile .\cluster.json -TemplateParameterFile .\cluster.parameters.json -Verbose
    ```

### <a name="deploy-api-management"></a><span data-ttu-id="a9fab-156">Implementación de API Management</span><span class="sxs-lookup"><span data-stu-id="a9fab-156">Deploy API Management</span></span>

<span data-ttu-id="a9fab-157">Por último, implemente API Management en la red virtual, en la subred y el grupo de seguridad de red designados para API Management.</span><span class="sxs-lookup"><span data-stu-id="a9fab-157">Finally, deploy API Management to the VNET in the subnet and NSG designated for API Management.</span></span> <span data-ttu-id="a9fab-158">No es necesario esperar a que finalice la implementación del clúster de Service Fabric para implementar API Management.</span><span class="sxs-lookup"><span data-stu-id="a9fab-158">You do not need to wait for the Service Fabric cluster deployment to finish before deploying API Management.</span></span> 

<span data-ttu-id="a9fab-159">Para este tutorial, la plantilla de Resource Manager para API Management está preconfigurada para los nombres de la red virtual, la subred y el grupo de seguridad de red que configuró en el paso anterior.</span><span class="sxs-lookup"><span data-stu-id="a9fab-159">For this tutorial, the API Management Resource Manager template is pre-configured to use the names of the VNET, subnet, and NSG that you set up in the previous step.</span></span> 

 1. <span data-ttu-id="a9fab-160">Descargue la plantilla de Resource Manager y el archivo de parámetros siguientes:</span><span class="sxs-lookup"><span data-stu-id="a9fab-160">Download the following Resource Manager template and parameters file:</span></span>
 
    - <span data-ttu-id="a9fab-161">[apim.json][apim-arm]</span><span class="sxs-lookup"><span data-stu-id="a9fab-161">[apim.json][apim-arm]</span></span>
    - <span data-ttu-id="a9fab-162">[apim.parameters.json][apim-parameters-arm]</span><span class="sxs-lookup"><span data-stu-id="a9fab-162">[apim.parameters.json][apim-parameters-arm]</span></span>

 2. <span data-ttu-id="a9fab-163">Rellene los parámetros vacíos en el archivo `apim.parameters.json` para la implementación.</span><span class="sxs-lookup"><span data-stu-id="a9fab-163">Fill in the empty parameters in the `apim.parameters.json` for your deployment.</span></span>

 3. <span data-ttu-id="a9fab-164">Use el siguiente comando de PowerShell para implementar la plantilla de Resource Manager y los archivos de parámetros para API Management:</span><span class="sxs-lookup"><span data-stu-id="a9fab-164">Use the following PowerShell command to deploy the Resource Manager template and parameter files for API Management:</span></span>

    ```powershell
    PS > New-AzureRmResourceGroupDeployment -ResourceGroupName <my-resource-group> -TemplateFile .\apim.json -TemplateParameterFile .\apim.parameters.json -Verbose
    ```

## <a name="configure-api-management"></a><span data-ttu-id="a9fab-165">Configuración de API Management</span><span class="sxs-lookup"><span data-stu-id="a9fab-165">Configure API Management</span></span>

<span data-ttu-id="a9fab-166">Una vez implementados API Management y el clúster de Service Fabric, puede configurar un back-end de Service Fabric en API Management.</span><span class="sxs-lookup"><span data-stu-id="a9fab-166">Once your API Management and Service Fabric cluster are deployed, you can configure a Service Fabric backend in API Management.</span></span> <span data-ttu-id="a9fab-167">De este modo, podrá crear una directiva de servicio de back-end que envíe tráfico al clúster de Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="a9fab-167">This allows you to create a backend service policy that sends traffic to your Service Fabric cluster.</span></span>

### <a name="api-management-security"></a><span data-ttu-id="a9fab-168">Seguridad de API Management</span><span class="sxs-lookup"><span data-stu-id="a9fab-168">API Management Security</span></span>

<span data-ttu-id="a9fab-169">Para configurar el back-end de Service Fabric, primero debe realizar la configuración de seguridad de API Management.</span><span class="sxs-lookup"><span data-stu-id="a9fab-169">To configure the Service Fabric backend, you first need to configure API Management security settings.</span></span> <span data-ttu-id="a9fab-170">Para configurar las opciones de seguridad, vaya a su servicio de API Management en Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="a9fab-170">To configure security settings, go to your API Management service in the Azure portal.</span></span>

#### <a name="enable-the-api-management-rest-api"></a><span data-ttu-id="a9fab-171">Habilitación de la API de REST de API Management</span><span class="sxs-lookup"><span data-stu-id="a9fab-171">Enable the API Management REST API</span></span>

<span data-ttu-id="a9fab-172">La API de REST de API Management actualmente es la única manera de configurar un servicio back-end.</span><span class="sxs-lookup"><span data-stu-id="a9fab-172">The API Management REST API is currently the only way to configure a backend service.</span></span> <span data-ttu-id="a9fab-173">El primer paso es habilitar la API de REST de API Management y protegerla.</span><span class="sxs-lookup"><span data-stu-id="a9fab-173">The first step is to enable the API Management REST API and secure it.</span></span>

 1. <span data-ttu-id="a9fab-174">En **Seguridad** del servicio API Management, seleccione **API Management (versión preliminar)**.</span><span class="sxs-lookup"><span data-stu-id="a9fab-174">In the API Management service, select **Management API - PREVIEW** under **Security**.</span></span>
 2. <span data-ttu-id="a9fab-175">Marque la casilla **Habilitar API de REST de API Management**.</span><span class="sxs-lookup"><span data-stu-id="a9fab-175">Check the **Enable API Management REST API** checkbox.</span></span>
 3. <span data-ttu-id="a9fab-176">Anote la URL de API Management, se usará más adelante para configurar el back-end de Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="a9fab-176">Note the Management API URL - this is the URL we'll use later to set up the Service Fabric backend</span></span>
 4. <span data-ttu-id="a9fab-177">Genere un **token de acceso**; para ello, seleccione una fecha de expiración y una clave, y haga clic en el botón **Generar** situado hacia la parte inferior de la página.</span><span class="sxs-lookup"><span data-stu-id="a9fab-177">Generate an **access Token** by selecting an expiry date and a key, then click the **Generate** button toward the bottom of the page.</span></span>
 5. <span data-ttu-id="a9fab-178">Copie el **token de acceso** y guárdelo, lo usaremos en los pasos siguientes.</span><span class="sxs-lookup"><span data-stu-id="a9fab-178">Copy the **access token** and save it - we'll use this in the following steps.</span></span> <span data-ttu-id="a9fab-179">Tenga en cuenta que es distinto de las claves principal y secundaria.</span><span class="sxs-lookup"><span data-stu-id="a9fab-179">Note this is different from the primary key and secondary key.</span></span>

#### <a name="upload-a-service-fabric-client-certificate"></a><span data-ttu-id="a9fab-180">Carga de un certificado de cliente de Service Fabric</span><span class="sxs-lookup"><span data-stu-id="a9fab-180">Upload a Service Fabric client certificate</span></span>

<span data-ttu-id="a9fab-181">API Management debe autenticarse con el clúster de Service Fabric para la detección de servicios mediante un certificado de cliente con acceso al clúster.</span><span class="sxs-lookup"><span data-stu-id="a9fab-181">API Management must authenticate with your Service Fabric cluster for service discovery using a client certificate that has access to your cluster.</span></span> <span data-ttu-id="a9fab-182">Para facilitar las cosas, en este tutorial se usa el mismo certificado que se especificó al crear el clúster de Service Fabric, que, de forma predeterminada, se puede usar para acceder al clúster.</span><span class="sxs-lookup"><span data-stu-id="a9fab-182">For simplicity, this tutorial uses the same certificate specified when creating the Service Fabric cluster, which by default can be used to access your cluster.</span></span>

 1. <span data-ttu-id="a9fab-183">En **Seguridad** del servicio API Management, seleccione **Certificados de cliente (versión preliminar)**.</span><span class="sxs-lookup"><span data-stu-id="a9fab-183">In the API Management service, select **Client certificates - PREVIEW** under **Security**.</span></span>
 2. <span data-ttu-id="a9fab-184">Haga clic en el botón **+ Agregar**.</span><span class="sxs-lookup"><span data-stu-id="a9fab-184">Click the **+ Add** button</span></span>
 2. <span data-ttu-id="a9fab-185">Seleccione el archivo de clave privada (.pfx) del certificado de clúster que especificó al crear el clúster de Service Fabric, asígnele un nombre y escriba la contraseña de clave privada.</span><span class="sxs-lookup"><span data-stu-id="a9fab-185">Select the private key file (.pfx) of the cluster certificate that you specified when creating your Service Fabric cluster, give it a name, and provide the private key password.</span></span>

> [!NOTE]
> <span data-ttu-id="a9fab-186">En este tutorial se usa el mismo certificado para la autenticación de cliente y la seguridad de nodo a nodo del clúster.</span><span class="sxs-lookup"><span data-stu-id="a9fab-186">This tutorial uses the same certificate for client authentication and cluster node-to-node security.</span></span> <span data-ttu-id="a9fab-187">Puede utilizar otro certificado de cliente si tiene uno configurado para acceder al clúster de Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="a9fab-187">You may use a separate client certificate if you have one configured to access your Service Fabric cluster.</span></span>

### <a name="configure-the-backend"></a><span data-ttu-id="a9fab-188">Configuración del back-end</span><span class="sxs-lookup"><span data-stu-id="a9fab-188">Configure the backend</span></span>

<span data-ttu-id="a9fab-189">Ahora que se ha configurado la seguridad de API Management, puede configurar el back-end de Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="a9fab-189">Now that API Management security is configured, you can configure the Service Fabric backend.</span></span> <span data-ttu-id="a9fab-190">Para Service Fabric, su clúster sirve de back-end, en lugar de usar un servicio de Service Fabric específico.</span><span class="sxs-lookup"><span data-stu-id="a9fab-190">For Service Fabric backends, the Service Fabric cluster is the backend, rather than a specific Service Fabric service.</span></span> <span data-ttu-id="a9fab-191">Esto permite que una única directiva enrute a más de un servicio del clúster.</span><span class="sxs-lookup"><span data-stu-id="a9fab-191">This allows a single policy to route to more than one service in the cluster.</span></span>

<span data-ttu-id="a9fab-192">Este paso requiere el token de acceso que se generó anteriormente y la huella digital para el certificado de clúster que se cargó en API Management en el paso anterior.</span><span class="sxs-lookup"><span data-stu-id="a9fab-192">This step requires the access token you generated earlier and the thumbprint for your cluster certificate you uploaded to API Management in the previous step.</span></span>

> [!NOTE]
> <span data-ttu-id="a9fab-193">Si usó un certificado de cliente independiente en el paso anterior para API Management, para este paso necesita la huella digital del certificado de cliente además de la huella digital de certificado de clúster.</span><span class="sxs-lookup"><span data-stu-id="a9fab-193">If you used a separate client certificate in the previous step for API Management, you need the thumbprint for the client certificate in addition to the cluster certificate thumbprint in this step.</span></span>

<span data-ttu-id="a9fab-194">Envíe la solicitud de PUT de HTTP siguiente a la URL de la API de API Management que anotó anteriormente al habilitar la API de REST de API Management para configurar el servicio de back-end de Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="a9fab-194">Send the following HTTP PUT request to the API Management API URL you noted earlier when enabling the API Management REST API to configure the Service Fabric backend service.</span></span> <span data-ttu-id="a9fab-195">Verá una respuesta `HTTP 201 Created` al ejecutarse el comando correctamente.</span><span class="sxs-lookup"><span data-stu-id="a9fab-195">You should see an `HTTP 201 Created` response when the command succeeds.</span></span> <span data-ttu-id="a9fab-196">Para más información sobre cada campo, consulte la [documentación de referencia de la API de back-end](https://docs.microsoft.com/rest/api/apimanagement/apimanagementrest/azure-api-management-rest-api-contract-reference#a-namebackenda-backend) de API Management.</span><span class="sxs-lookup"><span data-stu-id="a9fab-196">For more information on each field, see the API Management [backend API reference documentation](https://docs.microsoft.com/rest/api/apimanagement/apimanagementrest/azure-api-management-rest-api-contract-reference#a-namebackenda-backend).</span></span>

<span data-ttu-id="a9fab-197">Comando HTTP y dirección URL:</span><span class="sxs-lookup"><span data-stu-id="a9fab-197">HTTP command and URL:</span></span>
```http
PUT https://your-apim.management.azure-api.net/backends/servicefabric?api-version=2016-10-10
```

<span data-ttu-id="a9fab-198">Encabezados de solicitud:</span><span class="sxs-lookup"><span data-stu-id="a9fab-198">Request headers:</span></span>
```http
Authorization: SharedAccessSignature <your access token>
Content-Type: application/json
```

<span data-ttu-id="a9fab-199">Cuerpo de la solicitud:</span><span class="sxs-lookup"><span data-stu-id="a9fab-199">Request body:</span></span>
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

<span data-ttu-id="a9fab-200">Este parámetro **url** es el nombre de acceso completo del servicio en el clúster al que se enrutan todas las solicitudes de forma predeterminada si no se especifica ningún nombre de servicio en una directiva de back-end.</span><span class="sxs-lookup"><span data-stu-id="a9fab-200">The **url** parameter here is a fully-qualified service name of a service in your cluster that all requests are routed to by default if no service name is specified in a backend policy.</span></span> <span data-ttu-id="a9fab-201">Puede usar un nombre de servicio falso, como "fabric:/fake/service" si no desea un servicio de reserva.</span><span class="sxs-lookup"><span data-stu-id="a9fab-201">You may use a fake service name, such as "fabric:/fake/service" if you do not intend to have a fallback service.</span></span>

<span data-ttu-id="a9fab-202">Para más información sobre cada campo, consulte la [documentación de referencia de la API de back-end](https://docs.microsoft.com/rest/api/apimanagement/apimanagementrest/azure-api-management-rest-api-contract-reference#a-namebackenda-backend) de API Management.</span><span class="sxs-lookup"><span data-stu-id="a9fab-202">Refer to the API Management [backend API reference documentation](https://docs.microsoft.com/rest/api/apimanagement/apimanagementrest/azure-api-management-rest-api-contract-reference#a-namebackenda-backend) for more details on each field.</span></span>

#### <a name="example"></a><span data-ttu-id="a9fab-203">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="a9fab-203">Example</span></span>

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

## <a name="deploy-a-service-fabric-back-end-service"></a><span data-ttu-id="a9fab-204">Implementación de un servicio de back-end de Service Fabric</span><span class="sxs-lookup"><span data-stu-id="a9fab-204">Deploy a Service Fabric back-end service</span></span>

<span data-ttu-id="a9fab-205">Ahora que tiene Service Fabric configurado como back-end para API Management, puede crear directivas de back-end para las API que envían tráfico a los servicios de Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="a9fab-205">Now that you have the Service Fabric configured as a backend to API Management, you can author backend policies for your APIs that send traffic to your Service Fabric services.</span></span> <span data-ttu-id="a9fab-206">Pero primero necesita que un servicio que se ejecute en Service Fabric acepte las solicitudes.</span><span class="sxs-lookup"><span data-stu-id="a9fab-206">But first you need a service running in Service Fabric to accept requests.</span></span>

### <a name="create-a-service-fabric-service-with-an-http-endpoint"></a><span data-ttu-id="a9fab-207">Creación de un servicio de Service Fabric con un punto de conexión HTTP</span><span class="sxs-lookup"><span data-stu-id="a9fab-207">Create a Service Fabric service with an HTTP endpoint</span></span>

<span data-ttu-id="a9fab-208">Para este tutorial, vamos a crear un servicio básico confiable de ASP.NET Core sin estado con la plantilla de proyecto de API web predeterminada.</span><span class="sxs-lookup"><span data-stu-id="a9fab-208">For this tutorial, we'll create a basic stateless ASP.NET Core Reliable Service using the default Web API project template.</span></span> <span data-ttu-id="a9fab-209">Así se crea un punto de conexión HTTP para el servicio que se expondrá en Azure API Management:</span><span class="sxs-lookup"><span data-stu-id="a9fab-209">This creates an HTTP endpoint for your service, which you'll expose through Azure API Management:</span></span>

```
/api/values
```

<span data-ttu-id="a9fab-210">Empiece por [configurar el entorno de desarrollo para ASP.NET Core](service-fabric-add-a-web-frontend.md#set-up-your-environment-for-aspnet-core).</span><span class="sxs-lookup"><span data-stu-id="a9fab-210">Start by [setting up your development environment for ASP.NET Core development](service-fabric-add-a-web-frontend.md#set-up-your-environment-for-aspnet-core).</span></span>

<span data-ttu-id="a9fab-211">Una vez configurado el entorno de desarrollo, inicie Visual Studio como administrador y cree un servicio ASP.NET Core:</span><span class="sxs-lookup"><span data-stu-id="a9fab-211">Once your development environment is set up, start Visual Studio as Administrator and create an ASP.NET Core service:</span></span>

 1. <span data-ttu-id="a9fab-212">En Visual Studio, seleccione Archivo -> Nuevo proyecto.</span><span class="sxs-lookup"><span data-stu-id="a9fab-212">In Visual Studio, select File -> New Project.</span></span>
 2. <span data-ttu-id="a9fab-213">En Nube, seleccione la plantilla de aplicación de Service Fabric y asígnele el nombre **"ApiApplication"**.</span><span class="sxs-lookup"><span data-stu-id="a9fab-213">Select the Service Fabric Application template under Cloud and name it **"ApiApplication"**.</span></span>
 3. <span data-ttu-id="a9fab-214">Seleccione la plantilla de servicio de ASP.NET Core y denomine el proyecto **"WebApiService"**.</span><span class="sxs-lookup"><span data-stu-id="a9fab-214">Select the ASP.NET Core service template and name the project **"WebApiService"**.</span></span>
 4. <span data-ttu-id="a9fab-215">Seleccione la plantilla de proyecto de ASP.NET Core 1.1 de API web.</span><span class="sxs-lookup"><span data-stu-id="a9fab-215">Select the Web API ASP.NET Core 1.1 project template.</span></span>
 5. <span data-ttu-id="a9fab-216">Una vez creado el proyecto, abra `PackageRoot\ServiceManifest.xml` y quite los atributos `Port` de la configuración del recurso de punto de conexión:</span><span class="sxs-lookup"><span data-stu-id="a9fab-216">Once the project is created, open `PackageRoot\ServiceManifest.xml` and remove the `Port` attribute from the endpoint resource configuration:</span></span>
 
    ```xml
    <Resources>
      <Endpoints>
        <Endpoint Protocol="http" Name="ServiceEndpoint" Type="Input" />
      </Endpoints>
    </Resources>
    ```

    <span data-ttu-id="a9fab-217">Así, Service Fabric puede especificar un puerto dinámicamente desde el intervalo de puertos de la aplicación, que habremos abierto a través del grupo de seguridad de red en la plantilla del clúster de Resource Manager para que el tráfico fluya a él desde API Management.</span><span class="sxs-lookup"><span data-stu-id="a9fab-217">This allows Service Fabric to specify a port dynamically from the application port range, which we opened through the Network Security Group in the cluster Resource Manager template, allowing traffic to flow to it from API Management.</span></span>
 
 6. <span data-ttu-id="a9fab-218">Presione F5 en Visual Studio para comprobar que la API web está disponible de manera local.</span><span class="sxs-lookup"><span data-stu-id="a9fab-218">Press F5 in Visual Studio to verify the web API is available locally.</span></span> 

    <span data-ttu-id="a9fab-219">Abra Service Fabric Explorer y vaya a una instancia específica del servicio ASP.NET Core para ver la dirección base donde escucha el servicio.</span><span class="sxs-lookup"><span data-stu-id="a9fab-219">Open Service Fabric Explorer and drill down to a specific instance of the ASP.NET Core service to see the base address the service is listening on.</span></span> <span data-ttu-id="a9fab-220">Agregue `/api/values` a la dirección base y ábrala en un explorador.</span><span class="sxs-lookup"><span data-stu-id="a9fab-220">Add `/api/values` to the base address and open it in a browser.</span></span> <span data-ttu-id="a9fab-221">Esta acción invoca el método Get en la clase ValuesController de la plantilla de API web y</span><span class="sxs-lookup"><span data-stu-id="a9fab-221">This invokes the Get method on the ValuesController in the Web API template.</span></span> <span data-ttu-id="a9fab-222">devuelve la respuesta predeterminada de la plantilla, una matriz JSON con dos cadenas:</span><span class="sxs-lookup"><span data-stu-id="a9fab-222">It returns the default response that is provided by the template, a JSON array that contains two strings:</span></span>

    ```json
    ["value1", "value2"]`
    ```

    <span data-ttu-id="a9fab-223">Este es el punto de conexión que deberá exponer a través de API Management en Azure.</span><span class="sxs-lookup"><span data-stu-id="a9fab-223">This is the endpoint that you'll expose through API Management in Azure.</span></span>

 7. <span data-ttu-id="a9fab-224">Por último, implemente la aplicación en el clúster en Azure.</span><span class="sxs-lookup"><span data-stu-id="a9fab-224">Finally, deploy the application to your cluster in Azure.</span></span> <span data-ttu-id="a9fab-225">**Con Visual Studio**, haga clic con el botón derecho en el proyecto de la aplicación y seleccione [Publicar](service-fabric-publish-app-remote-cluster.md#to-publish-an-application-using-the-publish-service-fabric-application-dialog-box).</span><span class="sxs-lookup"><span data-stu-id="a9fab-225">[Using Visual Studio](service-fabric-publish-app-remote-cluster.md#to-publish-an-application-using-the-publish-service-fabric-application-dialog-box), right-click the Application project and select **Publish**.</span></span> <span data-ttu-id="a9fab-226">Proporcione el punto de conexión del clúster (por ejemplo, `mycluster.westus.cloudapp.azure.com:19000`) para implementar la aplicación en el clúster de Service Fabric en Azure.</span><span class="sxs-lookup"><span data-stu-id="a9fab-226">Provide your cluster endpoint (for example, `mycluster.westus.cloudapp.azure.com:19000`) to deploy the application to your Service Fabric cluster in Azure.</span></span>

<span data-ttu-id="a9fab-227">En el clúster de Service Fabric en Azure ahora se ejecutará un servicio sin estado ASP.NET Core denominado `fabric:/ApiApplication/WebApiService`.</span><span class="sxs-lookup"><span data-stu-id="a9fab-227">An ASP.NET Core stateless service named `fabric:/ApiApplication/WebApiService` should now be running in your Service Fabric cluster in Azure.</span></span>

## <a name="create-an-api-operation"></a><span data-ttu-id="a9fab-228">Creación de una operación de API</span><span class="sxs-lookup"><span data-stu-id="a9fab-228">Create an API operation</span></span>

<span data-ttu-id="a9fab-229">Ahora estamos listos crear una operación en API Management que los clientes externos usarán para comunicarse con el servicio sin estado ASP.NET Core que se ejecuta en el clúster de Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="a9fab-229">Now we're ready to create an operation in API Management that external clients use to communicate with the ASP.NET Core stateless service running in the Service Fabric cluster.</span></span>

 1. <span data-ttu-id="a9fab-230">Inicie sesión en Azure Portal y vaya a la implementación del servicio API Management.</span><span class="sxs-lookup"><span data-stu-id="a9fab-230">Log in to the Azure portal and navigate to your API Management service deployment.</span></span>
 2. <span data-ttu-id="a9fab-231">En la hoja del servicio API Management, seleccione **API - VERSIÓN PRELIMINAR**.</span><span class="sxs-lookup"><span data-stu-id="a9fab-231">In the API Management service blade, select **APIs - Preview**</span></span>
 3. <span data-ttu-id="a9fab-232">Haga clic en el cuadro **Blank API** (API en blanco) y rellene el cuadro de diálogo para agregar una API nueva:</span><span class="sxs-lookup"><span data-stu-id="a9fab-232">Add a new API by clicking the **Blank API** box and filling out the dialog box:</span></span>

     - <span data-ttu-id="a9fab-233">**URL de servicio Web**: para los back-end de Service Fabric, no se utiliza.</span><span class="sxs-lookup"><span data-stu-id="a9fab-233">**Web service URL**: For Service Fabric backends, this URL value is not used.</span></span> <span data-ttu-id="a9fab-234">Puede escribir aquí cualquier valor.</span><span class="sxs-lookup"><span data-stu-id="a9fab-234">You can put any value here.</span></span> <span data-ttu-id="a9fab-235">Para este tutorial usaremos `http://servicefabric`.</span><span class="sxs-lookup"><span data-stu-id="a9fab-235">For this tutorial, use: `http://servicefabric`.</span></span>
     - <span data-ttu-id="a9fab-236">**Nombre**: proporcione cualquier nombre para la API.</span><span class="sxs-lookup"><span data-stu-id="a9fab-236">**Name**: Provide any name for your API.</span></span> <span data-ttu-id="a9fab-237">Para este tutorial usaremos `Service Fabric App`.</span><span class="sxs-lookup"><span data-stu-id="a9fab-237">For this tutorial, use `Service Fabric App`.</span></span>
     - <span data-ttu-id="a9fab-238">**Esquema URL**: seleccione HTTP, HTTPS o ambos.</span><span class="sxs-lookup"><span data-stu-id="a9fab-238">**URL scheme**: Select either HTTP, HTTPS, or both.</span></span> <span data-ttu-id="a9fab-239">Para este tutorial usaremos `both`.</span><span class="sxs-lookup"><span data-stu-id="a9fab-239">For this tutorial, use `both`.</span></span>
     - <span data-ttu-id="a9fab-240">**API URL Suffix** (Sufijo de URL para API): proporcione un sufijo para la API.</span><span class="sxs-lookup"><span data-stu-id="a9fab-240">**API URL Suffix**: Provide a suffix for our API.</span></span> <span data-ttu-id="a9fab-241">Para este tutorial usaremos `myapp`.</span><span class="sxs-lookup"><span data-stu-id="a9fab-241">For this tutorial, use `myapp`.</span></span>
 
 4. <span data-ttu-id="a9fab-242">Una vez creada la API, haga clic en **+ Add operation** (+ Agregar operación) para agregar una operación de API de front-end.</span><span class="sxs-lookup"><span data-stu-id="a9fab-242">Once the API is created, click **+ Add operation** to add a front-end API operation.</span></span> <span data-ttu-id="a9fab-243">Rellene los valores:</span><span class="sxs-lookup"><span data-stu-id="a9fab-243">Fill out the values:</span></span>
    
     - <span data-ttu-id="a9fab-244">**URL**: seleccione `GET` y proporcione una ruta de acceso URL para la API.</span><span class="sxs-lookup"><span data-stu-id="a9fab-244">**URL**: Select `GET` and provide a URL path for the API.</span></span> <span data-ttu-id="a9fab-245">Para este tutorial usaremos `/api/values`.</span><span class="sxs-lookup"><span data-stu-id="a9fab-245">For this tutorial, use `/api/values`.</span></span>
     
       <span data-ttu-id="a9fab-246">De forma predeterminada, la ruta de acceso URL que se especifica aquí se envía al servicio de back-end de Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="a9fab-246">By default, the URL path specified here is the URL path sent to the backend Service Fabric service.</span></span> <span data-ttu-id="a9fab-247">Si utiliza aquí la misma ruta de acceso URL que usa el servicio, en este caso, `/api/values`, la operación funciona sin más modificaciones.</span><span class="sxs-lookup"><span data-stu-id="a9fab-247">If you use the same URL path here that your service uses, in this case `/api/values`, then the operation works without further modification.</span></span> <span data-ttu-id="a9fab-248">También puede especificar aquí una ruta de acceso URL distinta de la que usa el servicio de back-end de Service Fabric, en cuyo caso también deberá especificar después una ruta de acceso de reescritura en la directiva de la operación.</span><span class="sxs-lookup"><span data-stu-id="a9fab-248">You may also specify a URL path here that is different from the URL path used by your backend Service Fabric service, in which case you will also need to specify a path rewrite in your operation policy later.</span></span>
     - <span data-ttu-id="a9fab-249">**Nombre para mostrar**: proporcione cualquier nombre para la API.</span><span class="sxs-lookup"><span data-stu-id="a9fab-249">**Display name**: Provide any name for the API.</span></span> <span data-ttu-id="a9fab-250">Para este tutorial usaremos `Values`.</span><span class="sxs-lookup"><span data-stu-id="a9fab-250">For this tutorial, use `Values`.</span></span>

## <a name="configure-a-backend-policy"></a><span data-ttu-id="a9fab-251">Configuración de una directiva de back-end</span><span class="sxs-lookup"><span data-stu-id="a9fab-251">Configure a backend policy</span></span>

<span data-ttu-id="a9fab-252">La directiva de back-end une todos los elementos.</span><span class="sxs-lookup"><span data-stu-id="a9fab-252">The backend policy ties everything together.</span></span> <span data-ttu-id="a9fab-253">Es donde se configura el servicio de back-end de Service Fabric al que se enrutan las solicitudes.</span><span class="sxs-lookup"><span data-stu-id="a9fab-253">This is where you configure the backend Service Fabric service to which requests are routed.</span></span> <span data-ttu-id="a9fab-254">Puede aplicar esta directiva a cualquier operación de API.</span><span class="sxs-lookup"><span data-stu-id="a9fab-254">You can apply this policy to any API operation.</span></span> <span data-ttu-id="a9fab-255">La [configuración de back-end de Service Fabric](https://docs.microsoft.com/azure/api-management/api-management-transformation-policies#SetBackendService) proporciona los controles de enrutamiento de solicitudes siguientes:</span><span class="sxs-lookup"><span data-stu-id="a9fab-255">The [backend configuration for Service Fabric](https://docs.microsoft.com/azure/api-management/api-management-transformation-policies#SetBackendService) provides the following request routing controls:</span></span> 
 - <span data-ttu-id="a9fab-256">Selección de instancias de servicio mediante la especificación de un nombre de instancia de servicio de Service Fabric, ya sea codificado de forma rígida (por ejemplo, `"fabric:/myapp/myservice"`) o generado a partir de la solicitud HTTP (por ejemplo, `"fabric:/myapp/users/" + context.Request.MatchedParameters["name"]`).</span><span class="sxs-lookup"><span data-stu-id="a9fab-256">Service instance selection by specifying a Service Fabric service instance name, either hardcoded (for example, `"fabric:/myapp/myservice"`) or generated from the HTTP request (for example, `"fabric:/myapp/users/" + context.Request.MatchedParameters["name"]`).</span></span>
 - <span data-ttu-id="a9fab-257">Resolución de la partición mediante la generación de una clave de partición a partir de cualquier esquema de partición de Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="a9fab-257">Partition resolution by generating a partition key using any Service Fabric partitioning scheme.</span></span>
 - <span data-ttu-id="a9fab-258">Selección de réplicas para los servicios con estado.</span><span class="sxs-lookup"><span data-stu-id="a9fab-258">Replica selection for stateful services.</span></span>
 - <span data-ttu-id="a9fab-259">Condiciones de reintento de resolución que permiten especificar las condiciones para volver a resolver una ubicación de servicio y volver a enviar una solicitud.</span><span class="sxs-lookup"><span data-stu-id="a9fab-259">Resolution retry conditions that allow you to specify the conditions for re-resolving a service location and resending a request.</span></span>

<span data-ttu-id="a9fab-260">Para este tutorial, cree una directiva de back-end que enrute las solicitudes directamente al servicio sin estado ASP.NET Core implementado anteriormente:</span><span class="sxs-lookup"><span data-stu-id="a9fab-260">For this tutorial, create a backend policy that routes requests directly to the ASP.NET Core stateless service deployed earlier:</span></span>

 1. <span data-ttu-id="a9fab-261">Seleccione y edite las **directivas de entrada** para la operación `Values`; para ello, haga clic en el icono de edición y seleccione **Vista Código**.</span><span class="sxs-lookup"><span data-stu-id="a9fab-261">Select and edit the **inbound policies** for the `Values` operation by clicking the edit icon, and then selecting **Code View**.</span></span>
 2. <span data-ttu-id="a9fab-262">En el editor de código de directivas, agregue una directiva `set-backend-service` en las directivas de entrada tal y como se muestra aquí y haga clic en el botón **Guardar**:</span><span class="sxs-lookup"><span data-stu-id="a9fab-262">In the policy code editor, add a `set-backend-service` policy under inbound policies as shown here and click the **Save** button:</span></span>
    
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

<span data-ttu-id="a9fab-263">Para obtener un conjunto completo de los atributos de directiva de back-end de Service Fabric, consulte la [documentación de back-end de API Management](https://docs.microsoft.com/azure/api-management/api-management-transformation-policies#SetBackendService).</span><span class="sxs-lookup"><span data-stu-id="a9fab-263">For a full set of Service Fabric back-end policy attributes, refer to the [API Management back-end documentation](https://docs.microsoft.com/azure/api-management/api-management-transformation-policies#SetBackendService)</span></span>

### <a name="add-the-api-to-a-product"></a><span data-ttu-id="a9fab-264">Incorporación de la API a un producto</span><span class="sxs-lookup"><span data-stu-id="a9fab-264">Add the API to a product.</span></span> 

<span data-ttu-id="a9fab-265">Antes de que se pueda llamar a la API, debe agregarse a un producto para conceder acceso a los usuarios.</span><span class="sxs-lookup"><span data-stu-id="a9fab-265">Before you can call the API, it must be added to a product where you can grant access to users.</span></span> 

 1. <span data-ttu-id="a9fab-266">En el servicio API Management, seleccione **Productos - VERSIÓN PRELIMINAR**.</span><span class="sxs-lookup"><span data-stu-id="a9fab-266">In the API Management service, select **Products - PREVIEW**.</span></span>
 2. <span data-ttu-id="a9fab-267">De forma predeterminada, API Management ofrece dos productos: Starter y Unlimited.</span><span class="sxs-lookup"><span data-stu-id="a9fab-267">By default, API Management providers two products: Starter and Unlimited.</span></span> <span data-ttu-id="a9fab-268">Seleccione el producto Unlimited.</span><span class="sxs-lookup"><span data-stu-id="a9fab-268">Select the Unlimited product.</span></span>
 3. <span data-ttu-id="a9fab-269">Seleccione las API.</span><span class="sxs-lookup"><span data-stu-id="a9fab-269">Select APIs.</span></span>
 4. <span data-ttu-id="a9fab-270">Haga clic en el botón **+ Agregar**.</span><span class="sxs-lookup"><span data-stu-id="a9fab-270">Click the **+ Add** button.</span></span>
 5. <span data-ttu-id="a9fab-271">Seleccione la API `Service Fabric App` que creó en los pasos anteriores y haga clic en el botón **Seleccionar**.</span><span class="sxs-lookup"><span data-stu-id="a9fab-271">Select the `Service Fabric App` API you created in the previous steps and click the **Select** button.</span></span>

### <a name="test-it"></a><span data-ttu-id="a9fab-272">Pruébelo.</span><span class="sxs-lookup"><span data-stu-id="a9fab-272">Test it</span></span>

<span data-ttu-id="a9fab-273">Ahora puede intentar enviar una solicitud al servicio back-end de Service Fabric a través de API Management directamente desde Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="a9fab-273">You can now try sending a request to your back-end service in Service Fabric through API Management directly from the Azure portal.</span></span>

 1. <span data-ttu-id="a9fab-274">En el servicio API Management, seleccione **API - PREVIEW** (API [versión preliminar]).</span><span class="sxs-lookup"><span data-stu-id="a9fab-274">In the API Management service, select **API - PREVIEW**.</span></span>
 2. <span data-ttu-id="a9fab-275">En la API `Service Fabric App` que creó en los pasos anteriores, seleccione la pestaña **Prueba**.</span><span class="sxs-lookup"><span data-stu-id="a9fab-275">In the `Service Fabric App` API you created in the previous steps, select the **Test** tab.</span></span>
 3. <span data-ttu-id="a9fab-276">Haga clic en el botón **Enviar** para enviar una solicitud de prueba al servicio de back-end.</span><span class="sxs-lookup"><span data-stu-id="a9fab-276">Click the **Send** button to send a test request to the backend service.</span></span>

## <a name="next-steps"></a><span data-ttu-id="a9fab-277">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="a9fab-277">Next steps</span></span>

<span data-ttu-id="a9fab-278">Llegados a este punto, debe tener una configuración básica de Service Fabric y API Management.</span><span class="sxs-lookup"><span data-stu-id="a9fab-278">At this point, you should have a basic setup with Service Fabric and API Management.</span></span>

<span data-ttu-id="a9fab-279">Para una rápida configuración, en este tutorial se utiliza la autenticación de usuario básica basada en certificados para el clúster de Service Fabric,</span><span class="sxs-lookup"><span data-stu-id="a9fab-279">This tutorial uses basic certificate-based user authentication for your Service Fabric cluster to get you set up quickly.</span></span> <span data-ttu-id="a9fab-280">aunque para el clúster de Service Fabric es preferible una autenticación de usuarios más avanzada con [autenticación de Azure Active Directory](service-fabric-cluster-creation-via-arm.md#set-up-azure-active-directory-for-client-authentication).</span><span class="sxs-lookup"><span data-stu-id="a9fab-280">More advanced user authentication for your Service Fabric cluster is preferable with [Azure Active Directory authentication](service-fabric-cluster-creation-via-arm.md#set-up-azure-active-directory-for-client-authentication).</span></span> 

<span data-ttu-id="a9fab-281">A continuación, [cree y configure las opciones de producto avanzadas en Azure API Management](https://docs.microsoft.com/azure/api-management/api-management-howto-product-with-rules) para preparar la aplicación para el tráfico del mundo real.</span><span class="sxs-lookup"><span data-stu-id="a9fab-281">Next, [create and configure advanced product settings in Azure API Management](https://docs.microsoft.com/azure/api-management/api-management-howto-product-with-rules) to prepare your application for real world traffic.</span></span>

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
