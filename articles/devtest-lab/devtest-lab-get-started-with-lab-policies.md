---
title: "las directivas de laboratorio básico aaaManage en los laboratorios de desarrollo y pruebas de Azure | Documentos de Microsoft"
description: "Obtenga información acerca de cómo tooset algunos hello básico de directivas de (configuración) para un laboratorio de prácticas de desarrollo y pruebas"
services: devtest-lab,virtual-machines
documentationcenter: na
author: tomarcher
manager: douge
editor: 
ms.assetid: 
ms.service: devtest-lab
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/29/2017
ms.author: tarcher
ms.openlocfilehash: 792c0d19cfe73964be9c03d3de7751a868fd86e8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="manage-basic-policies-for-a-lab-in-azure-devtest-labs"></a>Administración de directivas básicas para un laboratorio de Azure DevTest Labs

Laboratorios de desarrollo y pruebas de Azure permite toocontrol costo y minimizar residuos en los laboratorios de mediante la administración de directivas (valores) para cada laboratorio. En este artículo, empezar a trabajar con las directivas de aprendizaje cómo tooset dos directivas más importantes de hello - limitar Hola número de máquinas virtuales (VM) que se puede crear o presentadas por un usuario individual y configurar apagado automático. tooview cómo tooset todas las directivas de laboratorio, consulte el artículo de hello, [definir directivas de laboratorio en los laboratorios de desarrollo y pruebas de Azure](devtest-lab-set-lab-policy.md).  

## <a name="accessing-a-labs-policies-in-azure-devtest-labs"></a>Acceso a las directivas de laboratorio en Azure DevTest Labs
Hello siguientes pasos le guiarán configuración de directivas para un laboratorio de prácticas de desarrollo y pruebas de Azure:

directivas de hello tooview (y cambiar) para un laboratorio, siga estos pasos:

1. Inicie sesión en toohello [portal de Azure](http://go.microsoft.com/fwlink/p/?LinkID=525040).

1. Seleccione **más servicios**y, a continuación, seleccione **laboratorios de desarrollo y pruebas** de lista de Hola.

1. En lista de Hola de laboratorios, seleccione laboratorio deseado Hola.   

1. Seleccione **Configuration and policies** (Directivas y configuración).

    ![Hoja de configuración de directiva](./media/devtest-lab-set-lab-policy/policies-menu.png)

1. Hola **directivas y configuración** hoja contiene un menú de opciones que puede especificar. En este artículo se analizan sólo las opciones de Hola para **máquinas virtuales por usuario** y **apagado automático**. toolearn sobre Hola restantes de la configuración, consulte [administrar todas las directivas para un laboratorio de prácticas de desarrollo y pruebas de Azure](./devtest-lab-set-lab-policy.md). 
   
## <a name="set-virtual-machines-per-user"></a>Establecimiento de máquinas virtuales por usuario
Hola directiva para **máquinas virtuales por usuario** permite un número máximo de hello toospecify de máquinas virtuales que se pueden crear un usuario individual. Si un usuario intenta toocreate o notificación de una máquina virtual cuando se ha alcanzado el límite de usuarios de hello, un mensaje de error indica que Hola que VM no se puede que crear/presentado. 

1. En el laboratorio de hello **directivas y configuración** menú, seleccione **máquinas virtuales por usuario**.
   
    ![Máquinas virtuales por usuario](./media/devtest-lab-set-lab-policy/max-vms-per-user.png)

1. Seleccione **Sí** toolimit número de Hola de máquinas virtuales por usuario. Si no desea toolimit número de Hola de máquinas virtuales por usuario, seleccione **No**. Si selecciona **Sí**, especifique un valor numérico que indica el número máximo de Hola de máquinas virtuales que se puede crear o presentado por un usuario. 

1. Seleccione **Sí** número de hello toolimit de máquinas virtuales que puede usar SSD (disco de estado sólido). Si no desea toolimit número de Hola de máquinas virtuales que puede usar SSD, seleccione **No**. Si selecciona **Sí**, escriba un valor que indica el número máximo de Hola de máquinas virtuales que pueden crearse con SSD. 

1. Seleccione **Guardar**.

## <a name="set-auto-shutdown"></a>Establecimiento del apagado automático
Directiva de cierre automático de Hello ayuda toominimize laboratorio residuos permitiéndole tiempo de hello toospecify que apagar máquinas virtuales de este laboratorio.

1. En el laboratorio de hello **directivas y configuración** hoja, seleccione **apagado automático**.
   
    ![Apagado automático](./media/devtest-lab-set-lab-policy/auto-shutdown.png)

1. Seleccione **en** tooenable esta directiva, y **desactivar** toodisable lo.

1. Si habilita esta directiva, especifique hello tooshut hora (y zona horaria) hacia abajo de todas las máquinas virtuales en laboratorio actual Hola.

1. Especifique **Sí** o **n** para hello opción toosend un toohello antes de 15 minutos de notificación especificado tiempo de cierre automático. Si especifica **Sí**, escriba una notificación de hello webhook tooreceive de punto de conexión de dirección URL. Para obtener más información sobre los webhooks, consulte [Creación de un webhook o una función de API de Azure](../azure-functions/functions-create-a-web-hook-or-api-function.md). 

1. Seleccione **Guardar**.

    De forma predeterminada, una vez habilitada, esta directiva aplica a máquinas virtuales de tooall en laboratorio actual Hola. tooremove esta configuración de una máquina virtual específica, abra la máquina virtual de hello hoja y cambie su **apagado automático** configuración 

## <a name="set-auto-start"></a>Establecimiento del inicio automático
Directiva de inicio automático de Hello permite toospecify cuando se debe iniciar hello las máquinas virtuales en el laboratorio actual de Hola.  

1. En el laboratorio de hello **directivas y configuración** hoja, seleccione **inicio automático**.
   
    ![Inicio automático](./media/devtest-lab-set-lab-policy/auto-start.png)

2. Seleccione **en** tooenable esta directiva, y **desactivar** toodisable lo.

3. Si habilita esta directiva, especifique la hora de inicio programada de hello, zona horaria y Hola días de la semana de Hola para qué hello tiempo se aplica. 

4. Seleccione **Guardar**.

    Una vez habilitada, esta directiva no está tooany aplica automáticamente las máquinas virtuales en laboratorio actual Hola. tooapply este tooa configuración VM específica, la máquina virtual de hello Abrir hoja y cambie su **inicio automático** configuración 

## <a name="next-steps"></a>Pasos siguientes

- [Definir directivas de laboratorio en los laboratorios de desarrollo y pruebas de Azure](devtest-lab-set-lab-policy.md) -Obtenga información acerca de cómo toomodify otras directivas de laboratorio 
