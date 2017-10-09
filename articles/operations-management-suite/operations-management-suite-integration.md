---
title: aaaIntegrating con Operations Management Suite (OMS) | Documentos de Microsoft
description: "Además toousing Hola características estándares de OMS, puede integrar con otro tooprovide de aplicaciones y servicios de administración en un entorno de administración híbrida, entorno de tooyour único de escenarios de administración personalizado tooprovide o tooprovide personalizado experiencia de administración para sus clientes.  En este artículo se proporciona información general de las diferentes opciones para la integración con OMS y vincula tooarticles proporciona información técnica detallada."
services: operations-management-suite
documentationcenter: 
author: bwren
manager: jwhit
editor: tysonn
ms.assetid: fc5f3a8a-77f7-4103-bd7e-744c15ffcca7
ms.service: operations-management-suite
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 04/11/2017
ms.author: bwren
ms.openlocfilehash: dce752dcdc6c725bbafd49db4a5055750487ecf9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="integrating-with-operations-management-suite-oms"></a>Integración con Operations Management Suite (OMS)
Operations Management Suite es la solución de administración de TI basada en la nube de Microsoft que le ayuda a administrar y proteger su infraestructura local y en la nube.  Además toousing Hola características estándares de OMS, puede integrar con otro tooprovide de aplicaciones y servicios de administración en un entorno de administración híbrida, entorno de tooyour único de escenarios de administración personalizado tooprovide o tooprovide personalizado experiencia de administración para sus clientes.  Este artículo proporciona información general sobre las diferentes opciones para integrar con OMS servicios y vincula tooarticles proporciona información técnica detallada. 

## <a name="log-analytics"></a>Log Analytics
Todos los datos de administración que recopila Log Analytics se almacenan en un repositorio que se hospeda en Azure.  Todos los datos almacenados en el repositorio de hello está disponible en las búsquedas de registro que proporcionan análisis rápido en extremadamente grandes cantidades de datos.  Los requisitos de integración pueden ser repositorio de hello toopopulate con nuevos datos, haciendo que esté disponible para el análisis, o los datos de tooextract de hello repositorio tooprovide una visualización nueva o toointegrate con otra herramienta de administración.

Cada parte de los datos en el repositorio de Hola se almacena como un registro.  Al rellenar el repositorio de hello, debe proporcionar a los usuarios con el tipo de registro de hello que utiliza la solución y una descripción de sus propiedades.  Cuando se recuperan datos, necesitará esta información acerca de los datos de Hola que está trabajando.

![Rellenar el repositorio de OMS Hola](media/operations-management-suite-integration/repository.png)

### <a name="populate-hello-log-analytics-repository"></a>Rellenar el repositorio de análisis de registros de Hola
Existen varios métodos para rellenar el repositorio de OMS Hola.  Hello método que use dependerá de factores como donde se encuentran datos de origen de hello, formato de Hola de datos de Hola y que los clientes necesitan toosupport.  Una vez que los datos se almacenan en el repositorio de hello, no produce ninguna diferencia cómo se recopiló el inventario.

Hello las secciones siguientes describen las distintas opciones de Hola para rellenar el repositorio de OMS Hola.

#### <a name="connected-sources-and-data-sources"></a>Orígenes de datos y orígenes conectados
Orígenes conectados son las ubicaciones de Hola donde se pueden recuperar los datos para el repositorio OMS Hola.  Orígenes de datos y soluciones de ejecutan en orígenes conectados y definen los datos específicos de Hola que se recopilan.  Si su aplicación escribe tooone de datos de estos orígenes de datos, puede recopilar mediante la configuración de origen de datos de Hola.  Por ejemplo, si la aplicación crea eventos Syslog, a continuación, se pueden recopilar por origen de datos de Syslog de hello en un agente de Linux.

* [Orígenes de datos en Log Analytics](../log-analytics/log-analytics-data-sources.md)

#### <a name="solutions"></a>Soluciones
Soluciones de amplían las capacidades de Hola de OMS.  Una solución puede recopilar datos de origen conectado Hola o pueden realizar análisis en los registros que ya se han recopilado en el repositorio de Hola.  Cada solución proporcionada por Microsoft tiene un artículo individual que proporciona los detalles de hello en los datos de Hola que recopila.

* [Soluciones en Log Analytics](../log-analytics/log-analytics-add-solutions.md)

#### <a name="http-data-collector-api"></a>API del recopilador de datos HTTP
Hola API de recopilador de datos de análisis de registros HTTP es una API de REST que permite repositorio de análisis de registros de tooadd JSON datos toohello.  Puede aprovechar esta API cuando tiene una aplicación que no proporciona datos a través de uno de hello otros orígenes de datos o soluciones.  Puede ser repositorio de hello toopopulate usado desde cualquier cliente que puede llamar a la API de hello y no se basa en la programación de la colección de Hola de cualquier origen de datos o la solución.

* [API del recopilador de datos HTTP de Log Analytics](../log-analytics/log-analytics-data-collector-api.md)

### <a name="retrieve-data-from-hello-log-analytics-repository"></a>Recuperar datos de repositorio de análisis de registros de Hola
Existen varios métodos para recuperar datos de repositorio de OMS Hola.  Puede desea que los usuarios tooretrieve datos mediante la consola de OMS de Hola y les proporcionan diferentes tipos de visualizaciones y análisis.  También puede recuperar los datos de Hola desde un proceso externo, como otra solución de administración.

