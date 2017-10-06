---
title: "Hola aaaUse mapa de servicio de la solución en Operations Management Suite | Documentos de Microsoft"
description: "Mapa de servicio es una solución de Operations Management Suite que detecta automáticamente los componentes de la aplicación en Windows y mapas y sistemas Linux Hola comunicación entre los servicios. En este artículo se proporciona información para implementar la solución Mapa de servicio en su entorno y utilizarla en distintos escenarios."
services: operations-management-suite
documentationcenter: 
author: daveirwin1
manager: jwhit
editor: tysonn
ms.assetid: 3ceb84cc-32d7-4a7a-a916-8858ef70c0bd
ms.service: operations-management-suite
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 11/22/2016
ms.author: daseidma;bwren;dairwin
ms.openlocfilehash: f7c209182c9171cc520192ac13ca4d85174081b5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-service-map-solution-in-operations-management-suite"></a>Usar la solución de mapa de servicio de hello en Operations Management Suite
Mapa de servicio detecta automáticamente los componentes de la aplicación en los sistemas Windows y Linux y mapas Hola comunicación entre los servicios. Con el mapa de servicio, puede ver los servidores en forma de Hola que piensa de ellos: como sistemas interconectados que ofrecen servicios críticos. Mapa de servicio muestra las conexiones entre servidores, los procesos y los puertos a través de cualquier arquitectura conectado de TCP, sin ninguna configuración necesaria distinto de hello instalación de un agente.

En este artículo se describe los detalles de hello del uso de mapa de servicio. Para más información sobre cómo configurar Service Map y los agentes integrados, vea [Configuración de la solución Mapa de servicio de Operations Management Suite (OMS)](operations-management-suite-service-map-configure.md).


## <a name="use-cases-make-your-it-processes-dependency-aware"></a>Casos de uso: Haga que sus procesos de TI tengan en cuenta la dependencia

### <a name="discovery"></a>Detección
Mapa de servicio crea automáticamente una asignación de referencias comunes de dependencias entre servidores, procesos y servicios de terceros. Detecta y asigna todas las dependencias TCP, identificación de conexiones sorpresa, sistemas remotos de otros fabricantes que depende y tootraditional las áreas oscuras dependencias de la red, como Active Directory. Mapa de servicio detecta las conexiones de red que sus sistemas administrados están intentando toomake, que ayudan a identificar posibles errores de configuración de servidor, interrupción del servicio y problemas de red.

### <a name="incident-management"></a>Administración de incidentes
Mapa de servicio ayuda a eliminar las suposiciones de Hola de aislar los problemas que muestra cómo se conectan los sistemas y afectar al resto. Además de tooidentifying conexiones erróneas, ayuda a identificar los equilibradores de carga mal configurada, carga incoherentes o excesivo en los servicios críticos y no autorizados a los clientes, como equipos de desarrollador hablando tooproduction sistemas. Al usar flujos de trabajo integrados con Operations Management Suite Change Tracking, también puede ver si un evento de cambio en una máquina de back-end o un servicio explica la causa de Hola de un incidente.

### <a name="migration-assurance"></a>Garantía de migración
El empleo de Service Map permite planear, acelerar y validar de forma eficaz las migraciones de Azure, lo que ayuda a garantizar que nada se quede atrás y que no se produzcan interrupciones por sorpresa. Puede detectar interdependientes todos los sistemas que toomigrate necesidad juntos, evaluar la capacidad y la configuración del sistema e identificar si un sistema en ejecución aún sigue dando servicio a los usuarios o es un candidato para la retirada en lugar de la migración. Una vez completado el movimiento de hello, puede comprobar en tooverify de carga y la identidad de cliente que sistemas de prueba y se conectan los clientes. Si las definiciones de planeación y el firewall de subred tienen problemas, errores de conexión en las asignaciones de mapa de servicio punto toohello sistemas que necesitan conectividad.

