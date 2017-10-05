---
title: "Varias direcciones IP para máquinas virtuales de Azure: Portal | Microsoft Docs"
description: "Obtenga información sobre cómo asignar varias direcciones IP a una máquina virtual con Azure Portal | Resource Manager."
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
ms.openlocfilehash: d264bd47d76db8015a64f09248c57c94572e2693
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="assign-multiple-ip-addresses-to-virtual-machines-using-the-azure-portal"></a>Asignación de varias direcciones IP a máquinas virtuales con Azure Portal

>[!INCLUDE [virtual-network-multiple-ip-addresses-intro.md](../../includes/virtual-network-multiple-ip-addresses-intro.md)]
>
En este artículo se describe cómo crear una máquina virtual con el modelo de implementación de Azure Resource Manager mediante Azure Portal. No se pueden asignar varias direcciones IP a los recursos creados mediante el modelo de implementación clásica. Para información acerca de los modelos de implementación de Azure, lea el artículo [Understand deployment models](../resource-manager-deployment-model.md) (Descripción de los modelos de implementación).

[!INCLUDE [virtual-network-multiple-ip-addresses-template-scenario.md](../../includes/virtual-network-multiple-ip-addresses-scenario.md)]

## <a name = "create"></a>Creación de una máquina virtual con varias direcciones IP

