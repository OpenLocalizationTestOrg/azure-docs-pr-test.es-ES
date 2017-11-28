---
title: aaaDjango y base de datos de SQL en Azure con Python Tools 2.2 para Visual Studio
description: "Obtenga información acerca de cómo toouse Hola Python Tools para Visual Studio toocreate una aplicación web Django que almacena datos en una instancia de base de datos SQL e impleméntela tooAzure aplicación del servicio Web de aplicaciones."
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
ms.openlocfilehash: b5b2ef4f3292e7df85007465c5394c8660a7d231
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="django-and-sql-database-on-azure-with-python-tools-22-for-visual-studio"></a><span data-ttu-id="d4b3a-103">Django y Base de datos SQL en Azure con Python Tools 2.2 para Visual Studio</span><span class="sxs-lookup"><span data-stu-id="d4b3a-103">Django and SQL Database on Azure with Python Tools 2.2 for Visual Studio</span></span>
<span data-ttu-id="d4b3a-104">En este tutorial, usaremos [Python Tools para Visual Studio] sondea de toocreate una sencilla aplicación web con una de las plantillas de ejemplo de Hola PTVS.</span><span class="sxs-lookup"><span data-stu-id="d4b3a-104">In this tutorial, we'll use [Python Tools for Visual Studio] toocreate a simple polls web app using one of hello PTVS sample templates.</span></span> <span data-ttu-id="d4b3a-105">Este tutorial también se encuentra disponible como [vídeo](https://www.youtube.com/watch?v=ZwcoGcIeHF4).</span><span class="sxs-lookup"><span data-stu-id="d4b3a-105">This tutorial is also available as a [video](https://www.youtube.com/watch?v=ZwcoGcIeHF4).</span></span>

