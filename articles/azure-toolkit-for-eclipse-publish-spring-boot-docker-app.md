---
title: "aaaPublish como un contenedor de Docker mediante el uso de una aplicación de arranque de primavera hello Azure Toolkit for Eclipse | Documentos de Microsoft"
description: "Obtenga información acerca de cómo toopublish una tooMicrosoft de aplicación web Azure como un contenedor de Docker mediante el uso de hello Azure Toolkit for Eclipse."
services: 
documentationcenter: java
author: rmcmurray
manager: erikre
editor: 
ms.assetid: 
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: multiple
ms.devlang: Java
ms.topic: article
ms.date: 06/21/2017
ms.author: robmcm
ms.openlocfilehash: 29390c49c339a1ebb87cb3951b21cea01c0da15f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="publish-a-spring-boot-app-as-a-docker-container-by-using-hello-azure-toolkit-for-eclipse"></a><span data-ttu-id="26013-103">Publicar una aplicación de arranque de primavera como un contenedor de Docker mediante el uso de hello Kit de herramientas de Azure para Eclipse</span><span class="sxs-lookup"><span data-stu-id="26013-103">Publish a Spring Boot app as a Docker container by using hello Azure Toolkit for Eclipse</span></span>

<span data-ttu-id="26013-104">Hola [Spring Framework] es una solución de código abierto que ayuda a los desarrolladores de Java a crear aplicaciones de nivel empresarial.</span><span class="sxs-lookup"><span data-stu-id="26013-104">hello [Spring Framework] is an open-source solution that helps Java developers create enterprise-level applications.</span></span> <span data-ttu-id="26013-105">Uno de los proyectos de más populares de Hola que se compila sobre dicha plataforma es [arranque primavera], que proporciona un enfoque simplificado para crear aplicaciones de Java de independiente.</span><span class="sxs-lookup"><span data-stu-id="26013-105">One of hello more-popular projects that is built on top of that platform is [Spring Boot], which provides a simplified approach for creating standalone Java applications.</span></span>

<span data-ttu-id="26013-106">[Docker] es una solución de código abierto que ayuda a los desarrolladores automatizar la implementación de hello, ajuste de escala y administración de las aplicaciones que se ejecutan en contenedores.</span><span class="sxs-lookup"><span data-stu-id="26013-106">[Docker] is an open-source solution that helps developers automate hello deployment, scaling, and management of their applications that are running in containers.</span></span>

<span data-ttu-id="26013-107">Este tutorial le guiará por hello pasos toodeploy una aplicación Spring arranque como un tooMicrosoft de contenedor de Docker Azure mediante el uso de hello Kit de herramientas de Azure para Eclipse.</span><span class="sxs-lookup"><span data-stu-id="26013-107">This tutorial walks you through hello steps toodeploy a Spring Boot application as a Docker container tooMicrosoft Azure by using hello Azure Toolkit for Eclipse.</span></span>

[!INCLUDE [azure-toolkit-for-eclipse-prerequisites](../includes/azure-toolkit-for-eclipse-prerequisites.md)]

## <a name="clone-hello-default-spring-boot-docker-repository"></a><span data-ttu-id="26013-108">Clonar el repositorio de Docker de arranque de primavera de hello predeterminado</span><span class="sxs-lookup"><span data-stu-id="26013-108">Clone hello default Spring Boot Docker repository</span></span>

### <a name="import-hello-public-repository"></a><span data-ttu-id="26013-109">Repositorio público de Hola de importación</span><span class="sxs-lookup"><span data-stu-id="26013-109">Import hello public repository</span></span>

<span data-ttu-id="26013-110">Hello pasos siguientes le guían a través de clonación ordenador de hello Spring arranque Docker repositorio tooyour utilizando IntelliJ.</span><span class="sxs-lookup"><span data-stu-id="26013-110">hello following steps walk you through cloning hello Spring Boot Docker repository tooyour local computer by using IntelliJ.</span></span> <span data-ttu-id="26013-111">Si desea toouse una línea de comandos, consulte [implementar una aplicación de arranque del muelle en Linux en el servicio de contenedor de Azure][Deploy Spring Boot on Linux in ACS].</span><span class="sxs-lookup"><span data-stu-id="26013-111">If you want toouse a command line, see [Deploy a Spring Boot application on Linux in Azure Container Service][Deploy Spring Boot on Linux in ACS].</span></span>

