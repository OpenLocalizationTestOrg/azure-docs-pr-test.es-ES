---
title: aaaAdd un tooa de usuario Linux VM en Azure | Documentos de Microsoft
description: Agregar una VM de Linux tooa de usuario en Azure.
services: virtual-machines-linux
documentationcenter: 
author: vlivech
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: f8aa633b-8b75-45d7-b61d-11ac112cedd5
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 08/18/2016
ms.author: v-livech
ms.openlocfilehash: eed050154adf0cbed2c168e7aa675bd3ded85fcd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="add-a-user-tooan-azure-vm"></a><span data-ttu-id="0cca4-103">Agregar una máquina virtual de Azure tooan de usuario</span><span class="sxs-lookup"><span data-stu-id="0cca4-103">Add a user tooan Azure VM</span></span>
<span data-ttu-id="0cca4-104">Una de las primeras tareas de Hola en cualquier nueva VM de Linux es toocreate un nuevo usuario.</span><span class="sxs-lookup"><span data-stu-id="0cca4-104">One of hello first tasks on any new Linux VM is toocreate a new user.</span></span>  <span data-ttu-id="0cca4-105">En este artículo, le guían por la creación de una cuenta de usuario de sudo, establecer la contraseña de hello, añadir claves públicas SSH y finalmente utilizar `visudo` tooallow sudo sin una contraseña.</span><span class="sxs-lookup"><span data-stu-id="0cca4-105">In this article, we walk through creating a sudo user account, setting hello password, adding SSH Public Keys, and finally use `visudo` tooallow sudo without a password.</span></span>