### <a name="business-continuity"></a>Continuidad del negocio
Si utilizas Azure Site Recovery y debe definir la secuencia de recuperación de Hola para su entorno de aplicación, mapa de servicio de ayuda puede automáticamente mostrarle cómo sistemas dependen entre sí tooensure que el plan de recuperación es de confianza. Al elegir un servidor crítico o grupo y ver a sus clientes, puede identificar qué toorecover sistemas front-end después de hello servidor está restaurada y disponible. Por el contrario, examinando las dependencias de back-end de los servidores críticos, puede identificar qué toorecover sistemas antes de que se restauran los sistemas de foco.

### <a name="patch-management"></a>Administración de revisiones
Mapa de servicio se mejora el uso de hello evaluación de actualización de sistema de Operations Management Suite mostrando que dependen otros equipos y servidores de su servicio, por lo que puede notificarles con antelación antes de poner los sistemas para aplicar una revisión. Service Map también mejora la administración de revisiones en Operations Management Suite al mostrar si los servicios están disponibles y conectados correctamente después de haber sido revisados y reiniciados.


## <a name="mapping-overview"></a>Información general de asignación
Agentes de mapa de servicio recopilan información acerca de todos los procesos conectados TCP en servidor de Hola donde están instalados y los detalles acerca de Hola conexiones entrantes y salientes para cada proceso. En la lista de hello en el panel izquierdo de hello, puede seleccionar equipos o grupos que tienen Service Map agentes toovisualize sus dependencias en un intervalo de tiempo especificado. Dependencia de máquina asigna foco en un equipo concreto, y muestran todas las máquinas de Hola que son clientes directos de TCP o servidores de la máquina.  Las asignaciones de grupos de equipos muestran conjuntos de servidores y sus dependencias.

![Introducción a Mapa de servicio](media/oms-service-map/service-map-overview.png)

Las máquinas se pueden expandir en Hola Hola de tooshow mapa procesos en ejecución con conexiones de red activas durante un intervalo de tiempo Hola seleccionado. Cuando un equipo remoto con un agente de mapa de servicio está expandido tooshow detalles del proceso, se muestran solo los procesos que se comunican con el equipo de foco Hola. recuento de Hola de máquinas de front-end sin agente que se conectan en la máquina de foco de Hola se indica a la izquierda Hola de procesos de Hola a que se conectan. Si la máquina de foco Hola está realizando una máquina de back-end de tooa de conexión que no tiene ningún agente, servidor de back-end de Hola se incluye en un grupo de puertos de servidor, junto con otra conexiones toohello mismo número de puerto.

De forma predeterminada, mapa de servicio asigna mostrar hello últimos 30 minutos de la información de dependencia. Mediante el uso de controles en tiempo de hello en la parte superior izquierda de hello, puede consultar los mapas para intervalos de tiempo históricos de seguridad tooone hora tooshow cómo buscan las dependencias en hello pasado (por ejemplo, durante un incidente o antes de que se ha producido un cambio). Los datos de Mapa de servicio se almacenan durante 30 días en áreas de trabajo pagadas y durante 7 días en áreas de trabajo disponibles.

## <a name="status-badges-and-border-coloring"></a>Notificaciones de estado y colores en el borde
En hello parte inferior de cada servidor de asignación de hello puede ser una lista de notificaciones de estado ofrecer información de estado sobre el servidor de Hola. distintivos de Hello indican que hay cierta información relevante para servidor de hello uno de integraciones de solución de hello Operations Management Suite. Al hacer clic en un distintivo le lleva directamente toohello detalles del estado de hello en el panel derecho de Hola. Hello actualmente notificaciones de estado disponibles incluyen las alertas, los cambios, departamento de servicios, seguridad y actualizaciones.

Según la gravedad Hola de notificaciones de estado de hello, bordes de nodo de equipo pueden estar coloreada amarillo (crítico), rojo (advertencia) o azul (informativos). color de Hello representa el estado de más grave de Hola de cualquiera de las notificaciones de estado de Hola. Un borde gris indica que un nodo no tiene indicadores de estado.

![Notificaciones de estado](media/oms-service-map/status-badges.png)

## <a name="machine-groups"></a>Grupos de equipos
Los grupos de máquina permiten toosee mapas centrados en un conjunto de servidores, no solo uno para que pueda ver a todos los miembros de Hola de un clúster de servidor o la aplicación de varios nivel en una asignación.

