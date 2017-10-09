---
title: "¿Cómo tooconfigure enrutamiento (emparejamiento) por un circuito ExpressRoute: el Administrador de recursos: Azure | Documentos de Microsoft"
description: "En este artículo le guiará por los pasos de Hola para crear y aprovisionamiento Hola privado, público y emparejamiento de Microsoft de un circuito de ExpressRoute. Este artículo también muestra cómo toocheck estado de hello, actualizar o eliminar emparejamientos para el circuito."
documentationcenter: na
services: expressroute
author: cherylmc
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 8c2a7ed2-ae5c-4e49-81f6-77cf9f2b2ac9
ms.service: expressroute
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/31/2017
ms.author: cherylmc
ms.openlocfilehash: a8ca25f488dde728cb3b06cd2c91873f3069feaf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-modify-peering-for-an-expressroute-circuit"></a>Creación y modificación del emparejamiento de un circuito ExpressRoute

En este artículo le ayuda a crear y administrar la configuración de enrutamiento para un circuito ExpressRoute en modelo de implementación de administrador de recursos de hello mediante Hola portal de Azure. También puede comprobar el estado de hello, update o delete y desaprovisionar los emparejamientos de un circuito de ExpressRoute. Si desea toouse una toowork otro método con el circuito, seleccione un artículo de hello lista siguiente:


## <a name="configuration-prerequisites"></a>Requisitos previos de configuración

* Asegúrese de que ha revisado hello [requisitos previos](expressroute-prerequisites.md) página hello [requisitos de enrutamiento](expressroute-routing.md) hello y página [flujos de trabajo](expressroute-workflows.md) página antes de comenzar la configuración.
* Tiene que tener un circuito ExpressRoute activo. Siga las instrucciones de hello demasiado[crear un circuito ExpressRoute](expressroute-howto-circuit-portal-resource-manager.md) y tener circuito de hello habilitada por el proveedor de conectividad antes de continuar. Hola circuito de ExpressRoute debe estar en un estado habilitado y aprovisionado para usted toobe toorun capaz de hello cmdlets en las secciones siguientes se Hola.
* Si tiene previsto toouse un hash MD5/clave compartido, ser seguro toouse esto en ambos lados del Hola túnel y límite Hola el número máximo de caracteres tooa de 25.

Estas instrucciones aplican solo toocircuits creado con proveedores de servicios que ofrece servicios de conectividad de nivel 2. Si usa un proveedor de servicios que ofrece servicios administrados de nivel 3 (normalmente VPN IP, como MPLS), el mismo proveedor de conectividad configura y administra el enrutamiento. 

> [!IMPORTANT]
> Se actualmente no se publica emparejamientos configurados por los proveedores de servicios a través del portal de administración de servicios de Hola. Se está trabajando para habilitar esta funcionalidad pronto. Antes de configurar los emparejamientos BGP, realice las comprobaciones pertinentes con su proveedor de servicios.
> 
> 

Puede configurar una, dos o las tres configuraciones entre pares (Azure privado, Azure público y Microsoft) para un circuito ExpressRoute. Puede establecer las configuraciones entre pares en cualquier orden. Sin embargo, debe asegurarse de completar configuración de Hola de cada uno de ellos emparejamiento a la vez.

## <a name="azure-private-peering"></a>Configuración entre pares privados de Azure

En esta sección le ayuda a crear, obtener, actualizar y eliminar hello Azure configuración privada de emparejamiento de un circuito de ExpressRoute.

### <a name="toocreate-azure-private-peering"></a>toocreate emparejamiento privado de Azure

1. Configurar circuito de ExpressRoute Hola. Asegúrese de que el circuito de hello está aprovisionado por completo por el proveedor de conectividad de hello antes de continuar.

  ![list](./media/expressroute-howto-routing-portal-resource-manager/listprovisioned.png)
