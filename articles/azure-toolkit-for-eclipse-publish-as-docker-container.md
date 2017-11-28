---
title: aaaPublish un contenedor de Docker mediante el uso de hello Azure Toolkit for Eclipse | Documentos de Microsoft
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
ms.date: 04/14/2017
ms.author: robmcm
ms.openlocfilehash: 53ec3a7f7a171691024e03622fd48d6f1e257b50
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="publish-a-web-app-as-a-docker-container-by-using-hello-azure-toolkit-for-eclipse"></a><span data-ttu-id="d3ed7-103">Publicar una aplicación web como un contenedor de Docker mediante Hola Kit de herramientas de Azure para Eclipse</span><span class="sxs-lookup"><span data-stu-id="d3ed7-103">Publish a web app as a Docker container by using hello Azure Toolkit for Eclipse</span></span>

<span data-ttu-id="d3ed7-104">Los contenedores de Docker son un método muy utilizado para implementar aplicaciones web.</span><span class="sxs-lookup"><span data-stu-id="d3ed7-104">Docker containers are a widely used method for deploying web applications.</span></span> <span data-ttu-id="d3ed7-105">Mediante el uso de contenedores de Docker, los desarrolladores pueden consolidar todos sus archivos de proyecto y las dependencias en un único paquete para el servidor de implementación tooa.</span><span class="sxs-lookup"><span data-stu-id="d3ed7-105">By using Docker containers, developers can consolidate all their project files and dependencies into a single package for deployment tooa server.</span></span> <span data-ttu-id="d3ed7-106">Hello Azure Toolkit for Eclipse simplifica este proceso para los desarrolladores de Java agregando *publicar como contenedor de Docker* características de implementación tooMicrosoft Azure.</span><span class="sxs-lookup"><span data-stu-id="d3ed7-106">hello Azure Toolkit for Eclipse simplifies this process for Java developers by adding *Publish as Docker Container* features for deployment tooMicrosoft Azure.</span></span> <span data-ttu-id="d3ed7-107">Este artículo le guiará a través de hello pasos necesarios toopublish su tooAzure de aplicaciones como contenedores de Docker.</span><span class="sxs-lookup"><span data-stu-id="d3ed7-107">This article walks you through hello steps required toopublish your applications tooAzure as Docker containers.</span></span>

> [!NOTE]
> <span data-ttu-id="d3ed7-108">Para obtener más información sobre Docker está disponible en hello [sitio Web de Docker].</span><span class="sxs-lookup"><span data-stu-id="d3ed7-108">More information about Docker is available on hello [Docker website].</span></span>
>

[!INCLUDE [azure-toolkit-for-eclipse-prerequisites](../includes/azure-toolkit-for-eclipse-prerequisites.md)]

## <a name="publish-your-web-app-tooazure-by-using-a-docker-container"></a><span data-ttu-id="d3ed7-109">Publicar su tooAzure de aplicación web mediante el uso de un contenedor de Docker</span><span class="sxs-lookup"><span data-stu-id="d3ed7-109">Publish your web app tooAzure by using a Docker container</span></span>

1. <span data-ttu-id="d3ed7-110">Abra el proyecto de aplicación web en Eclipse.</span><span class="sxs-lookup"><span data-stu-id="d3ed7-110">Open your web app project in Eclipse.</span></span>

2. <span data-ttu-id="d3ed7-111">Hola toostart **publicar como contenedor de Docker** asistente, realice una de las siguientes de hello:</span><span class="sxs-lookup"><span data-stu-id="d3ed7-111">toostart hello **Publish as Docker Container** wizard, do either of hello following:</span></span>

   * <span data-ttu-id="d3ed7-112">Hola **navegador** ver, haga clic en el proyecto, haga clic en **Azure**y, a continuación, haga clic en **publicar como contenedor de Docker**.</span><span class="sxs-lookup"><span data-stu-id="d3ed7-112">In hello **Navigator** view, right-click your project, click **Azure**, and then click **Publish as Docker Container**.</span></span>

      ![Vista de navegador del comando Publish as Docker Container (Publicar como contenedor de Docker)][PUB01]

   * <span data-ttu-id="d3ed7-114">En la barra de herramientas de Eclipse hello, haga clic en hello **publicar** botón y, a continuación, haga clic en **publicar como contenedor de Docker**.</span><span class="sxs-lookup"><span data-stu-id="d3ed7-114">On hello Eclipse toolbar, click hello **Publish** button, and then click **Publish as Docker Container**.</span></span>

      ![Barra de herramientas de Eclipse del comando Publish as Docker Container (Publicar como contenedor de Docker)][PUB02]
      
    <span data-ttu-id="d3ed7-116">Hola **implementar contenedor de Docker en Azure** abre el asistente.</span><span class="sxs-lookup"><span data-stu-id="d3ed7-116">hello **Deploy Docker Container on Azure** wizard opens.</span></span>

    ![Hola implementar contenedor de Docker en el Asistente de Azure][PUB03]

