---
title: "Creación y uso de un par de claves SSH para máquinas virtuales Linux en Azure | Microsoft Docs"
description: "Creación y uso de un par de claves SSH pública y privada para máquinas virtuales Linux en Azure para mejorar la seguridad del proceso de autenticación."
services: virtual-machines-linux
documentationcenter: 
author: iainfoulds
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 34ae9482-da3e-4b2d-9d0d-9d672aa42498
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: get-started-article
ms.date: 08/14/2017
ms.author: iainfou
ms.openlocfilehash: 0fb71d2ffe533afba6e1e527b727a7b085e7da14
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/18/2017
---
# <a name="how-to-create-and-use-an-ssh-public-and-private-key-pair-for-linux-vms-in-azure"></a><span data-ttu-id="abd15-103">Creación y uso de un par de claves SSH pública y privada para máquinas virtuales Linux en Azure</span><span class="sxs-lookup"><span data-stu-id="abd15-103">How to create and use an SSH public and private key pair for Linux VMs in Azure</span></span>
<span data-ttu-id="abd15-104">Con un par de claves de shell seguro (SSH), puede crear máquinas virtuales en Azure que usen claves SSH para autenticación, lo que elimina la necesidad de usar contraseñas para iniciar sesión.</span><span class="sxs-lookup"><span data-stu-id="abd15-104">With a secure shell (SSH) key pair, you can create virtual machines (VMs) in Azure that use SSH keys for authentication, eliminating the need for passwords to log in.</span></span> <span data-ttu-id="abd15-105">En este artículo se muestra cómo generar y usar rápidamente un par de archivos de clave pública y privada en formato RSA versión 2 del protocolo SSH para máquinas virtuales Linux.</span><span class="sxs-lookup"><span data-stu-id="abd15-105">This article shows you how to quickly generate and use an SSH protocol version 2 RSA public and private key file pair for Linux VMs.</span></span> <span data-ttu-id="abd15-106">Para pasos más detallados y ejemplos adicionales, consulte los [pasos detallados para crear pares de claves SSH y certificados](create-ssh-keys-detailed.md).</span><span class="sxs-lookup"><span data-stu-id="abd15-106">For more detailed steps and additional examples, see [detailed steps to create SSH key pairs and certificates](create-ssh-keys-detailed.md).</span></span>

## <a name="create-an-ssh-key-pair"></a><span data-ttu-id="abd15-107">Creación de un par de claves SSH</span><span class="sxs-lookup"><span data-stu-id="abd15-107">Create an SSH key pair</span></span>
<span data-ttu-id="abd15-108">Use el comando `ssh-keygen` para crear los archivos de clave SSH pública y privada que se crean de forma predeterminada en el directorio `~/.ssh`. Puede especificar una ubicación diferente y una frase de contraseña adicional (una contraseña para acceder al archivo de clave privada) cuando se le solicite.</span><span class="sxs-lookup"><span data-stu-id="abd15-108">Use the `ssh-keygen` command to create SSH public and private key files that are by default created in the `~/.ssh` directory, but you can specify a different location and additional passphrase (a password to access the private key file) when prompted.</span></span> <span data-ttu-id="abd15-109">Ejecute el siguiente comando desde un shell de Bash y responda a los mensajes con su propia información.</span><span class="sxs-lookup"><span data-stu-id="abd15-109">Run the following command from a Bash shell, answering the prompts with your own information.</span></span>

```bash
ssh-keygen -t rsa -b 2048
```