#### <a name="log-searches"></a>Búsqueda de registros
Todos los datos almacenados en el repositorio OMS Hola está disponible a través de búsquedas de registros.  Los usuarios podrán realizar su propio análisis ad hoc en la consola de OMS de Hola o cree un panel con una visualización para una búsqueda de registros determinado.  Las soluciones pueden contener vistas personalizadas con visualizaciones basadas en búsquedas predefinidas.  Puede usar datos de tooaccess de API de búsqueda de registros de hello en el repositorio OMS Hola desde una herramienta de administración o la aplicación externa.  

* [Búsquedas de registros en Log Analytics](../log-analytics/log-analytics-log-searches.md)
* [API de REST de búsqueda de registros de Log Analytics](../log-analytics/log-analytics-log-search-api.md)
* [Cmdlets deLog Analytics](https://msdn.microsoft.com/library/mt188224.aspx)

#### <a name="custom-views"></a>Vistas personalizadas
Hola Diseñador de vistas permite toocreate vistas personalizadas en la consola de OMS de Hola que proporcionarán a los usuarios de visualización y análisis de datos de hello en la solución.  Cada vista incluye un icono que se muestra en la página principal de Hola de consola de Hola y de cualquier número de elementos de visualización que se basan en búsquedas de registros que defina.

* [Diseñador de vistas de Log Analytics](../log-analytics/log-analytics-view-designer.md)

#### <a name="power-bi"></a>Power BI
Análisis de registros pueden exportar automáticamente datos de repositorio de OMS de hello en Power BI lo que permite aprovechar sus visualizaciones y herramientas de análisis.  Por lo que los datos de Hola se mantengan actualizados toodate realiza esta exportación según una programación. 

* [Exportar datos de análisis de registros tooPower BI](../log-analytics/log-analytics-powerbi.md)

## <a name="automation"></a>Automation
OMS puede automatizar procesos tooreact toocollected datos o tooperform otras funciones de administración.  Puede recopilar datos de la aplicación e insertarlo en el repositorio de OMS hello, o puede automatizar la corrección de Hola de un problema conocido en toodata de respuesta que se encuentra en el repositorio de Hola. 

![Automation](media/operations-management-suite-integration/automate.png)

### <a name="runbooks"></a>Runbooks
Runbooks de automatización de Azure ejecutar scripts de PowerShell y los flujos de trabajo en hello nube de Azure.  Puede usarlas toomanage recursos de Azure o cualquier otro recurso que puede tener acceso desde la nube de Hola.  También se pueden ejecutar runbooks en un centro de datos local con Hybrid Runbook Worker.  Puede iniciar un runbook desde Hola portal de Azure o desde procesos externos mediante un número de métodos como PowerShell u Hola API de automatización.

* [Inicio de un runbook en Azure Automation](../automation/automation-starting-a-runbook.md)
* [Cmdlets de Azure Automation](https://msdn.microsoft.com/library/dn690262.aspx)
* [API de REST de Automation](https://msdn.microsoft.com/library/mt662285.aspx)
* [Automation .NET](https://msdn.microsoft.com//library/mt465763.aspx)

### <a name="alerts"></a>Alertas
Las reglas de alerta ejecutan automáticamente según la programación de tooa de búsquedas de registros.  Si los resultados de hello coinciden con determinada alerta resultante de criterios Hola puede iniciar un runbook en automatización de Azure o llamar a un webhook que puede iniciar un proceso externo.  Dos de estas respuestas pueden incluir detalles de alerta de hello incluye datos de hello devueltos en la búsqueda de registro de hello.

* [Alertas de Log Analytics](../log-analytics/log-analytics-alerts.md)
* [API de alertas de Log Analytics](../log-analytics/log-analytics-api-alerts.md)

## <a name="backup-and-site-recovery"></a>Backup y Site Recovery
Copia de seguridad y recuperación del sitio de Azure proporcionan servicios para proteger los datos de su empresa y garantizar la disponibilidad de Hola de servidores y aplicaciones.  Puede aprovechar estas tooperform servicios tales escenarios como proporcionar servicios de copia de seguridad de la aplicación o iniciar una conmutación por error de una máquina virtual.

* [Cmdlets de Azure Backup](https://msdn.microsoft.com/library/mt619253.aspx)
* [API de REST de Azure Site Recovery](https://msdn.microsoft.com/library/azure/mt750497.aspx)
* [Cmdlets de Azure Site Recovery](https://msdn.microsoft.com/library/mt637930.aspx)

## <a name="custom-solutions"></a>Soluciones personalizadas
Puede encapsular la lógica de integración en una solución personalizada toorun en el área de trabajo o en el área de trabajo de un cliente.  La solución puede incluir cualquiera de los métodos de integración de hello en este artículo en suma tooother recursos tooprovide un escenario de administración completa.  recursos de Hello en solución de Hola se empaquetan tal que cuando se quita la solución de hello, todos los recursos de Hola que creó se quitan del área de trabajo OMS de Hola y suscripción de Azure.

Por ejemplo, la solución podría incluir un runbook de automatización toogather y proceso de datos y, a continuación, rellenar el repositorio de análisis de registros de hello mediante Hola API de recopilador de datos HTTP.  También puede incluir una vista personalizada que presenta y analiza los datos recopilado de saludo.  

* Creación de soluciones personalizadas (próximamente)    

## <a name="next-steps"></a>Pasos siguientes
* Hola de referencia [OMS SDK](operations-management-suite-sdk.md) para obtener información técnica acerca de cómo automatizar los servicios de OMS.  

