---
title: "par de claves de aaaDetailed pasos toocreate un SSH para máquinas virtuales de Linux en Azure | Documentos de Microsoft"
description: "Obtenga información acerca de pasos adicionales toocreate un par de claves de públicas y privado de SSH para máquinas virtuales de Linux en Azure, junto con certificados específicos para distintos casos de uso."
services: virtual-machines-linux
documentationcenter: 
author: dlepow
manager: timlt
editor: 
tags: 
ms.assetid: 
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 6/28/2017
ms.author: danlep
ms.openlocfilehash: 9ac52ef4dc87e73b9c07ccc323adc955829e2014
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="detailed-walk-through-toocreate-an-ssh-key-pair-and-additional-certificates-for-a-linux-vm-in-azure"></a><span data-ttu-id="977e1-103">Tutorial detallado toocreate un par de claves de SSH y certificados adicionales para una VM de Linux en Azure</span><span class="sxs-lookup"><span data-stu-id="977e1-103">Detailed walk through toocreate an SSH key pair and additional certificates for a Linux VM in Azure</span></span>
<span data-ttu-id="977e1-104">Con un par de claves de SSH, puede crear máquinas virtuales en Azure esos valores predeterminados de las claves SSH de toousing para la autenticación, eliminando la necesidad de Hola de toolog de las contraseñas en.</span><span class="sxs-lookup"><span data-stu-id="977e1-104">With an SSH key pair, you can create Virtual Machines on Azure that default toousing SSH keys for authentication, eliminating hello need for passwords toolog in.</span></span> <span data-ttu-id="977e1-105">Las contraseñas pueden ser adivinadas y abrir las máquinas virtuales una tooguess de intentos de toorelentless por fuerza bruta la contraseña.</span><span class="sxs-lookup"><span data-stu-id="977e1-105">Passwords can be guessed, and open your VMs up toorelentless brute force attempts tooguess your password.</span></span> <span data-ttu-id="977e1-106">Las máquinas virtuales creadas con plantillas de CLI de Azure o el Administrador de recursos de hello pueden incluir la clave pública SSH como parte de la implementación de hello, quitar un paso de configuración de implementación de post de deshabilitar los inicios de sesión de contraseña de SSH.</span><span class="sxs-lookup"><span data-stu-id="977e1-106">VMs created with hello Azure CLI or Resource Manager templates can include your SSH public key as part of hello deployment, removing a post deployment configuration step of disabling password logins for SSH.</span></span> <span data-ttu-id="977e1-107">En este artículo se proporcionan pasos detallados y otros ejemplos de generación de certificados, como los que se usan con las máquinas virtuales Linux.</span><span class="sxs-lookup"><span data-stu-id="977e1-107">This article provides detailed steps and additional examples of generating certificates, such as for use with Linux virtual machines.</span></span> <span data-ttu-id="977e1-108">Si desea que tooquickly crear y utilizar un par de claves de SSH, consulte [cómo emparejar toocreate una clave pública y privada de SSH para máquinas virtuales de Linux en Azure](mac-create-ssh-keys.md).</span><span class="sxs-lookup"><span data-stu-id="977e1-108">If you want tooquickly create and use an SSH key pair, see [How toocreate an SSH public and private key pair for Linux VMs in Azure](mac-create-ssh-keys.md).</span></span>

## <a name="understanding-ssh-keys"></a><span data-ttu-id="977e1-109">Descripción de las claves SSH</span><span class="sxs-lookup"><span data-stu-id="977e1-109">Understanding SSH keys</span></span>