1. <span data-ttu-id="26013-112">Abra Eclipse.</span><span class="sxs-lookup"><span data-stu-id="26013-112">Open Eclipse.</span></span>

1. <span data-ttu-id="26013-113">Haga clic en **Archivo** > **Importar**.</span><span class="sxs-lookup"><span data-stu-id="26013-113">Click **File** > **Import**.</span></span>

   ![Menú de importación de archivo][CL01]

1. <span data-ttu-id="26013-115">Cuando Hola **importación** abre el cuadro de diálogo:</span><span class="sxs-lookup"><span data-stu-id="26013-115">When hello **Import** dialog box opens:</span></span>

   <span data-ttu-id="26013-116">a.</span><span class="sxs-lookup"><span data-stu-id="26013-116">a.</span></span> <span data-ttu-id="26013-117">Expanda **GIT**.</span><span class="sxs-lookup"><span data-stu-id="26013-117">Expand **Git**.</span></span>

   <span data-ttu-id="26013-118">b.</span><span class="sxs-lookup"><span data-stu-id="26013-118">b.</span></span> <span data-ttu-id="26013-119">Seleccione **Proyectos de GIT**.</span><span class="sxs-lookup"><span data-stu-id="26013-119">Select **Projects from Git**.</span></span>
   
   <span data-ttu-id="26013-120">c.</span><span class="sxs-lookup"><span data-stu-id="26013-120">c.</span></span> <span data-ttu-id="26013-121">Haga clic en **Siguiente**.</span><span class="sxs-lookup"><span data-stu-id="26013-121">Click **Next**.</span></span>

   ![Cuadro de diálogo de importación][CL02]

1. <span data-ttu-id="26013-123">En hello **Seleccionar origen de repositorio** página:</span><span class="sxs-lookup"><span data-stu-id="26013-123">On hello **Select Repository Source** page:</span></span>

   <span data-ttu-id="26013-124">a.</span><span class="sxs-lookup"><span data-stu-id="26013-124">a.</span></span> <span data-ttu-id="26013-125">Seleccione **Clonar URI**.</span><span class="sxs-lookup"><span data-stu-id="26013-125">Select **Clone URI**.</span></span>
   
   <span data-ttu-id="26013-126">b.</span><span class="sxs-lookup"><span data-stu-id="26013-126">b.</span></span> <span data-ttu-id="26013-127">Haga clic en **Siguiente**.</span><span class="sxs-lookup"><span data-stu-id="26013-127">Click **Next**.</span></span>

   ![Página Seleccionar origen del repositorio][CL03]

1. <span data-ttu-id="26013-129">En hello **repositorio de código fuente Git** página:</span><span class="sxs-lookup"><span data-stu-id="26013-129">On hello **Source Git Repository** page:</span></span>

   <span data-ttu-id="26013-130">a.</span><span class="sxs-lookup"><span data-stu-id="26013-130">a.</span></span> <span data-ttu-id="26013-131">Para **URI**, escriba `https://github.com/spring-guides/gs-spring-boot-docker.git`.</span><span class="sxs-lookup"><span data-stu-id="26013-131">For **URI**, enter `https://github.com/spring-guides/gs-spring-boot-docker.git`.</span></span> <span data-ttu-id="26013-132">Este paso debe rellenar de forma automática hello **Host** y **ruta del repositorio** campos con hello corregir valores.</span><span class="sxs-lookup"><span data-stu-id="26013-132">This step should automatically populate hello **Host** and **Repository path** fields with hello correct values.</span></span>
   
   <span data-ttu-id="26013-133">b.</span><span class="sxs-lookup"><span data-stu-id="26013-133">b.</span></span> <span data-ttu-id="26013-134">repositorio de arranque de primavera de Hello es pública, por lo que no debería ser necesario tooenter el nombre de usuario de Git y la contraseña.</span><span class="sxs-lookup"><span data-stu-id="26013-134">hello Spring Boot repository is public, so you should not have tooenter your Git username and password.</span></span>
   
   <span data-ttu-id="26013-135">c.</span><span class="sxs-lookup"><span data-stu-id="26013-135">c.</span></span> <span data-ttu-id="26013-136">Haga clic en **Siguiente**.</span><span class="sxs-lookup"><span data-stu-id="26013-136">Click **Next**.</span></span>

   ![Página Repositorio de GIT de origen][CL04]

