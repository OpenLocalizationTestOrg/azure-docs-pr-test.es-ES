---
title: aaaJenkins CI/CD con Kubernetes en el servicio de contenedor de Azure | Documentos de Microsoft
description: "Cómo procesar tooautomate un CD de integración continua con Jenkins toodeploy y actualiza una aplicación en contenedores en Kubernetes en el servicio de contenedor de Azure"
services: container-service
documentationcenter: 
author: chzbrgr71
manager: johny
editor: 
tags: acs, azure-container-service, jenkins
keywords: Docker, contenedores, Kubernetes, Azure, Jenkins
ms.assetid: 
ms.service: container-service
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/23/2017
ms.author: briar
ms.custom: mvc
ms.openlocfilehash: e00e13bf06619bed73e82878777e55458ea3dd77
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="jenkins-integration-with-azure-container-service-and-kubernetes"></a>Integración de Jenkins con Azure Container Service y Kubernetes 
En este tutorial, recorreremos Hola proceso tooset la integración continua de una aplicación de contenedor múltiples en Kubernetes de servicio de contenedor de Azure con la plataforma de Jenkins Hola. flujo de trabajo de Hello imagen de contenedor de hello en Docker Hub de actualizaciones pod de hello Kubernetes mediante una ejecución de la implementación. 

## <a name="high-level-process"></a>Proceso de alto nivel
Hola pasos básicos descritos en este artículo son: 
- Instalación de un clúster de Kubernetes en Container Service
- Configurar Jenkins y acceso tooContainer servicio
- Creación de un flujo de trabajo de Jenkins
- Probar el proceso final tooend de hello CI/CD

## <a name="install-a-kubernetes-cluster"></a>Instalación de un clúster de Kubernetes
    
Implementar el clúster de Kubernetes de hello en el servicio de contenedor de Azure con hello pasos. La documentación completa se encuentra [aquí](container-service-kubernetes-walkthrough.md).

### <a name="step-1-create-a-resource-group"></a>Paso 1: Creación de un grupo de recursos
```azurecli
RESOURCE_GROUP=my-resource-group
LOCATION=westus

az group create --name=$RESOURCE_GROUP --location=$LOCATION
```

### <a name="step-2-deploy-hello-cluster"></a>Paso 2: Implementar el clúster de Hola
> [!NOTE]
> Hello estos pasos requieren una clave pública local de SSH almacenada en la carpeta de ~/.ssh Hola.
>

```azurecli
RESOURCE_GROUP=my-resource-group
DNS_PREFIX=some-unique-value
CLUSTER_NAME=any-acs-cluster-name

az acs create \
--orchestrator-type=kubernetes \
--resource-group $RESOURCE_GROUP \
--name=$CLUSTER_NAME \
--dns-prefix=$DNS_PREFIX \
--ssh-key-value ~/.ssh/id_rsa.pub \
--admin-username=azureuser \
--master-count=1 \
--agent-count=5 \
--agent-vm-size=Standard_D1_v2
```

## <a name="set-up-jenkins-and-configure-access-toocontainer-service"></a>Configurar Jenkins y acceso tooContainer servicio