Los usuarios seleccionar qué servidores forman un conjunto en un grupo y elija un nombre para el grupo de Hola.  Puede elegir tooview Hola grupo con todos sus procesos y las conexiones o verlo con solo los procesos de Hola y las conexiones que se relacionan directamente toohello otros miembros del grupo de Hola.

![Grupo de equipos](media/oms-service-map/machine-group.png)

### <a name="creating-a-machine-group"></a>Creación de un grupo de equipos
toocreate un grupo, equipo seleccione Hola o máquinas que desee en máquinas de hello lista y haga clic en **agregar toogroup**.

![Crear grupo](media/oms-service-map/machine-groups-create.png)

Allí, puede elegir **crear nuevo** y proporcione un nombre de grupo de Hola.

![Dar nombre al grupo](media/oms-service-map/machine-groups-name.png)

>[!NOTE]
>Grupos de máquinas están limitadas actualmente too10 servidores, pero tenemos previsto tooincrease este límite pronto.

### <a name="viewing-a-group"></a>Visualización de un grupo
Una vez que ha creado algunos grupos, puede verlos eligiendo la ficha grupos de Hola.

![Pestaña Grupos](media/oms-service-map/machine-groups-tab.png)

A continuación, seleccione asignación de Hola de tooview de nombre de grupo de Hola para ese grupo de máquinas.
![Grupo de equipos](media/oms-service-map/machine-group.png) máquinas de Hola que pertenecen toohello grupo se describen en blanco en el mapa de Hola.

Hola expansión de grupo mostrará una lista de máquinas de Hola que componen Hola grupo de equipos.

![Equipos del grupo de equipos](media/oms-service-map/machine-groups-machines.png)

### <a name="filter-by-processes"></a>Filtrar por procesos
Puede alternar vista de mapa de hello entre que muestra todos los procesos y las conexiones de grupo Hola y Hola solo aquellos que se relacionan directamente toohello grupo de equipos.  Hola vista predeterminada es tooshow todos los procesos.  Puede cambiar la vista Hola haciendo clic en el icono de filtro de Hola por encima del mapa de Hola.

![Filtrar grupo](media/oms-service-map/machine-groups-filter.png)

Cuando **todos los procesos** está seleccionado, mapa de hello incluirá todos los procesos y las conexiones en cada uno de los equipos de Hola Hola grupo.

![Todos los procesos del grupo de equipos](media/oms-service-map/machine-groups-all.png)

Si cambia Hola vista solo tooshow **conectado por el grupo de procesos**, mapa de Hola que se va a restringir hacia abajo tooonly esos procesos y las conexiones que están directamente conectan tooother máquinas en el grupo de hello, crear una vista simplificada.

![Procesos filtrados del grupo de equipos](media/oms-service-map/machine-groups-filtered.png)
 
### <a name="adding-machines-tooa-group"></a>Agregar grupo de tooa de máquinas
tooadd máquinas tooan de grupo existente, compruebe máquinas de toohello siguientes que desee y, a continuación, haga clic en los cuadros hello **agregar toogroup**.  A continuación, elija el grupo de hello que desea tooadd Hola equipos.
 
### <a name="removing-machines-from-a-group"></a>Eliminación de equipos de un grupo
En la lista de grupos de hello, expanda máquinas Hola grupo nombre toolist Hola Hola grupo de máquinas.  A continuación, haga clic en hello puntos suspensivos menú siguiente toohello máquina desee tooremove y elija **quitar**.

![Quitar equipo del grupo](media/oms-service-map/machine-groups-remove.png)

### <a name="removing-or-renaming-a-group"></a>Eliminación o cambio del nombre de un grupo
Haga clic en hello puntos suspensivos menú siguiente toohello nombre de grupo en la lista de grupos de Hola.

![Menú Grupo de equipos](media/oms-service-map/machine-groups-menu.png)


## <a name="role-icons"></a>Iconos de rol
Ciertos procesos cumplen roles determinados en los equipos: servidores web, servidores de aplicaciones, base de datos, etc. Mapa de servicio anota el proceso y cuadros de máquina con rol iconos toohelp identifican en un rol de la vista Hola un proceso o un servidor desempeña.