3. <span data-ttu-id="d3ed7-118">Hola **escriba un nombre de imagen, seleccione la ruta de acceso del artefacto de Hola y comprobar una toobe de host de Docker usan** ventana, Hola siguientes:</span><span class="sxs-lookup"><span data-stu-id="d3ed7-118">In hello **Type an image name, select hello artifact's path and check a Docker host toobe used** window, do hello following:</span></span>

    <span data-ttu-id="d3ed7-119">a.</span><span class="sxs-lookup"><span data-stu-id="d3ed7-119">a.</span></span> <span data-ttu-id="d3ed7-120">Hola **nombre de la imagen de Docker** cuadro, escriba un nombre único para el host Docker.</span><span class="sxs-lookup"><span data-stu-id="d3ed7-120">In hello **Docker image name** box, enter a unique name for your Docker host.</span></span> <span data-ttu-id="d3ed7-121">(Asistente de hello crea automáticamente un nombre, pero se puede modificar.)</span><span class="sxs-lookup"><span data-stu-id="d3ed7-121">(hello wizard automatically creates a name, but you can modify it.)</span></span>

    <span data-ttu-id="d3ed7-122">b.</span><span class="sxs-lookup"><span data-stu-id="d3ed7-122">b.</span></span> <span data-ttu-id="d3ed7-123">Hola **Hosts** área muestra todos los hosts de Docker que ya haya creado.</span><span class="sxs-lookup"><span data-stu-id="d3ed7-123">hello **Hosts** area displays any Docker hosts that you have already created.</span></span> <span data-ttu-id="d3ed7-124">Realice una de las siguientes de hello:</span><span class="sxs-lookup"><span data-stu-id="d3ed7-124">Do either of hello following:</span></span>

    * <span data-ttu-id="d3ed7-125">Si tiene un host Docker existente, puede implementar su tooit de aplicación web.</span><span class="sxs-lookup"><span data-stu-id="d3ed7-125">If you have an existing Docker host, you can deploy your web app tooit.</span></span>
    * <span data-ttu-id="d3ed7-126">Haga clic en un nuevo host Docker, toocreate **agregar**.</span><span class="sxs-lookup"><span data-stu-id="d3ed7-126">toocreate a new Docker host, click **Add**.</span></span>  
      
    <span data-ttu-id="d3ed7-127">Hola **crear un Host Docker** abre el cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="d3ed7-127">hello **Create Docker Host** dialog box opens.</span></span>

    ![Asistente Deploy Docker Container on Azure (Implementar contenedor de Docker en Azure)][PUB04a]

