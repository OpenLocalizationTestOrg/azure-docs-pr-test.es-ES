---
title: "par de claves de aaaCreate un SSH para máquinas virtuales de Linux en Azure | Documentos de Microsoft"
description: "Cree de forma segura un par de claves SSH pública y privada para máquinas virtuales Linux de Azure."
services: virtual-machines-linux
documentationcenter: 
author: vlivech
manager: timlt
editor: 
tags: 
ms.assetid: 34ae9482-da3e-4b2d-9d0d-9d672aa42498
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: get-started-article
ms.date: 03/08/2017
ms.author: rasquill
ms.openlocfilehash: c4c7cec77c9b48295f2a28c8179b30a4dc38a555
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-ssh-public-and-private-key-pair-for-linux-vms"></a><span data-ttu-id="1d7e9-103">Creación de un par de claves SSH pública y privada para máquinas virtuales Linux</span><span class="sxs-lookup"><span data-stu-id="1d7e9-103">Create an SSH public and private key pair for Linux VMs</span></span>

<span data-ttu-id="1d7e9-104">Este artículo muestra cómo toogenerate una Protocolo versión 2 RSA pública y privada clave SSH archivo toouse par con máquinas virtuales de Linux.</span><span class="sxs-lookup"><span data-stu-id="1d7e9-104">This article shows you how toogenerate an SSH protocol version 2 RSA public and private key file pair toouse with Linux VMs.</span></span>  <span data-ttu-id="1d7e9-105">Con un par de claves de SSH, puede crear máquinas virtuales en Azure esos valores predeterminados de las claves SSH de toousing para la autenticación, eliminando la necesidad de Hola de toolog de las contraseñas en.</span><span class="sxs-lookup"><span data-stu-id="1d7e9-105">With an SSH key pair, you can create Virtual Machines on Azure that default toousing SSH keys for authentication, eliminating hello need for passwords toolog in.</span></span>  <span data-ttu-id="1d7e9-106">Las contraseñas pueden ser adivinadas y abrir las máquinas virtuales una tooguess de intentos de toorelentless por fuerza bruta la contraseña.</span><span class="sxs-lookup"><span data-stu-id="1d7e9-106">Passwords can be guessed, and open your VMs up toorelentless brute force attempts tooguess your password.</span></span> <span data-ttu-id="1d7e9-107">Las máquinas virtuales creadas con plantillas de Azure o hello `azure-cli` puede incluir la clave pública SSH como parte de la implementación de hello, quitar un paso de configuración de implementación de post de deshabilitar los inicios de sesión de contraseña de SSH.</span><span class="sxs-lookup"><span data-stu-id="1d7e9-107">VMs created with Azure Templates or hello `azure-cli` can include your SSH public key as part of hello deployment, removing a post deployment configuration step of disabling password logins for SSH.</span></span>

## <a name="quick-commands"></a><span data-ttu-id="1d7e9-108">Comandos rápidos</span><span class="sxs-lookup"><span data-stu-id="1d7e9-108">Quick Commands</span></span>

<span data-ttu-id="1d7e9-109">Ejecute hello siguientes comandos de shell de Bash, reemplazando los ejemplos de hello con sus propias opciones.</span><span class="sxs-lookup"><span data-stu-id="1d7e9-109">Run hello following commands from a Bash shell, replacing hello examples with your own choices.</span></span>

<span data-ttu-id="1d7e9-110">El archivo de clave pública SSH se crea de forma predeterminada en `~/.ssh/id_rsa.pub`.</span><span class="sxs-lookup"><span data-stu-id="1d7e9-110">Your SSH public key file is by default created at `~/.ssh/id_rsa.pub`.</span></span> <span data-ttu-id="1d7e9-111">Cuando se le solicite mediante el siguiente comando de hello, debe crear un toosecure "frase de contraseña" su clave privada.</span><span class="sxs-lookup"><span data-stu-id="1d7e9-111">When prompted using hello following command, you should create a "passphrase" toosecure your private key.</span></span> <span data-ttu-id="1d7e9-112">(frase de contraseña de hello es que utiliza una contraseña tooencrypt su clave privada).</span><span class="sxs-lookup"><span data-stu-id="1d7e9-112">(hello passphrase is a password used tooencrypt your private key.)</span></span>

```bash
ssh-keygen -t rsa -b 2048 
```

