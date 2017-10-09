---
title: "aaaConfigure de direcciones IP privadas para las máquinas virtuales (clásico): portal de Azure | Documentos de Microsoft"
description: "Obtenga información acerca de cómo tooconfigure de direcciones IP privadas de máquinas virtuales (clásicas) mediante Hola portal de Azure."
services: virtual-network
documentationcenter: na
author: jimdial
manager: timlt
editor: tysonn
tags: azure-service-management
ms.assetid: b8ef8367-58b2-42df-9f26-3269980950b8
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/04/2016
ms.author: jdial
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: df4bfa6768fc9e66db89785b633ffdb0274dbc46
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="configure-private-ip-addresses-for-a-virtual-machine-classic-using-hello-azure-portal"></a>Configurar las direcciones IP privadas para una máquina virtual (clásica) mediante Hola portal de Azure

[!INCLUDE [virtual-networks-static-private-ip-selectors-classic-include](../../includes/virtual-networks-static-private-ip-selectors-classic-include.md)]

[!INCLUDE [virtual-networks-static-private-ip-intro-include](../../includes/virtual-networks-static-private-ip-intro-include.md)]

[!INCLUDE [azure-arm-classic-important-include](../../includes/azure-arm-classic-important-include.md)]

Este artículo trata el modelo de implementación clásica de Hola. También puede [administrar una dirección IP privada estática en el modelo de implementación del Administrador de recursos de hello](virtual-networks-static-private-ip-arm-pportal.md).

[!INCLUDE [virtual-networks-static-ip-scenario-include](../../includes/virtual-networks-static-ip-scenario-include.md)]

siguientes pasos de ejemplo de Hola esperan un entorno simple ya creado. Si desea toorun pasos de hello, que se muestran en este documento, en primer lugar crear entorno de prueba de Hola se describe en [crear una red virtual](virtual-networks-create-vnet-classic-pportal.md).

## <a name="how-toospecify-a-static-private-ip-address-when-creating-a-vm"></a>¿Cómo toospecify una privada de direcciones IP estáticas al crear una máquina virtual
una máquina virtual denominada toocreate *DNS01* en hello *front-end* subred de una red virtual denominada *TestVNet* con una dirección IP estática privada de *192.168.1.101*, Siga los pasos de hello siguientes:

1. Desde un explorador, navegue toohttp://portal.azure.com y, si es necesario, inicie sesión con su cuenta de Azure.
2. Haga clic en **NEW** > **proceso** > **Windows Server 2012 R2 Datacenter**, tenga en cuenta que hello **seleccionar un modelo de implementación** lista ya se muestran **clásico**y, a continuación, haga clic en **crear**.
   
    ![Creación de una VM en el Portal de Azure](./media/virtual-networks-static-ip-classic-pportal/figure01.png)
3. Hola **crear VM** hoja, escriba nombre Hola de hello VM toobe creado (*DNS01* en nuestro escenario), Hola cuenta de administrador local y la contraseña.
   
    ![Creación de una VM en el Portal de Azure](./media/virtual-networks-static-ip-classic-pportal/figure02.png)
4. Haga clic en **Configuración opcional** > **Red** > **Virtual Network** y en **TestVNet**. Si **TestVNet** no está disponible, asegúrese de que está utilizando hello *Central US* ubicación y se ha creado el entorno de prueba de hello descrito al principio de Hola de este artículo.
   
    ![Creación de una VM en el Portal de Azure](./media/virtual-networks-static-ip-classic-pportal/figure03.png)
5. Hola **red** hoja, asegúrese de que Hola la subred seleccionada actualmente es *front-end*, a continuación, haga clic en **direcciones IP**, en **delaasignacióndedireccionesIP** haga clic en **estático**y, a continuación, escriba *192.168.1.101* para **dirección IP** tal como se muestra a continuación.
   
    ![Creación de una VM en el Portal de Azure](./media/virtual-networks-static-ip-classic-pportal/figure04.png)    
6. Haga clic en **Aceptar** en hello **direcciones IP** blade, a continuación, haga clic en **Aceptar** en hello **red** hoja y haga clic en **Aceptar**Hola **configuración opcional** hoja.
7. Hola **crear VM** hoja, haga clic en **crear**. Aviso Hola mosaico siguientes aparecen en el panel.
   
    ![Creación de una VM en el Portal de Azure](./media/virtual-networks-static-ip-classic-pportal/figure05.png)

## <a name="how-tooretrieve-static-private-ip-address-information-for-a-vm"></a>¿Cómo tooretrieve dirección IP estática privada información de dirección de una máquina virtual
tooview Hola privada información direcciones IP estáticas para hello máquinas virtuales crean con hello los pasos descritos anteriormente, ejecute los pasos de Hola a continuación.

1. En el portal de Azure de Azure de hello, haga clic en **examinar todos los** > **máquinas virtuales (clásicas)** > **DNS01**  >   **Todas las configuraciones** > **direcciones IP** y observe Hola asignación de direcciones IP y la dirección IP, tal como se muestra a continuación.
   
    ![Creación de una VM en el Portal de Azure](./media/virtual-networks-static-ip-classic-pportal/figure06.png)

## <a name="how-tooremove-a-static-private-ip-address-from-a-vm"></a>¿Cómo tooremove una privada de direcciones IP estáticas de una máquina virtual
tooremove Hola privada dirección IP estática de hello virtual creado anteriormente, siga los pasos de Hola a continuación.

1. De hello **direcciones IP** hoja mostrado anteriormente, haga clic en **dinámica** toohello derecha de **asignación de direcciones IP**, a continuación, haga clic en **guardar**y, a continuación, Haga clic en **Sí**.
   
    ![Creación de una VM en el Portal de Azure](./media/virtual-networks-static-ip-classic-pportal/figure07.png)

## <a name="how-tooadd-a-static-private-ip-address-tooan-existing-vm"></a>Cómo tooadd una dirección IP estática privada direccionan tooan existente de la máquina virtual
tooadd una toohello de dirección IP privada máquinas virtuales creadas mediante Hola pasos anteriores, estático, siga Hola pasos:

1. De hello **direcciones IP** hoja mostrado anteriormente, haga clic en **estático** toohello derecha de **asignación de direcciones IP**.
2. Escriba *192.168.1.101* en **Dirección IP** y haga clic en **Guardar** y en **Sí**.

## <a name="next-steps"></a>Pasos siguientes
* Obtenga más información acerca de las [direcciones IP públicas reservadas](virtual-networks-reserved-public-ip.md) .
* Obtenga información sobre las [direcciones IP públicas a nivel de instancia (ILPIP)](virtual-networks-instance-level-public-ip.md) .
* Consulte hello [API de REST para IP reservadas](https://msdn.microsoft.com/library/azure/dn722420.aspx).

