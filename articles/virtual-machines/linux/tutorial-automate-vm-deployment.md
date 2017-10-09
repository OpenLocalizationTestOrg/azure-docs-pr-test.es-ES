---
title: aaaCustomize una VM de Linux en el primer inicio en Azure | Documentos de Microsoft
description: "Obtenga información acerca de cómo toouse nube-init y Hola de máquinas virtuales de Linux de almacén de claves toocustomze primera vez que se inicien en Azure"
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
ms.date: 08/11/2017
ms.author: iainfou
ms.custom: mvc
ms.openlocfilehash: 280189723ac0205226f9c0068bd605da13249ace
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="how-toocustomize-a-linux-virtual-machine-on-first-boot"></a><span data-ttu-id="5070d-103">¿Cómo toocustomize una máquina virtual de Linux en el primer arranque</span><span class="sxs-lookup"><span data-stu-id="5070d-103">How toocustomize a Linux virtual machine on first boot</span></span>
<span data-ttu-id="5070d-104">En un tutorial anterior, se habrá aprendido cómo tooSSH tooa virtual machine (VM) e instalar manualmente NGINX.</span><span class="sxs-lookup"><span data-stu-id="5070d-104">In a previous tutorial, you learned how tooSSH tooa virtual machine (VM) and manually install NGINX.</span></span> <span data-ttu-id="5070d-105">Normalmente se desea toocreate máquinas virtuales de una manera rápida y coherente, alguna forma de automatización.</span><span class="sxs-lookup"><span data-stu-id="5070d-105">toocreate VMs in a quick and consistent manner, some form of automation is typically desired.</span></span> <span data-ttu-id="5070d-106">Un toocustomize enfoque común una máquina virtual en el primer inicio es toouse [init de la nube](https://cloudinit.readthedocs.io).</span><span class="sxs-lookup"><span data-stu-id="5070d-106">A common approach toocustomize a VM on first boot is toouse [cloud-init](https://cloudinit.readthedocs.io).</span></span> <span data-ttu-id="5070d-107">En este tutorial, aprenderá a:</span><span class="sxs-lookup"><span data-stu-id="5070d-107">In this tutorial you learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="5070d-108">Crear un archivo de configuración cloud-init</span><span class="sxs-lookup"><span data-stu-id="5070d-108">Create a cloud-init config file</span></span>
> * <span data-ttu-id="5070d-109">Crear una máquina virtual que usa un archivo cloud-init</span><span class="sxs-lookup"><span data-stu-id="5070d-109">Create a VM that uses a cloud-init file</span></span>
> * <span data-ttu-id="5070d-110">Ver una aplicación en ejecución Node.js después de hello que VM.</span><span class="sxs-lookup"><span data-stu-id="5070d-110">View a running Node.js app after hello VM is created</span></span>
> * <span data-ttu-id="5070d-111">Usar el almacén de claves toosecurely almacén de certificados</span><span class="sxs-lookup"><span data-stu-id="5070d-111">Use Key Vault toosecurely store certificates</span></span>
> * <span data-ttu-id="5070d-112">Automatizar implementaciones seguras de NGINX con cloud-init</span><span class="sxs-lookup"><span data-stu-id="5070d-112">Automate secure deployments of NGINX with cloud-init</span></span>


[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="5070d-113">Si elige tooinstall y usar hello CLI localmente, este tutorial requiere que se ejecuta la versión de CLI de Azure de hello 2.0.4 o versiones posteriores.</span><span class="sxs-lookup"><span data-stu-id="5070d-113">If you choose tooinstall and use hello CLI locally, this tutorial requires that you are running hello Azure CLI version 2.0.4 or later.</span></span> <span data-ttu-id="5070d-114">Ejecutar `az --version` toofind versión de Hola.</span><span class="sxs-lookup"><span data-stu-id="5070d-114">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="5070d-115">Si necesita tooinstall o una actualización, consulte [instalar Azure CLI 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="5070d-115">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span>  



## <a name="cloud-init-overview"></a><span data-ttu-id="5070d-116">Introducción a cloud-init</span><span class="sxs-lookup"><span data-stu-id="5070d-116">Cloud-init overview</span></span>
<span data-ttu-id="5070d-117">[En la nube init](https://cloudinit.readthedocs.io) es un enfoque ampliamente utilizado toocustomize una VM Linux tal y como se arranca para hello primera vez.</span><span class="sxs-lookup"><span data-stu-id="5070d-117">[Cloud-init](https://cloudinit.readthedocs.io) is a widely used approach toocustomize a Linux VM as it boots for hello first time.</span></span> <span data-ttu-id="5070d-118">Puede usar en la nube init tooinstall paquetes y escribir archivos, o los usuarios de tooconfigure y seguridad.</span><span class="sxs-lookup"><span data-stu-id="5070d-118">You can use cloud-init tooinstall packages and write files, or tooconfigure users and security.</span></span> <span data-ttu-id="5070d-119">Como init de la nube se ejecuta durante el proceso de arranque inicial de hello, no hay ningún paso adicional o requiere la configuración de agentes tooapply.</span><span class="sxs-lookup"><span data-stu-id="5070d-119">As cloud-init runs during hello initial boot process, there are no additional steps or required agents tooapply your configuration.</span></span>

<span data-ttu-id="5070d-120">cloud-init también funciona entre distribuciones.</span><span class="sxs-lookup"><span data-stu-id="5070d-120">Cloud-init also works across distributions.</span></span> <span data-ttu-id="5070d-121">Por ejemplo, no usar **install apt get** o **yum instalar** tooinstall un paquete.</span><span class="sxs-lookup"><span data-stu-id="5070d-121">For example, you don't use **apt-get install** or **yum install** tooinstall a package.</span></span> <span data-ttu-id="5070d-122">En su lugar, puede definir una lista de paquetes tooinstall.</span><span class="sxs-lookup"><span data-stu-id="5070d-122">Instead you can define a list of packages tooinstall.</span></span> <span data-ttu-id="5070d-123">Init de la nube usa automáticamente herramienta de administración del paquete nativo de Hola para distribución de Hola que seleccione.</span><span class="sxs-lookup"><span data-stu-id="5070d-123">Cloud-init automatically uses hello native package management tool for hello distro you select.</span></span>

<span data-ttu-id="5070d-124">Estamos trabajando con nuestro socios tooget nube-init incluida y estamos trabajando en las imágenes de Hola que proporcionan tooAzure.</span><span class="sxs-lookup"><span data-stu-id="5070d-124">We are working with our partners tooget cloud-init included and working in hello images that they provide tooAzure.</span></span> <span data-ttu-id="5070d-125">Hello en la tabla siguiente describe la disponibilidad de hello actual init de la nube en las imágenes de la plataforma Windows Azure:</span><span class="sxs-lookup"><span data-stu-id="5070d-125">hello following table outlines hello current cloud-init availability on Azure platform images:</span></span>

| <span data-ttu-id="5070d-126">Alias</span><span class="sxs-lookup"><span data-stu-id="5070d-126">Alias</span></span> | <span data-ttu-id="5070d-127">Publicador</span><span class="sxs-lookup"><span data-stu-id="5070d-127">Publisher</span></span> | <span data-ttu-id="5070d-128">Oferta</span><span class="sxs-lookup"><span data-stu-id="5070d-128">Offer</span></span> | <span data-ttu-id="5070d-129">SKU</span><span class="sxs-lookup"><span data-stu-id="5070d-129">SKU</span></span> | <span data-ttu-id="5070d-130">Versión</span><span class="sxs-lookup"><span data-stu-id="5070d-130">Version</span></span> |
|:--- |:--- |:--- |:--- |:--- |:--- |
| <span data-ttu-id="5070d-131">UbuntuLTS</span><span class="sxs-lookup"><span data-stu-id="5070d-131">UbuntuLTS</span></span> |<span data-ttu-id="5070d-132">Canonical</span><span class="sxs-lookup"><span data-stu-id="5070d-132">Canonical</span></span> |<span data-ttu-id="5070d-133">UbuntuServer</span><span class="sxs-lookup"><span data-stu-id="5070d-133">UbuntuServer</span></span> |<span data-ttu-id="5070d-134">16.04-LTS</span><span class="sxs-lookup"><span data-stu-id="5070d-134">16.04-LTS</span></span> |<span data-ttu-id="5070d-135">más reciente</span><span class="sxs-lookup"><span data-stu-id="5070d-135">latest</span></span> |
| <span data-ttu-id="5070d-136">UbuntuLTS</span><span class="sxs-lookup"><span data-stu-id="5070d-136">UbuntuLTS</span></span> |<span data-ttu-id="5070d-137">Canonical</span><span class="sxs-lookup"><span data-stu-id="5070d-137">Canonical</span></span> |<span data-ttu-id="5070d-138">UbuntuServer</span><span class="sxs-lookup"><span data-stu-id="5070d-138">UbuntuServer</span></span> |<span data-ttu-id="5070d-139">14.04.5-LTS</span><span class="sxs-lookup"><span data-stu-id="5070d-139">14.04.5-LTS</span></span> |<span data-ttu-id="5070d-140">más reciente</span><span class="sxs-lookup"><span data-stu-id="5070d-140">latest</span></span> |
| <span data-ttu-id="5070d-141">CoreOS</span><span class="sxs-lookup"><span data-stu-id="5070d-141">CoreOS</span></span> |<span data-ttu-id="5070d-142">CoreOS</span><span class="sxs-lookup"><span data-stu-id="5070d-142">CoreOS</span></span> |<span data-ttu-id="5070d-143">CoreOS</span><span class="sxs-lookup"><span data-stu-id="5070d-143">CoreOS</span></span> |<span data-ttu-id="5070d-144">Stable</span><span class="sxs-lookup"><span data-stu-id="5070d-144">Stable</span></span> |<span data-ttu-id="5070d-145">más reciente</span><span class="sxs-lookup"><span data-stu-id="5070d-145">latest</span></span> |


## <a name="create-cloud-init-config-file"></a><span data-ttu-id="5070d-146">Creación de un archivo de configuración cloud-init</span><span class="sxs-lookup"><span data-stu-id="5070d-146">Create cloud-init config file</span></span>
<span data-ttu-id="5070d-147">en la nube de toosee-init en acción, cree una máquina virtual que NGINX se instala y se ejecuta una aplicación sencilla de Node.js de "Hello World".</span><span class="sxs-lookup"><span data-stu-id="5070d-147">toosee cloud-init in action, create a VM that installs NGINX and runs a simple 'Hello World' Node.js app.</span></span> <span data-ttu-id="5070d-148">Hola siguiente configuración de nube init instala los paquetes de saludo necesario, crea una aplicación Node.js, a continuación, inicializa e inicia la aplicación hello.</span><span class="sxs-lookup"><span data-stu-id="5070d-148">hello following cloud-init configuration installs hello required packages, creates a Node.js app, then initialize and starts hello app.</span></span>

<span data-ttu-id="5070d-149">En el shell actual, cree un archivo denominado *init.txt nube* y pegar Hola siguiente configuración.</span><span class="sxs-lookup"><span data-stu-id="5070d-149">In your current shell, create a file named *cloud-init.txt* and paste hello following configuration.</span></span> <span data-ttu-id="5070d-150">Por ejemplo, crear archivo hello en hello Shell en la nube, no en el equipo local.</span><span class="sxs-lookup"><span data-stu-id="5070d-150">For example, create hello file in hello Cloud Shell not on your local machine.</span></span> <span data-ttu-id="5070d-151">Puede utilizar el editor que prefiera.</span><span class="sxs-lookup"><span data-stu-id="5070d-151">You can use any editor you wish.</span></span> <span data-ttu-id="5070d-152">Escriba `sensible-editor cloud-init.txt` toocreate Hola archivo y ver una lista de editores disponibles.</span><span class="sxs-lookup"><span data-stu-id="5070d-152">Enter `sensible-editor cloud-init.txt` toocreate hello file and see a list of available editors.</span></span> <span data-ttu-id="5070d-153">Asegúrese de que ese archivo de nube-init todo Hola se copia correctamente, especialmente Hola primera línea:</span><span class="sxs-lookup"><span data-stu-id="5070d-153">Make sure that hello whole cloud-init file is copied correctly, especially hello first line:</span></span>

```yaml
#cloud-config
package_upgrade: true
packages:
  - nginx
  - nodejs
  - npm
write_files:
  - owner: www-data:www-data
  - path: /etc/nginx/sites-available/default
    content: |
      server {
        listen 80;
        location / {
          proxy_pass http://localhost:3000;
          proxy_http_version 1.1;
          proxy_set_header Upgrade $http_upgrade;
          proxy_set_header Connection keep-alive;
          proxy_set_header Host $host;
          proxy_cache_bypass $http_upgrade;
        }
      }
  - owner: azureuser:azureuser
  - path: /home/azureuser/myapp/index.js
    content: |
      var express = require('express')
      var app = express()
      var os = require('os');
      app.get('/', function (req, res) {
        res.send('Hello World from host ' + os.hostname() + '!')
      })
      app.listen(3000, function () {
        console.log('Hello world app listening on port 3000!')
      })
runcmd:
  - service nginx restart
  - cd "/home/azureuser/myapp"
  - npm init
  - npm install express -y
  - nodejs index.js
```

<span data-ttu-id="5070d-154">Para más información sobre las opciones de configuración de cloud-init, consulte los [ejemplos de configuración de cloud-init](https://cloudinit.readthedocs.io/en/latest/topics/examples.html).</span><span class="sxs-lookup"><span data-stu-id="5070d-154">For more information about cloud-init configuration options, see [cloud-init config examples](https://cloudinit.readthedocs.io/en/latest/topics/examples.html).</span></span>

## <a name="create-virtual-machine"></a><span data-ttu-id="5070d-155">Create virtual machine</span><span class="sxs-lookup"><span data-stu-id="5070d-155">Create virtual machine</span></span>
<span data-ttu-id="5070d-156">Antes de poder crear una máquina virtual, cree un grupo de recursos con [az group create](/cli/azure/group#create).</span><span class="sxs-lookup"><span data-stu-id="5070d-156">Before you can create a VM, create a resource group with [az group create](/cli/azure/group#create).</span></span> <span data-ttu-id="5070d-157">Hello en el ejemplo siguiente se crea un grupo de recursos denominado *myResourceGroupAutomate* en hello *eastus* ubicación:</span><span class="sxs-lookup"><span data-stu-id="5070d-157">hello following example creates a resource group named *myResourceGroupAutomate* in hello *eastus* location:</span></span>

```azurecli-interactive 
az group create --name myResourceGroupAutomate --location eastus
```

<span data-ttu-id="5070d-158">Ahora cree una máquina virtual con el comando [az vm create](/cli/azure/vm#create).</span><span class="sxs-lookup"><span data-stu-id="5070d-158">Now create a VM with [az vm create](/cli/azure/vm#create).</span></span> <span data-ttu-id="5070d-159">Hola de uso `--custom-data` toopass de parámetro en el archivo de configuración de nube init.</span><span class="sxs-lookup"><span data-stu-id="5070d-159">Use hello `--custom-data` parameter toopass in your cloud-init config file.</span></span> <span data-ttu-id="5070d-160">Proporcionar toohello de ruta de acceso completa de hello *init.txt nube* config si guarda el archivo hello fuera de su directorio de trabajo actual.</span><span class="sxs-lookup"><span data-stu-id="5070d-160">Provide hello full path toohello *cloud-init.txt* config if you saved hello file outside of your present working directory.</span></span> <span data-ttu-id="5070d-161">Hello en el ejemplo siguiente se crea una máquina virtual denominada *myAutomatedVM*:</span><span class="sxs-lookup"><span data-stu-id="5070d-161">hello following example creates a VM named *myAutomatedVM*:</span></span>

```azurecli-interactive 
az vm create \
    --resource-group myResourceGroupAutomate \
    --name myVM \
    --image UbuntuLTS \
    --admin-username azureuser \
    --generate-ssh-keys \
    --custom-data cloud-init.txt
```

<span data-ttu-id="5070d-162">Se tarda unos minutos para hello VM toobe creado, tooinstall de paquetes de Hola y Hola toostart de aplicación.</span><span class="sxs-lookup"><span data-stu-id="5070d-162">It takes a few minutes for hello VM toobe created, hello packages tooinstall, and hello app toostart.</span></span> <span data-ttu-id="5070d-163">Hay tareas en segundo plano que continúan toorun después de hello CLI de Azure devuelve toohello símbolo del sistema.</span><span class="sxs-lookup"><span data-stu-id="5070d-163">There are background tasks that continue toorun after hello Azure CLI returns you toohello prompt.</span></span> <span data-ttu-id="5070d-164">Es posible que otro par de minutos antes de que se puede tener acceso a la aplicación hello.</span><span class="sxs-lookup"><span data-stu-id="5070d-164">It may be another couple of minutes before you can access hello app.</span></span> <span data-ttu-id="5070d-165">Cuando se ha creado Hola VM, tome nota de hello `publicIpAddress` muestra de Hola CLI de Azure.</span><span class="sxs-lookup"><span data-stu-id="5070d-165">When hello VM has been created, take note of hello `publicIpAddress` displayed by hello Azure CLI.</span></span> <span data-ttu-id="5070d-166">Esta dirección es tooaccess usado hello Node.js aplicación a través de un explorador web.</span><span class="sxs-lookup"><span data-stu-id="5070d-166">This address is used tooaccess hello Node.js app via a web browser.</span></span>

<span data-ttu-id="5070d-167">tooallow web tooreach de tráfico de la máquina virtual, abrir el puerto 80 de hello Internet con [az de vm abrir puerto](/cli/azure/vm#open-port):</span><span class="sxs-lookup"><span data-stu-id="5070d-167">tooallow web traffic tooreach your VM, open port 80 from hello Internet with [az vm open-port](/cli/azure/vm#open-port):</span></span>

```azurecli-interactive 
az vm open-port --port 80 --resource-group myResourceGroupAutomate --name myVM
```

## <a name="test-web-app"></a><span data-ttu-id="5070d-168">Prueba de la aplicación web</span><span class="sxs-lookup"><span data-stu-id="5070d-168">Test web app</span></span>
<span data-ttu-id="5070d-169">Ahora puede abrir un explorador web y escriba *http://<publicIpAddress>*  en la barra de direcciones de Hola.</span><span class="sxs-lookup"><span data-stu-id="5070d-169">Now you can open a web browser and enter *http://<publicIpAddress>* in hello address bar.</span></span> <span data-ttu-id="5070d-170">Proporcionar su propia público dirección IP de hello VM crear proceso.</span><span class="sxs-lookup"><span data-stu-id="5070d-170">Provide your own public IP address from hello VM create process.</span></span> <span data-ttu-id="5070d-171">La aplicación Node.js se muestra como en el siguiente ejemplo de Hola:</span><span class="sxs-lookup"><span data-stu-id="5070d-171">Your Node.js app is displayed as in hello following example:</span></span>

![Ver sitio de NGINX en funcionamiento](./media/tutorial-automate-vm-deployment/nginx.png)


## <a name="inject-certificates-from-key-vault"></a><span data-ttu-id="5070d-173">Inserción de certificados desde Key Vault</span><span class="sxs-lookup"><span data-stu-id="5070d-173">Inject certificates from Key Vault</span></span>
<span data-ttu-id="5070d-174">Esta sección opcional muestra cómo se puede almacenar certificados en el almacén de claves de Azure y se insertan durante la implementación de VM de Hola forma segura.</span><span class="sxs-lookup"><span data-stu-id="5070d-174">This optional section shows how you can securely store certificates in Azure Key Vault and inject them during hello VM deployment.</span></span> <span data-ttu-id="5070d-175">En lugar de usar una imagen personalizada que incluye los certificados de hello preparadas, este proceso garantiza que los certificados más actualizados de Hola se insertan tooa VM en el primer arranque.</span><span class="sxs-lookup"><span data-stu-id="5070d-175">Rather than using a custom image that includes hello certificates baked-in, this process ensures that hello most up-to-date certificates are injected tooa VM on first boot.</span></span> <span data-ttu-id="5070d-176">Durante el proceso de hello, certificado de hello nunca deja Hola plataforma Windows Azure o se expone en un script, el historial de la línea de comandos o la plantilla.</span><span class="sxs-lookup"><span data-stu-id="5070d-176">During hello process, hello certificate never leaves hello Azure platform or is exposed in a script, command-line history, or template.</span></span>

<span data-ttu-id="5070d-177">Azure Key Vault protege claves y secretos criptográficos, como certificados y contraseñas.</span><span class="sxs-lookup"><span data-stu-id="5070d-177">Azure Key Vault safeguards cryptographic keys and secrets, such as certificates or passwords.</span></span> <span data-ttu-id="5070d-178">El almacén de claves ayuda a simplificar el proceso de administración de claves de Hola y permite toomaintain control de claves que tienen acceso y cifrar los datos.</span><span class="sxs-lookup"><span data-stu-id="5070d-178">Key Vault helps streamline hello key management process and enables you toomaintain control of keys that access and encrypt your data.</span></span> <span data-ttu-id="5070d-179">Este escenario se presentan algunos toocreate de conceptos de almacén de claves y usar un certificado, aunque no es exhaustiva información general acerca de cómo toouse el almacén de claves.</span><span class="sxs-lookup"><span data-stu-id="5070d-179">This scenario introduces some Key Vault concepts toocreate and use a certificate, though is not an exhaustive overview on how toouse Key Vault.</span></span>

<span data-ttu-id="5070d-180">Hola siguientes pasos muestra cómo se puede:</span><span class="sxs-lookup"><span data-stu-id="5070d-180">hello following steps show how you can:</span></span>

- <span data-ttu-id="5070d-181">Crear una instancia de Azure Key Vault</span><span class="sxs-lookup"><span data-stu-id="5070d-181">Create an Azure Key Vault</span></span>
- <span data-ttu-id="5070d-182">Generar o cargar un almacén de claves de certificado toohello</span><span class="sxs-lookup"><span data-stu-id="5070d-182">Generate or upload a certificate toohello Key Vault</span></span>
- <span data-ttu-id="5070d-183">Crear un secreto de hello certificado tooinject en tooa VM</span><span class="sxs-lookup"><span data-stu-id="5070d-183">Create a secret from hello certificate tooinject in tooa VM</span></span>
- <span data-ttu-id="5070d-184">Crear una máquina virtual e insertar certificado de Hola</span><span class="sxs-lookup"><span data-stu-id="5070d-184">Create a VM and inject hello certificate</span></span>

### <a name="create-an-azure-key-vault"></a><span data-ttu-id="5070d-185">Crear una instancia de Azure Key Vault</span><span class="sxs-lookup"><span data-stu-id="5070d-185">Create an Azure Key Vault</span></span>
<span data-ttu-id="5070d-186">En primer lugar, cree una instancia de Key Vault con [az keyvault create](/cli/azure/keyvault#create) y habilítela para su uso al implementar una máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="5070d-186">First, create a Key Vault with [az keyvault create](/cli/azure/keyvault#create) and enable it for use when you deploy a VM.</span></span> <span data-ttu-id="5070d-187">Cada instancia de Key Vault requiere un nombre único, que debe estar todo en minúsculas.</span><span class="sxs-lookup"><span data-stu-id="5070d-187">Each Key Vault requires a unique name, and should be all lower case.</span></span> <span data-ttu-id="5070d-188">Reemplace *mykeyvault* en el siguiente ejemplo con su propio nombre de almacén de claves único de hello:</span><span class="sxs-lookup"><span data-stu-id="5070d-188">Replace *mykeyvault* in hello following example with your own unique Key Vault name:</span></span>

```azurecli-interactive 
keyvault_name=mykeyvault
az keyvault create \
    --resource-group myResourceGroupAutomate \
    --name $keyvault_name \
    --enabled-for-deployment
```

### <a name="generate-certificate-and-store-in-key-vault"></a><span data-ttu-id="5070d-189">Generación de un certificado y su almacenamiento en Key Vault</span><span class="sxs-lookup"><span data-stu-id="5070d-189">Generate certificate and store in Key Vault</span></span>
<span data-ttu-id="5070d-190">Para usarlo en producción, debe importar un certificado válido firmado por un proveedor de confianza con [az keyvault certificate import](/cli/azure/keyvault/certificate#import).</span><span class="sxs-lookup"><span data-stu-id="5070d-190">For production use, you should import a valid certificate signed by trusted provider with [az keyvault certificate import](/cli/azure/keyvault/certificate#import).</span></span> <span data-ttu-id="5070d-191">Para este tutorial, hello en el ejemplo siguiente se muestra cómo puede generar un certificado autofirmado con [crear certificado de keyvault az](/cli/azure/keyvault/certificate#create) que usa la directiva de certificado de hello predeterminada:</span><span class="sxs-lookup"><span data-stu-id="5070d-191">For this tutorial, hello following example shows how you can generate a self-signed certificate with [az keyvault certificate create](/cli/azure/keyvault/certificate#create) that uses hello default certificate policy:</span></span>

```azurecli-interactive 
az keyvault certificate create \
    --vault-name $keyvault_name \
    --name mycert \
    --policy "$(az keyvault certificate get-default-policy)"
```


### <a name="prepare-certificate-for-use-with-vm"></a><span data-ttu-id="5070d-192">Preparación del certificado para usarlo con la máquina virtual</span><span class="sxs-lookup"><span data-stu-id="5070d-192">Prepare certificate for use with VM</span></span>
<span data-ttu-id="5070d-193">certificado de hello toouse durante Hola VM crear proceso, obtener Id. de hello del certificado con [az keyvault secreto lista versiones](/cli/azure/keyvault/secret#list-versions).</span><span class="sxs-lookup"><span data-stu-id="5070d-193">toouse hello certificate during hello VM create process, obtain hello ID of your certificate with [az keyvault secret list-versions](/cli/azure/keyvault/secret#list-versions).</span></span> <span data-ttu-id="5070d-194">Hola VM necesita certificado de hello en un determinado tooinject de formato que se arranque el sistema, por lo que convertir el certificado de hello con [az de vm formato secreto](/cli/azure/vm#format-secret).</span><span class="sxs-lookup"><span data-stu-id="5070d-194">hello VM needs hello certificate in a certain format tooinject it on boot, so convert hello certificate with [az vm format-secret](/cli/azure/vm#format-secret).</span></span> <span data-ttu-id="5070d-195">Hola de ejemplo siguiente asigna a salida de hello de estos toovariables de comandos para facilitar su uso en hello pasos siguientes:</span><span class="sxs-lookup"><span data-stu-id="5070d-195">hello following example assigns hello output of these commands toovariables for ease of use in hello next steps:</span></span>

```azurecli-interactive 
secret=$(az keyvault secret list-versions \
          --vault-name $keyvault_name \
          --name mycert \
          --query "[?attributes.enabled].id" --output tsv)
vm_secret=$(az vm format-secret --secret "$secret")
```


### <a name="create-cloud-init-config-toosecure-nginx"></a><span data-ttu-id="5070d-196">Crear configuración de nube init toosecure NGINX</span><span class="sxs-lookup"><span data-stu-id="5070d-196">Create cloud-init config toosecure NGINX</span></span>
<span data-ttu-id="5070d-197">Cuando se crea una máquina virtual, certificados y claves se almacenan en hello protegido */var/lib/waagent/* directory.</span><span class="sxs-lookup"><span data-stu-id="5070d-197">When you create a VM, certificates and keys are stored in hello protected */var/lib/waagent/* directory.</span></span> <span data-ttu-id="5070d-198">tooautomate agregar Hola certificado toohello máquina virtual y configurar NGINX, puede usar una configuración actualizada en la nube al inicio del ejemplo anterior de Hola.</span><span class="sxs-lookup"><span data-stu-id="5070d-198">tooautomate adding hello certificate toohello VM and configuring NGINX, you can use an updated cloud-init config from hello previous example.</span></span>

<span data-ttu-id="5070d-199">Cree un archivo denominado *nube-init-secured.txt* y pegar Hola siguiente configuración.</span><span class="sxs-lookup"><span data-stu-id="5070d-199">Create a file named *cloud-init-secured.txt* and paste hello following configuration.</span></span> <span data-ttu-id="5070d-200">De nuevo, si usas Hola Shell en la nube, crear el archivo de configuración de nube init Hola localizada ahí y no en el equipo local.</span><span class="sxs-lookup"><span data-stu-id="5070d-200">Again, if you use hello Cloud Shell, create hello cloud-init config file there and not on your local machine.</span></span> <span data-ttu-id="5070d-201">Use `sensible-editor cloud-init-secured.txt` toocreate Hola archivo y ver una lista de editores disponibles.</span><span class="sxs-lookup"><span data-stu-id="5070d-201">Use `sensible-editor cloud-init-secured.txt` toocreate hello file and see a list of available editors.</span></span> <span data-ttu-id="5070d-202">Asegúrese de que ese archivo de nube-init todo Hola se copia correctamente, especialmente Hola primera línea:</span><span class="sxs-lookup"><span data-stu-id="5070d-202">Make sure that hello whole cloud-init file is copied correctly, especially hello first line:</span></span>

```yaml
#cloud-config
package_upgrade: true
packages:
  - nginx
  - nodejs
  - npm
write_files:
  - owner: www-data:www-data
  - path: /etc/nginx/sites-available/default
    content: |
      server {
        listen 80;
        listen 443 ssl;
        ssl_certificate /etc/nginx/ssl/mycert.cert;
        ssl_certificate_key /etc/nginx/ssl/mycert.prv;
        location / {
          proxy_pass http://localhost:3000;
          proxy_http_version 1.1;
          proxy_set_header Upgrade $http_upgrade;
          proxy_set_header Connection keep-alive;
          proxy_set_header Host $host;
          proxy_cache_bypass $http_upgrade;
        }
      }
  - owner: azureuser:azureuser
  - path: /home/azureuser/myapp/index.js
    content: |
      var express = require('express')
      var app = express()
      var os = require('os');
      app.get('/', function (req, res) {
        res.send('Hello World from host ' + os.hostname() + '!')
      })
      app.listen(3000, function () {
        console.log('Hello world app listening on port 3000!')
      })
runcmd:
  - secretsname=$(find /var/lib/waagent/ -name "*.prv" | cut -c -57)
  - mkdir /etc/nginx/ssl
  - cp $secretsname.crt /etc/nginx/ssl/mycert.cert
  - cp $secretsname.prv /etc/nginx/ssl/mycert.prv
  - service nginx restart
  - cd "/home/azureuser/myapp"
  - npm init
  - npm install express -y
  - nodejs index.js
```

### <a name="create-secure-vm"></a><span data-ttu-id="5070d-203">Creación de una máquina virtual segura</span><span class="sxs-lookup"><span data-stu-id="5070d-203">Create secure VM</span></span>
<span data-ttu-id="5070d-204">Ahora cree una máquina virtual con el comando [az vm create](/cli/azure/vm#create).</span><span class="sxs-lookup"><span data-stu-id="5070d-204">Now create a VM with [az vm create](/cli/azure/vm#create).</span></span> <span data-ttu-id="5070d-205">datos del certificado Hola se inyección desde el almacén de claves con hello `--secrets` parámetro.</span><span class="sxs-lookup"><span data-stu-id="5070d-205">hello certificate data is injected from Key Vault with hello `--secrets` parameter.</span></span> <span data-ttu-id="5070d-206">Como en el ejemplo anterior de hello, también pasar en la configuración de nube init Hola con hello `--custom-data` parámetro:</span><span class="sxs-lookup"><span data-stu-id="5070d-206">As in hello previous example, you also pass in hello cloud-init config with hello `--custom-data` parameter:</span></span>

```azurecli-interactive 
az vm create \
    --resource-group myResourceGroupAutomate \
    --name myVMSecured \
    --image UbuntuLTS \
    --admin-username azureuser \
    --generate-ssh-keys \
    --custom-data cloud-init-secured.txt \
    --secrets "$vm_secret"
```

<span data-ttu-id="5070d-207">Se tarda unos minutos para hello VM toobe creado, tooinstall de paquetes de Hola y Hola toostart de aplicación.</span><span class="sxs-lookup"><span data-stu-id="5070d-207">It takes a few minutes for hello VM toobe created, hello packages tooinstall, and hello app toostart.</span></span> <span data-ttu-id="5070d-208">Hay tareas en segundo plano que continúan toorun después de hello CLI de Azure devuelve toohello símbolo del sistema.</span><span class="sxs-lookup"><span data-stu-id="5070d-208">There are background tasks that continue toorun after hello Azure CLI returns you toohello prompt.</span></span> <span data-ttu-id="5070d-209">Es posible que otro par de minutos antes de que se puede tener acceso a la aplicación hello.</span><span class="sxs-lookup"><span data-stu-id="5070d-209">It may be another couple of minutes before you can access hello app.</span></span> <span data-ttu-id="5070d-210">Cuando se ha creado Hola VM, tome nota de hello `publicIpAddress` muestra de Hola CLI de Azure.</span><span class="sxs-lookup"><span data-stu-id="5070d-210">When hello VM has been created, take note of hello `publicIpAddress` displayed by hello Azure CLI.</span></span> <span data-ttu-id="5070d-211">Esta dirección es tooaccess usado hello Node.js aplicación a través de un explorador web.</span><span class="sxs-lookup"><span data-stu-id="5070d-211">This address is used tooaccess hello Node.js app via a web browser.</span></span>

<span data-ttu-id="5070d-212">tooallow secure web tráfico tooreach la máquina virtual, abrir el puerto 443 de hello Internet con [az de vm abrir puerto](/cli/azure/vm#open-port):</span><span class="sxs-lookup"><span data-stu-id="5070d-212">tooallow secure web traffic tooreach your VM, open port 443 from hello Internet with [az vm open-port](/cli/azure/vm#open-port):</span></span>

```azurecli-interactive 
az vm open-port \
    --resource-group myResourceGroupAutomate \
    --name myVMSecured \
    --port 443
```

### <a name="test-secure-web-app"></a><span data-ttu-id="5070d-213">Prueba de la aplicación web segura</span><span class="sxs-lookup"><span data-stu-id="5070d-213">Test secure web app</span></span>
<span data-ttu-id="5070d-214">Ahora puede abrir un explorador web y escriba *https://<publicIpAddress>*  en la barra de direcciones de Hola.</span><span class="sxs-lookup"><span data-stu-id="5070d-214">Now you can open a web browser and enter *https://<publicIpAddress>* in hello address bar.</span></span> <span data-ttu-id="5070d-215">Proporcionar su propia público dirección IP de hello VM crear proceso.</span><span class="sxs-lookup"><span data-stu-id="5070d-215">Provide your own public IP address from hello VM create process.</span></span> <span data-ttu-id="5070d-216">Acepte la advertencia de seguridad de hello si usa un certificado autofirmado:</span><span class="sxs-lookup"><span data-stu-id="5070d-216">Accept hello security warning if you used a self-signed certificate:</span></span>

![Aceptar la advertencia de seguridad del explorador web](./media/tutorial-automate-vm-deployment/browser-warning.png)

<span data-ttu-id="5070d-218">El sitio NGINX y Node.js protegida, a continuación, se muestra la aplicación como en el siguiente ejemplo de Hola:</span><span class="sxs-lookup"><span data-stu-id="5070d-218">Your secured NGINX site and Node.js app is then displayed as in hello following example:</span></span>

![Ver el sitio de NGINX seguro en funcionamiento](./media/tutorial-automate-vm-deployment/secured-nginx.png)


## <a name="next-steps"></a><span data-ttu-id="5070d-220">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="5070d-220">Next steps</span></span>
<span data-ttu-id="5070d-221">En este tutorial, ha configurado las máquinas virtuales en el primer inicio con cloud-init.</span><span class="sxs-lookup"><span data-stu-id="5070d-221">In this tutorial, you configured VMs on first boot with cloud-init.</span></span> <span data-ttu-id="5070d-222">Ha aprendido a:</span><span class="sxs-lookup"><span data-stu-id="5070d-222">You learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="5070d-223">Crear un archivo de configuración cloud-init</span><span class="sxs-lookup"><span data-stu-id="5070d-223">Create a cloud-init config file</span></span>
> * <span data-ttu-id="5070d-224">Crear una máquina virtual que usa un archivo cloud-init</span><span class="sxs-lookup"><span data-stu-id="5070d-224">Create a VM that uses a cloud-init file</span></span>
> * <span data-ttu-id="5070d-225">Ver una aplicación en ejecución Node.js después de hello que VM.</span><span class="sxs-lookup"><span data-stu-id="5070d-225">View a running Node.js app after hello VM is created</span></span>
> * <span data-ttu-id="5070d-226">Usar el almacén de claves toosecurely almacén de certificados</span><span class="sxs-lookup"><span data-stu-id="5070d-226">Use Key Vault toosecurely store certificates</span></span>
> * <span data-ttu-id="5070d-227">Automatizar implementaciones seguras de NGINX con cloud-init</span><span class="sxs-lookup"><span data-stu-id="5070d-227">Automate secure deployments of NGINX with cloud-init</span></span>

<span data-ttu-id="5070d-228">Avanzar toohello siguiente tutorial toolearn cómo toocreate imágenes de máquina virtual personalizadas.</span><span class="sxs-lookup"><span data-stu-id="5070d-228">Advance toohello next tutorial toolearn how toocreate custom VM images.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="5070d-229">Creación de imágenes personalizadas de máquinas virtuales</span><span class="sxs-lookup"><span data-stu-id="5070d-229">Create custom VM images</span></span>](./tutorial-custom-images.md)
