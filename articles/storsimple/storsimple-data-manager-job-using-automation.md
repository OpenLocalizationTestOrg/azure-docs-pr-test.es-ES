---
title: "Automatización de Azure de aaaUse tootrigger un trabajo | Documentos de Microsoft"
description: "Obtenga información acerca de cómo toouse automatización de Azure para la activación de trabajos de administrador de datos de StorSimple (vista previa privada)"
services: storsimple
documentationcenter: NA
author: vidarmsft
manager: syadav
editor: 
ms.assetid: 
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 03/16/2017
ms.author: vidarmsft
ms.openlocfilehash: 0d9d6e5e6d52ed27ca759ed7e949b5f5dfd319c6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-automation-tootrigger-a-job-private-preview"></a>Usar la automatización de Azure tootrigger un trabajo (Private Preview)

En este artículo se describe cómo tootrigger de automatización de Azure toouse un trabajo del Administrador de datos de StorSimple.

## <a name="prerequisites"></a>Requisitos previos

Antes de comenzar, asegúrese de que dispone de:

*   Azure Powershell instalado. [Descarga de Azure PowerShell](https://azure.microsoft.com/documentation/articles/powershell-install-configure/).
*   Trabajo de transformación de datos Hola de configuración configuración tooinitialize (instrucciones tooobtain estas opciones se incluyen aquí).
*   Una definición del trabajo que se ha configurado correctamente en un recurso de datos híbridos de un grupo de recursos.
*   Descargar `DataTransformationApp.zip` [zip](https://github.com/Azure-Samples/storsimple-dotnet-data-manager-get-started/raw/master/Azure%20Automation%20For%20Data%20Manager/DataTransformationApp.zip) archivos del repositorio de github de Hola.
*   Descargar `Get-ConfigurationParams.ps1` [script](https://github.com/Azure-Samples/storsimple-dotnet-data-manager-get-started/blob/master/Azure%20Automation%20For%20Data%20Manager/Get-ConfigurationParams.ps1) del repositorio de github de Hola.
*   Descargar `Trigger-DataTransformation-Job.ps1` [script](https://github.com/Azure-Samples/storsimple-dotnet-data-manager-get-started/blob/master/Azure%20Automation%20For%20Data%20Manager/Trigger-DataTransformation-Job.ps1) del repositorio de github de Hola.

## <a name="step-by-step"></a>Paso a paso

### <a name="get-azure-active-directory-permissions-for-hello-automation-job-toorun-hello-job-definition"></a>Obtener permisos de Azure Active Directory de definición de trabajo de hello automatización trabajo toorun Hola

1. parámetros de configuración de hello tooretrieve para Active Directory, Hola lo siguiente:

    1. Abra Windows PowerShell en la máquina local. Asegúrese de que [Azure PowerShell](https://azure.microsoft.com/downloads/) esté instalado.
    1. Ejecute hello `Get-ConfigurationParams.ps1` script (en la carpeta de hello descargó anteriormente). Escriba el siguiente comando en la ventana de PowerShell de hello de Hola:

        ```
        .\Get-ConfigurationParams.ps1 -SubscriptionName "AzureSubscriptionName" -ActiveDirectoryKey "AnyRandomPassword" -AppName "ApplicationName"
         ```

        Hola ActiveDirectoryKey es una contraseña que utilizar más adelante. Escriba una contraseña de su elección. AppName puede ser cualquier cadena.

2. Este script genera Hola después valores que deben usarse durante la activación de runbook de automatización de Hola. Anote estos valores.

    - Id. de cliente
    - Id. de inquilino
    - Claves de Active Directory (igual que uno que Arri Hola)
    - Id. de suscripción

### <a name="set-up-hello-automation-account"></a>Configurar la cuenta de automatización de Hola

1. Inicie sesión en tooAzure y abra su cuenta de automatización.
2. Haga clic en **activos** icono tooopen Hola lista de activos.
3. Haga clic en **módulos** icono tooopen Hola lista de módulos.
4. Haga clic en **+ agregar un módulo** hello y botón hoja de módulo de complemento se inicia.

    ![Configuración de la cuenta de Automation](./media/storsimple-data-manager-job-using-automation/add-module1m.png)

5. Después de haber seleccionado hello `DataTransformationApp.zip` de archivos desde el equipo local, haga clic en **Aceptar** módulo de hello tooimport.

   Cuando una cuenta de tooyour de módulo se importa en automatización de Azure, extrae metadatos sobre el módulo de Hola. Esta operación puede demorar unos minutos.

   ![Configuración de la cuenta de Automation](./media/storsimple-data-manager-job-using-automation/add-module2m.png)

   

6. Recibirá una notificación se va a implementar ese módulo hello y otra notificación cuando se complete el proceso de Hola.  También puede comprobar el estado de hello **módulos** icono.

### <a name="tooimport-hello-runbook-that-triggers-hello-job-definition"></a>tooimport Hola runbook que desencadena la definición del trabajo Hola

1. Hola portal de Azure, abra su cuenta de automatización.
2. Haga clic en **Runbooks** icono tooopen Hola lista de runbooks.
3. Haga clic en **+ Agregar un runbook** y, luego, en **Importar un runbook existente**.

   ![Importar un runbook existente](./media/storsimple-data-manager-job-using-automation/import-a-runbook.png)

4. Haga clic en **archivo de Runbook** y Hola Seleccione archivo tooimport `Trigger-DataTransformation-Job.ps1`.
5. Haga clic en **crear** tooimport Hola runbook. Hola nuevo runbook aparecerá en lista de Hola de runbooks para hello cuenta de automatización.
7. Haga clic en el runbook **Trigger-DataTransformation-Job** y, luego, en **Editar**.
8. Haga clic en **Publicar** y, luego, en **Sí** cuando se pida confirmación.


### <a name="toorun-hello-runbook"></a>toorun Hola runbook:
1. Hola portal de Azure, abra su cuenta de automatización.
2. Haga clic en hello **Runbooks** icono tooopen Hola lista de runbooks.
3. Haga clic en **Trigger-DataTransformation-Job**.
4. Haga clic en **iniciar** toostart Hola runbook.

   ![Iniciar runbook](./media/storsimple-data-manager-job-using-automation/run-runbook1m.png)

5. Hola **iniciar runbook** hoja, escriba todos los parámetros de Hola. Haga clic en **Aceptar** trabajo de transformación de datos de toosubmit Hola.

   ![Iniciar runbook](./media/storsimple-data-manager-job-using-automation/run-runbook2m.png)


## <a name="next-steps"></a>Pasos siguientes

[Usar los datos de interfaz de usuario de administrador de datos de StorSimple tootransform](storsimple-data-manager-ui.md).
