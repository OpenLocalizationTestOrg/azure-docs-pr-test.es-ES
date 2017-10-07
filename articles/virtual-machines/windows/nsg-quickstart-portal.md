---
title: aaaOpen puertos tooa VM con Hola portal de Azure | Documentos de Microsoft
description: "Obtenga información acerca de cómo tooopen un puerto o cree una máquina virtual de Windows tooyour de punto de conexión con el modelo de implementación de administrador de recursos de Hola Hola Portal de Azure"
services: virtual-machines-windows
documentationcenter: 
author: iainfoulds
manager: timlt
editor: 
ms.assetid: f7cf0319-5ee7-435e-8f94-c484bf5ee6f1
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure-services
ms.date: 08/21/2017
ms.author: iainfou
ms.openlocfilehash: aba789c65254651899aa688f256fe616c3d0126d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooopen-ports-tooa-virtual-machine-with-hello-azure-portal"></a>¿Cómo tooopen puertos tooa virtual machine con hello portal de Azure
[!INCLUDE [virtual-machines-common-nsg-quickstart](../../../includes/virtual-machines-common-nsg-quickstart.md)]

## <a name="quick-commands"></a>Comandos rápidos
También puede [llevar a cabo estos pasos con Azure PowerShell](nsg-quickstart-powershell.md).

En primer lugar, cree el grupo de seguridad de red. Seleccione un grupo de recursos en el portal de hello, elija **agregar**, a continuación, busque y seleccione **grupo de seguridad de red**:

![Agregar un grupo de seguridad de red](./media/nsg-quickstart-portal/add-nsg.png)

Escriba el nombre del grupo de seguridad de red, seleccione un grupo de recursos, o créelo, y seleccione una ubicación. Cuando haya terminado, seleccione **Crear**:

![Creación de un grupo de seguridad de red](./media/nsg-quickstart-portal/create-nsg.png)

Seleccione el nuevo grupo de seguridad de red. Seleccione 'Reglas de seguridad de entrada', a continuación, seleccione hello **agregar** botón toocreate una regla:

![Agregar una regla de entrada](./media/nsg-quickstart-portal/add-inbound-rule.png)

Elija una común **servicio** desde el menú desplegable de hello, como *HTTP*. También puede seleccionar *personalizado* tooprovide toouse de un puerto específico. Si desea cambiar la prioridad de Hola o nombre. Hello prioridad afecta al orden de hello en el que se aplican las reglas - Hola Hola numérico un valor inferior, hello anteriores Hola regla se aplica. También puede seleccionar **avanzadas** en parte superior de Hola de este tooenter de pantalla de un determinado origen IP bloque o intervalo de puerto, por ejemplo. Cuando esté listo, seleccione **Aceptar** regla de Hola toocreate:

![Crear una regla de entrada](./media/nsg-quickstart-portal/create-inbound-rule.png)

El paso final es tooassociate grupo de seguridad de su red con una subred o una interfaz de red específica. Vamos a asociar Hola grupo de seguridad de red a una subred. Seleccione **Subredes** y elija **Asociar**:

![Asociar un grupo de seguridad de red a una subred](./media/nsg-quickstart-portal/associate-subnet.png)

Seleccione la red virtual y, a continuación, seleccione subred adecuada de hello:

![Asociar un grupo de seguridad de red a una red virtual](./media/nsg-quickstart-portal/select-vnet-subnet.png)

Ahora ha creado un grupo de seguridad de red, ha creado una regla de entrada que permite el tráfico en el puerto 80 y lo ha asociado con una subred. Todas las máquinas virtuales que se conecta toothat subred son accesibles en el puerto 80.

## <a name="more-information-on-network-security-groups"></a>Más información sobre los grupos de seguridad de red
Hola de comandos rápido aquí le permite tooget seguridad y en ejecución con tooyour del flujo de tráfico máquina virtual. Grupos de seguridad de red proporcionan muchas características excepcionales y granularidad para controlar acceso a los recursos tooyour. Puede leer más sobre la [creación de un grupo de seguridad de red y las reglas de ACL aquí](../../virtual-network/virtual-networks-create-nsg-arm-ps.md).

Para las aplicaciones web de alta disponibilidad, debe colocar las máquinas virtuales detrás de una instancia de Azure Load Balancer. equilibrador de carga de Hello distribuye el tráfico tooVMs, con un grupo de seguridad de red que proporciona filtrado de tráfico. Para obtener más información, consulte [cómo equilibrar tooload Linux virtual máquinas en Azure toocreate una aplicación de alta disponibilidad](tutorial-load-balancer.md).

## <a name="next-steps"></a>Pasos siguientes
En este ejemplo, ha creado el tráfico de tooallow HTTP de una regla sencilla. Puede encontrar información sobre cómo crear entornos más detallados en hello siguientes artículos:

* [Información general sobre Azure Resource Manager](../../azure-resource-manager/resource-group-overview.md)
* [¿Qué es un grupo de seguridad de red?](../../virtual-network/virtual-networks-nsg.md)