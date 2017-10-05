---
title: "Creación de un equilibrador de carga con conexión a Internet: Azure PowerShell clásico | Microsoft Docs"
description: "Obtenga información sobre cómo crear un equilibrador de carga orientado a Internet en el modo clásico con PowerShell."
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
ms.openlocfilehash: 1a41f3ba199fb692c111ea6a40ddb09605f91da2
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-creating-an-internet-facing-load-balancer-classic-in-powershell"></a><span data-ttu-id="475f2-103">Introducción a la creación de un equilibrador de carga orientado a Internet (clásico) en PowerShell</span><span class="sxs-lookup"><span data-stu-id="475f2-103">Get started creating an Internet facing load balancer (classic) in PowerShell</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="475f2-104">Portal de Azure clásico</span><span class="sxs-lookup"><span data-stu-id="475f2-104">Azure classic portal</span></span>](../load-balancer/load-balancer-get-started-internet-classic-portal.md)
> * [<span data-ttu-id="475f2-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="475f2-105">PowerShell</span></span>](../load-balancer/load-balancer-get-started-internet-classic-ps.md)
> * [<span data-ttu-id="475f2-106">CLI de Azure</span><span class="sxs-lookup"><span data-stu-id="475f2-106">Azure CLI</span></span>](../load-balancer/load-balancer-get-started-internet-classic-cli.md)
> * [<span data-ttu-id="475f2-107">Azure Cloud Services</span><span class="sxs-lookup"><span data-stu-id="475f2-107">Azure Cloud Services</span></span>](../load-balancer/load-balancer-get-started-internet-classic-cloud.md)

[!INCLUDE [load-balancer-get-started-internet-intro-include.md](../../includes/load-balancer-get-started-internet-intro-include.md)]

> [!IMPORTANT]
> <span data-ttu-id="475f2-108">Antes de trabajar con recursos de Azure, es importante comprender que Azure tiene actualmente dos modelos de implementación: Azure Resource Manager y el clásico.</span><span class="sxs-lookup"><span data-stu-id="475f2-108">Before you work with Azure resources, it's important to understand that Azure currently has two deployment models: Azure Resource Manager and classic.</span></span> <span data-ttu-id="475f2-109">Asegúrese de que comprende los [modelos de implementación y las herramientas](../azure-classic-rm.md) antes de trabajar con recursos de Azure.</span><span class="sxs-lookup"><span data-stu-id="475f2-109">Make sure you understand [deployment models and tools](../azure-classic-rm.md) before you work with any Azure resource.</span></span> <span data-ttu-id="475f2-110">Puede ver la documentación de las distintas herramientas haciendo clic en las fichas en la parte superior de este artículo.</span><span class="sxs-lookup"><span data-stu-id="475f2-110">You can view the documentation for different tools by clicking the tabs at the top of this article.</span></span> <span data-ttu-id="475f2-111">Este artículo trata sobre el modelo de implementación clásico.</span><span class="sxs-lookup"><span data-stu-id="475f2-111">This article covers the classic deployment model.</span></span> <span data-ttu-id="475f2-112">También puede [obtener información sobre cómo crear un equilibrador de carga orientado a Internet con el Administrador de recursos de Azure](load-balancer-get-started-internet-arm-ps.md).</span><span class="sxs-lookup"><span data-stu-id="475f2-112">You can also [Learn how to create an Internet facing load balancer using Azure Resource Manager](load-balancer-get-started-internet-arm-ps.md).</span></span>

[!INCLUDE [load-balancer-get-started-internet-scenario-include.md](../../includes/load-balancer-get-started-internet-scenario-include.md)]

## <a name="set-up-load-balancer-using-powershell"></a><span data-ttu-id="475f2-113">Configurar el equilibrador de carga con PowerShell</span><span class="sxs-lookup"><span data-stu-id="475f2-113">Set up load balancer using PowerShell</span></span>

<span data-ttu-id="475f2-114">Para configurar un equilibrador de carga con PowerShell, siga estos pasos:</span><span class="sxs-lookup"><span data-stu-id="475f2-114">To set up a load balancer using powershell, follow the steps below:</span></span>

1. <span data-ttu-id="475f2-115">Si es la primera vez que usa Azure PowerShell, consulte [Cómo instalar y configurar Azure PowerShell](/powershell/azure/overview) y siga las instrucciones hasta el final para iniciar sesión en Azure y seleccionar su suscripción.</span><span class="sxs-lookup"><span data-stu-id="475f2-115">If you have never used Azure PowerShell, see [How to Install and Configure Azure PowerShell](/powershell/azure/overview) and follow the instructions all the way to the end to sign into Azure and select your subscription.</span></span>
2. <span data-ttu-id="475f2-116">Después de crear una máquina virtual, puede usar cmdlets de PowerShell para agregar un equilibrador de carga a una máquina virtual dentro del mismo servicio en la nube.</span><span class="sxs-lookup"><span data-stu-id="475f2-116">After creating a virtual machine, you can use PowerShell cmdlets to add a load balancer to a virtual machine within the same cloud service.</span></span>

<span data-ttu-id="475f2-117">En el ejemplo siguiente se agregará un conjunto de equilibrador de carga denominado "webfarm" al servicio en la nube "mytestcloud" (o myctestcloud.cloudapp.net), agregando los puntos de conexión para el equilibrador de carga a las máquinas virtuales denominadas "web1" y "web2".</span><span class="sxs-lookup"><span data-stu-id="475f2-117">In the following example you will add a load balancer set called "webfarm" to cloud service "mytestcloud" (or myctestcloud.cloudapp.net) , adding the endpoints for the load balancer to virtual machines named "web1" and "web2".</span></span> <span data-ttu-id="475f2-118">El equilibrador de carga recibe tráfico de red en el puerto 80 y equilibra la carga entre las máquinas virtuales definidas por el punto de conexión local (en este caso el puerto 80) mediante TCP.</span><span class="sxs-lookup"><span data-stu-id="475f2-118">The load balancer receives network traffic on port 80 and load balances between the virtual machines defined by the local endpoint (in this case port 80) using TCP.</span></span>

### <a name="step-1"></a><span data-ttu-id="475f2-119">Paso 1</span><span class="sxs-lookup"><span data-stu-id="475f2-119">Step 1</span></span>

<span data-ttu-id="475f2-120">Crear un punto de conexión con equilibrio de carga para la primera máquina virtual "web1"</span><span class="sxs-lookup"><span data-stu-id="475f2-120">Create a load balanced endpoint for the first VM "web1"</span></span>

```powershell
Get-AzureVM -ServiceName "mytestcloud" -Name "web1" | Add-AzureEndpoint -Name "HttpIn" -Protocol "tcp" -PublicPort 80 -LocalPort 80 -LBSetName "WebFarm" -ProbePort 80 -ProbeProtocol "http" -ProbePath '/' | Update-AzureVM
```

### <a name="step-2"></a><span data-ttu-id="475f2-121">Paso 2</span><span class="sxs-lookup"><span data-stu-id="475f2-121">Step 2</span></span>

<span data-ttu-id="475f2-122">Crear otro punto de conexión para la segunda máquina virtual "web2" con el mismo nombre del conjunto de equilibrador de carga</span><span class="sxs-lookup"><span data-stu-id="475f2-122">Create another endpoint for the second VM  "web2" using the same load balancer set name</span></span>

```powershell
Get-AzureVM -ServiceName "mytestcloud" -Name "web2" | Add-AzureEndpoint -Name "HttpIn" -Protocol "tcp" -PublicPort 80 -LocalPort 80 -LBSetName "WebFarm" -ProbePort 80 -ProbeProtocol "http" -ProbePath '/' | Update-AzureVM
```

## <a name="remove-a-virtual-machine-from-a-load-balancer"></a><span data-ttu-id="475f2-123">Quitar una máquina virtual de un equilibrador de carga</span><span class="sxs-lookup"><span data-stu-id="475f2-123">Remove a virtual machine from a load balancer</span></span>

<span data-ttu-id="475f2-124">Puede usar Remove-AzureEndpoint para quitar un punto de conexión de la máquina virtual del equilibrador de carga.</span><span class="sxs-lookup"><span data-stu-id="475f2-124">You can use Remove-AzureEndpoint to remove a virtual machine endpoint from the load balancer</span></span>

```powershell
Get-azureVM -ServiceName mytestcloud  -Name web1 |Remove-AzureEndpoint -Name httpin | Update-AzureVM
```

## <a name="next-steps"></a><span data-ttu-id="475f2-125">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="475f2-125">Next steps</span></span>

<span data-ttu-id="475f2-126">También puede [empezar a crear un equilibrador de carga interno](load-balancer-get-started-ilb-classic-ps.md) y configurar el tipo de [modo de distribución](load-balancer-distribution-mode.md) para un comportamiento del tráfico de red de un equilibrador de carga específico.</span><span class="sxs-lookup"><span data-stu-id="475f2-126">You can also [get started creating an internal load balancer](load-balancer-get-started-ilb-classic-ps.md) and configure what type of [distribution mode](load-balancer-distribution-mode.md) for a specific load balancer network traffic behavior.</span></span>

<span data-ttu-id="475f2-127">Si la aplicación necesita mantener conexiones activas para servidores detrás de un equilibrador de carga, puede obtener más información acerca de la [configuración de tiempo de espera de inactividad de TCP para el equilibrador de carga](load-balancer-tcp-idle-timeout.md).</span><span class="sxs-lookup"><span data-stu-id="475f2-127">If your application needs to keep connections alive for servers behind a load balancer, you can understand more about [idle TCP timeout settings for a load balancer](load-balancer-tcp-idle-timeout.md).</span></span> <span data-ttu-id="475f2-128">Le ayudará a conocer el comportamiento de conexión del tiempo de inactividad cuando se usa el Equilibrador de carga de Azure.</span><span class="sxs-lookup"><span data-stu-id="475f2-128">It will help to learn about idle connection behavior when you are using Azure Load Balancer.</span></span>