1. <span data-ttu-id="26013-138">En hello **selección rama** página, haga clic en **siguiente**.</span><span class="sxs-lookup"><span data-stu-id="26013-138">On hello **Branch Selection** page, click **Next**.</span></span>

   ![Página Selección de rama][CL05]

1. <span data-ttu-id="26013-140">En hello **destino Local** página:</span><span class="sxs-lookup"><span data-stu-id="26013-140">On hello **Local Destination** page:</span></span>

   <span data-ttu-id="26013-141">a.</span><span class="sxs-lookup"><span data-stu-id="26013-141">a.</span></span> <span data-ttu-id="26013-142">Especifique Hola carpeta local donde desea que el repositorio local.</span><span class="sxs-lookup"><span data-stu-id="26013-142">Specify hello local folder where you want your local repo.</span></span>
   
   <span data-ttu-id="26013-143">b.</span><span class="sxs-lookup"><span data-stu-id="26013-143">b.</span></span> <span data-ttu-id="26013-144">Haga clic en **Siguiente**.</span><span class="sxs-lookup"><span data-stu-id="26013-144">Click **Next**.</span></span>

   ![Página Destino local][CL06]

1. <span data-ttu-id="26013-146">En hello **seleccionar un toouse del Asistente para importar proyectos** página:</span><span class="sxs-lookup"><span data-stu-id="26013-146">On hello **Select a wizard toouse for importing projects** page:</span></span>

   <span data-ttu-id="26013-147">a.</span><span class="sxs-lookup"><span data-stu-id="26013-147">a.</span></span> <span data-ttu-id="26013-148">Seleccione **Import as a general project** (Importar como proyecto general).</span><span class="sxs-lookup"><span data-stu-id="26013-148">Select **Import as a general project**.</span></span>
   
   <span data-ttu-id="26013-149">b.</span><span class="sxs-lookup"><span data-stu-id="26013-149">b.</span></span> <span data-ttu-id="26013-150">Haga clic en **Siguiente**.</span><span class="sxs-lookup"><span data-stu-id="26013-150">Click **Next**.</span></span>

   ![Página "Seleccionar una toouse del Asistente para importar proyectos"][CL07]

1. <span data-ttu-id="26013-152">En hello **importar proyectos** página:</span><span class="sxs-lookup"><span data-stu-id="26013-152">On hello **Import Projects** page:</span></span>

   <span data-ttu-id="26013-153">a.</span><span class="sxs-lookup"><span data-stu-id="26013-153">a.</span></span> <span data-ttu-id="26013-154">Especifique el nombre del proyecto.</span><span class="sxs-lookup"><span data-stu-id="26013-154">Specify your project name.</span></span>
   
   <span data-ttu-id="26013-155">b.</span><span class="sxs-lookup"><span data-stu-id="26013-155">b.</span></span> <span data-ttu-id="26013-156">Haga clic en **Finalizar**</span><span class="sxs-lookup"><span data-stu-id="26013-156">Click **Finish**.</span></span>

   ![Página Importar proyectos][CL08]

1. <span data-ttu-id="26013-158">Al repositorio de Hola se clona correctamente, verá todos los archivos de hello enumerados en Eclipse.</span><span class="sxs-lookup"><span data-stu-id="26013-158">When hello repository is cloned successfully, you see all hello files listed in Eclipse.</span></span>

   ![Repositorio local][CL09]

### <a name="create-a-maven-project-from-your-local-repository"></a><span data-ttu-id="26013-160">Crear un proyecto de Maven desde el repositorio local</span><span class="sxs-lookup"><span data-stu-id="26013-160">Create a Maven project from your local repository</span></span>

<span data-ttu-id="26013-161">repositorio de Docker de arranque de primavera de Hello contiene un proyecto de Maven completado, que va a utilizar para este tutorial.</span><span class="sxs-lookup"><span data-stu-id="26013-161">hello Spring Boot Docker repository contains a completed Maven project, which you will use for this tutorial.</span></span> 