4. <span data-ttu-id="d3ed7-129">Hola **configurar la máquina virtual nueva de hello** ventana, especifique Hola siguientes opciones para el host de Docker.</span><span class="sxs-lookup"><span data-stu-id="d3ed7-129">In hello **Configure hello new virtual machine** window, specify hello following options for your Docker host.</span></span> <span data-ttu-id="d3ed7-130">(Asistente de hello genera automáticamente la mayoría de las opciones de Hola para usted, pero puede modificar cualquiera de ellos).</span><span class="sxs-lookup"><span data-stu-id="d3ed7-130">(hello wizard automatically generates most of hello options for you, but you can modify any of them.)</span></span>

   <span data-ttu-id="d3ed7-131">a.</span><span class="sxs-lookup"><span data-stu-id="d3ed7-131">a.</span></span> <span data-ttu-id="d3ed7-132">**Nombre**: escriba un nombre único para el host de Docker Hola.</span><span class="sxs-lookup"><span data-stu-id="d3ed7-132">**Name**: Enter a unique name for hello Docker host.</span></span> <span data-ttu-id="d3ed7-133">(Es no Hola igual Hola nombre de la imagen de Docker que especificó anteriormente).</span><span class="sxs-lookup"><span data-stu-id="d3ed7-133">(It is not hello same as hello Docker image name that you specified earlier.)</span></span>

   <span data-ttu-id="d3ed7-134">b.</span><span class="sxs-lookup"><span data-stu-id="d3ed7-134">b.</span></span> <span data-ttu-id="d3ed7-135">**Suscripción**: escriba Hola suscripción de Azure que usa para el host.</span><span class="sxs-lookup"><span data-stu-id="d3ed7-135">**Subscription**: Enter hello Azure subscription that you use for your host.</span></span>

   <span data-ttu-id="d3ed7-136">c.</span><span class="sxs-lookup"><span data-stu-id="d3ed7-136">c.</span></span> <span data-ttu-id="d3ed7-137">**Región**: ENTRAR Hola región geográfica donde se encuentra el host.</span><span class="sxs-lookup"><span data-stu-id="d3ed7-137">**Region**: Enter hello geographical region where your host is located.</span></span>

   <span data-ttu-id="d3ed7-138">d.</span><span class="sxs-lookup"><span data-stu-id="d3ed7-138">d.</span></span> <span data-ttu-id="d3ed7-139">En hello **SO Host y el tamaño** ficha:</span><span class="sxs-lookup"><span data-stu-id="d3ed7-139">On hello **Host OS and Size** tab:</span></span>
     * <span data-ttu-id="d3ed7-140">**Sistema operativo de host**: escriba el sistema operativo de hello para la máquina virtual de Hola que contiene el host.</span><span class="sxs-lookup"><span data-stu-id="d3ed7-140">**Host OS**: Enter hello operating system for hello virtual machine that contains your host.</span></span>
     * <span data-ttu-id="d3ed7-141">**Tamaño**: especifique el tamaño de la máquina virtual de hello para el host.</span><span class="sxs-lookup"><span data-stu-id="d3ed7-141">**Size**: Enter hello virtual-machine size for your host.</span></span>

   <span data-ttu-id="d3ed7-142">e.</span><span class="sxs-lookup"><span data-stu-id="d3ed7-142">e.</span></span> <span data-ttu-id="d3ed7-143">En hello **grupo de recursos** ficha:</span><span class="sxs-lookup"><span data-stu-id="d3ed7-143">On hello **Resource Group** tab:</span></span>
     * <span data-ttu-id="d3ed7-144">**New resource group** (Nuevo grupo de recursos): cree un grupo de recursos para el host.</span><span class="sxs-lookup"><span data-stu-id="d3ed7-144">**New resource group**: Create a new resource group for your host.</span></span>
     * <span data-ttu-id="d3ed7-145">**Existing resource group** (Grupo de recursos existente): especifique un grupo de recursos existente desde su cuenta de Azure.</span><span class="sxs-lookup"><span data-stu-id="d3ed7-145">**Existing resource group**: Enter an existing resource group from your Azure account.</span></span>

   <span data-ttu-id="d3ed7-146">f.</span><span class="sxs-lookup"><span data-stu-id="d3ed7-146">f.</span></span> <span data-ttu-id="d3ed7-147">En hello **red** ficha:</span><span class="sxs-lookup"><span data-stu-id="d3ed7-147">On hello **Network** tab:</span></span>
     * <span data-ttu-id="d3ed7-148">**New virtual network** (Nueva red virtual): cree una red virtual para el host.</span><span class="sxs-lookup"><span data-stu-id="d3ed7-148">**New virtual network**: Create a new virtual network for your host.</span></span>
     * <span data-ttu-id="d3ed7-149">**Existing virtual network** (Red virtual existente): especifique una red virtual existente desde su cuenta de Azure.</span><span class="sxs-lookup"><span data-stu-id="d3ed7-149">**Existing virtual network**: Enter an existing virtual network from your Azure account.</span></span>

   <span data-ttu-id="d3ed7-150">g.</span><span class="sxs-lookup"><span data-stu-id="d3ed7-150">g.</span></span> <span data-ttu-id="d3ed7-151">En hello **almacenamiento** ficha:</span><span class="sxs-lookup"><span data-stu-id="d3ed7-151">On hello **Storage** tab:</span></span>
     * <span data-ttu-id="d3ed7-152">**New storage account** (Nueva cuenta de almacenamiento): cree una cuenta de almacenamiento para el host.</span><span class="sxs-lookup"><span data-stu-id="d3ed7-152">**New storage account**: Create a new storage account for your host.</span></span>
     * <span data-ttu-id="d3ed7-153">**Existing storage account** (Cuenta de almacenamiento existente): especifique una cuenta de almacenamiento existente desde su cuenta de Azure.</span><span class="sxs-lookup"><span data-stu-id="d3ed7-153">**Existing storage account**: Enter an existing storage account from your Azure account.</span></span>

