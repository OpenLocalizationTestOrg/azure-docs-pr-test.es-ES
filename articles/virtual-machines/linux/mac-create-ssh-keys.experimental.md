---
title: "Creación de un par de claves SSH para máquinas virtuales Linux en Azure | Microsoft Docs"
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
ms.openlocfilehash: 19acd4efca7ef043f31b436b96f9129caee9591b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="create-an-ssh-public-and-private-key-pair-for-linux-vms"></a><span data-ttu-id="02040-103">Creación de un par de claves SSH pública y privada para máquinas virtuales Linux</span><span class="sxs-lookup"><span data-stu-id="02040-103">Create an SSH public and private key pair for Linux VMs</span></span>

<span data-ttu-id="02040-104">En este artículo se muestra cómo generar un par de archivos de clave pública y privada en formato RSA versión 2 del protocolo SSH para su uso en máquinas virtuales Linux.</span><span class="sxs-lookup"><span data-stu-id="02040-104">This article shows you how to generate an SSH protocol version 2 RSA public and private key file pair to use with Linux VMs.</span></span>  <span data-ttu-id="02040-105">Con un par de claves SSH, puede crear máquinas virtuales en Azure que usen claves SSH para autenticación de forma predeterminada, lo que elimina la necesidad de usar contraseñas para iniciar sesión.</span><span class="sxs-lookup"><span data-stu-id="02040-105">With an SSH key pair, you can create Virtual Machines on Azure that default to using SSH keys for authentication, eliminating the need for passwords to log in.</span></span>  <span data-ttu-id="02040-106">Las contraseñas se pueden adivinar y dejan las máquinas virtuales expuestas a intentos constantes de adivinarlas.</span><span class="sxs-lookup"><span data-stu-id="02040-106">Passwords can be guessed, and open your VMs up to relentless brute force attempts to guess your password.</span></span> <span data-ttu-id="02040-107">Las máquinas virtuales creadas con plantillas de Azure o la `azure-cli` pueden incluir la clave SSH pública como parte de la implementación, por lo que no es necesario deshabilitar el inicio de sesión con contraseña después de configurar la implementación.</span><span class="sxs-lookup"><span data-stu-id="02040-107">VMs created with Azure Templates or the `azure-cli` can include your SSH public key as part of the deployment, removing a post deployment configuration step of disabling password logins for SSH.</span></span>

## <a name="quick-commands"></a><span data-ttu-id="02040-108">Comandos rápidos</span><span class="sxs-lookup"><span data-stu-id="02040-108">Quick Commands</span></span>

<span data-ttu-id="02040-109">Ejecute los siguientes comandos desde un shell de Bash y reemplace los ejemplos por sus propios valores.</span><span class="sxs-lookup"><span data-stu-id="02040-109">Run the following commands from a Bash shell, replacing the examples with your own choices.</span></span>

<span data-ttu-id="02040-110">El archivo de clave pública SSH se crea de forma predeterminada en `~/.ssh/id_rsa.pub`.</span><span class="sxs-lookup"><span data-stu-id="02040-110">Your SSH public key file is by default created at `~/.ssh/id_rsa.pub`.</span></span> <span data-ttu-id="02040-111">Cuando se le solicite mediante el siguiente comando, debe crear una "frase de contraseña" para proteger la clave privada.</span><span class="sxs-lookup"><span data-stu-id="02040-111">When prompted using the following command, you should create a "passphrase" to secure your private key.</span></span> <span data-ttu-id="02040-112">(La frase de contraseña es una contraseña usada para cifrar la clave privada).</span><span class="sxs-lookup"><span data-stu-id="02040-112">(The passphrase is a password used to encrypt your private key.)</span></span>

```bash
ssh-keygen -t rsa -b 2048 
```

<span data-ttu-id="02040-113">Agregue la clave recién creada al `ssh-agent`:</span><span class="sxs-lookup"><span data-stu-id="02040-113">Add the newly created key to `ssh-agent`:</span></span>

```bash
ssh-add ~/.ssh/id_rsa
```

