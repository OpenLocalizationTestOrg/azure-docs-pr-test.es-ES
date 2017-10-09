---
title: "información general de Management Suite (OMS) aaaOperations | Documentos de Microsoft"
description: "Microsoft Operations Management Suite (OMS) es la solución de administración de TI basada en la nube de Microsoft que le ayuda a administrar y proteger su infraestructura local y en la nube.  Este artículo describe el valor de Hola de OMS, identifica los servicios diferentes de Hola y ofertas que se incluyen en OMS y proporciona vínculos tootheir detallada contenido."
services: operations-management-suite
documentationcenter: 
author: bwren
manager: jwhit
editor: tysonn
ms.assetid: 9dc437b9-e83c-45da-917c-cb4f4d8d6333
ms.service: operations-management-suite
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/16/2017
ms.author: bwren
ms.openlocfilehash: ec3fe6d82aec46d1f715a4338f126e79e04a9147
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="what-is-operations-management-suite-oms"></a>¿Qué es Operations Management Suite (OMS)?
Este artículo proporciona un tooOperations Management Suite (OMS) incluyendo una breve descripción de valor para el negocio Hola proporciona, soluciones de servicios y la administración de hello incluye y ofertas de Hola que empaquetar juntos servicios diferentes de introducción y soluciones.  Se incluyen vínculos toohello obtener documentación sobre la implementación y uso de cada servicio y la solución.

## <a name="from-on-premises-toohello-cloud"></a>Desde la nube de toohello local
Microsoft lleva ya mucho tiempo proporcionado productos para la administración de entornos empresariales.  Varios productos se consolidan en conjunto de productos de administración de System Center de hello en 2007.  Esto incluye el Administrador de configuración que proporciona características como la distribución de software e inventario, Operations Manager que proporciona supervisión proactiva de sistemas y aplicaciones, Orchestrator que incluye procesos manuales de runbooks tooautomate y el Administrador de protección de datos de copia de seguridad y recuperación de datos críticos.

Con más recursos informáticos mover toohello en la nube, los productos de System Center habían obtenido más características en la nube, como Operations Manager y administrar recursos de Azure de Orchestrator.  No obstante estas soluciones estaban diseñadas fundamentalmente como soluciones de entorno local y requieren una inversión importante para la implementación y el mantenimiento de un entorno de administración local.  toocompletely aprovechar nube hello y admitir futuras aplicaciones, un nuevo toomanagement enfoque era necesaria.

## <a name="introducing-operations-management-suite"></a>Introducción a Microsoft Operations Management Suite
Operations Management Suite (también conocido como OMS) es una colección de servicios de administración que se diseñaron en nube de Hola desde el inicio de Hola.  En lugar de implementar y administrar recursos locales, los componentes de OMS se hospedan en su totalidad en Azure.  La configuración es mínima, y puede estar listo y rindiendo literalmente en cuestión de minutos.  

- **Mínimo costo y complejidad de implementación.**  Dado que todos los componentes de Hola y datos de OMS se almacenan en Azure, pueden funcionar y ejecuta en poco tiempo sin la complejidad de Hola e inversión en local componentes.
- **Niveles de la escala de toocloud.**  No tienes tooworry acerca del pago de los recursos de proceso que no es necesario o acerca de quedarse sin espacio de almacenamiento desde hello en la nube permite toopay solo para lo que realmente utiliza y ajusta con rapidez carga tooany que necesita.  Puede iniciar debido a que administra unos tooget de recursos iniciado y, a continuación, escalar tooyour todo el entorno.
- **Aprovechar las características más recientes de Hola.**  Las características de los servicios de OMS se están agregando y actualizando constantemente.  Constantemente tendrá acceso toohello características más recientes sin las actualizaciones de toodeploy de requisito.
- **Servicios integrados.**  Mientras que cada uno de los servicios de OMS Hola proporcionan un valor significativo en sus propios, puedan funcionar juntos toosolve escenarios de administración complejas.  Por ejemplo, un runbook en automatización de Azure puede dirigir un proceso de conmutación por error con Azure Site Recovery y, a continuación, registrar información tooLog análisis toogenerate una alerta.
- **Información global.**  Soluciones de administración de OMS continuamente tengan información más reciente de toohello de acceso.  Hola solución seguridad y auditoría, por ejemplo, puede realizar un análisis de amenazas con las amenazas más recientes de hello detectadas alrededor de Hola a todos.
- **Acceso desde cualquier lugar.**  Obtenga acceso a su entorno de administración desde cualquier lugar en donde tenga un explorador.  Instalar aplicación OMS de hello en tu smartphone para datos de supervisión de tooyour de acceso.

