---
title: aaaInstall MongoDB en una VM de Linux con hello CLI de Azure | Documentos de Microsoft
description: "Obtenga información acerca de cómo tooinstall y configurar MongoDB en un iusing de máquina virtual Linux Hola 2.0 de CLI de Azure"
services: virtual-machines-linux
documentationcenter: 
author: iainfoulds
manager: timlt
editor: 
ms.assetid: 3f55b546-86df-4442-9ef4-8a25fae7b96e
ms.service: virtual-machines-linux
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 06/23/2017
ms.author: iainfou
ms.openlocfilehash: 97a4d9913f0eeaf7b8bf15d7fc81befe538cdc8d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooinstall-and-configure-mongodb-on-a-linux-vm"></a><span data-ttu-id="84418-103">¿Cómo tooinstall y configurar MongoDB en una VM Linux</span><span class="sxs-lookup"><span data-stu-id="84418-103">How tooinstall and configure MongoDB on a Linux VM</span></span>
<span data-ttu-id="84418-104">[MongoDB](http://www.mongodb.org) es una conocida base de datos NoSQL de código abierto y alto rendimiento.</span><span class="sxs-lookup"><span data-stu-id="84418-104">[MongoDB](http://www.mongodb.org) is a popular open-source, high-performance NoSQL database.</span></span> <span data-ttu-id="84418-105">Este artículo muestra cómo tooinstall y configurar MongoDB en una VM de Linux con hello 2.0 de CLI de Azure.</span><span class="sxs-lookup"><span data-stu-id="84418-105">This article shows you how tooinstall and configure MongoDB on a Linux VM with hello Azure CLI 2.0.</span></span> <span data-ttu-id="84418-106">También puede realizar estos pasos con hello [Azure CLI 1.0](install-mongodb-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="84418-106">You can also perform these steps with hello [Azure CLI 1.0](install-mongodb-nodejs.md).</span></span> <span data-ttu-id="84418-107">Se muestran algunos ejemplos detallados de:</span><span class="sxs-lookup"><span data-stu-id="84418-107">Examples are shown that detail how to:</span></span>

* [<span data-ttu-id="84418-108">Instalación y configuración manuales de una instancia básica de MongoDB</span><span class="sxs-lookup"><span data-stu-id="84418-108">Manually install and configure a basic MongoDB instance</span></span>](#manually-install-and-configure-mongodb-on-a-vm)
* [<span data-ttu-id="84418-109">Creación de una instancia básica de MongoDB mediante una plantilla de Resource Manager</span><span class="sxs-lookup"><span data-stu-id="84418-109">Create a basic MongoDB instance using a Resource Manager template</span></span>](#create-basic-mongodb-instance-on-centos-using-a-template)
* [<span data-ttu-id="84418-110">Creación de un clúster complejo con particiones de MongoDB con conjuntos de réplicas mediante una plantilla de Resource Manager</span><span class="sxs-lookup"><span data-stu-id="84418-110">Create a complex MongoDB sharded cluster with replica sets using a Resource Manager template</span></span>](#create-a-complex-mongodb-sharded-cluster-on-centos-using-a-template)


## <a name="manually-install-and-configure-mongodb-on-a-vm"></a><span data-ttu-id="84418-111">Instalación y configuración manuales de MongoDB en una máquina virtual</span><span class="sxs-lookup"><span data-stu-id="84418-111">Manually install and configure MongoDB on a VM</span></span>
<span data-ttu-id="84418-112">MongoDB [proporciona instrucciones de instalación](https://docs.mongodb.com/manual/administration/install-on-linux/) para distribuciones de Linux, incluidos Red Hat/CentOS, SUSE, Ubuntu y Debian.</span><span class="sxs-lookup"><span data-stu-id="84418-112">MongoDB [provide installation instructions](https://docs.mongodb.com/manual/administration/install-on-linux/) for Linux distros including Red Hat / CentOS, SUSE, Ubuntu, and Debian.</span></span> <span data-ttu-id="84418-113">Hello ejemplo siguiente se crea un *CentOS* máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="84418-113">hello following example creates a *CentOS* VM.</span></span> <span data-ttu-id="84418-114">toocreate este entorno, deberá hello más reciente [CLI de Azure 2.0](/cli/azure/install-az-cli2) instalado y registrado en tooan cuenta de Azure mediante [inicio de sesión de az](/cli/azure/#login).</span><span class="sxs-lookup"><span data-stu-id="84418-114">toocreate this environment, you need hello latest [Azure CLI 2.0](/cli/azure/install-az-cli2) installed and logged in tooan Azure account using [az login](/cli/azure/#login).</span></span>

<span data-ttu-id="84418-115">Cree un grupo de recursos con [az group create](/cli/azure/group#create).</span><span class="sxs-lookup"><span data-stu-id="84418-115">Create a resource group with [az group create](/cli/azure/group#create).</span></span> <span data-ttu-id="84418-116">Hello en el ejemplo siguiente se crea un grupo de recursos denominado *myResourceGroup* en hello *eastus* ubicación:</span><span class="sxs-lookup"><span data-stu-id="84418-116">hello following example creates a resource group named *myResourceGroup* in hello *eastus* location:</span></span>

```azurecli
az group create --name myResourceGroup --location eastus
```

<span data-ttu-id="84418-117">Cree la máquina virtual con [az vm create](/cli/azure/vm#create).</span><span class="sxs-lookup"><span data-stu-id="84418-117">Create a VM with [az vm create](/cli/azure/vm#create).</span></span> <span data-ttu-id="84418-118">Hello en el ejemplo siguiente se crea una máquina virtual denominada *myVM* con un usuario denominado *azureuser* mediante la autenticación de clave pública SSH</span><span class="sxs-lookup"><span data-stu-id="84418-118">hello following example creates a VM named *myVM* with a user named *azureuser* using SSH public key authentication</span></span>

```azurecli
az vm create \
    --resource-group myResourceGroup \
    --name myVM \
    --image CentOS \
    --admin-username azureuser \
    --generate-ssh-keys
```

<span data-ttu-id="84418-119">SSH toohello VM con su propio nombre de usuario y hello `publicIpAddress` aparece en la salida de hello del paso anterior hello:</span><span class="sxs-lookup"><span data-stu-id="84418-119">SSH toohello VM using your own username and hello `publicIpAddress` listed in hello output from hello previous step:</span></span>

```bash
ssh azureuser@<publicIpAddress>
```

<span data-ttu-id="84418-120">crear orígenes de la instalación tooadd Hola para MongoDB, un **yum** archivo repositorio como sigue:</span><span class="sxs-lookup"><span data-stu-id="84418-120">tooadd hello installation sources for MongoDB, create a **yum** repository file as follows:</span></span>

```bash
sudo touch /etc/yum.repos.d/mongodb-org-3.4.repo
```

<span data-ttu-id="84418-121">Abrir archivo de repositorio de MongoDB Hola para editarlo.</span><span class="sxs-lookup"><span data-stu-id="84418-121">Open hello MongoDB repo file for editing.</span></span> <span data-ttu-id="84418-122">Agregue Hola siguientes líneas:</span><span class="sxs-lookup"><span data-stu-id="84418-122">Add hello following lines:</span></span>

```sh
[mongodb-org-3.4]
name=MongoDB Repository
baseurl=https://repo.mongodb.org/yum/redhat/$releasever/mongodb-org/3.4/x86_64/
gpgcheck=1
enabled=1
gpgkey=https://www.mongodb.org/static/pgp/server-3.4.asc
```

<span data-ttu-id="84418-123">Instale MongoDB mediante **yum** como se indica a continuación:</span><span class="sxs-lookup"><span data-stu-id="84418-123">Install MongoDB using **yum** as follows:</span></span>

```bash
sudo yum install -y mongodb-org
```

<span data-ttu-id="84418-124">De forma predeterminada, SELinux está aplicado en las imágenes de CentOS, lo que impide el acceso de MongoDB.</span><span class="sxs-lookup"><span data-stu-id="84418-124">By default, SELinux is enforced on CentOS images that prevents you from accessing MongoDB.</span></span> <span data-ttu-id="84418-125">Instalar herramientas de administración de directivas y configure SELinux tooallow MongoDB toooperate en su 27017 el puerto TCP predeterminado de la siguiente manera:</span><span class="sxs-lookup"><span data-stu-id="84418-125">Install policy management tools and configure SELinux tooallow MongoDB toooperate on its default TCP port 27017 as follows:</span></span>

```bash
sudo yum install -y policycoreutils-python
sudo semanage port -a -t mongod_port_t -p tcp 27017
```

<span data-ttu-id="84418-126">Iniciar servicio de MongoDB hello como sigue:</span><span class="sxs-lookup"><span data-stu-id="84418-126">Start hello MongoDB service as follows:</span></span>

```bash
sudo service mongod start
```

<span data-ttu-id="84418-127">Comprobar la instalación de MongoDB Hola al conectar con hello local `mongo` cliente:</span><span class="sxs-lookup"><span data-stu-id="84418-127">Verify hello MongoDB installation by connecting using hello local `mongo` client:</span></span>

```bash
mongo
```

<span data-ttu-id="84418-128">Ahora puede probar instancia de MongoDB Hola agregando algunos datos y, a continuación, buscar:</span><span class="sxs-lookup"><span data-stu-id="84418-128">Now test hello MongoDB instance by adding some data and then searching:</span></span>

```sh
> db
test
> db.foo.insert( { a : 1 } )  
> db.foo.find()  
{ "_id" : ObjectId("57ec477cd639891710b90727"), "a" : 1 }
> exit
```

<span data-ttu-id="84418-129">Si lo desea, configure MongoDB toostart automáticamente durante un reinicio del sistema:</span><span class="sxs-lookup"><span data-stu-id="84418-129">If desired, configure MongoDB toostart automatically during a system reboot:</span></span>

```bash
sudo chkconfig mongod on
```


## <a name="create-basic-mongodb-instance-on-centos-using-a-template"></a><span data-ttu-id="84418-130">Creación de una instancia básica de MongoDB en CentOS mediante una plantilla</span><span class="sxs-lookup"><span data-stu-id="84418-130">Create basic MongoDB instance on CentOS using a template</span></span>
<span data-ttu-id="84418-131">Puede crear una instancia de MongoDB básica en una sola máquina virtual CentOS mediante Hola siguientes plantilla de inicio rápido de Azure de GitHub.</span><span class="sxs-lookup"><span data-stu-id="84418-131">You can create a basic MongoDB instance on a single CentOS VM using hello following Azure quickstart template from GitHub.</span></span> <span data-ttu-id="84418-132">Esta plantilla utiliza la extensión de Script personalizado de Hola para Linux tooadd una **yum** tooyour repositorio recién creado la máquina virtual CentOS y, a continuación, instalar MongoDB.</span><span class="sxs-lookup"><span data-stu-id="84418-132">This template uses hello Custom Script extension for Linux tooadd a **yum** repository tooyour newly created CentOS VM and then install MongoDB.</span></span>

* <span data-ttu-id="84418-133">[Instancia básica de MongoDB en CentOS](https://github.com/Azure/azure-quickstart-templates/tree/master/mongodb-on-centos): https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/mongodb-on-centos/azuredeploy.json</span><span class="sxs-lookup"><span data-stu-id="84418-133">[Basic MongoDB instance on CentOS](https://github.com/Azure/azure-quickstart-templates/tree/master/mongodb-on-centos) - https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/mongodb-on-centos/azuredeploy.json</span></span>

<span data-ttu-id="84418-134">toocreate este entorno, deberá hello más reciente [CLI de Azure 2.0](/cli/azure/install-az-cli2) instalado y registrado en tooan cuenta de Azure mediante [inicio de sesión de az](/cli/azure/#login).</span><span class="sxs-lookup"><span data-stu-id="84418-134">toocreate this environment, you need hello latest [Azure CLI 2.0](/cli/azure/install-az-cli2) installed and logged in tooan Azure account using [az login](/cli/azure/#login).</span></span> <span data-ttu-id="84418-135">En primer lugar, cree un grupo de recursos con [az group create](/cli/azure/group#create).</span><span class="sxs-lookup"><span data-stu-id="84418-135">First, create a resource group with [az group create](/cli/azure/group#create).</span></span> <span data-ttu-id="84418-136">Hello en el ejemplo siguiente se crea un grupo de recursos denominado *myResourceGroup* en hello *eastus* ubicación:</span><span class="sxs-lookup"><span data-stu-id="84418-136">hello following example creates a resource group named *myResourceGroup* in hello *eastus* location:</span></span>

```azurecli
az group create --name myResourceGroup --location eastus
```

<span data-ttu-id="84418-137">A continuación, implementar la plantilla de MongoDB Hola con [Crear implementación de grupo az](/cli/azure/group/deployment#create).</span><span class="sxs-lookup"><span data-stu-id="84418-137">Next, deploy hello MongoDB template with [az group deployment create](/cli/azure/group/deployment#create).</span></span> <span data-ttu-id="84418-138">Defina sus propios nombres y tamaños de recursos donde sea necesario; por ejemplo, para *newStorageAccountName*, *virtualNetworkName* y *vmSize*:</span><span class="sxs-lookup"><span data-stu-id="84418-138">Define your own resource names and sizes where needed such as for *newStorageAccountName*, *virtualNetworkName*, and *vmSize*:</span></span>

```azurecli
az group deployment create --resource-group myResourceGroup \
  --parameters '{"newStorageAccountName": {"value": "mystorageaccount"},
    "adminUsername": {"value": "azureuser"},
    "adminPassword": {"value": "P@ssw0rd!"},
    "dnsNameForPublicIP": {"value": "mypublicdns"},
    "virtualNetworkName": {"value": "myVnet"},
    "vmSize": {"value": "Standard_DS2_v2"},
    "vmName": {"value": "myVM"},
    "publicIPAddressName": {"value": "myPublicIP"},
    "nicName": {"value": "myNic"}}' \
  --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/mongodb-on-centos/azuredeploy.json
```

<span data-ttu-id="84418-139">Inicie sesión en toohello VM utilizando Hola dirección pública de DNS de la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="84418-139">Log on toohello VM using hello public DNS address of your VM.</span></span> <span data-ttu-id="84418-140">Puede ver la dirección DNS pública Hola con [mostrar de la máquina virtual de az](/cli/azure/vm#show):</span><span class="sxs-lookup"><span data-stu-id="84418-140">You can view hello public DNS address with [az vm show](/cli/azure/vm#show):</span></span>

```azurecli
az vm show -g myResourceGroup -n myVM -d --query [fqdns] -o tsv
```

<span data-ttu-id="84418-141">SSH tooyour VM con su propio nombre de usuario y la dirección DNS pública:</span><span class="sxs-lookup"><span data-stu-id="84418-141">SSH tooyour VM using your own username and public DNS address:</span></span>

```bash
ssh azureuser@mypublicdns.eastus.cloudapp.azure.com
```

<span data-ttu-id="84418-142">Comprobar la instalación de MongoDB Hola al conectar con hello local `mongo` cliente como sigue:</span><span class="sxs-lookup"><span data-stu-id="84418-142">Verify hello MongoDB installation by connecting using hello local `mongo` client as follows:</span></span>

```bash
mongo
```

<span data-ttu-id="84418-143">Ahora puede probar instancia Hola agregando algunos datos y buscar los siguientes:</span><span class="sxs-lookup"><span data-stu-id="84418-143">Now test hello instance by adding some data and searching as follows:</span></span>

```sh
> db
test
> db.foo.insert( { a : 1 } )  
> db.foo.find()  
{ "_id" : ObjectId("57ec477cd639891710b90727"), "a" : 1 }
> exit
```


## <a name="create-a-complex-mongodb-sharded-cluster-on-centos-using-a-template"></a><span data-ttu-id="84418-144">Creación de un clúster complejo con particiones de MongoDB en CentOS mediante una plantilla</span><span class="sxs-lookup"><span data-stu-id="84418-144">Create a complex MongoDB Sharded Cluster on CentOS using a template</span></span>
<span data-ttu-id="84418-145">Se puede crear un clúster particionado de MongoDB complejo con hello siguientes plantilla de inicio rápido de Azure de GitHub.</span><span class="sxs-lookup"><span data-stu-id="84418-145">You can create a complex MongoDB sharded cluster using hello following Azure quickstart template from GitHub.</span></span> <span data-ttu-id="84418-146">Esta plantilla sigue hello [prácticas recomendadas de MongoDB clúster particionada](https://docs.mongodb.com/manual/core/sharded-cluster-components/) tooprovide redundancia y alta disponibilidad.</span><span class="sxs-lookup"><span data-stu-id="84418-146">This template follows hello [MongoDB sharded cluster best practices](https://docs.mongodb.com/manual/core/sharded-cluster-components/) tooprovide redundancy and high availability.</span></span> <span data-ttu-id="84418-147">plantilla de Hello crea dos particiones, con tres nodos en cada conjunto de réplicas.</span><span class="sxs-lookup"><span data-stu-id="84418-147">hello template creates two shards, with three nodes in each replica set.</span></span> <span data-ttu-id="84418-148">También se crean un conjunto con tres nodos de réplicas de servidor de configuración, más dos **mongos** enrutador servidores tooprovide coherencia tooapplications de entre las particiones de Hola.</span><span class="sxs-lookup"><span data-stu-id="84418-148">One config server replica set with three nodes is also created, plus two **mongos** router servers tooprovide consistency tooapplications from across hello shards.</span></span>

* <span data-ttu-id="84418-149">[Clúster con particiones de MongoDB en CentOS](https://github.com/Azure/azure-quickstart-templates/tree/master/mongodb-sharding-centos): https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/mongodb-sharding-centos/azuredeploy.json</span><span class="sxs-lookup"><span data-stu-id="84418-149">[MongoDB Sharding Cluster on CentOS](https://github.com/Azure/azure-quickstart-templates/tree/master/mongodb-sharding-centos) - https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/mongodb-sharding-centos/azuredeploy.json</span></span>

> [!WARNING]
> <span data-ttu-id="84418-150">Implementación de este clúster de MongoDB particionada complejo requiere más de 20 núcleos, que normalmente es el recuento de núcleos de hello predeterminado por región para una suscripción.</span><span class="sxs-lookup"><span data-stu-id="84418-150">Deploying this complex MongoDB sharded cluster requires more than 20 cores, which is typically hello default core count per region for a subscription.</span></span> <span data-ttu-id="84418-151">Abra su recuento de núcleos de un tooincrease de solicitud de soporte técnico de Azure.</span><span class="sxs-lookup"><span data-stu-id="84418-151">Open an Azure support request tooincrease your core count.</span></span>

<span data-ttu-id="84418-152">toocreate este entorno, deberá hello más reciente [CLI de Azure 2.0](/cli/azure/install-az-cli2) instalado y registrado en tooan cuenta de Azure mediante [inicio de sesión de az](/cli/azure/#login).</span><span class="sxs-lookup"><span data-stu-id="84418-152">toocreate this environment, you need hello latest [Azure CLI 2.0](/cli/azure/install-az-cli2) installed and logged in tooan Azure account using [az login](/cli/azure/#login).</span></span> <span data-ttu-id="84418-153">En primer lugar, cree un grupo de recursos con [az group create](/cli/azure/group#create).</span><span class="sxs-lookup"><span data-stu-id="84418-153">First, create a resource group with [az group create](/cli/azure/group#create).</span></span> <span data-ttu-id="84418-154">Hello en el ejemplo siguiente se crea un grupo de recursos denominado *myResourceGroup* en hello *eastus* ubicación:</span><span class="sxs-lookup"><span data-stu-id="84418-154">hello following example creates a resource group named *myResourceGroup* in hello *eastus* location:</span></span>

```azurecli
az group create --name myResourceGroup --location eastus
```

<span data-ttu-id="84418-155">A continuación, implementar la plantilla de MongoDB Hola con [Crear implementación de grupo az](/cli/azure/group/deployment#create).</span><span class="sxs-lookup"><span data-stu-id="84418-155">Next, deploy hello MongoDB template with [az group deployment create](/cli/azure/group/deployment#create).</span></span> <span data-ttu-id="84418-156">Defina sus propios nombres de recursos y tamaños donde sea necesario; por ejemplo, para *mongoAdminUsername*, *sizeOfDataDiskInGB* y *configNodeVmSize*:</span><span class="sxs-lookup"><span data-stu-id="84418-156">Define your own resource names and sizes where needed such as for *mongoAdminUsername*, *sizeOfDataDiskInGB*, and *configNodeVmSize*:</span></span>

```azurecli
az group deployment create --resource-group myResourceGroup \
  --parameters '{"adminUsername": {"value": "azureuser"},
    "adminPassword": {"value": "P@ssw0rd!"},
    "mongoAdminUsername": {"value": "mongoadmin"},
    "mongoAdminPassword": {"value": "P@ssw0rd!"},
    "dnsNamePrefix": {"value": "mypublicdns"},
    "environment": {"value": "AzureCloud"},
    "numDataDisks": {"value": "4"},
    "sizeOfDataDiskInGB": {"value": 20},
    "centOsVersion": {"value": "7.0"},
    "routerNodeVmSize": {"value": "Standard_DS3_v2"},
    "configNodeVmSize": {"value": "Standard_DS3_v2"},
    "replicaNodeVmSize": {"value": "Standard_DS3_v2"},
    "zabbixServerIPAddress": {"value": "Null"}}' \
  --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/mongodb-sharding-centos/azuredeploy.json \
  --name myMongoDBCluster \
  --no-wait
```

<span data-ttu-id="84418-157">Esta implementación puede asumir un toodeploy de hora y configurar todas las instancias de máquina virtual de Hola.</span><span class="sxs-lookup"><span data-stu-id="84418-157">This deployment can take over an hour toodeploy and configure all hello VM instances.</span></span> <span data-ttu-id="84418-158">Hola `--no-wait` marca se utiliza al final de Hola de hello anterior símbolo de comando de tooreturn control toohello una vez que la implementación de la plantilla de hello haya sido aceptado por hello plataforma Windows Azure.</span><span class="sxs-lookup"><span data-stu-id="84418-158">hello `--no-wait` flag is used at hello end of hello preceding command tooreturn control toohello command prompt once hello template deployment has been accepted by hello Azure platform.</span></span> <span data-ttu-id="84418-159">A continuación, puede ver el estado de implementación de hello con [muestra de implementación de grupo az](/cli/azure/group/deployment#show).</span><span class="sxs-lookup"><span data-stu-id="84418-159">You can then view hello deployment status with [az group deployment show](/cli/azure/group/deployment#show).</span></span> <span data-ttu-id="84418-160">vistas de ejemplo siguientes Hola Hola estado de hello *myMongoDBCluster* implementación Hola *myResourceGroup* grupo de recursos:</span><span class="sxs-lookup"><span data-stu-id="84418-160">hello following example views hello status for hello *myMongoDBCluster* deployment in hello *myResourceGroup* resource group:</span></span>

```azurecli
az group deployment show \
    --resource-group myResourceGroup \
    --name myMongoDBCluster \
    --query [properties.provisioningState] \
    --output tsv
```

## <a name="next-steps"></a><span data-ttu-id="84418-161">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="84418-161">Next steps</span></span>
<span data-ttu-id="84418-162">En estos ejemplos, puede conectar toohello MongoDB instancia localmente desde Hola máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="84418-162">In these examples, you connect toohello MongoDB instance locally from hello VM.</span></span> <span data-ttu-id="84418-163">Si desea tooconnect toohello MongoDB instancia desde otra máquina virtual o una red, asegúrese de hello adecuado [se crean las reglas del grupo de seguridad de red](nsg-quickstart.md).</span><span class="sxs-lookup"><span data-stu-id="84418-163">If you want tooconnect toohello MongoDB instance from another VM or network, ensure hello appropriate [Network Security Group rules are created](nsg-quickstart.md).</span></span>

<span data-ttu-id="84418-164">Estos ejemplos implementación el entorno de MongoDB de núcleo de Hola para fines de desarrollo.</span><span class="sxs-lookup"><span data-stu-id="84418-164">These examples deploy hello core MongoDB environment for development purposes.</span></span> <span data-ttu-id="84418-165">Aplicar opciones de configuración de seguridad de hello necesario para su entorno.</span><span class="sxs-lookup"><span data-stu-id="84418-165">Apply hello required security configuration options for your environment.</span></span> <span data-ttu-id="84418-166">Para obtener más información, vea hello [documentos de seguridad de MongoDB](https://docs.mongodb.com/manual/security/).</span><span class="sxs-lookup"><span data-stu-id="84418-166">For more information, see hello [MongoDB security docs](https://docs.mongodb.com/manual/security/).</span></span>

<span data-ttu-id="84418-167">Para obtener más información acerca de cómo crear mediante plantillas, vea hello [Introducción a Azure Resource Manager](../../azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="84418-167">For more information about creating using templates, see hello [Azure Resource Manager overview](../../azure-resource-manager/resource-group-overview.md).</span></span>

<span data-ttu-id="84418-168">plantillas de Azure Resource Manager Hola usar toodownload de extensión de Script personalizado de Hola y ejecutan scripts en las máquinas virtuales.</span><span class="sxs-lookup"><span data-stu-id="84418-168">hello Azure Resource Manager templates use hello Custom Script Extension toodownload and execute scripts on your VMs.</span></span> <span data-ttu-id="84418-169">Para obtener más información, consulte [hello mediante extensión de Script personalizado de Azure con las máquinas virtuales Linux](extensions-customscript.md).</span><span class="sxs-lookup"><span data-stu-id="84418-169">For more information, see [Using hello Azure Custom Script Extension with Linux Virtual Machines](extensions-customscript.md).</span></span>

