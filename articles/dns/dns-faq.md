---
title: "Preguntas más frecuentes de DNS aaaAzure | Documentos de Microsoft"
description: "Preguntas más frecuentes sobre DNS de Azure"
services: dns
documentationcenter: na
author: jtuliani
manager: timlt
editor: 
ms.service: dns
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 04/21/2017
ms.author: jonatul
ms.openlocfilehash: 55006e9d8b311f1e94678eb9d35ce3448b936488
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="azure-dns-faq"></a>Preguntas más frecuentes sobre DNS de Azure

## <a name="about-azure-dns"></a>Más información sobre DNS de Azure

### <a name="what-is-azure-dns"></a>¿Qué es Azure DNS?

Hola sistema de nombres de dominio o DNS, es responsable de traducir (o la resolución de) un sitio Web o servicio name tooits dirección IP. DNS de Azure es un servicio de hospedaje para los dominios DNS, que permite resolver nombres mediante la infraestructura de Microsoft Azure. Mediante el hospedaje de los dominios en Azure, puede administrar su DNS los registros mediante Hola mismas credenciales, API, herramientas y facturación como los servicios de Azure.

Los dominios DNS de DNS de Azure se hospedan en la red global de servidores de nombres DNS de Azure. Utilizamos difusión por proximidad de red para que cada consulta DNS se responde por servidor DNS más cercano disponible de Hola. Esto ofrece un rendimiento rápido y alta disponibilidad para el dominio.

Hola servicio DNS de Azure se basa en el Administrador de recursos de Azure. Como tal, se beneficia de características Resource Manager, como control de acceso basado en roles, registros de auditoría y bloqueo de recursos. Los dominios y los registros se pueden administrar a través de hello portal de Azure, cmdlets de PowerShell de Azure y Hola CLI de Azure entre plataformas. Las aplicaciones que requieren la administración automática de DNS pueden integrar con el servicio de Hola a través de hello REST API y SDK.

### <a name="how-much-does-azure-dns-cost"></a>¿Cuánto cuesta DNS de Azure?

modelo de facturación de Hello DNS de Azure se basa en el número de Hola de las zonas DNS hospedadas en DNS de Azure y el número de Hola de consultas DNS que reciben. Los descuentos se proporcionan en función del uso.