1. <span data-ttu-id="26013-162">Haga clic en **Archivo** > **Importar**.</span><span class="sxs-lookup"><span data-stu-id="26013-162">Click **File** > **Import**.</span></span>

   ![Importar en el menú archivo de hello, comando][CL01]

1. <span data-ttu-id="26013-164">Cuando Hola **importación** abre el cuadro de diálogo:</span><span class="sxs-lookup"><span data-stu-id="26013-164">When hello **Import** dialog box opens:</span></span>

   <span data-ttu-id="26013-165">a.</span><span class="sxs-lookup"><span data-stu-id="26013-165">a.</span></span> <span data-ttu-id="26013-166">Expanda **Maven**.</span><span class="sxs-lookup"><span data-stu-id="26013-166">Expand **Maven**.</span></span>
   
   <span data-ttu-id="26013-167">b.</span><span class="sxs-lookup"><span data-stu-id="26013-167">b.</span></span> <span data-ttu-id="26013-168">Seleccione **Existing Maven Projects** (Proyectos existentes de Maven).</span><span class="sxs-lookup"><span data-stu-id="26013-168">Select **Existing Maven Projects**.</span></span>
   
   <span data-ttu-id="26013-169">c.</span><span class="sxs-lookup"><span data-stu-id="26013-169">c.</span></span> <span data-ttu-id="26013-170">Haga clic en **Siguiente**.</span><span class="sxs-lookup"><span data-stu-id="26013-170">Click **Next**.</span></span>

   ![Cuadro de diálogo de importación][MV01]

1. <span data-ttu-id="26013-172">En hello **proyectos de Maven** página:</span><span class="sxs-lookup"><span data-stu-id="26013-172">On hello **Maven Projects** page:</span></span>

   <span data-ttu-id="26013-173">a.</span><span class="sxs-lookup"><span data-stu-id="26013-173">a.</span></span> <span data-ttu-id="26013-174">Para **directorio raíz**, especifique hello **completa** carpeta en el repositorio local.</span><span class="sxs-lookup"><span data-stu-id="26013-174">For **Root Directory**, specify hello **complete** folder in your local repository.</span></span>
   
   <span data-ttu-id="26013-175">b.</span><span class="sxs-lookup"><span data-stu-id="26013-175">b.</span></span> <span data-ttu-id="26013-176">Expanda hello **avanzadas** sección y escriba un nombre personalizado para **plantilla del nombre**.</span><span class="sxs-lookup"><span data-stu-id="26013-176">Expand hello **Advanced** section, and enter a custom name for **Name template**.</span></span>
   
   <span data-ttu-id="26013-177">c.</span><span class="sxs-lookup"><span data-stu-id="26013-177">c.</span></span> <span data-ttu-id="26013-178">Cuadro Seleccione Hola Hola **pom.xml** archivo de proyecto de Hola.</span><span class="sxs-lookup"><span data-stu-id="26013-178">Select hello box for hello **pom.xml** file in hello project.</span></span>
   
   <span data-ttu-id="26013-179">d.</span><span class="sxs-lookup"><span data-stu-id="26013-179">d.</span></span> <span data-ttu-id="26013-180">Haga clic en **Finalizar**</span><span class="sxs-lookup"><span data-stu-id="26013-180">Click **Finish**.</span></span>

   ![Página de proyectos de Maven][MV02]

1. <span data-ttu-id="26013-182">Cuando se abre el proyecto de Maven de hello correctamente, verá un segundo proyecto aparece en Eclipse.</span><span class="sxs-lookup"><span data-stu-id="26013-182">When hello Maven project is opened successfully, you see a second project listed in Eclipse.</span></span>

   ![Proyecto local de Maven][MV03]

## <a name="build-your-spring-boot-app-by-using-maven"></a><span data-ttu-id="26013-184">Crear una aplicación Spring Boot mediante Maven</span><span class="sxs-lookup"><span data-stu-id="26013-184">Build your Spring Boot app by using Maven</span></span>

1. <span data-ttu-id="26013-185">En el Explorador de proyectos de Eclipse hello, seleccione el proyecto de Maven de Hola.</span><span class="sxs-lookup"><span data-stu-id="26013-185">In hello Eclipse Project Explorer, select hello Maven project.</span></span>

