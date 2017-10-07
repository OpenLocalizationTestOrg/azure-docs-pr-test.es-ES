---
title: "aaaSource integración del Control de automatización de Azure | Documentos de Microsoft"
description: "En este artículo se describe la integración del control de código fuente con GitHub en Automatización de Azure."
services: automation
documentationcenter: 
author: mgoedtel
manager: jwhit
editor: tysonn
ms.assetid: 224d7375-9887-44dd-b137-06ffe396a4b4
ms.service: automation
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 11/21/2016
ms.author: magoedte;sngun
ms.openlocfilehash: 6ceee1de8065fafe85a13bbd7f585e74dbc96b47
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="source-control-integration-in-azure-automation"></a>Integración del control de código fuente en Automatización de Azure
Integración del control de código fuente permite tooassociate runbooks en el repositorio de control de código fuente de GitHub de automatización de la cuenta tooa. Control de código fuente permite tooeasily colaborar con su equipo, seguimiento de cambios y deshacer versiones tooearlier de sus runbooks. Por ejemplo, control de código fuente permite toosync diferentes bifurcaciones de control de código fuente tooyour desarrollo, prueba o producción cuentas de automatización, lo que toopromote fácil código que se ha probado en la producción de tooyour de entorno de desarrollo automatización cuenta.

Control de código fuente permite toopush código de control de automatización de Azure toosource o extraer los runbooks de control de código fuente tooAzure automatización. Este artículo describe cómo controlar tooset el origen en el entorno de automatización de Azure. Se iniciará mediante la configuración de automatización de Azure tooaccess el repositorio de GitHub y guiará a través de diferentes operaciones que se pueden realizar mediante la integración del control de código fuente. 

