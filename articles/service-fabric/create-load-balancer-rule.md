---
title: "aaaCreate una regla de equilibrador de carga de Azure para un clúster"
description: "Configurar los puertos de tooopen de un equilibrador de carga de Azure para el clúster de Azure Service Fabric."
services: service-fabric
documentationcenter: na
author: thraka
manager: timlt
editor: 
ms.assetid: 
ms.service: service-fabric
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 08/22/2017
ms.author: adegeo
ms.openlocfilehash: 4a40f62422bd895d782be8cbaace5f4e1af81db3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="open-ports-for-a-service-fabric-cluster"></a><span data-ttu-id="0667e-103">Abrir puertos para un clúster de Service Fabric</span><span class="sxs-lookup"><span data-stu-id="0667e-103">Open ports for a Service Fabric cluster</span></span>

<span data-ttu-id="0667e-104">equilibrador de carga de Hello implementado con el clúster de Azure Service Fabric dirige el tráfico tooyour aplicación que se ejecuta en un nodo.</span><span class="sxs-lookup"><span data-stu-id="0667e-104">hello load balancer deployed with your Azure Service Fabric cluster directs traffic tooyour app running on a node.</span></span> <span data-ttu-id="0667e-105">Si cambia su toouse de aplicación un puerto diferente, debe exponer dicho puerto (o enrutar un puerto diferente) Hola equilibrador de carga de Azure.</span><span class="sxs-lookup"><span data-stu-id="0667e-105">If you change your app toouse a different port, you must expose that port (or route a different port) in hello Azure Load Balancer.</span></span>

<span data-ttu-id="0667e-106">Cuando implementa la tooAzure de clúster de tejido de servicio, se crea automáticamente un equilibrador de carga.</span><span class="sxs-lookup"><span data-stu-id="0667e-106">When you deployed your service fabric cluster tooAzure, a load balancer was automatically created for you.</span></span> <span data-ttu-id="0667e-107">Si no tiene un equilibrador de carga, consulte [Creación de un equilibrador de carga orientado a Internet](..\load-balancer\load-balancer-get-started-internet-portal.md).</span><span class="sxs-lookup"><span data-stu-id="0667e-107">If you do not have a load balancer, see [Configure an Internet-facing load balancer](..\load-balancer\load-balancer-get-started-internet-portal.md).</span></span>

## <a name="configure-service-fabric"></a><span data-ttu-id="0667e-108">Configurar Service Fabric</span><span class="sxs-lookup"><span data-stu-id="0667e-108">Configure service fabric</span></span>

<span data-ttu-id="0667e-109">La aplicación de Service Fabric **ServiceManifest.xml** el archivo de configuración define los puntos de conexión de hello toouse de espera de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="0667e-109">Your Service Fabric application **ServiceManifest.xml** config file defines hello endpoints your application expects toouse.</span></span> <span data-ttu-id="0667e-110">Después de que el archivo de configuración de hello ha sido actualizada toodefine un punto de conexión, equilibrador de carga de hello debe ser actualizada tooexpose ese (o a diferentes) puerto.</span><span class="sxs-lookup"><span data-stu-id="0667e-110">After hello config file has been updated toodefine an endpoint, hello load balancer must be updated tooexpose that (or a different) port.</span></span> <span data-ttu-id="0667e-111">Para obtener más información sobre cómo toocreate Hola extremo de tejido de servicio, consulte [configurar un punto de conexión](service-fabric-service-manifest-resources.md).</span><span class="sxs-lookup"><span data-stu-id="0667e-111">For more information on how toocreate hello service fabric endpoint, see [Setup an Endpoint](service-fabric-service-manifest-resources.md).</span></span>

## <a name="create-a-load-balancer-rule"></a><span data-ttu-id="0667e-112">Creación de una regla de equilibrador de carga</span><span class="sxs-lookup"><span data-stu-id="0667e-112">Create a load balancer rule</span></span>

<span data-ttu-id="0667e-113">Una regla de equilibrador de carga se abre un puerto de conexión a internet y reenvía el puerto del nodo interno de tráfico toohello utilizado por la aplicación.</span><span class="sxs-lookup"><span data-stu-id="0667e-113">A load balancer rule opens up an internet-facing port and forwards traffic toohello internal node's port used by your application.</span></span> <span data-ttu-id="0667e-114">Si no tiene un equilibrador de carga, consulte [Creación de un equilibrador de carga orientado a Internet](..\load-balancer\load-balancer-get-started-internet-portal.md).</span><span class="sxs-lookup"><span data-stu-id="0667e-114">If you do not have a load balancer, see [Configure an Internet-facing load balancer](..\load-balancer\load-balancer-get-started-internet-portal.md).</span></span>

