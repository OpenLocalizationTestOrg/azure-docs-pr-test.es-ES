---
title: "aaaDeploy una tooLinux de aplicación Node.js máquinas virtuales en Azure"
description: "Obtenga información acerca de cómo toodeploy un Node.js máquinas de virtuales tooLinux de aplicación en Azure."
services: 
documentationcenter: nodejs
author: stepro
manager: dmitryr
editor: 
ROBOTS: NOINDEX, NOFOLLOW
redirect_url: /azure
ms.assetid: 857a812d-c73e-4af7-a985-2d0baf8b6f71
ms.service: multiple
ms.devlang: nodejs
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 02/02/2016
ms.author: stephpr
ms.openlocfilehash: e876c8170a06f102f7f32ec7cb930b876647a707
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-a-nodejs-application-toolinux-virtual-machines-in-azure"></a>Implementar un tooLinux de aplicación Node.js máquinas virtuales en Azure
Este tutorial se muestra cómo una aplicación Node.js tootake e implementar máquinas virtuales de tooLinux ejecuta en Azure. instrucciones de Hello en este tutorial se pueden aplicar en cualquier sistema operativo que sea capaz de ejecutar Node.js.

Aprenderá a:

* Bifurcar y clonar un repositorio de GitHub con una aplicación simple de tarea pendiente
* Crear y configurar dos máquinas virtuales de Linux en la aplicación de Azure toorun hello;
* Recorrer en iteración en la aplicación hello insertando la máquina virtual de las actualizaciones toohello web front-end.

