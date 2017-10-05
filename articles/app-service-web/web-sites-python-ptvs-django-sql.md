---
title: Django y Base de datos SQL en Azure con Python Tools 2.2 para Visual Studio
description: "Obtenga información acerca de cómo usar las herramientas de Python para Visual Studio para crear una aplicación web Django que almacene datos en una instancia de base de datos SQL y se pueda implementar en Aplicaciones web del Servicio de aplicaciones de Azure."
services: app-service\web
tags: python
documentationcenter: python
author: huguesv
manager: erikre
editor: 
ms.assetid: 3a677e64-b5a9-4d43-b9c0-66246368b483
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: python
ms.topic: article
ms.date: 07/07/2016
ms.author: huvalo
ms.openlocfilehash: 65b59dee2b7bddca77d31c692dab713c68d67e24
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="django-and-sql-database-on-azure-with-python-tools-22-for-visual-studio"></a><span data-ttu-id="a7636-103">Django y Base de datos SQL en Azure con Python Tools 2.2 para Visual Studio</span><span class="sxs-lookup"><span data-stu-id="a7636-103">Django and SQL Database on Azure with Python Tools 2.2 for Visual Studio</span></span>
<span data-ttu-id="a7636-104">En este tutorial, usaremos las [Herramientas de Python para Visual Studio] a fin de crear una aplicación web de sondeos sencilla mediante una de las plantillas de ejemplo de PTVS.</span><span class="sxs-lookup"><span data-stu-id="a7636-104">In this tutorial, we'll use [Python Tools for Visual Studio] to create a simple polls web app using one of the PTVS sample templates.</span></span> <span data-ttu-id="a7636-105">Este tutorial también se encuentra disponible como [vídeo](https://www.youtube.com/watch?v=ZwcoGcIeHF4).</span><span class="sxs-lookup"><span data-stu-id="a7636-105">This tutorial is also available as a [video](https://www.youtube.com/watch?v=ZwcoGcIeHF4).</span></span>

