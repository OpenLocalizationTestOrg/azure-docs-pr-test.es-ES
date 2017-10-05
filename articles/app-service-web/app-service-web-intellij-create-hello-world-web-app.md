---
title: "Creación de una aplicación web básica de Azure en IntelliJ | Microsoft Docs"
description: "En este tutorial se muestra cómo utilizar el Kit de herramientas de Azure para IntelliJ para crear una aplicación web Hello World para Azure."
services: app-service\web
documentationcenter: java
author: selvasingh
manager: erikre
editor: 
ms.assetid: 75ce7b36-e3ae-491d-8305-4b42ce37db4e
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: Java
ms.topic: article
ms.date: 04/25/2017
ms.author: robmcm
ms.openlocfilehash: 20b2c3d86f5bde9302647f345aa99b030d78613a
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/29/2017
---
# <a name="create-a-basic-azure-web-app-in-intellij"></a><span data-ttu-id="ef0ec-103">Creación de una aplicación web básica de Azure en IntelliJ</span><span class="sxs-lookup"><span data-stu-id="ef0ec-103">Create a basic Azure web app in IntelliJ</span></span>
<span data-ttu-id="ef0ec-104">En este tutorial se muestra cómo crear e implementar una aplicación básica Hello World en Azure como una aplicación web mediante el [kit de herramientas de Azure para IntelliJ].</span><span class="sxs-lookup"><span data-stu-id="ef0ec-104">This tutorial shows how to create and deploy a basic Hello World application to Azure as a Web App by using the [Azure Toolkit for IntelliJ].</span></span> <span data-ttu-id="ef0ec-105">Para que sea más sencillo, se muestra un ejemplo básico de JSP, pero los pasos similares se aplicarían en el caso de un servlet Java en lo que respecta a la implementación de Azure.</span><span class="sxs-lookup"><span data-stu-id="ef0ec-105">A basic JSP example is shown for simplicity, but similar steps would be appropriate for a Java servlet, as far as Azure deployment is concerned.</span></span>

<span data-ttu-id="ef0ec-106">Cuando haya completado este tutorial, la aplicación se parecerá a la que se muestra en la siguiente ilustración al verla en un explorador web:</span><span class="sxs-lookup"><span data-stu-id="ef0ec-106">When you have completed this tutorial, your application will look similar to the following illustration when you view it in a web browser:</span></span>

![Página web de ejemplo][01]

## <a name="prerequisites"></a><span data-ttu-id="ef0ec-108">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="ef0ec-108">Prerequisites</span></span>
* <span data-ttu-id="ef0ec-109">Un kit para desarrolladores de Java (JDK) de la versión 1.8 o superior.</span><span class="sxs-lookup"><span data-stu-id="ef0ec-109">A Java Developer Kit (JDK), v 1.8 or later.</span></span>
* <span data-ttu-id="ef0ec-110">IntelliJ IDEA Ultimate Edition.</span><span class="sxs-lookup"><span data-stu-id="ef0ec-110">IntelliJ IDEA Ultimate Edition.</span></span> <span data-ttu-id="ef0ec-111">Se puede descargar desde <https://www.jetbrains.com/idea/download/index.html>.</span><span class="sxs-lookup"><span data-stu-id="ef0ec-111">This can be downloaded from <https://www.jetbrains.com/idea/download/index.html>.</span></span>
* <span data-ttu-id="ef0ec-112">Una distribución de un servidor web basado en Java o un servidor de aplicaciones, como [Apache Tomcat] o [Jetty].</span><span class="sxs-lookup"><span data-stu-id="ef0ec-112">A distribution of a Java-based web server or application server, such as [Apache Tomcat] or [Jetty].</span></span>
* <span data-ttu-id="ef0ec-113">Una suscripción a Azure, que se puede adquirir en <https://azure.microsoft.com/free/> o <http://azure.microsoft.com/pricing/purchase-options/>.</span><span class="sxs-lookup"><span data-stu-id="ef0ec-113">An Azure subscription, which can be acquired from <https://azure.microsoft.com/free/> or <http://azure.microsoft.com/pricing/purchase-options/>.</span></span>
* <span data-ttu-id="ef0ec-114">El [kit de herramientas de Azure para IntelliJ].</span><span class="sxs-lookup"><span data-stu-id="ef0ec-114">The [Azure Toolkit for IntelliJ].</span></span> <span data-ttu-id="ef0ec-115">Para obtener información acerca de la instalación del kit de herramientas de Azure, consulte [Instalación del kit de herramientas de Azure para IntelliJ].</span><span class="sxs-lookup"><span data-stu-id="ef0ec-115">For information about installing the Azure Toolkit, see [Installing the Azure Toolkit for IntelliJ].</span></span>

## <a name="to-create-a-hello-world-application"></a><span data-ttu-id="ef0ec-116">Para crear una aplicación Hola a todos</span><span class="sxs-lookup"><span data-stu-id="ef0ec-116">To create a Hello World application</span></span>
<span data-ttu-id="ef0ec-117">En primer lugar, empezaremos con la creación de un proyecto Java.</span><span class="sxs-lookup"><span data-stu-id="ef0ec-117">First, we'll start off with creating a Java project.</span></span>

1. <span data-ttu-id="ef0ec-118">Inicie IntelliJ y haga clic en **File** (Archivo), **New** (Nuevo) y, finalmente, en **Project** (Proyecto).</span><span class="sxs-lookup"><span data-stu-id="ef0ec-118">Start IntelliJ and click the **File** menu, then click **New**, and then click **Project**.</span></span>
   
    ![Archivo Nuevo Proyecto][02]
2. <span data-ttu-id="ef0ec-120">En el cuadro de diálogo New Project (Nuevo proyecto), seleccione **Java** y **Web Application** (Aplicación web) y, después, haga clic en **New** (Nuevo) para agregar un SDK del proyecto.</span><span class="sxs-lookup"><span data-stu-id="ef0ec-120">In the New Project dialog box, select **Java**, then **Web Application**, and then click **New** to add a Project SDK.</span></span>
   
    ![Cuadro de diálogo Nuevo proyecto][03a]
   