5. <span data-ttu-id="d3ed7-154">Haga clic en **Siguiente**.</span><span class="sxs-lookup"><span data-stu-id="d3ed7-154">Click **Next**.</span></span>

6. <span data-ttu-id="d3ed7-155">Hola **configurar registro en las credenciales y configuración de puerto** ventana, seleccione una de las siguientes opciones de hello:</span><span class="sxs-lookup"><span data-stu-id="d3ed7-155">In hello **Configure log in credentials and port settings** window, select one of hello following options:</span></span>

    * <span data-ttu-id="d3ed7-156">**Import credentials from Azure Key Vault** (Importar credenciales de Azure Key Vault): especifique un conjunto de credenciales previamente guardadas que están almacenadas en la suscripción de Azure.</span><span class="sxs-lookup"><span data-stu-id="d3ed7-156">**Import credentials from Azure Key Vault**: Specifies a previously saved set of credentials that are stored in your Azure subscription.</span></span>

      >[!NOTE]
      ><span data-ttu-id="d3ed7-157">Un almacén de claves de Azure que se crea con una cuenta específica o una entidad de servicio no es automáticamente accesible por otra cuenta o entidad de servicio que comparte suscripción Hola.</span><span class="sxs-lookup"><span data-stu-id="d3ed7-157">An Azure Key Vault that's created with a specific account or service principal is not automatically accessible by another account or service principal that shares hello subscription.</span></span> <span data-ttu-id="d3ed7-158">tooallow toouse de entidad de seguridad otra cuenta o servicio Hola el almacén de claves, debe utilizar cuenta de Azure tooadd portal Hola Hola o entidad de servicio.</span><span class="sxs-lookup"><span data-stu-id="d3ed7-158">tooallow another account or service principal toouse hello Key Vault, you must use hello Azure portal tooadd hello account or service principal.</span></span>

    * <span data-ttu-id="d3ed7-159">**New log in credentials** (Nuevas credenciales de inicio de sesión): crea un conjunto de credenciales de inicio de sesión.</span><span class="sxs-lookup"><span data-stu-id="d3ed7-159">**New log in credentials**: Creates a new set of login credentials.</span></span> <span data-ttu-id="d3ed7-160">Si selecciona esta opción, Hola siguientes:</span><span class="sxs-lookup"><span data-stu-id="d3ed7-160">If you select this option, do hello following:</span></span>
    
      * <span data-ttu-id="d3ed7-161">En hello **las credenciales de la máquina virtual** ficha, elija una de hello siguientes opciones para las credenciales de inicio de sesión de máquina virtual de hello del host Docker:</span><span class="sxs-lookup"><span data-stu-id="d3ed7-161">On hello **VM Credentials** tab, choose one of hello following options for hello virtual-machine login credentials of your Docker host:</span></span>

          * <span data-ttu-id="d3ed7-162">**Nombre de usuario**: escriba el nombre de usuario de hello las credenciales de inicio de sesión de máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="d3ed7-162">**Username**: Enter hello username for your virtual machine login credentials.</span></span>
          * <span data-ttu-id="d3ed7-163">**Contraseña** y **confirmar**: escriba la contraseña de hello las credenciales de inicio de sesión de máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="d3ed7-163">**Password** and **Confirm**: Enter hello password for your virtual machine login credentials.</span></span>
          * <span data-ttu-id="d3ed7-164">**SSH**: especifique la configuración de Shell seguro (SSH) de hello para el host de Docker.</span><span class="sxs-lookup"><span data-stu-id="d3ed7-164">**SSH**: Enter hello Secure Shell (SSH) settings for your Docker host.</span></span> <span data-ttu-id="d3ed7-165">Puede elegir entre Hola siguientes opciones:</span><span class="sxs-lookup"><span data-stu-id="d3ed7-165">You can choose from hello following options:</span></span>
            * <span data-ttu-id="d3ed7-166">**None** (Ninguna): especifica que la máquina virtual no permitirá conexiones SSH.</span><span class="sxs-lookup"><span data-stu-id="d3ed7-166">**None**: Specifies that your virtual machine will not allow SSH connections.</span></span>
            * <span data-ttu-id="d3ed7-167">**Generar automáticamente**: automáticamente crea Hola la configuración necesaria para conectarse a través de SSH.</span><span class="sxs-lookup"><span data-stu-id="d3ed7-167">**Auto-generate**: Automatically creates hello requisite settings for connecting via SSH.</span></span>
            * <span data-ttu-id="d3ed7-168">**Import from directory** (Importar desde directorio): especifica un directorio que contiene un conjunto de configuraciones de SSH previamente guardadas.</span><span class="sxs-lookup"><span data-stu-id="d3ed7-168">**Import from directory**: Specifies a directory that contains a set of previously saved SSH settings.</span></span> <span data-ttu-id="d3ed7-169">directorio de Hello debe contener Hola después de dos archivos:</span><span class="sxs-lookup"><span data-stu-id="d3ed7-169">hello directory must contain hello following two files:</span></span>
                * <span data-ttu-id="d3ed7-170">*id_rsa*: contiene la identificación de RSA de Hola para un usuario.</span><span class="sxs-lookup"><span data-stu-id="d3ed7-170">*id_rsa*: Contains hello RSA identification for a user.</span></span>
                * <span data-ttu-id="d3ed7-171">*id_rsa.pub*: contiene la clave pública de hello RSA que se utiliza para la autenticación.</span><span class="sxs-lookup"><span data-stu-id="d3ed7-171">*id_rsa.pub*: Contains hello RSA public key that is used for authentication.</span></span>
        
        ![Create Docker Host (Crear host de Docker)][PUB05]

      * <span data-ttu-id="d3ed7-173">En hello **Docker Daemon credenciales** ficha, especifique Hola siguientes opciones:</span><span class="sxs-lookup"><span data-stu-id="d3ed7-173">On hello **Docker Daemon Credentials** tab, specify hello following options:</span></span>

          * <span data-ttu-id="d3ed7-174">**Puerto de demonio de docker**: escriba el puerto TCP único hello para el host Docker.</span><span class="sxs-lookup"><span data-stu-id="d3ed7-174">**Docker Daemon port**: Enter hello unique TCP port for your Docker host.</span></span>
          * <span data-ttu-id="d3ed7-175">**Seguridad de TLS**: especifique la configuración de seguridad de la capa de transporte de Hola de su host de Docker.</span><span class="sxs-lookup"><span data-stu-id="d3ed7-175">**TLS Security**: Enter hello Transport Layer Security settings for your Docker host.</span></span> <span data-ttu-id="d3ed7-176">Puede elegir entre Hola siguientes opciones:</span><span class="sxs-lookup"><span data-stu-id="d3ed7-176">You can choose from hello following options:</span></span>
            * <span data-ttu-id="d3ed7-177">**None** (Ninguna): especifica que su máquina virtual no permitirá conexiones TLS.</span><span class="sxs-lookup"><span data-stu-id="d3ed7-177">**None**: Specifies that your virtual machine will not allow TLS connections.</span></span>
            * <span data-ttu-id="d3ed7-178">**Generar automáticamente**: automáticamente crea Hola la configuración necesaria para conectarse a través de TLS.</span><span class="sxs-lookup"><span data-stu-id="d3ed7-178">**Auto-generate**: Automatically creates hello requisite settings for connecting via TLS.</span></span>
            * <span data-ttu-id="d3ed7-179">**Import from directory** (Importar desde directorio): especifica un directorio que contiene un conjunto de configuraciones de TLS previamente guardadas.</span><span class="sxs-lookup"><span data-stu-id="d3ed7-179">**Import from directory**: Specifies a directory that contains a set of previously saved TLS settings.</span></span> <span data-ttu-id="d3ed7-180">Más concretamente, el directorio de hello debe contener Hola siguientes seis archivos:</span><span class="sxs-lookup"><span data-stu-id="d3ed7-180">More specifically, hello directory must contain hello following six files:</span></span>
                * <span data-ttu-id="d3ed7-181">*CA.PEM* y *key.pem ca*: contienen el certificado de hello y una clave pública para hello entidad emisora de certificados de TLS.</span><span class="sxs-lookup"><span data-stu-id="d3ed7-181">*ca.pem* and *ca-key.pem*: Contain hello certificate and public key for hello TLS Certificate Authority.</span></span>
                * <span data-ttu-id="d3ed7-182">*CERT.PEM* y *key.pem*: contienen el certificado de cliente de hello y una clave pública que se utiliza para la autenticación TLS.</span><span class="sxs-lookup"><span data-stu-id="d3ed7-182">*cert.pem* and *key.pem*: Contain hello client certificate and public key that is used for TLS authentication.</span></span>
                * <span data-ttu-id="d3ed7-183">*Server.PEM* y *key.pem server*: contienen el certificado de servidor de Hola y de clave pública para el host de Hola.</span><span class="sxs-lookup"><span data-stu-id="d3ed7-183">*server.pem* and *server-key.pem*: Contain hello server certificate and public key for hello host.</span></span>

        ![Create Docker Host (Crear host de Docker)][PUB06]