> [!NOTE]
> El control de código fuente admite la extracción e inserción de [runbooks del flujo de trabajo de PowerShell](automation-runbook-types.md#powershell-workflow-runbooks) y de [runbooks de PowerShell](automation-runbook-types.md#powershell-runbooks). Los [runbooks gráficos](automation-runbook-types.md#graphical-runbooks) aún no se admiten.<br><br>
> 
> 

Hay dos pasos sencillos tooconfigure requiere control de código fuente su cuenta de automatización y solo uno si ya tiene una cuenta de GitHub. Son las siguientes:

## <a name="step-1--create-a-github-repository"></a>Paso 1: Creación de un repositorio de GitHub
Si ya tiene una cuenta de GitHub y un repositorio que desee toolink tooAzure automatización, a continuación, tooyour de inicio de sesión existente de la cuenta y comenzar desde el paso 2 a continuación. En caso contrario, vaya demasiado[GitHub](https://github.com/), registrarse para una cuenta nueva y [crear un nuevo repositorio](https://help.github.com/articles/create-a-repo/).

## <a name="step-2--set-up-source-control-in-azure-automation"></a>Paso 2: Configuración del control de código fuente en Automatización de Azure
1. En la hoja de la cuenta de automatización de Hola Hola portal de Azure, haga clic en **establecer Control de código fuente.** 
   
    ![Configuración del control de código fuente](media/automation-source-control-integration/automation_01_SetUpSourceControl.png)
2. Hola **Control de código fuente** se abre la hoja, donde puede configurar los detalles de la cuenta de GitHub. Abajo aparece la lista de Hola de tooconfigure de parámetros:  
   
   | **Parámetro** | **Descripción** |
   |:--- |:--- |
   | Elegir origen |Seleccione origen Hola. Actualmente, solo se admite **GitHub** . |
   | Autorización |Haga clic en hello **Authorize** repositorio de GitHub de tooyour de acceso de botón toogrant automatización de Azure. Si ya ha iniciado sesión en tooyour cuenta de GitHub en una ventana diferente, Hola se utilizan las credenciales de dicha cuenta. Una vez que la autorización es correcta, hoja de hello mostrará el nombre de usuario de GitHub en **propiedad autorización**. |
   | Selección del repositorio |Seleccione un repositorio de GitHub de lista de Hola de repositorios disponibles. |
   | Elegir rama |Seleccione una rama de lista de Hola de ramas disponibles. Hola solo **maestro** rama se muestra si no ha creado las bifurcaciones. |
   | Ruta de acceso de la carpeta de runbook |ruta de acceso de carpeta de runbooks de Hello especifica la ruta de acceso de hello en el repositorio de GitHub de Hola desde la que desea toopush o extraer el código. Debe especificarse en formato de hello **/nombreCarpeta/nombresubcarpeta**. Solo runbooks en la ruta de acceso de carpeta de runbooks de hello estarán sincronizado tooyour cuenta de automatización. Le runbooks en las subcarpetas de Hola de ruta de acceso de carpeta de runbooks de hello **no** se sincronizará. Use  **/**  toosync todos Hola runbooks en el repositorio de Hola. |
3. Por ejemplo, si tiene un repositorio denominado **scriptsDePowerShell** que contiene una carpeta denominada **carpetaRaíz**, que a su vez contiene una carpeta denominada **subCarpeta**. Puede usar Hola después cadenas toosync cada nivel de carpeta:
   
   1. runbooks de toosync de **repositorio**, es la ruta de acceso de carpeta de runbooks*/*
   2. runbooks de toosync de **RootFolder**, ruta de acceso de carpeta de runbook es */RootFolder*
   3. runbooks de toosync de **subcarpeta**, es la ruta de acceso de carpeta de runbooks */RootFolder/subcarpeta*.
4. Después de configurar los parámetros de hello, se muestran en hello **hoja establecer Control de código fuente.**  
   
    ![Hoja Configurar](media/automation-source-control-integration/automation_02_SourceControlConfigure.png)
5. Al hacer clic en Aceptar, la integración del control de código fuente estará configurada para la cuenta de Automatización y debe actualizarse con la información de GitHub. Ahora puede hacer clic en esta parte tooview todos del control de código fuente historial de trabajos de sincronización.  
   
    ![Valores de repositorio](media/automation-source-control-integration/automation_03_RepoValues.png)
6. Después de configurar el control de código fuente, hello siguientes recursos de automatización se creará en la cuenta de automatización:  
   Se crean dos [recursos de variables](automation-variables.md).  
   
   * variable de Hello **Microsoft.Azure.Automation.SourceControl.Connection** contiene valores de hello de cadena de conexión de hello, tal y como se muestra a continuación.  
     
     | **Parámetro** | **Valor** |
     |:--- |:--- |
     | Nombre |Microsoft.Azure.Automation.SourceControl.Connection |
     | Tipo |String |
     | Valor |{"Branch":\<*nombreDeRama*>,"RunbookFolderPath":\<*rutaDeCarpetaDeRunbook*>,"ProviderType":\<*tiene un valor de 1 para GitHub*>,"Repository":\<*nombreDelRepositorio*>,"Username":\<*nombreDe UsuarioDeGitHub*>} |

    * variable de Hello **Microsoft.Azure.Automation.SourceControl.OAuthToken**, contiene el valor cifrado seguro Hola de su OAuthToken.  

    |**Parámetro**            |**Valor** |
    |:---|:---|
    | Nombre  | Microsoft.Azure.Automation.SourceControl.OAuthToken |
    | Tipo | Unknown(Encrypted) |
    | Valor | <*OAuthToken cifrado*> |  

    ![variables](media/automation-source-control-integration/automation_04_Variables.png)  

    * **Control de código fuente de automatización** se agrega como una cuenta de GitHub de tooyour aplicaciones autorizados. aplicación de hello tooview: desde la página principal de GitHub, navegue tooyour **perfil** > **configuración** > **aplicaciones**. Esta aplicación permite a automatización de Azure toosync su tooan de repositorio de GitHub cuenta de automatización.  

    ![Aplicación Git](media/automation-source-control-integration/automation_05_GitApplication.png)


## <a name="using-source-control-in-automation"></a>Uso del control de código fuente en Automatización
### <a name="check-in-a-runbook-from-azure-automation-toosource-control"></a>En el repositorio de control de automatización de Azure toosource un runbook
En el repositorio de runbook permite cambios de hello toopush realizados tooa runbook en automatización de Azure en el repositorio de control de código fuente. A continuación se muestran los pasos de hello toocheck en un runbook:

1. Desde su cuenta de Automation, [cree un nuevo runbook textual](automation-first-runbook-textual.md) o [edite un runbook textual existente](automation-edit-textual-runbook.md). Este runbook puede ser un flujo de trabajo de PowerShell o un runbook de scripts de PowerShell.  
2. Después de editar el runbook, guardarlo y haga clic en **en el repositorio** de hello **editar** hoja.  
   
    ![Botón Proteger](media/automation-source-control-integration/automation_06_CheckinButton.png)

     > [!NOTE] 
     > En el repositorio de automatización de Azure, sobrescribirá el código de hello que existen actualmente en el control de código fuente. Hola instrucción equivalente de línea de comandos de Git en toocheck es **agregar git + confirmación de git + git push**  

1. Al hacer clic en **en el repositorio**, aparecerá un mensaje de confirmación, haga clic en Sí toocontinue.  
   
    ![Mensaje de protección](media/automation-source-control-integration/automation_07_CheckinMessage.png)
2. Inicia Hola runbook de control de código fuente en el repositorio: **MicrosoftAzureAutomationAccountToGitHubV1 de sincronización**. Este runbook conecta tooGitHub e inserta los cambios del repositorio de tooyour de automatización de Azure. Hola tooview en el repositorio historial de trabajos, vuelva atrás toohello **integración del Control de código fuente** ficha y haga clic en la hoja de sincronización de repositorio de tooopen Hola. Esta hoja muestra todos los trabajos de control de código fuente.  Seleccione Hola trabajo que desee tooview y haga clic en detalles de hello tooview.  
   
    ![Runbook de protección](media/automation-source-control-integration/automation_08_CheckinRunbook.png)
   
   > [!NOTE]
   > Los runbooks de control de código fuente son runbooks de Automatización especiales que no se pueden ver ni editar. Aunque no se muestran en la lista de runbooks, verá que se muestran los trabajos de sincronización en la lista de trabajos.
   > 
   > 
3. nombre de Hola de runbook de hello modificado se envía como un parámetro de entrada toohello en el repositorio runbook. También puede [ver detalles del trabajo hello](automation-runbook-execution.md#viewing-job-status-from-the-azure-portal) expandiendo runbook en **repositorio sincronización** hoja.  
   
    ![Entrada de protección](media/automation-source-control-integration/automation_09_CheckinInput.png)
4. Actualizar el repositorio de GitHub cuando completa el trabajo Hola cambios de hello tooview.  Debería haber una confirmación en el repositorio con un mensaje de confirmación: **Updated *nombre de Runbook* en automatización de Azure.**  

### <a name="sync-runbooks-from-source-control-tooazure-automation"></a>Runbooks de sincronización de tooAzure de control de código fuente automatización
botón de sincronización de Hello en la hoja de sincronización de repositorio de hello permite toopull todos Hola runbooks en la ruta de acceso de carpeta de hello runbooks de su cuenta de automatización de tooyour de repositorio. Hello mismo repositorio puede ser toomore sincronizado que una cuenta de automatización. A continuación se muestran Hola pasos toosync un runbook:

1. En hello cuenta de automatización que configurar control de código fuente, abra hello **hoja de sincronización de integración/repositorio de Control de código fuente** y haga clic en **sincronización** , a continuación, se le pedirá una confirmación el mensaje, haga clic en **Sí** toocontinue.  
   
    ![Botón Sincronizar](media/automation-source-control-integration/automation_10_SyncButtonwithMessage.png)
2. Hola runbook inicia la sincronización: **MicrosoftAzureAutomationAccountFromGitHubV1 de sincronización**. Este runbook conecta tooGitHub y extrae Hola cambios de la automatización de tooAzure de repositorio. Debería ver un nuevo trabajo en hello **repositorio sincronización** hoja para esta acción. tooview obtener más información sobre el trabajo de sincronización de hello, haga clic en la hoja de detalles de trabajo de tooopen Hola.  
   
    ![Runbook de sincronización](media/automation-source-control-integration/automation_11_SyncRunbook.png)

    > [!NOTE] 
    > Una sincronización de control de código fuente sobrescribe la versión de borrador de Hola Hola runbooks que existen actualmente en su cuenta de automatización para **todos los** runbooks que están actualmente en el control de origen. Hola Git toosync de instrucción de línea de comandos equivalente es **extracción**


## <a name="troubleshooting-source-control-problems"></a>Solución de problemas de control de código fuente
Si hay algún error en un trabajo en el repositorio o la sincronización, el estado del trabajo de hello debe suspenderse y puede ver más detalles sobre el error de hello en la hoja de trabajo de Hola.  Hola **todos los registros de** parte le mostrará todos los Hola secuencias de PowerShell asociadas con ese trabajo. Esto proporcionará que detalles Hola había toohelp arregle cualquier problema con la protección o la sincronización. También le mostrará hello secuencia de acciones que se produjeron durante la sincronización o comprobación de un runbook.  

![Imagen de todos los registros](media/automation-source-control-integration/automation_13_AllLogs.png)

## <a name="disconnecting-source-control"></a>Desconexión del control de código fuente
toodisconnect de su cuenta de GitHub, abrir la hoja de sincronización de repositorio de Hola y haga clic en **desconexión**. Una vez que se desconecta el control de código fuente, runbooks que se han sincronizado anteriormente seguirá estando en su cuenta de automatización, pero no se habilitará la hoja de sincronización de repositorio de Hola.  

  ![Botón Desconectar](media/automation-source-control-integration/automation_12_Disconnect.png)

## <a name="next-steps"></a>Pasos siguientes
Para obtener más información acerca de la integración del control de código fuente, vea Hola recursos siguientes:  

* [Automatización de Azure: integración del control de código fuente en Automatización de Azure](https://azure.microsoft.com/blog/azure-automation-source-control-13/)  
* [Vote por su sistema de control de código fuente favorito](https://www.surveymonkey.com/r/?sm=2dVjdcrCPFdT0dFFI8nUdQ%3d%3d)  
* [Automatización de Azure: integración del control de código fuente de runbook mediante Visual Studio Team Services](https://azure.microsoft.com/blog/azure-automation-integrating-runbook-source-control-using-visual-studio-online/)  

