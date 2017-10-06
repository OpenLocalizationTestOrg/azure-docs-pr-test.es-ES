---
title: "aaa \"conexiones híbridas del servicio de aplicación de Azure | Documentos de Microsoft\""
description: "¿Cómo toocreate y el uso de recursos de tooaccess de conexiones híbridas en redes dispares"
services: app-service
documentationcenter: 
author: ccompy
manager: stefsch
editor: 
ms.assetid: 66774bde-13f5-45d0-9a70-4e9536a4f619
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/22/2017
ms.author: ccompy
ms.openlocfilehash: 61d58068ab0a7c803019e3f0e92bde4273d1a053
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="azure-app-service-hybrid-connections"></a>Hybrid Connections de Azure App Service #

## <a name="overview"></a>Información general ##

Las conexiones híbridas es un servicio en Azure así como una característica de hello servicio de aplicaciones de Azure.  Como un servicio tiene uso y capacidades más allá de aquellas que se aprovechan en hello servicio de aplicaciones de Azure.  más información acerca de las conexiones híbridas y su uso fuera de hello en este caso, puede iniciar el servicio de aplicaciones de Azure toolearn [las conexiones híbridas de retransmisión de Azure][HCService]

Dentro de hello servicio de aplicaciones de Azure, las conexiones híbridas pueden ser tooaccess usa recursos de la aplicación en otras redes. Proporciona acceso desde el punto de conexión de aplicación de tooan de aplicación.  No habilita una funcionalidad alternativa tooaccess la aplicación.  Dado que se utiliza en hello servicio de aplicaciones, cada conexión híbrida correlaciona tooa combinación única de TCP host y puerto.  Esto significa que ese extremo de conexión híbrida Hola puede en cualquier sistema operativo y cualquier aplicación proporcionarse que está alcanzando un puerto de escucha TCP. Las conexiones híbridas no conoce ni qué protocolo de aplicación hello es o tiene acceso.  Simplemente ofrece acceso a la red.  


## <a name="how-it-works"></a>Cómo funciona ##
característica de las conexiones de Hello híbrida consta de dos llamadas salientes tooService retransmisión de Bus.  Hay una conexión desde una biblioteca en el host de Hola donde se ejecuta la aplicación de servicio de aplicaciones de hello y, a continuación, hay una conexión de retransmisión de Bus de hello híbrida conexión Manager(HCM) tooService.  Hola gestión es un servicio de retransmisión que se implementa dentro de hospedaje de red de Hola 

A través de hello dos conexiones unido a la aplicación tiene un tooa de túnel TCP corregido combinación de host: puerto en hello otro lado de hello gestión.  conexión de Hello usa TLS 1.2 para la seguridad y las claves SAS para la autenticación/autorización.    

![][1]

Cuando la aplicación realiza una solicitud DNS que coincida con un punto de conexión de la conexión híbrida configurar, a continuación, el tráfico TCP saliente Hola se redirigirán hacia abajo de la conexión híbrida de Hola.  

> [!NOTE]
> Esto significa que debe intentar tooalways use un nombre DNS para la conexión híbrida.  Algunos programas de software de cliente no lleva a cabo una búsqueda de DNS si el punto de conexión de hello utiliza una dirección IP en su lugar.
>
>

Hay dos tipos de conexiones híbridas, conexiones híbridas nueva Hola que se proporcionan como un servicio de retransmisión de Azure y hello las conexiones antiguas híbrida de BizTalk.  Hello las conexiones antiguas híbrida de BizTalk son clásico conexiones híbridas de tooas que se hace referencia en el portal de Hola.  En este mismo documento encontrará más información acerca de ellas.

### <a name="app-service-hybrid-connection-benefits"></a>Beneficios de usar las conexiones híbridas de App Service ###

Hay una serie de ventajas toohello híbrida conexiones capacidad incluidos