### <a name="is-it-just-for-hello-cloud"></a>¿Es solo para la nube de hello?
Solo porque servicios OMS se ejecutan en nube de hello no significa que no se puede administrar eficazmente el entorno local.  Colocar a un agente en todas las ventanas o equipo de Linux en su centro de datos y enviará tooLog de datos donde se pueden analizar junto con todos los demás datos de análisis recopilados de los servicios en la nube o local.  Usar copia de seguridad de Azure y Azure Site Recovery tooleverage hello en la nube para copia de seguridad y de alta disponibilidad para los recursos locales.  
Runbooks de nube de hello normalmente no puede acceder a los recursos locales, pero puede instalar un agente en uno o más equipos demasiado que va a hospedar runbooks en su centro de datos.  Cuando se inicia un runbook, simplemente especifique si desea toorun en nube de Hola o en un trabajo local.

## <a name="hybrid-management-with-system-center"></a>Administración híbrida con System Center
Si tiene una instalación existente de System Center, puede integrar estos componentes con servicios OMS tooprovide una solución híbrida para sus locales y entornos aprovechando especialidades relativa de Hola de cada producto en la nube.  Conectar los existente Operations Manager grupo tooLog análisis tooanalyze administrar agentes de administración en la nube de Hola.  Utilice el proceso de copia de seguridad existente con Data Protection Manager toobackup su toohello datos en la nube.  


## <a name="oms-services"></a>Servicios de OMS
un conjunto de servicios que se ejecutan en Azure proporciona funcionalidad básica de Hola de OMS.  Cada servicio proporciona una función de administración específico y puede combinar escenarios de administración diferente de tooachieve de servicios.

|| Servicio | Descripción |
|:--|:--|:--|
| ![Log Analytics](media/operations-management-suite-overview/icon-log-analytics.png) | Log Analytics | Supervisar y analizar la disponibilidad de Hola y el rendimiento de los distintos recursos incluidos físicos y máquinas virtuales. |
| ![Azure Automation](media/operations-management-suite-overview/icon-automation.png) | Automatización | Automatización de procesos manuales y aplicación de configuraciones a máquinas físicas y virtuales. |
| ![Copia de seguridad de Azure](media/operations-management-suite-overview/icon-backup.png) | Backup | Realización de copias de seguridad y restauración de datos críticos. |
| ![Azure Site Recovery](media/operations-management-suite-overview/icon-site-recovery.png) | Site Recovery | Provisión de una alta disponibilidad para las aplicaciones críticas. |