2. Configurar Azure intercambio de tráfico privado para el circuito de Hola. Asegúrese de que dispone de hello siguientes elementos antes de continuar con los pasos siguientes de hello:

  * / 30 subred para el vínculo principal Hola. subred de Hello no debe formar parte de cualquier espacio de direcciones reservada para las redes virtuales.
  * / 30 subred para el vínculo secundario Hola. subred de Hello no debe formar parte de cualquier espacio de direcciones reservada para las redes virtuales.
  * Un tooestablish de Id. de VLAN válido este emparejamiento correctamente. No Asegúrese de que ningún otro emparejamiento en el circuito de hello usa Hola mismo identificador de VLAN.
  * Número de sistema autónomo (AS) para la configuración entre pares. Puede usar 2 bytes o 4 bytes como números AS. Puede usar un número AS privado para esta configuración entre pares. Asegúrese de que no usa 65515.
  * **Opcional:** un hash MD5 si elige toouse uno.
3. Seleccione la fila de emparejamiento privada de Azure de hello, como se muestra en el siguiente ejemplo de Hola:

  ![privado](./media/expressroute-howto-routing-portal-resource-manager/rprivate1.png)
4. Configure el emparejamiento privado. Hola siguiente imagen muestra un ejemplo de configuración:

  ![configurar el emparejamiento privado](./media/expressroute-howto-routing-portal-resource-manager/rprivate2.png)
5. Guardar configuración de hello una vez que haya especificado todos los parámetros. Una vez que ha aceptado correctamente la configuración de hello, verá algo similar toohello siguiente ejemplo:

  ![guardar emparejamiento privado](./media/expressroute-howto-routing-portal-resource-manager/rprivate3.png)

### <a name="tooview-azure-private-peering-details"></a>tooview privada emparejamiento detalles de Azure

Puede ver propiedades de Hola de emparejamiento privado Azure seleccionando Hola emparejamiento.

![ver emparejamiento privado](./media/expressroute-howto-routing-portal-resource-manager/rprivate3.png)

### <a name="tooupdate-azure-private-peering-configuration"></a>tooupdate configuración de emparejamiento privada de Azure

Puede seleccionar la fila de hello para el emparejamiento y modificar las propiedades de emparejamiento de Hola.

![actualizar emparejamiento privado](./media/expressroute-howto-routing-portal-resource-manager/rprivate2.png)

### <a name="toodelete-azure-private-peering"></a>toodelete emparejamiento privado de Azure

Puede quitar la configuración de emparejamiento seleccionando el icono de eliminación de hello, como se muestra en hello después de imagen:

![eliminar emparejamiento privado](./media/expressroute-howto-routing-portal-resource-manager/rprivate4.png)

## <a name="azure-public-peering"></a>Configuración entre pares públicos de Azure

En esta sección le ayuda a crear, obtener, actualizar y eliminar hello Azure configuración de emparejamiento público de un circuito de ExpressRoute.

### <a name="toocreate-azure-public-peering"></a>toocreate pares públicos de Azure

1. Configure un circuito de ExpressRoute. Asegúrese de que el circuito de hello está aprovisionado por completo por el proveedor de conectividad de hello antes de continuar más.

  ![mostrar emparejamiento público](./media/expressroute-howto-routing-portal-resource-manager/listprovisioned.png)
2. Configure pares públicos de Azure para el circuito de Hola. Asegúrese de que dispone de hello siguientes elementos antes de continuar con los pasos siguientes de hello:

  * / 30 subred para el vínculo principal Hola. Tiene que ser un prefijo IPv4 público válido.
  * / 30 subred para el vínculo secundario Hola. Tiene que ser un prefijo IPv4 público válido.
  * Un tooestablish de Id. de VLAN válido este emparejamiento correctamente. No Asegúrese de que ningún otro emparejamiento en el circuito de hello usa Hola mismo identificador de VLAN.
  * Número de sistema autónomo (AS) para la configuración entre pares. Puede usar 2 bytes o 4 bytes como números AS.
  * **Opcional:** un hash MD5 si elige toouse uno.
