---
title: aaaInstall MongoDB en una VM de Linux con Hola 1.0 de CLI de Azure | Documentos de Microsoft
description: "Obtenga información acerca de cómo tooinstall y configurar MongoDB en una máquina virtual de Linux en Azure con el modelo de implementación del Administrador de recursos de Hola."
services: virtual-machines-linux
documentationcenter: 
author: iainfoulds
manager: timlt
editor: 
ms.assetid: 3f55b546-86df-4442-9ef4-8a25fae7b96e
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 05/11/2017
ms.author: iainfou
ms.openlocfilehash: 4ce21a2c63da7d00a4422e0a6766e2103e7f12d7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooinstall-and-configure-mongodb-on-a-linux-vm-using-hello-azure-cli-10"></a><span data-ttu-id="76513-103">¿Cómo tooinstall y configurar MongoDB en una VM de Linux con hello Azure CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="76513-103">How tooinstall and configure MongoDB on a Linux VM using hello Azure CLI 1.0</span></span>
<span data-ttu-id="76513-104">[MongoDB](http://www.mongodb.org) es una conocida base de datos NoSQL de código abierto y alto rendimiento.</span><span class="sxs-lookup"><span data-stu-id="76513-104">[MongoDB](http://www.mongodb.org) is a popular open-source, high-performance NoSQL database.</span></span> <span data-ttu-id="76513-105">Este artículo muestra cómo tooinstall y configurar MongoDB en una VM de Linux en Azure con el modelo de implementación del Administrador de recursos de Hola.</span><span class="sxs-lookup"><span data-stu-id="76513-105">This article shows you how tooinstall and configure MongoDB on a Linux VM in Azure using hello Resource Manager deployment model.</span></span> <span data-ttu-id="76513-106">Se muestran algunos ejemplos detallados de:</span><span class="sxs-lookup"><span data-stu-id="76513-106">Examples are shown that detail how to:</span></span>

* [<span data-ttu-id="76513-107">Instalación y configuración manuales de una instancia básica de MongoDB</span><span class="sxs-lookup"><span data-stu-id="76513-107">Manually install and configure a basic MongoDB instance</span></span>](#manually-install-and-configure-mongodb-on-a-vm)
* [<span data-ttu-id="76513-108">Creación de una instancia básica de MongoDB mediante una plantilla de Resource Manager</span><span class="sxs-lookup"><span data-stu-id="76513-108">Create a basic MongoDB instance using a Resource Manager template</span></span>](#create-basic-mongodb-instance-on-centos-using-a-template)
* [<span data-ttu-id="76513-109">Creación de un clúster complejo con particiones de MongoDB con conjuntos de réplicas mediante una plantilla de Resource Manager</span><span class="sxs-lookup"><span data-stu-id="76513-109">Create a complex MongoDB sharded cluster with replica sets using a Resource Manager template</span></span>](#create-a-complex-mongodb-sharded-cluster-on-centos-using-a-template)


## <a name="cli-versions-toocomplete-hello-task"></a><span data-ttu-id="76513-110">Tarea CLI versiones toocomplete hello</span><span class="sxs-lookup"><span data-stu-id="76513-110">CLI versions toocomplete hello task</span></span>
<span data-ttu-id="76513-111">Puede completar la tarea hello mediante uno de hello después de las versiones CLI:</span><span class="sxs-lookup"><span data-stu-id="76513-111">You can complete hello task using one of hello following CLI versions:</span></span>

- <span data-ttu-id="76513-112">CLI de Azure 1.0 – nuestro CLI para hello clásico y recursos administración modelos de implementación (en este artículo)</span><span class="sxs-lookup"><span data-stu-id="76513-112">Azure CLI 1.0 – our CLI for hello classic and resource management deployment models (this article)</span></span>
- <span data-ttu-id="76513-113">[Azure 2.0 CLI](create-cli-complete-nodejs.md) -nuestro CLI de próxima generación para el modelo de implementación de administración de recursos de Hola</span><span class="sxs-lookup"><span data-stu-id="76513-113">[Azure CLI 2.0](create-cli-complete-nodejs.md) - our next generation CLI for hello resource management deployment model</span></span>


## <a name="manually-install-and-configure-mongodb-on-a-vm"></a><span data-ttu-id="76513-114">Instalación y configuración manuales de MongoDB en una máquina virtual</span><span class="sxs-lookup"><span data-stu-id="76513-114">Manually install and configure MongoDB on a VM</span></span>
<span data-ttu-id="76513-115">MongoDB [proporciona instrucciones de instalación](https://docs.mongodb.com/manual/administration/install-on-linux/) para distribuciones de Linux, incluidos Red Hat/CentOS, SUSE, Ubuntu y Debian.</span><span class="sxs-lookup"><span data-stu-id="76513-115">MongoDB [provide installation instructions](https://docs.mongodb.com/manual/administration/install-on-linux/) for Linux distros including Red Hat / CentOS, SUSE, Ubuntu, and Debian.</span></span> <span data-ttu-id="76513-116">Hello ejemplo siguiente se crea un *CentOS* máquina virtual con una clave SSH almacenada en *~/.ssh/id_rsa.pub*.</span><span class="sxs-lookup"><span data-stu-id="76513-116">hello following example creates a *CentOS* VM using an SSH key stored at *~/.ssh/id_rsa.pub*.</span></span> <span data-ttu-id="76513-117">Hola de respuesta solicita nombre de la cuenta de almacenamiento, nombre DNS y credenciales de administrador:</span><span class="sxs-lookup"><span data-stu-id="76513-117">Answer hello prompts for storage account name, DNS name, and admin credentials:</span></span>

```azurecli
azure vm quick-create \
    --image-urn CentOS \
    --ssh-publickey-file ~/.ssh/id_rsa.pub 
```

<span data-ttu-id="76513-118">Inicie sesión en toohello VM mediante la dirección IP pública Hola que se muestra al final de Hola de hello anterior paso de creación de la máquina virtual:</span><span class="sxs-lookup"><span data-stu-id="76513-118">Log on toohello VM using hello public IP address displayed at hello end of hello preceding VM creation step:</span></span>

```bash
ssh azureuser@40.78.23.145
```

<span data-ttu-id="76513-119">crear orígenes de la instalación tooadd Hola para MongoDB, un **yum** archivo repositorio como sigue:</span><span class="sxs-lookup"><span data-stu-id="76513-119">tooadd hello installation sources for MongoDB, create a **yum** repository file as follows:</span></span>

```bash
sudo touch /etc/yum.repos.d/mongodb-org-3.4.repo
```

<span data-ttu-id="76513-120">Abrir archivo de repositorio de MongoDB Hola para editarlo.</span><span class="sxs-lookup"><span data-stu-id="76513-120">Open hello MongoDB repo file for editing.</span></span> <span data-ttu-id="76513-121">Agregue Hola siguientes líneas:</span><span class="sxs-lookup"><span data-stu-id="76513-121">Add hello following lines:</span></span>

```sh
[mongodb-org-3.4]
name=MongoDB Repository
baseurl=https://repo.mongodb.org/yum/redhat/$releasever/mongodb-org/3.4/x86_64/
gpgcheck=1
enabled=1
gpgkey=https://www.mongodb.org/static/pgp/server-3.4.asc
```

<span data-ttu-id="76513-122">Instale MongoDB mediante **yum** como se indica a continuación:</span><span class="sxs-lookup"><span data-stu-id="76513-122">Install MongoDB using **yum** as follows:</span></span>

```bash
sudo yum install -y mongodb-org
```

<span data-ttu-id="76513-123">De forma predeterminada, SELinux está aplicado en las imágenes de CentOS, lo que impide el acceso de MongoDB.</span><span class="sxs-lookup"><span data-stu-id="76513-123">By default, SELinux is enforced on CentOS images that prevents you from accessing MongoDB.</span></span> <span data-ttu-id="76513-124">Instalar herramientas de administración de directivas y configure SELinux tooallow MongoDB toooperate en su puerto TCP 27017 como se indica a continuación.</span><span class="sxs-lookup"><span data-stu-id="76513-124">Install policy management tools and configure SELinux tooallow MongoDB toooperate on its default TCP port 27017 as follows.</span></span> 

```bash
sudo yum install -y policycoreutils-python
sudo semanage port -a -t mongod_port_t -p tcp 27017
```

<span data-ttu-id="76513-125">Iniciar servicio de MongoDB hello como sigue:</span><span class="sxs-lookup"><span data-stu-id="76513-125">Start hello MongoDB service as follows:</span></span>

```bash
sudo service mongod start
```

<span data-ttu-id="76513-126">Comprobar la instalación de MongoDB Hola al conectar con hello local `mongo` cliente:</span><span class="sxs-lookup"><span data-stu-id="76513-126">Verify hello MongoDB installation by connecting using hello local `mongo` client:</span></span>

```bash
mongo
```

<span data-ttu-id="76513-127">Ahora puede probar instancia de MongoDB Hola agregando algunos datos y, a continuación, buscar:</span><span class="sxs-lookup"><span data-stu-id="76513-127">Now test hello MongoDB instance by adding some data and then searching:</span></span>

```sh
> db
test
> db.foo.insert( { a : 1 } )  
> db.foo.find()  
{ "_id" : ObjectId("57ec477cd639891710b90727"), "a" : 1 }
> exit
```

<span data-ttu-id="76513-128">Si lo desea, configure MongoDB toostart automáticamente durante un reinicio del sistema:</span><span class="sxs-lookup"><span data-stu-id="76513-128">If desired, configure MongoDB toostart automatically during a system reboot:</span></span>

```bash
sudo chkconfig mongod on
```


## <a name="create-basic-mongodb-instance-on-centos-using-a-template"></a><span data-ttu-id="76513-129">Creación de una instancia básica de MongoDB en CentOS mediante una plantilla</span><span class="sxs-lookup"><span data-stu-id="76513-129">Create basic MongoDB instance on CentOS using a template</span></span>
<span data-ttu-id="76513-130">Puede crear una instancia de MongoDB básica en una sola máquina virtual CentOS mediante Hola siguientes plantilla de inicio rápido de Azure de GitHub.</span><span class="sxs-lookup"><span data-stu-id="76513-130">You can create a basic MongoDB instance on a single CentOS VM using hello following Azure quickstart template from GitHub.</span></span> <span data-ttu-id="76513-131">Esta plantilla utiliza la extensión de Script personalizado de Hola para Linux tooadd una `yum` tooyour repositorio recién creado la máquina virtual CentOS y, a continuación, instalar MongoDB.</span><span class="sxs-lookup"><span data-stu-id="76513-131">This template uses hello Custom Script extension for Linux tooadd a `yum` repository tooyour newly created CentOS VM and then install MongoDB.</span></span>

* <span data-ttu-id="76513-132">[Instancia básica de MongoDB en CentOS](https://github.com/Azure/azure-quickstart-templates/tree/master/mongodb-on-centos): https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/mongodb-on-centos/azuredeploy.json</span><span class="sxs-lookup"><span data-stu-id="76513-132">[Basic MongoDB instance on CentOS](https://github.com/Azure/azure-quickstart-templates/tree/master/mongodb-on-centos) - https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/mongodb-on-centos/azuredeploy.json</span></span>

<span data-ttu-id="76513-133">Hello en el ejemplo siguiente se crea un grupo de recursos con nombre hello `myResourceGroup` en hello `eastus` región.</span><span class="sxs-lookup"><span data-stu-id="76513-133">hello following example creates a resource group with hello name `myResourceGroup` in hello `eastus` region.</span></span> <span data-ttu-id="76513-134">Escriba sus propios valores, como se indica a continuación:</span><span class="sxs-lookup"><span data-stu-id="76513-134">Enter your own values as follows:</span></span>

```azurecli
azure group create \
    --name myResourceGroup \
    --location eastus \
    --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/mongodb-on-centos/azuredeploy.json
```

> [!NOTE]
> <span data-ttu-id="76513-135">Hola CLI de Azure devuelve tooa símbolo del sistema en cuestión de segundos de creación de la implementación de hello, pero cuya instalación hello y configuración toma toocomplete unos minutos.</span><span class="sxs-lookup"><span data-stu-id="76513-135">hello Azure CLI returns you tooa prompt within a few seconds of creating hello deployment, but hello installation and configuration takes a few minutes toocomplete.</span></span> <span data-ttu-id="76513-136">Comprobar el estado de Hola de implementación de hello con `azure group deployment show myResourceGroup`, escribir el nombre de Hola de su grupo de recursos según corresponda.</span><span class="sxs-lookup"><span data-stu-id="76513-136">Check hello status of hello deployment with `azure group deployment show myResourceGroup`, entering hello name of your resource group accordingly.</span></span> <span data-ttu-id="76513-137">Espere hasta que hello **ProvisioningState** muestra *correcto* antes de tratar de tooSSH toohello máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="76513-137">Wait until hello **ProvisioningState** shows *Succeeded* before trying tooSSH toohello VM.</span></span>

<span data-ttu-id="76513-138">Una vez finalizada la implementación de hello completa, SSH toohello máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="76513-138">Once hello deployment is complete, SSH toohello VM.</span></span> <span data-ttu-id="76513-139">Obtener dirección IP de saludo de la máquina virtual con hello `azure vm show` comando como en el siguiente ejemplo de Hola:</span><span class="sxs-lookup"><span data-stu-id="76513-139">Obtain hello IP address of your VM using hello `azure vm show` command as in hello following example:</span></span>

```azurecli
azure vm show --resource-group myResourceGroup --name myLinuxVM
```

<span data-ttu-id="76513-140">Casi final Hola de salida de hello, se muestra la dirección IP pública Hola.</span><span class="sxs-lookup"><span data-stu-id="76513-140">Near hello end of hello output, hello public IP address is displayed.</span></span> <span data-ttu-id="76513-141">SSH tooyour máquina virtual con la dirección IP de saludo de la máquina virtual:</span><span class="sxs-lookup"><span data-stu-id="76513-141">SSH tooyour VM with hello IP address of your VM:</span></span>

```bash
ssh azureuser@138.91.149.74
```

<span data-ttu-id="76513-142">Comprobar la instalación de MongoDB Hola al conectar con hello local `mongo` cliente como sigue:</span><span class="sxs-lookup"><span data-stu-id="76513-142">Verify hello MongoDB installation by connecting using hello local `mongo` client as follows:</span></span>

```bash
mongo
```

<span data-ttu-id="76513-143">Ahora puede probar instancia Hola agregando algunos datos y buscar los siguientes:</span><span class="sxs-lookup"><span data-stu-id="76513-143">Now test hello instance by adding some data and searching as follows:</span></span>

```sh
> db
test
> db.foo.insert( { a : 1 } )  
> db.foo.find()  
{ "_id" : ObjectId("57ec477cd639891710b90727"), "a" : 1 }
> exit
```


## <a name="create-a-complex-mongodb-sharded-cluster-on-centos-using-a-template"></a><span data-ttu-id="76513-144">Creación de un clúster complejo con particiones de MongoDB en CentOS mediante una plantilla</span><span class="sxs-lookup"><span data-stu-id="76513-144">Create a complex MongoDB Sharded Cluster on CentOS using a template</span></span>
<span data-ttu-id="76513-145">Se puede crear un clúster particionado de MongoDB complejo con hello siguientes plantilla de inicio rápido de Azure de GitHub.</span><span class="sxs-lookup"><span data-stu-id="76513-145">You can create a complex MongoDB sharded cluster using hello following Azure quickstart template from GitHub.</span></span> <span data-ttu-id="76513-146">Esta plantilla sigue hello [prácticas recomendadas de MongoDB clúster particionada](https://docs.mongodb.com/manual/core/sharded-cluster-components/) tooprovide redundancia y alta disponibilidad.</span><span class="sxs-lookup"><span data-stu-id="76513-146">This template follows hello [MongoDB sharded cluster best practices](https://docs.mongodb.com/manual/core/sharded-cluster-components/) tooprovide redundancy and high availability.</span></span> <span data-ttu-id="76513-147">plantilla de Hello crea dos particiones, con tres nodos en cada conjunto de réplicas.</span><span class="sxs-lookup"><span data-stu-id="76513-147">hello template creates two shards, with three nodes in each replica set.</span></span> <span data-ttu-id="76513-148">También se crean un conjunto con tres nodos de réplicas de servidor de configuración, más dos **mongos** enrutador servidores tooprovide coherencia tooapplications de entre las particiones de Hola.</span><span class="sxs-lookup"><span data-stu-id="76513-148">One config server replica set with three nodes is also created, plus two **mongos** router servers tooprovide consistency tooapplications from across hello shards.</span></span>

* <span data-ttu-id="76513-149">[Clúster con particiones de MongoDB en CentOS](https://github.com/Azure/azure-quickstart-templates/tree/master/mongodb-sharding-centos): https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/mongodb-sharding-centos/azuredeploy.json</span><span class="sxs-lookup"><span data-stu-id="76513-149">[MongoDB Sharding Cluster on CentOS](https://github.com/Azure/azure-quickstart-templates/tree/master/mongodb-sharding-centos) - https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/mongodb-sharding-centos/azuredeploy.json</span></span>

> [!WARNING]
> <span data-ttu-id="76513-150">Implementación de este clúster de MongoDB particionada complejo requiere más de 20 núcleos, que normalmente es el recuento de núcleos de hello predeterminado por región para una suscripción.</span><span class="sxs-lookup"><span data-stu-id="76513-150">Deploying this complex MongoDB sharded cluster requires more than 20 cores, which is typically hello default core count per region for a subscription.</span></span> <span data-ttu-id="76513-151">Abra su recuento de núcleos de un tooincrease de solicitud de soporte técnico de Azure.</span><span class="sxs-lookup"><span data-stu-id="76513-151">Open an Azure support request tooincrease your core count.</span></span>

<span data-ttu-id="76513-152">Hello en el ejemplo siguiente se crea un grupo de recursos con nombre hello *myResourceGroup* en hello *eastus* región.</span><span class="sxs-lookup"><span data-stu-id="76513-152">hello following example creates a resource group with hello name *myResourceGroup* in hello *eastus* region.</span></span> <span data-ttu-id="76513-153">Escriba sus propios valores, como se indica a continuación:</span><span class="sxs-lookup"><span data-stu-id="76513-153">Enter your own values as follows:</span></span>

```azurecli
azure group create \
    --name myResourceGroup \
    --location eastus \
    --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/mongodb-sharding-centos/azuredeploy.json
```

> [!NOTE]
> <span data-ttu-id="76513-154">Hola CLI de Azure devuelve tooa símbolo del sistema en cuestión de segundos de creación de la implementación de hello, pero hello instalación y configuración pueden tardar más de una hora toocomplete.</span><span class="sxs-lookup"><span data-stu-id="76513-154">hello Azure CLI returns you tooa prompt within a few seconds of creating hello deployment, but hello installation and configuration can take over an hour toocomplete.</span></span> <span data-ttu-id="76513-155">Comprobar el estado de Hola de implementación de hello con `azure group deployment show myResourceGroup`, ajustar el nombre de Hola de su grupo de recursos según corresponda.</span><span class="sxs-lookup"><span data-stu-id="76513-155">Check hello status of hello deployment with `azure group deployment show myResourceGroup`, adjusting hello name of your resource group accordingly.</span></span> <span data-ttu-id="76513-156">Espere hasta que hello **ProvisioningState** muestra *correcto* antes de conectar máquinas virtuales toohello.</span><span class="sxs-lookup"><span data-stu-id="76513-156">Wait until hello **ProvisioningState** shows *Succeeded* before connecting toohello VMs.</span></span>


## <a name="next-steps"></a><span data-ttu-id="76513-157">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="76513-157">Next steps</span></span>
<span data-ttu-id="76513-158">En estos ejemplos, puede conectar toohello MongoDB instancia localmente desde Hola máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="76513-158">In these examples, you connect toohello MongoDB instance locally from hello VM.</span></span> <span data-ttu-id="76513-159">Si desea tooconnect toohello MongoDB instancia desde otra máquina virtual o una red, asegúrese de hello adecuado [se crean las reglas del grupo de seguridad de red](nsg-quickstart.md).</span><span class="sxs-lookup"><span data-stu-id="76513-159">If you want tooconnect toohello MongoDB instance from another VM or network, ensure hello appropriate [Network Security Group rules are created](nsg-quickstart.md).</span></span>

<span data-ttu-id="76513-160">Para obtener más información acerca de cómo crear mediante plantillas, vea hello [Introducción a Azure Resource Manager](../../azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="76513-160">For more information about creating using templates, see hello [Azure Resource Manager overview](../../azure-resource-manager/resource-group-overview.md).</span></span>

<span data-ttu-id="76513-161">plantillas de Azure Resource Manager Hola usar toodownload de extensión de Script personalizado de Hola y ejecutan scripts en las máquinas virtuales.</span><span class="sxs-lookup"><span data-stu-id="76513-161">hello Azure Resource Manager templates use hello Custom Script Extension toodownload and execute scripts on your VMs.</span></span> <span data-ttu-id="76513-162">Para obtener más información, consulte [hello mediante extensión de Script personalizado de Azure con las máquinas virtuales Linux](extensions-customscript.md).</span><span class="sxs-lookup"><span data-stu-id="76513-162">For more information, see [Using hello Azure Custom Script Extension with Linux Virtual Machines](extensions-customscript.md).</span></span>

