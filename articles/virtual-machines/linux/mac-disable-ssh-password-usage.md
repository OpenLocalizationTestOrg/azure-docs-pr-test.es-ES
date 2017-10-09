---
title: "las contraseñas SSH de aaaDisable en la VM de Linux mediante la configuración SSHD | Documentos de Microsoft"
description: "Proteja su máquina virtual de Linux en Azure mediante la deshabilitación de los inicios de sesión mediante contraseña para SSH."
services: virtual-machines-linux
documentationcenter: 
author: vlivech
manager: timlt
editor: 
tags: 
ms.assetid: 46137640-a7d2-40e5-a1e9-9effef7eb190
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 08/26/2016
ms.author: v-livech
ms.openlocfilehash: fb67b2f5b8b3bf2ba214858940b04f2ea9013fb5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="disable-ssh-passwords-on-your-linux-vm-by-configuring-sshd"></a><span data-ttu-id="96718-103">Deshabilitación de las contraseñas SSH en la máquina virtual de Linux mediante la configuración de SSHD</span><span class="sxs-lookup"><span data-stu-id="96718-103">Disable SSH passwords on your Linux VM by configuring SSHD</span></span>
<span data-ttu-id="96718-104">En este artículo se centra en cómo toolock la seguridad de inicio de sesión de saludo de la VM de Linux.</span><span class="sxs-lookup"><span data-stu-id="96718-104">This article focuses on how toolock down hello login security of your Linux VM.</span></span>  <span data-ttu-id="96718-105">En cuanto se abre el puerto SSH 22 hello toohello world bots empieza toologin al tratar de adivinar las contraseñas.</span><span class="sxs-lookup"><span data-stu-id="96718-105">As soon as hello SSH port 22 is opened toohello world bots start trying toologin by guessing passwords.</span></span>  <span data-ttu-id="96718-106">Lo que haremos en este artículo es deshabilitar los inicios de sesión de contraseña a través de SSH.</span><span class="sxs-lookup"><span data-stu-id="96718-106">What we will do in this article is disable password logins over SSH.</span></span>  <span data-ttu-id="96718-107">Quitando completamente la capacidad de hello contraseñas toouse protegemos Hola Linux VM de este tipo de ataques de ataque de fuerza.</span><span class="sxs-lookup"><span data-stu-id="96718-107">By completely removing hello ability toouse passwords we protect hello Linux VM from this type of brute force attack.</span></span>  <span data-ttu-id="96718-108">Hola agregado bonificación es configuramos SSHD Linux tooonly permitir inicios de sesión a través de SSH claves públicas y privadas, con diferencia Hola tooLinux de toologin de manera más segura.</span><span class="sxs-lookup"><span data-stu-id="96718-108">hello added bonus is we will configure Linux SSHD tooonly allow logins via SSH public & private keys, by far hello most secure way toologin tooLinux.</span></span>  <span data-ttu-id="96718-109">las posibles combinaciones de Hello del mismo requeriría clave privada de tooguess hello es inmensa y, por tanto, no recomienda: bots de molestarle incluso claves SSH de tootry toobrute force.</span><span class="sxs-lookup"><span data-stu-id="96718-109">hello possible combinations of it would require tooguess hello private key is immense and therefore discourages bots from even bothering tootry toobrute force SSH keys.</span></span>

## <a name="goals"></a><span data-ttu-id="96718-110">Objetivos</span><span class="sxs-lookup"><span data-stu-id="96718-110">Goals</span></span>
* <span data-ttu-id="96718-111">Configurar SSHD toodisallow:</span><span class="sxs-lookup"><span data-stu-id="96718-111">Configure SSHD toodisallow:</span></span>
  * <span data-ttu-id="96718-112">Inicios de sesión de contraseña</span><span class="sxs-lookup"><span data-stu-id="96718-112">Password logins</span></span>
  * <span data-ttu-id="96718-113">Inicio de sesión de usuario raíz</span><span class="sxs-lookup"><span data-stu-id="96718-113">Root user login</span></span>
  * <span data-ttu-id="96718-114">Autenticación de desafío/respuesta</span><span class="sxs-lookup"><span data-stu-id="96718-114">Challenge-response authentication</span></span>
