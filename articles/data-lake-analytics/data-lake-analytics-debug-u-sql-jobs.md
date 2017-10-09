---
title: trabajos de aaaDebug U-SQL | Documentos de Microsoft
description: "Obtenga información acerca de cómo toodebug U-SQL no pudo vértices con Visual Studio."
services: data-lake-analytics
documentationcenter: 
author: saveenr
manager: jhubbard
editor: cgronlun
ms.assetid: bcd0b01e-1755-4112-8e8a-a5cabdca4df2
ms.service: data-lake-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 09/02/2016
ms.author: saveenr
ms.openlocfilehash: 092bffa1a59ed91c5837402d0276447480b923fe
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="debug-user-defined-c-code-for-failed-u-sql-jobs"></a>Depuración de código C# definido por el usuario para trabajos de U-SQL con errores

U-SQL proporciona un modelo de extensibilidad con C#, por lo que puede escribir la funcionalidad de tooadd de código como un extractor personalizado o reductor. más información, consulte toolearn [Guía de programación de SQL U](https://docs.microsoft.com/en-us/azure/data-lake-analytics/data-lake-analytics-u-sql-programmability-guide#use-user-defined-functions-udf). En la práctica, puede que un código necesite depuración y los sistemas de macrodatos solo pueden proporcionar información limitada de depuración de tiempo de ejecución, como los archivos de registro.

Azure Data Lake Tools para Visual Studio incluye una característica denominada **no se pudo depurar vértices**, lo que le permite clonar un trabajo con error desde el equipo local tooyour de hello en la nube para la depuración. clon local Hola captura entorno de nube todo hello, incluidos los datos de entrada y el código de usuario.

Hello vídeo siguiente muestra no se pudo depurar vértices en Azure Data Lake Tools para Visual Studio.