<span data-ttu-id="d4b3a-106">Obtendrá información sobre cómo toouse una base de datos SQL hospeda en Azure, cómo tooconfigure Hola toouse de aplicación web a una base de datos SQL y cómo toopublish Hola aplicación web demasiado[aplicaciones de Web del servicio de aplicación de Azure](http://go.microsoft.com/fwlink/?LinkId=529714).</span><span class="sxs-lookup"><span data-stu-id="d4b3a-106">We'll learn how toouse a SQL database hosted on Azure, how tooconfigure hello web app toouse a SQL database, and how toopublish hello web app too[Azure App Service Web Apps](http://go.microsoft.com/fwlink/?LinkId=529714).</span></span>

<span data-ttu-id="d4b3a-107">Vea hello [Centro para desarrolladores de Python] para ver más artículos que cubren el desarrollo de aplicaciones de Web del servicio de aplicación de Azure con PTVS mediante Bottle por sí solo, matraz y Django web marcos de trabajo, con los servicios de almacenamiento de tabla de Azure, MySQL y base de datos SQL.</span><span class="sxs-lookup"><span data-stu-id="d4b3a-107">See hello [Python Developer Center] for more articles that cover development of Azure App Service Web Apps with PTVS using Bottle, Flask and Django web frameworks, with Azure Table Storage, MySQL and SQL Database services.</span></span> <span data-ttu-id="d4b3a-108">Aunque en este artículo se centra en el servicio de aplicaciones, los pasos de hello son similares al desarrollar [servicios en la nube].</span><span class="sxs-lookup"><span data-stu-id="d4b3a-108">While this article focuses on App Service, hello steps are similar when developing [Azure Cloud Services].</span></span>

## <a name="prerequisites"></a><span data-ttu-id="d4b3a-109">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="d4b3a-109">Prerequisites</span></span>
* <span data-ttu-id="d4b3a-110">Visual Studio 2015</span><span class="sxs-lookup"><span data-stu-id="d4b3a-110">Visual Studio 2015</span></span>
* <span data-ttu-id="d4b3a-111">[Python 2.7 de 32 bits]</span><span class="sxs-lookup"><span data-stu-id="d4b3a-111">[Python 2.7 32-bit]</span></span>
* <span data-ttu-id="d4b3a-112">[Python Tools 2.2 para Visual Studio]</span><span class="sxs-lookup"><span data-stu-id="d4b3a-112">[Python Tools 2.2 for Visual Studio]</span></span>
* <span data-ttu-id="d4b3a-113">[Python Tools 2.2 para Visual Studio ejemplos VSIX]</span><span class="sxs-lookup"><span data-stu-id="d4b3a-113">[Python Tools 2.2 for Visual Studio Samples VSIX]</span></span>
* <span data-ttu-id="d4b3a-114">[Azure SDK y herramientas para VS 2015]</span><span class="sxs-lookup"><span data-stu-id="d4b3a-114">[Azure SDK Tools for VS 2015]</span></span>
* <span data-ttu-id="d4b3a-115">Django 1.9 o posterior</span><span class="sxs-lookup"><span data-stu-id="d4b3a-115">Django 1.9 or later</span></span>

[!INCLUDE [create-account-and-websites-note](../../includes/create-account-and-websites-note.md)]

> [!NOTE]
> <span data-ttu-id="d4b3a-116">Si desea tooget iniciado con el servicio de aplicación de Azure antes de registrarse para una cuenta de Azure, vaya demasiado[pruebe el servicio de aplicaciones](https://azure.microsoft.com/try/app-service/), donde puede crear inmediatamente una aplicación web de inicio de corta duración en el servicio de aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="d4b3a-116">If you want tooget started with Azure App Service before signing up for an Azure account, go too[Try App Service](https://azure.microsoft.com/try/app-service/), where you can immediately create a short-lived starter web app in App Service.</span></span> <span data-ttu-id="d4b3a-117">No es necesario proporcionar ninguna tarjeta de crédito ni asumir ningún compromiso.</span><span class="sxs-lookup"><span data-stu-id="d4b3a-117">No credit cards required; no commitments.</span></span>
>
>

## <a name="create-hello-project"></a><span data-ttu-id="d4b3a-118">Crear proyecto de hello</span><span class="sxs-lookup"><span data-stu-id="d4b3a-118">Create hello Project</span></span>
<span data-ttu-id="d4b3a-119">En esta sección, vamos a crear un proyecto de Visual Studio con la utilización de una plantilla de ejemplo.</span><span class="sxs-lookup"><span data-stu-id="d4b3a-119">In this section, we'll create a Visual Studio project using a sample template.</span></span> <span data-ttu-id="d4b3a-120">Vamos a crear un entorno virtual e instalar los paquetes necesarios.</span><span class="sxs-lookup"><span data-stu-id="d4b3a-120">We'll create a virtual environment and install required packages.</span></span> <span data-ttu-id="d4b3a-121">Vamos a crear una base de datos local con sqlite.</span><span class="sxs-lookup"><span data-stu-id="d4b3a-121">We'll create a local database using sqlite.</span></span> <span data-ttu-id="d4b3a-122">A continuación, ejecutaremos aplicación web de hello localmente.</span><span class="sxs-lookup"><span data-stu-id="d4b3a-122">Then we'll run hello web app locally.</span></span>

1. <span data-ttu-id="d4b3a-123">En Visual Studio, seleccione **Archivo**, **Nuevo proyecto**.</span><span class="sxs-lookup"><span data-stu-id="d4b3a-123">In Visual Studio, select **File**, **New Project**.</span></span>
2. <span data-ttu-id="d4b3a-124">Hola plantillas de proyecto de hello [Python Tools 2.2 para Visual Studio ejemplos VSIX] están disponibles en **Python**, **ejemplos**.</span><span class="sxs-lookup"><span data-stu-id="d4b3a-124">hello project templates from hello [Python Tools 2.2 for Visual Studio Samples VSIX] are available under **Python**, **Samples**.</span></span> <span data-ttu-id="d4b3a-125">Seleccione **proyecto Web de sondeos Django** y haga clic en Aceptar toocreate Hola proyecto.</span><span class="sxs-lookup"><span data-stu-id="d4b3a-125">Select **Polls Django Web Project** and click OK toocreate hello project.</span></span>

     ![Cuadro de diálogo Nuevo proyecto](./media/web-sites-python-ptvs-django-sql/PollsDjangoNewProject.png)
3. <span data-ttu-id="d4b3a-127">Es posible que los paquetes externos tooinstall solicitadas.</span><span class="sxs-lookup"><span data-stu-id="d4b3a-127">You will be prompted tooinstall external packages.</span></span> <span data-ttu-id="d4b3a-128">Seleccione **Instalar en un entorno virtual**.</span><span class="sxs-lookup"><span data-stu-id="d4b3a-128">Select **Install into a virtual environment**.</span></span>

     ![Cuadro de diálogo Paquetes externos](./media/web-sites-python-ptvs-django-sql/PollsDjangoExternalPackages.png)
4. <span data-ttu-id="d4b3a-130">Seleccione **Python 2.7** como intérprete base Hola.</span><span class="sxs-lookup"><span data-stu-id="d4b3a-130">Select **Python 2.7** as hello base interpreter.</span></span>

     ![Cuadro de diálogo Agregar entorno virtual](./media/web-sites-python-ptvs-django-sql/PollsCommonAddVirtualEnv.png)
5. <span data-ttu-id="d4b3a-132">En **el Explorador de soluciones**, haga doble clic en el nodo del proyecto de Hola y seleccione **Python**y, a continuación, seleccione **Django migrar**.</span><span class="sxs-lookup"><span data-stu-id="d4b3a-132">In **Solution Explorer**, right-click on hello project node and select **Python**, and then select **Django Migrate**.</span></span>  <span data-ttu-id="d4b3a-133">Después, seleccione **Django Create Superuser (Crear superusuario de Django)**.</span><span class="sxs-lookup"><span data-stu-id="d4b3a-133">Then select **Django Create Superuser**.</span></span>
6. <span data-ttu-id="d4b3a-134">Se abrirá una consola de administración de Django y crear una base de datos de sqlite en la carpeta del proyecto Hola.</span><span class="sxs-lookup"><span data-stu-id="d4b3a-134">This will open a Django Management Console and create a sqlite database in hello project folder.</span></span> <span data-ttu-id="d4b3a-135">Siga los mensajes de Hola toocreate un usuario.</span><span class="sxs-lookup"><span data-stu-id="d4b3a-135">Follow hello prompts toocreate a user.</span></span>
7. <span data-ttu-id="d4b3a-136">Confirme que la aplicación hello funciona presionando <kbd>F5</kbd>.</span><span class="sxs-lookup"><span data-stu-id="d4b3a-136">Confirm that hello application works by pressing <kbd>F5</kbd>.</span></span>
8. <span data-ttu-id="d4b3a-137">Haga clic en **sesión** de barra de navegación superior de Hola Hola.</span><span class="sxs-lookup"><span data-stu-id="d4b3a-137">Click **Log in** from hello navigation bar at hello top.</span></span>

     ![Explorador web](./media/web-sites-python-ptvs-django-sql/PollsDjangoCommonBrowserLocalMenu.png)
9. <span data-ttu-id="d4b3a-139">Escriba las credenciales de hello para el usuario de Hola que creó al sincronizar base de datos de Hola.</span><span class="sxs-lookup"><span data-stu-id="d4b3a-139">Enter hello credentials for hello user you created when you synchronized hello database.</span></span>

     ![Explorador web](./media/web-sites-python-ptvs-django-sql/PollsDjangoCommonBrowserLocalLogin.png)
10. <span data-ttu-id="d4b3a-141">Haga clic en **Create Sample Polls**(Crear sondeos de ejemplo).</span><span class="sxs-lookup"><span data-stu-id="d4b3a-141">Click **Create Sample Polls**.</span></span>

      ![Explorador web](./media/web-sites-python-ptvs-django-sql/PollsDjangoCommonBrowserNoPolls.png)
11. <span data-ttu-id="d4b3a-143">Haga clic en un sondeo y vote.</span><span class="sxs-lookup"><span data-stu-id="d4b3a-143">Click on a poll and vote.</span></span>

      ![Explorador web](./media/web-sites-python-ptvs-django-sql/PollsDjangoSqliteBrowser.png)

## <a name="create-a-sql-database"></a><span data-ttu-id="d4b3a-145">una Base de datos SQL</span><span class="sxs-lookup"><span data-stu-id="d4b3a-145">Create a SQL Database</span></span>
<span data-ttu-id="d4b3a-146">Para la base de datos de hello, vamos a crear una base de datos de SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="d4b3a-146">For hello database, we'll create an Azure SQL database.</span></span>

<span data-ttu-id="d4b3a-147">Siga estos pasos para crear una base de datos.</span><span class="sxs-lookup"><span data-stu-id="d4b3a-147">You can create a database by following these steps.</span></span>

1. <span data-ttu-id="d4b3a-148">Inicie sesión en hello [Portal de Azure].</span><span class="sxs-lookup"><span data-stu-id="d4b3a-148">Log into hello [Azure Portal].</span></span>
2. <span data-ttu-id="d4b3a-149">En la parte inferior de hello del panel de navegación de hello, haga clic en **nuevo**.</span><span class="sxs-lookup"><span data-stu-id="d4b3a-149">At hello bottom of hello navigation pane, click **NEW**.</span></span> <span data-ttu-id="d4b3a-150">A continuación, haga clic en **Datos y almacenamiento** > **SQL Database**.</span><span class="sxs-lookup"><span data-stu-id="d4b3a-150">, click **Data + Storage** > **SQL Database**.</span></span>
3. <span data-ttu-id="d4b3a-151">Configurar Hola nueva base de datos de SQL mediante la creación de un nuevo grupo de recursos y seleccione Hola ubicación adecuada para él.</span><span class="sxs-lookup"><span data-stu-id="d4b3a-151">Configure hello new SQL Database by creating a new resource group and select hello appropriate location for it.</span></span>
4. <span data-ttu-id="d4b3a-152">Una vez creada la base de datos SQL de hello, haga clic en **abierta en Visual Studio** en la hoja de la base de datos de Hola.</span><span class="sxs-lookup"><span data-stu-id="d4b3a-152">Once hello SQL Database is created, click **Open in Visual Studio** in hello database blade.</span></span>
5. <span data-ttu-id="d4b3a-153">Haga clic en **Configurar el firewall**.</span><span class="sxs-lookup"><span data-stu-id="d4b3a-153">Click **Configure your firewall**.</span></span>
6. <span data-ttu-id="d4b3a-154">Hola **configuración de Firewall** hoja, agregar una regla de firewall con **IP inicial** y **IP final** establecer toohello de dirección IP pública de su equipo de desarrollo.</span><span class="sxs-lookup"><span data-stu-id="d4b3a-154">In hello **Firewall Settings** blade, add a firewall rule with **START IP** and **END IP** set toohello public IP address of your development machine.</span></span> <span data-ttu-id="d4b3a-155">Haga clic en **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="d4b3a-155">Click **Save**.</span></span>

   <span data-ttu-id="d4b3a-156">Esto permitirá que el servidor de base de datos de toohello de las conexiones desde el equipo de desarrollo.</span><span class="sxs-lookup"><span data-stu-id="d4b3a-156">This will allow connections toohello database server from your development machine.</span></span>
7. <span data-ttu-id="d4b3a-157">En la hoja de la base de datos de hello, haga clic en **propiedades**, a continuación, haga clic en **mostrar cadenas de conexión de base de datos**.</span><span class="sxs-lookup"><span data-stu-id="d4b3a-157">Back in hello database blade, click **Properties**, then click **Show database connection strings**.</span></span>
8. <span data-ttu-id="d4b3a-158">Usar valor Hola copia botón tooput Hola de **ADO.NET** en Portapapeles Hola.</span><span class="sxs-lookup"><span data-stu-id="d4b3a-158">Use hello copy button tooput hello value of **ADO.NET** on hello clipboard.</span></span>

## <a name="configure-hello-project"></a><span data-ttu-id="d4b3a-159">Configurar proyecto Hola</span><span class="sxs-lookup"><span data-stu-id="d4b3a-159">Configure hello Project</span></span>
<span data-ttu-id="d4b3a-160">En esta sección, vamos a configurar nuestro web app toouse Hola base de datos SQL que acabamos de crear.</span><span class="sxs-lookup"><span data-stu-id="d4b3a-160">In this section, we'll configure our web app toouse hello SQL database we just created.</span></span> <span data-ttu-id="d4b3a-161">También vamos a instalar bases de datos SQL de toouse necesarios adicionales paquetes de Python con Django.</span><span class="sxs-lookup"><span data-stu-id="d4b3a-161">We'll also install additional Python packages required toouse SQL databases with Django.</span></span> <span data-ttu-id="d4b3a-162">A continuación, ejecutaremos aplicación web de hello localmente.</span><span class="sxs-lookup"><span data-stu-id="d4b3a-162">Then we'll run hello web app locally.</span></span>

1. <span data-ttu-id="d4b3a-163">En Visual Studio, abra **settings.py**, de hello *ProjectName* carpeta.</span><span class="sxs-lookup"><span data-stu-id="d4b3a-163">In Visual Studio, open **settings.py**, from hello *ProjectName* folder.</span></span> <span data-ttu-id="d4b3a-164">Pegue temporalmente cadena de conexión de hello en el editor de Hola.</span><span class="sxs-lookup"><span data-stu-id="d4b3a-164">Temporarily paste hello connection string in hello editor.</span></span> <span data-ttu-id="d4b3a-165">cadena de conexión de Hello tiene este formato:</span><span class="sxs-lookup"><span data-stu-id="d4b3a-165">hello connection string is in this format:</span></span>

       Server=<ServerName>,<ServerPort>;Database=<DatabaseName>;User ID=<UserName>;Password={your_password_here};Encrypt=True;TrustServerCertificate=False;Connection Timeout=30;

<span data-ttu-id="d4b3a-166">Editar definición de Hola de `DATABASES` valores de hello toouse indicados anteriormente.</span><span class="sxs-lookup"><span data-stu-id="d4b3a-166">Edit hello definition of `DATABASES` toouse hello values above.</span></span>

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

1. <span data-ttu-id="d4b3a-167">En el Explorador de soluciones, bajo **entornos de Python**, haga doble clic en el entorno virtual de Hola y seleccione **instalar un paquete de Python**.</span><span class="sxs-lookup"><span data-stu-id="d4b3a-167">In Solution Explorer, under **Python Environments**, right-click on hello virtual environment and select **Install Python Package**.</span></span>
2. <span data-ttu-id="d4b3a-168">Instalar el paquete de hello `pyodbc` con **pip**.</span><span class="sxs-lookup"><span data-stu-id="d4b3a-168">Install hello package `pyodbc` using **pip**.</span></span>

     ![Cuadro de diálogo Instalar paquete de Python](./media/web-sites-python-ptvs-django-sql/PollsDjangoSqlInstallPackagePyodbc.png)
3. <span data-ttu-id="d4b3a-170">Instalar el paquete de hello `django-pyodbc-azure` con **pip**.</span><span class="sxs-lookup"><span data-stu-id="d4b3a-170">Install hello package `django-pyodbc-azure` using **pip**.</span></span>

     ![Cuadro de diálogo Instalar paquete de Python](./media/web-sites-python-ptvs-django-sql/PollsDjangoSqlInstallPackageDjangoPyodbcAzure.png)
4. <span data-ttu-id="d4b3a-172">En **el Explorador de soluciones**, haga doble clic en el nodo del proyecto de Hola y seleccione **Python**y, a continuación, seleccione **Django migrar**.</span><span class="sxs-lookup"><span data-stu-id="d4b3a-172">In **Solution Explorer**, right-click on hello project node and select **Python**, and then select **Django Migrate**.</span></span>  <span data-ttu-id="d4b3a-173">Después, seleccione **Django Create Superuser (Crear superusuario de Django)**.</span><span class="sxs-lookup"><span data-stu-id="d4b3a-173">Then select **Django Create Superuser**.</span></span>

   <span data-ttu-id="d4b3a-174">Esto creará tablas de Hola para base de datos SQL de hello que hemos creado en la sección anterior de Hola.</span><span class="sxs-lookup"><span data-stu-id="d4b3a-174">This will create hello tables for hello SQL database we created in hello previous section.</span></span> <span data-ttu-id="d4b3a-175">Siga los mensajes de Hola toocreate un usuario, que no tiene el usuario de hello toomatch en base de datos de sqlite de hello creado en la primera sección de Hola.</span><span class="sxs-lookup"><span data-stu-id="d4b3a-175">Follow hello prompts toocreate a user, which doesn't have toomatch hello user in hello sqlite database created in hello first section.</span></span>
5. <span data-ttu-id="d4b3a-176">Ejecutar la aplicación hello con `F5`.</span><span class="sxs-lookup"><span data-stu-id="d4b3a-176">Run hello application with `F5`.</span></span> <span data-ttu-id="d4b3a-177">Sondeos que se crean con **crear sondeos de ejemplo** y se van a serializar datos Hola enviados votando en la base de datos SQL de Hola.</span><span class="sxs-lookup"><span data-stu-id="d4b3a-177">Polls that are created with **Create Sample Polls** and hello data submitted by voting will be serialized in hello SQL database.</span></span>

## <a name="publish-hello-web-app-tooazure-app-service"></a><span data-ttu-id="d4b3a-178">Publicar hello web app tooAzure servicio de aplicaciones</span><span class="sxs-lookup"><span data-stu-id="d4b3a-178">Publish hello web app tooAzure App Service</span></span>
<span data-ttu-id="d4b3a-179">Hello Azure SDK para .NET proporciona un toodeploy fácilmente su tooAzure de aplicación web de web aplicación del servicio de aplicaciones Web.</span><span class="sxs-lookup"><span data-stu-id="d4b3a-179">hello Azure .NET SDK provides an easy way toodeploy your web web app tooAzure App Service Web Apps.</span></span>

1. <span data-ttu-id="d4b3a-180">En **el Explorador de soluciones**, haga doble clic en el nodo del proyecto de Hola y seleccione **publicar**.</span><span class="sxs-lookup"><span data-stu-id="d4b3a-180">In **Solution Explorer**, right-click on hello project node and select **Publish**.</span></span>

     ![Cuadro de diálogo Publicación web](./media/web-sites-python-ptvs-django-sql/PollsCommonPublishWebSiteDialog.png)
2. <span data-ttu-id="d4b3a-182">Haga clic en **Aplicaciones web de Microsoft Azure**.</span><span class="sxs-lookup"><span data-stu-id="d4b3a-182">Click on **Microsoft Azure Web Apps**.</span></span>
3. <span data-ttu-id="d4b3a-183">Haga clic en **New** toocreate una nueva aplicación web.</span><span class="sxs-lookup"><span data-stu-id="d4b3a-183">Click on **New** toocreate a new web app.</span></span>
4. <span data-ttu-id="d4b3a-184">Rellene Hola después de campos y haga clic en **crear**.</span><span class="sxs-lookup"><span data-stu-id="d4b3a-184">Fill in hello following fields and click **Create**.</span></span>

   * <span data-ttu-id="d4b3a-185">**Nombre de aplicación web**</span><span class="sxs-lookup"><span data-stu-id="d4b3a-185">**Web App name**</span></span>
   * <span data-ttu-id="d4b3a-186">**Plan del Servicio de aplicaciones**</span><span class="sxs-lookup"><span data-stu-id="d4b3a-186">**App Service plan**</span></span>
   * <span data-ttu-id="d4b3a-187">**Grupos de recursos**</span><span class="sxs-lookup"><span data-stu-id="d4b3a-187">**Resource group**</span></span>
   * <span data-ttu-id="d4b3a-188">**Región**</span><span class="sxs-lookup"><span data-stu-id="d4b3a-188">**Region**</span></span>
   * <span data-ttu-id="d4b3a-189">Deje **servidor de base de datos** establecido demasiado**ninguna base de datos**</span><span class="sxs-lookup"><span data-stu-id="d4b3a-189">Leave **Database server** set too**No database**</span></span>
5. <span data-ttu-id="d4b3a-190">Acepte todos los valores predeterminados y haga clic en **Publicar**.</span><span class="sxs-lookup"><span data-stu-id="d4b3a-190">Accept all other defaults and click **Publish**.</span></span>
6. <span data-ttu-id="d4b3a-191">El explorador web abrirá automáticamente aplicaciones web publicadas de toohello.</span><span class="sxs-lookup"><span data-stu-id="d4b3a-191">Your web browser will open automatically toohello published web app.</span></span> <span data-ttu-id="d4b3a-192">Debería ver el trabajo de aplicación web de hello según lo esperado, con hello **SQL** base de datos hospedada en Azure.</span><span class="sxs-lookup"><span data-stu-id="d4b3a-192">You should see hello web app working as expected, using hello **SQL** database hosted on Azure.</span></span>

   <span data-ttu-id="d4b3a-193">¡Enhorabuena!</span><span class="sxs-lookup"><span data-stu-id="d4b3a-193">Congratulations!</span></span>

     ![Explorador web](./media/web-sites-python-ptvs-django-sql/PollsDjangoAzureBrowser.png)

## <a name="next-steps"></a><span data-ttu-id="d4b3a-195">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="d4b3a-195">Next steps</span></span>
<span data-ttu-id="d4b3a-196">Siga estos toolearn de vínculos más información acerca de Python Tools para Visual Studio, Django y base de datos SQL.</span><span class="sxs-lookup"><span data-stu-id="d4b3a-196">Follow these links toolearn more about Python Tools for Visual Studio, Django and SQL Database.</span></span>

* <span data-ttu-id="d4b3a-197">[Documentación sobre Python Tools para Visual Studio]</span><span class="sxs-lookup"><span data-stu-id="d4b3a-197">[Python Tools for Visual Studio Documentation]</span></span>
  * <span data-ttu-id="d4b3a-198">[Proyectos web]</span><span class="sxs-lookup"><span data-stu-id="d4b3a-198">[Web Projects]</span></span>
  * <span data-ttu-id="d4b3a-199">[Proyectos de servicio en la nube]</span><span class="sxs-lookup"><span data-stu-id="d4b3a-199">[Cloud Service Projects]</span></span>
  * <span data-ttu-id="d4b3a-200">[Depuración remota en Microsoft Azure]</span><span class="sxs-lookup"><span data-stu-id="d4b3a-200">[Remote Debugging on Microsoft Azure]</span></span>
* <span data-ttu-id="d4b3a-201">[Documentación de Django]</span><span class="sxs-lookup"><span data-stu-id="d4b3a-201">[Django Documentation]</span></span>
* <span data-ttu-id="d4b3a-202">[Base de datos SQL]</span><span class="sxs-lookup"><span data-stu-id="d4b3a-202">[SQL Database]</span></span>

## <a name="whats-changed"></a><span data-ttu-id="d4b3a-203">Lo que ha cambiado</span><span class="sxs-lookup"><span data-stu-id="d4b3a-203">What's changed</span></span>
* <span data-ttu-id="d4b3a-204">Para una toohello guía consulte cambio con respecto a sitios Web tooApp servicio: [servicio de aplicaciones de Azure y su impacto en los servicios de Azure existente](http://go.microsoft.com/fwlink/?LinkId=529714)</span><span class="sxs-lookup"><span data-stu-id="d4b3a-204">For a guide toohello change from Websites tooApp Service see: [Azure App Service and Its Impact on Existing Azure Services](http://go.microsoft.com/fwlink/?LinkId=529714)</span></span>

<!--Link references-->
[Centro para desarrolladores de Python]: /develop/python/
[servicios en la nube]: ../cloud-services/cloud-services-python-ptvs.md

<!--External Link references-->
[Portal de Azure]: https://portal.azure.com
[Python Tools para Visual Studio]: http://aka.ms/ptvs
[Python Tools 2.2 para Visual Studio]: http://go.microsoft.com/fwlink/?LinkID=624025
[Python Tools 2.2 para Visual Studio ejemplos VSIX]: http://go.microsoft.com/fwlink/?LinkID=624025
[Azure SDK y herramientas para VS 2015]: http://go.microsoft.com/fwlink/?LinkId=518003
[Python 2.7 de 32 bits]: http://go.microsoft.com/fwlink/?LinkId=517190
[Documentación sobre Python Tools para Visual Studio]: http://aka.ms/ptvsdocs
[Depuración remota en Microsoft Azure]: http://go.microsoft.com/fwlink/?LinkId=624026
[Proyectos web]: http://go.microsoft.com/fwlink/?LinkId=624027
[Proyectos de servicio en la nube]: http://go.microsoft.com/fwlink/?LinkId=624028
[Documentación de Django]: https://www.djangoproject.com/
[Base de datos SQL]: /documentation/services/sql-database/
