---
title: "una aplicación web de Azure básico en IntelliJ aaaCreate | Documentos de Microsoft"
description: "Este tutorial muestra cómo toouse hello Azure Toolkit para IntelliJ toocreate una aplicación de Hello World Web de Azure."
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
ms.openlocfilehash: 4667497213cac3ddf754d164e614c809f338cce5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-basic-azure-web-app-in-intellij"></a><span data-ttu-id="7c20e-103">Creación de una aplicación web básica de Azure en IntelliJ</span><span class="sxs-lookup"><span data-stu-id="7c20e-103">Create a basic Azure web app in IntelliJ</span></span>
<span data-ttu-id="7c20e-104">Este tutorial se muestra cómo toocreate e implementar un tooAzure de aplicación Hello World básico como una aplicación Web mediante hello [Azure Toolkit for IntelliJ].</span><span class="sxs-lookup"><span data-stu-id="7c20e-104">This tutorial shows how toocreate and deploy a basic Hello World application tooAzure as a Web App by using hello [Azure Toolkit for IntelliJ].</span></span> <span data-ttu-id="7c20e-105">Para que sea más sencillo, se muestra un ejemplo básico de JSP, pero los pasos similares se aplicarían en el caso de un servlet Java en lo que respecta a la implementación de Azure.</span><span class="sxs-lookup"><span data-stu-id="7c20e-105">A basic JSP example is shown for simplicity, but similar steps would be appropriate for a Java servlet, as far as Azure deployment is concerned.</span></span>

<span data-ttu-id="7c20e-106">Cuando se haya completado este tutorial, la aplicación tendrá un aspecto similar toohello siguientes ilustración al verlo en un explorador web:</span><span class="sxs-lookup"><span data-stu-id="7c20e-106">When you have completed this tutorial, your application will look similar toohello following illustration when you view it in a web browser:</span></span>

![Página web de ejemplo][01]

## <a name="prerequisites"></a><span data-ttu-id="7c20e-108">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="7c20e-108">Prerequisites</span></span>
* <span data-ttu-id="7c20e-109">Un kit para desarrolladores de Java (JDK) de la versión 1.8 o superior.</span><span class="sxs-lookup"><span data-stu-id="7c20e-109">A Java Developer Kit (JDK), v 1.8 or later.</span></span>
* <span data-ttu-id="7c20e-110">IntelliJ IDEA Ultimate Edition.</span><span class="sxs-lookup"><span data-stu-id="7c20e-110">IntelliJ IDEA Ultimate Edition.</span></span> <span data-ttu-id="7c20e-111">Se puede descargar desde <https://www.jetbrains.com/idea/download/index.html>.</span><span class="sxs-lookup"><span data-stu-id="7c20e-111">This can be downloaded from <https://www.jetbrains.com/idea/download/index.html>.</span></span>
* <span data-ttu-id="7c20e-112">Una distribución de un servidor web basado en Java o un servidor de aplicaciones, como [Apache Tomcat] o [Jetty].</span><span class="sxs-lookup"><span data-stu-id="7c20e-112">A distribution of a Java-based web server or application server, such as [Apache Tomcat] or [Jetty].</span></span>
* <span data-ttu-id="7c20e-113">Una suscripción a Azure, que se puede adquirir en <https://azure.microsoft.com/free/> o <http://azure.microsoft.com/pricing/purchase-options/>.</span><span class="sxs-lookup"><span data-stu-id="7c20e-113">An Azure subscription, which can be acquired from <https://azure.microsoft.com/free/> or <http://azure.microsoft.com/pricing/purchase-options/>.</span></span>
* <span data-ttu-id="7c20e-114">Hola [Azure Toolkit for IntelliJ].</span><span class="sxs-lookup"><span data-stu-id="7c20e-114">hello [Azure Toolkit for IntelliJ].</span></span> <span data-ttu-id="7c20e-115">Para obtener información acerca de cómo instalar hello Azure Toolkit, vea [instalar hello Azure Toolkit for IntelliJ].</span><span class="sxs-lookup"><span data-stu-id="7c20e-115">For information about installing hello Azure Toolkit, see [Installing hello Azure Toolkit for IntelliJ].</span></span>

## <a name="toocreate-a-hello-world-application"></a><span data-ttu-id="7c20e-116">toocreate una aplicación Hello World</span><span class="sxs-lookup"><span data-stu-id="7c20e-116">toocreate a Hello World application</span></span>
<span data-ttu-id="7c20e-117">En primer lugar, empezaremos con la creación de un proyecto Java.</span><span class="sxs-lookup"><span data-stu-id="7c20e-117">First, we'll start off with creating a Java project.</span></span>

1. <span data-ttu-id="7c20e-118">Iniciar IntelliJ y haga clic en hello **archivo** menú, a continuación, haga clic en **New**y, a continuación, haga clic en **proyecto**.</span><span class="sxs-lookup"><span data-stu-id="7c20e-118">Start IntelliJ and click hello **File** menu, then click **New**, and then click **Project**.</span></span>
   
    ![Archivo Nuevo Proyecto][02]
2. <span data-ttu-id="7c20e-120">En el cuadro de diálogo nuevo proyecto de hello, seleccione **Java**, a continuación, **aplicación Web**y, a continuación, haga clic en **New** tooadd un SDK de Project.</span><span class="sxs-lookup"><span data-stu-id="7c20e-120">In hello New Project dialog box, select **Java**, then **Web Application**, and then click **New** tooadd a Project SDK.</span></span>
   
    ![Cuadro de diálogo Nuevo proyecto][03a]
   
