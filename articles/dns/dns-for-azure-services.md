---
title: Uso de Azure DNS con otros servicios de Azure | Microsoft Docs
description: "Descripción de cómo usar Azure DNS para resolver el nombre de otros servicios de Azure"
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
ms.openlocfilehash: 5b95d5455c08d09a088c740e9df9605d3d7f719b
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/03/2017
---
# <a name="how-azure-dns-works-with-other-azure-services"></a>Funcionamiento de Azure DNS con otros servicios de Azure

Azure DNS es un servicio de resolución de nombres y administración de DNS hospedado. Esto le permite crear nombres DNS públicos para las otras aplicaciones y servicios que tiene implementados en Azure. Crear el nombre para un servicio de Azure en el dominio personalizado es tan simple como agregar un registro del tipo correcto del servicio.

* Para las direcciones IP asignadas dinámicamente, debe crear un registro CNAME de DNS que se asigna al nombre DNS que Azure creó para el servicio. Los estándares DNS evitan que use un registro CNAME para el vértice de la zona.
* Para las direcciones IP asignadas de forma estática, puede crear un registro D de DNS con cualquier nombre, incluido un nombre de *dominio simple* en el vértice de la zona.

En la tabla siguiente se describen los tipos de registro compatibles que se pueden usar para diversos servicios de Azure. Como puede ver en esta tabla, Azure DNS solo admite registros DNS para recursos de red orientados a Internet. Azure DNS no se puede usar para la resolución de nombres de direcciones privadas internas.

| Servicio de Azure | Interfaz de red | Description |
| --- | --- | --- |
| Application Gateway |[Dirección IP pública front-end](dns-custom-domain.md#public-ip-address) |Puede crear un registro D o CNAME de DNS. |
| Load Balancer |[Dirección IP pública front-end](dns-custom-domain.md#public-ip-address)  |Puede crear un registro D o CNAME de DNS. Load Balancer puede tener una dirección IP pública IPv6 que se asigna dinámicamente. Por lo tanto, debe crear un registro CNAME para una dirección IPv6. |
| Administrador de tráfico |Nombre público |Solo puede crear un registro CNAME que se asigne al nombre de trafficmanager.net que está asignado a su perfil de Traffic Manager. Para más información, consulte [Cómo funciona Traffic Manager](../traffic-manager/traffic-manager-overview.md#traffic-manager-example). |
| Servicio en la nube |[Dirección IP pública](dns-custom-domain.md#public-ip-address) |Para las direcciones IP asignadas de forma estática, puede crear un registro D de DNS. Para las direcciones IP asignadas dinámicamente, debe crear un registro CNAME que se asigne al nombre de *cloudapp.net* . Esta regla se aplica a las máquinas virtuales creadas en el portal clásico, porque están implementadas como servicio en la nube. Para más información, consulte [Configurar un nombre de dominio personalizado en Cloud Services](../cloud-services/cloud-services-custom-domain-name-portal.md). |
| App Service | [Dirección IP externa](dns-custom-domain.md#app-service-web-apps) |Para las direcciones IP externas, puede crear un registro D de DNS. De lo contrario, deberá crear un registro CNAME que se asigne al nombre de azurewebsites.net. Para más información, consulte [Asignación de un nombre de dominio personalizado a una aplicación de Azure](../app-service-web/web-sites-custom-domain-name.md) |
| Máquinas virtuales de Resource Manager |[Dirección IP pública](dns-custom-domain.md#public-ip-address) |Las máquinas virtuales de Resource Manager pueden tener direcciones IP públicas. Una máquina virtual con una dirección IP pública también puede encontrarse detrás de un equilibrador de carga. Puede crear un registro CNAME o D de DNS para la dirección pública. Este nombre personalizado se puede usar para omitir el VIP en el equilibrador de carga. |
| Máquinas virtuales clásicas |[Dirección IP pública](dns-custom-domain.md#public-ip-address) |Las máquinas virtuales clásicas creadas con PowerShell o la CLI se pueden configurar con una dirección virtual dinámica o estática (reservada). Puede crear un registro CNAME o D de DNS, respectivamente. |