<span data-ttu-id="a7636-106">Vamos a aprender a usar una base de datos SQL hospedada en Azure, configurar la aplicación web para usar una base de datos SQL y publicar la aplicación web en [Aplicaciones web del Servicio de aplicaciones de Azure](http://go.microsoft.com/fwlink/?LinkId=529714).</span><span class="sxs-lookup"><span data-stu-id="a7636-106">We'll learn how to use a SQL database hosted on Azure, how to configure the web app to use a SQL database, and how to publish the web app to [Azure App Service Web Apps](http://go.microsoft.com/fwlink/?LinkId=529714).</span></span>

<span data-ttu-id="a7636-107">Vea el [Centro para desarrolladores de Python] para acceder a más artículos sobre el desarrollo de Aplicaciones web del Servicio de aplicaciones de Azure con PTVS mediante marcos web Bottle, Flask y Django, con Almacenamiento de tablas de Azure y los servicios de Base de datos MySQL y SQL.</span><span class="sxs-lookup"><span data-stu-id="a7636-107">See the [Python Developer Center] for more articles that cover development of Azure App Service Web Apps with PTVS using Bottle, Flask and Django web frameworks, with Azure Table Storage, MySQL and SQL Database services.</span></span> <span data-ttu-id="a7636-108">Si bien estos artículos se centran en el Servicio de aplicaciones, los pasos son similares a los que se aplican para desarrollar [Servicios en la nube de Azure].</span><span class="sxs-lookup"><span data-stu-id="a7636-108">While this article focuses on App Service, the steps are similar when developing [Azure Cloud Services].</span></span>

## <a name="prerequisites"></a><span data-ttu-id="a7636-109">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="a7636-109">Prerequisites</span></span>
* <span data-ttu-id="a7636-110">Visual Studio 2015</span><span class="sxs-lookup"><span data-stu-id="a7636-110">Visual Studio 2015</span></span>
* <span data-ttu-id="a7636-111">[Python 2.7 de 32 bits]</span><span class="sxs-lookup"><span data-stu-id="a7636-111">[Python 2.7 32-bit]</span></span>
* <span data-ttu-id="a7636-112">[Python Tools 2.2 para Visual Studio]</span><span class="sxs-lookup"><span data-stu-id="a7636-112">[Python Tools 2.2 for Visual Studio]</span></span>
* <span data-ttu-id="a7636-113">[archivos VSIX de ejemplo de Python Tools 2.2 para Visual Studio]</span><span class="sxs-lookup"><span data-stu-id="a7636-113">[Python Tools 2.2 for Visual Studio Samples VSIX]</span></span>
* <span data-ttu-id="a7636-114">[Azure SDK y herramientas para VS 2015]</span><span class="sxs-lookup"><span data-stu-id="a7636-114">[Azure SDK Tools for VS 2015]</span></span>
* <span data-ttu-id="a7636-115">Django 1.9 o posterior</span><span class="sxs-lookup"><span data-stu-id="a7636-115">Django 1.9 or later</span></span>

[!INCLUDE [create-account-and-websites-note](../../includes/create-account-and-websites-note.md)]

> [!NOTE]
> <span data-ttu-id="a7636-116">Si desea empezar a trabajar con el Servicio de aplicaciones de Azure antes de inscribirse para abrir una cuenta de Azure, vaya a [Prueba del Servicio de aplicaciones](https://azure.microsoft.com/try/app-service/), donde podrá crear inmediatamente una aplicación web de inicio de corta duración en el Servicio de aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="a7636-116">If you want to get started with Azure App Service before signing up for an Azure account, go to [Try App Service](https://azure.microsoft.com/try/app-service/), where you can immediately create a short-lived starter web app in App Service.</span></span> <span data-ttu-id="a7636-117">No es necesario proporcionar ninguna tarjeta de crédito ni asumir ningún compromiso.</span><span class="sxs-lookup"><span data-stu-id="a7636-117">No credit cards required; no commitments.</span></span>
>
>

## <a name="create-the-project"></a><span data-ttu-id="a7636-118">Creación del proyecto</span><span class="sxs-lookup"><span data-stu-id="a7636-118">Create the Project</span></span>
<span data-ttu-id="a7636-119">En esta sección, vamos a crear un proyecto de Visual Studio con la utilización de una plantilla de ejemplo.</span><span class="sxs-lookup"><span data-stu-id="a7636-119">In this section, we'll create a Visual Studio project using a sample template.</span></span> <span data-ttu-id="a7636-120">Vamos a crear un entorno virtual e instalar los paquetes necesarios.</span><span class="sxs-lookup"><span data-stu-id="a7636-120">We'll create a virtual environment and install required packages.</span></span> <span data-ttu-id="a7636-121">Vamos a crear una base de datos local con sqlite.</span><span class="sxs-lookup"><span data-stu-id="a7636-121">We'll create a local database using sqlite.</span></span> <span data-ttu-id="a7636-122">A continuación, ejecutaremos la aplicación web localmente.</span><span class="sxs-lookup"><span data-stu-id="a7636-122">Then we'll run the web app locally.</span></span>

1. <span data-ttu-id="a7636-123">En Visual Studio, seleccione **Archivo**, **Nuevo proyecto**.</span><span class="sxs-lookup"><span data-stu-id="a7636-123">In Visual Studio, select **File**, **New Project**.</span></span>
2. <span data-ttu-id="a7636-124">Las plantillas de proyecto de los [archivos VSIX de ejemplo de Python Tools 2.2 para Visual Studio] se encuentran disponibles en **Python**, **Ejemplos**.</span><span class="sxs-lookup"><span data-stu-id="a7636-124">The project templates from the [Python Tools 2.2 for Visual Studio Samples VSIX] are available under **Python**, **Samples**.</span></span> <span data-ttu-id="a7636-125">Seleccione **Polls Django Web Project** (Proyecto web de Django para sondeos) y haga clic en OK (Aceptar) para crear el proyecto.</span><span class="sxs-lookup"><span data-stu-id="a7636-125">Select **Polls Django Web Project** and click OK to create the project.</span></span>

     ![Cuadro de diálogo Nuevo proyecto](./media/web-sites-python-ptvs-django-sql/PollsDjangoNewProject.png)
3. <span data-ttu-id="a7636-127">Se le pedirá que instale paquetes externos.</span><span class="sxs-lookup"><span data-stu-id="a7636-127">You will be prompted to install external packages.</span></span> <span data-ttu-id="a7636-128">Seleccione **Instalar en un entorno virtual**.</span><span class="sxs-lookup"><span data-stu-id="a7636-128">Select **Install into a virtual environment**.</span></span>

     ![Cuadro de diálogo Paquetes externos](./media/web-sites-python-ptvs-django-sql/PollsDjangoExternalPackages.png)
4. <span data-ttu-id="a7636-130">Seleccione **Python 2.7** como intérprete de base.</span><span class="sxs-lookup"><span data-stu-id="a7636-130">Select **Python 2.7** as the base interpreter.</span></span>

     ![Cuadro de diálogo Agregar entorno virtual](./media/web-sites-python-ptvs-django-sql/PollsCommonAddVirtualEnv.png)
5. <span data-ttu-id="a7636-132">En el **Explorador de soluciones**, haga clic con el botón derecho en el nodo de proyecto, seleccione **Python** y **Django Migrate** (Migración de Django).</span><span class="sxs-lookup"><span data-stu-id="a7636-132">In **Solution Explorer**, right-click on the project node and select **Python**, and then select **Django Migrate**.</span></span>  <span data-ttu-id="a7636-133">Después, seleccione **Django Create Superuser (Crear superusuario de Django)**.</span><span class="sxs-lookup"><span data-stu-id="a7636-133">Then select **Django Create Superuser**.</span></span>
6. <span data-ttu-id="a7636-134">Se abre la consola de administración de Django donde se va a crear una base de datos de sqlite en la carpeta del proyecto.</span><span class="sxs-lookup"><span data-stu-id="a7636-134">This will open a Django Management Console and create a sqlite database in the project folder.</span></span> <span data-ttu-id="a7636-135">Siga las indicaciones para crear un usuario.</span><span class="sxs-lookup"><span data-stu-id="a7636-135">Follow the prompts to create a user.</span></span>
7. <span data-ttu-id="a7636-136">Presione <kbd>F5</kbd> para confirmar que la aplicación funciona.</span><span class="sxs-lookup"><span data-stu-id="a7636-136">Confirm that the application works by pressing <kbd>F5</kbd>.</span></span>
8. <span data-ttu-id="a7636-137">Haga clic en **Iniciar sesión** en la barra de navegación de la parte superior.</span><span class="sxs-lookup"><span data-stu-id="a7636-137">Click **Log in** from the navigation bar at the top.</span></span>

     ![Explorador web](./media/web-sites-python-ptvs-django-sql/PollsDjangoCommonBrowserLocalMenu.png)
9. <span data-ttu-id="a7636-139">Escriba las credenciales del usuario que ha creado al sincronizar la base de datos.</span><span class="sxs-lookup"><span data-stu-id="a7636-139">Enter the credentials for the user you created when you synchronized the database.</span></span>

     ![Explorador web](./media/web-sites-python-ptvs-django-sql/PollsDjangoCommonBrowserLocalLogin.png)
10. <span data-ttu-id="a7636-141">Haga clic en **Create Sample Polls**(Crear sondeos de ejemplo).</span><span class="sxs-lookup"><span data-stu-id="a7636-141">Click **Create Sample Polls**.</span></span>

      ![Explorador web](./media/web-sites-python-ptvs-django-sql/PollsDjangoCommonBrowserNoPolls.png)
11. <span data-ttu-id="a7636-143">Haga clic en un sondeo y vote.</span><span class="sxs-lookup"><span data-stu-id="a7636-143">Click on a poll and vote.</span></span>

      ![Explorador web](./media/web-sites-python-ptvs-django-sql/PollsDjangoSqliteBrowser.png)

## <a name="create-a-sql-database"></a><span data-ttu-id="a7636-145">una Base de datos SQL</span><span class="sxs-lookup"><span data-stu-id="a7636-145">Create a SQL Database</span></span>
<span data-ttu-id="a7636-146">Para la base de datos, vamos a crear una base de datos SQL de Azure.</span><span class="sxs-lookup"><span data-stu-id="a7636-146">For the database, we'll create an Azure SQL database.</span></span>

<span data-ttu-id="a7636-147">Siga estos pasos para crear una base de datos.</span><span class="sxs-lookup"><span data-stu-id="a7636-147">You can create a database by following these steps.</span></span>

1. <span data-ttu-id="a7636-148">Inicie sesión en el [Portal de Azure].</span><span class="sxs-lookup"><span data-stu-id="a7636-148">Log into the [Azure Portal].</span></span>
2. <span data-ttu-id="a7636-149">En la parte inferior del panel de navegación, haga clic en **NUEVO**.</span><span class="sxs-lookup"><span data-stu-id="a7636-149">At the bottom of the navigation pane, click **NEW**.</span></span> <span data-ttu-id="a7636-150">A continuación, haga clic en **Datos y almacenamiento** > **SQL Database**.</span><span class="sxs-lookup"><span data-stu-id="a7636-150">, click **Data + Storage** > **SQL Database**.</span></span>
3. <span data-ttu-id="a7636-151">Configure la nueva Base de datos SQL mediante la creación de un nuevo grupo de recursos y seleccione la ubicación adecuada para él.</span><span class="sxs-lookup"><span data-stu-id="a7636-151">Configure the new SQL Database by creating a new resource group and select the appropriate location for it.</span></span>
4. <span data-ttu-id="a7636-152">Una vez creada la Base de datos SQL, haga clic en **Abrir en Visual Studio** en la hoja de la base de datos.</span><span class="sxs-lookup"><span data-stu-id="a7636-152">Once the SQL Database is created, click **Open in Visual Studio** in the database blade.</span></span>
5. <span data-ttu-id="a7636-153">Haga clic en **Configurar el firewall**.</span><span class="sxs-lookup"><span data-stu-id="a7636-153">Click **Configure your firewall**.</span></span>
6. <span data-ttu-id="a7636-154">En la hoja **Configuración de firewall**, agregue una regla de firewall con **IP INICIAL** e **IP FINAL** establecidos en la dirección IP pública de su equipo de desarrollo.</span><span class="sxs-lookup"><span data-stu-id="a7636-154">In the **Firewall Settings** blade, add a firewall rule with **START IP** and **END IP** set to the public IP address of your development machine.</span></span> <span data-ttu-id="a7636-155">Haga clic en **Save**.</span><span class="sxs-lookup"><span data-stu-id="a7636-155">Click **Save**.</span></span>

   <span data-ttu-id="a7636-156">De esta forma, se permitirán las conexiones al servidor de la base de datos desde el equipo de desarrollo.</span><span class="sxs-lookup"><span data-stu-id="a7636-156">This will allow connections to the database server from your development machine.</span></span>
7. <span data-ttu-id="a7636-157">De nuevo en la hoja de la base de datos, haga clic en **Propiedades** y en **Mostrar cadenas de conexión de la base de datos**.</span><span class="sxs-lookup"><span data-stu-id="a7636-157">Back in the database blade, click **Properties**, then click **Show database connection strings**.</span></span>
8. <span data-ttu-id="a7636-158">Use el botón Copiar para colocar el valor de **ADO.NET** en el Portapapeles.</span><span class="sxs-lookup"><span data-stu-id="a7636-158">Use the copy button to put the value of **ADO.NET** on the clipboard.</span></span>

## <a name="configure-the-project"></a><span data-ttu-id="a7636-159">Configuración del proyecto</span><span class="sxs-lookup"><span data-stu-id="a7636-159">Configure the Project</span></span>
<span data-ttu-id="a7636-160">En esta sección, vamos a configurar nuestra aplicación web para usar la base de datos SQL que acabamos de crear.</span><span class="sxs-lookup"><span data-stu-id="a7636-160">In this section, we'll configure our web app to use the SQL database we just created.</span></span> <span data-ttu-id="a7636-161">También vamos a instalar paquetes adicionales de Python necesarios para utilizar bases de datos SQL con Django.</span><span class="sxs-lookup"><span data-stu-id="a7636-161">We'll also install additional Python packages required to use SQL databases with Django.</span></span> <span data-ttu-id="a7636-162">A continuación, ejecutaremos la aplicación web localmente.</span><span class="sxs-lookup"><span data-stu-id="a7636-162">Then we'll run the web app locally.</span></span>

1. <span data-ttu-id="a7636-163">En Visual Studio, abra **settings.py**desde la carpeta *ProjectName* .</span><span class="sxs-lookup"><span data-stu-id="a7636-163">In Visual Studio, open **settings.py**, from the *ProjectName* folder.</span></span> <span data-ttu-id="a7636-164">Pegue temporalmente la cadena de conexión en el editor.</span><span class="sxs-lookup"><span data-stu-id="a7636-164">Temporarily paste the connection string in the editor.</span></span> <span data-ttu-id="a7636-165">La cadena de conexión tiene el siguiente formato:</span><span class="sxs-lookup"><span data-stu-id="a7636-165">The connection string is in this format:</span></span>

       Server=<ServerName>,<ServerPort>;Database=<DatabaseName>;User ID=<UserName>;Password={your_password_here};Encrypt=True;TrustServerCertificate=False;Connection Timeout=30;

<span data-ttu-id="a7636-166">Edite la definición de `DATABASES` para usar los valores anteriores.</span><span class="sxs-lookup"><span data-stu-id="a7636-166">Edit the definition of `DATABASES` to use the values above.</span></span>

        DATABASES = {
            'default': {
                'ENGINE': 'sql_server.pyodbc',
                'NAME': '<DatabaseName>',
                'USER': '<UserName>',
                'PASSWORD': '{your_password_here}',
                'HOST': '<ServerName>',
                'PORT': '<ServerPort>',
                'OPTIONS': {
                    'driver': 'SQL Server Native Client 11.0',
                    'MARS_Connection': 'True',
                }
            }
        }

1. <span data-ttu-id="a7636-167">En el Explorador de soluciones, en **Entornos de Python**, haga clic con el botón derecho en el entorno virtual y seleccione **Instalar paquete de Python**.</span><span class="sxs-lookup"><span data-stu-id="a7636-167">In Solution Explorer, under **Python Environments**, right-click on the virtual environment and select **Install Python Package**.</span></span>
2. <span data-ttu-id="a7636-168">Instale el paquete `pyodbc` con **pip**.</span><span class="sxs-lookup"><span data-stu-id="a7636-168">Install the package `pyodbc` using **pip**.</span></span>

     ![Cuadro de diálogo Instalar paquete de Python](./media/web-sites-python-ptvs-django-sql/PollsDjangoSqlInstallPackagePyodbc.png)
3. <span data-ttu-id="a7636-170">Instale el paquete `django-pyodbc-azure` con **pip**.</span><span class="sxs-lookup"><span data-stu-id="a7636-170">Install the package `django-pyodbc-azure` using **pip**.</span></span>

     ![Cuadro de diálogo Instalar paquete de Python](./media/web-sites-python-ptvs-django-sql/PollsDjangoSqlInstallPackageDjangoPyodbcAzure.png)
4. <span data-ttu-id="a7636-172">En el **Explorador de soluciones**, haga clic con el botón derecho en el nodo de proyecto, seleccione **Python** y **Django Migrate** (Migración de Django).</span><span class="sxs-lookup"><span data-stu-id="a7636-172">In **Solution Explorer**, right-click on the project node and select **Python**, and then select **Django Migrate**.</span></span>  <span data-ttu-id="a7636-173">Después, seleccione **Django Create Superuser (Crear superusuario de Django)**.</span><span class="sxs-lookup"><span data-stu-id="a7636-173">Then select **Django Create Superuser**.</span></span>

   <span data-ttu-id="a7636-174">De esta forma, se crearán las tablas para la base de datos SQL que hemos creado en la sección anterior.</span><span class="sxs-lookup"><span data-stu-id="a7636-174">This will create the tables for the SQL database we created in the previous section.</span></span> <span data-ttu-id="a7636-175">Siga las indicaciones para crear un usuario, que no tiene que coincidir con el usuario de la base de datos sqlite creada en la primera sección.</span><span class="sxs-lookup"><span data-stu-id="a7636-175">Follow the prompts to create a user, which doesn't have to match the user in the sqlite database created in the first section.</span></span>
5. <span data-ttu-id="a7636-176">Presione `F5`para ejecutar la aplicación.</span><span class="sxs-lookup"><span data-stu-id="a7636-176">Run the application with `F5`.</span></span> <span data-ttu-id="a7636-177">Los sondeos creados con **Create Sample Polls** (Crear sondeos de ejemplo) y los datos enviados al votar se serializarán en la base de datos SQL.</span><span class="sxs-lookup"><span data-stu-id="a7636-177">Polls that are created with **Create Sample Polls** and the data submitted by voting will be serialized in the SQL database.</span></span>

## <a name="publish-the-web-app-to-azure-app-service"></a><span data-ttu-id="a7636-178">Publicación de aplicación web del Servicio de aplicaciones de Azure</span><span class="sxs-lookup"><span data-stu-id="a7636-178">Publish the web app to Azure App Service</span></span>
<span data-ttu-id="a7636-179">El SDK de Azure .NET ofrece una forma fácil de implementar la aplicación web en Aplicaciones web del Servicio de aplicaciones de Azure.</span><span class="sxs-lookup"><span data-stu-id="a7636-179">The Azure .NET SDK provides an easy way to deploy your web web app to Azure App Service Web Apps.</span></span>

1. <span data-ttu-id="a7636-180">En el **Explorador de soluciones**, haga clic con el botón derecho en el nodo del proyecto y seleccione **Publicar**.</span><span class="sxs-lookup"><span data-stu-id="a7636-180">In **Solution Explorer**, right-click on the project node and select **Publish**.</span></span>

     ![Cuadro de diálogo Publicación web](./media/web-sites-python-ptvs-django-sql/PollsCommonPublishWebSiteDialog.png)
2. <span data-ttu-id="a7636-182">Haga clic en **Aplicaciones web de Microsoft Azure**.</span><span class="sxs-lookup"><span data-stu-id="a7636-182">Click on **Microsoft Azure Web Apps**.</span></span>
3. <span data-ttu-id="a7636-183">Haga clic en **Nuevo** para crear una aplicación web nueva.</span><span class="sxs-lookup"><span data-stu-id="a7636-183">Click on **New** to create a new web app.</span></span>
4. <span data-ttu-id="a7636-184">Rellene los campos siguientes y haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="a7636-184">Fill in the following fields and click **Create**.</span></span>

   * <span data-ttu-id="a7636-185">**Nombre de aplicación web**</span><span class="sxs-lookup"><span data-stu-id="a7636-185">**Web App name**</span></span>
   * <span data-ttu-id="a7636-186">**Plan del Servicio de aplicaciones**</span><span class="sxs-lookup"><span data-stu-id="a7636-186">**App Service plan**</span></span>
   * <span data-ttu-id="a7636-187">**Grupos de recursos**</span><span class="sxs-lookup"><span data-stu-id="a7636-187">**Resource group**</span></span>
   * <span data-ttu-id="a7636-188">**Región**</span><span class="sxs-lookup"><span data-stu-id="a7636-188">**Region**</span></span>
   * <span data-ttu-id="a7636-189">Deje **Servidor de base de datos** establecido en **No hay base de datos**</span><span class="sxs-lookup"><span data-stu-id="a7636-189">Leave **Database server** set to **No database**</span></span>
5. <span data-ttu-id="a7636-190">Acepte todos los valores predeterminados y haga clic en **Publicar**.</span><span class="sxs-lookup"><span data-stu-id="a7636-190">Accept all other defaults and click **Publish**.</span></span>
6. <span data-ttu-id="a7636-191">El explorador web se abrirá automáticamente en la aplicación web publicada.</span><span class="sxs-lookup"><span data-stu-id="a7636-191">Your web browser will open automatically to the published web app.</span></span> <span data-ttu-id="a7636-192">La aplicación web ahora debe funcionar según lo previsto, con el uso de la base de datos **SQL** hospedada en Azure.</span><span class="sxs-lookup"><span data-stu-id="a7636-192">You should see the web app working as expected, using the **SQL** database hosted on Azure.</span></span>

   <span data-ttu-id="a7636-193">¡Enhorabuena!</span><span class="sxs-lookup"><span data-stu-id="a7636-193">Congratulations!</span></span>

     ![Explorador web](./media/web-sites-python-ptvs-django-sql/PollsDjangoAzureBrowser.png)

## <a name="next-steps"></a><span data-ttu-id="a7636-195">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="a7636-195">Next steps</span></span>
<span data-ttu-id="a7636-196">Siga estos vínculos para obtener más información sobre las herramientas de Python para Visual Studio, Django y Base de datos SQL.</span><span class="sxs-lookup"><span data-stu-id="a7636-196">Follow these links to learn more about Python Tools for Visual Studio, Django and SQL Database.</span></span>

* <span data-ttu-id="a7636-197">[Documentación sobre Python Tools para Visual Studio]</span><span class="sxs-lookup"><span data-stu-id="a7636-197">[Python Tools for Visual Studio Documentation]</span></span>
  * <span data-ttu-id="a7636-198">[Proyectos web]</span><span class="sxs-lookup"><span data-stu-id="a7636-198">[Web Projects]</span></span>
  * <span data-ttu-id="a7636-199">[Proyectos de servicio en la nube]</span><span class="sxs-lookup"><span data-stu-id="a7636-199">[Cloud Service Projects]</span></span>
  * <span data-ttu-id="a7636-200">[Depuración remota en Microsoft Azure]</span><span class="sxs-lookup"><span data-stu-id="a7636-200">[Remote Debugging on Microsoft Azure]</span></span>
* <span data-ttu-id="a7636-201">[Documentación de Django]</span><span class="sxs-lookup"><span data-stu-id="a7636-201">[Django Documentation]</span></span>
* <span data-ttu-id="a7636-202">[Base de datos SQL]</span><span class="sxs-lookup"><span data-stu-id="a7636-202">[SQL Database]</span></span>

## <a name="whats-changed"></a><span data-ttu-id="a7636-203">Lo que ha cambiado</span><span class="sxs-lookup"><span data-stu-id="a7636-203">What's changed</span></span>
* <span data-ttu-id="a7636-204">Para obtener una guía del cambio de Sitios web a Servicio de aplicaciones, consulte: [Servicio de aplicaciones de Azure y su impacto en los servicios de Azure existentes](http://go.microsoft.com/fwlink/?LinkId=529714)</span><span class="sxs-lookup"><span data-stu-id="a7636-204">For a guide to the change from Websites to App Service see: [Azure App Service and Its Impact on Existing Azure Services](http://go.microsoft.com/fwlink/?LinkId=529714)</span></span>

<!--Link references-->
<span data-ttu-id="a7636-205">[Centro para desarrolladores de Python]: /develop/python/</span><span class="sxs-lookup"><span data-stu-id="a7636-205">[Python Developer Center]: /develop/python/</span></span>
<span data-ttu-id="a7636-206">[Servicios en la nube de Azure]: ../cloud-services/cloud-services-python-ptvs.md</span><span class="sxs-lookup"><span data-stu-id="a7636-206">[Azure Cloud Services]: ../cloud-services/cloud-services-python-ptvs.md</span></span>

<!--External Link references-->
<span data-ttu-id="a7636-207">[Portal de Azure]: https://portal.azure.com</span><span class="sxs-lookup"><span data-stu-id="a7636-207">[Azure Portal]: https://portal.azure.com</span></span>
<span data-ttu-id="a7636-208">[Herramientas de Python para Visual Studio]: http://aka.ms/ptvs</span><span class="sxs-lookup"><span data-stu-id="a7636-208">[Python Tools for Visual Studio]: http://aka.ms/ptvs</span></span>
<span data-ttu-id="a7636-209">[Python Tools 2.2 para Visual Studio]: http://go.microsoft.com/fwlink/?LinkID=624025</span><span class="sxs-lookup"><span data-stu-id="a7636-209">[Python Tools 2.2 for Visual Studio]: http://go.microsoft.com/fwlink/?LinkID=624025</span></span>
<span data-ttu-id="a7636-210">[archivos VSIX de ejemplo de Python Tools 2.2 para Visual Studio]: http://go.microsoft.com/fwlink/?LinkID=624025</span><span class="sxs-lookup"><span data-stu-id="a7636-210">[Python Tools 2.2 for Visual Studio Samples VSIX]: http://go.microsoft.com/fwlink/?LinkID=624025</span></span>
<span data-ttu-id="a7636-211">[Azure SDK y herramientas para VS 2015]: http://go.microsoft.com/fwlink/?LinkId=518003</span><span class="sxs-lookup"><span data-stu-id="a7636-211">[Azure SDK Tools for VS 2015]: http://go.microsoft.com/fwlink/?LinkId=518003</span></span>
<span data-ttu-id="a7636-212">[Python 2.7 de 32 bits]: http://go.microsoft.com/fwlink/?LinkId=517190</span><span class="sxs-lookup"><span data-stu-id="a7636-212">[Python 2.7 32-bit]: http://go.microsoft.com/fwlink/?LinkId=517190</span></span>
<span data-ttu-id="a7636-213">[Documentación sobre Python Tools para Visual Studio]: http://aka.ms/ptvsdocs</span><span class="sxs-lookup"><span data-stu-id="a7636-213">[Python Tools for Visual Studio Documentation]: http://aka.ms/ptvsdocs</span></span>
<span data-ttu-id="a7636-214">[Depuración remota en Microsoft Azure]: http://go.microsoft.com/fwlink/?LinkId=624026</span><span class="sxs-lookup"><span data-stu-id="a7636-214">[Remote Debugging on Microsoft Azure]: http://go.microsoft.com/fwlink/?LinkId=624026</span></span>
<span data-ttu-id="a7636-215">[Proyectos web]: http://go.microsoft.com/fwlink/?LinkId=624027</span><span class="sxs-lookup"><span data-stu-id="a7636-215">[Web Projects]: http://go.microsoft.com/fwlink/?LinkId=624027</span></span>
<span data-ttu-id="a7636-216">[Proyectos de servicio en la nube]: http://go.microsoft.com/fwlink/?LinkId=624028</span><span class="sxs-lookup"><span data-stu-id="a7636-216">[Cloud Service Projects]: http://go.microsoft.com/fwlink/?LinkId=624028</span></span>
<span data-ttu-id="a7636-217">[Documentación de Django]: https://www.djangoproject.com/</span><span class="sxs-lookup"><span data-stu-id="a7636-217">[Django Documentation]: https://www.djangoproject.com/</span></span>
<span data-ttu-id="a7636-218">[Base de datos SQL]: /documentation/services/sql-database/</span><span class="sxs-lookup"><span data-stu-id="a7636-218">[SQL Database]: /documentation/services/sql-database/</span></span>