7. <span data-ttu-id="d3ed7-185">Después de haber escrito todos Hola información anterior, haga clic en **finalizar**.</span><span class="sxs-lookup"><span data-stu-id="d3ed7-185">After you have entered all of hello preceding information, click **Finish**.</span></span>

8. <span data-ttu-id="d3ed7-186">Hola **implementar contenedor de Docker en Azure** asistente, haga clic en **siguiente**.</span><span class="sxs-lookup"><span data-stu-id="d3ed7-186">In hello **Deploy Docker Container on Azure** wizard, click **Next**.</span></span>

   ![Hola implementar contenedor de Docker en el Asistente de Azure][PUB07]

9. <span data-ttu-id="d3ed7-188">Hola **configurar hello Docker contenedor toobe crea** ventana, Hola siguientes:</span><span class="sxs-lookup"><span data-stu-id="d3ed7-188">In hello **Configure hello Docker container toobe created** window, do hello following:</span></span>

   <span data-ttu-id="d3ed7-189">a.</span><span class="sxs-lookup"><span data-stu-id="d3ed7-189">a.</span></span> <span data-ttu-id="d3ed7-190">Hola **nombre del contenedor de Docker** cuadro, escriba un nombre único para el contenedor de Docker.</span><span class="sxs-lookup"><span data-stu-id="d3ed7-190">In hello **Docker container name** box, enter a unique name for your Docker container.</span></span>

   <span data-ttu-id="d3ed7-191">b.</span><span class="sxs-lookup"><span data-stu-id="d3ed7-191">b.</span></span> <span data-ttu-id="d3ed7-192">Elija uno de hello después de imágenes de Docker:</span><span class="sxs-lookup"><span data-stu-id="d3ed7-192">Choose one of hello following Docker images:</span></span>
     * <span data-ttu-id="d3ed7-193">**Predefined Docker image** (Imagen de Docker predefinida): especifica una imagen de Docker preexistente de Azure.</span><span class="sxs-lookup"><span data-stu-id="d3ed7-193">**Predefined Docker image**: Specifies a pre-existing Docker image from Azure.</span></span>

       >[!NOTE]
       ><span data-ttu-id="d3ed7-194">Hola lista de imágenes de Docker en este cuadro está formada por varias imágenes que hello Azure Toolkit ha sido configurado toopatch para que el artefacto se implementa automáticamente.</span><span class="sxs-lookup"><span data-stu-id="d3ed7-194">hello list of Docker images in this box consists of several images that hello Azure Toolkit has been configured toopatch so that your artifact is deployed automatically.</span></span>

     * <span data-ttu-id="d3ed7-195">**Custom Dockerfile** (Dockerfile personalizado): especifica un Dockerfile guardado antes desde el equipo local.</span><span class="sxs-lookup"><span data-stu-id="d3ed7-195">**Custom Dockerfile**: Specifies a previously saved Dockerfile from your local computer.</span></span>

       >[!NOTE]
       ><span data-ttu-id="d3ed7-196">Se trata de una característica más avanzada para los desarrolladores que deseen toodeploy su propios Dockerfile.</span><span class="sxs-lookup"><span data-stu-id="d3ed7-196">This is a more advanced feature for developers who want toodeploy their own Dockerfile.</span></span> <span data-ttu-id="d3ed7-197">Sin embargo, resulta una toodevelopers que usan este tooensure opción que sus Dockerfile se ha creado correctamente.</span><span class="sxs-lookup"><span data-stu-id="d3ed7-197">However, it is up toodevelopers who use this option tooensure that their Dockerfile is built correctly.</span></span> <span data-ttu-id="d3ed7-198">Hola Kit de herramientas de Azure no validar el contenido de hello en un archivo Dockerfile personalizado, por lo que puede producir un error en la implementación de Hola si hello Dockerfile tiene problemas.</span><span class="sxs-lookup"><span data-stu-id="d3ed7-198">hello Azure Toolkit does not validate hello content in a custom Dockerfile, so hello deployment might fail if hello Dockerfile has issues.</span></span> <span data-ttu-id="d3ed7-199">Además, hello Azure Toolkit espera Hola personalizado Dockerfile toocontain un artefacto de la aplicación web y tratará de tooopen una conexión HTTP.</span><span class="sxs-lookup"><span data-stu-id="d3ed7-199">In addition, hello Azure Toolkit expects hello custom Dockerfile toocontain a web app artifact, and it will attempt tooopen an HTTP connection.</span></span> <span data-ttu-id="d3ed7-200">Si los desarrolladores publican un tipo diferente de artefacto, podrían recibir errores inofensivos después de la implementación.</span><span class="sxs-lookup"><span data-stu-id="d3ed7-200">If developers publish a different type of artifact, they may receive innocuous errors after deployment.</span></span>

   <span data-ttu-id="d3ed7-201">c.</span><span class="sxs-lookup"><span data-stu-id="d3ed7-201">c.</span></span> <span data-ttu-id="d3ed7-202">**Configuración de puertos**: especifique el enlace de puerto TCP único de hello para el contenedor de Docker.</span><span class="sxs-lookup"><span data-stu-id="d3ed7-202">**Port settings**: Enter hello unique TCP port binding for your Docker container.</span></span>

     ![ventana de Hello configurar hello Docker contenedor toobe creado][PUB08]