| Icono de rol | Descripción |
|:--|:--|
| ![Servidor Web](media/oms-service-map/role-web-server.png) | Servidor Web |
| ![Servidor de aplicaciones](media/oms-service-map/role-application-server.png) | Servidor de aplicaciones |
| ![Servidor de bases de datos](media/oms-service-map/role-database.png) | Servidor de bases de datos |
| ![Servidor LDAP](media/oms-service-map/role-ldap.png) | Servidor LDAP |
| ![Servidor SMB](media/oms-service-map/role-smb.png) | Servidor SMB |

![Iconos de rol](media/oms-service-map/role-icons.png)


## <a name="failed-connections"></a>Conexiones con errores
Conexiones erróneas se muestran en el mapa de servicio se asigna para los procesos y equipos, con una línea roja discontinua que indica que un sistema cliente haya errores tooreach un proceso o un puerto. Conexiones erróneas se informan de cualquier sistema con un agente de mapa de servicio implementado si ese sistema es una conexión de hello no se pudo intentar Hola. Mapa de servicio mide este proceso mediante la observación de sockets TCP que no cumplan tooestablish una conexión. Este error podría deberse a un firewall, un error de configuración de cliente de Hola o servidor, o un servicio remoto no esté disponible.

![Conexiones con errores](media/oms-service-map/failed-connections.png)

La comprensión de las conexiones con errores pueden ayudar a solucionar problemas, a la validación de la migración, el análisis de seguridad y al entendimiento general de la arquitectura. Errores de conexión a veces son inofensivos, pero a menudo señalan directamente problema tooa, por ejemplo, un entorno de conmutación por error de repente pase a ser inaccesible o de dos niveles de aplicación que se va a tootalk no se puede después de una migración a la nube.

## <a name="client-groups"></a>Grupos de clientes
Grupos de clientes son cuadros en el mapa de Hola que representan los equipos cliente que no tienen agentes de dependencia. Un único grupo de cliente representa a los clientes de Hola para un proceso individual o una máquina.

![Grupos de clientes](media/oms-service-map/client-groups.png)

direcciones IP de hello toosee de servidores de hello en un grupo de cliente, el grupo de hello select. contenido de Hello del grupo de Hola se enumeran en hello **propiedades de grupo de cliente** panel.

![Propiedades del grupo de clientes](media/oms-service-map/client-group-properties.png)

## <a name="server-port-groups"></a>Grupos de puertos de servidor
Los grupos de puertos de servidor son cuadros que representan los puertos del servidor en servidores que no tienen agentes de dependencia. cuadro de Hello contiene el puerto del servidor de Hola y un recuento del número de Hola de servidores con el puerto de toothat de conexiones. Expanda las conexiones y servidores individuales de hello cuadro toosee Hola. Si hay un solo servidor en el cuadro de hello, aparece hello nombre o dirección IP.

![Grupos de puertos de servidor](media/oms-service-map/server-port-groups.png)

## <a name="context-menu"></a>Menú contextual
Clic en Hola de puntos suspensivos (...) en la parte superior de hello derecha de cualquier servidor que muestra el menú contextual de Hola para ese servidor.

![Conexiones con errores](media/oms-service-map/context-menu.png)

### <a name="load-server-map"></a>Cargar mapa del servidor
Haga clic en **carga servidor mapa** toma tooa nueva asignación con el servidor seleccionado de hello como nueva máquina de foco Hola.

### <a name="show-self-links"></a>Mostrar autovínculos
Haga clic en **Self-Links mostrar** actualiza Hola nodo del servidor, los incluidos Self-Link, ¿cuáles son las conexiones de TCP que empiezan y terminan en procesos de servidor hello. Si Self-Link están se muestra, Hola cambios de comando de menú demasiado**Self-Links ocultar**, de modo que puede desactivarlos.

## <a name="computer-summary"></a>Resumen del equipo
Hola **máquina resumen** panel incluye una visión general del sistema operativo del servidor, recuentos de dependencia y datos desde otras soluciones de Operations Management Suite. Estos datos incluyen métricas de rendimiento, incidencias del departamento de servicios, seguimiento de cambios, seguridad y actualizaciones.

