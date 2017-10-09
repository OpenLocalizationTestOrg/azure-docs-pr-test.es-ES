---
title: aaaScale U-SQL local ejecutar y probar con el SDK de Azure datos Lake U-SQL | Documentos de Microsoft
description: "Obtenga información acerca de cómo trabajos de tooscale U-SQL de SDK de Azure datos Lake U-SQL toouse locales ejecutan y probar con la línea de comandos e interfaces de programación en la estación de trabajo local."
services: data-lake-analytics
documentationcenter: 
author: 
manager: 
editor: 
ms.assetid: 
ms.service: data-lake-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 03/01/2017
ms.author: yanacai
ms.openlocfilehash: 2b0a16229789268e333f723ff6fc2c3efdc29905
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="scale-u-sql-local-run-and-test-with-azure-data-lake-u-sql-sdk"></a>Escalado de prueba y depuración local de U-SQL con el SDK de U-SQL para Azure Data Lake

Al desarrollar el script U-SQL, es común toorun y script de prueba U SQL localmente antes de enviar se toocloud. Azure Data Lake proporciona un paquete Nuget denominado SDK de U-SQL para Azure Data Lake para esta situación, por lo que le resultará muy fácil realizar el escalado de prueba y ejecución local de U-SQL. También es posible toointegrate esta U-SQL probar con la compilación de CI (integración continua) sistema tooautomate hello y prueba.

Si le interesa cómo toomanually local ejecutar y depurar el script U-SQL con herramientas de interfaz gráfica de usuario, puede usar Azure Data Lake Tools para Visual Studio para. Puede obtener más información sobre esto [aquí](data-lake-analytics-data-lake-tools-local-run.md).

## <a name="install-azure-data-lake-u-sql-sdk"></a>Instalación del SDK de U-SQL para Azure Data Lake

