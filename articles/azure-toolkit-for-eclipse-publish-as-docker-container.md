---
title: "Publicación de un contenedor de Docker con el kit de herramientas de Azure para Eclipse| Microsoft Docs"
description: "Aprenda a publicar una aplicación web en Microsoft Azure como un contenedor de Docker con el kit de herramientas de Azure para Eclipse."
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
ms.openlocfilehash: 746bb0a073396b84fa8592adda6748a2a5692ee8
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="publish-a-web-app-as-a-docker-container-by-using-the-azure-toolkit-for-eclipse"></a><span data-ttu-id="32df1-103">Publicación de una aplicación web como contenedor de Docker con el kit de herramientas de Azure para Eclipse</span><span class="sxs-lookup"><span data-stu-id="32df1-103">Publish a web app as a Docker container by using the Azure Toolkit for Eclipse</span></span>

<span data-ttu-id="32df1-104">Los contenedores de Docker son un método muy utilizado para implementar aplicaciones web.</span><span class="sxs-lookup"><span data-stu-id="32df1-104">Docker containers are a widely used method for deploying web applications.</span></span> <span data-ttu-id="32df1-105">Usando contenedores de Docker, los desarrolladores pueden consolidar todos sus archivos de proyecto y dependencias en un único paquete para implementarlo en un servidor.</span><span class="sxs-lookup"><span data-stu-id="32df1-105">By using Docker containers, developers can consolidate all their project files and dependencies into a single package for deployment to a server.</span></span> <span data-ttu-id="32df1-106">El kit de herramientas de Azure para Eclipse simplifica este proceso para los desarrolladores de Java, ya que agrega características de *publicación como contenedor de Docker* para su implementación en Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="32df1-106">The Azure Toolkit for Eclipse simplifies this process for Java developers by adding *Publish as Docker Container* features for deployment to Microsoft Azure.</span></span> <span data-ttu-id="32df1-107">En este artículo se le guía por los pasos necesarios para publicar aplicaciones en Azure como contenedores de Docker.</span><span class="sxs-lookup"><span data-stu-id="32df1-107">This article walks you through the steps required to publish your applications to Azure as Docker containers.</span></span>

> [!NOTE]
> <span data-ttu-id="32df1-108">Hay más información disponible sobre Docker en el [sitio web de Docker].</span><span class="sxs-lookup"><span data-stu-id="32df1-108">More information about Docker is available on the [Docker website].</span></span>
>

[!INCLUDE [azure-toolkit-for-eclipse-prerequisites](../includes/azure-toolkit-for-eclipse-prerequisites.md)]

## <a name="publish-your-web-app-to-azure-by-using-a-docker-container"></a><span data-ttu-id="32df1-109">Publicación de su aplicación web en Azure mediante un contenedor de Docker</span><span class="sxs-lookup"><span data-stu-id="32df1-109">Publish your web app to Azure by using a Docker container</span></span>

1. <span data-ttu-id="32df1-110">Abra el proyecto de aplicación web en Eclipse.</span><span class="sxs-lookup"><span data-stu-id="32df1-110">Open your web app project in Eclipse.</span></span>

2. <span data-ttu-id="32df1-111">Para iniciar el asistente **Publish as Docker Container** (Publicar como contenedor de Docker), realice una de las siguientes acciones:</span><span class="sxs-lookup"><span data-stu-id="32df1-111">To start the **Publish as Docker Container** wizard, do either of the following:</span></span>

   * <span data-ttu-id="32df1-112">En la vista **Navegador**, haga clic con el botón derecho en el proyecto y haga clic en **Azure** y en **Publish as Docker Container** (Publicar como contenedor de Docker).</span><span class="sxs-lookup"><span data-stu-id="32df1-112">In the **Navigator** view, right-click your project, click **Azure**, and then click **Publish as Docker Container**.</span></span>

      ![Vista de navegador del comando Publish as Docker Container (Publicar como contenedor de Docker)][PUB01]

   * <span data-ttu-id="32df1-114">En la barra de herramientas de Eclipse, haga clic en el botón **Publish** (Publicar) y en **Publish as Docker Container** (Publicar como contenedor de Docker).</span><span class="sxs-lookup"><span data-stu-id="32df1-114">On the Eclipse toolbar, click the **Publish** button, and then click **Publish as Docker Container**.</span></span>

      ![Barra de herramientas de Eclipse del comando Publish as Docker Container (Publicar como contenedor de Docker)][PUB02]
      
    <span data-ttu-id="32df1-116">Se abre el asistente **Deploy Docker Container on Azure** (Implementar contenedor de Docker en Azure).</span><span class="sxs-lookup"><span data-stu-id="32df1-116">The **Deploy Docker Container on Azure** wizard opens.</span></span>

    ![Asistente Deploy Docker Container on Azure (Implementar contenedor de Docker en Azure)][PUB03]

