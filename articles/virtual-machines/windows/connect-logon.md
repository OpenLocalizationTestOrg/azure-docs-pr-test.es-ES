---
title: "Conexión a una máquina virtual de Windows Server | Microsoft Docs"
description: "Aprenda a conectarse a una máquina virtual de Windows y a iniciar sesión en ella mediante el Portal de Azure y el modelo de implementación de Resource Manager."
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
ms.openlocfilehash: 88431377a36d5bc36220c630f0c8d4a46ab4a434
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-connect-and-log-on-to-an-azure-virtual-machine-running-windows"></a><span data-ttu-id="7d69e-103">Conexión a una máquina virtual de Azure donde se ejecuta Windows e inicio de sesión en ella</span><span class="sxs-lookup"><span data-stu-id="7d69e-103">How to connect and log on to an Azure virtual machine running Windows</span></span>
<span data-ttu-id="7d69e-104">Para iniciar una sesión de Escritorio remoto (RDP) desde un escritorio de Windows, usará el botón **Conectar** de Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="7d69e-104">You'll use the **Connect** button in the Azure portal to start a Remote Desktop (RDP) session from a Windows desktop.</span></span> <span data-ttu-id="7d69e-105">En primer lugar, conéctese a la máquina virtual y luego inicie sesión.</span><span class="sxs-lookup"><span data-stu-id="7d69e-105">First you connect to the virtual machine, then you log on.</span></span>

<span data-ttu-id="7d69e-106">Si intenta conectarse a una máquina virtual Windows desde un equipo Mac, debe instalar un cliente de RDP para Mac como [Escritorio remoto de Microsoft](https://itunes.apple.com/app/microsoft-remote-desktop/id715768417).</span><span class="sxs-lookup"><span data-stu-id="7d69e-106">If you are trying to connect to a Windows VM from a Mac, you need to install an RDP client for Mac like [Microsoft Remote Desktop](https://itunes.apple.com/app/microsoft-remote-desktop/id715768417).</span></span>

## <a name="connect-to-the-virtual-machine"></a><span data-ttu-id="7d69e-107">Conexión a la máquina virtual</span><span class="sxs-lookup"><span data-stu-id="7d69e-107">Connect to the virtual machine</span></span>
1. <span data-ttu-id="7d69e-108">Si aún no lo ha hecho, inicie sesión en el [Portal de Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="7d69e-108">If you haven't already done so, sign in to the [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="7d69e-109">En el menú Centro, haga clic en **Máquinas virtuales**.</span><span class="sxs-lookup"><span data-stu-id="7d69e-109">On the Hub menu, click **Virtual Machines**.</span></span>
3. <span data-ttu-id="7d69e-110">Seleccione la máquina virtual en la lista.</span><span class="sxs-lookup"><span data-stu-id="7d69e-110">Select the virtual machine from the list.</span></span>
4. <span data-ttu-id="7d69e-111">En la hoja de la máquina virtual, haga clic en **Conectar**.</span><span class="sxs-lookup"><span data-stu-id="7d69e-111">On the blade for the virtual machine, click **Connect**.</span></span>
   
    ![Captura de pantalla del Portal de Azure que muestra cómo conectarse a la máquina virtual.](./media/connect-logon/connect.png)
   
   > [!TIP]
   > <span data-ttu-id="7d69e-113">Si el botón **Conectar** del portal está atenuado y no está conectado a Azure a través de una conexión [Express Route](../../expressroute/expressroute-introduction.md) o [VPN de sitio a sitio](../../vpn-gateway/vpn-gateway-howto-site-to-site-resource-manager-portal.md), deberá crear y asignar a la máquina virtual una dirección IP pública antes de poder usar RDP.</span><span class="sxs-lookup"><span data-stu-id="7d69e-113">If the **Connect** button in the portal is greyed out and you are not connected to Azure via an [Express Route](../../expressroute/expressroute-introduction.md) or [Site-to-Site VPN](../../vpn-gateway/vpn-gateway-howto-site-to-site-resource-manager-portal.md) connection, you need to create and assign your VM a public IP address before you can use RDP.</span></span> <span data-ttu-id="7d69e-114">Aquí puede leer más sobre [direcciones IP públicas en Azure](../../virtual-network/virtual-network-ip-addresses-overview-arm.md).</span><span class="sxs-lookup"><span data-stu-id="7d69e-114">You can read more about [public IP addresses in Azure](../../virtual-network/virtual-network-ip-addresses-overview-arm.md).</span></span>
   > 
   > 

## <a name="log-on-to-the-virtual-machine"></a><span data-ttu-id="7d69e-115">Iniciar sesión en la nueva máquina virtual</span><span class="sxs-lookup"><span data-stu-id="7d69e-115">Log on to the virtual machine</span></span>
[!INCLUDE [virtual-machines-log-on-win-server](../../../includes/virtual-machines-log-on-win-server.md)]

## <a name="next-steps"></a><span data-ttu-id="7d69e-116">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="7d69e-116">Next steps</span></span>
<span data-ttu-id="7d69e-117">Si surgen problemas al intentar conectarse, consulte [Solución de problemas de conexiones del Escritorio remoto](troubleshoot-rdp-connection.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="7d69e-117">If you run into trouble when you try to connect, see [Troubleshoot Remote Desktop connections](troubleshoot-rdp-connection.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span> <span data-ttu-id="7d69e-118">En este artículo se le guiará a través del diagnóstico y la resolución de problemas comunes.</span><span class="sxs-lookup"><span data-stu-id="7d69e-118">This article walks you through diagnosing and resolving common problems.</span></span>

