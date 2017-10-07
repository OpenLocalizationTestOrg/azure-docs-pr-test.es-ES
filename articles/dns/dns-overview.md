---
title: aaaOverview de DNS de Azure | Documentos de Microsoft
description: "Información general del servicio de hospedaje de DNS en Microsoft Azure. Hospede el dominio en Microsoft Azure."
services: dns
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: 68747a0d-b358-4b8e-b5e2-e2570745ec3f
ms.service: dns
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 04/19/2017
ms.author: gwallace
ms.openlocfilehash: a10f87c488356469e9c04aabde31129049563891
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="azure-dns-overview"></a>Introducción a DNS de Azure

Hola sistema de nombres de dominio o DNS, es responsable de traducir (o la resolución de) un sitio Web o servicio name tooits dirección IP. DNS de Azure es un servicio de hospedaje para los dominios DNS, que permite resolver nombres mediante la infraestructura de Microsoft Azure. Mediante el hospedaje de los dominios en Azure, puede administrar su DNS los registros mediante Hola mismas credenciales, API, herramientas y facturación como los servicios de Azure.

![Información general de DNS](./media/dns-overview/scenario.png)

## <a name="features"></a>Características

* **Fiabilidad y rendimiento**: los dominios DNS de DNS de Azure se hospedan en la red global de servidores de nombres DNS de Azure. Utilizamos difusión por proximidad de red para que cada consulta DNS se responde por servidor DNS más cercano disponible de Hola. Esto ofrece un rendimiento rápido y alta disponibilidad para el dominio.

* **Integración sin problemas** -servicio de DNS de Azure de hello puede ser usado toomanage registros DNS para los servicios de Azure y puede ser usado tooprovide DNS para los recursos externos, así. DNS de Azure está integrado en hello portal de Azure y utiliza Hola mismas credenciales, facturación y contrato de soporte técnico como los servicios de Azure.

* **Seguridad** -Hola servicio DNS de Azure se basa en el Administrador de recursos de Azure. Como tal, se beneficia de características Resource Manager, como control de acceso basado en roles, registros de auditoría y bloqueo de recursos. Los dominios y los registros se pueden administrar a través de hello portal de Azure, cmdlets de PowerShell de Azure y Hola CLI de Azure entre plataformas. Las aplicaciones que requieren la administración automática de DNS pueden integrar con el servicio de Hola a través de hello REST API y SDK.

DNS de Azure actualmente no admite la adquisición de nombres de dominio. Si desea toopurchase dominios, deberá toouse un registrador de nombres de dominio de otro fabricante. registrador de Hello suelen cobra una pequeña cuota anual. dominios de Hello, a continuación, se pueden hospedar en DNS de Azure para la administración de registros DNS. Vea [delegar un tooAzure de dominio DNS](dns-domain-delegation.md) para obtener más información.

## <a name="pricing"></a>Precios

Facturación de DNS se basa en el número de Hola de las zonas DNS hospedadas en Azure y por número de Hola de las consultas DNS. más sobre los precios visita toolearn [precios de Azure DNS](https://azure.microsoft.com/pricing/details/dns/).

## <a name="faq"></a>P+F

Para las preguntas más frecuentes acerca de DNS de Azure, vea hello [preguntas más frecuentes de Azure DNS](dns-faq.md).

## <a name="next-steps"></a>Pasos siguientes

Visite [Información general sobre zonas y registros de DNS](dns-zones-records.md) para obtener más información sobre zonas y registros DNS.

Obtenga información acerca de cómo demasiado[crear una zona DNS](./dns-getstarted-create-dnszone-portal.md) en DNS de Azure.

Obtener información sobre algunas de hello otra clave [capacidades de red](../networking/networking-overview.md) de Azure.

