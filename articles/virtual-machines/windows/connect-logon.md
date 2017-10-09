---
title: aaaConnect tooa VM de Windows Server | Documentos de Microsoft
description: "Obtenga información acerca de cómo tooconnect y registro sobre el uso de la máquina virtual de Windows en la tooa hello Azure modelo de implementación de administrador de recursos de hello y portal."
services: virtual-machines-windows
documentationcenter: 
author: cynthn
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: ef62b02e-bf35-468d-b4c3-71b63fe7f409
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: get-started-article
ms.date: 03/01/2017
ms.author: cynthn
ms.openlocfilehash: dc397f435ef165ae5af09f1d037ad3d520bb7ac3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooconnect-and-log-on-tooan-azure-virtual-machine-running-windows"></a><span data-ttu-id="869ca-103">¿Cómo tooconnect y tooan virtual de Azure de inicio de sesión automático con Windows</span><span class="sxs-lookup"><span data-stu-id="869ca-103">How tooconnect and log on tooan Azure virtual machine running Windows</span></span>
<span data-ttu-id="869ca-104">Deberá usar hello **conectar** botón en hello Azure portal toostart una sesión de escritorio remoto (RDP) de un escritorio de Windows.</span><span class="sxs-lookup"><span data-stu-id="869ca-104">You'll use hello **Connect** button in hello Azure portal toostart a Remote Desktop (RDP) session from a Windows desktop.</span></span> <span data-ttu-id="869ca-105">Primero se conecta la máquina virtual de toohello, a continuación, inicie sesión.</span><span class="sxs-lookup"><span data-stu-id="869ca-105">First you connect toohello virtual machine, then you log on.</span></span>

<span data-ttu-id="869ca-106">Si está tratando de tooconnect tooa VM de Windows desde un equipo Mac, debe tooinstall como un cliente RDP para Mac [Microsoft Remote Desktop](https://itunes.apple.com/app/microsoft-remote-desktop/id715768417).</span><span class="sxs-lookup"><span data-stu-id="869ca-106">If you are trying tooconnect tooa Windows VM from a Mac, you need tooinstall an RDP client for Mac like [Microsoft Remote Desktop](https://itunes.apple.com/app/microsoft-remote-desktop/id715768417).</span></span>

## <a name="connect-toohello-virtual-machine"></a><span data-ttu-id="869ca-107">Conectar máquina virtual de toohello</span><span class="sxs-lookup"><span data-stu-id="869ca-107">Connect toohello virtual machine</span></span>
1. <span data-ttu-id="869ca-108">Si aún no lo ha hecho, inicie sesión en toohello [portal de Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="869ca-108">If you haven't already done so, sign in toohello [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="869ca-109">En el menú del concentrador hello, haga clic en **máquinas virtuales**.</span><span class="sxs-lookup"><span data-stu-id="869ca-109">On hello Hub menu, click **Virtual Machines**.</span></span>
3. <span data-ttu-id="869ca-110">Seleccione la máquina virtual de Hola de lista de Hola.</span><span class="sxs-lookup"><span data-stu-id="869ca-110">Select hello virtual machine from hello list.</span></span>
4. <span data-ttu-id="869ca-111">En la hoja de hello para la máquina virtual de hello, haga clic en **conectar**.</span><span class="sxs-lookup"><span data-stu-id="869ca-111">On hello blade for hello virtual machine, click **Connect**.</span></span>
   
    ![Captura de pantalla de hello Azure portal que se muestra cómo tooconnect tooyour máquina virtual.](./media/connect-logon/connect.png)
   
   > [!TIP]
   > <span data-ttu-id="869ca-113">Si hello **conectar** botón en hello portal está atenuada y no está conectado tooAzure a través de un [Express Route](../../expressroute/expressroute-introduction.md) o [VPN de sitio a sitio](../../vpn-gateway/vpn-gateway-howto-site-to-site-resource-manager-portal.md) conexión, deberá toocreate y asignar la máquina virtual una dirección IP pública para poder usar RDP.</span><span class="sxs-lookup"><span data-stu-id="869ca-113">If hello **Connect** button in hello portal is greyed out and you are not connected tooAzure via an [Express Route](../../expressroute/expressroute-introduction.md) or [Site-to-Site VPN](../../vpn-gateway/vpn-gateway-howto-site-to-site-resource-manager-portal.md) connection, you need toocreate and assign your VM a public IP address before you can use RDP.</span></span> <span data-ttu-id="869ca-114">Aquí puede leer más sobre [direcciones IP públicas en Azure](../../virtual-network/virtual-network-ip-addresses-overview-arm.md).</span><span class="sxs-lookup"><span data-stu-id="869ca-114">You can read more about [public IP addresses in Azure](../../virtual-network/virtual-network-ip-addresses-overview-arm.md).</span></span>
   > 
   > 

## <a name="log-on-toohello-virtual-machine"></a><span data-ttu-id="869ca-115">Inicie sesión en la máquina virtual de toohello</span><span class="sxs-lookup"><span data-stu-id="869ca-115">Log on toohello virtual machine</span></span>
[!INCLUDE [virtual-machines-log-on-win-server](../../../includes/virtual-machines-log-on-win-server.md)]

## <a name="next-steps"></a><span data-ttu-id="869ca-116">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="869ca-116">Next steps</span></span>
<span data-ttu-id="869ca-117">Si experimenta problemas cuando intente tooconnect, consulte [las conexiones de escritorio remoto solucionar](troubleshoot-rdp-connection.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="869ca-117">If you run into trouble when you try tooconnect, see [Troubleshoot Remote Desktop connections](troubleshoot-rdp-connection.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span> <span data-ttu-id="869ca-118">En este artículo se le guiará a través del diagnóstico y la resolución de problemas comunes.</span><span class="sxs-lookup"><span data-stu-id="869ca-118">This article walks you through diagnosing and resolving common problems.</span></span>

