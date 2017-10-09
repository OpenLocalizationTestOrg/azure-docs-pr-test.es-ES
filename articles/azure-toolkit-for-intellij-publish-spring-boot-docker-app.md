---
title: "aaaPublish como un contenedor de Docker mediante el uso de una aplicación de arranque de primavera hello Azure Toolkit para IntelliJ | Documentos de Microsoft"
description: "Obtenga información acerca de cómo toopublish una tooMicrosoft de aplicación web Azure como un contenedor de Docker mediante el uso de Hola Kit de herramientas de Azure para IntelliJ."
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
ms.openlocfilehash: 8964cb33fd8f61a39f091633ae9074d9658232fd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="publish-a-spring-boot-app-as-a-docker-container-by-using-hello-azure-toolkit-for-intellij"></a><span data-ttu-id="3b8df-103">Publicar una aplicación Spring arranque como un contenedor de Docker mediante hello Azure Toolkit para IntelliJ</span><span class="sxs-lookup"><span data-stu-id="3b8df-103">Publish a Spring Boot app as a Docker container by using hello Azure Toolkit for IntelliJ</span></span>

<span data-ttu-id="3b8df-104">Hola [Spring Framework] es una solución de código abierto que ayuda a los desarrolladores de Java a crear aplicaciones de nivel empresarial.</span><span class="sxs-lookup"><span data-stu-id="3b8df-104">hello [Spring Framework] is an open-source solution that helps Java developers create enterprise-level applications.</span></span> <span data-ttu-id="3b8df-105">Uno de los proyectos de más populares de Hola que se compila sobre dicha plataforma es [arranque primavera], que proporciona un enfoque simplificado para crear aplicaciones de Java de independiente.</span><span class="sxs-lookup"><span data-stu-id="3b8df-105">One of hello more-popular projects that is built on top of that platform is [Spring Boot], which provides a simplified approach for creating standalone Java applications.</span></span>

<span data-ttu-id="3b8df-106">[Docker] es una solución de código abierto que ayuda a los desarrolladores automatizar la implementación de hello, ajuste de escala y administración de las aplicaciones que se ejecutan en contenedores.</span><span class="sxs-lookup"><span data-stu-id="3b8df-106">[Docker] is an open-source solution that helps developers automate hello deployment, scaling, and management of their applications that are running in containers.</span></span>

<span data-ttu-id="3b8df-107">Este tutorial le guiará por hello pasos toodeploy una aplicación Spring arranque como un tooMicrosoft de contenedor de Docker Azure mediante el uso de hello Azure Toolkit para IntelliJ.</span><span class="sxs-lookup"><span data-stu-id="3b8df-107">This tutorial walks you through hello steps toodeploy a Spring Boot application as a Docker container tooMicrosoft Azure by using hello Azure Toolkit for IntelliJ.</span></span>

[!INCLUDE [azure-toolkit-for-intellij-prerequisites](../includes/azure-toolkit-for-intellij-prerequisites.md)]

## <a name="clone-hello-default-spring-boot-docker-repo"></a><span data-ttu-id="3b8df-108">Clonar Hola predeterminado Spring arranque Docker repositorio</span><span class="sxs-lookup"><span data-stu-id="3b8df-108">Clone hello default Spring Boot Docker repo</span></span>

<span data-ttu-id="3b8df-109">Hello pasos siguientes le guían a través de clonación de repositorio de Docker de arranque de primavera de hello utilizando IntelliJ.</span><span class="sxs-lookup"><span data-stu-id="3b8df-109">hello following steps walk you through cloning hello Spring Boot Docker repo by using IntelliJ.</span></span> <span data-ttu-id="3b8df-110">Si desea toouse una línea de comandos, consulte [implementar una aplicación de arranque del muelle en Linux en el servicio de contenedor de Azure][Deploy Spring Boot on Linux in ACS].</span><span class="sxs-lookup"><span data-stu-id="3b8df-110">If you want toouse a command line, see [Deploy a Spring Boot application on Linux in Azure Container Service][Deploy Spring Boot on Linux in ACS].</span></span>

1. <span data-ttu-id="3b8df-111">Abra IntelliJ.</span><span class="sxs-lookup"><span data-stu-id="3b8df-111">Open IntelliJ.</span></span>