1. <span data-ttu-id="26013-186">Haga clic en **Ejecutar** > **Ejecutar como** > **Compilación de Maven**.</span><span class="sxs-lookup"><span data-stu-id="26013-186">Click **Run** > **Run As** > **Maven build**.</span></span>

   ![Toorun de comandos como la compilación de Maven][BU01]

1. <span data-ttu-id="26013-188">Cuando la aplicación se compila correctamente, ventana de la consola de hello muestra el estado de saludo.</span><span class="sxs-lookup"><span data-stu-id="26013-188">When your application is successfully built, hello console window shows hello status.</span></span>

   ![Compilación correcta de Maven][BU02]

## <a name="publish-your-web-app-tooazure-by-using-a-docker-container"></a><span data-ttu-id="26013-190">Publicar su tooAzure de aplicación web mediante el uso de un contenedor de Docker</span><span class="sxs-lookup"><span data-stu-id="26013-190">Publish your web app tooAzure by using a Docker container</span></span>

1. <span data-ttu-id="26013-191">En el Explorador de proyectos de Eclipse hello, seleccione el proyecto de Maven de Hola.</span><span class="sxs-lookup"><span data-stu-id="26013-191">In hello Eclipse Project Explorer, select hello Maven project.</span></span>

1. <span data-ttu-id="26013-192">Haga clic en hello Azure **publicar** menú y, a continuación, haga clic en **publicar como contenedor de Docker**.</span><span class="sxs-lookup"><span data-stu-id="26013-192">Click hello Azure **Publish** menu, and then click **Publish as Docker Container**.</span></span>

   ![Comando Publish as Docker Container (Publicar como contenedor de Docker)][PU01]

1. <span data-ttu-id="26013-194">Cuando Hola **implementación de contenedor de Docker en Azure** aparece el cuadro de diálogo:</span><span class="sxs-lookup"><span data-stu-id="26013-194">When hello **Deploying Docker Container on Azure** dialog box appears:</span></span>

   <span data-ttu-id="26013-195">a.</span><span class="sxs-lookup"><span data-stu-id="26013-195">a.</span></span> <span data-ttu-id="26013-196">Escriba un nombre de imagen de Docker personalizado.</span><span class="sxs-lookup"><span data-stu-id="26013-196">Enter a custom Docker image name.</span></span>
   
   <span data-ttu-id="26013-197">b.</span><span class="sxs-lookup"><span data-stu-id="26013-197">b.</span></span> <span data-ttu-id="26013-198">Para **artefacto toodeploy**, especifique toohello de ruta de acceso de hello **gs spring arranque docker 0.1.0** acaba de compilar el archivo.</span><span class="sxs-lookup"><span data-stu-id="26013-198">For **Artifact toodeploy**, specify hello path toohello **gs-spring-boot-docker-0.1.0.jar** file you just built.</span></span>

   ![Especificar opciones de Docker][PU02]

   <span data-ttu-id="26013-200">Se muestran todos los hosts de Docker existentes.</span><span class="sxs-lookup"><span data-stu-id="26013-200">Any existing Docker hosts are displayed.</span></span> 