> [!NOTE]
> toocomplete este tutorial, se necesita una cuenta de GitHub y una cuenta de Microsoft Azure y Hola capacidad toouse Git desde un equipo de desarrollo.
> 
> Si no tiene cuenta de GitHub, puede suscribirse para obtener una gratis [aquí](https://github.com/join).
> 
> Si no tiene una cuenta de [Microsoft Azure](https://azure.microsoft.com/), puede registrarse para obtener una evaluación gratuita [aquí](https://azure.microsoft.com/pricing/free-trial/). Esto le llevará también a través del proceso de registro de hello un [Account Microsoft](http://account.microsoft.com) si ya no dispone de uno. Como alternativa, si tiene una suscripción de Visual Studio, puede [activar los beneficios de MSDN](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A261C142F).
> 
> Si no tiene Git en la máquina de desarrollo y está utilizando un equipo Macintosh o Windows, instale Git desde [aquí](http://www.git-scm.com). Si usas Linux, instale git mediante el mecanismo de hello más adecuada para usted, como `sudo apt-get install git`.
> 
> 

## <a name="forking-and-cloning-hello-todo-application"></a>Bifurcación y clonar Hola la aplicación de tareas
Hola aplicación de lista de tareas usada por este tutorial implementa un servidor front-end web simple sobre una instancia de MongoDB que realiza un seguimiento de una lista de tareas. Tras iniciar sesión en tooGitHub, vaya [aquí](https://github.com/stepro/node-todo) toofind Hola aplicación y bifurcar mediante el vínculo de hello en la parte superior de hello derecha. Esto debería crear un repositorio en la cuenta con el nombre *accountname*/node-todo.

Ahora en la máquina de desarrollo, clone este repositorio:

    git clone https://github.com/accountname/node-todo.git

Usaremos este clon local del repositorio de hello un poco más adelante al realizar cambios de código fuente de toohello.

## <a name="creating-and-configuring-hello-linux-virtual-machines"></a>Crear y configurar Hola máquinas virtuales de Linux
Azure ofrece un buen soporte para los procesos sin formato con las máquinas virtuales Linux. Esta parte de hello tutorial, se muestra cómo puede poner en marcha dos máquinas virtuales de Linux e implementar toothem de aplicación de lista de tareas de hello, ejecución Hola front-end web en uno y Hola instancia MongoDB en hello otro fácilmente.

### <a name="creating-virtual-machines"></a>Creación de máquinas virtuales
toocreate de manera más fácil de Hello una nueva máquina virtual en Azure es toouse Hola Portal de Azure. Haga clic en [aquí](https://portal.azure.com) toosign en e inicie Hola Portal de Azure en el explorador web. Una vez que haya cargado Hola Portal de Azure, complete Hola pasos:

* Haga clic en Hola "+ nuevo" vincular;
* Seleccione la categoría de "Proceso" hello y elija "Ubuntu Server 14.04 LTS";
* Seleccione el modelo de implementación de "Administrador de recursos" hello y haga clic en "Crear";
* Rellene los conceptos básicos de hello siga estas instrucciones:
  * Especifique un nombre que pueda identificar fácilmente más tarde.
  * Para este tutorial, elija la autenticación mediante contraseña.
  * Cree un nuevo grupo de recursos con un nombre identificable.
* Para el tamaño de la máquina Virtual de hello, "A1" estándar"es una opción razonable para este tutorial.
* Para ver otras opciones, asegúrese de que el tipo de disco de hello es "Estándar" y acepte que Hola a todos los valores predeterminados restantes.
* Iniciar creación de hello en la página de resumen de Hola.

Realizar Hola anterior procesar dos veces toocreate dos las máquinas virtuales Linux, uno para front-end web de hello y otro para la instancia de MongoDB Hola. Creación de máquinas virtuales de hello tardará unos 5-10 minutos.

### <a name="assigning-a-dns-entry-for-virtual-machines"></a>Asignación de una entrada DNS para las máquinas virtuales
De manera predeterminada, a las máquinas virtuales creadas en Azure se puede acceder solo a través de una dirección IP pública, como 1.2.3.4. Vamos a hacer máquinas Hola identificar más fácilmente mediante la asignación de las entradas de DNS.

Una vez que el portal de hello indica que se han creado las máquinas virtuales hello, haga clic en vínculo de Hola "Máquinas virtuales" en la barra de navegación izquierdo de Hola y busque las máquinas. Para cada máquina:

* Busque la pestaña de Essentials hello y haga clic en hello la dirección IP pública;
* En la configuración de dirección IP pública hello, asigne una etiqueta de nombre DNS y guardar.

portal de Hello garantizará ese nombre de Hola que especifique estará disponible. Después de guardar la configuración de hello, las máquinas virtuales tendrán nombres de host similares demasiado`machinename.region.cloudapp.azure.com`.

### <a name="connecting-toohello-virtual-machines"></a>Conexión toohello máquinas virtuales
Cuando se aprovisionan las máquinas virtuales, eran tooallow preconfigurada de conexiones remotas a través de SSH. Se trata de mecanismo de hello usaremos máquinas virtuales de tooconfigure Hola. Si está utilizando Windows para el desarrollo, deberá tooget un cliente de SSH si ya no dispone de uno. Una opción común es PuTTY, que puede descargar desde [aquí](http://www.chiark.greenend.org.uk/~sgtatham/putty/). Los sistemas operativos Macintosh y Linux vienen con una versión de SSH preinstalada.

### <a name="configuring-hello-web-frontend-virtual-machine"></a>Configuración de máquina Virtual del servidor front-end Web de Hola
Máquina de front-end web SSH toohello creado mediante PuTTY, ssh línea de comandos o la herramienta SSH prefiera. Debería ver un mensaje de bienvenida seguido de un símbolo del sistema.

En primer lugar, debe asegurarse de que Git y el nodo estén instalados:

    sudo apt-get install -y git
    curl -sL https://deb.nodesource.com/setup_4.x | sudo -E bash -
    sudo apt-get install -y nodejs

Puesto que el front-end web de la aplicación hello depende de algunos módulos de Node.js nativo, necesitamos conjunto esencial de hello tooinstall de herramientas de compilación:

    sudo apt-get install -y build-essential

Por último, vamos a instalar una aplicación Node.js denominada *indefinidamente*, que permite a las aplicaciones de servidor de Node.js toorun:

    sudo npm install -g forever

Estas son todas las dependencias de hello necesarios en el front-end de máquina virtual toobe toorun capaz de Hola de esta aplicación web, así que vamos a hacer que ejecutan. toodo, primero crearemos a un clon del repositorio de GitHub de Hola que bifurcado previamente para que pueda publicar fácilmente las actualizaciones toohello virtual machine (hablaremos sobre este escenario de actualización más adelante) y, a continuación, clonar Hola clon tooprovide una versión de Hola repositorio que realmente se pueden ejecutar.

A partir del directorio de inicio (~) hello, ejecutar Hola después de comandos (reemplazando *accountname* con su nombre de cuenta de usuario de GitHub):

    git clone --bare https://github.com/accountname/node-todo.git
    git clone node-todo.git

Ahora escriba Hola todo en el nodo directorio y ejecute estos comandos:

    npm install
    forever start server.js

Hello front-end de la aplicación web se está ejecutando ahora, sin embargo, es un paso más poder tener acceso aplicación hello desde un explorador web. Hello máquina virtual que creó protegida por un recurso de Azure llama un *grupo de seguridad de red*, que se creó para que al aprovisionar Hola máquina virtual. Actualmente, este recurso sólo permite las solicitudes externas tooport toobe 22 enrutan toohello máquina virtual, que permite la comunicación de SSH con máquina Hola pero nada más. Por tanto, Hola de orden tooview aplicación de lista de tareas, que es toorun configurado en el puerto 8080, este puerto también debe toobe añadido.

Devolver toohello Portal de Azure y complete Hola pasos:

* Haga clic en "Grupos de recursos" en la barra de navegación izquierdo de hello;
* Seleccionar grupo de recursos de Hola que contiene la máquina virtual;
* En la lista resultante de Hola de recursos, seleccione el grupo de seguridad de red de hello (Hola uno con un icono de escudo);
* En Propiedades de hello, elija "las reglas de seguridad de entrada";
* En la barra de herramientas de hello, haga clic en "Agregar";
* Especifique un nombre como "default-allow-todo".
* Establecer el protocolo de hello demasiado "TCP";
* Establecer el intervalo de puertos de destino de hello demasiado "8080;"
* Haga clic en Aceptar y espere toobe de regla de seguridad de hello creado.

Después de crear esta regla de seguridad, Hola la aplicación de tareas está visible públicamente en internet de Hola y puede examinar tooit, por ejemplo mediante una dirección URL como:

    http://machinename.region.cloudapp.azure.com:8080

Observará que, aunque aún no hemos configurado máquina virtual de hello MongoDB, Hola la aplicación de tareas aparece toobe muy funcional. Esto es porque repositorio de código fuente de hello está codificado de forma rígida toouse una instancia de MongoDB previamente implementada. Una vez que hemos configurado Hola MongoDB virtual machine, se le volver atrás y cambiar tooutilize de código de origen de hello nuestra instancia privada de MongoDB en su lugar.

### <a name="configuring-hello-mongodb-virtual-machine"></a>Configuración de máquina Virtual de MongoDB Hola
SSH toohello segundo equipo que creó mediante PuTTY, ssh línea de comandos o la herramienta SSH prefiera. Después de ver el mensaje de bienvenida de Hola y el símbolo del sistema, instale MongoDB (estas instrucciones se realizaron desde [aquí](https://docs.mongodb.org/master/tutorial/install-mongodb-on-ubuntu/)):

    sudo apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv EA312927
    echo "deb http://repo.mongodb.org/apt/ubuntu trusty/mongodb-org/3.2 multiverse" | sudo tee /etc/apt/sources.list.d/mongodb-org-3.2.list
    sudo apt-get update
    sudo apt-get install -y mongodb-org

De forma predeterminada, MongoDB está configurado para que solo se pueda acceder localmente. Para este tutorial, se configurará MongoDB por lo que puede obtenerse de la máquina virtual de la aplicación hello. En un contexto de sudo, abra hello /etc/mongod.conf archivo y busque hello `# network interfaces` sección. Hola de cambio `net.bindIp` configuración valor demasiado`0.0.0.0`.

> [!NOTE]
> Esta configuración es para fines de Hola de este tutorial solo. **NO** constituye una práctica de seguridad recomendada y no se debe usar en entornos de producción.
> 
> 

Ahora asegúrese Hola MongoDB se ha iniciado el servicio:

    sudo service mongod restart

MongoDB funciona a través del puerto 27017 de manera predeterminada. Por lo tanto, en hello igual que necesitábamos tooopen el puerto 8080 en máquina virtual de hello web front-end, es necesario que el puerto de tooopen 27017 en la máquina virtual de hello MongoDB.

Devolver toohello Portal de Azure y complete Hola pasos:

* Haga clic en "Grupos de recursos" en la barra de navegación izquierdo de hello;
* Seleccionar grupo de recursos de Hola que contiene la máquina virtual de hello MongoDB;
* En la lista resultante de Hola de recursos, seleccione el grupo de seguridad de red de hello (Hola uno con un icono de escudo) con el mismo nombre que se le asignó la máquina virtual de toohello MongoDB; de Hola
* En Propiedades de hello, elija "las reglas de seguridad de entrada";
* En la barra de herramientas de hello, haga clic en "Agregar";
* Especifique un nombre como "default-allow-mongo".
* Establecer el protocolo de hello demasiado "TCP";
* Establecer el intervalo de puertos de destino de hello demasiado "27017;"
* Haga clic en Aceptar y espere toobe de regla de seguridad de hello creado.

## <a name="iterating-on-hello-todo-application"></a>Iterar en hello aplicación de lista de tareas
Hasta ahora, hemos proporcionamos dos máquinas virtuales de Linux: uno que ejecuta la aplicación hello front-end web y otra que esté ejecutando una instancia de MongoDB. Pero hay un problema: front-end web de hello no es realmente Hola aprovisionado MongoDB instancia todavía utiliza. Vamos a solucionar esto mediante la actualización de hello web front-end código toouse una variable de entorno en lugar de una instancia codificados de forma rígida.

### <a name="changing-hello-todo-application"></a>Cambio de la aplicación hello tareas
En el equipo de desarrollo donde clonó repositorio todo en el nodo de Hola por primera vez, abra hello `node-todo/config/database.js` un archivo en su editor favorito y cambie el valor de dirección url de Hola de valor codificado de forma rígida de hello como `mongodb://...` demasiado`process.env.MONGODB`.

Confirme los cambios e inserte a toohello GitHub master:

    git commit -am "Get MongoDB instance from env"
    git push origin master

Lamentablemente, esto no publica máquina virtual del Hola cambio toohello web front-end. Vamos a hacer un mecanismo simple pero eficaz para la publicación de actualizaciones para que pueda observar rápidamente efecto Hola de cambios de hello en el entorno activo de hello unos más cambios toothat máquina virtual tooenable.

### <a name="configuring-hello-web-frontend-virtual-machine"></a>Configuración de máquina Virtual del servidor front-end Web de Hola
Recuerde que creamos previamente un clon reconstrucción del repositorio de todo en el nodo de hello en la máquina virtual de hello web front-end. Esto resulta que esta acción crea un nuevo Git remoto toowhich cambios se pueden insertar. Sin embargo, simplemente insertar toothis remoto no proporciona bastante modelo del iteración rápida de Hola que están buscando los programadores al trabajar en su código.

Lo que nos gustaría toobe capaz de toodo es asegurarse de que cuando se produce un repositorio remoto de toohello de inserción en la máquina virtual de hello, ejecución de la aplicación tareas Hola se actualiza automáticamente. Afortunadamente, esto es fácil tooachieve con git.

GIT expone una serie de enlaces que se denominan a veces determinado tooreact tooactions realizadas en el repositorio de Hola. Se especifican mediante secuencias de comandos de shell en el repositorio de hello `hooks` carpeta. enlace de Hola que es más apropiado para el escenario de actualización automática de hello es hello `post-update` eventos.

En una máquina de virtual SSH sesión toohello web front-end, cambie toohello `~/node-todo.git/hooks` directorio y agregue Hola siguiente con el nombre el archivo de contenido tooa `post-update` (reemplazando `machinename` y `region` con la información de la máquina virtual de MongoDB):

    #!/bin/bash

    forever stopall
    unset 'GIT_DIR'
    export MONGODB="mongodb://machinename.region.cloudapp.azure.com:27017/tododb"
    cd ~/node-todo && git fetch origin && git pull origin master && npm install && forever start ~/node-todo/server.js
    exec git update-server-info

Asegúrese de que este archivo es ejecutable ejecutando Hola siguiente comando:

    chmod 755 post-update

Este script se asegura de que se detiene la aplicación de servidor actual de hello, código de hello en el repositorio clonado hello es toohello actualizada más reciente, se cumplen todas las dependencias actualizadas y se reinicia el servidor de Hola. También se asegura de que ese entorno Hola se ha configurado en preparación para recibir la primera instancia de aplicación actualización tooget Hola MongoDB de una variable de entorno.

### <a name="configuring-your-development-machine"></a>Configuración de la máquina de desarrollo
Ahora vamos a su equipo de desarrollo enlazarse de máquina virtual de toohello web front-end. Esto es tan simple como Agregar repositorio de reconstrucción de hello en la máquina virtual de Hola como un control remoto. Ejecutar este ejemplo Hola siguiendo el comando toodo (reemplazando *usuario* con su nombre de inicio de sesión de máquina virtual de front-end web y *machinename* y *región* según corresponda):

    git remote add azure user@machinename.region.cloudapp.azure.com:node-todo.git

Esto es todo lo que es necesario tooenable insertar o publicar en vigor, cambios de máquina virtual de toohello web front-end.

### <a name="publishing-updates"></a>Publicación de actualizaciones
Vamos a publicar el cambio de uno de Hola que se ha realizado hasta ahora para que la aplicación hello usará nuestra propia instancia de MongoDB:

    git push azure master

Debería ver toothis similar de salida:

    Counting objects: 4, done.
    Delta compression using up too4 threads.
    Compressing objects: 100% (3/3), done.
    Writing objects: 100% (4/4), 406 bytes | 0 bytes/s, done.
    Total 4 (delta 1), reused 0 (delta 0)
    remote: info:    Forever stopped processes:
    remote: data:        uid  command         script    forever pid  id logfile                         uptime
    remote: data:    [0] 0Lyh /usr/bin/nodejs server.js 9064    9301    /home/username/.forever/0Lyh.log 0:0:3:17.487
    remote: From /home/username/node-todo
    remote:    5f31fd7..5bc7be5  master     -> origin/master
    remote: From /home/username/node-todo
    remote:  * branch            master     -> FETCH_HEAD
    remote: Updating 5f31fd7..5bc7be5
    remote: Fast-forward
    remote:  config/database.js | 2 +-
    remote:  1 file changed, 1 insertion(+), 1 deletion(-)
    remote: npm WARN package.json node-todo@0.0.0 No repository field.
    remote: npm WARN package.json node-todo@0.0.0 No license field.
    remote: warn:    --minUptime not set. Defaulting to: 1000ms
    remote: warn:    --spinSleepTime not set. Your script will exit if it does not stay up for at least 1000ms
    remote: info:    Forever processing file: /home/username/node-todo/server.js
    toousername@machinename.region.cloudapp.azure.com:node-todo.git
    5f31fd7..5bc7be5  master -> master

Una vez completado este comando, pruebe a actualizar la aplicación hello en un explorador web. Debe ser capaz de toosee que lista de tareas de hello proporcionada en esta guía está vacía y ya no está enlazada toohello compartido implementado MongoDB instancia.

tutorial de hello toocomplete, vamos a hacer más visible, otro cambio. En el equipo de desarrollo, abra el archivo de node-todo/public/index.html de hello con su editor favorito. Localizar hello jumbotron encabezado y cambie el título de Hola de "Soy una lista de tareas-aholic" demasiado "Soy un aholic Todo en Azure!".

Ahora vamos a confirmarlo:

    git commit -am "Azurify hello title"

Esta vez, vamos a publicar hello tooAzure de cambio antes de insertar repositorio de GitHub de tooback toohello:

    git push azure master

Una vez completado este comando, página web de actualización de Hola y verá cambios Hola. Puesto que se muestren correctamente, push Hola cambio toohello atrás origen remoto: 

    git push origin master

## <a name="next-steps"></a>Pasos siguientes
En este artículo ha explicado cómo tootake una aplicación Node.js e implementar máquinas virtuales de tooLinux ejecuta en Azure. toolearn más información acerca de máquinas virtuales de Linux en Azure, consulte [tooLinux de introducción en Azure](/documentation/articles/virtual-machines-linux-introduction/).

Para obtener más información acerca de cómo toodevelop las aplicaciones Node.js en Azure, vea hello [Centro para desarrolladores de Node.js](/develop/nodejs/).