3. <span data-ttu-id="32df1-118">En la ventana **Type an image name, select the artifact's path and check a Docker host to be used** (Escriba un nombre de imagen, seleccione la ruta de acceso del artefacto y elija el host de Docker que se usará), haga lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="32df1-118">In the **Type an image name, select the artifact's path and check a Docker host to be used** window, do the following:</span></span>

    <span data-ttu-id="32df1-119">a.</span><span class="sxs-lookup"><span data-stu-id="32df1-119">a.</span></span> <span data-ttu-id="32df1-120">En el cuadro **Docker image name** (Nombre de imagen de Docker), escriba un nombre único para el host de Docker.</span><span class="sxs-lookup"><span data-stu-id="32df1-120">In the **Docker image name** box, enter a unique name for your Docker host.</span></span> <span data-ttu-id="32df1-121">(El asistente crea automáticamente un nombre, pero se puede modificar).</span><span class="sxs-lookup"><span data-stu-id="32df1-121">(The wizard automatically creates a name, but you can modify it.)</span></span>

    <span data-ttu-id="32df1-122">b.</span><span class="sxs-lookup"><span data-stu-id="32df1-122">b.</span></span> <span data-ttu-id="32df1-123">En el área **Hosts**, se muestran todos los hosts de Docker que ya haya creado.</span><span class="sxs-lookup"><span data-stu-id="32df1-123">The **Hosts** area displays any Docker hosts that you have already created.</span></span> <span data-ttu-id="32df1-124">Realice cualquiera de las siguientes acciones:</span><span class="sxs-lookup"><span data-stu-id="32df1-124">Do either of the following:</span></span>

    * <span data-ttu-id="32df1-125">Si tiene un host de Docker existente, puede implementar la aplicación web en él.</span><span class="sxs-lookup"><span data-stu-id="32df1-125">If you have an existing Docker host, you can deploy your web app to it.</span></span>
    * <span data-ttu-id="32df1-126">Para crear un nuevo host de Docker, haga clic en **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="32df1-126">To create a new Docker host, click **Add**.</span></span>  
      
    <span data-ttu-id="32df1-127">Se abre el cuadro de diálogo **Create Docker Host** (Crear host de Docker).</span><span class="sxs-lookup"><span data-stu-id="32df1-127">The **Create Docker Host** dialog box opens.</span></span>

    ![Asistente Deploy Docker Container on Azure (Implementar contenedor de Docker en Azure)][PUB04a]

