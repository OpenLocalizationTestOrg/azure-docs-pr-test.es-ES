---
title: "Herramientas de Azure Data Lake: Ejecución y depuración locales de U-SQL con Visual Studio Code | Microsoft Docs"
description: "Obtenga información acerca de cómo depurar toouse Azure Data Lake Tools para Visual Studio Code toolocal local y de ejecución."
Keywords: "Ruta de acceso de toostorage de carga de VScode, Azure Data Lake Tools, ejecución, depuración Local, depuración Local, archivo de almacenamiento de información de vista previa, Local"
services: data-lake-analytics
documentationcenter: 
author: jejiang
manager: DJ
editor: jejiang
tags: azure-portal
ms.assetid: dc9b21d8-c5f4-4f77-bcbc-eff458f48de2
ms.service: data-lake-analytics
ms.devlang: 
ms.topic: article
ms.tgt_pltfrm: 
ms.workload: big-data
ms.date: 07/14/2017
ms.author: jejiang
ms.openlocfilehash: fb152f07fe8c4b03dde8fb8e62c7475eccda0578
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="u-sql-local-run-and-local-debug-with-visual-studio-code"></a>Ejecución y depuración locales de U-SQL con Visual Studio Code

## <a name="prerequisites"></a>Requisitos previos
Asegúrese de que tiene Hola siguiendo los requisitos previos en su lugar antes de iniciar estos procedimientos:
- Herramientas de Azure Data Lake para Visual Studio Code. Para instrucciones, consulte [Uso de Herramientas de Azure Data Lake para Visual Studio Code](data-lake-analytics-data-lake-tools-for-vscode.md).
- C# para código de Visual Studio (si quiere que la depuración local tooperform U-SQL).

   ![Instalación de C# en Herramientas de Data Lake para Visual Studio Code](./media/data-lake-analytics-data-lake-tools-for-vscode-local-run-and-debug/data-lake-tools-for-vscode-install-ms-vscodecsharp.png)
   
   > [!NOTE]
   > Hola ejecución local de SQL de U y características de depuración solo admiten actualmente los usuarios de Windows. 


## <a name="set-up-hello-u-sql-local-run-environment"></a>Configurar el entorno de ejecución local de hello U-SQL

1. Seleccione la paleta de comando de Ctrl + Mayús + P tooopen hello y, a continuación, escriba **ADL: Descargar LocalRun dependencia** paquetes de saludo toodownload.  

   ![Descargar los paquetes de dependencia de LocalRun ADL Hola](./media/data-lake-analytics-data-lake-tools-for-vscode-local-run-and-debug/DownloadLocalRun.png)

2. Busque los paquetes de dependencia de Hola de ruta de acceso de Hola se muestra en hello **salida** panel y, a continuación, instalar BuildTools y Win10SDK 10240. A continuación se muestra una ruta de acceso de ejemplo:  
`C:\Users\xxx\.vscode\extensions\usqlextpublisher.usql-vscode-ext-x.x.x\LocalRunDependency
`  
  ![Busque los paquetes de dependencia de Hola](./media/data-lake-analytics-data-lake-tools-for-vscode-local-run-and-debug/LocateDependencyPath.png)

   a. tooinstall BuildTools, siga las instrucciones del asistente Hola.   

  ![Instalación de BuildTools](./media/data-lake-analytics-data-lake-tools-for-vscode-local-run-and-debug/InstallBuildTools.png)

   b. tooinstall Win10SDK 10240, siga las instrucciones del Asistente de Hola.  

  ![Instalación de Win10SDK 10240](./media/data-lake-analytics-data-lake-tools-for-vscode-local-run-and-debug/InstallWin10SDK.png)

3. Configurar la variable de entorno de Hola. Conjunto hello **SCOPE_CPP_SDK** variable de entorno:  
`C:\Users\xxx\.vscode\extensions\usqlextpublisher.usql-vscode-ext-x.x.x\LocalRunDependency\CppSDK_3rdparty
`  
4. Reinicie Hola OS toomake seguro de que los valores de variable de entorno de hello surtan efecto.  

   ![Asegúrese de variable de entorno de hello SCOPE_CPP_SDK está instalado](./media/data-lake-analytics-data-lake-tools-for-vscode-local-run-and-debug/ConfigScopeCppSDk.png)

## <a name="start-hello-local-run-service-and-submit-hello-u-sql-job-tooa-local-account"></a>Iniciar el servicio de ejecución local de Hola y enviar la cuenta local de hello U-SQL trabajo tooa 
Para el usuario de la primera vez de hello, son hello toodownload solicitadas ADL: Descargar LocalRun dependencia paquetes si ya no están instalados.
1. Seleccione la paleta de comando de Ctrl + Mayús + P tooopen hello y, a continuación, escriba **ADL: iniciar el servicio ejecutar Local**.
2. Seleccione **Accept** tooaccept Hola términos de licencia de Software de Microsoft para hello primera vez. 

   ![Acepte los términos de licencia del Software de Microsoft de Hola](./media/data-lake-analytics-data-lake-tools-for-vscode-local-run-and-debug/AcceptEULA.png)   
3. Abre la consola de Hello cmd. Para los usuarios de la primera vez, deberá tooenter **3**y, a continuación, busque la ruta de acceso de carpeta local de Hola para los datos de entrada y salida. Para ver otras opciones, puede usar valores predeterminados de Hola. 

   ![Cmd de ejecución local de Data Lake Tools para Visual Studio Code](./media/data-lake-analytics-data-lake-tools-for-vscode-local-run-and-debug/data-lake-tools-for-vscode-local-run-cmd.png)
4. Seleccione Ctrl + Mayús + P tooopen Hola comando paleta, especifique **ADL: enviar trabajo**y, a continuación, seleccione **Local** toosubmit cuenta local de hello trabajo tooyour.

   ![Selección local de Herramientas de Data Lake para Visual Studio Code](./media/data-lake-analytics-data-lake-tools-for-vscode-local-run-and-debug/data-lake-tools-for-vscode-select-local.png)
5. Después de enviar el trabajo de hello, puede ver detalles de envío de Hola. Seleccione detalles de envío de hello tooview **jobUrl** en hello **salida** ventana. También puede ver el estado de envío del trabajo de Hola desde la consola de cmd de Hola. Escriba **7** en la consola de cmd de hello si desea que tooknow más detalles del trabajo.

   ![Salida d ejecución local de Herramientas de Data Lake para Visual Studio Code](./media/data-lake-analytics-data-lake-tools-for-vscode-local-run-and-debug/data-lake-tools-for-vscode-local-run-result.png)
   ![Herramientas de Data Lake para el estado de cmd de ejecución local de Visual Studio Code](./media/data-lake-analytics-data-lake-tools-for-vscode-local-run-and-debug/data-lake-tools-for-vscode-localrun-cmd-status.png) 


## <a name="start-a-local-debug-for-hello-u-sql-job"></a>Iniciar una depuración local de trabajo de SQL U Hola  
Para el usuario de la primera vez de hello, son hello toodownload solicitadas ADL: Descargar LocalRun dependencia paquetes si ya no están instalados.
  
1. Seleccione la paleta de comando de Ctrl + Mayús + P tooopen hello y, a continuación, escriba **ADL: iniciar el servicio ejecutar Local**. Abre la consola de Hello cmd. Asegúrese de que ese hello **DataRoot** se establece.
3. Establezca un punto de interrupción en el código subyacente de C#.
4. En el editor de secuencias de comandos de hello, seleccione la consola de comandos de Ctrl + Mayús + P tooopen hello y, a continuación, escriba **depurar Local** toostart su servicio en la depuración local.

![Resultado de la depuración local de Herramientas de Data Lake para Visual Studio Code](./media/data-lake-analytics-data-lake-tools-for-vscode-local-run-and-debug/data-lake-tools-for-vscode-local-debug-result.png)


## <a name="next-steps"></a>Pasos siguientes
- Para usar Herramientas de Azure Data Lake para Visual Studio, consulte [Use the Azure Data Lake Tools for Visual Studio Code](data-lake-analytics-data-lake-tools-for-vscode.md) (Uso de Herramientas de Azure Data Lake para Visual Studio Code).
- Para información detallada sobre cómo empezar a trabajar con Data Lake Analytics, consulte [Tutorial: Introducción a Azure Data Lake Analytics](data-lake-analytics-get-started-portal.md).
- Para información sobre Herramientas de Data Lake para Visual Studio, consulte [Tutorial: Desarrollo de scripts U-SQL mediante Herramientas de Data Lake para Visual Studio](data-lake-analytics-data-lake-tools-get-started.md).
- Para obtener información de hello en desarrollar ensamblados, vea [ensamblados desarrollar U-SQL para trabajos de análisis de Azure Data Lake](data-lake-analytics-u-sql-develop-assemblies.md).
