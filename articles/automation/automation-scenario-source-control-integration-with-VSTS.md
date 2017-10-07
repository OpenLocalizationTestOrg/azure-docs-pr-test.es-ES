---
title: "aaaIntegrate automatización de Azure con control de código fuente de Visual Studio Team Services | Documentos de Microsoft"
description: "Escenario que le lleva por la configuración de la integración con una cuenta de Azure Automation y el control de código fuente de Visual Studio Team Services."
services: automation
documentationcenter: 
author: eamono
manager: 
editor: 
keywords: "azure powershell, VSTS, control de código fuente, automation"
ms.assetid: a43b395a-e740-41a3-ae62-40eac9d0ec00
ms.service: automation
ms.workload: infrastructure-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/24/2017
ms.openlocfilehash: 8f6faa596a5ad1f8b72e820ca320b3e103d83579
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="azure-automation-scenario---automation-source-control-integration-with-visual-studio-team-services"></a>Escenario de Azure Automation: integración del control del código fuente de Automation con Visual Studio Team Services

En este escenario, tiene un proyecto de Visual Studio Team Services que está usando toomanage runbooks de automatización de Azure o las configuraciones de DSC bajo control de código fuente.
Este artículo se describe cómo toointegrate VSTS con su entorno de automatización de Azure, por lo que ocurre que la integración continua para cada protección.

## <a name="getting-hello-scenario"></a>Introducción al escenario de Hola