4. <span data-ttu-id="32df1-129">En la ventana **Configure the new virtual machine** (Configurar la nueva máquina virtual), especifique las siguientes opciones de su host de Docker</span><span class="sxs-lookup"><span data-stu-id="32df1-129">In the **Configure the new virtual machine** window, specify the following options for your Docker host.</span></span> <span data-ttu-id="32df1-130">(el asistente genera automáticamente la mayor parte de las opciones, pero puede modificarla).</span><span class="sxs-lookup"><span data-stu-id="32df1-130">(The wizard automatically generates most of the options for you, but you can modify any of them.)</span></span>

   <span data-ttu-id="32df1-131">a.</span><span class="sxs-lookup"><span data-stu-id="32df1-131">a.</span></span> <span data-ttu-id="32df1-132">**Name** (Nombre): escriba un nombre único para el host de Docker</span><span class="sxs-lookup"><span data-stu-id="32df1-132">**Name**: Enter a unique name for the Docker host.</span></span> <span data-ttu-id="32df1-133">(no es lo mismo que el nombre de imagen de Docker que especificó antes).</span><span class="sxs-lookup"><span data-stu-id="32df1-133">(It is not the same as the Docker image name that you specified earlier.)</span></span>

   <span data-ttu-id="32df1-134">b.</span><span class="sxs-lookup"><span data-stu-id="32df1-134">b.</span></span> <span data-ttu-id="32df1-135">**Subscription** (Suscripción): escriba la suscripción de Azure que usa para el host.</span><span class="sxs-lookup"><span data-stu-id="32df1-135">**Subscription**: Enter the Azure subscription that you use for your host.</span></span>

   <span data-ttu-id="32df1-136">c.</span><span class="sxs-lookup"><span data-stu-id="32df1-136">c.</span></span> <span data-ttu-id="32df1-137">**Region** (Región): escriba la región geográfica donde se encuentra el host.</span><span class="sxs-lookup"><span data-stu-id="32df1-137">**Region**: Enter the geographical region where your host is located.</span></span>

   <span data-ttu-id="32df1-138">d.</span><span class="sxs-lookup"><span data-stu-id="32df1-138">d.</span></span> <span data-ttu-id="32df1-139">En la pestaña **Host OS and Size** (Sistema operativo y tamaño del host):</span><span class="sxs-lookup"><span data-stu-id="32df1-139">On the **Host OS and Size** tab:</span></span>
     * <span data-ttu-id="32df1-140">**Host OS** (Sistema operativo de host): escriba el sistema operativo de la máquina virtual que contiene el host.</span><span class="sxs-lookup"><span data-stu-id="32df1-140">**Host OS**: Enter the operating system for the virtual machine that contains your host.</span></span>
     * <span data-ttu-id="32df1-141">**Size** (Tamaño): escriba el tamaño de la máquina virtual del host.</span><span class="sxs-lookup"><span data-stu-id="32df1-141">**Size**: Enter the virtual-machine size for your host.</span></span>

   <span data-ttu-id="32df1-142">e.</span><span class="sxs-lookup"><span data-stu-id="32df1-142">e.</span></span> <span data-ttu-id="32df1-143">En la pestaña **Resource Group** (Grupo de recursos):</span><span class="sxs-lookup"><span data-stu-id="32df1-143">On the **Resource Group** tab:</span></span>
     * <span data-ttu-id="32df1-144">**New resource group** (Nuevo grupo de recursos): cree un grupo de recursos para el host.</span><span class="sxs-lookup"><span data-stu-id="32df1-144">**New resource group**: Create a new resource group for your host.</span></span>
     * <span data-ttu-id="32df1-145">**Existing resource group** (Grupo de recursos existente): especifique un grupo de recursos existente desde su cuenta de Azure.</span><span class="sxs-lookup"><span data-stu-id="32df1-145">**Existing resource group**: Enter an existing resource group from your Azure account.</span></span>

   <span data-ttu-id="32df1-146">f.</span><span class="sxs-lookup"><span data-stu-id="32df1-146">f.</span></span> <span data-ttu-id="32df1-147">En la pestaña**Network** (Red):</span><span class="sxs-lookup"><span data-stu-id="32df1-147">On the **Network** tab:</span></span>
     * <span data-ttu-id="32df1-148">**New virtual network** (Nueva red virtual): cree una red virtual para el host.</span><span class="sxs-lookup"><span data-stu-id="32df1-148">**New virtual network**: Create a new virtual network for your host.</span></span>
     * <span data-ttu-id="32df1-149">**Existing virtual network** (Red virtual existente): especifique una red virtual existente desde su cuenta de Azure.</span><span class="sxs-lookup"><span data-stu-id="32df1-149">**Existing virtual network**: Enter an existing virtual network from your Azure account.</span></span>

   <span data-ttu-id="32df1-150">g.</span><span class="sxs-lookup"><span data-stu-id="32df1-150">g.</span></span> <span data-ttu-id="32df1-151">Haga clic en la pestaña **Storage** (Almacenamiento):</span><span class="sxs-lookup"><span data-stu-id="32df1-151">On the **Storage** tab:</span></span>
     * <span data-ttu-id="32df1-152">**New storage account** (Nueva cuenta de almacenamiento): cree una cuenta de almacenamiento para el host.</span><span class="sxs-lookup"><span data-stu-id="32df1-152">**New storage account**: Create a new storage account for your host.</span></span>
     * <span data-ttu-id="32df1-153">**Existing storage account** (Cuenta de almacenamiento existente): especifique una cuenta de almacenamiento existente desde su cuenta de Azure.</span><span class="sxs-lookup"><span data-stu-id="32df1-153">**Existing storage account**: Enter an existing storage account from your Azure account.</span></span>

5. <span data-ttu-id="32df1-154">Haga clic en **Siguiente**.</span><span class="sxs-lookup"><span data-stu-id="32df1-154">Click **Next**.</span></span>