1. <span data-ttu-id="3b8df-112">En la pantalla de bienvenida de bienvenida, seleccione hello **GitHub** opción Hola **desproteger del Control de versiones** lista.</span><span class="sxs-lookup"><span data-stu-id="3b8df-112">On hello welcome screen, select hello **GitHub** option in hello **Check out from Version Control** list.</span></span>

   ![Opción de GitHub para el control de versiones][CL01]

1. <span data-ttu-id="3b8df-114">Escriba sus credenciales si es toolog solicitada en.</span><span class="sxs-lookup"><span data-stu-id="3b8df-114">Enter your credentials if you are prompted toolog in.</span></span>

   * <span data-ttu-id="3b8df-115">Si está usando un nombre de usuario/contraseña toolog en tooGitHub:</span><span class="sxs-lookup"><span data-stu-id="3b8df-115">If you are using a username/password toolog in tooGitHub:</span></span>

      ![Cuadro de diálogo para escribir el nombre de usuario y la contraseña de GitHub][CL02a]

   * <span data-ttu-id="3b8df-117">Si está utilizando un token toolog en tooGitHub:</span><span class="sxs-lookup"><span data-stu-id="3b8df-117">If you are using a token toolog in tooGitHub:</span></span>

      ![Cuadro de diálogo para especificar un token de GitHub][CL02b]

1. <span data-ttu-id="3b8df-119">Escriba **https://github.com/spring-guides/gs-spring-boot-docker.git** para la dirección URL del repositorio de hello, especifique la ruta de acceso local y la información de la carpeta y, a continuación, haga clic en **clon**.</span><span class="sxs-lookup"><span data-stu-id="3b8df-119">Enter **https://github.com/spring-guides/gs-spring-boot-docker.git** for hello repo URL, specify your local path and folder information, and then click **Clone**.</span></span>

   ![Cuadro de diálogo Clonar repositorio][CL03]

1. <span data-ttu-id="3b8df-121">Cuando se le pide un proyecto IntelliJ, seleccione toocreate **No**.</span><span class="sxs-lookup"><span data-stu-id="3b8df-121">When you're prompted toocreate an IntelliJ project, select **No**.</span></span>

   ![Rechazar toocreate un proyecto IntelliJ][CL04]

1. <span data-ttu-id="3b8df-123">En la página de bienvenida de hello, haga clic en **Importar proyecto**.</span><span class="sxs-lookup"><span data-stu-id="3b8df-123">On hello welcome page, click **Import Project**.</span></span>

   ![Selección de Importar proyecto][CL05]

1. <span data-ttu-id="3b8df-125">Buscar ruta de acceso de Hola donde clonó repositorio de arranque de primavera de hello, seleccione hello **completa** carpeta bajo la raíz de hello y, a continuación, haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="3b8df-125">Locate hello path where you cloned hello Spring Boot repo, select hello **complete** folder under hello root, and then click **OK**.</span></span>

   ![Seleccionar una carpeta para la importación][CL06]

1. <span data-ttu-id="3b8df-127">Cuando se le pida, seleccione **Create project from existing sources** (Crear proyecto a partir de orígenes existentes).</span><span class="sxs-lookup"><span data-stu-id="3b8df-127">When you're prompted, select **Create project from existing sources**.</span></span>

   ![Opción toocreate un proyecto a partir de orígenes existentes][CL07]

1. <span data-ttu-id="3b8df-129">Especifique el nombre del proyecto o acepte el predeterminado de hello, compruebe toohello de ruta de acceso correcta de hello **completa** carpeta y, a continuación, haga clic en **siguiente**.</span><span class="sxs-lookup"><span data-stu-id="3b8df-129">Specify your project name or accept hello default, verify hello correct path toohello **complete** folder, and then click **Next**.</span></span>

   ![Especifique el nombre del proyecto de Hola][CL08]

1. <span data-ttu-id="3b8df-131">Personalice los directorios para importar y haga clic en **Next** (Siguiente).</span><span class="sxs-lookup"><span data-stu-id="3b8df-131">Customize any directories for importing, and then click **Next**.</span></span>

   ![Elegir directorios][CL09]

