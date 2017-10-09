---
title: aaaUsing DNS de Azure con otros servicios de Azure | Documentos de Microsoft
description: "Descripción de cómo el nombre toouse DNS de Azure tooresolve para otros servicios de Azure"
services: dns
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
tags: azure dns
ms.assetid: e9b5eb94-7984-4640-9930-564bb9e82b78
ms.service: dns
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.custom: H1Hack27Feb2017
ms.workload: infrastructure-services
ms.date: 09/21/2016
ms.author: gwallace
ms.openlocfilehash: 791f93d6aff2c638c08518e9f1e8ab89ac8de3f2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="how-azure-dns-works-with-other-azure-services"></a>Funcionamiento de Azure DNS con otros servicios de Azure

Azure DNS es un servicio de resolución de nombres y administración de DNS hospedado. Esto permite toocreate públicos nombres DNS para hello otras aplicaciones y servicios implementados en Azure. Crear un nombre para un servicio de Azure en su dominio personalizado es tan simple como agregar un registro de hello tipo correcto para el servicio.

* Para las direcciones IP asignadas dinámicamente, debe crear un registro CNAME DNS ese nombre DNS de toohello mapas creados en Azure para su servicio. Estándares DNS impedirle usar un registro CNAME para el vértice de la zona de Hola.
* Para las direcciones IP asignadas estáticamente, puede crear un registro DNS A con cualquier nombre, incluido un *dominio naked* nombre en vértice de la zona de Hola.

Hola Hola de esquemas de tabla siguientes admite tipos de registro que pueden utilizarse para varios servicios de Azure. Como puede ver en esta tabla, Azure DNS solo admite registros DNS para recursos de red orientados a Internet. Azure DNS no se puede usar para la resolución de nombres de direcciones privadas internas.

| Servicio de Azure | Interfaz de red | Description |
| --- | --- | --- |
| Application Gateway |[Dirección IP pública front-end](dns-custom-domain.md#public-ip-address) |Puede crear un registro D o CNAME de DNS. |
| Load Balancer |[Dirección IP pública front-end](dns-custom-domain.md#public-ip-address)  |Puede crear un registro D o CNAME de DNS. Load Balancer puede tener una dirección IP pública IPv6 que se asigna dinámicamente. Por lo tanto, debe crear un registro CNAME para una dirección IPv6. |
| Administrador de tráfico |Nombre público |Solo se puede crear un CNAME que asigne toohello trafficmanager.net nombre asignado tooyour perfil de Traffic Manager. Para más información, consulte [Cómo funciona Traffic Manager](../traffic-manager/traffic-manager-overview.md#traffic-manager-example). |
| Servicio en la nube |[Dirección IP pública](dns-custom-domain.md#public-ip-address) |Para las direcciones IP asignadas de forma estática, puede crear un registro D de DNS. Para las direcciones IP asignadas dinámicamente, debe crear un registro CNAME que asigna toohello *cloudapp.net* nombre. Esta regla aplica tooVMs creadas en portal clásico de hello, ya que se implementan como un servicio de nube. Para más información, consulte [Configurar un nombre de dominio personalizado en Cloud Services](../cloud-services/cloud-services-custom-domain-name-portal.md). |
| App Service | [Dirección IP externa](dns-custom-domain.md#app-service-web-apps) |Para las direcciones IP externas, puede crear un registro D de DNS. En caso contrario, debe crear un registro CNAME que asigna toohello azurewebsites.net nombre. Para obtener más información, vea [asignar un tooan de nombre de dominio personalizado aplicación de Azure](../app-service-web/web-sites-custom-domain-name.md) |
| Máquinas virtuales de Resource Manager |[Dirección IP pública](dns-custom-domain.md#public-ip-address) |Las máquinas virtuales de Resource Manager pueden tener direcciones IP públicas. Una máquina virtual con una dirección IP pública también puede encontrarse detrás de un equilibrador de carga. Puede crear un registro DNS A o CNAME para hello dirección pública. Este nombre personalizado puede ser usado toobypass Hola VIP de equilibrador de carga de Hola. |
| Máquinas virtuales clásicas |[Dirección IP pública](dns-custom-domain.md#public-ip-address) |Las máquinas virtuales clásicas creadas con PowerShell o la CLI se pueden configurar con una dirección virtual dinámica o estática (reservada). Puede crear un registro CNAME o D de DNS, respectivamente. |