6. <span data-ttu-id="32df1-155">En la ventana **Configure log in credentials and port settings** (Configurar credenciales de inicio de sesión y configuración de puerto), seleccione una de las siguientes opciones:</span><span class="sxs-lookup"><span data-stu-id="32df1-155">In the **Configure log in credentials and port settings** window, select one of the following options:</span></span>

    * <span data-ttu-id="32df1-156">**Import credentials from Azure Key Vault** (Importar credenciales de Azure Key Vault): especifique un conjunto de credenciales previamente guardadas que están almacenadas en la suscripción de Azure.</span><span class="sxs-lookup"><span data-stu-id="32df1-156">**Import credentials from Azure Key Vault**: Specifies a previously saved set of credentials that are stored in your Azure subscription.</span></span>

      >[!NOTE]
      ><span data-ttu-id="32df1-157">Una instancia de Azure Key Vault que se crea con una cuenta o entidad de servicio específica no es accesible automáticamente para otra cuenta o entidad de servicio que comparta la suscripción.</span><span class="sxs-lookup"><span data-stu-id="32df1-157">An Azure Key Vault that's created with a specific account or service principal is not automatically accessible by another account or service principal that shares the subscription.</span></span> <span data-ttu-id="32df1-158">Para permitir que otra cuenta o entidad de servicio use la instancia de Key Vault, debe usar Azure Portal para agregar la cuenta o entidad de servicio.</span><span class="sxs-lookup"><span data-stu-id="32df1-158">To allow another account or service principal to use the Key Vault, you must use the Azure portal to add the account or service principal.</span></span>

    * <span data-ttu-id="32df1-159">**New log in credentials** (Nuevas credenciales de inicio de sesión): crea un conjunto de credenciales de inicio de sesión.</span><span class="sxs-lookup"><span data-stu-id="32df1-159">**New log in credentials**: Creates a new set of login credentials.</span></span> <span data-ttu-id="32df1-160">Si selecciona esta opción, haga lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="32df1-160">If you select this option, do the following:</span></span>
    
      * <span data-ttu-id="32df1-161">En la pestaña **VM Credentials** (Credenciales de máquina virtual), elija una de las siguientes opciones para el inicio de sesión de máquina virtual del host de Docker:</span><span class="sxs-lookup"><span data-stu-id="32df1-161">On the **VM Credentials** tab, choose one of the following options for the virtual-machine login credentials of your Docker host:</span></span>

          * <span data-ttu-id="32df1-162">**Username** (Nombre de usuario): especifica el nombre de usuario de las credenciales inicio de sesión de la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="32df1-162">**Username**: Enter the username for your virtual machine login credentials.</span></span>
          * <span data-ttu-id="32df1-163">**Password** (Contraseña) y **Confirm** (Confirmar): escriba la contraseña para las credenciales del inicio de sesión de la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="32df1-163">**Password** and **Confirm**: Enter the password for your virtual machine login credentials.</span></span>
          * <span data-ttu-id="32df1-164">**SSH**: especifique la configuración de Secure Shell (SSH) para el host de Docker.</span><span class="sxs-lookup"><span data-stu-id="32df1-164">**SSH**: Enter the Secure Shell (SSH) settings for your Docker host.</span></span> <span data-ttu-id="32df1-165">Puede elegir entre las siguientes opciones:</span><span class="sxs-lookup"><span data-stu-id="32df1-165">You can choose from the following options:</span></span>
            * <span data-ttu-id="32df1-166">**None** (Ninguna): especifica que la máquina virtual no permitirá conexiones SSH.</span><span class="sxs-lookup"><span data-stu-id="32df1-166">**None**: Specifies that your virtual machine will not allow SSH connections.</span></span>
            * <span data-ttu-id="32df1-167">**Auto-generate** (Generar automáticamente): crea automáticamente la configuración necesaria para la conexión mediante SSH.</span><span class="sxs-lookup"><span data-stu-id="32df1-167">**Auto-generate**: Automatically creates the requisite settings for connecting via SSH.</span></span>
            * <span data-ttu-id="32df1-168">**Import from directory** (Importar desde directorio): especifica un directorio que contiene un conjunto de configuraciones de SSH previamente guardadas.</span><span class="sxs-lookup"><span data-stu-id="32df1-168">**Import from directory**: Specifies a directory that contains a set of previously saved SSH settings.</span></span> <span data-ttu-id="32df1-169">El directorio debe contener los dos archivos siguientes:</span><span class="sxs-lookup"><span data-stu-id="32df1-169">The directory must contain the following two files:</span></span>
                * <span data-ttu-id="32df1-170">*id_rsa*: contiene la identificación de RSA de un usuario.</span><span class="sxs-lookup"><span data-stu-id="32df1-170">*id_rsa*: Contains the RSA identification for a user.</span></span>
                * <span data-ttu-id="32df1-171">*id_rsa.pub*: contiene la clave pública de RSA que se usa para la autenticación.</span><span class="sxs-lookup"><span data-stu-id="32df1-171">*id_rsa.pub*: Contains the RSA public key that is used for authentication.</span></span>
        
        ![Create Docker Host (Crear host de Docker)][PUB05]

      * <span data-ttu-id="32df1-173">En la pestaña **Docker Daemon Credentials** (Credenciales demonio de Docker), especifique las siguientes opciones:</span><span class="sxs-lookup"><span data-stu-id="32df1-173">On the **Docker Daemon Credentials** tab, specify the following options:</span></span>

          * <span data-ttu-id="32df1-174">**Docker Daemon port** (Puerto de demonio de Docker): especifica el puerto TCP único de su host de Docker.</span><span class="sxs-lookup"><span data-stu-id="32df1-174">**Docker Daemon port**: Enter the unique TCP port for your Docker host.</span></span>
          * <span data-ttu-id="32df1-175">**Seguridad de TLS**: especifique la configuración de seguridad de la capa de transporte para el host de Docker.</span><span class="sxs-lookup"><span data-stu-id="32df1-175">**TLS Security**: Enter the Transport Layer Security settings for your Docker host.</span></span> <span data-ttu-id="32df1-176">Puede elegir entre las siguientes opciones:</span><span class="sxs-lookup"><span data-stu-id="32df1-176">You can choose from the following options:</span></span>
            * <span data-ttu-id="32df1-177">**None** (Ninguna): especifica que su máquina virtual no permitirá conexiones TLS.</span><span class="sxs-lookup"><span data-stu-id="32df1-177">**None**: Specifies that your virtual machine will not allow TLS connections.</span></span>
            * <span data-ttu-id="32df1-178">**Auto-generate** (Generar automáticamente): crea automáticamente la configuración necesaria para la conexión mediante TLS.</span><span class="sxs-lookup"><span data-stu-id="32df1-178">**Auto-generate**: Automatically creates the requisite settings for connecting via TLS.</span></span>
            * <span data-ttu-id="32df1-179">**Import from directory** (Importar desde directorio): especifica un directorio que contiene un conjunto de configuraciones de TLS previamente guardadas.</span><span class="sxs-lookup"><span data-stu-id="32df1-179">**Import from directory**: Specifies a directory that contains a set of previously saved TLS settings.</span></span> <span data-ttu-id="32df1-180">Más concretamente, el directorio debe contener los seis archivos siguientes:</span><span class="sxs-lookup"><span data-stu-id="32df1-180">More specifically, the directory must contain the following six files:</span></span>
                * <span data-ttu-id="32df1-181">*ca.pem* y *ca-key.pem*: contienen el certificado y la clave pública de la entidad de certificación de TLS.</span><span class="sxs-lookup"><span data-stu-id="32df1-181">*ca.pem* and *ca-key.pem*: Contain the certificate and public key for the TLS Certificate Authority.</span></span>
                * <span data-ttu-id="32df1-182">*cert.pem* y *key.pem*: contienen el certificado de cliente y la clave pública que se usarán para la autenticación TLS.</span><span class="sxs-lookup"><span data-stu-id="32df1-182">*cert.pem* and *key.pem*: Contain the client certificate and public key that is used for TLS authentication.</span></span>
                * <span data-ttu-id="32df1-183">*server.pem* y *server-key.pem*: contienen el certificado de servidor y la clave pública del host.</span><span class="sxs-lookup"><span data-stu-id="32df1-183">*server.pem* and *server-key.pem*: Contain the server certificate and public key for the host.</span></span>

        ![Create Docker Host (Crear host de Docker)][PUB06]