Este escenario consta de dos runbooks de PowerShell que se pueden importar directamente desde hello [Galería de runbooks](automation-runbook-gallery.md) en Hola portal de Azure o descargar desde hello [Galería de PowerShell](https://www.powershellgallery.com).

### <a name="runbooks"></a>Runbooks

Runbook | Descripción| 
--------|------------|
Sync-VSTS | Importa runbooks o configuraciones de control de código fuente de VSTS cuando se realiza una inserción en el repositorio. Si ejecuta manualmente, importará y publicar todos los runbooks o configuraciones en hello cuenta de automatización.| 
Sync-VSTSGit | Importa runbooks o configuraciones de VSTS bajo control de código fuente de GIT cuando se realiza una inserción en el repositorio. Si ejecuta manualmente, importará y publicar todos los runbooks o configuraciones en hello cuenta de automatización.|

### <a name="variables"></a>variables

Variable | Descripción|
-----------|------------|
VSToken | Activo de variable seguro creará que contiene el token de acceso personal de VSTS Hola. Aprenderá cómo toocreate un personal VSTS acceso token en hello [página de autenticación de VSTS](https://www.visualstudio.com/en-us/docs/integrate/get-started/auth/overview). 
## <a name="installing-and-configuring-this-scenario"></a>Instalación y configuración de este escenario

Crear un [token de acceso personal](https://www.visualstudio.com/en-us/docs/integrate/get-started/auth/overview) en VSTS que va a usar toosync Hola runbooks o configuraciones en su cuenta de automatización.

![](media/automation-scenario-source-control-integration-with-VSTS/VSTSPersonalToken.png) 

Crear un [variable $secure](automation-variables.md) en su Hola de toohold de automatización de la cuenta de acceso personal token para que pueda autenticar Hola runbook tooVSTS y sincronización runbooks Hola o configuraciones en hello cuenta de automatización. Puede llamarla VSToken. 

![](media/automation-scenario-source-control-integration-with-VSTS/VSTSTokenVariable.png)

Importar runbook de Hola que sincronizará los runbooks o configuraciones en la cuenta de automatización de Hola. Puede usar hello [runbook de ejemplo VSTS](https://www.powershellgallery.com/packages/Sync-VSTS/1.0/DisplayScript) o hello [VSTS con runbook de ejemplo Git] (https://www.powershellgallery.com/packages/Sync-VSTSGit/1.0/DisplayScript) de hello PowerShellGallery.com dependiendo de si usas VSTS VSTS con Git o control de origen e implementar tooyour cuenta de automatización.

![](media/automation-scenario-source-control-integration-with-VSTS/VSTSPowerShellGallery.png)

Ahora puede [publicar](automation-creating-importing-runbook.md#publishing-a-runbook) este runbook y así crear un webhook. 
![](media/automation-scenario-source-control-integration-with-VSTS/VSTSPublishRunbook.png)

Crear un [webhook](automation-webhooks.md) para este runbook VSTS de sincronización y el relleno en parámetros de hello tal y como se muestra a continuación. Asegúrese de que copiar dirección url del webhook hello, ya que será necesario para un enlace de servicio en VSTS. Hola VSAccessTokenVariableName es el nombre de hello (VSToken) de variable $secure Hola que creó el token de acceso personal de hello toohold anterior. 

Integración con VSTS (sincronización VSTS.ps1) tardará Hola parámetros siguientes.
### <a name="sync-vsts-parameters"></a>Parámetros de Sync-VSTS

Parámetro | Descripción| 
--------|------------|
WebhookData | Contendrá información de registro de hello enviada desde el enlace de servicio VSTS Hola. Este parámetro se debe dejar en blanco.| 
ResourceGroup | Este es el nombre de Hola Hola del grupo de recursos que la cuenta de automatización de hello es en.|
AutomationAccountName | nombre de Hola de cuenta de automatización de Hola que se sincronizará con VSTS.|
VSFolder | El nombre de carpeta de hello en VSTS donde existen Hola runbooks y las configuraciones.|
VSAccount | nombre de Hola de hello cuenta de Visual Studio Team Services.| 
VSAccessTokenVariableName | nombre de Hola de variable seguros de hello (VSToken) que contiene el token de acceso personal de VSTS Hola.| 


![](media/automation-scenario-source-control-integration-with-VSTS/VSTSWebhook.png)

Si usas VSTS con GIT (sincronización VSTSGit.ps1) tardará Hola parámetros siguientes.

Parámetro | Descripción|
--------|------------|
WebhookData | Contendrá información de registro de hello enviada desde el enlace de servicio VSTS Hola. Este parámetro se debe dejar en blanco.| ResourceGroup | Este nombre de Hola Hola del grupo de recursos que la cuenta de automatización de hello es en.|
AutomationAccountName | nombre de Hola de cuenta de automatización de Hola que se sincronizará con VSTS.|
VSAccount | nombre de Hola de hello cuenta de Visual Studio Team Services.|
VSProject | nombre de Hello del proyecto de hello en VSTS donde existen Hola runbooks y las configuraciones.|
GitRepo | nombre de Hello del repositorio de Git Hola.|
GitBranch | nombre de Hola de bifurcación de hello en el repositorio de Git de VSTS.|
Carpeta | nombre de Hola de carpeta de hello en VSTS Git bifurcación.|
VSAccessTokenVariableName | nombre de Hola de variable seguros de hello (VSToken) que contiene el token de acceso personal de VSTS Hola.|

![](media/automation-scenario-source-control-integration-with-VSTS/VSTSGitWebhook.png)

Crear un enlace de servicio en VSTS para las carpetas de toohello protecciones que desencadena esta webhook en el repositorio de código. Seleccione enlaces Web como Hola servicio toointegrate con cuando se crea una nueva suscripción. Puede aprender más sobre los enlaces de servicio en la [documentación de enlaces de servicio de VSTS](https://www.visualstudio.com/en-us/docs/marketplace/integrate/service-hooks/get-started).
![](media/automation-scenario-source-control-integration-with-VSTS/VSTSServiceHook.png)

Debe ahora ser capaz de toodo todas las protecciones de los runbooks y las configuraciones en VSTS y hacer que éstas automáticamente sincronizar tenía en su cuenta de automatización.

![](media/automation-scenario-source-control-integration-with-VSTS/VSTSSyncRunbookOutput.png)

Si ejecuta este runbook manualmente sin que se desencadena por VSTS, puede dejar vacío parámetro webhookdata de hello y realizará una sincronización completa de carpeta VSTS Hola especificada.

Si desea que el escenario de hello toouninstall, quite el enlace de servicio de Hola de VSTS, elimine runbook Hola y Hola VSToken variable.
