---
title: Equilibrio de carga de aaaUsing de servicios de Azure | Documentos de Microsoft
description: "Este tutorial muestra cómo toocreate un escenario mediante el uso de Hola cartera de equilibrio de carga de Azure: Traffic Manager, la puerta de enlace de aplicación y el equilibrador de carga."
services: traffic-manager
documentationcenter: 
author: liumichelle
manager: vitinnan
editor: 
ms.assetid: f89be3be-a16f-4d47-bcae-db2ab72ade17
ms.service: traffic-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 10/27/2016
ms.author: limichel
ms.openlocfilehash: d217047102d8c4828250dc0733e8ec9ee1e84b3f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="using-load-balancing-services-in-azure"></a>Uso de servicios de equilibrio de carga en Azure

## <a name="introduction"></a>Introducción

Microsoft Azure proporciona varios servicios para administrar cómo se distribuye el tráfico de red y se equilibra la carga. Puede usar estos servicios individualmente o combinar sus métodos, según sus necesidades, la solución óptima de toobuild Hola.

En este tutorial, primero definimos un caso de uso de cliente y ver cómo se puede establecer más sólidos y eficientes mediante Hola después de la cartera de equilibrio de carga de Azure: Traffic Manager, la puerta de enlace de aplicación y el equilibrador de carga. A continuación, se proporcionan instrucciones paso a paso para crear una implementación que es redundante geográficamente, distribuye el tráfico tooVMs y le ayuda a administran distintos tipos de solicitudes.

En un nivel conceptual, cada uno de estos servicios desempeña un papel distinto de jerarquía de equilibrio de carga de Hola.

* **Traffic Manager** proporciona equilibrio de carga de DNS global. Se examinan las solicitudes entrantes de DNS y responde con un extremo en buen estado, con arreglo a Hola enrutamiento cliente de Hola de directiva se ha seleccionado. Las opciones de los métodos de enrutamiento son:
  * Rendimiento enrutamiento toosend Hola solicitante toohello extremo más cercano en términos de latencia.
  * Prioridad de enrutamiento toodirect todo tráfico tooan punto de conexión, con otros extremos como copia de seguridad.
  * Ponderada round robin enrutamiento, que distribuye el tráfico basado en la ponderación de Hola que se asigna el punto de conexión tooeach.

  Hola cliente conecta directamente toothat extremo. Azure Traffic Manager detecta cuando un punto de conexión está en mal estado y, a continuación, las redirecciones de Hola instancia correcto de los clientes tooanother. Consulte demasiado[documentación de Azure Traffic Manager](traffic-manager-overview.md) toolearn más información acerca del servicio de Hola.
* **Application Gateway** proporciona un controlador de entrega de aplicaciones (ADC) como servicio, así como diversas funcionalidades de equilibrio de carga de nivel 7 para la aplicación. Permite a los clientes productividad de granja de servidores web toooptimize mediante la descarga de puerta de enlace de aplicaciones de toohello de finalización de SSL de la CPU. Otras capacidades de enrutamiento de nivel 7 incluyen la distribución de round robin de tráfico entrante, afinidad de sesión basado en cookies, enrutamiento basado en la ruta de acceso de direcciones URL y toohost de capacidad de hello varios sitios Web detrás de una puerta de enlace de aplicación único. Application Gateway puede configurarse como una puerta de enlace accesible desde Internet, una puerta de enlace solo para uso interno o una combinación de las dos. Application Gateway está completamente administrada por Azure, es escalable y tiene una elevada disponibilidad. Cuenta con un amplio conjunto de funcionalidades de diagnóstico y registro, lo que facilita su administración.
* **El equilibrador de carga** es una parte integral de la pila de Azure SDN hello, proporciona gran rendimiento y baja latencia capa 4 equilibrio de carga servicios para los protocolos de todos los UDP y TCP. Administra conexiones entrantes y salientes. Puede configurar los extremos con equilibrio de carga públicos e internos y definir reglas toomap entrada destinos de grupo de conexiones tooback-end utilizando HTTP y TCP sondeo de estado opciones toomanage disponibilidad del servicio.

## <a name="scenario"></a>Escenario

En este escenario de ejemplo, se usa un sitio web sencillo que sirve dos tipos de contenido: imágenes y páginas web representadas de forma dinámica. sitio Web de Hello debe ser geográficamente redundante y debería servir sus usuarios de hello más cercano (latencia más baja) toothem de ubicación. Hello desarrollador de la aplicación ha decidido que las direcciones URL que coinciden con Hola patrón/imágenes / * se atienden desde un grupo de máquinas virtuales que son diferentes del resto de Hola de granja de servidores de hello web dedicado.