3. <span data-ttu-id="7c20e-122">Hola seleccionar el directorio particular de cuadro de diálogo JDK, seleccione Hola carpeta donde está instalado el JDK y, a continuación, haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="7c20e-122">In hello Select Home Directory for JDK dialog box, select hello folder where your JDK is installed, and then click **OK**.</span></span> <span data-ttu-id="7c20e-123">Haga clic en **siguiente** en toocontinue del cuadro de diálogo de hello nuevo proyecto.</span><span class="sxs-lookup"><span data-stu-id="7c20e-123">Click **Next** in hello New Project dialog box toocontinue.</span></span>
   
    ![Especificación del directorio de inicio de JDK][03b]
4. <span data-ttu-id="7c20e-125">Para fines de este tutorial, denomine el proyecto de hello **Java aplicación Web en Azure**y, a continuación, haga clic en **finalizar**.</span><span class="sxs-lookup"><span data-stu-id="7c20e-125">For purposes of this tutorial, name hello project **Java-Web-App-On-Azure**, and then click **Finish**.</span></span>
   
    ![Cuadro de diálogo Nuevo proyecto][04]
5. <span data-ttu-id="7c20e-127">En la vista del explorador de proyectos de IntelliJ, expanda **Java-Web-App-On-Azure**, después expanda **web** y, luego, haga doble clic en **index.jsp**.</span><span class="sxs-lookup"><span data-stu-id="7c20e-127">Within IntelliJ's Project Explorer view, expand **Java-Web-App-On-Azure**, then expand **web**, and then double-click **index.jsp**.</span></span>
   
    ![Abrir página de índice][05c]
6. <span data-ttu-id="7c20e-129">Cuando se abre el archivo index.jsp en IntelliJ, agregar en la presentación del texto toodynamically **Hello World!**</span><span class="sxs-lookup"><span data-stu-id="7c20e-129">When your index.jsp file opens in IntelliJ, add in text toodynamically display **Hello World!**</span></span> <span data-ttu-id="7c20e-130">dentro de hello existente `<body>` elemento.</span><span class="sxs-lookup"><span data-stu-id="7c20e-130">within hello existing `<body>` element.</span></span> <span data-ttu-id="7c20e-131">Su actualizada `<body>` contenido debe parecerse al siguiente ejemplo de Hola:</span><span class="sxs-lookup"><span data-stu-id="7c20e-131">Your updated `<body>` content should resemble hello following example:</span></span>
   
    `<body><b><% out.println("Hello World!"); %></b></body>` 
7. <span data-ttu-id="7c20e-132">Guarde el archivo index.jsp.</span><span class="sxs-lookup"><span data-stu-id="7c20e-132">Save index.jsp.</span></span>

## <a name="toodeploy-your-application-tooan-azure-web-app-container"></a><span data-ttu-id="7c20e-133">toodeploy su tooan aplicación contenedor de aplicación Web de Azure</span><span class="sxs-lookup"><span data-stu-id="7c20e-133">toodeploy your application tooan Azure Web App Container</span></span>
<span data-ttu-id="7c20e-134">Hay varias maneras, por lo que puede implementar un tooAzure de aplicación web de Java.</span><span class="sxs-lookup"><span data-stu-id="7c20e-134">There are several ways by which you can deploy a Java web application tooAzure.</span></span> <span data-ttu-id="7c20e-135">Este tutorial describe uno de hello más sencilla: la aplicación será implementado tooan contenedor de aplicación Web de Azure: no se necesitan ningún tipo de proyecto especiales ni herramientas adicionales.</span><span class="sxs-lookup"><span data-stu-id="7c20e-135">This tutorial describes one of hello simplest: your application will be deployed tooan Azure Web App Container - no special project type nor additional tools are needed.</span></span> <span data-ttu-id="7c20e-136">software de contenedor de web JDK y Hola Hola se proporcionarán automáticamente con Azure, así que no hay ninguna necesidad de tooupload su propio; todo lo que necesita es la aplicación Web de Java.</span><span class="sxs-lookup"><span data-stu-id="7c20e-136">hello JDK and hello web container software will be provided for you by Azure, so there is no need tooupload your own; all you need is your Java Web App.</span></span> <span data-ttu-id="7c20e-137">Como resultado, el proceso de publicación de hello para la aplicación tardará a segundos, minutos no.</span><span class="sxs-lookup"><span data-stu-id="7c20e-137">As a result, hello publishing process for your application will take seconds, not minutes.</span></span>

<span data-ttu-id="7c20e-138">Antes de publicar la aplicación, primero debe tooconfigure su configuración para el módulo.</span><span class="sxs-lookup"><span data-stu-id="7c20e-138">Before you publish your application, you first need tooconfigure your module settings.</span></span> <span data-ttu-id="7c20e-139">toodo por lo tanto, use Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="7c20e-139">toodo so, use hello following steps:</span></span>

1. <span data-ttu-id="7c20e-140">En el Explorador de proyectos del IntelliJ, haga clic en hello **Java aplicación Web en Azure** proyecto.</span><span class="sxs-lookup"><span data-stu-id="7c20e-140">In IntelliJ's Project Explorer, right-click hello **Java-Web-App-On-Azure** project.</span></span> <span data-ttu-id="7c20e-141">Cuando aparezca el menú contextual de hello, haga clic en **configuración para abrir el módulo**.</span><span class="sxs-lookup"><span data-stu-id="7c20e-141">When hello context menu appears, click **Open Module Settings**.</span></span>

    ![Abrir configuración del módulo][05a]
