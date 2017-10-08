---
title: "aaaWhat es la automatización de Azure | Documentos de Microsoft"
description: "Obtenga información acerca de qué valor proporciona la automatización de Azure y obtener respuestas toocommon preguntas para que puede empezar a trabajar crear, con runbooks y DSC de automatización de Azure."
services: automation
documentationcenter: 
author: mgoedtel
manager: jwhit
editor: 
keywords: "qué es la automatización, automatización de azure, ejemplos de automatización de azure"
ms.assetid: 0cf1f3e8-dd30-4f33-b52a-e148e97802a9
ms.service: automation
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 05/10/2016
ms.author: magoedte;bwren
ms.openlocfilehash: 1e5a90e272d6b2beb7b5007e2fea2c110dbd79b1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="azure-automation-overview"></a>Información general sobre Automatización de Azure
Automatización de Microsoft Azure proporciona una manera para los usuarios tooautomate hello, larga ejecución, propensas a errores, tareas manuales y repiten con frecuencia que se realizan normalmente en un entorno de nube y empresarial. Ahorra tiempo y aumenta la confiabilidad de Hola de tareas administrativas normales e incluso programa toobe automáticamente realiza a intervalos regulares. Puede automatizar procesos mediante runbooks o automatizar la administración de configuración mediante la configuración de estado deseado. En este artículo se ofrece una breve información general sobre Automatización de Azure y se responden algunas preguntas habituales. Puede hacer referencia tooother artículos en esta biblioteca para obtener más información sobre temas diferentes Hola.

## <a name="automating-processes-with-runbooks"></a>Procesos de automatización con runbooks
Un runbook es un conjunto de tareas que realizan algún proceso automatizado en Automatización de Azure. Puede ser un proceso sencillo, como iniciar una máquina virtual y la creación de una entrada del registro, o puede que tenga un runbook complejo que combina otro más pequeño tooperform de runbooks un proceso complejo en varios recursos o incluso varios nubes y entornos locales.  

Por ejemplo, podría tener un manual existente del proceso para truncar una base de datos SQL si se acerque al tamaño máximo que incluye varios pasos como conexión server toohello, conectar toohello base de datos, obtener Hola tamaño actual de la base de datos, compruebe si umbral superó y, a continuación, truncará y notificar al usuario. En lugar de realizar manualmente cada uno de estos pasos, podría crear un runbook que realizara todas estas tareas como un solo proceso. Podría iniciar runbook hello, proporcione información de hello necesario, como SQL server nombre de Hola y nombre de base de datos, correo electrónico del destinatario y, a continuación, se colocan mientras se completa el proceso de Hola. 

## <a name="what-can-runbooks-automate"></a>¿Qué pueden automatizar los runbooks?
Los runbooks de Automatización de Azure se basan en Windows PowerShell o en el flujo de trabajo de PowerShell, por lo que hacen todo lo que puede hacer PowerShell. Si una aplicación o servicio tiene una API, un runbook puede trabajar con ella. Si dispone de un módulo de PowerShell para la aplicación hello, puede cargar ese módulo en automatización de Azure e incluyen estos cmdlets en su runbook. Runbooks de automatización de Azure ejecutan en hello nube de Azure y puede tener acceso a recursos externos que pueden tener acceso desde la nube de hello ni recursos en la nube. Usar [Hybrid Runbook Worker](automation-hybrid-runbook-worker.md), runbooks pueden ejecutarse en los datos locales recursos locales de toomanage center. 