1. <span data-ttu-id="3b8df-133">Revise Hola bibliotecas tooimport y, a continuación, haga clic en **siguiente**.</span><span class="sxs-lookup"><span data-stu-id="3b8df-133">Review hello libraries tooimport, and then click **Next**.</span></span>

   ![Revisar bibliotecas de proyecto][CL10]

1. <span data-ttu-id="3b8df-135">Revise la estructura del módulo de hello y, a continuación, haga clic en **siguiente**.</span><span class="sxs-lookup"><span data-stu-id="3b8df-135">Review hello module structure, and then click **Next**.</span></span>

   ![Revisar la estructura del módulo][CL11]

1. <span data-ttu-id="3b8df-137">Especifique el JDK y, después, haga clic en **Next** (Siguiente).</span><span class="sxs-lookup"><span data-stu-id="3b8df-137">Specify your JDK, and then click **Next**.</span></span>

   ![Especificar un JDK][CL12]

1. <span data-ttu-id="3b8df-139">Haga clic en **Finalizar**</span><span class="sxs-lookup"><span data-stu-id="3b8df-139">Click **Finish**.</span></span>

   ![Botón Finalizar][CL13]

<span data-ttu-id="3b8df-141">IntelliJ importa la aplicación de arranque de primavera de hello como un proyecto y muestra la estructura de hello cuando ha finalizado la importación de Hola.</span><span class="sxs-lookup"><span data-stu-id="3b8df-141">IntelliJ imports hello Spring Boot app as a project and displays hello structure when hello import has finished.</span></span>

![Aplicación Spring Boot en IntelliJ][CL14]

## <a name="build-your-spring-boot-app"></a><span data-ttu-id="3b8df-143">Crear una aplicación Spring Boot</span><span class="sxs-lookup"><span data-stu-id="3b8df-143">Build your Spring Boot app</span></span>

### <a name="build-hello-app-by-using-hello-maven-pom"></a><span data-ttu-id="3b8df-144">Compilar la aplicación hello mediante hello Maven POM</span><span class="sxs-lookup"><span data-stu-id="3b8df-144">Build hello app by using hello Maven POM</span></span>

1. <span data-ttu-id="3b8df-145">Abrir ventana de herramientas de hello Maven si no está ya abierto.</span><span class="sxs-lookup"><span data-stu-id="3b8df-145">Open hello Maven tool window if it is not already opened.</span></span> <span data-ttu-id="3b8df-146">Haga clic en **Vista** > **Ventanas de herramientas** > **Proyectos de Maven**.</span><span class="sxs-lookup"><span data-stu-id="3b8df-146">Click **View** > **Tool Windows** > **Maven Projects**.</span></span>

   ![Comandos Ventanas de herramientas y Proyectos de Maven][BU01]

1. <span data-ttu-id="3b8df-148">En la ventana de herramientas de Maven hello, haga clic en **paquete** y seleccione **ejecutar la compilación de Maven**.</span><span class="sxs-lookup"><span data-stu-id="3b8df-148">In hello Maven tool window, right-click **package** and select **Run Maven Build**.</span></span> <span data-ttu-id="3b8df-149">(Si el proyecto de Maven no se muestran automáticamente, haga clic en hello **, vuelva a importar** icono en la barra de herramientas de hello Maven.)</span><span class="sxs-lookup"><span data-stu-id="3b8df-149">(If your Maven project does not show up automatically, click hello **Reimport** icon on hello Maven toolbar.)</span></span>

   ![Comando Ejecutar la compilación de Maven][BU02]

1. <span data-ttu-id="3b8df-151">IntelliJ debería mostrar un mensaje **COMPILACIÓN CORRECTA** cuando se cree correctamente la aplicación Spring Boot.</span><span class="sxs-lookup"><span data-stu-id="3b8df-151">IntelliJ should display a **BUILD SUCCESS** message when your Spring Boot app is successfully created.</span></span>

   ![Mensaje COMPILACIÓN CORRECTA][BU03]

### <a name="create-a-deployment-ready-artifact"></a><span data-ttu-id="3b8df-153">Creación de un artefacto preparado para la implementación</span><span class="sxs-lookup"><span data-stu-id="3b8df-153">Create a deployment-ready artifact</span></span>

