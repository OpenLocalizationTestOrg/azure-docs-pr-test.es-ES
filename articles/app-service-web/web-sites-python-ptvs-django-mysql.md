---
title: aaaDjango y MySQL en Azure con Python Tools 2.2 para Visual Studio
description: "Obtenga información acerca de cómo toouse Hola Python Tools para Visual Studio toocreate una aplicación web Django que almacena datos en una instancia de base de datos MySQL y lo implementará tooAzure aplicación del servicio Web de aplicaciones."
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
ms.openlocfilehash: 1597c391d20c8e8ef629b4e4d05c9eb64c83bffc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="django-and-mysql-on-azure-with-python-tools-22-for-visual-studio"></a><span data-ttu-id="e01ba-103">Django y MySQL en Azure con Python Tools 2.2 para Visual Studio</span><span class="sxs-lookup"><span data-stu-id="e01ba-103">Django and MySQL on Azure with Python Tools 2.2 for Visual Studio</span></span>
[!INCLUDE [tabs](../../includes/app-service-web-get-started-nav-tabs.md)]

<span data-ttu-id="e01ba-104">En este tutorial, usará [Python Tools para Visual Studio](https://www.visualstudio.com/vs/python) sondea de toocreate una sencilla aplicación web con una de las plantillas de ejemplo de Hola PTVS.</span><span class="sxs-lookup"><span data-stu-id="e01ba-104">In this tutorial, you'll use [Python Tools for Visual Studio](https://www.visualstudio.com/vs/python) toocreate a simple polls web app using one of hello PTVS sample templates.</span></span> <span data-ttu-id="e01ba-105">Aprenderá cómo toouse un servicio MySQL hospedado en Azure, cómo tooconfigure Hola toouse de aplicación web MySQL y cómo toopublish Hola aplicación web demasiado[aplicaciones de Web del servicio de aplicación de Azure](http://go.microsoft.com/fwlink/?LinkId=529714).</span><span class="sxs-lookup"><span data-stu-id="e01ba-105">You'll learn how toouse a MySQL service hosted on Azure, how tooconfigure hello web app toouse MySQL, and how toopublish hello web app too[Azure App Service Web Apps](http://go.microsoft.com/fwlink/?LinkId=529714).</span></span>

> [!NOTE]
> <span data-ttu-id="e01ba-106">información de Hello contenida en este tutorial también está disponible en hello después de vídeo:</span><span class="sxs-lookup"><span data-stu-id="e01ba-106">hello information contained in this tutorial is also available in hello following video:</span></span>
> 
> <span data-ttu-id="e01ba-107">[PTVS 2.1: Django app with MySQL][video] (PTVS 2.1: aplicación Django con MySQL)</span><span class="sxs-lookup"><span data-stu-id="e01ba-107">[PTVS 2.1: Django app with MySQL][video]</span></span>
> 
> 

<span data-ttu-id="e01ba-108">Vea hello [Centro para desarrolladores de Python] para ver más artículos que cubren el desarrollo de aplicaciones de Web del servicio de aplicación de Azure con PTVS mediante Bottle por sí solo, matraz y Django web marcos de trabajo, con los servicios de almacenamiento de tabla de Azure, MySQL y base de datos SQL.</span><span class="sxs-lookup"><span data-stu-id="e01ba-108">See hello [Python Developer Center] for more articles that cover development of Azure App Service Web Apps with PTVS using Bottle, Flask and Django web frameworks, with Azure Table Storage, MySQL, and SQL Database services.</span></span> <span data-ttu-id="e01ba-109">Aunque en este artículo se centra en el servicio de aplicaciones, los pasos de hello son similares al desarrollar [servicios en la nube].</span><span class="sxs-lookup"><span data-stu-id="e01ba-109">While this article focuses on App Service, hello steps are similar when developing [Azure Cloud Services].</span></span>

## <a name="prerequisites"></a><span data-ttu-id="e01ba-110">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="e01ba-110">Prerequisites</span></span>
* <span data-ttu-id="e01ba-111">Visual Studio 2015</span><span class="sxs-lookup"><span data-stu-id="e01ba-111">Visual Studio 2015</span></span>
* <span data-ttu-id="e01ba-112">[Python 2.7 de 32 bits] o [Python 3.4 de 32 bits]</span><span class="sxs-lookup"><span data-stu-id="e01ba-112">[Python 2.7 32-bit] or [Python 3.4 32-bit]</span></span>
* <span data-ttu-id="e01ba-113">[Python Tools 2.2 para Visual Studio]</span><span class="sxs-lookup"><span data-stu-id="e01ba-113">[Python Tools 2.2 for Visual Studio]</span></span>
* <span data-ttu-id="e01ba-114">[Python Tools 2.2 para Visual Studio ejemplos VSIX]</span><span class="sxs-lookup"><span data-stu-id="e01ba-114">[Python Tools 2.2 for Visual Studio Samples VSIX]</span></span>
* <span data-ttu-id="e01ba-115">[Azure SDK y herramientas para VS 2015]</span><span class="sxs-lookup"><span data-stu-id="e01ba-115">[Azure SDK Tools for VS 2015]</span></span>
* <span data-ttu-id="e01ba-116">Django 1.9 o posterior</span><span class="sxs-lookup"><span data-stu-id="e01ba-116">Django 1.9 or later</span></span>

[!INCLUDE [create-account-and-websites-note](../../includes/create-account-and-websites-note.md)]

<!-- This note should not render as part of hello hello previous include. -->

> [!NOTE]
> <span data-ttu-id="e01ba-117">Si desea tooget iniciado con el servicio de aplicación de Azure antes de registrarse para una cuenta de Azure, vaya demasiado[pruebe el servicio de aplicaciones](https://azure.microsoft.com/try/app-service/), donde puede crear inmediatamente una aplicación web de inicio de corta duración en el servicio de aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="e01ba-117">If you want tooget started with Azure App Service before signing up for an Azure account, go too[Try App Service](https://azure.microsoft.com/try/app-service/), where you can immediately create a short-lived starter web app in App Service.</span></span> <span data-ttu-id="e01ba-118">No es necesario proporcionar ninguna tarjeta de crédito ni asumir ningún compromiso.</span><span class="sxs-lookup"><span data-stu-id="e01ba-118">No credit card is required, and no commitments are necessary.</span></span>
> 
> 

## <a name="create-hello-project"></a><span data-ttu-id="e01ba-119">Crear proyecto de hello</span><span class="sxs-lookup"><span data-stu-id="e01ba-119">Create hello Project</span></span>
<span data-ttu-id="e01ba-120">En esta sección, va a crear un proyecto de Visual Studio con la utilización de una plantilla de ejemplo.</span><span class="sxs-lookup"><span data-stu-id="e01ba-120">In this section, you'll create a Visual Studio project using a sample template.</span></span> <span data-ttu-id="e01ba-121">Va a crear un entorno virtual e instalar los paquetes necesarios.</span><span class="sxs-lookup"><span data-stu-id="e01ba-121">You'll create a virtual environment and install required packages.</span></span> <span data-ttu-id="e01ba-122">Va a crear una base de datos local con sqlite.</span><span class="sxs-lookup"><span data-stu-id="e01ba-122">You'll create a local database using sqlite.</span></span> <span data-ttu-id="e01ba-123">A continuación, ejecutaremos aplicación hello localmente.</span><span class="sxs-lookup"><span data-stu-id="e01ba-123">Then you'll run hello application locally.</span></span>

1. <span data-ttu-id="e01ba-124">En Visual Studio, seleccione **Archivo**, **Nuevo proyecto**.</span><span class="sxs-lookup"><span data-stu-id="e01ba-124">In Visual Studio, select **File**, **New Project**.</span></span>
2. <span data-ttu-id="e01ba-125">Hola plantillas de proyecto de hello [Python Tools 2.2 para Visual Studio ejemplos VSIX] están disponibles en **Python**, **ejemplos**.</span><span class="sxs-lookup"><span data-stu-id="e01ba-125">hello project templates from hello [Python Tools 2.2 for Visual Studio Samples VSIX] are available under **Python**, **Samples**.</span></span> <span data-ttu-id="e01ba-126">Seleccione **proyecto Web de sondeos Django** y haga clic en Aceptar toocreate Hola proyecto.</span><span class="sxs-lookup"><span data-stu-id="e01ba-126">Select **Polls Django Web Project** and click OK toocreate hello project.</span></span>
   
    ![Cuadro de diálogo Nuevo proyecto](./media/web-sites-python-ptvs-django-mysql/PollsDjangoNewProject.png)
3. <span data-ttu-id="e01ba-128">Es posible que los paquetes externos tooinstall solicitadas.</span><span class="sxs-lookup"><span data-stu-id="e01ba-128">You will be prompted tooinstall external packages.</span></span> <span data-ttu-id="e01ba-129">Seleccione **Instalar en un entorno virtual**.</span><span class="sxs-lookup"><span data-stu-id="e01ba-129">Select **Install into a virtual environment**.</span></span>
   
    ![Cuadro de diálogo Paquetes externos](./media/web-sites-python-ptvs-django-mysql/PollsDjangoExternalPackages.png)
4. <span data-ttu-id="e01ba-131">Seleccione **Python 2.7** o **3.4 de Python** como intérprete base Hola.</span><span class="sxs-lookup"><span data-stu-id="e01ba-131">Select **Python 2.7** or **Python 3.4** as hello base interpreter.</span></span>
   
    ![Cuadro de diálogo Agregar entorno virtual](./media/web-sites-python-ptvs-django-mysql/PollsCommonAddVirtualEnv.png)
5. <span data-ttu-id="e01ba-133">En **el Explorador de soluciones**, haga doble clic en el nodo del proyecto de Hola y seleccione **Python**y, a continuación, seleccione **Django migrar**.</span><span class="sxs-lookup"><span data-stu-id="e01ba-133">In **Solution Explorer**, right-click on hello project node and select **Python**, and then select **Django Migrate**.</span></span>  <span data-ttu-id="e01ba-134">Después, seleccione **Django Create Superuser (Crear superusuario de Django)**.</span><span class="sxs-lookup"><span data-stu-id="e01ba-134">Then select **Django Create Superuser**.</span></span>
6. <span data-ttu-id="e01ba-135">Se abrirá una consola de administración de Django y crear una base de datos de sqlite en la carpeta del proyecto Hola.</span><span class="sxs-lookup"><span data-stu-id="e01ba-135">This will open a Django Management Console and create a sqlite database in hello project folder.</span></span> <span data-ttu-id="e01ba-136">Siga los mensajes de Hola toocreate un usuario.</span><span class="sxs-lookup"><span data-stu-id="e01ba-136">Follow hello prompts toocreate a user.</span></span>
7. <span data-ttu-id="e01ba-137">Confirme que la aplicación hello funciona presionando `F5`.</span><span class="sxs-lookup"><span data-stu-id="e01ba-137">Confirm that hello application works by pressing `F5`.</span></span>
8. <span data-ttu-id="e01ba-138">Haga clic en **sesión** de barra de navegación superior de Hola Hola.</span><span class="sxs-lookup"><span data-stu-id="e01ba-138">Click **Log in** from hello navigation bar at hello top.</span></span>
   
    ![Barra de navegación de Django](./media/web-sites-python-ptvs-django-mysql/PollsDjangoCommonBrowserLocalMenu.png)
9. <span data-ttu-id="e01ba-140">Escriba las credenciales de hello para el usuario de Hola que creó al sincronizar base de datos de Hola.</span><span class="sxs-lookup"><span data-stu-id="e01ba-140">Enter hello credentials for hello user you created when you synchronized hello database.</span></span>
   
    ![Formulario de inicio de sesión](./media/web-sites-python-ptvs-django-mysql/PollsDjangoCommonBrowserLocalLogin.png)
10. <span data-ttu-id="e01ba-142">Haga clic en **Create Sample Polls**(Crear sondeos de ejemplo).</span><span class="sxs-lookup"><span data-stu-id="e01ba-142">Click **Create Sample Polls**.</span></span>
    
     ![Create Sample Polls](./media/web-sites-python-ptvs-django-mysql/PollsDjangoCommonBrowserNoPolls.png)
11. <span data-ttu-id="e01ba-144">Haga clic en un sondeo y vote.</span><span class="sxs-lookup"><span data-stu-id="e01ba-144">Click on a poll and vote.</span></span>
    
     ![Votación en sondeos de ejemplo](./media/web-sites-python-ptvs-django-mysql/PollsDjangoSqliteBrowser.png)

## <a name="create-a-mysql-database"></a><span data-ttu-id="e01ba-146">Creación de una base de datos MySQL</span><span class="sxs-lookup"><span data-stu-id="e01ba-146">Create a MySQL Database</span></span>
<span data-ttu-id="e01ba-147">Para base de datos de hello, creará una base de datos ClearDB MySQL hospedado en Azure.</span><span class="sxs-lookup"><span data-stu-id="e01ba-147">For hello database, you'll create a ClearDB MySQL hosted database on Azure.</span></span>

<span data-ttu-id="e01ba-148">Como alternativa, puede crear su propia máquina virtual para que se ejecute en Azure y, a continuación, instalar y administrar MySQL por su cuenta.</span><span class="sxs-lookup"><span data-stu-id="e01ba-148">As an alternative, you can create your own Virtual Machine running in Azure, then install and administer MySQL yourself.</span></span>

<span data-ttu-id="e01ba-149">Siga estos pasos para crear una base de datos con un plan gratuito.</span><span class="sxs-lookup"><span data-stu-id="e01ba-149">You can create a database with a free plan by following these steps.</span></span>

1. <span data-ttu-id="e01ba-150">Inicie sesión en toohello [Portal de Azure].</span><span class="sxs-lookup"><span data-stu-id="e01ba-150">Log in toohello [Azure Portal].</span></span>
2. <span data-ttu-id="e01ba-151">En la parte superior del panel de navegación de Hola Hola, haga clic en **NEW**, a continuación, haga clic en **datos + almacenamiento**y, a continuación, haga clic en **base de datos MySQL**.</span><span class="sxs-lookup"><span data-stu-id="e01ba-151">At hello Top of hello navigation pane, click **NEW**, then click **Data + Storage**, and then click **MySQL Database**.</span></span>
3. <span data-ttu-id="e01ba-152">Configurar base de datos de MySQL nueva hello mediante la creación de un nuevo grupo de recursos y seleccione la ubicación adecuada de hello para el mismo.</span><span class="sxs-lookup"><span data-stu-id="e01ba-152">Configure hello new MySQL database by creating a new resource group and select hello appropriate location for it.</span></span>
4. <span data-ttu-id="e01ba-153">Una vez que se crea la base de datos de MySQL de hello, haga clic en **propiedades** en la hoja de la base de datos de Hola.</span><span class="sxs-lookup"><span data-stu-id="e01ba-153">Once hello MySQL database is created, click **Properties** in hello database blade.</span></span>
5. <span data-ttu-id="e01ba-154">Usar valor Hola copia botón tooput Hola de **cadena de conexión** en Portapapeles Hola.</span><span class="sxs-lookup"><span data-stu-id="e01ba-154">Use hello copy button tooput hello value of **CONNECTION STRING** on hello clipboard.</span></span>

## <a name="configure-hello-project"></a><span data-ttu-id="e01ba-155">Configurar proyecto Hola</span><span class="sxs-lookup"><span data-stu-id="e01ba-155">Configure hello Project</span></span>
<span data-ttu-id="e01ba-156">En esta sección, configurará la aplicación toouse Hola MySQL base de datos web que acaba de crear.</span><span class="sxs-lookup"><span data-stu-id="e01ba-156">In this section, you'll configure our web app toouse hello MySQL database you just created.</span></span> <span data-ttu-id="e01ba-157">También deberá instalar bases de datos de MySQL de toouse necesarios adicionales paquetes de Python con Django.</span><span class="sxs-lookup"><span data-stu-id="e01ba-157">You'll also install additional Python packages required toouse MySQL databases with Django.</span></span> <span data-ttu-id="e01ba-158">A continuación, podrá ejecutar aplicación de hello web localmente.</span><span class="sxs-lookup"><span data-stu-id="e01ba-158">Then you'll run hello web app locally.</span></span>

1. <span data-ttu-id="e01ba-159">En Visual Studio, abra **settings.py**, de hello *ProjectName* carpeta.</span><span class="sxs-lookup"><span data-stu-id="e01ba-159">In Visual Studio, open **settings.py**, from hello *ProjectName* folder.</span></span> <span data-ttu-id="e01ba-160">Pegue temporalmente cadena de conexión de hello en el editor de Hola.</span><span class="sxs-lookup"><span data-stu-id="e01ba-160">Temporarily paste hello connection string in hello editor.</span></span> <span data-ttu-id="e01ba-161">cadena de conexión de Hello tiene este formato:</span><span class="sxs-lookup"><span data-stu-id="e01ba-161">hello connection string is in this format:</span></span>
   
        Database=<NAME>;Data Source=<HOST>;User Id=<USER>;Password=<PASSWORD>
   
    <span data-ttu-id="e01ba-162">Base de datos de cambio Hola predeterminada **motor** toouse MySQL y establezca Hola valores para **nombre**, **usuario**, **contraseña** y  **HOST** de hello **CONNECTIONSTRING**.</span><span class="sxs-lookup"><span data-stu-id="e01ba-162">Change hello default database **ENGINE** toouse MySQL, and set hello values for **NAME**, **USER**, **PASSWORD** and **HOST** from hello **CONNECTIONSTRING**.</span></span>
   
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
2. <span data-ttu-id="e01ba-163">En el Explorador de soluciones, bajo **entornos de Python**, haga doble clic en el entorno virtual de Hola y seleccione **instalar un paquete de Python**.</span><span class="sxs-lookup"><span data-stu-id="e01ba-163">In Solution Explorer, under **Python Environments**, right-click on hello virtual environment and select **Install Python Package**.</span></span>
3. <span data-ttu-id="e01ba-164">Instalar el paquete de hello `mysqlclient` con **pip**.</span><span class="sxs-lookup"><span data-stu-id="e01ba-164">Install hello package `mysqlclient` using **pip**.</span></span>
   
    ![Cuadro de diálogo Instalar paquete](./media/web-sites-python-ptvs-django-mysql/PollsDjangoMySQLInstallPackage.png)
4. <span data-ttu-id="e01ba-166">En **el Explorador de soluciones**, haga doble clic en el nodo del proyecto de Hola y seleccione **Python**y, a continuación, seleccione **Django migrar**.</span><span class="sxs-lookup"><span data-stu-id="e01ba-166">In **Solution Explorer**, right-click on hello project node and select **Python**, and then select **Django Migrate**.</span></span>  <span data-ttu-id="e01ba-167">Después, seleccione **Django Create Superuser (Crear superusuario de Django)**.</span><span class="sxs-lookup"><span data-stu-id="e01ba-167">Then select **Django Create Superuser**.</span></span>
   
    <span data-ttu-id="e01ba-168">Esto creará tablas de hello para la base de datos de MySQL de Hola que creó en la sección anterior de Hola.</span><span class="sxs-lookup"><span data-stu-id="e01ba-168">This will create hello tables for hello MySQL database you created in hello previous section.</span></span> <span data-ttu-id="e01ba-169">Siga los mensajes de Hola toocreate un usuario, que no tiene el usuario de hello toomatch en base de datos de sqlite de hello creado en la primera sección de este artículo de Hola.</span><span class="sxs-lookup"><span data-stu-id="e01ba-169">Follow hello prompts toocreate a user, which doesn't have toomatch hello user in hello sqlite database created in hello first section of this article.</span></span>
5. <span data-ttu-id="e01ba-170">Ejecutar la aplicación hello con `F5`.</span><span class="sxs-lookup"><span data-stu-id="e01ba-170">Run hello application with `F5`.</span></span> <span data-ttu-id="e01ba-171">Sondeos que se crean con **crear sondeos de ejemplo** y se van a serializar datos Hola enviados votando en la base de datos de MySQL de Hola.</span><span class="sxs-lookup"><span data-stu-id="e01ba-171">Polls that are created with **Create Sample Polls** and hello data submitted by voting will be serialized in hello MySQL database.</span></span>

## <a name="publish-hello-web-app-tooazure-app-service"></a><span data-ttu-id="e01ba-172">Publicar hello web app tooAzure servicio de aplicaciones</span><span class="sxs-lookup"><span data-stu-id="e01ba-172">Publish hello web app tooAzure App Service</span></span>
<span data-ttu-id="e01ba-173">Hello Azure SDK para .NET proporciona una manera sencilla de toodeploy su tooAzure de aplicación web servicio de aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="e01ba-173">hello Azure .NET SDK provides an easy way toodeploy your web app tooAzure App Service.</span></span>

1. <span data-ttu-id="e01ba-174">En **el Explorador de soluciones**, haga doble clic en el nodo del proyecto de Hola y seleccione **publicar**.</span><span class="sxs-lookup"><span data-stu-id="e01ba-174">In **Solution Explorer**, right-click on hello project node and select **Publish**.</span></span>
   
    ![Cuadro de diálogo Publicación web](./media/web-sites-python-ptvs-django-mysql/PollsCommonPublishWebSiteDialog.png)
2. <span data-ttu-id="e01ba-176">Haga clic en **Servicio de aplicaciones de Microsoft Azure**.</span><span class="sxs-lookup"><span data-stu-id="e01ba-176">Click on **Microsoft Azure App Service**.</span></span>
3. <span data-ttu-id="e01ba-177">Haga clic en **New** toocreate una nueva aplicación web.</span><span class="sxs-lookup"><span data-stu-id="e01ba-177">Click on **New** toocreate a new web app.</span></span>
4. <span data-ttu-id="e01ba-178">Rellene Hola después de campos y haga clic en **crear**:</span><span class="sxs-lookup"><span data-stu-id="e01ba-178">Fill in hello following fields and click **Create**:</span></span>
   
   * <span data-ttu-id="e01ba-179">**Nombre de aplicación web**</span><span class="sxs-lookup"><span data-stu-id="e01ba-179">**Web App name**</span></span>
   * <span data-ttu-id="e01ba-180">**Plan del Servicio de aplicaciones**</span><span class="sxs-lookup"><span data-stu-id="e01ba-180">**App Service plan**</span></span>
   * <span data-ttu-id="e01ba-181">**Grupos de recursos**</span><span class="sxs-lookup"><span data-stu-id="e01ba-181">**Resource group**</span></span>
   * <span data-ttu-id="e01ba-182">**Región**</span><span class="sxs-lookup"><span data-stu-id="e01ba-182">**Region**</span></span>
   * <span data-ttu-id="e01ba-183">Deje **servidor de base de datos** establecido demasiado**ninguna base de datos**</span><span class="sxs-lookup"><span data-stu-id="e01ba-183">Leave **Database server** set too**No database**</span></span>
5. <span data-ttu-id="e01ba-184">Acepte todos los valores predeterminados y haga clic en **Publicar**.</span><span class="sxs-lookup"><span data-stu-id="e01ba-184">Accept all other defaults and click **Publish**.</span></span>
6. <span data-ttu-id="e01ba-185">El explorador web abrirá automáticamente aplicaciones web publicadas de toohello.</span><span class="sxs-lookup"><span data-stu-id="e01ba-185">Your web browser will open automatically toohello published web app.</span></span> <span data-ttu-id="e01ba-186">Debería ver el trabajo de aplicación web de hello según lo esperado, con hello **MySQL** base de datos hospedada en Azure.</span><span class="sxs-lookup"><span data-stu-id="e01ba-186">You should see hello web app working as expected, using hello **MySQL** database hosted on Azure.</span></span>
   
    ![Explorador web](./media/web-sites-python-ptvs-django-mysql/PollsDjangoAzureBrowser.png)
   
    <span data-ttu-id="e01ba-188">¡Enhorabuena!</span><span class="sxs-lookup"><span data-stu-id="e01ba-188">Congratulations!</span></span> <span data-ttu-id="e01ba-189">Se ha publicado correctamente su tooAzure de aplicación web basada en MySQL.</span><span class="sxs-lookup"><span data-stu-id="e01ba-189">You have successfully published your MySQL-based web app tooAzure.</span></span>

## <a name="next-steps"></a><span data-ttu-id="e01ba-190">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="e01ba-190">Next steps</span></span>
<span data-ttu-id="e01ba-191">Siga estos toolearn de vínculos más información acerca de Python Tools para Visual Studio, Django y MySQL.</span><span class="sxs-lookup"><span data-stu-id="e01ba-191">Follow these links toolearn more about Python Tools for Visual Studio, Django and MySQL.</span></span>

* <span data-ttu-id="e01ba-192">[Documentación sobre Python Tools para Visual Studio]</span><span class="sxs-lookup"><span data-stu-id="e01ba-192">[Python Tools for Visual Studio Documentation]</span></span>
  * <span data-ttu-id="e01ba-193">[Proyectos web]</span><span class="sxs-lookup"><span data-stu-id="e01ba-193">[Web Projects]</span></span>
  * <span data-ttu-id="e01ba-194">[Proyectos de servicio en la nube]</span><span class="sxs-lookup"><span data-stu-id="e01ba-194">[Cloud Service Projects]</span></span>
  * <span data-ttu-id="e01ba-195">[Depuración remota en Microsoft Azure]</span><span class="sxs-lookup"><span data-stu-id="e01ba-195">[Remote Debugging on Microsoft Azure]</span></span>
* <span data-ttu-id="e01ba-196">[Documentación de Django]</span><span class="sxs-lookup"><span data-stu-id="e01ba-196">[Django Documentation]</span></span>
* <span data-ttu-id="e01ba-197">[MySQL]</span><span class="sxs-lookup"><span data-stu-id="e01ba-197">[MySQL]</span></span>

<span data-ttu-id="e01ba-198">Para obtener más información, vea hello [Centro para desarrolladores de Python](/develop/python/).</span><span class="sxs-lookup"><span data-stu-id="e01ba-198">For more information, see hello [Python Developer Center](/develop/python/).</span></span>

<!--Link references-->

[Centro para desarrolladores de Python]: /develop/python/
[servicios en la nube]: ../cloud-services/cloud-services-python-ptvs.md

<!--External Link references-->

[Portal de Azure]: https://portal.azure.com
[Python Tools for Visual Studio]: https://www.visualstudio.com/vs/python/
[Python Tools 2.2 para Visual Studio]: http://go.microsoft.com/fwlink/?LinkID=624025
[Python Tools 2.2 para Visual Studio ejemplos VSIX]: http://go.microsoft.com/fwlink/?LinkID=624025
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
