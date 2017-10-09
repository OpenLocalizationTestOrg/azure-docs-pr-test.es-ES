---
title: enrutamiento de aaaAsymmetric | Documentos de Microsoft
description: "Este artículo le guiará a través de los problemas de hello que podría se enfrentan a un cliente con el enrutamiento asimétrico en una red que tiene varios vínculos tooa destino."
documentationcenter: na
services: expressroute
author: osamazia
manager: carmonm
editor: 
ms.assetid: a754bff9-95c9-44b5-9796-377fc21e8322
ms.service: expressroute
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 10/10/2016
ms.author: osamam
ms.openlocfilehash: 01a16242437a3674dcfe27b074911a829a6c1abd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="asymmetric-routing-with-multiple-network-paths"></a>Enrutamiento asimétrico con varias rutas de acceso de red
En este artículo se explica cómo el tráfico de red de reenvío y de retorno puede tomar distintas rutas cuando hay varias rutas de acceso disponibles entre el origen y el destino de la red.

Es importante toounderstand dos conceptos toounderstand asimétrica de enrutamiento. Uno es el efecto de Hola de varias rutas de acceso de red. Hola otro es cómo los dispositivos, como un firewall, mantienen el estado. Estos tipos de dispositivos se denominan dispositivos con estado. Una combinación de estos dos factores crea en la red a tráfico se quita un dispositivo con estado porque no detectan dispositivos con estado de Hola que se originó el tráfico con el propio dispositivo Hola de escenarios.

## <a name="multiple-network-paths"></a>Varias rutas de acceso de red
Cuando una red de empresa tiene solo un toohello vínculo viaja de Internet a través de su proveedor de servicios de Internet, todas las tooand de tráfico de Internet Hola Hola misma ruta de acceso. A menudo, las empresas adquirir varios circuitos, como rutas redundantes, el tiempo de actividad de red de tooimprove. Cuando esto sucede, es posible que el tráfico que sale fuera de la red de hello, toohello Internet, atraviesa hello y un vínculo devuelto tráfico pasa a través de otro vínculo. Normalmente, esto se conoce como enrutamiento asimétrico. En el enrutamiento asimétrico, inversa tráfico de red toma otra ruta de acceso de flujo de hello original.

![Red con varias rutas de acceso](./media/expressroute-asymmetric-routing/AsymmetricRouting3.png)

Aunque se produce principalmente en hello Internet, enrutamiento asimétrica también aplica tooother combinaciones de varias rutas de acceso. Se aplica, por ejemplo, ruta de acceso de Internet tooan y una ruta de acceso privada que vaya toohello mismo destino y toomultiple rutas de acceso privada que vaya toohello mismo destino.

Cada enrutador a lo largo de la forma de hello, de origen toodestination, calcula Hola mejor ruta de acceso tooreach un destino. Hello determinación del enrutador del mejor posible ruta de acceso se basa en dos factores principales:

* El enrutamiento entre redes externas se basa en un protocolo de enrutamiento llamado Border Gateway Protocol (BGP). BGP toma anuncios de vecinos y ejecuta a ellos a través de una serie de pasos toodetermine Hola mejor ruta de acceso toohello pensado destino. Almacena mejor ruta de hello en su tabla de enrutamiento.
* longitud de Hola de una máscara de subred asociada con una ruta influye en las rutas de acceso de enrutamientos. Si recibe un enrutador varios anuncios de Hola la misma dirección IP pero con diferentes máscaras de subred, enrutador Hola prefiere anuncio de Hola con una máscara de subred más tiempo ya que considera una ruta más específica.

## <a name="stateful-devices"></a>Dispositivos con estado
Buscar enrutadores en el encabezado IP de Hola de un paquete para fines de enrutamiento. Algunos dispositivos buscar aún más profundos en el paquete de saludo. Normalmente, estos dispositivos miran los encabezados de la capa (4) (Protocolo de control de transmisión o TCP, o Protocolo de datagramas de usuario o UDP) o incluso de la capa 7 (capa de aplicación). Estas variantes de dispositivos son dispositivos de seguridad o dispositivos de optimización de ancho de banda. 

Un firewall es un ejemplo común de dispositivo con estado. Un firewall permite o deniega un toopass de paquete a través de sus interfaces según varios campos, como protocolo y el puerto TCP/UDP, encabezados de dirección URL. Este nivel de inspección de paquetes coloca a mucha carga de procesamiento en el dispositivo de Hola. rendimiento tooimprove, firewall de hello inspecciona primer paquete de saludo de un flujo. Si permite tooproceed de paquetes de Hola, mantiene información de flujo de hello en su tabla de estado. Todos los paquetes posteriores toothis relacionados flujo se permiten en función de determinación de saludo inicial. Los paquetes que forma parte de un flujo existente pueden llegar en firewall de Hola. Si firewall de hello tiene información de estado anterior, firewall de Hola quita el paquete de saludo.

## <a name="asymmetric-routing-with-expressroute"></a>Enrutamiento asimétrico con ExpressRoute
Cuando se conecta tooMicrosoft a través de ExpressRoute de Azure, los cambios de red similar a la siguiente:

* Tener varias tooMicrosoft de vínculos. Un vínculo es la conexión a Internet existente y Hola otro es a través de ExpressRoute. Algunos tooMicrosoft de tráfico puede recorrer Hola Internet pero volver a través de ExpressRoute, o viceversa.
* Recibe direcciones IP más específicas a través de ExpressRoute. Por lo tanto, para el tráfico de su tooMicrosoft de red para servicios ofrecidos a través de ExpressRoute, enrutadores siempre son preferibles ExpressRoute.