- Las aplicaciones pueden acceder de forma segura a los servicios y sistemas locales.
- característica de Hello no requiere un extremo accesible de internet
- es muy rápido y fácil tooset seguridad  
- cada conexión híbrida coincide con la combinación de host: puerto único tooa que es un aspecto excelente de seguridad
- Normalmente no requiere vulnerabilidades de firewall como hello las conexiones son todo el tráfico saliente a través de puertos web estándar
- porque la característica de hello es el nivel de red que también significa que es de idioma de toohello independiente usado por la tecnología de hello y la aplicación usada el punto de conexión de Hola
- se puede utilizar acceso tooprovide en varias redes de una única aplicación 

### <a name="things-you-cannot-do-with-hybrid-connections"></a>Cosas que no se pueden hacer con las conexiones híbridas ###

Estas operaciones no se pueden realizar con las conexiones híbridas:

- montar una unidad;
- usar UDP;
- acceder a servicios basados en TCP que usen puertos dinámicos, como el modo pasivo de FTP o el modo pasivo extendido;
- proporcionar soporte para LDAP, ya que a veces requiere UDP;
- proporcionar soporte para Active Directory

## <a name="adding-and-creating-a-hybrid-connection-in-your-app"></a>Adición y creación de una conexión híbrida en una aplicación ##

Las conexiones híbridas pueden crearse a través del portal de la aplicación de Hola o desde el portal de servicios de conexión híbrida de Hola.  Se recomienda encarecidamente que utilice hello toocreate portal de aplicación Hola conexiones híbridas desea toouse con la aplicación.  toocreate una conexión híbrida vaya toohello [portal de Azure] [ portal] y pasa a Hola interfaz de usuario para la aplicación.  Seleccione **Redes > Configure los extremos de la conexión híbrida**.  Desde aquí puede ver conexiones híbridas de Hola que se configuran con la aplicación  

![][2]

tooadd una conexión híbrida nueva, haga clic en Agregar conexión híbrida.  Hola interfaz de usuario que se abre muestra conexiones híbridas de Hola que ya haya creado.  tooadd uno o varios de ellos tooyour aplicación, haga clic en hello que desea y presione **selecciona Agregar conexión híbrida**.  

![][3]

Si desea toocreate una conexión híbrida nueva, haga clic en **crear conexión híbrida nueva**.  En el cuadro que aparece, especifique el: 

- nombre del punto de conexión
- nombre de host del punto de conexión
- puerto del punto de conexión
- espacio de nombres de bus de servicio que se va toouse

![][4]

Cada conexión híbrida es el espacio de nombres del bus de servicio de tooa relacionados y cada espacio de nombres del bus de servicio está en una región de Azure.  Es importante tootry y usar un servicio de bus de espacio de nombres en Hola misma región que la aplicación así como la latencia de red inducida por tooavoid.

Si desea tooremove la conexión híbrida desde su aplicación, haga clic con el botón secundario en él y seleccione **desconexión**.  

Una vez que una conexión híbrida se agrega la aplicación web de tooyour, puede ver los detalles en él simplemente haciendo clic en él.  

![][5]

## <a name="hybrid-connections-and-app-service-plans"></a>Conexiones híbridas y planes de App Service ##

Hola híbrida solo las conexiones que ahora pueden hacer son Hola nueva híbrida.  Solo están disponibles en las SKU de precios de nivel Básico, Estándar, Premium y Aislado.  No hay toohello límites vinculados plan de precios.  

| Plan de precios | Número de conexiones híbridas se puede usar en el plan de Hola |
|----|----|
| Básica | 5 |
| Estándar | 25 |
| Premium | 200 |
| Aislado | 200 |

Dado que existen restricciones de Plan de servicio de aplicaciones también hay interfaz de usuario en hello Plan del servicio de aplicación que muestra el número de conexiones híbridas se usan y qué aplicaciones.  

![][6]

Al igual que con la vista de la aplicación de hello, puede ver detalles de la conexión híbrida haciendo clic en él.  En Propiedades de Hola se muestra a continuación puede ver toda la información de Hola que tenía en la vista de la aplicación de hello, pero también puede ver cuántas otras aplicaciones en hello el mismo Plan de servicio de aplicación está utilizando esa conexión híbrida.

![][7]

