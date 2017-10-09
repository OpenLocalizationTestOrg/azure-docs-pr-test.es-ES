---
title: las directivas de laboratorio aaaManage en los laboratorios de desarrollo y pruebas de Azure | Documentos de Microsoft
description: "Obtenga información acerca de cómo tamaños de directivas de laboratorio toodefine como máquina virtual, máquinas virtuales máximas por usuario y la automatización de cierre."
services: devtest-lab,virtual-machines
documentationcenter: na
author: tomarcher
manager: douge
editor: 
ms.assetid: 7756aa64-49ca-45a0-9f90-0fd101c7be85
ms.service: devtest-lab
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/13/2017
ms.author: tarcher
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 351b3645a1fd729455884e5d177877c2986bd853
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="manage-all-policies-for-a-lab-in-azure-devtest-labs"></a>Administración de todas las directivas para un laboratorio de Azure DevTest Labs

Azure DevTest Labs le permite controlar los costos y desperdiciar lo mínimo posible en sus laboratorios gracias a la posibilidad de administrar políticas (configuración) en cada uno de ellos. Este artículo se explica detalladamente paso a paso cómo tooset cada directiva.  

## <a name="set-allowed-virtual-machine-sizes"></a>Establecimiento de tamaños de máquina virtual permitidos
Hello directiva para Hola de configuración permite tamaños de máquina virtual ayuda toominimize laboratorio residuos habilitando toospecify qué tamaños de máquina virtual se permiten en el laboratorio de Hola. Si se activa esta directiva, solo los tamaños de máquinas virtuales de esta lista pueden ser usado toocreate las máquinas virtuales.

1. En el laboratorio de hello **directivas y configuración** hoja, seleccione **permite tamaños de máquinas virtuales**.
   
    ![Allowed virtual machines sizes](./media/devtest-lab-set-lab-policy/allowed-vm-sizes.png)

1. Seleccione **en** tooenable esta directiva, y **desactivar** toodisable lo.

1. Si habilita esta directiva, seleccione uno o varios tamaños de máquina virtual que se pueden crear en el laboratorio.

1. Seleccione **Guardar**.

## <a name="set-virtual-machines-per-user"></a>Establecimiento de máquinas virtuales por usuario
Hola directiva para **máquinas virtuales por usuario** permite un número máximo de hello toospecify de máquinas virtuales que se pueden crear un usuario individual. Si un usuario intenta toocreate o notificación de una máquina virtual cuando se ha alcanzado el límite de usuarios de hello, un mensaje de error indica que Hola que VM no se puede que crear/presentado. 

1. En el laboratorio de hello **directivas y configuración** menú, seleccione **máquinas virtuales por usuario**.
   
    ![Máquinas virtuales por usuario](./media/devtest-lab-set-lab-policy/max-vms-per-user.png)

1. Seleccione **Sí** toolimit número de Hola de máquinas virtuales por usuario. Si no desea toolimit número de Hola de máquinas virtuales por usuario, seleccione **No**. Si selecciona **Sí**, especifique un valor numérico que indica el número máximo de Hola de máquinas virtuales que se puede crear o presentado por un usuario. 

1. Seleccione **Sí** número de hello toolimit de máquinas virtuales que puede usar SSD (disco de estado sólido). Si no desea toolimit número de Hola de máquinas virtuales que puede usar SSD, seleccione **No**. Si selecciona **Sí**, escriba un valor que indica el número máximo de Hola de máquinas virtuales que pueden crearse con SSD. 

1. Seleccione **Guardar**.

## <a name="set-virtual-machines-per-lab"></a>Establecimiento de máquinas virtuales por laboratorio
Hola directiva para **máquinas virtuales por laboratorio** permite un número máximo de hello toospecify de máquinas virtuales que se pueden crear para laboratorio actual de Hola. Si un usuario intenta toocreate una máquina virtual cuando se ha alcanzado el límite de laboratorio de hello, un mensaje de error indica que no se puede crear la máquina virtual de Hola. 

1. En el laboratorio de hello **directivas y configuración** menú, seleccione **máquinas virtuales por laboratorio**.
   
    ![Máquinas virtuales por laboratorio](./media/devtest-lab-set-lab-policy/max-vms-per-lab.png)

1. Seleccione **Sí** toolimit número de Hola de máquinas virtuales por laboratorio. Si no desea toolimit número de Hola de máquinas virtuales por laboratorio, seleccione **No**. Si selecciona **Sí**, especifique un valor numérico que indica el número máximo de Hola de máquinas virtuales que se puede crear o presentado por un usuario. 

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

## <a name="set-expiration-date"></a>Establecimiento de la fecha de expiración
Puede establecer una expiración de fecha cuando se [crear hello VM](devtest-lab-add-vm.md). En **configuración avanzada**, elija toospecify de icono de calendario Hola una fecha en la que Hola VM se eliminarán automáticamente.  De forma predeterminada, el Hola VM nunca expirará.

[!INCLUDE [devtest-lab-try-it-out](../../includes/devtest-lab-try-it-out.md)]

## <a name="next-steps"></a>Pasos siguientes
Una vez que haya definido y aplicado Hola distintas configuraciones de directiva de máquina virtual para el laboratorio, a continuación le presentamos algunas tootry cosas:

* [Comprender las direcciones IP compartidas](devtest-lab-shared-ip.md) -explica cómo compartido IP direcciones se utilizan en el número de laboratorios de desarrollo y pruebas toominimize Hola pública tooconnect requiere tooyour laboratorio máquinas virtuales de direcciones IP.
* [Configurar la administración de costos](devtest-lab-configure-cost-management.md) -ilustra cómo hello toouse **tendencia de costo mensual estimado** gráfico  
  tooview Hola estimado costo hasta la fecha del mes actual y el costo de fin de mes de hello proyectado.
* [Creación de una imagen personalizada](devtest-lab-create-template.md): cuando cree una máquina virtual, deberá especificar una base, que puede ser una imagen personalizada o una imagen de Marketplace. Este artículo explica cómo toocreate personalizado de la imagen desde un archivo de disco duro virtual.
* [Configuración de imágenes de Marketplace](devtest-lab-configure-marketplace-images.md): Azure DevTest Labs admite la creación de máquinas virtuales basadas en imágenes de Azure Marketplace. Este artículo se explica cómo toospecify que, si lo hay, imágenes de Azure Marketplace se pueden usar al crear máquinas virtuales en un laboratorio.
* [Crear una máquina virtual en un laboratorio](devtest-lab-add-vm-with-artifacts.md) -ilustra cómo toocreate una máquina virtual desde una imagen base (ya sea personalizado o Marketplace) y cómo toowork con los artefactos en la máquina virtual.

