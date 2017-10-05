---
title: Compatibilidad con SSH para Web App on Linux de Azure App Service | Microsoft Docs
description: Aprenda a usar SSH con Web App on Linux de Azure.
keywords: "azure app service, aplicación web, linux, oss"
services: app-service
documentationcenter: 
author: wesmc7777
manager: erikre
editor: 
ms.assetid: 66f9988f-8ffa-414a-9137-3a9b15a5573c
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/25/2017
ms.author: wesmc
ms.openlocfilehash: feee7a5c91d213a6b0bfdaf264a4da4d9e79cbe7
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/29/2017
---
# <a name="ssh-support-for-azure-web-app-on-linux"></a><span data-ttu-id="7869b-104">Compatibilidad con SSH para Web App on Linux de Azure</span><span class="sxs-lookup"><span data-stu-id="7869b-104">SSH support for Azure Web App on Linux</span></span>

[!INCLUDE [app-service-linux-preview](../../includes/app-service-linux-preview.md)]

## <a name="overview"></a><span data-ttu-id="7869b-105">Información general</span><span class="sxs-lookup"><span data-stu-id="7869b-105">Overview</span></span>

<span data-ttu-id="7869b-106">[Secure Shell (SSH)](https://en.wikipedia.org/wiki/Secure_Shell) es un protocolo de red criptográfico que permite usar servicios de red de forma segura.</span><span class="sxs-lookup"><span data-stu-id="7869b-106">[Secure Shell (SSH)](https://en.wikipedia.org/wiki/Secure_Shell) is a cryptographic network protocol for using network services securely.</span></span> <span data-ttu-id="7869b-107">Normalmente, se usa para iniciar sesión en un sistema de forma remota y segura desde una línea de comandos, además de para ejecutar comandos administrativos de forma remota.</span><span class="sxs-lookup"><span data-stu-id="7869b-107">It is most commonly used to log into a system remotely securely from a command-line and execute administrative commands remotely.</span></span>

<span data-ttu-id="7869b-108">Web App on Linux proporciona compatibilidad con SSH en el contenedor de la aplicación para todas las imágenes de Docker integradas que se usan para la pila en tiempo de ejecución de nuevas aplicaciones web.</span><span class="sxs-lookup"><span data-stu-id="7869b-108">Web App on Linux provides SSH support into the app container with each of the built-in Docker images used for the Runtime Stack of new web apps.</span></span> 

![Pilas en tiempo de ejecución](./media/app-service-linux-ssh-support/app-service-linux-runtime-stack.png)

<span data-ttu-id="7869b-110">También puede usar SSH con sus imágenes de Docker personalizadas. Para ello, incluya el servidor SSH como parte de la imagen y configúrelo como se indica en este tema.</span><span class="sxs-lookup"><span data-stu-id="7869b-110">You can also use SSH with your custom Docker images by including the SSH server as part of the image and configuring it as described in this topic.</span></span>



## <a name="making-a-client-connection"></a><span data-ttu-id="7869b-111">Establecimiento de una conexión de cliente</span><span class="sxs-lookup"><span data-stu-id="7869b-111">Making a client connection</span></span>

<span data-ttu-id="7869b-112">Para establecer una conexión de cliente SSH, se debe iniciar el sitio principal.</span><span class="sxs-lookup"><span data-stu-id="7869b-112">To make an SSH client connection, the main site must be started.</span></span> 

<span data-ttu-id="7869b-113">Pegue el punto de conexión de Administración del control de código fuente (SCM) de la aplicación web en el explorador con el siguiente formulario:</span><span class="sxs-lookup"><span data-stu-id="7869b-113">Paste the Source Control Management (SCM) endpoint for your web app into your browser using the following form:</span></span>

        https://<your sitename>.scm.azurewebsites.net/webssh/host

<span data-ttu-id="7869b-114">Si no lo está ya, será necesario que se autentique con su suscripción a Azure para poder conectarse.</span><span class="sxs-lookup"><span data-stu-id="7869b-114">If you are not already authenticated, you are required to authenticate with your Azure subscription to connect.</span></span>

![Conexión SSH](./media/app-service-linux-ssh-support/app-service-linux-ssh-connection.png)


## <a name="ssh-support-with-custom-docker-images"></a><span data-ttu-id="7869b-116">Compatibilidad con SSH para imágenes personalizadas de Docker</span><span class="sxs-lookup"><span data-stu-id="7869b-116">SSH support with custom Docker images</span></span>

<span data-ttu-id="7869b-117">Para que una imagen personalizada de Docker admita la comunicación mediante SSH entre el contenedor y el cliente de Azure Portal, realice los siguientes pasos para su imagen de Docker.</span><span class="sxs-lookup"><span data-stu-id="7869b-117">In order for a custom Docker image to support SSH communication between the container and the client in the Azure portal, perform the following steps for your Docker image.</span></span> 

<span data-ttu-id="7869b-118">Estos pasos se indican en el repositorio de Azure App Service, como en [este](https://github.com/Azure-App-Service/node/blob/master/6.9.3/) ejemplo.</span><span class="sxs-lookup"><span data-stu-id="7869b-118">These steps are are shown in the Azure App Service repository as an example [here](https://github.com/Azure-App-Service/node/blob/master/6.9.3/).</span></span>

1. <span data-ttu-id="7869b-119">Incluya la instalación `openssh-server` en la instrucción [`RUN`](https://docs.docker.com/engine/reference/builder/#run) del Dockerfile de la imagen y establezca la contraseña de la cuenta raíz a `"Docker!"`.</span><span class="sxs-lookup"><span data-stu-id="7869b-119">Include the `openssh-server` installation in [`RUN` instruction](https://docs.docker.com/engine/reference/builder/#run) in the Dockerfile for your image and set the password for the root account to `"Docker!"`.</span></span> 

    > [!NOTE] 
    > <span data-ttu-id="7869b-120">Esta configuración no permite realizar conexiones externas al contenedor.</span><span class="sxs-lookup"><span data-stu-id="7869b-120">This configuration does not allow external connections to the container.</span></span> <span data-ttu-id="7869b-121">Solo es posible acceder a SSH a través del sitio de Kudu o SCM, que se autentica con las credenciales de publicación.</span><span class="sxs-lookup"><span data-stu-id="7869b-121">SSH can only be accessed via the Kudu / SCM Site, which is authenticated using the publishing credentials.</span></span>

    ```docker
    # ------------------------
    # SSH Server support
    # ------------------------
    RUN apt-get update \ 
      && apt-get install -y --no-install-recommends openssh-server \
      && echo "root:Docker!" | chpasswd
    ``` 

2. <span data-ttu-id="7869b-122">Agregue una instrucción [`COPY`](https://docs.docker.com/engine/reference/builder/#copy) al Dockerfile para copiar un archivo [sshd_config](http://man.openbsd.org/sshd_config) en el directorio */etc/ssh/*.</span><span class="sxs-lookup"><span data-stu-id="7869b-122">Add a [`COPY` instruction](https://docs.docker.com/engine/reference/builder/#copy) to the Dockerfile to copy a [sshd_config](http://man.openbsd.org/sshd_config) file to the */etc/ssh/* directory.</span></span> <span data-ttu-id="7869b-123">Su archivo de configuración debería basarse en nuestro archivo sshd_config del repositorio de GitHub de Azure App Service, localizable [aquí](https://github.com/Azure-App-Service/node/blob/master/6.11/sshd_config).</span><span class="sxs-lookup"><span data-stu-id="7869b-123">Your configuration file should be based on our sshd_config file in the Azure-App-Service GitHub repository [here](https://github.com/Azure-App-Service/node/blob/master/6.11/sshd_config).</span></span>

    > [!NOTE] 
    > <span data-ttu-id="7869b-124">El archivo *sshd_config* debe incluir los siguientes elementos o se producirá un error de conexión:</span><span class="sxs-lookup"><span data-stu-id="7869b-124">The *sshd_config* file must include the following or the connection fails:</span></span> 
    > * <span data-ttu-id="7869b-125">`Ciphers` debe incluir al menos uno de los siguientes elementos: `aes128-cbc,3des-cbc,aes256-cbc`.</span><span class="sxs-lookup"><span data-stu-id="7869b-125">`Ciphers` must include at least one of the following: `aes128-cbc,3des-cbc,aes256-cbc`.</span></span>
    > * <span data-ttu-id="7869b-126">`MACs` debe incluir al menos uno de los siguientes elementos: `hmac-sha1,hmac-sha1-96`.</span><span class="sxs-lookup"><span data-stu-id="7869b-126">`MACs` must include at least one of the following: `hmac-sha1,hmac-sha1-96`.</span></span>

    ```docker
    COPY sshd_config /etc/ssh/
    ```


3. <span data-ttu-id="7869b-127">Incluya el puerto 2222 en la instrucción [`EXPOSE`](https://docs.docker.com/engine/reference/builder/#expose) del Dockerfile.</span><span class="sxs-lookup"><span data-stu-id="7869b-127">Include port 2222 in the [`EXPOSE` instruction](https://docs.docker.com/engine/reference/builder/#expose) for the Dockerfile.</span></span> <span data-ttu-id="7869b-128">Aunque se conozca la contraseña raíz, no es posible acceder al puerto 2222 desde Internet.</span><span class="sxs-lookup"><span data-stu-id="7869b-128">Although the root password is known, port 2222 cannot be accessed from the internet.</span></span> <span data-ttu-id="7869b-129">Se trata de un puerto interno exclusivo al que solo pueden acceder los contenedores que se encuentren en el puente de una red privada virtual.</span><span class="sxs-lookup"><span data-stu-id="7869b-129">It is an internal only port accessible only by containers within the bridge network of a private virtual network.</span></span>

    ```docker
    EXPOSE 2222 80
    ```

4. <span data-ttu-id="7869b-130">Asegúrese de iniciar el servicio SSH.</span><span class="sxs-lookup"><span data-stu-id="7869b-130">Make sure to start the ssh service.</span></span> <span data-ttu-id="7869b-131">En [este](https://github.com/Azure-App-Service/node/blob/master/6.9.3/startup/init_container.sh) ejemplo, se usa un script de shell en el directorio */bin*.</span><span class="sxs-lookup"><span data-stu-id="7869b-131">The example [here](https://github.com/Azure-App-Service/node/blob/master/6.9.3/startup/init_container.sh) uses a shell script in */bin* directory.</span></span>

    ```bash
    #!/bin/bash
    service ssh start
    ```

    <span data-ttu-id="7869b-132">El Dockerfile usa la instrucción [`CMD`](https://docs.docker.com/engine/reference/builder/#cmd) para ejecutar el script.</span><span class="sxs-lookup"><span data-stu-id="7869b-132">The Dockerfile uses the [`CMD` instruction](https://docs.docker.com/engine/reference/builder/#cmd) to run the script.</span></span>

    ```docker
    COPY init_container.sh /bin/
      ...
    RUN chmod 755 /bin/init_container.sh 
      ...       
    CMD ["/bin/init_container.sh"]
    ```



## <a name="next-steps"></a><span data-ttu-id="7869b-133">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="7869b-133">Next steps</span></span>
<span data-ttu-id="7869b-134">Visite los siguientes vínculos para obtener más información acerca de Web App on Linux.</span><span class="sxs-lookup"><span data-stu-id="7869b-134">See the following links for more information regarding Web App on Linux.</span></span> <span data-ttu-id="7869b-135">Puede publicar preguntas y problemas en [nuestro foro](https://social.msdn.microsoft.com/forums/azure/home?forum=windowsazurewebsitespreview).</span><span class="sxs-lookup"><span data-stu-id="7869b-135">You can post questions and concerns on [our forum](https://social.msdn.microsoft.com/forums/azure/home?forum=windowsazurewebsitespreview).</span></span>

* [<span data-ttu-id="7869b-136">Uso de una imagen personalizada de Docker para Web App on Linux de Azure</span><span class="sxs-lookup"><span data-stu-id="7869b-136">How to use a custom Docker image for Azure Web App on Linux</span></span>](app-service-linux-using-custom-docker-image.md)
* [<span data-ttu-id="7869b-137">Uso de la configuración de PM2 para Node.js en Web App on Linux de Azure</span><span class="sxs-lookup"><span data-stu-id="7869b-137">Using PM2 Configuration for Node.js in Azure Web App on Linux</span></span>](app-service-linux-using-nodejs-pm2.md)
* [<span data-ttu-id="7869b-138">Uso de .NET Core en Web App on Linux de Azure</span><span class="sxs-lookup"><span data-stu-id="7869b-138">Using .NET Core in Azure Web App on Linux</span></span>](app-service-linux-using-dotnetcore.md)
* [<span data-ttu-id="7869b-139">Uso de Ruby en Web App on Linux de Azure</span><span class="sxs-lookup"><span data-stu-id="7869b-139">Using Ruby in Azure Web App on Linux</span></span>](app-service-linux-ruby-get-started.md)
* [<span data-ttu-id="7869b-140">Preguntas más frecuentes sobre Web App on Linux de Azure App Service</span><span class="sxs-lookup"><span data-stu-id="7869b-140">Azure App Service Web App on Linux FAQ</span></span>](app-service-linux-faq.md)

