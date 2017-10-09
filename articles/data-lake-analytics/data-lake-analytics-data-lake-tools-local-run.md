---
title: "aaaTest y depuración SQL U trabajos mediante el uso locales ejecutar y Hola SDK de Azure datos Lake U-SQL | Documentos de Microsoft"
description: "Obtenga información acerca de cómo toouse Azure Data Lake Tools para Visual Studio y tootest del SDK de SQL Azure datos Lake U hello y depuración SQL U trabajos en la estación de trabajo local."
services: data-lake-analytics
documentationcenter: 
author: mumian
manager: jhubbard
editor: cgronlun
ms.assetid: 66dd58b1-0b28-46d1-aaae-43ee2739ae0a
ms.service: data-lake-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 11/15/2016
ms.author: yanacai
ms.openlocfilehash: be04558a504acf6a088e207608ee2d4a011d3ffc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="test-and-debug-u-sql-jobs-by-using-local-run-and-hello-azure-data-lake-u-sql-sdk"></a>Probar y depurar los trabajos de SQL U mediante local ejecutar y Hola SDK de SQL Azure datos Lake U

Puede usar Azure Data Lake Tools para Visual Studio y trabajos de hello SDK de Azure datos Lake U-SQL toorun U-SQL en la estación de trabajo, igual que lo haría en el servicio de Azure Data Lake Hola. Estas dos características de ejecución local ahorran tiempo para probar y depurar los trabajos de U-SQL.

## <a name="understand-hello-data-root-folder-and-hello-file-path"></a>Comprender la carpeta de datos raíz de Hola y ruta de acceso de archivo de Hola

Ejecución local y hello U-SQL SDK requieren una carpeta raíz de datos. carpeta de datos raíz de Hello es un "almacén local" para la cuenta de proceso local Hola. Es la cuenta de almacén de Azure Data Lake toohello equivalente de una cuenta de análisis de Data Lake. Cambiar tooa carpeta raíz de datos diferentes es igual que cambiar la cuenta de otro almacén de tooa. Si desea tooaccess comúnmente suelen compartir datos con las carpetas raíz de datos diferente, debe usar rutas de acceso absolutas en las secuencias de comandos. O bien, crear vínculos simbólicos de sistema de archivos (por ejemplo, **mklink** en NTFS) en la carpeta toopoint toohello de hello raíz de datos de los datos compartidos.

carpeta de datos raíz de Hola se utiliza para:

- Almacenar metadatos, lo que incluye bases de datos, tablas, funciones con valores de tabla (TVF) y ensamblados.
- Buscar Hola de entrada y las rutas de acceso de salida que se definen como rutas de acceso relativas en U-SQL. Usar rutas de acceso relativas resulta más fácil toodeploy su tooAzure de proyectos U-SQL.

Puede usar tanto una ruta de acceso relativa como una ruta de acceso absoluta local en los scripts U-SQL. ruta de acceso relativa de Hello es relativa toohello ruta de la carpeta de raíz de datos especificado. Se recomienda que se utilice "/" como Hola toomake de separador de ruta de acceso las secuencias de comandos compatibles con el lado del servidor de Hola. Estos son algunos ejemplos de rutas de acceso relativas y sus rutas de acceso absolutas equivalentes. En estos ejemplos, C:\LocalRunDataRoot es la carpeta de datos raíz de Hola.

|Ruta de acceso relativa|Ruta de acceso absoluta|
|-------------|-------------|
|/abc/def/input.csv |C:\LocalRunDataRoot\abc\def\input.csv|
|abc/def/input.csv  |C:\LocalRunDataRoot\abc\def\input.csv|
|D:/abc/def/input.csv |D:\abc\def\input.csv|

## <a name="use-local-run-from-visual-studio"></a>Uso de ejecución local desde Visual Studio

Data Lake Tools para Visual Studio proporciona la experiencia de ejecución local de U-SQL en Visual Studio. Con esta característica, puede:

- Ejecutar scripts U-SQL localmente, junto con los ensamblados de C#.
- Depurar un ensamblado de C# localmente.
- Crear, ver y eliminar catálogos de U-SQL (bases de datos locales, ensamblados, esquemas y tablas) desde el Explorador de servidores. También puede encontrar el catálogo local hello también desde el Explorador de servidores.

    ![Catálogo local de ejecución local de Data Lake Tools para Visual Studio](./media/data-lake-analytics-data-lake-tools-local-run/data-lake-tools-for-visual-studio-local-run-local-catalog.png)

