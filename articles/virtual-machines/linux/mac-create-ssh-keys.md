---
title: "aaaCreate y use un SSH par de claves para máquinas virtuales de Linux en Azure | Documentos de Microsoft"
description: "¿Cómo toocreate y use un par de claves de públicas y privado de SSH para máquinas virtuales Linux en Azure tooimprove Hola seguridad Hola del proceso de autenticación."
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
ms.openlocfilehash: 7fb94841d34d5bc006f3134adf91102ddce5f174
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="how-toocreate-and-use-an-ssh-public-and-private-key-pair-for-linux-vms-in-azure"></a><span data-ttu-id="d2313-103">¿Cómo de pares de toocreate y use una clave pública y privada de SSH para máquinas virtuales de Linux en Azure</span><span class="sxs-lookup"><span data-stu-id="d2313-103">How toocreate and use an SSH public and private key pair for Linux VMs in Azure</span></span>
<span data-ttu-id="d2313-104">Con un par de claves de shell seguro (SSH), puede crear máquinas virtuales (VM) en Azure que utilizan claves SSH para la autenticación, elimina la necesidad de Hola para contraseñas toolog en.</span><span class="sxs-lookup"><span data-stu-id="d2313-104">With a secure shell (SSH) key pair, you can create virtual machines (VMs) in Azure that use SSH keys for authentication, eliminating hello need for passwords toolog in.</span></span> <span data-ttu-id="d2313-105">Este artículo muestra cómo tooquickly generar y usar un par de archivo de clave pública y privada RSA de SSH protocol versión 2 para máquinas virtuales de Linux.</span><span class="sxs-lookup"><span data-stu-id="d2313-105">This article shows you how tooquickly generate and use an SSH protocol version 2 RSA public and private key file pair for Linux VMs.</span></span> <span data-ttu-id="d2313-106">Para obtener más pasos y ejemplos adicionales, consulte [obtener certificados y pares de claves SSH pasos toocreate](create-ssh-keys-detailed.md).</span><span class="sxs-lookup"><span data-stu-id="d2313-106">For more detailed steps and additional examples, see [detailed steps toocreate SSH key pairs and certificates](create-ssh-keys-detailed.md).</span></span>

## <a name="create-an-ssh-key-pair"></a><span data-ttu-id="d2313-107">Creación de un par de claves SSH</span><span class="sxs-lookup"><span data-stu-id="d2313-107">Create an SSH key pair</span></span>
<span data-ttu-id="d2313-108">Hola de uso `ssh-keygen` archivos de comandos toocreate SSH públicos y privados claves mediante el valor predeterminado creado en hello `~/.ssh` directorio, pero puede especificar una ubicación diferente y la frase de contraseña adicional (un contraseña tooaccess Hola archivo de clave privada) cuando se le solicite.</span><span class="sxs-lookup"><span data-stu-id="d2313-108">Use hello `ssh-keygen` command toocreate SSH public and private key files that are by default created in hello `~/.ssh` directory, but you can specify a different location and additional passphrase (a password tooaccess hello private key file) when prompted.</span></span> <span data-ttu-id="d2313-109">Ejecute hello siguiente comando desde un shell de Bash, responder a mensajes de Hola con su propia información.</span><span class="sxs-lookup"><span data-stu-id="d2313-109">Run hello following command from a Bash shell, answering hello prompts with your own information.</span></span>

```bash
ssh-keygen -t rsa -b 2048
```

