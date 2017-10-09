---
title: "aaaIntegrate una aplicación con una red Virtual de Azure"
description: "Muestra cómo tooconnect una aplicación de servicio de aplicaciones de Azure tooa existente o nueva red virtual de Azure"
services: app-service
documentationcenter: 
author: ccompy
manager: erikre
editor: cephalin
ms.assetid: 90bc6ec6-133d-4d87-a867-fcf77da75f5a
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/23/2017
ms.author: ccompy
ms.openlocfilehash: a93c504481400245b02220b541a008a7c874d10a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="integrate-your-app-with-an-azure-virtual-network"></a>Integración de su aplicación con una red virtual de Azure
Este documento describe la característica de integración de red virtual de servicio de aplicaciones de Azure de Hola y muestra cómo tooset, configúrelo con aplicaciones en [servicio de aplicaciones de Azure](http://go.microsoft.com/fwlink/?LinkId=529714). Si no está familiarizado con las redes virtuales de Azure (redes virtuales), esto es una funcionalidad que permite tooplace muchos de los recursos de Azure en una red de internet no enrutables que controle el acceso a. Estas redes se pueden redes locales de tooyour conectados mediante una variedad de tecnologías VPN. toolearn más información acerca de redes virtuales de Azure, comience con la información de hello aquí: [información general de red Virtual de Azure][VNETOverview]. 

Hola servicio de aplicaciones de Azure tiene dos formas. 

1. sistemas de varios inquilinos de Hola que admiten la gama completa de Hola de planes de precios
2. característica de premium del entorno de servicio de aplicación (ASE) Hello, que se implementa en la red virtual. 

Este documento pasa a través de Integración con red virtual y no de App Service Environment. Si desea más información acerca de la característica de hello ASE toolearn, comience con información de hello aquí: [Introducción entono][ASEintro].

Integración de la red virtual da como resultado la tooresources de acceso de aplicación web en la red virtual pero no se le otorga la aplicación web de acceso privada tooyour de red virtual de Hola. Acceso al sitio privada hace referencia toomaking la aplicación solo es accesible desde una red privada como desde dentro de una red virtual de Azure. El acceso privado al sitio solo está disponible con un ASE configurado con un Equilibrador de carga interno (ILB). Para obtener más información sobre el uso de una ASE de ILB, comenzar con el artículo de hello aquí: [crear y usar una ASE de ILB][ILBASE]. 

Un escenario común donde se usa la integración de red virtual es habilitar el acceso de la base de datos de tooa de aplicación web o un servicio web que se ejecuta en una máquina virtual en la red virtual de Azure. Con la integración de red virtual, no es necesario tooexpose un extremo público para las aplicaciones en su máquina virtual pero puede usar direcciones enrutable de hello privadas de internet que no sea en su lugar. 

característica de integración de la red virtual de Hello:

* requiere un plan de precios Premium, Estándar o Aislado; 
* funciona con una red virtual clásica o de Resource Manager; 
* es compatible con TCP y UDP;
* funciona con aplicaciones web, móviles y de API;
* permite un tooonly de tooconnect de aplicación 1 red virtual a la vez
* habilita la toofive toobe de redes virtuales integrada en un Plan de servicio de aplicaciones 
* permite Hola mismo toobe de red virtual utilizado por varias aplicaciones en un Plan de servicio de aplicaciones
* es compatible con un SLA del 99,9% debido toohello SLA en hello puerta de enlace de red virtual

Hay algunos aspectos que Integración con red virtual no admite, como:

* montar una unidad;
* la integración de AD; 
* NetBios;
* el acceso privado a sitios.

### <a name="getting-started"></a>Introducción
Estas son algunas cosas tookeep en cuenta antes de conectar la red virtual de la tooa de aplicación web:

* Integración con red virtual solo funciona con aplicaciones en un plan de precios **Estándar**, **Premium** o **Aislado**. Si habilita la característica hello y, a continuación, escalar su tooan de Plan de servicio de aplicaciones no compatible plan de precios sus aplicaciones pierdan su toohello conexiones redes virtuales que están utilizando. 
* Si la red virtual de destino ya existe, debe tener VPN de sitio a punto habilitada con una puerta de enlace de enrutamiento dinámico antes de poder aplicación tooan conectado. Si la puerta de enlace está configurada con enrutamiento estático, no puede habilitar una red privada virtual (VPN) de punto a sitio.
* red virtual Hello debe ser una Hola misma suscripción que su Plan(ASP) de servicio de aplicación. 
* las aplicaciones de Hola que se integran con una red virtual usan Hola DNS que se especifica para esa red virtual.
* De forma predeterminada las aplicaciones de la integración sólo enrutan el tráfico en la red virtual en función de las rutas de Hola que se definen en la red virtual. 

## <a name="enabling-vnet-integration"></a>Habilitación de Integración con red virtual
Este documento se centra principalmente en el uso de hello portal de Azure para la integración de red virtual. tooenable integración de red virtual con la aplicación con PowerShell, siga instrucciones de hello aquí: [conectar su red virtual de tooyour de aplicación mediante PowerShell][IntPowershell].

Tener Hola opción tooconnect su aplicación tooa existente o nueva red virtual. Si crea una nueva red como parte de la integración, a continuación, además toojust crear Hola red virtual, una puerta de enlace de enrutamiento dinámico está preconfigurado para y punto tooSite VPN está habilitada. 

> [!NOTE]
> Se puede tardar unos minutos en configurar una nueva integración con redes virtuales. 
> 
> 

tooenable integración de red virtual, abra la configuración de la aplicación y, a continuación, seleccione las redes. Hola interfaz de usuario que se abre ofrece tres opciones de red. En esta guía solo se va a tratar Integración con red virtual, aunque más adelante en este documento se explicarán Conexiones híbridas y a instancias de App Service Environment. 

Si la aplicación no está en hello correcto de plan de precios, Hola interfaz de usuario permite tooscale su tooa plan superior precios plan de su elección.

![][1]

### <a name="enabling-vnet-integration-with-a-pre-existing-vnet"></a>Habilitación de Integración con red virtual con una red virtual existente
Hola interfaz de usuario de integración de red virtual le permite tooselect en una lista de sus redes virtuales. Hola redes virtuales clásicas indicar que son como con la palabra Hola "Clásico" en el siguiente nombre de red virtual toohello paréntesis. Hello lista se ordena de modo que hello VNets el Administrador de recursos se enumeran en primer lugar. Hola imagen que se muestra a continuación, puede ver que se puede seleccionar solo una red virtual. Existen varias razones por las que una red virtual estará atenuada, entre otras:

* Hola red virtual está en otra suscripción que la cuenta tiene acceso a
* Hola red virtual no tiene tooSite punto habilitada
* Hola red virtual no tiene una puerta de enlace de enrutamiento dinámico

![][2]

integración de tooenable simplemente haga clic en Hola red virtual que se va toointegrate con. Después de seleccionar Hola red virtual, la aplicación se reinicia automáticamente para hello cambios tootake efecto. 

##### <a name="enable-point-toosite-in-a-classic-vnet"></a>Habilitar tooSite punto en una red virtual clásica
Si la red virtual no tiene una puerta de enlace ni tiene tooSite de punto, tendrá tooset primero arriba. toodo para una red virtual clásica, vaya toohello [portal de Azure] [ AzurePortal] y para hacer que la lista de Hola de Networks(classic) Virtual. Desde aquí, haga clic en la red de Hola que desee toointegrate con y haga clic en el cuadro grande de hello en Essentials llamado a las conexiones VPN. Desde aquí, puede crear la VPN de punto toosite e incluso tener crear una puerta de enlace. Después de recorrer Hola punto toosite con experiencia de creación de puerta de enlace es aproximadamente 30 minutos antes de esté listo. 

![][8]

##### <a name="enabling-point-toosite-in-a-resource-manager-vnet"></a>Habilitar punto tooSite en un administrador de recursos de VNet
tooconfigure una VNet el Administrador de recursos con una puerta de enlace y el punto tooSite, puede usar PowerShell tal como se describe aquí, [configurar una punto a sitio conexión tooa red virtual con PowerShell] [ V2VNETP2S] o use Hola portal de Azure tal como se describe aquí, [configurar un punto a sitio conexión tooa red virtual con Hola portal de Azure][V2VNETPortal]. tooperform de interfaz de usuario de Hello esta funcionalidad no aún disponible. Tenga en cuenta que debe toocreate certificados para la configuración de punto tooSite Hola. Esto se configura automáticamente cuando se conecta la red virtual de WebApp toohello. 

### <a name="creating-a-pre-configured-vnet"></a>Creación de una red virtual preconfigurada
Si desea toocreate una red virtual nueva que esté configurada con una puerta de enlace y de punto a sitio, servicio de aplicaciones de interfaz de usuario de red hello tiene Hola capacidad toodo pero solo para una red virtual de administrador de recursos. Si desea toocreate una red virtual clásica con una puerta de enlace y Point-to-Site, a continuación, lo necesita toodo manualmente a través de la interfaz de usuario de red de Hola. 

toocreate una VNet el Administrador de recursos a través de hello interfaz de usuario de integración de red virtual, simplemente seleccione **crear nueva red Virtual** y proporcione el:

* El nombre de la red virtual
* El bloque de direcciones de la red virtual
* Nombre de subred
* El bloque de direcciones de la subred
* El bloque de direcciones de la puerta de enlace
* El bloque de direcciones de la conexión de punto a sitio

Si desea que este tooany de tooconnect de red virtual otras redes, debe evitar espacio de direcciones IP que se superpone a las redes de selección. 

> [!NOTE]
> Creación de VNet Administrador de recursos con una puerta de enlace dura aproximadamente 30 minutos y actualmente no integra Hola red virtual con la aplicación. Una vez creada la red virtual con la puerta de enlace de hello necesario toocome tooyour atrás aplicación interfaz de usuario de integración de red virtual y seleccione la red virtual nueva.
> 
> 

![][3]

Las redes virtuales de Azure normalmente se crean dentro de direcciones de red privadas. Por Hola de forma predeterminada la integración de red virtual característica enruta todo el tráfico destinado a los intervalos de direcciones IP en la red virtual. intervalos de direcciones IP privadas de Hello son:

* 10.0.0.0/8 - esto es Hola igual como 10.0.0.0 - 10.255.255.255
* 172.16.0.0/12 - esto es Hola igual como 172.16.0.0 - 172.31.255.255 
* 192.168.0.0/16 - esto es Hola igual como 192.168.0.0 - 192.168.255.255

Hola espacio de direcciones de red virtual debe toobe especificado en la notación CIDR. Si no está familiarizado con la notación CIDR, es un método para especificar los bloques de direcciones con una dirección IP y un entero que representa la máscara de red Hola. Como referencia rápida, tenga en cuenta que 10.1.0.0/24 corresponde a 256 direcciones y 10.1.0.0/25, a 128. Una dirección IPv4 con un /32 sería simplemente una dirección. 

Si establece aquí Hola información del servidor DNS, que está establecida para la red virtual. Después de la creación de la red virtual puede editar esta información de experiencias de usuario de red virtual de Hola. Si cambia Hola DNS de red virtual de hello, debe tooperform una operación de red de sincronización.

Cuando se crea una red virtual clásica con hello interfaz de usuario de integración de red virtual, crea una red virtual en hello mismo grupo de recursos que la aplicación. 

## <a name="how-hello-system-works"></a>Funcionamiento del sistema Hola
Tras los bastidores de hello esta característica basa en Point-to-Site VPN tecnología tooconnect su red virtual tooyour de aplicación. Las aplicaciones de Azure App Service tienen una arquitectura de sistema de varios inquilinos que impide el aprovisionamiento de una aplicación directamente en una red virtual como se hace con las máquinas virtuales. A partir de la tecnología punto a sitio limitamos red acceso toojust Hola máquina virtual que hospeda aplicación hello. Red de toohello de acceso se restringe aún más en los hosts de la aplicación para que las aplicaciones solo pueden tener acceso a redes de hello configurarlos tooaccess. 

![][4]

Si no ha configurado un servidor DNS con la red virtual, la aplicación necesitará toouse IP direcciones tooreach recursos Hola red virtual. Durante el uso de direcciones IP, recuerde que ventaja principal de Hola de esta característica es que le permite direcciones privadas de hello toouse dentro de la red privada. Si establece la aplicación de toouse direcciones IP públicas para uno de sus máquinas virtuales, no está usando la característica de integración de la red virtual de Hola y se comunican a través Hola internet.

## <a name="managing-hello-vnet-integrations"></a>Administración de integraciones de red virtual de Hola
Hola tooconnect de capacidad y desconecte tooa que red virtual tiene un nivel de aplicación. Las operaciones que pueden afectar a Hola integración de red virtual entre varias aplicaciones tienen un nivel ASP. Desde la interfaz de usuario que se muestra en el nivel de aplicación Hola Hola, puede obtener detalles en la red virtual. Mayoría de hello mismo también se muestra información en hello ASP nivel. 

![][5]

Desde la página de estado de la característica de red de hello, puede ver si la aplicación se encuentra conectado tooyour red virtual. Si la puerta de enlace de red virtual no está disponible por cualquier razón, aparecerá como no conectada. 

información de Hello tiene ahora tooyou disponible en la aplicación hello nivel interfaz de usuario de integración de red virtual es igual Hola como información detallada de hello obtendrá de hello ASP. Esto es lo que cubre:

* Nombre de red virtual - este vínculo abre Hola red virtual de Azure interfaz de usuario
* Ubicación: Esto refleja la ubicación de saludo de la red virtual. Es posible toointegrate con una red virtual en otra ubicación.
* Estado de certificado - hay conexión de VPN de certificados que se usan toosecure Hola entre la aplicación hello y Hola red virtual. Esto refleja un tooensure de prueba están sincronizadas.
* Estado de la puerta de enlace: las puertas de enlace deben hacia abajo por cualquier motivo, a continuación, la aplicación no puede acceder a recursos de red virtual de Hola. 
* Espacio de direcciones de red virtual: se trata de espacio de direcciones IP de hello para la red virtual. 
* Espacio de direcciones del punto de tooSite - se trata de espacio de direcciones IP de hello toosite de punto para la red virtual. La aplicación muestra la comunicación como procedente de uno de hello IP en este espacio de direcciones. 
* Espacio de direcciones de sitio toosite - puede utilizar tooconnect de VPN de sitio tooSite su tooyour de red virtual local recursos o tooother red virtual. Debe tener configurar, a continuación, los intervalos IP de hello definidos con que se muestra aquí la conexión VPN.
* Servidores DNS: si tiene servidores DNS configurados con la red virtual, aparecen aquí.
* Direcciones IP enrutan toohello red virtual: hay una lista de direcciones IP que la red virtual tiene definido para el enrutamiento y esas direcciones mostrar aquí. 

puede realizar en la vista de la aplicación de hello de la integración de red virtual única operación de Hello es toodisconnect Hola de la aplicación de red virtual está conectado actualmente a. toodo este simplemente haga clic en Desconectar en la parte superior de Hola. Esta acción no cambia la red virtual. Hola red virtual y su configuración incluidas las puertas de enlace de hello permanece sin cambios. Si a continuación, deberá toodelete la red virtual, deberá toofirst delete Hola recursos, incluidas las puertas de enlace de Hola. 

Hola vista Plan de servicio de aplicación tiene un número de operaciones adicionales. También se accede diferente que desde la aplicación hello. Hola tooreach interfaz de usuario de red de ASP simplemente abra la interfaz de usuario de ASP y desplácese hacia abajo. Hay un elemento de interfaz de usuario llamado Estado de característica de red. Ofrece varios detalles menores sobre Integración con red virtual. Al hacer clic en esta interfaz de usuario, abre Hola interfaz de usuario de estado de característica de red. Si, a continuación, haga clic en "haga clic aquí toomanage", Hola interfaz de usuario que muestra hello integraciones de red virtual en este ASP se abre.

![][6]

ubicación de Hola de hello ASP es buena tooremember al buscar en ubicaciones de Hola de hello redes virtuales que se va a integrar con. Una vez Hola red virtual en otra ubicación son más proclives problemas de latencia de toosee. 

Hola redes virtuales que se integra con es un recordatorio en redes virtuales cuántos que sus aplicaciones se integran con en este ASP y cuántos puede tener. 

toosee agrega detalles en cada red virtual, haga clic en hello red virtual que le interesen. Además toohello detalles que se indicaron anteriormente, también verá una lista de aplicaciones de hello en este ASP que usan esa red virtual. 

Con respecto tooactions existe son dos acciones principales. Hola en primer lugar es rutas de tooadd de capacidad de Hola que controlan el tráfico que sale de la aplicación en la red virtual. segunda acción de Hello es certificados de toosync de capacidad de Hola y la información de red.

![][7]

**Enrutamiento** tal y como se indicaba anteriormente las rutas de Hola que se definen en la red virtual son lo que se usa para dirigir el tráfico en la red virtual de la aplicación. Hay algunos usos aunque donde los clientes desean toosend el tráfico de salida adicionales desde una aplicación en la red virtual de Hola y les proporciona esta capacidad. ¿Qué ocurre toohello tráfico después de esté en el cliente de hello toohow configura su red virtual. 

**Certificados** Hola certificado estado refleja una comprobación que está realizarla hello toovalidate de servicio de aplicaciones que los certificados de Hola que usamos para conexión VPN hello son sigue siendo buenos. Cuando se habilita la integración de red virtual, a continuación, si se trata de hello primera integración toothat red virtual de las aplicaciones en esta página ASP, hay un intercambio necesario de seguridad de certificados tooensure Hola de conexión de Hola. Junto con los certificados de hello obtenemos la configuración de DNS de hello, rutas y otras acciones similares que describen la red de Hola.
Si se cambia los certificados o la información de red, debe tooclick "Red de sincronización". **NOTA**: Al hacer clic en "Sincronizar red", se producirá una breve interrupción en la conectividad entre la aplicación y la red virtual. Mientras la aplicación no se reinicia, pérdida de Hola de conectividad podría provocar que la función toonot del sitio correctamente. 

## <a name="accessing-on-premises-resources"></a>Obtener acceso a recursos locales
Una de las ventajas de Hola de característica de integración de la red virtual de hello es que si está conectada a la red virtual tooyour local red con una VPN de sitio tooSite, a continuación, las aplicaciones pueden tener acceso a los recursos locales tooyour desde la aplicación. Para este toowork aunque puede que necesite tooupdate enruta la puerta de enlace VPN local con hello para el intervalo IP tooSite de punto. Cuando Hola sitio tooSite VPN está configurado en primer lugar, a continuación, las secuencias de comandos de hello usan tooconfigure se debe establecer rutas incluidas la VPN de punto tooSite. Si agrega Hola VPN de punto tooSite después de crear la VPN de sitio tooSite, a continuación, debe rutas de hello tooupdate manualmente. Información detallada sobre cómo toodo que varíe en cada puerta de enlace y no se describe aquí. 

> [!NOTE]
> característica de integración de la red virtual de Hello no integra una aplicación con una red virtual que tiene una puerta de enlace de ExpressRoute. Aunque esté configurado Hola puerta de enlace ExpressRoute en [modo de coexistencia] [ VPNERCoex] hello no funciona la integración de red virtual. Si necesita recursos tooaccess a través de una conexión ExpressRoute, a continuación, puede usar un [entono][ASE], que se ejecuta en la red virtual.
> 
> 

## <a name="pricing-details"></a>Detalles de precios
Hay algunos matices que debe tener en cuenta al utilizar la característica de integración de la red virtual de Hola de precios. Hay 3 cargos relacionados toohello uso de esta característica:

* Requisitos del plan de tarifa para el plan de servicio de aplicaciones
* Costos de la transferencia de datos
* Costos de la puerta de enlace de VPN

Para su toouse capaz de aplicaciones toobe esta característica, necesitan toobe en un Plan de servicio de aplicaciones Premium o estándar. Puede ver más detalles sobre esos costos aquí: [Precios de App Service][ASPricing]. 

Debido toohello manera tooSite punto se tratan las redes privadas virtuales, siempre con un cargo para datos salientes a través de la conexión de red virtual integración aunque Hola red virtual esté en Hola mismo centro de datos. toosee ¿cuáles son los cargos, eche un vistazo aquí: [detalles de precios de transferencia de datos][DataPricing]. 

último elemento de Hello es costo Hola de puertas de enlace de red virtual de Hola. Si no necesita puertas de enlace de Hola para otra cosa como tooSite VPN de sitio, a continuación, va a pagar para la característica de integración de la red virtual de las puertas de enlace toosupport Hola. Los detalles sobre esos costos están aquí: [Precios de Puerta de enlace de VPN][VNETPricing]. 

## <a name="troubleshooting"></a>Solución de problemas
Mientras la característica de hello es fácil tooset hacia arriba, eso no significa que la experiencia será problema libre. Deben encontrarse problemas para acceder a su punto de conexión deseado existe son algunas de las utilidades que puede usar la conectividad de tootest desde la consola de aplicación Hola. Puede usar dos experiencias de consola. Desde la consola de Kudu de Hola y Hola otro es consola Hola que puede alcanzar en hello portal de Azure. consola de tooget toohello Kudu desde la aplicación vaya tooTools -> Kudu. Esto mismo es Hola como va demasiado [nombre del sitio]. scm.azurewebsites.net. Una vez que se abre toohello simplemente vaya depuración consola ficha tooget toohello consola hospedado de Azure portal, a continuación, desde la aplicación vaya tooTools -> consola. 

#### <a name="tools"></a>Herramientas
Hola herramientas ping, nslookup y tracert no funcionarán a través de la consola de hello debido a restricciones de toosecurity. toofill Hola allí void han sido dos herramientas independientes que se agrega. En la funcionalidad DNS de orden tootest agregamos una herramienta denominada nameresolver.exe. Hola sintaxis es:

    nameresolver.exe hostname [optional: DNS Server]

Puede usar nameresolver toocheck Hola hostnames que depende de la aplicación. De esta forma puede probar si tiene algo mal configurado con el DNS o quizás no tiene servidor DNS de acceso tooyour.

herramienta siguiente Hola permite tootest para TCP conectividad tooa host y combinación de puerto. Esta herramienta se denomina tcpping.exe y sintaxis de hello es:

    tcpping.exe hostname [optional: port]

utilidad de Hello tcpping indica si se pueden llegar a un host específico y un puerto. Solo puede mostrar correcto si: hay una aplicación escuchando en la combinación de host y el puerto de hello y no hay acceso a la red desde el host de aplicación toohello especificado y el puerto.

#### <a name="debugging-access-toovnet-hosted-resources"></a>Depuración tooVNet de acceso a los recursos hospedados
Hay varias situaciones que pueden impedir que la aplicación llegue a un host y un puerto específicos. La mayoría de las veces de hello es uno de los tres cosas:

* **Hay un firewall en hello forma** si tiene un firewall en forma de hello, alcanzará el tiempo de espera de hello TCP. En este caso, es de 21 segundos. Usar la conectividad de tootest de hello tcpping herramienta. Los tiempos de espera TCP pueden ser debido a la toomany cosas más allá de los servidores de seguridad pero empezar por ahí. 
* **DNS no es accesible** el tiempo de espera de hello DNS es de tres segundos por cada servidor DNS. Si tiene dos servidores DNS, tiempo de espera de hello es de 6 segundos. Utilice nameresolver toosee si DNS está funcionando. Recuerde que no se puede utilizar nslookup que utilice Hola DNS se configura la red virtual con.
* **Intervalo no válido de P2S IP** intervalo IP de hello toosite de punto necesita toobe en intervalos de IP privadas de hello RFC 1918 (10.0.0.0-10.255.255.255 / 172.16.0.0-172.31.255.255 / 192.168.0.0-192.168.255.255). Si el intervalo de hello usa direcciones IP fuera, lo no funciona. 

Si los elementos no responden a su problema, busque en primer lugar Hola simple cosas: 

* ¿Hola puerta de enlace aparezca como una en el portal de hello?
* ¿Indican los certificados que están sincronizados?
* ¿Todo el personal cambiar configuración de red de hello sin tener que realizar una "red de sincronización" en ASP Hola afectado? 

Si la puerta de enlace está inactiva, vuelva a activarla. Si los certificados están sincronizados, ir a vista ASP toohello de la integración de red virtual y llamadas "Red de sincronización". Si sospecha que ha habido una configuración de red virtual de tooyour cambio realizado y no fue sincronización haría con su ASP, a continuación, vaya a la vista ASP toohello de la integración de red virtual y alcanza Just "Red de sincronización" como recordatorio, esto hace que una breve interrupción con la conexión de red virtual y las aplicaciones . 

Si todo esto es correcto, deberá toodig en algo un poco más:

* ¿Se produce ninguna otra aplicación con recursos de tooreach de integración de la red virtual de Hola misma red virtual? 
* ¿Puede ir toohello consola de aplicación y usar tcpping tooreach otros recursos de la red virtual? 

Cuando se cumple cualquiera de hello anterior, a continuación, la integración de red virtual es correcto y problema Hola esté en alguna otra. Esto es donde obtiene toobe más de un desafío porque no hay ningún toosee de manera sencilla por qué no se puede llegar a un host: puerto. Algunas de las causas de hello son:

* tener un servidor de seguridad hasta en su host impide acceso toohello aplicación puerto desde el intervalo IP toosite de punto. Para cruzar subredes, se requiere a menudo acceso público.
* el host de destino está inactivo;
* la aplicación está inactiva;
* había Hola incorrecto IP o nombre de host
* la aplicación escucha en un puerto diferente del que se esperaba. Puede comprobarlo si va a ese host y usar "netstat - aon" desde el símbolo del sistema de hello cmd. Esto le muestra qué identificador de proceso está escuchando en qué puerto; 
* los grupos de seguridad de red se configuran de forma que evitan los host de aplicación de tooyour de acceso y el puerto de su intervalo IP toosite de punto

Recuerde que no sabe qué IP en el intervalo IP de tooSite de punto que se va a usar la aplicación por lo que necesita acceso de tooallow desde el intervalo completo de Hola. 

Otros pasos de depuración son:

* Inicie sesión en otra máquina virtual en la red virtual e intente tooreach los recursos de host: puerto desde allí. Hay algunas utilidades ping basadas en TCP que sirven para este propósito o incluso puede usar telnet si es necesario. Hola propósito en este documento es toodetermine solo si hay conectividad desde esta otra máquina virtual. 
* abrir una aplicación en otra máquina virtual y tener acceso a toothat host y puerto de consola Hola desde la aplicación de prueba

#### <a name="on-premises-resources"></a>Recursos locales ####
Si la aplicación no puede tener acceso a recursos locales, debe comprobar primero que de hello es si puede llegar a un recurso de la red virtual. Si eso funciona, intente aplicación de tooreach Hola local de una máquina virtual en hello red virtual. Puede usar telnet o una utilidad ping basada en TCP. Si la máquina virtual no puede conectar con el recurso local, asegúrese de que la conexión de VPN de sitio tooSite funciona. Si está en funcionamiento, compruebe Hola lo mismo se ha indicado anteriormente, así como la configuración de puerta de enlace local de Hola y el estado. 

Ahora si hospeda la red virtual VM puede llegar a su sistema local pero la aplicación no puede, a continuación, el motivo de hello es probablemente una de las siguientes de hello:

* las rutas no están configuradas con los intervalos IP toosite de punto en la puerta de enlace local
* los grupos de seguridad de red están bloqueando el acceso para el intervalo IP tooSite de punto
* los firewalls locales están bloqueando el tráfico de su intervalo IP tooSite de punto
* tener un Route(UDR) de usuario definidos en la red virtual que impide que el tráfico en función de tooSite de punto de llegar a la red local

## <a name="hybrid-connections-and-app-service-environments"></a>Conexiones híbridas y entornos del Servicio de aplicaciones
Hay tres características que permiten acceder a los recursos tooVNet hospedado. Son las siguientes:

* Integración con red virtual
* conexiones híbridas
* Entornos del Servicio de aplicaciones

Las conexiones híbridas requiere tooinstall un agente de retransmisión llamado hello Manager(HCM) de conexión híbrida en la red. Hola gestión necesita toobe tooconnect capaz de tooAzure y también tooyour aplicación. Esta solución es especialmente atractiva desde una red remota como su red local o incluso otra red hospedada en la nube porque no requiere un punto de conexión accesible por Internet. Hola gestión solo se ejecuta en Windows y puede tener hasta instancias toofive ejecutando tooprovide alta disponibilidad. Las conexiones híbridas solo admite TCP aunque y cada extremo HC tiene la combinación de toomatch tooa host: puerto específico. 

función del entorno de servicio de aplicación Hola permite toorun una instancia de servicio de aplicaciones de Azure de hello en la red virtual. Esto permite que sus aplicaciones accedan a recursos de la red virtual sin ningún paso adicional. Algunos de hello otras ventajas de un entorno de servicio de aplicaciones son que se pueden utilizar los trabajadores Dv2 según con too14 GB de RAM. Otra ventaja es que puede escalar Hola sistema toomeet sus necesidades. A diferencia de los entornos de varios inquilinos de Hola donde ASP es limitado too20 instancias, en un ASE se puede escalar too100 instancias ASP. Uno de los aspectos de Hola que se obtienen con un ASE que no lo hace con la integración de red virtual es que un entorno de servicio de aplicaciones pueden trabajar con una VPN de ExpressRoute. 

Aunque no hay que algunos superposición de casos de uso, ninguna de estas características puede reemplazar cualquiera del programa Hola a otros usuarios. Saber qué toouse característica está ligada tooyour necesidades. Por ejemplo:

* Si es un desarrollador y simplemente deseen toorun un sitio en Azure y tiene tener acceso a base de datos de hello en la estación de trabajo de hello en el departamento de soporte, toouse lo más fácil de hello es conexiones híbridas. 
* Si una organización de gran tamaño que desea tooput un gran número de propiedades de web de nube pública de Hola y administrarlos en su propia red, a continuación, deberá toogo con hello entorno del servicio de aplicaciones. 
* Si tiene un número de servicio de aplicaciones hospedan aplicaciones y simplemente desea tooaccess recursos de la red virtual, integración de la red virtual será Hola forma toogo. 

Más allá de los casos de uso de hello, hay algunos simplicidad relacionados con aspectos. Si la red virtual ya está conectada tooyour red, a continuación, mediante la integración de red virtual local o un entorno de servicio de aplicaciones es una manera sencilla de tooconsume recursos locales. En hello otra parte, si la red virtual no es tooyour local de red conectados a es mucho que más tooset sobrecarga de una VPN a la red virtual de sitio toosite comparada con la instalación Hola gestión. 

Más allá Hola diferencias funcionales, existe también son precios de las diferencias. función del entorno de servicio de aplicación Hola es un servicio de Premium ofrecen pero Hola ofrece la mayoría de las posibilidades de configuración de red además tooother excelentes características. Integración de la red virtual puede usarse con Standard o Premium ASP y es perfecta para consumir recursos de la red virtual de servicio de aplicaciones de varios inquilinos de Hola de forma segura. Conexiones híbridas actualmente depende de un BizTalk las cuentas que tengan niveles que se inician libre y, a continuación, obtener progresivamente más costoso de precios según cantidad Hola necesita. Cuando se trata tooworking en muchas redes sin embargo, no hay ninguna otra característica como conexiones híbridas, lo que hace posible tooaccess recursos en más de 100 redes independientes. 

<!--Image references-->
[1]: ./media/web-sites-integrate-with-vnet/vnetint-upgradeplan.png
[2]: ./media/web-sites-integrate-with-vnet/vnetint-existingvnet.png
[3]: ./media/web-sites-integrate-with-vnet/vnetint-createvnet.png
[4]: ./media/web-sites-integrate-with-vnet/vnetint-howitworks.png
[5]: ./media/web-sites-integrate-with-vnet/vnetint-appmanage.png
[6]: ./media/web-sites-integrate-with-vnet/vnetint-aspmanage.png
[7]: ./media/web-sites-integrate-with-vnet/vnetint-aspmanagedetail.png
[8]: ./media/web-sites-integrate-with-vnet/vnetint-vnetp2s.png

<!--Links-->
[VNETOverview]: http://azure.microsoft.com/documentation/articles/virtual-networks-overview/ 
[AzurePortal]: http://portal.azure.com/
[ASPricing]: http://azure.microsoft.com/pricing/details/app-service/
[VNETPricing]: http://azure.microsoft.com/pricing/details/vpn-gateway/
[DataPricing]: http://azure.microsoft.com/pricing/details/data-transfers/
[V2VNETP2S]: http://azure.microsoft.com/documentation/articles/vpn-gateway-howto-point-to-site-rm-ps/
[IntPowershell]: http://azure.microsoft.com/documentation/articles/app-service-vnet-integration-powershell/
[ASEintro]: http://docs.microsoft.com/azure/app-service/app-service-environment/intro
[ILBASE]: http://docs.microsoft.com/azure/app-service/app-service-environment/create-ilb-ase
[V2VNETPortal]: https://docs.microsoft.com/en-us/azure/vpn-gateway/vpn-gateway-howto-point-to-site-resource-manager-portal
[VPNERCoex]: http://docs.microsoft.com/en-us/azure/expressroute/expressroute-howto-coexist-resource-manager
[ASE]: http://docs.microsoft.com/azure/app-service/app-service-environment/intro
