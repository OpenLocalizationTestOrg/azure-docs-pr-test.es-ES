---
title: "aaaLog en tooa VM de Azure clásico | Documentos de Microsoft"
description: "Usar hello toolog de portal de Azure en la máquina virtual de tooa Windows creada con el modelo de implementación clásica de Hola."
services: virtual-machines-windows
documentationcenter: 
author: cynthn
manager: timlt
editor: tysonn
tags: azure-service-management
ms.assetid: 3c1239ed-07dc-48b8-8b3d-dc8c5f0ab20e
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 05/30/2017
ms.author: cynthn
ms.openlocfilehash: 2e32b7036c2538e73b46580e0f5f8f4979e8a685
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="log-on-tooa-windows-virtual-machine-using-hello-azure-portal"></a>Inicie sesión en tooa máquina virtual de Windows con hello portal de Azure
Hola portal de Azure, use hello **conectar** botón toostart una sesión de escritorio remoto y tooa VM de Windows de inicio de sesión.

¿Desea tooconnect tooa VM de Linux? Vea [cómo toolog en la máquina virtual de tooa ejecutan Linux](../../linux/mac-create-ssh-keys.md).

<!--
Deleting, but not 100% sure
Learn how too[perform these steps using new Azure portal](../connect-logon.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).
-->

> [!IMPORTANT]
> Azure tiene dos modelos de implementación diferentes para crear recursos y trabajar con ellos: [Resource Manager y el clásico](../../../resource-manager-deployment-model.md). Este artículo tratan con modelo de implementación de hello clásico. Microsoft recomienda que más nuevas implementaciones de usar el modelo del Administrador de recursos de Hola. Para obtener información acerca de cómo toolog sobre el uso de la máquina virtual de tooa Hola Administrador de recursos del modelo, vea [aquí](../connect-logon.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).

## <a name="connect-toohello-virtual-machine"></a>Conectar máquina virtual de toohello
1. Inicie sesión en toohello portal de Azure.
2. Haga clic en la máquina virtual de Hola que desea tooaccess. Hola nombre aparece en hello **todos los recursos** panel.

    ![Virtual-machine-locations](./media/connect-logon/azureportaldashboard.png)

3. Haga clic en **conectar** en la barra de comandos de hello encima del panel de la máquina virtual de Hola.

    ![Icono de la máquina virtual de hello Connect](./media/connect-logon/virtualmachine_dashboard_connect.png)

<!-- Don't know if this still applies
     I think we can zap this.
> [!TIP]
> If hello **Connect** button isn't available, see hello troubleshooting tips at hello end of this article.
>
>
-->

## <a name="log-on-toohello-virtual-machine"></a>Inicie sesión en la máquina virtual de toohello
[!INCLUDE [virtual-machines-log-on-win-server](../../../../includes/virtual-machines-log-on-win-server.md)]

## <a name="next-steps"></a>Pasos siguientes
* Si hello **conectar** botón está inactivo o tiene otros problemas con conexión a Escritorio remoto hello, pruebe a restablecer la configuración de Hola. Haga clic en **restablecer el acceso remoto** desde el panel de la máquina virtual de Hola.

    ![Reset-remote-access](./media/connect-logon/virtualmachine_dashboard_reset_remote_access.png)

* Si experimenta problemas con la contraseña, intente restablecerla. Haga clic en **de restablecimiento de contraseña** a lo largo de hello borde izquierdo del panel de la máquina virtual, en **soporte técnico y solución de problemas**.

    ![Reset-password](./media/connect-logon/virtualmachine_dashboard_reset_password.png)

Si las sugerencias no funcionan o no son lo que necesita, consulte [tooa de conexiones de escritorio remoto solucionar problemas de máquina Virtual de Azure basado en Windows](../troubleshoot-rdp-connection.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json). En este artículo se le guiará a través del diagnóstico y la resolución de problemas comunes.
