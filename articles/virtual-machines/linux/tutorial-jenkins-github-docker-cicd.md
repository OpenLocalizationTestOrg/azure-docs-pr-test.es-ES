---
title: "una canalización de desarrollo en Azure con Jenkins aaaCreate | Documentos de Microsoft"
description: "Obtenga información acerca de cómo toocreate un Jenkins virtual automático en Azure que extrae desde GitHub en cada código de confirmación y crea a una nuevo Docker contenedor toorun la aplicación"
services: virtual-machines-linux
documentationcenter: virtual-machines
author: iainfoulds
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 05/08/2017
ms.author: iainfou
ms.custom: mvc
ms.openlocfilehash: c079e3c9186c9da0a3e51e1823215779c565e0dc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="how-toocreate-a-development-infrastructure-on-a-linux-vm-in-azure-with-jenkins-github-and-docker"></a>¿Cómo toocreate una infraestructura de desarrollo en una VM de Linux en Azure con Jenkins, GitHub y Docker
tooautomate Hola compilación y prueba la fase de desarrollo de aplicaciones, puede usar una integración continua y la canalización de implementación (CI/CD). En este tutorial, creará una canalización de CI/CD en una máquina virtual de Azure, y aprenderá los siguientes temas:

> [!div class="checklist"]
> * Crear una máquina virtual de Jenkins
> * Instalar y configurar Jenkins
> * Crear la integración de webhook entre GitHub y Jenkins
> * Crear y desencadenar trabajos de compilación de Jenkins desde confirmaciones de GitHub
> * Crear una imagen de Docker para la aplicación
> * Comprobar que GitHub confirma la imagen de Docker de nueva compilación y actualiza la aplicación en ejecución


