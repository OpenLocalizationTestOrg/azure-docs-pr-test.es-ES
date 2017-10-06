---
title: aaaOverview de DNS inversa en Azure | Documentos de Microsoft
description: "Aprenda cómo funciona DNS inverso y cómo se puede usar en Azure"
services: dns
documentationcenter: na
author: jtuliani
manager: timlt
ms.service: dns
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 05/29/2017
ms.author: jonatul
ms.openlocfilehash: 687663fb83469ab8e696bb714649d0856915bad6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="overview-of-reverse-dns-and-support-in-azure"></a>Introducción a DNS inverso y compatibilidad en Azure

Este artículo proporciona información general sobre cómo inversa DNS funciona, hello y escenarios de DNS inversos se admite en Azure.

## <a name="what-is-reverse-dns"></a>¿Qué es un DNS inverso?

Los registros DNS convencionales habilitar una asignación de una dirección IP de DNS nombre (como 'www.contoso.com') tooan (por ejemplo, 64.4.6.100).  DNS inversa habilita la traducción de hello un IP (64.4.6.100) tooa atrás del nombre de dirección ('www.contoso.com').

Los registros de DNS inversos se utilizan en distintas situaciones, entre ellas, en la validación de servidores y en la autenticación de solicitudes de servidor. Por ejemplo, los registros DNS inversos se utilizan ampliamente para combatir el correo basura comprobando remitente Hola de un mensaje de correo electrónico.  recupera del servidor de correo electrónico receptor de Hola Hola registro DNS inverso de hello enviar la dirección IP del servidor y comprueba si el host que origina toosend autorizados por correo electrónico de hello dominio. 

## <a name="how-reverse-dns-works"></a>Cómo funciona un DNS inverso

Los registros de DNS inverso se hospedan en zonas DNS especiales conocidas como zonas “ARPA”.  Estas zonas forman una jerarquía DNS independiente en paralelo con jerarquía normal Hola hospedaje de dominios como "contoso.com".

Por ejemplo, hello 'www.contoso.com' del registro de DNS se implementa mediante un registro DNS 'A' con el nombre de Hola "www" en la zona de Hola "contoso.com".  Este registro señala la dirección IP toohello correspondiente, en este caso 64.4.6.100.  búsqueda inversa de Hola se implementa por separado, usando un registro de 'PTR' denominado '100' en la zona de hello '6.4.64.in-addr.arpa' (tenga en cuenta que las direcciones IP se invierten en las zonas ARPA.)  Este registro PTR, si se ha configurado correctamente, señala toohello nombre 'www.contoso.com'.

Cuando una organización se le asigna un bloque de direcciones IP, adquieren zona hello toomanage derecho Hola correspondiente ARPA. Hola zonas ARPA correspondiente de la dirección IP de toohello bloques uso Azure hospedados y administrados por Microsoft. Su ISP puede hospedar la zona ARPA Hola para sus propias direcciones IP automáticamente, o puede permitir host tooyou zona ARPA de hello en un servicio DNS de su elección, como DNS de Azure.

> [!NOTE]
> Las búsquedas DNS directas e inversas se implementan en jerarquías de DNS independientes y paralelas. Hola de búsqueda inversa para 'www.contoso.com' es **no** hospedado en la zona de hello 'contoso.com', en su lugar se hospeda en zona ARPA hello para el bloque de direcciones IP correspondiente Hola. Se utilizan zonas independientes para los bloques de direcciones IPv4 e IPv6.

### <a name="ipv4"></a>IPv4

Hola nombre de una zona de búsqueda inversa IPv4 debe ser Hola siguiendo el formato: `<IPv4 network prefix in reverse order>.in-addr.arpa`.

Por ejemplo, al crear una zona inversa toohost registros para hosts con direcciones IP que están en el prefijo de hello 192.0.2.0/24, nombre de la zona de Hola se crearían aislar el prefijo de red de Hola de dirección de hello (192.0.2) y, a continuación, invertir orden hello (2.0.192) y agregar Hola sufijo `.in-addr.arpa`.

|Clase de subred|Prefijo de red  |Prefijo de red invertido  |Sufijo estándar  |Nombre de zona inversa |
|-------|----------------|------------|-----------------|---------------------------|
|Clase A|203.0.0.0/8     | 203        | .in-addr.arpa   | `203.in-addr.arpa`        |
|Clase B|198.51.0.0/16   | 51.198     | .in-addr.arpa   | `51.198.in-addr.arpa`     |
|Clase C|192.0.2.0/24    | 2.0.192    | .in-addr.arpa   | `2.0.192.in-addr.arpa`    |

### <a name="classless-ipv4-delegation"></a>Delegación IPv4 sin clases

En algunos casos, el intervalo IP de hello asignada tooan organización es menor que una clase de C (/ 24) intervalo. En este caso, el intervalo IP de hello no está en un límite de la zona en hello `.in-addr.arpa` jerarquía de la zona y, por lo tanto, no se puede delegar como una zona secundaria.

En su lugar, se utiliza un mecanismo diferente tooa dedicado de la zona DNS de registros de control de tootransfer de búsqueda inversa individual (PTR). Este mecanismo delega una zona secundaria para cada intervalo de IP y, a continuación, se asigna cada dirección IP en hello individualmente intervalo toothat zona de secundaria mediante registros CNAME.

