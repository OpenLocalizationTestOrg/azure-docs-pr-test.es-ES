---
title: "aaaTroubleshooting y supervisión de SAP HANA en Azure (instancias de gran tamaño) | Documentos de Microsoft"
description: "Solución de problemas y supervisión de SAP HANA en Azure (Instancias grandes)."
services: virtual-machines-linux
documentationcenter: 
author: RicksterCDN
manager: timlt
editor: 
ms.service: virtual-machines-linux
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 12/01/2016
ms.author: rclaus
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 1f1cd35820e227fd99af495431cd4b826aa53600
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="how-tootroubleshoot-and-monitor-sap-hana-large-instances-on-azure"></a>¿Cómo tootroubleshoot y monitor de SAP HANA (instancias de gran tamaño) en Azure


## <a name="monitoring-in-sap-hana-on-azure-large-instances"></a>Supervisión de SAP HANA en Azure (Instancias grandes)

SAP HANA en Azure (instancias de gran tamaño) no es diferente de cualquier otra implementación de IaaS, es necesario toomonitor qué Hola OS y aplicación hello es hacerlo y cómo estos consumen Hola recursos siguientes:

- CPU
- Memoria
- Ancho de banda de red
- Espacio en disco

Como con las máquinas virtuales Azure necesite toofigure si son suficientes las clases de recursos de hello mencionadas anteriormente, o si éstos obtengan agota. Aquí es más detalle en cada una de las distintas clases de hello:

**Consumo de recursos de CPU:** proporción de Hola que SAP definido para ciertas cargas de trabajo con HANA es obligatorio toomake seguro de que debe haber suficientes recursos de CPU disponible toowork a través de los datos de Hola que se almacenan en memoria. No obstante, puede darse el caso donde HANA consume mucha CPU al ejecutar consultas de vencimiento toomissing índices o problemas similares. Esto significa que debe supervisar el consumo de recursos de CPU de la unidad de hello HANA instancia grande, así como los recursos de CPU utilizados por servicios concretos de HANA de Hola.

**Consumo de memoria:** es importante toomonitor desde dentro de HANA, así como fuera de HANA en la unidad de Hola. Dentro de HANA, supervisar cómo consume datos de hello HANA asignado a la memoria en toostay de orden dentro de hello necesario ajustar el tamaño de las directrices de SAP. También puede toomonitor el consumo de memoria en hello instancia grande toomake nivel seguro que adicionales HANA-no instalado software no consumir demasiada memoria y, por tanto, entren en conflicto con HANA para la memoria.

**Ancho de banda de red:** puerta de enlace de red virtual de Azure Hola está limitado el ancho de banda de datos que se transfieren en hello red virtual de Azure, por lo que resulta útil toomonitor datos de saludo recibidos por todos los Hola máquinas virtuales de Azure dentro de un toofigure de red virtual información acerca de cómo cerrar son límites de toohello de hello Azure puerta de enlace de SKU que ha seleccionado. En la unidad de instancia grande de HANA hello, que le sentido toomonitor entrantes y salientes tráfico de red así y realizar un seguimiento de tookeep de volúmenes de Hola que se administran con el tiempo.

**Espacio en disco:** normalmente su uso aumenta a lo largo del tiempo. Hay muchas razones para ello, pero las principales son: aumenta el volumen de datos, la ejecución de copias de seguridad de los registros de transacciones, el almacenamiento de los archivos de seguimiento y la realización de instantáneas de almacenamiento. Por lo tanto, es importante toomonitor uso del espacio de disco y administrar espacio en disco Hola asociado con una unidad de instancia grande de HANA Hola.

## <a name="monitoring-and-troubleshooting-from-hana-side"></a>Supervisión y solución de problemas en el lado HANA

En orden tooeffectively analizar problemas relacionados tooSAP HANA en Azure (instancias grandes), resulta útil toonarrow hacia abajo de la causa raíz de Hola de un problema. SAP ha publicado una gran cantidad de documentación toohelp.

Aplicable preguntas más frecuentes relacionadas tooSAP HANA rendimiento puede encontrarse en hello siguiendo las notas de SAP:

- [SAP Note #2222200 – FAQ: SAP HANA Network](https://launchpad.support.sap.com/#/notes/2222200) (Nota de SAP 2222200: preguntas más frecuentes sobre la red de SAP HANA)
- [SAP Note #2100040 – FAQ: SAP HANA CPU](https://launchpad.support.sap.com/#/notes/0002100040) (Nota de SAP 2100040: preguntas más frecuentes sobre la CPU de SAP HANA)
- [SAP Note #199997 – FAQ: SAP HANA Memory](https://launchpad.support.sap.com/#/notes/2177064) (Nota de SAP 199997: preguntas más frecuentes sobre la memoria de SAP HANA)
- [SAP Note #200000 – FAQ: SAP HANA Performance Optimization](https://launchpad.support.sap.com/#/notes/2000000) (Nota de SAP 199997: preguntas más frecuentes sobre la optimización del rendimiento de SAP HANA)
- [SAP Note #199930 – FAQ: SAP HANA I/O Analysis](https://launchpad.support.sap.com/#/notes/1999930) (Nota de SAP 199930: preguntas más frecuentes sobre el análisis de E/S de SAP HANA)
- [SAP Note #2177064 – FAQ: SAP HANA Service Restart and Crashes](https://launchpad.support.sap.com/#/notes/2177064) (Nota de SAP #2177064: preguntas más frecuentes sobre el reinicio y la caída del servicio)

**Alertas de SAP HANA**

Como primer paso, compruebe los registros de alertas de SAP HANA actuales Hola. En SAP HANA Studio, vaya demasiado**consola de administración: alertas: mostrar: todas las alertas**. Esta ficha muestra todas las alertas de SAP HANA determinados valores (memoria física libre, el uso de CPU, etc.) que se encuentran fuera de hello establecer la duración mínima y máximos umbrales. De forma predeterminada, las comprobaciones se actualizan automáticamente cada 15 minutos.

![En SAP HANA Studio, vaya tooAdministration consola: alertas: mostrar: todas las alertas](./media/troubleshooting-monitoring/image1-show-alerts.png)

**CPU**

Para una alerta desencadenada debido tooimproper umbral configurado, una resolución es tooreset toohello valor o un valor de umbral más razonable.

![Restablecer el valor predeterminado de toohello o un valor de umbral más razonable](./media/troubleshooting-monitoring/image2-cpu-utilization.png)

Hola siguiendo las alertas puede indicar problemas de recursos de CPU:

- Uso de CPU del host (alerta 5)
- Operación del punto de retorno más reciente (alerta 28)
- Duración del punto de retorno (alerta 54)

Puede observar alto consumo de CPU en la base de datos de SAP HANA desde uno de hello siguientes:

- La alerta 5 (Uso de CPU del host) se desencadena para el uso de CPU actual o antiguo
- Hello muestra el uso de CPU en pantalla de información general de bienvenida

![Muestra el uso de CPU en pantalla de información general de bienvenida](./media/troubleshooting-monitoring/image3-cpu-usage.png)

gráfico de carga de Hello podría mostrar alto consumo de CPU o más consumo Hola anteriores:

![gráfico de carga de Hello puede mostrar alto consumo de CPU o más consumo Hola anteriores](./media/troubleshooting-monitoring/image4-load-graph.png)

Alerta desencadenada debido a la utilización de CPU toohigh pueden deberse a varias razones, entre ellas, pero sin limitarse a: ejecución de ciertas transacciones, carga de datos, que no responden de trabajos de larga ejecución instrucciones SQL y el rendimiento de consulta no válidos (por ejemplo, con BW en HANA cubos).

Consulte toohello [solución de problemas de SAP HANA: hace relacionados de CPU y soluciones](http://help.sap.com/saphelp_hanaplatform/helpdata/en/4f/bc915462db406aa2fe92b708b95189/content.htm?frameset=/en/db/6ca50424714af8b370960c04ce667b/frameset.htm&amp;current_toc=/en/85/d132c3f05e40a2b20c25aa5fd6331b/plain.htm&amp;node_id=46&amp;show_children=false) sitio pasos de solución de problemas detallada.

**Sistema operativo**

Uno de los más importantes de hello comprueba para SAP HANA en Linux es toomake seguro de que estén deshabilitadas transparente páginas muy grandes, consulte [SAP nota #2131662: transparente enorme páginas (THP) en servidores de SAP HANA](https://launchpad.support.sap.com/#/notes/2131662).

- Puede comprobar si hay páginas enorme transparente habilitadas a través de hello siguiente comando de Linux: **cat /sys/kernel/mm/transparent\_hugepage/habilitado**
- Si _siempre_ se encierra entre corchetes como sigue, significa que están habilitadas Hola transparente enorme páginas: [siempre] madvise nunca; si _nunca_ se incluye entre corchetes como sigue, significa que Hola transparente Páginas enormes están deshabilitadas: siempre madvise [nunca]

Hola siguiente comando de Linux debe devolver nada: **rpm - qa | grep ulimit.** Si indica que _ulimit_ está instalado, desinstálelo inmediatamente.

**Memoria**

Puede observar esa cantidad de Hola de memoria asignada por hello SAP HANA, base de datos es mayor de lo esperado. Hola siguiendo las alertas indica problemas con mayor uso de memoria:

- Uso de memoria física del host (alerta 1)
- Uso de memoria del servidor de nombres (alerta 12)
- Uso total de la memoria de las tablas de almacenamiento de columnas (alerta 40)
- Uso de memoria de los servicios (alerta 43)
- Uso de memoria del almacenamiento principal de las tablas de almacenamiento de columnas (alerta 45)
- Archivos de volcado de tiempo de ejecución (alerta 46)

Consulte toohello [solución de problemas de SAP HANA: problemas de memoria](http://help.sap.com/saphelp_hanaplatform/helpdata/en/db/6ca50424714af8b370960c04ce667b/content.htm?frameset=/en/59/5eaa513dde43758b51378ab3315ebb/frameset.htm&amp;current_toc=/en/85/d132c3f05e40a2b20c25aa5fd6331b/plain.htm&amp;node_id=26&amp;show_children=false) sitio pasos de solución de problemas detallada.

**Red**

Consulte demasiado[SAP nota #2081065: solución de problemas de red de SAP HANA](https://launchpad.support.sap.com/#/notes/2081065) y realice los pasos descritos en esta nota de SAP de solución de problemas de red de Hola.

1. Analice el tiempo de ida y vuelta entre el cliente y el servidor.
  A. Ejecutar script SQL de hello [ _HANA\_red\_clientes_](https://launchpad.support.sap.com/#/notes/1969700)_._
  
2. Analice la comunicación entre nodos.
  A. Ejecute el script SQL [_HANA\_Network\_Services_](https://launchpad.support.sap.com/#/notes/1969700)_._

3. Ejecute el comando de Linux **ifconfig** (salida de hello muestra si se producen las pérdidas de paquetes).
4. Ejecute el comando de Linux **tcpdump**.

Además, utilizar código abierto de hello [IPERF](https://iperf.fr/) herramienta (o similar) rendimiento de la red de toomeasure real de la aplicación.

Consulte toohello [solución de problemas de SAP HANA: problemas de conectividad y de rendimiento de red](http://help.sap.com/saphelp_hanaplatform/helpdata/en/a3/ccdff1aedc4720acb24ed8826938b6/content.htm?frameset=/en/dc/6ff98fa36541e997e4c719a632cbd8/frameset.htm&amp;current_toc=/en/85/d132c3f05e40a2b20c25aa5fd6331b/plain.htm&amp;node_id=142&amp;show_children=false) sitio pasos de solución de problemas detallada.

**Almacenamiento**

Desde la perspectiva del usuario final, una aplicación (o sistema de Hola como un todo) se ejecuta con lentitud, deja de responder o incluso puede parecer toohang si hay problemas de rendimiento de E/S. Hola **volúmenes** ficha en SAP HANA Studio, puede ver Hola adjunta volúmenes y los volúmenes se utilizan por cada servicio.

![En la ficha de volúmenes de hello en SAP HANA Studio, puede ver Hola adjunta volúmenes y los volúmenes se utilizan por cada servicio](./media/troubleshooting-monitoring/image5-volumes-tab-a.png)

Los volúmenes conectados en la parte inferior de Hola de pantalla de bienvenida, de que puede ver detalles Hola volúmenes, como archivos y estadísticas de E/S.

![Los volúmenes conectados en la parte inferior de Hola de pantalla de bienvenida, de que puede ver detalles Hola volúmenes, como archivos y estadísticas de E/S](./media/troubleshooting-monitoring/image6-volumes-tab-b.png)

Consulte toohello [solución de problemas de SAP HANA: E/S relacionados causas y soluciones](http://help.sap.com/saphelp_hanaplatform/helpdata/en/dc/6ff98fa36541e997e4c719a632cbd8/content.htm?frameset=/en/47/4cb08a715c42fe9f7cc5efdc599959/frameset.htm&amp;current_toc=/en/85/d132c3f05e40a2b20c25aa5fd6331b/plain.htm&amp;node_id=55&amp;show_children=false) y [solución de problemas de SAP HANA: disco relacionados causas y soluciones](http://help.sap.com/saphelp_hanaplatform/helpdata/en/47/4cb08a715c42fe9f7cc5efdc599959/content.htm?frameset=/en/44/3e1db4f73d42da859008df4f69e37a/frameset.htm&amp;current_toc=/en/85/d132c3f05e40a2b20c25aa5fd6331b/plain.htm&amp;node_id=53&amp;show_children=false) sitio pasos de solución de problemas detallada.

**Herramientas de diagnóstico**

Realice una comprobación del estado de SAP HANA mediante HANA\_Configuration\_Minichecks. Esta herramienta devuelve problemas técnicos potencialmente críticos que ya deberían haber aparecido como alertas en SAP HANA Studio.

Consulte demasiado[SAP nota #1969700: colección de instrucciones SQL para SAP HANA](https://launchpad.support.sap.com/#/notes/1969700) y descargar nota de hello SQL Statements.zip archivo toothat adjunto. Almacene este archivo .zip en la unidad de disco duro local Hola.

En SAP HANA Studio, en hello **información del sistema** pestaña, haga clic en hello **nombre** columna y seleccione **instrucciones de importación SQL**.

![En SAP HANA Studio, en la ficha de información del sistema de hello, haga clic en la columna de nombre de Hola y seleccione instrucciones SQL de importación](./media/troubleshooting-monitoring/image7-import-statements-a.png)

Seleccione Hola SQL Statements.zip archivo almacena localmente y se importará una carpeta con instrucciones SQL correspondientes de Hola. En este momento, hello que muchas comprobaciones de diagnóstico diferentes se pueden ejecutar con estas instrucciones SQL.

Por ejemplo, requisitos de ancho de banda de replicación del sistema de SAP HANA tootest, haga clic en hello **ancho de banda** instrucción en **replicación: ancho de banda** y seleccione **abiertos** en la consola de SQL.

instrucción SQL completa de Hello abre toobe de parámetros de entrada (sección de modificación) lo que permite cambiar y, a continuación, se ejecuta.

![instrucción SQL completa de Hello abre toobe de parámetros de entrada (sección de modificación) lo que permite cambiar y, a continuación, ejecutar](./media/troubleshooting-monitoring/image8-import-statements-b.png)

Otro ejemplo es clic en las instrucciones de hello en **replicación: información general sobre**. Seleccione **Execute** desde el menú contextual de hello:

![Otro ejemplo es clic en las instrucciones de hello en la replicación: información general. Seleccione Ejecutar desde el menú contextual de Hola](./media/troubleshooting-monitoring/image9-import-statements-c.png)

Esto genera información que ayuda a solucionar el problema:

![Esto generará información que ayudará a solucionar el problema](./media/troubleshooting-monitoring/image10-import-statements-d.png)

Hola igual de HANA\_configuración\_Minichecks y compruebe si hay alguna _X_ marcas en hello _C_ columna (crítico).

Ejemplo de salidas:

**HANA\_Configuration\_MiniChecks\_Rev102.01+1** para comprobaciones general de SAP HANA.

![HANA\_Configuration\_MiniChecks\_Rev102.01+1 para comprobaciones general de SAP HANA](./media/troubleshooting-monitoring/image11-configuration-minichecks.png)

**HANA\_Services\_Overview** para información general sobre los servicios de SAP HANA que se están ejecutando.

![HANA\_Services\_Overview para información general sobre los servicios de SAP HANA que se están ejecutando](./media/troubleshooting-monitoring/image12-services-overview.png)

**HANA\_Services\_Statistics**para información sobre los servicio de SAP HANA (CPU, memoria, etc.).

![HANA\_Services\_Statistics para información sobre los servicio de SAP HANA ](./media/troubleshooting-monitoring/image13-services-statistics.png)

**HANA\_configuración\_Introducción\_Rev110 +** para obtener información general sobre la instancia de SAP HANA Hola.

![HANA\_configuración\_Introducción\_Rev110 + para obtener información general sobre la instancia de SAP HANA Hola](./media/troubleshooting-monitoring/image14-configuration-overview.png)

**HANA\_configuración\_parámetros\_Rev70 +** toocheck parámetros de SAP HANA.

![HANA\_configuración\_parámetros\_parámetros de SAP HANA de toocheck Rev70 +](./media/troubleshooting-monitoring/image15-configuration-parameters.png)

