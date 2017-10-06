---
title: "solución de análisis de Azure Log Analytics aaaDNS | Documentos de Microsoft"
description: "Configurar y usar soluciones de análisis de DNS de hello en visión toogather de análisis de registros en la infraestructura DNS en operaciones, rendimiento y seguridad."
services: log-analytics
documentationcenter: 
author: bandersmsft
manager: carmonm
editor: 
ms.assetid: f44a40c4-820a-406e-8c40-70bd8dc67ae7
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/07/2017
ms.author: banders
ms.openlocfilehash: be7982c54b65ba0c4b1c15ae7516d02eced313f8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="gather-insights-about-your-dns-infrastructure-with-hello-dns-analytics-preview-solution"></a>Recopilar información detallada sobre la infraestructura DNS con hello solución de vista previa de análisis de DNS

![Símbolo de DNS Analytics](./media/log-analytics-dns/dns-analytics-symbol.png)

Este artículo describe cómo tooset seguridad y el uso Hola soluciones de análisis de DNS de Azure en visión toogather de análisis de registros de Azure en la infraestructura DNS en operaciones, rendimiento y seguridad.

DNS Analytics le ayuda a:

- Identificar a los clientes que intentan los nombres de dominio malintencionado tooresolve.
- Identificar los registros de recursos obsoletos.
- Identificar los nombres de dominio consultados con más frecuencia y los clientes DNS participativos.
- Ver la carga de solicitudes en los servidores DNS.
- Ver errores de registro DNS dinámicos.

solución de Hello recopila, analiza y correlaciona analíticos de DNS de Windows y otros datos relacionados de los servidores DNS y registros de auditoría.

## <a name="connected-sources"></a>Orígenes conectados

Hello en la tabla siguiente describe los orígenes de hello conectado que son compatibles con esta solución:

| **Origen conectado** | **Soporte técnico** | **Descripción** |
| --- | --- | --- |
| [Agentes de Windows](log-analytics-windows-agents.md) | Sí | solución de Hola recopila información de DNS de Windows para agentes. |
| [Agentes de Linux](log-analytics-linux-agents.md) | No | solución de Hola no recopila información de DNS de directa agentes de Linux. |
| [Grupo de administración de System Center Operations](log-analytics-om-agents.md) | Sí | solución de Hello recopila información de DNS de agentes en un grupo de administración de Operations Manager conectado. No se requiere una conexión directa de toohello de agente de Operations Manager de hello Operations Management Suite. Datos se reenvían desde el repositorio de Operations Management Suite de toohello del grupo de administración de Hola. |
| [Cuenta de Almacenamiento de Azure](log-analytics-azure-storage.md) | No | Hola solución no utiliza el almacenamiento de Azure. |

### <a name="data-collection-details"></a>Detalles de la recopilación de datos

