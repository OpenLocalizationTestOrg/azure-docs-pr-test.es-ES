---
title: "aaaConfigure de direcciones IP privadas para las máquinas virtuales: portal de Azure | Documentos de Microsoft"
description: "Obtenga información acerca de cómo tooconfigure de direcciones IP privadas de máquinas virtuales mediante Hola portal de Azure."
services: virtual-network
documentationcenter: na
author: jimdial
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 11245645-357d-4358-9a14-dd78e367b494
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/04/2016
ms.author: jdial
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 474161303cdf8cb98e16ffd7cef6b74debdbc49a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="configure-private-ip-addresses-for-a-virtual-machine-using-hello-azure-portal"></a>Configurar las direcciones IP privadas para una máquina virtual mediante Hola portal de Azure

> [!div class="op_single_selector"]
> * [Portal de Azure](virtual-networks-static-private-ip-arm-pportal.md)
> * [PowerShell](virtual-networks-static-private-ip-arm-ps.md)
> * [CLI de Azure](virtual-networks-static-private-ip-arm-cli.md)
> * [Portal de Azure (clásico)](virtual-networks-static-private-ip-classic-pportal.md)
> * [PowerShell (clásico)](virtual-networks-static-private-ip-classic-ps.md)
> * [CLI de Azure (clásico)](virtual-networks-static-private-ip-classic-cli.md)


[!INCLUDE [virtual-networks-static-private-ip-intro-include](../../includes/virtual-networks-static-private-ip-intro-include.md)]

[!INCLUDE [azure-arm-classic-important-include](../../includes/azure-arm-classic-important-include.md)]

Este artículo trata el modelo de implementación del Administrador de recursos de Hola. También puede [administrar dirección IP privada estática en el modelo de implementación clásica de hello](virtual-networks-static-private-ip-classic-pportal.md).

[!INCLUDE [virtual-networks-static-ip-scenario-include](../../includes/virtual-networks-static-ip-scenario-include.md)]

siguientes pasos de ejemplo de Hola esperan un entorno simple ya creado. Si desea toorun pasos de hello, que se muestran en este documento, en primer lugar crear entorno de prueba de Hola se describe en [crear una red virtual](virtual-networks-create-vnet-arm-pportal.md).

## <a name="how-toocreate-a-vm-for-testing-static-private-ip-addresses"></a>Cómo aborda toocreate una máquina virtual para la prueba de dirección IP estática privada
No se puede establecer una dirección IP privada estática durante la creación de hello de una máquina virtual en el modo de implementación del Administrador de recursos de hello mediante Hola portal de Azure. Primero deberá crear Hola VM, tehn establecer su privada toobe IP estática.

una máquina virtual denominada toocreate *DNS01* en hello *front-end* subred de una red virtual con el nombre *TestVNet*, siga estos pasos Hola.

1. Desde un explorador, navegue toohttp://portal.azure.com y, si es necesario, inicie sesión con su cuenta de Azure.
2. Haga clic en **NEW** > **proceso** > **Windows Server 2012 R2 Datacenter**, tenga en cuenta que hello **seleccionar un modelo de implementación** lista ya se muestran **el Administrador de recursos**y, a continuación, haga clic en **crear**, como se muestra en la siguiente ilustración de Hola.
   
    ![Creación de una VM en el Portal de Azure](./media/virtual-networks-static-ip-arm-pportal/figure01.png)
3. Hola **Fundamentos** hoja, escriba nombre Hola de hello VM toobe creado (*DNS01* en nuestro escenario), Hola cuenta de administrador local y la contraseña, como se muestra en la siguiente ilustración de Hola.
   
    ![Hoja Básico](./media/virtual-networks-static-ip-arm-pportal/figure02.png)
4. Realizar Hola seguro **ubicación** seleccionado es *Central US*, a continuación, haga clic en **seleccione existente** en **grupo de recursos**, a continuación, haga clic en **Grupo de recursos** , a continuación, haga clic en el nuevo, *TestRG*y, a continuación, haga clic en **Aceptar**.
   
    ![Hoja Básico](./media/virtual-networks-static-ip-arm-pportal/figure03.png)
