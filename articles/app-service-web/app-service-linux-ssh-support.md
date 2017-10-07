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
# <a name="ssh-support-for-azure-web-app-on-linux"></a>Compatibilidad con SSH para Web App on Linux de Azure

[!INCLUDE [app-service-linux-preview](../../includes/app-service-linux-preview.md)]

## <a name="overview"></a>Información general

[Secure Shell (SSH)](https://en.wikipedia.org/wiki/Secure_Shell) es un protocolo de red criptográfico que permite usar servicios de red de forma segura. Es toolog utilizada con más frecuencia en un sistema de forma remota segura desde una línea de comandos y ejecutar comandos administrativos de forma remota.

Aplicación en Linux Web proporciona compatibilidad SSH en el contenedor de la aplicación Hola a cada una de las imágenes Docker integradas Hola que se utilizan para hello pila de tiempo de ejecución de nuevas aplicaciones web. 

![Pilas en tiempo de ejecución](./media/app-service-linux-ssh-support/app-service-linux-runtime-stack.png)

También puede utilizar SSH con las imágenes del Docker personalizadas mediante la inclusión de servidor SSH de hello como parte de la imagen de Hola y configurarlo como se describe en este tema.



## <a name="making-a-client-connection"></a>Establecimiento de una conexión de cliente

se debe iniciar una conexión de cliente SSH, sitio principal de hello toomake. 

Pegue el extremo de administración de Control de código fuente (SCM) de hello para la aplicación web en el explorador con hello siguiendo el formato:

        https://<your sitename>.scm.azurewebsites.net/webssh/host

Si no está autenticado ya, son necesario tooauthenticate con su tooconnect de suscripción de Azure.

![Conexión SSH](./media/app-service-linux-ssh-support/app-service-linux-ssh-connection.png)


## <a name="ssh-support-with-custom-docker-images"></a>Compatibilidad con SSH para imágenes personalizadas de Docker

Para lograr una personalizada Docker imagen toosupport SSH comunicación entre el contenedor de Hola y el cliente de Hola Hola portal de Azure, realizar Hola siguiendo los pasos para la imagen de Docker. 

Estos pasos son se muestran en hello repositorio de servicio de aplicaciones de Azure como ejemplo [aquí](https://github.com/Azure-App-Service/node/blob/master/6.9.3/).

1. Incluir hello `openssh-server` instalación en [ `RUN` instrucción](https://docs.docker.com/engine/reference/builder/#run) en hello Dockerfile para la imagen y establecer contraseña de hello para la cuenta raíz de hello demasiado`"Docker!"`. 

    > [!NOTE] 
    > Esta configuración no permita contenedor toohello de conexiones externas. SSH solo son accesibles a través de hello Kudu / Hola de sitio de SCM, lo que se autentica utilizando las credenciales de publicación.

    ```docker
    # ------------------------
    # SSH Server support
    # ------------------------
    RUN apt-get update \ 
      && apt-get install -y --no-install-recommends openssh-server \
      && echo "root:Docker!" | chpasswd
    ``` 

2. Agregar un [ `COPY` instrucción](https://docs.docker.com/engine/reference/builder/#copy) toohello Dockerfile toocopy una [sshd_config](http://man.openbsd.org/sshd_config) archivo toohello */etcetera/ssh/* directory. El archivo de configuración debe basarse en nuestro archivo sshd_config en el repositorio de GitHub de servicio de aplicaciones de Azure de hello [aquí](https://github.com/Azure-App-Service/node/blob/master/6.11/sshd_config).

    > [!NOTE] 
    > Hola *sshd_config* archivo debe incluir la siguiente de Hola o se produce un error en la conexión de hello: 
    > * `Ciphers`debe incluir al menos uno de los siguientes hello: `aes128-cbc,3des-cbc,aes256-cbc`.
    > * `MACs`debe incluir al menos uno de los siguientes hello: `hmac-sha1,hmac-sha1-96`.

    ```docker
    COPY sshd_config /etc/ssh/
    ```


3. Incluye el puerto 2222 Hola [ `EXPOSE` instrucción](https://docs.docker.com/engine/reference/builder/#expose) para hello Dockerfile. Aunque se conoce la contraseña de la raíz de hello, puerto 2222 no son accesibles desde Hola internet. Es un puerto único interno accesible solo por contenedores dentro de la red con puente Hola de una red privada virtual.

    ```docker
    EXPOSE 2222 80
    ```

4. Asegúrese de que toostart Hola de ssh servicio. ejemplo de Hola [aquí](https://github.com/Azure-App-Service/node/blob/master/6.9.3/startup/init_container.sh) usa un script de shell en */bin* directory.

    ```bash
    #!/bin/bash
    service ssh start
    ```

    Hola Dockerfile usa hello [ `CMD` instrucción](https://docs.docker.com/engine/reference/builder/#cmd) secuencia de comandos de toorun Hola.

    ```docker
    COPY init_container.sh /bin/
      ...
    RUN chmod 755 /bin/init_container.sh 
      ...       
    CMD ["/bin/init_container.sh"]
    ```



## <a name="next-steps"></a>Pasos siguientes
Vea Hola siguientes vínculos para obtener más información sobre la aplicación Web en Linux. Puede publicar preguntas y problemas en [nuestro foro](https://social.msdn.microsoft.com/forums/azure/home?forum=windowsazurewebsitespreview).

* [Cómo la imagen toouse una Docker personalizada para la aplicación Web de Azure en Linux](app-service-linux-using-custom-docker-image.md)
* [Uso de la configuración de PM2 para Node.js en Web App on Linux de Azure](app-service-linux-using-nodejs-pm2.md)
* [Uso de .NET Core en Web App on Linux de Azure](app-service-linux-using-dotnetcore.md)
* [Uso de Ruby en Web App on Linux de Azure](app-service-linux-ruby-get-started.md)
* [Preguntas más frecuentes sobre Web App on Linux de Azure App Service](app-service-linux-faq.md)

