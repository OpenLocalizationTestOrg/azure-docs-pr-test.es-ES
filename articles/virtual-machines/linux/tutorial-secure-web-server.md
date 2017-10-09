---
title: aaaSecure certificados de un servidor web con SSL en Azure | Documentos de Microsoft
description: "Obtenga información acerca de cómo certificados de servidor de toosecure hello NGINX web con SSL en una VM de Linux en Azure"
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
ms.date: 07/17/2017
ms.author: iainfou
ms.custom: mvc
ms.openlocfilehash: d3a62d77ac05c9aa2a44356b7c8e44cb485b81aa
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="secure-a-web-server-with-ssl-certificates-on-a-linux-virtual-machine-in-azure"></a><span data-ttu-id="c7b9a-103">Protección de un servidor web con certificados SSL en una máquina virtual Linux en Azure</span><span class="sxs-lookup"><span data-stu-id="c7b9a-103">Secure a web server with SSL certificates on a Linux virtual machine in Azure</span></span>
<span data-ttu-id="c7b9a-104">los servidores web toosecure, que puede ser un certificado Secure Sockets más adelante (SSL) utiliza el tráfico web tooencrypt.</span><span class="sxs-lookup"><span data-stu-id="c7b9a-104">toosecure web servers, a Secure Sockets Later (SSL) certificate can be used tooencrypt web traffic.</span></span> <span data-ttu-id="c7b9a-105">Estos certificados SSL pueden almacenarse en el almacén de claves de Azure y permiten implementaciones seguras de certificados tooLinux máquinas virtuales (VMs) en Azure.</span><span class="sxs-lookup"><span data-stu-id="c7b9a-105">These SSL certificates can be stored in Azure Key Vault, and allow secure deployments of certificates tooLinux virtual machines (VMs) in Azure.</span></span> <span data-ttu-id="c7b9a-106">En este tutorial, aprenderá a:</span><span class="sxs-lookup"><span data-stu-id="c7b9a-106">In this tutorial you learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="c7b9a-107">Crear una instancia de Azure Key Vault</span><span class="sxs-lookup"><span data-stu-id="c7b9a-107">Create an Azure Key Vault</span></span>
> * <span data-ttu-id="c7b9a-108">Generar o cargar un almacén de claves de certificado toohello</span><span class="sxs-lookup"><span data-stu-id="c7b9a-108">Generate or upload a certificate toohello Key Vault</span></span>
> * <span data-ttu-id="c7b9a-109">Crear una máquina virtual e instale el servidor de web NGINX Hola</span><span class="sxs-lookup"><span data-stu-id="c7b9a-109">Create a VM and install hello NGINX web server</span></span>
> * <span data-ttu-id="c7b9a-110">Insertar certificado de hello en hello VM y configurar NGINX con un enlace SSL</span><span class="sxs-lookup"><span data-stu-id="c7b9a-110">Inject hello certificate into hello VM and configure NGINX with an SSL binding</span></span>

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="c7b9a-111">Si elige tooinstall y usar hello CLI localmente, este tutorial requiere que se ejecuta la versión de CLI de Azure de hello 2.0.4 o versiones posteriores.</span><span class="sxs-lookup"><span data-stu-id="c7b9a-111">If you choose tooinstall and use hello CLI locally, this tutorial requires that you are running hello Azure CLI version 2.0.4 or later.</span></span> <span data-ttu-id="c7b9a-112">Ejecutar `az --version` toofind versión de Hola.</span><span class="sxs-lookup"><span data-stu-id="c7b9a-112">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="c7b9a-113">Si necesita tooinstall o una actualización, consulte [instalar Azure CLI 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="c7b9a-113">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span>  


## <a name="overview"></a><span data-ttu-id="c7b9a-114">Información general</span><span class="sxs-lookup"><span data-stu-id="c7b9a-114">Overview</span></span>
<span data-ttu-id="c7b9a-115">Azure Key Vault protege claves y secretos criptográficos, como certificados y contraseñas.</span><span class="sxs-lookup"><span data-stu-id="c7b9a-115">Azure Key Vault safeguards cryptographic keys and secrets, such certificates or passwords.</span></span> <span data-ttu-id="c7b9a-116">El almacén de claves ayuda a simplificar el proceso de administración de certificados de Hola y permite toomaintain control de claves que tienen acceso a dichos certificados.</span><span class="sxs-lookup"><span data-stu-id="c7b9a-116">Key Vault helps streamline hello certificate management process and enables you toomaintain control of keys that access those certificates.</span></span> <span data-ttu-id="c7b9a-117">Puede crear un certificado autofirmado en Key Vault o cargar un certificado de confianza existente que ya posea.</span><span class="sxs-lookup"><span data-stu-id="c7b9a-117">You can create a self-signed certificate inside Key Vault, or upload an existing, trusted certificate that you already own.</span></span>

<span data-ttu-id="c7b9a-118">En lugar de usar una imagen de máquina virtual personalizada que incluya los certificados preparados, inserta los certificados en una máquina virtual en ejecución.</span><span class="sxs-lookup"><span data-stu-id="c7b9a-118">Rather than using a custom VM image that includes certificates baked-in, you inject certificates into a running VM.</span></span> <span data-ttu-id="c7b9a-119">Este proceso garantiza que los certificados más actualizados de hello están instalados en un servidor web durante la implementación.</span><span class="sxs-lookup"><span data-stu-id="c7b9a-119">This process ensures that hello most up-to-date certificates are installed on a web server during deployment.</span></span> <span data-ttu-id="c7b9a-120">Si renovar o reemplazar un certificado, no tendrá también toocreate una nueva imagen de máquina virtual personalizada.</span><span class="sxs-lookup"><span data-stu-id="c7b9a-120">If you renew or replace a certificate, you don't also have toocreate a new custom VM image.</span></span> <span data-ttu-id="c7b9a-121">los certificados más recientes de Hola se insertan automáticamente a medida que cree máquinas virtuales adicionales.</span><span class="sxs-lookup"><span data-stu-id="c7b9a-121">hello latest certificates are automatically injected as you create additional VMs.</span></span> <span data-ttu-id="c7b9a-122">Durante el proceso completo de hello, certificados de hello nunca deje Hola plataforma Windows Azure o se exponen en un script, el historial de la línea de comandos o la plantilla.</span><span class="sxs-lookup"><span data-stu-id="c7b9a-122">During hello whole process, hello certificates never leave hello Azure platform or are exposed in a script, command-line history, or template.</span></span>


## <a name="create-an-azure-key-vault"></a><span data-ttu-id="c7b9a-123">Crear una instancia de Azure Key Vault</span><span class="sxs-lookup"><span data-stu-id="c7b9a-123">Create an Azure Key Vault</span></span>
<span data-ttu-id="c7b9a-124">Para poder crear una instancia de Key Vault y certificados, cree un grupo de recursos con [az group create](/cli/azure/group#create).</span><span class="sxs-lookup"><span data-stu-id="c7b9a-124">Before you can create a Key Vault and certificates, create a resource group with [az group create](/cli/azure/group#create).</span></span> <span data-ttu-id="c7b9a-125">Hello en el ejemplo siguiente se crea un grupo de recursos denominado *myResourceGroupSecureWeb* en hello *eastus* ubicación:</span><span class="sxs-lookup"><span data-stu-id="c7b9a-125">hello following example creates a resource group named *myResourceGroupSecureWeb* in hello *eastus* location:</span></span>

```azurecli-interactive 
az group create --name myResourceGroupSecureWeb --location eastus
```

<span data-ttu-id="c7b9a-126">Después, cree una instancia de Key Vault con [az keyvault create](/cli/azure/keyvault#create) y habilítela para usarla al implementar una máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="c7b9a-126">Next, create a Key Vault with [az keyvault create](/cli/azure/keyvault#create) and enable it for use when you deploy a VM.</span></span> <span data-ttu-id="c7b9a-127">Cada instancia de Key Vault requiere un nombre único, que debe estar todo en minúsculas.</span><span class="sxs-lookup"><span data-stu-id="c7b9a-127">Each Key Vault requires a unique name, and should be all lower case.</span></span> <span data-ttu-id="c7b9a-128">Reemplace  *<mykeyvault>*  en el siguiente ejemplo con su propio nombre de almacén de claves único de hello:</span><span class="sxs-lookup"><span data-stu-id="c7b9a-128">Replace *<mykeyvault>* in hello following example with your own unique Key Vault name:</span></span>

```azurecli-interactive 
keyvault_name=<mykeyvault>
az keyvault create \
    --resource-group myResourceGroupSecureWeb \
    --name $keyvault_name \
    --enabled-for-deployment
```

## <a name="generate-a-certificate-and-store-in-key-vault"></a><span data-ttu-id="c7b9a-129">Generación de un certificado y almacenamiento en Key Vault</span><span class="sxs-lookup"><span data-stu-id="c7b9a-129">Generate a certificate and store in Key Vault</span></span>
<span data-ttu-id="c7b9a-130">Para usarlo en producción, debe importar un certificado válido firmado por un proveedor de confianza con [az keyvault certificate import](/cli/azure/certificate#import).</span><span class="sxs-lookup"><span data-stu-id="c7b9a-130">For production use, you should import a valid certificate signed by trusted provider with [az keyvault certificate import](/cli/azure/certificate#import).</span></span> <span data-ttu-id="c7b9a-131">Para este tutorial, hello en el ejemplo siguiente se muestra cómo puede generar un certificado autofirmado con [crear certificado de keyvault az](/cli/azure/certificate#create) que usa la directiva de certificado de hello predeterminada:</span><span class="sxs-lookup"><span data-stu-id="c7b9a-131">For this tutorial, hello following example shows how you can generate a self-signed certificate with [az keyvault certificate create](/cli/azure/certificate#create) that uses hello default certificate policy:</span></span>

```azurecli-interactive 
az keyvault certificate create \
    --vault-name $keyvault_name \
    --name mycert \
    --policy "$(az keyvault certificate get-default-policy)"
```

### <a name="prepare-a-certificate-for-use-with-a-vm"></a><span data-ttu-id="c7b9a-132">Preparación del certificado para usarlo con una máquina virtual</span><span class="sxs-lookup"><span data-stu-id="c7b9a-132">Prepare a certificate for use with a VM</span></span>
<span data-ttu-id="c7b9a-133">certificado de hello toouse durante Hola VM crear proceso, obtener Id. de hello del certificado con [az keyvault secreto lista versiones](/cli/azure/keyvault/secret#list-versions).</span><span class="sxs-lookup"><span data-stu-id="c7b9a-133">toouse hello certificate during hello VM create process, obtain hello ID of your certificate with [az keyvault secret list-versions](/cli/azure/keyvault/secret#list-versions).</span></span> <span data-ttu-id="c7b9a-134">Convertir el certificado de hello con [az de vm formato secreto](/cli/azure/vm#format-secret).</span><span class="sxs-lookup"><span data-stu-id="c7b9a-134">Convert hello certificate with [az vm format-secret](/cli/azure/vm#format-secret).</span></span> <span data-ttu-id="c7b9a-135">Hola de ejemplo siguiente asigna a salida de hello de estos toovariables de comandos para facilitar su uso en hello pasos siguientes:</span><span class="sxs-lookup"><span data-stu-id="c7b9a-135">hello following example assigns hello output of these commands toovariables for ease of use in hello next steps:</span></span>

```azurecli-interactive 
secret=$(az keyvault secret list-versions \
          --vault-name $keyvault_name \
          --name mycert \
          --query "[?attributes.enabled].id" --output tsv)
vm_secret=$(az vm format-secret --secret "$secret")
```

### <a name="create-a-cloud-init-config-toosecure-nginx"></a><span data-ttu-id="c7b9a-136">Crear un toosecure de configuración de nube init NGINX</span><span class="sxs-lookup"><span data-stu-id="c7b9a-136">Create a cloud-init config toosecure NGINX</span></span>
<span data-ttu-id="c7b9a-137">[En la nube init](https://cloudinit.readthedocs.io) es un enfoque ampliamente utilizado toocustomize una VM Linux tal y como se arranca para hello primera vez.</span><span class="sxs-lookup"><span data-stu-id="c7b9a-137">[Cloud-init](https://cloudinit.readthedocs.io) is a widely used approach toocustomize a Linux VM as it boots for hello first time.</span></span> <span data-ttu-id="c7b9a-138">Puede usar en la nube init tooinstall paquetes y escribir archivos, o los usuarios de tooconfigure y seguridad.</span><span class="sxs-lookup"><span data-stu-id="c7b9a-138">You can use cloud-init tooinstall packages and write files, or tooconfigure users and security.</span></span> <span data-ttu-id="c7b9a-139">Como init de la nube se ejecuta durante el proceso de arranque inicial de hello, no hay ningún paso adicional o requiere la configuración de agentes tooapply.</span><span class="sxs-lookup"><span data-stu-id="c7b9a-139">As cloud-init runs during hello initial boot process, there are no additional steps or required agents tooapply your configuration.</span></span>

<span data-ttu-id="c7b9a-140">Cuando se crea una máquina virtual, certificados y claves se almacenan en hello protegido */var/lib/waagent/* directory.</span><span class="sxs-lookup"><span data-stu-id="c7b9a-140">When you create a VM, certificates and keys are stored in hello protected */var/lib/waagent/* directory.</span></span> <span data-ttu-id="c7b9a-141">Agregar tooautomate Hola certificado toohello VM y configuración de servidor web de hello, utilice init de la nube.</span><span class="sxs-lookup"><span data-stu-id="c7b9a-141">tooautomate adding hello certificate toohello VM and configuring hello web server, use cloud-init.</span></span> <span data-ttu-id="c7b9a-142">En este ejemplo, se instalar y configura el servidor de web NGINX Hola.</span><span class="sxs-lookup"><span data-stu-id="c7b9a-142">In this example, we install and configure hello NGINX web server.</span></span> <span data-ttu-id="c7b9a-143">Puede usar hello mismo proceso tooinstall y configurar Apache.</span><span class="sxs-lookup"><span data-stu-id="c7b9a-143">You can use hello same process tooinstall and configure Apache.</span></span> 

<span data-ttu-id="c7b9a-144">Cree un archivo denominado *nube-init-web-server.txt* y pegar Hola siguiente configuración:</span><span class="sxs-lookup"><span data-stu-id="c7b9a-144">Create a file named *cloud-init-web-server.txt* and paste hello following configuration:</span></span>

```yaml
#cloud-config
package_upgrade: true
packages:
  - nginx
write_files:
  - owner: www-data:www-data
  - path: /etc/nginx/sites-available/default
    content: |
      server {
        listen 443 ssl;
        ssl_certificate /etc/nginx/ssl/mycert.cert;
        ssl_certificate_key /etc/nginx/ssl/mycert.prv;
      }
runcmd:
  - secretsname=$(find /var/lib/waagent/ -name "*.prv" | cut -c -57)
  - mkdir /etc/nginx/ssl
  - cp $secretsname.crt /etc/nginx/ssl/mycert.cert
  - cp $secretsname.prv /etc/nginx/ssl/mycert.prv
  - service nginx restart
```

### <a name="create-a-secure-vm"></a><span data-ttu-id="c7b9a-145">Creación de una máquina virtual segura</span><span class="sxs-lookup"><span data-stu-id="c7b9a-145">Create a secure VM</span></span>
<span data-ttu-id="c7b9a-146">Ahora cree una máquina virtual con el comando [az vm create](/cli/azure/vm#create).</span><span class="sxs-lookup"><span data-stu-id="c7b9a-146">Now create a VM with [az vm create](/cli/azure/vm#create).</span></span> <span data-ttu-id="c7b9a-147">datos del certificado Hola se inyección desde el almacén de claves con hello `--secrets` parámetro.</span><span class="sxs-lookup"><span data-stu-id="c7b9a-147">hello certificate data is injected from Key Vault with hello `--secrets` parameter.</span></span> <span data-ttu-id="c7b9a-148">Se pasa en la configuración de nube init Hola con hello `--custom-data` parámetro:</span><span class="sxs-lookup"><span data-stu-id="c7b9a-148">You pass in hello cloud-init config with hello `--custom-data` parameter:</span></span>

```azurecli-interactive 
az vm create \
    --resource-group myResourceGroupSecureWeb \
    --name myVM \
    --image UbuntuLTS \
    --admin-username azureuser \
    --generate-ssh-keys \
    --custom-data cloud-init-web-server.txt \
    --secrets "$vm_secret"
```

<span data-ttu-id="c7b9a-149">Se tarda unos minutos para hello VM toobe creado, tooinstall de paquetes de Hola y Hola toostart de aplicación.</span><span class="sxs-lookup"><span data-stu-id="c7b9a-149">It takes a few minutes for hello VM toobe created, hello packages tooinstall, and hello app toostart.</span></span> <span data-ttu-id="c7b9a-150">Cuando se ha creado Hola VM, tome nota de hello `publicIpAddress` muestra de Hola CLI de Azure.</span><span class="sxs-lookup"><span data-stu-id="c7b9a-150">When hello VM has been created, take note of hello `publicIpAddress` displayed by hello Azure CLI.</span></span> <span data-ttu-id="c7b9a-151">Esta dirección es tooaccess usa su sitio en un explorador web.</span><span class="sxs-lookup"><span data-stu-id="c7b9a-151">This address is used tooaccess your site in a web browser.</span></span>

<span data-ttu-id="c7b9a-152">tooallow secure web tráfico tooreach la máquina virtual, abrir el puerto 443 de hello Internet con [az de vm abrir puerto](/cli/azure/vm#open-port):</span><span class="sxs-lookup"><span data-stu-id="c7b9a-152">tooallow secure web traffic tooreach your VM, open port 443 from hello Internet with [az vm open-port](/cli/azure/vm#open-port):</span></span>

```azurecli-interactive 
az vm open-port \
    --resource-group myResourceGroupSecureWeb \
    --name myVM \
    --port 443
```


### <a name="test-hello-secure-web-app"></a><span data-ttu-id="c7b9a-153">Aplicación de prueba hello web segura</span><span class="sxs-lookup"><span data-stu-id="c7b9a-153">Test hello secure web app</span></span>
<span data-ttu-id="c7b9a-154">Ahora puede abrir un explorador web y escriba *https://<publicIpAddress>*  en la barra de direcciones de Hola.</span><span class="sxs-lookup"><span data-stu-id="c7b9a-154">Now you can open a web browser and enter *https://<publicIpAddress>* in hello address bar.</span></span> <span data-ttu-id="c7b9a-155">Proporcionar su propia público dirección IP de hello VM crear proceso.</span><span class="sxs-lookup"><span data-stu-id="c7b9a-155">Provide your own public IP address from hello VM create process.</span></span> <span data-ttu-id="c7b9a-156">Acepte la advertencia de seguridad de hello si usa un certificado autofirmado:</span><span class="sxs-lookup"><span data-stu-id="c7b9a-156">Accept hello security warning if you used a self-signed certificate:</span></span>

![Aceptar la advertencia de seguridad del explorador web](./media/tutorial-secure-web-server/browser-warning.png)

<span data-ttu-id="c7b9a-158">El sitio NGINX seguro, a continuación, se muestra como en el siguiente ejemplo de Hola:</span><span class="sxs-lookup"><span data-stu-id="c7b9a-158">Your secured NGINX site is then displayed as in hello following example:</span></span>

![Ver el sitio de NGINX seguro en funcionamiento](./media/tutorial-secure-web-server/secured-nginx.png)


## <a name="next-steps"></a><span data-ttu-id="c7b9a-160">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="c7b9a-160">Next steps</span></span>

<span data-ttu-id="c7b9a-161">En este tutorial, protegió un servidor web NGINX con un certificado SSL almacenado en Azure Key Vault.</span><span class="sxs-lookup"><span data-stu-id="c7b9a-161">In this tutorial, you secured an NGINX web server with an SSL certificate stored in Azure Key Vault.</span></span> <span data-ttu-id="c7b9a-162">Ha aprendido a:</span><span class="sxs-lookup"><span data-stu-id="c7b9a-162">You learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="c7b9a-163">Crear una instancia de Azure Key Vault</span><span class="sxs-lookup"><span data-stu-id="c7b9a-163">Create an Azure Key Vault</span></span>
> * <span data-ttu-id="c7b9a-164">Generar o cargar un almacén de claves de certificado toohello</span><span class="sxs-lookup"><span data-stu-id="c7b9a-164">Generate or upload a certificate toohello Key Vault</span></span>
> * <span data-ttu-id="c7b9a-165">Crear una máquina virtual e instale el servidor de web NGINX Hola</span><span class="sxs-lookup"><span data-stu-id="c7b9a-165">Create a VM and install hello NGINX web server</span></span>
> * <span data-ttu-id="c7b9a-166">Insertar certificado de hello en hello VM y configurar NGINX con un enlace SSL</span><span class="sxs-lookup"><span data-stu-id="c7b9a-166">Inject hello certificate into hello VM and configure NGINX with an SSL binding</span></span>

<span data-ttu-id="c7b9a-167">Siga este toosee vínculo pregeneradas ejemplos de script de máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="c7b9a-167">Follow this link toosee pre-built virtual machine script samples.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="c7b9a-168">Ejemplos de scripts de máquina virtual Windows</span><span class="sxs-lookup"><span data-stu-id="c7b9a-168">Windows virtual machine script samples</span></span>](./cli-samples.md)