---
title: "galerías de aaaRunbook y el módulo de automatización de Azure | Documentos de Microsoft"
description: "Los runbooks y módulos de comunidad hello y Microsoft están disponibles para tooinstall y usar en su entorno de automatización de Azure.  Este artículo describe cómo se puede tener acceso a estos recursos y toocontribute la Galería de runbooks toohello."
services: automation
documentationcenter: 
author: mgoedtel
manager: jwhit
editor: tysonn
ms.assetid: d3fee7b4-630a-4c10-8425-9bf51d7c9e58
ms.service: automation
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 12/14/2016
ms.author: magoedte;bwren
ms.openlocfilehash: 10b634460edf66dd7548017e3a2f7111b7125f30
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="runbook-and-module-galleries-for-azure-automation"></a>Galerías de runbooks y módulos para Automatización de Azure
En lugar de crear sus propios módulos y runbooks en automatización de Azure, puede tener acceso a una variedad de escenarios que ya se han generado por la Comunidad de Microsoft y Hola.  Puede usar estos escenarios sin modificaciones o como punto de partida para modificarlos según sus requisitos específicos.

Puede obtener runbooks de hello [Galería de runbooks](#runbooks-in-runbook-gallery) y módulos de hello [Galería de PowerShell](#modules-in-powerShell-gallery).  También puede contribuir toohello Comunidad compartiendo escenarios que desarrolle.

## <a name="runbooks-in-runbook-gallery"></a>Runbooks en la Galería de runbooks
Hola [Galería de runbooks](http://gallery.technet.microsoft.com/scriptcenter/site/search?f\[0\].Type=RootCategory&f\[0\].Value=WindowsAzure&f\[1\].Type=SubCategory&f\[1\].Value=WindowsAzure_automation&f\[1\].Text=Automation) proporciona una variedad de runbooks de comunidad hello y Microsoft que puede importar a automatización de Azure. Puede optar por descargar un runbook de galería de Hola que se hospeda en hello [centro de scripts de TechNet](https://gallery.technet.microsoft.com/scriptcenter/site/upload), o puede importar runbooks directamente desde la Galería de Hola de hello portal de Azure clásico o portal de Azure.

Sólo puede importar directamente desde la Galería de runbooks hello mediante Hola portal de Azure clásico o el portal de Azure. No se puede llevar a cabo esta función mediante Windows PowerShell.

> [!NOTE]
> Debe validar el contenido de Hola de los runbooks que obtiene de hello Galería de runbooks y tener mucho cuidado al instalar y ejecutarlos en un entorno de producción. |
> 
> 

### <a name="tooimport-a-runbook-from-hello-runbook-gallery-with-hello-azure-classic-portal"></a>tooimport un runbook de hello Galería de runbooks con hello portal de Azure clásico
1. Hola Portal de Azure, haga clic en, **New**, **servicios de aplicaciones**, **automatización**, **Runbook**, **de la galería**.
2. Seleccione una categoría tooview relacionadas con runbooks y seleccione un runbook tooview sus detalles. Cuando se selecciona runbook Hola que desee, haga clic en botón de flecha derecha Hola.
   
    ![Galería de runbooks](media/automation-runbook-gallery/runbook-gallery.png)
3. Revise Hola contenido de runbook de Hola y tenga en cuenta los requisitos de descripción de Hola. Cuando haya terminado, haga clic en botón de flecha derecha Hola.
4. Escriba los detalles de runbook de hello y, a continuación, haga clic en botón de marca de verificación de Hola. nombre del runbook Hola ya se rellenará.
5. Hola runbook aparecerá en hello **Runbooks** pestaña Hola cuenta de automatización.

### <a name="tooimport-a-runbook-from-hello-runbook-gallery-with-hello-azure-portal"></a>tooimport un runbook de hello Galería de runbooks con hello portal de Azure
1. Hola Portal de Azure, abra su cuenta de automatización.
2. Haga clic en hello **Runbooks** icono tooopen Hola lista de runbooks.
3. Haga clic en el botón **Examinar galería** .
   
    ![Botón Examinar galería](media/automation-runbook-gallery/browse-gallery-button.png)
4. Busque el elemento de la Galería de Hola que desee y seleccione tooview sus detalles.
   
    ![Examinar galería](media/automation-runbook-gallery/browse-gallery.png)
5. Haga clic en **proyecto de código fuente de vista** tooview elemento Hola Hola [centro de scripts de TechNet](http://gallery.technet.microsoft.com/).
6. tooimport un elemento, haga clic en ella tooview sus detalles y, a continuación, haga clic en hello **importación** botón.
   
    ![Botón Importar](media/automation-runbook-gallery/gallery-item-detail.png)
7. Opcionalmente, cambiar nombre de Hola de runbook de hello y, a continuación, haga clic en **Aceptar** tooimport Hola runbook.
8. Hola runbook aparecerá en hello **Runbooks** pestaña Hola cuenta de automatización.

### <a name="adding-a-runbook-toohello-runbook-gallery"></a>Agregar una galería de runbooks runbook toohello
Microsoft le anima tooadd runbooks toohello Galería de runbooks que cree que sería útil tooother clientes.  Puede agregar un runbook por [cargarlo toohello centro de scripts de](http://gallery.technet.microsoft.com/site/upload) teniendo en hello cuenta detalles siguientes.

* Debe especificar *Windows Azure* para hello **categoría** y *automatización* para hello **subcategoría** de muestra de Hola runbook toobe en el Asistente de Hola.  
* carga de Hello debe ser un único archivo. ps1 o .graphrunbook.  Si runbook Hola requiere los módulos, los runbooks secundarios o los activos, a continuación, debe indicarlos en la descripción de hello del envío de Hola y en la sección de comentarios de Hola de runbook de Hola.  Si tiene un escenario que requiere varios runbooks, a continuación, cargar cada uno de ellos por separado y nombres Hola de lista de hello relacionados con runbooks en cada uno de sus descripciones. Asegúrese de que usa Hola mismo etiquetas para que se mostrarán en hello misma categoría. Un usuario tenga tooread Hola descripción tooknow que otros runbooks son necesarios Hola escenario toowork.
* Agregar etiquetas de Hola "GraphicalPS" Si va a publicar un **runbook gráfico** (no en un flujo de trabajo gráfico). 
* Insertar fragmento de código de un PowerShell o el flujo de trabajo de PowerShell en hello descripción utilizando **Insertar sección de código** icono.
* Hello resumen para la carga de Hola se mostrará en hello que Galería de runbooks provoca por lo que debe proporcionar información detallada que le ayudará a un usuario para identificar la funcionalidad de Hola de runbook de Hola.
* Debe asignar una toothree de hello después carga toohello de etiquetas.  Hola runbook se mostrarán en el Asistente de hello en categorías de Hola que coincidan con sus etiquetas.  Asistente de hello omitirá las etiquetas no estén en esta lista. Si no se especifica ninguna etiqueta coincidente, será Hola runbook aparecen en hello otra categoría.
  
  * Backup
  * Administración de la capacidad
  * Control de cambios
  * Cumplimiento normativo
  * Desarrollo y entornos de prueba
  * Recuperación ante desastres
  * Supervisión
  * Aplicación de revisiones
  * Aprovisionamiento
  * Corrección
  * Administración del ciclo de vida de VM
* La automatización actualiza Hola Galería cada hora, por lo que no verá sus contribuciones inmediatamente.

## <a name="modules-in-powershell-gallery"></a>Módulos en la Galería de PowerShell
Módulos de PowerShell contienen cmdlets que puede usar en sus runbooks y módulos existentes que se pueden instalar en automatización de Azure están disponibles en hello [Galería de PowerShell](http://www.powershellgallery.com).  También puede iniciar esta galería de hello portal de Azure e instalarlos directamente en la automatización de Azure, o se puede descargarlas e instalarlas manualmente.  No se puede instalar módulos de hello directamente desde el portal de Azure clásico hello, pero puede descargarlos instalarlos como lo haría con cualquier otro módulo.

### <a name="tooimport-a-module-from-hello-automation-module-gallery-with-hello-azure-portal"></a>tooimport un módulo de hello Galería de módulos de automatización con hello portal de Azure
1. Hola Portal de Azure, abra su cuenta de automatización.
2. Haga clic en hello **activos** icono tooopen Hola lista de activos.
3. Haga clic en hello **módulos** icono tooopen Hola lista de módulos.
4. Haga clic en hello **explorar la galería** hoja de galería hello y el botón Examinar se inicia.
   
    ![Galería de módulos](media/automation-runbook-gallery/modules-blade.png) <br>
5. Una vez que haya iniciado la hoja de hello examinar la galería, puede buscar por hello siguientes campos:
   
   * Nombre de módulo
   * Etiquetas
   * Autor
   * Nombre de cmdlet/recurso de DSC
6. Localice un módulo que le interesa y seleccione tooview sus detalles.  
   Al agrupar los datos en un módulo específico, puede ver más información sobre el módulo de hello, incluyendo un toohello de espera de vínculo Galería de PowerShell, las dependencias de necesarias y todos los cmdlets de Hola o los recursos de DSC que Hola módulo contiene.
   
    ![Detalles del módulo de PowerShell](media/automation-runbook-gallery/gallery-item-details-blade.png) <br>
7. módulo de hello tooinstall directamente en la automatización de Azure, haga clic en hello **importación** botón.
   
    ![Botón de importación de módulo](media/automation-runbook-gallery/module-import-button.png)
8. Al hacer clic en botón Importar de hello, verá el nombre de módulo de Hola que va tooimport. Si se instalan todas las dependencias de hello, Hola **Aceptar** botón estará activo. Si no tiene dependencias, debe tooimport los para poder importar este módulo.
9. Haga clic en **Aceptar** tooimport Hola módulo y hoja de módulo de Hola se iniciarán. Cuando una cuenta de tooyour de módulo se importa en automatización de Azure, extrae metadatos sobre el módulo de Hola y Hola cmdlets.
   
    ![Hoja de importación de módulo](media/automation-runbook-gallery/module-import-blade.png)
   
    Puesto que cada actividad necesita toobe extraído, esto puede tardar unos minutos.
10. Recibirá una notificación se va a implementar ese módulo hello y una notificación cuando se ha completado.
11. Una vez importado el módulo de hello, verá actividades disponibles hello y puede usar sus recursos en sus runbooks y la configuración de estado deseado.

## <a name="requesting-a-runbook-or-module"></a>Solicitud de un runbook o módulo
Puede enviar solicitudes demasiado[User Voice](https://feedback.azure.com/forums/246290-azure-automation/).  Si necesita ayuda para escribir un runbook o tiene alguna pregunta acerca de PowerShell, publique una pregunta tooour [foro](http://social.msdn.microsoft.com/Forums/windowsazure/en-US/home?forum=azureautomation&filter=alltypes&sort=lastpostdesc).

## <a name="next-steps"></a>Pasos siguientes
* tooget a trabajar con runbooks, vea [crear o importar un runbook en automatización de Azure](automation-creating-importing-runbook.md)
* diferencias de hello toounderstand entre PowerShell y flujo de trabajo de PowerShell a runbooks, vea [flujo de trabajo de PowerShell de aprendizaje](automation-powershell-workflow.md)