![Panel de resumen del equipo](media/oms-service-map/machine-summary.png)

## <a name="computer-and-process-properties"></a>Propiedades de proceso y de equipo
Cuando se desplaza de un mapa de asignación de servicio, puede seleccionar máquinas y procesos contexto adicional toogain sobre sus propiedades. Equipos proporcionan información sobre el nombre DNS, las direcciones IPv4, CPU y memoria capacidad, tipo de máquina virtual, sistema operativo y versión, reinicie última hora e identificadores de Hola de sus agentes de Operations Management Suite y mapa de servicio.

![Panel Propiedades de la máquina](media/oms-service-map/machine-properties.png)

Puede recopilar detalles del proceso de los metadatos del sistema operativo sobre procesos en ejecución, como el nombre del proceso, la descripción del proceso, el nombre de usuario y el dominio (en Windows), el nombre de la compañía, el nombre del producto, la versión del producto, el directorio de trabajo, la línea de comandos y la hora de inicio del proceso.

![Panel Propiedades del proceso](media/oms-service-map/process-properties.png)

Hola **resumen del proceso de** panel proporciona información adicional acerca de la conectividad del proceso de hello, incluidos sus puertos de enlace, las conexiones entrantes y salientes y no se pudo conexiones.

![Panel Resumen de proceso](media/oms-service-map/process-summary.png)

## <a name="operations-management-suite-alerts-integration"></a>Integración de Operations Management Suite Alerts
Mapa de servicio se integra con alertas de Operations Management Suite tooshow activada las alertas del servidor seleccionado de hello en intervalo de tiempo de hello seleccionado. servidor Hello muestra un icono si hay alertas actuales, hello y **máquina alertas** panel muestra las alertas de Hola.

![Panel de alertas del equipo](media/oms-service-map/machine-alerts.png)

tooenable las alertas pertinentes toodisplay mapa de servicio, cree una regla de alerta que se activa para un equipo específico. toocreate alertas apropiado:
- Incluir una cláusula toogroup por equipo (por ejemplo, **por intervalo de equipo 1 minuto**).
- Elija tooalert en función de medida de métrica.

![Configuración de alertas](media/oms-service-map/alert-configuration.png)


## <a name="operations-management-suite-log-events-integration"></a>Integración de eventos de registro de Operations Management Suite
Mapa de servicio se integra con tooshow de búsqueda de registros un recuento de todos los eventos de registro disponibles para el servidor seleccionado de Hola durante el intervalo de tiempo de hello seleccionado. Puede haga clic en cualquier fila de la lista de Hola de evento recuentos toojump tooLog búsqueda y ver los eventos de registro individuales de Hola.

![Panel de eventos de registro del equipo](media/oms-service-map/log-events.png)