Además, grupo VM predeterminado Hola servir contenido dinámico de hello tiene tootalk tooa back-end base de datos hospedada en un clúster de alta disponibilidad. toda la implementación de Hola se configura a través del Administrador de recursos de Azure.

El uso de equilibrador de carga, puerta de enlace de aplicaciones y Traffic Manager permite este sitio Web tooachieve estos objetivos de diseño:

* **Redundancia geográfica múltiples**: si una región se bloquea, rutas de Traffic Manager perfectamente tráfico toohello región más cercana sin la intervención del propietario de la aplicación hello.
* **Menor latencia**: dado que el Administrador de tráfico dirige automáticamente región más cercana de hello cliente toohello, cliente hello experimenta una menor latencia cuando se solicitan contenido de página Web de Hola.
* **Escalabilidad independiente**: porque la carga de trabajo de aplicación hello web está separado por tipo de contenido, propietario de la aplicación hello puede escalar cargas de trabajo de solicitud a Hola independientes entre sí. Puerta de enlace de aplicación garantiza que el tráfico de Hola se grupos derecho de toohello enrutado basados en hello especificado reglas y el estado de saludo de la aplicación hello.
* **Equilibrio de carga interno**: porque equilibrador de carga es delante de clúster de alta disponibilidad de hello, sólo el punto de conexión de hello activo y en buen estado para una base de datos está expuesto toohello aplicación. Además, un administrador de base de datos puede optimizar la carga de trabajo de hello mediante la distribución de las réplicas activas y pasivas en el clúster de hello independiente de la aplicación front-end de hello. Equilibrador de carga ofrece el clúster de alta disponibilidad de las conexiones toohello y garantiza que solo las bases de datos correcto reciben solicitudes de conexión.

Hello siguiente diagrama muestra la arquitectura de Hola de este escenario:

![Diagrama de la arquitectura de equilibrio de carga](./media/traffic-manager-load-balancing-azure/scenario-diagram.png)

> [!NOTE]
> En este ejemplo es solo una de muchas configuraciones posibles de servicios de hello equilibrio de carga que ofrece Azure. El Administrador de tráfico y puerta de enlace de aplicaciones, equilibrador de carga se pueden mezclar y toobest coincidente según sus necesidades de equilibrio de carga. Por ejemplo, si la descarga de SSL o el procesamiento de nivel 7 no son necesarios, se puede usar Load Balancer en lugar de Application Gateway.

## <a name="setting-up-hello-load-balancing-stack"></a>Configurar la pila de equilibrio de carga de Hola

### <a name="step-1-create-a-traffic-manager-profile"></a>Paso 1: Creación de un perfil de Traffic Manager

1. Hola portal de Azure, haga clic en **nuevo**y, a continuación, busque hello en marketplace "Perfil de Traffic Manager."
2. En hello **crear Traffic Manager perfil** hoja, escriba Hola siguiendo la información básica:

  * **Nombre**: proporciona un nombre de prefijo DNS para el perfil de Traffic Manager.
  * **Método de enrutamiento**: seleccione Hola directiva del método de enrutamiento de tráfico. Para obtener más información acerca de los métodos de hello, consulte [acerca del Administrador de tráfico de los métodos de enrutamiento de tráfico](traffic-manager-routing-methods.md).
  * **Suscripción**: seleccione suscripción Hola que contiene el perfil de Hola.
  * **Grupo de recursos**: grupo de recursos de hello Select que contiene el perfil de Hola. Puede ser un grupo de recursos nuevo o existente.
  * **Ubicación del grupo de recursos**: servicio de administrador de tráfico es la ubicación de tooa global y no está enlazado. Sin embargo, debe especificar una región para el grupo de Hola donde residen los metadatos de hello asociados con el perfil de Traffic Manager de Hola. Esta ubicación no influye en la disponibilidad de hello en tiempo de ejecución de perfil de Hola.

3. Haga clic en **crear** toogenerate Hola perfil de Traffic Manager.

  ![Hoja de creación de perfil de Traffic Manager](./media/traffic-manager-load-balancing-azure/s1-create-tm-blade.png)

### <a name="step-2-create-hello-application-gateways"></a>Paso 2: Crear hello las puertas de enlace de aplicaciones

