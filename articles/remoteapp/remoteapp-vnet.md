---
title: "Validación de la red virtual de Azure para su uso con Azure RemoteApp | Microsoft Docs"
description: "Obtenga información sobre cómo asegurarse de que la red virtual de Azure está lista para usarse con Azure RemoteApp"
services: remoteapp
documentationcenter: 
author: msmbaldwin
manager: mbaldwin
ms.assetid: b573ba02-4587-4be5-9821-27bd891a73b2
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/23/2016
ms.author: mbaldwin
ms.openlocfilehash: 05c8a0ff04293947cec391b6467cc4adddb6a7b0
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="validate-the-azure-vnet-to-use-with-azure-remoteapp"></a><span data-ttu-id="8acd2-103">Validación de la red virtual de Azure para su uso con Azure RemoteApp</span><span class="sxs-lookup"><span data-stu-id="8acd2-103">Validate the Azure VNET to use with Azure RemoteApp</span></span>
> [!IMPORTANT]
> <span data-ttu-id="8acd2-104">Azure RemoteApp dejará de estar disponible el 31 de agosto de 2017.</span><span class="sxs-lookup"><span data-stu-id="8acd2-104">Azure RemoteApp is being discontinued on August 31, 2017.</span></span> <span data-ttu-id="8acd2-105">Para obtener más información, lea el [anuncio](https://go.microsoft.com/fwlink/?linkid=821148) .</span><span class="sxs-lookup"><span data-stu-id="8acd2-105">Read the [announcement](https://go.microsoft.com/fwlink/?linkid=821148) for details.</span></span>
> 
> 

<span data-ttu-id="8acd2-106">Antes de usar una red virtual de Azure con Azure RemoteApp, debe validar la red virtual.</span><span class="sxs-lookup"><span data-stu-id="8acd2-106">Before you use an Azure VNET with Azure RemoteApp, you might want to validate the VNET.</span></span> <span data-ttu-id="8acd2-107">Esto ayuda a evitar problemas con la conectividad.</span><span class="sxs-lookup"><span data-stu-id="8acd2-107">This helps prevent issues with connectivity.</span></span>

<span data-ttu-id="8acd2-108">Para validar la red virtual de Azure, haga lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="8acd2-108">To validate your Azure VNET, do the following:</span></span>

1. <span data-ttu-id="8acd2-109">Cree una máquina virtual de Azure dentro de la subred de la red virtual de Azure que quiere usar con Azure RemoteApp.</span><span class="sxs-lookup"><span data-stu-id="8acd2-109">Create an Azure virtual machine inside the subnet of the Azure VNET you want to use with Azure RemoteApp.</span></span>
2. <span data-ttu-id="8acd2-110">Conéctese a esa máquina virtual mediante la opción **Conectar** del portal de administración.</span><span class="sxs-lookup"><span data-stu-id="8acd2-110">Connect to that VM by using the **Connect** option in the management portal.</span></span>
3. <span data-ttu-id="8acd2-111">Conecte la máquina virtual al mismo dominio que desea usar con Azure RemoteApp.</span><span class="sxs-lookup"><span data-stu-id="8acd2-111">Join the virtual machine to the same domain that you want to use with Azure RemoteApp.</span></span> <span data-ttu-id="8acd2-112">Si está creando una colección híbrida que se conecta a la red local, una la máquina virtual al dominio local.</span><span class="sxs-lookup"><span data-stu-id="8acd2-112">If you are creating a hybrid collection that connects to your on-premises network, join the virtual machine to your local domain.</span></span>

<span data-ttu-id="8acd2-113">Si esto se realiza correctamente, la red virtual de Azure está lista para usarse con RemoteApp.</span><span class="sxs-lookup"><span data-stu-id="8acd2-113">If this is successful, the Azure VNET is ready to use with RemoteApp.</span></span>

<span data-ttu-id="8acd2-114">Para obtener más información sobre el flujo de trabajo completo de la colección híbrida, vea los siguientes artículos:</span><span class="sxs-lookup"><span data-stu-id="8acd2-114">For more information about the end-to-end hybrid collection workflow, see the following articles:</span></span>

* [<span data-ttu-id="8acd2-115">Planeación de la red virtual de Azure RemoteApp</span><span class="sxs-lookup"><span data-stu-id="8acd2-115">How to plan your virtual network for Azure RemoteApp</span></span>](remoteapp-planvnet.md)
* [<span data-ttu-id="8acd2-116">Creación de una colección híbrida</span><span class="sxs-lookup"><span data-stu-id="8acd2-116">Create a hybrid collection</span></span>](remoteapp-create-hybrid-deployment.md)
* [<span data-ttu-id="8acd2-117">Implementación de la colección Azure RemoteApp en la Red virtual de Azure (con compatibilidad para ExpressRoute)</span><span class="sxs-lookup"><span data-stu-id="8acd2-117">Deploy Azure RemoteApp collection to your Azure Virtual Network (with support for ExpressRoute)</span></span>](http://blogs.msdn.com/b/rds/archive/2015/04/23/deploy-azure-remoteapp-collection-to-your-azure-virtual-network-with-support-for-expressroute.aspx)