### <a name="step-1-install-jenkins"></a>Paso 1: Instalación de Jenkins
1. Cree una máquina virtual de Azure con Ubuntu 16.04 LTS.  Puesto que más adelante en hello los pasos se necesita tooconnect toothis VM con bash en el equipo local, la clave pública de conjunto hello 'Tipo de autenticación' too'SSH' y pegar Hola clave pública SSH que se almacena localmente en la carpeta ~/.ssh.  Además, tome nota de hello 'Nombre de usuario' que se especifican como este nombre de usuario estará panel de tooview necesario Hola Jenkins y para la conexión toohello Jenkins VM en pasos posteriores.
2. Instale Jenkins mediante estas [instrucciones](https://wiki.jenkins-ci.org/display/JENKINS/Installing+Jenkins+on+Ubuntu). Se puede encontrar un tutorial más detallado en [howtoforge.com](https://www.howtoforge.com/tutorial/how-to-install-jenkins-with-apache-on-ubuntu-16-04).
3. tooview Hola Jenkins panel en el equipo local, actualizar el puerto de tooallow 8080 para el grupo de seguridad de red de Azure hello mediante la adición de una regla de entrada que permite acceso tooport 8080.  Además, puede configurar el desvío del puerto mediante la ejecución de este comando: `ssh -i ~/.ssh/id_rsa -L 8080:localhost:8080 <your_jenkins_user>@<your_jenkins_public_ip`
4. Conecte tooyour Jenkins servidor mediante el Explorador de hello desplazándose IP pública de toohello (http:// < your_jenkins_public_ip >: 8080) y desbloquear el panel de Jenkins Hola para hello primera vez con la contraseña de administrador inicial de Hola.  contraseña de administrador de Hola se almacena en /var/lib/jenkins/secrets/initialAdminPassword en hello Jenkins VM.  Un tooget fácilmente esta contraseña es tooSSH en Hola Jenkins VM: `ssh <your_jenkins_user>@<your_jenkins_public_ip>`.  A continuación, ejecute: `sudo cat /var/lib/jenkins/secrets/initialAdminPassword`.
5. Instalación de Docker en la máquina de hello Jenkins a través de estos [instrucciones](https://docs.docker.com/cs-engine/1.13/#install-on-ubuntu-1404-lts-or-1604-lts). Esto permite toobe de comandos de Docker ejecutar trabajos Jenkins.
6. Configurar Docker permisos tooallow Jenkins tooaccess hello Docker extremo.

    ```bash
    sudo chmod 777 /run/docker.sock
    ```
8. Instale la CLI de `kubectl` en Jenkins. Se pueden encontrar más detalles en [Installing and Setting up kubectl](https://kubernetes.io/docs/tasks/kubectl/install/) (Instalación y configuración de kubectl).  Trabajos de Jenkins usará 'kubectl' toomanage e implementar toohello Kubernetes clúster.

    ```bash
    curl -LO https://storage.googleapis.com/kubernetes-release/release/$(curl -s https://storage.googleapis.com/kubernetes-release/release/stable.txt)/bin/linux/amd64/kubectl

    chmod +x ./kubectl

    sudo mv ./kubectl /usr/local/bin/kubectl
    ```

### <a name="step-2-set-up-access-toohello-kubernetes-cluster"></a>Paso 2: Configurar el clúster de acceso toohello Kubernetes

> [!NOTE]
> Hay varios Hola de tooaccomplishing enfoques pasos. Usar el enfoque de Hola que sea más fácil para usted.
>

1. Hola copia `kubectl` toohello del archivo de configuración Jenkins automático para que los trabajos Jenkins tengan clúster de acceso toohello Kubernetes. Estas instrucciones se supone que está usando intensiva de errores desde un equipo diferente de Hola Jenkins VM y que una clave pública de SSH local se almacena en la carpeta de la máquina de hello ~/.ssh.

```bash
export KUBE_MASTER=<your_cluster_master_fqdn>
export JENKINS_USER=<your_jenkins_user>
export JENKINS_SERVER=<your_jenkins_public_ip>
sudo ssh $JENKINS_USER@$JENKINS_SERVER sudo mkdir -m 777 /home/$JENKINS_USER/.kube/ \
&& sudo ssh $JENKINS_USER@$JENKINS_SERVER sudo mkdir /var/lib/jenkins/.kube/ \
&& sudo scp -3 -i ~/.ssh/id_rsa azureuser@$KUBE_MASTER:.kube/config $JENKINS_USER@$JENKINS_SERVER:~/.kube/config \
&& sudo ssh -i ~/.ssh/id_rsa $JENKINS_USER@$JENKINS_SERVER sudo cp /home/$JENKINS_USER/.kube/config /var/lib/jenkins/.kube/config \
```
        
2. Validar from Jenkins ese hello Kubernetes clúster es accesible.  toodo, SSH en hello Jenkins VM: `ssh <your_jenkins_user>@<your_jenkins_public_ip>`.  A continuación, compruebe Jenkins puede conectarse correctamente clúster tooyour: `kubectl cluster-info`.
    

## <a name="create-a-jenkins-workflow"></a>Creación de un flujo de trabajo de Jenkins

### <a name="prerequisites"></a>Requisitos previos

- Cuenta de GitHub para el repositorio de código.
- Concentrador cuenta toostore y actualizar imágenes de docker.
- Aplicación en contenedor que se puede volver a compilar y actualizar. Puede usar esta aplicación de contenedor de ejemplo escrita en Golang: https://github.com/chzbrgr71/go-web. 

> [!NOTE]
> Hello estos pasos se deben realizar en su propia cuenta de GitHub. Cree hello tooclone libre por encima del repositorio, pero debe utilizar sus propio webhooks de hello tooconfigure de cuenta y tener acceso Jenkins.
>

### <a name="step-1-deploy-initial-v1-of-application"></a>Paso 1: Implementación de la v1 inicial de la aplicación
1. Crear aplicación hello de máquina del desarrollador de hello con hello siga los comandos. Reemplace `myrepo` por el suyo propio.
    
    ```bash
    git clone https://github.com/chzbrgr71/go-web.git
    cd go-web
    docker build -t myrepo/go-web .
    ```

2. Insertar imagen tooDocker concentrador.

    ```bash
    docker login
    docker push myrepo/go-web
    ```

3. Implementar toohello Kubernetes clúster.
    
    > [!NOTE] 
    > Editar hello `go-web.yaml` archivo tooupdate su imagen de contenedor y el repositorio.
    >
        
    ```bash
    kubectl create -f ./go-web.yaml --record
    ```
### <a name="step-2-configure-jenkins-system"></a>Paso 2: Configuración del sistema Jenkins
1. Haga clic en **Manage Jenkins** >  (Administrar Jenkins) **Configure System** (Configurar el sistema).
2. En **GitHub**, seleccione **Add GitHub Server** (Agregar servidor de GitHub).
3. Deje **API URL** (Dirección URL de API) como valor predeterminado.
4. En **Credentials** (Credenciales), agregue una credencial de Jenkins mediante **texto secreto**. Se recomienda usar tokens de acceso personal de GitHub, que se configuran en la configuración de su cuenta de usuario de GitHub. Puede encontrar más detalles al respecto [aquí.](https://help.github.com/articles/creating-a-personal-access-token-for-the-command-line/)
5. Haga clic en **Probar conexión** tooensure esto está configurado correctamente.
6. En **Global Properties** (Propiedades globales), agregue una variable de entorno `DOCKER_HUB` y proporcione su contraseña de Docker Hub. (Esto es útil en esta demostración, pero en un escenario de producción sería necesario un enfoque más seguro).
7. Haga clic en Save (Guardar).

![Acceso a GitHub de Jenkins](./media/container-service-kubernetes-jenkins/jenkins-github-access.png)

### <a name="step-3-create-hello-jenkins-workflow"></a>Paso 3: Crear el flujo de trabajo de hello Jenkins
1. Cree un elemento de Jenkins.
2. Proporcione un nombre (por ejemplo, "go-web") y seleccione **Freestyle Project** (Proyecto de estilo libre). 
3. Comprobar **GitHub proyecto** y proporcione el repositorio de GitHub de tooyour de dirección URL de Hola.
4. En **administración de código fuente**, proporcione la dirección URL de repositorio de GitHub de Hola y las credenciales. 
5. Agregar un **paso de compilación** de tipo **ejecutar shell** y use Hola siguiendo texto:

    ```bash
    WEB_IMAGE_NAME="myrepo/go-web:kube${BUILD_NUMBER}"
    docker build -t $WEB_IMAGE_NAME .
    docker login -u <your-dockerhub-username> -p ${DOCKER_HUB}
    docker push $WEB_IMAGE_NAME
    ```

6. Agregue otro **paso de compilación** de tipo **ejecutar shell** y use Hola siguiendo texto:

    ```bash
    WEB_IMAGE_NAME="myrepo/go-web:kube${BUILD_NUMBER}"
    kubectl set image deployment/go-web go-web=$WEB_IMAGE_NAME --kubeconfig /var/lib/jenkins/config
    ```

![Pasos de compilación de Jenkins](./media/container-service-kubernetes-jenkins/jenkins-build-steps.png)
    
7. Guardar elemento de hello Jenkins y probar con **generar ahora**.

### <a name="step-4-connect-github-webhook"></a>Paso 4: Conexión del webhook de GitHub
1. En el elemento de Jenkins Hola que creó, haga clic en **configurar**.
2. En **Build Triggers** (Compila desencadenadores), seleccione **GitHub hook trigger for GITScm polling** (Desencadenador de enlace de GitHub para sondeo de GITScm) y haga clic en **Save** (Guardar). Esto configura automáticamente hello GitHub webhook.
3. En el repositorio de GitHub para go-web, haga clic en **Settings > Webhooks** (Configuración > Webhooks).
4. Compruebe que hello webhook Jenkins dirección URL se agregó correctamente. dirección URL de Hello debe finalizar en "github webhook".

![Configuración del webhook de Jenkins](./media/container-service-kubernetes-jenkins/jenkins-webhook.png)

## <a name="test-hello-cicd-process-end-tooend"></a>Probar el proceso final tooend de hello CI/CD

1. Actualizar código para el repositorio de Hola e inserción/sincronización con el repositorio de GitHub de Hola.
2. Desde la consola de Jenkins hello, active hello **generar historial** y validar ese Hola trabajo se ha ejecutado. Ver detalles de toosee de salida de consola.
3. Desde Kubernetes, ver detalles de hello actualizan implementación:

    ```bash
    kubectl rollout history deployment/go-web
    ```

## <a name="next-steps"></a>Pasos siguientes

- Implemente Azure Container Registry y almacene las imágenes en un repositorio seguro. Consulte [Documentación de Azure Container Registry](https://docs.microsoft.com/azure/container-registry).
- Cree un flujo de trabajo más complejo que incluya la implementación en paralelo y pruebas automatizadas de Jenkins.
- Para obtener más información acerca de elementos de configuración/CD con Jenkins y Kubernetes, vea hello [Jenkins blog](https://jenkins.io/blog/2015/07/24/integrating-kubernetes-and-jenkins/).