1. Hola portal de Azure, en el panel izquierdo de hello, haga clic en **New** > **red** > **Application Gateway**.
2. Escriba Hola siguiendo la información básica acerca de la puerta de enlace de aplicaciones de hello:

  * **Nombre**: nombre de Hola de puerta de enlace de aplicación Hola.
  * **Tamaño de la SKU**: Hola tamaño de hello aplicación puerta de enlace, disponible como pequeño, mediano o grande.
  * **El número de instancias**: Hola número de instancias, un valor entre 2 y 10.
  * **Grupo de recursos**: grupo de recursos de Hola que contiene la puerta de enlace de aplicaciones de Hola. Puede ser un grupo de recursos existente o uno nuevo.
  * **Ubicación**: región Hola Hola aplicación puerta de enlace, que es Hola misma ubicación que el grupo de recursos de Hola. ubicación de Hello es importante, porque la red virtual de Hola y dirección IP pública deben estar en hello misma ubicación que la puerta de enlace de Hola.
3. Haga clic en **Aceptar**.
4. Definir la red virtual de hello, subred, IP de front-end y configuraciones de agente de escucha para puerta de enlace de aplicación Hola. En este escenario, es la dirección IP front-end de hello **público**, que permite que se toobe agregado como un perfil de Traffic Manager de punto de conexión toohello más adelante.
5. Configurar el agente de escucha de hello con uno de hello siguientes opciones:
    * Si utiliza HTTP, no hay nada tooconfigure. Haga clic en **Aceptar**.
    * Para usar HTTPS, se requiere configuración adicional. Consulte demasiado[crear una puerta de enlace de la aplicación](../application-gateway/application-gateway-create-gateway-portal.md), empezando en el paso 9. Cuando se haya completado la configuración de hello, haga clic en **Aceptar**.

#### <a name="configure-url-routing-for-application-gateways"></a>Configuración del enrutamiento de direcciones URL para puertas de enlace de aplicaciones

Cuando se elige un grupo back-end, una puerta de enlace de la aplicación que está configurado con una regla basada en la ruta de acceso tiene un patrón de ruta de acceso de dirección URL de solicitud de Hola en distribución Round-robin tooround de adición. En este escenario, vamos a agregar una regla basada en la ruta de acceso toodirect cualquier dirección URL con "/ images /\*" grupo de servidores de imagen toohello. Para obtener más información acerca de cómo configurar la dirección URL de enrutamiento basado en ruta de acceso para una puerta de enlace de aplicaciones, consulte demasiado[crear una regla basada en la ruta de acceso para una puerta de enlace de la aplicación](../application-gateway/application-gateway-create-url-route-portal.md).

![Diagrama de nivel de web de Application Gateway](./media/traffic-manager-load-balancing-azure/web-tier-diagram.png)

1. Desde el grupo de recursos, ir toohello instancia de puerta de enlace de aplicaciones de Hola que creó en la sección anterior de Hola.
2. En **configuración**, seleccione **grupos back-end**y, a continuación, seleccione **agregar** tooadd hello las máquinas virtuales que desea tooassociate con grupos de hello capa web back-end.
3. En hello **Agregar grupo back-end** hoja, escriba nombre de hello del grupo back-end de Hola y todas las direcciones IP de Hola de máquinas de Hola que residen en el grupo de Hola. En este escenario, se conectan dos grupos de servidores de back-end de máquinas virtuales.

  ![Hoja "Add backend pool" (Agregar grupo de back-end) de Application Gateway](./media/traffic-manager-load-balancing-azure/s2-appgw-add-bepool.png)

4. En **configuración** de puerta de enlace de aplicación Hola, seleccione **reglas**y, a continuación, haga clic en hello **en función de la ruta de acceso** botón tooadd una regla.

  ![Botón "Basada en ruta de acceso" de las reglas de Application Gateway](./media/traffic-manager-load-balancing-azure/s2-appgw-add-pathrule.png)

