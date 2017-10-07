---
title: aaaOverview de las copias de varios inquilinos termina con la puerta de enlace de aplicaciones de Azure | Documentos de Microsoft
description: "Esta página proporciona una visión general de soporte técnico de puerta de enlace de aplicación Hola para varios inquilinos back-ends."
documentationcenter: na
services: application-gateway
author: georgewallace
manager: timlt
editor: 
ms.service: application-gateway
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/26/2017
ms.author: gwallace
ms.openlocfilehash: b7da8c9c68e34bd83ad2b828fab62c00caea354a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="application-gateway-support-for-multi-tenant-back-ends"></a>Compatibilidad de Application Gateway con servidores back-end multiinquilino

Azure Application Gateway admite conjuntos de escalado de máquinas virtuales, interfaces de red, IP públicas/privadas o nombres de dominio completos (FQDN) como parte de sus grupos de servidores back-end. De forma predeterminada, puerta de enlace de aplicaciones no cambia el encabezado de host HTTP entrante de Hola desde el cliente de Hola y envía Hola encabezado inalterados toohello back-end. Hay muchos servicios como [aplicaciones Web de Azure](../app-service-web/app-service-web-overview.md) y [administración de API](../api-management/api-management-key-concepts.md) que forman una naturaleza multiempresa y se basan en un encabezado de host específico o SNI extensión tooresolve toohello punto de conexión correcto. Puerta de enlace de aplicaciones ahora admite la capacidad de Hola para usuarios toooverwrite Hola entrantes HTTP encabezado de host en función de la configuración de back-end HTTP de Hola. Esta funcionalidad permite la compatibilidad con servidores back-end multiinquilino, Azure Web Apps y API Management. Esta funcionalidad está disponible para saludo estándar y WAFS SKU. Multiempresa back end compatibilidad también funciona con escenarios SSL de tooend de final y la terminación SSL.

![escenario de aplicación web](./media/application-gateway-web-app-overview/scenario.png)

Hola de Hello capacidad toospecify una invalidación de host está definida en configuración de HTTP, y puede se aplicado tooany volver terminar grupo durante la creación de reglas. Varios inquilinos volver finaliza Hola de soporte técnico de invalidación de encabezado de host y la extensión SNI maneras siguientes.

1. tooa de nombre de host de Hello capacidad tooset Hola había corregido valor Hola opciones de configuración de HTTP. Esta funcionalidad garantiza que se invalida ese encabezado de host de hello toothis valor para todos los bloques de back-end de toohello tráfico donde se aplica la configuración de hello HTTP. Al usar final tooend SSL, se usa este nombre de host invalidado en hello extensión SNI. Esta función permite escenarios donde una granja de servidores del grupo back-end espera un encabezado de host que es diferente de encabezado de host de Hola entrantes del cliente.

2. nombre de host de Hola Hola capacidad tooderive de hello IP o FQDN de los miembros del grupo back-end Hola. Configuración de HTTP también proporciona un nombre de host de opción toopick Hola de nombre de dominio completo de un miembro del grupo back-end si ha configurado con el nombre de host de hello opción tooderive de un miembro del grupo back-end individuales. Cuando se usa final tooend SSL, este nombre de host se deriva de hello FQDN y se utiliza en hello extensión SNI. Esta función permite escenarios donde un grupo back-end puede tener dos o más servicios de PaaS de varios inquilinos como aplicaciones web de Azure y miembro de tooeach de encabezado de host de la solicitud de hello contiene el nombre de host de hello derivada su FQDN.

> [!NOTE]
> En ambos Hola anteriores casos Hola configuración sólo afecta a comportamiento de tráfico en vivo de hello y no el comportamiento de sondeo del estado de Hola. Las comprobaciones de personalizado ya toospecify de capacidad de Hola de compatibilidad con un encabezado de host en la configuración de sondeo de Hola. Sondeos personalizados también admiten ahora comportamiento del encabezado de host de hello capacidad tooderive Hola de configuración de HTTP de hello configurado actualmente. Esta configuración puede especificarse mediante hello `PickHostNameFromback endAddress` parámetro de configuración de sondeo de Hola. Para final tooend funcionalidad toowork, sondeo de Hola y la configuración de HTTP de hello deben configuración correcta de hello tooreflect modificado.

Con esta capacidad, los clientes especificar opciones de hello en la configuración de HTTP de Hola y personalizados comprobaciones de la configuración adecuada de toohello. Esta configuración, a continuación, se vincula una copia de seguridad y la escucha de tooa finalizan grupo mediante una regla.

## <a name="next-steps"></a>Pasos siguientes

Obtenga información acerca de cómo tooset de una puerta de enlace de la aplicación con una aplicación web como un back end miembro del grupo visitando: [configurar el servicio de aplicación web aplicaciones con puerta de enlace de aplicaciones](application-gateway-web-app-powershell.md)
