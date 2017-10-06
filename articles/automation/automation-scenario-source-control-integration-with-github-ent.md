---
title: "Integración de Control de código fuente de automatización con GitHub Enterprise aaaAzure | Documentos de Microsoft"
description: "Describe los detalles de Hola de cómo la integración de tooconfigure con GitHub Enterprise para control de código fuente de runbooks de automatización."
services: automation
documentationCenter: 
authors: mgoedtel
manager: jwhit
editor: 
ms.assetid: e01d817c-7d38-421c-adf5-647a4b526eb4
ms.service: automation
ms.workload: infrastructure-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/26/2017
ms.author: magoedte
ms.openlocfilehash: 915d36ccabb72fdee1dba663049a0b331249cd73
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="azure-automation-scenario---automation-source-control-integration-with-github-enterprise"></a>Escenario de Azure Automation: integración del control del código fuente de Automation con GitHub Enterprise

Automatización actualmente admite la integración de control de código fuente, lo que permite tooassociate runbooks en el repositorio de control de código fuente de GitHub de automatización de la cuenta tooa.  Sin embargo, los clientes que hayan implementado [GitHub Enterprise](https://enterprise.github.com/home) toosupport prácticas de sus DevOps, también desea toouse, ciclo de vida de toomanage Hola de runbooks que desarrolló tooautomate los procesos empresariales y administración de servicios operaciones.  

En este escenario, tiene un equipo de Windows en el centro de datos configurado como un Hybrid Runbook Worker con módulos de Azure Resource Manager hello y las herramientas de Git instaladas.  máquina de trabajador híbrido de Hello tiene un clon del repositorio de Git local Hola.  Cuando se ejecuta runbook hello en hybrid worker de hello, Hola Git directory se sincroniza y contenido del archivo de runbook de Hola se importa en hello cuenta de automatización.

Este artículo se describe cómo tooset esta configuración en su entorno de automatización de Azure. Comenzamos mediante la configuración de automatización con las credenciales de seguridad de Hola, runbooks necesario toosupport este escenario y la implementación de un Hybrid Runbook Worker en los datos toorun Hola runbooks del centro y tener acceso a su toosynchronize de repositorio de GitHub Enterprise runbooks con su cuenta de automatización.  


## <a name="getting-hello-scenario"></a>Introducción al escenario de Hola

Este escenario consta de dos runbooks de PowerShell que se pueden importar directamente desde hello [Galería de runbooks](automation-runbook-gallery.md) en Hola portal de Azure o descargar desde hello [Galería de PowerShell](https://www.powershellgallery.com).

### <a name="runbooks"></a>Runbooks

Runbook | Descripción| 
--------|------------|
Export-RunAsCertificateToHybridWorker | Runbook exporta un certificado de ejecución de un trabajador de automatización de la cuenta tooa híbrido para que runbooks en el trabajo de hello pueda autenticarse con Azure en orden tooimport runbooks en hello cuenta de automatización.| 
Sync-LocalGitFolderToAutomationAccount | Runbook sincronizaciones Hola carpeta Git local en equipo híbrido de hello y, a continuación, importación archivos de runbook de hello (*.ps1) en la cuenta de automatización de Hola.|

### <a name="credentials"></a>Credenciales

Credential: | Descripción|
-----------|------------|
GitHRWCredential | Activo de credencial se crea el nombre de usuario de toocontain hello y una contraseña para un usuario con toohello hybrid worker de permisos.|

## <a name="installing-and-configuring-this-scenario"></a>Instalación y configuración de este escenario

### <a name="prerequisites"></a>Requisitos previos

1. Hola LocalGitFolderToAutomationAccount sincronización runbook autentica mediante hello [cuenta de identificación de Azure](automation-sec-configure-azure-runas-account.md). 

2. También es necesario un área de trabajo de Microsoft Operations Management Suite (OMS) con hello solución de automatización de Azure habilitada y configurada.  Si no tiene uno que está asociado con hello automatización de la cuenta usada tooinstall y configurar este escenario, se crea y se configuran automáticamente cuando se ejecuta hello **OnPremiseHybridWorker.ps1 New** script desde híbrida Hola trabajo de runbook.        

    > [!NOTE]
    > Actualmente hello siguientes regiones solo admiten la automatización de la integración con OMS - **sudeste de Australia**, **UU 2**, **sudeste de Asia**, y **oeste Europa**. 

3. Un equipo que puede actuar como un Hybrid Runbook Worker dedicado que hospedará también software de GitHub de Hola y mantener archivos de runbook de hello (*runbook*. ps1) en un directorio de origen en hello toosynchronize de sistema de archivos entre GitHub y el Cuenta de automatización.

### <a name="import-and-publish-hello-runbooks"></a>Importar y publicar runbooks Hola

Hola tooimport *exportación RunAsCertificateToHybridWorker* y *LocalGitFolderToAutomationAccount sincronización* runbooks desde Hola Galería de runbooks de su cuenta de automatización en hello portal de Azure, Siga los procedimientos de hello en [importar Runbook de hello Galería de runbooks](automation-runbook-gallery.md#to-import-a-runbook-from-the-runbook-gallery-with-the-azure-portal). Publicar Hola runbooks después de que se han importado correctamente en su cuenta de automatización.

### <a name="deploy-and-configure-hybrid-runbook-worker"></a>Implementación y configuración de Hybrid Runbook Worker

Si no tiene un Runbook Worker híbrido ya implementados en su centro de datos, debe revisar los requisitos de Hola y seguir los pasos de instalación automatizada de hello mediante el procedimiento de hello en [Azure Automation Hybrid Runbook Workers: automatizar la instalación Configuración y](automation-hybrid-runbook-worker.md#automated-deployment).  Una vez que haya instalado correctamente hybrid worker de hello en un equipo, realice Hola siguientes pasos toocomplete su toosupport configuración este escenario.

1. Sesión toohello hospedaje Hola Hybrid Runbook Worker función del equipo con una cuenta que tenga derechos administrativos locales y cree un directorio toohold Hola Git runbook los archivos.  Clon Hola interno Git toohello directorio del repositorio.
2. Si ya no tiene una cuenta de ejecución creada o si desea toocreate uno nuevo dedicada para este fin, desde el portal de Azure Hola desplácese tooAutomation cuentas, seleccione su cuenta de automatización y crear un [activo de credencial](automation-credentials.md) que contiene Hola username y password para un usuario con permisos toohello híbrido de trabajo.  
3. Desde su cuenta de automatización, [editar runbook hello](automation-edit-textual-runbook.md)**exportación RunAsCertificateToHybridWorker** y modificar valor de Hola de variable de hello *$Password* con una fuerte contraseña.    Después de modificar el valor de hello, haga clic en **publicar** toohave Hola versión de borrador Hola runbook publicado. 
5. Iniciar runbook hello **exportación RunAsCertificateToHybridWorker**y en hello **iniciar Runbook** hoja, en la opción de hello **los parámetros de ejecución** seleccione opción hello **Hybrid Worker** y en el grupo Hola lista desplegable seleccione Hola Hybrid worker que creó anteriormente para este escenario.  

    Exporta un certificado toohello híbrido de trabajo para que runbooks en el trabajo de hello pueda autenticarse con Azure con hello ejecutar como conexión de orden toomanage recursos de Azure (en particular para este escenario: importar runbooks toohello cuenta de automatización).

4. Desde su cuenta de automatización, seleccione Hola grupo Hybrid worker que creó anteriormente y [especificar una cuenta de ejecución](automation-hrw-run-runbooks.md#runas-account) para el grupo Hybrid worker de Hola y activo de credencial de hello elegía simplemente o ya ha creado.  Esto garantiza que ese runbook de sincronización de hello puede ejecutar comandos de Git. 
5. Iniciar runbook hello **sincronización LocalGitFolderToAutomationAccount**, proporcionar siguiente Hola requiere valores de parámetro de entrada y en hello **iniciar Runbook** hoja, en la opción de hello **ejecutar configuración de** seleccione opción hello **Hybrid Worker** y en el grupo Hola lista desplegable seleccione Hola Hybrid worker que creó anteriormente para este escenario:
    * *ResourceGroup* : hello nombre de su grupo de recursos asociado con su cuenta de automatización
    * *AutomationAccountName* : hello nombre de la cuenta de automatización
    * *GitPath* : Hola carpeta local o de archivos en Hola donde se configura Git toopull cambios más recientes en Hybrid Runbook Worker

    Esto carpeta Git local de hello en el equipo de trabajo de hello híbrido de sincronización y, a continuación, importar archivos. ps1 de Hola de hello origen directory toohello cuenta de automatización.

    ![Start Sync-LocalGitFolderToAutomationAccount Runbook](media/automation-scenario-source-control-integration-with-github-ent/start-runbook-synclocalgitfoldertoautoacct.png)<br>

7. Ver los detalles de resumen de trabajo de runbook de hello seleccionándola de Hola **Runbooks** hoja en tu cuenta de automatización y, a continuación, seleccione Hola **trabajos** icono.  Confirme que se ha completado correctamente seleccionando hello **todos los registros de** icono y el flujo de registro detallado de hello revisado.  

## <a name="next-steps"></a>Pasos siguientes

-  tooknow más información acerca de los tipos de runbook, sus ventajas y limitaciones, consulte [tipos de runbook de automatización de Azure](automation-runbook-types.md)
-  Para obtener más información sobre la característica de compatibilidad con scripts de PowerShell, consulte [Announcing Native PowerShell Script Support in Azure Automation](https://azure.microsoft.com/blog/announcing-powershell-script-support-azure-automation-2/)
