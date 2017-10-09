---
title: "solución de Monitor de rendimiento en Azure Log Analytics aaaNetwork | Documentos de Microsoft"
description: "Monitor de rendimiento de red en el análisis de registros de Azure le ayuda a supervisar el rendimiento de Hola de sus redes en casi real tiempo toodetect y buscar cuellos de botella de rendimiento de red."
services: log-analytics
documentationcenter: 
author: bandersmsft
manager: carmonm
editor: 
ms.assetid: 5b9c9c83-3435-488c-b4f6-7653003ae18a
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/11/2017
ms.author: banders
ms.openlocfilehash: e074948221fdd003c640861d759c4ce69ced1cd7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="network-performance-monitor-solution-in-log-analytics"></a>Solución Monitor de rendimiento de red de Log Analytics

![Símbolo de Network Performance Monitor](./media/log-analytics-network-performance-monitor/npm-symbol.png)

Este documento describe cómo tooset vertical y use Hola solución de Monitor de rendimiento de red en el análisis de registros, que le ayuda a supervisar el rendimiento de Hola de sus redes en casi real tiempo toodetect y buscar cuellos de botella de rendimiento de red. Con hello soluciones de Monitor de rendimiento de red, puede supervisar Hola pérdida y la latencia entre dos redes, subredes o servidores. Monitor de rendimiento de red detecta posibles problemas de red como blackholing de tráfico, enrutamiento errores y problemas que los métodos de supervisión de red convencional no son toodetect pueda. Monitor de rendimiento de red genera alertas y notifica cómo y cuándo se supera un umbral en un vínculo de red. Estos umbrales se pueden aprender automáticamente por el sistema de Hola o puede configurar reglas de alerta personalizados toouse. Monitor de rendimiento de red garantiza la detección oportuna de los problemas de rendimiento de red y localiza el origen de Hola de segmento de red determinado de hello problema tooa o un dispositivo.

Puede detectar problemas de red con el panel de la solución de Hola que muestra información resumida acerca de la red, incluidos vínculos de subred que se enfrentan a latencia y pérdida de paquetes alta, vínculos de red incorrectos y eventos recientes de mantenimiento de red. Puede desplazarse en un red vínculo tooview Hola actual estado de mantenimiento de vínculos de subred, así como vínculos de nodo a nodo. También puede ver las tendencias históricas de Hola de latencia en el nivel de nodo a nodo, subred y red hello y las pérdidas. Puede encontrar problemas de red transitorios visualizando gráficos de tendencias históricas de pérdida de paquetes y latencia, y buscar cuellos de botella de red en un mapa de topología. gráfico de topología interactivos de Hello permite rutas de red de salto a salto de toovisualize hello y determinar Hola origen del problema de Hola. Así como cualquier otras soluciones, puede usar la búsqueda de registro para el análisis de diversos informes personalizados de requisitos toocreate basan en datos de hello recopilados por el Monitor de rendimiento de red.

solución de Hello utiliza transacciones sintéticas como los errores de red de toodetect de un mecanismo principal. Por ello, puede utilizarla con independencia del modelo o el proveedor del dispositivo de red. Funciona en entornos locales, híbridos y en la nube (IaaS). solución de Hola detecta automáticamente la topología de red de Hola y varias rutas de la red.

Red típica supervisión productos se centran en supervisión Hola estado del dispositivo (enrutadores, conmutadores, etc.) de red, pero no proporcionan visiones Hola real de calidad de conectividad de red entre dos puntos, lo hace de Monitor de rendimiento de red.

### <a name="using-hello-solution-standalone"></a>Usa Hola solución independiente
Si desea que la calidad de hello toomonitor de conexiones de red entre sus cargas de trabajo críticas, redes, los centros de datos o sitios de office, se puede usar Hola Monitor de rendimiento de red solución por sí sola toomonitor estado de conectividad entre:

* varios centros de datos u oficinas que estén conectados con una red pública o privada;
* cargas de trabajo que ejecuten aplicaciones de línea de negocio;
* Servicios de nube pública como Microsoft Azure o redes de Amazon Web Services (AWS) y local, si tiene IaaS (VM) disponibles y tienen las puertas de enlace configuran tooallow comunicación entre redes locales y redes en la nube
* redes locales y de Azure cuando utilice ExpressRoute.

### <a name="using-hello-solution-with-other-networking-tools"></a>Usar soluciones de hello con otras herramientas de red
Si desea toomonitor una aplicación de línea de negocio, puede utilizar Hola soluciones de Monitor de rendimiento de red como un herramientas de complementaria de red de tooother de solución. Una red lenta puede provocar tooslow aplicaciones y Monitor de rendimiento de red puede ayudar a investigar los problemas de rendimiento de aplicación que se deben a problemas de red subyacentes. Porque Hola solución no requiere ningún dispositivo de toonetwork de acceso, Administrador de la aplicación hello no necesita toorely en una equipo tooprovide la información de red acerca de cómo red Hola está afectando a las aplicaciones.