3. Seleccione hello Azure fila emparejamiento público, tal como se muestra en hello después de imagen:

  ![seleccionar fila de emparejamiento público](./media/expressroute-howto-routing-portal-resource-manager/rpublic1.png)
4. Configure el emparejamiento público. Hola siguiente imagen muestra un ejemplo de configuración:

  ![Configuración del emparejamiento público](./media/expressroute-howto-routing-portal-resource-manager/rpublic2.png)
5. Guardar configuración de hello una vez que haya especificado todos los parámetros. Una vez que ha aceptado correctamente la configuración de hello, verá algo similar toohello siguiente ejemplo:

  ![Guardado de configuración de emparejamiento público](./media/expressroute-howto-routing-portal-resource-manager/rpublic3.png)

### <a name="tooview-azure-public-peering-details"></a>tooview Azure pública emparejamiento detalles

Puede ver propiedades de Hola de emparejamiento público Azure seleccionando Hola emparejamiento.

![ver propiedades de emparejamiento público](./media/expressroute-howto-routing-portal-resource-manager/rpublic3.png)

### <a name="tooupdate-azure-public-peering-configuration"></a>tooupdate configuración de interconexión pública de Azure

Puede seleccionar la fila de hello para el emparejamiento y modificar las propiedades de emparejamiento de Hola.

![seleccionar fila de emparejamiento público](./media/expressroute-howto-routing-portal-resource-manager/rpublic2.png)

### <a name="toodelete-azure-public-peering"></a>toodelete pares públicos de Azure

Puede quitar la configuración de emparejamiento seleccionando el icono de eliminación de hello, como se muestra en el siguiente ejemplo de Hola:

![eliminar emparejamiento público](./media/expressroute-howto-routing-portal-resource-manager/rpublic4.png)

## <a name="microsoft-peering"></a>Emparejamiento de Microsoft

En esta sección le ayuda a crear, obtener, actualizar y eliminar la configuración de emparejamiento de Microsoft de Hola por un circuito ExpressRoute.

> [!IMPORTANT]
> Emparejamiento de Microsoft de circuitos ExpressRoute que estaban configurados anterior tooAugust 1, 2017 tendrá todos los prefijos de servicio implementados a través de emparejamiento de Microsoft hello, incluso si no se definen los filtros de ruta. Emparejamiento de Microsoft de circuitos ExpressRoute configurados en o después del 1 de agosto de 2017 no tendrá todos los prefijos anunciados hasta que se conecte un filtro de ruta toohello circuito. Para más información, consulte [Configuración de un filtro de ruta para el emparejamiento de Microsoft](how-to-routefilter-powershell.md).
> 
> 

### <a name="toocreate-microsoft-peering"></a>emparejamiento de Microsoft toocreate

1. Configure un circuito de ExpressRoute. Asegúrese de que el circuito de hello está aprovisionado por completo por el proveedor de conectividad de hello antes de continuar más.

  ![mostrar emparejamiento de Microsoft](./media/expressroute-howto-routing-portal-resource-manager/listprovisioned.png)
