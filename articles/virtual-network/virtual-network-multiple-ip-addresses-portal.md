---
title: "aaaMultiple las direcciones IP de máquinas virtuales de Azure: Portal | Documentos de Microsoft"
description: "Obtenga información acerca de cómo tooassign varias direcciones IP tooa máquina virtual usando Hola portal de Azure | Administrador de recursos."
services: virtual-network
documentationcenter: na
author: anavinahar
manager: narayan
editor: 
tags: azure-resource-manager
ms.assetid: 3a8cae97-3bed-430d-91b3-274696d91e34
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 11/30/2016
ms.author: annahar
ms.openlocfilehash: 34075766ac68c8de38c258a4d70e35881f28bb0b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="assign-multiple-ip-addresses-toovirtual-machines-using-hello-azure-portal"></a>Asignar varias máquinas de toovirtual de direcciones IP mediante Hola portal de Azure

>[!INCLUDE [virtual-network-multiple-ip-addresses-intro.md](../../includes/virtual-network-multiple-ip-addresses-intro.md)]
>
Este artículo explica cómo toocreate una máquina virtual (VM) a través de modelo de implementación de Azure Resource Manager de hello mediante Hola portal de Azure. No se puede asignar tooresources que se creó mediante el modelo de implementación clásica de Hola a varias direcciones IP. más información acerca de los modelos de implementación de Azure, lea hello toolearn [comprender los modelos de implementación](../resource-manager-deployment-model.md) artículo.

[!INCLUDE [virtual-network-multiple-ip-addresses-template-scenario.md](../../includes/virtual-network-multiple-ip-addresses-scenario.md)]

## <a name = "create"></a>Creación de una máquina virtual con varias direcciones IP

