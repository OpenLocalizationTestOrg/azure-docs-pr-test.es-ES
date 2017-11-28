---
title: Django y MySQL en Azure con Python Tools 2.2 para Visual Studio
description: "Obtenga información acerca de cómo usar las herramientas de Python para Visual Studio para crear una aplicación web Django que almacene datos en una instancia de base de datos MySQL y se pueda implementar en Aplicaciones web del Servicio de aplicaciones de Azure."
services: app-service\web
documentationcenter: python
author: huguesv
manager: erikre
editor: 
ms.assetid: c60a50b5-8b5e-4818-a442-16362273dabb
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: python
ms.topic: article
ms.date: 07/07/2016
ms.author: huvalo
ms.openlocfilehash: fd85337ecdc638a4c18065a0ce94f697da8197f1
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/29/2017
---
# <a name="django-and-mysql-on-azure-with-python-tools-22-for-visual-studio"></a><span data-ttu-id="7f688-103">Django y MySQL en Azure con Python Tools 2.2 para Visual Studio</span><span class="sxs-lookup"><span data-stu-id="7f688-103">Django and MySQL on Azure with Python Tools 2.2 for Visual Studio</span></span>
[!INCLUDE [tabs](../../includes/app-service-web-get-started-nav-tabs.md)]

<span data-ttu-id="7f688-104">En este tutorial, se usarán las [Herramientas de Python para Visual Studio](https://www.visualstudio.com/vs/python) a fin de crear una aplicación web de sondeos sencilla mediante una de las plantillas de ejemplo de PTVS.</span><span class="sxs-lookup"><span data-stu-id="7f688-104">In this tutorial, you'll use [Python Tools for Visual Studio](https://www.visualstudio.com/vs/python) to create a simple polls web app using one of the PTVS sample templates.</span></span> <span data-ttu-id="7f688-105">Aprenderá a usar un servicio de MySQL hospedado en Azure, a configurar la aplicación web para usar MySQL y publicar la aplicación web en [Aplicaciones web del Servicio de aplicaciones de Azure](http://go.microsoft.com/fwlink/?LinkId=529714).</span><span class="sxs-lookup"><span data-stu-id="7f688-105">You'll learn how to use a MySQL service hosted on Azure, how to configure the web app to use MySQL, and how to publish the web app to [Azure App Service Web Apps](http://go.microsoft.com/fwlink/?LinkId=529714).</span></span>

> [!NOTE]
> <span data-ttu-id="7f688-106">La información de este tutorial también está disponible en el siguiente vídeo:</span><span class="sxs-lookup"><span data-stu-id="7f688-106">The information contained in this tutorial is also available in the following video:</span></span>
> 
> <span data-ttu-id="7f688-107">[PTVS 2.1: Django app with MySQL][video] (PTVS 2.1: aplicación Django con MySQL)</span><span class="sxs-lookup"><span data-stu-id="7f688-107">[PTVS 2.1: Django app with MySQL][video]</span></span>
> 
> 

<span data-ttu-id="7f688-108">Consulte el [Centro para desarrolladores de Python] para acceder a más artículos sobre el desarrollo de Aplicaciones web del Servicio de aplicaciones de Azure con PTVS mediante marcos web Bottle, Flask y Django, con Almacenamiento de tablas de Azure y los servicios de Base de datos MySQL y SQL.</span><span class="sxs-lookup"><span data-stu-id="7f688-108">See the [Python Developer Center] for more articles that cover development of Azure App Service Web Apps with PTVS using Bottle, Flask and Django web frameworks, with Azure Table Storage, MySQL, and SQL Database services.</span></span> <span data-ttu-id="7f688-109">Si bien estos artículos se centran en el Servicio de aplicaciones, los pasos son similares a los que se aplican para desarrollar [Servicios en la nube de Azure].</span><span class="sxs-lookup"><span data-stu-id="7f688-109">While this article focuses on App Service, the steps are similar when developing [Azure Cloud Services].</span></span>

## <a name="prerequisites"></a><span data-ttu-id="7f688-110">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="7f688-110">Prerequisites</span></span>
* <span data-ttu-id="7f688-111">Visual Studio 2015</span><span class="sxs-lookup"><span data-stu-id="7f688-111">Visual Studio 2015</span></span>
* <span data-ttu-id="7f688-112">[Python 2.7 de 32 bits] o [Python 3.4 de 32 bits]</span><span class="sxs-lookup"><span data-stu-id="7f688-112">[Python 2.7 32-bit] or [Python 3.4 32-bit]</span></span>
* <span data-ttu-id="7f688-113">[Python Tools 2.2 para Visual Studio]</span><span class="sxs-lookup"><span data-stu-id="7f688-113">[Python Tools 2.2 for Visual Studio]</span></span>
* <span data-ttu-id="7f688-114">[archivos VSIX de ejemplo de Python Tools 2.2 para Visual Studio]</span><span class="sxs-lookup"><span data-stu-id="7f688-114">[Python Tools 2.2 for Visual Studio Samples VSIX]</span></span>
* <span data-ttu-id="7f688-115">[Azure SDK y herramientas para VS 2015]</span><span class="sxs-lookup"><span data-stu-id="7f688-115">[Azure SDK Tools for VS 2015]</span></span>
* <span data-ttu-id="7f688-116">Django 1.9 o posterior</span><span class="sxs-lookup"><span data-stu-id="7f688-116">Django 1.9 or later</span></span>

[!INCLUDE [create-account-and-websites-note](../../includes/create-account-and-websites-note.md)]

<!-- This note should not render as part of the the previous include. -->

> [!NOTE]
> <span data-ttu-id="7f688-117">Si desea empezar a trabajar con el Servicio de aplicaciones de Azure antes de inscribirse para abrir una cuenta de Azure, vaya a [Prueba del Servicio de aplicaciones](https://azure.microsoft.com/try/app-service/), donde podrá crear inmediatamente una aplicación web de inicio de corta duración en el Servicio de aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="7f688-117">If you want to get started with Azure App Service before signing up for an Azure account, go to [Try App Service](https://azure.microsoft.com/try/app-service/), where you can immediately create a short-lived starter web app in App Service.</span></span> <span data-ttu-id="7f688-118">No es necesario proporcionar ninguna tarjeta de crédito ni asumir ningún compromiso.</span><span class="sxs-lookup"><span data-stu-id="7f688-118">No credit card is required, and no commitments are necessary.</span></span>
> 
> 

## <a name="create-the-project"></a><span data-ttu-id="7f688-119">Creación del proyecto</span><span class="sxs-lookup"><span data-stu-id="7f688-119">Create the Project</span></span>
<span data-ttu-id="7f688-120">En esta sección, va a crear un proyecto de Visual Studio con la utilización de una plantilla de ejemplo.</span><span class="sxs-lookup"><span data-stu-id="7f688-120">In this section, you'll create a Visual Studio project using a sample template.</span></span> <span data-ttu-id="7f688-121">Va a crear un entorno virtual e instalar los paquetes necesarios.</span><span class="sxs-lookup"><span data-stu-id="7f688-121">You'll create a virtual environment and install required packages.</span></span> <span data-ttu-id="7f688-122">Va a crear una base de datos local con sqlite.</span><span class="sxs-lookup"><span data-stu-id="7f688-122">You'll create a local database using sqlite.</span></span> <span data-ttu-id="7f688-123">Después, va a ejecutar la aplicación localmente.</span><span class="sxs-lookup"><span data-stu-id="7f688-123">Then you'll run the application locally.</span></span>

1. <span data-ttu-id="7f688-124">En Visual Studio, seleccione **Archivo**, **Nuevo proyecto**.</span><span class="sxs-lookup"><span data-stu-id="7f688-124">In Visual Studio, select **File**, **New Project**.</span></span>
2. <span data-ttu-id="7f688-125">Las plantillas de proyecto de los [archivos VSIX de ejemplo de Python Tools 2.2 para Visual Studio] se encuentran disponibles en **Python**, **Ejemplos**.</span><span class="sxs-lookup"><span data-stu-id="7f688-125">The project templates from the [Python Tools 2.2 for Visual Studio Samples VSIX] are available under **Python**, **Samples**.</span></span> <span data-ttu-id="7f688-126">Seleccione **Polls Django Web Project** (Proyecto web de Django para sondeos) y haga clic en OK (Aceptar) para crear el proyecto.</span><span class="sxs-lookup"><span data-stu-id="7f688-126">Select **Polls Django Web Project** and click OK to create the project.</span></span>
   
    ![Cuadro de diálogo Nuevo proyecto](./media/web-sites-python-ptvs-django-mysql/PollsDjangoNewProject.png)
3. <span data-ttu-id="7f688-128">Se le pedirá que instale paquetes externos.</span><span class="sxs-lookup"><span data-stu-id="7f688-128">You will be prompted to install external packages.</span></span> <span data-ttu-id="7f688-129">Seleccione **Instalar en un entorno virtual**.</span><span class="sxs-lookup"><span data-stu-id="7f688-129">Select **Install into a virtual environment**.</span></span>
   
    ![Cuadro de diálogo Paquetes externos](./media/web-sites-python-ptvs-django-mysql/PollsDjangoExternalPackages.png)
4. <span data-ttu-id="7f688-131">Seleccione **Python 2.7** o **Python 3.4** como intérprete de base.</span><span class="sxs-lookup"><span data-stu-id="7f688-131">Select **Python 2.7** or **Python 3.4** as the base interpreter.</span></span>
   
    ![Cuadro de diálogo Agregar entorno virtual](./media/web-sites-python-ptvs-django-mysql/PollsCommonAddVirtualEnv.png)
5. <span data-ttu-id="7f688-133">En el **Explorador de soluciones**, haga clic con el botón derecho en el nodo de proyecto, seleccione **Python** y **Django Migrate** (Migración de Django).</span><span class="sxs-lookup"><span data-stu-id="7f688-133">In **Solution Explorer**, right-click on the project node and select **Python**, and then select **Django Migrate**.</span></span>  <span data-ttu-id="7f688-134">Después, seleccione **Django Create Superuser (Crear superusuario de Django)**.</span><span class="sxs-lookup"><span data-stu-id="7f688-134">Then select **Django Create Superuser**.</span></span>
6. <span data-ttu-id="7f688-135">Se abre la consola de administración de Django donde se va a crear una base de datos de sqlite en la carpeta del proyecto.</span><span class="sxs-lookup"><span data-stu-id="7f688-135">This will open a Django Management Console and create a sqlite database in the project folder.</span></span> <span data-ttu-id="7f688-136">Siga las indicaciones para crear un usuario.</span><span class="sxs-lookup"><span data-stu-id="7f688-136">Follow the prompts to create a user.</span></span>
7. <span data-ttu-id="7f688-137">Presione `F5`para confirmar que la aplicación funciona.</span><span class="sxs-lookup"><span data-stu-id="7f688-137">Confirm that the application works by pressing `F5`.</span></span>
8. <span data-ttu-id="7f688-138">Haga clic en **Iniciar sesión** en la barra de navegación de la parte superior.</span><span class="sxs-lookup"><span data-stu-id="7f688-138">Click **Log in** from the navigation bar at the top.</span></span>
   
    ![Barra de navegación de Django](./media/web-sites-python-ptvs-django-mysql/PollsDjangoCommonBrowserLocalMenu.png)
9. <span data-ttu-id="7f688-140">Escriba las credenciales del usuario que ha creado al sincronizar la base de datos.</span><span class="sxs-lookup"><span data-stu-id="7f688-140">Enter the credentials for the user you created when you synchronized the database.</span></span>
   
    ![Formulario de inicio de sesión](./media/web-sites-python-ptvs-django-mysql/PollsDjangoCommonBrowserLocalLogin.png)
10. <span data-ttu-id="7f688-142">Haga clic en **Create Sample Polls**(Crear sondeos de ejemplo).</span><span class="sxs-lookup"><span data-stu-id="7f688-142">Click **Create Sample Polls**.</span></span>
    
     ![Create Sample Polls](./media/web-sites-python-ptvs-django-mysql/PollsDjangoCommonBrowserNoPolls.png)
11. <span data-ttu-id="7f688-144">Haga clic en un sondeo y vote.</span><span class="sxs-lookup"><span data-stu-id="7f688-144">Click on a poll and vote.</span></span>
    
     ![Votación en sondeos de ejemplo](./media/web-sites-python-ptvs-django-mysql/PollsDjangoSqliteBrowser.png)

## <a name="create-a-mysql-database"></a><span data-ttu-id="7f688-146">Creación de una base de datos MySQL</span><span class="sxs-lookup"><span data-stu-id="7f688-146">Create a MySQL Database</span></span>
<span data-ttu-id="7f688-147">Para la base de datos, va a crear una base de datos MySQL de ClearDB hospedada en Azure.</span><span class="sxs-lookup"><span data-stu-id="7f688-147">For the database, you'll create a ClearDB MySQL hosted database on Azure.</span></span>

<span data-ttu-id="7f688-148">Como alternativa, puede crear su propia máquina virtual para que se ejecute en Azure y, a continuación, instalar y administrar MySQL por su cuenta.</span><span class="sxs-lookup"><span data-stu-id="7f688-148">As an alternative, you can create your own Virtual Machine running in Azure, then install and administer MySQL yourself.</span></span>

<span data-ttu-id="7f688-149">Siga estos pasos para crear una base de datos con un plan gratuito.</span><span class="sxs-lookup"><span data-stu-id="7f688-149">You can create a database with a free plan by following these steps.</span></span>

1. <span data-ttu-id="7f688-150">Inicie sesión en el [Portal de Azure].</span><span class="sxs-lookup"><span data-stu-id="7f688-150">Log in to the [Azure Portal].</span></span>
2. <span data-ttu-id="7f688-151">En la parte superior del panel de navegación, haga clic en **NUEVO**, **Datos y almacenamiento** y, finalmente, en **Base de datos MySQL**.</span><span class="sxs-lookup"><span data-stu-id="7f688-151">At the Top of the navigation pane, click **NEW**, then click **Data + Storage**, and then click **MySQL Database**.</span></span>
3. <span data-ttu-id="7f688-152">Configure la nueva base de datos MySQL mediante la creación de un nuevo grupo de recursos y seleccione la ubicación adecuada para él.</span><span class="sxs-lookup"><span data-stu-id="7f688-152">Configure the new MySQL database by creating a new resource group and select the appropriate location for it.</span></span>
4. <span data-ttu-id="7f688-153">Una vez creada la base de datos MySQL, haga clic en **Propiedades** en la hoja de la base de datos.</span><span class="sxs-lookup"><span data-stu-id="7f688-153">Once the MySQL database is created, click **Properties** in the database blade.</span></span>
5. <span data-ttu-id="7f688-154">Use el botón Copiar para colocar el valor de **CONNECTIONSTRING** en el Portapapeles.</span><span class="sxs-lookup"><span data-stu-id="7f688-154">Use the copy button to put the value of **CONNECTION STRING** on the clipboard.</span></span>

## <a name="configure-the-project"></a><span data-ttu-id="7f688-155">Configuración del proyecto</span><span class="sxs-lookup"><span data-stu-id="7f688-155">Configure the Project</span></span>
<span data-ttu-id="7f688-156">En esta sección, va a configurar nuestra aplicación web para usar la base de datos MySQL que acaba de crear.</span><span class="sxs-lookup"><span data-stu-id="7f688-156">In this section, you'll configure our web app to use the MySQL database you just created.</span></span> <span data-ttu-id="7f688-157">También va a instalar paquetes adicionales de Python necesarios para utilizar bases de datos MySQL con Django.</span><span class="sxs-lookup"><span data-stu-id="7f688-157">You'll also install additional Python packages required to use MySQL databases with Django.</span></span> <span data-ttu-id="7f688-158">Después, ejecutará la aplicación web localmente.</span><span class="sxs-lookup"><span data-stu-id="7f688-158">Then you'll run the web app locally.</span></span>

1. <span data-ttu-id="7f688-159">En Visual Studio, abra **settings.py**desde la carpeta *ProjectName* .</span><span class="sxs-lookup"><span data-stu-id="7f688-159">In Visual Studio, open **settings.py**, from the *ProjectName* folder.</span></span> <span data-ttu-id="7f688-160">Pegue temporalmente la cadena de conexión en el editor.</span><span class="sxs-lookup"><span data-stu-id="7f688-160">Temporarily paste the connection string in the editor.</span></span> <span data-ttu-id="7f688-161">La cadena de conexión tiene el siguiente formato:</span><span class="sxs-lookup"><span data-stu-id="7f688-161">The connection string is in this format:</span></span>
   
        Database=<NAME>;Data Source=<HOST>;User Id=<USER>;Password=<PASSWORD>
   
    <span data-ttu-id="7f688-162">Cambie el **MOTOR** predeterminado de la base de datos para que use MySQL y establezca los valores de **NOMBRE**, **USUARIO**, **CONTRASEÑA** y **HOST** desde **CONNECTIONSTRING**.</span><span class="sxs-lookup"><span data-stu-id="7f688-162">Change the default database **ENGINE** to use MySQL, and set the values for **NAME**, **USER**, **PASSWORD** and **HOST** from the **CONNECTIONSTRING**.</span></span>
   
        DATABASES = {
            'default': {
                'ENGINE': 'django.db.backends.mysql',
                'NAME': '<Database>',
                'USER': '<User Id>',
                'PASSWORD': '<Password>',
                'HOST': '<Data Source>',
                'PORT': '',
            }
        }
2. <span data-ttu-id="7f688-163">En el Explorador de soluciones, en **Entornos de Python**, haga clic con el botón derecho en el entorno virtual y seleccione **Instalar paquete de Python**.</span><span class="sxs-lookup"><span data-stu-id="7f688-163">In Solution Explorer, under **Python Environments**, right-click on the virtual environment and select **Install Python Package**.</span></span>
3. <span data-ttu-id="7f688-164">Instale el paquete `mysqlclient` con **pip**.</span><span class="sxs-lookup"><span data-stu-id="7f688-164">Install the package `mysqlclient` using **pip**.</span></span>
   
    ![Cuadro de diálogo Instalar paquete](./media/web-sites-python-ptvs-django-mysql/PollsDjangoMySQLInstallPackage.png)
4. <span data-ttu-id="7f688-166">En el **Explorador de soluciones**, haga clic con el botón derecho en el nodo de proyecto, seleccione **Python** y **Django Migrate** (Migración de Django).</span><span class="sxs-lookup"><span data-stu-id="7f688-166">In **Solution Explorer**, right-click on the project node and select **Python**, and then select **Django Migrate**.</span></span>  <span data-ttu-id="7f688-167">Después, seleccione **Django Create Superuser (Crear superusuario de Django)**.</span><span class="sxs-lookup"><span data-stu-id="7f688-167">Then select **Django Create Superuser**.</span></span>
   
    <span data-ttu-id="7f688-168">De esta forma, se crearán las tablas para la base de datos MySQL que ha creado en la sección anterior.</span><span class="sxs-lookup"><span data-stu-id="7f688-168">This will create the tables for the MySQL database you created in the previous section.</span></span> <span data-ttu-id="7f688-169">Siga las indicaciones para crear un usuario, que no tiene que coincidir con el usuario de la base de datos sqlite creada en la primera sección de este artículo.</span><span class="sxs-lookup"><span data-stu-id="7f688-169">Follow the prompts to create a user, which doesn't have to match the user in the sqlite database created in the first section of this article.</span></span>
5. <span data-ttu-id="7f688-170">Presione `F5`para ejecutar la aplicación.</span><span class="sxs-lookup"><span data-stu-id="7f688-170">Run the application with `F5`.</span></span> <span data-ttu-id="7f688-171">Los sondeos creados con **Create Sample Polls** (Crear sondeos de ejemplo) y los datos enviados al votar se serializarán en la base de datos MySQL.</span><span class="sxs-lookup"><span data-stu-id="7f688-171">Polls that are created with **Create Sample Polls** and the data submitted by voting will be serialized in the MySQL database.</span></span>

## <a name="publish-the-web-app-to-azure-app-service"></a><span data-ttu-id="7f688-172">Publicación de aplicación web del Servicio de aplicaciones de Azure</span><span class="sxs-lookup"><span data-stu-id="7f688-172">Publish the web app to Azure App Service</span></span>
<span data-ttu-id="7f688-173">El SDK de Azure .NET ofrece una forma fácil de implementar la aplicación web en el Servicio de aplicaciones de Azure.</span><span class="sxs-lookup"><span data-stu-id="7f688-173">The Azure .NET SDK provides an easy way to deploy your web app to Azure App Service.</span></span>

1. <span data-ttu-id="7f688-174">En el **Explorador de soluciones**, haga clic con el botón derecho en el nodo del proyecto y seleccione **Publicar**.</span><span class="sxs-lookup"><span data-stu-id="7f688-174">In **Solution Explorer**, right-click on the project node and select **Publish**.</span></span>
   
    ![Cuadro de diálogo Publicación web](./media/web-sites-python-ptvs-django-mysql/PollsCommonPublishWebSiteDialog.png)
2. <span data-ttu-id="7f688-176">Haga clic en **Servicio de aplicaciones de Microsoft Azure**.</span><span class="sxs-lookup"><span data-stu-id="7f688-176">Click on **Microsoft Azure App Service**.</span></span>
3. <span data-ttu-id="7f688-177">Haga clic en **Nuevo** para crear una aplicación web nueva.</span><span class="sxs-lookup"><span data-stu-id="7f688-177">Click on **New** to create a new web app.</span></span>
4. <span data-ttu-id="7f688-178">Rellene los campos siguientes y haga clic en **Crear**:</span><span class="sxs-lookup"><span data-stu-id="7f688-178">Fill in the following fields and click **Create**:</span></span>
   
   * <span data-ttu-id="7f688-179">**Nombre de aplicación web**</span><span class="sxs-lookup"><span data-stu-id="7f688-179">**Web App name**</span></span>
   * <span data-ttu-id="7f688-180">**Plan del Servicio de aplicaciones**</span><span class="sxs-lookup"><span data-stu-id="7f688-180">**App Service plan**</span></span>
   * <span data-ttu-id="7f688-181">**Grupos de recursos**</span><span class="sxs-lookup"><span data-stu-id="7f688-181">**Resource group**</span></span>
   * <span data-ttu-id="7f688-182">**Región**</span><span class="sxs-lookup"><span data-stu-id="7f688-182">**Region**</span></span>
   * <span data-ttu-id="7f688-183">Deje **Servidor de base de datos** establecido en **No hay base de datos**</span><span class="sxs-lookup"><span data-stu-id="7f688-183">Leave **Database server** set to **No database**</span></span>
5. <span data-ttu-id="7f688-184">Acepte todos los valores predeterminados y haga clic en **Publicar**.</span><span class="sxs-lookup"><span data-stu-id="7f688-184">Accept all other defaults and click **Publish**.</span></span>
6. <span data-ttu-id="7f688-185">El explorador web se abrirá automáticamente en la aplicación web publicada.</span><span class="sxs-lookup"><span data-stu-id="7f688-185">Your web browser will open automatically to the published web app.</span></span> <span data-ttu-id="7f688-186">La aplicación web ahora debe funcionar según lo previsto, con el uso de la base de datos **MySQL** hospedada en Azure.</span><span class="sxs-lookup"><span data-stu-id="7f688-186">You should see the web app working as expected, using the **MySQL** database hosted on Azure.</span></span>
   
    ![Explorador web](./media/web-sites-python-ptvs-django-mysql/PollsDjangoAzureBrowser.png)
   
    <span data-ttu-id="7f688-188">¡Enhorabuena!</span><span class="sxs-lookup"><span data-stu-id="7f688-188">Congratulations!</span></span> <span data-ttu-id="7f688-189">Ha publicado correctamente la aplicación web basada en MySQL en Azure.</span><span class="sxs-lookup"><span data-stu-id="7f688-189">You have successfully published your MySQL-based web app to Azure.</span></span>

## <a name="next-steps"></a><span data-ttu-id="7f688-190">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="7f688-190">Next steps</span></span>
<span data-ttu-id="7f688-191">Siga estos vínculos para obtener más información sobre las herramientas de Python para Visual Studio, Django y MySQL.</span><span class="sxs-lookup"><span data-stu-id="7f688-191">Follow these links to learn more about Python Tools for Visual Studio, Django and MySQL.</span></span>

* <span data-ttu-id="7f688-192">[Documentación sobre Python Tools para Visual Studio]</span><span class="sxs-lookup"><span data-stu-id="7f688-192">[Python Tools for Visual Studio Documentation]</span></span>
  * <span data-ttu-id="7f688-193">[Proyectos web]</span><span class="sxs-lookup"><span data-stu-id="7f688-193">[Web Projects]</span></span>
  * <span data-ttu-id="7f688-194">[Proyectos de servicio en la nube]</span><span class="sxs-lookup"><span data-stu-id="7f688-194">[Cloud Service Projects]</span></span>
  * <span data-ttu-id="7f688-195">[Depuración remota en Microsoft Azure]</span><span class="sxs-lookup"><span data-stu-id="7f688-195">[Remote Debugging on Microsoft Azure]</span></span>
* <span data-ttu-id="7f688-196">[Documentación de Django]</span><span class="sxs-lookup"><span data-stu-id="7f688-196">[Django Documentation]</span></span>
* <span data-ttu-id="7f688-197">[MySQL]</span><span class="sxs-lookup"><span data-stu-id="7f688-197">[MySQL]</span></span>

<span data-ttu-id="7f688-198">Para más información, vea el [Centro para desarrolladores de Python](/develop/python/).</span><span class="sxs-lookup"><span data-stu-id="7f688-198">For more information, see the [Python Developer Center](/develop/python/).</span></span>

<!--Link references-->

[Centro para desarrolladores de Python]: /develop/python/
[Servicios en la nube de Azure]: ../cloud-services/cloud-services-python-ptvs.md

<!--External Link references-->

[Portal de Azure]: https://portal.azure.com
[Python Tools for Visual Studio]: https://www.visualstudio.com/vs/python/
[Python Tools 2.2 para Visual Studio]: http://go.microsoft.com/fwlink/?LinkID=624025
[archivos VSIX de ejemplo de Python Tools 2.2 para Visual Studio]: http://go.microsoft.com/fwlink/?LinkID=624025
[Azure SDK y herramientas para VS 2015]: http://go.microsoft.com/fwlink/?LinkId=518003
[Python 2.7 de 32 bits]: http://go.microsoft.com/fwlink/?LinkId=517190
[Python 3.4 de 32 bits]: http://go.microsoft.com/fwlink/?LinkId=517191
[Documentación sobre Python Tools para Visual Studio]: http://aka.ms/ptvsdocs
[Depuración remota en Microsoft Azure]: http://go.microsoft.com/fwlink/?LinkId=624026
[Proyectos web]: http://go.microsoft.com/fwlink/?LinkId=624027
[Proyectos de servicio en la nube]: http://go.microsoft.com/fwlink/?LinkId=624028
[Documentación de Django]: https://www.djangoproject.com/
[MySQL]: http://www.mysql.com/
[video]: http://youtu.be/oKCApIrS0Lo