2. Configurar Microsoft emparejamiento para el circuito de Hola. Asegúrese de que haya Hola siguiente información antes de continuar.

  * / 30 subred para el vínculo principal Hola. Debe ser un prefijo de IPv4 público válido que sea de su propiedad y esté registrado en un Registro regional de Internet (RIR) o un Registro de enrutamiento de Internet (IRR).
  * / 30 subred para el vínculo secundario Hola. Debe ser un prefijo de IPv4 público válido que sea de su propiedad y esté registrado en un Registro regional de Internet (RIR) o un Registro de enrutamiento de Internet (IRR).
  * Un tooestablish de Id. de VLAN válido este emparejamiento correctamente. No Asegúrese de que ningún otro emparejamiento en el circuito de hello usa Hola mismo identificador de VLAN.
  * Número de sistema autónomo (AS) para la configuración entre pares. Puede usar 2 bytes o 4 bytes como números AS.
  * Anuncian prefijos: debe proporcionar una lista de todos los prefijos piensa tooadvertise en las sesiones BGP Hola. Se aceptan solo prefijos de direcciones IP públicas. Si tiene previsto toosend un conjunto de prefijos, puede enviar una lista separada por comas. Estos prefijos deben ser tooyou registrado en un RIR / IRR.
  * **Opcional:** cliente ASN: si es que los prefijos de publicidad que no están registrado toohello emparejamiento como número, puede especificar hello como número toowhich están registrados.
  * Nombre del enrutamiento del registro: Puede especificar Hola RIR / IRR en qué hello como número y los prefijos registrados.
  * **Opcional:** un hash MD5 si elige toouse uno.
3. Puede seleccionar Hola emparejamiento desea tooconfigure, como se muestra en hello después de ejemplo. Seleccione la fila de emparejamiento de Microsoft de Hola.

  ![seleccionar fila de emparejamiento de Microsoft](./media/expressroute-howto-routing-portal-resource-manager/rmicrosoft1.png)
4. Configure el emparejamiento de Microsoft Hola siguiente imagen muestra un ejemplo de configuración:

  ![configurar emparejamiento de Microsoft](./media/expressroute-howto-routing-portal-resource-manager/rmicrosoft2.png)
5. Guardar configuración de hello una vez que haya especificado todos los parámetros.

  Si el circuito obtiene tooa 'Validación necesaria' estado (como se muestra en la imagen de hello), debe abrir una tooshow de vale de soporte técnico de prueba de posesión del equipo de soporte técnico de hello prefijos tooour.

  ![Guardado de la configuración de emparejamiento de Microsoft](./media/expressroute-howto-routing-portal-resource-manager/rmicrosoft5.png)

  Puede abrir una incidencia de soporte técnico directamente desde el portal de hello, como se muestra en el siguiente ejemplo de Hola:

  ![](./media/expressroute-howto-routing-portal-resource-manager/rmicrosoft6.png)


1. Una vez que ha aceptado correctamente la configuración de hello, verá algo similar toohello después de imagen:

  ![](./media/expressroute-howto-routing-portal-resource-manager/rmicrosoft7.png)

### <a name="tooview-microsoft-peering-details"></a>detalles de emparejamiento de Microsoft tooview

Puede ver propiedades de Hola de emparejamiento público Azure seleccionando Hola emparejamiento.

![](./media/expressroute-howto-routing-portal-resource-manager/rmicrosoft3.png)

### <a name="tooupdate-microsoft-peering-configuration"></a>configuración de emparejamiento de Microsoft tooupdate

Puede seleccionar la fila de hello para el emparejamiento y modificar las propiedades de emparejamiento de Hola.

![](./media/expressroute-howto-routing-portal-resource-manager/rmicrosoft7.png)

### <a name="toodelete-microsoft-peering"></a>emparejamiento de Microsoft toodelete

Puede quitar la configuración de emparejamiento seleccionando el icono de eliminación de hello, como se muestra en hello después de imagen:

![](./media/expressroute-howto-routing-portal-resource-manager/rmicrosoft4.png)

## <a name="next-steps"></a>Pasos siguientes

Siguiente paso, [vincular un circuito de ExpressRoute de tooan de red virtual](expressroute-howto-linkvnet-portal-resource-manager.md)
* Para más información sobre los flujos de trabajo de ExpressRoute, vea [Flujos de trabajo de ExpressRoute](expressroute-workflows.md).
* Para más información sobre el emparejamiento de circuitos, vea [Circuitos y dominios de enrutamiento de ExpressRoute](expressroute-circuit-peerings.md).
* Para más información sobre redes virtuales, vea [Información general sobre redes virtuales](../virtual-network/virtual-networks-overview.md).