* <span data-ttu-id="96718-115">Configurar SSHD tooallow:</span><span class="sxs-lookup"><span data-stu-id="96718-115">Configure SSHD tooallow:</span></span>
  * <span data-ttu-id="96718-116">solo inicios de sesión de claves de SSH</span><span class="sxs-lookup"><span data-stu-id="96718-116">only SSH key logins</span></span>
* <span data-ttu-id="96718-117">Reiniciar SSHD mientras sigue conectado</span><span class="sxs-lookup"><span data-stu-id="96718-117">Restart SSHD while still logged in</span></span>
* <span data-ttu-id="96718-118">Configuración de prueba Hola nueva SSHD</span><span class="sxs-lookup"><span data-stu-id="96718-118">Test hello new SSHD configuration</span></span>

## <a name="introduction"></a><span data-ttu-id="96718-119">Introducción</span><span class="sxs-lookup"><span data-stu-id="96718-119">Introduction</span></span>
[<span data-ttu-id="96718-120">SSH definido</span><span class="sxs-lookup"><span data-stu-id="96718-120">SSH defined</span></span>](https://en.wikipedia.org/wiki/Secure_Shell)

<span data-ttu-id="96718-121">SSHD es hello servidor SSH que se ejecuta en hello VM de Linux.</span><span class="sxs-lookup"><span data-stu-id="96718-121">SSHD is hello SSH Server that runs on hello Linux VM.</span></span>  <span data-ttu-id="96718-122">SSH es un cliente que se ejecuta desde un shell en la estación de trabajo MacBook o Linux.</span><span class="sxs-lookup"><span data-stu-id="96718-122">SSH is a client that runs from a shell on your MacBook or Linux workstation.</span></span>  <span data-ttu-id="96718-123">SSH es también protocolo hello usa toosecure y cifrar la comunicación de hello entre la estación de trabajo y Hola VM de Linux.</span><span class="sxs-lookup"><span data-stu-id="96718-123">SSH is also hello protocol used toosecure and encrypt hello communication between your workstation and hello Linux VM.</span></span>

<span data-ttu-id="96718-124">Para este artículo es muy importante tookeep un inicio de sesión tooyour recorrer Linux VM abierto para hello todo.</span><span class="sxs-lookup"><span data-stu-id="96718-124">For this article it is very important tookeep one login tooyour Linux VM open for hello entire walk through.</span></span>  <span data-ttu-id="96718-125">Por esta razón se abrirá dos terminales y SSH toohello VM Linux de ambos.</span><span class="sxs-lookup"><span data-stu-id="96718-125">For this reason we will open two terminals and SSH toohello Linux VM from both of them.</span></span>  <span data-ttu-id="96718-126">Se usará el archivo de configuración de hello primera terminal toomake Hola cambios tooSSHDs y reiniciar servicio de hello SSHD.</span><span class="sxs-lookup"><span data-stu-id="96718-126">We will use hello first terminal toomake hello changes tooSSHDs configuration file and restart hello SSHD service.</span></span>  <span data-ttu-id="96718-127">Usaremos Hola segundo terminal tootest los cambios una vez que se reinicie el servicio de Hola.</span><span class="sxs-lookup"><span data-stu-id="96718-127">We will use hello second terminal tootest those changes once hello service is restarted.</span></span>  <span data-ttu-id="96718-128">Ya se están deshabilitando las contraseñas SSH y basarse estrictamente en claves SSH, si las claves SSH no son correctas y cierra Hola conexión toohello VM, hello VM será permanentemente bloqueado y nadie será tooit toologin puede requerir toobe eliminado y vuelto a crear.</span><span class="sxs-lookup"><span data-stu-id="96718-128">Because we are disabling SSH passwords and relying strictly on SSH keys, if your SSH keys are not correct and you close hello connection toohello VM, hello VM will be permanently locked and no one will be able toologin tooit requiring it toobe deleted and recreated.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="96718-129">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="96718-129">Prerequisites</span></span>
* [<span data-ttu-id="96718-130">Creación de claves SSH en Linux y Mac para máquinas virtuales Linux en Azure</span><span class="sxs-lookup"><span data-stu-id="96718-130">Create SSH keys on Linux and Mac for Linux VMs in Azure</span></span>](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* <span data-ttu-id="96718-131">Cuenta de Azure</span><span class="sxs-lookup"><span data-stu-id="96718-131">Azure account</span></span>
  * [<span data-ttu-id="96718-132">registro de versión de prueba gratuita</span><span class="sxs-lookup"><span data-stu-id="96718-132">free trial signup</span></span>](https://azure.microsoft.com/pricing/free-trial/)
  * [<span data-ttu-id="96718-133">Portal de Azure</span><span class="sxs-lookup"><span data-stu-id="96718-133">Azure portal</span></span>](http://portal.azure.com)
* <span data-ttu-id="96718-134">Máquina virtual de Linux que se ejecuta en Azure</span><span class="sxs-lookup"><span data-stu-id="96718-134">Linux VM running on azure</span></span>
* <span data-ttu-id="96718-135">Par de claves públicas y privadas SSH en `~/.ssh/`</span><span class="sxs-lookup"><span data-stu-id="96718-135">SSH public & private key pair in `~/.ssh/`</span></span>
* <span data-ttu-id="96718-136">Clave pública SSH en `~/.ssh/authorized_keys` en hello VM de Linux</span><span class="sxs-lookup"><span data-stu-id="96718-136">SSH public key in `~/.ssh/authorized_keys` on hello Linux VM</span></span>
* <span data-ttu-id="96718-137">Derechos de SUDO en hello VM</span><span class="sxs-lookup"><span data-stu-id="96718-137">Sudo rights on hello VM</span></span>
* <span data-ttu-id="96718-138">Puerto 22 abierto</span><span class="sxs-lookup"><span data-stu-id="96718-138">Port 22 open</span></span>

## <a name="quick-commands"></a><span data-ttu-id="96718-139">Comandos rápidos</span><span class="sxs-lookup"><span data-stu-id="96718-139">Quick Commands</span></span>
<span data-ttu-id="96718-140">*Los administradores de Linux hasta que solo desea versión de hello TLDR empiece aquí.  Para todos aquellos que desea Hola explicación detallada y recorrer omitir esta sección.*</span><span class="sxs-lookup"><span data-stu-id="96718-140">*Seasoned Linux Admins who just want hello TLDR version start here.  For everyone else that wants hello detailed explanation and walk through skip this section.*</span></span>

```bash
sudo vim /etc/ssh/sshd_config
```

<span data-ttu-id="96718-141">Edite el archivo de configuración de hello como sigue:</span><span class="sxs-lookup"><span data-stu-id="96718-141">Edit hello config file as follows:</span></span>

```sh
# Change PasswordAuthentication toothis:
PasswordAuthentication no

# Change PubkeyAuthentication toothis:
PubkeyAuthentication yes

# Change PermitRootLogin toothis:
PermitRootLogin no

# Change ChallengeResponseAuthentication toothis:
ChallengeResponseAuthentication no
```

<span data-ttu-id="96718-142">Reiniciar servicio de hello SSHD.</span><span class="sxs-lookup"><span data-stu-id="96718-142">Restart hello SSHD service.</span></span> <span data-ttu-id="96718-143">En distribuciones basadas en Debian:</span><span class="sxs-lookup"><span data-stu-id="96718-143">On Debian-based distros:</span></span>

```bash
sudo service ssh restart
```

<span data-ttu-id="96718-144">En distribuciones basada en Red Hat:</span><span class="sxs-lookup"><span data-stu-id="96718-144">On Red Hat-based distros:</span></span>

```bash
sudo service sshd restart
```

## <a name="detailed-walk-through"></a><span data-ttu-id="96718-145">Tutorial detallado</span><span class="sxs-lookup"><span data-stu-id="96718-145">Detailed Walk Through</span></span>
<span data-ttu-id="96718-146">Inicio de sesión toohello VM de Linux en terminal 1 (T1).</span><span class="sxs-lookup"><span data-stu-id="96718-146">Login toohello Linux VM on terminal 1 (T1).</span></span>  <span data-ttu-id="96718-147">Inicio de sesión toohello VM de Linux en 2 terminal (T2).</span><span class="sxs-lookup"><span data-stu-id="96718-147">Login toohello Linux VM on terminal 2 (T2).</span></span>

<span data-ttu-id="96718-148">En T2 vamos archivo de configuración de tooedit Hola SSHD.</span><span class="sxs-lookup"><span data-stu-id="96718-148">On T2 we are going tooedit hello SSHD configuration file.</span></span>  

```bash
sudo vim /etc/ssh/sshd_config
```

<span data-ttu-id="96718-149">Desde aquí agregaremos editar simplemente las contraseñas de hello configuración toodisable y habilitar los inicios de sesión de claves de SSH.</span><span class="sxs-lookup"><span data-stu-id="96718-149">From here we will edit just hello settings toodisable passwords and enable SSH key logins.</span></span>  <span data-ttu-id="96718-150">Hay muchas configuraciones de este archivo que debería investigar y cambiar toomake Linux & SSH tan seguro como sea necesario.</span><span class="sxs-lookup"><span data-stu-id="96718-150">There are many settings in this file that you should research and change toomake Linux & SSH as secure as you need.</span></span>

#### <a name="disable-password-logins"></a><span data-ttu-id="96718-151">Desactivación de inicios de sesión de contraseña</span><span class="sxs-lookup"><span data-stu-id="96718-151">Disable Password logins</span></span>

```sh
# Change PasswordAuthentication toothis:
PasswordAuthentication no
```

#### <a name="enable-public-key-authentication"></a><span data-ttu-id="96718-152">Habilitación de la autenticación de clave pública</span><span class="sxs-lookup"><span data-stu-id="96718-152">Enable Public Key Authentication</span></span>

```sh
# Change PubkeyAuthentication toothis:
PubkeyAuthentication yes
```

#### <a name="disable-root-login"></a><span data-ttu-id="96718-153">Deshabilitación del inicio de sesión raíz</span><span class="sxs-lookup"><span data-stu-id="96718-153">Disable Root Login</span></span>

```sh
# Change PermitRootLogin toothis:
PermitRootLogin no
```

#### <a name="disable-challenge-response-authentication"></a><span data-ttu-id="96718-154">Deshabilitación de la autenticación de desafío/respuesta</span><span class="sxs-lookup"><span data-stu-id="96718-154">Disable Challenge-response Authentication</span></span>
```sh
# Change ChallengeResponseAuthentication toothis:
ChallengeResponseAuthentication no
```

### <a name="restart-sshd"></a><span data-ttu-id="96718-155">Reinicio de SSHD</span><span class="sxs-lookup"><span data-stu-id="96718-155">Restart SSHD</span></span>
<span data-ttu-id="96718-156">Desde el shell de hello T1 comprobar que se siguen registrando.</span><span class="sxs-lookup"><span data-stu-id="96718-156">From hello T1 shell verify that you are still logged in.</span></span>  <span data-ttu-id="96718-157">Esto es importante, por lo que no bloquee la máquina virtual si las claves SSH no son correctas, ya que las contraseñas están ahora deshabilitadas.</span><span class="sxs-lookup"><span data-stu-id="96718-157">This is critical so you do not get locked out of your VM if your SSH keys are not correct since passwords are now disabled.</span></span>  <span data-ttu-id="96718-158">Si cualquier configuración no es correcto en la VM de Linux que se puede utilizar T1 toofix sshd_config como que todavía se registrará en y SSH mantendrá conexión Hola activo durante Hola service SSHD reiniciar.</span><span class="sxs-lookup"><span data-stu-id="96718-158">If any setting are incorrect on your Linux VM you can use T1 toofix sshd_config as you will still be logged in and SSH will keep hello connection alive during hello SSHD service restart.</span></span>

<span data-ttu-id="96718-159">Desde la ejecución de T2:</span><span class="sxs-lookup"><span data-stu-id="96718-159">From T2 run:</span></span>

##### <a name="on-hello-debian-family"></a><span data-ttu-id="96718-160">En la familia de Debian Hola</span><span class="sxs-lookup"><span data-stu-id="96718-160">On hello Debian Family</span></span>
```bash
sudo service ssh restart
```

##### <a name="on-hello-redhat-family"></a><span data-ttu-id="96718-161">En la familia de RedHat Hola</span><span class="sxs-lookup"><span data-stu-id="96718-161">On hello RedHat Family</span></span>
```bash
sudo service sshd restart
```

<span data-ttu-id="96718-162">Las contraseñas ahora están deshabilitadas en la máquina virtual, por lo que se protegen de los intentos de inicio de sesión de contraseña por fuerza bruta.</span><span class="sxs-lookup"><span data-stu-id="96718-162">Passwords are now disabled on your VM protecting it from brute force password login attempts.</span></span>  <span data-ttu-id="96718-163">Con solo SSH claves permitidas será capaz de toologin más rápido y mucho más seguro.</span><span class="sxs-lookup"><span data-stu-id="96718-163">With only SSH Keys allowed you will be able toologin faster and much more secure.</span></span>