Además, si ya invierte en otra herramientas de supervisión de red, solución Hola puede complementar estas herramientas porque más tradicionales soluciones de supervisión de red no proporcionan información sobre las métricas de rendimiento de red to-end como pérdida y la latencia.  Hola soluciones de Monitor de rendimiento de red puede ayudar a ese espacio de relleno.

## <a name="installing-and-configuring-agents-for-hello-solution"></a>Instalar y configurar los agentes para la solución de Hola
Usar agentes de tooinstall procesos básicos de hello en [tooLog de equipos de Windows conectarse análisis](log-analytics-windows-agents.md) y [tooLog de conexión de Operations Manager análisis](log-analytics-om-agents.md).

> [!NOTE]
> Podrá necesita a tooinstall al menos 2 agentes en orden toohave suficiente toodiscover de datos y supervisar los recursos de red. En caso contrario, solución de hello permanecerá en un estado de configuración hasta que instale y configure agentes adicionales.
>
>

### <a name="where-tooinstall-hello-agents"></a>Donde tooinstall Hola agentes
Antes de instalar agentes, considere la posibilidad de topología de saludo de la red y qué partes de Hola de red desea toomonitor. Se recomienda que instale a más de un agente para cada subred que desea toomonitor. En otras palabras, para cada subred que desea toomonitor, elija dos o más servidores o máquinas virtuales e instalar a agente de hello en ellos.

Si no está seguro acerca de la topología de saludo de la red, instalar a agentes de hello en servidores con cargas de trabajo críticas donde desea que el rendimiento de la red de toomonitor Hola. Por ejemplo, puede hacer seguimiento de tookeep de una conexión de red entre un servidor Web y un servidor que ejecuta SQL Server. En este ejemplo, podría instalar un agente en ambos servidores.

Los agentes supervisan la conectividad de red (vínculos) entre hosts--no Hola mismos hosts. Por lo tanto, toomonitor un vínculo de red, debe instalar agentes en los dos extremos del vínculo.

### <a name="configure-agents"></a>Configuración de los agentes

Si piensa que el protocolo ICMP de hello toouse para las transacciones sintéticas, necesita hello tooenable siguiendo las reglas de firewall para utilizar de forma confiable ICMP:

```
netsh advfirewall firewall add rule name="NPMDICMPV4Echo" protocol="icmpv4:8,any" dir=in action=allow
netsh advfirewall firewall add rule name="NPMDICMPV6Echo" protocol="icmpv6:128,any" dir=in action=allow
netsh advfirewall firewall add rule name="NPMDICMPV4DestinationUnreachable" protocol="icmpv4:3,any" dir=in action=allow
netsh advfirewall firewall add rule name="NPMDICMPV6DestinationUnreachable" protocol="icmpv6:1,any" dir=in action=allow
netsh advfirewall firewall add rule name="NPMDICMPV4TimeExceeded" protocol="icmpv4:11,any" dir=in action=allow
netsh advfirewall firewall add rule name="NPMDICMPV6TimeExceeded" protocol="icmpv6:3,any" dir=in action=allow
```