Puede obtener Hola SDK de SQL Azure datos Lake U [aquí](https://www.nuget.org/packages/Microsoft.Azure.DataLake.USQL.SDK/) en Nuget.org. Y antes de usarlo, debe toomake que tengan dependencias como se indica a continuación.

### <a name="dependencies"></a>Dependencias

Hola datos Lake U-SQL SDK requiere Hola siguientes dependencias:

- [Microsoft .NET Framework 4.6 o superior](https://www.microsoft.com/download/details.aspx?id=17851).
- Microsoft Visual C++ 14 y el SDK de Windows 10.0.10240.0 o posterior (que se denomina CppSDK en este artículo). Hay dos maneras tooget CppSDK:

    - Instale [Visual Studio Community Edition](https://developer.microsoft.com/downloads/vs-thankyou). Tendrá una carpeta \Windows Kits\10 en la carpeta de archivos de programa Hola: por ejemplo, C:\Program Files (x86) \Windows Kits\10\. También encontrará la versión del SDK de Windows 10 de hello en \Windows Kits\10\Lib. Si no ve estas carpetas, vuelva a instalar Visual Studio y estar seguro de tooselect Hola SDK de Windows 10 durante la instalación de Hola. Si tiene instalado con Visual Studio, compilador de saludo U-SQL local considerará automáticamente.

    ![SDK de Windows 10 para ejecución local de Data Lake Tools para Visual Studio](./media/data-lake-analytics-data-lake-tools-local-run/data-lake-tools-for-visual-studio-local-run-windows-10-sdk.png)

    - Instale [Data Lake Tools para Visual Studio](http://aka.ms/adltoolsvs). Puede encontrar Hola preestablecido archivos de Visual C++ y el SDK de Windows en C:\Program Files (x86) \Microsoft Visual Studio 14.0\Common7\IDE\Extensions\Microsoft\ADL Tools\X.X.XXXX.X\CppSDK. En este caso, compilador de saludo U-SQL local no encuentra las dependencias de hello automáticamente. Necesita ruta de acceso de toospecify hello CppSDK para él. Puede copiar la ubicación de los archivos tooanother Hola o utilizarlo tal como está.

## <a name="understand-basic-concepts"></a>Conceptos básicos

### <a name="data-root"></a>Raíz de datos

carpeta de datos raíz de Hello es un "almacén local" para la cuenta de proceso local Hola. Es la cuenta de almacén de Azure Data Lake toohello equivalente de una cuenta de análisis de Data Lake. Cambiar tooa carpeta raíz de datos diferentes es igual que cambiar la cuenta de otro almacén de tooa. Si desea tooaccess comúnmente suelen compartir datos con las carpetas raíz de datos diferente, debe usar rutas de acceso absolutas en las secuencias de comandos. O bien, crear vínculos simbólicos de sistema de archivos (por ejemplo, **mklink** en NTFS) en la carpeta toopoint toohello de hello raíz de datos de los datos compartidos.

carpeta de datos raíz de Hola se utiliza para:

- Almacenar metadatos, lo que incluye bases de datos, tablas, funciones con valores de tabla (TVF) y ensamblados.
- Buscar Hola de entrada y las rutas de acceso de salida que se definen como rutas de acceso relativas en U-SQL. Usar rutas de acceso relativas resulta más fácil toodeploy su tooAzure de proyectos U-SQL.

### <a name="file-path-in-u-sql"></a>Ruta de archivo de U-SQL

Puede usar tanto una ruta de acceso relativa como una ruta de acceso absoluta local en los scripts U-SQL. ruta de acceso relativa de Hello es relativa toohello ruta de la carpeta de raíz de datos especificado. Se recomienda que se utilice "/" como Hola toomake de separador de ruta de acceso las secuencias de comandos compatibles con el lado del servidor de Hola. Estos son algunos ejemplos de rutas de acceso relativas y sus rutas de acceso absolutas equivalentes. En estos ejemplos, C:\LocalRunDataRoot es la carpeta de datos raíz de Hola.

|Ruta de acceso relativa|Ruta de acceso absoluta|
|-------------|-------------|
|/abc/def/input.csv |C:\LocalRunDataRoot\abc\def\input.csv|
|abc/def/input.csv  |C:\LocalRunDataRoot\abc\def\input.csv|
|D:/abc/def/input.csv |D:\abc\def\input.csv|

### <a name="working-directory"></a>Directorio de trabajo

Cuando se ejecuta el script de Hola U-SQL localmente, se crea un directorio de trabajo durante la compilación en el directorio de ejecución actual. Además toohello compilación genera, hello necesarios en tiempo de ejecución para la ejecución local se generarán directorio de trabajo de instantáneas toothis copiada. Hola carpeta raíz de directorio de trabajo se denomina "ScopeWorkDir" y archivos de hello en hello directorio de trabajo son los siguientes:

|Directorio o archivo|Directorio o archivo|Directorio o archivo|Definición|Descripción|
|--------------|--------------|--------------|----------|-----------|
|C6A101DDCB470506| | |Cadena de hash de la versión del runtime|Instantánea de los archivos del runtime necesarios para la ejecución local|
| |Script_66AE4909AA0ED06C| |Nombre de script + cadena de hash de la ruta de acceso del script|Resultados de compilación y registro de los pasos de ejecución|
| | |\_script\_.abr|Salida del compilador|Archivo de álgebra|
| | |\_ScopeCodeGen\_.*|Salida del compilador|Código administrado generado|
| | |\_ScopeCodeGenEngine\_.*|Salida del compilador|Código nativo generado|
| | |ensamblados de referencia|Referencia de ensamblado|Archivos de ensamblados de referencia|
| | |deployed_resources|Implementación de recursos|Archivos de implementación de recursos|
| | |xxxxxxxx.xxx[1..n]\_\*.*|Registro de ejecución|Registro de pasos de ejecución|


## <a name="use-hello-sdk-from-hello-command-line"></a>Usar hello SDK desde la línea de comandos de Hola

### <a name="command-line-interface-of-hello-helper-application"></a>Interfaz de línea de comandos de la aplicación auxiliar de Hola

En SDK directory\build\runtime, LocalRunHelper.exe es aplicación de línea de comandos auxiliar de Hola que proporciona interfaces toomost de hello usada local y ejecutar funciones. Tenga en cuenta que ambos Hola comandos y modificadores de argumento Hola distinguen mayúsculas de minúsculas. tooinvoke:

    LocalRunHelper.exe <command> <Required-Command-Arguments> [Optional-Command-Arguments]

Ejecutar LocalRunHelper.exe sin argumentos o con hello **ayuda** cambiar información de Ayuda de Hola tooshow:

    > LocalRunHelper.exe help

        Command 'help' :  Show usage information
        Command 'compile' :  Compile hello script
        Required Arguments :
            -Script param
                    Script File Path
        Optional Arguments :
            -Shallow [default value 'False']
                    Shallow compile

Hola información de ayuda:

-  **Comando** proporciona Hola el nombre de comando.  
-  **Required Argument** enumera los argumentos que se deben proporcionar.  
-  **Optional Argument** enumera argumentos que son opcionales, con los valores predeterminados.  Argumentos booleanos opcionales no tienen parámetros y sus repeticiones significan el valor predeterminado de tootheir negativo.

### <a name="return-value-and-logging"></a>Valor devuelto y registro

Devuelve la aplicación auxiliar de Hello **0** para el éxito y **-1** error. De forma predeterminada, auxiliar Hola envía consola actual de todos los mensajes toohello. Sin embargo, la mayoría de los comandos de hello admite hello **- MessageOut rutaDeAccesoAlArchivoDeRegistro** argumento opcional que redirija Hola genera el archivo de registro tooa.

### <a name="environment-variable-configuring"></a>Configuración de la variable de entorno

La ejecución local de U-SQL requiere una raíz de datos explícita como cuenta de almacenamiento local, así como una ruta de acceso de CppSDK explícita para las dependencias. Puede ambos argumento de hello establecido en la variable de entorno de línea de comandos o está establecida para ellos.

- Conjunto hello **SCOPE_CPP_SDK** variable de entorno.

    Si se producen hello SDK de Windows y Microsoft Visual C++ mediante la instalación de Data Lake Tools para Visual Studio, compruebe que dispone de hello siguiente carpeta:

        C:\Program Files (x86)\Microsoft Visual Studio 14.0\Common7\IDE\Extensions\Microsoft\Microsoft Azure Data Lake Tools for Visual Studio 2015\X.X.XXXX.X\CppSDK

    Definir una nueva variable de entorno denominada **SCOPE_CPP_SDK** toopoint toothis directory. O copie Hola carpeta toohello otra ubicación y especificar **SCOPE_CPP_SDK** que.

    En la variable de entorno de suma toosetting hello, puede especificar hello **- CppSDK** argumento cuando se usa la línea de comandos de Hola. Este argumento sobrescribe la variable de entorno CppSDK predeterminada.

- Conjunto hello **LOCALRUN_DATAROOT** variable de entorno.

    Definir una nueva variable de entorno denominada **LOCALRUN_DATAROOT** que apunta la raíz de datos de toohello.

    En la variable de entorno de suma toosetting hello, puede especificar hello **- DataRoot** argumento con ruta de acceso de datos raíz de hello cuando se usa una línea de comandos. Este argumento sobrescribe la variable de entorno raíz de datos predeterminada. Debe tooadd esta línea de comandos de tooevery de argumento que está ejecutando para que se puede sobrescribir la variable de entorno de datos raíz de hello predeterminada para todas las operaciones.

### <a name="sdk-command-line-usage-samples"></a>Ejemplos de uso de línea de comandos del SDK

#### <a name="compile-and-run"></a>Compilación y ejecución

Hola **ejecutar** se utiliza el comando toocompile Hola script y, a continuación, ejecutar resultados compilados. Sus argumentos de línea de comandos son una combinación de los de **compile** y **execute**.

    LocalRunHelper run -Script path_to_usql_script.usql [optional_arguments]

Hello siguiente es argumentos opcionales para **ejecutar**:


|Argumento|Valor predeterminado|Descripción|
|--------|-------------|-----------|
|-CodeBehind|False|script de Hola tiene .cs código subyacente|
|-CppSDK| |Directorio CppSDK|
|-DataRoot| Variable de entorno de DataRoot|DataRoot para la ejecución local, predeterminado demasiado variable de entorno 'LOCALRUN_DATAROOT'|
|-MessageOut| |Mensajes de volcado de memoria en el archivo de consola tooa|
|-Parallel|1|Ejecute hello plan con hello especificado paralelismo|
|-References| |Lista de ensamblados de referencia de las rutas de acceso tooextra o archivos de datos de código subyacente, separado por ';'|
|-UdoRedirect|False|Generar la configuración de redirección de ensamblado de Udo|
|-UseDatabase|maestro|Toouse de base de datos para el código subyacente de registro de ensamblados temporales|
|-Verbose|False|Mostrar resultados detallados del runtime|
|-WorkDir|Directorio actual|Directorio para las salidas y el uso del compilador|
|-RunScopeCEP|0|ScopeCEP modo toouse|
|-ScopeCEPTempPath|temp|Ruta de acceso temporal toouse streaming de datos|
|-OptFlags| |Lista de marcas de optimizador separadas por comas|


Este es un ejemplo:

    LocalRunHelper run -Script d:\test\test1.usql -WorkDir d:\test\bin -CodeBehind -References "d:\asm\ref1.dll;d:\asm\ref2.dll" -UseDatabase testDB –Parallel 5 -Verbose

Además de combinación **compilar** y **ejecutar**, puede compilar y ejecutar ejecutables Hola compilado por separado.

#### <a name="compile-a-u-sql-script"></a>Compilación de un script U-SQL

Hola **compilar** comando es tooexecutables de script usados toocompile U T-SQL.

    LocalRunHelper compile -Script path_to_usql_script.usql [optional_arguments]

Hello siguiente es argumentos opcionales para **compilar**:


|Argumento|Descripción|
|--------|-----------|
| -CodeBehind [valor predeterminado 'False']|script de Hola tiene .cs código subyacente|
| -CppSDK [valor predeterminado '']|Directorio CppSDK|
| -DataRoot [valor predeterminado 'DataRoot environment variable']|DataRoot para la ejecución local, predeterminado demasiado variable de entorno 'LOCALRUN_DATAROOT'|
| -MessageOut [valor predeterminado '']|Mensajes de volcado de memoria en el archivo de consola tooa|
| -References [valor predeterminado '']|Lista de ensamblados de referencia de las rutas de acceso tooextra o archivos de datos de código subyacente, separado por ';'|
| -Shallow [valor predeterminado 'False']|Compilación superficial|
| -UdoRedirect [valor predeterminado 'False']|Generar la configuración de redirección de ensamblado de Udo|
| -UseDatabase [valor predeterminado 'master']|Toouse de base de datos para el código subyacente de registro de ensamblados temporales|
| -WorkDir [valor predeterminado 'Current Directory']|Directorio para las salidas y el uso del compilador|
| -RunScopeCEP [valor predeterminado '0']|ScopeCEP modo toouse|
| -ScopeCEPTempPath [valor predeterminado 'temp']|Ruta de acceso temporal toouse streaming de datos|
| -OptFlags [valor predeterminado '']|Lista de marcas de optimizador separadas por comas|


Estos son algunos ejemplos de uso.

Compile un script U-SQL:

    LocalRunHelper compile -Script d:\test\test1.usql

Compilar un script U-SQL y establecer carpeta de datos raíz de Hola. Tenga en cuenta que esta acción sobrescribirá la variable de entorno de conjunto de Hola.

    LocalRunHelper compile -Script d:\test\test1.usql –DataRoot c:\DataRoot

Compile un script U-SQL y establezca el directorio de trabajo, el ensamblado de referencia y la base de datos:

    LocalRunHelper compile -Script d:\test\test1.usql -WorkDir d:\test\bin -References "d:\asm\ref1.dll;d:\asm\ref2.dll" -UseDatabase testDB

#### <a name="execute-compiled-results"></a>Ejecución de resultados compilados

Hola **ejecutar** comando es resultados tooexecute usado compilado.   

    LocalRunHelper execute -Algebra path_to_compiled_algebra_file [optional_arguments]

Hello siguiente es argumentos opcionales para **ejecutar**:

|Argumento|Descripción|
|--------|-----------|
|-DataRoot [valor predeterminado '']|Raíz de datos para la ejecución de metadatos. El valor predeterminado es toohello **LOCALRUN_DATAROOT** variable de entorno.|
|-MessageOut [valor predeterminado '']|Los mensajes en el archivo de hello consola tooa de volcado de memoria.|
|-Parallel [valor predeterminado '1']|Pasos de ejecución local de indicador toorun Hola generado con hello especifican el nivel de paralelismo.|
|-Verbose [valor predeterminado 'False']|Indicador tooshow detallada genera una salida en tiempo de ejecución.|

Presentamos un ejemplo de uso:

    LocalRunHelper execute -Algebra d:\test\workdir\C6A101DDCB470506\Script_66AE4909AA0ED06C\__script__.abr –DataRoot c:\DataRoot –Parallel 5


## <a name="use-hello-sdk-with-programming-interfaces"></a>Usar hello SDK con interfaces de programación

interfaces de programación de Hola se encuentran en hello LocalRunHelper.exe. Puede usar funcionalidad de hello toointegrate de hello U-SQL SDK y Hola tooscale de marco de pruebas de C# de la prueba local del script U-SQL. En este artículo, usaré Hola estándar C# unidad prueba proyecto tooshow cómo toouse estas interfaces tootest el script U-SQL.

### <a name="step-1-create-c-unit-test-project-and-configuration"></a>Paso 1: Crear la configuración y el proyecto de prueba unitaria de C#

- Cree un proyecto de prueba unitaria de C# en Archivo > Nuevo > Proyecto > Visual C# > Probar > Proyecto de prueba unitaria.
- Agregar LocalRunHelper.exe como una referencia de proyecto de Hola. Hola LocalRunHelper.exe se encuentra en \build\runtime\LocalRunHelper.exe en el paquete de Nuget.

    ![Agregar referencia del SDK de U-SQL para Azure Data Lake](./media/data-lake-analytics-u-sql-sdk/data-lake-analytics-u-sql-sdk-add-reference.png)

- SDK de U-SQL **sólo** soporte x64 entorno, asegúrese de tooset seguro el destino de plataforma de compilación como x64. Se puede establecer en Propiedad del proyecto > Compilar > Destino de la plataforma.

    ![Configurar proyecto x64 del SDK de U-SQL para Azure Data Lake](./media/data-lake-analytics-u-sql-sdk/data-lake-analytics-u-sql-sdk-configure-x64.png)

- Hacer tooset seguro de que el entorno de prueba como x64. En Visual Studio, se puede establecer en Probar > Configuración de pruebas > Arquitectura del procesador predeterminada > x64.

    ![Configurar el entorno de prueba x64 del SDK de U-SQL para Azure Data Lake](./media/data-lake-analytics-u-sql-sdk/data-lake-analytics-u-sql-sdk-configure-test-x64.png)

- Asegúrese de que toocopy todos los archivos de dependencia en el directorio de trabajo de tooproject NugetPackage\build\runtime\ que se encuentra normalmente en ProjectFolder\bin\x64\Debug.

### <a name="step-2-create-u-sql-script-test-case"></a>Paso 2: Crear caso de prueba del script U-SQL

A continuación se muestra código de ejemplo de Hola para prueba de script U-SQL. Para las pruebas, deberá tooprepare scripts, archivos de entrada y archivos de resultados esperado.

    using System;
    using Microsoft.VisualStudio.TestTools.UnitTesting;
    using System.IO;
    using System.Text;
    using System.Security.Cryptography;
    using Microsoft.Analytics.LocalRun;

    namespace UnitTestProject1
    {
        [TestClass]
        public class USQLUnitTest
        {
            [TestMethod]
            public void TestUSQLScript()
            {
                //Specify hello local run message output path
                StreamWriter MessageOutput = new StreamWriter("../../../log.txt");

                LocalRunHelper localrun = new LocalRunHelper(MessageOutput);

                //Configure hello DateRoot path, Script Path and CPPSDK path
                localrun.DataRoot = "../../../";
                localrun.ScriptPath = "../../../Script/Script.usql";
                localrun.CppSdkDir = "../../../CppSDK";

                //Run U-SQL script
                localrun.DoRun();

                //Script output 
                string Result = Path.Combine(localrun.DataRoot, "Output/result.csv");

                //Expected script output
                string ExpectedResult = "../../../ExpectedOutput/result.csv";

                Test.Helpers.FileAssert.AreEqual(Result, ExpectedResult);

                //Don't forget tooclose MessageOutput tooget logs into file
                MessageOutput.Close();
            }
        }
    }

    namespace Test.Helpers
    {
        public static class FileAssert
        {
            static string GetFileHash(string filename)
            {
                Assert.IsTrue(File.Exists(filename));

                using (var hash = new SHA1Managed())
                {
                    var clearBytes = File.ReadAllBytes(filename);
                    var hashedBytes = hash.ComputeHash(clearBytes);
                    return ConvertBytesToHex(hashedBytes);
                }
            }

            static string ConvertBytesToHex(byte[] bytes)
            {
                var sb = new StringBuilder();

                for (var i = 0; i < bytes.Length; i++)
                {
                    sb.Append(bytes[i].ToString("x"));
                }
                return sb.ToString();
            }

            public static void AreEqual(string filename1, string filename2)
            {
                string hash1 = GetFileHash(filename1);
                string hash2 = GetFileHash(filename2);

                Assert.AreEqual(hash1, hash2);
            }
        }
    }


### <a name="programming-interfaces-in-localrunhelperexe"></a>Interfaces de programación de LocalRunHelper.exe

LocalRunHelper.exe proporciona Hola interfaces de programación para compilación local U-SQL, ejecutar, interfaces de hello etc. se indican a continuación.

**Constructor**

public LocalRunHelper([System.IO.TextWriter messageOutput = null])

|.|Tipo|Descripción|
|---------|----|-----------|
|messageOutput|System.IO.TextWriter|para los mensajes de salida, establezca toonull toouse consola|

**Propiedades**

|Propiedad|Escriba|Descripción|
|--------|----|-----------|
|AlgebraPath|cadena|archivo de tooalgebra de ruta de acceso de Hello (archivo álgebra es uno de los resultados de compilación de hello)|
|CodeBehindReferences|cadena|Si el script de Hola tiene código adicional detrás de las referencias, especificar rutas de acceso de hello separados por ';'|
|CppSdkDir|string|Directorio CppSDK|
|CurrentDir|string|Directorio actual|
|DataRoot|cadena|Ruta de acceso raíz de datos|
|DebuggerMailPath|cadena|el procesador de mensajes de Hola ruta de acceso toodebugger|
|GenerateUdoRedirect|booleano|Si lo deseamos carga de ensamblado toogenerate redirección invalidar configuración|
|HasCodeBehind|booleano|Si el script de Hola tiene código subyacente|
|InputDir|cadena|Directorio de datos de entrada|
|MessagePath|cadena|Ruta de acceso del archivo de volcado de memoria de mensajes|
|OutputDir|string|Directorio de datos de salida|
|Paralelismo|int|Álgebra de paralelismo toorun Hola|
|ParentPid|int|PID del elemento primario de hello en qué Hola servicio supervisa tooexit, conjunto too0 o tooignore negativo|
|ResultPath|string|Ruta de acceso del archivo de volcado de memoria de resultados|
|RuntimeDir|string|Directorio del entorno en tiempo de ejecución|
|scriptPath|cadena|Donde toofind hello secuencia de comandos|
|Shallow|booleano|Compilación superficial o no|
|TempDir|cadena|Directorio temporal|
|UseDataBase|cadena|Especificar hello toouse de base de datos para el código subyacente de registro del ensamblado temporal, maestro de forma predeterminada|
|WorkDir|string|Directorio de trabajo preferido|


**Método**

|Método|Descripción|Valor devuelto|Parámetro|
|------|-----------|------|---------|
|public bool DoCompile()|Compilar el script de Hola U-SQL|Si se realiza correctamente, devuelve True.| |
|public bool DoExec()|Ejecutar el resultado de hello compilado|Si se realiza correctamente, devuelve True.| |
|public bool DoRun()|Ejecutar script de Hola U-SQL (compilación + Execute)|Si se realiza correctamente, devuelve True.| |
|public bool IsValidRuntimeDir(string path)|Comprobar si Hola ruta de acceso dada es la ruta de acceso válida en tiempo de ejecución|True para válida|ruta de acceso de Hello del directorio en tiempo de ejecución|


## <a name="faq-about-common-issue"></a>Preguntas más frecuentes sobre problemas comunes

### <a name="error-1"></a>Error 1:
E_CSC_SYSTEM_INTERNAL: Error interno. No se pudo cargar el archivo o ensamblado 'ScopeEngineManaged.dll' ni una de sus dependencias. no se pudo encontrar el módulo especificado Hola.

Consulte el siguiente hello:

- Asegúrese de que tiene un entorno x64. plataforma de destino de compilación de Hola y el entorno de prueba de hello debe ser x64, consulte demasiado**paso 1: prueba unitaria de C# crear proyecto y configuración** anteriormente.
- Asegúrese de que ha copiado todos los archivos de dependencia en el directorio de trabajo de NugetPackage\build\runtime\ tooproject.


## <a name="next-steps"></a>Pasos siguientes

* toolearn T-SQL, vea [empezar a trabajar con el lenguaje de Azure Data Lake Analytics U-SQL](data-lake-analytics-u-sql-get-started.md).
* información de diagnóstico de toolog, consulte [acceso a registros de diagnóstico para el análisis de Azure Data Lake](data-lake-analytics-diagnostic-logs.md).
* toosee una consulta más compleja, vea [analizar registros de sitio Web mediante el análisis de Azure Data Lake](data-lake-analytics-analyze-weblogs.md).
* Ver detalles del trabajo tooview, [utilizar un trabajo del explorador y la vista de trabajos de trabajos de análisis de Azure Data Lake](data-lake-analytics-data-lake-tools-view-jobs.md).
* vista de ejecución de toouse Hola vértices, consulte [Hola Use vista de ejecución de vértices de Data Lake Tools para Visual Studio](data-lake-analytics-data-lake-tools-use-vertex-execution-view.md).
