---
title: "aaaDNS zonas y registros de información general - DNS de Azure | Documentos de Microsoft"
description: "Información general de soporte técnico para hospedar registros y zonas DNS en DNS de Microsoft Azure."
services: dns
documentationcenter: na
author: jtuliani
manager: carmonm
editor: 
ms.assetid: be4580d7-aa1b-4b6b-89a3-0991c0cda897
ms.service: dns
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.custom: H1Hack27Feb2017
ms.workload: infrastructure-services
ms.date: 12/05/2016
ms.author: jonatul
ms.openlocfilehash: f214c3e2e810a80a000281820acd35f0aaf5a7e1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="overview-of-dns-zones-and-records"></a>Información general sobre zonas y registros de DNS

Esta página explica los conceptos clave de Hola de dominios, las zonas DNS, los registros DNS y conjuntos de registros, y cómo se admiten en DNS de Azure.

## <a name="domain-names"></a>Nombres de dominio

Hola sistema de nombres de dominio es una jerarquía de dominios. jerarquía de Hola se inicia en el dominio de 'raíz' hello, cuyo nombre es simplemente '**.**'.  Después de él, se encuentran los dominios de primer nivel, a saber, “com”, “net”, “org”, “uk” o “jp”.  A continuación, se colocan los dominios de segundo nivel, como “org.uk” o “co.jp”. dominios de Hello en jerarquía DNS de hello globalmente se distribuyen, hospedadas por servidores de nombres DNS alrededor de Hola a todos.

Un registrador de nombres de dominio es una organización que le permite toopurchase un nombre de dominio, por ejemplo, "contoso.com".  Adquirir un dominio da nombre Hola jerarquía DNS de hello toocontrol derecha bajo ese nombre, por ejemplo, lo que el sitio web de empresa de toodirect nombre hello 'www.contoso.com' tooyour. registrador de Hello puede dominio hello en sus propios servidores de nombres en su nombre de host o permitir que a los servidores de nombres alternativos de toospecify.

DNS de Azure proporciona una infraestructura de servidor de nombres distribuidos globalmente, alta disponibilidad, que puede usar toohost en su dominio. Mediante el hospedaje de los dominios de DNS de Azure, puede administrar los registros DNS con hello mismas credenciales, API, herramientas, facturación y soporte a medida que los servicios de Azure.

DNS de Azure actualmente no admite la adquisición de nombres de dominio. Si desea que toopurchase un nombre de dominio, deberá toouse un registrador de nombres de dominio de otro fabricante. registrador de Hello suelen cobra una pequeña cuota anual. dominios de Hello, a continuación, se pueden hospedar en DNS de Azure para la administración de registros DNS. Vea [delegar un tooAzure de dominio DNS](dns-domain-delegation.md) para obtener más información.

## <a name="dns-zones"></a>Zonas DNS

[!INCLUDE [dns-create-zone-about](../../includes/dns-create-zone-about-include.md)]

## <a name="dns-records"></a>Registros DNS

[!INCLUDE [dns-about-records-include](../../includes/dns-about-records-include.md)]

### <a name="time-to-live"></a>Período de vida

tiempo de Hello toolive o TTL, especifica cuánto tiempo cada registro se almacena en caché los clientes antes de que se va a volver a consultar. Hola ejemplo anterior, Hola TTL es 3600 segundos o 1 hora.

En DNS de Azure, Hola TTL se especifica para el conjunto de registros de hello, no para cada registro, por lo que se usa el mismo valor para todas las entradas de registro de hello establecido.  Se puede especificar cualquier valor TTL entre 1 y 2 147 483 647 segundos.

### <a name="wildcard-records"></a>Registros de carácter comodín