7. <span data-ttu-id="32df1-185">Después de haber escrito toda la información anterior, haga clic en **Finish** (Finalizar).</span><span class="sxs-lookup"><span data-stu-id="32df1-185">After you have entered all of the preceding information, click **Finish**.</span></span>

8. <span data-ttu-id="32df1-186">En el asistente **Deploy Docker Container on Azure** (Implementar contenedor de Docker en Azure), haga clic en **Next** (Siguiente).</span><span class="sxs-lookup"><span data-stu-id="32df1-186">In the **Deploy Docker Container on Azure** wizard, click **Next**.</span></span>

   ![Asistente Deploy Docker Container on Azure (Implementar contenedor de Docker en Azure)][PUB07]

9. <span data-ttu-id="32df1-188">En la ventana **Configure the Docker container to be created** (Configurar el contenedor de Docker que se va a crear), realice lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="32df1-188">In the **Configure the Docker container to be created** window, do the following:</span></span>

   <span data-ttu-id="32df1-189">a.</span><span class="sxs-lookup"><span data-stu-id="32df1-189">a.</span></span> <span data-ttu-id="32df1-190">En el cuadro **Docker container name** (Nombre del contenedor de Docker), escriba un nombre único para el contenedor de Docker.</span><span class="sxs-lookup"><span data-stu-id="32df1-190">In the **Docker container name** box, enter a unique name for your Docker container.</span></span>

   <span data-ttu-id="32df1-191">b.</span><span class="sxs-lookup"><span data-stu-id="32df1-191">b.</span></span> <span data-ttu-id="32df1-192">Elija una de las siguientes imágenes de Docker:</span><span class="sxs-lookup"><span data-stu-id="32df1-192">Choose one of the following Docker images:</span></span>
     * <span data-ttu-id="32df1-193">**Predefined Docker image** (Imagen de Docker predefinida): especifica una imagen de Docker preexistente de Azure.</span><span class="sxs-lookup"><span data-stu-id="32df1-193">**Predefined Docker image**: Specifies a pre-existing Docker image from Azure.</span></span>

       >[!NOTE]
       ><span data-ttu-id="32df1-194">La lista de imágenes de Docker de este cuadro consta de varias imágenes para las que se ha configurado el kit de herramientas de Azure para aplicar revisiones, de modo que su artefacto se implementa automáticamente.</span><span class="sxs-lookup"><span data-stu-id="32df1-194">The list of Docker images in this box consists of several images that the Azure Toolkit has been configured to patch so that your artifact is deployed automatically.</span></span>

     * <span data-ttu-id="32df1-195">**Custom Dockerfile** (Dockerfile personalizado): especifica un Dockerfile guardado antes desde el equipo local.</span><span class="sxs-lookup"><span data-stu-id="32df1-195">**Custom Dockerfile**: Specifies a previously saved Dockerfile from your local computer.</span></span>

       >[!NOTE]
       ><span data-ttu-id="32df1-196">Esta es una característica más avanzada para desarrolladores que deseen implementar su propio Dockerfile.</span><span class="sxs-lookup"><span data-stu-id="32df1-196">This is a more advanced feature for developers who want to deploy their own Dockerfile.</span></span> <span data-ttu-id="32df1-197">Sin embargo, es responsabilidad de los desarrolladores que usen esta opción asegurarse de que su Dockerfile se ha creado correctamente.</span><span class="sxs-lookup"><span data-stu-id="32df1-197">However, it is up to developers who use this option to ensure that their Dockerfile is built correctly.</span></span> <span data-ttu-id="32df1-198">El kit de herramientas de Azure no valida el contenido de un Dockerfile personalizado, por lo que la implementación puede dar error si el Dockerfile tiene problemas.</span><span class="sxs-lookup"><span data-stu-id="32df1-198">The Azure Toolkit does not validate the content in a custom Dockerfile, so the deployment might fail if the Dockerfile has issues.</span></span> <span data-ttu-id="32df1-199">Además, dado que el kit de herramientas de Azure espera que el Dockerfile personalizado contenga un artefacto de aplicación web, intenta abrir una conexión HTTP.</span><span class="sxs-lookup"><span data-stu-id="32df1-199">In addition, the Azure Toolkit expects the custom Dockerfile to contain a web app artifact, and it will attempt to open an HTTP connection.</span></span> <span data-ttu-id="32df1-200">Si los desarrolladores publican un tipo diferente de artefacto, podrían recibir errores inofensivos después de la implementación.</span><span class="sxs-lookup"><span data-stu-id="32df1-200">If developers publish a different type of artifact, they may receive innocuous errors after deployment.</span></span>

   <span data-ttu-id="32df1-201">c.</span><span class="sxs-lookup"><span data-stu-id="32df1-201">c.</span></span> <span data-ttu-id="32df1-202">**Port settings** (Configuración de puerto): escriba el enlace de puerto TCP único para su contenedor de Docker.</span><span class="sxs-lookup"><span data-stu-id="32df1-202">**Port settings**: Enter the unique TCP port binding for your Docker container.</span></span>

     ![Ventana Configure the Docker container to be created (Configurar el contenedor de Docker que se va a crear)][PUB08]

