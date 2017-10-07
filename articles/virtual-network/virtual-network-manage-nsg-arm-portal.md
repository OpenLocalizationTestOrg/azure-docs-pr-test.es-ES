---
title: los NSG de aaaManage con hello portal de Azure | Documentos de Microsoft
description: "Obtenga información acerca de cómo toomanage existente NSG mediante Hola portal de Azure."
services: virtual-network
documentationcenter: na
author: jimdial
manager: carmonm
editor: 
tags: azure-resource-manager
ms.assetid: 5d55679d-57da-457c-97dc-1e1973909ee5
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 03/14/2016
ms.author: jdial
ms.openlocfilehash: ad9a4060bd81bae4597ad5a4f59622e10cd214cf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="manage-nsgs-using-hello-portal"></a>Administrar los NSG mediante el portal de Hola

> [!div class="op_single_selector"]
> * [Portal](virtual-network-manage-nsg-arm-portal.md)
> * [PowerShell](virtual-network-manage-nsg-arm-ps.md)
> * [CLI de Azure](virtual-network-manage-nsg-arm-cli.md)
>

[!INCLUDE [virtual-network-manage-nsg-intro-include.md](../../includes/virtual-network-manage-nsg-intro-include.md)]

> [!NOTE]
> Azure tiene dos modelos de implementación diferentes para crear recursos y trabajar con ellos: [Resource Manager y el clásico](../resource-manager-deployment-model.md). Este artículo incluye el uso de modelo de implementación de administrador de recursos de hello, que Microsoft recomienda para la mayoría de las nueva implementaciones en lugar del modelo de implementación clásica de Hola.
>

[!INCLUDE [virtual-network-manage-nsg-arm-scenario-include.md](../../includes/virtual-network-manage-nsg-arm-scenario-include.md)]

## <a name="retrieve-information"></a>Recuperar información
Puede consultar los NSG existentes, recuperar las reglas de un NSG existente y averiguar cuáles son los recursos a los que está asociado un NSG.

### <a name="view-existing-nsgs"></a>Consultar los NSG existentes

tooview todos los existentes NSG en una suscripción completa Hola pasos:

1. Desde un explorador, navegue toohttp://portal.azure.com y, si es necesario, inicie sesión con su cuenta de Azure.

2. Haga clic en **Examinar >** > **Grupos de seguridad de red**.

    ![Portal de Azure - NSG](./media/virtual-network-manage-nsg-arm-portal/figure1.png)

3. Comprobar lista de Hola de NSG Hola **grupos de seguridad de red** hoja.

    ![Portal de Azure - NSG](./media/virtual-network-manage-nsg-arm-portal/figure2.png)

### <a name="view-nsgs-in-a-resource-group"></a>Visualización de los NSG en un grupo de recursos

lista de Hola de tooview de NSG de hello **NSG RG** grupo de recursos, Hola completa pasos:

1. Haga clic en **Grupos de recursos >** > **RG-NSG** > **...**.

    ![Portal de Azure - NSG](./media/virtual-network-manage-nsg-arm-portal/figure3.png)

2. En la lista Hola de recursos, buscar elementos mostrando hello NSG icono, tal y como se muestra en hello **recursos** hoja a continuación.

    ![Portal de Azure - NSG](./media/virtual-network-manage-nsg-arm-portal/figure4.png)

### <a name="list-all-rules-for-an-nsg"></a>Mostrar todas las reglas de un NSG

reglas de hello tooview de un NSG denominado **NSG-front-end**completa Hola lo siguiente:

1. De hello **grupos de seguridad de red** hoja o hello **recursos** hoja mostrado anteriormente, haga clic en **NSG-front-end**.

2. Hola **configuración** , haga clic en **reglas de seguridad de entrada**.

    ![Portal de Azure - NSG](./media/virtual-network-manage-nsg-arm-portal/figure5.png)

