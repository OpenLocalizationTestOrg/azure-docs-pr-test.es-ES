---
title: aaaPublish un contenedor de Docker mediante el uso de hello Azure Toolkit para IntelliJ | Documentos de Microsoft
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
ms.date: 04/14/2017
ms.author: robmcm
ms.openlocfilehash: bee94cb269ea707ae7ad55232e23e915aec48c34
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="publish-a-web-app-as-a-docker-container-by-using-hello-azure-toolkit-for-intellij"></a><span data-ttu-id="e2a9c-103">Publicar una aplicación web como un contenedor de Docker mediante hello Azure Toolkit para IntelliJ</span><span class="sxs-lookup"><span data-stu-id="e2a9c-103">Publish a web app as a Docker container by using hello Azure Toolkit for IntelliJ</span></span>

<span data-ttu-id="e2a9c-104">Los contenedores de Docker son un método muy utilizado para implementar aplicaciones web.</span><span class="sxs-lookup"><span data-stu-id="e2a9c-104">Docker containers are a widely used method for deploying web applications.</span></span> <span data-ttu-id="e2a9c-105">Mediante el uso de contenedores de Docker, los desarrolladores pueden consolidar todos sus archivos de proyecto y las dependencias en un único paquete para el servidor de implementación tooa.</span><span class="sxs-lookup"><span data-stu-id="e2a9c-105">By using Docker containers, developers can consolidate all their project files and dependencies into a single package for deployment tooa server.</span></span> <span data-ttu-id="e2a9c-106">Hello Azure Toolkit for IntelliJ simplifica este proceso para los desarrolladores de Java agregando *publicar como contenedor de Docker* características de implementación tooMicrosoft Azure.</span><span class="sxs-lookup"><span data-stu-id="e2a9c-106">hello Azure Toolkit for IntelliJ simplifies this process for Java developers by adding *Publish as Docker Container* features for deployment tooMicrosoft Azure.</span></span> <span data-ttu-id="e2a9c-107">Este artículo le guiará a través de hello pasos necesarios toopublish su tooAzure de aplicaciones como contenedores de Docker.</span><span class="sxs-lookup"><span data-stu-id="e2a9c-107">This article walks you through hello steps required toopublish your applications tooAzure as Docker containers.</span></span>

> [!NOTE]
>
> <span data-ttu-id="e2a9c-108">Para obtener más información sobre Docker está disponible en hello [sitio Web de Docker].</span><span class="sxs-lookup"><span data-stu-id="e2a9c-108">More information about Docker is available on hello [Docker website].</span></span>
>

[!INCLUDE [azure-toolkit-for-intellij-prerequisites](../includes/azure-toolkit-for-intellij-prerequisites.md)]

## <a name="publish-your-web-app-tooazure-by-using-a-docker-container"></a><span data-ttu-id="e2a9c-109">Publicar su tooAzure de aplicación web mediante el uso de un contenedor de Docker</span><span class="sxs-lookup"><span data-stu-id="e2a9c-109">Publish your web app tooAzure by using a Docker container</span></span>

