---
title: "aaaCreate una conexión a Internet cargar equilibrador - PowerShell de Azure clásico | Documentos de Microsoft"
description: "Obtenga información acerca de cómo toocreate una conexión a Internet equilibrador de carga de modo clásico con PowerShell"
services: load-balancer
documentationcenter: na
author: kumudd
manager: timlt
tags: azure-service-management
ms.assetid: 73e8bfa4-8086-4ef0-9e35-9e00b24be319
ms.service: load-balancer
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 01/23/2017
ms.author: kumud
ms.openlocfilehash: 76d9a712a0acda223fc86b80be9c35c0ed9f3a50
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-creating-an-internet-facing-load-balancer-classic-in-powershell"></a><span data-ttu-id="32737-103">Introducción a la creación de un equilibrador de carga orientado a Internet (clásico) en PowerShell</span><span class="sxs-lookup"><span data-stu-id="32737-103">Get started creating an Internet facing load balancer (classic) in PowerShell</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="32737-104">Portal de Azure clásico</span><span class="sxs-lookup"><span data-stu-id="32737-104">Azure classic portal</span></span>](../load-balancer/load-balancer-get-started-internet-classic-portal.md)
> * [<span data-ttu-id="32737-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="32737-105">PowerShell</span></span>](../load-balancer/load-balancer-get-started-internet-classic-ps.md)
> * [<span data-ttu-id="32737-106">CLI de Azure</span><span class="sxs-lookup"><span data-stu-id="32737-106">Azure CLI</span></span>](../load-balancer/load-balancer-get-started-internet-classic-cli.md)
> * [<span data-ttu-id="32737-107">Servicios en la nube de Azure</span><span class="sxs-lookup"><span data-stu-id="32737-107">Azure Cloud Services</span></span>](../load-balancer/load-balancer-get-started-internet-classic-cloud.md)

[!INCLUDE [load-balancer-get-started-internet-intro-include.md](../../includes/load-balancer-get-started-internet-intro-include.md)]

> [!IMPORTANT]
> <span data-ttu-id="32737-108">Antes de trabajar con recursos de Azure, es importante toounderstand que Azure tiene dos modelos de implementación: Administrador de recursos de Azure y clásico.</span><span class="sxs-lookup"><span data-stu-id="32737-108">Before you work with Azure resources, it's important toounderstand that Azure currently has two deployment models: Azure Resource Manager and classic.</span></span> <span data-ttu-id="32737-109">Asegúrese de que comprende los [modelos de implementación y las herramientas](../azure-classic-rm.md) antes de trabajar con recursos de Azure.</span><span class="sxs-lookup"><span data-stu-id="32737-109">Make sure you understand [deployment models and tools](../azure-classic-rm.md) before you work with any Azure resource.</span></span> <span data-ttu-id="32737-110">Puede ver documentación de Hola de distintas herramientas, haga clic en las pestañas de hello en parte superior de Hola de este artículo.</span><span class="sxs-lookup"><span data-stu-id="32737-110">You can view hello documentation for different tools by clicking hello tabs at hello top of this article.</span></span> <span data-ttu-id="32737-111">Este artículo trata el modelo de implementación clásica de Hola.</span><span class="sxs-lookup"><span data-stu-id="32737-111">This article covers hello classic deployment model.</span></span> <span data-ttu-id="32737-112">También puede [Obtenga información acerca de cómo toocreate una conexión a Internet cargar equilibrador mediante Azure Resource Manager](load-balancer-get-started-internet-arm-ps.md).</span><span class="sxs-lookup"><span data-stu-id="32737-112">You can also [Learn how toocreate an Internet facing load balancer using Azure Resource Manager](load-balancer-get-started-internet-arm-ps.md).</span></span>

[!INCLUDE [load-balancer-get-started-internet-scenario-include.md](../../includes/load-balancer-get-started-internet-scenario-include.md)]

## <a name="set-up-load-balancer-using-powershell"></a><span data-ttu-id="32737-113">Configurar el equilibrador de carga con PowerShell</span><span class="sxs-lookup"><span data-stu-id="32737-113">Set up load balancer using PowerShell</span></span>

<span data-ttu-id="32737-114">tooset de un equilibrador de carga con powershell, siga Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="32737-114">tooset up a load balancer using powershell, follow hello steps below:</span></span>

1. <span data-ttu-id="32737-115">Si nunca ha usado PowerShell de Azure, consulte [cómo tooInstall y configurar Azure PowerShell](/powershell/azure/overview) y siga instrucciones de hello todos los toohello de manera Hola finalizar toosign en Azure y seleccione su suscripción.</span><span class="sxs-lookup"><span data-stu-id="32737-115">If you have never used Azure PowerShell, see [How tooInstall and Configure Azure PowerShell](/powershell/azure/overview) and follow hello instructions all hello way toohello end toosign into Azure and select your subscription.</span></span>
2. <span data-ttu-id="32737-116">Después de crear una máquina virtual, puede usar cmdlets de PowerShell tooadd una máquina de tooa de un equilibrador de carga dentro de hello mismo servicio en la nube.</span><span class="sxs-lookup"><span data-stu-id="32737-116">After creating a virtual machine, you can use PowerShell cmdlets tooadd a load balancer tooa virtual machine within hello same cloud service.</span></span>

<span data-ttu-id="32737-117">Hola el ejemplo siguiente se va a agregar un conjunto de equilibrador de carga denominada "granja de servidores Web" toocloud máquinas "mytestcloud" (o myctestcloud.cloudapp.net), agregar extremos de Hola para hello toovirtual de equilibrador de carga de servicio denominada "web1" y "web2".</span><span class="sxs-lookup"><span data-stu-id="32737-117">In hello following example you will add a load balancer set called "webfarm" toocloud service "mytestcloud" (or myctestcloud.cloudapp.net) , adding hello endpoints for hello load balancer toovirtual machines named "web1" and "web2".</span></span> <span data-ttu-id="32737-118">equilibrador de carga Hello recibe tráfico de red en el puerto 80 y equilibra la carga entre máquinas virtuales de hello definidas por el extremo local de hello (en este caso puerto 80) mediante TCP.</span><span class="sxs-lookup"><span data-stu-id="32737-118">hello load balancer receives network traffic on port 80 and load balances between hello virtual machines defined by hello local endpoint (in this case port 80) using TCP.</span></span>

### <a name="step-1"></a><span data-ttu-id="32737-119">Paso 1</span><span class="sxs-lookup"><span data-stu-id="32737-119">Step 1</span></span>

<span data-ttu-id="32737-120">Crear un extremo con equilibrio de carga para máquinas virtuales de primera Hola "web1"</span><span class="sxs-lookup"><span data-stu-id="32737-120">Create a load balanced endpoint for hello first VM "web1"</span></span>

```powershell
Get-AzureVM -ServiceName "mytestcloud" -Name "web1" | Add-AzureEndpoint -Name "HttpIn" -Protocol "tcp" -PublicPort 80 -LocalPort 80 -LBSetName "WebFarm" -ProbePort 80 -ProbeProtocol "http" -ProbePath '/' | Update-AzureVM
```

### <a name="step-2"></a><span data-ttu-id="32737-121">Paso 2</span><span class="sxs-lookup"><span data-stu-id="32737-121">Step 2</span></span>

<span data-ttu-id="32737-122">Cree otro punto de conexión para hello en segundo lugar máquina virtual "web2" con hello mismo carga nombre del equilibrador de conjunto</span><span class="sxs-lookup"><span data-stu-id="32737-122">Create another endpoint for hello second VM  "web2" using hello same load balancer set name</span></span>

```powershell
Get-AzureVM -ServiceName "mytestcloud" -Name "web2" | Add-AzureEndpoint -Name "HttpIn" -Protocol "tcp" -PublicPort 80 -LocalPort 80 -LBSetName "WebFarm" -ProbePort 80 -ProbeProtocol "http" -ProbePath '/' | Update-AzureVM
```

## <a name="remove-a-virtual-machine-from-a-load-balancer"></a><span data-ttu-id="32737-123">Quitar una máquina virtual de un equilibrador de carga</span><span class="sxs-lookup"><span data-stu-id="32737-123">Remove a virtual machine from a load balancer</span></span>

<span data-ttu-id="32737-124">Puede usar Remove-AzureEndpoint tooremove un punto de conexión de máquina virtual de equilibrador de carga de Hola</span><span class="sxs-lookup"><span data-stu-id="32737-124">You can use Remove-AzureEndpoint tooremove a virtual machine endpoint from hello load balancer</span></span>

```powershell
Get-azureVM -ServiceName mytestcloud  -Name web1 |Remove-AzureEndpoint -Name httpin | Update-AzureVM
```

## <a name="next-steps"></a><span data-ttu-id="32737-125">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="32737-125">Next steps</span></span>

<span data-ttu-id="32737-126">También puede [empezar a crear un equilibrador de carga interno](load-balancer-get-started-ilb-classic-ps.md) y configurar el tipo de [modo de distribución](load-balancer-distribution-mode.md) para un comportamiento del tráfico de red de un equilibrador de carga específico.</span><span class="sxs-lookup"><span data-stu-id="32737-126">You can also [get started creating an internal load balancer](load-balancer-get-started-ilb-classic-ps.md) and configure what type of [distribution mode](load-balancer-distribution-mode.md) for a specific load balancer network traffic behavior.</span></span>

<span data-ttu-id="32737-127">Si su aplicación necesita que las conexiones de tookeep activo de servidores detrás de un equilibrador de carga, puede conocer más acerca de [inactivo de la configuración de tiempo de espera TCP para un equilibrador de carga](load-balancer-tcp-idle-timeout.md).</span><span class="sxs-lookup"><span data-stu-id="32737-127">If your application needs tookeep connections alive for servers behind a load balancer, you can understand more about [idle TCP timeout settings for a load balancer](load-balancer-tcp-idle-timeout.md).</span></span> <span data-ttu-id="32737-128">Cuando se usa el equilibrador de carga de Azure le servirá de ayuda toolearn acerca del comportamiento de conexión inactiva.</span><span class="sxs-lookup"><span data-stu-id="32737-128">It will help toolearn about idle connection behavior when you are using Azure Load Balancer.</span></span>
