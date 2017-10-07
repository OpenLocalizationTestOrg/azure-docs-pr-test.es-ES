---
title: grupos de seguridad de red aaaCreate - portal de Azure | Documentos de Microsoft
description: "Obtenga información acerca de cómo toocreate e implementar grupos de seguridad de red mediante Hola portal de Azure."
services: virtual-network
documentationcenter: na
author: jimdial
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 5bc8fc2e-1e81-40e2-8231-0484cd5605cb
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/04/2016
ms.author: jdial
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: f74ecc7db06bb69f2041aa64d7b38b63eb379a70
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="create-network-security-groups-using-hello-azure-portal"></a>Crear grupos de seguridad mediante el portal de Azure Hola de red

[!INCLUDE [virtual-networks-create-nsg-selectors-arm-include](../../includes/virtual-networks-create-nsg-selectors-arm-include.md)]

[!INCLUDE [virtual-networks-create-nsg-intro-include](../../includes/virtual-networks-create-nsg-intro-include.md)]

[!INCLUDE [azure-arm-classic-important-include](../../includes/azure-arm-classic-important-include.md)]

Este artículo trata el modelo de implementación del Administrador de recursos de Hola. También puede [crear NSG en el modelo de implementación clásica de hello](virtual-networks-create-nsg-classic-ps.md).

[!INCLUDE [virtual-networks-create-nsg-scenario-include](../../includes/virtual-networks-create-nsg-scenario-include.md)]

ejemplo de Hola PowerShell comandos siguientes esperan un entorno simple ya creado se basa en escenario de hello anterior. Si desea toorun comandos de hello, que se muestran en este documento, en primer lugar crear entorno de prueba de hello implementando [esta plantilla](http://github.com/telmosampaio/azure-templates/tree/master/201-IaaS-WebFrontEnd-SQLBackEnd), haga clic en **implementar tooAzure**, reemplace los valores de parámetros predeterminados de Hola Si fuera necesario y siga las instrucciones de hello en Hola portal. Hola los pasos a continuación use **NSG RG** como nombre de Hola de plantilla de Hola de grupo de recursos de Hola se implementó en.

## <a name="create-hello-nsg-frontend-nsg"></a>Crear hello front-end de NSG NSG
Hola toocreate **front-end de NSG** NSG a como se muestra en el escenario de hello anterior, siga los pasos de Hola a continuación.

1. Desde un explorador, navegue toohttp://portal.azure.com y, si es necesario, inicie sesión con su cuenta de Azure.
2. Haga clic en **Examinar >** > **Grupos de seguridad de red**.
   
    ![Portal de Azure - NSG](./media/virtual-networks-create-nsg-arm-pportal/figure11.png)
3. Hola **grupos de seguridad de red** hoja, haga clic en **agregar**.
   
    ![Portal de Azure - NSG](./media/virtual-networks-create-nsg-arm-pportal/figure12.png)
4. Hola **crear grupo de seguridad de red** hoja, crear un NSG denominado *front-end de NSG* en hello *RG-NSG* grupo de recursos y, a continuación, haga clic en **crear**.
   
    ![Portal de Azure - NSG](./media/virtual-networks-create-nsg-arm-pportal/figure13.png)

## <a name="create-rules-in-an-existing-nsg"></a>Creación de reglas en un grupo de seguridad de red existente
reglas de toocreate en un NSG existente de hello portal de Azure, siga Hola pasos.

1. Haga clic en **Examinar >** > **Grupos de seguridad de red**.
2. En la lista de Hola de NSG, haga clic en **front-end de NSG** > **reglas de seguridad de entrada**
   
    ![Portal de Azure - NSG-FrontEnd](./media/virtual-networks-create-nsg-arm-pportal/figure2.png)
3. En la lista de Hola de **reglas de seguridad de entrada**, haga clic en **agregar**.
   
    ![Portal de Azure - Agregar regla](./media/virtual-networks-create-nsg-arm-pportal/figure3.png)
4. Hola **Agregar regla de seguridad de entrada** hoja, crear una regla denominada *regla web* con prioridad de *200* permitir el acceso a través de *TCP* tooport *80* tooany VM desde cualquier origen y, a continuación, haga clic en **Aceptar**. Observe que la mayoría de estas configuraciones son ya valores predeterminados.
   
    ![Portal de Azure - Configuración de la regla](./media/virtual-networks-create-nsg-arm-pportal/figure4.png)
5. Después de unos segundos se verá la nueva regla de Hola Hola NSG.
   
    ![Portal de Azure - Nueva regla](./media/virtual-networks-create-nsg-arm-pportal/figure5.png)
6. Repita los pasos too6 toocreate una regla de entrada denominada *rdp-rule* con una prioridad de *250* permitir el acceso a través de *TCP* tooport *3389* tooany máquina virtual desde cualquier origen.

## <a name="associate-hello-nsg-toohello-frontend-subnet"></a>Asociar la subred de front-end de hello NSG toohello
1. Haga clic en **Examinar >** > **Grupos de recursos** > **RG-NSG**.
2. Hola **RG-NSG** hoja, haga clic en **...**   >  **TestVNet**.
   
    ![Portal de Azure - TestVNet](./media/virtual-networks-create-nsg-arm-pportal/figure14.png)
3. Hola **configuración** hoja, haga clic en **subredes** > **front-end** > **grupo de seguridad de red**  >  **NSG-front-end**.
   
    ![Portal de Azure - Configuración de la subred](./media/virtual-networks-create-nsg-arm-pportal/figure15.png)
4. Hola **front-end** hoja, haga clic en **guardar**.
   
    ![Portal de Azure - Configuración de la subred](./media/virtual-networks-create-nsg-arm-pportal/figure16.png)

## <a name="create-hello-nsg-backend-nsg"></a>Crear hello NSG de back-end de NSG
Hola toocreate **back-end de NSG** NSG y asociarlo toohello **back-end** subred, siga los pasos de Hola a continuación.

1. Hola Repita los pasos de [crear Hola front-end de NSG NSG](#Create-the-NSG-FrontEnd-NSG) toocreate un NSG denominado *NSG-back-end*
2. Hola Repita los pasos de [crear reglas en un NSG existente](#Create-rules-in-an-existing-NSG) toocreate hello **entrada** reglas de hello tabla siguiente.
   
   | Regla de entrada | Regla de salida |
   | --- | --- |
   | ![Portal de Azure - Regla de entrada](./media/virtual-networks-create-nsg-arm-pportal/figure17.png) |![Portal de Azure - Regla de salida](./media/virtual-networks-create-nsg-arm-pportal/figure18.png) |
3. Hola Repita los pasos de [asociar la subred de front-end de hello NSG toohello](#Associate-the-NSG-to-the-FrontEnd-subnet) tooassociate hello **back-end de NSG** NSG toohello **back-end** subred.

## <a name="next-steps"></a>Pasos siguientes
* Obtenga información acerca de cómo demasiado[administrar NSG existentes](virtual-network-manage-nsg-arm-portal.md)
* [Habilite el registro](virtual-network-nsg-manage-log.md) para los grupos de seguridad de red.