solución de Hello recopila inventario DNS y datos relacionados con eventos DNS de los servidores DNS de Hola donde está instalado un agente de análisis de registros. Estos datos se, a continuación, cargan tooLog análisis y muestran en el panel de la solución de Hola. Datos relacionados con el inventario, como número de Hola de servidores DNS, zonas y registros de recursos, se recopilan mediante la ejecución de cmdlets de PowerShell de DNS de Hola. datos de Hola se actualizan una vez cada dos días. datos relacionados con eventos de saludo se recopilan prácticamente en tiempo real de hello [analítica y registros de auditoría](https://technet.microsoft.com/library/dn800669.aspx#enhanc) proporcionada por mejorar los diagnósticos en Windows Server 2012 R2 y el registro de DNS.

## <a name="configuration"></a>Configuración

Usar hello después de la solución de hello tooconfigure de información:

- Debe tener un [Windows](log-analytics-windows-agents.md) o [Operations Manager](log-analytics-om-agents.md) agente en cada servidor DNS que desea toomonitor.
- Puede agregar el área de trabajo de hello DNS análisis solución tooyour Operations Management Suite desde hello [Azure Marketplace](https://aka.ms/dnsanalyticsazuremarketplace). También puede utilizar el proceso de hello descrito en [soluciones de análisis de registro agregar desde la Galería de soluciones de hello](log-analytics-add-solutions.md).

solución de Hello empieza a recopilar datos sin necesidad de Hola de otra configuración. Sin embargo, puede usar Hola después de recopilación de datos de configuración toocustomize.

### <a name="configure-hello-solution"></a>Configurar la solución de Hola

En el panel de la solución de hello, haga clic en **configuración** página de configuración de DNS del análisis de tooopen Hola. Hay dos tipos de cambios de configuración que puede realizar:

- **Nombres de dominio de la lista de permitidos**. solución de Hello no procesa todas las consultas de búsqueda de Hola. Tiene una lista de los sufijos de nombres de dominio permitidos. solución de hello no procesa las consultas de búsqueda de Hola que resolver nombres de dominio de toohello que coinciden con los sufijos de nombre de dominio en la lista blanca. No procesa los nombres de dominio en la lista blanca, ayuda a datos de hello toooptimize enviados tooLog análisis. lista blanca de direcciones de Hello predeterminada incluye nombres de dominio público populares, como www.google.com y www.facebook.com. Puede ver Hola predeterminado completa lista mediante un desplazamiento.

 Puede modificar Hola lista tooadd ningún sufijo de nombre de dominio que desee tooview visión de búsqueda para. También puede quitar ningún sufijo de nombre de dominio que no desea tooview visión de búsqueda para.

- **Umbral de clientes participativos**. Los clientes DNS que sobrepasan el umbral de hello para el número de Hola de solicitudes de búsqueda se resalta en hello **los clientes DNS** hoja. umbral de Hello predeterminado es 1.000. Puede modificar el umbral de Hola.

    ![Nombre de dominio de la lista de permitidos](./media/log-analytics-dns/dns-config.png)

## <a name="management-packs"></a>Módulos de administración

Si usas el área de trabajo de hello Microsoft Monitoring Agent tooconnect tooyour Operations Management Suite, hello siguiente módulo de administración se instala:

- Microsoft DNS Data Collector Intelligence Pack (Microsft.IntelligencePacks.Dns)

Si el grupo de administración de Operations Manager es el área de trabajo de tooyour conectado Operations Management Suite, hello módulos de administración siguientes se instalan en Operations Manager cuando se agrega esta solución. No es necesario realizar tareas de configuración o mantenimiento de estos módulos de administración:

- Microsoft DNS Data Collector Intelligence Pack (Microsft.IntelligencePacks.Dns)
- Microsoft System Center Advisor DNS Analytics Configuration (Microsoft.IntelligencePack.Dns.Configuration)

Para obtener más información sobre cómo se actualizan los módulos de administración de soluciones, consulte [tooLog de conexión de Operations Manager análisis](log-analytics-om-agents.md).

## <a name="use-hello-dns-analytics-solution"></a>Usar la solución de análisis de DNS de Hola

Esta sección explican todas las funciones de panel de Hola y cómo toouse ellos.

Una vez agregado el área de trabajo de hello solución tooyour, icono de solución de hello en la página de introducción a Operations Management Suite Hola proporciona un resumen rápido de la infraestructura DNS. Incluye el número de Hola de servidores DNS donde se está recopilando datos de Hola. También incluye el número de Hola de las solicitudes realizadas por los clientes tooresolve malintencionado dominios hello las últimas 24 horas. Al hacer clic en el icono de hello, se abrirá el panel de la solución de Hola.

![Icono de DNS Analytics](./media/log-analytics-dns/dns-tile.png)

### <a name="solution-dashboard"></a>Panel de soluciones

panel de la solución de Hello muestra información resumida de Hola diversas características de solución de Hola. También incluye vínculos toohello vista para el análisis forense y el diagnóstico de detallada. De forma predeterminada, los datos de Hola se muestran para hello últimos siete días. Puede cambiar el intervalo de fecha y hora de hello mediante el uso de hello **control de selección de fecha y hora**, tal y como se muestra en hello después de imagen:

![Control de selección de hora](./media/log-analytics-dns/dns-time.png)

panel de la solución de Hola muestra Hola siguientes módulos:

**Seguridad de DNS**. Informes Hola a clientes DNS que están tratando de toocommunicate con dominios malintencionados. Mediante el uso de fuentes de distribución de Microsoft threat intelligence, análisis de DNS puede detectar a cliente direcciones IP que está tratando de dominios malintencionado tooaccess. En muchos casos, dispositivos infectados por malware "marcar" toohello "comando y control" Centro de dominio malintencionado de hello resolviendo Hola nombre de dominio de malware.

![Hoja Seguridad de DNS](./media/log-analytics-dns/dns-security-blade.png)

Al hacer clic en una dirección IP de cliente en la lista de hello, búsqueda de registros se abre y muestra los detalles de la búsqueda de Hola de consulta respectivos Hola. En el siguiente ejemplo de Hola, análisis de DNS ha detectado que la comunicación de Hola se realizaba con un [IRCbot](https://www.microsoft.com/security/portal/threat/encyclopedia/entry.aspx?Name=Win32/IRCbot):

![Resultados de Búsqueda de registros que muestran ircbot](./media/log-analytics-dns/ircbot.png)

Hola información le ayudará a tooidentify el:

- Cliente IP que inician la comunicación de Hola.
- Nombre de dominio que se resuelve la dirección IP malintencionada de toohello.
- Direcciones IP que Hola nombre de dominio se resuelve como.
- La dirección IP malintencionada.
- Gravedad del problema de Hola.
- Motivo para generar listas negras de IP malintencionadas Hola.
- La hora de detección.

**Dominios consultados**. Proporciona los nombres de dominio más frecuentes Hola que se está consultas los clientes DNS de hello en su entorno. Puede ver lista de Hola de todos los nombres de dominio de hello consultadas. También puede profundizar en los detalles de solicitud de búsqueda de Hola de un nombre de dominio específico en búsqueda de registros.

![Hoja Dominios consultados](./media/log-analytics-dns/domains-queried-blade.png)

**Clientes DNS**. Informes Hola clientes *violación umbral hello* para número de consultas en hello elegido el período de tiempo. Puede ver lista de Hola de todos los clientes DNS de Hola y detalles de Hola de consultas de hello realizadas por ellos en búsqueda de registros.

![Hoja Clientes DNS](./media/log-analytics-dns/dns-clients-blade.png)

**Registros de DNS dinámico**. Informa errores de registro del agente. Todos los errores de registro de dirección [registros de recursos](https://en.wikipedia.org/wiki/List_of_DNS_record_types) (tipo A y AAAA) se resaltan junto con el cliente de hello direcciones IP que realiza solicitudes de registro de hello. A continuación, puede usar esta causa de Hola de toofind de información de error de registro de hello siguiendo estos pasos:

1. Encontrar la zona de Hola que sea autoritativo para el nombre de Hola Hola cliente está tratando de tooupdate.

2. Usar información de inventario de hello solución toocheck Hola de esa zona.

3. Compruebe que actualización dinámica Hola de hello zona está habilitada.

4. Compruebe si la zona de hello está configurada para la actualización dinámica segura o no.

    ![Hoja Registros de DNS dinámico](./media/log-analytics-dns/dynamic-dns-reg-blade.png)

**Solicitudes de registro de nombres**. icono superior de Hello muestra una línea de tendencia de las solicitudes de actualización dinámica de DNS correctas e incorrectas. icono inferior Hola incluye a clientes de 10 principales de Hola que envían solicitudes de actualización DNS erróneas toohello los servidores DNS, ordenados por número de Hola de errores.

![Hoja Solicitudes de registro de nombres ](./media/log-analytics-dns/name-reg-req-blade.png)

**Consultas de DDI Analytics de ejemplo**. Contiene una lista hello más comunes de consultas de búsqueda que capturen los datos de análisis sin formato directamente.

[!include[log-analytics-log-search-nextgeneration](../../includes/log-analytics-log-search-nextgeneration.md)]

![Consultas de ejemplo](./media/log-analytics-dns/queries.png)

Puede usar estas consultas como punto de partida a fin de crear las suyas propias para generar informes personalizados. las consultas de Hello vinculan toohello página de búsqueda de registros de análisis de DNS donde se muestran los resultados:

- **Lista de servidores DNS**. Muestra una lista de todos los servidores DNS con el nombre de dominio público, el nombre de dominio, el nombre del bloque y las direcciones IP de servidor asociados.
- **Lista de zonas DNS**. Muestra una lista de todas las zonas DNS con el nombre de la zona asociada de hello, estado de actualización dinámica, servidores de nombres y estado de firma de DNSSEC.
- **Registros de recursos sin usar**. Muestra una lista de todos los registros de recursos sin usar/obsoletos Hola. Esta lista contiene el nombre de registro de recursos de hello, tipo de registro de recursos, Hola asociado servidor DNS, tiempo de generación de registros y nombre de la zona. Puede usar esta lista tooidentify Hola recursos DNS que ya no están en uso. Según esta información, puede quitar, a continuación, las entradas de los servidores DNS de Hola.
- **Carga de consultas de servidores DNS**. Muestra información para que pueda obtener una perspectiva de hello que DNS de carga en los servidores DNS. Esta información puede ayudarle a planear la capacidad de Hola para servidores de Hola. Puede ir toohello **métricas** pestaña visualización gráfica de toochange Hola vista tooa. Esta vista le ayudará a comprender cómo se distribuye Hola cargar DNS en todos los servidores DNS. Muestra las tendencias de velocidad de consultas de DNS de cada servidor.

    ![Resultados de Búsqueda de registros de consultas de servidores DNS](./media/log-analytics-dns/dns-servers-query-load.png)

- **Carga de consultas de zonas DNS**. Muestra hello las estadísticas de consulta de zona por segundo de DNS de todas las zonas de hello en los servidores DNS de hello administrados solución Hola. Haga clic en hello **métricas** ficha toochange Hola vista de visualización gráfica de tooa registros detallados de los resultados de Hola.
- **Eventos de configuración**. Muestra todos los eventos de cambio de configuración de DNS de Hola y mensajes asociados. A continuación, puede filtrar estos eventos basándose en la hora del servidor DNS de eventos, Id. de evento de hello, o categoría de tarea. datos de Hello pueden ayudar a los servidores DNS de los cambios realizados toospecific de auditoría a horas específicas.
- **Registro analítico de DNS**. Muestra todos los eventos analíticos de hello en todos los servidores DNS de hello administrados por solución Hola. A continuación, puede filtrar estos eventos basándose en la hora del servidor DNS de eventos, Id. de evento, hello, IP de cliente que realizó Hola consulta de búsqueda y categoría de tarea de tipo de consulta. Los eventos analíticos de DNS server habilitan la actividad de seguimiento en el servidor DNS de Hola. Un evento analítico se registra cada vez que servidor hello envía o recibe información de DNS.

### <a name="search-by-using-dns-analytics-log-search"></a>Búsqueda mediante Búsqueda de registros de DNS Analytics

En la página de búsqueda de registros de hello, puede crear una consulta. Puede filtrar los resultados de la búsqueda mediante controles de faceta. También puede crear consultas avanzadas tootransform, filtrar e informar sobre sus resultados. Iniciar con hello las siguientes consultas:

1. Hola **cuadro consulta de búsqueda**, tipo `Type=DnsEvents` tooview todos Hola eventos DNS generados por servidores DNS de hello administrados por solución Hola. los resultados de Hello muestran datos de registro de hello para todos los eventos relacionados toolookup consultas, registros dinámicos y cambios de configuración.

    ![Búsqueda de registros de Dnsevents](./media/log-analytics-dns/log-search-dnsevents.png)  

    a. datos de registro de hello tooview para las consultas de búsqueda, seleccione **LookUpQuery** como hello **subtipo** filtro desde el control de la faceta de Hola Hola izquierda. Se muestra una tabla que enumera todos los eventos de consulta de búsqueda de Hola para hello período de tiempo seleccionado.

    b. Seleccione los datos del registro de hello tooview para los registros dinámicos, **DynamicRegistration** como hello **subtipo** filtro desde el control de la faceta de Hola Hola izquierda. Se muestra una tabla que enumera todos los eventos de registro dinámico de Hola para hello período de tiempo seleccionado.

    c. datos de registro de hello tooview de cambios de configuración, seleccione **ConfigurationChange** como hello **subtipo** filtro desde el control de la faceta de Hola Hola izquierda. Se muestra una tabla que enumera todos los eventos de cambio de configuración de Hola para hello período de tiempo seleccionado.

2. Hola **cuadro consulta de búsqueda**, tipo `Type=DnsInventory` tooview todos Hola datos relacionadas con el inventario DNS para servidores DNS de hello administrados por solución Hola. los resultados de Hello muestran datos de registro de hello para registros de recursos, las zonas DNS y servidores DNS.

    ![Búsqueda de registros de DnsInventory](./media/log-analytics-dns/log-search-dnsinventory.png)

## <a name="feedback"></a>Comentarios

Hay dos maneras de proporcionar comentarios:

- **UserVoice**. Envíelas ideas para toowork de características de análisis de DNS. Visite hello [Operations Management Suite UserVoice página](https://aka.ms/dnsanalyticsuservoice).
- **Únase a nuestra cohorte**. Siempre nos interesa disponer de nuevos clientes unirse a nuestras características las cohortes tooget temprano acceso toonew y Ayúdenos a mejorar el análisis de DNS. Si está interesado en unirse, rellene esta [encuesta rápida](https://aka.ms/dnsanalyticssurvey).

## <a name="next-steps"></a>Pasos siguientes

[Buscar registros](log-analytics-log-searches.md) tooview detallada entradas del registro de DNS.
