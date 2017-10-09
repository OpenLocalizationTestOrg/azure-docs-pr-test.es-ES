---
title: aaaConfigure una red virtual en los laboratorios de desarrollo y pruebas de Azure | Documentos de Microsoft
description: "Obtenga información acerca de cómo tooconfigure una red virtual existente y la subred y usarlos en una máquina virtual con los laboratorios de desarrollo y pruebas de Azure"
services: devtest-lab,virtual-machines
documentationcenter: na
author: tomarcher
manager: douge
editor: 
ms.assetid: 6cda99c2-b87e-4047-90a0-5df10d8e9e14
ms.service: devtest-lab
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/16/2017
ms.author: tarcher
ms.openlocfilehash: a11ce8315e3c540e44aeacc9c5ee3dde014d4621
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="configure-a-virtual-network-in-azure-devtest-labs"></a>Configuración de una red virtual en Azure DevTest Labs
Como se explica en el artículo de hello, [agregar una máquina virtual con el laboratorio de artefactos tooa](devtest-lab-add-vm-with-artifacts.md), cuando se crea una máquina virtual en un laboratorio, puede especificar una red virtual configurada. Un escenario para hacer esto es si necesita tooaccess los recursos de la red corporativa desde las máquinas virtuales mediante Hola red virtual que se configuró con VPN de sitio a sitio o ExpressRoute. Hello próximas secciones se muestran cómo tooadd la red virtual existente a la configuración de red Virtual de un laboratorio para que esté disponible toochoose al crear máquinas virtuales.

## <a name="configure-a-virtual-network-for-a-lab-using-hello-azure-portal"></a>Configurar una red virtual para un laboratorio mediante Hola portal de Azure
Hello pasos siguientes le guían a través de agregar una existente virtual red (subred) tooa laboratorio y, por lo que se puede utilizar al crear una máquina virtual en hello mismo laboratorio. 

1. Inicie sesión en toohello [portal de Azure](http://go.microsoft.com/fwlink/p/?LinkID=525040).
2. Seleccione **más servicios**y, a continuación, seleccione **laboratorios de desarrollo y pruebas** de lista de Hola.
3. En lista de Hola de laboratorios, seleccione laboratorio deseado Hola. 
4. En la hoja del laboratorio de hello, seleccione **configuración**.
5. En el laboratorio de hello **configuración** hoja, seleccione **redes virtuales**.
6. En hello **redes virtuales** hoja, verá una lista de redes virtuales configuradas para el laboratorio de hello actual, así como la red virtual de hello predeterminada que se crea para el laboratorio. 
7. Seleccione **+Agregar**.
   
    ![Agregar un laboratorio de tooyour de red virtual existente](./media/devtest-lab-configure-vnet/lab-settings-vnet-add.png)
8. En hello **red Virtual** hoja, seleccione **[red virtual seleccione]**.
   
    ![Selección de una red virtual existente](./media/devtest-lab-configure-vnet/lab-settings-vnets-vnet1.png)
9. En hello **red virtual de elegir** hoja, red virtual de hello seleccione deseado. hoja Hello muestra todas las redes virtuales Hola que están bajo Hola misma región en la suscripción Hola laboratorio Hola.  
10. Después de seleccionar una red virtual, se devuelven toohello **red Virtual** haga clic en la subred de hello en lista de hello en parte inferior de Hola de hoja de Hola.

    ![Lista de subredes](./media/devtest-lab-configure-vnet/lab-settings-vnets-vnet2.png)
    
    se muestra la hoja de la subred del laboratorio de Hola.

    ![Hoja de la subred de laboratorio](./media/devtest-lab-configure-vnet/lab-subnet.png)

11. Especifique un **nombre de subred de laboratorio**.
12. tooallow un toobe de subred utilizado en laboratorio creación de VM, seleccione **uso en la creación de máquinas virtuales**.
13. tooenable una [comparten la dirección IP pública](devtest-lab-shared-ip.md), seleccione **habilitar la IP pública compartida**.
14. Seleccione tooallow de direcciones IP públicas en una subred, **permiten la creación de IP pública**.
15. Hola **máquinas virtuales de máximo por usuario** , especifique Hola máximas máquinas virtuales por usuario para cada subred. Si quiere un número ilimitado de máquinas virtuales, deje este campo en blanco.
16. Seleccione **Aceptar** hoja de subred del laboratorio de tooclose Hola.
17. Seleccione **guardar** hoja de red Virtual de tooclose Hola.
18. Ahora que hello red virtual está configurada, se puede seleccionar al crear una máquina virtual. 
    toosee cómo toocreate una máquina virtual y especifique una red virtual, consulte el artículo toohello, [agregar una máquina virtual con el laboratorio de artefactos tooa](devtest-lab-add-vm-with-artifacts.md). 

[!INCLUDE [devtest-lab-try-it-out](../../includes/devtest-lab-try-it-out.md)]

## <a name="next-steps"></a>Pasos siguientes
Cuando haya agregado Hola deseado laboratorio tooyour de red virtual, paso siguiente hello es demasiado[agregar un laboratorio VM tooyour](devtest-lab-add-vm-with-artifacts.md).

