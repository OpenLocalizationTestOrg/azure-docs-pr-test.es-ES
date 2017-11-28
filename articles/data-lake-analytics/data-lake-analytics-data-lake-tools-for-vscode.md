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
# <a name="use-azure-data-lake-tools-for-visual-studio-code"></a><span data-ttu-id="1d2b8-104">Uso de Herramientas de Azure Data Lake para Visual Studio Code</span><span class="sxs-lookup"><span data-stu-id="1d2b8-104">Use Azure Data Lake Tools for Visual Studio Code</span></span>

<span data-ttu-id="1d2b8-105">Obtenga información acerca de cómo toouse Azure Data Lake Tools para Visual Studio Code (código de VS) toocreate, probar y ejecutar secuencias de comandos SQL U.</span><span class="sxs-lookup"><span data-stu-id="1d2b8-105">Learn how toouse Azure Data Lake Tools for Visual Studio Code (VS Code) toocreate, test, and run U-SQL scripts.</span></span> <span data-ttu-id="1d2b8-106">También se ofrece información de Hola Hola después de vídeo:</span><span class="sxs-lookup"><span data-stu-id="1d2b8-106">hello information is also covered in hello following video:</span></span>

<a href="https://www.youtube.com/watch?v=J_gWuyFnaGA&feature=youtu.be"><img src="./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-video.png"></a>

## <a name="prerequisites"></a><span data-ttu-id="1d2b8-107">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="1d2b8-107">Prerequisites</span></span>

<span data-ttu-id="1d2b8-108">Data Lake Tools puede instalarse en plataformas de hello compatibles con VS Code.</span><span class="sxs-lookup"><span data-stu-id="1d2b8-108">Data Lake Tools can be installed on hello platforms supported by VS Code.</span></span> <span data-ttu-id="1d2b8-109">plataformas de Hello admitido incluyen Windows, Linux y MacOS.</span><span class="sxs-lookup"><span data-stu-id="1d2b8-109">hello supported platforms include Windows, Linux, and MacOS.</span></span> <span data-ttu-id="1d2b8-110">plataformas diferentes de Hello tienen Hola siguiendo los requisitos previos:</span><span class="sxs-lookup"><span data-stu-id="1d2b8-110">hello different platforms have hello following prerequisites:</span></span>