10. <span data-ttu-id="32df1-204">Después de completar todos los pasos anteriores, haga clic en **Finish** (Finalizar).</span><span class="sxs-lookup"><span data-stu-id="32df1-204">After you have completed all of the preceding steps, click **Finish**.</span></span>

<span data-ttu-id="32df1-205">El kit de herramientas de Azure comienza a implementar la aplicación web en Azure en un contenedor de Docker.</span><span class="sxs-lookup"><span data-stu-id="32df1-205">The Azure Toolkit begins deploying your web app to Azure in a Docker container.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="32df1-206">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="32df1-206">Next steps</span></span>
<span data-ttu-id="32df1-207">Para más información sobre los kits de herramientas de Azure para los IDE de Java, consulte los siguientes recursos:</span><span class="sxs-lookup"><span data-stu-id="32df1-207">For more information about the Azure Toolkits for Java IDEs, see the following resources:</span></span>

* <span data-ttu-id="32df1-208">[Kit de herramientas de Azure para Eclipse]</span><span class="sxs-lookup"><span data-stu-id="32df1-208">[Azure Toolkit for Eclipse]</span></span>
  * <span data-ttu-id="32df1-209">[Novedades del kit de herramientas de Azure para Eclipse]</span><span class="sxs-lookup"><span data-stu-id="32df1-209">[What's new in the Azure Toolkit for Eclipse]</span></span>
  * <span data-ttu-id="32df1-210">[Instalación del Kit de herramientas de Azure para Eclipse]</span><span class="sxs-lookup"><span data-stu-id="32df1-210">[Installing the Azure Toolkit for Eclipse]</span></span>
  * <span data-ttu-id="32df1-211">[Instrucciones de inicio de sesión del kit de herramientas de Azure para Eclipse]</span><span class="sxs-lookup"><span data-stu-id="32df1-211">[Sign-in instructions for the Azure Toolkit for Eclipse]</span></span>
  * <span data-ttu-id="32df1-212">[Creación de una aplicación web Hello World para Azure en Eclipse]</span><span class="sxs-lookup"><span data-stu-id="32df1-212">[Create a Hello World web app for Azure in Eclipse]</span></span>
* <span data-ttu-id="32df1-213">[Kit de herramientas de Azure para IntelliJ]</span><span class="sxs-lookup"><span data-stu-id="32df1-213">[Azure Toolkit for IntelliJ]</span></span>
  * <span data-ttu-id="32df1-214">[Novedades del kit de herramientas de Azure para IntelliJ]</span><span class="sxs-lookup"><span data-stu-id="32df1-214">[What's new in the Azure Toolkit for IntelliJ]</span></span>
  * <span data-ttu-id="32df1-215">[Instalación del kit de herramientas de Azure para IntelliJ]</span><span class="sxs-lookup"><span data-stu-id="32df1-215">[Installing the Azure Toolkit for IntelliJ]</span></span>
  * <span data-ttu-id="32df1-216">[Instrucciones de inicio de sesión del kit de herramientas de Azure para IntelliJ]</span><span class="sxs-lookup"><span data-stu-id="32df1-216">[Sign-in instructions for the Azure Toolkit for IntelliJ]</span></span>
  * <span data-ttu-id="32df1-217">[Creación de una aplicación web Hello World para Azure en IntelliJ]</span><span class="sxs-lookup"><span data-stu-id="32df1-217">[Create a Hello World web app for Azure in IntelliJ]</span></span>

<span data-ttu-id="32df1-218">Para obtener más información sobre el uso de Azure con Java, vea el [Centro para desarrolladores de Java de Azure] y la página de [herramientas de Java para Visual Studio Team Services].</span><span class="sxs-lookup"><span data-stu-id="32df1-218">For more information about using Azure with Java, see [Azure Java Developer Center] and [Java Tools for Visual Studio Team Services].</span></span>

<span data-ttu-id="32df1-219">Para más recursos de Docker, consulte el [sitio web de Docker] oficial.</span><span class="sxs-lookup"><span data-stu-id="32df1-219">For additional resources for Docker, see the official [Docker website].</span></span>

<!-- URL List -->

<span data-ttu-id="32df1-220">[Kit de herramientas de Azure para Eclipse]: ./azure-toolkit-for-eclipse.md</span><span class="sxs-lookup"><span data-stu-id="32df1-220">[Azure Toolkit for Eclipse]: ./azure-toolkit-for-eclipse.md</span></span>
<span data-ttu-id="32df1-221">[Kit de herramientas de Azure para IntelliJ]: ./azure-toolkit-for-intellij.md</span><span class="sxs-lookup"><span data-stu-id="32df1-221">[Azure Toolkit for IntelliJ]: ./azure-toolkit-for-intellij.md</span></span>
<span data-ttu-id="32df1-222">[Creación de una aplicación web Hello World para Azure en Eclipse]: ./app-service-web/app-service-web-eclipse-create-hello-world-web-app.md</span><span class="sxs-lookup"><span data-stu-id="32df1-222">[Create a Hello World web app for Azure in Eclipse]: ./app-service-web/app-service-web-eclipse-create-hello-world-web-app.md</span></span>
<span data-ttu-id="32df1-223">[Creación de una aplicación web Hello World para Azure en IntelliJ]: ./app-service-web/app-service-web-intellij-create-hello-world-web-app.md</span><span class="sxs-lookup"><span data-stu-id="32df1-223">[Create a Hello World web app for Azure in IntelliJ]: ./app-service-web/app-service-web-intellij-create-hello-world-web-app.md</span></span>
<span data-ttu-id="32df1-224">[Instalación del Kit de herramientas de Azure para Eclipse]: ./azure-toolkit-for-eclipse-installation.md</span><span class="sxs-lookup"><span data-stu-id="32df1-224">[Installing the Azure Toolkit for Eclipse]: ./azure-toolkit-for-eclipse-installation.md</span></span>
<span data-ttu-id="32df1-225">[Instalación del kit de herramientas de Azure para IntelliJ]: ./azure-toolkit-for-intellij-installation.md</span><span class="sxs-lookup"><span data-stu-id="32df1-225">[Installing the Azure Toolkit for IntelliJ]: ./azure-toolkit-for-intellij-installation.md</span></span>
<span data-ttu-id="32df1-226">[Instrucciones de inicio de sesión del kit de herramientas de Azure para Eclipse]: ./azure-toolkit-for-eclipse-sign-in-instructions.md</span><span class="sxs-lookup"><span data-stu-id="32df1-226">[Sign-in instructions for the Azure Toolkit for Eclipse]: ./azure-toolkit-for-eclipse-sign-in-instructions.md</span></span>
<span data-ttu-id="32df1-227">[Instrucciones de inicio de sesión del kit de herramientas de Azure para IntelliJ]: ./azure-toolkit-for-intellij-sign-in-instructions.md</span><span class="sxs-lookup"><span data-stu-id="32df1-227">[Sign-in instructions for the Azure Toolkit for IntelliJ]: ./azure-toolkit-for-intellij-sign-in-instructions.md</span></span>
<span data-ttu-id="32df1-228">[Novedades del kit de herramientas de Azure para Eclipse]: ./azure-toolkit-for-eclipse-whats-new.md</span><span class="sxs-lookup"><span data-stu-id="32df1-228">[What's new in the Azure Toolkit for Eclipse]: ./azure-toolkit-for-eclipse-whats-new.md</span></span>
<span data-ttu-id="32df1-229">[Novedades del kit de herramientas de Azure para IntelliJ]: ./azure-toolkit-for-intellij-whats-new.md</span><span class="sxs-lookup"><span data-stu-id="32df1-229">[What's new in the Azure Toolkit for IntelliJ]: ./azure-toolkit-for-intellij-whats-new.md</span></span>

<span data-ttu-id="32df1-230">[Centro para desarrolladores de Java de Azure]: https://azure.microsoft.com/develop/java/</span><span class="sxs-lookup"><span data-stu-id="32df1-230">[Azure Java Developer Center]: https://azure.microsoft.com/develop/java/</span></span>
<span data-ttu-id="32df1-231">[herramientas de Java para Visual Studio Team Services]: https://java.visualstudio.com/</span><span class="sxs-lookup"><span data-stu-id="32df1-231">[Java Tools for Visual Studio Team Services]: https://java.visualstudio.com/</span></span>

<span data-ttu-id="32df1-232">[sitio web de Docker]: https://www.docker.com/</span><span class="sxs-lookup"><span data-stu-id="32df1-232">[Docker website]: https://www.docker.com/</span></span>

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