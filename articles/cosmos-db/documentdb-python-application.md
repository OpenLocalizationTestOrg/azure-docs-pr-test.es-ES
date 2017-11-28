---
title: Tutorial sobre aplicaciones web de Python Flask para Azure Cosmos DB | Microsoft Docs
description: "Vea un tutorial de base de datos sobre el uso de Azure cosmos DB para almacenar datos y acceder a ellos desde una aplicación web de Python Flask hospedada en Azure. Encuentre soluciones de desarrollo de aplicaciones."
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
ms.openlocfilehash: ed5284b5a265840c43dbc9890082a7c038d22975
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/18/2017
---
# <a name="build-a-python-flask-web-application-using-azure-cosmos-db"></a><span data-ttu-id="79350-105">Compilación de una aplicación web Node.js de Python Flask mediante Azure cosmos DB</span><span class="sxs-lookup"><span data-stu-id="79350-105">Build a Python Flask web application using Azure Cosmos DB</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="79350-106">.NET</span><span class="sxs-lookup"><span data-stu-id="79350-106">.NET</span></span>](documentdb-dotnet-application.md)
> * [<span data-ttu-id="79350-107">Node.js</span><span class="sxs-lookup"><span data-stu-id="79350-107">Node.js</span></span>](documentdb-nodejs-application.md)
> * [<span data-ttu-id="79350-108">Java</span><span class="sxs-lookup"><span data-stu-id="79350-108">Java</span></span>](documentdb-java-application.md)
> * [<span data-ttu-id="79350-109">Python</span><span class="sxs-lookup"><span data-stu-id="79350-109">Python</span></span>](documentdb-python-application.md)
> 
> 

<span data-ttu-id="79350-110">En este tutorial aprenderá a usar el servicio Azure cosmos DB para almacenar datos y acceder a ellos desde cualquier aplicación web de Python hospedada en Azure. En él se presupone que tiene experiencia previa con los sitios web de Python y Azure.</span><span class="sxs-lookup"><span data-stu-id="79350-110">This tutorial shows you how to use Azure Cosmos DB to store and access data from a Python web application hosted on Azure and presumes that you have some prior experience using Python and Azure websites.</span></span>

<span data-ttu-id="79350-111">En este tutorial de base de datos se trata lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="79350-111">This database tutorial covers:</span></span>

1. <span data-ttu-id="79350-112">Crear y aprovisionar una cuenta de Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="79350-112">Creating and provisioning a Cosmos DB account.</span></span>
2. <span data-ttu-id="79350-113">Crear una aplicación Python Flask.</span><span class="sxs-lookup"><span data-stu-id="79350-113">Creating a Python Flask application.</span></span>
3. <span data-ttu-id="79350-114">Conectarse y utilizar Cosmos DB desde la aplicación web.</span><span class="sxs-lookup"><span data-stu-id="79350-114">Connecting to and using Cosmos DB from your web application.</span></span>
4. <span data-ttu-id="79350-115">Implementar la aplicación web en Azure.</span><span class="sxs-lookup"><span data-stu-id="79350-115">Deploying the web application to Azure.</span></span>

<span data-ttu-id="79350-116">Siguiendo este tutorial, podrá compilar una aplicación de votación simple que le permita votar en un sondeo.</span><span class="sxs-lookup"><span data-stu-id="79350-116">By following this tutorial, you will build a simple voting application that allows you to vote for a poll.</span></span>

![Captura de pantalla de la aplicación de votación creada con este tutorial](./media/documentdb-python-application/cosmos-db-pythonr-run-application.png)

## <a name="database-tutorial-prerequisites"></a><span data-ttu-id="79350-118">Requisitos previos del tutorial de base de datos</span><span class="sxs-lookup"><span data-stu-id="79350-118">Database tutorial prerequisites</span></span>
<span data-ttu-id="79350-119">Antes de seguir las instrucciones del presente artículo, debe asegurarse de tener instalados los siguientes elementos:</span><span class="sxs-lookup"><span data-stu-id="79350-119">Before following the instructions in this article, you should ensure that you have the following installed:</span></span>

* <span data-ttu-id="79350-120">Una cuenta de Azure activa.</span><span class="sxs-lookup"><span data-stu-id="79350-120">An active Azure account.</span></span> <span data-ttu-id="79350-121">En caso de no tener ninguna, puede crear una cuenta de evaluación gratuita en tan solo unos minutos.</span><span class="sxs-lookup"><span data-stu-id="79350-121">If you don't have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="79350-122">Para obtener más información, consulte [Evaluación gratuita de Azure](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="79350-122">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
 
    <span data-ttu-id="79350-123">OR</span><span class="sxs-lookup"><span data-stu-id="79350-123">OR</span></span> 

    <span data-ttu-id="79350-124">Una instalación local del [Emulador de Azure Cosmos DB](local-emulator.md).</span><span class="sxs-lookup"><span data-stu-id="79350-124">A local installation of the [Azure Cosmos DB Emulator](local-emulator.md).</span></span>