## <a name="use-hello-ssh-key-pair"></a><span data-ttu-id="d2313-110">Utilice Hola par de claves de SSH</span><span class="sxs-lookup"><span data-stu-id="d2313-110">Use hello SSH key pair</span></span>
<span data-ttu-id="d2313-111">clave pública de Hola que coloque en la VM de Linux en Azure es de forma predeterminada, almacena en `~/.ssh/id_rsa.pub`, a menos que se ha cambiado la ubicación de hello cuando los creó.</span><span class="sxs-lookup"><span data-stu-id="d2313-111">hello public key that you place on your Linux VM in Azure is by default stored in `~/.ssh/id_rsa.pub`, unless you changed hello location when you created them.</span></span> <span data-ttu-id="d2313-112">Si usas hello [CLI de Azure 2.0](/cli/azure) toocreate la máquina virtual, especificar ubicación de Hola de esta clave pública cuando se utiliza hello [crear vm az](/cli/azure/vm#create) con hello `--ssh-key-path` opción.</span><span class="sxs-lookup"><span data-stu-id="d2313-112">If you use hello [Azure CLI 2.0](/cli/azure) toocreate your VM, specify hello location of this public key when you use hello [az vm create](/cli/azure/vm#create) with hello `--ssh-key-path` option.</span></span> <span data-ttu-id="d2313-113">Si copiar y pegar contenido de Hola de toouse del archivo de clave pública de hello en Hola portal de Azure o una plantilla de administrador de recursos, asegúrese de que no se copian ningún espacio en blanco adicional.</span><span class="sxs-lookup"><span data-stu-id="d2313-113">If you copy and paste hello contents of hello public key file toouse in hello Azure portal or a Resource Manager template, make sure you don't copy any additional whitespace.</span></span> <span data-ttu-id="d2313-114">Por ejemplo, si utiliza OS X, se puede canalizar el archivo de clave pública de hello (de forma predeterminada, **~/.ssh/id_rsa.pub**) demasiado**pbcopy** contenido de hello toocopy (no hay otros programas de Linux que Hola lo mismo, por ejemplo, `xclip`).</span><span class="sxs-lookup"><span data-stu-id="d2313-114">For example, if you use OS X, you can pipe hello public key file (by default, **~/.ssh/id_rsa.pub**) too**pbcopy** toocopy hello contents (there are other Linux programs that do hello same thing, such as `xclip`).</span></span>

<span data-ttu-id="d2313-115">Si no está familiarizado con las claves públicas SSH, puede ver su clave pública ejecutando `cat` de la siguiente manera y reemplazando `~/.ssh/id_rsa.pub` por la ubicación de su propio archivo de clave pública:</span><span class="sxs-lookup"><span data-stu-id="d2313-115">If you're not familiar with SSH public keys, you can see your public key by running `cat` as follows, replacing `~/.ssh/id_rsa.pub` with your own public key file location:</span></span>

```bash
cat ~/.ssh/id_rsa.pub
```

<span data-ttu-id="d2313-116">Con la clave pública de hello en la VM de Azure, SSH tooyour VM con Hola dirección IP o nombre DNS de la máquina virtual (recuerde tooreplace `azureuser` y `myvm.westus.cloudapp.azure.com` a continuación con el nombre de usuario de administrador de Hola o una dirección IP y nombre de dominio completo de hello--dirección):</span><span class="sxs-lookup"><span data-stu-id="d2313-116">With hello public key on your Azure VM, SSH tooyour VM using hello IP address or DNS name of your VM (remember tooreplace `azureuser` and `myvm.westus.cloudapp.azure.com` below with hello admin username and hello fully qualified domain name -- or IP address):</span></span>

```bash
ssh azureuser@myvm.westus.cloudapp.azure.com
```

<span data-ttu-id="d2313-117">Si proporciona una frase de contraseña cuando se creó el par de claves, escriba la frase de contraseña de hello cuando se le solicite durante el proceso de inicio de sesión de Hola.</span><span class="sxs-lookup"><span data-stu-id="d2313-117">If you provided a passphrase when you created your key pair, enter hello passphrase when prompted during hello login process.</span></span> <span data-ttu-id="d2313-118">(se agrega el servidor de hello tooyour `~/.ssh/known_hosts` carpeta y no se le pida tooconnect nuevamente hasta la clave pública de hello en los cambios de la máquina virtual de Azure o se quita el nombre del servidor hello de `~/.ssh/known_hosts`.)</span><span class="sxs-lookup"><span data-stu-id="d2313-118">(hello server is added tooyour `~/.ssh/known_hosts` folder, and you won't be asked tooconnect again until hello public key on your Azure VM changes or hello server name is removed from `~/.ssh/known_hosts`.)</span></span>

## <a name="next-steps"></a><span data-ttu-id="d2313-119">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="d2313-119">Next steps</span></span>

<span data-ttu-id="d2313-120">Máquinas virtuales creadas mediante claves SSH están configurados con las contraseñas deshabilitadas de forma predeterminada, fuerza bruta adivinen toomake intenta mucho más caro y, por tanto, difícil.</span><span class="sxs-lookup"><span data-stu-id="d2313-120">VMs created using SSH keys are by default configured with passwords disabled, toomake brute-forced guessing attempts vastly more expensive and therefore difficult.</span></span> <span data-ttu-id="d2313-121">En este tema se describe cómo crear un par de claves SSH simple para uso rápido.</span><span class="sxs-lookup"><span data-stu-id="d2313-121">This topic describes creating a simple SSH key pair for quick usage.</span></span> <span data-ttu-id="d2313-122">Si necesita más ayuda para crear el par de claves de SSH o requieren certificados adicionales, consulte [obtener certificados y pares de claves SSH pasos toocreate](create-ssh-keys-detailed.md).</span><span class="sxs-lookup"><span data-stu-id="d2313-122">If you need more assistance in creating your SSH key pair or require additional certificates, see [Detailed steps toocreate SSH key pairs and certificates](create-ssh-keys-detailed.md).</span></span>

<span data-ttu-id="d2313-123">Puede crear máquinas virtuales que usan el par de claves de SSH mediante Hola portal de Azure, CLI y plantillas:</span><span class="sxs-lookup"><span data-stu-id="d2313-123">You can create VMs that use your SSH key pair using hello Azure portal, CLI, and templates:</span></span>

* [<span data-ttu-id="d2313-124">Crear una VM de Linux segura mediante Hola portal de Azure</span><span class="sxs-lookup"><span data-stu-id="d2313-124">Create a secure Linux VM using hello Azure portal</span></span>](quick-create-portal.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [<span data-ttu-id="d2313-125">Crear una VM de Linux segura mediante hello Azure CLI 2.0)</span><span class="sxs-lookup"><span data-stu-id="d2313-125">Create a secure Linux VM using hello Azure CLI 2.0)</span></span>](quick-create-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [<span data-ttu-id="d2313-126">Creación de una máquina virtual Linux protegida mediante una plantilla de Azure</span><span class="sxs-lookup"><span data-stu-id="d2313-126">Create a secure Linux VM using an Azure template</span></span>](create-ssh-secured-vm-from-template.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
