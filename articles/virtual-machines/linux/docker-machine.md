---
title: "aaaUse máquina Docker toocreate Linux se hospeda en Azure | Documentos de Microsoft"
description: "Describe cómo se hospeda toouse máquina Docker toocreate Docker en Azure."
services: virtual-machines-linux
documentationcenter: 
author: iainfoulds
manager: timlt
editor: tysonn
ms.assetid: 164b47de-6b17-4e29-8b7d-4996fa65bea4
ms.service: virtual-machines-linux
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 06/19/2017
ms.author: iainfou
ms.openlocfilehash: 905c645add51c78305aac85a7013441b3a73972f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-docker-machine-toocreate-hosts-in-azure"></a>Cómo toouse máquina Docker toocreate se hospeda en Azure
Este artículo detalles de cómo toouse [máquina Docker](https://docs.docker.com/machine/) toocreate hosts en Azure. Hola `docker-machine` comando crea una máquina virtual (VM) de Linux en Azure, a continuación, instala Docker. A continuación, puede administrar los hosts de Docker en Azure mediante Hola mismas herramientas locales y los flujos de trabajo.

## <a name="create-vms-with-docker-machine"></a>Creación de VM con la máquina de Docker
En primer lugar, obtenga el identificador de suscripción de Azure con el comando [az account show](/cli/azure/account#show) de la manera siguiente:

```azurecli
sub=$(az account show --query "id" -o tsv)
```

Crear máquinas virtuales del host de Docker en Azure con `docker-machine create` especificando *azure* como controlador de Hola. Para obtener más información, vea hello [documentación del controlador de Azure Docker](https://docs.docker.com/machine/drivers/azure/)

Hello en el ejemplo siguiente se crea una máquina virtual denominada *myVM*, crea una cuenta de usuario denominada *azureuser*y abre el puerto *80* hello en el host de máquina virtual. Siga cualquier toolog indicaciones en tooyour cuenta de Azure y conceder máquina Docker permisos toocreate y administrar los recursos.

```bash
docker-machine create -d azure \
    --azure-subscription-id $sub \
    --azure-ssh-user azureuser \
    --azure-open-port 80 \
    myvm
```

salida de Hello tiene un aspecto similar toohello siguiente ejemplo:

```bash
Creating CA: /Users/user/.docker/machine/certs/ca.pem
Creating client certificate: /Users/user/.docker/machine/certs/cert.pem
Running pre-create checks...
(myvmdocker) Completed machine pre-create checks.
Creating machine...
(myvmdocker) Querying existing resource group.  name="docker-machine"
(myvmdocker) Creating resource group.  name="docker-machine" location="westus"
(myvmdocker) Configuring availability set.  name="docker-machine"
(myvmdocker) Configuring network security group.  name="myvmdocker-firewall" location="westus"
(myvmdocker) Querying if virtual network already exists.  rg="docker-machine" location="westus" name="docker-machine-vnet"
(myvmdocker) Creating virtual network.  name="docker-machine-vnet" rg="docker-machine" location="westus"
(myvmdocker) Configuring subnet.  name="docker-machine" vnet="docker-machine-vnet" cidr="192.168.0.0/16"
(myvmdocker) Creating public IP address.  name="myvmdocker-ip" static=false
(myvmdocker) Creating network interface.  name="myvmdocker-nic"
(myvmdocker) Creating storage account.  sku=Standard_LRS name="vhdski0hvfazyd8mn991cg50" location="westus"
(myvmdocker) Creating virtual machine.  location="westus" size="Standard_A2" username="azureuser" osImage="canonical:UbuntuServer:16.04.0-LTS:latest" name="myvmdocker"
Waiting for machine toobe running, this may take a few minutes...
Detecting operating system of created instance...
Waiting for SSH toobe available...
Detecting hello provisioner...
Provisioning with ubuntu(systemd)...
Installing Docker...
Copying certs toohello local machine directory...
Copying certs toohello remote machine...
Setting Docker configuration on hello remote daemon...
Checking connection tooDocker...
Docker is up and running!
toosee how tooconnect your Docker Client toohello Docker Engine running on this virtual machine, run: docker-machine env myvmdocker
```

## <a name="configure-your-docker-shell"></a>Configuración del shell de Docker
host de Docker de tooconnect tooyour en Azure, defina la configuración de conexión adecuada de Hola. Como se indicó al final de Hola de salida de hello, ver información de conexión de hello para el host Docker como se indica a continuación: 

```bash
docker-machine env myvmdocker
```

Hola de salida es similar toohello siguiente ejemplo:

```bash
export DOCKER_TLS_VERIFY="1"
export DOCKER_HOST="tcp://40.68.254.142:2376"
export DOCKER_CERT_PATH="/Users/user/.docker/machine/machines/machine"
export DOCKER_MACHINE_NAME="machine"
# Run this command tooconfigure your shell:
# eval $(docker-machine env myvmdocker)
```

configuración de la conexión de hello toodefine puede cualquier ejecución Hola sugiere los comandos de configuración (`eval $(docker-machine env myvmdocker)`), o se pueden establecer variables de entorno de hello manualmente. 

## <a name="run-a-container"></a>Ejecución de un contenedor
toosee un contenedor en acción, permite ejecutar un servidor de Web NGINX básica. Cree un contenedor con `docker run` y exponga el puerto 80 al tráfico web de la manera siguiente:

```bash
docker run -d -p 80:80 --restart=always nginx
```

Hola de salida es similar toohello siguiente ejemplo:

```bash
Unable toofind image 'nginx:latest' locally
latest: Pulling from library/nginx
ff3d52d8f55f: Pull complete
226f4ec56ba3: Pull complete
53d7dd52b97d: Pull complete
Digest: sha256:41ad9967ea448d7c2b203c699b429abe1ed5af331cd92533900c6d77490e0268
Status: Downloaded newer image for nginx:latest
675e6056cb81167fe38ab98bf397164b01b998346d24e567f9eb7a7e94fba14a
```

Vea los contenedores en funcionamiento con `docker ps`. Hello siguiente salida de ejemplo muestra hello NGINX que se ejecutan con el puerto 80 expuestas:

```bash
CONTAINER ID    IMAGE    COMMAND                   CREATED          STATUS          PORTS                          NAMES
d5b78f27b335    nginx    "nginx -g 'daemon off"    5 minutes ago    Up 5 minutes    0.0.0.0:80->80/tcp, 443/tcp    festive_mirzakhani
```

## <a name="test-hello-container"></a>Contenedor de prueba Hola
Obtener dirección IP pública de Hola de host Docker como se indica a continuación:


```bash
docker-machine ip myvmdocker
```

contenedor de hello toosee en acción, abra un explorador web y escriba la dirección IP pública Hola que se indican en la salida de hello de hello anterior comando:

![Ejecución del contenedor ngnix](./media/docker-machine/nginx.png)

## <a name="next-steps"></a>Pasos siguientes
También puede crear hosts con hello [extensión de máquina virtual de Docker](dockerextension.md). Para ver ejemplos sobre el uso de Docker Compose, consulte [Introducción a Docker y Compose en Azure](docker-compose-quickstart.md).