3. Hola **reglas de seguridad de entrada** hoja se muestra tal y como se muestra a continuación.

    ![Portal de Azure - NSG](./media/virtual-network-manage-nsg-arm-portal/figure6.png)

4. Hola **configuración** , haga clic en **reglas de seguridad de salida** toosee Hola reglas de salida.

    > [!NOTE]
    > las reglas predeterminadas de tooview, haga clic en hello **reglas predeterminadas** situado en la parte superior de Hola de hoja de Hola que muestra las reglas de Hola.
    >

### <a name="view-nsgs-associations"></a>Consultar las asociaciones de NSG

tooview qué Hola recursos **front-end de NSG** NSG está asociado con la, completa Hola siguiendo los pasos:

1. De hello **grupos de seguridad de red** hoja o hello **recursos** hoja mostrado anteriormente, haga clic en **NSG-front-end**.

2. Hola **configuración** , haga clic en **subredes** tooview qué subredes son asociados toohello NSG.

    ![Portal de Azure - NSG](./media/virtual-network-manage-nsg-arm-portal/figure7.png)

3. Hola **configuración** , haga clic en **interfaces de red** tooview qué NIC están asociadas toohello NSG.

## <a name="manage-rules"></a>Administrar las reglas
Puede agregar tooan de reglas existente NSG, editar las reglas existentes y quitar las reglas.

### <a name="add-a-rule"></a>Agregar una regla
tooadd una regla que permite **entrante** tráfico tooport **443** desde cualquier máquina toohello **front-end de NSG** NSG, Hola completa pasos:

1. De hello **grupos de seguridad de red** hoja o hello **recursos** hoja mostrado anteriormente, haga clic en **NSG-front-end**.
2. Hola **configuración** , haga clic en **reglas de seguridad de entrada**.
3. Hola **reglas de seguridad de entrada** hoja, haga clic en **agregar**. A continuación, en hello **Agregar regla de seguridad de entrada** hoja, rellenar los valores de hello tal y como se muestra a continuación y, a continuación, haga clic en **Aceptar**.

    ![Portal de Azure - NSG](./media/virtual-network-manage-nsg-arm-portal/figure8.png)

    Después de unos segundos, tenga en cuenta nueva regla de Hola Hola **reglas de seguridad de entrada** hoja.

    ![Portal de Azure - NSG](./media/virtual-network-manage-nsg-arm-portal/figure9.png)

### <a name="change-a-rule"></a>Cambiar una regla
regla de hello toochange creada anteriormente tooallow el tráfico entrante desde hello **Internet** Hola únicamente, completar pasos:

1. De hello **grupos de seguridad de red** hoja o hello **recursos** hoja mostrado anteriormente, haga clic en **NSG-front-end**.
2. Hola **configuración** , haga clic en regla Hola creada anteriormente.
3. Hola **https permitir** hoja, cambio hello **origen** propiedad tal y como se muestra a continuación y, a continuación, haga clic en **guardar**.

    ![Portal de Azure - NSG](./media/virtual-network-manage-nsg-arm-portal/figure10.png)

### <a name="delete-a-rule"></a>Eliminar una regla

toodelete Hola regla creada anteriormente, completa Hola pasos:

1. De hello **grupos de seguridad de red** hoja o hello **recursos** hoja mostrado anteriormente, haga clic en **NSG-front-end**.
2. Hola **configuración** , haga clic en regla Hola creada anteriormente.
3. Hola **https permitir** hoja, haga clic en **eliminar**y, a continuación, haga clic en **Sí**.

    ![Portal de Azure - NSG](./media/virtual-network-manage-nsg-arm-portal/figure11.png)

## <a name="manage-associations"></a>Administrar las asociaciones
Puede asociar un NSG toosubnets y NIC. También puede desasociar un NSG de cualquier recurso al que está asociado.

### <a name="associate-an-nsg-tooa-nic"></a>Asociar una NIC de NSG tooa
Hola tooassociate **front-end de NSG** NSG toohello **TestNICWeb1** NIC, Hola completa pasos:

1. De hello **grupos de seguridad de red** hoja o hello **recursos** hoja mostrado anteriormente, haga clic en **NSG-front-end**.
2. Hola **configuración** , haga clic en **interfaces de red** > **asociar** > **TestNICWeb1**.

    ![Portal de Azure - NSG](./media/virtual-network-manage-nsg-arm-portal/figure12.png)

### <a name="dissociate-an-nsg-from-a-nic"></a>Desasociar un NSG de una NIC

Hola toodissociate **front-end de NSG** NSG de hello **TestNICWeb1** NIC, Hola completa pasos:

1. En el portal de Azure hello, haga clic en **grupos de recursos >** > **RG-NSG** > **...**   >  **TestNICWeb1**.

2. Hola **TestNICWeb1** hoja, haga clic en **cambiar la seguridad...**   >  **Ninguno**.

    ![Portal de Azure - NSG](./media/virtual-network-manage-nsg-arm-portal/figure13.png)

> [!NOTE]
> También puede utilizar este tooany NIC de hoja tooassociate Hola existente NSG.
>

### <a name="dissociate-an-nsg-from-a-subnet"></a>Desasociar un NSG de una subred

Hola toodissociate **front-end de NSG** NSG de hello **front-end** subred, Hola completa pasos:

1. En el portal de Azure hello, haga clic en **grupos de recursos >** > **RG-NSG** > **...**   >  **TestVNet**.

2. Hola **configuración** hoja, haga clic en **subredes** > **front-end** > **grupo de seguridad de red**  >  **Ninguno**.

    ![Portal de Azure - NSG](./media/virtual-network-manage-nsg-arm-portal/figure14.png)

3. Hola **front-end** hoja, haga clic en **guardar**.

    ![Portal de Azure - NSG](./media/virtual-network-manage-nsg-arm-portal/figure15.png)

### <a name="associate-an-nsg-tooa-subnet"></a>Asociar una subred de tooa NSG

Hola tooassociate **front-end de NSG** NSG toohello **FronEnd** subred nuevo, completa Hola pasos:

1. En el portal de Azure hello, haga clic en **grupos de recursos >** > **RG-NSG** > **...**   >  **TestVNet**.
2. Hola **configuración** hoja, haga clic en **subredes** > **front-end** > **grupo de seguridad de red**  >  **NSG-front-end**.
3. Hola **front-end** hoja, haga clic en **guardar**.

> [!NOTE]
> También puede asociar una subred de tooa NSG de thh NSG **configuración** hoja.
>

## <a name="delete-an-nsg"></a>Eliminación de un grupo de seguridad de red
Sólo se puede eliminar un NSG si no tiene asociados recursos tooany. toodelete un NSG, Hola completa pasos:.

1. En el portal de Azure hello, haga clic en **grupos de recursos >** > **RG-NSG** > **...**   >  **NSG-front-end**.
2. Hola **configuración** hoja, haga clic en **interfaces de red**.
3. Si no hay ninguna NIC aparece, haga clic en hello NIC y siga el paso 2 en [desasociar un NSG de una NIC](#Dissociate-an-NSG-from-a-NIC).
4. Repita el paso 3 para cada NIC.
5. Hola **configuración** hoja, haga clic en **subredes**.
6. Si no hay ninguna subred que aparece, haga clic en la subred de Hola y siga los pasos 2 y 3 en [desasociar un NSG de subred](#Dissociate-an-NSG-from-a-subnet).
7. Se desplaza izquierdo toohello **front-end de NSG** hoja, a continuación, haga clic en **eliminar** > **Sí**.

    ![Portal de Azure - NSG](./media/virtual-network-manage-nsg-arm-portal/figure16.png)

## <a name="next-steps"></a>Pasos siguientes
* [Habilite el registro](virtual-network-nsg-manage-log.md) para los NSG.