instalador de Data Lake Tools Hola crea un toobe de carpeta C:\LocalRunRoot utilizado como carpeta raíz de datos predeterminada del saludo. paralelismo de ejecución local de Hello predeterminado es 1.

### <a name="tooconfigure-local-run-in-visual-studio"></a>tooconfigure local se ejecuta en Visual Studio

1. Abra Visual Studio.
2. Abra el **Explorador de servidores**.
3. Expanda **Azure** > **Data Lake Analytics**.
4. Haga clic en hello **Data Lake** menú y, a continuación, haga clic en **opciones y configuración**.
5. En el árbol de la izquierda hello, expanda **Azure Data Lake**y, a continuación, expanda **General**.

    ![Configuración de ejecución local de Data Lake Tools para Visual Studio](./media/data-lake-analytics-data-lake-tools-local-run/data-lake-tools-for-visual-studio-local-run-configure.png)

Se necesita un proyecto de U-SQL de Visual Studio para realizar la ejecución local. Esta parte es diferente de la ejecución de scripts U-SQL desde Azure.

### <a name="toorun-a-u-sql-script-locally"></a>la secuencia de comandos de toorun un U-SQL localmente
1. En Visual Studio, abra el proyecto U-SQL.   
2. Haga clic con el botón derecho en un script U-SQL en el Explorador de soluciones y después haga clic en **Submit Script** (Enviar script).
3. Seleccione **(Local)** hello análisis cuenta toorun localmente la secuencia de comandos.
También puede hacer clic en hello **(Local)** cuenta en la parte superior de Hola de ventana de script y, a continuación, haga clic en **enviar** (o utilice Hola Ctrl + método abreviado de teclado F5).

    ![Trabajos de envío de ejecución local de Data Lake Tools para Visual Studio](./media/data-lake-analytics-data-lake-tools-local-run/data-lake-tools-for-visual-studio-local-run-submit-job.png)

### <a name="debug-scripts-and-c-assemblies-locally"></a>Depurar scripts y ensamblados de C# localmente

Puede depurar los ensamblados de C# sin enviar y registrar tooAzure servicio de análisis de datos Lake. Puede establecer puntos de interrupción en ambos Hola archivo de código subyacente y en un proyecto de C# que se hace referencia.

#### <a name="toodebug-local-code-in-code-behind-file"></a>toodebug código local en el archivo de código subyacente

1. Establezca puntos de interrupción Hola archivo de código subyacente.
2. Presione F5 toodebug hello secuencia de comandos de forma local.

> [!NOTE]
   > Hola siguiendo el procedimiento solo funciona en Visual Studio 2015. En Visual Studio anterior puede ser necesario toomanually agregar archivos pdb de Hola.  
   >
   >

#### <a name="toodebug-local-code-in-a-referenced-c-project"></a>toodebug código local en un proyecto de C# que se hace referencia

1. Crear un proyecto de ensamblado de C# y genérelo dll de salida de hello toogenerate.
2. Registre la dll de hello mediante una instrucción SQL U:

        CREATE ASSEMBLY assemblyname FROM @"..\..\path\to\output\.dll";
        
3. Establecer puntos de interrupción en código C# Hola.
4. Presione F5 toodebug hello secuencia de comandos que hacen referencia a la dll de hello C# localmente.

## <a name="use-local-run-from-hello-data-lake-u-sql-sdk"></a>Usar local ejecutar de hello datos Lake U-SQL SDK

Además de scripts toorunning U-SQL localmente mediante Visual Studio, puede usar secuencias de comandos de hello SDK de Azure datos Lake U-SQL toorun U-SQL localmente con interfaces de línea de comandos y programación. A través de estos elementos, puede escalar la prueba local de U-SQL.

Obtenga más información sobre el [SDK de U-SQL para Azure Data Lake](data-lake-analytics-u-sql-sdk.md).


## <a name="next-steps"></a>Pasos siguientes

* toosee una consulta más compleja, vea [analizar registros de sitio Web mediante el análisis de Azure Data Lake](data-lake-analytics-analyze-weblogs.md).
* Ver detalles del trabajo tooview, [utilizar un trabajo del explorador y la vista de trabajos de trabajos de análisis de Azure Data Lake](data-lake-analytics-data-lake-tools-view-jobs.md).
* vista de ejecución de toouse Hola vértices, consulte [Hola Use vista de ejecución de vértices de Data Lake Tools para Visual Studio](data-lake-analytics-data-lake-tools-use-vertex-execution-view.md).
