---
title: 'Herramientas de Azure Data Lake: Uso de Herramientas de Azure Data Lake para Visual Studio Code | Microsoft Docs'
description: "Obtenga información acerca de cómo toouse Azure Data Lake Tools para Visual Studio Code toocreate, probar y ejecutar secuencias de comandos SQL U. "
Keywords: "Ruta de acceso de toostorage de carga de VScode, Azure Data Lake Tools, ejecución, depuración Local, depuración Local, archivo de almacenamiento de información de vista previa, Local"
services: data-lake-analytics
documentationcenter: 
author: jejiang
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: dc9b21d8-c5f4-4f77-bcbc-eff458f48de2
ms.service: data-lake-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 07/14/2017
ms.author: jejiang
ms.openlocfilehash: 77771c5d5dae3bfce4ad2df240ea6c6ef848f288
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-data-lake-tools-for-visual-studio-code"></a>Uso de Herramientas de Azure Data Lake para Visual Studio Code

Obtenga información acerca de cómo toouse Azure Data Lake Tools para Visual Studio Code (código de VS) toocreate, probar y ejecutar secuencias de comandos SQL U. También se ofrece información de Hola Hola después de vídeo:

<a href="https://www.youtube.com/watch?v=J_gWuyFnaGA&feature=youtu.be"><img src="./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-video.png"></a>

## <a name="prerequisites"></a>Requisitos previos

Data Lake Tools puede instalarse en plataformas de hello compatibles con VS Code. plataformas de Hello admitido incluyen Windows, Linux y MacOS. plataformas diferentes de Hello tienen Hola siguiendo los requisitos previos:

- Windows

    - [Visual Studio Code]( https://www.visualstudio.com/products/code-vs.aspx).
    - [Java SE Runtime Environment Version 8 Update 77 o posterior](https://java.com/download/manual.jsp). Agregar ruta variables del entorno de sistema de hello java.exe ruta de acceso toohello. Para obtener instrucciones de configuración, consulte [cómo establecer o cambiar la variable del sistema Path Hola?]( https://www.java.com/download/help/path.xml). ruta de acceso de Hello es tooC:\Program Files\Java\jdk1.8.0_77\jre\bin similar.
    - [SDK 1.0.3 de .NET Core o el runtime de .NET Core 1.1](https://www.microsoft.com/net/download).
    
- Linux (se recomienda Ubuntu 14.04 LTS)

    - [Visual Studio Code]( https://www.visualstudio.com/products/code-vs.aspx). tooinstall Hola código, escriba el siguiente comando de hello:

              sudo dpkg -i code_<version_number>_amd64.deb

    - [Mono 4.2.x](http://www.mono-project.com/docs/getting-started/install/linux/). 

        - paquete de tooupdate Hola deb de origen, escriba Hola siguientes comandos:

                sudo apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv-keys 3FA7E0328081BFF6A14DA29AA6A19B38D3D831EF
                echo "deb http://download.mono-project.com/repo/debian wheezy/snapshots 4.2.4.4/main" | sudo tee /etc/apt/sources.list.d/mono-xamarin.list
                sudo apt-get update

        - tooinstall Mono, escriba Hola siguiente comando:

                sudo apt-get install mono-complete

            > [!NOTE] 
            > Mono 4.6 no se admite. Desinstale completamente la versión 4.6 antes de instalar 4.2.x.  

        - [Java SE Runtime Environment Version 8 Update 77 o posterior](https://java.com/download/manual.jsp). Para obtener instrucciones sobre la instalación, vea hello [las instrucciones de instalación de Linux de 64 bits para Java]( https://java.com/en/download/help/linux_x64_install.xml) página.
        - [SDK 1.0.3 de .NET Core o el runtime de .NET Core 1.1](https://www.microsoft.com/net/download).
- MacOS

    - [Visual Studio Code]( https://www.visualstudio.com/products/code-vs.aspx).
    - [Mono 4.2.4](http://download.mono-project.com/archive/4.2.4/macos-10-x86/). 
    - [Java SE Runtime Environment Version 8 Update 77 o posterior](https://java.com/download/manual.jsp). Para obtener instrucciones sobre la instalación, vea hello [las instrucciones de instalación de Linux de 64 bits para Java](https://java.com/en/download/help/mac_install.xml) página.
    - [SDK 1.0.3 de .NET Core o el runtime de .NET Core 1.1](https://www.microsoft.com/net/download).

## <a name="install-data-lake-tools"></a>Instalación de Herramientas de Data Lake

Después de instalar requisitos previos de hello, puede instalar Data Lake Tools para el código de VS.

**tooinstall Data Lake Tools**

1. Abra Visual Studio Code.
2. Seleccione CTRL+p y, a continuación, escriba Hola siguiente comando:
```
ext install usql-vscode-ext
```
Puede ver una lista de extensiones de código de Visual Studio. Una de ellas es **Herramientas de Azure Data Lake**.

3. Seleccione **instalar** siguiente demasiado**Azure Data Lake Tools**. Después de unos segundos, Hola **instalar** botón cambios demasiado**volver a cargar**.
4. Seleccione **recarga** extensión de hello tooactivate.
5. Seleccione **Aceptar** tooconfirm. Puede ver Azure Data Lake Tools Hola **extensiones** panel.
    ![Panel Extensiones de Herramientas de Data Lake para Visual Studio Code](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-extensions.png)

## <a name="activate-azure-data-lake-tools"></a>Activación de Azure Data Lake Tools
Cree un nuevo archivo .usql o abra existente .usql tooactivate Hola extensión de archivo. 

## <a name="connect-tooazure"></a>Conectar tooAzure

Antes de que puede compilar y ejecutar secuencias de comandos de U-SQL de análisis de Data Lake, debe conectar tooyour cuenta de Azure.

**tooconnect tooAzure**

1.  Seleccione Ctrl + Mayús + P tooopen Hola comando paleta. 
2.  Escriba **ADL: Login**. información de inicio de sesión de Hello aparece en hello **salida** panel.

    ![Herramientas de Data Lake para Visual Studio Code: paleta de comandos](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-extension-login.png)
    ![Herramientas de Data Lake para Visual Studio Code: información de inicio de sesión del dispositivo](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-login-info.png)
3. Seleccione Ctrl + clic en la dirección URL de inicio de sesión de hello: página Web de inicio de sesión de https://aka.ms/devicelogin tooopen Hola. Introduzca el código de hello **G567LX42V** en el cuadro de texto de hello y, a continuación, seleccione **continuar**.

   ![Código de inicio de sesión pegado de Herramientas de Data Lake para Visual Studio Code](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-extension-login-paste-code.png )   
4.  Siga toosign de instrucciones de hello en de página Web de Hola. Cuando está conectado, su nombre de cuenta de Azure aparece en la barra de estado de hello en la esquina inferior izquierda de Hola de hello **VS Code** ventana. 

    > [!NOTE] 
    > Si la cuenta tiene habilitada la autenticación de dos pasos, se recomienda usar la autenticación por teléfono en lugar de usar un PIN.

toosign, escriba el comando de hello **ADL: cierre de sesión**.

## <a name="list-your-data-lake-analytics-accounts"></a>Enumeración de las cuentas de Data Lake Analytics

conexión de hello tootest, obtener una lista de las cuentas de análisis de Data Lake.

**cuentas de análisis de Data Lake toolist hello en su suscripción de Azure**

1. Seleccione Ctrl + Mayús + P tooopen Hola comando paleta.
2. Escriba **ADL: List Accounts**. cuentas de Hello aparecen en hello **salida** panel.

## <a name="open-hello-sample-script"></a>Script de ejemplo de Hola abierto
Abrir la paleta de comando hello (Ctrl + Mayús + P) y escriba **ADL: abrir secuencia de comandos de ejemplo**. Con esto se abre otra instancia de este ejemplo. En esta instancia también puede editar, configurar y enviar scripts.

## <a name="work-with-u-sql"></a>Trabajo con U-SQL

Se necesita abrir un archivo U-SQL o una carpeta toowork con U-SQL.

**tooopen una carpeta para el proyecto de SQL U**

1. En el código de Visual Studio, seleccione hello **archivo** menú y, a continuación, seleccione **Abrir carpeta**.
2. Especifique una carpeta y, luego, seleccione **Seleccionar carpeta**.
3. Seleccione hello **archivo** menú y, a continuación, seleccione **nuevo**. Un archivo sin título 1 se agrega el proyecto toohello.
4. Escriba Hola siguiente código en el archivo hello sin título 1:

        @departments  = 
            SELECT * FROM 
                (VALUES
                    (31,    "Sales"),
                    (33,    "Engineering"), 
                    (34,    "Clerical"),
                    (35,    "Marketing")
                ) AS 
                      D( DepID, DepName );
         
        OUTPUT @departments
            TO “/Output/departments.csv”

    script de Hola crea un archivo de departments.csv con algunos datos incluidos en carpeta de Hola/output.

5. Guardar archivo de hello como **myUSQL.usql** Hola abre la carpeta. También se agrega a un archivo de configuración de adltools_settings.json toohello proyecto.
4. Abrir y configurar adltools_settings.json con hello propiedades siguientes:

    - Cuenta: Cuenta de Data Lake Analytics de su suscripción de Azure.
    - Base de datos: Una base de datos en su cuenta. valor predeterminado de Hello es **principal**.
    - Esquema: Un esquema en la base de datos. valor predeterminado de Hello es **dbo**.
    - Configuración opcional:
        - Prioridad: Hola prioridad oscila entre 1 too1000 con 1 como de prioridad más alta de Hola. es el valor predeterminado de Hello **1000**.
        - Paralelismo: Hola paralelismo oscila entre 1 too150. valor predeterminado de Hello es paralelismo máximo Hola permitido en su cuenta de análisis de Data Lake de Azure. 
        
        > [!NOTE] 
        > Si los parámetros de hello son válidos, se usan valores predeterminados de Hola.

    ![Archivo de configuración de Data Lake Tools para Visual Studio Code](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-configuration-file.png)

    Un proceso de análisis de Data Lake cuenta es necesario toocompile y ejecutar los trabajos de SQL U. Debe configurar la cuenta de equipo de hello antes de poder compilar y ejecutar trabajos de SQL U.
    
Después de guarda la configuración de hello, información de cuenta, base de datos y esquema de hello aparece en la barra de estado de hello en la esquina inferior izquierda de Hola Hola .usql del archivo de correspondiente. 
 
 
Tooopening en comparación con un archivo, cuando se abre una carpeta, puede:

- Usar un archivo de código subyacente. En el modo de archivo único de hello, código subyacente no se admite.
- Usar un archivo de configuración. Cuando se abre una carpeta, las secuencias de comandos de Hola Hola carpeta de trabajo comparten un único archivo de configuración.


Hola script U-SQL compila remotamente a través del servicio de análisis de Data Lake Hola. Cuando emita hello **compilar** comando, script U-SQL Hola se envía la cuenta de análisis de Data Lake tooyour. Más adelante, código de Visual Studio recibe el resultado de compilación Hola. Debido a la compilación remoto toohello, código de Visual Studio requiere que se muestra información de hello tooconnect tooyour análisis de Data Lake cuenta en el archivo de configuración de Hola.

**secuencia de comandos de toocompile U T-SQL**

1. Seleccione Ctrl + Mayús + P tooopen Hola comando paleta. 
2. Escriba **ADL: Compile Script**. Hello resultados de compilación aparecen en hello **salida** ventana. Puede también haga clic en un archivo de script y, a continuación, seleccione **ADL: Script de compilación** trabajo toocompile U T-SQL. el resultado de compilación Hola aparece en hello **salida** panel.
 

**secuencia de comandos de toosubmit U T-SQL**

1. Seleccione Ctrl + Mayús + P tooopen Hola comando paleta. 
2. Escriba **ADL: Submit Job**.  También puede hacer clic con el botón derecho en un archivo de script y, luego, seleccionar **ADL: Submit Job**. 

Después de enviar un trabajo de SQL U, registros de envío de hello aparecen en hello **salida** ventana en VS Code. Si el envío de hello es correcto, dirección URL de trabajo de hello aparece también. Puede abrir dirección URL de trabajo de hello en un estado de trabajo en tiempo real de web explorador tootrack Hola.

salida de hello tooenable de detalles del trabajo hello, establezca **jobInformationOutputPath** en hello **frente a código de hello u-sql_settings.json** archivo.
 
## <a name="use-a-code-behind-file"></a>Uso de un archivo de código subyacente

Un archivo de código subyacente es un archivo C# asociado con un solo script U-SQL. Puede definir un script dedicado tooUDO, UDA, UDT y UDF en el archivo de código subyacente de Hola. Hello UDO, UDA, UDT y UDF pueden utilizarse directamente en el script de Hola sin registrar ensamblado de hello en primer lugar. Hello archivo de código subyacente se coloca en hello misma carpeta que su archivo de script SQL U emparejamiento. Si el script de Hola se denomina xxx.usql, código de hello en segundo plano se denomina xxx.usql.cs. Si lo eliminó manualmente el archivo de código subyacente de hello, la característica de código subyacente de hello está deshabilitada para su script U-SQL asociado. Para más información sobre cómo escribir código de cliente para el script U-SQL, consulte [Writing and Using Custom Code in U-SQL – User-Defined Functions]( https://blogs.msdn.microsoft.com/visualstudio/2015/10/28/writing-and-using-custom-code-in-u-sql-user-defined-functions/) (Escritura y uso de código personalizado en U-SQL: funciones definidas por el usuario).

toosupport código subyacente, debe abrir una carpeta de trabajo. 

**toogenerate un archivo de código subyacente**

1. Abra un archivo de origen. 
2. Seleccione Ctrl + Mayús + P tooopen Hola comando paleta.
3. Escriba **ADL: Generate Code Behind**. Se crea un archivo de código subyacente en hello misma carpeta. 

También puede hacer clic con el botón derecho en un archivo de script y, luego, seleccionar **ADL: Generate Code Behind**. 

toocompile y enviar un script U-SQL con un archivo de código subyacente se Hola igual que con hello independiente U-SQL los archivos de scripts.

Hola siguiendo dos capturas de pantalla muestra un archivo de código subyacente y su archivo de script U-SQL asociado:
 
![Herramientas de Data Lake para Visual Studio Code: código subyacente](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-code-behind.png)

![Herramientas de Data Lake para Visual Studio Code: archivo de script de código subyacente](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-code-behind-call.png) 

## <a name="use-assemblies"></a>Uso de ensamblados

Para información sobre el desarrollo de ensamblados, consulte [Desarrollo de ensamblados U-SQL para trabajos de Azure Data Lake Analytics](data-lake-analytics-u-sql-develop-assemblies.md).

Puede usar los ensamblados de código personalizado de Data Lake Tools tooregister en el catálogo de análisis de Data Lake Hola.

**tooregister un ensamblado**

Puede registrar ensamblado de Hola a través de hello **ADL: registrar ensamblado de** o **ADL: registrar el ensamblado a través de la configuración** comandos.

**tooregister a través de hello ADL: registrar agregado (comando)**
1.  Seleccione Ctrl + Mayús + P tooopen Hola comando paleta.
2.  Escriba **ADL: Register Assembly**. 
3.  Especifique la ruta de acceso de ensamblado locales de Hola. 
4.  Seleccione una cuenta de Data Lake Analytics.
5.  Seleccione una base de datos.

Resultados: portal de Hola se abre en un explorador y muestra el proceso de registro del ensamblado de Hola.  

Hola de tootrigger de otra forma cómoda **ADL: registrar ensamblado de** comando es tooright y haga clic en archivo de .dll hello en el Explorador de archivos. 

**tooregister aunque Hola ADL: registrar el ensamblado a través de los comandos de configuración**
1.  Seleccione Ctrl + Mayús + P tooopen Hola comando paleta.
2.  Escriba **ADL: Register Assembly through Configuration**. 
3.  Especifique la ruta de acceso de ensamblado locales de Hola. 
4.  se muestra el archivo JSON de Hello. Revisar y editar las dependencias de ensamblado de Hola y parámetros de recursos, si es necesario. Las instrucciones se muestran en hello **salida** ventana. tooproceed toohello registro de ensamblados, guardar el archivo JSON de hello (CTRL+s).

![Herramientas de Data Lake para Visual Studio Code: código subyacente](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-register-assembly-advance.png)
>[!NOTE]
>- Las dependencias de ensamblado: detecta automáticamente Azure Data Lake Tools si Hola DLL tiene todas las dependencias. dependencias de Hola se muestran en el archivo JSON de hello después de que se detecten. 
>- Recursos: Puede cargar los recursos DLL (por ejemplo, .txt, .png y .csv) como parte del registro de ensamblados de Hola. 

Hola de tootrigger de otra manera **ADL: registrar el ensamblado a través de la configuración** comando es tooright y haga clic en archivo de .dll hello en el Explorador de archivos. 

Hola sigue U-SQL código se muestra cómo toocall un ensamblado. En el ejemplo de Hola, es el nombre del ensamblado de hello *probar*.

```
REFERENCE ASSEMBLY [test];

@a = 
    EXTRACT 
        Iid int,
    Starts DateTime,
    Region string,
    Query string,
    DwellTime int,
    Results string,
    ClickedUrls string 
    FROM @"Sample/SearchLog.txt" 
    USING Extractors.Tsv();

@d =
    SELECT DISTINCT Region 
    FROM @a;

@d1 = 
    PROCESS @d
    PRODUCE 
        Region string,
    Mkt string
    USING new USQLApplication_codebehind.MyProcessor();

OUTPUT @d1 
    too@"Sample/SearchLogtest.txt" 
    USING Outputters.Tsv();
```


## <a name="access-hello-data-lake-analytics-catalog"></a>Catálogo de análisis de Data Lake Hola de acceso

Después de haber conectado tooAzure, puede usar Hola siguiendo el catálogo de hello U-SQL tooaccess de pasos.

**metadatos de análisis de Azure Data Lake hello tooaccess**

1.  Seleccione Ctrl+Mayús+P y, luego, escriba **ADL: List Tables**.
2.  Seleccione una de las cuentas de análisis de Data Lake Hola.
3.  Seleccione una de las bases de datos de análisis de Data Lake de Hola.
4.  Seleccione uno de los esquemas de Hola. Puede ver la lista de Hola de tablas.

## <a name="view-data-lake-analytics-jobs"></a>Vista de los trabajos de Data Lake Analytics

**trabajos de análisis de Data Lake tooview**
1.  Abrir la paleta de comando hello (Ctrl + Mayús + P) y seleccione **ADL: Mostrar trabajo**. 
2.  Seleccione una cuenta de Data Lake Analytics o una cuenta local. 
3.  Espere para lista de trabajos de Hola Hola cuenta tooappear.
4.  Seleccione un trabajo de la lista de trabajos, Data Lake Tools abre los detalles del trabajo de Hola Hola portal de Azure y muestra el archivo JobInfo de hello en VS Code.

![Tipos de objetos de IntelliSense de Data Lake Tools para Visual Studio Code](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-show-job.png)

## <a name="azure-data-lake-storage-integration"></a>Integración de Azure Data Lake Storage

Puede usar comandos relacionados con Azure Data Lake Storage para:
 - Examine los recursos de almacenamiento de Azure datos Lake Hola. 
 - Archivo de almacenamiento de Azure datos Lake hello de vista previa.  
 - Cargar Hola archivo tooAzure Lake el almacenamiento de datos directamente en el código de VS. 

### <a name="list-hello-storage-path"></a>Ruta de acceso de almacenamiento de Hola de lista 
Puede mostrar la ruta de acceso de almacenamiento de Hola a través de la paleta de comando de Hola o menú contextual.

**ruta de acceso de almacenamiento de toolist Hola a través de la paleta de comando hello**

1.  Abrir la paleta de comando hello (Ctrl + Mayús + P) y escriba **ADL: ruta de acceso de almacenamiento de lista**.

    ![Herramientas de Data Lake para Visual Studio Code: enumerar la ruta de acceso de almacenamiento](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-list-storage.png)

2.  Seleccione la forma preferida para enumerar la ruta de acceso de almacenamiento de Hola. En este paso se usa **Enter a path** (Escribir una ruta de acceso) como ejemplo.

    ![Data Lake Tools para Visual Studio Code ruta de acceso de almacenamiento de una manera toolist Hola](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-list-account-selectoneway.png)

    > [!NOTE]
    >- FRENTE a código mantiene la ruta de acceso de hello visitado por el último en cada cuenta de análisis de Data Lake. Por ejemplo: /tt/ss.
    >- Explorador de ruta de acceso raíz: ruta de raíz de la lista de Hola desde su cuenta de análisis de Data Lake seleccionada o una ruta de acceso local.
    >- Enter a path (Escribir una ruta de acceso): indica una ruta de acceso especificada desde la cuenta de Data Lake Analytics seleccionada o una ruta de acceso local.
    
3. Seleccione una cuenta de la ruta de acceso local de Hola o una cuenta de análisis de Data Lake.

    ![Más selecciones de Herramientas de Data Lake para Visual Studio Code](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-list-account.png)

4. Seleccione **más** toolist más cuentas de análisis de Data Lake y, a continuación, seleccione una cuenta de análisis de Data Lake.

    ![Herramientas de Data Lake para Visual Studio Code: selección de una cuenta](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-select-adla-account.png)

5.  Escriba una ruta de acceso de almacenamiento de Azure. Por ejemplo, /output.

    ![Herramientas de Data Lake para Visual Studio Code: escribir la ruta de acceso de almacenamiento](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-input-path.png)

6.  Resultados: paleta de hello comando muestra información de ruta de acceso de hello en función de las entradas.

    ![Herramientas de Data Lake para Visual Studio Code: enumerar los resultados de la ruta de acceso de almacenamiento](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-list-path.png)

Una manera más conveniente de ruta de acceso relativa de toolist hello es a través de hello haga clic en el menú contextual.

**Pulse el botón derecho en la ruta de acceso de almacenamiento de toolist Hola a través de**

1.  Haga clic en tooselect de cadena de ruta de acceso de hello **ruta de acceso de almacenamiento de lista**.

       ![Herramientas de Data Lake para Visual Studio Code: menú contextual](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-right-click-path.png)

2. ruta de acceso relativa Hola seleccionado aparece en la paleta de comando Hola.

   ![Herramientas de Data Lake para Visual Studio Code: ruta de acceso relativa seleccionada](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-list-relative-path.png)

3.  Seleccione una cuenta de la ruta de acceso local de Hola o una cuenta de análisis de Data Lake.

       ![Herramientas de Data Lake para Visual Studio Code: selección de una cuenta](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-list-account.png)

4.  Resultados: listas de paleta de comando Hola Hola carpetas y archivos para la ruta de acceso actual de Hola.

       ![Data Lake Tools para lista de código de Visual Studio desde la ruta de acceso actual de Hola](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-list-current.png)

### <a name="preview-hello-storage-file"></a>Archivo de almacenamiento de hello de vista previa
Puede obtener una vista previa de archivo de almacenamiento de hello a través de la paleta de comando de Hola o menú contextual.

**archivo de almacenamiento de hello toopreview a través de la paleta de comando hello**

1.  Abrir la paleta de comando hello (Ctrl + Mayús + P) y escriba **ADL: vista previa de un archivo de almacenamiento**.

       ![Herramientas de Data Lake para Visual Studio Code: vista previa del archivo de almacenamiento](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-list-preview.png)

2.  Seleccione una cuenta de la ruta de acceso local de Hola o una cuenta de análisis de Data Lake.

       ![Herramientas de Data Lake para Visual Studio Code: enumerar cuentas](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-list-account.png)

3.  Seleccione **más** toolist más cuentas de análisis de Data Lake y, a continuación, seleccione una cuenta de análisis de Data Lake.

       ![Herramientas de Data Lake para Visual Studio Code: selección de una cuenta](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-select-adla-account.png)

4.  Escriba un archivo o ruta de almacenamiento de Azure. Por ejemplo, /output/SearchLog.txt.

       ![Herramientas de Data Lake para Visual Studio Code: escribir el archivo y la ruta de acceso de almacenamiento](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-input-preview-file.png)

5.  Resultados: paleta de hello comando muestra información de ruta de acceso de hello en función de las entradas.

       ![Herramientas de Data Lake para Visual Studio Code: resultado de la vista previa de archivo](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-preview-results.png)

**Pulse el botón derecho en la ruta de acceso de almacenamiento de toolist Hola a través de**

1.  toopreview un archivo, haga clic en la ruta de acceso de archivo Hola.

   ![Herramientas de Data Lake para Visual Studio Code: menú contextual](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-right-click-preview.png) 

2.  Seleccione una cuenta de la ruta de acceso local de Hola o una cuenta de análisis de Data Lake.

       ![Herramientas de Data Lake para Visual Studio Code: selección de una cuenta](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-list-account.png)

3.  Resultados: VS Code muestra resultados de vista previa de Hola de archivo hello.

       ![Herramientas de Data Lake para Visual Studio Code: resultado de la vista previa de archivo](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-preview-results.png)

### <a name="upload-a-file"></a>Cargar un archivo 

Puede cargar archivos escribiendo comandos de hello **ADL: cargar archivo** o **ADL: cargar archivo de configuración**.

**archivos de tooupload aunque Hola ADL: cargar archivo (comando)**
1. Seleccione Ctrl + Mayús + P tooopen Hola comando paleta o haga clic en editor de script de Hola y, a continuación, escriba **cargar archivo**.
2.  Hola tooupload de archivo, escriba una ruta de acceso local.

    ![Herramientas de Data Lake para Visual Studio Code: escribir la ruta de acceso local](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-auto-input-local-path.png)

3. Seleccione una de las formas de Hola de ruta de acceso de almacenamiento de anuncio Hola. En este paso se usa **Enter a path** (Escribir una ruta de acceso) como ejemplo.

    ![Herramientas de Data Lake para Visual Studio Code: enumerar la ruta de acceso de almacenamiento](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-list-account-selectoneway.png)
    >[!NOTE]
    >- FRENTE a código mantiene la ruta de acceso de hello visitado por el último en cada cuenta de análisis de Data Lake. Por ejemplo: /tt/ss.
    >- Explorador de ruta de acceso raíz: ruta de raíz de la lista de Hola desde su cuenta de análisis de Data Lake seleccionada o una ruta de acceso local.
    >- Enter a path (Escribir una ruta de acceso): indica una ruta de acceso especificada desde la cuenta de Data Lake Analytics seleccionada o una ruta de acceso local.

4. Seleccione una cuenta de la ruta de acceso local de Hola o una cuenta de análisis de Data Lake.

    ![Herramientas de Data Lake Tools para Visual Studio Code: clic derecho en almacenamiento](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-list-account.png)

5. Escriba una ruta de acceso de almacenamiento de Azure. Por ejemplo: /output.

       ![Data Lake Tools for Visual Studio Code enter storage path](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-input-preview-file.png)

6. Busque la ruta de acceso de almacenamiento de Azure. Seleccione **Choose current folder** (Elegir carpeta actual).

    ![Herramientas de Data Lake para Visual Studio Code: selección de una carpeta](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-choose-current-folder.png)

7.  Resultados: Hola **salida** ventana muestra el estado de carga del archivo de Hola.

       ![Herramientas de Data Lake para Visual Studio Code: estado de carga](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-upload-status.png)    

**archivos de tooupload aunque Hola ADL: cargar archivos a través de los comandos de configuración**
1.  Seleccione Ctrl + Mayús + P tooopen Hola comando paleta o haga clic en editor de script de Hola y, a continuación, escriba **cargar archivo de configuración**.
2.  VS Code muestra un archivo JSON. Puede especificar las rutas de acceso de archivo y cargar varios archivos en hello mismo tiempo. Las instrucciones se muestran en hello **salida** ventana. tooproceed tooupload archivo hello, guardar el archivo JSON de hello (CTRL+s).

       ![Herramientas de Data Lake para Visual Studio Code: ruta de acceso de archivo](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-upload-file.png)

3.  Resultados: Hola **salida** ventana muestra el estado de carga del archivo de Hola.

       ![Herramientas de Data Lake para Visual Studio Code: estado de carga](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-upload-status.png)     

Otro tooupload de manera un archivo toostorage es a través de Hola haga clic en el menú en la ruta de acceso completa del archivo de Hola o ruta de acceso relativa del archivo de hello en el editor de script de Hola. Escriba la ruta de acceso de archivo local de hello y, a continuación, seleccione la cuenta de hello. Hola **salida** ventana muestra el estado de la carga de Hola. 

### <a name="open-azure-storage-explorer"></a>Apertura del Explorador de Azure Storage
Puede abrir **Azure Storage Explorer** escribiendo el comando hello **ADL: Abrir Explorador de almacenamiento de Azure Web** o mediante la selección de menú contextual Hola.

**tooopen Explorador de almacenamiento de Azure**

1. Seleccione Ctrl + Mayús + P tooopen Hola comando paleta.
2. Escriba **Abrir Explorador de almacenamiento de Azure Web** o haga doble clic en una ruta de acceso relativa o la ruta de acceso completa de hello en el editor de secuencia de comandos de hello y, a continuación, seleccione **Abrir Explorador de almacenamiento de Azure Web**.
3. Seleccione una cuenta de Data Lake Analytics.

Data Lake Tools abre la ruta de acceso de almacenamiento de Azure de hello en hello portal de Azure. Puede encontrar archivo de Hola de hello ruta de acceso y la vista previa de web de Hola.

### <a name="local-run-and-local-debug-for-windows-users"></a>Ejecución y depuración locales de usuarios de Windows
Ejecución local de SQL U comprueba los datos locales y valida el script localmente, antes de que el código sea publicada tooData Lake Analytics. Hola característica de depuración local permite toocomplete Hola siguiente las tareas antes de que el código envía tooData Lake Analytics: 
- Depure el código subyacente de C#. 
- Recorrer el código de hello. 
- Valide localmente el script.

Para instrucciones sobre la ejecución y la depuración locales, consulte [Ejecución y depuración locales de U-SQL con Visual Studio Code](data-lake-tools-for-vscode-local-run-and-debug.md).

## <a name="additional-features"></a>Características adicionales

Data Lake Tools para VS Code admite Hola siguientes características:

-   Autocompletar de IntelliSense: aparecen sugerencias en ventanas emergentes en torno a elementos, como palabras clave, métodos y variables. Los distintos iconos representan diferentes tipos de objetos de hello:

    - Tipo de datos de escala
    - Tipo de datos complejo
    - UDT integrada
    - Clases y colección .NET
    - Expresiones de C#
    - UDF, UDO y UDAAG integrados de C# 
    - Funciones de U-SQL
    - Función de ventana de U-SQL
 
    ![Tipos de objetos de IntelliSense de Data Lake Tools para Visual Studio Code](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-auto-complete-objects.png)
 
-   IntelliSense Autocompletar en metadatos de análisis de Data Lake: Data Lake Tools descarga información de metadatos de análisis de Data Lake de hello localmente. característica de IntelliSense de Hello rellena automáticamente los objetos, incluida la base de datos de hello, esquema, tabla, vista, función con valores de tabla, procedimientos y ensamblados de C#, de los metadatos de análisis de Data Lake Hola.
 
    ![Metadatos de IntelliSense de Data Lake Tools para Visual Studio Code](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-auto-complete-metastore.png)

-   Marcador de error de IntelliSense: Data Lake Tools subraya Hola editar errores de SQL de U y C#. 
-   Resaltado de sintaxis: Data Lake Tools usa elementos de toodifferentiate de distintos colores, como las variables, palabras clave, tipo de datos y funciones. 

    ![Aspectos destacados de la sintaxis de Data Lake Tools para Visual Studio Code](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-syntax-highlights.png)

## <a name="next-steps"></a>Pasos siguientes

- Para la ejecución y depuración locales de U-SQL con Visual Studio Code, consulte [Ejecución y depuración locales de U-SQL con Visual Studio Code](data-lake-tools-for-vscode-local-run-and-debug.md).
- Para información detallada sobre cómo empezar a trabajar con Data Lake Analytics, consulte [Tutorial: Introducción a Azure Data Lake Analytics](data-lake-analytics-get-started-portal.md).
- Para información sobre Herramientas de Data Lake para Visual Studio, consulte [Tutorial: Desarrollo de scripts U-SQL mediante Herramientas de Data Lake para Visual Studio](data-lake-analytics-data-lake-tools-get-started.md).
- Para información sobre el desarrollo de ensamblados, consulte [Desarrollo de ensamblados U-SQL para trabajos de Azure Data Lake Analytics](data-lake-analytics-u-sql-develop-assemblies.md).