## <a name="use-the-ssh-key-pair"></a><span data-ttu-id="abd15-110">Uso de un par de claves SSH</span><span class="sxs-lookup"><span data-stu-id="abd15-110">Use the SSH key pair</span></span>
<span data-ttu-id="abd15-111">La clave pública que coloca en la máquina virtual Linux en Azure se almacena de forma predeterminada en `~/.ssh/id_rsa.pub`, a menos que cambiara la ubicación cuando la creó.</span><span class="sxs-lookup"><span data-stu-id="abd15-111">The public key that you place on your Linux VM in Azure is by default stored in `~/.ssh/id_rsa.pub`, unless you changed the location when you created them.</span></span> <span data-ttu-id="abd15-112">Si usa la [CLI de Azure 2.0](/cli/azure) para crear la máquina virtual, especifique la ubicación de esta clave pública cuando use [az vm create](/cli/azure/vm#create) con la opción `--ssh-key-path`.</span><span class="sxs-lookup"><span data-stu-id="abd15-112">If you use the [Azure CLI 2.0](/cli/azure) to create your VM, specify the location of this public key when you use the [az vm create](/cli/azure/vm#create) with the `--ssh-key-path` option.</span></span> <span data-ttu-id="abd15-113">Si copia y pega el contenido del archivo de clave pública para usarlo en Azure Portal o en una plantilla de Resource Manager, asegúrese de no copiar ningún espacio en blanco adicional.</span><span class="sxs-lookup"><span data-stu-id="abd15-113">If you copy and paste the contents of the public key file to use in the Azure portal or a Resource Manager template, make sure you don't copy any additional whitespace.</span></span> <span data-ttu-id="abd15-114">Por ejemplo, si utiliza OS X, puede canalizar el archivo de clave pública (de forma predeterminada, **~/.ssh/id_rsa.pub**) hacia **pbcopy** para copiar el contenido (hay otros programas de Linux que hacen lo mismo que `xclip`).</span><span class="sxs-lookup"><span data-stu-id="abd15-114">For example, if you use OS X, you can pipe the public key file (by default, **~/.ssh/id_rsa.pub**) to **pbcopy** to copy the contents (there are other Linux programs that do the same thing, such as `xclip`).</span></span>

<span data-ttu-id="abd15-115">Si no está familiarizado con las claves públicas SSH, puede ver su clave pública ejecutando `cat` de la siguiente manera y reemplazando `~/.ssh/id_rsa.pub` por la ubicación de su propio archivo de clave pública:</span><span class="sxs-lookup"><span data-stu-id="abd15-115">If you're not familiar with SSH public keys, you can see your public key by running `cat` as follows, replacing `~/.ssh/id_rsa.pub` with your own public key file location:</span></span>

```bash
cat ~/.ssh/id_rsa.pub
```

<span data-ttu-id="abd15-116">Con la clave pública en la máquina virtual de Azure, SSH en la máquina virtual mediante la dirección IP o el nombre DNS de la máquina virtual (no olvide reemplazar `azureuser` y `myvm.westus.cloudapp.azure.com` que aparecen a continuación por el nombre de usuario y el nombre de dominio completo, o la dirección IP):</span><span class="sxs-lookup"><span data-stu-id="abd15-116">With the public key on your Azure VM, SSH to your VM using the IP address or DNS name of your VM (remember to replace `azureuser` and `myvm.westus.cloudapp.azure.com` below with the admin username and the fully qualified domain name -- or IP address):</span></span>

```bash
ssh azureuser@myvm.westus.cloudapp.azure.com
```

<span data-ttu-id="abd15-117">Si proporcionó una frase de contraseña cuando creó el par de claves, escríbala cuando se le solicite durante el proceso de inicio de sesión.</span><span class="sxs-lookup"><span data-stu-id="abd15-117">If you provided a passphrase when you created your key pair, enter the passphrase when prompted during the login process.</span></span> <span data-ttu-id="abd15-118">(El servidor se agrega a la carpeta `~/.ssh/known_hosts` y no se le pedirá que se conecte de nuevo hasta que la clave pública de la máquina virtual de Azure cambie o se quite el nombre del servidor de `~/.ssh/known_hosts`).</span><span class="sxs-lookup"><span data-stu-id="abd15-118">(The server is added to your `~/.ssh/known_hosts` folder, and you won't be asked to connect again until the public key on your Azure VM changes or the server name is removed from `~/.ssh/known_hosts`.)</span></span>

## <a name="next-steps"></a><span data-ttu-id="abd15-119">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="abd15-119">Next steps</span></span>

<span data-ttu-id="abd15-120">Las máquinas virtuales creadas con claves SSH están configuradas de forma predeterminada con las contraseñas deshabilitadas, a fin de evitar los intentos de adivinarlas por fuerza bruta que resultan bastante más caros y más complejos.</span><span class="sxs-lookup"><span data-stu-id="abd15-120">VMs created using SSH keys are by default configured with passwords disabled, to make brute-forced guessing attempts vastly more expensive and therefore difficult.</span></span> <span data-ttu-id="abd15-121">En este tema se describe cómo crear un par de claves SSH simple para uso rápido.</span><span class="sxs-lookup"><span data-stu-id="abd15-121">This topic describes creating a simple SSH key pair for quick usage.</span></span> <span data-ttu-id="abd15-122">Si necesita más ayuda para crear el par de claves SSH o requiere más certificados, consulte los [pasos detallados para crear pares de claves SSH y certificados](create-ssh-keys-detailed.md).</span><span class="sxs-lookup"><span data-stu-id="abd15-122">If you need more assistance in creating your SSH key pair or require additional certificates, see [Detailed steps to create SSH key pairs and certificates](create-ssh-keys-detailed.md).</span></span>

<span data-ttu-id="abd15-123">También puede crear máquinas virtuales que usen el par de claves SSH mediante Azure Portal, la CLI y las plantillas:</span><span class="sxs-lookup"><span data-stu-id="abd15-123">You can create VMs that use your SSH key pair using the Azure portal, CLI, and templates:</span></span>

* [<span data-ttu-id="abd15-124">Creación de una máquina virtual Linux protegida mediante el Portal de Azure</span><span class="sxs-lookup"><span data-stu-id="abd15-124">Create a secure Linux VM using the Azure portal</span></span>](quick-create-portal.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [<span data-ttu-id="abd15-125">Creación de una máquina virtual Linux segura mediante la CLI de Azure 2.0</span><span class="sxs-lookup"><span data-stu-id="abd15-125">Create a secure Linux VM using the Azure CLI 2.0)</span></span>](quick-create-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [<span data-ttu-id="abd15-126">Creación de una máquina virtual Linux protegida mediante una plantilla de Azure</span><span class="sxs-lookup"><span data-stu-id="abd15-126">Create a secure Linux VM using an Azure template</span></span>](create-ssh-secured-vm-from-template.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