3. <span data-ttu-id="ef0ec-122">En el cuadro de diálogo Select Home Directory for JDK (Seleccionar directorio de inicio para JDK), seleccione la carpeta donde está instalado el JDK y, después, haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="ef0ec-122">In the Select Home Directory for JDK dialog box, select the folder where your JDK is installed, and then click **OK**.</span></span> <span data-ttu-id="ef0ec-123">Haga clic en **Siguiente** en el cuadro de diálogo de nuevo proyecto para continuar.</span><span class="sxs-lookup"><span data-stu-id="ef0ec-123">Click **Next** in the New Project dialog box to continue.</span></span>
   
    ![Especificación del directorio de inicio de JDK][03b]
4. <span data-ttu-id="ef0ec-125">Para este tutorial, asigne al proyecto el nombre **Java-Web-App-On-Azure** y haga clic en **Finish** (Finalizar).</span><span class="sxs-lookup"><span data-stu-id="ef0ec-125">For purposes of this tutorial, name the project **Java-Web-App-On-Azure**, and then click **Finish**.</span></span>
   
    ![Cuadro de diálogo Nuevo proyecto][04]
5. <span data-ttu-id="ef0ec-127">En la vista del explorador de proyectos de IntelliJ, expanda **Java-Web-App-On-Azure**, después expanda **web** y, luego, haga doble clic en **index.jsp**.</span><span class="sxs-lookup"><span data-stu-id="ef0ec-127">Within IntelliJ's Project Explorer view, expand **Java-Web-App-On-Azure**, then expand **web**, and then double-click **index.jsp**.</span></span>
   
    ![Abrir página de índice][05c]
6. <span data-ttu-id="ef0ec-129">Cuando el archivo index.jsp se abra en IntelliJ, agregue texto para que se muestre dinámicamente **Hello World!**</span><span class="sxs-lookup"><span data-stu-id="ef0ec-129">When your index.jsp file opens in IntelliJ, add in text to dynamically display **Hello World!**</span></span> <span data-ttu-id="ef0ec-130">dentro del elemento `<body>` existente.</span><span class="sxs-lookup"><span data-stu-id="ef0ec-130">within the existing `<body>` element.</span></span> <span data-ttu-id="ef0ec-131">El contenido de `<body>` actualizado debe parecerse al siguiente ejemplo:</span><span class="sxs-lookup"><span data-stu-id="ef0ec-131">Your updated `<body>` content should resemble the following example:</span></span>
   
    `<body><b><% out.println("Hello World!"); %></b></body>` 
7. <span data-ttu-id="ef0ec-132">Guarde el archivo index.jsp.</span><span class="sxs-lookup"><span data-stu-id="ef0ec-132">Save index.jsp.</span></span>

## <a name="to-deploy-your-application-to-an-azure-web-app-container"></a><span data-ttu-id="ef0ec-133">Para implementar la aplicación en un contenedor de aplicaciones web de Azure</span><span class="sxs-lookup"><span data-stu-id="ef0ec-133">To deploy your application to an Azure Web App Container</span></span>
<span data-ttu-id="ef0ec-134">Existen varias maneras de implementar una aplicación web de Java en Azure.</span><span class="sxs-lookup"><span data-stu-id="ef0ec-134">There are several ways by which you can deploy a Java web application to Azure.</span></span> <span data-ttu-id="ef0ec-135">En este tutorial se describe una de las más sencillas: la aplicación se implementará en un contenedor de aplicaciones de Azure: no se necesita ningún tipo de proyecto especial ni herramientas adicionales.</span><span class="sxs-lookup"><span data-stu-id="ef0ec-135">This tutorial describes one of the simplest: your application will be deployed to an Azure Web App Container - no special project type nor additional tools are needed.</span></span> <span data-ttu-id="ef0ec-136">Azure facilitará el JDK y el software de contenedor web, así que no es necesario que cargue los suyos; lo único que necesita es su aplicación web de Java.</span><span class="sxs-lookup"><span data-stu-id="ef0ec-136">The JDK and the web container software will be provided for you by Azure, so there is no need to upload your own; all you need is your Java Web App.</span></span> <span data-ttu-id="ef0ec-137">Como resultado, el proceso de publicación de su aplicación tardará unos segundos y no minutos.</span><span class="sxs-lookup"><span data-stu-id="ef0ec-137">As a result, the publishing process for your application will take seconds, not minutes.</span></span>

<span data-ttu-id="ef0ec-138">Antes de publicar la aplicación, primero debe configurar el módulo.</span><span class="sxs-lookup"><span data-stu-id="ef0ec-138">Before you publish your application, you first need to configure your module settings.</span></span> <span data-ttu-id="ef0ec-139">Para ello, siga estos pasos:</span><span class="sxs-lookup"><span data-stu-id="ef0ec-139">To do so, use the following steps:</span></span>

1. <span data-ttu-id="ef0ec-140">En el Explorador de proyectos de IntelliJ, haga clic con el botón derecho en el proyecto **Java-Web-App-On-Azure** .</span><span class="sxs-lookup"><span data-stu-id="ef0ec-140">In IntelliJ's Project Explorer, right-click the **Java-Web-App-On-Azure** project.</span></span> <span data-ttu-id="ef0ec-141">Cuando aparezca el menú contextual, haga clic en **Open Module Settings** (Abrir configuración del módulo).</span><span class="sxs-lookup"><span data-stu-id="ef0ec-141">When the context menu appears, click **Open Module Settings**.</span></span>

    ![Abrir configuración del módulo][05a]