5. Hola **elegir un tamaño de** hoja, seleccione **estándar A1**y, a continuación, haga clic en **seleccione**.
   
    ![Selección de una hoja de tamaño](./media/virtual-networks-static-ip-arm-pportal/figure04.png)    
6. En el **configuración** hoja, asegúrese de hello seguro propiedades siguientes se establecen se establecen con valores de hello siguiente y, a continuación, haga clic en **Aceptar**.
   
    -**Cuenta de almacenamiento**: *vnetstorage*
   
   * **Red**: *TestVNet*
   * **Subred**: *FrontEnd*
     
     ![Selección de una hoja de tamaño](./media/virtual-networks-static-ip-arm-pportal/figure05.png)     
7. Hola **resumen** hoja, haga clic en **Aceptar**. Aviso Hola mosaico siguientes aparecen en el panel.
   
    ![Creación de una VM en el Portal de Azure](./media/virtual-networks-static-ip-arm-pportal/figure06.png)

## <a name="how-tooretrieve-static-private-ip-address-information-for-a-vm"></a>¿Cómo tooretrieve dirección IP estática privada información de dirección de una máquina virtual
tooview Hola privada información direcciones IP estáticas para hello máquinas virtuales crean con hello los pasos descritos anteriormente, ejecute los pasos de Hola a continuación.

1. En el portal de Azure de Azure de hello, haga clic en **examinar todos los** > **máquinas virtuales** > **DNS01** > **todos configuración de** > **interfaces de red** y, a continuación, haga clic en hello única interfaz de red enumerado.
   
    ![Implementación del icono de máquina virtual](./media/virtual-networks-static-ip-arm-pportal/figure07.png)
2. Hola **interfaz de red** hoja, haga clic en **toda la configuración de** > **direcciones IP** aviso hello y **asignación** y **Dirección IP** valores.
   
    ![Implementación del icono de máquina virtual](./media/virtual-networks-static-ip-arm-pportal/figure08.png)

## <a name="how-tooadd-a-static-private-ip-address-tooan-existing-vm"></a>Cómo tooadd una dirección IP estática privada direccionan tooan existente de la máquina virtual
tooadd una toohello de dirección IP privada máquinas virtuales creadas mediante Hola pasos anteriores, estático, siga Hola pasos:

1. De hello **direcciones IP** hoja mostrado anteriormente, haga clic en **estático** en **asignación**.
2. Escriba *192.168.1.101* en **Dirección IP** y, después, haga clic en **Guardar**.
   
    ![Creación de una VM en el Portal de Azure](./media/virtual-networks-static-ip-arm-pportal/figure09.png)

> [!NOTE]
> Si después de hacer clic en **guardar** tenga en cuenta que la asignación de hello sigue establecida demasiado**dinámica**, significa que la dirección IP de Hola que escribió ya está en uso. Pruebe una dirección IP distinta.
> 
> 

## <a name="how-tooremove-a-static-private-ip-address-from-a-vm"></a>¿Cómo tooremove una privada de direcciones IP estáticas de una máquina virtual
tooremove Hola privada dirección IP estática de hello máquina virtual creada anteriormente, complete Hola siguiendo el paso:

De hello **direcciones IP** hoja mostrado anteriormente, haga clic en **dinámica** en **asignación**y, a continuación, haga clic en **guardar**.

## <a name="next-steps"></a>Pasos siguientes
* Obtenga más información acerca de las [direcciones IP públicas reservadas](virtual-networks-reserved-public-ip.md) .
* Obtenga información sobre las [direcciones IP públicas a nivel de instancia (ILPIP)](virtual-networks-instance-level-public-ip.md) .
* Consulte hello [API de REST para IP reservadas](https://msdn.microsoft.com/library/azure/dn722420.aspx).