### <a name="log-analytics"></a>Log Analytics
[Log Analytics](http://azure.microsoft.com/documentation/services/log-analytics) proporciona servicios de supervisión para OMS recopilando datos de los recursos administrados en un repositorio central.  Estos datos podrían incluir eventos, datos de rendimiento o datos personalizados proporcionadas a través de la API de Hola. Una vez recopilados, datos de hello están disponibles para las alertas, el análisis y la exportación.  Este método le permite tooconsolidate datos desde una variedad de orígenes, por lo que puede combinar datos de los servicios de Azure con su entorno local existente.  Separa claramente también colección Hola de datos de Hola de acción de hello realizada en los datos para que todas las acciones están disponibles tooall tipos de datos.  

![Introducción a Log Analytics](media/operations-management-suite-overview/overview-log-analytics.png)

#### <a name="collecting-data"></a>La recopilación de datos
Hay una variedad de formas que se pueden obtener datos en el repositorio de Hola para tooanalyze de análisis de registros.

- **Equipos y máquinas virtuales de Windows o Linux.**  Instalar Microsoft Monitoring Agent de hello en [Windows](../log-analytics/log-analytics-windows-agents.md) y [Linux](../log-analytics/log-analytics-linux-agents.md) equipos o máquinas virtuales que desea toocollect datos de.  agente de Hello descargará automáticamente de la configuración de análisis de registros que define los eventos y toocollect de datos de rendimiento.  Fácilmente puede instalar a agente de hello en máquinas virtuales que ejecutan en Azure con hello portal de Azure.  Si tiene un entorno de Operations Manager existente, puede conectarse tooLog de grupo de administración de hello análisis y empezar a recopilar datos de todos los agentes existentes automáticamente.
- **Servicios de Azure.**  Análisis de registros recopila telemetría de [diagnósticos de Azure y supervisión de Azure](../log-analytics/log-analytics-azure-storage.md) en el repositorio de Hola para que pueda supervisar recursos de Azure.
- **API del recopilador de datos.**  Log Analytics tiene una [API de REST para rellenar los datos desde cualquier cliente](../log-analytics/log-analytics-data-collector-api.md).  Esto permite los datos de toocollect desde aplicaciones de otros fabricantes o implementar escenarios de administración personalizado.  Un método común es toouse un runbook en datos de toocollect de automatización de Azure y, a continuación, usar Hola API del recopilador de datos toowrite se toohello repositorio.

#### <a name="reporting-and-analyzing-data"></a>Informes y análisis de datos
Análisis de registros incluyen una consulta eficaz lenguaje tooextract de datos almacenado en el repositorio de Hola.  Puesto que los datos de todos los orígenes se almacenan como registros, puede analizar datos de varios orígenes en una sola consulta.
  
Además tooad hoc análisis, análisis de registros proporciona tooreport de varias maneras y analizar datos desde una consulta.

- **Vistas y paneles.**  [Vistas](../log-analytics/log-analytics-view-designer.md) y [paneles](../log-analytics/log-analytics-dashboards.md) visualizar Hola resultados de una consulta en el portal de Hola.  Soluciones de administración normalmente incluirá vistas que analice los datos de Hola de solución de Hola.  También puede crear sus propias vistas personalizadas de datos tooanalyze y con facilidad está disponible en el portal personalizado.
- **Exportación.**  Tener resultados de Hola Hola opción tooexport de cualquier consulta que se puede analizar fuera de análisis de registros.  Incluso puede programar una exportación regular[Power BI](../log-analytics/log-analytics-powerbi.md) que proporciona capacidades de visualización y análisis significativas.
- **API de búsqueda de registros.**  Log Analytics tiene una [API de REST para recopilar datos desde cualquier cliente](../log-analytics/log-analytics-log-search-api.md).  Esto le permite tooprogrammatically trabajo con los datos recopilados en el repositorio de Hola o acceder a él desde otra herramienta de supervisión.

#### <a name="alerting"></a>Alertas
Log Analytics puede [alertar de forma proactiva](../log-analytics/log-analytics-alerts.md), o realizar una acción correctora cuando detecta un problema.  Al igual que todos los demás análisis en Log Analytics, esto se realiza mediante una búsqueda de registros.  Esta búsqueda se ejecuta según una programación regular y se crea una alerta si los resultados de hello coincide con determinados criterios.

![Alertas de Log Analytics](media/operations-management-suite-overview/overview-alerts.png)

Además toocreating un registro de alertas en el repositorio de análisis de registros de hello, las alertas pueden llevan Hola siguientes acciones.

- **Correo electrónico.**  Enviar un correo electrónico tooproactively recibir una notificación de un problema detectado.
- **Runbook.**  Una alerta de Log Analytics puede iniciar un runbook en Azure Automation.  Esto se hace normalmente problema de tooattempt toocorrect Hola detectado.  Hello runbook se puede iniciar en la nube de Hola Hola se pudo iniciar el caso de un problema en Azure u otro en la nube o en un agente local para un problema en una máquina física o virtual.
- **Webhook.**  Una alerta puede iniciar un webhook y pasar datos de resultados de Hola Hola de búsqueda de registros.  Esto permite la integración con servicios externos, como un sistema de alertas alternativo o traten tootake acción correctiva para un sitio web externo.

### <a name="azure-automation"></a>Azure Automation
[Automatización de Azure](http://azure.microsoft.com/documentation/services/automation) proporciona tooOMS de administración de automatización y la configuración de proceso.  Automatiza los procesos manuales y ayuda a las configuraciones de tooenforce de equipos físicos y virtuales.  

#### <a name="process-automation"></a>Automatización de procesos
Azure Automation automatiza procesos manuales mediante [runbooks](../automation/automation-runbook-types.md) que se basan en un script de PowerShell o un flujo de trabajo de PowerShell.  También incluye activos auxiliares runbooks, tales como variables que se pueden compartir entre varios runbooks y las credenciales y conexiones que le permiten información toostore cifrado que podría ser necesario para un runbook para la autenticación.
Runbooks ofrecen automatización de procesos para hello otros servicios en el conjunto de Hola.  Puesto que cada Hola pueden tener acceso a otros servicios con PowerShell o a través de una API de REST, puede crear runbooks tooperform funciones como la recopilación de datos de administración de análisis de registros o bien iniciando una copia de seguridad con copias de seguridad de Azure.

##### <a name="accessing-resources"></a>Acceso a los recursos
Puesto que los runbooks se basan en PowerShell, pueden administrar cualquier recurso al que se puede acceder con cmdlets de PowerShell.  Cuando se [cargar un módulo](../automation/automation-integration-modules.md) en su cuenta de automatización, se convierte en runbooks tooall disponible en esa cuenta. 
 
Cuando los runbooks se ejecutan en la nube de hello, pueden acceder los recursos accesibles desde la nube de Hola.  Podría tratarse de recursos de la suscripción de Azure, de otra nube, como Amazon Web Services (AWS) o de un servicio accesible a través de una API de REST.  Runbooks de hello nube no se ejecutan bajo las credenciales, pero pueden aprovechar los activos de automatización, como las credenciales y conexiones, certificados tooauthenticate tooresources tienen acceso a.

En su centro de datos más probable es que no se pueden tener acceso a recursos de un runbook que se ejecutan en la nube de Hola.  Puede instalar uno o varios [Hybrid Runbook Workers](../automation/automation-hybrid-runbook-worker.md) en los datos aunque centro toorun runbooks que requieren acceso a los recursos de toolocal.  Cuando se inicia un runbook, especifica si debe ejecutarse en la nube de Hola o en un trabajador específico.

![Runbooks de Azure Automation](media/operations-management-suite-overview/overview-runbooks.png)

##### <a name="starting-a-runbook"></a>Inicio de un runbook
Los runbooks se pueden [iniciar con una serie de métodos](../automation/automation-starting-a-runbook.md) lo que permite que puedan incluirse en una variedad de escenarios de administración.  

- **Azure Portal.**  Al igual que otros servicios de Azure, automatización de Azure puede administrarse desde Hola Portal de Azure.  Además toostarting runbooks, puede importarlos o crear sus propios.
- **Programación.**  Puede programar runbooks toostart a intervalos regulares.  Esto le permite tooautomatically repetir un proceso de administración normal o recopilar datos tooLog análisis.
- **PowerShell y API.**  Puede iniciar runbooks y pase ellos requiere información de parámetros de un cmdlet de PowerShell u Hola API de REST de automatización de Azure.  
- **Webhook.**  Se puede crear un webhook para cualquier runbook que le permite toobe inició desde otras aplicaciones o sitios web.
- **Alerta de Log Analytics.**  Una alerta de análisis de registros puede iniciar automáticamente un problema de hello toocorrect de tooattempt de runbook identificado por alerta de Hola.

#### <a name="configuration-management"></a>Administración de configuración
[Configuración de estado deseado (DSC) de PowerShell](../automation/automation-dsc-overview.md) es una plataforma de administración de Windows PowerShell que permite toodeploy y aplicar la configuración de hello físicos y máquinas virtuales.  Automatización de Azure administra las configuraciones de DSC y proporciona a un servidor de extracción en la nube de Hola que agentes pueden tener acceso a las configuraciones de tooretrieve necesario.

![DSC de Azure Automation](media/operations-management-suite-overview/overview-dsc.png)

### <a name="azure-backup-and-azure-site-recovery"></a>Azure Backup y Azure Site Recovery
Copia de seguridad de Azure y Azure Site Recovery contribuyen toobusiness continuidad y recuperación ante desastres.  Cada uno de ellos tiene características que le ayudarán a tooensure que las aplicaciones permanecen disponibles cuando se producen de interrupciones y devolverán toonormal operaciones cuando los sistemas vienen vuelve a estar conectados.  Ambos servicios contribuyen toohello objetivos de punto de recuperación (RPO) y objetivos de tiempo de recuperación (RTO) definidos para su organización. El RPO define en el que datos no están disponibles durante una interrupción de límite aceptable de Hola y Hola RTO limita la cantidad aceptable de Hola de tiempo en el que un servicio o aplicación no está disponible durante una interrupción.

#### <a name="azure-backup"></a>Azure Backup
[Azure Backup](http://azure.microsoft.com/documentation/services/backup) proporciona copias de seguridad de datos y restauración de servicios de OMS.  Protege los datos de las aplicaciones y los conserva durante años sin necesidad de realizar ninguna inversión y afrontando unos costes operativos mínimos.  Hacer una copia de datos desde servidores Windows físicos y virtuales en las cargas de trabajo tooapplication de suma, como SQL Server y SharePoint.  También puede utilizarse por tooAzure de datos de System Center Data Protection Manager (DPM) tooreplicate protegido para ofrecer redundancia y almacenamiento a largo plazo.

Los datos protegidos en Azure Backup se almacenan en un almacén de copia de seguridad ubicado en una región geográfica determinada. Hola datos se replican dentro Hola la misma región y, según tipo hello de almacén, también se puede tooanother replicada región para la resistencia adicional.

Azure Backup tiene tres escenarios fundamentales.

- **Máquina de Windows con agente de Azure Backup.** Copia de seguridad de archivos y carpetas desde cualquier cliente o servidor Windows directamente tooyour almacén de copia de seguridad de Azure.<br><br>![Máquina de Windows con agente de Azure Backup](media/operations-management-suite-overview/overview-backup-01.png)
- **System Center Data Protection Manager (DPM) o servidor de Microsoft Azure Backup.** Aprovechar archivos toobackup DPM o el servidor de copia de seguridad de Microsoft Azure y carpetas en las cargas de trabajo tooapplication de suma, como el almacenamiento toolocal SQL y SharePoint y, a continuación, se replican tooyour almacén de copia de seguridad de Azure. Es compatible con máquinas virtuales Windows y Linux en Hyper-V o VMware.<br><br>![System Center Data Protection Manager (DPM) o servidor de Microsoft Azure Backup](media/operations-management-suite-overview/overview-backup-02.png)
- **Extensiones de máquina virtual de Azure.** Copia de seguridad de Windows o Linux virtual máquinas en Azure tooyour almacén de copia de seguridad de Azure.<br><br>![Extensiones de la máquina virtual de Azure](media/operations-management-suite-overview/overview-backup-03.png)



#### <a name="azure-site-recovery"></a>Azure Site Recovery
[Azure Site Recovery](http://azure.microsoft.com/documentation/services/site-recovery) proporciona continuidad del negocio mediante la coordinación de la replicación de local virtuales y máquinas físicas tooAzure o tooa de sitio secundario. Si su sitio primario no está disponible, conmutación por error toohello de ubicación secundaria para que los usuarios pueden seguir trabajando y se producirá un error cuando sistemas tooworking de devolución. 

Azure Site Recovery proporciona alta disponibilidad para servidores y aplicaciones.  Contribuye tooyour la continuidad del negocio y una estrategia de recuperación (BCDR) mediante la coordinación de replicación, la conmutación por error y la recuperación de máquinas virtuales de Hyper-V de locales, máquinas virtuales de VMware y servidores físicos de Windows o Linux. Puede replicar el centro de datos secundario tooa máquinas o ampliar su centro de datos mediante replicación tooAzure. Site Recovery también proporciona conmutación por error simple y recuperación para cargas de trabajo. Se integra con mecanismos de recuperación ante desastres, como SQL Server AlwaysOn y proporciona planes de recuperación para una conmutación por error sencilla de cargas de trabajo que están organizados en niveles entre varias máquinas.

Azure Site Recovery tiene tres escenarios fundamentales de replicación.

- **Replicación de máquinas virtuales de Hyper-V.**  Si las máquinas virtuales de Hyper-V se administran en nubes VMM, puede replicar tooa almacenamiento de centro o tooAzure de datos secundaria. Replicación tooAzure es a través de una conexión a internet segura. Centro de datos de replicación tooa secundario está por encima de hello LAN.  Si las máquinas virtuales de Hyper-V no están administradas por VMM, puede replicar tooAzure almacenamiento solo. Replicación tooAzure es a través de una conexión a internet segura.<br><br>![Replicación de máquinas virtuales de Hyper-V](media/operations-management-suite-overview/overview-siterecovery-hyperv.png)
- **Replicación de máquinas virtuales de VMWare.**  Puede replicar VMware máquinas virtuales tooa centro de datos secundario ejecuta almacenamiento VMware o tooAzure. Replicación tooAzure puede producirse a través de una VPN de sitio a sitio o ExpressRoute de Azure o a través de una conexión a Internet segura. Centro de datos de replicación tooa secundario se produce a través de canal de datos de InMage Scout Hola.<br><br>![Replicación de máquinas virtuales de VMWare](media/operations-management-suite-overview/overview-siterecovery-vmware.png)
- **Replicación de servidores físicos de Windows o Linux.**  Puede replicar servidores físicos tooa centro de datos o tooAzure almacenamiento secundario. Replicación tooAzure puede producirse a través de una VPN de sitio a sitio o ExpressRoute de Azure o a través de una conexión a Internet segura. Centro de datos de replicación tooa secundario se produce a través de canal de datos de InMage Scout Hola. Azure Site Recovery tiene una solución de OMS que muestra algunas estadísticas, pero debe usar Hola portal de Azure para cualquier operación.<br><br>![Replicación de servidores físicos de Windows o Linux](media/operations-management-suite-overview/overview-siterecovery-physical.png)


Site Recovery almacena metadatos en almacenes ubicados en una región geográfica de Azure determinada. Ningún dato replicado se almacena por hello servicio Site Recovery.

## <a name="management-solutions"></a>Soluciones de administración
[Las soluciones de administración](operations-management-suite-solutions.md) son conjuntos de lógica preempaquetados que implementan un escenario de administración concreto aprovechando uno o más servicios de OMS.  Diferentes soluciones están disponibles de Microsoft y de asociados de negocios que puede agregar fácilmente tooyour suscripción de Azure tooincrease Hola valo su inversión de OMS.  Como un socio puede crear su propias soluciones toosupport sus aplicaciones y servicios y proporcionarlos toousers a través de hello Azure Marketplace o plantillas de inicio rápido.

Un buen ejemplo de una solución que aprovecha la funcionalidad adicional de varios servicios tooprovide es hello [solución de administración de actualizaciones](oms-solution-update-management.md).  Esta solución utiliza el agente de análisis de registros de Hola para Windows y Linux toocollect obtener información acerca de las actualizaciones necesarias en cada agente.  Escribe este repositorio de análisis de registros de toohello de datos donde se pueden analizar con un panel incluido.  Cuando se crea una implementación, runbooks en automatización de Azure son actualizaciones de tooinstall usado necesario.  Administrar todo este proceso en el portal de hello y no es necesario tooworry acerca de los detalles subyacentes de Hola.

![Solución](media/operations-management-suite-overview/overview-solution.png)

La mayoría de soluciones puede realizar una o varias de hello siguientes funciones.

- Recopilar información adicional.  Log Analytics recopila una variedad de datos de los clientes y servicios, incluidos los eventos y datos de rendimiento.  Una solución de administración puede recopilar información adicional que no esté disponible a partir de otros orígenes de datos, a menudo con runbooks de Azure Automation.
- Proporcionar un análisis adicional de la información recopilada.  Las soluciones de administración incluyen paneles y vistas que proporcionan análisis y visualización de los datos.  Estas búsquedas de registros de toopredefined atrás de vínculo que le permiten toodrill en hello datos detallan.  También pueden realizar análisis en los datos que se ya se han recopilado en el repositorio de hello, por ejemplo, buscar en eventos de seguridad de patrones que supone una amenaza.
- Agregar funcionalidad.  Algunas soluciones proporcionadas por Microsoft pueden basarse en las capacidades de Hola de funcionalidades adicionales de hello core services tooprovide.  Por ejemplo, mapa de servicio proporciona su propia consola toodiscover y asigna el servidor y dependencias de procesos en tiempo real.
Soluciones con regularidad añadidas tooOMS por Microsoft y partners permitiéndole toocontinuously aumentar el valor de Hola de su inversión.  Puede examinar e instalar soluciones de Microsoft a través de hello catálogo de soluciones en el portal de OMS de Hola o examinar e instalar soluciones de Microsoft y socios a través de hello Azure Marketplace en hello Portal de Azure.  

![Galería de soluciones](media/operations-management-suite-overview/solution-gallery.png)


## <a name="next-steps"></a>Pasos siguientes
* Obtenga información sobre [Log Analytics](http://azure.microsoft.com/documentation/services/log-analytics).
* Obtenga información sobre [Azure Automation](../automation/automation-intro.md).
* Obtenga información sobre [Azure Backup](http://azure.microsoft.com/documentation/services/backup).
* Obtenga información sobre [Azure Site Recovery](http://azure.microsoft.com/documentation/services/site-recovery).
* Detectar hello [soluciones disponibles](../log-analytics/log-analytics-add-solutions.md) en diferentes ofertas de OMS Hola. 