<span data-ttu-id="0cca4-106">Requisitos previos son: [una cuenta de Azure](https://azure.microsoft.com/pricing/free-trial/), [claves públicas y privadas de SSH](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json), un grupo de recursos de Azure y hello Azure CLI instalados y se cambia el modo de administrador de recursos de tooAzure mediante `azure config mode arm`.</span><span class="sxs-lookup"><span data-stu-id="0cca4-106">Prerequisites are: [an Azure account](https://azure.microsoft.com/pricing/free-trial/), [SSH public and private keys](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json), an Azure resource group, and hello Azure CLI installed and switched tooAzure Resource Manager mode using `azure config mode arm`.</span></span>

## <a name="quick-commands"></a><span data-ttu-id="0cca4-107">Comandos rápidos</span><span class="sxs-lookup"><span data-stu-id="0cca4-107">Quick Commands</span></span>
```bash
# Add a new user on RedHat family distros
sudo useradd -G wheel exampleUser

# Add a new user on Debian family distros
sudo useradd -G sudo exampleUser

# Set a password
sudo passwd exampleUser
Enter new UNIX password:
Retype new UNIX password:
passwd: password updated successfully

# Copy hello SSH Public Key toohello new user
ssh-copy-id -i ~/.ssh/id_rsa exampleuser@exampleserver

# Change sudoers tooallow no password
# Execute visudo as root tooedit hello /etc/sudoers file
visudo

# On RedHat family distros uncomment this line:
## Same thing without a password
# %wheel        ALL=(ALL)       NOPASSWD: ALL

# toothis
## Same thing without a password
%wheel        ALL=(ALL)       NOPASSWD: ALL

# On Debian family distros change this line:
# Allow members of group sudo tooexecute any command
%sudo   ALL=(ALL:ALL) ALL

# toothis
%sudo   ALL=(ALL) NOPASSWD:ALL

# Verify everything
# Verify hello SSH keys & User account
bill@slackware$ ssh -i ~/.ssh/id_rsa exampleuser@exampleserver

# Verify sudo access
sudo top
```

## <a name="detailed-walkthrough"></a><span data-ttu-id="0cca4-108">Tutorial detallado</span><span class="sxs-lookup"><span data-stu-id="0cca4-108">Detailed Walkthrough</span></span>
### <a name="introduction"></a><span data-ttu-id="0cca4-109">Introducción</span><span class="sxs-lookup"><span data-stu-id="0cca4-109">Introduction</span></span>
<span data-ttu-id="0cca4-110">Una tarea primera y más común de hello con un nuevo servidor es tooadd una cuenta de usuario.</span><span class="sxs-lookup"><span data-stu-id="0cca4-110">One of hello first and most common task with a new server is tooadd a user account.</span></span>  <span data-ttu-id="0cca4-111">Se deben deshabilitar los inicios de sesión de raíz y propia cuenta de raíz hello no debe usarse con el servidor Linux, sólo sudo.</span><span class="sxs-lookup"><span data-stu-id="0cca4-111">Root logins should be disabled and hello root account itself should not be used with your Linux server, only sudo.</span></span>  <span data-ttu-id="0cca4-112">Otorgar privilegios con sudo se Hola tooadminister de manera adecuada y usar Linux a una extensión de la raíz de usuario.</span><span class="sxs-lookup"><span data-stu-id="0cca4-112">Giving a user root escalation privileges using sudo it hello proper way tooadminister and use Linux.</span></span>

<span data-ttu-id="0cca4-113">Mediante el comando hello `useradd` vamos a agregar cuentas de usuario toohello VM de Linux.</span><span class="sxs-lookup"><span data-stu-id="0cca4-113">Using hello command `useradd` we are adding user accounts toohello Linux VM.</span></span>  <span data-ttu-id="0cca4-114">Si se ejecuta `useradd`, se modifica `/etc/passwd`, `/etc/shadow`, `/etc/group` y `/etc/gshadow`.</span><span class="sxs-lookup"><span data-stu-id="0cca4-114">Running `useradd` modifies `/etc/passwd`, `/etc/shadow`, `/etc/group`, and `/etc/gshadow`.</span></span>  <span data-ttu-id="0cca4-115">Vamos a agregar un indicador de línea de comandos toohello `useradd` comando tooalso agregar Hola nuevo toohello sudo correcto grupo de usuarios en Linux.</span><span class="sxs-lookup"><span data-stu-id="0cca4-115">We are adding a command-line flag toohello `useradd` command tooalso add hello new user toohello proper sudo group on Linux.</span></span>  <span data-ttu-id="0cca4-116">Incluso tú `useradd` crea una entrada en `/etc/passwd` nueva cuenta de usuario de hello no se ofrecerá una contraseña.</span><span class="sxs-lookup"><span data-stu-id="0cca4-116">Even thou `useradd` creates an entry into `/etc/passwd` it does not give hello new user account a password.</span></span>  <span data-ttu-id="0cca4-117">Vamos a crear una contraseña inicial Hola nuevo usuario con simple hello `passwd` comando.</span><span class="sxs-lookup"><span data-stu-id="0cca4-117">We are creating an initial password for hello new user using hello simple `passwd` command.</span></span>  <span data-ttu-id="0cca4-118">Hola último paso es toomodify hello sudo reglas tooallow que comandos de tooexecute de usuario con privilegios sudo sin necesidad de tooenter una contraseña para todos los comandos.</span><span class="sxs-lookup"><span data-stu-id="0cca4-118">hello last step is toomodify hello sudo rules tooallow that user tooexecute commands with sudo privileges without having tooenter a password for every command.</span></span>  <span data-ttu-id="0cca4-119">Iniciar sesión con la clave privada de Hola se supone que esa cuenta de usuario está protegida de actores no válidos y se va tooallow sudo acceso sin una contraseña.</span><span class="sxs-lookup"><span data-stu-id="0cca4-119">Logging in using hello Private key we are assuming that user account is safe from bad actors and are going tooallow sudo access without a password.</span></span>  

### <a name="adding-a-single-sudo-user-tooan-azure-vm"></a><span data-ttu-id="0cca4-120">Agregar un tooan de usuario único sudo máquina virtual de Azure</span><span class="sxs-lookup"><span data-stu-id="0cca4-120">Adding a single sudo user tooan Azure VM</span></span>
<span data-ttu-id="0cca4-121">Inicie sesión en toohello Azure VM utilizar claves de SSH.</span><span class="sxs-lookup"><span data-stu-id="0cca4-121">Log in toohello Azure VM using SSH keys.</span></span>  <span data-ttu-id="0cca4-122">Si no ha configurado el acceso de clave pública SSH, lea primero el artículo [Using Public Key Authentication with Azure](http://link.to/article)(Uso de la autenticación de clave pública con Azure).</span><span class="sxs-lookup"><span data-stu-id="0cca4-122">If you have not setup SSH public key access, complete this article first [Using Public Key Authentication with Azure](http://link.to/article).</span></span>  

<span data-ttu-id="0cca4-123">Hola `useradd` Hola siguiente las tareas haya completado el comando:</span><span class="sxs-lookup"><span data-stu-id="0cca4-123">hello `useradd` command completes hello following tasks:</span></span>

* <span data-ttu-id="0cca4-124">crear una nueva cuenta de usuario</span><span class="sxs-lookup"><span data-stu-id="0cca4-124">create a new user account</span></span>
* <span data-ttu-id="0cca4-125">crear un nuevo grupo de usuarios con hello mismo nombre</span><span class="sxs-lookup"><span data-stu-id="0cca4-125">create a new user group with hello same name</span></span>
* <span data-ttu-id="0cca4-126">Agregar una entrada en blanco demasiado`/etc/passwd`</span><span class="sxs-lookup"><span data-stu-id="0cca4-126">add a blank entry too`/etc/passwd`</span></span>
* <span data-ttu-id="0cca4-127">Agregar una entrada en blanco demasiado`/etc/gpasswd`</span><span class="sxs-lookup"><span data-stu-id="0cca4-127">add a blank entry too`/etc/gpasswd`</span></span>

<span data-ttu-id="0cca4-128">Hola `-G` marca de línea de comandos agrega Hola nueva cuenta de usuario toohello apropiado Linux grupo otorgar privilegios de extensión raíz a la cuenta de usuario nueva de Hola.</span><span class="sxs-lookup"><span data-stu-id="0cca4-128">hello `-G` command-line flag adds hello new user account toohello proper Linux group giving hello new user account root escalation privileges.</span></span>

#### <a name="add-hello-user"></a><span data-ttu-id="0cca4-129">Agregar usuario de Hola</span><span class="sxs-lookup"><span data-stu-id="0cca4-129">Add hello user</span></span>
```bash
# On RedHat family distros
sudo useradd -G wheel exampleUser

# On Debian family distros
sudo useradd -G sudo exampleUser
```

#### <a name="set-a-password"></a><span data-ttu-id="0cca4-130">Establecer una contraseña</span><span class="sxs-lookup"><span data-stu-id="0cca4-130">Set a password</span></span>
<span data-ttu-id="0cca4-131">Hola `useradd` comando crea el usuario de Hola y agrega una entrada tooboth `/etc/passwd` y `/etc/gpasswd` , pero realmente no se establece la contraseña de Hola.</span><span class="sxs-lookup"><span data-stu-id="0cca4-131">hello `useradd` command creates hello user and adds an entry tooboth `/etc/passwd` and `/etc/gpasswd` but does not actually set hello password.</span></span>  <span data-ttu-id="0cca4-132">Hello contraseña se agrega mediante Hola de entrada de toohello `passwd` comando.</span><span class="sxs-lookup"><span data-stu-id="0cca4-132">hello password is added toohello entry using hello `passwd` command.</span></span>

```bash
sudo passwd exampleUser
Enter new UNIX password:
Retype new UNIX password:
passwd: password updated successfully
```

<span data-ttu-id="0cca4-133">Ahora tenemos un usuario con privilegios sudo en servidor hello.</span><span class="sxs-lookup"><span data-stu-id="0cca4-133">We now have a user with sudo privileges on hello server.</span></span>

### <a name="add-your-ssh-public-key-toohello-new-user-account"></a><span data-ttu-id="0cca4-134">Agregue su cuenta de usuario nueva toohello de clave pública SSH</span><span class="sxs-lookup"><span data-stu-id="0cca4-134">Add your SSH Public Key toohello new user account</span></span>
<span data-ttu-id="0cca4-135">Desde su equipo, use hello `ssh-copy-id` comando con la nueva contraseña de Hola.</span><span class="sxs-lookup"><span data-stu-id="0cca4-135">From your machine, use hello `ssh-copy-id` command with hello new password.</span></span>

```bash
ssh-copy-id -i ~/.ssh/id_rsa exampleuser@exampleserver
```

### <a name="using-visudo-tooallow-sudo-usage-without-a-password"></a><span data-ttu-id="0cca4-136">Use visudo tooallow sudo utilización sin una contraseña</span><span class="sxs-lookup"><span data-stu-id="0cca4-136">Using visudo tooallow sudo usage without a password</span></span>
<span data-ttu-id="0cca4-137">Usar `visudo` tooedit hello `/etc/sudoers` archivo agrega unos niveles de protección contra la modificación incorrecta de este archivo importante.</span><span class="sxs-lookup"><span data-stu-id="0cca4-137">Using `visudo` tooedit hello `/etc/sudoers` file adds a few layers of protection against incorrectly modifying this important file.</span></span>  <span data-ttu-id="0cca4-138">Tras la ejecución de `visudo`, hello `/etc/sudoers` archivo está bloqueado tooensure ningún otro usuario puede realizar cambios mientras activamente se está editando.</span><span class="sxs-lookup"><span data-stu-id="0cca4-138">Upon executing `visudo`, hello `/etc/sudoers` file is locked tooensure no other user can make changes while it is actively being edited.</span></span>  <span data-ttu-id="0cca4-139">Hola `/etc/sudoers` también se comprueba el archivo de errores por `visudo` al intentar toosave o salir por lo que no se puede guardar un archivo de sudoers roto.</span><span class="sxs-lookup"><span data-stu-id="0cca4-139">hello `/etc/sudoers` file is also checked for mistakes by `visudo` when you attempt toosave or exit so you cannot save a broken sudoers file.</span></span>

<span data-ttu-id="0cca4-140">Ya tenemos a los usuarios en el grupo predeterminado correcto de Hola para acceso sudo.</span><span class="sxs-lookup"><span data-stu-id="0cca4-140">We already have users in hello correct default group for sudo access.</span></span>  <span data-ttu-id="0cca4-141">Ahora vamos tooenable esos grupos toouse de sudo con ninguna contraseña.</span><span class="sxs-lookup"><span data-stu-id="0cca4-141">Now we are going tooenable those groups toouse sudo with no password.</span></span>

```bash
# Execute visudo as root tooedit hello /etc/sudoers file
visudo

# On RedHat family distros uncomment this line:
## Same thing without a password
# %wheel        ALL=(ALL)       NOPASSWD: ALL

# toothis
## Same thing without a password
%wheel        ALL=(ALL)       NOPASSWD: ALL

# On Debian family distros change this line:
# Allow members of group sudo tooexecute any command
%sudo   ALL=(ALL:ALL) ALL

# toothis
%sudo   ALL=(ALL) NOPASSWD:ALL
```

### <a name="verify-hello-user-ssh-keys-and-sudo"></a><span data-ttu-id="0cca4-142">Compruebe el usuario de hello, ssh claves y sudo</span><span class="sxs-lookup"><span data-stu-id="0cca4-142">Verify hello user, ssh keys, and sudo</span></span>
```bash
# Verify hello SSH keys & User account
ssh -i ~/.ssh/id_rsa exampleuser@exampleserver

# Verify sudo access
sudo top
```