2. <span data-ttu-id="ef0ec-143">Cuando se muestre el cuadro de diálogo Project Structure (Estructura de proyecto):</span><span class="sxs-lookup"><span data-stu-id="ef0ec-143">When the Project Structure dialog box appears:</span></span>

   <span data-ttu-id="ef0ec-144">a.</span><span class="sxs-lookup"><span data-stu-id="ef0ec-144">a.</span></span> <span data-ttu-id="ef0ec-145">Haga clic en **Artefactos** en la lista de **configuración del proyecto**.</span><span class="sxs-lookup"><span data-stu-id="ef0ec-145">Click **Artifacts** in the list of **Project Settings**.</span></span>
   <span data-ttu-id="ef0ec-146">b.</span><span class="sxs-lookup"><span data-stu-id="ef0ec-146">b.</span></span> <span data-ttu-id="ef0ec-147">Cambie el nombre del artefacto en el cuadro **Nombre** para que contenga un espacio en blanco o caracteres especiales; esto es necesario porque el nombre se usará en el identificador uniforme de recursos (URI).</span><span class="sxs-lookup"><span data-stu-id="ef0ec-147">Change the artifact name in the **Name** box so that it doesn't contain whitespace or special characters; this is necessary since the name will be used in the Uniform Resource Identifier (URI).</span></span>
   <span data-ttu-id="ef0ec-148">c.</span><span class="sxs-lookup"><span data-stu-id="ef0ec-148">c.</span></span> <span data-ttu-id="ef0ec-149">Cambiar el **tipo** a **Aplicación Web: archivo**.</span><span class="sxs-lookup"><span data-stu-id="ef0ec-149">Change the **Type** to **Web Application: Archive**.</span></span>
   <span data-ttu-id="ef0ec-150">d.</span><span class="sxs-lookup"><span data-stu-id="ef0ec-150">d.</span></span> <span data-ttu-id="ef0ec-151">Haga clic en **OK** (Aceptar) para cerrar el cuadro de diálogo Project Structure (Estructura del proyecto).</span><span class="sxs-lookup"><span data-stu-id="ef0ec-151">Click **OK** to close the Project Structure dialog box.</span></span>

    ![Abrir configuración del módulo][05b]

<span data-ttu-id="ef0ec-153">Cuando se ha configurado el módulo, puede publicar la aplicación en Azure mediante los pasos siguientes:</span><span class="sxs-lookup"><span data-stu-id="ef0ec-153">When you have configured your module settings, you can publish your application to Azure by using the following steps:</span></span>

1. <span data-ttu-id="ef0ec-154">En el Explorador de proyectos de IntelliJ, haga clic con el botón derecho en el proyecto **Java-Web-App-On-Azure** .</span><span class="sxs-lookup"><span data-stu-id="ef0ec-154">In IntelliJ's Project Explorer, right-click the **Java-Web-App-On-Azure** project.</span></span> <span data-ttu-id="ef0ec-155">Cuando aparezca el menú contextual, seleccione **Azure** y, después, haga clic en **Publish as Azure Web App...** (Publicar como aplicación web de Azure)</span><span class="sxs-lookup"><span data-stu-id="ef0ec-155">When the context menu appears, select **Azure**, and then click **Publish as Azure Web App...**</span></span>
   
    ![Menú contextual de publicación de Azure][06]
2. <span data-ttu-id="ef0ec-157">Si aún no ha iniciado sesión en Azure desde IntelliJ, se le pedirá que lo haga.</span><span class="sxs-lookup"><span data-stu-id="ef0ec-157">If you have not already signed into Azure from IntelliJ, you will be prompted to sign into your Azure account.</span></span> <span data-ttu-id="ef0ec-158">(Si tiene varias cuentas de Azure, puede que algunos de los avisos que aparecen durante el proceso de inicio de sesión se muestren más de una vez, incluso si parecen ser iguales.</span><span class="sxs-lookup"><span data-stu-id="ef0ec-158">(If you have multiple Azure accounts, some of the prompts during the sign in process may be shown more than once, even if they appear to be the same.</span></span> <span data-ttu-id="ef0ec-159">Cuando esto ocurra, siga la instrucciones de inicio de sesión).</span><span class="sxs-lookup"><span data-stu-id="ef0ec-159">When this happens, continue to follow the sign in instructions.)</span></span>
   
    ![Cuadro de diálogo de inicio de sesión de Azure][07]