<span data-ttu-id="0667e-115">regla toocreate un equilibrador de carga, necesita hello toocollect siguiente información:</span><span class="sxs-lookup"><span data-stu-id="0667e-115">toocreate a load balancer rule, you need toocollect hello following information:</span></span>

- <span data-ttu-id="0667e-116">Nombre del equilibrador de carga.</span><span class="sxs-lookup"><span data-stu-id="0667e-116">Load balancer name.</span></span>
- <span data-ttu-id="0667e-117">Grupo de recursos de hello equilibrador de carga y clúster de service fabric.</span><span class="sxs-lookup"><span data-stu-id="0667e-117">Resource group of hello load balancer and service fabric cluster.</span></span>
- <span data-ttu-id="0667e-118">Puerto externo.</span><span class="sxs-lookup"><span data-stu-id="0667e-118">External port.</span></span>
- <span data-ttu-id="0667e-119">Puerto interno.</span><span class="sxs-lookup"><span data-stu-id="0667e-119">Internal port.</span></span>

## <a name="azure-cli"></a><span data-ttu-id="0667e-120">CLI de Azure</span><span class="sxs-lookup"><span data-stu-id="0667e-120">Azure CLI</span></span>
>[!NOTE]
><span data-ttu-id="0667e-121">Si necesita toodetermine Hola nombre del equilibrador de carga de hello, utilice este get tooquickly de comando una lista de todos los grupos de recursos de hello asociado y equilibradores de carga.</span><span class="sxs-lookup"><span data-stu-id="0667e-121">If you need toodetermine hello name of hello load balancer, use this command tooquickly get a list of all load balancers and hello associated resource groups.</span></span>
>
>`az network lb list --query "[].{ResourceGroup: resourceGroup, Name: name}"`
>

<span data-ttu-id="0667e-122">Basta con un único comando toocreate una regla de equilibrador de carga con hello **CLI de Azure**.</span><span class="sxs-lookup"><span data-stu-id="0667e-122">It only takes a single command toocreate a load balancer rule with hello **Azure CLI**.</span></span> <span data-ttu-id="0667e-123">Solo tiene tooknow tanto nombre Hola de carga de hello equilibrador y recursos toocreate de grupo una nueva regla.</span><span class="sxs-lookup"><span data-stu-id="0667e-123">You just need tooknow both hello name of hello load balancer and resource group toocreate a new rule.</span></span>

```azurecli
az network lb rule create --backend-port 40000 --frontend-port 39999 --protocol Tcp --lb-name LB-svcfab3 -g svcfab_cli -n my-app-rule
```

<span data-ttu-id="0667e-124">Hola comando de CLI de Azure tiene unos parámetros que se describen en hello en la tabla siguiente:</span><span class="sxs-lookup"><span data-stu-id="0667e-124">hello Azure CLI command has a few parameters that are described in hello following table:</span></span>

| <span data-ttu-id="0667e-125">Parámetro</span><span class="sxs-lookup"><span data-stu-id="0667e-125">Parameter</span></span> | <span data-ttu-id="0667e-126">Descripción</span><span class="sxs-lookup"><span data-stu-id="0667e-126">Description</span></span> |
| --------- | ----------- |
| `--backend-port`  | <span data-ttu-id="0667e-127">aplicación de tejido de Hello puerto Hola servicio está escuchando.</span><span class="sxs-lookup"><span data-stu-id="0667e-127">hello port hello service fabric application is listening to.</span></span> |
| `--frontend-port` | <span data-ttu-id="0667e-128">Hola Hola de puerto cargar equilibrador expone para las conexiones externas.</span><span class="sxs-lookup"><span data-stu-id="0667e-128">hello port hello load balancer exposes for external connections.</span></span> |
| `-lb-name` | <span data-ttu-id="0667e-129">nombre de Hola de hello cargar equilibrador toochange.</span><span class="sxs-lookup"><span data-stu-id="0667e-129">hello name of hello load balancer toochange.</span></span> |
| `-g`       | <span data-ttu-id="0667e-130">grupo de recursos de Hello con equilibrador de carga de Hola y clúster de service fabric.</span><span class="sxs-lookup"><span data-stu-id="0667e-130">hello resource group that has both hello load balancer and service fabric cluster.</span></span> |
| `-n`       | <span data-ttu-id="0667e-131">Hola elegido el nombre de regla de Hola.</span><span class="sxs-lookup"><span data-stu-id="0667e-131">hello chosen name of hello rule.</span></span> |


