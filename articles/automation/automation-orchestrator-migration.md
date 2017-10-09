---
title: "aaaMigrating de tooAzure Orchestrator automatización | Documentos de Microsoft"
description: "Describe cómo paquetes de integración y toomigrate runbooks de System Center Orchestrator tooAzure automatización."
services: automation
documentationcenter: 
author: bwren
manager: stevenka
editor: tysonn
ms.assetid: 1a7da58c-7a98-49b5-9d9d-001a9f6e631a
ms.service: automation
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/09/2016
ms.author: bwren
ms.openlocfilehash: 797b50067ef2aa68470760e99d494b89ab7baacf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="migrating-from-orchestrator-tooazure-automation-beta"></a>Migración de Orchestrator tooAzure automatización (Beta)
Los runbooks de [System Center Orchestrator](http://technet.microsoft.com/library/hh237242.aspx) se basan en actividades provenientes de paquetes de integración escritos específicamente para Orchestrator, mientras que los runbooks de Automatización de Azure se basan en Windows PowerShell.  [Runbooks gráficos](automation-runbook-types.md#graphical-runbooks) en automatización de Azure tiene un runbooks tooOrchestrator de apariencia similar con sus actividades que representan los cmdlets de PowerShell, runbooks secundarios y activos.

Hola [Kit de herramientas de migración de System Center Orchestrator](http://www.microsoft.com/download/details.aspx?id=47323&WT.mc_id=rss_alldownloads_all) incluye herramientas tooassist en convertir runbooks de Orchestrator tooAzure automatización.  Además runbooks de hello tooconverting por sí mismos, debe convertir los paquetes de integración de hello con actividades de Hola que Hola runbooks usar módulos de toointegration con cmdlets de Windows PowerShell.  

Aquí te mostramos proceso básico de Hola para convertir tooAzure de runbooks de Orchestrator automatización.  Cada uno de estos pasos se describe en detalle en secciones de hello siguientes.

1. Descargar hello [Kit de herramientas de migración de System Center Orchestrator](http://www.microsoft.com/download/details.aspx?id=47323&WT.mc_id=rss_alldownloads_all) que contiene herramientas de Hola y los módulos descritos en este artículo.
2. Importe el [Módulo de actividades estándar](#standard-activities-module) a Automatización de Azure.  Esto incluye versiones convertidas de las actividades estándar de Orchestrator que los runbooks convertidos pueden usar.
3. Importe los [Módulos de integración de System Center Orchestrator](#system-center-orchestrator-integration-modules) en Automatización de Azure para los paquetes de integración usados por los runbooks que acceden a System Center.
4. Convertir paquetes de integración de terceros y personalizados mediante hello [Integration Pack convertidor](#integration-pack-converter) e importar a automatización de Azure.
5. Convertir runbooks de Orchestrator mediante hello [Runbook convertidor](#runbook-converter) e instalar en automatización de Azure.
6. Crear manualmente los activos de Orchestrator requiere en automatización de Azure desde Hola Runbook convertidor no convierte estos recursos.
7. Configurar un [Hybrid Runbook Worker](#hybrid-runbook-worker) en sus runbooks de toorun convertir de centro de datos local que tendrá acceso a recursos locales.

## <a name="service-management-automation"></a>Service Management Automation
[Service Management Automation](http://technet.microsoft.com/library/dn469260.aspx) (SMA) almacena y ejecuta los runbooks en su centro de datos local como Orchestrator y usa Hola mismo módulos de integración como automatización de Azure. Hola [Runbook convertidor](#runbook-converter) convierte runbooks de Orchestrator runbooks toographical aunque no se admiten en SMA.  Aún puede instalar hello [módulo de actividades estándar](#standard-activities-module) y [módulos de integración de System Center Orchestrator](#system-center-orchestrator-integration-modules) en SMA, pero debe realizar manualmente [vuelva a escribir sus runbooks](http://technet.microsoft.com/library/dn469262.aspx).

## <a name="hybrid-runbook-worker"></a>Hybrid Runbook Worker
Los runbooks de Orchestrator se almacenan en un servidor de base de datos y se ejecutan en servidor de runbooks, ambos en su centro de datos local.  Runbooks de automatización de Azure se almacenan en hello nube de Azure y se puede ejecutar en su centro de datos locales con un [Hybrid Runbook Worker](automation-hybrid-runbook-worker.md).  Se trata cómo se suele ejecutar runbooks convertidos de Orchestrator ya están diseñada toorun en servidores locales.

## <a name="integration-pack-converter"></a>Convertidor de paquetes de integración
Hola Integration Pack convertidor convierte los paquetes de integración que se crearon con hello [Orchestrator Integration Kit (OIT)](http://technet.microsoft.com/library/hh855853.aspx) toointegration módulos basan en Windows PowerShell que puede importarse en automatización de Azure o Automatización de la administración de servicio.  

Cuando ejecute hello convertidor del módulo de integración, se le presentará un asistente que le permitirá tooselect un archivo de paquete (.oip) de integración.  Asistente de Hello, a continuación, enumera las actividades de hello incluidas en dicho paquete de integración y permite tooselect que se van a migrar.  Cuando se completa el Asistente de hello, crea un módulo de integración que incluye un cmdlet correspondiente para cada una de las actividades de hello en el paquete de integración de hello original.

### <a name="parameters"></a>parameters
Las propiedades de una actividad en el paquete de integración de hello son convertido tooparameters Hola cmdlet correspondiente en el módulo de integración de Hola.  Los cmdlets de Windows PowerShell tienen un conjunto de [parámetros comunes](http://technet.microsoft.com/library/hh847884.aspx) que se pueden usar con todos los cmdlets.  Por ejemplo, hello - Verbose parámetro hace que un cmdlet toooutput información detallada sobre su funcionamiento.  Ningún cmdlet puede tener un parámetro con el mismo nombre como un parámetro común de Hola.  Si una actividad tiene una propiedad con el mismo nombre como un parámetro común de hello, Asistente Hola le pedirá tooprovide otro nombre para el parámetro hello.

### <a name="monitor-activities"></a>Actividad de supervisión
Supervisar runbooks de inicio de Orchestrator con un [supervisar la actividad de](http://technet.microsoft.com/library/hh403827.aspx) y se ejecutan continuamente toobe espera invocado por un evento determinado.  Automatización de Azure no admite runbooks de monitor, por lo que no se convertirá cualquier monitor de actividades en el paquete de integración de Hola.  En su lugar, se crea un cmdlet de marcador de posición en el módulo de integración de Hola para supervisar la actividad de Hola.  Este cmdlet no tiene ninguna funcionalidad, pero permite que cualquier runbook convertido que lo utilice toobe instalado.  Este runbook no será capaz de toorun en automatización de Azure, pero se puede instalar para que pueda modificarla.

### <a name="integration-packs-that-cannot-be-converted"></a>Paquetes de integración que no se pueden convertir
No se puede convertir paquetes de integración que no se crearon con OIT con hello convertidor del módulo de integración. También hay algunos módulos de integración proporcionados por Microsoft que actualmente no se pueden convertir con esta herramienta.  Las versiones convertidas de estos paquetes de integración se [proporcionan para descarga](#system-center-orchestrator-integration-modules) para que se pueden instalar en Automatización de Azure o Service Management Automation.

## <a name="standard-activities-module"></a>Módulo de actividades estándar
Orchestrator incluye un conjunto de [actividades estándar](http://technet.microsoft.com/library/hh403832.aspx) que no están incluidas en un paquete de integración, pero que son usadas por muchos runbooks.  módulo de actividades estándar de Hello es un módulo de integración que incluye un cmdlet equivalente para cada una de estas actividades.  Debe instalar este módulo de integración en Automatización de Azure antes de importar cualquier runbook convertido que usa una actividad estándar.

Además toosupporting convertir runbooks, cmdlets de hello en el módulo de actividades estándar Hola puede utilizarse por alguien que esté familiarizado con Orchestrator toobuild nuevos runbooks en automatización de Azure.  Mientras la funcionalidad de Hola de todas las actividades estándar Hola puede realizarse con los cmdlets, podría operar de forma diferente.  Hello cmdlets en actividades estándar Hola convertir módulo funcionará Hola igual que sus actividades y usan correspondiente Hola mismos parámetros.  Esto puede ayudar a autor de runbook de Orchestrator existente de hello en su runbooks de automatización de tooAzure de transición.

## <a name="system-center-orchestrator-integration-modules"></a>Módulos de integración de System Center Orchestrator
Microsoft proporciona [paquetes de integración](http://technet.microsoft.com/library/hh295851.aspx) para la creación de componentes de System Center tooautomate de runbooks y otros productos.  Algunos de estos paquetes de integración actualmente se basan en OIT pero actualmente no se pueden convertir toointegration módulos debido a problemas conocidos.  [Módulos de integración de System Center Orchestrator](https://www.microsoft.com/download/details.aspx?id=49555) incluyen las versiones convertidas de estos paquetes de integración que se pueden importar a Automatización de Azure y Service Management Automation.  

Versión RTM de Hola de esta herramienta, las versiones actualizadas de los paquetes de integración de hello según OIT que se puede convertir con hello Integration Pack convertidor que se va a publicar.  También se proporcionará instrucciones tooassist de conversión de runbooks mediante actividades de paquetes de integración de hello no en función de OIT.

## <a name="runbook-converter"></a>Convertidor de runbooks
Convertidor de Runbook Hello convierte los runbooks de Orchestrator en [runbooks gráficos](automation-runbook-types.md#graphical-runbooks) que pueden importarse en automatización de Azure.  

Convertidor de runbook se implementa como un módulo de PowerShell con un cmdlet denominado **ConvertFrom-SCORunbook** que realiza la conversión de Hola.  Cuando se instala la herramienta de hello, creará una sesión de PowerShell de tooa de acceso directo que cargue Hola cmdlet.   

Siguiente es Hola proceso básico tooconvert un runbook de Orchestrator e impórtelo en automatización de Azure.  Hello las secciones siguientes proporcionan más detalles sobre el uso de la herramienta de Hola y trabajar con runbooks convertidos.

1. Exporte uno o varios runbooks desde Orchestrator.
2. Obtener los módulos de integración para todas las actividades de runbook de Hola.
3. Convertir los runbooks de Orchestrator hello en el archivo exportado de Hola.
4. Revisar la información de conversión de registros toovalidate hello y toodetermine las tareas manuales necesarias.
5. Importe los runbooks convertidos a Automatización de Azure.
6. Cree todos los recursos necesarios en Automatización de Azure.
7. Editar runbook de hello en automatización de Azure toomodify las actividades necesarias.

### <a name="using-runbook-converter"></a>Uso del Convertidor de runbooks
Hola sintaxis para **SCORunbook ConvertFrom** es como sigue:

    ConvertFrom-SCORunbook -RunbookPath <string> -Module <string[]> -OutputFolder <string>

* RunbookPath - archivo de exportación de toohello de ruta de acceso que contienen Hola runbooks tooconvert.
* Módulo: lista separada por comas de los módulos de integración que contiene actividades de runbooks Hola.
* OutputFolder - ruta de acceso toohello carpeta toocreate convertir runbooks gráficos.

Hola siguiente comando de ejemplo convierte Hola runbooks en un archivo de exportación denominado **MyRunbooks.ois_export**.  Estos runbooks usan Hola Active Directory y los paquetes de integración de Data Protection Manager.

    ConvertFrom-SCORunbook -RunbookPath "c:\runbooks\MyRunbooks.ois_export" -Module c:\ip\SystemCenter_IntegrationModule_ActiveDirectory.zip,c:\ip\SystemCenter_IntegrationModule_DPM.zip -OutputFolder "c:\runbooks"


### <a name="log-files"></a>Archivos de registro
Hola Runbook convertidor creará Hola siguientes archivos de registro de hello misma ubicación que Hola convertir runbook.  Si ya existen archivos de hello, sobrescribirá con la información de conversión último Hola.

| Archivo | Contenido |
|:--- |:--- |
| Runbook Converter - Progress.log |Pasos detallados de conversión de hello incluida la información para cada actividad que se ha convertido correctamente y advertencia para cada actividad no convertir. |
| Runbook Converter - Summary.log |Resumen de hello última conversión incluidas las advertencias y realizar un seguimiento de las tareas que necesitará tooperform como la creación de una variable necesaria para runbook Hola convertido. |

### <a name="exporting-runbooks-from-orchestrator"></a>Exportación de runbooks desde Orchestrator
Hola Runbook convertidor funciona con un archivo de exportación de Orchestrator que contiene uno o más runbooks.  Creará un runbook de automatización de Azure correspondiente para cada runbook de Orchestrator en el archivo de exportación de Hola.  

tooexport un runbook de Orchestrator, haga clic en nombre de Hola de runbook de hello en Runbook Designer y seleccione **exportar**.  tooexport todos los runbooks en una carpeta, haga clic en nombre de Hola de carpeta de Hola y seleccione **exportar**.

### <a name="runbook-activities"></a>Actividades de runbook
Hola Runbook convertidor convierte cada actividad en hello actividad correspondiente tooa de Orchestrator runbook en automatización de Azure.  Para esas actividades que no se puede convertir, se crea una actividad de marcador de posición en hello runbook con el texto de la advertencia.  Después de importar Hola convertir runbook en automatización de Azure, debe reemplazar cualquiera de estas actividades con actividades válidas que realizan la funcionalidad de hello necesario.

Las actividades de Orchestrator en hello [módulo de actividades estándar](#standard-activities-module) se convertirá.  Sin embargo, hay algunas actividades de Orchestrator estándar que no están en este módulo y no se convierten.  Por ejemplo, **Enviar evento de plataforma** no tiene ningún equivalente de automatización de Azure como eventos de hello es tooOrchestrator específico.

[Supervisar las actividades de](https://technet.microsoft.com/library/hh403827.aspx) no se convierten porque no hay ningún equivalente toothem en automatización de Azure.  Hello excepción son monitor de actividades en [convertir paquetes de integración](#integration-pack-converter) que será la actividad de marcador de posición de toohello convertido.

Cualquier actividad de un [convertir paquete de integración](#integration-pack-converter) se convertirán si proporciona el módulo de integración de toohello de ruta de acceso de hello con hello **módulos** parámetro.  Para paquetes de integración de System Center, puede usar hello [módulos de integración de System Center Orchestrator](#system-center-orchestrator-integration-modules).

### <a name="orchestrator-resources"></a>Recursos de Orchestrator
Hola Runbook convertidor solo convierte los runbooks, no otros recursos de Orchestrator como contadores, variables o conexiones.  Los contadores no se admiten en Automatización de Azure.  Las variables y conexiones se admiten, pero es necesario crearlas manualmente.  archivos de registro de Hello se le informan de hello runbook requiere estos recursos y especificar recursos correspondientes que necesite toocreate en automatización de Azure para hello convierten runbook toooperate correctamente.

Por ejemplo, un runbook puede utilizar una variable toopopulate un valor determinado en una actividad.  Hello runbook convertido convertirá actividad hello y especificar un activo de variable de automatización de Azure con hello mismo nombre como variable de Orchestrator Hola.  Esto se anotarán en hello **Runbook convertidor - Summary.log** archivo creado después de la conversión de Hola.  Necesitará toomanually crear este activo de variable de automatización de Azure antes de utilizar Hola runbook.

### <a name="input-parameters"></a>Parámetros de entrada
Runbooks de Orchestrator aceptan parámetros de entrada con hello **inicializar datos** actividad.  Si runbook Hola que se está convirtiendo incluye esta actividad, un [parámetro de entrada](automation-graphical-authoring-intro.md#runbook-input-and-output) en automatización de Azure Hola runbook se crea para cada parámetro en actividad hello.  A [control de secuencia de comandos de flujo de trabajo](automation-graphical-authoring-intro.md#activities) actividad se crea en runbook Hola convertir que recupera y devuelve cada parámetro.  Las actividades de runbook de Hola que utilizan un parámetro de entrada, consulte toohello salida de esta actividad.

motivo de Hola que se usa esta estrategia es una funcionalidad de toobest reflejado Hola Hola Orchestrator runbook.  Las actividades de runbooks gráficos nuevo deben hacer referencia directamente parámetros tooinput con un origen de datos de entrada de Runbook.

### <a name="invoke-runbook-activity"></a>Actividad Invocar Runbook
Runbooks de Orchestrator iniciar otros runbooks con hello **invocar Runbook** actividad. Si runbook Hola que se está convirtiendo incluye esta actividad y hello **esperar la finalización** opción está establecida, a continuación, se crea una actividad de runbook para él en hello convertir runbook.  Si hello **esperar la finalización** opción no está establecida, a continuación, se crea una actividad de secuencia de comandos de flujo de trabajo que utiliza **Start-AzureAutomationRunbook** toostart Hola runbook.  Después de importar Hola convertir runbook en automatización de Azure, debe modificar esta actividad con información de hello especificada en la actividad de Hola.

## <a name="related-articles"></a>Artículos relacionados
* [System Center 2012: Orchestrator](http://technet.microsoft.com/library/hh237242.aspx)
* [Service Management Automation](https://technet.microsoft.com/library/dn469260.aspx)
* [Trabajo híbrido de runbook](automation-hybrid-runbook-worker.md)
* [Actividades estándar de Orchestrator](http://technet.microsoft.com/library/hh403832.aspx)
* [Descargue el kit de herramientas para migración de System Center Orchestrator](https://www.microsoft.com/en-us/download/details.aspx?id=47323)