<span data-ttu-id="3b8df-154">toopublish la aplicación de arranque de primavera, deberá toocreate un artefacto preparada para la implementación.</span><span class="sxs-lookup"><span data-stu-id="3b8df-154">toopublish your Spring Boot app, you need toocreate a deployment-ready artifact.</span></span> <span data-ttu-id="3b8df-155">Usar hello pasos:</span><span class="sxs-lookup"><span data-stu-id="3b8df-155">Use hello following steps:</span></span>

1. <span data-ttu-id="3b8df-156">Abra el proyecto de aplicación web en IntelliJ.</span><span class="sxs-lookup"><span data-stu-id="3b8df-156">Open your web app project in IntelliJ.</span></span>

1. <span data-ttu-id="3b8df-157">Haga clic en **Archivo** y después en **Estructura del proyecto**.</span><span class="sxs-lookup"><span data-stu-id="3b8df-157">Click **File**, and then click **Project Structure**.</span></span>

   ![Comando Estructura del proyecto][ART01]

1. <span data-ttu-id="3b8df-159">Haga clic en hello verde plus (**+**) tooadd un artefacto de símbolos, haga clic en **JAR**y, a continuación, haga clic en **vacía**.</span><span class="sxs-lookup"><span data-stu-id="3b8df-159">Click hello green plus (**+**) symbol tooadd an artifact, click **JAR**, and then click **Empty**.</span></span>

   ![Agregar un artefacto][ART02]

1. <span data-ttu-id="3b8df-161">Nombre el artefacto asegurándose de que no tooadd Hola ".jar" extensión y, a continuación, especifique la carpeta de destino de Hola para hello Maven de salida.</span><span class="sxs-lookup"><span data-stu-id="3b8df-161">Name your artifact while making sure not tooadd hello ".jar" extension, and then specify hello target folder for hello Maven output.</span></span>

   ![Especificar las propiedades del artefacto][ART03]

1. <span data-ttu-id="3b8df-163">Cree un manifiesto para el artefacto (opcional):</span><span class="sxs-lookup"><span data-stu-id="3b8df-163">Create a manifest for your artifact (optional):</span></span>

   <span data-ttu-id="3b8df-164">a.</span><span class="sxs-lookup"><span data-stu-id="3b8df-164">a.</span></span> <span data-ttu-id="3b8df-165">Haga clic en **Create Manifest** (Crear manifiesto).</span><span class="sxs-lookup"><span data-stu-id="3b8df-165">Click **Create Manifest**.</span></span>

      ![Haga clic en botón crear manifiestos de Hola][ART04a]

   <span data-ttu-id="3b8df-167">b.</span><span class="sxs-lookup"><span data-stu-id="3b8df-167">b.</span></span> <span data-ttu-id="3b8df-168">Elija ruta de acceso de hello predeterminada de artefacto de hello y, a continuación, haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="3b8df-168">Choose hello default path for hello artifact, and then click **OK**.</span></span>

      ![Especificar la ruta de acceso del artefacto][ART04b]

   <span data-ttu-id="3b8df-170">c.</span><span class="sxs-lookup"><span data-stu-id="3b8df-170">c.</span></span> <span data-ttu-id="3b8df-171">Haga clic en el botón de puntos suspensivos hello (**...** ) clase principal de toolocate Hola.</span><span class="sxs-lookup"><span data-stu-id="3b8df-171">Click hello ellipsis (**...**) toolocate hello main class.</span></span>

      ![Buscar la clase principal][ART04c]

   <span data-ttu-id="3b8df-173">d.</span><span class="sxs-lookup"><span data-stu-id="3b8df-173">d.</span></span> <span data-ttu-id="3b8df-174">Elija la clase principal y haga clic en **OK** (Aceptar).</span><span class="sxs-lookup"><span data-stu-id="3b8df-174">Choose your main class, and then click **OK**.</span></span>

      ![Especificar la clase principal][ART04d]

1. <span data-ttu-id="3b8df-176">Haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="3b8df-176">Click **OK**.</span></span>

   ![Cierre el cuadro de diálogo de estructura del proyecto de Hola][ART05]

> [!NOTE]
> <span data-ttu-id="3b8df-178">Para obtener más información sobre cómo crear artefactos en IntelliJ, consulte [configurar artefactos] en el sitio Web de JetBrains Hola.</span><span class="sxs-lookup"><span data-stu-id="3b8df-178">For more information about creating artifacts in IntelliJ, see [Configuring Artifacts] on hello JetBrains website.</span></span>
>

