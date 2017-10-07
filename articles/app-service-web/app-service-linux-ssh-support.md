---
title: "compatibilidad con aaaSSH para la aplicación de Web de servicio de aplicación de Azure en Linux | Documentos de Microsoft"
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
ms.openlocfilehash: e00be6d4631e8936a2a8bc106da1fc06237a4b39
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="ssh-support-for-azure-web-app-on-linux"></a><span data-ttu-id="a9730-104">Compatibilidad con SSH para Web App on Linux de Azure</span><span class="sxs-lookup"><span data-stu-id="a9730-104">SSH support for Azure Web App on Linux</span></span>

[!INCLUDE [app-service-linux-preview](../../includes/app-service-linux-preview.md)]

## <a name="overview"></a><span data-ttu-id="a9730-105">Información general</span><span class="sxs-lookup"><span data-stu-id="a9730-105">Overview</span></span>

<span data-ttu-id="a9730-106">[Secure Shell (SSH)](https://en.wikipedia.org/wiki/Secure_Shell) es un protocolo de red criptográfico que permite usar servicios de red de forma segura.</span><span class="sxs-lookup"><span data-stu-id="a9730-106">[Secure Shell (SSH)](https://en.wikipedia.org/wiki/Secure_Shell) is a cryptographic network protocol for using network services securely.</span></span> <span data-ttu-id="a9730-107">Es toolog utilizada con más frecuencia en un sistema de forma remota segura desde una línea de comandos y ejecutar comandos administrativos de forma remota.</span><span class="sxs-lookup"><span data-stu-id="a9730-107">It is most commonly used toolog into a system remotely securely from a command-line and execute administrative commands remotely.</span></span>

<span data-ttu-id="a9730-108">Aplicación en Linux Web proporciona compatibilidad SSH en el contenedor de la aplicación Hola a cada una de las imágenes Docker integradas Hola que se utilizan para hello pila de tiempo de ejecución de nuevas aplicaciones web.</span><span class="sxs-lookup"><span data-stu-id="a9730-108">Web App on Linux provides SSH support into hello app container with each of hello built-in Docker images used for hello Runtime Stack of new web apps.</span></span> 

![Pilas en tiempo de ejecución](./media/app-service-linux-ssh-support/app-service-linux-runtime-stack.png)

<span data-ttu-id="a9730-110">También puede utilizar SSH con las imágenes del Docker personalizadas mediante la inclusión de servidor SSH de hello como parte de la imagen de Hola y configurarlo como se describe en este tema.</span><span class="sxs-lookup"><span data-stu-id="a9730-110">You can also use SSH with your custom Docker images by including hello SSH server as part of hello image and configuring it as described in this topic.</span></span>



## <a name="making-a-client-connection"></a><span data-ttu-id="a9730-111">Establecimiento de una conexión de cliente</span><span class="sxs-lookup"><span data-stu-id="a9730-111">Making a client connection</span></span>

<span data-ttu-id="a9730-112">se debe iniciar una conexión de cliente SSH, sitio principal de hello toomake.</span><span class="sxs-lookup"><span data-stu-id="a9730-112">toomake an SSH client connection, hello main site must be started.</span></span> 

<span data-ttu-id="a9730-113">Pegue el extremo de administración de Control de código fuente (SCM) de hello para la aplicación web en el explorador con hello siguiendo el formato:</span><span class="sxs-lookup"><span data-stu-id="a9730-113">Paste hello Source Control Management (SCM) endpoint for your web app into your browser using hello following form:</span></span>

        https://<your sitename>.scm.azurewebsites.net/webssh/host

<span data-ttu-id="a9730-114">Si no está autenticado ya, son necesario tooauthenticate con su tooconnect de suscripción de Azure.</span><span class="sxs-lookup"><span data-stu-id="a9730-114">If you are not already authenticated, you are required tooauthenticate with your Azure subscription tooconnect.</span></span>

![Conexión SSH](./media/app-service-linux-ssh-support/app-service-linux-ssh-connection.png)


## <a name="ssh-support-with-custom-docker-images"></a><span data-ttu-id="a9730-116">Compatibilidad con SSH para imágenes personalizadas de Docker</span><span class="sxs-lookup"><span data-stu-id="a9730-116">SSH support with custom Docker images</span></span>

<span data-ttu-id="a9730-117">Para lograr una personalizada Docker imagen toosupport SSH comunicación entre el contenedor de Hola y el cliente de Hola Hola portal de Azure, realizar Hola siguiendo los pasos para la imagen de Docker.</span><span class="sxs-lookup"><span data-stu-id="a9730-117">In order for a custom Docker image toosupport SSH communication between hello container and hello client in hello Azure portal, perform hello following steps for your Docker image.</span></span> 

<span data-ttu-id="a9730-118">Estos pasos son se muestran en hello repositorio de servicio de aplicaciones de Azure como ejemplo [aquí](https://github.com/Azure-App-Service/node/blob/master/6.9.3/).</span><span class="sxs-lookup"><span data-stu-id="a9730-118">These steps are are shown in hello Azure App Service repository as an example [here](https://github.com/Azure-App-Service/node/blob/master/6.9.3/).</span></span>

1. <span data-ttu-id="a9730-119">Incluir hello `openssh-server` instalación en [ `RUN` instrucción](https://docs.docker.com/engine/reference/builder/#run) en hello Dockerfile para la imagen y establecer contraseña de hello para la cuenta raíz de hello demasiado`"Docker!"`.</span><span class="sxs-lookup"><span data-stu-id="a9730-119">Include hello `openssh-server` installation in [`RUN` instruction](https://docs.docker.com/engine/reference/builder/#run) in hello Dockerfile for your image and set hello password for hello root account too`"Docker!"`.</span></span> 

    > [!NOTE] 
    > <span data-ttu-id="a9730-120">Esta configuración no permita contenedor toohello de conexiones externas.</span><span class="sxs-lookup"><span data-stu-id="a9730-120">This configuration does not allow external connections toohello container.</span></span> <span data-ttu-id="a9730-121">SSH solo son accesibles a través de hello Kudu / Hola de sitio de SCM, lo que se autentica utilizando las credenciales de publicación.</span><span class="sxs-lookup"><span data-stu-id="a9730-121">SSH can only be accessed via hello Kudu / SCM Site, which is authenticated using hello publishing credentials.</span></span>

    ```docker
    # ------------------------
    # SSH Server support
    # ------------------------
    RUN apt-get update \ 
      && apt-get install -y --no-install-recommends openssh-server \
      && echo "root:Docker!" | chpasswd
    ``` 

2. <span data-ttu-id="a9730-122">Agregar un [ `COPY` instrucción](https://docs.docker.com/engine/reference/builder/#copy) toohello Dockerfile toocopy una [sshd_config](http://man.openbsd.org/sshd_config) archivo toohello */etcetera/ssh/* directory.</span><span class="sxs-lookup"><span data-stu-id="a9730-122">Add a [`COPY` instruction](https://docs.docker.com/engine/reference/builder/#copy) toohello Dockerfile toocopy a [sshd_config](http://man.openbsd.org/sshd_config) file toohello */etc/ssh/* directory.</span></span> <span data-ttu-id="a9730-123">El archivo de configuración debe basarse en nuestro archivo sshd_config en el repositorio de GitHub de servicio de aplicaciones de Azure de hello [aquí](https://github.com/Azure-App-Service/node/blob/master/6.11/sshd_config).</span><span class="sxs-lookup"><span data-stu-id="a9730-123">Your configuration file should be based on our sshd_config file in hello Azure-App-Service GitHub repository [here](https://github.com/Azure-App-Service/node/blob/master/6.11/sshd_config).</span></span>

    > [!NOTE] 
    > <span data-ttu-id="a9730-124">Hola *sshd_config* archivo debe incluir la siguiente de Hola o se produce un error en la conexión de hello:</span><span class="sxs-lookup"><span data-stu-id="a9730-124">hello *sshd_config* file must include hello following or hello connection fails:</span></span> 
    > * <span data-ttu-id="a9730-125">`Ciphers`debe incluir al menos uno de los siguientes hello: `aes128-cbc,3des-cbc,aes256-cbc`.</span><span class="sxs-lookup"><span data-stu-id="a9730-125">`Ciphers` must include at least one of hello following: `aes128-cbc,3des-cbc,aes256-cbc`.</span></span>
    > * <span data-ttu-id="a9730-126">`MACs`debe incluir al menos uno de los siguientes hello: `hmac-sha1,hmac-sha1-96`.</span><span class="sxs-lookup"><span data-stu-id="a9730-126">`MACs` must include at least one of hello following: `hmac-sha1,hmac-sha1-96`.</span></span>

    ```docker
    COPY sshd_config /etc/ssh/
    ```


3. <span data-ttu-id="a9730-127">Incluye el puerto 2222 Hola [ `EXPOSE` instrucción](https://docs.docker.com/engine/reference/builder/#expose) para hello Dockerfile.</span><span class="sxs-lookup"><span data-stu-id="a9730-127">Include port 2222 in hello [`EXPOSE` instruction](https://docs.docker.com/engine/reference/builder/#expose) for hello Dockerfile.</span></span> <span data-ttu-id="a9730-128">Aunque se conoce la contraseña de la raíz de hello, puerto 2222 no son accesibles desde Hola internet.</span><span class="sxs-lookup"><span data-stu-id="a9730-128">Although hello root password is known, port 2222 cannot be accessed from hello internet.</span></span> <span data-ttu-id="a9730-129">Es un puerto único interno accesible solo por contenedores dentro de la red con puente Hola de una red privada virtual.</span><span class="sxs-lookup"><span data-stu-id="a9730-129">It is an internal only port accessible only by containers within hello bridge network of a private virtual network.</span></span>

    ```docker
    EXPOSE 2222 80
    ```

4. <span data-ttu-id="a9730-130">Asegúrese de que toostart Hola de ssh servicio.</span><span class="sxs-lookup"><span data-stu-id="a9730-130">Make sure toostart hello ssh service.</span></span> <span data-ttu-id="a9730-131">ejemplo de Hola [aquí](https://github.com/Azure-App-Service/node/blob/master/6.9.3/startup/init_container.sh) usa un script de shell en */bin* directory.</span><span class="sxs-lookup"><span data-stu-id="a9730-131">hello example [here](https://github.com/Azure-App-Service/node/blob/master/6.9.3/startup/init_container.sh) uses a shell script in */bin* directory.</span></span>

    ```bash
    #!/bin/bash
    service ssh start
    ```

    <span data-ttu-id="a9730-132">Hola Dockerfile usa hello [ `CMD` instrucción](https://docs.docker.com/engine/reference/builder/#cmd) secuencia de comandos de toorun Hola.</span><span class="sxs-lookup"><span data-stu-id="a9730-132">hello Dockerfile uses hello [`CMD` instruction](https://docs.docker.com/engine/reference/builder/#cmd) toorun hello script.</span></span>

    ```docker
    COPY init_container.sh /bin/
      ...
    RUN chmod 755 /bin/init_container.sh 
      ...       
    CMD ["/bin/init_container.sh"]
    ```



## <a name="next-steps"></a><span data-ttu-id="a9730-133">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="a9730-133">Next steps</span></span>
<span data-ttu-id="a9730-134">Vea Hola siguientes vínculos para obtener más información sobre la aplicación Web en Linux.</span><span class="sxs-lookup"><span data-stu-id="a9730-134">See hello following links for more information regarding Web App on Linux.</span></span> <span data-ttu-id="a9730-135">Puede publicar preguntas y problemas en [nuestro foro](https://social.msdn.microsoft.com/forums/azure/home?forum=windowsazurewebsitespreview).</span><span class="sxs-lookup"><span data-stu-id="a9730-135">You can post questions and concerns on [our forum](https://social.msdn.microsoft.com/forums/azure/home?forum=windowsazurewebsitespreview).</span></span>

* [<span data-ttu-id="a9730-136">Cómo la imagen toouse una Docker personalizada para la aplicación Web de Azure en Linux</span><span class="sxs-lookup"><span data-stu-id="a9730-136">How toouse a custom Docker image for Azure Web App on Linux</span></span>](app-service-linux-using-custom-docker-image.md)
* [<span data-ttu-id="a9730-137">Uso de la configuración de PM2 para Node.js en Web App on Linux de Azure</span><span class="sxs-lookup"><span data-stu-id="a9730-137">Using PM2 Configuration for Node.js in Azure Web App on Linux</span></span>](app-service-linux-using-nodejs-pm2.md)
* [<span data-ttu-id="a9730-138">Uso de .NET Core en Web App on Linux de Azure</span><span class="sxs-lookup"><span data-stu-id="a9730-138">Using .NET Core in Azure Web App on Linux</span></span>](app-service-linux-using-dotnetcore.md)
* [<span data-ttu-id="a9730-139">Uso de Ruby en Web App on Linux de Azure</span><span class="sxs-lookup"><span data-stu-id="a9730-139">Using Ruby in Azure Web App on Linux</span></span>](app-service-linux-ruby-get-started.md)
* [<span data-ttu-id="a9730-140">Preguntas más frecuentes sobre Web App on Linux de Azure App Service</span><span class="sxs-lookup"><span data-stu-id="a9730-140">Azure App Service Web App on Linux FAQ</span></span>](app-service-linux-faq.md)