<span data-ttu-id="1d7e9-113">Agregar clave de hello recién creado demasiado`ssh-agent`:</span><span class="sxs-lookup"><span data-stu-id="1d7e9-113">Add hello newly created key too`ssh-agent`:</span></span>

```bash
ssh-add ~/.ssh/id_rsa
```

> [!IMPORTANT] 
> <span data-ttu-id="1d7e9-114">Hola por encima de trabajo de comandos en sistemas operativos Linux casi todas las distribuciones, pero no funcionan necesariamente en contenedores, como entorno de hello puede restringirse radicalmente.</span><span class="sxs-lookup"><span data-stu-id="1d7e9-114">hello above commands work on Linux operating systems of almost all distributions, but do not necessarily work in containers, as hello environment can be radically constrained.</span></span> 

## <a name="detailed-walkthrough"></a><span data-ttu-id="1d7e9-115">Tutorial detallado</span><span class="sxs-lookup"><span data-stu-id="1d7e9-115">Detailed Walkthrough</span></span>

<span data-ttu-id="1d7e9-116">El uso de claves públicas y privadas de SSH es toolog de manera más fácil de hello en servidores Linux de tooyour.</span><span class="sxs-lookup"><span data-stu-id="1d7e9-116">Using SSH public and private keys is hello easiest way toolog in tooyour Linux servers.</span></span> <span data-ttu-id="1d7e9-117">[Criptografía de clave pública](https://en.wikipedia.org/wiki/Public-key_cryptography) proporciona un toolog de manera mucho más seguro en tooyour Linux o BSD VM en Azure que las contraseñas, que pueden forzarse mucho más fácilmente.</span><span class="sxs-lookup"><span data-stu-id="1d7e9-117">[Public-key cryptography](https://en.wikipedia.org/wiki/Public-key_cryptography) provides a much more secure way toolog in tooyour Linux or BSD VM in Azure than passwords, which can be brute-forced far more easily.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="1d7e9-118">La clave pública se puede compartir con cualquiera. Sin embargo, la clave privada es propiedad exclusivamente suya (o de su infraestructura de seguridad local).</span><span class="sxs-lookup"><span data-stu-id="1d7e9-118">Your public key can be shared with anyone; but only you (or your local security infrastructure) possess your private key.</span></span>  <span data-ttu-id="1d7e9-119">clave privada de Hello SSH debe tener un [contraseña muy segura](https://www.xkcd.com/936/) (origen:[xkcd.com](https://xkcd.com)) toosafeguard se.</span><span class="sxs-lookup"><span data-stu-id="1d7e9-119">hello SSH private key should have a [very secure password](https://www.xkcd.com/936/) (source:[xkcd.com](https://xkcd.com)) toosafeguard it.</span></span>  <span data-ttu-id="1d7e9-120">Esta contraseña es la clave privada de SSH de tooaccess simplemente hello y **no es** contraseña de cuenta de usuario de Hola.</span><span class="sxs-lookup"><span data-stu-id="1d7e9-120">This password is just tooaccess hello private SSH key and **is not** hello user account password.</span></span>  <span data-ttu-id="1d7e9-121">Cuando se agrega una clave SSH de tooyour de contraseña, cifra la clave privada de hello mediante AES de 128 bits, para que hello clave privada es inútil sin Hola contraseña toodecrypt lo.</span><span class="sxs-lookup"><span data-stu-id="1d7e9-121">When you add a password tooyour SSH key, it encrypts hello private key using 128-bit AES, so that hello private key is useless without hello password toodecrypt it.</span></span>  <span data-ttu-id="1d7e9-122">Si un atacante robar la clave privada y que la clave no tenía una contraseña, sería capaz de toouse es privada clave toolog en servidores de tooany que tiene la correspondiente clave pública de Hola.</span><span class="sxs-lookup"><span data-stu-id="1d7e9-122">If an attacker stole your private key and that key did not have a password, they would be able toouse that private key toolog in tooany servers that have hello corresponding public key.</span></span>  <span data-ttu-id="1d7e9-123">Si una clave privada está protegida con una contraseña, el atacante no podrá usarla, ya que la contraseña constituye un nivel adicional de seguridad en la infraestructura de Azure.</span><span class="sxs-lookup"><span data-stu-id="1d7e9-123">If a private key is password protected it cannot be used by that attacker, providing an additional layer of security for your infrastructure on Azure.</span></span>

<span data-ttu-id="1d7e9-124">En este artículo se crea versión del protocolo SSH 2 RSA públicos y privados archivos de clave, que se recomiendan para las implementaciones en hello Administrador de recursos.</span><span class="sxs-lookup"><span data-stu-id="1d7e9-124">This article creates SSH protocol version 2 RSA public and private key files, which are recommended for deployments on hello Resource Manager.</span></span>  <span data-ttu-id="1d7e9-125">*SSH-rsa* las claves son necesarias en hello [portal](https://portal.azure.com) para clásico e implementaciones de administrador de recursos.</span><span class="sxs-lookup"><span data-stu-id="1d7e9-125">*ssh-rsa* keys are required on hello [portal](https://portal.azure.com) for both classic and Resource Manager deployments.</span></span>

## <a name="disable-ssh-passwords-by-using-ssh-keys"></a><span data-ttu-id="1d7e9-126">Deshabilitar contraseñas SSH mediante claves SSH</span><span class="sxs-lookup"><span data-stu-id="1d7e9-126">Disable SSH passwords by using SSH keys</span></span>

<span data-ttu-id="1d7e9-127">Azure requiere al menos claves públicas y privadas de 2048 bits con el formato ssh-rsa.</span><span class="sxs-lookup"><span data-stu-id="1d7e9-127">Azure requires at least 2048-bit, ssh-rsa format public and private keys.</span></span> <span data-ttu-id="1d7e9-128">uso de claves de hello toocreate `ssh-keygen`, que realiza una serie de preguntas y, a continuación, escribe una clave privada y una clave pública correspondiente.</span><span class="sxs-lookup"><span data-stu-id="1d7e9-128">toocreate hello keys use `ssh-keygen`, which asks a series of questions and then writes a private key and a matching public key.</span></span> <span data-ttu-id="1d7e9-129">Cuando se crea una máquina virtual de Azure, la clave pública de Hola se copia demasiado`~/.ssh/authorized_keys`.</span><span class="sxs-lookup"><span data-stu-id="1d7e9-129">When an Azure VM is created, hello public key is copied too`~/.ssh/authorized_keys`.</span></span>  <span data-ttu-id="1d7e9-130">Claves SSH en `~/.ssh/authorized_keys` son toochallenge usado hello toomatch Hola correspondiente clave privada de cliente en una conexión de inicio de sesión SSH.</span><span class="sxs-lookup"><span data-stu-id="1d7e9-130">SSH keys in `~/.ssh/authorized_keys` are used toochallenge hello client toomatch hello corresponding private key on an SSH login connection.</span></span>  <span data-ttu-id="1d7e9-131">Cuando se crea una máquina virtual Linux de Azure mediante claves de SSH para la autenticación, Azure configura Hola SSHD toonot server permite inicios de sesión de contraseña, solo las claves SSH.</span><span class="sxs-lookup"><span data-stu-id="1d7e9-131">When an Azure Linux VM is created using SSH keys for authentication, Azure configures hello SSHD server toonot allow password logins, only SSH keys.</span></span>  <span data-ttu-id="1d7e9-132">Por lo tanto, mediante la creación de máquinas virtuales de Linux de Azure con claves SSH, permiten una implementación segura Hola VM y ahorrarse el paso de configuración posteriores a la implementación típica de Hola de deshabilitar las contraseñas en el archivo de configuración de hello sshd_config.</span><span class="sxs-lookup"><span data-stu-id="1d7e9-132">Therefore, by creating Azure Linux VMs with SSH keys, you can help secure hello VM deployment and save yourself hello typical post-deployment configuration step of disabling passwords in hello sshd_config config file.</span></span>

## <a name="using-ssh-keygen"></a><span data-ttu-id="1d7e9-133">Uso de ssh-keygen</span><span class="sxs-lookup"><span data-stu-id="1d7e9-133">Using ssh-keygen</span></span>

<span data-ttu-id="1d7e9-134">Este comando crea una contraseña protegida (cifrada) par de claves de SSH mediante RSA de 2048 bits y está marcada como comentario tooeasily identificarlo.</span><span class="sxs-lookup"><span data-stu-id="1d7e9-134">This command creates a password secured (encrypted) SSH key pair using 2048-bit RSA and it is commented tooeasily identify it.</span></span>  

<span data-ttu-id="1d7e9-135">SSH claves son de forma predeterminada que se mantienen en hello `~/.ssh` directory.</span><span class="sxs-lookup"><span data-stu-id="1d7e9-135">SSH keys are by default kept in hello `~/.ssh` directory.</span></span>  <span data-ttu-id="1d7e9-136">Si no tiene un `~/.ssh` directorio, hello `ssh-keygen` comando crea automáticamente con hello permisos correctos.</span><span class="sxs-lookup"><span data-stu-id="1d7e9-136">If you do not have a `~/.ssh` directory, hello `ssh-keygen` command creates it for you with hello correct permissions.</span></span>

```bash
ssh-keygen \
-t rsa \
-b 2048 
```

<span data-ttu-id="1d7e9-137">*Explicación del comando*</span><span class="sxs-lookup"><span data-stu-id="1d7e9-137">*Command explained*</span></span>

<span data-ttu-id="1d7e9-138">`ssh-keygen`= Hola programa utilizado toocreate Hola claves</span><span class="sxs-lookup"><span data-stu-id="1d7e9-138">`ssh-keygen` = hello program used toocreate hello keys</span></span>

<span data-ttu-id="1d7e9-139">`-t rsa`= tipo de clave toocreate que es el formato RSA Hola [wikipedia](https://en.wikipedia.org/wiki/RSA_(cryptosystem)</span><span class="sxs-lookup"><span data-stu-id="1d7e9-139">`-t rsa` = type of key toocreate which is hello RSA format [wikipedia](https://en.wikipedia.org/wiki/RSA_(cryptosystem)</span></span>

<span data-ttu-id="1d7e9-140">`-b 2048`= bits de clave de Hola</span><span class="sxs-lookup"><span data-stu-id="1d7e9-140">`-b 2048` = bits of hello key</span></span>


## <a name="classic-portal-and-x509-certs"></a><span data-ttu-id="1d7e9-141">Portal clásico y certificados X.509</span><span class="sxs-lookup"><span data-stu-id="1d7e9-141">Classic portal and X.509 certs</span></span>

<span data-ttu-id="1d7e9-142">Si utilizas hello Azure [portal clásico](https://manage.windowsazure.com/), requiere certificados X.509 para las claves SSH de Hola.</span><span class="sxs-lookup"><span data-stu-id="1d7e9-142">If you are using hello Azure [classic portal](https://manage.windowsazure.com/), it requires X.509 certs for hello SSH keys.</span></span>  <span data-ttu-id="1d7e9-143">No se permite ningún otro tipo de claves públicas SSH, *deben* ser certificados X.509.</span><span class="sxs-lookup"><span data-stu-id="1d7e9-143">No other types of SSH public keys are allowed, they *must* be X.509 certs.</span></span>

<span data-ttu-id="1d7e9-144">toocreate un certificado X.509 de su clave privada SSH-RSA existente:</span><span class="sxs-lookup"><span data-stu-id="1d7e9-144">toocreate an X.509 cert from your existing SSH-RSA private key:</span></span>

```bash
openssl req -x509 \
-key ~/.ssh/id_rsa \
-nodes \
-days 365 \
-newkey rsa:2048 \
-out ~/.ssh/id_rsa.pem
```

## <a name="classic-deploy-using-asm"></a><span data-ttu-id="1d7e9-145">Implementación clásica mediante `asm`</span><span class="sxs-lookup"><span data-stu-id="1d7e9-145">Classic deploy using `asm`</span></span>

<span data-ttu-id="1d7e9-146">Si usas clásico de Hola implementar modelo (administración de servicios Azure CLI `asm`), puede usar una clave pública SSH-RSA o un RFC4716 con formato clave en un **.pem** contenedor.</span><span class="sxs-lookup"><span data-stu-id="1d7e9-146">If you are using hello classic deploy model (Azure service management CLI `asm`), you can use an SSH-RSA public key or an RFC4716 formatted key in a **.pem** container.</span></span>  <span data-ttu-id="1d7e9-147">clave pública SSH-RSA Hello es lo que se creó anteriormente en este artículo mediante `ssh-keygen`.</span><span class="sxs-lookup"><span data-stu-id="1d7e9-147">hello SSH-RSA public key is what was created earlier in this article using `ssh-keygen`.</span></span>

<span data-ttu-id="1d7e9-148">toocreate un RFC4716 formato de clave de una clave pública SSH existente:</span><span class="sxs-lookup"><span data-stu-id="1d7e9-148">toocreate a RFC4716 formatted key from an existing SSH public key:</span></span>

```bash
ssh-keygen \
-f ~/.ssh/id_rsa.pub \
-e \
-m RFC4716 > ~/.ssh/id_ssh2.pem
```

## <a name="example-of-ssh-keygen"></a><span data-ttu-id="1d7e9-149">Ejemplo de ssh-keygen</span><span class="sxs-lookup"><span data-stu-id="1d7e9-149">Example of ssh-keygen</span></span>

```bash
ssh-keygen -t rsa -b 2048 -C "ahmet@myserver"
Generating public/private rsa key pair.
Enter file in which toosave hello key (/home/ahmet/.ssh/id_rsa): 
Enter passphrase (empty for no passphrase):
Enter same passphrase again:
Your identification has been saved in /home/ahmet/.ssh/id_rsa.
Your public key has been saved in /home/ahmet/.ssh/id_rsa.pub.
hello key fingerprint is:
14:a3:cb:3e:78:ad:25:cc:55:e9:0c:08:e5:d1:a9:08 ahmet@myserver
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

<span data-ttu-id="1d7e9-150">Archivos de clave guardados:</span><span class="sxs-lookup"><span data-stu-id="1d7e9-150">Saved key files:</span></span>

`Enter file in which toosave hello key (/home/ahmet/.ssh/id_rsa): ~/.ssh/id_rsa`

<span data-ttu-id="1d7e9-151">nombre del par de claves de Hola de este artículo.</span><span class="sxs-lookup"><span data-stu-id="1d7e9-151">hello key pair name for this article.</span></span>  <span data-ttu-id="1d7e9-152">Tener un par de claves denominado **id_rsa** es el valor predeterminado de Hola y algunas herramientas podrían esperar hello **id_rsa** nombre de archivo de clave privada para disponer de uno es una buena idea.</span><span class="sxs-lookup"><span data-stu-id="1d7e9-152">Having a key pair named **id_rsa** is hello default and some tools might expect hello **id_rsa** private key file name so having one is a good idea.</span></span> <span data-ttu-id="1d7e9-153">directorio de Hello `~/.ssh/` es ubicación predeterminada de Hola para pares de claves de SSH y archivo de configuración SSH de Hola.</span><span class="sxs-lookup"><span data-stu-id="1d7e9-153">hello directory `~/.ssh/` is hello default location for SSH key pairs and hello SSH config file.</span></span>  <span data-ttu-id="1d7e9-154">Si no se especifica con una ruta de acceso completa, `ssh-keygen` van a crear claves de hello en el directorio de trabajo actual de hello, no Hola predeterminado `~/.ssh`.</span><span class="sxs-lookup"><span data-stu-id="1d7e9-154">If not specified with a full path, `ssh-keygen` will create hello keys in hello current working directory, not hello default `~/.ssh`.</span></span>

<span data-ttu-id="1d7e9-155">Una lista de hello `~/.ssh` directory.</span><span class="sxs-lookup"><span data-stu-id="1d7e9-155">A listing of hello `~/.ssh` directory.</span></span>

```bash
ls -al ~/.ssh
-rw------- 1 ahmet staff  1675 Aug 25 18:04 id_rsa
-rw-r--r-- 1 ahmet staff   410 Aug 25 18:04 rsa.pub
```

<span data-ttu-id="1d7e9-156">Contraseña de la clave:</span><span class="sxs-lookup"><span data-stu-id="1d7e9-156">Key Password:</span></span>

`Enter passphrase (empty for no passphrase):`

<span data-ttu-id="1d7e9-157">`ssh-keygen`hace referencia la clave privada de tooa contraseña utilizada tooencrypt hello como "una frase de contraseña".</span><span class="sxs-lookup"><span data-stu-id="1d7e9-157">`ssh-keygen` refers tooa password used tooencrypt hello private key as "a passphrase."</span></span>  <span data-ttu-id="1d7e9-158">Es *fuertemente* recomienda tooadd un par de claves de tooyour de frase de contraseña.</span><span class="sxs-lookup"><span data-stu-id="1d7e9-158">It is *strongly* recommended tooadd a passphrase tooyour key pairs.</span></span> <span data-ttu-id="1d7e9-159">Sin una frase de contraseña protección Hola clave privada, cualquier persona con el archivo de clave de hello puede utilizarse toolog en servidor tooany que tiene una clave pública correspondiente Hola.</span><span class="sxs-lookup"><span data-stu-id="1d7e9-159">Without a passphrase protecting hello private key, anyone with hello key file can use it toolog in tooany server that has hello corresponding public key.</span></span> <span data-ttu-id="1d7e9-160">Agregar una frase de contraseña ofrece una protección más en caso de que alguien es el archivo de clave privada tooyour toogain capaz de acceso, lo que proporciona claves de tiempo toochange Hola usan tooauthenticate.</span><span class="sxs-lookup"><span data-stu-id="1d7e9-160">Adding a passphrase offers more protection in case someone is able toogain access tooyour private key file, giving you time toochange hello keys used tooauthenticate you.</span></span>

## <a name="using-ssh-agent-toostore-your-private-key-password"></a><span data-ttu-id="1d7e9-161">Uso de ssh agente toostore su contraseña de clave privada</span><span class="sxs-lookup"><span data-stu-id="1d7e9-161">Using ssh-agent toostore your private key password</span></span>

<span data-ttu-id="1d7e9-162">frase de contraseña de archivo tooavoid escribir su clave privada con cada inicio de sesión SSH, puede usar `ssh-agent` toocache la contraseña del archivo de clave privada.</span><span class="sxs-lookup"><span data-stu-id="1d7e9-162">tooavoid typing your private key file passphrase with every SSH login, you can use `ssh-agent` toocache your private key file password.</span></span> <span data-ttu-id="1d7e9-163">Si utilizas un equipo Mac, Hola OSX llaveros almacena de forma segura las contraseñas de clave privada de hello al invocar `ssh-agent`.</span><span class="sxs-lookup"><span data-stu-id="1d7e9-163">If you are using a Mac, hello OSX Keychain securely stores hello private key passwords when you invoke `ssh-agent`.</span></span>

<span data-ttu-id="1d7e9-164">Compruebe y usar `ssh-agent` y `ssh-add` tooinform Hola SSH sistema acerca de los archivos de clave de Hola para que la frase de contraseña de hello no necesitará toobe usar de forma interactiva.</span><span class="sxs-lookup"><span data-stu-id="1d7e9-164">Verify and use `ssh-agent` and `ssh-add` tooinform hello SSH system about hello key files so that hello passphrase will not need toobe used interactively.</span></span>

```bash
eval "$(ssh-agent -s)"
```

<span data-ttu-id="1d7e9-165">Ahora agregue clave privada de hello demasiado`ssh-agent` mediante el comando hello `ssh-add`.</span><span class="sxs-lookup"><span data-stu-id="1d7e9-165">Now add hello private key too`ssh-agent` using hello command `ssh-add`.</span></span>

```bash
ssh-add ~/.ssh/id_rsa
```

<span data-ttu-id="1d7e9-166">contraseña de clave privada de Hello ahora se almacena en `ssh-agent`.</span><span class="sxs-lookup"><span data-stu-id="1d7e9-166">hello private key password is now stored in `ssh-agent`.</span></span>

## <a name="using-ssh-copy-id-tooinstall-hello-new-key"></a><span data-ttu-id="1d7e9-167">Usar `ssh-copy-id` nueva clave de tooinstall Hola</span><span class="sxs-lookup"><span data-stu-id="1d7e9-167">Using `ssh-copy-id` tooinstall hello new key</span></span>
<span data-ttu-id="1d7e9-168">Si ya ha creado una máquina virtual puede instalar Hola nueva SSH pública clave tooyour VM de Linux con el siguiente comando, sustituyendo el nombre de usuario de hello VM y dirección del servidor hello con sus propios valores de hello:</span><span class="sxs-lookup"><span data-stu-id="1d7e9-168">If you have already created a VM you can install hello new SSH public key tooyour Linux VM with hello following command, replacing hello VM username and hello server address with your own values:</span></span>

```bash
ssh-copy-id -i ~/.ssh/id_rsa.pub ahmet@myserver
```

## <a name="create-and-configure-an-ssh-config-file"></a><span data-ttu-id="1d7e9-169">Creación y configuración de un archivo de configuración de SSH</span><span class="sxs-lookup"><span data-stu-id="1d7e9-169">Create and configure an SSH config file</span></span>

<span data-ttu-id="1d7e9-170">Trata de un toocreate de prácticas recomendada y configurar un `~/.ssh/config` toospeed archivo los inicios de sesión y para optimizar el comportamiento de cliente SSH.</span><span class="sxs-lookup"><span data-stu-id="1d7e9-170">It is a best practice toocreate and configure an `~/.ssh/config` file toospeed up log ins and for optimizing your SSH client behavior.</span></span>

<span data-ttu-id="1d7e9-171">Hola de ejemplo siguiente muestra una configuración estándar.</span><span class="sxs-lookup"><span data-stu-id="1d7e9-171">hello following example shows a standard configuration.</span></span>

### <a name="create-hello-file"></a><span data-ttu-id="1d7e9-172">Crear archivo hello</span><span class="sxs-lookup"><span data-stu-id="1d7e9-172">Create hello file</span></span>

```bash
touch ~/.ssh/config
```

### <a name="edit-hello-file-tooadd-hello-new-ssh-configuration"></a><span data-ttu-id="1d7e9-173">Editar configuración de SSH nuevo de hello archivo tooadd hello:</span><span class="sxs-lookup"><span data-stu-id="1d7e9-173">Edit hello file tooadd hello new SSH configuration:</span></span>

```bash
vim ~/.ssh/config
```

### <a name="example-sshconfig-file"></a><span data-ttu-id="1d7e9-174">Archivo `~/.ssh/config` de ejemplo:</span><span class="sxs-lookup"><span data-stu-id="1d7e9-174">Example `~/.ssh/config` file:</span></span>

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

<span data-ttu-id="1d7e9-175">Esto deja de configuración SSH se secciones para cada servidor tooenable cada toohave su propio par de claves dedicado.</span><span class="sxs-lookup"><span data-stu-id="1d7e9-175">This SSH config gives you sections for each server tooenable each toohave its own dedicated key pair.</span></span> <span data-ttu-id="1d7e9-176">Hola configuración predeterminada (`Host *`) son para todos los hosts que no coincide con cualquiera de hello hosts específicos más arriba en el archivo de configuración de Hola.</span><span class="sxs-lookup"><span data-stu-id="1d7e9-176">hello default settings (`Host *`) are for any hosts that do not match any of hello specific hosts higher up in hello config file.</span></span>

### <a name="config-file-explained"></a><span data-ttu-id="1d7e9-177">Explicación del archivo de configuración</span><span class="sxs-lookup"><span data-stu-id="1d7e9-177">Config file explained</span></span>

<span data-ttu-id="1d7e9-178">`Host`= nombre de hello del host de Hola que se llama en hello terminal.</span><span class="sxs-lookup"><span data-stu-id="1d7e9-178">`Host` = hello name of hello host being called on hello terminal.</span></span>  <span data-ttu-id="1d7e9-179">`ssh fedora22`indica a `SSH` toouse valores de hello en bloque de configuración de hello con la etiqueta `Host fedora22` Nota: Host puede ser cualquier etiqueta que tiene sentido para su uso y no representa Hola hostname real de cualquier servidor.</span><span class="sxs-lookup"><span data-stu-id="1d7e9-179">`ssh fedora22` tells `SSH` toouse hello values in hello settings block labeled `Host fedora22`  NOTE: Host can be any label that is logical for your usage and does not represent hello actual hostname of any server.</span></span>

<span data-ttu-id="1d7e9-180">`Hostname 102.160.203.241`= dirección IP de Hola o nombre DNS de servidor de Hola que se obtiene acceso.</span><span class="sxs-lookup"><span data-stu-id="1d7e9-180">`Hostname 102.160.203.241` = hello IP address or DNS name for hello server being accessed.</span></span>

<span data-ttu-id="1d7e9-181">`User ahmet`= toouse de cuenta de usuario remoto hello al iniciar sesión en el servidor de toohello.</span><span class="sxs-lookup"><span data-stu-id="1d7e9-181">`User ahmet` = hello remote user account toouse when logging in toohello server.</span></span>

<span data-ttu-id="1d7e9-182">`PubKeyAuthentication yes`= indica SSH desea toouse un toolog clave SSH.</span><span class="sxs-lookup"><span data-stu-id="1d7e9-182">`PubKeyAuthentication yes` = tells SSH you want toouse an SSH key toolog in.</span></span>

<span data-ttu-id="1d7e9-183">`IdentityFile /home/ahmet/.ssh/id_id_rsa`= la clave privada de SSH de Hola y toouse de clave pública correspondiente para la autenticación.</span><span class="sxs-lookup"><span data-stu-id="1d7e9-183">`IdentityFile /home/ahmet/.ssh/id_id_rsa` = hello SSH private key and corresponding public key toouse for authentication.</span></span>

## <a name="ssh-into-linux-without-a-password"></a><span data-ttu-id="1d7e9-184">SSH en Linux sin contraseña</span><span class="sxs-lookup"><span data-stu-id="1d7e9-184">SSH into Linux without a password</span></span>

<span data-ttu-id="1d7e9-185">Ahora que tiene un par de claves de SSH y un archivo de configuración SSH configurado, es capaz de toolog en tooyour VM de Linux rápida y segura.</span><span class="sxs-lookup"><span data-stu-id="1d7e9-185">Now that you have an SSH key pair and a configured SSH config file, you are able toolog in tooyour Linux VM quickly and securely.</span></span> <span data-ttu-id="1d7e9-186">Hola primera vez que inicie en servidor de tooa mediante un símbolo del sistema de hello clave SSH se Hola frase de contraseña para este archivo de clave.</span><span class="sxs-lookup"><span data-stu-id="1d7e9-186">hello first time you log in tooa server using an SSH key hello command prompts you for hello passphrase for that key file.</span></span>

```bash
ssh fedora22
```

### <a name="command-explained"></a><span data-ttu-id="1d7e9-187">Explicación del comando</span><span class="sxs-lookup"><span data-stu-id="1d7e9-187">Command explained</span></span>

<span data-ttu-id="1d7e9-188">Cuando `ssh fedora22` se ejecuta SSH primero busca y carga los valores de configuración de hello `Host fedora22` bloque y, a continuación, carga todos Hola restantes valores de hello último bloque, `Host *`.</span><span class="sxs-lookup"><span data-stu-id="1d7e9-188">When `ssh fedora22` is executed SSH first locates and loads any settings from hello `Host fedora22` block, and then loads all hello remaining settings from hello last block, `Host *`.</span></span>

## <a name="next-steps"></a><span data-ttu-id="1d7e9-189">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="1d7e9-189">Next Steps</span></span>

<span data-ttu-id="1d7e9-190">A continuación una es toocreate máquinas virtuales de Linux de Azure con hello nueva SSH clave pública.</span><span class="sxs-lookup"><span data-stu-id="1d7e9-190">Next up is toocreate Azure Linux VMs using hello new SSH public key.</span></span>  <span data-ttu-id="1d7e9-191">Máquinas virtuales de Azure que se crean con una clave pública SSH como inicio de sesión de hello son más segura que las máquinas virtuales creadas con el método de inicio de sesión de hello de forma predeterminada, las contraseñas.</span><span class="sxs-lookup"><span data-stu-id="1d7e9-191">Azure VMs that are created with an SSH public key as hello login are better secured than VMs created with hello default login method, passwords.</span></span>  <span data-ttu-id="1d7e9-192">Las máquinas virtuales de Azure creadas con claves SSH están configuradas de forma predeterminada con las contraseñas deshabilitadas, a fin de evitar los intentos de adivinarlas por fuerza bruta.</span><span class="sxs-lookup"><span data-stu-id="1d7e9-192">Azure VMs created using SSH keys are by default configured with passwords disabled, avoiding brute-forced guessing attempts.</span></span> <span data-ttu-id="1d7e9-193">Si necesita más ayuda para crear el par de claves de SSH o requieren certificados adicionales, por ejemplo, para usarlo con el portal clásico de hello, consulte [obtener certificados y pares de claves SSH pasos toocreate](create-ssh-keys-detailed.md).</span><span class="sxs-lookup"><span data-stu-id="1d7e9-193">If you need more assistance in creating your SSH key pair or require additional certificates, such as for use with hello classic portal, see [Detailed steps toocreate SSH key pairs and certificates](create-ssh-keys-detailed.md).</span></span>

* [<span data-ttu-id="1d7e9-194">Creación de una máquina virtual Linux protegida mediante una plantilla de Azure</span><span class="sxs-lookup"><span data-stu-id="1d7e9-194">Create a secure Linux VM using an Azure template</span></span>](create-ssh-secured-vm-from-template.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [<span data-ttu-id="1d7e9-195">Crear una VM de Linux segura mediante Hola portal de Azure</span><span class="sxs-lookup"><span data-stu-id="1d7e9-195">Create a secure Linux VM using hello Azure portal</span></span>](quick-create-portal.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [<span data-ttu-id="1d7e9-196">Crear una VM de Linux segura mediante Hola CLI de Azure</span><span class="sxs-lookup"><span data-stu-id="1d7e9-196">Create a secure Linux VM using hello Azure CLI</span></span>](quick-create-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
