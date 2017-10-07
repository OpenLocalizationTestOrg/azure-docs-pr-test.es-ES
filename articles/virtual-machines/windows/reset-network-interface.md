---
title: "interfaz de red aaaHow tooreset para máquina virtual de Windows Azure | Documentos de Microsoft"
description: "Muestra cómo tooreset interfaz de red de VM en Windows Azure"
services: virtual-machines-windows, azure-resource-manager
documentationcenter: 
author: genlin
manager: willchen
editor: 
tags: top-support-issue, azure-resource-manager
ms.service: virtual-machines-windows
ms.workload: na
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 06/26/2017
ms.author: genli
ms.openlocfilehash: 1b653820927ef4c3bb8f384a7e752846a8be3da9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooreset-network-interface-for-azure-windows-vm"></a>¿Cómo tooreset interfaz de red de VM en Windows Azure 

[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-both-include.md)]

No se puede conectar la máquina Virtual de Windows Azure (VM) de tooMicrosoft después de deshabilitar de forma predeterminada Hola de interfaz de red (NIC) o se establece manualmente una dirección IP estática para la NIC de Hola. Este artículo muestra cómo tooreset Hola interfaz de red de máquina virtual de Windows Azure, que se resolverá el problema de conexión remota de Hola.

[!INCLUDE [support-disclaimer](../../../includes/support-disclaimer.md)]
## <a name="reset-network-interface"></a>Restablecimiento de la interfaz de red

### <a name="for-classic-vms"></a>Para máquinas virtuales clásicas

red de tooreset de la interfaz, siga estos pasos:

1.  Vaya toohello [portal de Azure]( https://ms.portal.azure.com).
2.  Seleccione **Máquinas virtuales (clásico)**.
3.  Seleccione Hola había afectado Máquina Virtual.
4.  Seleccione **Direcciones IP**.
5.  Si hello **asignación de IP privada** no **estático**, también cambian**estático**.
6.  Hola de cambio **dirección IP** dirección IP de tooanother que está disponible en hello subred.
7.  Seleccione Guardar.
8.  máquina virtual de Hello reiniciará tooinitialize Hola nuevo NIC toohello sistema.
9.  Intente tooRDP tooyour máquina. Si se realiza correctamente, puede cambiar Hola original de toohello inversa de dirección de IP privada si lo desea. De lo contrario, manténgala. 

### <a name="for-vms-deployed-in-resource-group-model"></a>Para máquinas virtuales implementadas en el módulo de grupo de recursos

1.  Vaya toohello [portal de Azure]( https://ms.portal.azure.com).
2.  Seleccione Hola había afectado Máquina Virtual.
3.  Seleccione **Interfaces de red**.
4.  Seleccione Hola que asociado la interfaz de red con el equipo
5.  Seleccione **Configuraciones IP**.
6.  Seleccione IP Hola. 
7.  Si hello **asignación de IP privada** no **estático**, también cambian**estático**.
8.  Hola de cambio **dirección IP** dirección IP de tooanother que está disponible en hello subred.
9. máquina virtual de Hello reiniciará tooinitialize Hola nuevo NIC toohello sistema.
10. Intente tooRDP tooyour máquina. Si se realiza correctamente, puede cambiar Hola original de toohello inversa de dirección de IP privada si lo desea. De lo contrario, manténgala. 

## <a name="delete-hello-unavailable-nics"></a>Eliminar Hola NIC no está disponible
Después puede máquina toohello de escritorio remoto, debe eliminar Hola antigua NIC tooavoid Hola posible problema:

1.  Abra el Administrador de dispositivos.
2.  Seleccione **Vista** > **Mostrar dispositivos ocultos**.
3.  Seleccione **Adaptadores de red**. 
4.  Compruebe si los adaptadores de hello denominados como "Adaptador de red de Hyper-V de Microsoft".
5.  Puede que vea un adaptador no disponible atenuado. Haga clic en el adaptador de hello y, a continuación, seleccione Desinstalar.

    ![imagen de Hola de hello NIC](media/reset-network-interface/nicpage.png)

    > [!NOTE]
    > Solo la desinstalación de adaptadores disponibles Hola que tienen el nombre de Hola "Adaptador de red de Hyper-V de Microsoft". Si desinstala cualquiera de hello otros adaptadores ocultos, podrían producirse problemas adicionales.
    >
    >

6.  Ahora deben borrarse todos los adaptadores no disponibles del sistema.