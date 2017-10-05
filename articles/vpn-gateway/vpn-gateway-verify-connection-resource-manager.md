---
title: "Verificación de una conexión de VPN Gateway | Microsoft Docs"
description: "En este artículo se explica cómo verificar una conexión de VPN Gateway de red virtual."
services: vpn-gateway
documentationcenter: na
author: cherylmc
manager: timlt
editor: 
tags: azure-service-management,azure-resource-manager
ms.assetid: 7e3d1043-caa9-4472-96d3-832f4e2c91ee
ms.service: vpn-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 05/16/2017
ms.author: cherylmc
ms.openlocfilehash: b2d702ecdd5e1fca342e7c84c6e75339097f0bcd
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="verify-a-vpn-gateway-connection"></a><span data-ttu-id="0eb0f-103">Verificación de una conexión de VPN Gateway</span><span class="sxs-lookup"><span data-stu-id="0eb0f-103">Verify a VPN Gateway connection</span></span>

<span data-ttu-id="0eb0f-104">En este artículo se muestra cómo comprobar una conexión de puerta de enlace de VPN para los modelos de implementación clásico y de Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="0eb0f-104">This article shows you how to verify a VPN gateway connection for both the classic and Resource Manager deployment models.</span></span>

## <a name="azure-portal"></a><span data-ttu-id="0eb0f-105">Portal de Azure</span><span class="sxs-lookup"><span data-stu-id="0eb0f-105">Azure portal</span></span>

[!INCLUDE [Azure portal](../../includes/vpn-gateway-verify-connection-portal-rm-include.md)]

## <a name="powershell"></a><span data-ttu-id="0eb0f-106">PowerShell</span><span class="sxs-lookup"><span data-stu-id="0eb0f-106">PowerShell</span></span>

<span data-ttu-id="0eb0f-107">Para comprobar el modelo de implementación de Resource Manager usado en una conexión de puerta de enlace de VPN con PowerShell, instale la versión más reciente de los [cmdlets de PowerShell de Azure Resource Manager](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="0eb0f-107">To verify a VPN gateway connection for the Resource Manager deployment model using PowerShell, install the latest version of the [Azure Resource Manager PowerShell cmdlets](/powershell/azure/overview).</span></span>

[!INCLUDE [PowerShell](../../includes/vpn-gateway-verify-connection-ps-rm-include.md)]

## <a name="azure-cli"></a><span data-ttu-id="0eb0f-108">CLI de Azure</span><span class="sxs-lookup"><span data-stu-id="0eb0f-108">Azure CLI</span></span>

<span data-ttu-id="0eb0f-109">Para comprobar el modelo de implementación de Resource Manager usado en una conexión de puerta de enlace de VPN con la CLI de Azure, instale la versión más reciente de los [comandos de CLI](https://docs.microsoft.com/cli/azure/install-azure-cli) (2.0 o posterior).</span><span class="sxs-lookup"><span data-stu-id="0eb0f-109">To verify a VPN gateway connection for the Resource Manager deployment model using Azure CLI, install the latest version of the [CLI commands](https://docs.microsoft.com/cli/azure/install-azure-cli) (2.0 or later).</span></span>

[!INCLUDE [CLI](../../includes/vpn-gateway-verify-connection-cli-rm-include.md)]


## <a name="azure-portal-classic"></a><span data-ttu-id="0eb0f-110">Azure Portal (clásico)</span><span class="sxs-lookup"><span data-stu-id="0eb0f-110">Azure portal (classic)</span></span>

[!INCLUDE [Azure portal](../../includes/vpn-gateway-verify-connection-azureportal-classic-include.md)]

## <a name="powershell-classic"></a><span data-ttu-id="0eb0f-111">PowerShell (clásico)</span><span class="sxs-lookup"><span data-stu-id="0eb0f-111">PowerShell (classic)</span></span>

<span data-ttu-id="0eb0f-112">Para comprobar el modelo de implementación clásico usado en la conexión de puerta de enlace de VPN con PowerShell, instale las versiones más reciente de los cmdlets de Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="0eb0f-112">To verify your VPN gateway connection for the classic deployment model using PowerShell, install the latest versions of the Azure PowerShell cmdlets.</span></span> <span data-ttu-id="0eb0f-113">Asegúrese de descargar e instalar el módulo de [Service Management](https://docs.microsoft.com/powershell/azure/install-azure-ps?view=azuresmps-3.7.0).</span><span class="sxs-lookup"><span data-stu-id="0eb0f-113">Be sure to download and install the [Service Management](https://docs.microsoft.com/powershell/azure/install-azure-ps?view=azuresmps-3.7.0) module.</span></span> <span data-ttu-id="0eb0f-114">Use "Add-AzureAccount" para iniciar sesión en el modelo de implementación clásica.</span><span class="sxs-lookup"><span data-stu-id="0eb0f-114">Use 'Add-AzureAccount' to log in to the classic deployment model.</span></span>

[!INCLUDE [Classic PowerShell](../../includes/vpn-gateway-verify-connection-ps-classic-include.md)]

## <a name="next-steps"></a><span data-ttu-id="0eb0f-115">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="0eb0f-115">Next steps</span></span>

* <span data-ttu-id="0eb0f-116">Puede agregar máquinas virtuales a las redes virtuales.</span><span class="sxs-lookup"><span data-stu-id="0eb0f-116">You can add virtual machines to your virtual networks.</span></span> <span data-ttu-id="0eb0f-117">Consulte [Creación de una máquina virtual que ejecuta Windows en Azure Portal](../virtual-machines/virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) para ver los pasos.</span><span class="sxs-lookup"><span data-stu-id="0eb0f-117">See [Create a Virtual Machine](../virtual-machines/virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) for steps.</span></span>