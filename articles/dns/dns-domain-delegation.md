---
title: "Introducción a la delegación DNS aaaAzure | Documentos de Microsoft"
description: "Comprender cómo toochange delegación del dominio y el uso de DNS de Azure nombre servidores tooprovide dominio hospeda."
services: dns
documentationcenter: na
author: georgewallace
manager: timlt
ms.assetid: 257da6ec-d6e2-4b6f-ad76-ee2dde4efbcc
ms.service: dns
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 04/12/2017
ms.author: gwallace
ms.openlocfilehash: eaf2d2e345004b4d631e8d81d548b8ca23277d05
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="delegation-of-dns-zones-with-azure-dns"></a>Delegación de zonas DNS con Azure DNS

DNS de Azure permite toohost una zona DNS y administrar los registros DNS de Hola para un dominio de Azure. En el orden de las consultas DNS para un tooreach de dominio DNS de Azure, el dominio de hello tiene toobe delegar tooAzure DNS de dominio primario de Hola. Tenga en cuenta el DNS de Azure no es un registrador de dominios de Hola. Este artículo se explica cómo funciona la delegación de dominio y cómo toodelegate tooAzure de dominios DNS.

## <a name="how-dns-delegation-works"></a>Funcionamiento de la delegación de DNS

### <a name="domains-and-zones"></a>Dominios y zonas

Hola sistema de nombres de dominio es una jerarquía de dominios. jerarquía de Hola se inicia en el dominio de 'raíz' hello, cuyo nombre es simplemente '**.**'.  Después de él, se encuentran los dominios de primer nivel, a saber, “com”, “net”, “org”, “uk” o “jp”.  A continuación, se colocan los dominios de segundo nivel, como “org.uk” o “co.jp”.  y así sucesivamente. dominios de Hola Hola jerarquía DNS se hospedan mediante zonas DNS independientes. Estas zonas se distribuyen globalmente hospedadas por servidores de nombres DNS alrededor de Hola a todos.

**Zona DNS** -un dominio es un nombre único en el sistema de nombres de dominio, por ejemplo, "contoso.com" Hola. Una zona DNS es toohost usado Hola registros DNS para un dominio en particular. Por ejemplo, el dominio de hello 'contoso.com' puede contener varios registros DNS como 'mail.contoso.com' (para un servidor de correo electrónico) y 'www.contoso.com' (para un sitio Web).

**Registrador de dominios**: un registrador de dominios es una empresa que puede ofrecer nombres de dominio de Internet. Comprueban si el dominio de Internet Hola desea toouse esté disponible y que le permiten toopurchase lo. Una vez que se registra el nombre de dominio de hello, son propietario legal de Hola Hola nombre de dominio. Si ya tiene un dominio de Internet, que usa Hola actual dominio registrador toodelegate tooAzure DNS.

toofind más información acerca del propietario de un nombre de dominio determinado, o para obtener información acerca de cómo toobuy un dominio, consulte [administración de dominios de Internet en Azure AD](https://msdn.microsoft.com/library/azure/hh969248.aspx).

### <a name="resolution-and-delegation"></a>Resolución y delegación

Existen dos tipos de servidores DNS:

* Un servidor DNS *autoritativo* hospeda zonas DNS. Solo responde a las consultas DNS de los registros de dichas zonas.
* Un servidor DNS *recursivo* no hospeda zonas DNS. Responde a todas las consultas DNS mediante una llamada a datos DNS autorizados servidores toogather Hola que necesita.

DNS de Azure proporciona un servicio DNS autoritativo.  No proporciona un servicio DNS recursivo. Servicios en la nube y máquinas virtuales en Azure son toouse configurada automáticamente un servicio DNS recursivas que se proporciona por separado como parte de la infraestructura de Azure. Para obtener información sobre cómo toochange esta configuración de DNS, consulte [resolución de nombres en Azure](../virtual-network/virtual-networks-name-resolution-for-vms-and-role-instances.md#name-resolution-using-your-own-dns-server).

Los clientes DNS de los equipos o dispositivos móviles normalmente llaman a un tooperform de servidor DNS recursivo hello las aplicaciones cliente tienen las consultas de DNS.

Cuando un servidor DNS recursivo recibe una consulta para un registro DNS como 'www.contoso.com', primero debe toofind Hola nombre hospedaje Hola zona del servidor de dominio de 'contoso.com' hello. servidor de nombres de hello toofind, empieza en servidores de nombres raíz de Hola y desde allí, busca servidores de nombres Hola donde se hospeda hello 'com' zona. A continuación, consulta hello 'com' nombre servidores toofind Hola servidores de nombres hospeda la zona de 'contoso.com' hello.  Por último, es capaz de tooquery estos servidores de nombres para 'www.contoso.com'.

Este procedimiento se denomina resolución de nombre DNS de Hola. En sentido estricto, resolución de DNS incluye pasos adicionales como CNAME siguiente, pero que no es importante toounderstanding cómo funciona la delegación DNS.

¿Cómo una zona principal 'punto' toohello servidores de nombres para una zona secundaria? Se consigue usando un tipo especial de registro DNS, denominado registro NS (NS, por sus siglas en inglés, significa “servidor de nombres”). Por ejemplo, zona de raíz de hello contiene registros NS para 'com' y muestra los servidores de nombres de Hola para zona de hello 'com'. A su vez, hello 'com' zona contiene los registros NS para "contoso.com", que se muestra en los servidores de nombres de Hola para zona de 'contoso.com' hello. Configurar registros de NS de Hola para una zona secundaria en una zona principal se denomina delegación de Hola de dominio.

Hola siguiente imagen muestra un ejemplo de consulta DNS. Partners.contoso.NET y contoso.net Hola son las zonas DNS de Azure.

![Dns-nameserver](./media/dns-domain-delegation/image1.png)

1. Hola las solicitudes de cliente `www.partners.contoso.net` desde su servidor DNS local.
1. servidor DNS local de Hello no tiene el registro de hello por lo que tiene un servidor de nombres raíz de solicitud tootheir.
1. servidor de nombres raíz de Hello no tiene el registro de hello, pero conoce dirección Hola de hello `.net` servidor de nombres, proporciona ese servidor DNS de toohello de dirección
1. Hola DNS envía Hola solicitud toohello `.net` servidor de nombres, no tiene registro de hello pero no conoce Hola Hola contoso.net del servidor de nombres. En este caso es una zona DNS hospedada en Azure DNS.
1. zona de Hello `contoso.net` no tiene el registro de hello pero sabe el servidor de nombres de Hola para `partners.contoso.net` y responde con el. En este caso es una zona DNS hospedada en Azure DNS.
1. servidor DNS de Hello solicita la dirección IP de Hola de `partners.contoso.net` de hello `partners.contoso.net` zona. Contiene un registro de hello y responde con la dirección IP de Hola.
1. servidor DNS de Hello proporciona Hola IP dirección toohello de cliente
1. sitio Web de toohello conecta el cliente de Hello `www.partners.contoso.net`.

Cada delegación realmente tiene dos copias de los registros NS Hola; uno en zona primaria de Hola que señala al toohello secundarios y otra en la zona secundaria de hello propio. zona de 'contoso.net' Hello contiene registros de hello NS para 'contoso.net' (en los registros de NS de suma toohello en "red"). Estos registros se denominan registros NS autoritativos y se sitúan en vértice Hola de zona secundaria de Hola.

## <a name="next-steps"></a>Pasos siguientes

Obtenga información acerca de cómo demasiado[delegar su tooAzure de dominio DNS](dns-delegate-domain-azure-dns.md)