Aunque no hay un límite del número de Hola de extremos de conexión híbrida que se puede usar en un Plan de servicio de aplicaciones, cada conexión híbrida usa puede usarse en cualquier número de aplicaciones en ese Plan de servicio de aplicaciones.  Que es toosay que si tuviera 1 conexión híbrida que he usado en 5 aplicaciones independientes en mi Plan de servicio de aplicaciones, es todavía solo 1 conexión híbrida.

Hay un conexiones de toohybrid costos adicionales más allá de que solo se puede usar en Basic, Standard, Premium o SKU aislado.  Para más información acerca de los precios de las conexiones híbridas, vaya aquí: [Precios de Service Bus][sbpricing].

## <a name="hybrid-connection-manager"></a>Hybrid Connection Manager ##

En orden para híbrida conexiones toowork necesita a un agente de retransmisión en red de Hola que hospeda el punto de conexión de la conexión híbrida.  Ese agente de retransmisión se denomina hello híbrida Connection Manager (gestión).  Esta herramienta puede descargarse desde hello **redes > configurar los extremos de conexión híbrida** interfaz de usuario disponible en la aplicación en hello [portal de Azure][portal].  

Esta herramienta se ejecuta en Windows Server 2008 R2 y en las versiones posteriores de Windows.  Una vez instalado Hola gestión se ejecuta como un servicio.  Este servicio conecta tooAzure retransmisión de bus de servicio en función de los puntos de conexión de hello configurado.  las conexiones de Hola de hello gestión son tooports salientes 80 y 443.    

Hola gestión tiene un tooconfigure de interfaz de usuario.  Después de hello que gestión está instalado puede poner en funcionamiento Hola interfaz de usuario mediante la ejecución de hello HybridConnectionManagerUi.exe que se encuentra en el directorio de instalación de administrador de conexiones híbridas de Hola.  Para acceder fácilmente en Windows 10, escriba *Interfaz de usuario de Hybrid Connection Manager* en el cuadro de búsqueda.  

Cuando hello HCM UI se inicia, lo primero que Hola consulte es una tabla que enumera la lista de conexiones híbridas de Hola que están configuradas con esta instancia de hello gestión.  Si desea toomake cualquier cambio deberá tooauthenticate con Azure. 

tooadd uno o más conexiones híbridas tooyour gestión:

1. Hola HCM UI de inicio
1. Haga clic en Configure other hybrid connection![][8] (Configurar otra conexión híbrida).

1. Inicie sesión con su cuenta de Azure
1. Elija una suscripción
1. Haga clic en las conexiones híbridas de Hola que desea que este toorelay de gestión![][9]

1. Haga clic en Guardar

En este momento, verá las conexiones híbridas de Hola que agregó.  También puede haga clic en la conexión híbrida de hello configurado y ver los detalles acerca de la conexión de Hola.

![][10]

Para las gestión toobe toosupport capaz de hello las conexiones híbridas se configura con, se necesita:

- TooAzure de acceso TCP a través de los puertos 80 y 443
- Extremo de la conexión de TCP acceso toohello híbrido
- capacidad toodo DNS apariencia SAI (UPS) en el host del punto de conexión de Hola y espacio de nombres de bus de servicio de azure Hola

Hola gestión admite nuevas conexiones híbridas así como las conexiones híbridas de BizTalk anteriores de Hola.

### <a name="redundancy"></a>Redundancia ###

Cada HCM puede admitir varias conexiones híbridas.  Además, varios HCM pueden admitir cualquier conexión híbrida dada.  comportamiento predeterminado de Hello es tooround tráfico de Round robin a través de hello configurado HCMs para cualquier punto de conexión determinado.  Si desea alta disponibilidad en las conexiones híbridas de la red, solo haya que crear instancias de varios HCM en equipos diferentes. 

### <a name="manually-adding-a-hybrid-connection"></a>Adición manual de una conexión híbrida ###

Si desea que alguien fuera de su suscripción toohost una instancia de gestión para una conexión híbrida determinado, puede compartir con ellos Hola la cadena de conexión de puerta de enlace de conexión híbrida de Hola.  Puede ver esto en las propiedades de hello para la conexión híbrida de hello [portal de Azure][portal]. toouse que cadena, haga clic en hello **configurar manualmente** botón Hola gestión y pegue en la cadena de conexión de puerta de enlace de Hola.


