---
title: "Guía de solución de problemas de DNS aaaAzure | Documentos de Microsoft"
description: "¿Cómo se problemas comunes de tootroubleshoot con DNS de Azure"
services: dns
documentationcenter: na
author: jtuliani
manager: carmonm
editor: 
ms.assetid: 95b01dc3-ee69-4575-a259-4227131e4f9c
ms.service: dns
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 01/20/2017
ms.author: jonatul
ms.openlocfilehash: 944aa1811c980063f739268cd2c79b647b2754a4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="azure-dns-troubleshooting-guide"></a>Guía de solución de problemas de Azure DNS

Esta página proporciona información para solucionar problemas para preguntas que se plantean con frecuencia sobre Azure DNS.

Si estos pasos no resuelven el problema, también puede buscar o publicar su problema en nuestro [foro de soporte técnico de la comunidad en MSDN](https://social.msdn.microsoft.com/Forums/en-US/home?forum=WAVirtualMachinesVirtualNetwork). Como alternativa, abra una solicitud de soporte técnico de Azure.


## <a name="i-cant-create-a-dns-zone"></a>No puedo crear una zona DNS

tooresolve problemas comunes, pruebe uno o varios de hello pasos:

1.  Hola de revisión de auditoría DNS de Azure registra el motivo del error toodetermine Hola.
2.  Cada nombre de zona DNS debe ser único dentro de su grupo de recursos. Es decir, dos zonas DNS con hello igual nombre no puede compartir un grupo de recursos. Intente usar otro nombre de zona u otro grupo de recursos.
3.  Puede ver un error "Se ha alcanzado o superado el número máximo de Hola de zonas en la suscripción {Id. de suscripción}." Use una suscripción de Azure diferente, elimine algunas zonas o póngase en contacto con soporte técnico de Azure tooraise el límite de suscripción.
4.  Puede ver un error "zona de hello '{nombre de zona}' no está disponible." Este error significa que el DNS de Azure estaba servidores de nombres no se puede tooallocate para esta zona DNS. Pruebe a usar otro nombre de zona. O bien, si es propietario de nombre de dominio de hello, póngase en contacto con soporte técnico de Azure, que puede asignar servidores de nombres para usted.


### <a name="recommended-documents"></a>**Documentos recomendados**

[DNS zones and records](dns-zones-records.md)
 (Registros y zonas DNS)<br>
[Creación de una zona DNS](dns-getstarted-create-dnszone-portal.md)

## <a name="i-cant-create-a-dns-record"></a>No puedo crear un registro de DNS

tooresolve problemas comunes, pruebe uno o varios de hello pasos:

1.  Hola de revisión de auditoría DNS de Azure registra el motivo del error toodetermine Hola.
2.  ¿Existe ya conjunto de registros de hello?  DNS de Azure administra los registros mediante el registro *establece*, que son colección de Hola de registros de hello mismo nombre y Hola mismo tipo. Si un registro con hello mismo nombre y tipo ya existe, tooadd otro registro de dicho tipo debe modificar el registro existente de Hola establezca.
3.  ¿Estás tratando de toocreate un registro en el vértice (Hola 'raíz' de la zona de hello) de la zona DNS del Hola? Si es así, Hola convención DNS es toouse Hola ' @' carácter como nombre de registro de hello. Tenga en cuenta también que los estándares de DNS hello no permiten registros CNAME en vértice de la zona de Hola.
4.  ¿Tiene un conflicto de CNAME?  los estándares de DNS Hello no permiten un registro CNAME con el mismo nombre como un registro de cualquier otro tipo de Hola. Si tienes un CNAME existente, crear un registro con hello se produce un error en el mismo nombre de un tipo diferente.  Del mismo modo, crear un CNAME se produce un error si el nombre de hello coincide con un registro existente de un tipo diferente. Quitar conflicto Hola quitando Hola otro registro o elegir un nombre de registro diferente.
5.  ¿Ha alcanzado Hola Hola número límite de conjuntos de registros que se permiten en una zona DNS? establece el número actual de Hola de registro y hello número máximo de conjuntos de registros aparecen en el portal de Azure, en "Hello"propiedades"para zona de Hola Hola. Si se ha alcanzado este límite, a continuación, eliminar algunos conjuntos de registros o póngase en contacto con soporte técnico de Azure tooraise el límite de conjunto de registros para esta zona, vuelva a intentarlo. 


### <a name="recommended-documents"></a>**Documentos recomendados**

[DNS zones and records](dns-zones-records.md)
 (Registros y zonas DNS)<br>
[Creación de una zona DNS](dns-getstarted-create-dnszone-portal.md)



## <a name="i-cant-resolve-my-dns-record"></a>No puedo resolver mi registro de DNS

La resolución de nombres de DNS es un proceso de varios pasos que puede generar un error por diversos motivos. Hello pasos siguientes ayudarle a investigar por qué se producen errores en la resolución de DNS para un registro DNS en una zona alojada en DNS de Azure.

1.  Confirme que se hayan configurado correctamente los registros DNS de hello en DNS de Azure. Revise los registros DNS de Hola Hola portal de Azure, la comprobación de que el nombre de la zona de Hola, nombre del registro y tipo de registro son correctos.
2.  Confirme que los registros DNS de hello resuelven correctamente en servidores de nombres DNS de Azure Hola.
    - Si realiza las consultas DNS del equipo local, puede ver los resultados almacenados en caché que no reflejan el estado actual de Hola Hola de servidores de nombres.  Además, las redes corporativas suelen utilizar servidores de proxy DNS, que impiden las consultas DNS dirige toospecific servidores de nombres.  tooavoid estos problemas, utilice un servicio de resolución de nombres basado en web como [digwebinterface](http://digwebinterface.com).
    - Ser toospecify seguro de servidores de nombres correcta de hello para la zona DNS, como se muestra en hello portal de Azure.
    - Compruebe que el nombre DNS de hello es correcto (tiene toospecify Hola completo nombre, incluido el nombre de la zona de hello) y tipo de registro de hello es correcta
3.  Confirmar ese nombre de dominio DNS de hello ha sido correctamente [delegado servidores de nombres DNS de Azure toohello](dns-domain-delegation.md). Hay un [muchos sitios web de terceros que ofrecen la validación de la delegación de DNS](https://www.bing.com/search?q=dns+check+tool). Esta prueba es un *zona* prueba de delegación, por lo que sólo se deben escribir el nombre de zona del DNS de hello y no Hola registro nombre completo.
4.  Completada Hola anterior, el registro DNS debe resolver correctamente. tooverify, puede volver a usar [digwebinterface](http://digwebinterface.com), pero esta vez con la configuración de servidor de nombre de hello predeterminada.


### <a name="recommended-documents"></a>**Documentos recomendados**

[Delegar un tooAzure de dominio DNS](dns-domain-delegation.md)



## <a name="how-do-i-specify-hello-service-and-protocol-for-an-srv-record"></a>¿Cómo puedo especificar Hola "service" y "protocol" para un registro SRV?

DNS de Azure administra los registros DNS como conjuntos de registros: Hola colección de registros con hello mismo nombre y Hola mismo tipo. Para un conjunto de registros de SRV, Hola "service" y "protocol" necesitan toobe especificado como parte del nombre de conjunto de registros de Hola. Hello otros parámetros SRV ('priority', 'weight', 'puerto' y 'target') se especifican por separado para cada registro de conjunto de registros de Hola.

Ejemplo de nombres de registros SRV (nombre de servicio "sip", protocolo "tcp"):

- \_SIP. \_tcp (crea un conjunto en vértice de la zona de Hola de registros)
- \_sip.\_tcp.sipservice (crea un conjunto de registros con el nombre "sipservice")

### <a name="recommended-documents"></a>**Documentos recomendados**

[DNS zones and records](dns-zones-records.md)
 (Registros y zonas DNS)<br>
[Crear conjuntos de registros de DNS y los registros mediante Hola portal de Azure](dns-getstarted-create-recordset-portal.md)
<br>
[Tipo de registro SRV (Wikipedia)](https://en.wikipedia.org/wiki/SRV_record)


## <a name="next-steps"></a>Pasos siguientes

* Más información sobre [Registros y zonas DNS](dns-zones-records.md)
* toostart mediante DNS de Azure, obtenga información acerca de cómo demasiado[crear una zona DNS](dns-getstarted-create-dnszone-portal.md) y [crear registros DNS](dns-getstarted-create-recordset-portal.md).
* toomigrate una zona DNS existente, obtenga información acerca de cómo demasiado[importar y exportar un archivo de zona DNS](dns-import-export.md).