## <a name="getting-runbooks-from-hello-community"></a>Obtener runbooks de la Comunidad de Hola
Hola [Galería de runbooks](automation-runbook-gallery.md#runbooks-in-runbook-gallery) contiene runbooks de comunidad hello y Microsoft que puede utilizar sin cambios en su entorno o personalícelos para sus propios fines. También son útiles tooas referencias toolearn cómo toocreate sus propios runbooks. Incluso puede aportar su propia galería de toohello de runbooks que cree que otros usuarios pueden encontrar útiles. 

## <a name="creating-runbooks-with-azure-automation"></a>Creación de runbooks con Automatización de Azure
También puede [crear sus propios runbooks](automation-creating-importing-runbook.md) de desecho o modificación de runbooks de hello [Galería de runbooks](http://msdn.microsoft.com/library/azure/dn781422.aspx) para sus propios requisitos. Hay cuatro [tipos de runbooks](automation-runbook-types.md) diferentes entre los que puede elegir en función de sus requisitos y de la experiencia con PowerShell. Si prefiere toowork directamente con hello código de PowerShell, puede usar un [PowerShell runbook](automation-runbook-types.md#powershell-runbooks) o [runbook de flujo de trabajo de PowerShell](automation-runbook-types.md#powershell-workflow-runbooks) que editar sin conexión o con hello [editor de texto](http://msdn.microsoft.com/library/azure/dn879137.aspx) Hola portal de Azure. Si lo prefiere tooedit un runbook sin estar expuesto toohello subyacente el código, a continuación, puede crear un [runbook gráfico](automation-runbook-types.md#graphical-runbooks) con hello [editor gráfico](automation-graphical-authoring-intro.md) Hola portal de Azure. 

¿Prefiere ver tooreading? Eche un vistazo a hello debajo de vídeo de la sesión de Microsoft Ignite en mayo de 2015. Nota: Aunque hello conceptos y características que se describen en este vídeo son correctas, que automatización de Azure ha progresado mucho porque este vídeo se grabó, ahora tiene una interfaz de usuario más amplia de hello portal de Azure y capacidades adicionales de admite.

> [!VIDEO https://channel9.msdn.com/Events/Ignite/2015/BRK3451/player]
> 
> 

## <a name="automating-configuration-management-with-desired-state-configuration"></a>Automatización de la administración de configuración con la configuración de estado deseado
[DSC de PowerShell](https://technet.microsoft.com/library/dn249912.aspx) es una plataforma de administración que permite toomanage, implementar y exigir una configuración para hosts físicos y máquinas virtuales mediante la sintaxis declarativa de PowerShell. Puede definir configuraciones en un servidor de extracción DSC que las máquinas de destino pueden recuperar y aplicar. DSC proporciona un conjunto de cmdlets de PowerShell que puede usar recursos y configuraciones de toomanage.  

[DSC de Automatización de Azure](automation-dsc-overview.md) es una solución basada en la nube para DSC de PowerShell que proporciona los servicios necesarios para los entornos empresariales.  Puede administrar los recursos de DSC de automatización de Azure y aplicar configuraciones toovirtual o máquinas físicas que recuperarlos desde un servidor de extracción de DSC en hello nube de Azure.  También proporciona servicios de informes que le informan de eventos importantes, como cuando se desvían los nodos de su configuración asignada y cuando se ha aplicado una nueva configuración. 

## <a name="creating-your-own-dsc-configurations-with-azure-automation"></a>Creación de sus propias configuraciones DSC con Automatización de Azure
[Las configuraciones de DSC](automation-dsc-overview.md) especificar estado de hello deseado de un nodo.  Pueden aplicar varios nodos Hola mismo tooassure de configuración que mantienen un estado idéntico.  Puede crear una configuración con cualquier texto editor en el equipo local y, después, importarla en Automatización de Azure donde la puede compilar y aplicar los nodos.

## <a name="getting-modules-and-configurations"></a>Obtención de módulos y configuraciones
Puede obtener [módulos de PowerShell](automation-runbook-gallery.md#modules-in-powershell-gallery) que contiene cmdlets que puede usar en sus runbooks y las configuraciones de DSC de hello [Galería de PowerShell](http://www.powershellgallery.com/). También puede iniciar esta galería de hello portal de Azure e Importar módulos directamente en automatización de Azure, o puede descargar e importarlas manualmente. No se puede instalar módulos de hello directamente desde Hola portal de Azure, pero puede descargarlos instalarlos como lo haría con cualquier otro módulo. 

## <a name="example-practical-applications-of-azure-automation"></a>Aplicaciones prácticas de ejemplo de Automatización de Azure
Estos son solo unos pocos ejemplos de ¿qué tipos de Hola de escenarios de automatización con automatización de Azure. 

* Cree y copie máquinas virtuales en diferentes suscripciones de Azure. 
* Programar copias de archivos de un contenedor de almacenamiento de blobs de Azure de tooan de equipo local. 
* Automatice las funciones de seguridad como denegar las solicitudes de un cliente cuando se detecta un ataque de denegación de servicio. 
* Asegúrese de que las máquinas se ajustan continuamente a la directiva de seguridad configuradas.
* Administre la implementación continua del código de aplicación por la infraestructura local y en la nube. 
* Cree un bosque de Active Directory en Azure para su entorno de laboratorio. 
* Trunque una tabla en una Base de datos SQL si la base de datos se acerca al tamaño máximo. 
* Actualice de forma remota la configuración del entorno para un sitio web de Azure. 

## <a name="how-does-azure-automation-relate-tooother-automation-tools"></a>¿Cómo relaciona tooother herramientas de automatización de la automatización de Azure?
[Service Management Automation (SMA)](http://technet.microsoft.com/library/dn469260.aspx) está previsto tooautomate tareas de administración en la nube privada de Hola. Se instala localmente en el centro de datos como componente del [paquete de Microsoft Azure](https://www.microsoft.com/en-us/server-cloud/). SMA y la automatización de Azure usan Hola basada en el mismo formato de runbook en el flujo de trabajo de Windows PowerShell y Windows PowerShell, pero no admite la SMA [runbooks gráficos](automation-graphical-authoring-intro.md).  

[System Center 2012 Orchestrator](http://technet.microsoft.com/library/hh237242.aspx) está pensado para la automatización de recursos locales. Utiliza un formato de runbook diferente que Service Management Automation y automatización de Azure y tiene un interfaz gráfica toocreate los runbooks sin necesidad de utilizar scripts. Sus runbooks se componen de actividades de paquetes de integración escritas específicamente para Orchestrator. 

## <a name="where-can-i-get-more-information"></a>¿Dónde puedo obtener más información?
Una variedad de recursos están disponibles para toolearn más información acerca de la automatización de Azure y crear sus propios runbooks. 

* **biblioteca de Automatización de Azure** . artículos de Hola de esta biblioteca proporciona documentación completa sobre la configuración de Hola y administración de automatización de Azure y para crear sus propios runbooks. 
* [cmdlets de Azure PowerShell](http://msdn.microsoft.com/library/jj156055.aspx) proporcionan información para automatizar operaciones de Azure mediante Windows PowerShell. Los runbooks usan estos cmdlets toowork con recursos de Azure. 
* [Blog de administración](https://azure.microsoft.com/blog/tag/azure-automation/) proporciona información más reciente de hello en automatización de Azure y otras tecnologías de administración de Microsoft. Debe suscribirse toothis blog toostay una toodate con hello más recientes del equipo de automatización de Azure Hola. 
* [Foro de automatización](http://go.microsoft.com/fwlink/p/?LinkId=390561) permite toopost preguntas sobre toobe de automatización de Azure direccionado por Microsoft y Hola Comunidad de automatización. 
* [cmdlets de Automatización de Azure](https://msdn.microsoft.com/library/mt244122.aspx) proporcionan información para automatizar las tareas de administración. Contiene cuentas de automatización de toomanage de cmdlets, activos, runbooks, DSC.

## <a name="can-i-provide-feedback"></a>¿Puedo proporcionar comentarios?
**Envíenos sus comentarios** Si está buscando una solución de runbook o un módulo de integración de Automatización de Azure, publique una solicitud de script en el centro de scripts. Si tiene comentarios o solicitudes de características para Automatización de Azure, publíquelos en [Voz del usuario](http://feedback.windowsazure.com/forums/34192--general-feedback). Gracias. 