### <a name="build-hello-artifact-for-deployment"></a><span data-ttu-id="3b8df-179">Generar artefactos de hello para la implementación</span><span class="sxs-lookup"><span data-stu-id="3b8df-179">Build hello artifact for deployment</span></span>

1. <span data-ttu-id="3b8df-180">Haga clic en **Build** (Compilar) y haga clic en **Artifacts** (Artefactos).</span><span class="sxs-lookup"><span data-stu-id="3b8df-180">Click **Build**, and then click **Artifacts**.</span></span>

   ![Comando Compilar artefactos][BU04]

1. <span data-ttu-id="3b8df-182">Cuando Hola **crear artefacto** aparece el menú contextual, haga clic en **generar**.</span><span class="sxs-lookup"><span data-stu-id="3b8df-182">When hello **Build Artifact** context menu appears, click **Build**.</span></span>

   ![Menú contextual Compilar artefacto][BU05]

<span data-ttu-id="3b8df-184">IntelliJ debe aparecer artefacto Hola completado para la aplicación de arranque del muelle en ventana de herramientas de proyecto de Hola.</span><span class="sxs-lookup"><span data-stu-id="3b8df-184">IntelliJ should display hello completed artifact for your Spring Boot app in hello project tool window.</span></span>

   ![Artefacto creado][BU06]

## <a name="publish-your-web-app-tooazure-by-using-a-docker-container"></a><span data-ttu-id="3b8df-186">Publicar su tooAzure de aplicación web mediante el uso de un contenedor de Docker</span><span class="sxs-lookup"><span data-stu-id="3b8df-186">Publish your web app tooAzure by using a Docker container</span></span>

1. <span data-ttu-id="3b8df-187">Si no se ha registrado en tooyour cuenta de Azure, siga los pasos de hello en [instrucciones de inicio de sesión para hello Azure Toolkit para IntelliJ][Azure Sign In for IntelliJ].</span><span class="sxs-lookup"><span data-stu-id="3b8df-187">If you have not signed in tooyour Azure account, follow hello steps in [Sign-in instructions for hello Azure Toolkit for IntelliJ][Azure Sign In for IntelliJ].</span></span>

1. <span data-ttu-id="3b8df-188">En la ventana de herramientas del explorador de proyectos de hello, haga clic en proyecto de hello y, a continuación, seleccione **Azure** > **publicar como contenedor de Docker**.</span><span class="sxs-lookup"><span data-stu-id="3b8df-188">In hello Project Explorer tool window, right-click hello project, and then select **Azure** > **Publish as Docker Container**.</span></span>

   ![Comando Publish as Docker Container (Publicar como contenedor de Docker)][PU01]