1. <span data-ttu-id="26013-201">Si elige toodeploy tooan de host existente, puede omitir toostep 5.</span><span class="sxs-lookup"><span data-stu-id="26013-201">If you choose toodeploy tooan existing host, you can skip toostep 5.</span></span> <span data-ttu-id="26013-202">En caso contrario, utilice Hola siguiendo los pasos toocreate un host:</span><span class="sxs-lookup"><span data-stu-id="26013-202">Otherwise, use hello following steps toocreate a host:</span></span>

   <span data-ttu-id="26013-203">a.</span><span class="sxs-lookup"><span data-stu-id="26013-203">a.</span></span> <span data-ttu-id="26013-204">Haga clic en **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="26013-204">Click **Add**.</span></span>

      ![Agregar un nuevo host de Docker][PU03]

   <span data-ttu-id="26013-206">b.</span><span class="sxs-lookup"><span data-stu-id="26013-206">b.</span></span> <span data-ttu-id="26013-207">Cuando Hola **crear un Host Docker** aparece el cuadro de diálogo, puede elegir los valores predeterminados de tooaccept Hola o puede especificar cualquier configuración personalizada para el nuevo host Docker.</span><span class="sxs-lookup"><span data-stu-id="26013-207">When hello **Create Docker Host** dialog box appears, you can choose tooaccept hello defaults, or you can specify any custom settings for your new Docker host.</span></span> <span data-ttu-id="26013-208">(Para obtener descripciones detalladas de hello distintas configuraciones, vea [publicar una aplicación web como un contenedor de Docker mediante hello Azure Toolkit para IntelliJ][Publish Container with Azure Toolkit].) Haga clic en **siguiente** cuando se especifica qué toouse de configuración.</span><span class="sxs-lookup"><span data-stu-id="26013-208">(For detailed descriptions of hello various settings, see [Publish a web app as a Docker container by using hello Azure Toolkit for IntelliJ][Publish Container with Azure Toolkit].) Click **Next** when you have specified which settings toouse.</span></span>

      ![Especificar las opciones de host de Docker][PU04]

   <span data-ttu-id="26013-210">c.</span><span class="sxs-lookup"><span data-stu-id="26013-210">c.</span></span> <span data-ttu-id="26013-211">Puede elegir las credenciales de inicio de sesión existentes toouse desde un almacén de claves de Azure, o puede elegir tooenter nuevas credenciales de inicio de sesión de Docker.</span><span class="sxs-lookup"><span data-stu-id="26013-211">You can choose toouse existing login credentials from an Azure key vault, or you can choose tooenter new Docker login credentials.</span></span> <span data-ttu-id="26013-212">Haga clic en **Finalizar** cuando haya especificado las opciones.</span><span class="sxs-lookup"><span data-stu-id="26013-212">Click **Finish** when you have specified your options.</span></span>

      ![Especificar credenciales del host de Docker][PU05]

1. <span data-ttu-id="26013-214">Seleccione el host de Docker y, después, haga clic en **Siguiente**.</span><span class="sxs-lookup"><span data-stu-id="26013-214">Select your Docker host, and then click **Next**.</span></span>

   ![Seleccione toouse de host de Docker][PU06]

1. <span data-ttu-id="26013-216">En la última página de Hola de hello **implementación de contenedor de Docker en Azure** cuadro de diálogo, especifique Hola siguientes opciones:</span><span class="sxs-lookup"><span data-stu-id="26013-216">On hello last page of hello **Deploying Docker Container on Azure** dialog box, specify hello following options:</span></span>

   <span data-ttu-id="26013-217">a.</span><span class="sxs-lookup"><span data-stu-id="26013-217">a.</span></span> <span data-ttu-id="26013-218">Puede elegir un nombre personalizado para el contenedor de Hola que va a hospedar el contenedor de Docker toospecify, o puede aceptar predeterminado Hola.</span><span class="sxs-lookup"><span data-stu-id="26013-218">You can choose toospecify a custom name for hello container that will host your Docker container, or you can accept hello default.</span></span>

   <span data-ttu-id="26013-219">b.</span><span class="sxs-lookup"><span data-stu-id="26013-219">b.</span></span> <span data-ttu-id="26013-220">Escriba los puertos TCP hello para el host de docker mediante Hola según la sintaxis: *[puerto externo]*:*[puerto interno]*.</span><span class="sxs-lookup"><span data-stu-id="26013-220">Enter hello TCP ports for your docker host by using hello following syntax: *[external port]*:*[internal port]*.</span></span> <span data-ttu-id="26013-221">Por ejemplo, **80:8080** especifica un puerto externo del 80 y el puerto Hola predeterminado de arranque Spring interno de 8080.</span><span class="sxs-lookup"><span data-stu-id="26013-221">For example, **80:8080** specifies an external port of 80 and hello default internal Spring Boot port of 8080.</span></span>
   
      <span data-ttu-id="26013-222">Si ha personalizado el puerto interno (por ejemplo, editando el archivo de hello application.yml), necesitará toospecify número de puerto de Hola para hello toooccur de enrutamiento correcto en Azure.</span><span class="sxs-lookup"><span data-stu-id="26013-222">If you have customized your internal port (for example, by editing hello application.yml file), you need toospecify hello port number for hello correct routing toooccur in Azure.</span></span>

   <span data-ttu-id="26013-223">c.</span><span class="sxs-lookup"><span data-stu-id="26013-223">c.</span></span> <span data-ttu-id="26013-224">Después de configurar estas opciones, haga clic en **Finalizar**.</span><span class="sxs-lookup"><span data-stu-id="26013-224">After you configure these options, click **Finish**.</span></span>

   ![Implementar un contenedor de Docker en Azure][PU07]