efecto de hello toounderstand tienen estos dos cambios en una red, veamos algunos escenarios. Por ejemplo, tiene un único circuito toohello Internet y consumir todos los servicios de Microsoft a través de Internet de Hola. tráfico de Hola desde su recorra tooMicrosoft y de vuelta de red Hola mismo vínculo a Internet y pasa a través de firewall de Hola. registros de firewall de Hola Hola flujo cuando ve el primer paquete de Hola y devolver los paquetes se permiten porque flujo Hola existe en la tabla de estado de Hola.

![Enrutamiento asimétrico con ExpressRoute](./media/expressroute-asymmetric-routing/AsymmetricRouting1.png)

A continuación, ya puede activar ExpressRoute y consumir los servicios ofrecidos por Microsoft a través de ExpressRoute. Todos los demás servicios de Microsoft se consumen durante Hola Internet. Implementar un servidor de seguridad independiente en el extremo que está conectado tooExpressRoute. Microsoft anuncia la red de tooyour de prefijos más específica a través de ExpressRoute para servicios específicos. Su infraestructura de enrutamiento elige ExpressRoute como ruta de acceso preferida de Hola para dichos prefijos. Si no va a anunciar su tooMicrosoft de direcciones IP pública a través de ExpressRoute, Microsoft se comunica con las direcciones IP públicas a través de Internet de Hola. Reenvíe el tráfico de la red tooMicrosoft utiliza ExpressRoute y tráfico inverso de Microsoft utiliza Hola Internet. Cuando firewall de hello en el perímetro de hello ve un paquete de respuesta para un flujo que no se encuentra en la tabla de estado de hello, quita el tráfico del retorno Hola.

Si elige hello toouse mismo traducción de direcciones de red (NAT) del grupo de ExpressRoute y de hello Internet, verá problemas similares con clientes de hello en la red en direcciones IP privadas. Solicitudes para servicios como Windows Update se enviarán a través de Internet de hello porque las direcciones IP para estos servicios no se anuncian a través de ExpressRoute. Sin embargo, tráfico del retorno Hola vuelve a través de ExpressRoute. Si Microsoft recibe una dirección IP con Hola misma máscara de subred de hello Internet y ExpressRoute, prefiere ExpressRoute Hola Internet. Si un firewall u otro dispositivo con estado que se encuentra en el perímetro de la red y boca ExpressRoute no tiene ninguna información previa sobre el flujo de hello, quita los paquetes de saludo que pertenecen toothat flujo.

## <a name="asymmetric-routing-solutions"></a>Soluciones de enrutamiento asimétrico
Tiene dos opciones principales toosolve Hola problema de enrutamiento asimétrico. Una es a través de enrutamiento y Hola otro consiste en usar NAT basada en origen (SNAT).

### <a name="routing"></a>Enrutamiento
Asegúrese de que las direcciones IP públicas son vínculos de tooappropriate anunciado wide area network (WAN). Por ejemplo, si desea toouse Hola Internet para el tráfico de autenticación y ExpressRoute para el tráfico de correo electrónico, no deben anunciar las direcciones IP públicas de los servicios de federación de Active Directory (AD FS) a través de ExpressRoute. Igualmente, asegúrese de no tooexpose un local las direcciones de tooIP de servidor de AD FS que Hola enrutador recibe a través de ExpressRoute. Las rutas recibidas a través de ExpressRoute son más específicas, por lo que hacen ruta preferida de hello ExpressRoute para tooMicrosoft de tráfico de autenticación. Esto provocará un enrutamiento asimétrico.

Si desea toouse ExpressRoute para la autenticación, asegúrese de que va a anunciar las direcciones IP públicas de AD FS a través de ExpressRoute sin NAT. De esta manera, el tráfico que se origina en Microsoft y queda tooan local de servidor de AD FS que se pasa a través de ExpressRoute. El tráfico devuelto desde tooMicrosoft cliente use ExpressRoute porque es ruta preferida de Hola a través de Internet de Hola.

### <a name="source-based-nat"></a>NAT basada en origen
Otra manera de resolver los problemas de enrutamiento asimétrico es mediante SNAT. Por ejemplo, no ha anunciado dirección IP pública de Hola de un servidor de Protocolo Simple de transferencia de correo (SMTP) local a través de ExpressRoute como se pretende toouse Hola Internet para este tipo de comunicación. Una solicitud que se origina con Microsoft y, a continuación, sale tooyour local de servidor SMTP recorre Hola Internet. Se SNAT Hola dirección IP de entrada solicitud tooan interno. El tráfico inverso del servidor SMTP de hello dirige toohello firewall perimetral (que utiliza para NAT) en lugar de a través de ExpressRoute. tráfico del retorno Hola vuelve a través de Internet de Hola.

![Configuración de red con NAT basada en origen](./media/expressroute-asymmetric-routing/AsymmetricRouting2.png)

## <a name="asymmetric-routing-detection"></a>Detección de enrutamiento asimétrico
Traceroute es toomake de manera mejor de hello seguro de que el tráfico de red atraviesa la ruta de acceso de hello esperado. Si espera que el tráfico de la ruta local SMTP server tooMicrosoft tootake Hola Internet, Hola espera traceroute procede Hola SMTP server tooOffice 365. resultado de Hello valida que el tráfico está abandonando realmente la red hacia Internet hello y no hacia ExpressRoute.