2. <span data-ttu-id="7c20e-143">Cuando aparezca el cuadro de diálogo de estructura del proyecto de hello:</span><span class="sxs-lookup"><span data-stu-id="7c20e-143">When hello Project Structure dialog box appears:</span></span>

   <span data-ttu-id="7c20e-144">a.</span><span class="sxs-lookup"><span data-stu-id="7c20e-144">a.</span></span> <span data-ttu-id="7c20e-145">Haga clic en **artefactos** en la lista de Hola de **configuración del proyecto**.</span><span class="sxs-lookup"><span data-stu-id="7c20e-145">Click **Artifacts** in hello list of **Project Settings**.</span></span>
   <span data-ttu-id="7c20e-146">b.</span><span class="sxs-lookup"><span data-stu-id="7c20e-146">b.</span></span> <span data-ttu-id="7c20e-147">Cambiar el nombre del artefacto de Hola Hola **nombre** cuadro para que no contenga espacios en blanco o caracteres especiales; esto es necesario ya que se utilizará el nombre de Hola Hola identificador uniforme de recursos (URI).</span><span class="sxs-lookup"><span data-stu-id="7c20e-147">Change hello artifact name in hello **Name** box so that it doesn't contain whitespace or special characters; this is necessary since hello name will be used in hello Uniform Resource Identifier (URI).</span></span>
   <span data-ttu-id="7c20e-148">c.</span><span class="sxs-lookup"><span data-stu-id="7c20e-148">c.</span></span> <span data-ttu-id="7c20e-149">Hola de cambio **tipo** demasiado**aplicación Web: archivo**.</span><span class="sxs-lookup"><span data-stu-id="7c20e-149">Change hello **Type** too**Web Application: Archive**.</span></span>
   <span data-ttu-id="7c20e-150">d.</span><span class="sxs-lookup"><span data-stu-id="7c20e-150">d.</span></span> <span data-ttu-id="7c20e-151">Haga clic en **Aceptar** cuadro de diálogo de tooclose Hola estructura del proyecto.</span><span class="sxs-lookup"><span data-stu-id="7c20e-151">Click **OK** tooclose hello Project Structure dialog box.</span></span>

    ![Abrir configuración del módulo][05b]

<span data-ttu-id="7c20e-153">Cuando se ha configurado el módulo, puede publicar su aplicación tooAzure mediante Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="7c20e-153">When you have configured your module settings, you can publish your application tooAzure by using hello following steps:</span></span>

1. <span data-ttu-id="7c20e-154">En el Explorador de proyectos del IntelliJ, haga clic en hello **Java aplicación Web en Azure** proyecto.</span><span class="sxs-lookup"><span data-stu-id="7c20e-154">In IntelliJ's Project Explorer, right-click hello **Java-Web-App-On-Azure** project.</span></span> <span data-ttu-id="7c20e-155">Cuando aparezca el menú contextual de hello, seleccione **Azure**y, a continuación, haga clic en **publicar como aplicación Web de Azure...**</span><span class="sxs-lookup"><span data-stu-id="7c20e-155">When hello context menu appears, select **Azure**, and then click **Publish as Azure Web App...**</span></span>
   
    ![Menú contextual de publicación de Azure][06]
2. <span data-ttu-id="7c20e-157">Si todavía no está suscrito a Azure desde IntelliJ, es posible que toosign solicitada en su cuenta de Azure.</span><span class="sxs-lookup"><span data-stu-id="7c20e-157">If you have not already signed into Azure from IntelliJ, you will be prompted toosign into your Azure account.</span></span> <span data-ttu-id="7c20e-158">(Si tiene varias cuentas de Azure, algunos de los mensajes de Hola durante el inicio de sesión de hello en proceso pueden ser se muestra más de una vez, incluso si aparecen toobe Hola igual.</span><span class="sxs-lookup"><span data-stu-id="7c20e-158">(If you have multiple Azure accounts, some of hello prompts during hello sign in process may be shown more than once, even if they appear toobe hello same.</span></span> <span data-ttu-id="7c20e-159">Cuando esto sucede, continúe con el inicio de sesión de toofollow hello en instrucciones).</span><span class="sxs-lookup"><span data-stu-id="7c20e-159">When this happens, continue toofollow hello sign in instructions.)</span></span>
   
    ![Cuadro de diálogo de inicio de sesión de Azure][07]