* <span data-ttu-id="79350-125">[Microsoft Visual Studio Community 2017](http://www.visualstudio.com/)</span><span class="sxs-lookup"><span data-stu-id="79350-125">[Microsoft Visual Studio Community 2017](http://www.visualstudio.com/).</span></span>  
* <span data-ttu-id="79350-126">[Herramientas de Python para Visual Studio](https://github.com/Microsoft/PTVS/)</span><span class="sxs-lookup"><span data-stu-id="79350-126">[Python Tools for Visual Studio](https://github.com/Microsoft/PTVS/).</span></span>  
* <span data-ttu-id="79350-127">[SDK de Microsoft Azure para Python 2.7](https://azure.microsoft.com/downloads/)</span><span class="sxs-lookup"><span data-stu-id="79350-127">[Microsoft Azure SDK for Python 2.7](https://azure.microsoft.com/downloads/).</span></span> 
* <span data-ttu-id="79350-128">[Python 2.7.13](https://www.python.org/downloads/windows/)</span><span class="sxs-lookup"><span data-stu-id="79350-128">[Python 2.7.13](https://www.python.org/downloads/windows/).</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="79350-129">Si va a instalar Python 2.7 por primera vez, asegúrese de que en la pantalla Personalizar Python 2.7.13 selecciona **Agregar python.exe a la ruta de acceso**.</span><span class="sxs-lookup"><span data-stu-id="79350-129">If you are installing Python 2.7 for the first time, ensure that in the Customize Python 2.7.13 screen, you select **Add python.exe to Path**.</span></span>
> 
> ![Captura de pantalla de la pantalla Personalizar Python 2.7.11, donde debe seleccionar Agregar python.exe a la ruta de acceso](./media/documentdb-python-application/cosmos-db-python-install.png)
> 
> 

* <span data-ttu-id="79350-131">[Compilador de Microsoft Visual C++ 2013 para Python 2.7](https://www.microsoft.com/en-us/download/details.aspx?id=44266)</span><span class="sxs-lookup"><span data-stu-id="79350-131">[Microsoft Visual C++ Compiler for Python 2.7](https://www.microsoft.com/en-us/download/details.aspx?id=44266).</span></span>

## <a name="step-1-create-an-azure-cosmos-db-database-account"></a><span data-ttu-id="79350-132">Paso 1: Creación de una cuenta de base de datos de Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="79350-132">Step 1: Create an Azure Cosmos DB database account</span></span>
<span data-ttu-id="79350-133">Para comenzar, creemos una cuenta de Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="79350-133">Let's start by creating an Cosmos DB account.</span></span> <span data-ttu-id="79350-134">Si ya tiene una cuenta o si usa el Emulador de Azure Cosmos DB en este tutorial, puede ir directamente al [Paso 2: Creación de una nueva aplicación web de Python Flask](#step-2-create-a-new-python-flask-web-application).</span><span class="sxs-lookup"><span data-stu-id="79350-134">If you already have an account or if you are using the Azure Cosmos DB Emulator for this tutorial, you can skip to [Step 2: Create a new Python Flask web application](#step-2-create-a-new-python-flask-web-application).</span></span>

[!INCLUDE [cosmos-db-create-dbaccount](../../includes/cosmos-db-create-dbaccount.md)]

<br/>
<span data-ttu-id="79350-135">Ahora veremos cómo crear una nueva aplicación web de Phyton Flask partiendo de cero.</span><span class="sxs-lookup"><span data-stu-id="79350-135">We will now walk through how to create a new Python Flask web application from the ground up.</span></span>

## <a name="step-2-create-a-new-python-flask-web-application"></a><span data-ttu-id="79350-136">Paso 2: Creación de una nueva aplicación web de Python Flask</span><span class="sxs-lookup"><span data-stu-id="79350-136">Step 2: Create a new Python Flask web application</span></span>
1. <span data-ttu-id="79350-137">En Visual Studio, en el menú **Archivo**, seleccione **Nuevo** y luego haga clic en **Proyecto**.</span><span class="sxs-lookup"><span data-stu-id="79350-137">In Visual Studio, on the **File** menu, point to **New**, and then click **Project**.</span></span>
   
    <span data-ttu-id="79350-138">Aparecerá el cuadro de diálogo **Nuevo proyecto** .</span><span class="sxs-lookup"><span data-stu-id="79350-138">The **New Project** dialog box appears.</span></span>
2. <span data-ttu-id="79350-139">En el panel izquierdo, expanda **Plantillas**, **Python** y luego haga clic en **Web**.</span><span class="sxs-lookup"><span data-stu-id="79350-139">In the left pane, expand **Templates** and then **Python**, and then click **Web**.</span></span> 
3. <span data-ttu-id="79350-140">Seleccione **Proyecto web Flask** en el panel central; después en el cuadro **Nombre** escriba **tutorial** y, finalmente, haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="79350-140">Select **Flask  Web Project** in the center pane, then in the **Name** box type **tutorial**, and then click **OK**.</span></span> <span data-ttu-id="79350-141">Recuerde que los nombres de paquete de Python deben escribirse en minúsculas, tal como se describe en [Style Guide for Python Code](https://www.python.org/dev/peps/pep-0008/#package-and-module-names).</span><span class="sxs-lookup"><span data-stu-id="79350-141">Remember that Python package names should be all lowercase, as described in the [Style Guide for Python Code](https://www.python.org/dev/peps/pep-0008/#package-and-module-names).</span></span>
   
    <span data-ttu-id="79350-142">Para aquellos que desconozcan Python Flask, se trata de un marco de desarrollo de aplicaciones web que ayuda a compilar aplicaciones web en Python más rápidamente.</span><span class="sxs-lookup"><span data-stu-id="79350-142">For those new to Python Flask, it is a web application development framework that helps you build web applications in Python faster.</span></span>
   
    ![Captura de pantalla de la ventana Nuevo proyecto en Visual Studio con Python resaltado a la izquierda, el proyecto web de Python Flask seleccionado en el centro y el nombre tutorial en el cuadro Nombre](./media/documentdb-python-application/image9.png)
4. <span data-ttu-id="79350-144">En la ventana **Herramientas de Python para Visual Studio**, haga clic en **Instalar en un entorno virtual**.</span><span class="sxs-lookup"><span data-stu-id="79350-144">In the **Python Tools for Visual Studio** window, click **Install into a virtual environment**.</span></span> 
   
    ![Captura de pantalla del tutorial de base de datos: ventana Herramientas de Python para Visual Studio](./media/documentdb-python-application/python-install-virtual-environment.png)
5. <span data-ttu-id="79350-146">En la ventana **Agregar entorno virtual**, puede aceptar los valores predeterminados y usar Python 2.7 como entorno de base, ya que PyDocumentDB no admite de momento Python 3.x y, después, haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="79350-146">In the **Add Virtual Environment** window, you can accept the defaults and use Python 2.7 as the base environment because PyDocumentDB does not currently support Python 3.x, and then click **Create**.</span></span> <span data-ttu-id="79350-147">Esto configura el entorno virtual de Python requerido para el proyecto.</span><span class="sxs-lookup"><span data-stu-id="79350-147">This sets up the required Python virtual environment for your project.</span></span>
   
    ![Captura de pantalla del tutorial de base de datos: ventana Herramientas de Python para Visual Studio](./media/documentdb-python-application/image10_A.png)
   
    <span data-ttu-id="79350-149">Muestra la ventana de salida `Successfully installed Flask-0.10.1 Jinja2-2.8 MarkupSafe-0.23 Werkzeug-0.11.5 itsdangerous-0.24 'requirements.txt' was installed successfully.` cuando el entorno está instalado correctamente.</span><span class="sxs-lookup"><span data-stu-id="79350-149">The output window displays `Successfully installed Flask-0.10.1 Jinja2-2.8 MarkupSafe-0.23 Werkzeug-0.11.5 itsdangerous-0.24 'requirements.txt' was installed successfully.` when the environment is successfully installed.</span></span>

## <a name="step-3-modify-the-python-flask-web-application"></a><span data-ttu-id="79350-150">Paso 3: Modificación de la aplicación web de Python Flask</span><span class="sxs-lookup"><span data-stu-id="79350-150">Step 3: Modify the Python Flask web application</span></span>
### <a name="add-the-python-flask-packages-to-your-project"></a><span data-ttu-id="79350-151">Adición de paquetes de Python Flask al proyecto</span><span class="sxs-lookup"><span data-stu-id="79350-151">Add the Python Flask packages to your project</span></span>
<span data-ttu-id="79350-152">Después de que el proyecto esté configurado, es preciso agregar el paquete Flask necesario al proyecto, incluido pydocumentdb, el paquete de Python para DocumentDB.</span><span class="sxs-lookup"><span data-stu-id="79350-152">After your project is set up, you'll need to add the required Flask packages to your project, including pydocumentdb, the Python package for DocumentDB.</span></span>

1. <span data-ttu-id="79350-153">En el Explorador de soluciones, abra el archivo llamado **requirements.txt** y reemplace su contenido por lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="79350-153">In Solution Explorer, open the file named **requirements.txt** and replace the contents with the following:</span></span>
   
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
2. <span data-ttu-id="79350-154">Guarde el archivo **requirements.txt** .</span><span class="sxs-lookup"><span data-stu-id="79350-154">Save the **requirements.txt** file.</span></span> 
3. <span data-ttu-id="79350-155">En el Explorador de soluciones, haga clic con el botón derecho en **env** y haga clic en **Install from requirements.txt**.</span><span class="sxs-lookup"><span data-stu-id="79350-155">In Solution Explorer, right-click **env** and click **Install from requirements.txt**.</span></span>
   
    ![Captura de pantalla que muestra env (Python 2.7) seleccionado con Instalación desde requirements.txt resaltado en la lista](./media/documentdb-python-application/cosmos-db-python-install-from-requirements.png)
   
    <span data-ttu-id="79350-157">Después de una instalación correcta, la ventana de salidas muestra lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="79350-157">After successful installation, the output window displays the following:</span></span>
   
        Successfully installed Babel-2.3.2 Tempita-0.5.2 WTForms-2.1 Whoosh-2.7.4 blinker-1.4 decorator-4.0.9 flask-0.9 flask-babel-0.8 flask-mail-0.7.6 flask-sqlalchemy-0.16 flask-whooshalchemy-0.55a0 flask-wtf-0.8.4 flup-1.0.2 pydocumentdb-1.6.1 pytz-2013b0 speaklater-1.3 sqlalchemy-0.7.9 sqlalchemy-migrate-0.7.2
   
   > [!NOTE]
   > <span data-ttu-id="79350-158">En casos excepcionales, es posible que aparezca un error en la ventana de salida.</span><span class="sxs-lookup"><span data-stu-id="79350-158">In rare cases, you might see a failure in the output window.</span></span> <span data-ttu-id="79350-159">De ser así, compruebe si el error está relacionado con la limpieza.</span><span class="sxs-lookup"><span data-stu-id="79350-159">If this happens, check if the error is related to cleanup.</span></span> <span data-ttu-id="79350-160">En ocasiones, se produce un error en la limpieza, pero la instalación se realiza correctamente (desplácese hacia arriba en la ventana de salida para comprobarlo).</span><span class="sxs-lookup"><span data-stu-id="79350-160">Sometimes the cleanup fails, but the installation will still be successful (scroll up in the output window to verify this).</span></span> <span data-ttu-id="79350-161">Puede comprobar la instalación mediante la [comprobación del entorno virtual](#verify-the-virtual-environment).</span><span class="sxs-lookup"><span data-stu-id="79350-161">You can check your installation by [Verifying the virtual environment](#verify-the-virtual-environment).</span></span> <span data-ttu-id="79350-162">Si se produjo un error en la instalación, pero la comprobación es correcta, se puede continuar sin problemas.</span><span class="sxs-lookup"><span data-stu-id="79350-162">If the installation failed but the verification is successful, it's OK to continue.</span></span>
   > 
   > 

### <a name="verify-the-virtual-environment"></a><span data-ttu-id="79350-163">Comprobación del entorno virtual</span><span class="sxs-lookup"><span data-stu-id="79350-163">Verify the virtual environment</span></span>
<span data-ttu-id="79350-164">Asegurémonos de que todo esté instalado correctamente.</span><span class="sxs-lookup"><span data-stu-id="79350-164">Let's make sure that everything is installed correctly.</span></span>

1. <span data-ttu-id="79350-165">Copile la solución presionando **Ctrl**+**Mayús**+**B**.</span><span class="sxs-lookup"><span data-stu-id="79350-165">Build the solution by pressing **Ctrl**+**Shift**+**B**.</span></span>
2. <span data-ttu-id="79350-166">Una vez realizada correctamente la compilación, inicie el sitio web presionando **F5**.</span><span class="sxs-lookup"><span data-stu-id="79350-166">Once the build succeeds, start the website by pressing **F5**.</span></span> <span data-ttu-id="79350-167">De este modo se iniciará el servidor de desarrollo de Flask y el explorador web.</span><span class="sxs-lookup"><span data-stu-id="79350-167">This launches the Flask development server and starts your web browser.</span></span> <span data-ttu-id="79350-168">Debe ver la página siguiente.</span><span class="sxs-lookup"><span data-stu-id="79350-168">You should see the following page.</span></span>
   
    ![Proyecto de desarrollo web de Python Flask vacío en un explorador](./media/documentdb-python-application/image12.png)
3. <span data-ttu-id="79350-170">Detenga la depuración del sitio web presionando **Mayús**+**F5** en Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="79350-170">Stop debugging the website by pressing **Shift**+**F5** in Visual Studio.</span></span>

### <a name="create-database-collection-and-document-definitions"></a><span data-ttu-id="79350-171">Creación de definiciones de base de datos, colección y documento</span><span class="sxs-lookup"><span data-stu-id="79350-171">Create database, collection, and document definitions</span></span>
<span data-ttu-id="79350-172">Ahora vamos a crear la aplicación de votación mediante la adición de archivos nuevos y de la actualización de otros.</span><span class="sxs-lookup"><span data-stu-id="79350-172">Now let's create your voting application by adding new files and updating others.</span></span>

1. <span data-ttu-id="79350-173">En el Explorador de soluciones, haga clic con el botón derecho en el proyecto de **tutorial**, a continuación haga clic en **Agregar** y, por último, en **Nuevo elemento**.</span><span class="sxs-lookup"><span data-stu-id="79350-173">In Solution Explorer, right-click the **tutorial** project, click **Add**, and then click **New Item**.</span></span> <span data-ttu-id="79350-174">Seleccione **Archivo Python vacío** y asigne el nombre **forms.py** al archivo.</span><span class="sxs-lookup"><span data-stu-id="79350-174">Select **Empty Python File** and name the file **forms.py**.</span></span>  
2. <span data-ttu-id="79350-175">Agregue el código siguiente al archivo forms.py y, después, guárdelo.</span><span class="sxs-lookup"><span data-stu-id="79350-175">Add the following code to the forms.py file, and then save the file.</span></span>

```python
from flask.ext.wtf import Form
from wtforms import RadioField

class VoteForm(Form):
    deploy_preference  = RadioField('Deployment Preference', choices=[
        ('Web Site', 'Web Site'),
        ('Cloud Service', 'Cloud Service'),
        ('Virtual Machine', 'Virtual Machine')], default='Web Site')
```


### <a name="add-the-required-imports-to-viewspy"></a><span data-ttu-id="79350-176">Agregue las importaciones necesarias a views.py.</span><span class="sxs-lookup"><span data-stu-id="79350-176">Add the required imports to views.py</span></span>
1. <span data-ttu-id="79350-177">En el Explorador de soluciones, expanda la carpeta **tutorial** y abra el archivo **views.py**.</span><span class="sxs-lookup"><span data-stu-id="79350-177">In Solution Explorer, expand the **tutorial** folder, and open the **views.py** file.</span></span> 
2. <span data-ttu-id="79350-178">Agregue las siguientes instrucciones de importación a la parte superior del archivo **views.py** y, después, guarde el archivo.</span><span class="sxs-lookup"><span data-stu-id="79350-178">Add the following import statements to the top of the **views.py** file, then save the file.</span></span> <span data-ttu-id="79350-179">Con estas instrucciones se importarán los paquetes de PythonSDK y Flask de Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="79350-179">These import Cosmos DB's PythonSDK and the Flask packages.</span></span>
   
    ```python
    from forms import VoteForm
    import config
    import pydocumentdb.document_client as document_client
    ```

### <a name="create-database-collection-and-document"></a><span data-ttu-id="79350-180">Creación de base de datos, colección y documento</span><span class="sxs-lookup"><span data-stu-id="79350-180">Create database, collection, and document</span></span>
* <span data-ttu-id="79350-181">Todavía en **views.py**, agregue el siguiente código al final del archivo.</span><span class="sxs-lookup"><span data-stu-id="79350-181">Still in **views.py**, add the following code to the end of the file.</span></span> <span data-ttu-id="79350-182">Esta acción se encarga de crear la base de datos que usa el formulario.</span><span class="sxs-lookup"><span data-stu-id="79350-182">This takes care of creating the database used by the form.</span></span> <span data-ttu-id="79350-183">No elimine el código existente en **views.py**.</span><span class="sxs-lookup"><span data-stu-id="79350-183">Do not delete any of the existing code in **views.py**.</span></span> <span data-ttu-id="79350-184">Solo tiene que incluir esto al final.</span><span class="sxs-lookup"><span data-stu-id="79350-184">Simply append this to the end.</span></span>

```python
@app.route('/create')
def create():
    """Renders the contact page."""
    client = document_client.DocumentClient(config.DOCUMENTDB_HOST, {'masterKey': config.DOCUMENTDB_KEY})

    # Attempt to delete the database.  This allows this to be used to recreate as well as create
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


### <a name="read-database-collection-document-and-submit-form"></a><span data-ttu-id="79350-185">Lectura de la base de datos, la colección y el documento, y envío del formulario</span><span class="sxs-lookup"><span data-stu-id="79350-185">Read database, collection, document, and submit form</span></span>
* <span data-ttu-id="79350-186">Todavía en **views.py**, agregue el siguiente código al final del archivo.</span><span class="sxs-lookup"><span data-stu-id="79350-186">Still in **views.py**, add the following code to the end of the file.</span></span> <span data-ttu-id="79350-187">Esta acción se encarga de configurar el formulario mediante la lectura de la base de datos, la colección y el documento.</span><span class="sxs-lookup"><span data-stu-id="79350-187">This takes care of setting up the form, reading the database, collection, and document.</span></span> <span data-ttu-id="79350-188">No elimine el código existente en **views.py**.</span><span class="sxs-lookup"><span data-stu-id="79350-188">Do not delete any of the existing code in **views.py**.</span></span> <span data-ttu-id="79350-189">Solo tiene que incluir esto al final.</span><span class="sxs-lookup"><span data-stu-id="79350-189">Simply append this to the end.</span></span>

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

        # Take the data from the deploy_preference and increment our database
        doc[form.deploy_preference.data] = doc[form.deploy_preference.data] + 1
        replaced_document = client.ReplaceDocument(doc['_self'], doc)

        # Create a model to pass to results.html
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


### <a name="create-the-html-files"></a><span data-ttu-id="79350-190">Creación de los archivos HTML</span><span class="sxs-lookup"><span data-stu-id="79350-190">Create the HTML files</span></span>
1. <span data-ttu-id="79350-191">En el Explorador de soluciones, en la carpeta **tutorial**, haga clic con el botón derecho en la carpeta **templates**, haga clic en **Agregar** y, después, haga clic en **Nuevo elemento**.</span><span class="sxs-lookup"><span data-stu-id="79350-191">In Solution Explorer, in the **tutorial** folder, right click the **templates** folder, click **Add**, and then click **New Item**.</span></span> 
2. <span data-ttu-id="79350-192">Seleccione **Página HTML** y luego en el cuadro **Nombre** escriba create.html.</span><span class="sxs-lookup"><span data-stu-id="79350-192">Select **HTML Page**, and then in the name box type **create.html**.</span></span> 
3. <span data-ttu-id="79350-193">Repita los pasos 1 y 2 para crear dos archivos HTML adicionales: results.html y vote.html.</span><span class="sxs-lookup"><span data-stu-id="79350-193">Repeat steps 1 and 2 to create two additional HTML files: results.html and vote.html.</span></span>
4. <span data-ttu-id="79350-194">Agregue el siguiente código a **create.html** in the `<body>` .</span><span class="sxs-lookup"><span data-stu-id="79350-194">Add the following code to **create.html** in the `<body>` element.</span></span> <span data-ttu-id="79350-195">Se muestra un mensaje que indica que hemos creado una nueva base de datos, colección y documento.</span><span class="sxs-lookup"><span data-stu-id="79350-195">It displays a message stating that we created a new database, collection, and document.</span></span>
   
    ```html
    {% extends "layout.html" %}
    {% block content %}
    <h2>{{ title }}.</h2>
    <h3>{{ message }}</h3>
    <p><a href="{{ url_for('vote') }}" class="btn btn-primary btn-large">Vote &raquo;</a></p>
    {% endblock %}
    ```
5. <span data-ttu-id="79350-196">Agregue el siguiente código a **results.html** en el elemento `<body`>.</span><span class="sxs-lookup"><span data-stu-id="79350-196">Add the following code to **results.html** in the `<body`> element.</span></span> <span data-ttu-id="79350-197">Se muestran los resultados del sondeo.</span><span class="sxs-lookup"><span data-stu-id="79350-197">It displays the results of the poll.</span></span>
   
    ```html
    {% extends "layout.html" %}
    {% block content %}
    <h2>Results of the vote</h2>
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
6. <span data-ttu-id="79350-198">Agregue el siguiente código a **vote.html** en el elemento `<body`>.</span><span class="sxs-lookup"><span data-stu-id="79350-198">Add the following code to **vote.html** in the `<body`> element.</span></span> <span data-ttu-id="79350-199">Muestra el sondeo y acepta los votos.</span><span class="sxs-lookup"><span data-stu-id="79350-199">It displays the poll and accepts the votes.</span></span> <span data-ttu-id="79350-200">Al registrar los votos, el control se pasa a views.py, donde reconoceremos el voto emitido y se anexará al documento en consecuencia.</span><span class="sxs-lookup"><span data-stu-id="79350-200">On registering the votes, the control is passed over to views.py where we will recognize the vote cast and append the document accordingly.</span></span>
   
    ```html
    {% extends "layout.html" %}
    {% block content %}
    <h2>What is your favorite way to host an application on Azure?</h2>
    <form action="" method="post" name="vote">
        {{form.hidden_tag()}}
            {{form.deploy_preference}}
            <button class="btn btn-primary" type="submit">Vote</button>
    </form>
    {% endblock %}
    ```
7. <span data-ttu-id="79350-201">En la carpeta **templates**, reemplace el contenido de **index.html** por lo siguiente.</span><span class="sxs-lookup"><span data-stu-id="79350-201">In the **templates** folder, replace the contents of **index.html** with the following.</span></span> <span data-ttu-id="79350-202">Esto sirve como la página de aterrizaje de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="79350-202">This serves as the landing page for your application.</span></span>
   
    ```html
    {% extends "layout.html" %}
    {% block content %}
    <h2>Python + Azure Cosmos DB Voting Application.</h2>
    <h3>This is a sample Cosmos DB voting application using PyDocumentDB</h3>
    <p><a href="{{ url_for('create') }}" class="btn btn-primary btn-large">Create/Clear the Voting Database &raquo;</a></p>
    <p><a href="{{ url_for('vote') }}" class="btn btn-primary btn-large">Vote &raquo;</a></p>
    {% endblock %}
    ```

### <a name="add-a-configuration-file-and-change-the-initpy"></a><span data-ttu-id="79350-203">Adición de un archivo de configuración y modificación de \_\_init\_\_.py</span><span class="sxs-lookup"><span data-stu-id="79350-203">Add a configuration file and change the \_\_init\_\_.py</span></span>
1. <span data-ttu-id="79350-204">En el Explorador de soluciones, haga clic con el botón derecho en el proyecto **tutorial**, haga clic en **Agregar**, en **Nuevo elemento**, seleccione **Archivo Python vacío** y, a continuación, asigne al archivo el nombre de **config.py**.</span><span class="sxs-lookup"><span data-stu-id="79350-204">In Solution Explorer, right-click the **tutorial** project, click **Add**, click **New Item**, select **Empty Python File**, and then name the file **config.py**.</span></span> <span data-ttu-id="79350-205">Los formularios de Flask requieren este archivo de configuración.</span><span class="sxs-lookup"><span data-stu-id="79350-205">This config file is required by forms in Flask.</span></span> <span data-ttu-id="79350-206">También se puede usar para proporcionar una clave secreta.</span><span class="sxs-lookup"><span data-stu-id="79350-206">You can use it to provide a secret key as well.</span></span> <span data-ttu-id="79350-207">Sin embargo, dicha clave no es necesaria para este tutorial.</span><span class="sxs-lookup"><span data-stu-id="79350-207">This key is not needed for this tutorial though.</span></span>
2. <span data-ttu-id="79350-208">Agregue el siguiente código a config.py, deberá modificar los valores de **DOCUMENTDB\_HOST** y **DOCUMENTDB\_KEY** en el paso siguiente.</span><span class="sxs-lookup"><span data-stu-id="79350-208">Add the following code to config.py, you'll need to alter the values of **DOCUMENTDB\_HOST** and **DOCUMENTDB\_KEY** in the next step.</span></span>
   
    ```python
    CSRF_ENABLED = True
    SECRET_KEY = 'you-will-never-guess'
   
    DOCUMENTDB_HOST = 'https://YOUR_DOCUMENTDB_NAME.documents.azure.com:443/'
    DOCUMENTDB_KEY = 'YOUR_SECRET_KEY_ENDING_IN_=='
   
    DOCUMENTDB_DATABASE = 'voting database'
    DOCUMENTDB_COLLECTION = 'voting collection'
    DOCUMENTDB_DOCUMENT = 'voting document'
    ```
3. <span data-ttu-id="79350-209">En [Azure Portal](https://portal.azure.com/), haga clic en **Examinar** y en **Azure Cosmos DB Accounts** (Cuentas de Azure Cosmos DB) para ir a la hoja **Claves**; después, haga doble clic en el nombre de la cuenta que desea usar y haga clic en el botón **Claves** del área **Información esencial**.</span><span class="sxs-lookup"><span data-stu-id="79350-209">In the [Azure portal](https://portal.azure.com/), navigate to the **Keys** blade by clicking **Browse**, **Azure Cosmos DB Accounts**, double-click the name of the account to use, and then click the **Keys** button in the **Essentials** area.</span></span> <span data-ttu-id="79350-210">En la hoja **Claves**, copie el valor del identificador **URI** y péguelo en el archivo **config.py**, como valor de la propiedad **DOCUMENTDB\_HOST**.</span><span class="sxs-lookup"><span data-stu-id="79350-210">In the **Keys** blade, copy the **URI** value and paste it into the **config.py** file, as the value for the **DOCUMENTDB\_HOST** property.</span></span> 
4. <span data-ttu-id="79350-211">De nuevo en Azure Portal, en la hoja **Claves**, copie el valor de la **clave principal** o de la **clave secundaria** y péguelo en el archivo **config.py**, como valor de la propiedad **DOCUMENTDB\_KEY**.</span><span class="sxs-lookup"><span data-stu-id="79350-211">Back in the Azure portal, in the **Keys** blade, copy the value of the **Primary Key** or the **Secondary Key**, and paste it into the **config.py** file, as the value for the **DOCUMENTDB\_KEY** property.</span></span>
5. <span data-ttu-id="79350-212">En el archivo **\_\_init\_\_.py**, agregue la siguiente línea.</span><span class="sxs-lookup"><span data-stu-id="79350-212">In the **\_\_init\_\_.py** file, add the following line.</span></span> 
   
        app.config.from_object('config')
   
    <span data-ttu-id="79350-213">Por lo tanto, el contenido del archivo es:</span><span class="sxs-lookup"><span data-stu-id="79350-213">So that the content of the file is:</span></span>
   
    ```python
    from flask import Flask
    app = Flask(__name__)
    app.config.from_object('config')
    import tutorial.views
    ```
6. <span data-ttu-id="79350-214">Después de agregar todos los archivos, Explorador de soluciones debe ser similar al siguiente:</span><span class="sxs-lookup"><span data-stu-id="79350-214">After adding all the files, Solution Explorer should look like this:</span></span>
   
    ![Captura de pantalla de la ventana del explorador de soluciones de Visual Studio](./media/documentdb-python-application/cosmos-db-python-solution-explorer.png)

## <a name="step-4-run-your-web-application-locally"></a><span data-ttu-id="79350-216">Paso 4: Ejecución local de la aplicación web</span><span class="sxs-lookup"><span data-stu-id="79350-216">Step 4: Run your web application locally</span></span>
1. <span data-ttu-id="79350-217">Copile la solución presionando **Ctrl**+**Mayús**+**B**.</span><span class="sxs-lookup"><span data-stu-id="79350-217">Build the solution by pressing **Ctrl**+**Shift**+**B**.</span></span>
2. <span data-ttu-id="79350-218">Una vez realizada correctamente la compilación, inicie el sitio web presionando **F5**.</span><span class="sxs-lookup"><span data-stu-id="79350-218">Once the build succeeds, start the website by pressing **F5**.</span></span> <span data-ttu-id="79350-219">Debería ver lo siguiente en la pantalla.</span><span class="sxs-lookup"><span data-stu-id="79350-219">You should see the following on your screen.</span></span>
   
    ![Captura de pantalla de la aplicación de voto Python + Azure Cosmos DB mostrada en un explorador web](./media/documentdb-python-application/cosmos-db-pythonr-run-application.png)
3. <span data-ttu-id="79350-221">Haga clic en **Create/Clear the Voting Database** (Crear/borrar la base de datos de votos) para generar la base de datos.</span><span class="sxs-lookup"><span data-stu-id="79350-221">Click **Create/Clear the Voting Database** to generate the database.</span></span>
   
    ![Captura de pantalla de la página de creación de la aplicación web: detalles sobre el desarrollo](./media/documentdb-python-application/cosmos-db-python-run-create-page.png)
4. <span data-ttu-id="79350-223">A continuación, haga clic en **Vote** (Votar) y seleccione su opción.</span><span class="sxs-lookup"><span data-stu-id="79350-223">Then, click **Vote** and select your option.</span></span>
   
    ![Captura de pantalla de la aplicación web con una pregunta de votación formulada](./media/documentdb-python-application/cosmos-db-vote.png)
5. <span data-ttu-id="79350-225">Por cada voto que emita se incrementará el contador correspondiente.</span><span class="sxs-lookup"><span data-stu-id="79350-225">For every vote you cast, it increments the appropriate counter.</span></span>
   
    ![Captura de pantalla de la página Resultados de la votación mostrada](./media/documentdb-python-application/cosmos-db-voting-results.png)
6. <span data-ttu-id="79350-227">Detenga la depuración del proyecto presionando MAYÚS+F5.</span><span class="sxs-lookup"><span data-stu-id="79350-227">Stop debugging the project by pressing Shift+F5.</span></span>

## <a name="step-5-deploy-the-web-application-to-azure"></a><span data-ttu-id="79350-228">Paso 5: Implementación de la aplicación web en Azure</span><span class="sxs-lookup"><span data-stu-id="79350-228">Step 5: Deploy the web application to Azure</span></span>
<span data-ttu-id="79350-229">Ahora que toda la aplicación funciona correctamente con Azure Cosmos DB, vamos a implementarla en Azure.</span><span class="sxs-lookup"><span data-stu-id="79350-229">Now that you have the complete application working correctly against Cosmos DB, we're going to deploy this to Azure.</span></span>

1. <span data-ttu-id="79350-230">Haga clic con el botón derecho en el proyecto en el Explorador de soluciones (asegúrese de que no se ejecuta localmente) y seleccione **Publicar**.</span><span class="sxs-lookup"><span data-stu-id="79350-230">Right-click the project in Solution Explorer (make sure you're not still running it locally) and select **Publish**.</span></span>  
   
     ![Captura de pantalla del tutorial seleccionado en el Explorador de soluciones, con la opción Publicar resaltada](./media/documentdb-python-application/image20.png)
2. <span data-ttu-id="79350-232">En el cuadro de diálogo **Publicar**, seleccione **Microsoft Azure App Service**, seleccione **Crear nuevo** y, después, haga clic en **Publicar**.</span><span class="sxs-lookup"><span data-stu-id="79350-232">In the **Publish** dialog box, select **Microsoft Azure App Service**, select **Create New**, and then click **Publish**.</span></span>
   
    ![Captura de pantalla de la ventana de publicación web con Microsoft Azure App Service resaltada](./media/documentdb-python-application/cosmos-db-python-publish.png)
3. <span data-ttu-id="79350-234">En el cuadro de diálogo **Crear App Service**, escriba el nombre de la aplicación web, junto con la **suscripción**, el **grupo de recursos**, el **plan de App Service** y, a continuación, haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="79350-234">In the **Create App Service** dialog box, enter the name for your web app along with your **Subscription**, **Resource Group**, and **App Service Plan**, then click **Create**.</span></span>
   
    ![Captura de pantalla de la ventana Aplicaciones web de Microsoft Azure](./media/documentdb-python-application/cosmos-db-python-create-app-service.png)
4. <span data-ttu-id="79350-236">En pocos segundos, Visual Studio terminará de publicar el servicio de aplicaciones y ejecutará un explorador donde podrá ver su trabajo ejecutándose en Azure.</span><span class="sxs-lookup"><span data-stu-id="79350-236">In a few seconds, Visual Studio will finish publishing your app service and launch a browser where you can see your handiwork running in Azure!</span></span>

    ![Captura de pantalla de la ventana Aplicaciones web de Microsoft Azure](./media/documentdb-python-application/cosmos-db-python-appservice-created.png)

## <a name="troubleshooting"></a><span data-ttu-id="79350-238">Solución de problemas</span><span class="sxs-lookup"><span data-stu-id="79350-238">Troubleshooting</span></span>
<span data-ttu-id="79350-239">Si esta es la primera aplicación de Python que se ejecuta en el equipo, asegúrese de que las carpetas siguientes (o las ubicaciones de instalación equivalentes) se incluyen en la variable PATH:</span><span class="sxs-lookup"><span data-stu-id="79350-239">If this is the first Python app you've run on your computer, ensure that the following folders (or the equivalent installation locations) are included in your PATH variable:</span></span>

    C:\Python27\site-packages;C:\Python27\;C:\Python27\Scripts;

<span data-ttu-id="79350-240">Si recibe un error en la página de votos y asignó al proyecto otro nombre distinto del de **tutorial**, asegúrese de que **\_\_init\_\_.py** hace referencia al nombre de proyecto correcto en la línea: `import tutorial.view`.</span><span class="sxs-lookup"><span data-stu-id="79350-240">If you receive an error on your vote page, and you named your project something other than **tutorial**, make sure that **\_\_init\_\_.py** references the correct project name in the line: `import tutorial.view`.</span></span>

## <a name="next-steps"></a><span data-ttu-id="79350-241">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="79350-241">Next steps</span></span>
<span data-ttu-id="79350-242">¡Enhorabuena!</span><span class="sxs-lookup"><span data-stu-id="79350-242">Congratulations!</span></span> <span data-ttu-id="79350-243">Acaba de completar su primera aplicación web de Python con Cosmos DB y de publicarla en Azure.</span><span class="sxs-lookup"><span data-stu-id="79350-243">You have just completed your first Python web application using Cosmos DB and published it to Azure.</span></span>

<span data-ttu-id="79350-244">Actualizamos y mejoramos este tema con frecuencia en función de los comentarios que recibimos.</span><span class="sxs-lookup"><span data-stu-id="79350-244">We update and improve this topic frequently based on your feedback.</span></span>  <span data-ttu-id="79350-245">Una vez completado el tutorial, no olvide incluir sus comentarios sobre las mejoras que quiera que se hagan. Para ello, use los botones de voto de la parte superior e inferior de esta página.</span><span class="sxs-lookup"><span data-stu-id="79350-245">Once you've completed the tutorial, please using the voting buttons at the top and bottom of this page, and be sure to include your feedback on what improvements you want to see made.</span></span> <span data-ttu-id="79350-246">Si quiere que nos pongamos en contacto directamente con usted, puede incluir su dirección de correo electrónico en los comentarios.</span><span class="sxs-lookup"><span data-stu-id="79350-246">If you'd like us to contact you directly, feel free to include your email address in your comments.</span></span>

<span data-ttu-id="79350-247">Para agregar funcionalidad adicional a la aplicación web, revise las API disponibles en el [SDK de Python de Azure Cosmos DB](documentdb-sdk-python.md).</span><span class="sxs-lookup"><span data-stu-id="79350-247">To add additional functionality to your web application, review the APIs available in the [Azure Cosmos DB Python SDK](documentdb-sdk-python.md).</span></span>

<span data-ttu-id="79350-248">Para más información acerca de Azure, Visual Studio y Python, consulte el [Python Developer Center](https://azure.microsoft.com/develop/python/).</span><span class="sxs-lookup"><span data-stu-id="79350-248">For more information about Azure, Visual Studio, and Python, see the [Python Developer Center](https://azure.microsoft.com/develop/python/).</span></span> 

<span data-ttu-id="79350-249">Para ver tutoriales adicionales sobre Python Flask, consulte el tutorial [The Flask Mega-Tutorial, Part I: Hello, World!](http://blog.miguelgrinberg.com/post/the-flask-mega-tutorial-part-i-hello-world).</span><span class="sxs-lookup"><span data-stu-id="79350-249">For additional Python Flask tutorials, see [The Flask Mega-Tutorial, Part I: Hello, World!](http://blog.miguelgrinberg.com/post/the-flask-mega-tutorial-part-i-hello-world).</span></span> 

[Visual Studio Express]: http://www.visualstudio.com/products/visual-studio-express-vs.aspx
[2]: https://www.python.org/downloads/windows/
[3]: https://www.microsoft.com/download/details.aspx?id=44266
[Microsoft Web Platform Installer]: http://www.microsoft.com/web/downloads/platform.aspx
[Azure portal]: http://portal.azure.com
