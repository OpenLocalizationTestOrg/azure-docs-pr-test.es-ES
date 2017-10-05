---
title: "Protección de un servidor web con certificados SSL en Azure | Microsoft Docs"
description: "Aprenda a proteger el servidor web NGINX con certificados SSL en una máquina virtual Linux en Azure"
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
ms.openlocfilehash: 181be35aeb61020db3abaeba22aa882848923c31
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/29/2017
---
# <a name="secure-a-web-server-with-ssl-certificates-on-a-linux-virtual-machine-in-azure"></a><span data-ttu-id="26462-103">Protección de un servidor web con certificados SSL en una máquina virtual Linux en Azure</span><span class="sxs-lookup"><span data-stu-id="26462-103">Secure a web server with SSL certificates on a Linux virtual machine in Azure</span></span>
<span data-ttu-id="26462-104">Para proteger los servidores web, se puede utilizar un certificado Capa de sockets seguros (SSL) para cifrar el tráfico web.</span><span class="sxs-lookup"><span data-stu-id="26462-104">To secure web servers, a Secure Sockets Later (SSL) certificate can be used to encrypt web traffic.</span></span> <span data-ttu-id="26462-105">Estos certificados SSL pueden almacenarse en Azure Key Vault y permiten implementaciones seguras de certificados en máquinas virtuales Linux en Azure.</span><span class="sxs-lookup"><span data-stu-id="26462-105">These SSL certificates can be stored in Azure Key Vault, and allow secure deployments of certificates to Linux virtual machines (VMs) in Azure.</span></span> <span data-ttu-id="26462-106">En este tutorial, aprenderá a:</span><span class="sxs-lookup"><span data-stu-id="26462-106">In this tutorial you learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="26462-107">Crear una instancia de Azure Key Vault</span><span class="sxs-lookup"><span data-stu-id="26462-107">Create an Azure Key Vault</span></span>
> * <span data-ttu-id="26462-108">Generar o cargar un certificado en Key Vault</span><span class="sxs-lookup"><span data-stu-id="26462-108">Generate or upload a certificate to the Key Vault</span></span>
> * <span data-ttu-id="26462-109">Creación de una máquina virtual e instalación del servidor web NGINX</span><span class="sxs-lookup"><span data-stu-id="26462-109">Create a VM and install the NGINX web server</span></span>
> * <span data-ttu-id="26462-110">Inserción del certificado en la máquina virtual y configuración de NGINX con un enlace SSL</span><span class="sxs-lookup"><span data-stu-id="26462-110">Inject the certificate into the VM and configure NGINX with an SSL binding</span></span>

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="26462-111">Si decide instalar y usar la CLI localmente, para este tutorial es preciso que ejecute la CLI de Azure versión 2.0.4 o posterior.</span><span class="sxs-lookup"><span data-stu-id="26462-111">If you choose to install and use the CLI locally, this tutorial requires that you are running the Azure CLI version 2.0.4 or later.</span></span> <span data-ttu-id="26462-112">Ejecute `az --version` para encontrar la versión.</span><span class="sxs-lookup"><span data-stu-id="26462-112">Run `az --version` to find the version.</span></span> <span data-ttu-id="26462-113">Si necesita instalarla o actualizarla, consulte [Instalación de la CLI de Azure 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="26462-113">If you need to install or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span>  


## <a name="overview"></a><span data-ttu-id="26462-114">Información general</span><span class="sxs-lookup"><span data-stu-id="26462-114">Overview</span></span>
<span data-ttu-id="26462-115">Azure Key Vault protege claves y secretos criptográficos, como certificados y contraseñas.</span><span class="sxs-lookup"><span data-stu-id="26462-115">Azure Key Vault safeguards cryptographic keys and secrets, such certificates or passwords.</span></span> <span data-ttu-id="26462-116">Key Vault ayuda a agilizar el proceso de administración de certificados y le permite mantener el control de las claves que acceden a ellos.</span><span class="sxs-lookup"><span data-stu-id="26462-116">Key Vault helps streamline the certificate management process and enables you to maintain control of keys that access those certificates.</span></span> <span data-ttu-id="26462-117">Puede crear un certificado autofirmado en Key Vault o cargar un certificado de confianza existente que ya posea.</span><span class="sxs-lookup"><span data-stu-id="26462-117">You can create a self-signed certificate inside Key Vault, or upload an existing, trusted certificate that you already own.</span></span>

<span data-ttu-id="26462-118">En lugar de usar una imagen de máquina virtual personalizada que incluya los certificados preparados, inserta los certificados en una máquina virtual en ejecución.</span><span class="sxs-lookup"><span data-stu-id="26462-118">Rather than using a custom VM image that includes certificates baked-in, you inject certificates into a running VM.</span></span> <span data-ttu-id="26462-119">Este proceso garantiza que los certificados más actualizados se instalan en un servidor web durante la implementación.</span><span class="sxs-lookup"><span data-stu-id="26462-119">This process ensures that the most up-to-date certificates are installed on a web server during deployment.</span></span> <span data-ttu-id="26462-120">Si renueva o reemplaza un certificado, no tiene también que crear una nueva imagen de máquina virtual personalizada.</span><span class="sxs-lookup"><span data-stu-id="26462-120">If you renew or replace a certificate, you don't also have to create a new custom VM image.</span></span> <span data-ttu-id="26462-121">Los certificados más recientes se insertan automáticamente a medida que se crean máquinas virtuales adicionales.</span><span class="sxs-lookup"><span data-stu-id="26462-121">The latest certificates are automatically injected as you create additional VMs.</span></span> <span data-ttu-id="26462-122">Durante el proceso completo, el certificado nunca deja la plataforma de Azure ni se expone en un script, historial de la línea de comandos o una plantilla.</span><span class="sxs-lookup"><span data-stu-id="26462-122">During the whole process, the certificates never leave the Azure platform or are exposed in a script, command-line history, or template.</span></span>


## <a name="create-an-azure-key-vault"></a><span data-ttu-id="26462-123">Crear una instancia de Azure Key Vault</span><span class="sxs-lookup"><span data-stu-id="26462-123">Create an Azure Key Vault</span></span>
<span data-ttu-id="26462-124">Para poder crear una instancia de Key Vault y certificados, cree un grupo de recursos con [az group create](/cli/azure/group#create).</span><span class="sxs-lookup"><span data-stu-id="26462-124">Before you can create a Key Vault and certificates, create a resource group with [az group create](/cli/azure/group#create).</span></span> <span data-ttu-id="26462-125">En el ejemplo siguiente, se crea un grupo de recursos denominado *myResourceGroupSecureWeb* en la ubicación *eastus*:</span><span class="sxs-lookup"><span data-stu-id="26462-125">The following example creates a resource group named *myResourceGroupSecureWeb* in the *eastus* location:</span></span>

```azurecli-interactive 
az group create --name myResourceGroupSecureWeb --location eastus
```

<span data-ttu-id="26462-126">Después, cree una instancia de Key Vault con [az keyvault create](/cli/azure/keyvault#create) y habilítela para usarla al implementar una máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="26462-126">Next, create a Key Vault with [az keyvault create](/cli/azure/keyvault#create) and enable it for use when you deploy a VM.</span></span> <span data-ttu-id="26462-127">Cada instancia de Key Vault requiere un nombre único, que debe estar todo en minúsculas.</span><span class="sxs-lookup"><span data-stu-id="26462-127">Each Key Vault requires a unique name, and should be all lower case.</span></span> <span data-ttu-id="26462-128">Reemplace *<mykeyvault>* en el siguiente ejemplo por su propio nombre único de Key Vault:</span><span class="sxs-lookup"><span data-stu-id="26462-128">Replace *<mykeyvault>* in the following example with your own unique Key Vault name:</span></span>

```azurecli-interactive 
keyvault_name=<mykeyvault>
az keyvault create \
    --resource-group myResourceGroupSecureWeb \
    --name $keyvault_name \
    --enabled-for-deployment
```

## <a name="generate-a-certificate-and-store-in-key-vault"></a><span data-ttu-id="26462-129">Generación de un certificado y almacenamiento en Key Vault</span><span class="sxs-lookup"><span data-stu-id="26462-129">Generate a certificate and store in Key Vault</span></span>
<span data-ttu-id="26462-130">Para usarlo en producción, debe importar un certificado válido firmado por un proveedor de confianza con [az keyvault certificate import](/cli/azure/certificate#import).</span><span class="sxs-lookup"><span data-stu-id="26462-130">For production use, you should import a valid certificate signed by trusted provider with [az keyvault certificate import](/cli/azure/certificate#import).</span></span> <span data-ttu-id="26462-131">En este tutorial, el ejemplo siguiente muestra cómo puede generar un certificado autofirmado con [az keyvault certificate create](/cli/azure/certificate#create) que usa la directiva de certificado predeterminada:</span><span class="sxs-lookup"><span data-stu-id="26462-131">For this tutorial, the following example shows how you can generate a self-signed certificate with [az keyvault certificate create](/cli/azure/certificate#create) that uses the default certificate policy:</span></span>

```azurecli-interactive 
az keyvault certificate create \
    --vault-name $keyvault_name \
    --name mycert \
    --policy "$(az keyvault certificate get-default-policy)"
```

### <a name="prepare-a-certificate-for-use-with-a-vm"></a><span data-ttu-id="26462-132">Preparación del certificado para usarlo con una máquina virtual</span><span class="sxs-lookup"><span data-stu-id="26462-132">Prepare a certificate for use with a VM</span></span>
<span data-ttu-id="26462-133">Para usar el certificado durante el proceso de creación de la máquina virtual, obtenga el id. del certificado con [az keyvault secret list-versions](/cli/azure/keyvault/secret#list-versions).</span><span class="sxs-lookup"><span data-stu-id="26462-133">To use the certificate during the VM create process, obtain the ID of your certificate with [az keyvault secret list-versions](/cli/azure/keyvault/secret#list-versions).</span></span> <span data-ttu-id="26462-134">Convierta el certificado con [az vm format-secret](/cli/azure/vm#format-secret).</span><span class="sxs-lookup"><span data-stu-id="26462-134">Convert the certificate with [az vm format-secret](/cli/azure/vm#format-secret).</span></span> <span data-ttu-id="26462-135">En el ejemplo siguiente se asigna la salida de estos comandos a las variables para facilitar su uso en los pasos siguientes:</span><span class="sxs-lookup"><span data-stu-id="26462-135">The following example assigns the output of these commands to variables for ease of use in the next steps:</span></span>

```azurecli-interactive 
secret=$(az keyvault secret list-versions \
          --vault-name $keyvault_name \
          --name mycert \
          --query "[?attributes.enabled].id" --output tsv)
vm_secret=$(az vm format-secret --secret "$secret")
```

### <a name="create-a-cloud-init-config-to-secure-nginx"></a><span data-ttu-id="26462-136">Creación de una configuración de cloud-init para proteger NGINX</span><span class="sxs-lookup"><span data-stu-id="26462-136">Create a cloud-init config to secure NGINX</span></span>
<span data-ttu-id="26462-137">[cloud-init](https://cloudinit.readthedocs.io) es un enfoque ampliamente usado para personalizar una máquina virtual Linux la primera vez que se arranca.</span><span class="sxs-lookup"><span data-stu-id="26462-137">[Cloud-init](https://cloudinit.readthedocs.io) is a widely used approach to customize a Linux VM as it boots for the first time.</span></span> <span data-ttu-id="26462-138">Puede usar cloud-init para instalar paquetes y escribir archivos o para configurar los usuarios y la seguridad.</span><span class="sxs-lookup"><span data-stu-id="26462-138">You can use cloud-init to install packages and write files, or to configure users and security.</span></span> <span data-ttu-id="26462-139">Como cloud-init se ejecuta durante el proceso de arranque inicial, no hay pasos adicionales o agentes requeridos que aplicar a la configuración.</span><span class="sxs-lookup"><span data-stu-id="26462-139">As cloud-init runs during the initial boot process, there are no additional steps or required agents to apply your configuration.</span></span>

<span data-ttu-id="26462-140">Cuando crea una máquina virtual, los certificados y las claves se almacenan en el directorio */var/lib/waagent/* protegido.</span><span class="sxs-lookup"><span data-stu-id="26462-140">When you create a VM, certificates and keys are stored in the protected */var/lib/waagent/* directory.</span></span> <span data-ttu-id="26462-141">Para automatizar la adición del certificado a la máquina virtual y configurar el servidor web, utilice cloud-init.</span><span class="sxs-lookup"><span data-stu-id="26462-141">To automate adding the certificate to the VM and configuring the web server, use cloud-init.</span></span> <span data-ttu-id="26462-142">En este ejemplo, se instala y configura el servidor web NGINX.</span><span class="sxs-lookup"><span data-stu-id="26462-142">In this example, we install and configure the NGINX web server.</span></span> <span data-ttu-id="26462-143">Puede usar el mismo proceso para instalar y configurar Apache.</span><span class="sxs-lookup"><span data-stu-id="26462-143">You can use the same process to install and configure Apache.</span></span> 

<span data-ttu-id="26462-144">Cree un archivo denominado *cloud-init-web-server.txt* y pegue la siguiente configuración:</span><span class="sxs-lookup"><span data-stu-id="26462-144">Create a file named *cloud-init-web-server.txt* and paste the following configuration:</span></span>

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

### <a name="create-a-secure-vm"></a><span data-ttu-id="26462-145">Creación de una máquina virtual segura</span><span class="sxs-lookup"><span data-stu-id="26462-145">Create a secure VM</span></span>
<span data-ttu-id="26462-146">Ahora cree una máquina virtual con el comando [az vm create](/cli/azure/vm#create).</span><span class="sxs-lookup"><span data-stu-id="26462-146">Now create a VM with [az vm create](/cli/azure/vm#create).</span></span> <span data-ttu-id="26462-147">Los datos del certificado se insertan desde Key Vault con el parámetro `--secrets`.</span><span class="sxs-lookup"><span data-stu-id="26462-147">The certificate data is injected from Key Vault with the `--secrets` parameter.</span></span> <span data-ttu-id="26462-148">Pase la configuración cloud-init con el parámetro `--custom-data`:</span><span class="sxs-lookup"><span data-stu-id="26462-148">You pass in the cloud-init config with the `--custom-data` parameter:</span></span>

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

<span data-ttu-id="26462-149">Transcurren unos minutos hasta que la máquina virtual se crea, los paquetes se instalan y la aplicación se inicia.</span><span class="sxs-lookup"><span data-stu-id="26462-149">It takes a few minutes for the VM to be created, the packages to install, and the app to start.</span></span> <span data-ttu-id="26462-150">Cuando se haya creado la máquina virtual, anote el valor `publicIpAddress` mostrado por la CLI de Azure.</span><span class="sxs-lookup"><span data-stu-id="26462-150">When the VM has been created, take note of the `publicIpAddress` displayed by the Azure CLI.</span></span> <span data-ttu-id="26462-151">Esta dirección se usa para acceder al sitio en un explorador web.</span><span class="sxs-lookup"><span data-stu-id="26462-151">This address is used to access your site in a web browser.</span></span>

<span data-ttu-id="26462-152">Para permitir que el tráfico web llegue a la máquina virtual, abra el puerto 443 desde Internet con el comando [az vm open-port](/cli/azure/vm#open-port):</span><span class="sxs-lookup"><span data-stu-id="26462-152">To allow secure web traffic to reach your VM, open port 443 from the Internet with [az vm open-port](/cli/azure/vm#open-port):</span></span>

```azurecli-interactive 
az vm open-port \
    --resource-group myResourceGroupSecureWeb \
    --name myVM \
    --port 443
```


### <a name="test-the-secure-web-app"></a><span data-ttu-id="26462-153">Prueba de la aplicación web segura</span><span class="sxs-lookup"><span data-stu-id="26462-153">Test the secure web app</span></span>
<span data-ttu-id="26462-154">Ahora puede abrir un explorador web y escribir *https://<publicIpAddress>* en la barra de direcciones.</span><span class="sxs-lookup"><span data-stu-id="26462-154">Now you can open a web browser and enter *https://<publicIpAddress>* in the address bar.</span></span> <span data-ttu-id="26462-155">Proporcione su propia dirección IP pública obtenida del proceso de creación de la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="26462-155">Provide your own public IP address from the VM create process.</span></span> <span data-ttu-id="26462-156">Acepte la advertencia de seguridad si usó un certificado autofirmado:</span><span class="sxs-lookup"><span data-stu-id="26462-156">Accept the security warning if you used a self-signed certificate:</span></span>

![Aceptar la advertencia de seguridad del explorador web](./media/tutorial-secure-web-server/browser-warning.png)

<span data-ttu-id="26462-158">A continuación, se muestra el sitio de NGINX protegido, como en el ejemplo siguiente:</span><span class="sxs-lookup"><span data-stu-id="26462-158">Your secured NGINX site is then displayed as in the following example:</span></span>

![Ver el sitio de NGINX seguro en funcionamiento](./media/tutorial-secure-web-server/secured-nginx.png)


## <a name="next-steps"></a><span data-ttu-id="26462-160">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="26462-160">Next steps</span></span>

<span data-ttu-id="26462-161">En este tutorial, protegió un servidor web NGINX con un certificado SSL almacenado en Azure Key Vault.</span><span class="sxs-lookup"><span data-stu-id="26462-161">In this tutorial, you secured an NGINX web server with an SSL certificate stored in Azure Key Vault.</span></span> <span data-ttu-id="26462-162">Ha aprendido a:</span><span class="sxs-lookup"><span data-stu-id="26462-162">You learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="26462-163">Crear una instancia de Azure Key Vault</span><span class="sxs-lookup"><span data-stu-id="26462-163">Create an Azure Key Vault</span></span>
> * <span data-ttu-id="26462-164">Generar o cargar un certificado en Key Vault</span><span class="sxs-lookup"><span data-stu-id="26462-164">Generate or upload a certificate to the Key Vault</span></span>
> * <span data-ttu-id="26462-165">Creación de una máquina virtual e instalación del servidor web NGINX</span><span class="sxs-lookup"><span data-stu-id="26462-165">Create a VM and install the NGINX web server</span></span>
> * <span data-ttu-id="26462-166">Inserción del certificado en la máquina virtual y configuración de NGINX con un enlace SSL</span><span class="sxs-lookup"><span data-stu-id="26462-166">Inject the certificate into the VM and configure NGINX with an SSL binding</span></span>

<span data-ttu-id="26462-167">Siga este vínculo para ver ejemplos de scripts de máquina virtual creados previamente.</span><span class="sxs-lookup"><span data-stu-id="26462-167">Follow this link to see pre-built virtual machine script samples.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="26462-168">Ejemplos de scripts de máquina virtual Windows</span><span class="sxs-lookup"><span data-stu-id="26462-168">Windows virtual machine script samples</span></span>](./cli-samples.md)