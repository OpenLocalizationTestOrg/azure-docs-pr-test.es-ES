---
title: "aaaGetting a trabajar con Operations Management Suite solución de seguridad y auditoría | Documentos de Microsoft"
description: "Este documento le ayuda a tooget inició con Operations Management Suite seguridad y auditoría toomonitor de capacidades de solución la nube híbrida."
services: operations-management-suite
documentationcenter: na
author: YuriDio
manager: mbaldwin
editor: 
ms.assetid: 754796ef-a43e-468a-86c9-04a2eda55b5b
ms.service: operations-management-suite
ms.custom: oms-security
ms.topic: get-started-article
ms.devlang: na
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/18/2017
ms.author: yurid
ms.openlocfilehash: 5cb3e5dbb3e60f9702a34c9413ddc1bf2b14b411
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="getting-started-with-operations-management-suite-security-and-audit-solution"></a>Introducción a la solución Seguridad y auditoría de Operations Management Suite
Este documento le ayuda a empezar a trabajar rápidamente con las funcionalidades de la solución Seguridad y auditoría de Operations Management Suite (OMS) al guiarle a través de cada opción.

## <a name="what-is-oms"></a>¿Qué es OMS?
Microsoft Operations Management Suite (OMS) es la solución de administración de TI basada en la nube de Microsoft que le ayuda a administrar y proteger su infraestructura local y en la nube. Para obtener más información acerca de OMS, lea el artículo de hello [Operations Management Suite](https://technet.microsoft.com/library/mt484091.aspx).

## <a name="oms-security-and-audit-dashboard"></a>Panel de Seguridad y auditoría de OMS
Hola solución de auditoría y seguridad de OMS proporciona una vista completa de su organización postura de seguridad de TI con consultas de búsqueda integradas para problemas importantes que requieren su atención. Hola **seguridad y auditoría** panel es la pantalla principal de Hola para todo lo relacionado con toosecurity de OMS. Proporciona una visión de alto nivel sobre estado de seguridad de Hola de los equipos. Hola capacidad tooview también incluye todos los eventos de hello últimas 24 horas, 7 días, o cualquier otro período de tiempo personalizado. Hola tooaccess **seguridad y auditoría** panel, siga estos pasos:

1. Hola **Microsoft Operations Management Suite** panel principal haga clic en **configuración** mosaico en hello izquierda.
2. Hola **configuración** hoja, en **soluciones** haga clic en **seguridad y auditoría** opción.
3. Hola **seguridad y auditoría** se muestra el panel:
   
    ![Panel de Seguridad y auditoría de OMS](./media/oms-security-getting-started/oms-getting-started-fig1-ga.png)

Si tiene acceso a este panel de hello primera vez y no tiene dispositivos supervisados por OMS, Hola iconos no se rellenará con datos obtenidos de agente de Hola. Una vez que instale el agente de hello, puede tardar algún tiempo toopopulate, por lo tanto, lo que ve inicialmente puede que falten algunos datos que aún está cargando toohello en la nube.  En este caso, es normal toosee algunos iconos sin información tangible. Lectura [equipos Windows conectarse directamente tooOMS](https://technet.microsoft.com/library/mt484108.aspx) para obtener más información acerca de cómo tooinstall agente de OMS en un sistema de Windows y [Linux conectar equipos tooOMS](https://technet.microsoft.com/library/mt622052.aspx) para obtener más información acerca de cómo tooperform esta tarea en un sistema Linux.

> [!NOTE]
> agente de Hello recopila información de hello en función de hello eventos actuales que están habilitados, por ejemplo el nombre del equipo, el nombre de usuario y la dirección IP. Sin embargo, no se recopila ningún documento, archivo, nombre de la base de datos ni datos privados.   
> 
> 

Las soluciones son una colección de reglas de lógica, visualización y adquisición de datos que solucionan los desafíos clave a los que se enfrentan los clientes. Seguridad y auditoría es una solución, pueden agregarse otras por separado. Leer el artículo de hello [agregar soluciones](https://technet.microsoft.com/library/mt674635.aspx) para obtener más información acerca de cómo tooadd una nueva solución.

panel de OMS seguridad y auditoría de Hola se organiza en cuatro categorías principales:

* **Dominios de seguridad**: en esta área será toofurther puede explorar los registros de seguridad con el tiempo, tener acceso a la evaluación de malware, actualizar evaluación, seguridad de red, información de identidad y acceso, los equipos con los eventos de seguridad y tener rápidamente panel de centro de seguridad de acceso tooAzure.
* **Problemas importantes**: esta opción le permitirá tooquickly identificar el número de problemas activos Hola y Hola gravedad de estos problemas.
* **Detecciones (versión preliminar)**: le permite tooidentify patrones de ataque al visualizar alertas de seguridad que realicen en los recursos.
* **Inteligencia de amenazas**: le permite tooidentify patrones de ataque al visualizar el número total de Hola de servidores con tráfico malintencionado saliente de IP, tipo de amenaza malintencionados de Hola y un mapa que muestra dónde proceden estas direcciones IP. 
* **Consultas comunes de seguridad**: esta opción proporciona una lista de seguridad más comunes de hello las consultas puede utilizar toomonitor en su entorno. Al hacer clic en una de las consultas, abre hello **búsqueda** hoja con resultados de Hola para esa consulta.

> [!NOTE]
> Para obtener más información sobre cómo OMS mantiene la seguridad de los datos, lea Cómo OMS protege los datos.
> 
> 

## <a name="security-domains"></a>Dominios de seguridad
Al supervisar recursos, es importante toobe tooquickly capaz de acceso Hola estado actual de su entorno. Sin embargo también es importante toobe tootrack capaz de eventos atrás ocurridos en hello anterior que puede causar tooa una mejor comprensión de lo que sucede en su entorno en cierto punto en el tiempo. 

> [!NOTE]
> retención de datos se realiza de acuerdo toohello plan de precios de OMS. Para obtener más información, visite hello [Microsoft Operations Management Suite](https://www.microsoft.com/server-cloud/operations-management-suite/pricing.aspx) página de precios.
> 
> 

Escenarios de investigación forense y la respuesta incidentes directamente se beneficiarán de resultados de hello disponibles en hello **registros de seguridad con el tiempo** icono.

![Registros de seguridad con el paso del tiempo](./media/oms-security-getting-started/oms-getting-started-fig2.JPG)

Al hacer clic en este icono, Hola **búsqueda** se abrirá la hoja, que muestra el resultado de una consulta para **eventos de seguridad** (tipo = SecurityEvents) con datos basados en hello últimos siete días, tal y como se muestra a continuación:

[!include[log-analytics-log-search-nextgeneration](../../includes/log-analytics-log-search-nextgeneration.md)]

![Registros de seguridad con el paso del tiempo](./media/oms-security-getting-started/oms-getting-started-fig3.JPG)

resultado de la búsqueda de Hola se divide en dos paneles: panel izquierdo de hello proporciona un desglose del número de Hola de eventos de seguridad que se han encontrado equipos hello en el que se encontraron estos eventos, número de Hola de cuentas que se detectaron en estos equipos y los tipos de Hola de actividades. panel derecho de Hello proporciona resultados totales de hello y una vista cronológica Hola de eventos de seguridad con la actividad de nombre y eventos del equipo de Hola. También puede hacer clic en **mostrar más** tooview más detalles sobre este evento, como los datos de evento de hello, Id. de evento de Hola y origen del evento Hola.

> [!NOTE]
> Para obtener más información sobre la consulta de búsqueda de OMS, consulte [Referencia de búsqueda de OMS](https://technet.microsoft.com/library/mt450427.aspx).
> 
> 

### <a name="antimalware-assessment"></a>Evaluación de antimalware
Esto permite que opción tooquickly es identificar los equipos con protección insuficiente y los equipos que están expuestas a riesgos por un elemento de malware. Evaluación de malware, estado y las amenazas detectadas en los servidores de hello supervisado se leen y Hola, a continuación, los datos se envía toohello servicio OMS en la nube de Hola para su procesamiento. Servidores con amenazas detectadas y con protección insuficiente se muestran en el panel de evaluación de malware hello, que es accesible después de hacer clic en hello **evaluación Antimalware** icono. 

![evaluación de malware](./media/oms-security-getting-started/oms-getting-started-fig4-ga.png)

Al igual que cualquier otro icono dinámico disponibles en el panel de OMS, al hacer clic en él, Hola **búsqueda** hoja se abrirá con el resultado de la consulta de Hola. Para esta opción, si hace clic en hello **no proporcionan informes** opción **el estado de protección**, tendrá que el resultado de la consulta de Hola que esta entrada de único que contiene el nombre del equipo de Hola y el rango, como se muestra se muestra a continuación:

![resultado de la búsqueda](./media/oms-security-getting-started/oms-getting-started-fig5.png)

> [!NOTE]
> *rango* es una puntuación de estado de hello tooreflect de protección de hello (activado, desactivado, actualizar, etc.) y las amenazas que se encuentran. Al tener como un número agregaciones toomake de ayuda.
> 
> 

Si hace clic en el nombre del equipo de hello, tendrá la vista cronológico Hola Hola del estado de protección para este equipo. Esto es muy útil para escenarios en los que es necesario toounderstand si Hola antimalware estaba instalado y en algún momento se ha quitado.   

### <a name="update-assessment"></a>Evaluación de la actualización
Hola a este habilita la opción tooquickly es determinar los problemas de seguridad de toopotential exposición global y si o la gravedad de estas actualizaciones son para su entorno. Solución de auditoría y seguridad de OMS solo proporcionan visualización Hola de estas actualizaciones, proceden los datos reales de hello [soluciones de administración de actualizaciones](oms-solution-update-management.md), que es un módulo diferente de OMS. Aquí un ejemplo de Hola actualizaciones:

![actualizaciones del sistema](./media/oms-security-getting-started/oms-getting-started-fig6-new.png)

> [!NOTE]
> Para más información acerca de la solución de administración de actualizaciones, consulte [Solución de administración de actualizaciones de OMS](oms-solution-update-management.md).
> 
> 

### <a name="identity-and-access"></a>Identidad y acceso
La identidad debe ser control hello plano para la empresa, proteger la identidad debe ser la máxima prioridad. Aunque en hello anterior eran los perímetros alrededor de las organizaciones y los perímetros fueron uno de los límites de estable principal hello, hoy en día con más datos y aplicaciones más mover en la nube toohello identidad Hola deja de ser perimetral nueva Hola. 

> [!NOTE]
> actualmente datos Hola se basan solo en los datos de inicio de sesión de eventos de seguridad (4624 de Id. de evento) en inicios de sesión de Office 365 futuras hello y datos de Azure AD también se incluirán.
> 
> 

Al supervisar las actividades de identidad estará acciones proactivas tootake pueda antes un incidente tiene lugar o toostop acciones reactiva un intento de ataque. Hola **Identity and Access** panel proporciona información general sobre el estado de identidad, incluido el número de Hola de toolog de intentos fallidos de cuenta de usuario de Hola que se utilizaron durante el número de intentos, las cuentas que se han bloqueado, cuentas con cambiarán o restablecen la contraseña y número de cuentas que se registran en el que actualmente. 

Al hacer clic en hello **Identity and Access** icono verá Hola después de panel:

![identidad y acceso](./media/oms-security-getting-started/oms-getting-started-fig7-ga.png)

información de Hello disponible en este panel inmediatamente puede ayudarle a tooidentify una actividad sospechosa posible. Por ejemplo, hay 338 toolog intentos en como **administrador** y 100% de estos intentos por error. Esto puede deberse a un ataque de fuerza bruta contra esta cuenta. Si hace clic en esta cuenta obtendrá más información que le ayudarán a recurso de destino de hello toodetermine para este tipo de ataque potencial:

![search results](./media/oms-security-getting-started/oms-getting-started-fig8.JPG)

informe detallado Hello proporciona información importante acerca de este evento, incluidos: equipo de destino de hello, tipo de Hola de inicio de sesión (en este caso inicio de sesión de red), actividad de hello (en este caso mayúscula 4625) y una escala de tiempo completa de cada intento. 

### <a name="computers"></a>Equipos
Este icono puede ser usado tooaccess todos los equipos que tienen activamente los eventos de seguridad. Al hacer clic en este icono verá lista Hola de equipos con eventos de seguridad y un número de Hola de eventos en cada equipo:

![Equipos](./media/oms-security-getting-started/oms-getting-started-fig9.JPG)

Puede continuar la investigación, haga clic en cada equipo y revisar los eventos de seguridad de Hola que se marcaron.

### <a name="threat-intelligence"></a>Información sobre amenazas

Mediante la opción de inteligencia sobre amenazas de hello disponible en OMS seguridad y auditoría, los administradores de TI puede identificar las amenazas de seguridad en el entorno de hello, por ejemplo, identificar si un determinado equipo forma parte de una red de zombis. Los equipos pueden resultar nodos en una red de zombis cuando los atacantes instalación de forma ilegal malware que conecta secretamente este comando toohello el equipo y el control. También puede identificar posibles amenazas procedentes de canales de comunicación de tipo underground, como darknet. Obtener más información sobre inteligencia sobre amenazas leyendo [toosecurity de supervisión y de que responda las alertas en Operations Management Suite solución de seguridad y auditoría](oms-security-responding-alerts.md) artículo.

En algunos escenarios, puede que observe una posible dirección IP malintencionada a la que se accedió desde un equipo supervisado:

![mapa de información sobre amenazas](./media/oms-security-responding-alerts/oms-security-responding-alerts-fig6.png)

Esta alerta etc. en Hola misma categoría, se generan a través de la seguridad de OMS mediante el aprovechamiento de [Microsoft Threat Intelligence](https://youtu.be/O4WtxgUrDc8). Hola datos de inteligencia sobre amenazas es recopilada por Microsoft, así como adquiridas a través de los principales proveedores de inteligencia de amenazas. Estos datos se actualizan con frecuencia y adaptación mover toofast amenazas. Debido a la naturaleza tooits, debe combinarse con otras fuentes de información de seguridad al [investigando](https://blogs.technet.microsoft.com/msoms/2016/12/08/investigating-suspicious-activity-in-a-hybrid-cloud-with-oms-security/) una alerta de seguridad. 

### <a name="baseline-assessment"></a>Evaluación de línea base

Microsoft, junto con organizaciones gubernamentales y del sector de todo el mundo, define una configuración de Windows que representa implementaciones de servidor muy seguras. Esta configuración es un conjunto de claves del Registro, la configuración de la directiva de auditoría y la configuración de la directiva de seguridad, junto con los valores recomendados de Microsoft para esta configuración. Este conjunto de reglas se conoce como línea base de seguridad. Consulte [Evaluación de línea base en la solución Seguridad y auditoría de Operations Management Suite](oms-security-baseline.md) para más información sobre esta opción.

### <a name="azure-security-center"></a>Azure Security Center
Este icono es básicamente un panel de acceso directo tooaccess centro de seguridad de Azure. Lea [Introducción a Azure Security Center](../security-center/security-center-get-started.md) paramás información sobre esta solución.

## <a name="notable-issues"></a>Problemas importantes
propósito principal de Hola de este grupo de opciones es tooprovide una vista rápida de los problemas de Hola que tiene en su entorno, organizándolas en crítico, advertencia e informativo. Hola icono de tipo de problema activo es una visualización de estos problemas, pero no permite tooexplore más detalles acerca de ellos, para ello debe parte inferior de hello toouse de este icono que tiene nombre Hola de problema de hello (nombre), la cantidad de objetos tenía esto ocurra (recuento) y la importancia que tiene (gravedad).

![Problemas importantes](./media/oms-security-getting-started/oms-getting-started-fig10.JPG)

Puede ver que estos problemas se tratan ya en diferentes áreas de hello **dominios de seguridad** grupo, lo que refuerza la intención de Hola de esta vista: visualizar los problemas más importantes de hello en su entorno desde un único lugar.

## <a name="detections-preview"></a>Detecciones (vista previa)
Hello propósito principal de esta opción es tooallow TI tooquickly identificar entorno de tootheir de amenazas potenciales a través y la gravedad de Hola de esta amenaza.

![Información sobre amenazas](./media/oms-security-getting-started/oms-getting-started-fig12.png)

Esta opción también puede utilizarse durante un [investigación de respuesta a incidentes](https://blogs.msdn.microsoft.com/azuresecurity/2016/11/30/investigating-suspicious-activity-in-a-hybrid-cloud-with-oms-security/) tooperform Hola evaluación y obtener más información sobre los ataques de Hola.

> [!NOTE]
> Para obtener más información acerca de cómo toouse OMS para la respuesta a incidentes, vea este vídeo: [cómo tooLeverage hello Azure Security Center & Microsoft Operations Management Suite para una respuesta a incidentes](https://channel9.msdn.com/Blogs/Taste-of-Premier/ToP1703).
> 
> 

## <a name="threat-intelligence"></a>Información sobre amenazas
Hola nueva amenaza para la sección de inteligencia de solución de seguridad y auditoría de hello visualiza patrones de ataque posibles Hola de varias maneras: Hola número total de servidores con tráfico malintencionado saliente de IP, Hola tipo de amenaza malintencionados y un mapa que muestra dónde estas direcciones IP provienen de. Puede interactuar con el mapa de Hola y haga clic en hello direcciones IP para obtener más información.

Marcadores amarillos en el mapa de hello indican el tráfico entrante desde direcciones IP malintencionadas. No es raro que para los servidores que están expuestos toohello internet toosee malintencionado el tráfico entrante, pero se recomienda revisar estas toomake de intentos que ninguna de ellas fue correcta. Estos indicadores se basan en los registros del Firewall de Windows, WireData y registros de IIS.  

![Información sobre amenazas](./media/oms-security-getting-started/oms-getting-started-fig11-ga.png)

## <a name="common-security-queries"></a>Consultas comunes de seguridad
lista de Hola de consultas comunes de seguridad disponibles puede ser útil para obtener información toorapidly acceso del recurso y personalizarlo según las necesidades de su entorno. Estas consultas comunes son las siguientes:

* Todas las actividades de seguridad
* Actividades de seguridad en hello equipo "computer01.contoso.com" (reemplazar por su propio nombre de equipo)
* Actividades de seguridad en hello equipo "computer01.contoso.com" de la cuenta "Administrador" (reemplazar por sus propios nombres de equipo y cuenta)
* Actividad de inicio de sesión por equipo
* Cuentas que han acabado con el antimalware de Microsoft en cualquier equipo
* Equipos donde se finalizó Hola proceso antimalware de Microsoft
* Equipos en donde se ejecutó "hash.exe" ejecutan (sustituya por un nombre de proceso diferente)
* Todos los nombres de proceso que se han ejecutado
* Actividad de inicio de sesión por cuenta
* Cuentas que se registran de forma remota en hello equipo "computer01.contoso.com" (reemplazar por su propio nombre de equipo)

## <a name="see-also"></a>Otras referencias
En este documento, eran tooOMS se ha introducido solución seguridad y auditoría. toolearn más información acerca de la seguridad de OMS, consulte Hola siguientes artículos:

* [Información general de Operations Management Suite (OMS)](operations-management-suite-overview.md)
* [Supervisión y responde tooSecurity alertas en Operations Management Suite solución de seguridad y auditoría](oms-security-responding-alerts.md)
* [Supervisión de los recursos en la solución Seguridad y auditoría de Operations Management Suite](oms-security-monitoring-resources.md)