<span data-ttu-id="977e1-110">El uso de claves públicas y privadas de SSH es toolog de manera más fácil de hello en servidores Linux de tooyour.</span><span class="sxs-lookup"><span data-stu-id="977e1-110">Using SSH public and private keys is hello easiest way toolog in tooyour Linux servers.</span></span> <span data-ttu-id="977e1-111">[Criptografía de clave pública](https://en.wikipedia.org/wiki/Public-key_cryptography) proporciona un toolog de manera mucho más seguro en tooyour Linux o BSD VM en Azure que las contraseñas, que pueden forzarse mucho más fácilmente.</span><span class="sxs-lookup"><span data-stu-id="977e1-111">[Public-key cryptography](https://en.wikipedia.org/wiki/Public-key_cryptography) provides a much more secure way toolog in tooyour Linux or BSD VM in Azure than passwords, which can be brute-forced far more easily.</span></span>

<span data-ttu-id="977e1-112">La clave pública se puede compartir con cualquiera. Sin embargo, la clave privada es propiedad exclusivamente suya (o de su infraestructura de seguridad local).</span><span class="sxs-lookup"><span data-stu-id="977e1-112">Your public key can be shared with anyone; but only you (or your local security infrastructure) possess your private key.</span></span>  <span data-ttu-id="977e1-113">clave privada de Hello SSH debe tener un [contraseña muy segura](https://www.xkcd.com/936/) (origen:[xkcd.com](https://xkcd.com)) toosafeguard se.</span><span class="sxs-lookup"><span data-stu-id="977e1-113">hello SSH private key should have a [very secure password](https://www.xkcd.com/936/) (source:[xkcd.com](https://xkcd.com)) toosafeguard it.</span></span>  <span data-ttu-id="977e1-114">Esta contraseña es simplemente tooaccess Hola SSH archivo de clave privada y **no es** contraseña de cuenta de usuario de Hola.</span><span class="sxs-lookup"><span data-stu-id="977e1-114">This password is just tooaccess hello private SSH key file and **is not** hello user account password.</span></span>  <span data-ttu-id="977e1-115">Cuando se agrega una clave SSH de tooyour de contraseña, cifra la clave privada de hello mediante AES de 128 bits, para que hello clave privada es inútil sin Hola contraseña toodecrypt lo.</span><span class="sxs-lookup"><span data-stu-id="977e1-115">When you add a password tooyour SSH key, it encrypts hello private key using 128-bit AES, so that hello private key is useless without hello password toodecrypt it.</span></span>  <span data-ttu-id="977e1-116">Si un atacante robar la clave privada y que la clave no tenía una contraseña, sería capaz de toouse es privada clave toolog en servidores de tooany que tiene la correspondiente clave pública de Hola.</span><span class="sxs-lookup"><span data-stu-id="977e1-116">If an attacker stole your private key and that key did not have a password, they would be able toouse that private key toolog in tooany servers that have hello corresponding public key.</span></span>  <span data-ttu-id="977e1-117">Si una clave privada está protegida con una contraseña, el atacante no podrá usarla, ya que la contraseña constituye un nivel adicional de seguridad en la infraestructura de Azure.</span><span class="sxs-lookup"><span data-stu-id="977e1-117">If a private key is password protected it cannot be used by that attacker, providing an additional layer of security for your infrastructure on Azure.</span></span>

<span data-ttu-id="977e1-118">En este artículo se crea una versión del protocolo SSH 2 pares de archivo de claves públicas y privadas de RSA (también denominado tooas "ssh-rsa" claves), que se recomiendan para las implementaciones con el Administrador de recursos de Azure.</span><span class="sxs-lookup"><span data-stu-id="977e1-118">This article creates an SSH protocol version 2 RSA public and private key file pair (also referred tooas "ssh-rsa" keys), which are recommended for deployments with Azure Resource Manager.</span></span> <span data-ttu-id="977e1-119">*SSH-rsa* las claves son necesarias en hello [portal](https://portal.azure.com) para clásico e implementaciones de administrador de recursos.</span><span class="sxs-lookup"><span data-stu-id="977e1-119">*ssh-rsa* keys are required on hello [portal](https://portal.azure.com) for both classic and Resource Manager deployments.</span></span>

## <a name="ssh-keys-use-and-benefits"></a><span data-ttu-id="977e1-120">Uso y ventajas de las claves SSH</span><span class="sxs-lookup"><span data-stu-id="977e1-120">SSH keys use and benefits</span></span>

<span data-ttu-id="977e1-121">Azure se necesita al menos 2048 bits, del protocolo SSH versión 2 RSA formato claves públicas y privadas; archivo de clave pública de Hello tiene hello `.pub` formato de contenedor.</span><span class="sxs-lookup"><span data-stu-id="977e1-121">Azure requires at least 2048-bit, SSH protocol version 2 RSA format public and private keys; hello public key file has hello `.pub` container format.</span></span> <span data-ttu-id="977e1-122">uso de claves de hello toocreate `ssh-keygen`, que realiza una serie de preguntas y, a continuación, escribe una clave privada y una clave pública correspondiente.</span><span class="sxs-lookup"><span data-stu-id="977e1-122">toocreate hello keys use `ssh-keygen`, which asks a series of questions and then writes a private key and a matching public key.</span></span> <span data-ttu-id="977e1-123">Cuando se crea una máquina virtual de Azure, Azure copias Hola toohello de clave pública `~/.ssh/authorized_keys` carpeta Hola máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="977e1-123">When an Azure VM is created, Azure copies hello public key toohello `~/.ssh/authorized_keys` folder on hello VM.</span></span> <span data-ttu-id="977e1-124">Claves SSH en `~/.ssh/authorized_keys` son toochallenge usado hello toomatch Hola correspondiente clave privada de cliente en una conexión de inicio de sesión SSH.</span><span class="sxs-lookup"><span data-stu-id="977e1-124">SSH keys in `~/.ssh/authorized_keys` are used toochallenge hello client toomatch hello corresponding private key on an SSH login connection.</span></span>  <span data-ttu-id="977e1-125">Cuando se crea una máquina virtual Linux de Azure mediante claves de SSH para la autenticación, Azure configura Hola SSHD toonot server permite inicios de sesión de contraseña, solo las claves SSH.</span><span class="sxs-lookup"><span data-stu-id="977e1-125">When an Azure Linux VM is created using SSH keys for authentication, Azure configures hello SSHD server toonot allow password logins, only SSH keys.</span></span>  <span data-ttu-id="977e1-126">Por lo tanto, mediante la creación de máquinas virtuales de Linux de Azure con claves SSH, puede ayudar a proteger la implementación de VM de Hola y ahórrese paso de configuración posteriores a la implementación típica de Hola de deshabilitar las contraseñas en hello **sshd_config** archivo.</span><span class="sxs-lookup"><span data-stu-id="977e1-126">Therefore, by creating Azure Linux VMs with SSH keys, you can help secure hello VM deployment and save yourself hello typical post-deployment configuration step of disabling passwords in hello **sshd_config** file.</span></span>

## <a name="using-ssh-keygen"></a><span data-ttu-id="977e1-127">Uso de ssh-keygen</span><span class="sxs-lookup"><span data-stu-id="977e1-127">Using ssh-keygen</span></span>

<span data-ttu-id="977e1-128">Este comando crea una contraseña protegida (cifrada) par de claves de SSH mediante RSA de 2048 bits y está marcada como comentario tooeasily identificarlo.</span><span class="sxs-lookup"><span data-stu-id="977e1-128">This command creates a password secured (encrypted) SSH key pair using 2048-bit RSA and it is commented tooeasily identify it.</span></span>  

<span data-ttu-id="977e1-129">SSH claves son de forma predeterminada que se mantienen en hello `~/.ssh` directory.</span><span class="sxs-lookup"><span data-stu-id="977e1-129">SSH keys are by default kept in hello `~/.ssh` directory.</span></span>  <span data-ttu-id="977e1-130">Si no tiene un `~/.ssh` directorio, hello `ssh-keygen` comando crea automáticamente con hello permisos correctos.</span><span class="sxs-lookup"><span data-stu-id="977e1-130">If you do not have a `~/.ssh` directory, hello `ssh-keygen` command creates it for you with hello correct permissions.</span></span>

```bash
ssh-keygen \
    -t rsa \
    -b 2048 \
    -C "azureuser@myserver" \
    -f ~/.ssh/id_rsa \
    -N mypassword
```

<span data-ttu-id="977e1-131">*Explicación del comando*</span><span class="sxs-lookup"><span data-stu-id="977e1-131">*Command explained*</span></span>

<span data-ttu-id="977e1-132">`ssh-keygen`= Hola programa utilizado toocreate Hola claves</span><span class="sxs-lookup"><span data-stu-id="977e1-132">`ssh-keygen` = hello program used toocreate hello keys</span></span>

<span data-ttu-id="977e1-133">`-t rsa`= tipo de clave toocreate que es el formato RSA Hola [wikipedia][paréntesis final](`https://en.wikipedia.org/wiki/RSA_(cryptosystem) `) 
 `-b 2048` = bits de clave de Hola</span><span class="sxs-lookup"><span data-stu-id="977e1-133">`-t rsa` = type of key toocreate which is hello RSA format [wikipedia][parens at end](`https://en.wikipedia.org/wiki/RSA_(cryptosystem) `)
`-b 2048` = bits of hello key</span></span>

<span data-ttu-id="977e1-134">`-C "azureuser@myserver"`= un comentario final toohello anexado de hello tooeasily de archivo de clave pública para identificarlo.</span><span class="sxs-lookup"><span data-stu-id="977e1-134">`-C "azureuser@myserver"` = a comment appended toohello end of hello public key file tooeasily identify it.</span></span>  <span data-ttu-id="977e1-135">Normalmente se usa un correo electrónico como comentario Hola pero puede usar cualquier cosa que funcione mejor para su infraestructura.</span><span class="sxs-lookup"><span data-stu-id="977e1-135">Normally an email is used as hello comment but you can use whatever works best for your infrastructure.</span></span>

## <a name="classic-deploy-using-asm"></a><span data-ttu-id="977e1-136">Implementación clásica mediante `asm`</span><span class="sxs-lookup"><span data-stu-id="977e1-136">Classic deploy using `asm`</span></span>

<span data-ttu-id="977e1-137">Si está utilizando el modelo de implementación clásica de hello (`asm` modo Hola CLI), puede usar una clave pública SSH-RSA o un RFC4716 con formato clave en un contenedor de pem.</span><span class="sxs-lookup"><span data-stu-id="977e1-137">If you are using hello classic deployment model (`asm` mode in hello CLI), you can use an SSH-RSA public key or an RFC4716 formatted key in a pem container.</span></span>  <span data-ttu-id="977e1-138">clave pública SSH-RSA Hello es lo que se creó anteriormente en este artículo mediante `ssh-keygen`.</span><span class="sxs-lookup"><span data-stu-id="977e1-138">hello SSH-RSA public key is what was created earlier in this article using `ssh-keygen`.</span></span>

<span data-ttu-id="977e1-139">toocreate un RFC4716 formato de clave de una clave pública SSH existente:</span><span class="sxs-lookup"><span data-stu-id="977e1-139">toocreate a RFC4716 formatted key from an existing SSH public key:</span></span>

```bash
ssh-keygen \
-f ~/.ssh/id_rsa.pub \
-e \
-m RFC4716 > ~/.ssh/id_ssh2.pem
```

## <a name="example-of-ssh-keygen"></a><span data-ttu-id="977e1-140">Ejemplo de ssh-keygen</span><span class="sxs-lookup"><span data-stu-id="977e1-140">Example of ssh-keygen</span></span>

```bash
ssh-keygen -t rsa -b 2048 -C "azureuser@myserver"
Generating public/private rsa key pair.
Enter file in which toosave hello key (/home/azureuser/.ssh/id_rsa):
Enter passphrase (empty for no passphrase):
Enter same passphrase again:
Your identification has been saved in /home/azureuser/.ssh/id_rsa.
Your public key has been saved in /home/azureuser/.ssh/id_rsa.pub.
hello key fingerprint is:
14:a3:cb:3e:78:ad:25:cc:55:e9:0c:08:e5:d1:a9:08 azureuser@myserver
hello keys randomart image is:
+--[ RSA 2048]----+
|        o o. .   |
|      E. = .o    |
|      ..o...     |
|     . o....     |
|      o S =      |
|     . + O       |
|      + = =      |
|       o +       |
|        .        |
+-----------------+
```

<span data-ttu-id="977e1-141">Archivos de clave guardados:</span><span class="sxs-lookup"><span data-stu-id="977e1-141">Saved key files:</span></span>

`Enter file in which toosave hello key (/home/azureuser/.ssh/id_rsa): ~/.ssh/id_rsa`

<span data-ttu-id="977e1-142">nombre del par de claves de Hola de este artículo.</span><span class="sxs-lookup"><span data-stu-id="977e1-142">hello key pair name for this article.</span></span>  <span data-ttu-id="977e1-143">Tener un par de claves denominado **id_rsa** es el valor predeterminado de Hola y algunas herramientas podrían esperar hello **id_rsa** nombre de archivo de clave privada para disponer de uno es una buena idea.</span><span class="sxs-lookup"><span data-stu-id="977e1-143">Having a key pair named **id_rsa** is hello default and some tools might expect hello **id_rsa** private key file name so having one is a good idea.</span></span> <span data-ttu-id="977e1-144">directorio de Hello `~/.ssh/` es ubicación predeterminada de Hola para pares de claves de SSH y archivo de configuración SSH de Hola.</span><span class="sxs-lookup"><span data-stu-id="977e1-144">hello directory `~/.ssh/` is hello default location for SSH key pairs and hello SSH config file.</span></span>  <span data-ttu-id="977e1-145">Si no se especifica con una ruta de acceso completa, `ssh-keygen` crea claves de hello en no Hola de forma predeterminada, el directorio actual de trabajo hello `~/.ssh`.</span><span class="sxs-lookup"><span data-stu-id="977e1-145">If not specified with a full path, `ssh-keygen` creates hello keys in hello current working directory, not hello default `~/.ssh`.</span></span>

<span data-ttu-id="977e1-146">Una lista de hello `~/.ssh` directory.</span><span class="sxs-lookup"><span data-stu-id="977e1-146">A listing of hello `~/.ssh` directory.</span></span>

```bash
ls -al ~/.ssh
-rw------- 1 azureuser staff  1675 Aug 25 18:04 id_rsa
-rw-r--r-- 1 azureuser staff   410 Aug 25 18:04 id_rsa.pub
```

<span data-ttu-id="977e1-147">Contraseña de la clave:</span><span class="sxs-lookup"><span data-stu-id="977e1-147">Key Password:</span></span>

`Enter passphrase (empty for no passphrase):`

<span data-ttu-id="977e1-148">`ssh-keygen`hace referencia tooa contraseña para el archivo de clave privada de hello como "una frase de contraseña".</span><span class="sxs-lookup"><span data-stu-id="977e1-148">`ssh-keygen` refers tooa password for hello private key file as "a passphrase."</span></span>  <span data-ttu-id="977e1-149">Es *fuertemente* recomienda tooadd una clave privada de tooyour de contraseña.</span><span class="sxs-lookup"><span data-stu-id="977e1-149">It is *strongly* recommended tooadd a password tooyour private key.</span></span> <span data-ttu-id="977e1-150">Sin un contraseña protección Hola archivo de clave, cualquier persona con archivo hello puede usar toolog en servidor tooany que tiene una clave pública correspondiente Hola.</span><span class="sxs-lookup"><span data-stu-id="977e1-150">Without a password protecting hello key file, anyone with hello file can use it toolog in tooany server that has hello corresponding public key.</span></span> <span data-ttu-id="977e1-151">Agregar una contraseña (frase de contraseña) ofrece una protección más en caso de que alguien es el archivo de clave privada tooyour toogain capaz de acceso, dado las claves de tiempo toochange hello usan tooauthenticate.</span><span class="sxs-lookup"><span data-stu-id="977e1-151">Adding a password (passphrase) offers more protection in case someone is able toogain access tooyour private key file, given you time toochange hello keys used tooauthenticate you.</span></span>

## <a name="using-ssh-agent-toostore-your-private-key-password"></a><span data-ttu-id="977e1-152">Uso de ssh agente toostore su contraseña de clave privada</span><span class="sxs-lookup"><span data-stu-id="977e1-152">Using ssh-agent toostore your private key password</span></span>

<span data-ttu-id="977e1-153">tooavoid escriba la contraseña del archivo de clave privada con cada inicio de sesión SSH, puede usar `ssh-agent` toocache la contraseña del archivo de clave privada.</span><span class="sxs-lookup"><span data-stu-id="977e1-153">tooavoid typing your private key file password with every SSH login, you can use `ssh-agent` toocache your private key file password.</span></span> <span data-ttu-id="977e1-154">Si utilizas un equipo Mac, Hola OSX llaveros almacena de forma segura las contraseñas de clave privada de hello al invocar `ssh-agent`.</span><span class="sxs-lookup"><span data-stu-id="977e1-154">If you are using a Mac, hello OSX Keychain securely stores hello private key passwords when you invoke `ssh-agent`.</span></span>

<span data-ttu-id="977e1-155">Compruebe y utilizar a ssh agente y ssh-agregar tooinform Hola SSH sistema acerca de los archivos de clave de Hola para que la frase de contraseña de hello no necesitará toobe usar de forma interactiva.</span><span class="sxs-lookup"><span data-stu-id="977e1-155">Verify and use ssh-agent and ssh-add tooinform hello SSH system about hello key files so that hello passphrase will not need toobe used interactively.</span></span>

```bash
eval "$(ssh-agent -s)"
```

<span data-ttu-id="977e1-156">Ahora agregue clave privada de hello demasiado`ssh-agent` mediante el comando hello `ssh-add`.</span><span class="sxs-lookup"><span data-stu-id="977e1-156">Now add hello private key too`ssh-agent` using hello command `ssh-add`.</span></span>

```bash
ssh-add ~/.ssh/id_rsa
```

<span data-ttu-id="977e1-157">contraseña de clave privada de Hello ahora se almacena en `ssh-agent`.</span><span class="sxs-lookup"><span data-stu-id="977e1-157">hello private key password is now stored in `ssh-agent`.</span></span>

## <a name="using-ssh-copy-id-toocopy-hello-key-tooan-existing-vm"></a><span data-ttu-id="977e1-158">Usar `ssh-copy-id` toocopy hello tooan clave existente de la máquina virtual</span><span class="sxs-lookup"><span data-stu-id="977e1-158">Using `ssh-copy-id` toocopy hello key tooan existing VM</span></span>
<span data-ttu-id="977e1-159">Si ya ha creado una máquina virtual puede instalar Hola nueva SSH pública clave tooyour VM de Linux con:</span><span class="sxs-lookup"><span data-stu-id="977e1-159">If you have already created a VM you can install hello new SSH public key tooyour Linux VM with:</span></span>

```bash
ssh-copy-id -i ~/.ssh/id_rsa.pub ahmet@myserver
```

## <a name="create-and-configure-an-ssh-config-file"></a><span data-ttu-id="977e1-160">Creación y configuración de un archivo de configuración de SSH</span><span class="sxs-lookup"><span data-stu-id="977e1-160">Create and configure an SSH config file</span></span>

<span data-ttu-id="977e1-161">Es una mejor toocreate de práctica recomendada y configurar un `~/.ssh/config` toospeed archivo los inicios de sesión y para optimizar el comportamiento de cliente SSH.</span><span class="sxs-lookup"><span data-stu-id="977e1-161">It is a recommended best practice toocreate and configure an `~/.ssh/config` file toospeed up log ins and for optimizing your SSH client behavior.</span></span>

<span data-ttu-id="977e1-162">Hola de ejemplo siguiente muestra una configuración estándar.</span><span class="sxs-lookup"><span data-stu-id="977e1-162">hello following example shows a standard configuration.</span></span>

### <a name="create-hello-file"></a><span data-ttu-id="977e1-163">Crear archivo hello</span><span class="sxs-lookup"><span data-stu-id="977e1-163">Create hello file</span></span>

```bash
touch ~/.ssh/config
```

### <a name="edit-hello-file-tooadd-hello-new-ssh-configuration"></a><span data-ttu-id="977e1-164">Editar configuración de SSH nuevo de hello archivo tooadd hello:</span><span class="sxs-lookup"><span data-stu-id="977e1-164">Edit hello file tooadd hello new SSH configuration:</span></span>

```bash
vim ~/.ssh/config
```

### <a name="example-sshconfig-file"></a><span data-ttu-id="977e1-165">Archivo `~/.ssh/config` de ejemplo:</span><span class="sxs-lookup"><span data-stu-id="977e1-165">Example `~/.ssh/config` file:</span></span>

```bash
# Azure Keys
Host fedora22
  Hostname 102.160.203.241
  User ahmet
# ./Azure Keys
# Default Settings
Host *
  PubkeyAuthentication=yes
  IdentitiesOnly=yes
  ServerAliveInterval=60
  ServerAliveCountMax=30
  ControlMaster auto
  ControlPath ~/.ssh/SSHConnections/ssh-%r@%h:%p
  ControlPersist 4h
  IdentityFile ~/.ssh/id_rsa
```

<span data-ttu-id="977e1-166">Esto deja de configuración SSH se secciones para cada servidor tooenable cada toohave su propio par de claves dedicado.</span><span class="sxs-lookup"><span data-stu-id="977e1-166">This SSH config gives you sections for each server tooenable each toohave its own dedicated key pair.</span></span> <span data-ttu-id="977e1-167">Hola configuración predeterminada (`Host *`) son para todos los hosts que no coincide con cualquiera de hello hosts específicos más arriba en el archivo de configuración de Hola.</span><span class="sxs-lookup"><span data-stu-id="977e1-167">hello default settings (`Host *`) are for any hosts that do not match any of hello specific hosts higher up in hello config file.</span></span>

### <a name="config-file-explained"></a><span data-ttu-id="977e1-168">Explicación del archivo de configuración</span><span class="sxs-lookup"><span data-stu-id="977e1-168">Config file explained</span></span>

<span data-ttu-id="977e1-169">`Host`= nombre de hello del host de Hola que se llama en hello terminal.</span><span class="sxs-lookup"><span data-stu-id="977e1-169">`Host` = hello name of hello host being called on hello terminal.</span></span>  <span data-ttu-id="977e1-170">`ssh fedora22`indica a `SSH` toouse valores de hello en bloque de configuración de hello con la etiqueta `Host fedora22` Nota: Host puede ser cualquier etiqueta que tiene sentido para su uso y no representa Hola hostname real de cualquier servidor.</span><span class="sxs-lookup"><span data-stu-id="977e1-170">`ssh fedora22` tells `SSH` toouse hello values in hello settings block labeled `Host fedora22`  NOTE: Host can be any label that is logical for your usage and does not represent hello actual hostname of any server.</span></span>

<span data-ttu-id="977e1-171">`Hostname 102.160.203.241`= dirección IP de Hola o nombre DNS de servidor de Hola que se obtiene acceso.</span><span class="sxs-lookup"><span data-stu-id="977e1-171">`Hostname 102.160.203.241` = hello IP address or DNS name for hello server being accessed.</span></span>

<span data-ttu-id="977e1-172">`User ahmet`= toouse de cuenta de usuario remoto hello al iniciar sesión en el servidor de toohello.</span><span class="sxs-lookup"><span data-stu-id="977e1-172">`User ahmet` = hello remote user account toouse when logging in toohello server.</span></span>

<span data-ttu-id="977e1-173">`PubKeyAuthentication yes`= indica SSH desea toouse un toolog clave SSH.</span><span class="sxs-lookup"><span data-stu-id="977e1-173">`PubKeyAuthentication yes` = tells SSH you want toouse an SSH key toolog in.</span></span>

<span data-ttu-id="977e1-174">`IdentityFile /home/ahmet/.ssh/id_id_rsa`= la clave privada de SSH de Hola y toouse de clave pública correspondiente para la autenticación.</span><span class="sxs-lookup"><span data-stu-id="977e1-174">`IdentityFile /home/ahmet/.ssh/id_id_rsa` = hello SSH private key and corresponding public key toouse for authentication.</span></span>

## <a name="ssh-into-linux-without-a-password"></a><span data-ttu-id="977e1-175">SSH en Linux sin contraseña</span><span class="sxs-lookup"><span data-stu-id="977e1-175">SSH into Linux without a password</span></span>

<span data-ttu-id="977e1-176">Ahora que tiene un par de claves de SSH y un archivo de configuración SSH configurado, es capaz de toolog en tooyour VM de Linux rápida y segura.</span><span class="sxs-lookup"><span data-stu-id="977e1-176">Now that you have an SSH key pair and a configured SSH config file, you are able toolog in tooyour Linux VM quickly and securely.</span></span> <span data-ttu-id="977e1-177">Hola primera vez que inicie en servidor de tooa mediante un símbolo del sistema de hello clave SSH se Hola frase de contraseña para este archivo de clave.</span><span class="sxs-lookup"><span data-stu-id="977e1-177">hello first time you log in tooa server using an SSH key hello command prompts you for hello passphrase for that key file.</span></span>

```bash
ssh fedora22
```

### <a name="command-explained"></a><span data-ttu-id="977e1-178">Explicación del comando</span><span class="sxs-lookup"><span data-stu-id="977e1-178">Command explained</span></span>

<span data-ttu-id="977e1-179">Cuando `ssh fedora22` se ejecuta SSH primero busca y carga los valores de configuración de hello `Host fedora22` bloque y, a continuación, carga todos Hola restantes valores de hello último bloque, `Host *`.</span><span class="sxs-lookup"><span data-stu-id="977e1-179">When `ssh fedora22` is executed SSH first locates and loads any settings from hello `Host fedora22` block, and then loads all hello remaining settings from hello last block, `Host *`.</span></span>

## <a name="next-steps"></a><span data-ttu-id="977e1-180">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="977e1-180">Next Steps</span></span>

<span data-ttu-id="977e1-181">A continuación una es toocreate máquinas virtuales de Linux de Azure con hello nueva SSH clave pública.</span><span class="sxs-lookup"><span data-stu-id="977e1-181">Next up is toocreate Azure Linux VMs using hello new SSH public key.</span></span>  <span data-ttu-id="977e1-182">Máquinas virtuales de Azure que se crean con una clave pública SSH como inicio de sesión de hello son más segura que las máquinas virtuales creadas con el método de inicio de sesión de hello de forma predeterminada, las contraseñas.</span><span class="sxs-lookup"><span data-stu-id="977e1-182">Azure VMs that are created with an SSH public key as hello login are better secured than VMs created with hello default login method, passwords.</span></span>  <span data-ttu-id="977e1-183">Las máquinas virtuales de Azure creadas con claves SSH están configuradas de forma predeterminada con las contraseñas deshabilitadas, a fin de evitar los intentos de adivinarlas por fuerza bruta.</span><span class="sxs-lookup"><span data-stu-id="977e1-183">Azure VMs created using SSH keys are by default configured with passwords disabled, avoiding brute-forced guessing attempts.</span></span>

* [<span data-ttu-id="977e1-184">Creación de una máquina virtual Linux protegida mediante una plantilla de Azure</span><span class="sxs-lookup"><span data-stu-id="977e1-184">Create a secure Linux VM using an Azure template</span></span>](create-ssh-secured-vm-from-template.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [<span data-ttu-id="977e1-185">Crear una VM de Linux segura mediante Hola portal de Azure</span><span class="sxs-lookup"><span data-stu-id="977e1-185">Create a secure Linux VM using hello Azure portal</span></span>](quick-create-portal.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [<span data-ttu-id="977e1-186">Crear una VM de Linux segura mediante Hola CLI de Azure</span><span class="sxs-lookup"><span data-stu-id="977e1-186">Create a secure Linux VM using hello Azure CLI</span></span>](quick-create-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