10. <span data-ttu-id="d3ed7-204">Después de haber completado todos los pasos anteriores de Hola, haga clic en **finalizar**.</span><span class="sxs-lookup"><span data-stu-id="d3ed7-204">After you have completed all of hello preceding steps, click **Finish**.</span></span>

<span data-ttu-id="d3ed7-205">Hello Azure Toolkit comienza implementar su tooAzure de aplicación web en un contenedor de Docker.</span><span class="sxs-lookup"><span data-stu-id="d3ed7-205">hello Azure Toolkit begins deploying your web app tooAzure in a Docker container.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="d3ed7-206">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="d3ed7-206">Next steps</span></span>
<span data-ttu-id="d3ed7-207">Para obtener más información acerca de hello kits de herramientas de Azure para Java IDE, vea Hola recursos siguientes:</span><span class="sxs-lookup"><span data-stu-id="d3ed7-207">For more information about hello Azure Toolkits for Java IDEs, see hello following resources:</span></span>

* <span data-ttu-id="d3ed7-208">[Kit de herramientas de Azure para Eclipse]</span><span class="sxs-lookup"><span data-stu-id="d3ed7-208">[Azure Toolkit for Eclipse]</span></span>
  * <span data-ttu-id="d3ed7-209">[Novedades de hello Azure Toolkit for Eclipse]</span><span class="sxs-lookup"><span data-stu-id="d3ed7-209">[What's new in hello Azure Toolkit for Eclipse]</span></span>
  * <span data-ttu-id="d3ed7-210">[Instalar hello Azure Toolkit for Eclipse]</span><span class="sxs-lookup"><span data-stu-id="d3ed7-210">[Installing hello Azure Toolkit for Eclipse]</span></span>
  * <span data-ttu-id="d3ed7-211">[Instrucciones de inicio de sesión para hello Azure Toolkit for Eclipse]</span><span class="sxs-lookup"><span data-stu-id="d3ed7-211">[Sign-in instructions for hello Azure Toolkit for Eclipse]</span></span>
  * <span data-ttu-id="d3ed7-212">[Creación de una aplicación web Hello World para Azure en Eclipse]</span><span class="sxs-lookup"><span data-stu-id="d3ed7-212">[Create a Hello World web app for Azure in Eclipse]</span></span>
* <span data-ttu-id="d3ed7-213">[Kit de herramientas de Azure para IntelliJ]</span><span class="sxs-lookup"><span data-stu-id="d3ed7-213">[Azure Toolkit for IntelliJ]</span></span>
  * <span data-ttu-id="d3ed7-214">[Novedades de hello Azure Toolkit for IntelliJ]</span><span class="sxs-lookup"><span data-stu-id="d3ed7-214">[What's new in hello Azure Toolkit for IntelliJ]</span></span>
  * <span data-ttu-id="d3ed7-215">[Instalación hello Azure Toolkit for IntelliJ]</span><span class="sxs-lookup"><span data-stu-id="d3ed7-215">[Installing hello Azure Toolkit for IntelliJ]</span></span>
  * <span data-ttu-id="d3ed7-216">[Instrucciones de inicio de sesión para hello Azure Toolkit para IntelliJ]</span><span class="sxs-lookup"><span data-stu-id="d3ed7-216">[Sign-in instructions for hello Azure Toolkit for IntelliJ]</span></span>
  * <span data-ttu-id="d3ed7-217">[Creación de una aplicación web Hello World para Azure en IntelliJ]</span><span class="sxs-lookup"><span data-stu-id="d3ed7-217">[Create a Hello World web app for Azure in IntelliJ]</span></span>

<span data-ttu-id="d3ed7-218">Para obtener más información sobre el uso de Azure con Java, vea el [Centro para desarrolladores de Java de Azure] y la página de [herramientas de Java para Visual Studio Team Services].</span><span class="sxs-lookup"><span data-stu-id="d3ed7-218">For more information about using Azure with Java, see [Azure Java Developer Center] and [Java Tools for Visual Studio Team Services].</span></span>

<span data-ttu-id="d3ed7-219">Para obtener recursos adicionales de Docker, consulte oficial de hello [sitio Web de Docker].</span><span class="sxs-lookup"><span data-stu-id="d3ed7-219">For additional resources for Docker, see hello official [Docker website].</span></span>

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

<!-- IMG List -->

[PUB01]: ./media/azure-toolkit-for-eclipse-publish-as-docker-container/PUB01.png
[PUB02]: ./media/azure-toolkit-for-eclipse-publish-as-docker-container/PUB02.png
[PUB03]: ./media/azure-toolkit-for-eclipse-publish-as-docker-container/PUB03.png
[PUB04a]: ./media/azure-toolkit-for-eclipse-publish-as-docker-container/PUB04a.png
[PUB04b]: ./media/azure-toolkit-for-eclipse-publish-as-docker-container/PUB04b.png
[PUB04c]: ./media/azure-toolkit-for-eclipse-publish-as-docker-container/PUB04c.png
[PUB04d]: ./media/azure-toolkit-for-eclipse-publish-as-docker-container/PUB04d.png
[PUB05]: ./media/azure-toolkit-for-eclipse-publish-as-docker-container/PUB05.png
[PUB06]: ./media/azure-toolkit-for-eclipse-publish-as-docker-container/PUB06.png
[PUB07]: ./media/azure-toolkit-for-eclipse-publish-as-docker-container/PUB07.png
[PUB08]: ./media/azure-toolkit-for-eclipse-publish-as-docker-container/PUB08.png