## <a name="operations-management-suite-service-desk-integration"></a>Integración de Operations Management Suite Service Desk
Integración con el mapa de servicio con hello conector de administración de servicios de TI es automática cuando ambas soluciones están habilitados y configurados en el área de trabajo de Operations Management Suite. integración de Hello en mapa de servicio tiene la etiqueta "Departamento de servicios". Para más información, vea [Administración centralizada de los elementos de trabajo ITSM con IT Service Management Connector (versión preliminar)](https://docs.microsoft.com/azure/log-analytics/log-analytics-itsmc-overview).

Hola **departamento de servicios de máquina** panel muestran todos los eventos de administración de servicios de TI de servidor seleccionado, hello en el intervalo de tiempo de hello seleccionado. servidor de Hello muestra un icono si hay elementos actuales y panel de departamento de servicios de máquina de hello mostrarlos.

![Panel de departamento de servicios del equipo](media/oms-service-map/service-desk.png)

elemento de hello tooopen en la solución ITSM conectada, haga clic en **elemento de trabajo de vista**.

tooview Hola detalles del elemento de hello en búsqueda de registros, haga clic en **muestran en Log Search**.


## <a name="operations-management-suite-change-tracking-integration"></a>Integración de Operations Management Suite Change Tracking
La integración de Service Map con Change Tracking es automática si ambas soluciones están habilitadas y configuradas en el área de trabajo de Operations Management Suite.

Hola **el seguimiento de cambios en la máquina** panel enumera todos los cambios, con hello más reciente en primer lugar, junto con un toodrill de vínculo hacia abajo tooLog búsqueda para obtener más detalles.

![Panel de seguimiento de cambios del equipo](media/oms-service-map/change-tracking.png)

Hello imagen siguiente es una vista detallada de un evento ConfigurationChange que es posible que vea después de seleccionar **mostrar en análisis de registros**.

![Evento ConfigurationChange](media/oms-service-map/configuration-change-event.png)


## <a name="operations-management-suite-performance-integration"></a>Integración de rendimiento de Operations Management Suite
Hola **rendimiento de las máquinas** panel muestra las métricas de rendimiento estándar para el servidor seleccionado Hola. métricas de Hello incluyen la utilización de CPU, uso de memoria, bytes de red enviados y recibidos y una lista de los procesos principales de hello en bytes de red enviados y recibidos. datos de rendimiento de red de hello tooget, debe también ha habilitado Hola solución 2.0 de datos de conexión de Operations Management Suite.

![Panel Rendimiento de la máquina](media/oms-service-map/machine-performance.png)


## <a name="operations-management-suite-security-integration"></a>Integración de Operations Management Suite Security
La integración de Service Map con Security and Audit es automática si ambas soluciones están habilitadas y configuradas en el área de trabajo de Operations Management Suite.

Hola **máquina seguridad** panel muestra datos de solución Operations Management Suite seguridad y auditoría para el servidor seleccionado Hola Hola. panel Hola presenta un resumen de los problemas de seguridad pendientes para servidor de Hola durante el intervalo de tiempo de hello seleccionado. Al hacer clic en cualquiera de los ejercicios de problemas de seguridad de hello hacia abajo en una búsqueda de registros para obtener más información acerca de ellos.

![Panel de seguridad del equipo](media/oms-service-map/machine-security.png)


## <a name="operations-management-suite-updates-integration"></a>Integración de Operations Management Suite Updates
La integración de Service Map con Update Management es automática si ambas soluciones están habilitadas y configuradas en el área de trabajo de Operations Management Suite.

Hola **máquina actualizaciones** panel muestra los datos de la solución de administración de actualizaciones de Operations Management Suite para el servidor seleccionado Hola Hola. panel de Hello presenta un resumen de las actualizaciones que faltan para servidor de Hola durante el intervalo de tiempo de hello seleccionado.

![Panel de seguimiento de cambios del equipo](media/oms-service-map/machine-updates.png)

## <a name="log-analytics-records"></a>Registros de Log Analytics
Los datos de inventario de equipos y procesos de Service Map están disponibles para [buscar](../log-analytics/log-analytics-log-searches.md) en Log Analytics. Puede aplicar este tooscenarios de datos que incluyen la planeación de la migración, análisis de capacidad, detección y solución de problemas de rendimiento a petición.

Se genera un registro por hora para cada equipo único y el proceso, además los registros de toohello que se generan cuando un proceso o un equipo se inicia o está integrada tooService están asignados. Estos registros tienen propiedades de hello en hello las tablas siguientes. Hola campos y valores en los eventos de hello ServiceMapComputer_CL asignan toofields de recurso de la máquina en la API del Administrador de recursos de Azure ServiceMap Hola Hola. Hello campos y valores en los eventos de hello ServiceMapProcess_CL campos se asignan toohello de recurso de proceso en la API del Administrador de recursos de Azure ServiceMap Hola Hola. campo de Hello ResourceName_s coincide con campo de nombre de hello en el recurso de administrador de recursos correspondiente de Hola. 

>[!NOTE]
>A medida que aumentan los elementos del mapa de servicio, estos campos son toochange de asunto.

Hay propiedades generados internamente que puede utilizar equipos y procesos de tooidentify único:

- Equipo: Utilice ResourceId o ResourceName_s toouniquely identificar un equipo dentro de un área de trabajo de Operations Management Suite.
- Proceso: Use ResourceId toouniquely identificar un proceso dentro de un área de trabajo de Operations Management Suite. ResourceName_s es único en el contexto de hello del equipo de hello en qué Hola proceso está ejecutando (MachineResourceName_s) 

Dado que pueden existir varios registros para un proceso especificado y un equipo de un intervalo de tiempo especificado, las consultas pueden devolver más de un registro de hello mismo proceso o equipo. tooinclude Hola solo registro más reciente, agregue "| consulta de toohello de desduplicación ResourceId".

### <a name="servicemapcomputercl-records"></a>Registros de ServiceMapComputer_CL
Los registros con un tipo de *ServiceMapComputer_CL* tienen datos de inventario de servidores con agentes de Mapa de servicio. Estos registros tienen propiedades de hello en hello en la tabla siguiente:

| Propiedad | Descripción |
|:--|:--|
| Tipo | *ServiceMapComputer_CL* |
| SourceSystem | *OpsManager* |
| ResourceId | Identificador único para una máquina en el área de trabajo de Hola de Hola |
| ResourceName_s | Identificador único para una máquina en el área de trabajo de Hola de Hola |
| ComputerName_s | FQDN del equipo Hola |
| Ipv4Addresses_s | Una lista de las direcciones IPv4 del servidor de Hola |
| Ipv6Addresses_s | Una lista de las direcciones IPv6 del servidor de Hola |
| DnsNames_s | Matriz de nombres DNS |
| OperatingSystemFamily_s | Windows o Linux |
| OperatingSystemFullName_s | nombre completo del sistema operativo de Hola Hola  |
| Bitness_s | valor de bits de Hola de máquina de hello (32 bits o 64 bits)  |
| PhysicalMemory_d | memoria física de Hello en MB |
| Cpus_d | número de Hola de CPU |
| CpuSpeed_d | Hola velocidad de CPU en MHz|
| VirtualizationState_s | *unknown*, *physical*, *virtual*, *hypervisor* |
| VirtualMachineType_s | *hyperv*, *vmware*, etc. |
| VirtualMachineNativeMachineId_g | Hola Id. de máquina virtual tal como lo asignó el hipervisor |
| VirtualMachineName_s | nombre de Hola de hello VM |
| BootTime_t | tiempo de arranque de Hola |



### <a name="servicemapprocesscl-type-records"></a>Registros con un tipo ServiceMapProcess_CL
Los registros con un tipo de *ServiceMapProcess_CL* tienen datos de inventario para procesos con conexión TCP en servidores con agentes de Mapa de servicio. Estos registros tienen propiedades de hello en hello en la tabla siguiente:

| Propiedad | Descripción |
|:--|:--|
| Tipo | *ServiceMapProcess_CL* |
| SourceSystem | *OpsManager* |
| ResourceId | Identificador único para un proceso en el área de trabajo de Hola de Hola |
| ResourceName_s | Identificador único de Hola para un proceso de máquina de hello en el que se está ejecutando|
| MachineResourceName_s | nombre de recurso de Hola de máquina de Hola |
| ExecutableName_s | nombre de Hello del ejecutable del proceso Hola |
| StartTime_t | hora de inicio de grupo de proceso de Hola |
| FirstPid_d | Hola primera PID en el grupo de procesos de Hola |
| Description_s | Descripción del proceso de Hola |
| CompanyName_s | nombre de Hola de empresa de Hola |
| InternalName_s | nombre interno de Hola |
| ProductName_s | nombre de Hello del producto de Hola |
| ProductVersion_s | versión del producto Hola |
| FileVersion_s | versión del archivo Hola |
| CommandLine_s | línea de comandos de Hola |
| ExecutablePath _s | archivo ejecutable de Hello ruta de acceso toohello |
| WorkingDirectory_s | directorio de trabajo de Hola |
| UserName | cuenta de Hello bajo qué Hola proceso se está ejecutando |
| UserDomain | dominio de Hello bajo qué Hola proceso se está ejecutando |


## <a name="sample-log-searches"></a>Búsquedas de registros de ejemplo

### <a name="list-all-known-machines"></a>Enumerar todas las máquinas conocidas
Type=ServiceMapComputer_CL | dedup ResourceId

### <a name="list-hello-physical-memory-capacity-of-all-managed-computers"></a>Capacidad de memoria física de Hola de lista de todos los equipos administrados.
Type=ServiceMapComputer_CL | select PhysicalMemory_d, ComputerName_s | Dedup ResourceId

### <a name="list-computer-name-dns-ip-and-os"></a>Enumerar el nombre de equipo, DNS, IP y SO.
Type=ServiceMapComputer_CL | select ComputerName_s, OperatingSystemFullName_s, DnsNames_s, IPv4Addresses_s  | dedup ResourceId

### <a name="find-all-processes-with-sql-in-hello-command-line"></a>Buscar todos los procesos con "sql" en la línea de comandos de Hola
Type=ServiceMapProcess_CL CommandLine_s = \*sql\* | dedup ResourceId

### <a name="find-a-machine-most-recent-record-by-resource-name"></a>Buscar una máquina (registro más reciente) por el nombre de recurso
Type=ServiceMapComputer_CL "m-4b9c93f9-bc37-46df-b43c-899ba829e07b" | dedup ResourceId

### <a name="find-a-machine-most-recent-record-by-ip-address"></a>Buscar un equipo (registro más reciente) por dirección IP
Type=ServiceMapComputer_CL "10.229.243.232" | dedup ResourceId

### <a name="list-all-known-processes-on-a-specified-machine"></a>Enumerar todos los procesos conocidos en un equipo determinado
Type=ServiceMapProcess_CL MachineResourceName_s="m-4b9c93f9-bc37-46df-b43c-899ba829e07b" | dedup ResourceId

### <a name="list-all-computers-running-sql"></a>Enumerar todos los equipos que ejecutan SQL
Type=ServiceMapComputer_CL ResourceName_s IN {Type=ServiceMapProcess_CL \*sql\* | Distinct MachineResourceName_s} | dedup ResourceId | Distinct ComputerName_s

### <a name="list-all-unique-product-versions-of-curl-in-my-datacenter"></a>Enumerar todas las versiones de producto únicas de curl en mi centro de datos
Type=ServiceMapProcess_CL ExecutableName_s=curl | Distinct ProductVersion_s

### <a name="create-a-computer-group-of-all-computers-running-centos"></a>Crear un grupo de equipos de todos los equipos con CentOS
Type=ServiceMapComputer_CL OperatingSystemFullName_s = \*CentOS\* | Distinct ComputerName_s


## <a name="rest-api"></a>API de REST
Todos los datos de servidor, el proceso y la dependencia de hello en mapa de servicio está disponible a través de hello [API de REST de servicios mapa](https://docs.microsoft.com/rest/api/servicemap/).


## <a name="diagnostic-and-usage-data"></a>Datos de diagnóstico y uso
Microsoft recopila automáticamente datos de uso y rendimiento mediante el uso del programa Hola a servicio de mapas de servicio. Microsoft usa esta tooprovide de datos y mejorar la calidad de hello, seguridad e integridad de hello servicio de mapas de servicio. tooprovide precisas y eficaces capacidades de resolución, datos de hello incluyen información sobre la configuración de hello del software, como sistema operativo y versión, dirección IP, nombre DNS y el nombre de estación de trabajo. Microsoft no recopila nombres, direcciones ni otra información de contacto.

Para obtener más información acerca del uso y recopilación de datos, vea hello [declaración de privacidad de Microsoft Online Services](https://go.microsoft.com/fwlink/?LinkId=512132).


## <a name="next-steps"></a>Pasos siguientes
Obtenga más información sobre [búsquedas de registro](../log-analytics/log-analytics-log-searches.md) en los datos de tooretrieve de análisis de registros recopilados por el mapa de servicio.


## <a name="troubleshooting"></a>Solución de problemas
Vea hello [solución de problemas de sección del documento de configuración de mapa de servicio de hello](operations-management-suite-service-map-configure.md#troubleshooting).


## <a name="feedback"></a>Comentarios
¿Quiere hacernos llegar algún comentario acerca de Mapa de servicio o esta documentación?  Visite la [página UserVoice](https://feedback.azure.com/forums/267889-log-analytics/category/184492-service-map) para sugerir características o votar sugerencias existentes.