3. <span data-ttu-id="7c20e-161">Después de iniciar sesión en su cuenta de Azure, Hola **administrar suscripciones** cuadro de diálogo mostrará una lista de suscripciones que están asociados con sus credenciales.</span><span class="sxs-lookup"><span data-stu-id="7c20e-161">After you have successfully signed into your Azure account, hello **Manage Subscriptions** dialog box will display a list of subscriptions that are associated with your credentials.</span></span> <span data-ttu-id="7c20e-162">(Si hay varias suscripciones aparece y desea toowork con sólo un subconjunto específico de ellos, si lo desea puede desactivar suscripciones de Hola que no desea toouse). Cuando haya seleccionado las suscripciones, haga clic en **Cerrar**.</span><span class="sxs-lookup"><span data-stu-id="7c20e-162">(If there are multiple subscriptions listed and you want toowork with only a specific subset of them, you may optionally uncheck hello subscriptions you don't want toouse.) When you have selected your subscriptions, click **Close**.</span></span>
   
    ![Administrar suscripciones][08]
4. <span data-ttu-id="7c20e-164">Cuando Hola **implementar tooAzure contenedor de la aplicación Web** aparece el cuadro de diálogo, se mostrará a los contenedores de la aplicación Web que creó anteriormente; si no ha creado los contenedores, lista de hello estará vacío.</span><span class="sxs-lookup"><span data-stu-id="7c20e-164">When hello **Deploy tooAzure Web App Container** dialog box appears, it will display any Web App containers that you have previously created; if you have not created any containers, hello list will be empty.</span></span>
   
    ![Contenedores de aplicaciones][09]
5. <span data-ttu-id="7c20e-166">Si no ha creado un contenedor de aplicación Web de Azure antes o si desea que toopublish su tooa nuevo contenedor de aplicación, use Hola pasos.</span><span class="sxs-lookup"><span data-stu-id="7c20e-166">If you have not created an Azure Web App Container before, or if you would like toopublish your application tooa new container, use hello following steps.</span></span> <span data-ttu-id="7c20e-167">En caso contrario, seleccione un contenedor de la aplicación Web existente y omitir toostep 6 a continuación.</span><span class="sxs-lookup"><span data-stu-id="7c20e-167">Otherwise, select an existing Web App Container and skip toostep 6 below.</span></span>
   
   1. <span data-ttu-id="7c20e-168">Haga clic en **+**</span><span class="sxs-lookup"><span data-stu-id="7c20e-168">Click **+**</span></span>
      
       ![Agregar contenedor de aplicaciones][10]
   2. <span data-ttu-id="7c20e-170">Hola **nuevo contenedor de la aplicación Web** se mostrará el cuadro de diálogo, que será utilizado para hello junto varios pasos.</span><span class="sxs-lookup"><span data-stu-id="7c20e-170">hello **New Web App Container** dialog box will be displayed, which will be used for hello next several steps.</span></span>
      
       ![Nuevo contenedor de aplicaciones][11a]
   3. <span data-ttu-id="7c20e-172">Escriba un **etiqueta DNS** para el contenedor de la aplicación Web; esto formará etiqueta DNS de hoja de Hola de dirección URL del host de hello para la aplicación web en Azure.</span><span class="sxs-lookup"><span data-stu-id="7c20e-172">Enter a **DNS Label** for your Web App Container; this will form hello leaf DNS label of hello host URL for your web application in Azure.</span></span> <span data-ttu-id="7c20e-173">Tenga en cuenta ese nombre hello debe estar disponibles y cumplir los requisitos de nombres de aplicación Web de tooAzure.</span><span class="sxs-lookup"><span data-stu-id="7c20e-173">Note that hello name must be available and conform tooAzure Web App naming requirements.</span></span>
   4. <span data-ttu-id="7c20e-174">Hola **contenedor Web** menú desplegable, el software adecuado de Hola seleccione para la aplicación.</span><span class="sxs-lookup"><span data-stu-id="7c20e-174">In hello **Web Container** drop-down menu, select hello appropriate software for your application.</span></span>
      
       <span data-ttu-id="7c20e-175">Actualmente, puede elegir entre Tomcat 8, Tomcat 7 o Jetty 9.</span><span class="sxs-lookup"><span data-stu-id="7c20e-175">Currently, you can choose from Tomcat 8, Tomcat 7 or Jetty 9.</span></span> <span data-ttu-id="7c20e-176">Una distribución recientes de software de hello seleccionado se proporcionarán con Azure y se ejecutará en una distribución reciente de JDK 8 creada por Oracle y proporcionado por Azure.</span><span class="sxs-lookup"><span data-stu-id="7c20e-176">A recent distribution of hello selected software will be provided by Azure, and it will run on a recent distribution of JDK 8 created by Oracle and provided by Azure.</span></span>
   5. <span data-ttu-id="7c20e-177">Hola **suscripción** menú desplegable, suscripción Hola seleccione desea toouse para esta implementación.</span><span class="sxs-lookup"><span data-stu-id="7c20e-177">In hello **Subscription** drop-down menu, select hello subscription you want toouse for this deployment.</span></span>
   6. <span data-ttu-id="7c20e-178">Hola **grupo de recursos** menú desplegable, seleccione Hola grupo de recursos con el que desea tooassociate la aplicación Web.</span><span class="sxs-lookup"><span data-stu-id="7c20e-178">In hello **Resource Group** drop-down menu, select hello Resource Group with which you want tooassociate your Web App.</span></span> <span data-ttu-id="7c20e-179">(Grupos de recursos de azure permiten toogroup recursos relacionados juntos para que, por ejemplo, pueden eliminarse juntos).</span><span class="sxs-lookup"><span data-stu-id="7c20e-179">(Azure Resource Groups allow you toogroup related resources together so that, for example, they can be deleted together.)</span></span>
      
       <span data-ttu-id="7c20e-180">Puede seleccionar un grupo de recursos existente (si tiene alguno) y omitir toostep g a continuación, o si uso Hola sigue los pasos toocreate un nuevo grupo de recursos:</span><span class="sxs-lookup"><span data-stu-id="7c20e-180">You can select an existing Resource Group (if you have any) and skip toostep g below, or use hello following steps toocreate a new Resource Group:</span></span>
      
      * <span data-ttu-id="7c20e-181">Seleccione  **&lt; &lt; crear nuevo grupo de recursos &gt; &gt;**  en hello **grupo de recursos** menú desplegable.</span><span class="sxs-lookup"><span data-stu-id="7c20e-181">Select **&lt;&lt; Create new Resource Group &gt;&gt;** in hello **Resource Group** drop-down menu.</span></span>
      * <span data-ttu-id="7c20e-182">Hola **nuevo grupo de recursos** se mostrará el cuadro de diálogo:</span><span class="sxs-lookup"><span data-stu-id="7c20e-182">hello **New Resource Group** dialog box will be displayed:</span></span>
        
          ![Nuevo grupo de recursos][12]
      * <span data-ttu-id="7c20e-184">Hola Hola **nombre** cuadro de texto, especifique un nombre para el nuevo grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="7c20e-184">In hello hello **Name** textbox, specify a name for your new Resource Group.</span></span>
      * <span data-ttu-id="7c20e-185">Hola Hola **región** menú desplegable, ubicación para el grupo de recursos del centro de datos de Azure adecuada Hola select.</span><span class="sxs-lookup"><span data-stu-id="7c20e-185">In hello hello **Region** drop-down menu, select hello appropriate Azure data center location for your Resource Group.</span></span>
      * <span data-ttu-id="7c20e-186">Haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="7c20e-186">Click **OK**.</span></span>
   7. <span data-ttu-id="7c20e-187">Hola **Plan de servicio de aplicaciones** menú desplegable muestra planes de servicio de aplicación Hola que están asociados con hello grupo de recursos que ha seleccionado.</span><span class="sxs-lookup"><span data-stu-id="7c20e-187">hello **App Service Plan** drop-down menu lists hello app service plans that are associated with hello Resource Group that you selected.</span></span> <span data-ttu-id="7c20e-188">(Un Plan de servicio de aplicaciones especifica información como ubicación de saludo de la aplicación Web, Hola plan de tarifa y tamaño de instancia de proceso de Hola.</span><span class="sxs-lookup"><span data-stu-id="7c20e-188">(An App Service Plan specifies information such as hello location of your Web App, hello pricing tier and hello compute instance size.</span></span> <span data-ttu-id="7c20e-189">Un único plan de App Service se puede usar para varias aplicaciones web, motivo por el cual se mantiene independiente de una implementación específica de aplicaciones web.</span><span class="sxs-lookup"><span data-stu-id="7c20e-189">A single App Service Plan can be used for multiple Web Apps, which is why it is maintained separately from a specific Web App deployment.)</span></span>
      
       <span data-ttu-id="7c20e-190">Puede seleccionar un Plan de servicio de aplicación existente (si tiene alguno) y omitir toostep h siguiente o usar hello después toocreate pasos un nuevo Plan de servicio de aplicación:</span><span class="sxs-lookup"><span data-stu-id="7c20e-190">You can select an existing App Service Plan (if you have any) and skip toostep h below, or use hello following steps toocreate a new App Service Plan:</span></span>
      
      * <span data-ttu-id="7c20e-191">Seleccione  **&lt; &lt; crear nuevo Plan de servicio de aplicación &gt; &gt;**  en hello **Plan de servicio de aplicaciones** menú desplegable.</span><span class="sxs-lookup"><span data-stu-id="7c20e-191">Select **&lt;&lt; Create new App Service Plan &gt;&gt;** in hello **App Service Plan** drop-down menu.</span></span>
      * <span data-ttu-id="7c20e-192">Hola **nuevo Plan de servicio de aplicación** se mostrará el cuadro de diálogo:</span><span class="sxs-lookup"><span data-stu-id="7c20e-192">hello **New App Service Plan** dialog box will be displayed:</span></span>
        
          ![Nuevo plan de App Service][13]
      * <span data-ttu-id="7c20e-194">Hola Hola **nombre** cuadro de texto, especifique un nombre para el nuevo Plan de servicio de aplicación.</span><span class="sxs-lookup"><span data-stu-id="7c20e-194">In hello hello **Name** textbox, specify a name for your new App Service Plan.</span></span>
      * <span data-ttu-id="7c20e-195">Hola Hola **ubicación** menú desplegable, ubicación para el plan de hello del centro de datos de Azure adecuada Hola select.</span><span class="sxs-lookup"><span data-stu-id="7c20e-195">In hello hello **Location** drop-down menu, select hello appropriate Azure data center location for hello plan.</span></span>
      * <span data-ttu-id="7c20e-196">Hola Hola **tarifa** menú desplegable, seleccione Hola adecuado de precios para el plan de Hola.</span><span class="sxs-lookup"><span data-stu-id="7c20e-196">In hello hello **Pricing Tier** drop-down menu, select hello appropriate pricing for hello plan.</span></span> <span data-ttu-id="7c20e-197">Con fines de prueba, puede elegir **Gratis**.</span><span class="sxs-lookup"><span data-stu-id="7c20e-197">For testing purposes you can choose **Free**.</span></span>
      * <span data-ttu-id="7c20e-198">Hola Hola **tamaño de la instancia** menú desplegable, el tamaño de la instancia adecuada de hello seleccione plan Hola.</span><span class="sxs-lookup"><span data-stu-id="7c20e-198">In hello hello **Instance Size** drop-down menu, select hello appropriate instance size for hello plan.</span></span> <span data-ttu-id="7c20e-199">Con fines de prueba, puede elegir **Pequeño**.</span><span class="sxs-lookup"><span data-stu-id="7c20e-199">For testing purposes you can choose **Small**.</span></span>
      * <span data-ttu-id="7c20e-200">Haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="7c20e-200">Click **OK**.</span></span>
   8. <span data-ttu-id="7c20e-201">(Opcional) De forma predeterminada, una distribución reciente de Java 8 se implementarán automáticamente como la JVM por contenedor de aplicaciones web de Azure tooyour.</span><span class="sxs-lookup"><span data-stu-id="7c20e-201">(Optional) By default, a recent distribution of Java 8 will be automatically deployed as your JVM by Azure tooyour web app container.</span></span> <span data-ttu-id="7c20e-202">Sin embargo, puede seleccionar una versión diferente y la distribución de hello JVM.</span><span class="sxs-lookup"><span data-stu-id="7c20e-202">However, you can select a different version and distribution of hello JVM.</span></span> <span data-ttu-id="7c20e-203">toodo por lo tanto, use Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="7c20e-203">toodo so, use hello following steps:</span></span>
      
      * <span data-ttu-id="7c20e-204">Haga clic en hello **JDK** ficha hello **nuevo contenedor de la aplicación Web** cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="7c20e-204">Click hello **JDK** tab in hello **New Web App Container** dialog box.</span></span>
      * <span data-ttu-id="7c20e-205">Puede elegir una de las siguientes opciones de hello:</span><span class="sxs-lookup"><span data-stu-id="7c20e-205">You can choose from one of hello following options:</span></span>
        
        * <span data-ttu-id="7c20e-206">Implementación predeterminada de hello JDK que se ofrece a través de Azure</span><span class="sxs-lookup"><span data-stu-id="7c20e-206">Deploy hello default JDK which is offered by Azure</span></span>
        * <span data-ttu-id="7c20e-207">Implementar un JDK de terceros de lista desplegable de JDK adicionales que están disponibles en Azure</span><span class="sxs-lookup"><span data-stu-id="7c20e-207">Deploy a 3rd party JDK from a drop-down list of additional JDKs which are available on Azure</span></span>
        * <span data-ttu-id="7c20e-208">Implementar un JDK personalizado, que debe estar empaquetado en un archivo ZIP y bien estar disponible públicamente o en su cuenta de Azure Storage</span><span class="sxs-lookup"><span data-stu-id="7c20e-208">Deploy a custom JDK, which must be packaged as a ZIP file and either publicly available or in your Azure storage account</span></span>
        
        ![Pestaña JDK de nuevo contenedor de aplicaciones][11b]
   9. <span data-ttu-id="7c20e-210">Una vez que haya completado todas de hello por encima de los pasos, cuadro de diálogo nuevo contenedor de la aplicación Web de hello debe ser similar a Hola siguiente ilustración:</span><span class="sxs-lookup"><span data-stu-id="7c20e-210">Once you have completed all of hello above steps, hello New Web App Container dialog box should resemble hello following illustration:</span></span>
      
       ![Nuevo contenedor de aplicaciones][14]
   10. <span data-ttu-id="7c20e-212">Haga clic en **Aceptar** creación de hello toocomplete de su nuevo contenedor de aplicación Web.</span><span class="sxs-lookup"><span data-stu-id="7c20e-212">Click **OK** toocomplete hello creation of your new Web App container.</span></span>
       
        <span data-ttu-id="7c20e-213">Actualiza espera unos segundos para obtener lista de Hola de toobe de contenedores de aplicación Web de Hola y el contenedor de la aplicación web recién creado debería estar ahora seleccionado en la lista de Hola.</span><span class="sxs-lookup"><span data-stu-id="7c20e-213">Wait a few seconds for hello list of hello Web App containers toobe refreshed, and your newly-created web app container should now be selected in hello list.</span></span>
6. <span data-ttu-id="7c20e-214">Ya estás implementación inicial de hello listo toocomplete de tooAzure de su aplicación Web; Haga clic en **Aceptar** toodeploy su toohello de aplicación Java seleccionado contenedor de la aplicación Web.</span><span class="sxs-lookup"><span data-stu-id="7c20e-214">You are now ready toocomplete hello initial deployment of your Web App tooAzure; click **OK** toodeploy your Java application toohello selected Web App container.</span></span> <span data-ttu-id="7c20e-215">De forma predeterminada, la aplicación se implementará como un subdirectorio del servidor de aplicaciones de Hola.</span><span class="sxs-lookup"><span data-stu-id="7c20e-215">By default, your application will be deployed as a subdirectory of hello application server.</span></span> <span data-ttu-id="7c20e-216">Si desea toobe implementado como aplicación de la raíz de hello, compruebe hello **implementar tooroot** casilla antes de hacer clic **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="7c20e-216">If you want it toobe deployed as hello root application, check hello **Deploy tooroot** checkbox before clicking **OK**.</span></span>
   
    ![Implementar tooAzure][15]
7. <span data-ttu-id="7c20e-218">A continuación, debería ver Hola **Azure Activity Log** vista, que indicará el estado de implementación de saludo de la aplicación Web.</span><span class="sxs-lookup"><span data-stu-id="7c20e-218">Next, you should see hello **Azure Activity Log** view, which will indicate hello deployment status of your Web App.</span></span>
   
    ![Indicador de progreso][16]
   
    <span data-ttu-id="7c20e-220">proceso de Hello de la implementación de la aplicación Web tooAzure tardará unos pocos segundos toocomplete.</span><span class="sxs-lookup"><span data-stu-id="7c20e-220">hello process of deploying your Web App tooAzure should take only a few seconds toocomplete.</span></span> <span data-ttu-id="7c20e-221">Cuando esté listo aplicación, verá un vínculo denominado **publicada** en hello **estado** columna.</span><span class="sxs-lookup"><span data-stu-id="7c20e-221">When your application ready, you will see a link named **Published** in hello **Status** column.</span></span> <span data-ttu-id="7c20e-222">Al hacer clic en el vínculo de hello, le permitirán página principal de la aplicación Web tooyour implementado, o puede usar pasos Hola Hola después de la aplicación web de sección toobrowse tooyour.</span><span class="sxs-lookup"><span data-stu-id="7c20e-222">When you click hello link, it will take you tooyour deployed Web App's home page, or you can use hello steps in hello following section toobrowse tooyour web app.</span></span>

## <a name="browsing-tooyour-web-app-on-azure"></a><span data-ttu-id="7c20e-223">Exploración tooyour aplicación Web en Azure</span><span class="sxs-lookup"><span data-stu-id="7c20e-223">Browsing tooyour Web App on Azure</span></span>
<span data-ttu-id="7c20e-224">toobrowse tooyour aplicación Web en Azure, puede usar hello **Azure explorador** vista.</span><span class="sxs-lookup"><span data-stu-id="7c20e-224">toobrowse tooyour Web App on Azure, you can use hello **Azure Explorer** view.</span></span>

<span data-ttu-id="7c20e-225">Si hello **explorador Azure** vista ya no está abierta, puede abrirlo haciendo clic, a continuación, en **vista** IntelliJ, a continuación, haga clic en **las ventanas de herramientas**y, a continuación, haga clic en  **Servicio explorador**.</span><span class="sxs-lookup"><span data-stu-id="7c20e-225">If hello **Azure Explorer** view is not already open, you can open it by clicking then **View** menu in IntelliJ, then click **Tool Windows**, and then click **Service Explorer**.</span></span> <span data-ttu-id="7c20e-226">Si anteriormente no han iniciado sesión, se le pedirá que toodo así.</span><span class="sxs-lookup"><span data-stu-id="7c20e-226">If you have not previously logged in, it will prompt you toodo so.</span></span>

<span data-ttu-id="7c20e-227">Cuando Hola **explorador Azure** se muestra la vista, use siga estas tooyour de toobrowse pasos aplicación Web:</span><span class="sxs-lookup"><span data-stu-id="7c20e-227">When hello **Azure Explorer** view is displayed, use follow these steps toobrowse tooyour Web App:</span></span> 

1. <span data-ttu-id="7c20e-228">Expanda hello **Azure** nodo.</span><span class="sxs-lookup"><span data-stu-id="7c20e-228">Expand hello **Azure** node.</span></span>
2. <span data-ttu-id="7c20e-229">Expanda hello **aplicaciones Web** nodo.</span><span class="sxs-lookup"><span data-stu-id="7c20e-229">Expand hello **Web Apps** node.</span></span> 
3. <span data-ttu-id="7c20e-230">Menú contextual Hola había deseado aplicación Web.</span><span class="sxs-lookup"><span data-stu-id="7c20e-230">Right-click hello desired Web App.</span></span>
4. <span data-ttu-id="7c20e-231">Cuando aparezca el menú contextual de hello, haga clic en **abrir en el explorador**.</span><span class="sxs-lookup"><span data-stu-id="7c20e-231">When hello context menu appears, click **Open in Browser**.</span></span>
   
    ![Examinar una aplicación web][17]

## <a name="updating-your-web-app"></a><span data-ttu-id="7c20e-233">Actualización de la aplicación web</span><span class="sxs-lookup"><span data-stu-id="7c20e-233">Updating your web app</span></span>
<span data-ttu-id="7c20e-234">Actualizar una aplicación web de Azure existente es un proceso rápido y sencillo, y tiene dos opciones para ello:</span><span class="sxs-lookup"><span data-stu-id="7c20e-234">Updating an existing running Azure Web App is a quick and easy process, and you have two options for updating:</span></span>

* <span data-ttu-id="7c20e-235">Puede actualizar la implementación de Hola de una aplicación Web de Java existente.</span><span class="sxs-lookup"><span data-stu-id="7c20e-235">You can update hello deployment of an existing Java Web App.</span></span>
* <span data-ttu-id="7c20e-236">Puede publicar un toohello adicional de aplicación de Java mismo contenedor de la aplicación Web.</span><span class="sxs-lookup"><span data-stu-id="7c20e-236">You can publish an additional Java application toohello same Web App Container.</span></span>

<span data-ttu-id="7c20e-237">En cualquier caso, el proceso de hello es idéntico y tarda solo unos segundos:</span><span class="sxs-lookup"><span data-stu-id="7c20e-237">In either case, hello process is identical and takes only a few seconds:</span></span>

1. <span data-ttu-id="7c20e-238">En el Explorador de proyectos de hello IntelliJ, haga clic en aplicación de Java de hello desee tooupdate o agregar tooan existente contenedor de la aplicación Web.</span><span class="sxs-lookup"><span data-stu-id="7c20e-238">In hello IntelliJ project explorer, right-click hello Java application you want tooupdate or add tooan existing Web App Container.</span></span>
2. <span data-ttu-id="7c20e-239">Cuando aparezca el menú contextual de hello, seleccione **Azure** y, a continuación, **publicar como aplicación Web de Azure...**</span><span class="sxs-lookup"><span data-stu-id="7c20e-239">When hello context menu appears, select **Azure** and then **Publish as Azure Web App...**</span></span>
3. <span data-ttu-id="7c20e-240">Puesto que ya ha iniciado sesión anteriormente, verá una lista de contenedores de aplicaciones web existentes.</span><span class="sxs-lookup"><span data-stu-id="7c20e-240">Since you have already logged in previously, you will see a list of your existing Web App containers.</span></span> <span data-ttu-id="7c20e-241">Seleccione Hola uno desea toopublish o volver a publicar el Java aplicación tooand, haga clic **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="7c20e-241">Select hello one you want toopublish or re-publish your Java application tooand click **OK**.</span></span>

<span data-ttu-id="7c20e-242">Hola unos segundos más tarde, **Azure Activity Log** vista mostrará la implementación actualizada como **publicada** y será capaz de tooverify la aplicación actualizada en un explorador web.</span><span class="sxs-lookup"><span data-stu-id="7c20e-242">A few seconds later, hello **Azure Activity Log** view will show your updated deployment as **Published** and you will be able tooverify your updated application in a web browser.</span></span>

## <a name="starting-stopping-or-restarting-an-existing-web-app"></a><span data-ttu-id="7c20e-243">Inicio, detención o reinicio de una aplicación web existente</span><span class="sxs-lookup"><span data-stu-id="7c20e-243">Starting, stopping, or restarting an existing web app</span></span>
<span data-ttu-id="7c20e-244">toostart o detener un contenedor de aplicación Web de Azure existente, (incluido todas las aplicaciones de Java de hello implementado en él), puede usar hello **Azure explorador** vista.</span><span class="sxs-lookup"><span data-stu-id="7c20e-244">toostart or stop an existing Azure Web App container, (including all hello deployed Java applications in it), you can use hello **Azure Explorer** view.</span></span>

<span data-ttu-id="7c20e-245">Si hello **explorador Azure** vista ya no está abierta, puede abrirlo haciendo clic, a continuación, en **vista** IntelliJ, a continuación, haga clic en **las ventanas de herramientas**y, a continuación, haga clic en  **Servicio explorador**.</span><span class="sxs-lookup"><span data-stu-id="7c20e-245">If hello **Azure Explorer** view is not already open, you can open it by clicking then **View** menu in IntelliJ, then click **Tool Windows**, and then click **Service Explorer**.</span></span> <span data-ttu-id="7c20e-246">Si anteriormente no han iniciado sesión, se le pedirá que toodo así.</span><span class="sxs-lookup"><span data-stu-id="7c20e-246">If you have not previously logged in, it will prompt you toodo so.</span></span>

<span data-ttu-id="7c20e-247">Cuando Hola **explorador Azure** se muestra la vista, use, siga estos pasos toostart o detener la aplicación Web:</span><span class="sxs-lookup"><span data-stu-id="7c20e-247">When hello **Azure Explorer** view is displayed, use follow these steps toostart or stop your Web App:</span></span> 

1. <span data-ttu-id="7c20e-248">Expanda hello **Azure** nodo.</span><span class="sxs-lookup"><span data-stu-id="7c20e-248">Expand hello **Azure** node.</span></span>
2. <span data-ttu-id="7c20e-249">Expanda hello **aplicaciones Web** nodo.</span><span class="sxs-lookup"><span data-stu-id="7c20e-249">Expand hello **Web Apps** node.</span></span> 
3. <span data-ttu-id="7c20e-250">Menú contextual Hola había deseado aplicación Web.</span><span class="sxs-lookup"><span data-stu-id="7c20e-250">Right-click hello desired Web App.</span></span>
4. <span data-ttu-id="7c20e-251">Cuando aparezca el menú contextual de hello, haga clic en **iniciar**, **detener**, o **reiniciar**.</span><span class="sxs-lookup"><span data-stu-id="7c20e-251">When hello context menu appears, click **Start**, **Stop**, or **Restart**.</span></span> <span data-ttu-id="7c20e-252">Tenga en cuenta que las opciones de menú de hello en contexto, por lo que solo puede detener una aplicación web en ejecución o iniciar una aplicación web que no se está ejecutando actualmente.</span><span class="sxs-lookup"><span data-stu-id="7c20e-252">Note that hello menu choices are context-aware, so you can only stop a running web app or start a web app which is not currently running.</span></span>
   
    ![Detener aplicación web][18]

## <a name="next-steps"></a><span data-ttu-id="7c20e-254">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="7c20e-254">Next Steps</span></span>
<span data-ttu-id="7c20e-255">Para obtener más información acerca de hello kits de herramientas de Azure para Java IDE, vea Hola siguientes vínculos:</span><span class="sxs-lookup"><span data-stu-id="7c20e-255">For more information about hello Azure Toolkits for Java IDEs, see hello following links:</span></span>

* <span data-ttu-id="7c20e-256">[Kit de herramientas de Azure para Eclipse]</span><span class="sxs-lookup"><span data-stu-id="7c20e-256">[Azure Toolkit for Eclipse]</span></span>
  * <span data-ttu-id="7c20e-257">[Instalar hello Azure Toolkit for Eclipse]</span><span class="sxs-lookup"><span data-stu-id="7c20e-257">[Installing hello Azure Toolkit for Eclipse]</span></span>
  * <span data-ttu-id="7c20e-258">[Creación de una aplicación web Hello World para Azure en Eclipse]</span><span class="sxs-lookup"><span data-stu-id="7c20e-258">[Create a Hello World Web App for Azure in Eclipse]</span></span>
  * <span data-ttu-id="7c20e-259">[What's New en hello Azure Toolkit for Eclipse]</span><span class="sxs-lookup"><span data-stu-id="7c20e-259">[What's New in hello Azure Toolkit for Eclipse]</span></span>
* <span data-ttu-id="7c20e-260">[Azure Toolkit for IntelliJ]</span><span class="sxs-lookup"><span data-stu-id="7c20e-260">[Azure Toolkit for IntelliJ]</span></span>
  * <span data-ttu-id="7c20e-261">[instalar hello Azure Toolkit for IntelliJ]</span><span class="sxs-lookup"><span data-stu-id="7c20e-261">[Installing hello Azure Toolkit for IntelliJ]</span></span>
  * <span data-ttu-id="7c20e-262">*Creación de una aplicación web Hello World para Azure en IntelliJ (este artículo)*</span><span class="sxs-lookup"><span data-stu-id="7c20e-262">*Create a Hello World Web App for Azure in IntelliJ (This Article)*</span></span>
  * <span data-ttu-id="7c20e-263">[What's New en hello Azure Toolkit for IntelliJ]</span><span class="sxs-lookup"><span data-stu-id="7c20e-263">[What's New in hello Azure Toolkit for IntelliJ]</span></span>

<a name="see-also"></a>

## <a name="see-also"></a><span data-ttu-id="7c20e-264">Otras referencias</span><span class="sxs-lookup"><span data-stu-id="7c20e-264">See Also</span></span>
<span data-ttu-id="7c20e-265">Para obtener más información acerca del uso de Azure con Java, vea hello [Centro para desarrolladores de Java de Azure].</span><span class="sxs-lookup"><span data-stu-id="7c20e-265">For more information about using Azure with Java, see hello [Azure Java Developer Center].</span></span>

<span data-ttu-id="7c20e-266">Para obtener información adicional acerca de cómo crear aplicaciones Web de Azure, vea hello [información general de aplicaciones Web].</span><span class="sxs-lookup"><span data-stu-id="7c20e-266">For additional information about creating Azure Web Apps, see hello [Web Apps Overview].</span></span>

[!INCLUDE [app-service-web-try-app-service](../../includes/app-service-web-try-app-service.md)]

<!-- URL List -->

[Kit de herramientas de Azure para Eclipse]: ../azure-toolkit-for-eclipse.md
[Azure Toolkit for IntelliJ]: ../azure-toolkit-for-intellij.md
[Creación de una aplicación web Hello World para Azure en Eclipse]: ./app-service-web-eclipse-create-hello-world-web-app.md
[Create a Hello World Web App for Azure in IntelliJ]: ./app-service-web-intellij-create-hello-world-web-app.md
[Instalar hello Azure Toolkit for Eclipse]: ../azure-toolkit-for-eclipse-installation.md
[instalar hello Azure Toolkit for IntelliJ]: ../azure-toolkit-for-intellij-installation.md
[What's New en hello Azure Toolkit for Eclipse]: ../azure-toolkit-for-eclipse-whats-new.md
[What's New en hello Azure Toolkit for IntelliJ]: ../azure-toolkit-for-intellij-whats-new.md

[Centro para desarrolladores de Java de Azure]: https://azure.microsoft.com/develop/java/
[información general de aplicaciones Web]: ./app-service-web-overview.md
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
