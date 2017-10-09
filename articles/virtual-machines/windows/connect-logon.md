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
# <a name="how-tooconnect-and-log-on-tooan-azure-virtual-machine-running-windows"></a>¿Cómo tooconnect y tooan virtual de Azure de inicio de sesión automático con Windows
Deberá usar hello **conectar** botón en hello Azure portal toostart una sesión de escritorio remoto (RDP) de un escritorio de Windows. Primero se conecta la máquina virtual de toohello, a continuación, inicie sesión.

Si está tratando de tooconnect tooa VM de Windows desde un equipo Mac, debe tooinstall como un cliente RDP para Mac [Microsoft Remote Desktop](https://itunes.apple.com/app/microsoft-remote-desktop/id715768417).

## <a name="connect-toohello-virtual-machine"></a>Conectar máquina virtual de toohello
1. Si aún no lo ha hecho, inicie sesión en toohello [portal de Azure](https://portal.azure.com/).
2. En el menú del concentrador hello, haga clic en **máquinas virtuales**.
3. Seleccione la máquina virtual de Hola de lista de Hola.
4. En la hoja de hello para la máquina virtual de hello, haga clic en **conectar**.
   
    ![Captura de pantalla de hello Azure portal que se muestra cómo tooconnect tooyour máquina virtual.](./media/connect-logon/connect.png)
   
   > [!TIP]
   > Si hello **conectar** botón en hello portal está atenuada y no está conectado tooAzure a través de un [Express Route](../../expressroute/expressroute-introduction.md) o [VPN de sitio a sitio](../../vpn-gateway/vpn-gateway-howto-site-to-site-resource-manager-portal.md) conexión, deberá toocreate y asignar la máquina virtual una dirección IP pública para poder usar RDP. Aquí puede leer más sobre [direcciones IP públicas en Azure](../../virtual-network/virtual-network-ip-addresses-overview-arm.md).
   > 
   > 

## <a name="log-on-toohello-virtual-machine"></a>Inicie sesión en la máquina virtual de toohello
[!INCLUDE [virtual-machines-log-on-win-server](../../../includes/virtual-machines-log-on-win-server.md)]

## <a name="next-steps"></a>Pasos siguientes
Si experimenta problemas cuando intente tooconnect, consulte [las conexiones de escritorio remoto solucionar](troubleshoot-rdp-connection.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json). En este artículo se le guiará a través del diagnóstico y la resolución de problemas comunes.