- <span data-ttu-id="1d2b8-111">Windows</span><span class="sxs-lookup"><span data-stu-id="1d2b8-111">Windows</span></span>

    - <span data-ttu-id="1d2b8-112">[Visual Studio Code]( https://www.visualstudio.com/products/code-vs.aspx).</span><span class="sxs-lookup"><span data-stu-id="1d2b8-112">[Visual Studio Code]( https://www.visualstudio.com/products/code-vs.aspx).</span></span>
    - <span data-ttu-id="1d2b8-113">[Java SE Runtime Environment Version 8 Update 77 o posterior](https://java.com/download/manual.jsp).</span><span class="sxs-lookup"><span data-stu-id="1d2b8-113">[Java SE Runtime Environment version 8 update 77 or later](https://java.com/download/manual.jsp).</span></span> <span data-ttu-id="1d2b8-114">Agregar ruta variables del entorno de sistema de hello java.exe ruta de acceso toohello.</span><span class="sxs-lookup"><span data-stu-id="1d2b8-114">Add hello java.exe path toohello system environment variable path.</span></span> <span data-ttu-id="1d2b8-115">Para obtener instrucciones de configuración, consulte [cómo establecer o cambiar la variable del sistema Path Hola?]( https://www.java.com/download/help/path.xml).</span><span class="sxs-lookup"><span data-stu-id="1d2b8-115">For configuration instructions, see [How do I set or change hello Path system variable?]( https://www.java.com/download/help/path.xml).</span></span> <span data-ttu-id="1d2b8-116">ruta de acceso de Hello es tooC:\Program Files\Java\jdk1.8.0_77\jre\bin similar.</span><span class="sxs-lookup"><span data-stu-id="1d2b8-116">hello path is similar tooC:\Program Files\Java\jdk1.8.0_77\jre\bin.</span></span>
    - <span data-ttu-id="1d2b8-117">[SDK 1.0.3 de .NET Core o el runtime de .NET Core 1.1](https://www.microsoft.com/net/download).</span><span class="sxs-lookup"><span data-stu-id="1d2b8-117">[.NET Core SDK 1.0.3 or .NET Core 1.1 runtime](https://www.microsoft.com/net/download).</span></span>
    
- <span data-ttu-id="1d2b8-118">Linux (se recomienda Ubuntu 14.04 LTS)</span><span class="sxs-lookup"><span data-stu-id="1d2b8-118">Linux (We recommend Ubuntu 14.04 LTS)</span></span>

    - <span data-ttu-id="1d2b8-119">[Visual Studio Code]( https://www.visualstudio.com/products/code-vs.aspx).</span><span class="sxs-lookup"><span data-stu-id="1d2b8-119">[Visual Studio Code]( https://www.visualstudio.com/products/code-vs.aspx).</span></span> <span data-ttu-id="1d2b8-120">tooinstall Hola código, escriba el siguiente comando de hello:</span><span class="sxs-lookup"><span data-stu-id="1d2b8-120">tooinstall hello code, enter hello following command:</span></span>

              sudo dpkg -i code_<version_number>_amd64.deb

    - <span data-ttu-id="1d2b8-121">[Mono 4.2.x](http://www.mono-project.com/docs/getting-started/install/linux/).</span><span class="sxs-lookup"><span data-stu-id="1d2b8-121">[Mono 4.2.x](http://www.mono-project.com/docs/getting-started/install/linux/).</span></span> 

        - <span data-ttu-id="1d2b8-122">paquete de tooupdate Hola deb de origen, escriba Hola siguientes comandos:</span><span class="sxs-lookup"><span data-stu-id="1d2b8-122">tooupdate hello deb package source, enter hello following commands:</span></span>

                sudo apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv-keys 3FA7E0328081BFF6A14DA29AA6A19B38D3D831EF
                echo "deb http://download.mono-project.com/repo/debian wheezy/snapshots 4.2.4.4/main" | sudo tee /etc/apt/sources.list.d/mono-xamarin.list
                sudo apt-get update

        - <span data-ttu-id="1d2b8-123">tooinstall Mono, escriba Hola siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="1d2b8-123">tooinstall Mono, enter hello following command:</span></span>

                sudo apt-get install mono-complete

            > [!NOTE] 
            > <span data-ttu-id="1d2b8-124">Mono 4.6 no se admite.</span><span class="sxs-lookup"><span data-stu-id="1d2b8-124">Mono 4.6 is not supported.</span></span> <span data-ttu-id="1d2b8-125">Desinstale completamente la versión 4.6 antes de instalar 4.2.x.</span><span class="sxs-lookup"><span data-stu-id="1d2b8-125">Uninstall version 4.6 entirely before you install 4.2.x.</span></span>  

        - <span data-ttu-id="1d2b8-126">[Java SE Runtime Environment Version 8 Update 77 o posterior](https://java.com/download/manual.jsp).</span><span class="sxs-lookup"><span data-stu-id="1d2b8-126">[Java SE Runtime Environment version 8 update 77 or later](https://java.com/download/manual.jsp).</span></span> <span data-ttu-id="1d2b8-127">Para obtener instrucciones sobre la instalación, vea hello [las instrucciones de instalación de Linux de 64 bits para Java]( https://java.com/en/download/help/linux_x64_install.xml) página.</span><span class="sxs-lookup"><span data-stu-id="1d2b8-127">For instructions on installation, see hello [Linux 64-bit installation instructions for Java]( https://java.com/en/download/help/linux_x64_install.xml) page.</span></span>
        - <span data-ttu-id="1d2b8-128">[SDK 1.0.3 de .NET Core o el runtime de .NET Core 1.1](https://www.microsoft.com/net/download).</span><span class="sxs-lookup"><span data-stu-id="1d2b8-128">[.NET Core SDK 1.0.3 or .NET Core 1.1 runtime](https://www.microsoft.com/net/download).</span></span>
- <span data-ttu-id="1d2b8-129">MacOS</span><span class="sxs-lookup"><span data-stu-id="1d2b8-129">MacOS</span></span>

    - <span data-ttu-id="1d2b8-130">[Visual Studio Code]( https://www.visualstudio.com/products/code-vs.aspx).</span><span class="sxs-lookup"><span data-stu-id="1d2b8-130">[Visual Studio Code]( https://www.visualstudio.com/products/code-vs.aspx).</span></span>
    - <span data-ttu-id="1d2b8-131">[Mono 4.2.4](http://download.mono-project.com/archive/4.2.4/macos-10-x86/).</span><span class="sxs-lookup"><span data-stu-id="1d2b8-131">[Mono 4.2.4](http://download.mono-project.com/archive/4.2.4/macos-10-x86/).</span></span> 
    - <span data-ttu-id="1d2b8-132">[Java SE Runtime Environment Version 8 Update 77 o posterior](https://java.com/download/manual.jsp).</span><span class="sxs-lookup"><span data-stu-id="1d2b8-132">[Java SE Runtime Environment version 8 update 77 or later](https://java.com/download/manual.jsp).</span></span> <span data-ttu-id="1d2b8-133">Para obtener instrucciones sobre la instalación, vea hello [las instrucciones de instalación de Linux de 64 bits para Java](https://java.com/en/download/help/mac_install.xml) página.</span><span class="sxs-lookup"><span data-stu-id="1d2b8-133">For instructions on installation, see hello [Linux 64-bit installation instructions for Java](https://java.com/en/download/help/mac_install.xml) page.</span></span>
    - <span data-ttu-id="1d2b8-134">[SDK 1.0.3 de .NET Core o el runtime de .NET Core 1.1](https://www.microsoft.com/net/download).</span><span class="sxs-lookup"><span data-stu-id="1d2b8-134">[.NET Core SDK 1.0.3 or .NET Core 1.1 runtime](https://www.microsoft.com/net/download).</span></span>

## <a name="install-data-lake-tools"></a><span data-ttu-id="1d2b8-135">Instalación de Herramientas de Data Lake</span><span class="sxs-lookup"><span data-stu-id="1d2b8-135">Install Data Lake Tools</span></span>

<span data-ttu-id="1d2b8-136">Después de instalar requisitos previos de hello, puede instalar Data Lake Tools para el código de VS.</span><span class="sxs-lookup"><span data-stu-id="1d2b8-136">After you install hello prerequisites, you can install Data Lake Tools for VS Code.</span></span>

<span data-ttu-id="1d2b8-137">**tooinstall Data Lake Tools**</span><span class="sxs-lookup"><span data-stu-id="1d2b8-137">**tooinstall Data Lake Tools**</span></span>

1. <span data-ttu-id="1d2b8-138">Abra Visual Studio Code.</span><span class="sxs-lookup"><span data-stu-id="1d2b8-138">Open Visual Studio Code.</span></span>
2. <span data-ttu-id="1d2b8-139">Seleccione CTRL+p y, a continuación, escriba Hola siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="1d2b8-139">Select Ctrl+P, and then enter hello following command:</span></span>
```
ext install usql-vscode-ext
```
<span data-ttu-id="1d2b8-140">Puede ver una lista de extensiones de código de Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="1d2b8-140">You can see a list of Visual Studio code extensions.</span></span> <span data-ttu-id="1d2b8-141">Una de ellas es **Herramientas de Azure Data Lake**.</span><span class="sxs-lookup"><span data-stu-id="1d2b8-141">One of them is **Azure Data Lake Tools**.</span></span>

3. <span data-ttu-id="1d2b8-142">Seleccione **instalar** siguiente demasiado**Azure Data Lake Tools**.</span><span class="sxs-lookup"><span data-stu-id="1d2b8-142">Select **Install** next too**Azure Data Lake Tools**.</span></span> <span data-ttu-id="1d2b8-143">Después de unos segundos, Hola **instalar** botón cambios demasiado**volver a cargar**.</span><span class="sxs-lookup"><span data-stu-id="1d2b8-143">After a few seconds, hello **Install** button changes too**Reload**.</span></span>
4. <span data-ttu-id="1d2b8-144">Seleccione **recarga** extensión de hello tooactivate.</span><span class="sxs-lookup"><span data-stu-id="1d2b8-144">Select **Reload** tooactivate hello extension.</span></span>
5. <span data-ttu-id="1d2b8-145">Seleccione **Aceptar** tooconfirm.</span><span class="sxs-lookup"><span data-stu-id="1d2b8-145">Select **OK** tooconfirm.</span></span> <span data-ttu-id="1d2b8-146">Puede ver Azure Data Lake Tools Hola **extensiones** panel.</span><span class="sxs-lookup"><span data-stu-id="1d2b8-146">You can see Azure Data Lake Tools in hello **Extensions** pane.</span></span>
    <span data-ttu-id="1d2b8-147">![Panel Extensiones de Herramientas de Data Lake para Visual Studio Code](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-extensions.png)</span><span class="sxs-lookup"><span data-stu-id="1d2b8-147">![Data Lake Tools for Visual Studio Code Extensions pane](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-extensions.png)</span></span>

## <a name="activate-azure-data-lake-tools"></a><span data-ttu-id="1d2b8-148">Activación de Azure Data Lake Tools</span><span class="sxs-lookup"><span data-stu-id="1d2b8-148">Activate Azure Data Lake Tools</span></span>
<span data-ttu-id="1d2b8-149">Cree un nuevo archivo .usql o abra existente .usql tooactivate Hola extensión de archivo.</span><span class="sxs-lookup"><span data-stu-id="1d2b8-149">Create a new .usql file or open an existing .usql file tooactivate hello extension.</span></span> 

## <a name="connect-tooazure"></a><span data-ttu-id="1d2b8-150">Conectar tooAzure</span><span class="sxs-lookup"><span data-stu-id="1d2b8-150">Connect tooAzure</span></span>

<span data-ttu-id="1d2b8-151">Antes de que puede compilar y ejecutar secuencias de comandos de U-SQL de análisis de Data Lake, debe conectar tooyour cuenta de Azure.</span><span class="sxs-lookup"><span data-stu-id="1d2b8-151">Before you can compile and run U-SQL scripts in Data Lake Analytics, you must connect tooyour Azure account.</span></span>

<span data-ttu-id="1d2b8-152">**tooconnect tooAzure**</span><span class="sxs-lookup"><span data-stu-id="1d2b8-152">**tooconnect tooAzure**</span></span>

1.  <span data-ttu-id="1d2b8-153">Seleccione Ctrl + Mayús + P tooopen Hola comando paleta.</span><span class="sxs-lookup"><span data-stu-id="1d2b8-153">Select Ctrl+Shift+P tooopen hello command palette.</span></span> 
2.  <span data-ttu-id="1d2b8-154">Escriba **ADL: Login**.</span><span class="sxs-lookup"><span data-stu-id="1d2b8-154">Enter **ADL: Login**.</span></span> <span data-ttu-id="1d2b8-155">información de inicio de sesión de Hello aparece en hello **salida** panel.</span><span class="sxs-lookup"><span data-stu-id="1d2b8-155">hello login information appears in hello **Output** pane.</span></span>

    <span data-ttu-id="1d2b8-156">![Herramientas de Data Lake para Visual Studio Code: paleta de comandos](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-extension-login.png)
    ![Herramientas de Data Lake para Visual Studio Code: información de inicio de sesión del dispositivo](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-login-info.png)</span><span class="sxs-lookup"><span data-stu-id="1d2b8-156">![Data Lake Tools for Visual Studio Code command palette](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-extension-login.png)
![Data Lake Tools for Visual Studio Code device login information](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-login-info.png)</span></span>
3. <span data-ttu-id="1d2b8-157">Seleccione Ctrl + clic en la dirección URL de inicio de sesión de hello: página Web de inicio de sesión de https://aka.ms/devicelogin tooopen Hola.</span><span class="sxs-lookup"><span data-stu-id="1d2b8-157">Select Ctrl+click on hello login URL: https://aka.ms/devicelogin tooopen hello login webpage.</span></span> <span data-ttu-id="1d2b8-158">Introduzca el código de hello **G567LX42V** en el cuadro de texto de hello y, a continuación, seleccione **continuar**.</span><span class="sxs-lookup"><span data-stu-id="1d2b8-158">Enter hello code **G567LX42V** into hello text box, and then select **Continue**.</span></span>

   ![Código de inicio de sesión pegado de Herramientas de Data Lake para Visual Studio Code](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-extension-login-paste-code.png )   
4.  <span data-ttu-id="1d2b8-160">Siga toosign de instrucciones de hello en de página Web de Hola.</span><span class="sxs-lookup"><span data-stu-id="1d2b8-160">Follow hello instructions toosign in from hello webpage.</span></span> <span data-ttu-id="1d2b8-161">Cuando está conectado, su nombre de cuenta de Azure aparece en la barra de estado de hello en la esquina inferior izquierda de Hola de hello **VS Code** ventana.</span><span class="sxs-lookup"><span data-stu-id="1d2b8-161">When you're connected, your Azure account name appears on hello status bar in hello lower-left corner of hello **VS Code** window.</span></span> 

    > [!NOTE] 
    > <span data-ttu-id="1d2b8-162">Si la cuenta tiene habilitada la autenticación de dos pasos, se recomienda usar la autenticación por teléfono en lugar de usar un PIN.</span><span class="sxs-lookup"><span data-stu-id="1d2b8-162">If your account has two factors enabled, we recommend that you use phone authentication rather than using a PIN.</span></span>

<span data-ttu-id="1d2b8-163">toosign, escriba el comando de hello **ADL: cierre de sesión**.</span><span class="sxs-lookup"><span data-stu-id="1d2b8-163">toosign out, enter hello command **ADL: Logout**.</span></span>

## <a name="list-your-data-lake-analytics-accounts"></a><span data-ttu-id="1d2b8-164">Enumeración de las cuentas de Data Lake Analytics</span><span class="sxs-lookup"><span data-stu-id="1d2b8-164">List your Data Lake Analytics accounts</span></span>

<span data-ttu-id="1d2b8-165">conexión de hello tootest, obtener una lista de las cuentas de análisis de Data Lake.</span><span class="sxs-lookup"><span data-stu-id="1d2b8-165">tootest hello connection, get a list of your Data Lake Analytics accounts.</span></span>

<span data-ttu-id="1d2b8-166">**cuentas de análisis de Data Lake toolist hello en su suscripción de Azure**</span><span class="sxs-lookup"><span data-stu-id="1d2b8-166">**toolist hello Data Lake Analytics accounts under your Azure subscription**</span></span>

1. <span data-ttu-id="1d2b8-167">Seleccione Ctrl + Mayús + P tooopen Hola comando paleta.</span><span class="sxs-lookup"><span data-stu-id="1d2b8-167">Select Ctrl+Shift+P tooopen hello command palette.</span></span>
2. <span data-ttu-id="1d2b8-168">Escriba **ADL: List Accounts**.</span><span class="sxs-lookup"><span data-stu-id="1d2b8-168">Enter **ADL: List Accounts**.</span></span> <span data-ttu-id="1d2b8-169">cuentas de Hello aparecen en hello **salida** panel.</span><span class="sxs-lookup"><span data-stu-id="1d2b8-169">hello accounts appear in hello **Output** pane.</span></span>

## <a name="open-hello-sample-script"></a><span data-ttu-id="1d2b8-170">Script de ejemplo de Hola abierto</span><span class="sxs-lookup"><span data-stu-id="1d2b8-170">Open hello sample script</span></span>
<span data-ttu-id="1d2b8-171">Abrir la paleta de comando hello (Ctrl + Mayús + P) y escriba **ADL: abrir secuencia de comandos de ejemplo**.</span><span class="sxs-lookup"><span data-stu-id="1d2b8-171">Open hello command palette (Ctrl+Shift+P) and enter **ADL: Open Sample Script**.</span></span> <span data-ttu-id="1d2b8-172">Con esto se abre otra instancia de este ejemplo.</span><span class="sxs-lookup"><span data-stu-id="1d2b8-172">This opens another instance of this sample.</span></span> <span data-ttu-id="1d2b8-173">En esta instancia también puede editar, configurar y enviar scripts.</span><span class="sxs-lookup"><span data-stu-id="1d2b8-173">You can also edit, configure, and submit script on this instance.</span></span>

## <a name="work-with-u-sql"></a><span data-ttu-id="1d2b8-174">Trabajo con U-SQL</span><span class="sxs-lookup"><span data-stu-id="1d2b8-174">Work with U-SQL</span></span>

<span data-ttu-id="1d2b8-175">Se necesita abrir un archivo U-SQL o una carpeta toowork con U-SQL.</span><span class="sxs-lookup"><span data-stu-id="1d2b8-175">You need open either a U-SQL file or a folder toowork with U-SQL.</span></span>

<span data-ttu-id="1d2b8-176">**tooopen una carpeta para el proyecto de SQL U**</span><span class="sxs-lookup"><span data-stu-id="1d2b8-176">**tooopen a folder for your U-SQL project**</span></span>

1. <span data-ttu-id="1d2b8-177">En el código de Visual Studio, seleccione hello **archivo** menú y, a continuación, seleccione **Abrir carpeta**.</span><span class="sxs-lookup"><span data-stu-id="1d2b8-177">From Visual Studio Code, select hello **File** menu, and then select **Open Folder**.</span></span>
2. <span data-ttu-id="1d2b8-178">Especifique una carpeta y, luego, seleccione **Seleccionar carpeta**.</span><span class="sxs-lookup"><span data-stu-id="1d2b8-178">Specify a folder, and then select **Select Folder**.</span></span>
3. <span data-ttu-id="1d2b8-179">Seleccione hello **archivo** menú y, a continuación, seleccione **nuevo**.</span><span class="sxs-lookup"><span data-stu-id="1d2b8-179">Select hello **File** menu, and then select **New**.</span></span> <span data-ttu-id="1d2b8-180">Un archivo sin título 1 se agrega el proyecto toohello.</span><span class="sxs-lookup"><span data-stu-id="1d2b8-180">An Untitled-1 file is added toohello project.</span></span>
4. <span data-ttu-id="1d2b8-181">Escriba Hola siguiente código en el archivo hello sin título 1:</span><span class="sxs-lookup"><span data-stu-id="1d2b8-181">Enter hello following code into hello Untitled-1 file:</span></span>

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

    <span data-ttu-id="1d2b8-182">script de Hola crea un archivo de departments.csv con algunos datos incluidos en carpeta de Hola/output.</span><span class="sxs-lookup"><span data-stu-id="1d2b8-182">hello script creates a departments.csv file with some data included in hello /output folder.</span></span>

5. <span data-ttu-id="1d2b8-183">Guardar archivo de hello como **myUSQL.usql** Hola abre la carpeta.</span><span class="sxs-lookup"><span data-stu-id="1d2b8-183">Save hello file as **myUSQL.usql** in hello opened folder.</span></span> <span data-ttu-id="1d2b8-184">También se agrega a un archivo de configuración de adltools_settings.json toohello proyecto.</span><span class="sxs-lookup"><span data-stu-id="1d2b8-184">A adltools_settings.json configuration file is also added toohello project.</span></span>
4. <span data-ttu-id="1d2b8-185">Abrir y configurar adltools_settings.json con hello propiedades siguientes:</span><span class="sxs-lookup"><span data-stu-id="1d2b8-185">Open and configure adltools_settings.json with hello following properties:</span></span>

    - <span data-ttu-id="1d2b8-186">Cuenta: Cuenta de Data Lake Analytics de su suscripción de Azure.</span><span class="sxs-lookup"><span data-stu-id="1d2b8-186">Account:  A Data Lake Analytics account under your Azure subscription.</span></span>
    - <span data-ttu-id="1d2b8-187">Base de datos: Una base de datos en su cuenta.</span><span class="sxs-lookup"><span data-stu-id="1d2b8-187">Database: A database under your account.</span></span> <span data-ttu-id="1d2b8-188">valor predeterminado de Hello es **principal**.</span><span class="sxs-lookup"><span data-stu-id="1d2b8-188">hello default is **master**.</span></span>
    - <span data-ttu-id="1d2b8-189">Esquema: Un esquema en la base de datos.</span><span class="sxs-lookup"><span data-stu-id="1d2b8-189">Schema: A schema under your database.</span></span> <span data-ttu-id="1d2b8-190">valor predeterminado de Hello es **dbo**.</span><span class="sxs-lookup"><span data-stu-id="1d2b8-190">hello default is **dbo**.</span></span>
    - <span data-ttu-id="1d2b8-191">Configuración opcional:</span><span class="sxs-lookup"><span data-stu-id="1d2b8-191">Optional settings:</span></span>
        - <span data-ttu-id="1d2b8-192">Prioridad: Hola prioridad oscila entre 1 too1000 con 1 como de prioridad más alta de Hola.</span><span class="sxs-lookup"><span data-stu-id="1d2b8-192">Priority: hello priority range is from 1 too1000 with 1 as hello highest priority.</span></span> <span data-ttu-id="1d2b8-193">es el valor predeterminado de Hello **1000**.</span><span class="sxs-lookup"><span data-stu-id="1d2b8-193">hello default value is **1000**.</span></span>
        - <span data-ttu-id="1d2b8-194">Paralelismo: Hola paralelismo oscila entre 1 too150.</span><span class="sxs-lookup"><span data-stu-id="1d2b8-194">Parallelism: hello parallelism range is from 1 too150.</span></span> <span data-ttu-id="1d2b8-195">valor predeterminado de Hello es paralelismo máximo Hola permitido en su cuenta de análisis de Data Lake de Azure.</span><span class="sxs-lookup"><span data-stu-id="1d2b8-195">hello default value is hello maximum parallelism allowed in your Azure Data Lake Analytics account.</span></span> 
        
        > [!NOTE] 
        > <span data-ttu-id="1d2b8-196">Si los parámetros de hello son válidos, se usan valores predeterminados de Hola.</span><span class="sxs-lookup"><span data-stu-id="1d2b8-196">If hello settings are invalid, hello default values are used.</span></span>

    ![Archivo de configuración de Data Lake Tools para Visual Studio Code](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-configuration-file.png)

    <span data-ttu-id="1d2b8-198">Un proceso de análisis de Data Lake cuenta es necesario toocompile y ejecutar los trabajos de SQL U.</span><span class="sxs-lookup"><span data-stu-id="1d2b8-198">A compute Data Lake Analytics account is needed toocompile and run U-SQL jobs.</span></span> <span data-ttu-id="1d2b8-199">Debe configurar la cuenta de equipo de hello antes de poder compilar y ejecutar trabajos de SQL U.</span><span class="sxs-lookup"><span data-stu-id="1d2b8-199">You must configure hello computer account before you can compile and run U-SQL jobs.</span></span>
    
<span data-ttu-id="1d2b8-200">Después de guarda la configuración de hello, información de cuenta, base de datos y esquema de hello aparece en la barra de estado de hello en la esquina inferior izquierda de Hola Hola .usql del archivo de correspondiente.</span><span class="sxs-lookup"><span data-stu-id="1d2b8-200">After hello configuration is saved, hello account, database, and schema information appears on hello status bar at hello bottom-left corner of hello corresponding .usql file.</span></span> 
 
 
<span data-ttu-id="1d2b8-201">Tooopening en comparación con un archivo, cuando se abre una carpeta, puede:</span><span class="sxs-lookup"><span data-stu-id="1d2b8-201">Compared tooopening a file, when you open a folder you can:</span></span>

- <span data-ttu-id="1d2b8-202">Usar un archivo de código subyacente.</span><span class="sxs-lookup"><span data-stu-id="1d2b8-202">Use a code-behind file.</span></span> <span data-ttu-id="1d2b8-203">En el modo de archivo único de hello, código subyacente no se admite.</span><span class="sxs-lookup"><span data-stu-id="1d2b8-203">In hello single-file mode, code-behind is not supported.</span></span>
- <span data-ttu-id="1d2b8-204">Usar un archivo de configuración.</span><span class="sxs-lookup"><span data-stu-id="1d2b8-204">Use a configuration file.</span></span> <span data-ttu-id="1d2b8-205">Cuando se abre una carpeta, las secuencias de comandos de Hola Hola carpeta de trabajo comparten un único archivo de configuración.</span><span class="sxs-lookup"><span data-stu-id="1d2b8-205">When you open a folder, hello scripts in hello working folder share a single configuration file.</span></span>


<span data-ttu-id="1d2b8-206">Hola script U-SQL compila remotamente a través del servicio de análisis de Data Lake Hola.</span><span class="sxs-lookup"><span data-stu-id="1d2b8-206">hello U-SQL script compiles remotely through hello Data Lake Analytics service.</span></span> <span data-ttu-id="1d2b8-207">Cuando emita hello **compilar** comando, script U-SQL Hola se envía la cuenta de análisis de Data Lake tooyour.</span><span class="sxs-lookup"><span data-stu-id="1d2b8-207">When you issue hello **compile** command, hello U-SQL script is sent tooyour Data Lake Analytics account.</span></span> <span data-ttu-id="1d2b8-208">Más adelante, código de Visual Studio recibe el resultado de compilación Hola.</span><span class="sxs-lookup"><span data-stu-id="1d2b8-208">Later, Visual Studio Code receives hello compilation result.</span></span> <span data-ttu-id="1d2b8-209">Debido a la compilación remoto toohello, código de Visual Studio requiere que se muestra información de hello tooconnect tooyour análisis de Data Lake cuenta en el archivo de configuración de Hola.</span><span class="sxs-lookup"><span data-stu-id="1d2b8-209">Due toohello remote compilation, Visual Studio Code requires that you list hello information tooconnect tooyour Data Lake Analytics account in hello configuration file.</span></span>

<span data-ttu-id="1d2b8-210">**secuencia de comandos de toocompile U T-SQL**</span><span class="sxs-lookup"><span data-stu-id="1d2b8-210">**toocompile a U-SQL script**</span></span>

1. <span data-ttu-id="1d2b8-211">Seleccione Ctrl + Mayús + P tooopen Hola comando paleta.</span><span class="sxs-lookup"><span data-stu-id="1d2b8-211">Select Ctrl+Shift+P tooopen hello command palette.</span></span> 
2. <span data-ttu-id="1d2b8-212">Escriba **ADL: Compile Script**.</span><span class="sxs-lookup"><span data-stu-id="1d2b8-212">Enter **ADL: Compile Script**.</span></span> <span data-ttu-id="1d2b8-213">Hello resultados de compilación aparecen en hello **salida** ventana.</span><span class="sxs-lookup"><span data-stu-id="1d2b8-213">hello compile results appear in hello **Output** window.</span></span> <span data-ttu-id="1d2b8-214">Puede también haga clic en un archivo de script y, a continuación, seleccione **ADL: Script de compilación** trabajo toocompile U T-SQL.</span><span class="sxs-lookup"><span data-stu-id="1d2b8-214">You can also right-click a script file, and then select **ADL: Compile Script** toocompile a U-SQL job.</span></span> <span data-ttu-id="1d2b8-215">el resultado de compilación Hola aparece en hello **salida** panel.</span><span class="sxs-lookup"><span data-stu-id="1d2b8-215">hello compilation result appears in hello **Output** pane.</span></span>
 

<span data-ttu-id="1d2b8-216">**secuencia de comandos de toosubmit U T-SQL**</span><span class="sxs-lookup"><span data-stu-id="1d2b8-216">**toosubmit a U-SQL script**</span></span>

1. <span data-ttu-id="1d2b8-217">Seleccione Ctrl + Mayús + P tooopen Hola comando paleta.</span><span class="sxs-lookup"><span data-stu-id="1d2b8-217">Select Ctrl+Shift+P tooopen hello command palette.</span></span> 
2. <span data-ttu-id="1d2b8-218">Escriba **ADL: Submit Job**.</span><span class="sxs-lookup"><span data-stu-id="1d2b8-218">Enter **ADL: Submit Job**.</span></span>  <span data-ttu-id="1d2b8-219">También puede hacer clic con el botón derecho en un archivo de script y, luego, seleccionar **ADL: Submit Job**.</span><span class="sxs-lookup"><span data-stu-id="1d2b8-219">You can also right-click a script file, and then select **ADL: Submit Job**.</span></span> 

<span data-ttu-id="1d2b8-220">Después de enviar un trabajo de SQL U, registros de envío de hello aparecen en hello **salida** ventana en VS Code.</span><span class="sxs-lookup"><span data-stu-id="1d2b8-220">After you submit a U-SQL job, hello submission logs appear in hello **Output** window in VS Code.</span></span> <span data-ttu-id="1d2b8-221">Si el envío de hello es correcto, dirección URL de trabajo de hello aparece también.</span><span class="sxs-lookup"><span data-stu-id="1d2b8-221">If hello submission is successful, hello job URL appears as well.</span></span> <span data-ttu-id="1d2b8-222">Puede abrir dirección URL de trabajo de hello en un estado de trabajo en tiempo real de web explorador tootrack Hola.</span><span class="sxs-lookup"><span data-stu-id="1d2b8-222">You can open hello job URL in a web browser tootrack hello real-time job status.</span></span>

<span data-ttu-id="1d2b8-223">salida de hello tooenable de detalles del trabajo hello, establezca **jobInformationOutputPath** en hello **frente a código de hello u-sql_settings.json** archivo.</span><span class="sxs-lookup"><span data-stu-id="1d2b8-223">tooenable hello output of hello job details, set **jobInformationOutputPath** in hello **vs code for hello u-sql_settings.json** file.</span></span>
 
## <a name="use-a-code-behind-file"></a><span data-ttu-id="1d2b8-224">Uso de un archivo de código subyacente</span><span class="sxs-lookup"><span data-stu-id="1d2b8-224">Use a code-behind file</span></span>

<span data-ttu-id="1d2b8-225">Un archivo de código subyacente es un archivo C# asociado con un solo script U-SQL.</span><span class="sxs-lookup"><span data-stu-id="1d2b8-225">A code-behind file is a C# file associated with a single U-SQL script.</span></span> <span data-ttu-id="1d2b8-226">Puede definir un script dedicado tooUDO, UDA, UDT y UDF en el archivo de código subyacente de Hola.</span><span class="sxs-lookup"><span data-stu-id="1d2b8-226">You can define a script dedicated tooUDO, UDA, UDT, and UDF in hello code-behind file.</span></span> <span data-ttu-id="1d2b8-227">Hello UDO, UDA, UDT y UDF pueden utilizarse directamente en el script de Hola sin registrar ensamblado de hello en primer lugar.</span><span class="sxs-lookup"><span data-stu-id="1d2b8-227">hello UDO, UDA, UDT, and UDF can be used directly in hello script without registering hello assembly first.</span></span> <span data-ttu-id="1d2b8-228">Hello archivo de código subyacente se coloca en hello misma carpeta que su archivo de script SQL U emparejamiento.</span><span class="sxs-lookup"><span data-stu-id="1d2b8-228">hello code-behind file is put in hello same folder as its peering U-SQL script file.</span></span> <span data-ttu-id="1d2b8-229">Si el script de Hola se denomina xxx.usql, código de hello en segundo plano se denomina xxx.usql.cs.</span><span class="sxs-lookup"><span data-stu-id="1d2b8-229">If hello script is named xxx.usql, hello code-behind is named as xxx.usql.cs.</span></span> <span data-ttu-id="1d2b8-230">Si lo eliminó manualmente el archivo de código subyacente de hello, la característica de código subyacente de hello está deshabilitada para su script U-SQL asociado.</span><span class="sxs-lookup"><span data-stu-id="1d2b8-230">If you manually delete hello code-behind file, hello code-behind feature is disabled for its associated U-SQL script.</span></span> <span data-ttu-id="1d2b8-231">Para más información sobre cómo escribir código de cliente para el script U-SQL, consulte [Writing and Using Custom Code in U-SQL – User-Defined Functions]( https://blogs.msdn.microsoft.com/visualstudio/2015/10/28/writing-and-using-custom-code-in-u-sql-user-defined-functions/) (Escritura y uso de código personalizado en U-SQL: funciones definidas por el usuario).</span><span class="sxs-lookup"><span data-stu-id="1d2b8-231">For more information about writing customer code for U-SQL script, see [Writing and Using Custom Code in U-SQL: User-Defined Functions]( https://blogs.msdn.microsoft.com/visualstudio/2015/10/28/writing-and-using-custom-code-in-u-sql-user-defined-functions/).</span></span>

<span data-ttu-id="1d2b8-232">toosupport código subyacente, debe abrir una carpeta de trabajo.</span><span class="sxs-lookup"><span data-stu-id="1d2b8-232">toosupport code-behind, you must open a working folder.</span></span> 

<span data-ttu-id="1d2b8-233">**toogenerate un archivo de código subyacente**</span><span class="sxs-lookup"><span data-stu-id="1d2b8-233">**toogenerate a code-behind file**</span></span>

1. <span data-ttu-id="1d2b8-234">Abra un archivo de origen.</span><span class="sxs-lookup"><span data-stu-id="1d2b8-234">Open a source file.</span></span> 
2. <span data-ttu-id="1d2b8-235">Seleccione Ctrl + Mayús + P tooopen Hola comando paleta.</span><span class="sxs-lookup"><span data-stu-id="1d2b8-235">Select Ctrl+Shift+P tooopen hello command palette.</span></span>
3. <span data-ttu-id="1d2b8-236">Escriba **ADL: Generate Code Behind**.</span><span class="sxs-lookup"><span data-stu-id="1d2b8-236">Enter **ADL: Generate Code Behind**.</span></span> <span data-ttu-id="1d2b8-237">Se crea un archivo de código subyacente en hello misma carpeta.</span><span class="sxs-lookup"><span data-stu-id="1d2b8-237">A code-behind file is created in hello same folder.</span></span> 

<span data-ttu-id="1d2b8-238">También puede hacer clic con el botón derecho en un archivo de script y, luego, seleccionar **ADL: Generate Code Behind**.</span><span class="sxs-lookup"><span data-stu-id="1d2b8-238">You can also right-click a script file, and then select **ADL: Generate Code Behind**.</span></span> 

<span data-ttu-id="1d2b8-239">toocompile y enviar un script U-SQL con un archivo de código subyacente se Hola igual que con hello independiente U-SQL los archivos de scripts.</span><span class="sxs-lookup"><span data-stu-id="1d2b8-239">toocompile and submit a U-SQL script with a code-behind file is hello same as with hello standalone U-SQL script file.</span></span>

<span data-ttu-id="1d2b8-240">Hola siguiendo dos capturas de pantalla muestra un archivo de código subyacente y su archivo de script U-SQL asociado:</span><span class="sxs-lookup"><span data-stu-id="1d2b8-240">hello following two screenshots show a code-behind file and its associated U-SQL script file:</span></span>
 
![Herramientas de Data Lake para Visual Studio Code: código subyacente](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-code-behind.png)

![Herramientas de Data Lake para Visual Studio Code: archivo de script de código subyacente](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-code-behind-call.png) 

## <a name="use-assemblies"></a><span data-ttu-id="1d2b8-243">Uso de ensamblados</span><span class="sxs-lookup"><span data-stu-id="1d2b8-243">Use assemblies</span></span>

<span data-ttu-id="1d2b8-244">Para información sobre el desarrollo de ensamblados, consulte [Desarrollo de ensamblados U-SQL para trabajos de Azure Data Lake Analytics](data-lake-analytics-u-sql-develop-assemblies.md).</span><span class="sxs-lookup"><span data-stu-id="1d2b8-244">For information on developing assemblies, see [Develop U-SQL assemblies for Azure Data Lake Analytics jobs](data-lake-analytics-u-sql-develop-assemblies.md).</span></span>

<span data-ttu-id="1d2b8-245">Puede usar los ensamblados de código personalizado de Data Lake Tools tooregister en el catálogo de análisis de Data Lake Hola.</span><span class="sxs-lookup"><span data-stu-id="1d2b8-245">You can use Data Lake Tools tooregister custom code assemblies in hello Data Lake Analytics catalog.</span></span>

<span data-ttu-id="1d2b8-246">**tooregister un ensamblado**</span><span class="sxs-lookup"><span data-stu-id="1d2b8-246">**tooregister an assembly**</span></span>

<span data-ttu-id="1d2b8-247">Puede registrar ensamblado de Hola a través de hello **ADL: registrar ensamblado de** o **ADL: registrar el ensamblado a través de la configuración** comandos.</span><span class="sxs-lookup"><span data-stu-id="1d2b8-247">You can register hello assembly through hello **ADL: Register Assembly** or **ADL: Register Assembly through Configuration** commands.</span></span>

<span data-ttu-id="1d2b8-248">**tooregister a través de hello ADL: registrar agregado (comando)**</span><span class="sxs-lookup"><span data-stu-id="1d2b8-248">**tooregister through hello ADL: Register Assembly command**</span></span>
1.  <span data-ttu-id="1d2b8-249">Seleccione Ctrl + Mayús + P tooopen Hola comando paleta.</span><span class="sxs-lookup"><span data-stu-id="1d2b8-249">Select Ctrl+Shift+P tooopen hello command palette.</span></span>
2.  <span data-ttu-id="1d2b8-250">Escriba **ADL: Register Assembly**.</span><span class="sxs-lookup"><span data-stu-id="1d2b8-250">Enter **ADL: Register Assembly**.</span></span> 
3.  <span data-ttu-id="1d2b8-251">Especifique la ruta de acceso de ensamblado locales de Hola.</span><span class="sxs-lookup"><span data-stu-id="1d2b8-251">Specify hello local assembly path.</span></span> 
4.  <span data-ttu-id="1d2b8-252">Seleccione una cuenta de Data Lake Analytics.</span><span class="sxs-lookup"><span data-stu-id="1d2b8-252">Select a Data Lake Analytics account.</span></span>
5.  <span data-ttu-id="1d2b8-253">Seleccione una base de datos.</span><span class="sxs-lookup"><span data-stu-id="1d2b8-253">Select a database.</span></span>

<span data-ttu-id="1d2b8-254">Resultados: portal de Hola se abre en un explorador y muestra el proceso de registro del ensamblado de Hola.</span><span class="sxs-lookup"><span data-stu-id="1d2b8-254">Results: hello portal is opened in a browser and displays hello assembly registration process.</span></span>  

<span data-ttu-id="1d2b8-255">Hola de tootrigger de otra forma cómoda **ADL: registrar ensamblado de** comando es tooright y haga clic en archivo de .dll hello en el Explorador de archivos.</span><span class="sxs-lookup"><span data-stu-id="1d2b8-255">Another convenient way tootrigger hello **ADL: Register Assembly** command is tooright-click hello .dll file in File Explorer.</span></span> 

<span data-ttu-id="1d2b8-256">**tooregister aunque Hola ADL: registrar el ensamblado a través de los comandos de configuración**</span><span class="sxs-lookup"><span data-stu-id="1d2b8-256">**tooregister though hello ADL: Register Assembly through Configuration command**</span></span>
1.  <span data-ttu-id="1d2b8-257">Seleccione Ctrl + Mayús + P tooopen Hola comando paleta.</span><span class="sxs-lookup"><span data-stu-id="1d2b8-257">Select Ctrl+Shift+P tooopen hello command palette.</span></span>
2.  <span data-ttu-id="1d2b8-258">Escriba **ADL: Register Assembly through Configuration**.</span><span class="sxs-lookup"><span data-stu-id="1d2b8-258">Enter **ADL: Register Assembly through Configuration**.</span></span> 
3.  <span data-ttu-id="1d2b8-259">Especifique la ruta de acceso de ensamblado locales de Hola.</span><span class="sxs-lookup"><span data-stu-id="1d2b8-259">Specify hello local assembly path.</span></span> 
4.  <span data-ttu-id="1d2b8-260">se muestra el archivo JSON de Hello.</span><span class="sxs-lookup"><span data-stu-id="1d2b8-260">hello JSON file is displayed.</span></span> <span data-ttu-id="1d2b8-261">Revisar y editar las dependencias de ensamblado de Hola y parámetros de recursos, si es necesario.</span><span class="sxs-lookup"><span data-stu-id="1d2b8-261">Review and edit hello assembly dependencies and resource parameters, if needed.</span></span> <span data-ttu-id="1d2b8-262">Las instrucciones se muestran en hello **salida** ventana.</span><span class="sxs-lookup"><span data-stu-id="1d2b8-262">Instructions are displayed in hello **Output** window.</span></span> <span data-ttu-id="1d2b8-263">tooproceed toohello registro de ensamblados, guardar el archivo JSON de hello (CTRL+s).</span><span class="sxs-lookup"><span data-stu-id="1d2b8-263">tooproceed toohello assembly registration, save (Ctrl+S) hello JSON file.</span></span>

![Herramientas de Data Lake para Visual Studio Code: código subyacente](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-register-assembly-advance.png)
>[!NOTE]
>- <span data-ttu-id="1d2b8-265">Las dependencias de ensamblado: detecta automáticamente Azure Data Lake Tools si Hola DLL tiene todas las dependencias.</span><span class="sxs-lookup"><span data-stu-id="1d2b8-265">Assembly dependencies: Azure Data Lake Tools autodetects whether hello DLL has any dependencies.</span></span> <span data-ttu-id="1d2b8-266">dependencias de Hola se muestran en el archivo JSON de hello después de que se detecten.</span><span class="sxs-lookup"><span data-stu-id="1d2b8-266">hello dependencies are displayed in hello JSON file after they are detected.</span></span> 
>- <span data-ttu-id="1d2b8-267">Recursos: Puede cargar los recursos DLL (por ejemplo, .txt, .png y .csv) como parte del registro de ensamblados de Hola.</span><span class="sxs-lookup"><span data-stu-id="1d2b8-267">Resources: You can upload your DLL resources (for example, .txt, .png, and .csv) as part of hello assembly registration.</span></span> 

<span data-ttu-id="1d2b8-268">Hola de tootrigger de otra manera **ADL: registrar el ensamblado a través de la configuración** comando es tooright y haga clic en archivo de .dll hello en el Explorador de archivos.</span><span class="sxs-lookup"><span data-stu-id="1d2b8-268">Another way tootrigger hello **ADL: Register Assembly through Configuration** command is tooright-click hello .dll file in File Explorer.</span></span> 

<span data-ttu-id="1d2b8-269">Hola sigue U-SQL código se muestra cómo toocall un ensamblado.</span><span class="sxs-lookup"><span data-stu-id="1d2b8-269">hello following U-SQL code demonstrates how toocall an assembly.</span></span> <span data-ttu-id="1d2b8-270">En el ejemplo de Hola, es el nombre del ensamblado de hello *probar*.</span><span class="sxs-lookup"><span data-stu-id="1d2b8-270">In hello sample, hello assembly name is *test*.</span></span>

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


## <a name="access-hello-data-lake-analytics-catalog"></a><span data-ttu-id="1d2b8-271">Catálogo de análisis de Data Lake Hola de acceso</span><span class="sxs-lookup"><span data-stu-id="1d2b8-271">Access hello Data Lake Analytics catalog</span></span>

<span data-ttu-id="1d2b8-272">Después de haber conectado tooAzure, puede usar Hola siguiendo el catálogo de hello U-SQL tooaccess de pasos.</span><span class="sxs-lookup"><span data-stu-id="1d2b8-272">After you have connected tooAzure, you can use hello following steps tooaccess hello U-SQL catalog.</span></span>

<span data-ttu-id="1d2b8-273">**metadatos de análisis de Azure Data Lake hello tooaccess**</span><span class="sxs-lookup"><span data-stu-id="1d2b8-273">**tooaccess hello Azure Data Lake Analytics metadata**</span></span>

1.  <span data-ttu-id="1d2b8-274">Seleccione Ctrl+Mayús+P y, luego, escriba **ADL: List Tables**.</span><span class="sxs-lookup"><span data-stu-id="1d2b8-274">Select Ctrl+Shift+P, and then enter **ADL: List Tables**.</span></span>
2.  <span data-ttu-id="1d2b8-275">Seleccione una de las cuentas de análisis de Data Lake Hola.</span><span class="sxs-lookup"><span data-stu-id="1d2b8-275">Select one of hello Data Lake Analytics accounts.</span></span>
3.  <span data-ttu-id="1d2b8-276">Seleccione una de las bases de datos de análisis de Data Lake de Hola.</span><span class="sxs-lookup"><span data-stu-id="1d2b8-276">Select one of hello Data Lake Analytics databases.</span></span>
4.  <span data-ttu-id="1d2b8-277">Seleccione uno de los esquemas de Hola.</span><span class="sxs-lookup"><span data-stu-id="1d2b8-277">Select one of hello schemas.</span></span> <span data-ttu-id="1d2b8-278">Puede ver la lista de Hola de tablas.</span><span class="sxs-lookup"><span data-stu-id="1d2b8-278">You can see hello list of tables.</span></span>

## <a name="view-data-lake-analytics-jobs"></a><span data-ttu-id="1d2b8-279">Vista de los trabajos de Data Lake Analytics</span><span class="sxs-lookup"><span data-stu-id="1d2b8-279">View Data Lake Analytics jobs</span></span>

<span data-ttu-id="1d2b8-280">**trabajos de análisis de Data Lake tooview**</span><span class="sxs-lookup"><span data-stu-id="1d2b8-280">**tooview Data Lake Analytics jobs**</span></span>
1.  <span data-ttu-id="1d2b8-281">Abrir la paleta de comando hello (Ctrl + Mayús + P) y seleccione **ADL: Mostrar trabajo**.</span><span class="sxs-lookup"><span data-stu-id="1d2b8-281">Open hello command palette (Ctrl+Shift+P) and select **ADL: Show Job**.</span></span> 
2.  <span data-ttu-id="1d2b8-282">Seleccione una cuenta de Data Lake Analytics o una cuenta local.</span><span class="sxs-lookup"><span data-stu-id="1d2b8-282">Select a Data Lake Analytics or local account.</span></span> 
3.  <span data-ttu-id="1d2b8-283">Espere para lista de trabajos de Hola Hola cuenta tooappear.</span><span class="sxs-lookup"><span data-stu-id="1d2b8-283">Wait for hello jobs list for hello account tooappear.</span></span>
4.  <span data-ttu-id="1d2b8-284">Seleccione un trabajo de la lista de trabajos, Data Lake Tools abre los detalles del trabajo de Hola Hola portal de Azure y muestra el archivo JobInfo de hello en VS Code.</span><span class="sxs-lookup"><span data-stu-id="1d2b8-284">Select a job from job list, Data Lake Tools opens hello job details in hello Azure portal and displays hello JobInfo file in VS Code.</span></span>

![Tipos de objetos de IntelliSense de Data Lake Tools para Visual Studio Code](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-show-job.png)

## <a name="azure-data-lake-storage-integration"></a><span data-ttu-id="1d2b8-286">Integración de Azure Data Lake Storage</span><span class="sxs-lookup"><span data-stu-id="1d2b8-286">Azure Data Lake Storage integration</span></span>

<span data-ttu-id="1d2b8-287">Puede usar comandos relacionados con Azure Data Lake Storage para:</span><span class="sxs-lookup"><span data-stu-id="1d2b8-287">You can use Azure Data Lake Storage-related commands to:</span></span>
 - <span data-ttu-id="1d2b8-288">Examine los recursos de almacenamiento de Azure datos Lake Hola.</span><span class="sxs-lookup"><span data-stu-id="1d2b8-288">Browse through hello Azure Data Lake Storage resources.</span></span> 
 - <span data-ttu-id="1d2b8-289">Archivo de almacenamiento de Azure datos Lake hello de vista previa.</span><span class="sxs-lookup"><span data-stu-id="1d2b8-289">Preview hello Azure Data Lake Storage file.</span></span>  
 - <span data-ttu-id="1d2b8-290">Cargar Hola archivo tooAzure Lake el almacenamiento de datos directamente en el código de VS.</span><span class="sxs-lookup"><span data-stu-id="1d2b8-290">Upload hello file directly tooAzure Data Lake Storage in VS Code.</span></span> 

### <a name="list-hello-storage-path"></a><span data-ttu-id="1d2b8-291">Ruta de acceso de almacenamiento de Hola de lista</span><span class="sxs-lookup"><span data-stu-id="1d2b8-291">List hello storage path</span></span> 
<span data-ttu-id="1d2b8-292">Puede mostrar la ruta de acceso de almacenamiento de Hola a través de la paleta de comando de Hola o menú contextual.</span><span class="sxs-lookup"><span data-stu-id="1d2b8-292">You can list hello storage path through hello command palette or through right-click.</span></span>

<span data-ttu-id="1d2b8-293">**ruta de acceso de almacenamiento de toolist Hola a través de la paleta de comando hello**</span><span class="sxs-lookup"><span data-stu-id="1d2b8-293">**toolist hello storage path through hello command palette**</span></span>

1.  <span data-ttu-id="1d2b8-294">Abrir la paleta de comando hello (Ctrl + Mayús + P) y escriba **ADL: ruta de acceso de almacenamiento de lista**.</span><span class="sxs-lookup"><span data-stu-id="1d2b8-294">Open hello command palette (Ctrl+Shift+P) and enter **ADL: List Storage Path**.</span></span>

    ![Herramientas de Data Lake para Visual Studio Code: enumerar la ruta de acceso de almacenamiento](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-list-storage.png)

2.  <span data-ttu-id="1d2b8-296">Seleccione la forma preferida para enumerar la ruta de acceso de almacenamiento de Hola.</span><span class="sxs-lookup"><span data-stu-id="1d2b8-296">Select your preferred way for listing hello storage path.</span></span> <span data-ttu-id="1d2b8-297">En este paso se usa **Enter a path** (Escribir una ruta de acceso) como ejemplo.</span><span class="sxs-lookup"><span data-stu-id="1d2b8-297">This passage uses **Enter a path** as an example.</span></span>

    ![Data Lake Tools para Visual Studio Code ruta de acceso de almacenamiento de una manera toolist Hola](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-list-account-selectoneway.png)

    > [!NOTE]
    >- <span data-ttu-id="1d2b8-299">FRENTE a código mantiene la ruta de acceso de hello visitado por el último en cada cuenta de análisis de Data Lake.</span><span class="sxs-lookup"><span data-stu-id="1d2b8-299">VS Code keeps hello last-visited path in every Data Lake Analytics account.</span></span> <span data-ttu-id="1d2b8-300">Por ejemplo: /tt/ss.</span><span class="sxs-lookup"><span data-stu-id="1d2b8-300">For example: /tt/ss.</span></span>
    >- <span data-ttu-id="1d2b8-301">Explorador de ruta de acceso raíz: ruta de raíz de la lista de Hola desde su cuenta de análisis de Data Lake seleccionada o una ruta de acceso local.</span><span class="sxs-lookup"><span data-stu-id="1d2b8-301">Browser from root path: hello list root path from your selected Data Lake Analytics account or a local path.</span></span>
    >- <span data-ttu-id="1d2b8-302">Enter a path (Escribir una ruta de acceso): indica una ruta de acceso especificada desde la cuenta de Data Lake Analytics seleccionada o una ruta de acceso local.</span><span class="sxs-lookup"><span data-stu-id="1d2b8-302">Enter a path: List a specified path from your selected Data Lake Analytics account or a local path.</span></span>
    
3. <span data-ttu-id="1d2b8-303">Seleccione una cuenta de la ruta de acceso local de Hola o una cuenta de análisis de Data Lake.</span><span class="sxs-lookup"><span data-stu-id="1d2b8-303">Select an account from hello local path or a Data Lake Analytics account.</span></span>

    ![Más selecciones de Herramientas de Data Lake para Visual Studio Code](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-list-account.png)

4. <span data-ttu-id="1d2b8-305">Seleccione **más** toolist más cuentas de análisis de Data Lake y, a continuación, seleccione una cuenta de análisis de Data Lake.</span><span class="sxs-lookup"><span data-stu-id="1d2b8-305">Select **more** toolist more Data Lake Analytics accounts, and then select a Data Lake Analytics account.</span></span>

    ![Herramientas de Data Lake para Visual Studio Code: selección de una cuenta](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-select-adla-account.png)

5.  <span data-ttu-id="1d2b8-307">Escriba una ruta de acceso de almacenamiento de Azure.</span><span class="sxs-lookup"><span data-stu-id="1d2b8-307">Enter an Azure storage path.</span></span> <span data-ttu-id="1d2b8-308">Por ejemplo, /output.</span><span class="sxs-lookup"><span data-stu-id="1d2b8-308">For example, /output.</span></span>

    ![Herramientas de Data Lake para Visual Studio Code: escribir la ruta de acceso de almacenamiento](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-input-path.png)

6.  <span data-ttu-id="1d2b8-310">Resultados: paleta de hello comando muestra información de ruta de acceso de hello en función de las entradas.</span><span class="sxs-lookup"><span data-stu-id="1d2b8-310">Results: hello command palette lists hello path information based on your entries.</span></span>

    ![Herramientas de Data Lake para Visual Studio Code: enumerar los resultados de la ruta de acceso de almacenamiento](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-list-path.png)

<span data-ttu-id="1d2b8-312">Una manera más conveniente de ruta de acceso relativa de toolist hello es a través de hello haga clic en el menú contextual.</span><span class="sxs-lookup"><span data-stu-id="1d2b8-312">A more convenient way toolist hello relative path is through hello right-click context menu.</span></span>

<span data-ttu-id="1d2b8-313">**Pulse el botón derecho en la ruta de acceso de almacenamiento de toolist Hola a través de**</span><span class="sxs-lookup"><span data-stu-id="1d2b8-313">**toolist hello storage path through right-click**</span></span>

1.  <span data-ttu-id="1d2b8-314">Haga clic en tooselect de cadena de ruta de acceso de hello **ruta de acceso de almacenamiento de lista**.</span><span class="sxs-lookup"><span data-stu-id="1d2b8-314">Right-click hello path string tooselect **List Storage Path**.</span></span>

       ![Herramientas de Data Lake para Visual Studio Code: menú contextual](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-right-click-path.png)

2. <span data-ttu-id="1d2b8-316">ruta de acceso relativa Hola seleccionado aparece en la paleta de comando Hola.</span><span class="sxs-lookup"><span data-stu-id="1d2b8-316">hello selected relative path appears in hello command palette.</span></span>

   ![Herramientas de Data Lake para Visual Studio Code: ruta de acceso relativa seleccionada](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-list-relative-path.png)

3.  <span data-ttu-id="1d2b8-318">Seleccione una cuenta de la ruta de acceso local de Hola o una cuenta de análisis de Data Lake.</span><span class="sxs-lookup"><span data-stu-id="1d2b8-318">Select an account from hello local path or a Data Lake Analytics account.</span></span>

       ![Herramientas de Data Lake para Visual Studio Code: selección de una cuenta](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-list-account.png)

4.  <span data-ttu-id="1d2b8-320">Resultados: listas de paleta de comando Hola Hola carpetas y archivos para la ruta de acceso actual de Hola.</span><span class="sxs-lookup"><span data-stu-id="1d2b8-320">Results: hello command palette lists hello folders and files for hello current path.</span></span>

       ![Data Lake Tools para lista de código de Visual Studio desde la ruta de acceso actual de Hola](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-list-current.png)

### <a name="preview-hello-storage-file"></a><span data-ttu-id="1d2b8-322">Archivo de almacenamiento de hello de vista previa</span><span class="sxs-lookup"><span data-stu-id="1d2b8-322">Preview hello storage file</span></span>
<span data-ttu-id="1d2b8-323">Puede obtener una vista previa de archivo de almacenamiento de hello a través de la paleta de comando de Hola o menú contextual.</span><span class="sxs-lookup"><span data-stu-id="1d2b8-323">You can preview hello storage file through hello command palette or through right-click.</span></span>

<span data-ttu-id="1d2b8-324">**archivo de almacenamiento de hello toopreview a través de la paleta de comando hello**</span><span class="sxs-lookup"><span data-stu-id="1d2b8-324">**toopreview hello storage file through hello command palette**</span></span>

1.  <span data-ttu-id="1d2b8-325">Abrir la paleta de comando hello (Ctrl + Mayús + P) y escriba **ADL: vista previa de un archivo de almacenamiento**.</span><span class="sxs-lookup"><span data-stu-id="1d2b8-325">Open hello command palette (Ctrl+Shift+P) and enter **ADL: Preview Storage File**.</span></span>

       ![Herramientas de Data Lake para Visual Studio Code: vista previa del archivo de almacenamiento](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-list-preview.png)

2.  <span data-ttu-id="1d2b8-327">Seleccione una cuenta de la ruta de acceso local de Hola o una cuenta de análisis de Data Lake.</span><span class="sxs-lookup"><span data-stu-id="1d2b8-327">Select an account from hello local path or a Data Lake Analytics account.</span></span>

       ![Herramientas de Data Lake para Visual Studio Code: enumerar cuentas](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-list-account.png)

3.  <span data-ttu-id="1d2b8-329">Seleccione **más** toolist más cuentas de análisis de Data Lake y, a continuación, seleccione una cuenta de análisis de Data Lake.</span><span class="sxs-lookup"><span data-stu-id="1d2b8-329">Select **more** toolist more Data Lake Analytics accounts, and then select a Data Lake Analytics account.</span></span>

       ![Herramientas de Data Lake para Visual Studio Code: selección de una cuenta](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-select-adla-account.png)

4.  <span data-ttu-id="1d2b8-331">Escriba un archivo o ruta de almacenamiento de Azure.</span><span class="sxs-lookup"><span data-stu-id="1d2b8-331">Enter an Azure storage path or file.</span></span> <span data-ttu-id="1d2b8-332">Por ejemplo, /output/SearchLog.txt.</span><span class="sxs-lookup"><span data-stu-id="1d2b8-332">For example, /output/SearchLog.txt.</span></span>

       ![Herramientas de Data Lake para Visual Studio Code: escribir el archivo y la ruta de acceso de almacenamiento](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-input-preview-file.png)

5.  <span data-ttu-id="1d2b8-334">Resultados: paleta de hello comando muestra información de ruta de acceso de hello en función de las entradas.</span><span class="sxs-lookup"><span data-stu-id="1d2b8-334">Results: hello command palette lists hello path information based on your entries.</span></span>

       ![Herramientas de Data Lake para Visual Studio Code: resultado de la vista previa de archivo](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-preview-results.png)

<span data-ttu-id="1d2b8-336">**Pulse el botón derecho en la ruta de acceso de almacenamiento de toolist Hola a través de**</span><span class="sxs-lookup"><span data-stu-id="1d2b8-336">**toolist hello storage path through right-click**</span></span>

1.  <span data-ttu-id="1d2b8-337">toopreview un archivo, haga clic en la ruta de acceso de archivo Hola.</span><span class="sxs-lookup"><span data-stu-id="1d2b8-337">toopreview a file, right-click hello file path.</span></span>

   ![Herramientas de Data Lake para Visual Studio Code: menú contextual](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-right-click-preview.png) 

2.  <span data-ttu-id="1d2b8-339">Seleccione una cuenta de la ruta de acceso local de Hola o una cuenta de análisis de Data Lake.</span><span class="sxs-lookup"><span data-stu-id="1d2b8-339">Select an account from hello local path or a Data Lake Analytics account.</span></span>

       ![Herramientas de Data Lake para Visual Studio Code: selección de una cuenta](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-list-account.png)

3.  <span data-ttu-id="1d2b8-341">Resultados: VS Code muestra resultados de vista previa de Hola de archivo hello.</span><span class="sxs-lookup"><span data-stu-id="1d2b8-341">Results: VS Code displays hello preview results of hello file.</span></span>

       ![Herramientas de Data Lake para Visual Studio Code: resultado de la vista previa de archivo](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-preview-results.png)

### <a name="upload-a-file"></a><span data-ttu-id="1d2b8-343">Cargar un archivo</span><span class="sxs-lookup"><span data-stu-id="1d2b8-343">Upload a file</span></span> 

<span data-ttu-id="1d2b8-344">Puede cargar archivos escribiendo comandos de hello **ADL: cargar archivo** o **ADL: cargar archivo de configuración**.</span><span class="sxs-lookup"><span data-stu-id="1d2b8-344">You can upload files by entering hello commands **ADL: Upload File** or **ADL: Upload File through Configuration**.</span></span>

<span data-ttu-id="1d2b8-345">**archivos de tooupload aunque Hola ADL: cargar archivo (comando)**</span><span class="sxs-lookup"><span data-stu-id="1d2b8-345">**tooupload files though hello ADL: Upload File command**</span></span>
1. <span data-ttu-id="1d2b8-346">Seleccione Ctrl + Mayús + P tooopen Hola comando paleta o haga clic en editor de script de Hola y, a continuación, escriba **cargar archivo**.</span><span class="sxs-lookup"><span data-stu-id="1d2b8-346">Select Ctrl+Shift+P tooopen hello command palette or right-click hello script editor, and then enter **Upload File**.</span></span>
2.  <span data-ttu-id="1d2b8-347">Hola tooupload de archivo, escriba una ruta de acceso local.</span><span class="sxs-lookup"><span data-stu-id="1d2b8-347">tooupload hello file, enter a local path.</span></span>

    ![Herramientas de Data Lake para Visual Studio Code: escribir la ruta de acceso local](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-auto-input-local-path.png)

3. <span data-ttu-id="1d2b8-349">Seleccione una de las formas de Hola de ruta de acceso de almacenamiento de anuncio Hola.</span><span class="sxs-lookup"><span data-stu-id="1d2b8-349">Select one of hello ways of listing hello storage path.</span></span> <span data-ttu-id="1d2b8-350">En este paso se usa **Enter a path** (Escribir una ruta de acceso) como ejemplo.</span><span class="sxs-lookup"><span data-stu-id="1d2b8-350">This passage uses **Enter a path** as an example.</span></span>

    ![Herramientas de Data Lake para Visual Studio Code: enumerar la ruta de acceso de almacenamiento](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-list-account-selectoneway.png)
    >[!NOTE]
    >- <span data-ttu-id="1d2b8-352">FRENTE a código mantiene la ruta de acceso de hello visitado por el último en cada cuenta de análisis de Data Lake.</span><span class="sxs-lookup"><span data-stu-id="1d2b8-352">VS Code keeps hello last-visited path in every Data Lake Analytics account.</span></span> <span data-ttu-id="1d2b8-353">Por ejemplo: /tt/ss.</span><span class="sxs-lookup"><span data-stu-id="1d2b8-353">For example: /tt/ss.</span></span>
    >- <span data-ttu-id="1d2b8-354">Explorador de ruta de acceso raíz: ruta de raíz de la lista de Hola desde su cuenta de análisis de Data Lake seleccionada o una ruta de acceso local.</span><span class="sxs-lookup"><span data-stu-id="1d2b8-354">Browser from root path: hello list root path from your selected Data Lake Analytics account or a local path.</span></span>
    >- <span data-ttu-id="1d2b8-355">Enter a path (Escribir una ruta de acceso): indica una ruta de acceso especificada desde la cuenta de Data Lake Analytics seleccionada o una ruta de acceso local.</span><span class="sxs-lookup"><span data-stu-id="1d2b8-355">Enter a path: List a specified path from your selected Data Lake Analytics account or a local path.</span></span>

4. <span data-ttu-id="1d2b8-356">Seleccione una cuenta de la ruta de acceso local de Hola o una cuenta de análisis de Data Lake.</span><span class="sxs-lookup"><span data-stu-id="1d2b8-356">Select an account from hello local path or a Data Lake Analytics account.</span></span>

    ![Herramientas de Data Lake Tools para Visual Studio Code: clic derecho en almacenamiento](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-list-account.png)

5. <span data-ttu-id="1d2b8-358">Escriba una ruta de acceso de almacenamiento de Azure.</span><span class="sxs-lookup"><span data-stu-id="1d2b8-358">Enter an Azure storage path.</span></span> <span data-ttu-id="1d2b8-359">Por ejemplo: /output.</span><span class="sxs-lookup"><span data-stu-id="1d2b8-359">For example: /output.</span></span>

       ![Data Lake Tools for Visual Studio Code enter storage path](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-input-preview-file.png)

6. <span data-ttu-id="1d2b8-360">Busque la ruta de acceso de almacenamiento de Azure.</span><span class="sxs-lookup"><span data-stu-id="1d2b8-360">Find your Azure storage path.</span></span> <span data-ttu-id="1d2b8-361">Seleccione **Choose current folder** (Elegir carpeta actual).</span><span class="sxs-lookup"><span data-stu-id="1d2b8-361">Select **Choose current folder**.</span></span>

    ![Herramientas de Data Lake para Visual Studio Code: selección de una carpeta](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-choose-current-folder.png)

7.  <span data-ttu-id="1d2b8-363">Resultados: Hola **salida** ventana muestra el estado de carga del archivo de Hola.</span><span class="sxs-lookup"><span data-stu-id="1d2b8-363">Results: hello **Output** window displays hello file upload status.</span></span>

       ![Herramientas de Data Lake para Visual Studio Code: estado de carga](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-upload-status.png)    

<span data-ttu-id="1d2b8-365">**archivos de tooupload aunque Hola ADL: cargar archivos a través de los comandos de configuración**</span><span class="sxs-lookup"><span data-stu-id="1d2b8-365">**tooupload files though hello ADL: Upload File through Configuration command**</span></span>
1.  <span data-ttu-id="1d2b8-366">Seleccione Ctrl + Mayús + P tooopen Hola comando paleta o haga clic en editor de script de Hola y, a continuación, escriba **cargar archivo de configuración**.</span><span class="sxs-lookup"><span data-stu-id="1d2b8-366">Select Ctrl+Shift+P tooopen hello command palette or right-click hello script editor, and then enter **Upload File through Configuration**.</span></span>
2.  <span data-ttu-id="1d2b8-367">VS Code muestra un archivo JSON.</span><span class="sxs-lookup"><span data-stu-id="1d2b8-367">VS Code displays a JSON file.</span></span> <span data-ttu-id="1d2b8-368">Puede especificar las rutas de acceso de archivo y cargar varios archivos en hello mismo tiempo.</span><span class="sxs-lookup"><span data-stu-id="1d2b8-368">You can enter file paths and upload multiple files at hello same time.</span></span> <span data-ttu-id="1d2b8-369">Las instrucciones se muestran en hello **salida** ventana.</span><span class="sxs-lookup"><span data-stu-id="1d2b8-369">Instructions are displayed in hello **Output** window.</span></span> <span data-ttu-id="1d2b8-370">tooproceed tooupload archivo hello, guardar el archivo JSON de hello (CTRL+s).</span><span class="sxs-lookup"><span data-stu-id="1d2b8-370">tooproceed tooupload hello file, save (Ctrl+S) hello JSON file.</span></span>

       ![Herramientas de Data Lake para Visual Studio Code: ruta de acceso de archivo](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-upload-file.png)

3.  <span data-ttu-id="1d2b8-372">Resultados: Hola **salida** ventana muestra el estado de carga del archivo de Hola.</span><span class="sxs-lookup"><span data-stu-id="1d2b8-372">Results: hello **Output** window displays hello file upload status.</span></span>

       ![Herramientas de Data Lake para Visual Studio Code: estado de carga](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-upload-status.png)     

<span data-ttu-id="1d2b8-374">Otro tooupload de manera un archivo toostorage es a través de Hola haga clic en el menú en la ruta de acceso completa del archivo de Hola o ruta de acceso relativa del archivo de hello en el editor de script de Hola.</span><span class="sxs-lookup"><span data-stu-id="1d2b8-374">Another way tooupload a file toostorage is through hello right-click menu on hello file's full path or hello file's relative path in hello script editor.</span></span> <span data-ttu-id="1d2b8-375">Escriba la ruta de acceso de archivo local de hello y, a continuación, seleccione la cuenta de hello.</span><span class="sxs-lookup"><span data-stu-id="1d2b8-375">Enter hello local file path, and then select hello account.</span></span> <span data-ttu-id="1d2b8-376">Hola **salida** ventana muestra el estado de la carga de Hola.</span><span class="sxs-lookup"><span data-stu-id="1d2b8-376">hello **Output** window displays hello upload status.</span></span> 

### <a name="open-azure-storage-explorer"></a><span data-ttu-id="1d2b8-377">Apertura del Explorador de Azure Storage</span><span class="sxs-lookup"><span data-stu-id="1d2b8-377">Open Azure Storage Explorer</span></span>
<span data-ttu-id="1d2b8-378">Puede abrir **Azure Storage Explorer** escribiendo el comando hello **ADL: Abrir Explorador de almacenamiento de Azure Web** o mediante la selección de menú contextual Hola.</span><span class="sxs-lookup"><span data-stu-id="1d2b8-378">You can open **Azure Storage Explorer** by entering hello command **ADL: Open Web Azure Storage Explorer** or by selecting it from hello right-click context menu.</span></span>

<span data-ttu-id="1d2b8-379">**tooopen Explorador de almacenamiento de Azure**</span><span class="sxs-lookup"><span data-stu-id="1d2b8-379">**tooopen Azure Storage Explorer**</span></span>

1. <span data-ttu-id="1d2b8-380">Seleccione Ctrl + Mayús + P tooopen Hola comando paleta.</span><span class="sxs-lookup"><span data-stu-id="1d2b8-380">Select Ctrl+Shift+P tooopen hello command palette.</span></span>
2. <span data-ttu-id="1d2b8-381">Escriba **Abrir Explorador de almacenamiento de Azure Web** o haga doble clic en una ruta de acceso relativa o la ruta de acceso completa de hello en el editor de secuencia de comandos de hello y, a continuación, seleccione **Abrir Explorador de almacenamiento de Azure Web**.</span><span class="sxs-lookup"><span data-stu-id="1d2b8-381">Enter **Open Web Azure Storage Explorer** or right-click on a relative path or hello full path in hello script editor, and then select **Open Web Azure Storage Explorer**.</span></span>
3. <span data-ttu-id="1d2b8-382">Seleccione una cuenta de Data Lake Analytics.</span><span class="sxs-lookup"><span data-stu-id="1d2b8-382">Select a Data Lake Analytics account.</span></span>

<span data-ttu-id="1d2b8-383">Data Lake Tools abre la ruta de acceso de almacenamiento de Azure de hello en hello portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="1d2b8-383">Data Lake Tools opens hello Azure storage path in hello Azure portal.</span></span> <span data-ttu-id="1d2b8-384">Puede encontrar archivo de Hola de hello ruta de acceso y la vista previa de web de Hola.</span><span class="sxs-lookup"><span data-stu-id="1d2b8-384">You can find hello path and preview hello file from hello web.</span></span>

### <a name="local-run-and-local-debug-for-windows-users"></a><span data-ttu-id="1d2b8-385">Ejecución y depuración locales de usuarios de Windows</span><span class="sxs-lookup"><span data-stu-id="1d2b8-385">Local run and local debug for Windows users</span></span>
<span data-ttu-id="1d2b8-386">Ejecución local de SQL U comprueba los datos locales y valida el script localmente, antes de que el código sea publicada tooData Lake Analytics.</span><span class="sxs-lookup"><span data-stu-id="1d2b8-386">U-SQL local run tests your local data and validates your script locally, before your code is published tooData Lake Analytics.</span></span> <span data-ttu-id="1d2b8-387">Hola característica de depuración local permite toocomplete Hola siguiente las tareas antes de que el código envía tooData Lake Analytics:</span><span class="sxs-lookup"><span data-stu-id="1d2b8-387">hello local debug feature enables you toocomplete hello following tasks before your code is submitted tooData Lake Analytics:</span></span> 
- <span data-ttu-id="1d2b8-388">Depure el código subyacente de C#.</span><span class="sxs-lookup"><span data-stu-id="1d2b8-388">Debug your C# code-behind.</span></span> 
- <span data-ttu-id="1d2b8-389">Recorrer el código de hello.</span><span class="sxs-lookup"><span data-stu-id="1d2b8-389">Step through hello code.</span></span> 
- <span data-ttu-id="1d2b8-390">Valide localmente el script.</span><span class="sxs-lookup"><span data-stu-id="1d2b8-390">Validate your script locally.</span></span>

<span data-ttu-id="1d2b8-391">Para instrucciones sobre la ejecución y la depuración locales, consulte [Ejecución y depuración locales de U-SQL con Visual Studio Code](data-lake-tools-for-vscode-local-run-and-debug.md).</span><span class="sxs-lookup"><span data-stu-id="1d2b8-391">For instructions on local run and local debug, see [U-SQL local run and local debug with Visual Studio Code](data-lake-tools-for-vscode-local-run-and-debug.md).</span></span>

## <a name="additional-features"></a><span data-ttu-id="1d2b8-392">Características adicionales</span><span class="sxs-lookup"><span data-stu-id="1d2b8-392">Additional features</span></span>

<span data-ttu-id="1d2b8-393">Data Lake Tools para VS Code admite Hola siguientes características:</span><span class="sxs-lookup"><span data-stu-id="1d2b8-393">Data Lake Tools for VS Code supports hello following features:</span></span>

-   <span data-ttu-id="1d2b8-394">Autocompletar de IntelliSense: aparecen sugerencias en ventanas emergentes en torno a elementos, como palabras clave, métodos y variables.</span><span class="sxs-lookup"><span data-stu-id="1d2b8-394">IntelliSense auto-complete: Suggestions appear in pop-up windows around items, such as keywords, methods, and variables.</span></span> <span data-ttu-id="1d2b8-395">Los distintos iconos representan diferentes tipos de objetos de hello:</span><span class="sxs-lookup"><span data-stu-id="1d2b8-395">Different icons represent different types of hello objects:</span></span>

    - <span data-ttu-id="1d2b8-396">Tipo de datos de escala</span><span class="sxs-lookup"><span data-stu-id="1d2b8-396">Scala data type</span></span>
    - <span data-ttu-id="1d2b8-397">Tipo de datos complejo</span><span class="sxs-lookup"><span data-stu-id="1d2b8-397">Complex data type</span></span>
    - <span data-ttu-id="1d2b8-398">UDT integrada</span><span class="sxs-lookup"><span data-stu-id="1d2b8-398">Built-in UDTs</span></span>
    - <span data-ttu-id="1d2b8-399">Clases y colección .NET</span><span class="sxs-lookup"><span data-stu-id="1d2b8-399">.NET collection and classes</span></span>
    - <span data-ttu-id="1d2b8-400">Expresiones de C#</span><span class="sxs-lookup"><span data-stu-id="1d2b8-400">C# expressions</span></span>
    - <span data-ttu-id="1d2b8-401">UDF, UDO y UDAAG integrados de C#</span><span class="sxs-lookup"><span data-stu-id="1d2b8-401">Built-in C# UDFs, UDOs, and UDAAGs</span></span> 
    - <span data-ttu-id="1d2b8-402">Funciones de U-SQL</span><span class="sxs-lookup"><span data-stu-id="1d2b8-402">U-SQL functions</span></span>
    - <span data-ttu-id="1d2b8-403">Función de ventana de U-SQL</span><span class="sxs-lookup"><span data-stu-id="1d2b8-403">U-SQL windowing function</span></span>
 
    ![Tipos de objetos de IntelliSense de Data Lake Tools para Visual Studio Code](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-auto-complete-objects.png)
 
-   <span data-ttu-id="1d2b8-405">IntelliSense Autocompletar en metadatos de análisis de Data Lake: Data Lake Tools descarga información de metadatos de análisis de Data Lake de hello localmente.</span><span class="sxs-lookup"><span data-stu-id="1d2b8-405">IntelliSense auto-complete on Data Lake Analytics metadata: Data Lake Tools downloads hello Data Lake Analytics metadata information locally.</span></span> <span data-ttu-id="1d2b8-406">característica de IntelliSense de Hello rellena automáticamente los objetos, incluida la base de datos de hello, esquema, tabla, vista, función con valores de tabla, procedimientos y ensamblados de C#, de los metadatos de análisis de Data Lake Hola.</span><span class="sxs-lookup"><span data-stu-id="1d2b8-406">hello IntelliSense feature automatically populates objects, including hello database, schema, table, view, table-valued function, procedures, and C# assemblies, from hello Data Lake Analytics metadata.</span></span>
 
    ![Metadatos de IntelliSense de Data Lake Tools para Visual Studio Code](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-auto-complete-metastore.png)

-   <span data-ttu-id="1d2b8-408">Marcador de error de IntelliSense: Data Lake Tools subraya Hola editar errores de SQL de U y C#.</span><span class="sxs-lookup"><span data-stu-id="1d2b8-408">IntelliSense error marker: Data Lake Tools underlines hello editing errors for U-SQL and C#.</span></span> 
-   <span data-ttu-id="1d2b8-409">Resaltado de sintaxis: Data Lake Tools usa elementos de toodifferentiate de distintos colores, como las variables, palabras clave, tipo de datos y funciones.</span><span class="sxs-lookup"><span data-stu-id="1d2b8-409">Syntax highlights: Data Lake Tools uses different colors toodifferentiate items, such as variables, keywords, data type, and functions.</span></span> 

    ![Aspectos destacados de la sintaxis de Data Lake Tools para Visual Studio Code](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-syntax-highlights.png)

## <a name="next-steps"></a><span data-ttu-id="1d2b8-411">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="1d2b8-411">Next steps</span></span>

- <span data-ttu-id="1d2b8-412">Para la ejecución y depuración locales de U-SQL con Visual Studio Code, consulte [Ejecución y depuración locales de U-SQL con Visual Studio Code](data-lake-tools-for-vscode-local-run-and-debug.md).</span><span class="sxs-lookup"><span data-stu-id="1d2b8-412">For U-SQL local run and local debug with Visual Studio Code, see [U-SQL local run and local debug with Visual Studio Code](data-lake-tools-for-vscode-local-run-and-debug.md).</span></span>
- <span data-ttu-id="1d2b8-413">Para información detallada sobre cómo empezar a trabajar con Data Lake Analytics, consulte [Tutorial: Introducción a Azure Data Lake Analytics](data-lake-analytics-get-started-portal.md).</span><span class="sxs-lookup"><span data-stu-id="1d2b8-413">For getting-started information on Data Lake Analytics, see [Tutorial: Get started with Azure Data Lake Analytics](data-lake-analytics-get-started-portal.md).</span></span>
- <span data-ttu-id="1d2b8-414">Para información sobre Herramientas de Data Lake para Visual Studio, consulte [Tutorial: Desarrollo de scripts U-SQL mediante Herramientas de Data Lake para Visual Studio](data-lake-analytics-data-lake-tools-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="1d2b8-414">For information about Data Lake Tools for Visual Studio, see [Tutorial: Develop U-SQL scripts by using Data Lake Tools for Visual Studio](data-lake-analytics-data-lake-tools-get-started.md).</span></span>
- <span data-ttu-id="1d2b8-415">Para información sobre el desarrollo de ensamblados, consulte [Desarrollo de ensamblados U-SQL para trabajos de Azure Data Lake Analytics](data-lake-analytics-u-sql-develop-assemblies.md).</span><span class="sxs-lookup"><span data-stu-id="1d2b8-415">For information on developing assemblies, see [Develop U-SQL assemblies for Azure Data Lake Analytics jobs](data-lake-analytics-u-sql-develop-assemblies.md).</span></span>