> [!IMPORTANT] 
> <span data-ttu-id="02040-114">Los comandos anteriores funcionan en sistemas operativos Linux de casi todas las distribuciones, pero no funcionan necesariamente en contenedores, dado que el entorno puede estar limitado radicalmente.</span><span class="sxs-lookup"><span data-stu-id="02040-114">The above commands work on Linux operating systems of almost all distributions, but do not necessarily work in containers, as the environment can be radically constrained.</span></span> 

## <a name="detailed-walkthrough"></a><span data-ttu-id="02040-115">Tutorial detallado</span><span class="sxs-lookup"><span data-stu-id="02040-115">Detailed Walkthrough</span></span>

<span data-ttu-id="02040-116">El uso de claves públicas y privadas SSH es la manera más fácil de iniciar sesión en los servidores de Linux.</span><span class="sxs-lookup"><span data-stu-id="02040-116">Using SSH public and private keys is the easiest way to log in to your Linux servers.</span></span> <span data-ttu-id="02040-117">La [criptografía de clave pública](https://en.wikipedia.org/wiki/Public-key_cryptography) ofrece una manera mucho más segura que las contraseñas de iniciar sesión en la máquina virtual Linux o BSD en Azure, que pueden ser forzadas con mucha más facilidad.</span><span class="sxs-lookup"><span data-stu-id="02040-117">[Public-key cryptography](https://en.wikipedia.org/wiki/Public-key_cryptography) provides a much more secure way to log in to your Linux or BSD VM in Azure than passwords, which can be brute-forced far more easily.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="02040-118">La clave pública se puede compartir con cualquiera. Sin embargo, la clave privada es propiedad exclusivamente suya (o de su infraestructura de seguridad local).</span><span class="sxs-lookup"><span data-stu-id="02040-118">Your public key can be shared with anyone; but only you (or your local security infrastructure) possess your private key.</span></span>  <span data-ttu-id="02040-119">La clave privada SSH debe tener una [contraseña muy segura ](https://www.xkcd.com/936/) (origen:[xkcd.com](https://xkcd.com)) para protegerla.</span><span class="sxs-lookup"><span data-stu-id="02040-119">The SSH private key should have a [very secure password](https://www.xkcd.com/936/) (source:[xkcd.com](https://xkcd.com)) to safeguard it.</span></span>  <span data-ttu-id="02040-120">Esta contraseña solo sirve para acceder a la clave privada SSH y **no es** la contraseña de la cuenta de usuario.</span><span class="sxs-lookup"><span data-stu-id="02040-120">This password is just to access the private SSH key and **is not** the user account password.</span></span>  <span data-ttu-id="02040-121">Cuando agrega una contraseña a la clave SSH, esta cifra la clave privada mediante AES de 128 bits para que no se pueda usar sin la contraseña que la descifra.</span><span class="sxs-lookup"><span data-stu-id="02040-121">When you add a password to your SSH key, it encrypts the private key using 128-bit AES, so that the private key is useless without the password to decrypt it.</span></span>  <span data-ttu-id="02040-122">Si un atacante robara la clave privada y esta no tuviera contraseña, podría usarla para iniciar sesión en los servidores que tuvieran instalada la clave pública correspondiente.</span><span class="sxs-lookup"><span data-stu-id="02040-122">If an attacker stole your private key and that key did not have a password, they would be able to use that private key to log in to any servers that have the corresponding public key.</span></span>  <span data-ttu-id="02040-123">Si una clave privada está protegida con una contraseña, el atacante no podrá usarla, ya que la contraseña constituye un nivel adicional de seguridad en la infraestructura de Azure.</span><span class="sxs-lookup"><span data-stu-id="02040-123">If a private key is password protected it cannot be used by that attacker, providing an additional layer of security for your infrastructure on Azure.</span></span>

<span data-ttu-id="02040-124">En este artículo se crean archivos de clave pública y privada con el formato RSA versión 2 del protocolo SSH, que son los recomendados para las implementaciones en Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="02040-124">This article creates SSH protocol version 2 RSA public and private key files, which are recommended for deployments on the Resource Manager.</span></span>  <span data-ttu-id="02040-125">Las claves *ssh-rsa* se requieren en el [portal](https://portal.azure.com) tanto para las implementaciones clásicas como para las de Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="02040-125">*ssh-rsa* keys are required on the [portal](https://portal.azure.com) for both classic and Resource Manager deployments.</span></span>

## <a name="disable-ssh-passwords-by-using-ssh-keys"></a><span data-ttu-id="02040-126">Deshabilitar contraseñas SSH mediante claves SSH</span><span class="sxs-lookup"><span data-stu-id="02040-126">Disable SSH passwords by using SSH keys</span></span>

<span data-ttu-id="02040-127">Azure requiere al menos claves públicas y privadas de 2048 bits con el formato ssh-rsa.</span><span class="sxs-lookup"><span data-stu-id="02040-127">Azure requires at least 2048-bit, ssh-rsa format public and private keys.</span></span> <span data-ttu-id="02040-128">Para crear las claves, use `ssh-keygen`, que realiza una serie de preguntas y después escribe una clave privada y una clave pública correspondiente.</span><span class="sxs-lookup"><span data-stu-id="02040-128">To create the keys use `ssh-keygen`, which asks a series of questions and then writes a private key and a matching public key.</span></span> <span data-ttu-id="02040-129">Cuando se crea una máquina virtual de Azure, la clave pública se copia en `~/.ssh/authorized_keys`.</span><span class="sxs-lookup"><span data-stu-id="02040-129">When an Azure VM is created, the public key is copied to `~/.ssh/authorized_keys`.</span></span>  <span data-ttu-id="02040-130">Las claves SSH en `~/.ssh/authorized_keys` se utilizan para presentar un desafío al cliente, que debe proporcionar la clave privada correspondiente en una conexión de inicio de sesión SSH.</span><span class="sxs-lookup"><span data-stu-id="02040-130">SSH keys in `~/.ssh/authorized_keys` are used to challenge the client to match the corresponding private key on an SSH login connection.</span></span>  <span data-ttu-id="02040-131">Cuando se crea una máquina virtual Linux de Azure que usa claves SSH para la autenticación, Azure configura el servidor SSHD para no permitir inicios de sesión con contraseña, solo las claves SSH.</span><span class="sxs-lookup"><span data-stu-id="02040-131">When an Azure Linux VM is created using SSH keys for authentication, Azure configures the SSHD server to not allow password logins, only SSH keys.</span></span>  <span data-ttu-id="02040-132">Por lo tanto, mediante la creación de máquinas virtuales Linux de Azure con claves SSH, puede ayudar a proteger la implementación de la máquina virtual y a ahorrarse el paso de configuración que es habitual después de la implementación para deshabilitar las contraseñas en el archivo de configuración sshd_config.</span><span class="sxs-lookup"><span data-stu-id="02040-132">Therefore, by creating Azure Linux VMs with SSH keys, you can help secure the VM deployment and save yourself the typical post-deployment configuration step of disabling passwords in the sshd_config config file.</span></span>

## <a name="using-ssh-keygen"></a><span data-ttu-id="02040-133">Uso de ssh-keygen</span><span class="sxs-lookup"><span data-stu-id="02040-133">Using ssh-keygen</span></span>

<span data-ttu-id="02040-134">Este comando crea un par de claves SSH protegidas con contraseña (cifradas) mediante RSA de 2048 bits e incluye un comentario para que se pueda identificar fácilmente.</span><span class="sxs-lookup"><span data-stu-id="02040-134">This command creates a password secured (encrypted) SSH key pair using 2048-bit RSA and it is commented to easily identify it.</span></span>  

<span data-ttu-id="02040-135">Las claves SSH se mantienen de forma predeterminada en el directorio `~/.ssh`.</span><span class="sxs-lookup"><span data-stu-id="02040-135">SSH keys are by default kept in the `~/.ssh` directory.</span></span>  <span data-ttu-id="02040-136">Si no tiene un directorio `~/.ssh`, el comando `ssh-keygen` lo crea automáticamente con los permisos correctos.</span><span class="sxs-lookup"><span data-stu-id="02040-136">If you do not have a `~/.ssh` directory, the `ssh-keygen` command creates it for you with the correct permissions.</span></span>

```bash
ssh-keygen \
-t rsa \
-b 2048 
```

<span data-ttu-id="02040-137">*Explicación del comando*</span><span class="sxs-lookup"><span data-stu-id="02040-137">*Command explained*</span></span>

<span data-ttu-id="02040-138">`ssh-keygen` = programa usado para crear las claves;</span><span class="sxs-lookup"><span data-stu-id="02040-138">`ssh-keygen` = the program used to create the keys</span></span>

<span data-ttu-id="02040-139">`-t rsa` = el tipo de clave que se va a crear que está en el formato RSA [wikipedia] (https://en.wikipedia.org/wiki/RSA_(cryptosystem)</span><span class="sxs-lookup"><span data-stu-id="02040-139">`-t rsa` = type of key to create which is the RSA format [wikipedia](https://en.wikipedia.org/wiki/RSA_(cryptosystem)</span></span>

<span data-ttu-id="02040-140">`-b 2048` = bits de la clave;</span><span class="sxs-lookup"><span data-stu-id="02040-140">`-b 2048` = bits of the key</span></span>


## <a name="classic-portal-and-x509-certs"></a><span data-ttu-id="02040-141">Portal clásico y certificados X.509</span><span class="sxs-lookup"><span data-stu-id="02040-141">Classic portal and X.509 certs</span></span>

<span data-ttu-id="02040-142">Si usa el [Portal de Azure clásico](https://manage.windowsazure.com/), este requiere certificados X.509 para las claves SSH.</span><span class="sxs-lookup"><span data-stu-id="02040-142">If you are using the Azure [classic portal](https://manage.windowsazure.com/), it requires X.509 certs for the SSH keys.</span></span>  <span data-ttu-id="02040-143">No se permite ningún otro tipo de claves públicas SSH, *deben* ser certificados X.509.</span><span class="sxs-lookup"><span data-stu-id="02040-143">No other types of SSH public keys are allowed, they *must* be X.509 certs.</span></span>

<span data-ttu-id="02040-144">Para crear un certificado X.509 a partir de la clave privada SSH-RSA existente:</span><span class="sxs-lookup"><span data-stu-id="02040-144">To create an X.509 cert from your existing SSH-RSA private key:</span></span>

```bash
openssl req -x509 \
-key ~/.ssh/id_rsa \
-nodes \
-days 365 \
-newkey rsa:2048 \
-out ~/.ssh/id_rsa.pem
```

## <a name="classic-deploy-using-asm"></a><span data-ttu-id="02040-145">Implementación clásica mediante `asm`</span><span class="sxs-lookup"><span data-stu-id="02040-145">Classic deploy using `asm`</span></span>

<span data-ttu-id="02040-146">Si usa el modelo de implementación clásica (CLI de Azure Service Management`asm`), puede usar una clave pública SSH-RSA o una clave con formato RFC4716 en un contenedor **.pem**.</span><span class="sxs-lookup"><span data-stu-id="02040-146">If you are using the classic deploy model (Azure service management CLI `asm`), you can use an SSH-RSA public key or an RFC4716 formatted key in a **.pem** container.</span></span>  <span data-ttu-id="02040-147">La clave pública SSH-RSA es la que se creó anteriormente en este artículo mediante `ssh-keygen`.</span><span class="sxs-lookup"><span data-stu-id="02040-147">The SSH-RSA public key is what was created earlier in this article using `ssh-keygen`.</span></span>

<span data-ttu-id="02040-148">Para crear una clave con formato RFC4716 a partir de una clave pública SSH existente:</span><span class="sxs-lookup"><span data-stu-id="02040-148">To create a RFC4716 formatted key from an existing SSH public key:</span></span>

```bash
ssh-keygen \
-f ~/.ssh/id_rsa.pub \
-e \
-m RFC4716 > ~/.ssh/id_ssh2.pem
```

## <a name="example-of-ssh-keygen"></a><span data-ttu-id="02040-149">Ejemplo de ssh-keygen</span><span class="sxs-lookup"><span data-stu-id="02040-149">Example of ssh-keygen</span></span>

```bash
ssh-keygen -t rsa -b 2048 -C "ahmet@myserver"
Generating public/private rsa key pair.
Enter file in which to save the key (/home/ahmet/.ssh/id_rsa): 
Enter passphrase (empty for no passphrase):
Enter same passphrase again:
Your identification has been saved in /home/ahmet/.ssh/id_rsa.
Your public key has been saved in /home/ahmet/.ssh/id_rsa.pub.
The key fingerprint is:
14:a3:cb:3e:78:ad:25:cc:55:e9:0c:08:e5:d1:a9:08 ahmet@myserver
The keys randomart image is:
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

<span data-ttu-id="02040-150">Archivos de clave guardados:</span><span class="sxs-lookup"><span data-stu-id="02040-150">Saved key files:</span></span>

`Enter file in which to save the key (/home/ahmet/.ssh/id_rsa): ~/.ssh/id_rsa`

<span data-ttu-id="02040-151">El nombre del par de claves en este artículo.</span><span class="sxs-lookup"><span data-stu-id="02040-151">The key pair name for this article.</span></span>  <span data-ttu-id="02040-152">Tener un par de claves denominado **id_rsa** es el valor predeterminado y algunas herramientas podrían esperar **id_rsa** como nombre del archivo de la clave privada, así que es buena idea tener uno.</span><span class="sxs-lookup"><span data-stu-id="02040-152">Having a key pair named **id_rsa** is the default and some tools might expect the **id_rsa** private key file name so having one is a good idea.</span></span> <span data-ttu-id="02040-153">El directorio `~/.ssh/` es la ubicación predeterminada para los pares de claves SSH y el archivo de configuración de SSH.</span><span class="sxs-lookup"><span data-stu-id="02040-153">The directory `~/.ssh/` is the default location for SSH key pairs and the SSH config file.</span></span>  <span data-ttu-id="02040-154">Si no se especifica con una ruta de acceso completa, `ssh-keygen` creará las claves en el directorio de trabajo actual, no en el predeterminado `~/.ssh`.</span><span class="sxs-lookup"><span data-stu-id="02040-154">If not specified with a full path, `ssh-keygen` will create the keys in the current working directory, not the default `~/.ssh`.</span></span>

<span data-ttu-id="02040-155">Una lista del directorio `~/.ssh` .</span><span class="sxs-lookup"><span data-stu-id="02040-155">A listing of the `~/.ssh` directory.</span></span>

```bash
ls -al ~/.ssh
-rw------- 1 ahmet staff  1675 Aug 25 18:04 id_rsa
-rw-r--r-- 1 ahmet staff   410 Aug 25 18:04 rsa.pub
```

<span data-ttu-id="02040-156">Contraseña de la clave:</span><span class="sxs-lookup"><span data-stu-id="02040-156">Key Password:</span></span>

`Enter passphrase (empty for no passphrase):`

<span data-ttu-id="02040-157">`ssh-keygen` hace referencia a una contraseña que se usa para cifrar el archivo de clave privada como "una frase de contraseña".</span><span class="sxs-lookup"><span data-stu-id="02040-157">`ssh-keygen` refers to a password used to encrypt the private key as "a passphrase."</span></span>  <span data-ttu-id="02040-158">Es *muy* recomendable agregar una frase de contraseña a los pares de clave.</span><span class="sxs-lookup"><span data-stu-id="02040-158">It is *strongly* recommended to add a passphrase to your key pairs.</span></span> <span data-ttu-id="02040-159">Sin una frase de contraseña que proteja la clave privada, cualquiera que disponga del archivo de clave puede usarlo para iniciar sesión en cualquier servidor que tenga la clave pública correspondiente.</span><span class="sxs-lookup"><span data-stu-id="02040-159">Without a passphrase protecting the private key, anyone with the key file can use it to log in to any server that has the corresponding public key.</span></span> <span data-ttu-id="02040-160">El uso de una frase de contraseña ofrece más protección en caso de que alguien obtenga acceso al archivo de clave privada, lo que le dará tiempo para cambiar las claves que se usan para autenticarse.</span><span class="sxs-lookup"><span data-stu-id="02040-160">Adding a passphrase offers more protection in case someone is able to gain access to your private key file, giving you time to change the keys used to authenticate you.</span></span>

## <a name="using-ssh-agent-to-store-your-private-key-password"></a><span data-ttu-id="02040-161">Uso de ssh-agent para almacenar la contraseña de clave privada</span><span class="sxs-lookup"><span data-stu-id="02040-161">Using ssh-agent to store your private key password</span></span>

<span data-ttu-id="02040-162">Para no tener que escribir la frase de contraseña del archivo de clave privada con cada inicio de sesión SSH, puede usar `ssh-agent` para almacenar en caché la contraseña del archivo de clave privada.</span><span class="sxs-lookup"><span data-stu-id="02040-162">To avoid typing your private key file passphrase with every SSH login, you can use `ssh-agent` to cache your private key file password.</span></span> <span data-ttu-id="02040-163">Si usa Mac, Llaveros en OSX almacena de forma segura las contraseñas de clave privada cuando invoque `ssh-agent`.</span><span class="sxs-lookup"><span data-stu-id="02040-163">If you are using a Mac, the OSX Keychain securely stores the private key passwords when you invoke `ssh-agent`.</span></span>

<span data-ttu-id="02040-164">Compruebe y use `ssh-agent` y `ssh-add` para informar al sistema SSH acerca de los archivos de clave para que no sea necesario usar la frase de contraseña de forma interactiva.</span><span class="sxs-lookup"><span data-stu-id="02040-164">Verify and use `ssh-agent` and `ssh-add` to inform the SSH system about the key files so that the passphrase will not need to be used interactively.</span></span>

```bash
eval "$(ssh-agent -s)"
```

<span data-ttu-id="02040-165">Ahora, agregue la clave privada a `ssh-agent` mediante el comando `ssh-add`.</span><span class="sxs-lookup"><span data-stu-id="02040-165">Now add the private key to `ssh-agent` using the command `ssh-add`.</span></span>

```bash
ssh-add ~/.ssh/id_rsa
```

<span data-ttu-id="02040-166">La contraseña de clave privada está almacenada ahora en `ssh-agent`.</span><span class="sxs-lookup"><span data-stu-id="02040-166">The private key password is now stored in `ssh-agent`.</span></span>

## <a name="using-ssh-copy-id-to-install-the-new-key"></a><span data-ttu-id="02040-167">Uso de `ssh-copy-id` para instalar la nueva clave</span><span class="sxs-lookup"><span data-stu-id="02040-167">Using `ssh-copy-id` to install the new key</span></span>
<span data-ttu-id="02040-168">Si ya ha creado una máquina virtual, puede instalar la nueva clave pública SSH en la máquina virtual Linux con el siguiente comando, sustituyendo el nombre de usuario de la máquina virtual y la dirección del servidor por sus propios valores:</span><span class="sxs-lookup"><span data-stu-id="02040-168">If you have already created a VM you can install the new SSH public key to your Linux VM with the following command, replacing the VM username and the server address with your own values:</span></span>

```bash
ssh-copy-id -i ~/.ssh/id_rsa.pub ahmet@myserver
```

## <a name="create-and-configure-an-ssh-config-file"></a><span data-ttu-id="02040-169">Creación y configuración de un archivo de configuración de SSH</span><span class="sxs-lookup"><span data-stu-id="02040-169">Create and configure an SSH config file</span></span>

<span data-ttu-id="02040-170">Es un procedimiento recomendado crear y configurar un archivo `~/.ssh/config` para acelerar los inicios de sesión y optimizar el comportamiento del cliente SSH.</span><span class="sxs-lookup"><span data-stu-id="02040-170">It is a best practice to create and configure an `~/.ssh/config` file to speed up log ins and for optimizing your SSH client behavior.</span></span>

<span data-ttu-id="02040-171">En el ejemplo siguiente se muestra una configuración estándar.</span><span class="sxs-lookup"><span data-stu-id="02040-171">The following example shows a standard configuration.</span></span>

### <a name="create-the-file"></a><span data-ttu-id="02040-172">Creación del archivo</span><span class="sxs-lookup"><span data-stu-id="02040-172">Create the file</span></span>

```bash
touch ~/.ssh/config
```

### <a name="edit-the-file-to-add-the-new-ssh-configuration"></a><span data-ttu-id="02040-173">Edite el archivo para agregar la nueva configuración de SSH:</span><span class="sxs-lookup"><span data-stu-id="02040-173">Edit the file to add the new SSH configuration:</span></span>

```bash
vim ~/.ssh/config
```

### <a name="example-sshconfig-file"></a><span data-ttu-id="02040-174">Archivo `~/.ssh/config` de ejemplo:</span><span class="sxs-lookup"><span data-stu-id="02040-174">Example `~/.ssh/config` file:</span></span>

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

<span data-ttu-id="02040-175">Esta configuración de SSH ofrece secciones para cada servidor para que cada uno tenga su propio par de claves dedicado.</span><span class="sxs-lookup"><span data-stu-id="02040-175">This SSH config gives you sections for each server to enable each to have its own dedicated key pair.</span></span> <span data-ttu-id="02040-176">La configuración predeterminada (`Host *`) es para los hosts que no coincidan con ninguno de los hosts específicos más arriba en el archivo de configuración.</span><span class="sxs-lookup"><span data-stu-id="02040-176">The default settings (`Host *`) are for any hosts that do not match any of the specific hosts higher up in the config file.</span></span>

### <a name="config-file-explained"></a><span data-ttu-id="02040-177">Explicación del archivo de configuración</span><span class="sxs-lookup"><span data-stu-id="02040-177">Config file explained</span></span>

<span data-ttu-id="02040-178">`Host` = nombre del host al que se llama en el terminal.</span><span class="sxs-lookup"><span data-stu-id="02040-178">`Host` = the name of the host being called on the terminal.</span></span>  <span data-ttu-id="02040-179">`ssh fedora22` indica a `SSH` que use los valores del bloque de configuración con la etiqueta `Host fedora22`. NOTA: el host puede ser cualquier etiqueta que resulte lógica para su uso y no representa el nombre de host real de ningún servidor.</span><span class="sxs-lookup"><span data-stu-id="02040-179">`ssh fedora22` tells `SSH` to use the values in the settings block labeled `Host fedora22`  NOTE: Host can be any label that is logical for your usage and does not represent the actual hostname of any server.</span></span>

<span data-ttu-id="02040-180">`Hostname 102.160.203.241` = dirección IP o nombre DNS del servidor al que se está accediendo.</span><span class="sxs-lookup"><span data-stu-id="02040-180">`Hostname 102.160.203.241` = the IP address or DNS name for the server being accessed.</span></span>

<span data-ttu-id="02040-181">`User ahmet` = cuenta de usuario remoto que se usará al iniciar sesión en el servidor.</span><span class="sxs-lookup"><span data-stu-id="02040-181">`User ahmet` = the remote user account to use when logging in to the server.</span></span>

<span data-ttu-id="02040-182">`PubKeyAuthentication yes` = indica a SSH que desea usar una clave SSH para iniciar sesión.</span><span class="sxs-lookup"><span data-stu-id="02040-182">`PubKeyAuthentication yes` = tells SSH you want to use an SSH key to log in.</span></span>

<span data-ttu-id="02040-183">`IdentityFile /home/ahmet/.ssh/id_id_rsa` = clave privada SSH y clave pública correspondiente que se usan para la autenticación.</span><span class="sxs-lookup"><span data-stu-id="02040-183">`IdentityFile /home/ahmet/.ssh/id_id_rsa` = the SSH private key and corresponding public key to use for authentication.</span></span>

## <a name="ssh-into-linux-without-a-password"></a><span data-ttu-id="02040-184">SSH en Linux sin contraseña</span><span class="sxs-lookup"><span data-stu-id="02040-184">SSH into Linux without a password</span></span>

<span data-ttu-id="02040-185">Ahora que tiene un par de claves SSH y un archivo de configuración de SSH configurado, puede iniciar sesión en la máquina virtual Linux de forma rápida y segura.</span><span class="sxs-lookup"><span data-stu-id="02040-185">Now that you have an SSH key pair and a configured SSH config file, you are able to log in to your Linux VM quickly and securely.</span></span> <span data-ttu-id="02040-186">La primera vez que inicie sesión en un servidor mediante una clave SSH, el símbolo del sistema le pedirá la frase de contraseña para ese archivo de clave.</span><span class="sxs-lookup"><span data-stu-id="02040-186">The first time you log in to a server using an SSH key the command prompts you for the passphrase for that key file.</span></span>

```bash
ssh fedora22
```

### <a name="command-explained"></a><span data-ttu-id="02040-187">Explicación del comando</span><span class="sxs-lookup"><span data-stu-id="02040-187">Command explained</span></span>

<span data-ttu-id="02040-188">Cuando se ejecuta `ssh fedora22`, primero SSH busca y carga la configuración del bloque `Host fedora22` y, después, carga la configuración restante del último bloque, `Host *`.</span><span class="sxs-lookup"><span data-stu-id="02040-188">When `ssh fedora22` is executed SSH first locates and loads any settings from the `Host fedora22` block, and then loads all the remaining settings from the last block, `Host *`.</span></span>

## <a name="next-steps"></a><span data-ttu-id="02040-189">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="02040-189">Next Steps</span></span>

<span data-ttu-id="02040-190">El siguiente paso es crear máquinas virtuales de Linux en Azure con la nueva clave pública SSH.</span><span class="sxs-lookup"><span data-stu-id="02040-190">Next up is to create Azure Linux VMs using the new SSH public key.</span></span>  <span data-ttu-id="02040-191">Las máquinas virtuales de Azure que se crean con una clave pública SSH como inicio de sesión están mejor protegidas que las creadas con contraseñas, el método de inicio de sesión predeterminado.</span><span class="sxs-lookup"><span data-stu-id="02040-191">Azure VMs that are created with an SSH public key as the login are better secured than VMs created with the default login method, passwords.</span></span>  <span data-ttu-id="02040-192">Las máquinas virtuales de Azure creadas con claves SSH están configuradas de forma predeterminada con las contraseñas deshabilitadas, a fin de evitar los intentos de adivinarlas por fuerza bruta.</span><span class="sxs-lookup"><span data-stu-id="02040-192">Azure VMs created using SSH keys are by default configured with passwords disabled, avoiding brute-forced guessing attempts.</span></span> <span data-ttu-id="02040-193">Si necesita más ayuda para crear el par de claves SSH o requiere certificados adicionales, para su uso en el portal clásico, consulte los [pasos detallados para crear los pares de clave SSH y los certificados](create-ssh-keys-detailed.md).</span><span class="sxs-lookup"><span data-stu-id="02040-193">If you need more assistance in creating your SSH key pair or require additional certificates, such as for use with the classic portal, see [Detailed steps to create SSH key pairs and certificates](create-ssh-keys-detailed.md).</span></span>

* [<span data-ttu-id="02040-194">Creación de una máquina virtual Linux protegida mediante una plantilla de Azure</span><span class="sxs-lookup"><span data-stu-id="02040-194">Create a secure Linux VM using an Azure template</span></span>](create-ssh-secured-vm-from-template.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [<span data-ttu-id="02040-195">Creación de una máquina virtual Linux protegida mediante Azure Portal</span><span class="sxs-lookup"><span data-stu-id="02040-195">Create a secure Linux VM using the Azure portal</span></span>](quick-create-portal.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [<span data-ttu-id="02040-196">Crear una máquina virtual de Linux segura mediante la CLI de Azure</span><span class="sxs-lookup"><span data-stu-id="02040-196">Create a secure Linux VM using the Azure CLI</span></span>](quick-create-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