> [!VIDEO https://e0d1.wpc.azureedge.net/80E0D1/OfficeMixProdMediaBlobStorage/asset-d3aeab42-6149-4ecc-b044-aa624901ab32/b0fc0373c8f94f1bb8cd39da1310adb8.mp4?sv=2012-02-12&sr=c&si=a91fad76-cfdd-4513-9668-483de39e739c&sig=K%2FR%2FdnIi9S6P%2FBlB3iLAEV5pYu6OJFBDlQy%2FQtZ7E7M%3D&se=2116-07-19T09:27:30Z&rscd=attachment%3B%20filename%3DDebugyourcustomcodeinUSQLADLA.mp4]
>

> [!NOTE]
> Visual Studio requiere Hola siguiendo dos actualizaciones si no están ya instalados: [Microsoft Visual C++ 2015 Redistributable Update 3](https://www.microsoft.com/en-us/download/details.aspx?id=53840) y [Universal en tiempo de ejecución de C para Windows](https://www.microsoft.com/download/details.aspx?id=50410).

## <a name="download-failed-vertex-toolocal-machine"></a>Error al descargar el vértice toolocal máquina

Al abrir un trabajo con error en Azure Data Lake Tools para Visual Studio, verá una barra amarilla de alerta con mensajes de error detallados en la ficha de error de Hola.

1. Haga clic en **descargar** necesarios de toodownload Hola a todos los recursos y los flujos de entrada. Si no completa la descarga de hello, haga clic en **vuelva a intentar**.

2. Haga clic en **abiertos** al finalizar la descarga de hello toogenerate un entorno de depuración local. Se creará y abrirá automáticamente una nueva instancia de Visual Studio con una solución de depuración.

![Descarga de vértices para depuración de trabajos U-SQL de Azure Data Lake Analytics en Visual Studio](./media/data-lake-analytics-debug-u-sql-jobs/data-lake-analytics-download-vertex.png)

Los trabajos pueden incluir archivos de origen con código subyacente o ensamblados registrados, y estos dos tipos tienen escenarios de depuración diferentes.

- [Depuración de un trabajo con error con código subyacente](#debug-job-failed-with-code-behind)
- [Depuración de un trabajo con error con ensamblados](#debug-job-failed-with-assemblies)


## <a name="debug-job-failed-with-code-behind"></a>Depuración de un trabajo con error con código subyacente

Si se produce un error en un trabajo de SQL de U y trabajo Hola incluye código de usuario (normalmente denominado `Script.usql.cs` en un proyecto de SQL U), que el código fuente se importa en hello depurar la solución.  Desde allí puede usar problema de hello Visual Studio depuración herramientas (inspección, variables, etc.) tootroubleshoot Hola.

> [!NOTE]
> Antes de depurar, ser seguro toocheck **excepciones de Common Language Runtime** en la ventana de configuración de excepciones de hello (**Ctrl + Alt + E**).

![Configuración de depuración de trabajos U-SQL de Azure Data Lake Analytics en Visual Studio](./media/data-lake-analytics-debug-u-sql-jobs/data-lake-analytics-clr-exception-setting.png)

1. Presione **F5** código subyacente de toorun Hola. Se ejecutará hasta que una excepción lo detenga.

2. Abra hello `ADLTool_Codebehind.usql.cs` de archivos y establecer puntos de interrupción, a continuación, presione **F5** código de hello toodebug paso a paso.

    ![Excepción de depuración de U-SQL de Azure Data Lake Analytics](./media/data-lake-analytics-debug-u-sql-jobs/data-lake-analytics-debug-exception.png)

## <a name="debug-job-failed-with-assemblies"></a>Error de depuración del trabajo con ensamblados

Si utiliza ensamblados registrados en el script U-SQL, sistema de hello no puede obtener código de hello automáticamente. En este caso, agregue manualmente origen código archivos toohello solución los ensamblados Hola.

### <a name="configure-hello-solution"></a>Configurar la solución de Hola

1. Haga clic en **solución 'VertexDebug' > Agregar > proyecto existente...**  toofind Hola código de origen de ensamblados y agregue Hola proyecto toohello depurar la solución.

    ![Depuración de U-SQL de Azure Data Lake Analytics: agregar proyecto](./media/data-lake-analytics-debug-u-sql-jobs/data-lake-analytics-add-project-to-debug-solution.png)

2. Haga clic en **LocalVertexHost > propiedades** Hola Hola de soluciones y copie **Working Directory** ruta de acceso.

3. Haga clic en **proyecto de código fuente de ensamblado > propiedades**, seleccione hello **generar** ficha a la izquierda y pegue Hola Copiar ruta de acceso como **salida > ruta de acceso de salida**.

    ![Depuración de U-SQL de Azure Data Lake Analytics: definición de la ruta de acceso de pdb](./media/data-lake-analytics-debug-u-sql-jobs/data-lake-analytics-set-pdb-path.png)

4. Presione **Ctrl + Alt + E** y marque **Common Language Runtime Exceptions** (Excepciones de Common Language Runtime) en la ventana de configuración de excepciones.

### <a name="start-debug"></a>Inicio de la depuración

1. Haga clic en **proyecto de código fuente de ensamblado > volver a generar** toohello los archivos .pdb toooutput `LocalVertexHost` directorio de trabajo.

2. Presione **F5** y proyecto de Hola se ejecutará hasta que se detiene debido a una excepción. Es posible que vea Hola siguiente mensaje de advertencia, que se puede omitir con seguridad. Puede tardar tooa tooget minuto toohello depuración pantalla hacia arriba.

    ![Advertencia de depuración de trabajos U-SQL de Azure Data Lake Analytics en Visual Studio](./media/data-lake-analytics-debug-u-sql-jobs/data-lake-analytics-visual-studio-u-sql-debug-warning.png)

3. Abra el código fuente y establecer puntos de interrupción, a continuación, presione **F5** código de hello toodebug paso a paso.

También puede utilizar el problema de hello Visual Studio depuración herramientas (inspección, variables, etc.) tootroubleshoot Hola.

> [!NOTE]
> Vuelva a generar proyecto de código fuente de hello ensamblado cada vez después de modificar toogenerate actualizar código de hello, .pdb (archivos).

Tras la depuración, si se completa correctamente el proyecto de hello ventana de salida de hello muestra hello siguiente mensaje:

```
hello Program 'LocalVertexHost.exe' has exited with code 0 (0x0).
```

![Azure Data Lake Analytics U-SQL debug succeed (La depuración de U-SQL de Azure Data Lake Analytics se realizó correctamente)](./media/data-lake-analytics-debug-u-sql-jobs/data-lake-analytics-debug-succeed.png)

## <a name="resubmit-hello-job"></a>Vuelva a enviar el trabajo de Hola

Una vez haya completado la depuración, vuelva a enviar Hola trabajo con errores.

1. Para los trabajos con soluciones de código subyacente, copie el código de C# en el archivo de código fuente del código subyacente de hello (normalmente `Script.usql.cs`).
2. Para los trabajos con ensamblados, registre los ensamblados .dll Hola actualizado en la base de datos ADLA:
    1. Desde el Explorador de servidores o el explorador en la nube, expanda hello **cuenta ADLA > bases de datos** nodo.
    2. Haga clic en **ensamblados** y registrar los ensamblados .dll nuevo con la base de datos de Hola ADLA: ![depuración de Azure Data Lake Analytics U-SQL registrar ensamblados](./media/data-lake-analytics-debug-u-sql-jobs/data-lake-analytics-register-assembly.png)
3. Vuelva a enviar el trabajo.

## <a name="next-steps"></a>Pasos siguientes

- [Guía de programación de U-SQL](data-lake-analytics-u-sql-programmability-guide.md)
- [Desarrollo de operadores U-SQL definidos por el usuario para trabajos de Azure Data Lake Analytics](data-lake-analytics-u-sql-develop-user-defined-operators.md)
- [Tutorial: Desarrollo de scripts U-SQL mediante Data Lake Tools for Visual Studio](data-lake-analytics-data-lake-tools-get-started.md)