3. <span data-ttu-id="ef0ec-161">Cuando haya iniciado sesión correctamente en su cuenta de Azure, el cuadro de diálogo **Manage Subscriptions** (Administrar suscripciones) mostrará una lista de suscripciones que están asociadas con sus credenciales.</span><span class="sxs-lookup"><span data-stu-id="ef0ec-161">After you have successfully signed into your Azure account, the **Manage Subscriptions** dialog box will display a list of subscriptions that are associated with your credentials.</span></span> <span data-ttu-id="ef0ec-162">Si aparecen varias suscripciones y quiere trabajar solo con un subconjunto específico de ellas, opcionalmente puede desactivar las que no utilice. Cuando haya seleccionado las suscripciones, haga clic en **Cerrar**.</span><span class="sxs-lookup"><span data-stu-id="ef0ec-162">(If there are multiple subscriptions listed and you want to work with only a specific subset of them, you may optionally uncheck the subscriptions you don't want to use.) When you have selected your subscriptions, click **Close**.</span></span>
   
    ![Administrar suscripciones][08]
4. <span data-ttu-id="ef0ec-164">Cuando aparezca el cuadro de diálogo **Deploy to Azure Web App Container** (Implementar en el contenedor de aplicaciones web de Azure), se mostrarán los contenedores de aplicaciones web creados anteriormente; si no ha creado ningún contenedor, la lista estará vacía.</span><span class="sxs-lookup"><span data-stu-id="ef0ec-164">When the **Deploy to Azure Web App Container** dialog box appears, it will display any Web App containers that you have previously created; if you have not created any containers, the list will be empty.</span></span>
   
    ![Contenedores de aplicaciones][09]
5. <span data-ttu-id="ef0ec-166">Si no ha creado un contenedor de aplicaciones web de Azure antes, o si quiere publicar la aplicación en un nuevo contenedor, siga estos pasos.</span><span class="sxs-lookup"><span data-stu-id="ef0ec-166">If you have not created an Azure Web App Container before, or if you would like to publish your application to a new container, use the following steps.</span></span> <span data-ttu-id="ef0ec-167">De lo contrario, seleccione un contenedor de aplicaciones web existente y vaya al paso 6 que encontrará a continuación.</span><span class="sxs-lookup"><span data-stu-id="ef0ec-167">Otherwise, select an existing Web App Container and skip to step 6 below.</span></span>
   
   1. <span data-ttu-id="ef0ec-168">Haga clic en **+**</span><span class="sxs-lookup"><span data-stu-id="ef0ec-168">Click **+**</span></span>
      
       ![Agregar contenedor de aplicaciones][10]
   2. <span data-ttu-id="ef0ec-170">Se mostrará el cuadro de diálogo **New Web App Container** (Nuevo contenedor de aplicaciones web), que se usará para los siguientes pasos.</span><span class="sxs-lookup"><span data-stu-id="ef0ec-170">The **New Web App Container** dialog box will be displayed, which will be used for the next several steps.</span></span>
      
       ![Nuevo contenedor de aplicaciones][11a]
   3. <span data-ttu-id="ef0ec-172">Escriba un valor para **Etiqueta DNS** para el contenedor de aplicaciones web; esta será la etiqueta DNS hoja de la dirección URL del host de la aplicación web en Azure.</span><span class="sxs-lookup"><span data-stu-id="ef0ec-172">Enter a **DNS Label** for your Web App Container; this will form the leaf DNS label of the host URL for your web application in Azure.</span></span> <span data-ttu-id="ef0ec-173">Tenga en cuenta que el nombre debe estar disponible y se ajusta a los requisitos de nomenclatura de las aplicaciones web de Azure.</span><span class="sxs-lookup"><span data-stu-id="ef0ec-173">Note that the name must be available and conform to Azure Web App naming requirements.</span></span>
   4. <span data-ttu-id="ef0ec-174">En el menú desplegable **Web Container** (Contenedor web), seleccione el software adecuado para su aplicación.</span><span class="sxs-lookup"><span data-stu-id="ef0ec-174">In the **Web Container** drop-down menu, select the appropriate software for your application.</span></span>
      
       <span data-ttu-id="ef0ec-175">Actualmente, puede elegir entre Tomcat 8, Tomcat 7 o Jetty 9.</span><span class="sxs-lookup"><span data-stu-id="ef0ec-175">Currently, you can choose from Tomcat 8, Tomcat 7 or Jetty 9.</span></span> <span data-ttu-id="ef0ec-176">Azure proporcionará una distribución reciente del software seleccionado y se ejecutará en una distribución reciente de JDK 8 creada por Oracle y proporcionada por Azure.</span><span class="sxs-lookup"><span data-stu-id="ef0ec-176">A recent distribution of the selected software will be provided by Azure, and it will run on a recent distribution of JDK 8 created by Oracle and provided by Azure.</span></span>
   5. <span data-ttu-id="ef0ec-177">En el menú desplegable **Suscripción** , seleccione la suscripción que quiere usar para esta implementación.</span><span class="sxs-lookup"><span data-stu-id="ef0ec-177">In the **Subscription** drop-down menu, select the subscription you want to use for this deployment.</span></span>
   6. <span data-ttu-id="ef0ec-178">En el menú desplegable **Grupo de recursos** , seleccione el grupo de recursos con el que desea asociar la aplicación web.</span><span class="sxs-lookup"><span data-stu-id="ef0ec-178">In the **Resource Group** drop-down menu, select the Resource Group with which you want to associate your Web App.</span></span> <span data-ttu-id="ef0ec-179">Los grupos de recursos de Azure permiten agrupar recursos relacionados para que, por ejemplo, se puedan eliminar juntos.</span><span class="sxs-lookup"><span data-stu-id="ef0ec-179">(Azure Resource Groups allow you to group related resources together so that, for example, they can be deleted together.)</span></span>
      
       <span data-ttu-id="ef0ec-180">Puede seleccionar un grupo de recursos existente (si tiene alguno) y pasar al paso g a continuación o usar los siguientes pasos para crear un nuevo grupo de recursos:</span><span class="sxs-lookup"><span data-stu-id="ef0ec-180">You can select an existing Resource Group (if you have any) and skip to step g below, or use the following steps to create a new Resource Group:</span></span>
      
      * <span data-ttu-id="ef0ec-181">Seleccione **&lt;&lt; Crear nuevo grupo de recursos&gt;&gt;** en el menú desplegable **Grupo de recursos**.</span><span class="sxs-lookup"><span data-stu-id="ef0ec-181">Select **&lt;&lt; Create new Resource Group &gt;&gt;** in the **Resource Group** drop-down menu.</span></span>
      * <span data-ttu-id="ef0ec-182">Se muestra el cuadro de diálogo **Nuevo grupo de recursos** :</span><span class="sxs-lookup"><span data-stu-id="ef0ec-182">The **New Resource Group** dialog box will be displayed:</span></span>
        
          ![Nuevo grupo de recursos][12]
      * <span data-ttu-id="ef0ec-184">En el cuadro de texto **Nombre** , especifique un nombre para el nuevo grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="ef0ec-184">In the the **Name** textbox, specify a name for your new Resource Group.</span></span>
      * <span data-ttu-id="ef0ec-185">En el menú desplegable **Región** , seleccione la ubicación adecuada del centro de datos de Azure para su grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="ef0ec-185">In the the **Region** drop-down menu, select the appropriate Azure data center location for your Resource Group.</span></span>
      * <span data-ttu-id="ef0ec-186">Haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="ef0ec-186">Click **OK**.</span></span>
   7. <span data-ttu-id="ef0ec-187">En el menú desplegable **Plan del servicio de aplicaciones** se muestran los planes del servicio de aplicaciones que están asociados con el grupo de recursos seleccionado.</span><span class="sxs-lookup"><span data-stu-id="ef0ec-187">The **App Service Plan** drop-down menu lists the app service plans that are associated with the Resource Group that you selected.</span></span> <span data-ttu-id="ef0ec-188">(Un plan de App Service especifica información como la ubicación de la aplicación web, el plan de tarifa y el tamaño de la instancia de proceso.</span><span class="sxs-lookup"><span data-stu-id="ef0ec-188">(An App Service Plan specifies information such as the location of your Web App, the pricing tier and the compute instance size.</span></span> <span data-ttu-id="ef0ec-189">Un único plan de App Service se puede usar para varias aplicaciones web, motivo por el cual se mantiene independiente de una implementación específica de aplicaciones web.</span><span class="sxs-lookup"><span data-stu-id="ef0ec-189">A single App Service Plan can be used for multiple Web Apps, which is why it is maintained separately from a specific Web App deployment.)</span></span>
      
       <span data-ttu-id="ef0ec-190">Puede seleccionar un plan de plan de App Service existente (si tiene alguno) y pasar al paso h a continuación o usar los siguientes pasos para crear un nuevo plan:</span><span class="sxs-lookup"><span data-stu-id="ef0ec-190">You can select an existing App Service Plan (if you have any) and skip to step h below, or use the following steps to create a new App Service Plan:</span></span>
      
      * <span data-ttu-id="ef0ec-191">Seleccione **&lt;&lt; Crear nuevo plan de App Service&gt;&gt;** en el menú desplegable **Plan de App Service**.</span><span class="sxs-lookup"><span data-stu-id="ef0ec-191">Select **&lt;&lt; Create new App Service Plan &gt;&gt;** in the **App Service Plan** drop-down menu.</span></span>
      * <span data-ttu-id="ef0ec-192">Se muestra el cuadro de diálogo **Nuevo plan del servicio de aplicaciones** :</span><span class="sxs-lookup"><span data-stu-id="ef0ec-192">The **New App Service Plan** dialog box will be displayed:</span></span>
        
          ![Nuevo plan de App Service][13]
      * <span data-ttu-id="ef0ec-194">En el cuadro de texto **Nombre** , especifique un nombre para el nuevo plan.</span><span class="sxs-lookup"><span data-stu-id="ef0ec-194">In the the **Name** textbox, specify a name for your new App Service Plan.</span></span>
      * <span data-ttu-id="ef0ec-195">En el menú desplegable **Ubicación** , seleccione la ubicación adecuada del centro de datos de Azure para el plan.</span><span class="sxs-lookup"><span data-stu-id="ef0ec-195">In the the **Location** drop-down menu, select the appropriate Azure data center location for the plan.</span></span>
      * <span data-ttu-id="ef0ec-196">En el menú desplegable **Plan de tarifa** , seleccione la tarifa adecuada para el plan.</span><span class="sxs-lookup"><span data-stu-id="ef0ec-196">In the the **Pricing Tier** drop-down menu, select the appropriate pricing for the plan.</span></span> <span data-ttu-id="ef0ec-197">Con fines de prueba, puede elegir **Gratis**.</span><span class="sxs-lookup"><span data-stu-id="ef0ec-197">For testing purposes you can choose **Free**.</span></span>
      * <span data-ttu-id="ef0ec-198">En el menú desplegable **Tamaño de instancia** , seleccione el tamaño de instancia adecuado para el plan.</span><span class="sxs-lookup"><span data-stu-id="ef0ec-198">In the the **Instance Size** drop-down menu, select the appropriate instance size for the plan.</span></span> <span data-ttu-id="ef0ec-199">Con fines de prueba, puede elegir **Pequeño**.</span><span class="sxs-lookup"><span data-stu-id="ef0ec-199">For testing purposes you can choose **Small**.</span></span>
      * <span data-ttu-id="ef0ec-200">Haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="ef0ec-200">Click **OK**.</span></span>
   8. <span data-ttu-id="ef0ec-201">(Opcional) De manera predeterminada, Azure implementará automáticamente una distribución reciente de Java 8 como máquina virtual de Java en el contenedor de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="ef0ec-201">(Optional) By default, a recent distribution of Java 8 will be automatically deployed as your JVM by Azure to your web app container.</span></span> <span data-ttu-id="ef0ec-202">Sin embargo, puede seleccionar una versión y una distribución diferentes de la máquina virtual de Java.</span><span class="sxs-lookup"><span data-stu-id="ef0ec-202">However, you can select a different version and distribution of the JVM.</span></span> <span data-ttu-id="ef0ec-203">Para ello, siga estos pasos:</span><span class="sxs-lookup"><span data-stu-id="ef0ec-203">To do so, use the following steps:</span></span>
      
      * <span data-ttu-id="ef0ec-204">Haga clic en la pestaña **JDK** en el cuadro de diálogo **New Web App Container** (Nuevo contenedor de aplicaciones web).</span><span class="sxs-lookup"><span data-stu-id="ef0ec-204">Click the **JDK** tab in the **New Web App Container** dialog box.</span></span>
      * <span data-ttu-id="ef0ec-205">Puede elegir una de las siguientes opciones:</span><span class="sxs-lookup"><span data-stu-id="ef0ec-205">You can choose from one of the following options:</span></span>
        
        * <span data-ttu-id="ef0ec-206">Implementar el JDK predeterminado que ofrece Azure</span><span class="sxs-lookup"><span data-stu-id="ef0ec-206">Deploy the default JDK which is offered by Azure</span></span>
        * <span data-ttu-id="ef0ec-207">Implementar un JDK de terceros de lista desplegable de JDK adicionales que están disponibles en Azure</span><span class="sxs-lookup"><span data-stu-id="ef0ec-207">Deploy a 3rd party JDK from a drop-down list of additional JDKs which are available on Azure</span></span>
        * <span data-ttu-id="ef0ec-208">Implementar un JDK personalizado, que debe estar empaquetado en un archivo ZIP y bien estar disponible públicamente o en su cuenta de Azure Storage</span><span class="sxs-lookup"><span data-stu-id="ef0ec-208">Deploy a custom JDK, which must be packaged as a ZIP file and either publicly available or in your Azure storage account</span></span>
        
        ![Pestaña JDK de nuevo contenedor de aplicaciones][11b]
   9. <span data-ttu-id="ef0ec-210">Cuando haya completado todos los pasos anteriores, el cuadro de diálogo Nuevo contenedor de aplicaciones web debe parecerse al de la siguiente ilustración:</span><span class="sxs-lookup"><span data-stu-id="ef0ec-210">Once you have completed all of the above steps, the New Web App Container dialog box should resemble the following illustration:</span></span>
      
       ![Nuevo contenedor de aplicaciones][14]
   10. <span data-ttu-id="ef0ec-212">Haga clic en **Aceptar** para finalizar la creación de su nuevo contenedor de aplicaciones web.</span><span class="sxs-lookup"><span data-stu-id="ef0ec-212">Click **OK** to complete the creation of your new Web App container.</span></span>
       
        <span data-ttu-id="ef0ec-213">Espere unos segundos para que se actualice la lista de los contenedores de aplicaciones web y el contenedor recién creado ya debería estar seleccionado en la lista.</span><span class="sxs-lookup"><span data-stu-id="ef0ec-213">Wait a few seconds for the list of the Web App containers to be refreshed, and your newly-created web app container should now be selected in the list.</span></span>
6. <span data-ttu-id="ef0ec-214">Ya puede completar la implementación inicial de su aplicación web en Azure; haga clic en **Aceptar** para implementar la aplicación de Java en el contenedor de aplicación web seleccionado.</span><span class="sxs-lookup"><span data-stu-id="ef0ec-214">You are now ready to complete the initial deployment of your Web App to Azure; click **OK** to deploy your Java application to the selected Web App container.</span></span> <span data-ttu-id="ef0ec-215">De forma predeterminada, la aplicación se implementará como un subdirectorio del servidor de aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="ef0ec-215">By default, your application will be deployed as a subdirectory of the application server.</span></span> <span data-ttu-id="ef0ec-216">Si desea que se implemente como aplicación raíz, active la casilla **Deploy to root** (Implementar en raíz) antes de hacer clic en **OK** (Aceptar).</span><span class="sxs-lookup"><span data-stu-id="ef0ec-216">If you want it to be deployed as the root application, check the **Deploy to root** checkbox before clicking **OK**.</span></span>
   
    ![Implementar en Azure][15]
7. <span data-ttu-id="ef0ec-218">A continuación, debería mostrarse la vista **Azure Activity Log** (Registro de actividad de Azure), que indicará el estado de implementación de la aplicación web.</span><span class="sxs-lookup"><span data-stu-id="ef0ec-218">Next, you should see the **Azure Activity Log** view, which will indicate the deployment status of your Web App.</span></span>
   
    ![Indicador de progreso][16]
   
    <span data-ttu-id="ef0ec-220">El proceso de implementación de la aplicación web en Azure debería tardar solo unos segundos en completarse.</span><span class="sxs-lookup"><span data-stu-id="ef0ec-220">The process of deploying your Web App to Azure should take only a few seconds to complete.</span></span> <span data-ttu-id="ef0ec-221">Cuando su aplicación esté lista, verá un vínculo denominado **Publicado** in the **Status** (Estado).</span><span class="sxs-lookup"><span data-stu-id="ef0ec-221">When your application ready, you will see a link named **Published** in the **Status** column.</span></span> <span data-ttu-id="ef0ec-222">Al hacer clic en el vínculo, se le llevará a la página principal de la aplicación web implementada. Por otro lado, puede utilizar los pasos de la sección siguiente para ir a la aplicación web.</span><span class="sxs-lookup"><span data-stu-id="ef0ec-222">When you click the link, it will take you to your deployed Web App's home page, or you can use the steps in the following section to browse to your web app.</span></span>

## <a name="browsing-to-your-web-app-on-azure"></a><span data-ttu-id="ef0ec-223">Desplazamiento hasta su aplicación web en Azure</span><span class="sxs-lookup"><span data-stu-id="ef0ec-223">Browsing to your Web App on Azure</span></span>
<span data-ttu-id="ef0ec-224">Para ir a su aplicación web en Azure, puede usar la vista **Azure Explorer**.</span><span class="sxs-lookup"><span data-stu-id="ef0ec-224">To browse to your Web App on Azure, you can use the **Azure Explorer** view.</span></span>

<span data-ttu-id="ef0ec-225">Si la vista del **Explorador de Azure** no está abierta, puede abrirla haciendo clic en el menú **View** (Ver) de IntelliJ, luego haga clic en **Tool Windows** (Ventanas de herramientas) y, después, en **Service Explorer** (Explorador de servicios).</span><span class="sxs-lookup"><span data-stu-id="ef0ec-225">If the **Azure Explorer** view is not already open, you can open it by clicking then **View** menu in IntelliJ, then click **Tool Windows**, and then click **Service Explorer**.</span></span> <span data-ttu-id="ef0ec-226">Si anteriormente no ha iniciado sesión, se le pedirá que lo haga.</span><span class="sxs-lookup"><span data-stu-id="ef0ec-226">If you have not previously logged in, it will prompt you to do so.</span></span>

<span data-ttu-id="ef0ec-227">Cuando se muestre la vista **Azure Explorer**, siga estos pasos para examinar su aplicación web:</span><span class="sxs-lookup"><span data-stu-id="ef0ec-227">When the **Azure Explorer** view is displayed, use follow these steps to browse to your Web App:</span></span> 

1. <span data-ttu-id="ef0ec-228">Expanda el nodo **Azure** .</span><span class="sxs-lookup"><span data-stu-id="ef0ec-228">Expand the **Azure** node.</span></span>
2. <span data-ttu-id="ef0ec-229">Expanda el nodo **Aplicaciones web** .</span><span class="sxs-lookup"><span data-stu-id="ef0ec-229">Expand the **Web Apps** node.</span></span> 
3. <span data-ttu-id="ef0ec-230">Haga clic en la aplicación web deseada.</span><span class="sxs-lookup"><span data-stu-id="ef0ec-230">Right-click the desired Web App.</span></span>
4. <span data-ttu-id="ef0ec-231">Cuando aparezca el menú contextual, haga clic en **Abrir en el explorador**.</span><span class="sxs-lookup"><span data-stu-id="ef0ec-231">When the context menu appears, click **Open in Browser**.</span></span>
   
    ![Examinar una aplicación web][17]

## <a name="updating-your-web-app"></a><span data-ttu-id="ef0ec-233">Actualización de la aplicación web</span><span class="sxs-lookup"><span data-stu-id="ef0ec-233">Updating your web app</span></span>
<span data-ttu-id="ef0ec-234">Actualizar una aplicación web de Azure existente es un proceso rápido y sencillo, y tiene dos opciones para ello:</span><span class="sxs-lookup"><span data-stu-id="ef0ec-234">Updating an existing running Azure Web App is a quick and easy process, and you have two options for updating:</span></span>

* <span data-ttu-id="ef0ec-235">Puede actualizar la implementación de una aplicación web de Java existente.</span><span class="sxs-lookup"><span data-stu-id="ef0ec-235">You can update the deployment of an existing Java Web App.</span></span>
* <span data-ttu-id="ef0ec-236">Puede publicar una aplicación Java adicional en el mismo contenedor de aplicaciones web.</span><span class="sxs-lookup"><span data-stu-id="ef0ec-236">You can publish an additional Java application to the same Web App Container.</span></span>

<span data-ttu-id="ef0ec-237">En cualquier caso, el proceso es idéntico y tarda unos pocos segundos:</span><span class="sxs-lookup"><span data-stu-id="ef0ec-237">In either case, the process is identical and takes only a few seconds:</span></span>

1. <span data-ttu-id="ef0ec-238">En el Explorador de proyectos de IntelliJ, haga clic con el botón derecho en la aplicación Java que quiere actualizar o agregar a un contenedor de aplicaciones web existente.</span><span class="sxs-lookup"><span data-stu-id="ef0ec-238">In the IntelliJ project explorer, right-click the Java application you want to update or add to an existing Web App Container.</span></span>
2. <span data-ttu-id="ef0ec-239">Cuando aparezca el menú contextual, seleccione **Azure** y, después, haga clic en **Publish as Azure Web App...** (Publicar como aplicación web de Azure).</span><span class="sxs-lookup"><span data-stu-id="ef0ec-239">When the context menu appears, select **Azure** and then **Publish as Azure Web App...**</span></span>
3. <span data-ttu-id="ef0ec-240">Puesto que ya ha iniciado sesión anteriormente, verá una lista de contenedores de aplicaciones web existentes.</span><span class="sxs-lookup"><span data-stu-id="ef0ec-240">Since you have already logged in previously, you will see a list of your existing Web App containers.</span></span> <span data-ttu-id="ef0ec-241">Seleccione aquel en el que quiere publicar o volver a publicar la aplicación Java y haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="ef0ec-241">Select the one you want to publish or re-publish your Java application to and click **OK**.</span></span>

<span data-ttu-id="ef0ec-242">Unos segundos más tarde, la vista **Azure Activity Log** (Registro de actividad de Azure) mostrará la implementación actualizada como **Published** (Publicado) y podrá comprobar la aplicación actualizada en un explorador web.</span><span class="sxs-lookup"><span data-stu-id="ef0ec-242">A few seconds later, the **Azure Activity Log** view will show your updated deployment as **Published** and you will be able to verify your updated application in a web browser.</span></span>

## <a name="starting-stopping-or-restarting-an-existing-web-app"></a><span data-ttu-id="ef0ec-243">Inicio, detención o reinicio de una aplicación web existente</span><span class="sxs-lookup"><span data-stu-id="ef0ec-243">Starting, stopping, or restarting an existing web app</span></span>
<span data-ttu-id="ef0ec-244">Para iniciar o detener un contenedor de aplicaciones web existente (junto con todas las aplicaciones Java implementadas en él), puede utilizar la vista **Azure Explorer** (Explorador de Azure).</span><span class="sxs-lookup"><span data-stu-id="ef0ec-244">To start or stop an existing Azure Web App container, (including all the deployed Java applications in it), you can use the **Azure Explorer** view.</span></span>

<span data-ttu-id="ef0ec-245">Si la vista del **Explorador de Azure** no está abierta, puede abrirla haciendo clic en el menú **View** (Ver) de IntelliJ, luego haga clic en **Tool Windows** (Ventanas de herramientas) y, después, en **Service Explorer** (Explorador de servicios).</span><span class="sxs-lookup"><span data-stu-id="ef0ec-245">If the **Azure Explorer** view is not already open, you can open it by clicking then **View** menu in IntelliJ, then click **Tool Windows**, and then click **Service Explorer**.</span></span> <span data-ttu-id="ef0ec-246">Si anteriormente no ha iniciado sesión, se le pedirá que lo haga.</span><span class="sxs-lookup"><span data-stu-id="ef0ec-246">If you have not previously logged in, it will prompt you to do so.</span></span>

<span data-ttu-id="ef0ec-247">Cuando se muestre la vista **Azure Explorer** (Explorador de Azure), siga estos pasos para iniciar o detener su aplicación web:</span><span class="sxs-lookup"><span data-stu-id="ef0ec-247">When the **Azure Explorer** view is displayed, use follow these steps to start or stop your Web App:</span></span> 

1. <span data-ttu-id="ef0ec-248">Expanda el nodo **Azure** .</span><span class="sxs-lookup"><span data-stu-id="ef0ec-248">Expand the **Azure** node.</span></span>
2. <span data-ttu-id="ef0ec-249">Expanda el nodo **Aplicaciones web** .</span><span class="sxs-lookup"><span data-stu-id="ef0ec-249">Expand the **Web Apps** node.</span></span> 
3. <span data-ttu-id="ef0ec-250">Haga clic en la aplicación web deseada.</span><span class="sxs-lookup"><span data-stu-id="ef0ec-250">Right-click the desired Web App.</span></span>
4. <span data-ttu-id="ef0ec-251">Cuando aparezca el menú contextual, haga clic en **Iniciar**, **Detener** o **Reiniciar**.</span><span class="sxs-lookup"><span data-stu-id="ef0ec-251">When the context menu appears, click **Start**, **Stop**, or **Restart**.</span></span> <span data-ttu-id="ef0ec-252">Tenga en cuenta que las opciones de menú dependen del contexto, por lo que solo podrá detener una aplicación web que se encuentre en ejecución o iniciar una aplicación web que no se esté ejecutando en ese momento.</span><span class="sxs-lookup"><span data-stu-id="ef0ec-252">Note that the menu choices are context-aware, so you can only stop a running web app or start a web app which is not currently running.</span></span>
   
    ![Detener aplicación web][18]

## <a name="next-steps"></a><span data-ttu-id="ef0ec-254">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="ef0ec-254">Next Steps</span></span>
<span data-ttu-id="ef0ec-255">Para más información acerca de los kits de herramientas de Azure para los IDE de Java, vea los siguientes vínculos:</span><span class="sxs-lookup"><span data-stu-id="ef0ec-255">For more information about the Azure Toolkits for Java IDEs, see the following links:</span></span>

* <span data-ttu-id="ef0ec-256">[Kit de herramientas de Azure para Eclipse]</span><span class="sxs-lookup"><span data-stu-id="ef0ec-256">[Azure Toolkit for Eclipse]</span></span>
  * <span data-ttu-id="ef0ec-257">[Instalación del Kit de herramientas de Azure para Eclipse]</span><span class="sxs-lookup"><span data-stu-id="ef0ec-257">[Installing the Azure Toolkit for Eclipse]</span></span>
  * <span data-ttu-id="ef0ec-258">[Creación de una aplicación web Hello World para Azure en Eclipse]</span><span class="sxs-lookup"><span data-stu-id="ef0ec-258">[Create a Hello World Web App for Azure in Eclipse]</span></span>
  * <span data-ttu-id="ef0ec-259">[Novedades del kit de herramientas de Azure para Eclipse]</span><span class="sxs-lookup"><span data-stu-id="ef0ec-259">[What's New in the Azure Toolkit for Eclipse]</span></span>
* <span data-ttu-id="ef0ec-260">[kit de herramientas de Azure para IntelliJ]</span><span class="sxs-lookup"><span data-stu-id="ef0ec-260">[Azure Toolkit for IntelliJ]</span></span>
  * <span data-ttu-id="ef0ec-261">[Instalación del kit de herramientas de Azure para IntelliJ]</span><span class="sxs-lookup"><span data-stu-id="ef0ec-261">[Installing the Azure Toolkit for IntelliJ]</span></span>
  * <span data-ttu-id="ef0ec-262">*Creación de una aplicación web Hello World para Azure en IntelliJ (este artículo)*</span><span class="sxs-lookup"><span data-stu-id="ef0ec-262">*Create a Hello World Web App for Azure in IntelliJ (This Article)*</span></span>
  * <span data-ttu-id="ef0ec-263">[Novedades del kit de herramientas de Azure para IntelliJ]</span><span class="sxs-lookup"><span data-stu-id="ef0ec-263">[What's New in the Azure Toolkit for IntelliJ]</span></span>

<a name="see-also"></a>

## <a name="see-also"></a><span data-ttu-id="ef0ec-264">Otras referencias</span><span class="sxs-lookup"><span data-stu-id="ef0ec-264">See Also</span></span>
<span data-ttu-id="ef0ec-265">Para obtener más información sobre el uso de Azure con Java, vea el [Centro para desarrolladores de Java de Azure].</span><span class="sxs-lookup"><span data-stu-id="ef0ec-265">For more information about using Azure with Java, see the [Azure Java Developer Center].</span></span>

<span data-ttu-id="ef0ec-266">Para obtener más información sobre cómo crear aplicaciones web de Azure, consulte [Introducción a Aplicaciones web].</span><span class="sxs-lookup"><span data-stu-id="ef0ec-266">For additional information about creating Azure Web Apps, see the [Web Apps Overview].</span></span>

[!INCLUDE [app-service-web-try-app-service](../../includes/app-service-web-try-app-service.md)]

<!-- URL List -->

[Kit de herramientas de Azure para Eclipse]: ../azure-toolkit-for-eclipse.md
[kit de herramientas de Azure para IntelliJ]: ../azure-toolkit-for-intellij.md
[Creación de una aplicación web Hello World para Azure en Eclipse]: ./app-service-web-eclipse-create-hello-world-web-app.md
[Create a Hello World Web App for Azure in IntelliJ]: ./app-service-web-intellij-create-hello-world-web-app.md
[Instalación del Kit de herramientas de Azure para Eclipse]: ../azure-toolkit-for-eclipse-installation.md
[Instalación del kit de herramientas de Azure para IntelliJ]: ../azure-toolkit-for-intellij-installation.md
[Novedades del kit de herramientas de Azure para Eclipse]: ../azure-toolkit-for-eclipse-whats-new.md
[Novedades del kit de herramientas de Azure para IntelliJ]: ../azure-toolkit-for-intellij-whats-new.md

[Centro para desarrolladores de Java de Azure]: https://azure.microsoft.com/develop/java/
[Introducción a Aplicaciones web]: ./app-service-web-overview.md
[Apache Tomcat]: http://tomcat.apache.org/
[Jetty]: http://www.eclipse.org/jetty/

<!-- IMG List -->

[01]: ./media/app-service-web-intellij-create-hello-world-web-app/01-Web-Page.png
[02]: ./media/app-service-web-intellij-create-hello-world-web-app/02-File-New-Project.png
[03a]: ./media/app-service-web-intellij-create-hello-world-web-app/03-New-Project-Dialog.png
[03b]: ./media/app-service-web-intellij-create-hello-world-web-app/03-New-Project-SDK-Dialog.png
[04]: ./media/app-service-web-intellij-create-hello-world-web-app/04-New-Project-Dialog.png
[05a]: ./media/app-service-web-intellij-create-hello-world-web-app/05-Open-Module-Settings.png
[05b]: ./media/app-service-web-intellij-create-hello-world-web-app/05-Project-Structure-Dialog.png
[05c]: ./media/app-service-web-intellij-create-hello-world-web-app/05-Open-Index-Page.png
[06]: ./media/app-service-web-intellij-create-hello-world-web-app/06-Azure-Publish-Context-Menu.png
[07]: ./media/app-service-web-intellij-create-hello-world-web-app/07-Azure-Log-In-Dialog.png
[08]: ./media/app-service-web-intellij-create-hello-world-web-app/08-Manage-Subscriptions.png
[09]: ./media/app-service-web-intellij-create-hello-world-web-app/09-App-Containers.png
[10]: ./media/app-service-web-intellij-create-hello-world-web-app/10-Add-App-Container.png
[11a]: ./media/app-service-web-intellij-create-hello-world-web-app/11-New-App-Container.png
[11b]: ./media/app-service-web-intellij-create-hello-world-web-app/11-New-App-Container-JDK-Tab.png
[12]: ./media/app-service-web-intellij-create-hello-world-web-app/12-New-Resource-Group.png
[13]: ./media/app-service-web-intellij-create-hello-world-web-app/13-New-App-Service-Plan.png
[14]: ./media/app-service-web-intellij-create-hello-world-web-app/14-New-App-Container.png
[15]: ./media/app-service-web-intellij-create-hello-world-web-app/15-Deploy-To-Azure.png
[16]: ./media/app-service-web-intellij-create-hello-world-web-app/16-Progress-Indicator.png
[17]: ./media/app-service-web-intellij-create-hello-world-web-app/17-Browse-Web-App.png
[18]: ./media/app-service-web-intellij-create-hello-world-web-app/18-Stop-Web-App.png