Si piensa toouse Hola protocolo TCP debe tooopen puertos del firewall para esos tooensure de equipos agentes puedan comunicarse. Tiene que toodownload y, a continuación, ejecutar hello [script de PowerShell de EnableRules.ps1](https://gallery.technet.microsoft.com/OMS-Network-Performance-04a66634) sin ningún parámetro en una ventana de PowerShell con privilegios administrativos.

script de Hola crea claves del registro necesarias por hello Monitor de rendimiento de red y se crea el firewall de Windows las conexiones TCP de reglas tooallow agentes toocreate entre sí. claves de registro de Hello creadas por el script de Hola también especifican si toolog Hola Depurar registros y la ruta de acceso de hello para el archivo de registros de hello. También define el puerto TCP de agente Hola usado para la comunicación. valores de Hello para estas claves se establecen automáticamente script de Hola, por lo que no debe cambiar manualmente estas claves.

puerto de Hello abre de forma predeterminada es 8084. Puede utilizar un puerto personalizado proporcionando el parámetro hello `portNumber` toohello script. Sin embargo, hello mismo puerto debe utilizarse en todos los equipos de Hola donde se ejecuta el script de Hola.

> [!NOTE]
> Hola EnableRules.ps1 script configura reglas de firewall de Windows sólo en equipo Hola donde se ejecuta el script de Hola. Si tiene un firewall de red, debe asegurarse de que permite el tráfico destinado al puerto TCP de Hola que se va a usar Monitor de rendimiento de red.
>
>

## <a name="configuring-hello-solution"></a>Configuración de solución de Hola
Usar hello después tooinstall de información y configurar soluciones de Hola.

1. Hola soluciones de Monitor de rendimiento de red adquiere datos desde equipos que ejecutan Windows Server 2008 Service Pack 1 o posterior o Windows 7 SP1 o versiones posteriores, que son Hola mismo requisitos de Hola Microsoft Monitoring Agent (MMA). Los agentes NPM se pueden ejecutar también en sistemas operativos escritorio/cliente de Windows (Windows 10, Windows 8.1, Windows 8 y Windows 7).
    >[!NOTE]
    >agentes de Hola para sistemas operativos Windows server admiten TCP e ICMP como protocolos de Hola para transacciones sintéticas. Sin embargo, los agentes de Hola para sistemas operativos cliente Windows sólo admiten ICMP como protocolo de Hola para transacciones sintéticas.

2. Agregar área de trabajo de hello Monitor de rendimiento de red solución tooyour de [Azure marketplace](https://azuremarketplace.microsoft.com/marketplace/apps/Microsoft.NetworkMonitoringOMS?tab=Overview) o mediante el proceso de hello descrito en [soluciones de análisis de registro agregar desde la Galería de soluciones de hello](log-analytics-add-solutions.md).  
   ![Símbolo del Network Performance Monitor](./media/log-analytics-network-performance-monitor/npm-symbol.png)
3. Portal de OMS de hello, verá un icono nuevo denominado **Monitor de rendimiento de red** con mensajes de bienvenida *solución requiere configuración adicional*. Necesitará tooconfigure Hola solución tooadd las redes en función de las subredes y los nodos que se detectan agentes. Haga clic en **Monitor de rendimiento de red** toostart la configuración de red predeterminada de Hola.  
   ![La solución necesita una configuración adicional](./media/log-analytics-network-performance-monitor/npm-config.png)

### <a name="configure-hello-solution-with-a-default-network"></a>Configurar la solución de hello con una red de forma predeterminada
En la página de configuración de hello, verá una única red denominada **predeterminado**. Si no ha definido ninguna red, todas las subredes de hello detectan automáticamente se colocan en la red predeterminada de Hola.

Siempre que cree una red, agregará un tooit de subred y esa subred se quita de la red predeterminada de Hola. Si elimina una red, todas sus subredes se devuelven automáticamente toohello red de forma predeterminada.

En otras palabras, la red predeterminada de hello es contenedor de Hola para todas las subredes de Hola que no estén contenidas en cualquier red definida por el usuario. No se puede editar o eliminar la red predeterminada de Hola. Siempre permanece en el sistema de Hola. Sin embargo, puede crear todas las redes que necesite.

En la mayoría de los casos, las subredes de hello en su organización se organizarán en más de una red y debería crear una o más toologically redes grupo las subredes.

### <a name="create-new-networks"></a>Creación de nuevas redes
En el Monitor de rendimiento de red, una red es un contenedor de subredes. Puede crear una red con cualquier nombre que desee y agregar subredes toohello red. Por ejemplo, puede crear una red denominada *edificio1* y, a continuación, agregar subredes, o puede crear una red denominada *DMZ* y, a continuación, agregue todas las subredes que pertenecen a red de toodemilitarized zona toothis.

#### <a name="toocreate-a-new-network"></a>toocreate una nueva red
1. Haga clic en **agregar red** y, a continuación, escriba nombre de red de hello y una descripción.
2. Seleccione una o varias subredes y, luego, haga clic en **Agregar**.
3. Haga clic en **guardar** configuración de toosave Hola.  
   ![Agregar red](./media/log-analytics-network-performance-monitor/npm-add-network.png)

### <a name="wait-for-data-aggregation"></a>Tiempo de espera hasta que se agreguen los datos
Después de guardar configuración de Hola por primera vez, solución de hello empieza a recopilar información de latencia y pérdida de paquetes de red entre los nodos de Hola donde están instalados los agentes. Este proceso puede tardar bastante, en ocasiones más de 30 minutos. Durante este estado, mosaico de Monitor de rendimiento de red de hello en la página de información general de hello muestra un mensaje que notifica *agregación de datos en proceso*.

![Agregación de datos en curso](./media/log-analytics-network-performance-monitor/npm-aggregation.png)

Cuando se hayan cargado los datos de hello, podrá ver datos de Hola que muestra actualizado de mosaico de Monitor de rendimiento de red.

![Icono Monitor de rendimiento de red](./media/log-analytics-network-performance-monitor/npm-tile.png)

Haga clic en panel de Monitor de rendimiento de red de hello mosaico tooview Hola.

![Panel Monitor de rendimiento de red](./media/log-analytics-network-performance-monitor/npm-dash01.png)

### <a name="edit-monitoring-settings-for-subnets"></a>Edición de la configuración de supervisión de subredes
Se muestran todas las subredes donde se instaló al menos un agente en hello **subredes** pestaña en la página de configuración de Hola.

#### <a name="tooenable-or-disable-monitoring-for-particular-subnetworks"></a>tooenable o deshabilitar la supervisión para determinada subredes
1. Active o desactive Hola cuadro siguiente toohello **Id. de subred** y, a continuación, asegúrese de que **uso para supervisión** está seleccionada o desactivada, según corresponda. Puede seleccionar o borrar varias subredes. Cuando está deshabilitado, las subredes no se supervisan como agentes de hello estará actualizada toostop hacer ping en otros agentes.
2. Elija nodos Hola que quiere toomonitor de una subred determinada, seleccione subred hello en lista de Hola y mover Hola nodos necesarios entre las listas de Hola que contiene los nodos no supervisados y supervisados.
   Puede agregar un personalizado **descripción** toohello de subred, si lo desea.
3. Haga clic en **guardar** configuración de toosave Hola.  
   ![Editar la subred](./media/log-analytics-network-performance-monitor/npm-edit-subnet.png)

### <a name="choose-nodes-toomonitor"></a>Elija toomonitor de nodos
Todos los nodos de Hola que tienen un agente instalado en ellos se muestran en hello **nodos** ficha.

#### <a name="tooenable-or-disable-monitoring-for-nodes"></a>tooenable o deshabilitar la supervisión para los nodos
1. Active o desactive los nodos de Hola que desee toomonitor o detener la supervisión.
2. Active la casilla **Usar para la supervisión** o desactívela, según corresponda.
3. Haga clic en **Guardar**.  
   ![Habilitar la supervisión de nodos](./media/log-analytics-network-performance-monitor/npm-enable-node-monitor.png)

### <a name="set-monitoring-rules"></a>Conjunto de reglas de supervisión
Monitor de rendimiento de red genera eventos de estado sobre la conectividad de hello entre un par de nodos o vínculos de red o de subred cuando se supera un umbral. Estos umbrales se pueden aprender automáticamente por el sistema de Hola o puede configurar reglas de alerta personalizadas.

Hola *regla predeterminada* creado por el sistema de Hola y crea un evento de estado cada vez que la pérdida o la latencia entre cualquier par de redes o subred vincula el umbral de infracciones Hola aprendido por el sistema. Puede elegir la regla predeterminada de toodisable hello y crear reglas personalizadas de supervisión

#### <a name="toocreate-custom-monitoring-rules"></a>toocreate personalizada de las reglas de supervisión
1. Haga clic en **Agregar regla** en hello **Monitor** pestaña y escriba el nombre de la regla de hello y una descripción.
2. Seleccione par Hola de red o subred toomonitor de vínculos en listas de Hola.
3. Primero seleccione red hello en qué Hola se encuentra la primera subred/s de interés en lista desplegable de red de hello y, a continuación, seleccione Hola subred/s de lista desplegable de subred correspondiente Hola.
   Seleccione **todas las subredes** si desea que toomonitor todos Hola subredes en un vínculo de red. De forma similar, seleccione Hola otra subred/s de interés. Y puede hacer clic en **Agregar excepción** tooexclude la supervisión de vínculos a una subred determinada de la selección de hello realizados.
4. Elija entre los protocolos ICMP y TCP para ejecutar transacciones sintéticas.
5. Si no desea toocreate eventos de mantenimiento para elementos de Hola que ha seleccionado, a continuación, desactive **habilitar la supervisión de mantenimiento en los vínculos de hello cubierto por esta regla**.
6. Elija las condiciones de supervisión.
   Puede establecer umbrales personalizados para la generación de eventos de estado escribiendo valores de umbral. Cada vez que el valor de Hola de condición de hello supera su umbral seleccionado para el par de red/subred seleccionada de hello, se genera un evento de estado.
7. Haga clic en **guardar** configuración de toosave Hola.  
   ![Crear una regla de supervisión personalizada](./media/log-analytics-network-performance-monitor/npm-monitor-rule.png)

Después de guardar una regla de supervisión, puede integrar esa regla con Administración de alertas haciendo clic en **Crear alerta**. Se crea automáticamente una regla de alerta con consultas de búsqueda de Hola y otros requiere parámetros rellenado de forma automática. Mediante una regla de alerta, puede recibir alertas de correo electrónico, además las alertas existentes de toohello dentro de NPM. Las alertas también pueden desencadenar acciones correctoras con runbooks o se pueden integrar con soluciones de administración de servicios existentes mediante webhooks. Puede hacer clic en **administrar alerta** tooedit configuración de alertas de Hola.

### <a name="choose-hello-right-protocol-icmp-or-tcp"></a>Elija el protocolo de hello derecha-ICMP o TCP

Monitor de rendimiento de red (NPM) usa métricas de rendimiento de red de las transacciones sintéticas toocalculate como la latencia de vínculo y de pérdida de paquetes. toounderstand esto mejor, considere la posibilidad de un NPM agente tooone conectado de final de un vínculo de red. Este NPM agente envía sondeo paquetes tooa segundo NPM agente tooanother conectado final de la red de Hola. Hola otro agente responde con paquetes de respuesta. Este proceso se repite varias veces. Mide el número de Hola de respuestas y tooreceive de tiempo que tarda cada respuesta, primer agente NPM Hola evalúa vínculo latencia y pérdida de paquetes.

Hello formato, el tamaño y la secuencia de estos paquetes se determina mediante Protocolo de Hola que elige al crear reglas de supervisión. En función de protocolo de paquetes de saludo, Hola dispositivos de red intermedios (enrutadores, conmutadores, etc.) puede procesar estos paquetes de forma diferente. Por lo tanto, su elección de protocolo afecta a la exactitud de Hola de resultados de Hola. Y la elección de protocolo también determina si debe realizar los pasos manualmente después de implementar soluciones NPM Hola.

NPM ofrece que Hola elegir entre protocolos ICMP y TCP para la ejecución de las transacciones sintéticas.
Si eliges ICMP cuando se crea una regla de transacción sintética, agentes NPM Hola usan latencia de red de eco ICMP mensajes toocalculate hello y pérdida de paquetes. Hola de usos de eco ICMP mismo del mensaje que se envía utilidad Ping convencional de Hola. Cuando se usa TCP como protocolo de hello, agentes NPM envían paquete TCP SYN a través de red de Hola. Esto va seguido de un protocolo de enlace TCP finalización y, a continuación, quitar conexión de hello mediante paquetes RST.

#### <a name="points-tooconsider-before-choosing-hello-protocol"></a>Tooconsider puntos antes de elegir el protocolo de Hola
Considere la posibilidad de hello siguiente información antes de elegir un toouse de protocolo:

##### <a name="discovering-multiple-network-routes"></a>Detección de varias rutas de red
TCP es más preciso cuando se detectan varias rutas y necesita menos agentes en cada subred. Por ejemplo, uno o dos agentes que utilicen TCP pueden detectar todas las rutas redundantes entre subredes. Sin embargo, deberá a varios agentes con resultados similares de tooachieve ICMP. Con ICMP, si tiene una cantidad *N* de rutas entre dos subredes, necesitará más de 5 veces *N* agentes en una subred de origen o de destino.

##### <a name="accuracy-of-results"></a>Precisión de los resultados
Conmutadores y enrutadores suelen tooassign tooICMP ECHO en comparación con los paquetes tooTCP paquetes de prioridad baja. En determinadas situaciones, cuando se cargan mucho los dispositivos de red, Hola obtenido mediante TCP más estrechamente reflejan pérdida de Hola y latencia de las aplicaciones que se ha producido. Esto ocurre porque la mayor parte del tráfico de la aplicación hello fluye a través de TCP. En tales casos, ICMP proporciona tooTCP de resultados en comparación con una precisión inferior.

##### <a name="firewall-configuration"></a>Configuración del firewall
Protocolo TCP requiere que los paquetes TCP se envíen tooa puerto de destino. Hola de puerto utilizado por los agentes NPM es 8084, sin embargo, puede cambiar este valor al configurar los agentes. Por lo tanto, debe tooensure que los firewalls de red o las reglas NSG (en Azure) están permitiendo el tráfico en el puerto de Hola. También necesita toomake seguro de que está configurado el firewall local hello en los equipos de Hola donde están instalados los agentes tooallow tráfico en este puerto.

Puede usar reglas de firewall de tooconfigure de secuencias de comandos de PowerShell en los equipos que ejecutan Windows, sin embargo, deberá tooconfigure el firewall de red manualmente.

En cambio, ICMP no utiliza ningún puerto. En la mayoría de los escenarios de empresa, se permite el tráfico ICMP a través de hello firewalls tooallow toouse herramientas de diagnóstico de red que Hola utilidad Ping. Por lo tanto, si puede hacer Ping en un equipo desde otro equipo, puede usar el protocolo ICMP Hola sin tener tooconfigure firewalls manualmente.

> [!NOTE]
> En caso de que no está seguro de qué protocolo toouse, elija toostart ICMP con. Si no está satisfecho con los resultados de hello, siempre podrá cambiar más adelante tooTCP.


#### <a name="how-tooswitch-hello-protocol"></a>¿Cómo tooswitch Hola protocolo

Si ha elegido toouse ICMP durante la implementación, puede cambiar tooTCP en cualquier momento mediante la edición predeterminada de hello las reglas de supervisión.

##### <a name="tooedit-hello-default-monitoring-rule"></a>regla de supervisión de tooedit Hola predeterminado
1.  Navegue demasiado**rendimiento de la red** > **Monitor** > **configurar** > **Monitor** y, a continuación, haga clic en **regla predeterminada**.
2.  Desplácese toohello **protocolo** sección y seleccione el protocolo de Hola que desea toouse.
3.  Haga clic en **guardar** configuración de tooapply Hola.

Incluso si la regla predeterminada de hello es mediante un protocolo específico, puede crear nuevas reglas con un protocolo diferente. Incluso puede crear una combinación de reglas que algunas de las reglas de hello usan ICMP y otro usa TCP.




## <a name="data-collection-details"></a>Detalles de la recopilación de datos
Monitor de rendimiento de red utiliza paquetes de protocolo de enlace de TCP SYN-SYNACK-confirmación cuando TCP está seleccionada y respuesta de eco de ICMP de eco de ICMP ICMP se elige como información de latencia y pérdida de la toocollect del protocolo Hola. Traceroute también es información de la topología de tooget usado.

Hello tabla siguiente muestran los métodos de recopilación de datos y otros detalles acerca de cómo se recopilan los datos de Monitor de rendimiento de red.

| plataforma | Agente directo | Agente de SCOM | Azure Storage | ¿Se necesita SCOM? | Datos del agente de SCOM enviados a través del grupo de administración | Frecuencia de recopilación |
| --- | --- | --- | --- | --- | --- | --- |
| Windows | &#8226; | &#8226; |  |  |  |Protocolos de enlace TCP/mensajes ICMP ECHO cada 5 segundos, datos enviados cada 3 minutos |

solución de Hello utiliza mantenimiento de las transacciones sintéticas tooassess Hola de red de Hola. Agentes OMS instalados en varias secciones de paquetes de saludo red exchange TCP o eco de ICMP (según el protocolo de hello seleccionado para la supervisión) entre sí. En proceso de hello, agentes información sobre Hola ida y vuelta tiempo y pérdida de paquetes, si existe. Periódicamente, cada agente también realiza una toofind de agentes de seguimiento ruta tooother que todos Hola diversas rutas de red de Hola que debe comprobarse. Con estos datos, pueden deducir los agentes de hello latencia de red de Hola y las cifras de pérdida de paquetes. pruebas de Hola se repiten cada cinco segundos y los datos se agregan durante un período de tres minutos por los agentes de hello antes de cargarlo toohello servicio de análisis de registros.

> [!NOTE]
> Aunque los agentes se comunican entre sí con frecuencia, que no generan una gran cantidad de tráfico de red mientras lleva a cabo pruebas de Hola. Agentes confían únicamente en TCP SYN-SYNACK-ACK mutuo paquetes toodetermine Hola pérdida y la latencia--ningún dato que se intercambian paquetes. Durante este proceso, los agentes se comunican entre sí cuando sea necesario y se optimiza la topología de comunicación de agente de hello tooreduce el tráfico de red.
>
>

## <a name="using-hello-solution"></a>Uso de solución de Hola
Esta sección explican todas las funciones de panel de Hola y cómo toouse ellos.

### <a name="solution-overview-tile"></a>Icono Información general del servicio
Después de habilitar la solución de Monitor de rendimiento de red de hello, icono de solución de hello en la página de información general de OMS Hola proporciona una vista rápida del estado de la red de Hola. Muestra un gráfico de anillos que muestra el número de Hola de vínculos de subred positiva y negativa. Al hacer clic en el icono de hello, abre el panel de la solución de Hola.

![Icono Monitor de rendimiento de red](./media/log-analytics-network-performance-monitor/npm-tile.png)

### <a name="network-performance-monitor-solution-dashboard"></a>Panel de la solución Monitor de rendimiento de red
Hola **red resumen** hoja muestra un resumen de las redes de hello junto con su tamaño relativo. Esto va seguido de iconos que muestra el número total de vínculos de red, vínculos de subred y las rutas de acceso de sistema de hello (una ruta de acceso se compone de direcciones IP de Hola de dos hosts con agentes y todos los saltos de hello entre ellos).

Hola **primeros eventos de estado de red** hoja proporciona una lista de eventos de estado más recientes y las alertas del sistema de Hola y tiempo de hello puesto que ha estado activa el evento de Hola. Se genera una alerta o un evento de estado cada vez que la pérdida de paquetes de Hola o de latencia de un vínculo de red o subred supera un umbral.

Hola **vínculos de red mal superior** hoja muestra una lista de vínculos de red incorrectos. Estos son vínculos de red de Hola que tienen uno o más eventos de mantenimiento adversos para ellos en el momento de Hola.

Hola **vínculos de subred de la parte superior con pérdida más** y **vínculos de subred con una latencia más** hojas mostrar vínculos de subred superior de Hola por pérdida de paquetes y los más comunes vínculos de subred por latencia respectivamente. Puede esperar una latencia alta o cierta cantidad de pérdida de paquetes en determinados vínculos de red. Estos vínculos aparecen en listas de los diez principales Hola pero no están marcados como incorrecto.

Hola **consultas comunes** hoja contiene un conjunto de consultas de búsqueda que capturar directamente los datos de supervisión de red sin formato. Puede usar estas consultas como punto de partida a fin de crear las suyas propias para generar informes personalizados.

![Panel Monitor de rendimiento de red](./media/log-analytics-network-performance-monitor/npm-dash01.png)

### <a name="drill-down-for-depth"></a>Exploración en profundidad
Puede hacer clic en los distintos vínculos de hello solución panel toodrill en profundidad un poco más en cualquier área de interés. Por ejemplo, cuando recibe una alerta o un vínculo de red incorrectos aparecen en el panel de hello, puede hacer clic en él tooinvestigate aún más. Se le dirigirá tooa página que enumera todos los vínculos de subred de hello para el enlace de red específico de Hola. Usted será capaz de toosee Hola pérdida, latencia y estado de salud de cada vínculo de subred y rápidamente Obtenga más información sobre los vínculos de subred están causando el problema de Hola. Puede, a continuación, haga clic en **ver vínculos del nodo** toosee todos los vínculos de nodo de Hola de subred incorrecto Hola vinculan. A continuación, pueden ver los vínculos de nodo a nodo individuales y encontrar vínculos de nodo incorrectos de Hola.

Puede hacer clic en **ver topología** tooview topología de salto a salto Hola de rutas de hello entre los nodos de origen y destino de Hola. Hola rutas incorrecto o saltos se muestran en color rojo para que pueda identificar rápidamente parte determinada tooa de hello problema de red de Hola.

![Datos en profundidad](./media/log-analytics-network-performance-monitor/npm-drill.png)

### <a name="network-state-recorder"></a>Grabadora de estado de la red

Cada vista muestra una instantánea del estado de su red en un momento determinado del tiempo. De forma predeterminada, se muestra el estado más reciente de Hola. barra de Hello al principio de Hola de página de hello muestra hello punto en el tiempo para el que se muestra el estado de saludo. Puede elegir toogo en el tiempo y la vista de instantánea de Hola de su estado de la red haciendo clic en la barra de hello en **acciones**. También puede elegir tooenable o deshabilitar la actualización automática para cualquier página mientras ve el estado más reciente de Hola.

![estado de la red](./media/log-analytics-network-performance-monitor/network-state.png)

#### <a name="trend-charts"></a>Gráficos de tendencias
En cada nivel que exploración en profundidad, puede ver la tendencia de Hola de latencia para un vínculo de red y las pérdidas. También tiene a su disposición gráficos de tendencias para vínculos de subred y nodo. Puede cambiar el intervalo de tiempo de Hola para hello gráfico tooplot mediante el control de tiempo de hello en parte superior de hello del gráfico de Hola.

Gráficos de tendencia muestran una perspectiva histórica del rendimiento de Hola de un vínculo de red. Algunos problemas de red son transitorios por naturaleza y serían difícil toocatch solo mirando en el estado actual de Hola de red de Hola. Esto es porque problemas pueden expuesta rápidamente y desaparezca antes de que nadie lo Note, solo tooreappear en un momento posterior. Estos problemas transitorios también pueden ser difíciles para los administradores de la aplicación porque los emite a menudo superficie como inexplicable aumenta el tiempo de respuesta de aplicación, incluso cuando todos los componentes de la aplicación aparecen toorun sin problemas.

Puede detectar fácilmente esos tipos de problemas de examinando un gráfico de tendencia donde problema Hola aparecerá como un pico súbito en pérdida de latencia o un paquete de red.

![Gráfico de tendencias](./media/log-analytics-network-performance-monitor/npm-trend.png)

#### <a name="hop-by-hop-topology-map"></a>Mapa de topología de salto a salto
Hola topología de salto a salto de rutas entre dos nodos en un mapa de topología interactivo se muestra en el Monitor de rendimiento de la red. Puede ver el mapa de topología de hello seleccionando un vínculo de nodo y, a continuación, haga clic en **ver topología**. Además, puede ver el mapa de topología de Hola haciendo clic en **las rutas de acceso** icono Panel de Hola. Al hacer clic en **las rutas de acceso** en el panel de hello, tendrá tooselect Hola nodos de origen y de destino desde el panel de la parte izquierda de hello y, a continuación, haga clic en **trazar** rutas de hello tooplot entre los nodos de hello dos.

mapa de topología de Hello muestra cuántas rutas están entre Hola dos nodos y qué rutas de acceso Hola datos paquetes tomar. Cuellos de botella de rendimiento de red se marcan en rojo en el mapa de topología de Hola. Puede buscar una conexión de red defectuoso o un dispositivo de red defectuoso examinando los elementos color rojos en el mapa de topología de Hola.

Al hacer clic en un nodo o al mantener el mouse sobre él cuando en el mapa de topología de hello, podrá ver propiedades de hello del nodo de hello como FQDN y la dirección IP. Haga clic en un toosee de salto es la dirección IP. Puede elegir toofilter rutas determinadas mediante filtros de hello en el panel de acciones que puede contraerse de Hola. Y también puede simplificar las topologías de red Hola ocultando saltos intermedios hello mediante el control deslizante de hello en el panel de acciones de Hola. Puede acercar o salir del modo de mapa de topología de hello mediante el uso de la rueda del mouse.

Tenga en cuenta esa topología Hola que se muestra en el mapa de hello es topología de capa 3 y no contiene conexiones y dispositivos de capa 2.

![Mapa de topología de salto a salto](./media/log-analytics-network-performance-monitor/npm-topology.png)

#### <a name="fault-localization"></a>Localización de defectos
Monitor de rendimiento de red es capaz de toofind cuellos de botella de red de hello sin conexión de dispositivos de red toohello. Basado en datos de Hola que recopila desde la red de Hola y aplicando algoritmos avanzados en el gráfico de red de hello, Monitor de rendimiento de red hace una estimación de las partes de Hola de red que son origen de hello más probable del problema de hello probabilística.

Este enfoque resulta útil toodetermine Hola red cuellos de botella toohops de acceso no está disponible porque no requiere ningún toobe datos recopilado de dispositivos de red de hello, como conmutadores o enrutadores. Esto también es útil cuando saltos Hola entre dos nodos no están bajo su control administrativo. Por ejemplo, saltos de hello pueden ser enrutadores de ISP.

### <a name="log-analytics-search"></a>Búsqueda de Log Analytics
Todos los datos que se exponen gráficamente mediante panel de Monitor de rendimiento de red de Hola y páginas de obtención de detalles también está disponible de forma nativa en la búsqueda de análisis de registros. Puede consultar datos de hello mediante el lenguaje de consulta de búsqueda de Hola y crear informes personalizados mediante la exportación de hello datos tooExcel o Power BI. Hola **consultas comunes** hoja en el panel de hello tiene algunas consultas útiles que puede usar como punto de partida para crear sus propios informes y consultas de Hola.

![Consultas de búsqueda](./media/log-analytics-network-performance-monitor/npm-queries.png)

## <a name="investigate-hello-root-cause-of-a-health-alert"></a>Investigar la causa de Hola de una alerta de estado
Ahora que ha leído acerca del Monitor de rendimiento de red, echemos un vistazo a una investigación sencilla en hello causa de un evento de estado.

1. En la página de información general de hello, obtendrá una instantánea rápida del estado de saludo de la red mediante la observación de hello **Monitor de rendimiento de red** icono. Tenga en cuenta que fuera de subredes de hello 6 vínculos que se está supervisando, 2 tienen un estado incorrecto. Esta situación se debe investigar. Haga clic en panel de solución de hello mosaico tooview Hola.  
   ![Icono Monitor de rendimiento de red](./media/log-analytics-network-performance-monitor/npm-investigation01.png)
2. En la imagen del ejemplo de Hola a continuación, observará que hay un evento de estado un vínculo de red que está en mal estado. Decida el problema de hello tooinvestigate y haga clic en hello **DMZ2 DMZ1** toofind de vínculo de red a raíz de Hola de problema de Hola.  
   ![Ejemplo de vínculo de red incorrecto](./media/log-analytics-network-performance-monitor/npm-investigation02.png)
3. página de exploración en profundidad de Hello muestra todos los vínculos de subred de hello en **DMZ2 DMZ1** vínculo de red. Observará que para ambos vínculos de subred hello, latencia de hello ha cruzado umbral Hola hacer que el vínculo de red de hello incorrecto. También puede ver las tendencias de latencia de Hola de ambos vínculos de subred Hola. Puede utilizar el tiempo de hello control de selección en hello gráfico toofocus en hello necesario intervalo de tiempo. Puede ver la hora de hello del día de hello cuando latencia alcanza su máximo. Más adelante puede buscar registros de Hola para este problema de hello tooinvestigate período de tiempo. Haga clic en **ver vínculos del nodo** toodrill en profundidad aún más.  
   ![Ejemplo de vínculos de subred incorrectos](./media/log-analytics-network-performance-monitor/npm-investigation03.png)
4. Página anterior toohello similar, página de exploración en profundidad de Hola para vínculo de una subred determinada Hola se enumera sus vínculos de nodo que lo componen. Puede realizar acciones similares a continuación tal y como hizo en el paso anterior de Hola. Haga clic en **ver topología** topología de hello tooview entre los nodos de hello 2.  
   ![Ejemplo de vínculos de nodo incorrectos](./media/log-analytics-network-performance-monitor/npm-investigation04.png)
5. Todas las rutas de acceso de hello entre los nodos de hello 2 seleccionado se trazan en mapa de topología de Hola. Puede visualizar la topología de salto a salto Hola de rutas entre dos nodos en el mapa de topología de Hola. Proporciona una visión clara de cuántas rutas existen entre dos nodos de Hola y Hola qué rutas de acceso a paquetes de datos a realizar. Los cuellos de botella de rendimiento de red se marcan en rojo. Puede buscar una conexión de red defectuoso o un dispositivo de red defectuoso examinando los elementos color rojos en el mapa de topología de Hola.  
   ![Ejemplo de la vista de topología incorrecta](./media/log-analytics-network-performance-monitor/npm-investigation05.png)
6. pérdida de Hello, latencia y número de Hola de saltos en cada ruta de acceso se pueden revisar de hello **acción** panel. Utilice Hola scrollbar tooview Hola detalles de las rutas de acceso incorrecto.  Use Hola filtros tooselect Hola rutas de acceso con salto incorrecto de Hola para que topología Hola para hello solo selecciona las rutas de acceso se traza. Puede usar el toozoom de rueda del mouse dentro o fuera de mapa de topología de Hola.

   Hola por debajo de la imagen podrá ver claramente Hola a causa de hello problema áreas toohello sección concreta de la red de hello examinando las rutas de acceso de Hola y saltos en color rojo. Al hacer clic en un nodo del mapa de topología de hello revela propiedades Hola Hola del nodo de, incluidas Hola FQDN y la dirección IP. Al hacer clic en un salto muestra la dirección IP de hello del salto Hola.  
   ![Ejemplo de topología incorrecta con detalles sobre las rutas de acceso](./media/log-analytics-network-performance-monitor/npm-investigation06.png)

## <a name="provide-feedback"></a>Envío de comentarios

- **UserVoice** -puede publicar sus ideas para características de Monitor de rendimiento de red que desea que nos toowork en. Visite nuestra [página UserVoice](https://feedback.azure.com/forums/267889-log-analytics/category/188146-network-monitoring).
- **Únase a nuestra cohortes**: siempre estamos interesados en que se unan nuevos clientes a nuestra cohorte. Como parte de ella, podrá obtener un acceso anticipado toonew características y Ayúdenos a mejorar el Monitor de rendimiento de red. Si está interesado en unirse, rellene esta [encuesta rápida](https://aka.ms/npmcohort).

## <a name="next-steps"></a>Pasos siguientes
* [Buscar registros](log-analytics-log-searches.md) tooview obtener registros de datos de rendimiento de red.