Si desea toocreate una máquina virtual con varias direcciones IP o una dirección IP privada estática, debe crearlo mediante PowerShell o hello CLI de Azure. Haga clic en hello PowerShell u opciones de CLI en parte superior de Hola de este artículo toolearn cómo. Puede crear una máquina virtual con una única dirección IP privada dinámica y (opcionalmente) en una única dirección IP pública mediante el portal de hello siguiendo los pasos de Hola Hola [crear una VM de Windows](../virtual-machines/virtual-machines-windows-hero-tutorial.md) o [crear una VM Linux](../virtual-machines/linux/quick-create-portal.md) artículos. Después de crear Hola VM, puede cambiar el tipo de dirección IP de Hola de toostatic dinámica y agregar más direcciones IP mediante el portal de hello siguiendo los pasos en hello [tooa VM las direcciones IP agregar](#add) sección de este artículo.

## <a name="add"></a>Agregar tooa de direcciones IP virtual

Puede agregar pública y privada tooa de direcciones IP NIC siguiendo los pasos de Hola que siguen. Hello en los ejemplos de hello las secciones siguientes se suponen que ya tiene una máquina virtual con configuraciones de IP de hello tres descritas en hello [escenario](#Scenario) en este artículo, pero no es necesario que lo haga.

### <a name="coreadd"></a>Pasos principales

1. Examinar toohello portal de Azure en https://portal.azure.com e inicie sesión en él, si es necesario.
2. En el portal de hello, haga clic en **más servicios** > tipo *máquinas virtuales* en Hola cuadro Filtro y, a continuación, haga clic en **máquinas virtuales**.
3. Hola **máquinas virtuales** hoja, haga clic en hello VM desea tooadd IP direcciones a. Haga clic en **interfaces de red** de hoja de la máquina virtual de Hola que aparece y la red de hello, a continuación, seleccione interfaz va tooadd Hola IP direcciones a. En el ejemplo de Hola Hola después de la imagen, Hola NIC denominado *myNIC* de máquina virtual denominada hello *myVM* está seleccionado:

    ![Interfaz de red](./media/virtual-network-multiple-ip-addresses-portal/figure1.png)

4. En la hoja de Hola que aparece para hello NIC que se ha seleccionado, haga clic en **configuraciones IP**.

Hola completa los pasos de una de las secciones de Hola que van a continuación, en función de tipo hello de dirección IP desea tooadd.

### <a name="add-a-private-ip-address"></a>**Incorporación de una dirección IP privada**

Completar Hola siguiendo los pasos tooadd una nueva dirección IP privada:

1. Hola completa los pasos de hello [principales pasos](#coreadd) sección de este artículo.
2. Haga clic en **Agregar**. Hola **configuración IP agregar** hoja que aparece, cree una configuración de IP denominada *IPConfig 4* con *10.0.0.7* como un *estático* IP privada de direcciones, a continuación, haga clic en **Aceptar**.

    > [!NOTE]
    > Al agregar una dirección IP estática, debe especificar una dirección no utilizada, válida en Hola Hola de subred A que NIC está conectada. Si no está disponible la dirección de Hola que seleccione, portal de hello mostrará una X para la dirección IP de Hola y debe tooselect uno diferente.

3. Una vez que haga clic en Aceptar, se cerrará hoja hello y verá la nueva configuración de IP Hola enumerado. Haga clic en **Aceptar** tooclose hello **configuración IP agregar** hoja.
4. Puede hacer clic en **agregar** tooadd configuraciones de IP adicionales, o cierre todas las abiertas las direcciones IP toofinish agregar hojas.
5. Sistema operativo de la VM de toohello las direcciones IP privada de agregar Hola siguiendo los pasos de hello para el sistema operativo en hello [sistema operativo de la VM de tooa las direcciones IP agregar](#os-config) sección de este artículo.

### <a name="add-a-public-ip-address"></a>Incorporación de una dirección IP pública

Se agrega una dirección IP pública asociando un tooeither de recurso de dirección IP pública de una nueva configuración de IP o una configuración de IP existente.

> [!NOTE]
> Las direcciones IP públicas tienen un precio simbólico. toolearn más información acerca de la IP direcciones sobre los precios, leer hello [precios de dirección IP](https://azure.microsoft.com/pricing/details/ip-addresses) página. Hay un toohello limitar el número de direcciones IP públicas que puede usarse en una suscripción. toolearn más acerca de los límites de hello, leer hello [Azure tiene una limitación](../azure-subscription-service-limits.md#networking-limits) artículo.
> 

### <a name="create-public-ip"></a>Creación de un recurso de dirección IP pública

Una dirección IP pública es una configuración para un recurso de dirección IP pública. Si tiene un recurso de dirección IP público que no está asociada actualmente tooan configuración de IP que desea tooassociate tooan la configuración de IP, omitir Hola siguiendo los pasos y complete los pasos de hello en una de las secciones de Hola que siguen, como sea necesario. Si no tiene un recurso de dirección IP público disponible, complete Hola siguiendo los pasos toocreate uno:

1. Examinar toohello portal de Azure en https://portal.azure.com e inicie sesión en él, si es necesario.
3. En el portal de hello, haga clic en **New** > **red** > **dirección IP pública**.
4. Hola **Crear dirección IP pública** hoja que aparece, escriba un **nombre**, seleccione un **asignación de direcciones IP** tipo, un **suscripción**, **Grupo de recursos**y un **ubicación**, a continuación, haga clic en **crear**, tal y como se muestra en hello después de imagen:

    ![Creación de un recurso de dirección IP pública](./media/virtual-network-multiple-ip-addresses-portal/figure5.png)

5. Hola completa los pasos en una de las secciones de Hola que siguen tooassociate Hola pública recursos tooan IP configuración de dirección IP.

#### <a name="associate-hello-public-ip-address-resource-tooa-new-ip-configuration"></a>Asociar Hola pública recursos tooa nueva IP configuración de dirección IP

1. Hola completa los pasos de hello [principales pasos](#coreadd) sección de este artículo.
2. Haga clic en **Agregar**. Hola **configuración IP agregar** hoja que aparece, cree una configuración de IP denominada *IPConfig 4*. Habilitar hello **dirección IP pública** y seleccione un existente, que está disponible público recurso de dirección IP de hello **Elegir dirección IP pública** hoja que aparece.

    Una vez que haya seleccionado el recurso de dirección IP público hello, haga clic en **Aceptar** y hoja de Hola se cerrará. Si no tiene una dirección IP pública existente, puede crear una siguiendo los pasos de Hola Hola [crear un recurso de dirección IP público](#create-public-ip) sección de este artículo. 

3. Revisión Hola nueva configuración de IP. Aunque no se ha asignado explícitamente una dirección IP privada, uno se asignó automáticamente toohello la configuración de IP, dado que todas las configuraciones de IP deben tener una dirección IP privada.
4. Puede hacer clic en **agregar** tooadd configuraciones de IP adicionales, o cierre todas las abiertas las direcciones IP toofinish agregar hojas.
5. Agregar: sistema operativo de la VM de hello privado IP dirección toohello siguiendo los pasos de hello para el sistema operativo en hello [sistema operativo de la VM de tooa las direcciones IP agregar](#os-config) sección de este artículo. No agregue el sistema de operativo para toohello el público dirección IP Hola.

#### <a name="associate-hello-public-ip-address-resource-tooan-existing-ip-configuration"></a>Asociar Hola pública recursos tooan existente IP configuración de dirección IP

1. Hola completa los pasos de hello [principales pasos](#coreadd) sección de este artículo.
2. Haga clic en configuración de IP de hello a que desea que el recurso de dirección IP pública de tooadd de Hola.
3. En la hoja de IPConfig Hola que aparece, haga clic en **dirección IP**.
4. Hola **Elegir dirección IP pública** hoja que aparece, seleccione una dirección IP pública.
5. Haga clic en **guardar** y hojas de Hola se cerrarán. Si no tiene una dirección IP pública existente, puede crear una siguiendo los pasos de Hola Hola [crear un recurso de dirección IP público](#create-public-ip) sección de este artículo.
3. Revisión Hola nueva configuración de IP.
4. Puede hacer clic en **agregar** tooadd configuraciones de IP adicionales, o cierre todas las abiertas las direcciones IP toofinish agregar hojas. No agregue el sistema de operativo para toohello el público dirección IP Hola.


[!INCLUDE [virtual-network-multiple-ip-addresses-os-config.md](../../includes/virtual-network-multiple-ip-addresses-os-config.md)]