[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

Si elige tooinstall y usar hello CLI localmente, este tutorial requiere que se ejecuta la versión de CLI de Azure de hello 2.0.4 o versiones posteriores. Ejecutar `az --version` toofind versión de Hola. Si necesita tooinstall o una actualización, consulte [instalar Azure CLI 2.0]( /cli/azure/install-azure-cli). 

## <a name="create-jenkins-instance"></a>Creación de la instancia de Jenkins
En un tutorial anterior en [cómo toocustomize una máquina virtual de Linux en el primer arranque](tutorial-automate-vm-deployment.md), también habrá aprendido cómo tooautomate personalización de máquina virtual con init de la nube. Este tutorial utiliza una nube init archivo tooinstall Jenkins y Docker en una máquina virtual. 

En el shell actual, cree un archivo denominado *init.txt nube* y pegar Hola siguiente configuración. Por ejemplo, crear archivo hello en hello Shell en la nube, no en el equipo local. Escriba `sensible-editor cloud-init-jenkins.txt` toocreate Hola archivo y ver una lista de editores disponibles. Asegúrese de que ese archivo de nube-init todo Hola se copia correctamente, especialmente Hola primera línea:

```yaml
#cloud-config
package_upgrade: true
write_files:
  - path: /etc/systemd/system/docker.service.d/docker.conf
    content: |
      [Service]
        ExecStart=
        ExecStart=/usr/bin/dockerd
  - path: /etc/docker/daemon.json
    content: |
      {
        "hosts": ["fd://","tcp://127.0.0.1:2375"]
      }
runcmd:
  - wget -q -O - https://jenkins-ci.org/debian/jenkins-ci.org.key | apt-key add -
  - sh -c 'echo deb http://pkg.jenkins-ci.org/debian-stable binary/ > /etc/apt/sources.list.d/jenkins.list'
  - apt-get update && apt-get install jenkins -y
  - curl -sSL https://get.docker.com/ | sh
  - usermod -aG docker azureuser
  - usermod -aG docker jenkins
  - service jenkins restart
```

Antes de poder crear una máquina virtual, cree un grupo de recursos con [az group create](/cli/azure/group#create). Hello en el ejemplo siguiente se crea un grupo de recursos denominado *myResourceGroupJenkins* en hello *eastus* ubicación:

```azurecli-interactive 
az group create --name myResourceGroupJenkins --location eastus
```

Ahora cree una máquina virtual con el comando [az vm create](/cli/azure/vm#create). Hola de uso `--custom-data` toopass de parámetro en el archivo de configuración de nube init. Proporcione la ruta de acceso completa de hello demasiado*nube-init-jenkins.txt* si guarda el archivo hello fuera de su directorio de trabajo actual.

```azurecli-interactive 
az vm create --resource-group myResourceGroupJenkins \
    --name myVM \
    --image UbuntuLTS \
    --admin-username azureuser \
    --generate-ssh-keys \
    --custom-data cloud-init-jenkins.txt
```

Se tarda unos minutos para hello toobe de máquina virtual creada y configurada.

tooallow web tooreach de tráfico de la máquina virtual, use [az de vm abrir puerto](/cli/azure/vm#open-port) tooopen puerto *8080* para tráfico Jenkins y el puerto *1337* para aplicación de Node.js de hello es toorun usa una aplicación de ejemplo:

```azurecli-interactive 
az vm open-port --resource-group myResourceGroupJenkins --name myVM --port 8080 --priority 1001
az vm open-port --resource-group myResourceGroupJenkins --name myVM --port 1337 --priority 1002
```


## <a name="configure-jenkins"></a>Configuración de Jenkins
tooaccess su Jenkins la instancia, obtener dirección IP pública de saludo de la máquina virtual:

```azurecli-interactive 
az vm show --resource-group myResourceGroupJenkins --name myVM -d --query [publicIps] --o tsv
```

Por motivos de seguridad, se necesita contraseña de administrador inicial de hello tooenter que se almacena en un archivo de texto en el saludo de toostart VM que Jenkins instalar. Usar dirección IP pública Hola obtenida en hello anterior paso tooSSH tooyour VM:

```bash
ssh azureuser@<publicIps>
```

Hola de vista `initialAdminPassword` para instalar sus Jenkins y se copia:

```bash
sudo cat /var/lib/jenkins/secrets/initialAdminPassword
```

Si el archivo hello aún no está disponible, espere unos minutos más en la nube init toocomplete Hola Jenkins e instalación de Docker.

Ahora, abra un explorador web y vaya demasiado`http://<publicIps>:8080`. Complete el saludo inicial Jenkins el programa de instalación como se indica a continuación:

- Escriba hello *initialAdminPassword* obtenido de hello VM en el paso anterior de Hola.
- Haga clic en **seleccione complementos tooinstall**
- Busque *GitHub* en el cuadro de texto de Hola a través de la parte superior de hello, seleccione hello *complemento de GitHub*, a continuación, haga clic en **instalar**
- toocreate una cuenta de usuario Jenkins, rellenar el formulario de hello según sea necesario. Desde la perspectiva de seguridad, debe crear este primer usuario Jenkins en lugar de continuar como cuenta de administrador predeterminada de Hola.
- Cuando termine, haga clic en **Start using Jenkins** (Empezar a usar Jenkins).


## <a name="create-github-webhook"></a>Creación de un webhook de GitHub
integración de hello tooconfigure con GitHub, abra hello [aplicación de ejemplo de Hola a todos Node.js](https://github.com/Azure-Samples/nodejs-docs-hello-world) desde el repositorio de ejemplos de Azure de Hola. toofork Hola repositorio tooyour posee la cuenta de GitHub, haga clic en hello **bifurcar** botón en la esquina superior derecha de Hola.

Crear un webhook dentro de bifurcación de Hola que creó:

- Haga clic en **configuración**, a continuación, seleccione **integraciones & servicios** en el lado izquierdo de Hola.
- Haga clic en **Agregar servicio** y, luego, escriba *Jenkins* en el cuadro de filtro.
- Seleccione *Jenkins (GitHub plugin)* Jenkins (complemento de GitHub).
- Para hello **Jenkins enlazar la dirección URL**, escriba `http://<publicIps>:8080/github-webhook/`. Asegúrese de incluir finales Hola /
- Haga clic en **Add service** (Agregar servicio).

![Agregar repositorio de GitHub webhook tooyour bifurcado](media/tutorial-jenkins-github-docker-cicd/github_webhook.png)


## <a name="create-jenkins-job"></a>Creación de trabajos de Jenkins
toohave Jenkins responden tooan evento en GitHub como Confirmar código, cree un trabajo de Jenkins. 

En el sitio Web Jenkins, haga clic en **crear trabajos nuevos** desde la página principal de hello:

- Escriba *HelloWorld* como nombre del trabajo. Seleccione **Freestyle project** (Proyecto de estilo libre) y elija **OK** (Aceptar).
- En hello **General** sección, seleccione **GitHub** proyecto y escriba la dirección URL de repositorio bifurcada, como por ejemplo *https://github.com/iainfoulds/nodejs-docs-hello-world*
- En hello **del origen de la administración de código** sección, seleccione **Git**, escriba su repositorio bifurcada *.git* de dirección URL, como *https://github.com/iainfoulds/nodejs-docs-hello-world.git*
- En hello **crear desencadenadores** sección, seleccione **GitHub desencadenador de enlace para el sondeo de GITscm**.
- En hello **generar** sección, elija **agregar el paso de compilación**. Seleccione **ejecutar shell**, a continuación, escriba `echo "Testing"` en la ventana de toocommand.
- Haga clic en **guardar** final Hola de ventana de trabajos de Hola.


## <a name="test-github-integration"></a>Prueba de la integración de GitHub
Hola tootest GitHub integración con Jenkins, confirmar un cambio en la bifurcación. 

En GitHub de interfaz de usuario web, seleccione el repositorio bifurcada y, a continuación, haga clic en hello **index.js** archivo. Haga clic en tooedit de icono de lápiz Hola este archivo para que lea la línea 6:

```nodejs
response.end("Hello World!");
```

toocommit los cambios, haga clic en hello **Confirmar cambios** situado en la parte inferior de Hola.

En Jenkins, se inicia una nueva compilación en hello **generar historial** sección de esquina Hola inferior izquierda de la página de trabajo. Haga clic en el vínculo de número de compilación de Hola y seleccione **consola salida** en tamaño izquierdo Hola. Puede ver los pasos de hello Jenkins tarda más que el código se haya extraído de hello y GitHub compilación acción salidas mensaje hello `Testing` toohello consola. Cada vez que se realiza una confirmación en GitHub, hello webhook llega tooJenkins y desencadenan una nueva compilación de este modo.


## <a name="define-docker-build-image"></a>Definición de la imagen de la compilación de Docker
aplicación de Node.js de hello toosee ejecutando basándose en las confirmaciones de GitHub, permite generar una Docker aplicación hello de imagen toorun. imagen de Hola se crea a partir de un archivo Dockerfile que define cómo tooconfigure Hola contenedor que se ejecuta la aplicación hello. 

Desde Hola SSH conexión tooyour VM, cambie el directorio de área de trabajo de Jenkins de toohello con el nombre de trabajo de Hola que creó en el paso anterior. En nuestro ejemplo, se llama "*HelloWorld*".

```bash
cd /var/lib/jenkins/workspace/HelloWorld
```

Cree un archivo con en este directorio de área de trabajo con `sudo sensible-editor Dockerfile` y pegar Hola siguiendo el contenido. Asegúrese de que ese hello que dockerfile todo es copiado correctamente, especialmente Hola primera línea:

```yaml
FROM node:alpine

EXPOSE 1337

WORKDIR /var/www
COPY package.json /var/www/
RUN npm install
COPY index.js /var/www/
```

Este Dockerfile usa Hola base Node.js imagen con Linux Alpine, puerto expone 1337 Hola aplicación Hola a todos, a continuación, se ejecuta, copia los archivos de aplicación Hola y la inicializa.


## <a name="create-jenkins-build-rules"></a>Creación de reglas de generación de Jenkins
En un paso anterior, creó una regla de compilación Jenkins básica que den como resultado una consola de toohello de mensaje. Permite crear toouse de paso de compilación de hello nuestro Dockerfile y ejecutar la aplicación hello.

En la instancia Jenkins, seleccione el trabajo de Hola que creó en el paso anterior. Haga clic en **configurar** en el lado izquierdo de Hola y desplácese hacia abajo toohello **generar** sección:

- Quite el paso de compilación `echo "Test"`. Haga clic en rojo cruzado en hello parte superior derecha del cuadro del paso de compilación existente de Hola Hola.
- Haga clic en **Add build step** (Agregar paso de compilación) y seleccione **Execute shell** (Ejecutar shell).
- Hola **comando** cuadro, escriba Hola siga los comandos de Docker y luego seleccione **guardar**:

  ```bash
  docker build --tag helloworld:$BUILD_NUMBER .
  docker stop helloworld && docker rm helloworld
  docker run --name helloworld -p 1337:1337 helloworld:$BUILD_NUMBER node /var/www/index.js &
  ```

pasos de compilación de Docker de Hello crean una imagen y etiqueta con hello Jenkins número de compilación de modo que pueda mantener un historial de imágenes. Los contenedores existentes que ejecuta la aplicación hello se detendrá y, a continuación, se quitará. Un nuevo contenedor es iniciado con imagen hello y se ejecuta la aplicación Node.js en función de confirmaciones más recientes de hello en GitHub.


## <a name="test-your-pipeline"></a>Prueba de la canalización
canalización completa de hello toosee en acción, editar hello *index.js* un archivo en el repositorio de GitHub bifurcado nuevo y haga clic en **Confirmar cambio**. Un nuevo trabajo se inicia en Jenkins según hello webhook para GitHub. Se tarda unos segundos en imagen de Docker de toocreate hello e iniciar la aplicación en un nuevo contenedor.

Si es necesario, volver a obtener la dirección IP pública de saludo de la máquina virtual:

```azurecli-interactive 
az vm show --resource-group myResourceGroupJenkins --name myVM -d --query [publicIps] --o tsv
```

Abra un explorador web y escriba `http://<publicIps>:1337`. La aplicación Node.js se muestra y refleja confirmaciones más recientes de hello en la bifurcación GitHub como se indica a continuación:

![Ejecución de la aplicación Node.js](media/tutorial-jenkins-github-docker-cicd/running_nodejs_app.png)

Ahora, realizar otro toohello editar *index.js* archivo en GitHub y Confirmar cambio de Hola. Espere unos segundos para toocomplete de trabajo de hello en Jenkins, a continuación, actualizar la versión de Hola actualizado de toosee de explorador web de la aplicación que se ejecuta en un nuevo contenedor, como se indica a continuación:

![Aplicación de Node.js en ejecución después de otra confirmación de GitHub](media/tutorial-jenkins-github-docker-cicd/another_running_nodejs_app.png)


## <a name="next-steps"></a>Pasos siguientes
En este tutorial, configurado GitHub toorun un trabajo de compilación Jenkins en cada confirmación de código y, a continuación, implementar un tootest del contenedor de Docker de la aplicación. Ha aprendido a:

> [!div class="checklist"]
> * Crear una máquina virtual de Jenkins
> * Instalar y configurar Jenkins
> * Crear la integración de webhook entre GitHub y Jenkins
> * Crear y desencadenar trabajos de compilación de Jenkins desde confirmaciones de GitHub
> * Crear una imagen de Docker para la aplicación
> * Comprobar que GitHub confirma la imagen de Docker de nueva compilación y actualiza la aplicación en ejecución

Avanzar toohello siguiente tutorial toolearn más información acerca de cómo toointegrate Jenkins con Visual Studio Team Services.

> [!div class="nextstepaction"]
> [Implementación de aplicaciones con Jenkins y Team Services](tutorial-build-deploy-jenkins.md)