1. <span data-ttu-id="3b8df-190">Cuando Hola **implementar contenedor de Docker en Azure** aparece el cuadro de diálogo, se muestran todos los hosts Docker existentes.</span><span class="sxs-lookup"><span data-stu-id="3b8df-190">When hello **Deploy Docker Container on Azure** dialog box appears, any existing Docker hosts are displayed.</span></span> <span data-ttu-id="3b8df-191">Si elige toodeploy tooan de host existente, puede omitir toostep 4.</span><span class="sxs-lookup"><span data-stu-id="3b8df-191">If you choose toodeploy tooan existing host, you can skip toostep 4.</span></span> <span data-ttu-id="3b8df-192">En caso contrario, utilice Hola siguiendo los pasos toocreate un host:</span><span class="sxs-lookup"><span data-stu-id="3b8df-192">Otherwise, use hello following steps toocreate a host:</span></span>

   <span data-ttu-id="3b8df-193">a.</span><span class="sxs-lookup"><span data-stu-id="3b8df-193">a.</span></span> <span data-ttu-id="3b8df-194">Haga clic en hello verde plus (**+**) símbolo.</span><span class="sxs-lookup"><span data-stu-id="3b8df-194">Click hello green plus (**+**) symbol.</span></span>

      ![Agregar un nuevo host de Docker][PU02]

   <span data-ttu-id="3b8df-196">b.</span><span class="sxs-lookup"><span data-stu-id="3b8df-196">b.</span></span> <span data-ttu-id="3b8df-197">Cuando Hola **crear un Host Docker** aparece el cuadro de diálogo, puede elegir los valores predeterminados de tooaccept Hola o puede especificar cualquier configuración personalizada para el nuevo host Docker.</span><span class="sxs-lookup"><span data-stu-id="3b8df-197">When hello **Create Docker Host** dialog box appears, you can choose tooaccept hello defaults, or you can specify any custom settings for your new Docker host.</span></span> <span data-ttu-id="3b8df-198">(Para obtener descripciones detalladas de hello distintas configuraciones, vea [publicar una aplicación web como un contenedor de Docker mediante hello Azure Toolkit para IntelliJ][Publish Container with Azure Toolkit].) Haga clic en **siguiente** cuando se especifica qué toouse de configuración.</span><span class="sxs-lookup"><span data-stu-id="3b8df-198">(For detailed descriptions of hello various settings, see [Publish a web app as a Docker container by using hello Azure Toolkit for IntelliJ][Publish Container with Azure Toolkit].) Click **Next** when you have specified which settings toouse.</span></span>

      ![Especificar las opciones de host de Docker][PU03a]

   <span data-ttu-id="3b8df-200">c.</span><span class="sxs-lookup"><span data-stu-id="3b8df-200">c.</span></span> <span data-ttu-id="3b8df-201">Puede elegir las credenciales de inicio de sesión existentes toouse desde un almacén de claves de Azure, o puede elegir tooenter nuevas credenciales de inicio de sesión de Docker.</span><span class="sxs-lookup"><span data-stu-id="3b8df-201">You can choose toouse existing login credentials from an Azure key vault, or you can choose tooenter new Docker login credentials.</span></span> <span data-ttu-id="3b8df-202">Haga clic en **Finalizar** cuando haya especificado las opciones.</span><span class="sxs-lookup"><span data-stu-id="3b8df-202">Click **Finish** when you have specified your options.</span></span>

      ![Especificar credenciales del host de Docker][PU03b]

1. <span data-ttu-id="3b8df-204">Seleccione el host de Docker y, después, haga clic en **Siguiente**.</span><span class="sxs-lookup"><span data-stu-id="3b8df-204">Select your Docker host, and then click **Next**.</span></span>

   ![Seleccione hello Docker host toouse][PU04]

1. <span data-ttu-id="3b8df-206">En la última página de Hola de hello **implementar contenedor de Docker en Azure** cuadro de diálogo, especifique Hola siguientes opciones:</span><span class="sxs-lookup"><span data-stu-id="3b8df-206">On hello last page of hello **Deploy Docker Container on Azure** dialog box, specify hello following options:</span></span>

   <span data-ttu-id="3b8df-207">a.</span><span class="sxs-lookup"><span data-stu-id="3b8df-207">a.</span></span> <span data-ttu-id="3b8df-208">Puede elegir un nombre personalizado para el contenedor de Hola que va a hospedar el contenedor de Docker toospecify, o puede aceptar predeterminado Hola.</span><span class="sxs-lookup"><span data-stu-id="3b8df-208">You can choose toospecify a custom name for hello container that will host your Docker container, or you can accept hello default.</span></span>

   <span data-ttu-id="3b8df-209">b.</span><span class="sxs-lookup"><span data-stu-id="3b8df-209">b.</span></span> <span data-ttu-id="3b8df-210">Escriba los puertos TCP hello para el host de docker mediante Hola según la sintaxis: *[puerto externo]*:*[puerto interno]*.</span><span class="sxs-lookup"><span data-stu-id="3b8df-210">Enter hello TCP ports for your docker host by using hello following syntax: *[external port]*:*[internal port]*.</span></span> <span data-ttu-id="3b8df-211">Por ejemplo, **80:8080** especifica un puerto externo del 80 y el puerto Hola predeterminado de arranque Spring interno de 8080.</span><span class="sxs-lookup"><span data-stu-id="3b8df-211">For example, **80:8080** specifies an external port of 80 and hello default internal Spring Boot port of 8080.</span></span>
   
      <span data-ttu-id="3b8df-212">Si ha personalizado el puerto interno (por ejemplo, editando el archivo de hello application.yml), necesitará toospecify número de puerto de Hola para hello toooccur de enrutamiento correcto en Azure.</span><span class="sxs-lookup"><span data-stu-id="3b8df-212">If you have customized your internal port (for example, by editing hello application.yml file), you need toospecify hello port number for hello correct routing toooccur in Azure.</span></span>

   <span data-ttu-id="3b8df-213">c.</span><span class="sxs-lookup"><span data-stu-id="3b8df-213">c.</span></span> <span data-ttu-id="3b8df-214">Después de configurar estas opciones, haga clic en **Finalizar**.</span><span class="sxs-lookup"><span data-stu-id="3b8df-214">After you have configured these options, click **Finish**.</span></span>

   ![Implementar un contenedor de Docker en Azure][PU05]

