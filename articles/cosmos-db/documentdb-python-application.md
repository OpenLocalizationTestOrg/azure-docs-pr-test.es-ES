---
title: "tutorial de aplicación de aaaPython matraz web para la base de datos de Azure Cosmos | Documentos de Microsoft"
description: "Revise un tutorial de base de datos sobre el uso de datos de base de datos de Azure Cosmos toostore y acceso desde una aplicación web de Python matraz hospedada en Azure. Encuentre soluciones de desarrollo de aplicaciones."
keywords: "Desarrollo de aplicaciones, python flask, aplicación web de python, desarrollo web de python"
services: cosmos-db
documentationcenter: python
author: mimig1
manager: jhubbard
editor: cgronlun
ms.assetid: 20ebec18-67c2-4988-a760-be7c30cfb745
ms.service: cosmos-db
ms.workload: data-management
ms.tgt_pltfrm: na
ms.devlang: python
ms.topic: article
ms.date: 08/09/2017
ms.author: mimig
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 87b73c656ed96a7efbd162843a1529d435f027f0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="build-a-python-flask-web-application-using-azure-cosmos-db"></a><span data-ttu-id="6b2c2-105">Compilación de una aplicación web Node.js de Python Flask mediante Azure cosmos DB</span><span class="sxs-lookup"><span data-stu-id="6b2c2-105">Build a Python Flask web application using Azure Cosmos DB</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="6b2c2-106">.NET</span><span class="sxs-lookup"><span data-stu-id="6b2c2-106">.NET</span></span>](documentdb-dotnet-application.md)
> * [<span data-ttu-id="6b2c2-107">Node.js</span><span class="sxs-lookup"><span data-stu-id="6b2c2-107">Node.js</span></span>](documentdb-nodejs-application.md)
> * [<span data-ttu-id="6b2c2-108">Java</span><span class="sxs-lookup"><span data-stu-id="6b2c2-108">Java</span></span>](documentdb-java-application.md)
> * [<span data-ttu-id="6b2c2-109">Python</span><span class="sxs-lookup"><span data-stu-id="6b2c2-109">Python</span></span>](documentdb-python-application.md)
> 
> 

<span data-ttu-id="6b2c2-110">Este tutorial muestra cómo toouse base de datos de Azure Cosmos toostore y acceso a datos desde un Python web aplicación hospedada en Azure y se da por supuesto que tiene cierta experiencia previa con Python y sitios Web de Azure.</span><span class="sxs-lookup"><span data-stu-id="6b2c2-110">This tutorial shows you how toouse Azure Cosmos DB toostore and access data from a Python web application hosted on Azure and presumes that you have some prior experience using Python and Azure websites.</span></span>

<span data-ttu-id="6b2c2-111">En este tutorial de base de datos se trata lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="6b2c2-111">This database tutorial covers:</span></span>

1. <span data-ttu-id="6b2c2-112">Crear y aprovisionar una cuenta de Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="6b2c2-112">Creating and provisioning a Cosmos DB account.</span></span>
2. <span data-ttu-id="6b2c2-113">Crear una aplicación Python Flask.</span><span class="sxs-lookup"><span data-stu-id="6b2c2-113">Creating a Python Flask application.</span></span>
3. <span data-ttu-id="6b2c2-114">Conexión tooand con Cosmos DB desde la aplicación web.</span><span class="sxs-lookup"><span data-stu-id="6b2c2-114">Connecting tooand using Cosmos DB from your web application.</span></span>
4. <span data-ttu-id="6b2c2-115">Implementación de aplicación tooAzure de hello web.</span><span class="sxs-lookup"><span data-stu-id="6b2c2-115">Deploying hello web application tooAzure.</span></span>

<span data-ttu-id="6b2c2-116">Si sigue este tutorial, compilará una aplicación simple de votación que le permite toovote para un sondeo.</span><span class="sxs-lookup"><span data-stu-id="6b2c2-116">By following this tutorial, you will build a simple voting application that allows you toovote for a poll.</span></span>

![Captura de pantalla de aplicación de votación de hello creada por este tutorial de base de datos](./media/documentdb-python-application/cosmos-db-pythonr-run-application.png)

## <a name="database-tutorial-prerequisites"></a><span data-ttu-id="6b2c2-118">Requisitos previos del tutorial de base de datos</span><span class="sxs-lookup"><span data-stu-id="6b2c2-118">Database tutorial prerequisites</span></span>
<span data-ttu-id="6b2c2-119">Antes de seguir las instrucciones de hello en este artículo, debe asegurarse de que tiene instalado el siguiente hello:</span><span class="sxs-lookup"><span data-stu-id="6b2c2-119">Before following hello instructions in this article, you should ensure that you have hello following installed:</span></span>

* <span data-ttu-id="6b2c2-120">Una cuenta de Azure activa.</span><span class="sxs-lookup"><span data-stu-id="6b2c2-120">An active Azure account.</span></span> <span data-ttu-id="6b2c2-121">En caso de no tener ninguna, puede crear una cuenta de evaluación gratuita en tan solo unos minutos.</span><span class="sxs-lookup"><span data-stu-id="6b2c2-121">If you don't have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="6b2c2-122">Para obtener más información, consulte [Evaluación gratuita de Azure](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="6b2c2-122">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
 
    <span data-ttu-id="6b2c2-123">OR</span><span class="sxs-lookup"><span data-stu-id="6b2c2-123">OR</span></span> 

    <span data-ttu-id="6b2c2-124">Una instalación local de hello [emulador de base de datos de Azure Cosmos](local-emulator.md).</span><span class="sxs-lookup"><span data-stu-id="6b2c2-124">A local installation of hello [Azure Cosmos DB Emulator](local-emulator.md).</span></span>