5. En hello **Agregar regla de ruta de acceso-based** hoja, configurar la regla de hello proporcionando Hola siguiente información.

   Configuración básica:

   + **Nombre**: nombre descriptivo de Hola de regla de Hola que sea accesible en el portal de Hola.
   + **Agente de escucha**: agente de escucha de Hola que se usa para la regla de Hola.
   + **Predeterminado grupo back-end**: Hola toobe de grupo back-end que se usa con la regla predeterminada de Hola.
   + **Configuración predeterminada de HTTP**: Hola HTTP configuración toobe utilizado con la regla predeterminada de Hola.

   Reglas basadas en ruta de acceso:

   + **Nombre**: nombre descriptivo de Hola de regla de ruta de acceso de Hola.
   + **Las rutas de acceso**: regla de ruta de acceso de Hola que se utiliza para reenviar el tráfico.
   + **Grupo back-end**: Hola toobe de grupo back-end que se usa con esta regla.
   + **Configuración de HTTP**: Hola HTTP configuración toobe utilizado con esta regla.

   > [!IMPORTANT]
   > Rutas de acceso: las rutas de acceso válidas deben comenzar por "/". Hola comodín "\*" se permite solo al final de Hola. Algunos ejemplos válidos son /xyz, /xyz\* o /xyz/\*.

   ![Hoja "Add path-based rule" (Agregar regla basada en ruta de acceso) para Application Gateway](./media/traffic-manager-load-balancing-azure/s2-appgw-pathrule-blade.png)

### <a name="step-3-add-application-gateways-toohello-traffic-manager-endpoints"></a>Paso 3: Agregar extremos de Traffic Manager de toohello de puertas de enlace de aplicaciones

En este escenario, el Administrador de tráfico es tooapplication conectado puertas de enlace (como está configurado en pasos anteriores de Hola) que se encuentran en regiones diferentes. Ahora que se configuran las puertas de enlace de aplicaciones de hello, Hola siguiente paso es tooconnect les tooyour perfil de Traffic Manager.

1. Abra el perfil de Traffic Manager. toodo buscar por lo tanto, en el grupo de recursos o busque Hola nombre de perfil de Traffic Manager Hola de **todos los recursos**.
2. En el panel izquierdo de hello, seleccione **extremos**y, a continuación, haga clic en **agregar** tooadd un punto de conexión.

  ![Botón "Agregar" de puntos de conexión de Traffic Manager](./media/traffic-manager-load-balancing-azure/s3-tm-add-endpoint.png)

3. En hello **Agregar extremo** hoja, crear un punto de conexión mediante la especificación de hello siguiente información:

  * **Tipo de**: Seleccionar tipo de hello del saldo tooload de punto de conexión. En este escenario, seleccione **extremo de Azure** porque se está conectando instancias de puerta de enlace de aplicaciones de toohello que se configuraron anteriormente.
  * **Nombre**: escriba Hola nombre de punto de conexión de Hola.
  * **Tipo de recurso de destino**: seleccione **dirección IP pública** y, a continuación, en **recurso de destino**, seleccione Hola IP pública de la puerta de enlace de aplicaciones de Hola que configuró anteriormente.

   ![Hoja "Add endpoint" (Agregar punto de conexión)](./media/traffic-manager-load-balancing-azure/s3-tm-add-endpoint-blade.png)

4. Ahora puede probar la configuración mediante el acceso a él con hello DNS de su perfil de Traffic Manager (en este ejemplo: TrafficManagerScenario.trafficmanager.net). Puede reenviar las solicitudes, abrirá o desconecta las máquinas virtuales y servidores web que se crearon en diferentes regiones y cambiar tootest de configuración de perfil de Traffic Manager de hello su instalación.

### <a name="step-4-create-a-load-balancer"></a>Paso 4: Creación de un equilibrador de carga

En este escenario, el equilibrador de carga distribuye las conexiones de bases de datos de toohello de nivel de hello web dentro de un clúster de alta disponibilidad.

Si el clúster de base de datos de alta disponibilidad está usando SQL Server AlwaysOn, consulte demasiado[configurar uno o más siempre en grupo de agentes de escucha disponibilidad](../virtual-machines/windows/sql/virtual-machines-windows-portal-sql-ps-alwayson-int-listener.md) para obtener instrucciones paso a paso.

Para obtener más información acerca de cómo configurar un equilibrador de carga interno, consulte [crear un equilibrador de carga interno en el portal de Azure hello](../load-balancer/load-balancer-get-started-ilb-arm-portal.md).

1. Hola portal de Azure, en el panel izquierdo de hello, haga clic en **New** > **red** > **equilibrador de carga**.
2. En hello **equilibrador de carga de crear** hoja, elija un nombre para el equilibrador de carga.
3. Conjunto hello **tipo** demasiado**interno**y elija la red virtual adecuada de Hola y la subred para tooreside de equilibrador de carga de hello en.
4. En **IP address assignment** (Asignación de direcciones IP), seleccione **Dinámica** o **Estática**.
5. En **grupo de recursos**, elija grupo de recursos de Hola Hola equilibrador de carga.
6. En **ubicación**, elija la región adecuada de Hola Hola equilibrador de carga.
7. Haga clic en **crear** equilibrador de carga de toogenerate Hola.