1. <span data-ttu-id="3b8df-216">Cuando hello Azure Toolkit ha terminado de publicar, Hola muestra de registro de actividad de Azure **publicada** para el estado de saludo.</span><span class="sxs-lookup"><span data-stu-id="3b8df-216">When hello Azure Toolkit has finished publishing, hello Azure Activity Log displays **Published** for hello status.</span></span>

   ![Host de Docker correctamente implementado][PU06]

## <a name="next-steps"></a><span data-ttu-id="3b8df-218">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="3b8df-218">Next steps</span></span>

[!INCLUDE [azure-toolkit-additional-resources](../includes/azure-toolkit-additional-resources.md)]

<span data-ttu-id="3b8df-219">toolearn sobre métodos adicionales para crear aplicaciones de arranque Spring mediante IntelliJ, consulte [crear proyectos de inicio de primavera](https://www.jetbrains.com/help/idea/creating-spring-boot-projects.html) en el sitio Web de JetBrains Hola.</span><span class="sxs-lookup"><span data-stu-id="3b8df-219">toolearn about additional methods for creating Spring Boot apps by using IntelliJ, see [Creating Spring Boot Projects](https://www.jetbrains.com/help/idea/creating-spring-boot-projects.html) on hello JetBrains website.</span></span>

<!-- URL List -->

[Azure Management Portal]: http://go.microsoft.com/fwlink/?LinkID=512959
[Azure Sign In for IntelliJ]: ./azure-toolkit-for-intellij-sign-in-instructions.md
[configurar artefactos]: https://www.jetbrains.com/help/idea/2016.1/configuring-artifacts.html (Configuración de artefactos)
[Deploy Spring Boot on Linux in ACS]:container-service/kubernetes/container-service-deploy-spring-boot-app-on-linux.md
[Docker]: https://www.docker.com/
[Publish Container with Azure Toolkit]: ./azure-toolkit-for-intellij-publish-as-docker-container.md
[arranque primavera]: http://projects.spring.io/spring-boot/
[Spring Framework]: https://spring.io/

<!-- IMG List -->

[CL01]: ./media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/CL01.png
[CL02a]: ./media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/CL02a.png
[CL02b]: ./media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/CL02b.png
[CL03]: ./media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/CL03.png
[CL04]: ./media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/CL04.png
[CL05]: ./media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/CL05.png
[CL06]: ./media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/CL06.png
[CL07]: ./media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/CL07.png
[CL08]: ./media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/CL08.png
[CL09]: ./media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/CL09.png
[CL10]: ./media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/CL10.png
[CL11]: ./media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/CL11.png
[CL12]: ./media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/CL12.png
[CL13]: ./media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/CL13.png
[CL14]: ./media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/CL14.png

[ART01]: ./media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/ART01.png
[ART02]: ./media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/ART02.png
[ART03]: ./media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/ART03.png
[ART04a]: ./media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/ART04a.png
[ART04b]: ./media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/ART04b.png
[ART04c]: ./media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/ART04c.png
[ART04d]: ./media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/ART04d.png
[ART05]: ./media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/ART05.png

[BU01]: ./media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/BU01.png
[BU02]: ./media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/BU02.png
[BU03]: ./media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/BU03.png
[BU04]: ./media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/BU04.png
[BU05]: ./media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/BU05.png
[BU06]: ./media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/BU06.png

[PU01]: ./media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/PU01.png
[PU02]: ./media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/PU02.png
[PU03a]: ./media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/PU03a.png
[PU03b]: ./media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/PU03b.png
[PU04]: ./media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/PU04.png
[PU05]: ./media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/PU05.png
[PU06]: ./media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/PU06.png