* <span data-ttu-id="6b2c2-125">[Microsoft Visual Studio Community 2017](http://www.visualstudio.com/)</span><span class="sxs-lookup"><span data-stu-id="6b2c2-125">[Microsoft Visual Studio Community 2017](http://www.visualstudio.com/).</span></span>  
* <span data-ttu-id="6b2c2-126">[Herramientas de Python para Visual Studio](https://github.com/Microsoft/PTVS/)</span><span class="sxs-lookup"><span data-stu-id="6b2c2-126">[Python Tools for Visual Studio](https://github.com/Microsoft/PTVS/).</span></span>  
* <span data-ttu-id="6b2c2-127">[SDK de Microsoft Azure para Python 2.7](https://azure.microsoft.com/downloads/)</span><span class="sxs-lookup"><span data-stu-id="6b2c2-127">[Microsoft Azure SDK for Python 2.7](https://azure.microsoft.com/downloads/).</span></span> 
* <span data-ttu-id="6b2c2-128">[Python 2.7.13](https://www.python.org/downloads/windows/)</span><span class="sxs-lookup"><span data-stu-id="6b2c2-128">[Python 2.7.13](https://www.python.org/downloads/windows/).</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="6b2c2-129">Si va a instalar Python 2.7 para hello primera vez, asegúrese de que en la pantalla de bienvenida personalizar Python 2.7.13, selecciona **agregar python.exe tooPath**.</span><span class="sxs-lookup"><span data-stu-id="6b2c2-129">If you are installing Python 2.7 for hello first time, ensure that in hello Customize Python 2.7.13 screen, you select **Add python.exe tooPath**.</span></span>
> 
> ![Captura de pantalla de pantalla de Python personalizar 2.7.11 de bienvenida, donde es necesario tooselect agregar python.exe tooPath](./media/documentdb-python-application/cosmos-db-python-install.png)
> 
> 

* <span data-ttu-id="6b2c2-131">[Compilador de Microsoft Visual C++ 2013 para Python 2.7](https://www.microsoft.com/en-us/download/details.aspx?id=44266)</span><span class="sxs-lookup"><span data-stu-id="6b2c2-131">[Microsoft Visual C++ Compiler for Python 2.7](https://www.microsoft.com/en-us/download/details.aspx?id=44266).</span></span>

## <a name="step-1-create-an-azure-cosmos-db-database-account"></a><span data-ttu-id="6b2c2-132">Paso 1: Creación de una cuenta de base de datos de Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="6b2c2-132">Step 1: Create an Azure Cosmos DB database account</span></span>
<span data-ttu-id="6b2c2-133">Para comenzar, creemos una cuenta de Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="6b2c2-133">Let's start by creating an Cosmos DB account.</span></span> <span data-ttu-id="6b2c2-134">Si ya tiene una cuenta o si usas Hola emulador de base de datos de Azure Cosmos para este tutorial, puede omitir demasiado[paso 2: crear una nueva aplicación web de Python matraz](#step-2-create-a-new-python-flask-web-application).</span><span class="sxs-lookup"><span data-stu-id="6b2c2-134">If you already have an account or if you are using hello Azure Cosmos DB Emulator for this tutorial, you can skip too[Step 2: Create a new Python Flask web application](#step-2-create-a-new-python-flask-web-application).</span></span>

[!INCLUDE [cosmos-db-create-dbaccount](../../includes/cosmos-db-create-dbaccount.md)]

<br/>
<span data-ttu-id="6b2c2-135">Ahora se le indicará cómo toocreate una nueva aplicación web de Python matraz de hello masa.</span><span class="sxs-lookup"><span data-stu-id="6b2c2-135">We will now walk through how toocreate a new Python Flask web application from hello ground up.</span></span>

## <a name="step-2-create-a-new-python-flask-web-application"></a><span data-ttu-id="6b2c2-136">Paso 2: Creación de una nueva aplicación web de Python Flask</span><span class="sxs-lookup"><span data-stu-id="6b2c2-136">Step 2: Create a new Python Flask web application</span></span>
1. <span data-ttu-id="6b2c2-137">En Visual Studio, en hello **archivo** menú, seleccione demasiado**New**y, a continuación, haga clic en **proyecto**.</span><span class="sxs-lookup"><span data-stu-id="6b2c2-137">In Visual Studio, on hello **File** menu, point too**New**, and then click **Project**.</span></span>
   
    <span data-ttu-id="6b2c2-138">Hola **nuevo proyecto** aparece el cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="6b2c2-138">hello **New Project** dialog box appears.</span></span>
2. <span data-ttu-id="6b2c2-139">En el panel izquierdo de hello, expanda **plantillas** y, a continuación, **Python**y, a continuación, haga clic en **Web**.</span><span class="sxs-lookup"><span data-stu-id="6b2c2-139">In hello left pane, expand **Templates** and then **Python**, and then click **Web**.</span></span> 
3. <span data-ttu-id="6b2c2-140">Seleccione **matraz Web proyecto** en el panel central de hello, luego, en hello **nombre** cuadro, escriba **tutorial**y, a continuación, haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="6b2c2-140">Select **Flask  Web Project** in hello center pane, then in hello **Name** box type **tutorial**, and then click **OK**.</span></span> <span data-ttu-id="6b2c2-141">Recuerde que los nombres de paquete de Python deben ser en minúsculas, como se describe en hello [Guía de estilo para el código de Python](https://www.python.org/dev/peps/pep-0008/#package-and-module-names).</span><span class="sxs-lookup"><span data-stu-id="6b2c2-141">Remember that Python package names should be all lowercase, as described in hello [Style Guide for Python Code](https://www.python.org/dev/peps/pep-0008/#package-and-module-names).</span></span>
   
    <span data-ttu-id="6b2c2-142">Para esos tooPython nueva matraz, es un marco de desarrollo de aplicaciones web que permite crear aplicaciones web de Python con mayor rapidez.</span><span class="sxs-lookup"><span data-stu-id="6b2c2-142">For those new tooPython Flask, it is a web application development framework that helps you build web applications in Python faster.</span></span>
   
    ![Captura de pantalla de ventana de hello nuevo proyecto en Visual Studio con Python resaltado en hello dejado, Python matraz Web proyecto seleccionado en medio de Hola y tutorial de nombre de hello en el cuadro de nombre de Hola](./media/documentdb-python-application/image9.png)
4. <span data-ttu-id="6b2c2-144">Hola **Python Tools para Visual Studio** ventana, haga clic en **instalar en un entorno virtual**.</span><span class="sxs-lookup"><span data-stu-id="6b2c2-144">In hello **Python Tools for Visual Studio** window, click **Install into a virtual environment**.</span></span> 
   
    ![Captura de pantalla de tutorial de base de datos de hello - Python Tools para la ventana de Visual Studio](./media/documentdb-python-application/python-install-virtual-environment.png)
5. <span data-ttu-id="6b2c2-146">Hola **agregar entorno Virtual** ventana, puede aceptar los valores predeterminados de Hola y usar Python 2.7 como entorno de base de hello porque PyDocumentDB no admite actualmente Python 3.x y, a continuación, haga clic en **crear**.</span><span class="sxs-lookup"><span data-stu-id="6b2c2-146">In hello **Add Virtual Environment** window, you can accept hello defaults and use Python 2.7 as hello base environment because PyDocumentDB does not currently support Python 3.x, and then click **Create**.</span></span> <span data-ttu-id="6b2c2-147">Esto configura el entorno virtual de Python Hola necesario para el proyecto.</span><span class="sxs-lookup"><span data-stu-id="6b2c2-147">This sets up hello required Python virtual environment for your project.</span></span>
   
    ![Captura de pantalla de tutorial de base de datos de hello - Python Tools para la ventana de Visual Studio](./media/documentdb-python-application/image10_A.png)
   
    <span data-ttu-id="6b2c2-149">muestra de la ventana de salida de Hello `Successfully installed Flask-0.10.1 Jinja2-2.8 MarkupSafe-0.23 Werkzeug-0.11.5 itsdangerous-0.24 'requirements.txt' was installed successfully.` cuando se instala correctamente el entorno de Hola.</span><span class="sxs-lookup"><span data-stu-id="6b2c2-149">hello output window displays `Successfully installed Flask-0.10.1 Jinja2-2.8 MarkupSafe-0.23 Werkzeug-0.11.5 itsdangerous-0.24 'requirements.txt' was installed successfully.` when hello environment is successfully installed.</span></span>

## <a name="step-3-modify-hello-python-flask-web-application"></a><span data-ttu-id="6b2c2-150">Paso 3: Modificar la aplicación web de hello matraz de Python</span><span class="sxs-lookup"><span data-stu-id="6b2c2-150">Step 3: Modify hello Python Flask web application</span></span>
### <a name="add-hello-python-flask-packages-tooyour-project"></a><span data-ttu-id="6b2c2-151">Agregar proyecto de tooyour de paquetes de saludo matraz de Python</span><span class="sxs-lookup"><span data-stu-id="6b2c2-151">Add hello Python Flask packages tooyour project</span></span>
<span data-ttu-id="6b2c2-152">Después de configurar el proyecto, deberá tooadd Hola necesario matraz paquetes tooyour proyecto, incluida la pydocumentdb, paquete de Python Hola de documentos.</span><span class="sxs-lookup"><span data-stu-id="6b2c2-152">After your project is set up, you'll need tooadd hello required Flask packages tooyour project, including pydocumentdb, hello Python package for DocumentDB.</span></span>

1. <span data-ttu-id="6b2c2-153">En el Explorador de soluciones, abra el archivo de hello denominado **requirements.txt** y reemplace el contenido de hello con siguiente hello:</span><span class="sxs-lookup"><span data-stu-id="6b2c2-153">In Solution Explorer, open hello file named **requirements.txt** and replace hello contents with hello following:</span></span>
   
        flask==0.9
        flask-mail==0.7.6
        sqlalchemy==0.7.9
        flask-sqlalchemy==0.16
        sqlalchemy-migrate==0.7.2
        flask-whooshalchemy==0.55a
        flask-wtf==0.8.4
        pytz==2013b
        flask-babel==0.8
        flup
        pydocumentdb>=1.0.0
2. <span data-ttu-id="6b2c2-154">Guardar hello **requirements.txt** archivo.</span><span class="sxs-lookup"><span data-stu-id="6b2c2-154">Save hello **requirements.txt** file.</span></span> 
3. <span data-ttu-id="6b2c2-155">En el Explorador de soluciones, haga clic con el botón derecho en **env** y haga clic en **Install from requirements.txt**.</span><span class="sxs-lookup"><span data-stu-id="6b2c2-155">In Solution Explorer, right-click **env** and click **Install from requirements.txt**.</span></span>
   
    ![Captura de pantalla que muestra env (Python 2.7) seleccionado con la instalación de requirements.txt resaltado en la lista de Hola](./media/documentdb-python-application/cosmos-db-python-install-from-requirements.png)
   
    <span data-ttu-id="6b2c2-157">Después de la instalación correcta, la ventana de salida de hello muestra siguiente hello:</span><span class="sxs-lookup"><span data-stu-id="6b2c2-157">After successful installation, hello output window displays hello following:</span></span>
   
        Successfully installed Babel-2.3.2 Tempita-0.5.2 WTForms-2.1 Whoosh-2.7.4 blinker-1.4 decorator-4.0.9 flask-0.9 flask-babel-0.8 flask-mail-0.7.6 flask-sqlalchemy-0.16 flask-whooshalchemy-0.55a0 flask-wtf-0.8.4 flup-1.0.2 pydocumentdb-1.6.1 pytz-2013b0 speaklater-1.3 sqlalchemy-0.7.9 sqlalchemy-migrate-0.7.2
   
   > [!NOTE]
   > <span data-ttu-id="6b2c2-158">En raras ocasiones, podría ver un error en la ventana de salida de hello.</span><span class="sxs-lookup"><span data-stu-id="6b2c2-158">In rare cases, you might see a failure in hello output window.</span></span> <span data-ttu-id="6b2c2-159">Si esto ocurre, comprobar si el error de hello es toocleanup relacionado.</span><span class="sxs-lookup"><span data-stu-id="6b2c2-159">If this happens, check if hello error is related toocleanup.</span></span> <span data-ttu-id="6b2c2-160">A veces se produce un error en la limpieza de hello, pero la instalación Hola aún será correcto (desplazarse hacia arriba en tooverify de ventana de salida de hello esto).</span><span class="sxs-lookup"><span data-stu-id="6b2c2-160">Sometimes hello cleanup fails, but hello installation will still be successful (scroll up in hello output window tooverify this).</span></span> <span data-ttu-id="6b2c2-161">Puede comprobar la instalación por [entorno virtual de comprobación hello](#verify-the-virtual-environment).</span><span class="sxs-lookup"><span data-stu-id="6b2c2-161">You can check your installation by [Verifying hello virtual environment](#verify-the-virtual-environment).</span></span> <span data-ttu-id="6b2c2-162">Si no se pudo instalar Hola pero Hola comprobación es correcta, es toocontinue Aceptar.</span><span class="sxs-lookup"><span data-stu-id="6b2c2-162">If hello installation failed but hello verification is successful, it's OK toocontinue.</span></span>
   > 
   > 

### <a name="verify-hello-virtual-environment"></a><span data-ttu-id="6b2c2-163">Comprobar el entorno virtual de Hola</span><span class="sxs-lookup"><span data-stu-id="6b2c2-163">Verify hello virtual environment</span></span>
<span data-ttu-id="6b2c2-164">Asegurémonos de que todo esté instalado correctamente.</span><span class="sxs-lookup"><span data-stu-id="6b2c2-164">Let's make sure that everything is installed correctly.</span></span>

1. <span data-ttu-id="6b2c2-165">Compile la solución de hello presionando **Ctrl**+**MAYÚS**+**B**.</span><span class="sxs-lookup"><span data-stu-id="6b2c2-165">Build hello solution by pressing **Ctrl**+**Shift**+**B**.</span></span>
2. <span data-ttu-id="6b2c2-166">Cuando se complete correctamente la compilación de hello, iniciar sitio Web de hello presionando **F5**.</span><span class="sxs-lookup"><span data-stu-id="6b2c2-166">Once hello build succeeds, start hello website by pressing **F5**.</span></span> <span data-ttu-id="6b2c2-167">Esta acción inicia el servidor de desarrollo de hello matraz e inicia el explorador web.</span><span class="sxs-lookup"><span data-stu-id="6b2c2-167">This launches hello Flask development server and starts your web browser.</span></span> <span data-ttu-id="6b2c2-168">Debería ver Hola después de la página.</span><span class="sxs-lookup"><span data-stu-id="6b2c2-168">You should see hello following page.</span></span>
   
    ![Hola Python matraz proyecto web vacío desarrollo mostrado en un explorador](./media/documentdb-python-application/image12.png)
3. <span data-ttu-id="6b2c2-170">Detener la depuración de sitio Web de hello presionando **MAYÚS**+**F5** en Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="6b2c2-170">Stop debugging hello website by pressing **Shift**+**F5** in Visual Studio.</span></span>

### <a name="create-database-collection-and-document-definitions"></a><span data-ttu-id="6b2c2-171">Creación de definiciones de base de datos, colección y documento</span><span class="sxs-lookup"><span data-stu-id="6b2c2-171">Create database, collection, and document definitions</span></span>
<span data-ttu-id="6b2c2-172">Ahora vamos a crear la aplicación de votación mediante la adición de archivos nuevos y de la actualización de otros.</span><span class="sxs-lookup"><span data-stu-id="6b2c2-172">Now let's create your voting application by adding new files and updating others.</span></span>

1. <span data-ttu-id="6b2c2-173">En el Explorador de soluciones, haga clic en hello **tutorial** proyecto de equipo y haga clic en **agregar**y, a continuación, haga clic en **nuevo elemento**.</span><span class="sxs-lookup"><span data-stu-id="6b2c2-173">In Solution Explorer, right-click hello **tutorial** project, click **Add**, and then click **New Item**.</span></span> <span data-ttu-id="6b2c2-174">Seleccione **vaciar el archivo Python** y archivo de nombre hello **forms.py**.</span><span class="sxs-lookup"><span data-stu-id="6b2c2-174">Select **Empty Python File** and name hello file **forms.py**.</span></span>  
2. <span data-ttu-id="6b2c2-175">Agregar Hola siguiente archivo de código toohello forms.py y, a continuación, guarde el archivo hello.</span><span class="sxs-lookup"><span data-stu-id="6b2c2-175">Add hello following code toohello forms.py file, and then save hello file.</span></span>

```python
from flask.ext.wtf import Form
from wtforms import RadioField

class VoteForm(Form):
    deploy_preference  = RadioField('Deployment Preference', choices=[
        ('Web Site', 'Web Site'),
        ('Cloud Service', 'Cloud Service'),
        ('Virtual Machine', 'Virtual Machine')], default='Web Site')
```


### <a name="add-hello-required-imports-tooviewspy"></a><span data-ttu-id="6b2c2-176">Agregar tooviews.py de importaciones de hello necesario</span><span class="sxs-lookup"><span data-stu-id="6b2c2-176">Add hello required imports tooviews.py</span></span>
1. <span data-ttu-id="6b2c2-177">En el Explorador de soluciones, expanda hello **tutorial** carpeta y abra hello **views.py** archivo.</span><span class="sxs-lookup"><span data-stu-id="6b2c2-177">In Solution Explorer, expand hello **tutorial** folder, and open hello **views.py** file.</span></span> 
2. <span data-ttu-id="6b2c2-178">Agregar Hola siguiendo las instrucciones de importación toohello parte superior de hello **views.py** de archivos, a continuación, guarde el archivo hello.</span><span class="sxs-lookup"><span data-stu-id="6b2c2-178">Add hello following import statements toohello top of hello **views.py** file, then save hello file.</span></span> <span data-ttu-id="6b2c2-179">Estos importación PythonSDK de Cosmos DB y Hola paquetes matraz.</span><span class="sxs-lookup"><span data-stu-id="6b2c2-179">These import Cosmos DB's PythonSDK and hello Flask packages.</span></span>
   
    ```python
    from forms import VoteForm
    import config
    import pydocumentdb.document_client as document_client
    ```

### <a name="create-database-collection-and-document"></a><span data-ttu-id="6b2c2-180">Creación de base de datos, colección y documento</span><span class="sxs-lookup"><span data-stu-id="6b2c2-180">Create database, collection, and document</span></span>
* <span data-ttu-id="6b2c2-181">Todavía en **views.py**, agregar Hola siguiente código toohello final de archivo hello.</span><span class="sxs-lookup"><span data-stu-id="6b2c2-181">Still in **views.py**, add hello following code toohello end of hello file.</span></span> <span data-ttu-id="6b2c2-182">Esto se encarga de crear base de datos de hello utilizado por formulario Hola.</span><span class="sxs-lookup"><span data-stu-id="6b2c2-182">This takes care of creating hello database used by hello form.</span></span> <span data-ttu-id="6b2c2-183">No elimine ninguno de código existente de hello en **views.py**.</span><span class="sxs-lookup"><span data-stu-id="6b2c2-183">Do not delete any of hello existing code in **views.py**.</span></span> <span data-ttu-id="6b2c2-184">Basta con anexar este extremo toohello.</span><span class="sxs-lookup"><span data-stu-id="6b2c2-184">Simply append this toohello end.</span></span>

```python
@app.route('/create')
def create():
    """Renders hello contact page."""
    client = document_client.DocumentClient(config.DOCUMENTDB_HOST, {'masterKey': config.DOCUMENTDB_KEY})

    # Attempt toodelete hello database.  This allows this toobe used toorecreate as well as create
    try:
        db = next((data for data in client.ReadDatabases() if data['id'] == config.DOCUMENTDB_DATABASE))
        client.DeleteDatabase(db['_self'])
    except:
        pass

    # Create database
    db = client.CreateDatabase({ 'id': config.DOCUMENTDB_DATABASE })

    # Create collection
    collection = client.CreateCollection(db['_self'],{ 'id': config.DOCUMENTDB_COLLECTION })

    # Create document
    document = client.CreateDocument(collection['_self'],
        { 'id': config.DOCUMENTDB_DOCUMENT,
          'Web Site': 0,
          'Cloud Service': 0,
          'Virtual Machine': 0,
          'name': config.DOCUMENTDB_DOCUMENT 
        })

    return render_template(
       'create.html',
        title='Create Page',
        year=datetime.now().year,
        message='You just created a new database, collection, and document.  Your old votes have been deleted')
```


### <a name="read-database-collection-document-and-submit-form"></a><span data-ttu-id="6b2c2-185">Lectura de la base de datos, la colección y el documento, y envío del formulario</span><span class="sxs-lookup"><span data-stu-id="6b2c2-185">Read database, collection, document, and submit form</span></span>
* <span data-ttu-id="6b2c2-186">Todavía en **views.py**, agregar Hola siguiente código toohello final de archivo hello.</span><span class="sxs-lookup"><span data-stu-id="6b2c2-186">Still in **views.py**, add hello following code toohello end of hello file.</span></span> <span data-ttu-id="6b2c2-187">Esto se encarga de configurar la forma de hello, leer el documento, la recopilación y la base de datos de Hola.</span><span class="sxs-lookup"><span data-stu-id="6b2c2-187">This takes care of setting up hello form, reading hello database, collection, and document.</span></span> <span data-ttu-id="6b2c2-188">No elimine ninguno de código existente de hello en **views.py**.</span><span class="sxs-lookup"><span data-stu-id="6b2c2-188">Do not delete any of hello existing code in **views.py**.</span></span> <span data-ttu-id="6b2c2-189">Basta con anexar este extremo toohello.</span><span class="sxs-lookup"><span data-stu-id="6b2c2-189">Simply append this toohello end.</span></span>

```python
@app.route('/vote', methods=['GET', 'POST'])
def vote(): 
    form = VoteForm()
    replaced_document ={}
    if form.validate_on_submit(): # is user submitted vote  
        client = document_client.DocumentClient(config.DOCUMENTDB_HOST, {'masterKey': config.DOCUMENTDB_KEY})

        # Read databases and take first since id should not be duplicated.
        db = next((data for data in client.ReadDatabases() if data['id'] == config.DOCUMENTDB_DATABASE))

        # Read collections and take first since id should not be duplicated.
        coll = next((coll for coll in client.ReadCollections(db['_self']) if coll['id'] == config.DOCUMENTDB_COLLECTION))

        # Read documents and take first since id should not be duplicated.
        doc = next((doc for doc in client.ReadDocuments(coll['_self']) if doc['id'] == config.DOCUMENTDB_DOCUMENT))

        # Take hello data from hello deploy_preference and increment our database
        doc[form.deploy_preference.data] = doc[form.deploy_preference.data] + 1
        replaced_document = client.ReplaceDocument(doc['_self'], doc)

        # Create a model toopass tooresults.html
        class VoteObject:
            choices = dict()
            total_votes = 0

        vote_object = VoteObject()
        vote_object.choices = {
            "Web Site" : doc['Web Site'],
            "Cloud Service" : doc['Cloud Service'],
            "Virtual Machine" : doc['Virtual Machine']
        }
        vote_object.total_votes = sum(vote_object.choices.values())

        return render_template(
            'results.html', 
            year=datetime.now().year, 
            vote_object = vote_object)

    else :
        return render_template(
            'vote.html', 
            title = 'Vote',
            year=datetime.now().year,
            form = form)
```


### <a name="create-hello-html-files"></a><span data-ttu-id="6b2c2-190">Crear Hola archivos HTML</span><span class="sxs-lookup"><span data-stu-id="6b2c2-190">Create hello HTML files</span></span>
1. <span data-ttu-id="6b2c2-191">En el Explorador de soluciones, en hello **tutorial** carpeta, derecho, haga clic en hello **plantillas** carpeta, haga clic en **agregar**y, a continuación, haga clic en **nuevo elemento**.</span><span class="sxs-lookup"><span data-stu-id="6b2c2-191">In Solution Explorer, in hello **tutorial** folder, right click hello **templates** folder, click **Add**, and then click **New Item**.</span></span> 
2. <span data-ttu-id="6b2c2-192">Seleccione **página HTML**y, a continuación, en hello cuadro Nombre, escriba **create.html**.</span><span class="sxs-lookup"><span data-stu-id="6b2c2-192">Select **HTML Page**, and then in hello name box type **create.html**.</span></span> 
3. <span data-ttu-id="6b2c2-193">Repita los pasos 1 y 2 toocreate dos otros HTML archivos: results.html y vote.html.</span><span class="sxs-lookup"><span data-stu-id="6b2c2-193">Repeat steps 1 and 2 toocreate two additional HTML files: results.html and vote.html.</span></span>
4. <span data-ttu-id="6b2c2-194">Agregar Hola sigue código demasiado**create.html** en hello `<body>` elemento.</span><span class="sxs-lookup"><span data-stu-id="6b2c2-194">Add hello following code too**create.html** in hello `<body>` element.</span></span> <span data-ttu-id="6b2c2-195">Se muestra un mensaje que indica que hemos creado una nueva base de datos, colección y documento.</span><span class="sxs-lookup"><span data-stu-id="6b2c2-195">It displays a message stating that we created a new database, collection, and document.</span></span>
   
    ```html
    {% extends "layout.html" %}
    {% block content %}
    <h2>{{ title }}.</h2>
    <h3>{{ message }}</h3>
    <p><a href="{{ url_for('vote') }}" class="btn btn-primary btn-large">Vote &raquo;</a></p>
    {% endblock %}
    ```
5. <span data-ttu-id="6b2c2-196">Agregar Hola sigue código demasiado**results.html** en hello `<body`> elemento.</span><span class="sxs-lookup"><span data-stu-id="6b2c2-196">Add hello following code too**results.html** in hello `<body`> element.</span></span> <span data-ttu-id="6b2c2-197">Muestra los resultados de Hola de sondeo de Hola.</span><span class="sxs-lookup"><span data-stu-id="6b2c2-197">It displays hello results of hello poll.</span></span>
   
    ```html
    {% extends "layout.html" %}
    {% block content %}
    <h2>Results of hello vote</h2>
        <br />
   
    {% for choice in vote_object.choices %}
    <div class="row">
        <div class="col-sm-5">{{choice}}</div>
            <div class="col-sm-5">
                <div class="progress">
                    <div class="progress-bar" role="progressbar" aria-valuenow="{{vote_object.choices[choice]}}" aria-valuemin="0" aria-valuemax="{{vote_object.total_votes}}" style="width: {{(vote_object.choices[choice]/vote_object.total_votes)*100}}%;">
                                {{vote_object.choices[choice]}}
                </div>
            </div>
            </div>
    </div>
    {% endfor %}
   
    <br />
    <a class="btn btn-primary" href="{{ url_for('vote') }}">Vote again?</a>
    {% endblock %}
    ```
6. <span data-ttu-id="6b2c2-198">Agregar Hola sigue código demasiado**vote.html** en hello `<body`> elemento.</span><span class="sxs-lookup"><span data-stu-id="6b2c2-198">Add hello following code too**vote.html** in hello `<body`> element.</span></span> <span data-ttu-id="6b2c2-199">Muestra el sondeo de Hola y acepta Hola votos.</span><span class="sxs-lookup"><span data-stu-id="6b2c2-199">It displays hello poll and accepts hello votes.</span></span> <span data-ttu-id="6b2c2-200">Sobre cómo registrar los votos de hello, el control de hello pasa a través de tooviews.py donde se reconocerá Hola voto conversión y anexar documento hello en consecuencia.</span><span class="sxs-lookup"><span data-stu-id="6b2c2-200">On registering hello votes, hello control is passed over tooviews.py where we will recognize hello vote cast and append hello document accordingly.</span></span>
   
    ```html
    {% extends "layout.html" %}
    {% block content %}
    <h2>What is your favorite way toohost an application on Azure?</h2>
    <form action="" method="post" name="vote">
        {{form.hidden_tag()}}
            {{form.deploy_preference}}
            <button class="btn btn-primary" type="submit">Vote</button>
    </form>
    {% endblock %}
    ```
7. <span data-ttu-id="6b2c2-201">Hola **plantillas** carpeta, contenido de Hola de reemplazo de **index.html** con siguiente Hola.</span><span class="sxs-lookup"><span data-stu-id="6b2c2-201">In hello **templates** folder, replace hello contents of **index.html** with hello following.</span></span> <span data-ttu-id="6b2c2-202">Esto sirve como Hola página para la aplicación de destino.</span><span class="sxs-lookup"><span data-stu-id="6b2c2-202">This serves as hello landing page for your application.</span></span>
   
    ```html
    {% extends "layout.html" %}
    {% block content %}
    <h2>Python + Azure Cosmos DB Voting Application.</h2>
    <h3>This is a sample Cosmos DB voting application using PyDocumentDB</h3>
    <p><a href="{{ url_for('create') }}" class="btn btn-primary btn-large">Create/Clear hello Voting Database &raquo;</a></p>
    <p><a href="{{ url_for('vote') }}" class="btn btn-primary btn-large">Vote &raquo;</a></p>
    {% endblock %}
    ```

### <a name="add-a-configuration-file-and-change-hello-initpy"></a><span data-ttu-id="6b2c2-203">Agregue un archivo de configuración y cambie hello \_ \_init\_\_.py</span><span class="sxs-lookup"><span data-stu-id="6b2c2-203">Add a configuration file and change hello \_\_init\_\_.py</span></span>
1. <span data-ttu-id="6b2c2-204">En el Explorador de soluciones, haga clic en hello **tutorial** proyecto de equipo y haga clic en **agregar**, haga clic en **nuevo elemento**, seleccione **vaciar el archivo Python**y, a continuación, archivo de nombre hello **config.py**.</span><span class="sxs-lookup"><span data-stu-id="6b2c2-204">In Solution Explorer, right-click hello **tutorial** project, click **Add**, click **New Item**, select **Empty Python File**, and then name hello file **config.py**.</span></span> <span data-ttu-id="6b2c2-205">Los formularios de Flask requieren este archivo de configuración.</span><span class="sxs-lookup"><span data-stu-id="6b2c2-205">This config file is required by forms in Flask.</span></span> <span data-ttu-id="6b2c2-206">Puede usar tooprovide también una clave secreta.</span><span class="sxs-lookup"><span data-stu-id="6b2c2-206">You can use it tooprovide a secret key as well.</span></span> <span data-ttu-id="6b2c2-207">Sin embargo, dicha clave no es necesaria para este tutorial.</span><span class="sxs-lookup"><span data-stu-id="6b2c2-207">This key is not needed for this tutorial though.</span></span>
2. <span data-ttu-id="6b2c2-208">Agregue Hola siguiente tooconfig.py de código, necesitará los valores de hello tooalter de **documentos\_HOST** y **DOCUMENTDB\_clave** en el paso siguiente Hola.</span><span class="sxs-lookup"><span data-stu-id="6b2c2-208">Add hello following code tooconfig.py, you'll need tooalter hello values of **DOCUMENTDB\_HOST** and **DOCUMENTDB\_KEY** in hello next step.</span></span>
   
    ```python
    CSRF_ENABLED = True
    SECRET_KEY = 'you-will-never-guess'
   
    DOCUMENTDB_HOST = 'https://YOUR_DOCUMENTDB_NAME.documents.azure.com:443/'
    DOCUMENTDB_KEY = 'YOUR_SECRET_KEY_ENDING_IN_=='
   
    DOCUMENTDB_DATABASE = 'voting database'
    DOCUMENTDB_COLLECTION = 'voting collection'
    DOCUMENTDB_DOCUMENT = 'voting document'
    ```
3. <span data-ttu-id="6b2c2-209">Hola [portal de Azure](https://portal.azure.com/), navegue toohello **claves** hoja haciendo clic en **examinar**, **cuentas de base de datos de Azure Cosmos**, haga doble clic en el nombre de Hola Hola toouse de la cuenta y, a continuación, haga clic en hello **claves** botón en hello **Essentials** área.</span><span class="sxs-lookup"><span data-stu-id="6b2c2-209">In hello [Azure portal](https://portal.azure.com/), navigate toohello **Keys** blade by clicking **Browse**, **Azure Cosmos DB Accounts**, double-click hello name of hello account toouse, and then click hello **Keys** button in hello **Essentials** area.</span></span> <span data-ttu-id="6b2c2-210">Hola **claves** hoja, Hola copia **URI** valor y pegarlo en hello **config.py** archivo, como valor de Hola de hello **documentos\_HOST**  propiedad.</span><span class="sxs-lookup"><span data-stu-id="6b2c2-210">In hello **Keys** blade, copy hello **URI** value and paste it into hello **config.py** file, as hello value for hello **DOCUMENTDB\_HOST** property.</span></span> 
4. <span data-ttu-id="6b2c2-211">En el portal de Azure, en Hola Hola **claves** hoja, copiar el valor de Hola de hello **Primary Key** o hello **clave secundaria**y péguela en hello **config.py**  archivo, como valor de Hola de hello **DOCUMENTDB\_clave** propiedad.</span><span class="sxs-lookup"><span data-stu-id="6b2c2-211">Back in hello Azure portal, in hello **Keys** blade, copy hello value of hello **Primary Key** or hello **Secondary Key**, and paste it into hello **config.py** file, as hello value for hello **DOCUMENTDB\_KEY** property.</span></span>
5. <span data-ttu-id="6b2c2-212">Hola  **\_ \_init\_\_.py** , agregue Hola después de línea.</span><span class="sxs-lookup"><span data-stu-id="6b2c2-212">In hello **\_\_init\_\_.py** file, add hello following line.</span></span> 
   
        app.config.from_object('config')
   
    <span data-ttu-id="6b2c2-213">Para que el contenido de hello del archivo hello es:</span><span class="sxs-lookup"><span data-stu-id="6b2c2-213">So that hello content of hello file is:</span></span>
   
    ```python
    from flask import Flask
    app = Flask(__name__)
    app.config.from_object('config')
    import tutorial.views
    ```
6. <span data-ttu-id="6b2c2-214">Después de agregar todos los archivos de hello, el Explorador de soluciones debe ser similar al siguiente:</span><span class="sxs-lookup"><span data-stu-id="6b2c2-214">After adding all hello files, Solution Explorer should look like this:</span></span>
   
    ![Captura de pantalla de ventana de Visual Studio Solution Explorer hello](./media/documentdb-python-application/cosmos-db-python-solution-explorer.png)

## <a name="step-4-run-your-web-application-locally"></a><span data-ttu-id="6b2c2-216">Paso 4: Ejecución local de la aplicación web</span><span class="sxs-lookup"><span data-stu-id="6b2c2-216">Step 4: Run your web application locally</span></span>
1. <span data-ttu-id="6b2c2-217">Compile la solución de hello presionando **Ctrl**+**MAYÚS**+**B**.</span><span class="sxs-lookup"><span data-stu-id="6b2c2-217">Build hello solution by pressing **Ctrl**+**Shift**+**B**.</span></span>
2. <span data-ttu-id="6b2c2-218">Cuando se complete correctamente la compilación de hello, iniciar sitio Web de hello presionando **F5**.</span><span class="sxs-lookup"><span data-stu-id="6b2c2-218">Once hello build succeeds, start hello website by pressing **F5**.</span></span> <span data-ttu-id="6b2c2-219">Debería ver siguiente de hello en la pantalla.</span><span class="sxs-lookup"><span data-stu-id="6b2c2-219">You should see hello following on your screen.</span></span>
   
    ![Captura de pantalla de Hola Python + Azure Cosmos DB votos de aplicación que se muestra en un explorador web](./media/documentdb-python-application/cosmos-db-pythonr-run-application.png)
3. <span data-ttu-id="6b2c2-221">Haga clic en **crear o borrar Hola votos de base de datos** base de datos de toogenerate Hola.</span><span class="sxs-lookup"><span data-stu-id="6b2c2-221">Click **Create/Clear hello Voting Database** toogenerate hello database.</span></span>
   
    ![Captura de pantalla de Hola Crear página de aplicación web de hello: detalles sobre el desarrollo](./media/documentdb-python-application/cosmos-db-python-run-create-page.png)
4. <span data-ttu-id="6b2c2-223">A continuación, haga clic en **Vote** (Votar) y seleccione su opción.</span><span class="sxs-lookup"><span data-stu-id="6b2c2-223">Then, click **Vote** and select your option.</span></span>
   
    ![Captura de pantalla de aplicación web de hello con una pregunta de votación que supone](./media/documentdb-python-application/cosmos-db-vote.png)
5. <span data-ttu-id="6b2c2-225">Para cada voto que convierte, incrementa el contador adecuado de Hola.</span><span class="sxs-lookup"><span data-stu-id="6b2c2-225">For every vote you cast, it increments hello appropriate counter.</span></span>
   
    ![Captura de pantalla de resultados de página de voto Hola que se muestra de Hola](./media/documentdb-python-application/cosmos-db-voting-results.png)
6. <span data-ttu-id="6b2c2-227">Detenga la depuración de proyectos de hello presionando MAYÚS+F5.</span><span class="sxs-lookup"><span data-stu-id="6b2c2-227">Stop debugging hello project by pressing Shift+F5.</span></span>

## <a name="step-5-deploy-hello-web-application-tooazure"></a><span data-ttu-id="6b2c2-228">Paso 5: Implementar tooAzure de aplicación web de Hola</span><span class="sxs-lookup"><span data-stu-id="6b2c2-228">Step 5: Deploy hello web application tooAzure</span></span>
<span data-ttu-id="6b2c2-229">Ahora que tiene la aplicación completa Hola funciona correctamente en la base de datos de Cosmos, vamos toodeploy esta tooAzure.</span><span class="sxs-lookup"><span data-stu-id="6b2c2-229">Now that you have hello complete application working correctly against Cosmos DB, we're going toodeploy this tooAzure.</span></span>

1. <span data-ttu-id="6b2c2-230">Menú contextual proyecto de hello en el Explorador de soluciones (asegúrese de que no está todavía ejecuta localmente) y seleccione **publicar**.</span><span class="sxs-lookup"><span data-stu-id="6b2c2-230">Right-click hello project in Solution Explorer (make sure you're not still running it locally) and select **Publish**.</span></span>  
   
     ![Captura de pantalla de tutorial de hello seleccionado en el Explorador de soluciones, con la opción de publicación de hello resaltado](./media/documentdb-python-application/image20.png)
2. <span data-ttu-id="6b2c2-232">Hola **publicar** cuadro de diálogo, seleccione **servicio de aplicaciones de Microsoft Azure**, seleccione **crear nuevo**y, a continuación, haga clic en **publicar**.</span><span class="sxs-lookup"><span data-stu-id="6b2c2-232">In hello **Publish** dialog box, select **Microsoft Azure App Service**, select **Create New**, and then click **Publish**.</span></span>
   
    ![Captura de pantalla de ventana de publicación Web de hello con el servicio de aplicación de Microsoft Azure resaltado](./media/documentdb-python-application/cosmos-db-python-publish.png)
3. <span data-ttu-id="6b2c2-234">Hola **crear servicio en la aplicación** diálogo cuadro, escriba el nombre de hello para la aplicación web junto con su **suscripción**, **grupo de recursos**, y **Plan de servicio de aplicaciones** , a continuación, haga clic en **crear**.</span><span class="sxs-lookup"><span data-stu-id="6b2c2-234">In hello **Create App Service** dialog box, enter hello name for your web app along with your **Subscription**, **Resource Group**, and **App Service Plan**, then click **Create**.</span></span>
   
    ![Captura de pantalla de ventana de la ventana de aplicaciones Web de Microsoft Azure de hello](./media/documentdb-python-application/cosmos-db-python-create-app-service.png)
4. <span data-ttu-id="6b2c2-236">En pocos segundos, Visual Studio terminará de publicar el servicio de aplicaciones y ejecutará un explorador donde podrá ver su trabajo ejecutándose en Azure.</span><span class="sxs-lookup"><span data-stu-id="6b2c2-236">In a few seconds, Visual Studio will finish publishing your app service and launch a browser where you can see your handiwork running in Azure!</span></span>

    ![Captura de pantalla de ventana de la ventana de aplicaciones Web de Microsoft Azure de hello](./media/documentdb-python-application/cosmos-db-python-appservice-created.png)

## <a name="troubleshooting"></a><span data-ttu-id="6b2c2-238">Solución de problemas</span><span class="sxs-lookup"><span data-stu-id="6b2c2-238">Troubleshooting</span></span>
<span data-ttu-id="6b2c2-239">Si esta es la primera aplicación de Python hello haya ejecutado en el equipo, asegúrese de que siguiente de hello carpetas (o ubicaciones de instalación equivalente de Hola) se incluyen en la variable de ruta de acceso:</span><span class="sxs-lookup"><span data-stu-id="6b2c2-239">If this is hello first Python app you've run on your computer, ensure that hello following folders (or hello equivalent installation locations) are included in your PATH variable:</span></span>

    C:\Python27\site-packages;C:\Python27\;C:\Python27\Scripts;

<span data-ttu-id="6b2c2-240">Si recibe un error en la página de voto y dio el nombre del proyecto algo distinto de **tutorial**, asegúrese de que  **\_ \_init\_\_.py** referencias Hola nombre correcto del proyecto en línea hello: `import tutorial.view`.</span><span class="sxs-lookup"><span data-stu-id="6b2c2-240">If you receive an error on your vote page, and you named your project something other than **tutorial**, make sure that **\_\_init\_\_.py** references hello correct project name in hello line: `import tutorial.view`.</span></span>

## <a name="next-steps"></a><span data-ttu-id="6b2c2-241">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="6b2c2-241">Next steps</span></span>
<span data-ttu-id="6b2c2-242">¡Enhorabuena!</span><span class="sxs-lookup"><span data-stu-id="6b2c2-242">Congratulations!</span></span> <span data-ttu-id="6b2c2-243">Acaba de completar su primera aplicación web de Python mediante DB Cosmos y haberlo publicado tooAzure.</span><span class="sxs-lookup"><span data-stu-id="6b2c2-243">You have just completed your first Python web application using Cosmos DB and published it tooAzure.</span></span>

<span data-ttu-id="6b2c2-244">Actualizamos y mejoramos este tema con frecuencia en función de los comentarios que recibimos.</span><span class="sxs-lookup"><span data-stu-id="6b2c2-244">We update and improve this topic frequently based on your feedback.</span></span>  <span data-ttu-id="6b2c2-245">Una vez se ha completado el tutorial de hello, póngase con hello votos botones en hello superior e inferior de esta página y estar seguro tooinclude sus comentarios acerca de qué mejoras que desee toosee realizado.</span><span class="sxs-lookup"><span data-stu-id="6b2c2-245">Once you've completed hello tutorial, please using hello voting buttons at hello top and bottom of this page, and be sure tooinclude your feedback on what improvements you want toosee made.</span></span> <span data-ttu-id="6b2c2-246">Si desea que nos toocontact directamente, cree libre tooinclude dirección de su correo electrónico en sus comentarios.</span><span class="sxs-lookup"><span data-stu-id="6b2c2-246">If you'd like us toocontact you directly, feel free tooinclude your email address in your comments.</span></span>

<span data-ttu-id="6b2c2-247">aplicación de web tooyour tooadd funcionalidad adicional, revisión Hola API disponibles en hello [SDK de Azure Cosmos DB Python](documentdb-sdk-python.md).</span><span class="sxs-lookup"><span data-stu-id="6b2c2-247">tooadd additional functionality tooyour web application, review hello APIs available in hello [Azure Cosmos DB Python SDK](documentdb-sdk-python.md).</span></span>

<span data-ttu-id="6b2c2-248">Para obtener más información acerca de Azure, Visual Studio y Python, vea hello [Centro para desarrolladores de Python](https://azure.microsoft.com/develop/python/).</span><span class="sxs-lookup"><span data-stu-id="6b2c2-248">For more information about Azure, Visual Studio, and Python, see hello [Python Developer Center](https://azure.microsoft.com/develop/python/).</span></span> 

<span data-ttu-id="6b2c2-249">Para ver los tutoriales Python matraz adicionales, consulte [Hola matraz Mega-Tutorial, parte I: Hello, World!](http://blog.miguelgrinberg.com/post/the-flask-mega-tutorial-part-i-hello-world).</span><span class="sxs-lookup"><span data-stu-id="6b2c2-249">For additional Python Flask tutorials, see [hello Flask Mega-Tutorial, Part I: Hello, World!](http://blog.miguelgrinberg.com/post/the-flask-mega-tutorial-part-i-hello-world).</span></span> 

[Visual Studio Express]: http://www.visualstudio.com/products/visual-studio-express-vs.aspx
[2]: https://www.python.org/downloads/windows/
[3]: https://www.microsoft.com/download/details.aspx?id=44266
[Microsoft Web Platform Installer]: http://www.microsoft.com/web/downloads/platform.aspx
[Azure portal]: http://portal.azure.com