Si desea crear una máquina virtual con varias direcciones IP, o una privada estática, debe crearla mediante PowerShell o la CLI de Azure. Para aprender cómo, haga clic en las opciones PowerShell o CLI en la parte superior de este artículo. Puede crear una máquina virtual con una sola dirección IP privada dinámica y (opcionalmente) una única dirección IP pública mediante el portal siguiendo los pasos descritos en los artículos [Creación de la primera máquina virtual de Windows en Azure Portal](../virtual-machines/virtual-machines-windows-hero-tutorial.md) o [Creación de una máquina virtual de Linux en Azure mediante el portal](../virtual-machines/linux/quick-create-portal.md). Después de crear la máquina virtual, puede cambiar los tipos de direcciones IP de dinámicas a estáticas y agregar más mediante el portal siguiendo los pasos de la sección [Incorporación de direcciones IP a una VM](#add) de este artículo.

## <a name="add"></a>Incorporación de direcciones IP a una VM

Puede agregar direcciones IP públicas y privadas a una NIC completando los pasos siguientes. En los ejemplos de las secciones siguientes se da por sentado que ya tiene una máquina virtual con las tres configuraciones de IP descritas en el [escenario](#Scenario) de este artículo, pero no es necesario que lo haga.

### <a name="coreadd"></a>Pasos principales

1. Vaya Azure Portal en https://portal.azure.com e inicie sesión en él, si es necesario.
2. En el portal, haga clic en **Más servicios** > tipo *Máquinas virtuales* en el cuadro de filtro y luego haga clic en **Máquinas virtuales**.
3. En la hoja **Máquinas virtuales**, haga clic en la VM a la que desea agregar direcciones IP. Haga clic en **Interfaces de red** en la hoja de la máquina virtual que aparece y luego seleccione la interfaz de red a la que desea agregar direcciones IP. En el ejemplo mostrado en la siguiente imagen, está seleccionada la NIC denominada *myNIC* de la VM llamada *myVM*:

    ![Interfaz de red](./media/virtual-network-multiple-ip-addresses-portal/figure1.png)

4. En la hoja que aparece para la NIC que ha seleccionado, haga clic en **Configuraciones de IP**.

Complete los pasos de una de las secciones siguientes según el tipo de dirección IP que desea agregar.

### <a name="add-a-private-ip-address"></a>**Incorporación de una dirección IP privada**

Complete los pasos siguientes para agregar una nueva dirección IP privada:

1. Complete los pasos de la sección [Pasos principales](#coreadd) de este artículo.
2. Haga clic en **Agregar**. En la hoja **Agregar configuración de IP** que aparece, cree una configuración de IP denominada *IPConfig 4* con *10.0.0.7* como una dirección IP privada de tipo *Estática* y luego haga clic en **Aceptar**.

    > [!NOTE]
    > Al agregar una dirección IP estática, debe especificar una dirección válida no utilizada en la subred a la que la está conectada la NIC. Si la dirección que seleccionó no está disponible, el portal mostrará una X para la dirección IP y deberá seleccionar otra.

3. Una vez que haga clic en Aceptar, se cerrará la hoja y verá la nueva configuración de IP en la lista. Haga clic en **Aceptar** para cerrar la hoja **Agregar configuración de IP**.
4. Puede hacer clic en **Agregar** agregue más configuraciones IP o cerrar todas las hojas abiertas para terminar de agregar direcciones IP.
5. Agregue al sistema operativo de la VM las direcciones IP privadas completando los pasos correspondientes al sistema operativo de la sección [Incorporación de direcciones IP a un sistema operativo de la VM](#os-config) de este artículo.

### <a name="add-a-public-ip-address"></a>Incorporación de una dirección IP pública

Una dirección IP pública se agrega mediante la asociación de un recurso de dirección IP pública a una nueva configuración de IP o una configuración de IP existente.

> [!NOTE]
> Las direcciones IP públicas tienen un precio simbólico. Para más información sobre los precios de las direcciones IP, lea la página [Precios de las direcciones IP](https://azure.microsoft.com/pricing/details/ip-addresses) . Existe un límite para el número de direcciones IP públicas que pueden usarse dentro de una suscripción. Para más información sobre los límites, lea el artículo sobre los [límites de Azure](../azure-subscription-service-limits.md#networking-limits).
> 

### <a name="create-public-ip"></a>Creación de un recurso de dirección IP pública

Una dirección IP pública es una configuración para un recurso de dirección IP pública. Si tiene un recurso de dirección IP pública que no está asociado actualmente a una configuración de IP que desea asociar a una configuración de IP, omita los pasos siguientes y complete los pasos de una de las secciones siguientes, según sea preciso. Si no tiene un recurso de dirección IP pública disponible, complete los pasos siguientes para crear uno:

1. Vaya Azure Portal en https://portal.azure.com e inicie sesión en él, si es necesario.
3. En el portal, haga clic en **Nuevo** > **Redes** > **Dirección IP pública**.
4. En la hoja **Crear dirección IP pública** que aparece, escriba un nombre en **Nombre**, seleccione un tipo en **Asignación de dirección IP**, una suscripción en **Suscripción**, un grupo de recursos sen **Grupo de recursos** y una ubicación en **Ubicación**. Luego, haga clic en **Crear** tal y como se muestra en la siguiente imagen:

    ![Creación de un recurso de dirección IP pública](./media/virtual-network-multiple-ip-addresses-portal/figure5.png)

5. Complete los pasos de una de las secciones siguientes para asociar el recurso de dirección IP pública a una configuración de IP.

#### <a name="associate-the-public-ip-address-resource-to-a-new-ip-configuration"></a>Asociación del recurso de dirección IP pública a una nueva configuración de IP

1. Complete los pasos de la sección [Pasos principales](#coreadd) de este artículo.
2. Haga clic en **Agregar**. En la hoja **Agregar configuración de IP** hoja que aparece, cree una configuración de IP denominada *IPConfig 4*. Habilite la opción **Dirección IP pública** y seleccione un recurso de dirección IP pública existente que esté disponible en la hoja **Elegir dirección IP pública** que aparece.

    Una vez que haya seleccionado la dirección IP pública, haga clic en **Aceptar** y la hoja se cerrará. Si no tiene una dirección IP pública existente, puede crear una completando los pasos descritos en la sección [Creación de un recurso de dirección IP pública](#create-public-ip) de este artículo. 

3. Revise la nueva configuración de IP. Aunque no se asignara explícitamente una dirección IP privada, se asigna una automáticamente a la configuración de IP, dado que todas las configuraciones IP deben tener una dirección IP privada.
4. Puede hacer clic en **Agregar** agregue más configuraciones IP o cerrar todas las hojas abiertas para terminar de agregar direcciones IP.
5. Agregue al sistema operativo de la VM la dirección IP privada completando los pasos de la sección [Incorporación de direcciones IP a un sistema operativo de la VM](#os-config) de este artículo. No agregue la dirección IP pública al sistema operativo.

#### <a name="associate-the-public-ip-address-resource-to-an-existing-ip-configuration"></a>Asociación del recurso de dirección IP pública a una configuración de IP existente

1. Complete los pasos de la sección [Pasos principales](#coreadd) de este artículo.
2. Haga clic en la configuración de IP a la que desee asociar el recurso de dirección IP pública.
3. En la hoja de configuración de IP que aparece, haga clic en **Dirección IP**.
4. Haga clic en la hoja**Elegir dirección IP pública** que aparece y seleccione una dirección IP pública.
5. Haga clic en **Guardar** y las hojas se cerrarán. Si no tiene una dirección IP pública existente, puede crear una completando los pasos descritos en la sección [Creación de un recurso de dirección IP pública](#create-public-ip) de este artículo.
3. Revise la nueva configuración de IP.
4. Puede hacer clic en **Agregar** agregue más configuraciones IP o cerrar todas las hojas abiertas para terminar de agregar direcciones IP. No agregue la dirección IP pública al sistema operativo.


[!INCLUDE [virtual-network-multiple-ip-addresses-os-config.md](../../includes/virtual-network-multiple-ip-addresses-os-config.md)]