## <a name="troubleshooting"></a>Solución de problemas ##

Cuando se configura la conexión híbrida con una aplicación en ejecución y hay al menos una gestión que tiene configurada esa conexión híbrida, a continuación, se indicará el estado de hello es **conectado** en el portal de Hola.  Si no se indica **conectado** significa que la aplicación está inactivo o no se puede conectar la gestión fuera tooAzure en los puertos 80 o 443.  

Hola razón principal por la que los clientes no pueden conectar el punto de conexión de tootheir es porque no se especificó el punto de conexión de hello mediante una dirección IP en lugar de un nombre DNS.  Si la aplicación no puede alcanzar el extremo de hello deseado y utiliza una dirección IP, cambiar toousing un nombre DNS que es válido en el host de Hola donde hello gestión se está ejecutando.  Otro toocheck cosas son ese Hola nombre DNS se resuelve adecuadamente en el host de Hola donde hello gestión se ejecuta y que hay conectividad de host de Hola donde hello gestión está ejecutando extremo de la conexión híbrida toohello.  

Hay una herramienta Hola servicio de aplicaciones que se puede invocar desde la consola de hello llamado tcpping.  Esta herramienta puede indicarle si tiene el punto de conexión de acceso tooa TCP pero no indica si tiene el extremo de la conexión de acceso tooa híbrida.  Cuando se utiliza en la consola de hello en el extremo de una conexión híbrida, un ping correcto sólo indicar que tiene una conexión híbrida configurada para la aplicación que use esa combinación de host: puerto.  

## <a name="biztalk-hybrid-connections"></a>Conexiones híbridas de BizTalk ##

capacidad de las conexiones híbridas BizTalk anterior Hola se ha cerrado desactivar toofurther creaciones de conexión híbrida de BizTalk.  Puede seguir usando su preexistentes conexiones híbridas de BizTalk con sus aplicaciones, pero deberá migrar toohello nuevo servicio.  Entre Hola ventajas en el nuevo servicio de Hola a través de la versión de BizTalk de hello son:

- No se requieren cuentas de BizTalk adicionales.
- La versión de TLS es la 1.2, en lugar de la 1.0 que era en las conexiones híbridas de BizTalk.
- La comunicación es a través de los puertos 80 y 443 usando un tooreach de nombre DNS Azure en lugar de direcciones IP y un intervalo de adicionales otros puertos.  

tooadd una aplicación híbrida conexión tooyour para BizTalk, vaya tooyour aplicación Hola [portal de Azure] [ portal] y haga clic en **redes > configurar los extremos de conexión híbrida**.  En tabla de conexiones híbridas de hello clásico, haga clic en **Agregar conexión híbrida clásico**.  Ahí verá una lista de las conexiones híbridas de BizTalk.  


<!--Image references-->
[1]: ./media/app-service-hybrid-connections/hybridconn-connectiondiagram.png
[2]: ./media/app-service-hybrid-connections/hybridconn-portal.png
[3]: ./media/app-service-hybrid-connections/hybridconn-addhc.png
[4]: ./media/app-service-hybrid-connections/hybridconn-createhc.png
[5]: ./media/app-service-hybrid-connections/hybridconn-properties.png
[6]: ./media/app-service-hybrid-connections/hybridconn-aspproperties.png
[7]: ./media/app-service-hybrid-connections/hybridconn-hcm.png
[8]: ./media/app-service-hybrid-connections/hybridconn-hcmadd.png
[9]: ./media/app-service-hybrid-connections/hybridconn-hcmadded.png
[10]: ./media/app-service-hybrid-connections/hybridconn-hcmdetails.png

<!--Links-->
[HCService]: http://docs.microsoft.com/azure/service-bus-relay/relay-hybrid-connections-protocol/
[portal]: http://portal.azure.com/
[oldhc]: http://docs.microsoft.com/azure/biztalk-services/integration-hybrid-connection-overview/
[sbpricing]: http://azure.microsoft.com/pricing/details/service-bus/