1. <span data-ttu-id="26013-226">Cuando hello Azure Toolkit ha terminado de publicar, Hola muestra de registro de actividad de Azure **publicada** para el estado de saludo.</span><span class="sxs-lookup"><span data-stu-id="26013-226">When hello Azure Toolkit has finished publishing, hello Azure Activity Log displays **Published** for hello status.</span></span>

   ![Host de Docker correctamente implementado][PU08]

## <a name="next-steps"></a><span data-ttu-id="26013-228">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="26013-228">Next steps</span></span>

[!INCLUDE [azure-toolkit-additional-resources](../includes/azure-toolkit-additional-resources.md)]

<!-- URL List -->

[Azure Management Portal]: http://go.microsoft.com/fwlink/?LinkID=512959
[Deploy Spring Boot on Linux in ACS]:container-service/kubernetes/container-service-deploy-spring-boot-app-on-linux.md
[Docker]: https://www.docker.com/
[Publish Container with Azure Toolkit]: ./azure-toolkit-for-intellij-publish-as-docker-container.md
[arranque primavera]: http://projects.spring.io/spring-boot/
[Spring Framework]: https://spring.io/

<!-- IMG List -->

[CL01]: ./media/azure-toolkit-for-eclipse-publish-spring-boot-docker-app/CL01.png
[CL02]: ./media/azure-toolkit-for-eclipse-publish-spring-boot-docker-app/CL02.png
[CL03]: ./media/azure-toolkit-for-eclipse-publish-spring-boot-docker-app/CL03.png
[CL04]: ./media/azure-toolkit-for-eclipse-publish-spring-boot-docker-app/CL04.png
[CL05]: ./media/azure-toolkit-for-eclipse-publish-spring-boot-docker-app/CL05.png
[CL06]: ./media/azure-toolkit-for-eclipse-publish-spring-boot-docker-app/CL06.png
[CL07]: ./media/azure-toolkit-for-eclipse-publish-spring-boot-docker-app/CL07.png
[CL08]: ./media/azure-toolkit-for-eclipse-publish-spring-boot-docker-app/CL08.png
[CL09]: ./media/azure-toolkit-for-eclipse-publish-spring-boot-docker-app/CL09.png

[MV01]: ./media/azure-toolkit-for-eclipse-publish-spring-boot-docker-app/MV01.png
[MV02]: ./media/azure-toolkit-for-eclipse-publish-spring-boot-docker-app/MV02.png
[MV03]: ./media/azure-toolkit-for-eclipse-publish-spring-boot-docker-app/MV03.png

[BU01]: ./media/azure-toolkit-for-eclipse-publish-spring-boot-docker-app/BU01.png
[BU02]: ./media/azure-toolkit-for-eclipse-publish-spring-boot-docker-app/BU02.png

[PU01]: ./media/azure-toolkit-for-eclipse-publish-spring-boot-docker-app/PU01.png
[PU02]: ./media/azure-toolkit-for-eclipse-publish-spring-boot-docker-app/PU02.png
[PU03]: ./media/azure-toolkit-for-eclipse-publish-spring-boot-docker-app/PU03.png
[PU04]: ./media/azure-toolkit-for-eclipse-publish-spring-boot-docker-app/PU04.png
[PU05]: ./media/azure-toolkit-for-eclipse-publish-spring-boot-docker-app/PU05.png
[PU06]: ./media/azure-toolkit-for-eclipse-publish-spring-boot-docker-app/PU06.png
[PU07]: ./media/azure-toolkit-for-eclipse-publish-spring-boot-docker-app/PU07.png
[PU08]: ./media/azure-toolkit-for-eclipse-publish-spring-boot-docker-app/PU08.png
