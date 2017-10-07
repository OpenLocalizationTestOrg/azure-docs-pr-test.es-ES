---
title: "aaaVerify una conexión de puerta de enlace VPN | Documentos de Microsoft"
description: "Este artículo muestra cómo tooverify un virtual red conexión de puerta de enlace VPN."
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
ms.openlocfilehash: 0d3da94a76b36251d629f82b1575328c7ac10b26
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="verify-a-vpn-gateway-connection"></a><span data-ttu-id="60b72-103">Verificación de una conexión de VPN Gateway</span><span class="sxs-lookup"><span data-stu-id="60b72-103">Verify a VPN Gateway connection</span></span>

<span data-ttu-id="60b72-104">Este artículo muestra cómo tooverify una conexión de puerta de enlace VPN para hello clásico y modelos de implementación del Administrador de recursos.</span><span class="sxs-lookup"><span data-stu-id="60b72-104">This article shows you how tooverify a VPN gateway connection for both hello classic and Resource Manager deployment models.</span></span>

## <a name="azure-portal"></a><span data-ttu-id="60b72-105">Azure Portal</span><span class="sxs-lookup"><span data-stu-id="60b72-105">Azure portal</span></span>

[!INCLUDE [Azure portal](../../includes/vpn-gateway-verify-connection-portal-rm-include.md)]

## <a name="powershell"></a><span data-ttu-id="60b72-106">PowerShell</span><span class="sxs-lookup"><span data-stu-id="60b72-106">PowerShell</span></span>

<span data-ttu-id="60b72-107">tooverify una conexión de puerta de enlace VPN para hello implementación del Administrador de recursos del modelo de uso de PowerShell, instale Hola la versión más reciente del programa Hola a [cmdlets de PowerShell del Administrador de recursos de Azure](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="60b72-107">tooverify a VPN gateway connection for hello Resource Manager deployment model using PowerShell, install hello latest version of hello [Azure Resource Manager PowerShell cmdlets](/powershell/azure/overview).</span></span>

[!INCLUDE [PowerShell](../../includes/vpn-gateway-verify-connection-ps-rm-include.md)]

## <a name="azure-cli"></a><span data-ttu-id="60b72-108">CLI de Azure</span><span class="sxs-lookup"><span data-stu-id="60b72-108">Azure CLI</span></span>

<span data-ttu-id="60b72-109">tooverify una conexión de puerta de enlace VPN para hello implementación del Administrador de recursos del modelo mediante la CLI de Azure, instale Hola la versión más reciente del programa Hola a [comandos de CLI](https://docs.microsoft.com/cli/azure/install-azure-cli) (2.0 o posterior).</span><span class="sxs-lookup"><span data-stu-id="60b72-109">tooverify a VPN gateway connection for hello Resource Manager deployment model using Azure CLI, install hello latest version of hello [CLI commands](https://docs.microsoft.com/cli/azure/install-azure-cli) (2.0 or later).</span></span>

[!INCLUDE [CLI](../../includes/vpn-gateway-verify-connection-cli-rm-include.md)]


## <a name="azure-portal-classic"></a><span data-ttu-id="60b72-110">Azure Portal (clásico)</span><span class="sxs-lookup"><span data-stu-id="60b72-110">Azure portal (classic)</span></span>

[!INCLUDE [Azure portal](../../includes/vpn-gateway-verify-connection-azureportal-classic-include.md)]

## <a name="powershell-classic"></a><span data-ttu-id="60b72-111">PowerShell (clásico)</span><span class="sxs-lookup"><span data-stu-id="60b72-111">PowerShell (classic)</span></span>

<span data-ttu-id="60b72-112">tooverify su conexión de puerta de enlace VPN para la implementación clásica de hello modelar con PowerShell, instale las últimas versiones de Hola de hello cmdlets de PowerShell de Azure.</span><span class="sxs-lookup"><span data-stu-id="60b72-112">tooverify your VPN gateway connection for hello classic deployment model using PowerShell, install hello latest versions of hello Azure PowerShell cmdlets.</span></span> <span data-ttu-id="60b72-113">Estar seguro de hello toodownload e instale [administración de servicios](https://docs.microsoft.com/powershell/azure/install-azure-ps?view=azuresmps-3.7.0) módulo.</span><span class="sxs-lookup"><span data-stu-id="60b72-113">Be sure toodownload and install hello [Service Management](https://docs.microsoft.com/powershell/azure/install-azure-ps?view=azuresmps-3.7.0) module.</span></span> <span data-ttu-id="60b72-114">Use 'Add-AzureAccount' toolog de modelo de implementación clásica de toohello.</span><span class="sxs-lookup"><span data-stu-id="60b72-114">Use 'Add-AzureAccount' toolog in toohello classic deployment model.</span></span>

[!INCLUDE [Classic PowerShell](../../includes/vpn-gateway-verify-connection-ps-classic-include.md)]

## <a name="next-steps"></a><span data-ttu-id="60b72-115">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="60b72-115">Next steps</span></span>

* <span data-ttu-id="60b72-116">Puede agregar redes virtuales de máquinas virtuales tooyour.</span><span class="sxs-lookup"><span data-stu-id="60b72-116">You can add virtual machines tooyour virtual networks.</span></span> <span data-ttu-id="60b72-117">Consulte [Creación de una máquina virtual que ejecuta Windows en el Portal de Azure](../virtual-machines/virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) para ver los pasos.</span><span class="sxs-lookup"><span data-stu-id="60b72-117">See [Create a Virtual Machine](../virtual-machines/virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) for steps.</span></span>