#### <a name="connect-a-back-end-database-tier-toohello-load-balancer"></a>Conectar un equilibrador de carga de toohello de nivel de base de datos back-end

1. En el grupo de recursos, observa el equilibrador de carga de Hola que creó en los pasos anteriores de Hola.
2. En **configuración**, haga clic en **grupos back-end**y, a continuación, haga clic en **agregar** tooadd un grupo back-end.

  ![Hoja "Add backend pool" (Agregar grupo de back-end) del equilibrador de carga](./media/traffic-manager-load-balancing-azure/s4-ilb-add-bepool.png)

3. En hello **Agregar grupo back-end** hoja, escriba Hola nombre de grupo de back-end de Hola.
4. Agregue los equipos individuales o un grupo de back-end de toohello de conjunto de disponibilidad.

#### <a name="configure-a-probe"></a>Configuración de un sondeo

1. En el equilibrador de carga, en **configuración**, seleccione **sondeos**y, a continuación, haga clic en **agregar** tooadd un sondeo.

 ![Hoja "Add probe" (Agregar sondeo) de Load Balancer](./media/traffic-manager-load-balancing-azure/s4-ilb-add-probe.png)

2. En hello **agregar sondeo** hoja, escriba nombre hello para la sonda de Hola.
3. Seleccione hello **protocolo** para la sonda de Hola. Para una base de datos, probablemente le convenga más un sondeo TCP que uno HTTP. toolearn más información sobre los sondeos del equilibrador de carga, consulte demasiado[sondeos del equilibrador de carga de entender](../load-balancer/load-balancer-custom-probe-overview.md).
4. Escriba hello **puerto** de su toobe de base de datos para tener acceso a sondeo Hola.
5. En **intervalo**, especifique con qué frecuencia tooprobe Hola aplicación.
6. En **umbral incorrecto**, especifique Hola número de errores de sondeo continuo que debe realizarse para toobe de máquina virtual de back-end de hello considera incorrecto.
7. Haga clic en **Aceptar** sondeo de hello toocreate.

#### <a name="configure-hello-load-balancing-rules"></a>Configurar reglas de equilibrio de carga de Hola

1. En **configuración** de un equilibrador de carga, seleccione **reglas de equilibrio de carga**y, a continuación, haga clic en **agregar** toocreate una regla.
2. En hello **regla de equilibrio de carga de agregar** hoja, escriba Hola **nombre** para la regla de equilibrio de carga de Hola.
3. Elija hello **dirección IP de front-end** de hello equilibrador de carga, **protocolo**, y **puerto**.
4. En **puerto back-end**, especifique Hola puerto toobe usa en el bloque de back-end de Hola.
5. Seleccione hello **grupo back-end** hello y **sondeo** que se crearon en hello pasos tooapply Hola regla anterior a.
6. En **persistencia de la sesión**, elija cómo desea Hola sesiones toopersist.
7. En **los tiempos de espera de inactividad**, especifique Hola número de minutos antes de un tiempo de inactividad.
8. En **Floating IP** (IP flotante), seleccione **Deshabilitada** o **Habilitada**.
9. Haga clic en **Aceptar** regla de toocreate Hola.

### <a name="step-5-connect-web-tier-vms-toohello-load-balancer"></a>Paso 5: Conectar equilibrador de carga de toohello de las máquinas virtuales de nivel de web

Ahora, configuramos Hola IP equilibrador de carga y la dirección de puerto front-end en las aplicaciones de Hola que se ejecutan en las máquinas virtuales de nivel web para cualquier conexión de base de datos. Esta configuración es específica toohello aplicaciones que se ejecutan en estas máquinas virtuales. dirección IP de destino de tooconfigure Hola y el puerto, consulte la documentación de la aplicación de toohello. dirección IP de hello toofind de front-end de hello, Hola portal de Azure, vaya toohello grupo de direcciones IP front-end en hello **configuración de equilibrador de carga** hoja.

![Panel de navegación "Frontend IP pool" (Grupo de IP de font-end) de Load Balancer](./media/traffic-manager-load-balancing-azure/s5-ilb-frontend-ippool.png)

## <a name="next-steps"></a>Pasos siguientes

* [¿Qué es Traffic Manager?](traffic-manager-overview.md)
* [Introducción a Application Gateway](../application-gateway/application-gateway-introduction.md)
* [Información general sobre Azure Load Balancer](../load-balancer/load-balancer-overview.md)