> [!NOTE]
> * <span data-ttu-id="e2a9c-110">toopublish la aplicación web, debe crear un artefacto preparada para la implementación.</span><span class="sxs-lookup"><span data-stu-id="e2a9c-110">toopublish your web app, you must create a deployment-ready artifact.</span></span> <span data-ttu-id="e2a9c-111">toolearn más información, vea hello [información adicional acerca de cómo crear artefactos](#artifacts) sección.</span><span class="sxs-lookup"><span data-stu-id="e2a9c-111">toolearn more, see hello [Additional information about creating artifacts](#artifacts) section.</span></span>
>
> * <span data-ttu-id="e2a9c-112">Después de haber completado al Asistente para implementación de hello al menos una vez, la mayor parte de la configuración se utiliza como predeterminada cuando vuelva a ejecutar el Asistente de Hola.</span><span class="sxs-lookup"><span data-stu-id="e2a9c-112">After you have completed hello deployment wizard at least once, most of your settings are used as defaults when you run hello wizard again.</span></span>
>

1. <span data-ttu-id="e2a9c-113">Abra el proyecto de aplicación web en IntelliJ.</span><span class="sxs-lookup"><span data-stu-id="e2a9c-113">Open your web app project in IntelliJ.</span></span>

2. <span data-ttu-id="e2a9c-114">Hola toostart **publicar como contenedor de Docker** asistente, realice una de las siguientes de hello:</span><span class="sxs-lookup"><span data-stu-id="e2a9c-114">toostart hello **Publish as Docker Container** wizard, do either of hello following:</span></span>

   * <span data-ttu-id="e2a9c-115">Hola **proyecto** ventana de herramientas, haga clic en el proyecto, haga clic en **Azure**y, a continuación, haga clic en **publicar como contenedor de Docker**:</span><span class="sxs-lookup"><span data-stu-id="e2a9c-115">In hello **Project** tool window, right-click your project, click **Azure**, and then click **Publish as Docker Container**:</span></span>

      ![Hola publicar como comando de contenedor de Docker][PUB01]

   * <span data-ttu-id="e2a9c-117">En la barra de herramientas de hello IntelliJ, haga clic en hello **grupo publicación** botón y, a continuación, haga clic en **publicar como contenedor de Docker**:</span><span class="sxs-lookup"><span data-stu-id="e2a9c-117">On hello IntelliJ toolbar, click hello **Publish Group** button, and then click **Publish as Docker Container**:</span></span>

      <span data-ttu-id="e2a9c-118">![Hola publicar como comando de contenedor de Docker][PUB02]</span><span class="sxs-lookup"><span data-stu-id="e2a9c-118">![hello Publish as Docker Container command][PUB02]</span></span>  
    <span data-ttu-id="e2a9c-119">Hola **implementar contenedor de Docker en Azure** abre el asistente.</span><span class="sxs-lookup"><span data-stu-id="e2a9c-119">hello **Deploy Docker Container on Azure** wizard opens.</span></span>

   ![Hola implementar contenedor de Docker en el Asistente de Azure][PUB03]

3. <span data-ttu-id="e2a9c-121">Hola **escriba un nombre de imagen, seleccione la ruta de acceso del artefacto de Hola y comprobar una toobe de host de Docker usan** ventana, Hola siguientes:</span><span class="sxs-lookup"><span data-stu-id="e2a9c-121">In hello **Type an image name, select hello artifact's path and check a Docker host toobe used** window, do hello following:</span></span> 

   <span data-ttu-id="e2a9c-122">a.</span><span class="sxs-lookup"><span data-stu-id="e2a9c-122">a.</span></span> <span data-ttu-id="e2a9c-123">Hola **nombre de la imagen de Docker** cuadro, escriba un nombre único para el host Docker.</span><span class="sxs-lookup"><span data-stu-id="e2a9c-123">In hello **Docker image name** box, enter a unique name for your Docker host.</span></span> <span data-ttu-id="e2a9c-124">(Asistente de hello crea automáticamente un nombre, pero se puede modificar.)</span><span class="sxs-lookup"><span data-stu-id="e2a9c-124">(hello wizard automatically creates a name, but you can modify it.)</span></span> 

   <span data-ttu-id="e2a9c-125">b.</span><span class="sxs-lookup"><span data-stu-id="e2a9c-125">b.</span></span> <span data-ttu-id="e2a9c-126">Hola **Hosts** área muestra todos los hosts de Docker que ya haya creado.</span><span class="sxs-lookup"><span data-stu-id="e2a9c-126">hello **Hosts** area displays any Docker hosts that you have already created.</span></span> <span data-ttu-id="e2a9c-127">Realice una de las siguientes de hello:</span><span class="sxs-lookup"><span data-stu-id="e2a9c-127">Do either of hello following:</span></span> 
      * <span data-ttu-id="e2a9c-128">Si tiene un host Docker existente, puede implementar su tooit de aplicación web.</span><span class="sxs-lookup"><span data-stu-id="e2a9c-128">If you have an existing Docker host, you can deploy your web app tooit.</span></span>
      * <span data-ttu-id="e2a9c-129">toocreate un host Docker, haga clic en verde hello más el signo (**+**).</span><span class="sxs-lookup"><span data-stu-id="e2a9c-129">toocreate a Docker host, click hello green plus sign (**+**).</span></span>  
       <span data-ttu-id="e2a9c-130">Hola **crear un Host Docker** abre el cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="e2a9c-130">hello **Create Docker Host** dialog box opens.</span></span> 

      ![Asistente Deploy Docker Container on Azure (Implementar contenedor de Docker en Azure)][PUB04a]

4. <span data-ttu-id="e2a9c-132">Hola **configurar la máquina virtual nueva de hello** ventana, proporcionar Hola después de obtener información sobre el host Docker.</span><span class="sxs-lookup"><span data-stu-id="e2a9c-132">In hello **Configure hello new virtual machine** window, provide hello following information about your Docker host.</span></span> <span data-ttu-id="e2a9c-133">(Asistente de hello genera automáticamente la mayoría de hello información automáticamente, pero puede modificar cualquiera de ellos).</span><span class="sxs-lookup"><span data-stu-id="e2a9c-133">(hello wizard automatically generates most of hello information for you, but you can modify any of them.)</span></span> 

   <span data-ttu-id="e2a9c-134">a.</span><span class="sxs-lookup"><span data-stu-id="e2a9c-134">a.</span></span> <span data-ttu-id="e2a9c-135">Hola **nombre** cuadro, escriba un nombre único para el host de Docker Hola.</span><span class="sxs-lookup"><span data-stu-id="e2a9c-135">In hello **Name** box, enter a unique name for hello Docker host.</span></span> <span data-ttu-id="e2a9c-136">(Es no Hola igual Hola nombre de la imagen de Docker que especificó anteriormente).</span><span class="sxs-lookup"><span data-stu-id="e2a9c-136">(It is not hello same as hello Docker image name that you specified earlier.)</span></span> 
    
   <span data-ttu-id="e2a9c-137">b.</span><span class="sxs-lookup"><span data-stu-id="e2a9c-137">b.</span></span> <span data-ttu-id="e2a9c-138">Hola **suscripción** cuadro, escriba Hola suscripción de Azure que usa para el host.</span><span class="sxs-lookup"><span data-stu-id="e2a9c-138">In hello **Subscription** box, enter hello Azure subscription that you use for your host.</span></span> 
      
   <span data-ttu-id="e2a9c-139">c.</span><span class="sxs-lookup"><span data-stu-id="e2a9c-139">c.</span></span> <span data-ttu-id="e2a9c-140">Hola **región** cuadro, escriba Hola región geográfica donde se encuentra el host.</span><span class="sxs-lookup"><span data-stu-id="e2a9c-140">In hello **Region** box, enter hello geographical region where your host is located.</span></span>
      
   <span data-ttu-id="e2a9c-141">d.</span><span class="sxs-lookup"><span data-stu-id="e2a9c-141">d.</span></span> <span data-ttu-id="e2a9c-142">En hello **OS y tamaño** ficha, Hola siguientes:</span><span class="sxs-lookup"><span data-stu-id="e2a9c-142">On hello **OS and Size** tab, do hello following:</span></span>      
      * <span data-ttu-id="e2a9c-143">**Sistema operativo de host**: escriba el sistema operativo de hello para la máquina virtual de Hola que contiene el host.</span><span class="sxs-lookup"><span data-stu-id="e2a9c-143">**Host OS**: Enter hello operating system for hello virtual machine that contains your host.</span></span> 
      * <span data-ttu-id="e2a9c-144">**Tamaño**: especifique el tamaño de la máquina virtual de hello para el host.</span><span class="sxs-lookup"><span data-stu-id="e2a9c-144">**Size**: Enter hello virtual-machine size for your host.</span></span>   
       
   <span data-ttu-id="e2a9c-145">e.</span><span class="sxs-lookup"><span data-stu-id="e2a9c-145">e.</span></span> <span data-ttu-id="e2a9c-146">En hello **grupo de recursos** ficha, seleccione cualquiera de hello siguientes:</span><span class="sxs-lookup"><span data-stu-id="e2a9c-146">On hello **Resource Group** tab, select either of hello following:</span></span>      
      * <span data-ttu-id="e2a9c-147">**New resource group** (Nuevo grupo de recursos): cree un grupo de recursos para el host.</span><span class="sxs-lookup"><span data-stu-id="e2a9c-147">**New resource group**: Create a resource group for your host.</span></span>
      * <span data-ttu-id="e2a9c-148">**Existing resource group** (Grupo de recursos existente): especifique un grupo de recursos existente desde su cuenta de Azure.</span><span class="sxs-lookup"><span data-stu-id="e2a9c-148">**Existing resource group**: Specify an existing resource group from your Azure account.</span></span> 
       
   <span data-ttu-id="e2a9c-149">f.</span><span class="sxs-lookup"><span data-stu-id="e2a9c-149">f.</span></span> <span data-ttu-id="e2a9c-150">En hello **red** ficha, seleccione cualquiera de hello siguientes:</span><span class="sxs-lookup"><span data-stu-id="e2a9c-150">On hello **Network** tab, select either of hello following:</span></span>      
      * <span data-ttu-id="e2a9c-151">**New virtual network** (Nueva red virtual): cree una red virtual para el host.</span><span class="sxs-lookup"><span data-stu-id="e2a9c-151">**New virtual network**: Create a virtual network for your host.</span></span>
      * <span data-ttu-id="e2a9c-152">**Existing virtual network** (Red virtual existente): especifique una red virtual existente desde su cuenta de Azure.</span><span class="sxs-lookup"><span data-stu-id="e2a9c-152">**Existing virtual network**: Specify an existing virtual network from your Azure account.</span></span> 
       
   <span data-ttu-id="e2a9c-153">g.</span><span class="sxs-lookup"><span data-stu-id="e2a9c-153">g.</span></span> <span data-ttu-id="e2a9c-154">En hello **almacenamiento** ficha, seleccione cualquiera de hello siguientes:</span><span class="sxs-lookup"><span data-stu-id="e2a9c-154">On hello **Storage** tab, select either of hello following:</span></span>      
      * <span data-ttu-id="e2a9c-155">**New storage account** (Nueva cuenta de almacenamiento): cree una cuenta de almacenamiento para el host.</span><span class="sxs-lookup"><span data-stu-id="e2a9c-155">**New storage account**: Create a storage account for your host.</span></span>
      * <span data-ttu-id="e2a9c-156">**Existing storage account** (Cuenta de almacenamiento existente): especifique una cuenta de almacenamiento existente desde su cuenta de Azure.</span><span class="sxs-lookup"><span data-stu-id="e2a9c-156">**Existing storage account**: Specify an existing storage account from your Azure account.</span></span>
       
5. <span data-ttu-id="e2a9c-157">Haga clic en **Siguiente**.</span><span class="sxs-lookup"><span data-stu-id="e2a9c-157">Click **Next**.</span></span>  
     <span data-ttu-id="e2a9c-158">Hola **configurar registro en las credenciales y configuración de puerto** se abre la ventana.</span><span class="sxs-lookup"><span data-stu-id="e2a9c-158">hello **Configure log in credentials and port settings** window opens.</span></span>

      ![registro de Hello configurar en las credenciales y la ventana de configuración de puerto][PUB05]

6. <span data-ttu-id="e2a9c-160">Seleccione una de las siguientes opciones de hello:</span><span class="sxs-lookup"><span data-stu-id="e2a9c-160">Select one of hello following options:</span></span>

      * <span data-ttu-id="e2a9c-161">**Import credentials from Azure Key Vault**  (Importar credenciales de Azure Key Vault): especifique un conjunto de credenciales previamente guardadas que están almacenadas en la suscripción de Azure.</span><span class="sxs-lookup"><span data-stu-id="e2a9c-161">**Import credentials from Azure Key Vault**: Specify a previously saved set of credentials that are stored in your Azure subscription.</span></span>

          > [!NOTE]
          > <span data-ttu-id="e2a9c-162">Un almacén de claves de Azure que se crea con una cuenta específica o una entidad de servicio no es automáticamente accesible por otra cuenta o entidad de servicio que comparte suscripción Hola.</span><span class="sxs-lookup"><span data-stu-id="e2a9c-162">An Azure key vault that's created with a specific account or service principal is not automatically accessible by another account or service principal that shares hello subscription.</span></span> <span data-ttu-id="e2a9c-163">tooallow otra clave de hello toouse principal cuenta o servicio de almacén, debe usar la cuenta de Azure tooadd portal Hola Hola o entidad de servicio.</span><span class="sxs-lookup"><span data-stu-id="e2a9c-163">tooallow another account or service principal toouse hello key vault, you must use hello Azure portal tooadd hello account or service principal.</span></span>

      * <span data-ttu-id="e2a9c-164">**New log in credentials** (Nuevas credenciales de inicio de sesión): cree un conjunto de credenciales de inicio de sesión.</span><span class="sxs-lookup"><span data-stu-id="e2a9c-164">**New log in credentials**: Create a new set of login credentials.</span></span> <span data-ttu-id="e2a9c-165">Si selecciona esta opción, Hola siguientes:</span><span class="sxs-lookup"><span data-stu-id="e2a9c-165">If you select this option, do hello following:</span></span>

        <span data-ttu-id="e2a9c-166">a.</span><span class="sxs-lookup"><span data-stu-id="e2a9c-166">a.</span></span> <span data-ttu-id="e2a9c-167">En hello **las credenciales de la máquina virtual** ficha, proporcione Hola siguiendo la información de credenciales de inicio de sesión de máquina virtual de hello del host Docker: * **nombre de usuario**: escriba el nombre de usuario de hello para el inicio de sesión de máquina virtual credenciales.</span><span class="sxs-lookup"><span data-stu-id="e2a9c-167">On hello **VM Credentials** tab, provide hello following information for hello virtual-machine login credentials of your Docker host: * **Username**: Enter hello username for your virtual-machine login credentials.</span></span>
             <span data-ttu-id="e2a9c-168">* **Contraseña** y **confirmar**: escriba la contraseña de hello las credenciales de inicio de sesión de máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="e2a9c-168">* **Password** and **Confirm**: Enter hello password for your virtual-machine login credentials.</span></span>
             <span data-ttu-id="e2a9c-169">* **SSH**: especifique la configuración de Shell seguro (SSH) de hello para el host de Docker.</span><span class="sxs-lookup"><span data-stu-id="e2a9c-169">* **SSH**: Enter hello Secure Shell (SSH) settings for your Docker host.</span></span> <span data-ttu-id="e2a9c-170">Puede seleccionar una de las siguientes opciones de hello: * **ninguno**: Especifica que la máquina virtual no se permiten las conexiones SSH.</span><span class="sxs-lookup"><span data-stu-id="e2a9c-170">You can select one of hello following options: * **None**: Specifies that your virtual machine does not allow SSH connections.</span></span>
                <span data-ttu-id="e2a9c-171">* **Generar automáticamente**: automáticamente crea Hola la configuración necesaria para conectarse a través de SSH.</span><span class="sxs-lookup"><span data-stu-id="e2a9c-171">* **Auto-generate**: Automatically creates hello requisite settings for connecting via SSH.</span></span>
                <span data-ttu-id="e2a9c-172">* **Importar desde el directorio**: permite toospecify un directorio que contiene un conjunto de configuración de SSH guardada anteriormente.</span><span class="sxs-lookup"><span data-stu-id="e2a9c-172">* **Import from directory**: Allows you toospecify a directory that contains a set of previously saved SSH settings.</span></span> <span data-ttu-id="e2a9c-173">directorio de Hello debe contener Hola después de dos archivos:</span><span class="sxs-lookup"><span data-stu-id="e2a9c-173">hello directory must contain hello following two files:</span></span>
                
                  * *id_rsa*: Contains hello RSA identification for a user.
                  * *id_rsa.pub*: Contains hello RSA public key that is used for authentication.
            
        <span data-ttu-id="e2a9c-174">b.</span><span class="sxs-lookup"><span data-stu-id="e2a9c-174">b.</span></span> <span data-ttu-id="e2a9c-175">En hello **Docker Daemon acceso** ficha, proporcione Hola siguiente información:</span><span class="sxs-lookup"><span data-stu-id="e2a9c-175">On hello **Docker Daemon Access** tab, provide hello following information:</span></span>

          ![Create Docker Host (Crear host de Docker)][PUB06]
    
             * **Docker Daemon port**: Enter hello unique TCP port for your Docker host.
             * **TLS Security**: Enter hello Transport Layer Security settings for your Docker host. You can choose from hello following options:
                * **None**: Specifies that your virtual machine does not allow TLS connections.
                * **Auto-generate**: Automatically creates hello requisite settings for connecting via TLS.
                * **Import from directory**: Specifies a directory that contains a set of previously saved TLS settings. hello directory must contain hello following six files: 
                   * *ca.pem* and *ca-key.pem*: Contain hello certificate and public key for hello TLS Certificate Authority.
                   * *cert.pem* and *key.pem*: Contain client certificate and public key which will be used for TLS authentication.
                   * *server.pem* and *server-key.pem*: Contain hello client certificate and public key that is used for TLS authentication.

7. <span data-ttu-id="e2a9c-177">Después de escribir información de hello necesario, haga clic en **finalizar**.</span><span class="sxs-lookup"><span data-stu-id="e2a9c-177">After you have entered hello required information, click **Finish**.</span></span>  
    <span data-ttu-id="e2a9c-178">Hola **implementar contenedor de Docker en Azure** Asistente vuelve a aparecer.</span><span class="sxs-lookup"><span data-stu-id="e2a9c-178">hello **Deploy Docker Container on Azure** wizard reappears.</span></span>

   ![Asistente Deploy Docker Container on Azure (Implementar contenedor de Docker en Azure)][PUB07]

8. <span data-ttu-id="e2a9c-180">Haga clic en **Siguiente**.</span><span class="sxs-lookup"><span data-stu-id="e2a9c-180">Click **Next**.</span></span>  
    <span data-ttu-id="e2a9c-181">Hola **configurar hello Docker contenedor toobe crea** abre la ventana.</span><span class="sxs-lookup"><span data-stu-id="e2a9c-181">hello **Configure hello Docker container toobe created** window opens.</span></span>

   ![ventana de Hello configurar hello Docker contenedor toobe creado][PUB08]

9. <span data-ttu-id="e2a9c-183">Hola **configurar hello Docker contenedor toobe crea** ventana, proporcionar Hola siguiente información:</span><span class="sxs-lookup"><span data-stu-id="e2a9c-183">In hello **Configure hello Docker container toobe created** window, provide hello following information:</span></span> 

   <span data-ttu-id="e2a9c-184">a.</span><span class="sxs-lookup"><span data-stu-id="e2a9c-184">a.</span></span> <span data-ttu-id="e2a9c-185">Hola **nombre del contenedor de Docker** cuadro, escriba un nombre único para el contenedor de Docker.</span><span class="sxs-lookup"><span data-stu-id="e2a9c-185">In hello **Docker container name** box, enter a unique name for your Docker container.</span></span>

   <span data-ttu-id="e2a9c-186">b.</span><span class="sxs-lookup"><span data-stu-id="e2a9c-186">b.</span></span> <span data-ttu-id="e2a9c-187">Elija uno de hello después de imágenes de Docker:</span><span class="sxs-lookup"><span data-stu-id="e2a9c-187">Choose one of hello following Docker images:</span></span> 

      * <span data-ttu-id="e2a9c-188">**Predefined Docker image** (Imagen de Docker predefinida): especifique una imagen de Docker preexistente de Azure.</span><span class="sxs-lookup"><span data-stu-id="e2a9c-188">**Predefined Docker image**: Specify a pre-existing Docker image from Azure.</span></span> 

        > [!NOTE]
        > <span data-ttu-id="e2a9c-189">Hola lista de imágenes de Docker en este cuadro está formada por varias imágenes que hello Azure Toolkit ha sido configurado toopatch para que el artefacto se implementa automáticamente.</span><span class="sxs-lookup"><span data-stu-id="e2a9c-189">hello list of Docker images in this box consists of several images that hello Azure Toolkit has been configured toopatch so that your artifact is deployed automatically.</span></span> 

      * <span data-ttu-id="e2a9c-190">**Custom Dockerfile** (Dockerfile personalizado): especifique un Dockerfile guardado antes desde el equipo local.</span><span class="sxs-lookup"><span data-stu-id="e2a9c-190">**Custom Dockerfile**: Specify a previously saved Dockerfile from your local computer.</span></span>

        > [!NOTE]
        > <span data-ttu-id="e2a9c-191">Se trata de una característica más avanzada para los desarrolladores que deseen toodeploy su propios Dockerfile.</span><span class="sxs-lookup"><span data-stu-id="e2a9c-191">This is a more advanced feature for developers who want toodeploy their own Dockerfile.</span></span> <span data-ttu-id="e2a9c-192">Sin embargo, resulta una toodevelopers que usan este tooensure opción que sus Dockerfile se ha creado correctamente.</span><span class="sxs-lookup"><span data-stu-id="e2a9c-192">However, it is up toodevelopers who use this option tooensure that their Dockerfile is built correctly.</span></span> <span data-ttu-id="e2a9c-193">Porque hello Azure Toolkit validan el contenido de hello en un archivo Dockerfile personalizado, implementación de hello podría producir errores si hello Dockerfile tiene problemas.</span><span class="sxs-lookup"><span data-stu-id="e2a9c-193">Because hello Azure Toolkit does not validate hello content in a custom Dockerfile, hello deployment might fail if hello Dockerfile has issues.</span></span> <span data-ttu-id="e2a9c-194">Además, dado que hello Azure Toolkit espera Hola personalizado Dockerfile toocontain un artefacto de la aplicación web, intenta tooopen una conexión HTTP.</span><span class="sxs-lookup"><span data-stu-id="e2a9c-194">In addition, because hello Azure Toolkit expects hello custom Dockerfile toocontain a web app artifact, it attempts tooopen an HTTP connection.</span></span> <span data-ttu-id="e2a9c-195">Si los desarrolladores publican un tipo diferente de artefacto, podrían recibir errores inofensivos después de la implementación.</span><span class="sxs-lookup"><span data-stu-id="e2a9c-195">If developers publish a different type of artifact, they might receive innocuous errors after deployment.</span></span>

   <span data-ttu-id="e2a9c-196">c.</span><span class="sxs-lookup"><span data-stu-id="e2a9c-196">c.</span></span> <span data-ttu-id="e2a9c-197">Hola **configuración de puertos** cuadro, escriba Hola único puerto el enlace TCP para el contenedor de Docker.</span><span class="sxs-lookup"><span data-stu-id="e2a9c-197">In hello **Port settings** box, enter hello unique TCP port binding for your Docker container.</span></span> 

10. <span data-ttu-id="e2a9c-198">Después de haber completado los pasos anteriores de hello, haga clic en **finalizar**.</span><span class="sxs-lookup"><span data-stu-id="e2a9c-198">After you have completed hello preceding steps, click **Finish**.</span></span> 

<span data-ttu-id="e2a9c-199">Hello Azure Toolkit comienza implementar su tooAzure de aplicación web en un contenedor de Docker.</span><span class="sxs-lookup"><span data-stu-id="e2a9c-199">hello Azure Toolkit begins deploying your web app tooAzure in a Docker container.</span></span> <span data-ttu-id="e2a9c-200">A menos que haya configurado toobe IntelliJ implementado en segundo plano de hello, un **implementar tooAzure** aparece la barra de progreso.</span><span class="sxs-lookup"><span data-stu-id="e2a9c-200">Unless you have configured IntelliJ toobe deployed in hello background, a **Deploying tooAzure** progress bar appears.</span></span> 

![barra de progreso de implementación de Hola][PUB09]

<a name="artifacts"></a>
## <a name="additional-information-about-creating-artifacts"></a><span data-ttu-id="e2a9c-202">Información adicional sobre la creación de artefactos</span><span class="sxs-lookup"><span data-stu-id="e2a9c-202">Additional information about creating artifacts</span></span>

<span data-ttu-id="e2a9c-203">toocreate un artefacto preparada para la implementación, Hola siguientes:</span><span class="sxs-lookup"><span data-stu-id="e2a9c-203">toocreate a deployment-ready artifact, do hello following:</span></span>

1. <span data-ttu-id="e2a9c-204">Abra el proyecto de aplicación web en IntelliJ.</span><span class="sxs-lookup"><span data-stu-id="e2a9c-204">Open your web app project in IntelliJ.</span></span>

2. <span data-ttu-id="e2a9c-205">Haga clic en **Archivo** y después en **Estructura del proyecto**.</span><span class="sxs-lookup"><span data-stu-id="e2a9c-205">Click **File**, and then click **Project Structure**.</span></span>

   ![Hola comandos de la estructura del proyecto][ART01]

3. <span data-ttu-id="e2a9c-207">tooadd un artefacto, haga clic en verde hello más el signo (**+**) y, a continuación, haga clic en **aplicación Web: archivo**.</span><span class="sxs-lookup"><span data-stu-id="e2a9c-207">tooadd an artifact, click hello green plus sign (**+**), and then click **Web Application: Archive**.</span></span>

   ![Hola comando "Archivo de: aplicación Web"][ART02]

4. <span data-ttu-id="e2a9c-209">Hola **nombre** cuadro, escriba un nombre para el artefacto (no incluya hello *.war* extensión) y, a continuación, haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="e2a9c-209">In hello **Name** box, enter a name for your artifact (do not include hello *.war* extension), and then click **OK**.</span></span>

   ![cuadro de nombre de artefacto de Hola][ART03]

<span data-ttu-id="e2a9c-211">Para obtener más información sobre cómo crear artefactos en IntelliJ, consulte [configurar artefactos] en el sitio Web de JetBrains Hola.</span><span class="sxs-lookup"><span data-stu-id="e2a9c-211">For more information about creating artifacts in IntelliJ, see [Configuring artifacts] on hello JetBrains website.</span></span>

## <a name="next-steps"></a><span data-ttu-id="e2a9c-212">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="e2a9c-212">Next steps</span></span>
<span data-ttu-id="e2a9c-213">Para obtener más información acerca de hello kits de herramientas de Azure para Java IDE, vea Hola recursos siguientes:</span><span class="sxs-lookup"><span data-stu-id="e2a9c-213">For more information about hello Azure Toolkits for Java IDEs, see hello following resources:</span></span>

* <span data-ttu-id="e2a9c-214">[Kit de herramientas de Azure para Eclipse]</span><span class="sxs-lookup"><span data-stu-id="e2a9c-214">[Azure Toolkit for Eclipse]</span></span>
  * <span data-ttu-id="e2a9c-215">[Novedades de hello Azure Toolkit for Eclipse]</span><span class="sxs-lookup"><span data-stu-id="e2a9c-215">[What's new in hello Azure Toolkit for Eclipse]</span></span>
  * <span data-ttu-id="e2a9c-216">[Instalar hello Azure Toolkit for Eclipse]</span><span class="sxs-lookup"><span data-stu-id="e2a9c-216">[Installing hello Azure Toolkit for Eclipse]</span></span>
  * <span data-ttu-id="e2a9c-217">[Instrucciones de inicio de sesión para hello Azure Toolkit for Eclipse]</span><span class="sxs-lookup"><span data-stu-id="e2a9c-217">[Sign-in instructions for hello Azure Toolkit for Eclipse]</span></span>
  * <span data-ttu-id="e2a9c-218">[Creación de una aplicación web Hello World para Azure en Eclipse]</span><span class="sxs-lookup"><span data-stu-id="e2a9c-218">[Create a Hello World web app for Azure in Eclipse]</span></span>
* <span data-ttu-id="e2a9c-219">[Kit de herramientas de Azure para IntelliJ]</span><span class="sxs-lookup"><span data-stu-id="e2a9c-219">[Azure Toolkit for IntelliJ]</span></span>
  * <span data-ttu-id="e2a9c-220">[Novedades de hello Azure Toolkit for IntelliJ]</span><span class="sxs-lookup"><span data-stu-id="e2a9c-220">[What's new in hello Azure Toolkit for IntelliJ]</span></span>
  * <span data-ttu-id="e2a9c-221">[Instalación hello Azure Toolkit for IntelliJ]</span><span class="sxs-lookup"><span data-stu-id="e2a9c-221">[Installing hello Azure Toolkit for IntelliJ]</span></span>
  * <span data-ttu-id="e2a9c-222">[Instrucciones de inicio de sesión para hello Azure Toolkit para IntelliJ]</span><span class="sxs-lookup"><span data-stu-id="e2a9c-222">[Sign-in instructions for hello Azure Toolkit for IntelliJ]</span></span>
  * <span data-ttu-id="e2a9c-223">[Creación de una aplicación web Hello World para Azure en IntelliJ]</span><span class="sxs-lookup"><span data-stu-id="e2a9c-223">[Create a Hello World web app for Azure in IntelliJ]</span></span>

<span data-ttu-id="e2a9c-224">Para obtener más información acerca del uso de Azure con Java, vea hello [Centro para desarrolladores de Java de Azure] hello y [herramientas de Java para Visual Studio Team Services].</span><span class="sxs-lookup"><span data-stu-id="e2a9c-224">For more information about using Azure with Java, see hello [Azure Java Developer Center] and hello [Java Tools for Visual Studio Team Services].</span></span>

<span data-ttu-id="e2a9c-225">Para obtener recursos adicionales de Docker, consulte oficial de hello [sitio Web de Docker].</span><span class="sxs-lookup"><span data-stu-id="e2a9c-225">For additional resources for Docker, see hello official [Docker website].</span></span>

<!-- URL List -->

[Kit de herramientas de Azure para Eclipse]: ./azure-toolkit-for-eclipse.md
[Kit de herramientas de Azure para IntelliJ]: ./azure-toolkit-for-intellij.md
[Creación de una aplicación web Hello World para Azure en Eclipse]: ./app-service-web/app-service-web-eclipse-create-hello-world-web-app.md
[Creación de una aplicación web Hello World para Azure en IntelliJ]: ./app-service-web/app-service-web-intellij-create-hello-world-web-app.md
[Instalar hello Azure Toolkit for Eclipse]: ./azure-toolkit-for-eclipse-installation.md
[Instalación hello Azure Toolkit for IntelliJ]: ./azure-toolkit-for-intellij-installation.md
[Instrucciones de inicio de sesión para hello Azure Toolkit for Eclipse]: ./azure-toolkit-for-eclipse-sign-in-instructions.md
[Instrucciones de inicio de sesión para hello Azure Toolkit para IntelliJ]: ./azure-toolkit-for-intellij-sign-in-instructions.md
[Novedades de hello Azure Toolkit for Eclipse]: ./azure-toolkit-for-eclipse-whats-new.md
[Novedades de hello Azure Toolkit for IntelliJ]: ./azure-toolkit-for-intellij-whats-new.md

[Centro para desarrolladores de Java de Azure]: https://azure.microsoft.com/develop/java/
[herramientas de Java para Visual Studio Team Services]: https://java.visualstudio.com/

[sitio Web de Docker]: https://www.docker.com/
[configurar artefactos]: https://www.jetbrains.com/help/idea/2016.1/configuring-artifacts.html (Configuración de artefactos)

<!-- IMG List -->

[PUB01]: ./media/azure-toolkit-for-intellij-publish-as-docker-container/PUB01.png
[PUB02]: ./media/azure-toolkit-for-intellij-publish-as-docker-container/PUB02.png
[PUB03]: ./media/azure-toolkit-for-intellij-publish-as-docker-container/PUB03.png
[PUB04a]: ./media/azure-toolkit-for-intellij-publish-as-docker-container/PUB04a.png
[PUB04b]: ./media/azure-toolkit-for-intellij-publish-as-docker-container/PUB04b.png
[PUB04c]: ./media/azure-toolkit-for-intellij-publish-as-docker-container/PUB04c.png
[PUB04d]: ./media/azure-toolkit-for-intellij-publish-as-docker-container/PUB04d.png
[PUB05]: ./media/azure-toolkit-for-intellij-publish-as-docker-container/PUB05.png
[PUB06]: ./media/azure-toolkit-for-intellij-publish-as-docker-container/PUB06.png
[PUB07]: ./media/azure-toolkit-for-intellij-publish-as-docker-container/PUB07.png
[PUB08]: ./media/azure-toolkit-for-intellij-publish-as-docker-container/PUB08.png
[PUB09]: ./media/azure-toolkit-for-intellij-publish-as-docker-container/PUB09.png

[ART01]: ./media/azure-toolkit-for-intellij-publish-as-docker-container/ART01.png
[ART02]: ./media/azure-toolkit-for-intellij-publish-as-docker-container/ART02.png
[ART03]: ./media/azure-toolkit-for-intellij-publish-as-docker-container/ART03.png