Por ejemplo, suponga que una organización se le concede Hola IP intervalo 192.0.2.128/26 por su ISP. Esto representa 64 direcciones IP, de 192.0.2.128 too192.0.2.191. El DNS inverso de este intervalo se implementa del modo siguiente:
- organización de Hello crea una zona de búsqueda inversa denominada 128-26.2.0.192.in-addr.arpa. prefijo de Hello ' 128-26' representa Hola red segmento asignado toohello organización dentro de Hola clase C (/ 24) intervalo.
- Hola ISP crea tooset de registros NS seguridad Hola delegación DNS para hello por encima de la zona de la zona primaria de clase C de Hola. También crea los registros CNAME en la zona de búsqueda inversa de hello primaria (clase C), asignación de cada dirección IP de hello IP intervalo toohello nueva zona creada por la organización de hello:

```
$ORIGIN 2.0.192.in-addr.arpa
; Delegate child zone
128-26    NS       <name server 1 for 128-26.2.0.192.in-addr.arpa>
128-26    NS       <name server 2 for 128-26.2.0.192.in-addr.arpa>
; CNAME records for each IP address
129       CNAME    129.128-26.2.0.192.in-addr.arpa
130       CNAME    130.128-26.2.0.192.in-addr.arpa
131       CNAME    131.128-26.2.0.192.in-addr.arpa
; etc
```
- a continuación, Hola organización administra los registros PTR de hello individuales dentro de su zona secundaria.

```
$ORIGIN 128-26.2.0.192.in-addr.arpa
; PTR records for each UIP address. Names match CNAME targets in parent zone
129      PTR    www.contoso.com
130      PTR    mail.contoso.com
131      PTR    partners.contoso.com
; etc
```
Una búsqueda inversa para consultas de '192.0.2.129' de la dirección IP de Hola para un registro PTR denominado '129.2.0.192.in-addr.arpa'. Esta consulta se resuelve a través de hello CNAME en registro Hola principal zona toohello PTR en zona secundaria de Hola.

### <a name="ipv6"></a>IPv6

nombre de Hola de una zona de búsqueda inversa IPv6 debe ser Hola siguiente forma:`<IPv6 network prefix in reverse order>.ip6.arpa`

Por ejemplo: Al crear una zona inversa toohost registros para hosts con direcciones IP que están en hello 2001:db8:1000:abdc:: / 64 prefijo, nombre de la zona de Hola se crearían aislar el prefijo de red de Hola de dirección de hello (2001:db8:abdc::). A continuación expanda tooremove de prefijo de red IPv6 hello [compresión de ceros](https://technet.microsoft.com/library/cc781672(v=ws.10).aspx), si es un prefijo de dirección de hello IPv6 tooshorten usado (2001:0db8:abdc:0000::). Invertir orden hello, con un punto como delimitador entre cada número hexadecimal de prefijo de Hola de Hola, hello toobuild invertir el prefijo de red (`0.0.0.0.c.d.b.a.8.b.d.0.1.0.0.2`) y agregue el sufijo de hello `.ip6.arpa`.


|Prefijo de red  |Prefijo de red expandido e invertido |Sufijo estándar |Nombre de zona inversa  |
|---------|---------|---------|---------|
|2001:db8:abdc::/64    | 0.0.0.0.c.d.b.a.8.b.d.0.1.0.0.2        | .ip6.arpa        | `0.0.0.0.c.d.b.a.8.b.d.0.1.0.0.2.ip6.arpa`       |
|2001:db8:1000:9102::/64    | 2.0.1.9.0.0.0.1.8.b.d.0.1.0.0.2        | .ip6.arpa        | `2.0.1.9.0.0.0.1.8.b.d.0.1.0.0.2.ip6.arpa`        |


## <a name="azure-support-for-reverse-dns"></a>Soporte técnico de Azure para DNS inverso

Azure admite dos escenarios independientes relacionadas con tooreverse DNS:

**Hospedaje Hola búsqueda inversa zona correspondiente tooyour bloque de direcciones IP.**
DNS de Azure puede utilizarse demasiado[hospedar las zonas de búsqueda inversa y administrar los registros PTR de Hola para cada búsqueda DNS inversa](dns-reverse-dns-hosting.md), para IPv4 e IPv6.  Hola el proceso de creación de la zona de búsqueda inversa (ARPA) de hello, configurar la delegación de hello, y configurar PTR registros es Hola igual que para las zonas DNS normales.  Hello solo diferencias son que Hola delegación debe configurarse a través de su ISP en lugar de su registrador DNS, y debe utilizarse solo Hola tipo de registro PTR.

**Configurar el registro DNS inversa de hello para la dirección IP de hello asignado tooyour servicio de Azure.** Azure permite demasiado[configurar la búsqueda inversa de Hola para direcciones IP que Hola asignan tooyour servicio de Azure](dns-reverse-dns-for-azure-services.md).  Esta búsqueda inversa está configurada de Azure como un registro PTR en la zona de hello correspondiente ARPA.  Estas zonas ARPA, correspondiente intervalos IP tooall Hola que utilizan Azure, están hospedadas por Microsoft

## <a name="next-steps"></a>Pasos siguientes

Para más información sobre los registros de DNS inverso, consulte información sobre la [búsqueda de DNS inverso en Wikipedia](http://en.wikipedia.org/wiki/Reverse_DNS_lookup).
<br>
Obtenga información acerca de cómo demasiado[zona de búsqueda inversa de Hola de host para el intervalo IP asignada por el ISP en DNS de Azure](dns-reverse-dns-for-azure-services.md).
<br>
Obtenga información acerca de cómo demasiado[administrar registros de DNS inverso para los servicios de Azure](dns-reverse-dns-for-azure-services.md).

