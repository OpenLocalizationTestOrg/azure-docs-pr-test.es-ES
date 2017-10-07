---
title: "Introducción a las conexiones aaaHybrid | Documentos de Microsoft"
description: "Obtenga información acerca de las conexiones híbridas, la seguridad, los puertos TCP y las configuraciones admitidas. MABS, WABS."
services: biztalk-services
documentationcenter: 
author: MandiOhlinger
manager: erikre
editor: 
ms.assetid: 216e4927-6863-46e7-aa7c-77fec575c8a6
ms.service: biztalk-services
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 10/18/2016
ms.author: ccompy
ms.openlocfilehash: f092c6019aae761e1e73f13d1af8446a896515c2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="hybrid-connections-overview"></a>Introducción a las conexiones híbridas

> [!IMPORTANT]
> Las Conexiones híbridas de BizTalk se han retirado y se han reemplazado por las Conexiones híbridas de App Service. Para obtener más información, incluido cómo toomanage las conexiones de híbrida de BizTalk existente, vea [las conexiones híbridas de servicio de aplicación de Azure](../app-service/app-service-hybrid-connections.md).

Introducción tooHybrid las conexiones, se enumeran las configuraciones de hello admite y listas Hola puertos TCP necesarios.

## <a name="what-is-a-hybrid-connection"></a>¿Qué es una conexión híbrida?
Las conexiones híbridas son una característica de los servicios de BizTalk de Azure: Las conexiones híbridas proporcionan una característica de las aplicaciones Web de forma sencilla y cómoda tooconnect hello en el servicio de aplicación de Azure (anteriormente sitios Web) y la característica de aplicaciones móviles de hello en recursos de tooon locales de servicio de aplicaciones de Azure (anteriormente Servicios móviles) detrás del firewall.

![conexiones híbridas][HCImage]

Las ventajas de las conexiones híbridas incluyen:

* Las Aplicaciones web y las Aplicaciones móviles pueden acceder a los datos y servicios locales existentes de forma segura.
* Varias aplicaciones Web o aplicaciones móviles pueden compartir un tooaccess de conexión híbrida un recurso local.
* Puertos TCP mínimo son tooaccess requiere la red.
* Las aplicaciones que usan las conexiones híbridas acceder solo recurso de local específico de Hola que se publica a través de hello conexión híbrida.
* Puede conectar el recurso local de tooany que usa un puerto TCP estático, como SQL Server, MySQL, las API Web de HTTP y mayoría de los servicios Web personalizados.
  
  > [!NOTE]
  > Los servicios basados en TCP que usan puertos dinámicos (como modo pasivo FTP o modo pasivo extendido) no se admiten actualmente. Tampoco se admite LDAP. LDAP utiliza un puerto TCP estático, pero también podría usar UDP. Como resultado, no se admite.
  > 
  > 
* Se pueden usar con todos los marcos compatibles con Aplicaciones web (.NET, PHP, Java, Python, Node.js) y Aplicaciones móviles (Node.js, .NET).
* Las aplicaciones Web y aplicaciones móviles que pueden tener acceso a recursos locales en hello exactamente igual manera que si hello Web o aplicación móvil se encuentra en la red local. Hola, por ejemplo, la misma cadena de conexión también se puede usar usar de forma local en Azure.

Conexiones híbridas también proporcionan a los administradores de empresa con un control y visibilidad de los recursos corporativos Hola acceso a aplicaciones híbridas, incluidos:

* Configuración de directiva de grupo, los administradores pueden permitir que las conexiones híbridas de red de Hola y designar recursos que pueden tener acceso a aplicaciones híbridas.
* Registros de eventos y auditoría en la red corporativa de hello proporcionan visibilidad de los recursos de hello accede al conexiones híbridas.

## <a name="example-scenarios"></a>Escenarios de ejemplo
Las conexiones híbridas admiten Hola siguientes combinaciones de framework y aplicaciones:

* .NET framework acceso tooSQL Server
* Servicios de .NET framework acceso tooHTTP/HTTPS con WebClient
* PHP acceso tooSQL Server, MySQL
* TooSQL de acceso de Java Server, MySQL y Oracle
* Servicios de tooHTTP/HTTPS de acceso de Java

Al usar conexiones híbridas tooaccess en SQL Server local, tenga en cuenta Hola siguiente:

* SQL Express denominada las instancias deben ser puertos estáticos toouse configurado. De forma predeterminada, las instancias con nombre de SQL Express usan puertos dinámicos.
* Las instancias predeterminadas de SQL Express usan un puerto estático, pero TCP debe estar habilitado. De forma predeterminada, TCP no está habilitado.
* Cuando se usa la agrupación en clústeres o grupos de disponibilidad, Hola `MultiSubnetFailover=true` modo no se admite actualmente.
* Hola `ApplicationIntent=ReadOnly` no se admite actualmente.
* Autenticación de SQL puede ser necesaria como método de autorización to-end de hello compatible con hello aplicación de Azure y SQL server de hello en local.

## <a name="security-and-ports"></a>Seguridad y puertos
Las conexiones híbridas usan conexiones de Hola de toosecure de autorización de firma de acceso compartido (SAS) de hello Azure hello y aplicaciones locales conexión de administrador de conexiones híbridas toohello híbrida. Se crean claves de conexión independiente para la aplicación hello y Hola Administrador de conexiones híbridas local. Estas claves de conexión se pueden sustituir y revocar de manera independiente.

Proporcionan las conexiones híbridas para una distribución segura y sin problemas de aplicaciones de toohello de claves de Hola y Hola Administrador de conexiones híbridas local.

Consulte [Creación y administración de conexiones híbridas](integration-hybrid-connection-create-manage.md).

*Autorización de la aplicación es independiente de hello conexión híbrida*. Se puede usar cualquier método de autorización adecuado. método de autorización de Hello depende de métodos de autorización to-end de hello admitidos a través de hello Azure en la nube y componentes locales de Hola. Por ejemplo, su aplicación de Azure accede a un servidor SQL local. En este escenario, autorización de SQL puede ser el método de autorización de hello es compatible-to-end.

#### <a name="tcp-ports"></a>Puertos TCP
Las conexiones híbridas requieren únicamente conectividad TCP o HTTP saliente de su red privada. No necesita tooopen los puertos del firewall o cambiar su tooallow de configuración de red perimetral cualquier conectividad entrante a la red.

las conexiones híbridas utiliza Hola siguientes puertos TCP:

| Port | Por qué es necesario |
| --- | --- |
| 9350 - 9354 |Estos puertos se usan para la transmisión de datos. Administrador de retransmisión de Bus de servicio de Hello las comprobaciones de puerto 9350 toodetermine si la conectividad TCP está disponible. Si lo está, asume que el puerto 9352 está también disponible. El tráfico de datos pasa por el puerto 9352. <br/><br/>Permitir conexiones salientes puertos toothese. |
| 5671 |Cuando se usa el puerto 9352 para el tráfico de datos, puerto 5671 se utiliza como canal de control de Hola. <br/><br/>Permitir conexiones salientes toothis puerto. |
| 80, 443 |Estos puertos se utilizan para algunos tooAzure de las solicitudes de datos. También, si los puertos 9352 y 5671 no son utilizables, *, a continuación,* los puertos 80 y 443 están puertos reserva Hola utilizados para canal de control de Hola y de transmisión de datos.<br/><br/>Permitir conexiones salientes puertos toothese. <br/><br/>**Tenga en cuenta** no resulta recomendable toouse estos como Hola reserva puertos en lugar de hello otros puertos TCP. Hola HTTP o WebSocket se utiliza como protocolo de hello en lugar de TCP nativo para los canales de datos. Podría provocar un rendimiento menor. |

## <a name="next-steps"></a>Pasos siguientes
[Create and manage Hybrid Connections](integration-hybrid-connection-create-manage.md)<br/>
[Conectar aplicaciones Web de Azure tooan recurso local](../app-service-web/web-sites-hybrid-connection-get-started.md)<br/>
[Conectar SQL Server local tooon desde una aplicación web de Azure](../app-service-web/web-sites-hybrid-connection-connect-on-premises-sql-server.md)<br/>

## <a name="see-also"></a>Otras referencias
[API REST para administrar los servicios de BizTalk en Microsoft Azure](http://msdn.microsoft.com/library/azure/dn232347.aspx)
[Servicios de BizTalk: gráfico de ediciones](biztalk-editions-feature-chart.md)<br/>
[Crear un Servicio de BizTalk mediante Azure Portal](biztalk-provision-services.md)<br/>
[Servicios de BizTalk: pestañas Panel, Monitor y Escala](biztalk-dashboard-monitor-scale-tabs.md)<br/>

[HCImage]: ./media/integration-hybrid-connection-overview/WABS_HybridConnectionImage.png
[HybridConnectionTab]: ./media/integration-hybrid-connection-overview/WABS_HybridConnectionTab.png
[HCOnPremSetup]: ./media/integration-hybrid-connection-overview/WABS_HybridConnectionOnPremSetup.png
[HCManageConnection]: ./media/integration-hybrid-connection-overview/WABS_HybridConnectionManageConn.png