Para obtener más información, vea hello [DNS de Azure página de precios](https://azure.microsoft.com/pricing/details/dns/).

### <a name="what-is-hello-sla-for-azure-dns"></a>¿Qué es Hola SLA para DNS de Azure?

Se garantiza que las solicitudes DNS válidas recibirá una respuesta de al menos un servidor de nombres DNS de Azure al menos 99,99% de tiempo de Hola.

Para obtener más información, vea hello [página de SLA de DNS de Azure](https://azure.microsoft.com/support/legal/sla/dns).

### <a name="what-is-a-dns-zone-is-it-hello-same-as-a-dns-domain"></a>¿Qué es una "zona DNS"? ¿Es lo mismo Hola como un dominio DNS? 

Un dominio es un nombre único en el sistema de nombres de dominio de hello, por ejemplo, "contoso.com".

Una zona DNS es toohost usado Hola registros DNS para un dominio en particular. Por ejemplo, dominio hello 'contoso.com' puede contener varios registros DNS, como 'mail.contoso.com' (para un servidor de correo electrónico) y 'www.contoso.com' (para un sitio web). Estos estaría hospedados en la zona DNS de Hola "contoso.com".

Nombre de dominio es *solo un nombre de*, mientras que una zona DNS es un recurso de datos que contiene registros DNS de Hola para un nombre de dominio. DNS de Azure permite toohost una zona DNS y administrar los registros DNS de Hola para un dominio de Azure. También proporciona a servidores de nombres DNS tooanswer consultas DNS de Internet de Hola.

### <a name="do-i-need-toopurchase-a-dns-domain-name-toouse-azure-dns"></a>¿Necesito toopurchase un nombre de dominio DNS toouse DNS de Azure? 

No necesariamente.

No es necesario toopurchase una toohost de dominio una zona DNS de DNS de Azure. Puede crear una zona DNS en cualquier momento sin necesidad de poseer el nombre de dominio de Hola. Las consultas DNS para esta zona se resolverán solo si se dirigen servidores de nombres DNS de Azure toohello asignan toohello zona.

Se necesita el nombre de dominio de Hola de toopurchase si desea que toolink la zona DNS en jerarquía DNS global hello: Esto permite consultas desde cualquier lugar en hello world toofind la zona DNS de DNS y responder con los registros DNS.

## <a name="azure-dns-features"></a>Características de DNS de Azure

### <a name="does-azure-dns-support-dns-based-traffic-routing-or-endpoint-failover"></a>¿DNS de Azure admite la conmutación por error de puntos de conexión o el enrutamiento basados en DNS?

Azure Traffic Manager proporciona las características de conmutación por error de puntos de conexión y el enrutamiento de tráfico basados en DNS. Se trata de un servicio de Azure independiente que puede utilizarse junto con el DNS de Azure. Para obtener más información, vea hello [Introducción al administrador de tráfico](../traffic-manager/traffic-manager-overview.md).

DNS de Azure solo admite el hospedaje 'static' dominios DNS, donde cada consulta DNS para un determinado registro DNS siempre recibe Hola misma respuesta DNS.

### <a name="does-azure-dns-support-domain-name-registration"></a>¿DNS de Azure admite el registro de nombres de dominio?

No. DNS de Azure actualmente no admite la adquisición de nombres de dominio. Si desea toopurchase dominios, deberá toouse un registrador de nombres de dominio de otro fabricante. registrador de Hello suelen cobra una pequeña cuota anual. dominios de Hello, a continuación, se pueden hospedar en DNS de Azure para la administración de registros DNS. Vea [delegar un tooAzure de dominio DNS](dns-domain-delegation.md) para obtener más información.

Se trata de una característica sujeta a seguimiento en el trabajo pendiente. Puede usar nuestro sitio de comentarios demasiado[registrar su compatibilidad para esta característica](https://feedback.azure.com/forums/217313-networking/suggestions/4996615-azure-should-be-its-own-domain-registrar).

### <a name="does-azure-dns-support-private-domains"></a>¿DNS de Azure admite dominios "privados"?

No. DNS de Azure actualmente solo admite dominios accesibles desde Internet.

Se trata de una característica sujeta a seguimiento en el trabajo pendiente. Puede usar nuestro sitio de comentarios demasiado[registrar su compatibilidad para esta característica](https://feedback.azure.com/forums/217313-networking/suggestions/10737696-enable-split-dns-for-providing-both-public-and-int).

Para obtener información sobre las opciones de DNS internas de Azure, vea [Resolución de nombres para las máquinas virtuales e instancias de rol](../virtual-network/virtual-networks-name-resolution-for-vms-and-role-instances.md).

### <a name="does-azure-dns-support-dnssec"></a>¿DNS de Azure admite DNSSEC?

No. DNS de Azure no es compatible actualmente con DNSSEC.

Se trata de una característica sujeta a seguimiento en el trabajo pendiente. Puede usar nuestro sitio de comentarios demasiado[registrar su compatibilidad para esta característica](https://feedback.azure.com/forums/217313-networking/suggestions/13284393-azure-dns-needs-dnssec-support).

### <a name="does-azure-dns-support-zone-transfers-axfrixfr"></a>¿DNS de Azure admite las transferencias de zona (AXFR/IXFR)?

No. DNS de Azure no es compatible actualmente con las transferencias de zona. Las zonas DNS pueden ser [importado en DNS de Azure mediante Azure CLI hello](dns-import-export.md). Los registros DNS, a continuación, se pueden administrar a través de hello [portal de administración de DNS de Azure](dns-operations-recordsets-portal.md), nuestro [API de REST](https://docs.microsoft.com/powershell/module/azurerm.dns), [SDK](dns-sdk.md), [cmdlets de PowerShell](dns-operations-recordsets.md), o [ Herramienta CLI](dns-operations-recordsets-cli.md).

Se trata de una característica sujeta a seguimiento en el trabajo pendiente. Puede usar nuestro sitio de comentarios demasiado[registrar su compatibilidad para esta característica](https://feedback.azure.com/forums/217313-networking/suggestions/12925503-extend-azure-dns-to-support-zone-transfers-so-it-c).

### <a name="does-azure-dns-support-url-redirects"></a>¿DNS de Azure admite los redireccionamientos de dirección URL?

No. Servicios de redirección de direcciones URL no son realmente un servicio DNS - funcionan en el nivel HTTP de hello, en lugar de nivel de DNS de Hola. Algunos proveedores DNS toobundle un servicio de redireccionamiento de dirección URL como parte de su oferta general. Esto solo se admite actualmente en DNS de Azure.

Esta característica está sujeta a un seguimiento en el trabajo pendiente. Puede usar nuestro sitio de comentarios demasiado[registrar su compatibilidad para esta característica](https://feedback.azure.com/forums/217313-networking/suggestions/10109736-provide-a-301-permanent-redirect-service-for-ape).

## <a name="using-azure-dns"></a>Uso de DNS de Azure

### <a name="can-i-co-host-a-domain-using-azure-dns-and-another-dns-provider"></a>¿Puedo hospedar de forma conjunta un dominio con DNS de Azure y otro proveedor DNS?

Sí. DNS de Azure es compatible con dominios de hospedaje conjunto con otros servicios DNS.

toodo por lo tanto, necesitará registros de hello NS toomodify para dominio de hello (qué control qué proveedores reciben DNS consulta dominio hello) toopoint toohello servidores de nombres de ambos proveedores. Estos registros NS deben toobe modificado en 3 lugares: en el DNS de Azure, en Hola otro proveedor y en la zona primaria de hello (normalmente se configura a través de registrador de nombres de dominio de hello). Para más información sobre la delegación DNS, vea [Delegación de dominios DNS](dns-domain-delegation.md).

Además, debe tooensure que Hola registros de DNS Hola dominio están sincronizados entre ambos proveedores DNS. DNS de Azure no es compatible actualmente con las transferencias de zonas DNS. Necesita los registros DNS de toosynchronize mediante cualquier hello [portal de administración de DNS de Azure](dns-operations-recordsets-portal.md), nuestro [API de REST](https://docs.microsoft.com/powershell/module/azurerm.dns), [SDK](dns-sdk.md), [cmdlets de PowerShell](dns-operations-recordsets.md) , o [herramienta CLI](dns-operations-recordsets-cli.md).

### <a name="do-i-have-toodelegate-my-domain-tooall-4-azure-dns-name-servers"></a>¿Es necesario toodelegate Mis servidores de nombres de dominio tooall 4 DNS de Azure?

Sí. DNS de Azure asigna a 4 servidores de nombres de zona DNS tooeach, para el aislamiento de errores y mayor resistencia. tooqualify para Hola SLA de DNS de Azure, deberá toodelegate sus servidores de nombres de dominio tooall 4.

### <a name="what-are-hello-usage-limits-for-azure-dns"></a>¿Cuáles son los límites de uso de Hola para DNS de Azure?

Hola siguiendo los límites predeterminados se aplica cuando se usa DNS de Azure:

[!INCLUDE [dns-limits](../../includes/dns-limits.md)]

### <a name="can-i-move-an-azure-dns-zone-between-resource-groups-or-between-subscriptions"></a>¿Puedo mover una zona de Azure DNS entre los grupos de recursos o entre las suscripciones?

Sí. Las zonas DNS se pueden mover entre grupos de recursos o entre suscripciones.

No hay ningún impacto en las consultas de DNS al mover una zona DNS. servidores de nombres Hola asignados toohello zona permanecen Hola que iguales y las consultas DNS se procesan como normal a lo largo.

Para obtener más información e instrucciones sobre cómo toomove zonas DNS, consulte [mover tooa de recursos nuevo grupo de recursos o suscripción](../azure-resource-manager/resource-group-move-resources.md).

### <a name="how-long-does-it-take-for-dns-changes-tootake-effect"></a>¿Cuánto tarda para DNS cambios tootake efecto?

Nuevas zonas DNS y los registros DNS son normalmente refleja en servidores de nombres DNS de Azure de hello rápidamente, dentro de unos segundos.

Registros de cambios tooexisting DNS pueden tardar un poco más, pero todavía deben reflejarse en servidores de nombres DNS de Azure de hello en 60 segundos. En este caso, almacenamiento en caché DNS fuera de DNS de Azure (por los clientes DNS y a las resoluciones DNS recursivas) también puede afectar a Hola tiempo de un toobe de cambio DNS efectivo. Esta duración de la caché puede controlarse mediante la propiedad Time-To-Live (TTL) de Hola de cada conjunto de registros.

### <a name="how-can-i-protect-my-dns-zones-against-accidental-deletion"></a>¿Cómo puedo proteger mis zonas DNS contra una eliminación accidental?

DNS de Azure se administran con el Administrador de recursos de Azure y se benefician de hello, obtener acceso a características de control que Azure Resource Manager proporciona. Control de acceso basada en funciones puede ser usado toocontrol qué usuarios tienen acceso de lectura o escritura zonas tooDNS y conjuntos de registros. Bloqueos de recursos pueden ser tooprevent aplicada la modificación accidental o eliminación de las zonas DNS y los conjuntos de registros.

Para más información, vea [Protección de zonas y registros DNS](dns-protect-zones-recordsets.md).

### <a name="how-do-i-set-up-spf-records-in-azure-dns"></a>¿Cómo puedo configurar registros de SPF en Azure DNS?

[!INCLUDE [dns-spf-include](../../includes/dns-spf-include.md)]

### <a name="how-do-i-set-up-an-international-domain-name-idn-in-azure-dns"></a>¿Cómo puedo configurar un nombre de dominio internacional (IDN) en Azure DNS?

Los nombres de dominio internacionales (IDN) funcionan mediante la codificación de cada nombre DNS con "[punycode](https://en.wikipedia.org/wiki/Punycode)". Las consultas de DNS se realizan con estos nombres codificados mediante punycode.

Puede configurar los nombres de dominio internacionales (IDN) en DNS de Azure por el primer nombre de zona Hola convertir o toopunycode de nombre de conjunto de registros. Azure DNS no admite actualmente la conversión integrada hacia o desde punycode.

## <a name="next-steps"></a>Pasos siguientes

[Más información sobre Azure DNS](dns-overview.md)
<br>
[Más información sobre zonas y registros DNS](dns-zones-records.md)
<br>
[Introducción a Azure DNS](dns-getstarted-portal.md)