DNS de Azure admite [registros de carácter comodín](https://en.wikipedia.org/wiki/Wildcard_DNS_record). Registros de carácter comodín se devuelven como consulta de tooany de respuesta con un nombre coincidente (a menos que haya una coincidencia más próxima de un conjunto de registros no comodín). Azure DNS admite los conjuntos de registros de carácter comodín para todos los tipos de registros, excepto NS y SOA.

toocreate un registro de comodín establecido, utilice el nombre de conjunto de registros de hello '\*'. Como alternativa, también puede utilizar un nombre con "\*" como su etiqueta a la izquierda, por ejemplo,"\*.foo".

### <a name="cname-records"></a>Registros CNAME

Conjuntos de registros CNAME no pueden coexistir con otros conjuntos de registros con hello mismo nombre. Por ejemplo, no se puede crear un conjunto con nombre relativo de hello 'www' de registros CNAME y una A grabar con nombre relativo hello 'www' en hello mismo tiempo.

Dado que vértice de la zona de hello (nombre = ' @') siempre contiene el registro SOA y NS de hello conjuntos que se crearon cuando se creó la zona de hello, no se puede crear un registro CNAME establecido en vértice de la zona de Hola.

Estas restricciones surjan de los estándares DNS de hello y no son limitaciones de DNS de Azure.

### <a name="ns-records"></a>Registros NS

registro de Hello NS establecer en vértice de la zona de hello (nombre ' @') se crea automáticamente con cada zona DNS y se elimina automáticamente cuando se elimina la zona de hello (no se puede eliminar por separado).

Este conjunto de registros contiene nombres de Hola de zona de hello Azure DNS nombre servidores toohello asignado. Puede agregar nombre adicionales servidores toothis NS conjunto de registros, toosupport alojar conjuntamente dominios con más de un proveedor DNS. También puede modificar Hola TTL y los metadatos para este conjunto de registros. Sin embargo, no se puede quitar o modificar servidores de nombres DNS de Azure previamente rellenados Hola. 

Tenga en cuenta que esto se aplica solo toohello NS conjunto de registros en vértice de la zona de Hola. Otros conjuntos de registros NS en su zona (como las zonas secundarias de toodelegate usado) pueden creados, modificados y eliminados sin restricción.

### <a name="soa-records"></a>Registros SOA

Un conjunto de registros SOA se crea automáticamente en vértice Hola de cada zona (nombre = ' @') y se elimina automáticamente cuando se elimina la zona de Hola.  Los registros SOA no pueden crearse ni eliminarse por separado.

Puede modificar todas las propiedades del registro SOA de hello excepto la propiedad de 'host' hello, que está preconfigurado toorefer toohello principal nombre del servidor DNS de Azure proporcionada.

### <a name="spf-records"></a>Registros SPF

[!INCLUDE [dns-spf-include](../../includes/dns-spf-include.md)]

### <a name="srv-records"></a>Registros SRV

[Los registros SRV](https://en.wikipedia.org/wiki/SRV_record) usan varias ubicaciones de servidor de servicios toospecify. Al especificar un registro SRV en DNS de Azure:

* Hola *servicio* y *protocolo* debe ser especificada como parte del nombre de conjunto de registros de hello, el prefijo de subrayado.  Por ejemplo, "\_sip.\_tcp.name".  Para un registro en vértice de la zona de hello, no hay ninguna necesidad de toospecify ' @' en nombre de registro de hello, basta con usar servicio de Hola y el protocolo, por ejemplo '\_sip.\_ TCP'.
* Hola *prioridad*, *peso*, *puerto*, y *destino* se especifican como parámetros de cada registro en el conjunto de registros de Hola.

### <a name="txt-records"></a>Registros TXT

Registros TXT son cadenas de texto de tooarbitrary de nombres de dominio de toomap usado. Se utilizan en varias aplicaciones, configuración de tooemail relacionados en concreto, como hello [marco de directivas de remitente (SPF)](https://en.wikipedia.org/wiki/Sender_Policy_Framework) y [correo identificado por claves de dominio (DKIM)](https://en.wikipedia.org/wiki/DomainKeys_Identified_Mail).

los estándares de DNS Hola permiten un único toocontain de registro TXT varias cadenas, cada una de ellas puede ser up too254 caracteres de longitud. Cuando se utilizan varias cadenas, se concatenan según los clientes y se tratan como una sola cadena.

Al llamar a Hola API de REST de DNS de Azure, debe toospecify cada cadena TXT por separado.  Al utilizar Hola portal de Azure, PowerShell o CLI interfaces debe especificar una sola cadena por cada registro, que automáticamente se divide en segmentos de 254 caracteres si es necesario.

Hola varias cadenas en un registro DNS no deben confundirse con Hola varios registros TXT en un conjunto de registros TXT.  Un conjunto de registros TXT puede contener varios registros, *cada uno de los cuales* puede contener varias cadenas.  DNS de Azure es compatible con una longitud de cadena total de los caracteres de too1024 en cada registro TXT establecido (a través de todos los registros combinados).

## <a name="tags-and-metadata"></a>Etiquetas y metadatos

### <a name="tags"></a>Etiquetas

Las etiquetas son una lista de pares nombre / valor y se utilizan por los recursos de Azure Resource Manager toolabel.  Administrador de recursos de Azure usa etiquetas tooenable filtrado vistas de la factura de Azure y también le permite tooset una directiva en las etiquetas que son necesarios. Para obtener más información acerca de las etiquetas, vea [mediante etiquetas tooorganize los recursos de Azure](../azure-resource-manager/resource-group-using-tags.md).

DNS de Azure admite el uso de etiquetas de Azure Resource Manager en recursos de zona DNS.  No admite etiquetas en conjuntos de registros de DNS, aunque, como alternativa, se admiten "metadatos" en estos tipos de conjuntos, como se explica a continuación.

### <a name="metadata"></a>Metadatos

Como una alternativa toorecord conjunto de etiquetas, DNS de Azure admite la anotación de conjuntos de registros mediante 'metadatos de '.  Tootags similar, metadatos permiten a tooassociate pares nombre / valor con cada conjunto de registros.  Esto puede ser útil, por ejemplo establezca propósito de hello toorecord de cada registro.  A diferencia de las etiquetas, los metadatos no pueden ser tooprovide usa una vista filtrada de la factura de Azure y no se puede especificar en una directiva de Azure Resource Manager.

## <a name="etags"></a>Etag

Suponga que dos personas o dos procesos intente toomodify un registro DNS en hello mismo tiempo. ¿Cuál gana? ¿Y ganador Hola sabe que han sobrescrito cambios creados por otra persona?

DNS de Azure usa Etags toohandle cambios simultáneos toohello mismo recurso de forma segura. Las etiquetas de entidad (ETag) son independientes de las ["etiquetas" de Azure Resource Manager](#tags). Cada recurso DNS (zona o conjunto de registros) tiene un valor de Etag asociado a él. Siempre que se recupera un recurso, también se recupera su Etag. Al actualizar un recurso, puede elegir volver toopass Hola Etag para que DNS de Azure pueda comprobar que Hola Etag en hello coincide con el servidor. Puesto que cada recurso de tooa actualización da como resultado Hola Etag que se va a volver a generar, un error de coincidencia de Etag indica que se ha producido un cambio simultáneo. ETags también puede utilizarse al crear un nuevo tooensure de recursos que ya no existe el recurso de Hola.

De manera predeterminada, PowerShell de DNS de Azure usa Etags tooblock cambios simultáneos toozones y conjuntos de registros. Hola opcional *-sobrescribir* conmutador puede ser utilizados toosuppress Etag comprobaciones, en cuyo caso cualquier simultáneas se sobrescriben los cambios que se han producido.

En el nivel de Hola de hello API de REST de DNS de Azure, Etags se especifican mediante encabezados HTTP.  Su comportamiento se expresa en hello en la tabla siguiente:

| Encabezado | Comportamiento |
| --- | --- |
| Ninguna |PUT always succeeds (no Etag checks) |
| If-match <etag> |PUT only succeeds if resource exists and Etag matches |
| If-match * |PUT only succeeds if resource exists |
| If-none-match * |PUT only succeeds if resource does not exist |


## <a name="limits"></a>límites

Hola siguiendo los límites predeterminados se aplica cuando se usa DNS de Azure:

[!INCLUDE [dns-limits](../../includes/dns-limits.md)]

## <a name="next-steps"></a>Pasos siguientes

* toostart mediante DNS de Azure, obtenga información acerca de cómo demasiado[crear una zona DNS](dns-getstarted-create-dnszone-portal.md) y [crear registros DNS](dns-getstarted-create-recordset-portal.md).
* toomigrate una zona DNS existente, obtenga información acerca de cómo demasiado[importar y exportar un archivo de zona DNS](dns-import-export.md).