>[!NOTE]
><span data-ttu-id="0667e-132">Para obtener más información sobre cómo toocreate un equilibrador de carga con hello CLI de Azure, consulte [crear un equilibrador de carga con hello Azure CLI](..\load-balancer\load-balancer-get-started-internet-arm-cli.md).</span><span class="sxs-lookup"><span data-stu-id="0667e-132">For more information on how toocreate a load balancer with hello Azure CLI, see [Create a load balancer with hello Azure CLI](..\load-balancer\load-balancer-get-started-internet-arm-cli.md).</span></span>

## <a name="powershell"></a><span data-ttu-id="0667e-133">PowerShell</span><span class="sxs-lookup"><span data-stu-id="0667e-133">PowerShell</span></span>

>[!NOTE]
><span data-ttu-id="0667e-134">Si necesita toodetermine Hola nombre del equilibrador de carga de hello, use este get tooquickly de comando una lista de todos los equilibradores de carga y grupos de recursos asociados.</span><span class="sxs-lookup"><span data-stu-id="0667e-134">If you need toodetermine hello name of hello load balancer, use this command tooquickly get a list of all load balancers and associated resource groups.</span></span>
>
>`Get-AzureRmLoadBalancer | Select Name, ResourceGroupName`

<span data-ttu-id="0667e-135">PowerShell es un poco más complicado que Hola CLI de Azure.</span><span class="sxs-lookup"><span data-stu-id="0667e-135">PowerShell is a little more complicated than hello Azure CLI.</span></span> <span data-ttu-id="0667e-136">Conceptualmente, hacer Hola siguiendo los pasos toocreate una regla.</span><span class="sxs-lookup"><span data-stu-id="0667e-136">Conceptually, do hello following steps toocreate a rule.</span></span>

1. <span data-ttu-id="0667e-137">Obtener el equilibrador de carga de Hola de Azure.</span><span class="sxs-lookup"><span data-stu-id="0667e-137">Get hello load balancer from Azure.</span></span>
2. <span data-ttu-id="0667e-138">Cree una regla.</span><span class="sxs-lookup"><span data-stu-id="0667e-138">Create a rule.</span></span>
3. <span data-ttu-id="0667e-139">Agregar equilibrador de carga de hello regla toohello.</span><span class="sxs-lookup"><span data-stu-id="0667e-139">Add hello rule toohello load balancer.</span></span>
4. <span data-ttu-id="0667e-140">Actualizar el equilibrador de carga de Hola.</span><span class="sxs-lookup"><span data-stu-id="0667e-140">Update hello load balancer.</span></span>

```powershell
# Get hello load balancer
$lb = Get-AzureRmLoadBalancer -Name LB-svcfab3 -ResourceGroupName svcfab_cli

# Create hello rule based on information from hello load balancer.
$lbrule = New-AzureRmLoadBalancerRuleConfig -Name my-app-rule7 -Protocol Tcp -FrontendPort 39990 -BackendPort 40009 `
                                            -FrontendIpConfiguration $lb.FrontendIpConfigurations[0] `
                                            -BackendAddressPool  $lb.BackendAddressPools[0] `
                                            -Probe $lb.Probes[0]

# Add hello rule toohello load balancer
$lb.LoadBalancingRules.Add($lbrule)

# Update hello load balancer on Azure
$lb | Set-AzureRmLoadBalancer
```

<span data-ttu-id="0667e-141">Con respecto a hello `New-AzureRmLoadBalancerRuleConfig` comando hello `-FrontendPort` expone representa Hola puerto Hola equilibrador de carga para las conexiones externas y hello `-BackendPort` representa Hola puerto Hola tejido del servicio de aplicaciones está escuchando.</span><span class="sxs-lookup"><span data-stu-id="0667e-141">Regarding hello `New-AzureRmLoadBalancerRuleConfig` command, hello `-FrontendPort` represents hello port hello load balancer exposes for external connections, and hello `-BackendPort` represents hello port hello service fabric app is listening to.</span></span>

>[!NOTE]
><span data-ttu-id="0667e-142">Para obtener más información sobre cómo toocreate un equilibrador de carga con PowerShell, vea [crear un equilibrador de carga con PowerShell](..\load-balancer\load-balancer-get-started-internet-arm-ps.md).</span><span class="sxs-lookup"><span data-stu-id="0667e-142">For more information on how toocreate a load balancer with PowerShell, see [Create a load balancer with PowerShell](..\load-balancer\load-balancer-get-started-internet-arm-ps.md).</span></span>

