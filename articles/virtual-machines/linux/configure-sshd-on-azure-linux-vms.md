---
title: "aaaConfigure SSHD en máquinas virtuales de Azure Linux | Documentos de Microsoft"
description: "Configurar SSHD de prácticas recomendadas de seguridad y toolockdown SSH tooAzure máquinas virtuales de Linux."
services: virtual-machines-linux
documentationcenter: 
author: vlivech
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 11/21/2016
ms.author: v-livech
ms.openlocfilehash: c2361be7199a24b129c06acfc899dd32f6e1d6fb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="configure-sshd-on-azure-linux-vms"></a><span data-ttu-id="ae7e2-103">Configuración de SSHD en Azure Linux Virtual Machines</span><span class="sxs-lookup"><span data-stu-id="ae7e2-103">Configure SSHD on Azure Linux VMs</span></span>

<span data-ttu-id="ae7e2-104">Este artículo muestra cómo toolockdown Hola servidor SSH en Linux, la seguridad de las prácticas recomendada tooprovide y la toospeed proceso de inicio de sesión SSH de hello mediante el uso de claves de SSH en lugar de contraseñas.</span><span class="sxs-lookup"><span data-stu-id="ae7e2-104">This article shows how toolockdown hello SSH Server on Linux, tooprovide best practices security and also toospeed up hello SSH login process by using SSH keys instead of passwords.</span></span>  <span data-ttu-id="ae7e2-105">bloqueo toofurther SSHD vamos a usuario de toodisable Hola raíz que se pueda toologin, limitar los usuarios de Hola que pueden toologin a través de una lista de grupos aprobados, deshabilitar la versión 1 del protocolo SSH, establecer un bit de clave mínima y configurar el cierre de sesión automático de usuarios en espera.</span><span class="sxs-lookup"><span data-stu-id="ae7e2-105">toofurther lockdown SSHD we are going toodisable hello root user from being able toologin, limit hello users that are allowed toologin via an approved group list, disabling SSH protocol version 1, set a minimum key bit, and configure auto-logout of idle users.</span></span>  <span data-ttu-id="ae7e2-106">requisitos de Hola para este artículo son: una cuenta de Azure ([obtener una evaluación gratuita](https://azure.microsoft.com/pricing/free-trial/)) y [archivos claves SSH pública y privada](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="ae7e2-106">hello requirements for this article are: an Azure account ([get a free trial](https://azure.microsoft.com/pricing/free-trial/)) and [SSH public and private key files](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

## <a name="quick-commands"></a><span data-ttu-id="ae7e2-107">Comandos rápidos</span><span class="sxs-lookup"><span data-stu-id="ae7e2-107">Quick Commands</span></span>

<span data-ttu-id="ae7e2-108">Configurar `/etc/ssh/sshd_config` con hello después de configuración:</span><span class="sxs-lookup"><span data-stu-id="ae7e2-108">Configure `/etc/ssh/sshd_config` with hello following settings:</span></span>

### <a name="disable-password-logins"></a><span data-ttu-id="ae7e2-109">Deshabilitación de inicios de sesión con contraseña</span><span class="sxs-lookup"><span data-stu-id="ae7e2-109">Disable password logins</span></span>

```bash
PasswordAuthentication no
```

### <a name="disable-login-by-hello-root-user"></a><span data-ttu-id="ae7e2-110">Deshabilitar inicio de sesión de usuario de la raíz de Hola</span><span class="sxs-lookup"><span data-stu-id="ae7e2-110">Disable login by hello root user</span></span>

```bash
PermitRootLogin no
```

### <a name="allowed-groups-list"></a><span data-ttu-id="ae7e2-111">Lista de grupos permitidos</span><span class="sxs-lookup"><span data-stu-id="ae7e2-111">Allowed groups list</span></span>

```bash
AllowGroups wheel
```

### <a name="allowed-users-list"></a><span data-ttu-id="ae7e2-112">Lista de usuarios permitidos</span><span class="sxs-lookup"><span data-stu-id="ae7e2-112">Allowed users list</span></span>

```bash
AllowUsers ahmet ralph
```

### <a name="disable-ssh-protocol-version-1"></a><span data-ttu-id="ae7e2-113">Deshabilitación del protocolo SSH versión 1</span><span class="sxs-lookup"><span data-stu-id="ae7e2-113">Disable SSH protocol version 1</span></span>

```bash
Protocol 2
```

### <a name="minimum-key-bits"></a><span data-ttu-id="ae7e2-114">Bits de clave mínima</span><span class="sxs-lookup"><span data-stu-id="ae7e2-114">Minimum key bits</span></span>

```bash
ServerKeyBits 2048
```

### <a name="disconnect-idle-users"></a><span data-ttu-id="ae7e2-115">Desconexión de usuarios inactivos</span><span class="sxs-lookup"><span data-stu-id="ae7e2-115">Disconnect idle users</span></span>

```bash
ClientAliveInterval 300
ClientAliveCountMax 0
```

## <a name="detailed-walkthrough"></a><span data-ttu-id="ae7e2-116">Tutorial detallado</span><span class="sxs-lookup"><span data-stu-id="ae7e2-116">Detailed Walkthrough</span></span>

<span data-ttu-id="ae7e2-117">SSHD es hello servidor SSH que se ejecuta en hello VM de Linux.</span><span class="sxs-lookup"><span data-stu-id="ae7e2-117">SSHD is hello SSH Server that runs on hello Linux VM.</span></span>  <span data-ttu-id="ae7e2-118">SSH es un cliente que se ejecuta desde un shell en la estación de trabajo MacBook o Linux o desde un Bash en Windows.</span><span class="sxs-lookup"><span data-stu-id="ae7e2-118">SSH is a client that runs from a shell on your MacBook, Linux workstation, or from a Bash on Windows.</span></span>  <span data-ttu-id="ae7e2-119">SSH también es el protocolo de hello usa toosecure y cifrar la comunicación de hello entre la estación de trabajo y Hola VM de Linux que realiza SSH también una VPN (red privada Virtual).</span><span class="sxs-lookup"><span data-stu-id="ae7e2-119">SSH is also hello protocol used toosecure and encrypt hello communication between your workstation and hello Linux VM making SSH also a VPN (Virtual Private Network).</span></span>

<span data-ttu-id="ae7e2-120">En este artículo, es muy importante tookeep un inicio de sesión tooyour abrir VM de Linux para ver tutorial completo de Hola.</span><span class="sxs-lookup"><span data-stu-id="ae7e2-120">For this article, it is very important tookeep one login tooyour Linux VM open for hello entire walk-through.</span></span>  <span data-ttu-id="ae7e2-121">Una vez establecida una conexión SSH, permanece como una sesión abierta siempre y cuando no se cierra la ventana hello.</span><span class="sxs-lookup"><span data-stu-id="ae7e2-121">Once an SSH connection is established, it remains as an open session as long as hello window is not closed.</span></span>  <span data-ttu-id="ae7e2-122">Tener un terminal conectado permite cambios toobe realizado toohello service SSHD sin que se bloquee si se realiza un cambio importante.</span><span class="sxs-lookup"><span data-stu-id="ae7e2-122">Having one terminal logged in, allows for changes toobe made toohello SSHD service without being locked out if a breaking change is made.</span></span>  <span data-ttu-id="ae7e2-123">Si ve bloqueada su VM de Linux con una configuración SSHD dañada, Azure ofrece Hola capacidad tooreset una configuración SSHD dañada con hello [extensión de acceso de VM de Azure](using-vmaccess-extension.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="ae7e2-123">If you do get locked out of your Linux VM with a broken SSHD configuration, Azure offers hello ability tooreset a broken SSHD configuration with hello [Azure VM Access Extension](using-vmaccess-extension.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

<span data-ttu-id="ae7e2-124">Por esta razón se abra dos terminales y SSH toohello VM Linux de ambos.</span><span class="sxs-lookup"><span data-stu-id="ae7e2-124">For this reason we open two terminals and SSH toohello Linux VM from both of them.</span></span>  <span data-ttu-id="ae7e2-125">Se utilizar archivo de configuración de hello primera terminal toomake Hola cambios tooSSHDs y reinicia el servicio de hello SSHD.</span><span class="sxs-lookup"><span data-stu-id="ae7e2-125">We use hello first terminal toomake hello changes tooSSHDs configuration file and restart hello SSHD service.</span></span>  <span data-ttu-id="ae7e2-126">Utilizamos Hola segundo terminal tootest los cambios una vez que se reinicie el servicio de Hola.</span><span class="sxs-lookup"><span data-stu-id="ae7e2-126">We use hello second terminal tootest those changes once hello service is restarted.</span></span>  <span data-ttu-id="ae7e2-127">Ya se están deshabilitando las contraseñas SSH y basarse estrictamente en claves SSH, si las claves SSH no son correctas y cierra Hola conexión toohello VM, hello VM será permanentemente bloqueado y nadie será tooit toologin puede requerir toobe eliminado y vuelto a crear.</span><span class="sxs-lookup"><span data-stu-id="ae7e2-127">Because we are disabling SSH passwords and relying strictly on SSH keys, if your SSH keys are not correct and you close hello connection toohello VM, hello VM will be permanently locked and no one will be able toologin tooit requiring it toobe deleted and recreated.</span></span>

## <a name="disable-password-logins"></a><span data-ttu-id="ae7e2-128">Deshabilitación de inicios de sesión con contraseña</span><span class="sxs-lookup"><span data-stu-id="ae7e2-128">Disable password logins</span></span>

<span data-ttu-id="ae7e2-129">Hola toosecure de manera más rápida que VM de Linux es inicios de sesión de contraseña toodisable.</span><span class="sxs-lookup"><span data-stu-id="ae7e2-129">hello quickest way toosecure you Linux VM is toodisable password logins.</span></span>  <span data-ttu-id="ae7e2-130">Cuando se habilitan los inicios de sesión de contraseña, bots rastreo web Hola iniciará inmediatamente a intentar toobrute forzar contraseña de Hola de estimación de la VM de Linux mediante SSH.</span><span class="sxs-lookup"><span data-stu-id="ae7e2-130">When password logins are enabled, bots crawling hello web will immediately start attempting toobrute force guess hello password for your Linux VM using SSH.</span></span>  <span data-ttu-id="ae7e2-131">Deshabilitar completamente los inicios de sesión de contraseña, permite Hola SSH server tooignore todos los intentos de inicio de sesión de contraseña.</span><span class="sxs-lookup"><span data-stu-id="ae7e2-131">Disabling password logins completely, enables hello SSH server tooignore all password login attempts.</span></span>

```bash
PasswordAuthentication no
```

## <a name="disable-login-by-hello-root-user"></a><span data-ttu-id="ae7e2-132">Deshabilitar inicio de sesión de usuario de la raíz de Hola</span><span class="sxs-lookup"><span data-stu-id="ae7e2-132">Disable login by hello root user</span></span>

<span data-ttu-id="ae7e2-133">Procedimientos recomendados de Linux, hello `root` usuario nunca se debe registrar a través de SSH o mediante `sudo su`.</span><span class="sxs-lookup"><span data-stu-id="ae7e2-133">Following Linux best practices, hello `root` user should never be logged into over SSH or using `sudo su`.</span></span>  <span data-ttu-id="ae7e2-134">Siempre se deben ejecutar todos los comandos que necesitan permisos de nivel de raíz a través de hello `sudo` comando, que registra todas las acciones de auditoría futura.</span><span class="sxs-lookup"><span data-stu-id="ae7e2-134">All commands needing root level permissions should always be run through hello `sudo` command, which logs all actions for future auditing.</span></span>  <span data-ttu-id="ae7e2-135">Deshabilitar hello `root` usuario de inicio de sesión mediante SSH es un paso de prácticas recomendado de seguridad que garantiza que sólo los usuarios autorizados pueden tooSSH.</span><span class="sxs-lookup"><span data-stu-id="ae7e2-135">Disabling hello `root` user from logging in via SSH is a security best practices step that ensures only authorized users are allowed tooSSH.</span></span>

```bash
PermitRootLogin no
```

## <a name="allowed-groups-list"></a><span data-ttu-id="ae7e2-136">Lista de grupos permitidos</span><span class="sxs-lookup"><span data-stu-id="ae7e2-136">Allowed groups list</span></span>

<span data-ttu-id="ae7e2-137">SSH ofrece un método para restringir los usuarios y grupos a los que se permite o deniega el inicio de sesión mediante SSH.</span><span class="sxs-lookup"><span data-stu-id="ae7e2-137">SSH offers a method of restricting users and group that are allowed or disallowed from logging in over SSH.</span></span>  <span data-ttu-id="ae7e2-138">Esta característica utiliza listas tooapprove o denegar usuarios y grupos concretos desde el inicio de sesión.</span><span class="sxs-lookup"><span data-stu-id="ae7e2-138">This feature uses lists tooapprove or deny specific users and groups from logging in.</span></span>  <span data-ttu-id="ae7e2-139">Establecer Hola rueda grupo toohello `AllowGroups` lista restringe los inicios de sesión aprobados a través de SSH toojust las cuentas de usuario que se encuentran en el grupo de rueda Hola.</span><span class="sxs-lookup"><span data-stu-id="ae7e2-139">Setting hello wheel group toohello `AllowGroups` list restricts approved logins over SSH toojust user accounts that are in hello wheel group.</span></span>

```bash
AllowGroups wheel
```

## <a name="allowed-users-list"></a><span data-ttu-id="ae7e2-140">Lista de usuarios permitidos</span><span class="sxs-lookup"><span data-stu-id="ae7e2-140">Allowed users list</span></span>

<span data-ttu-id="ae7e2-141">Restringir que los usuarios de toojust de inicios de sesión SSH es una manera más específica tooaccomplish Hola igual de tareas que `AllowGroups` es.</span><span class="sxs-lookup"><span data-stu-id="ae7e2-141">Restricting SSH logins toojust users is a more specific way tooaccomplish hello same task that `AllowGroups` is.</span></span>  

```bash
AllowUsers ahmet ralph
```

## <a name="disable-ssh-protocol-version-1"></a><span data-ttu-id="ae7e2-142">Deshabilitación del protocolo SSH versión 1</span><span class="sxs-lookup"><span data-stu-id="ae7e2-142">Disable SSH protocol version 1</span></span>

<span data-ttu-id="ae7e2-143">La versión 1 del protocolo SSH no es segura y debería estar deshabilitada.</span><span class="sxs-lookup"><span data-stu-id="ae7e2-143">SSH protocol version 1 is insecure and should be disabled.</span></span>  <span data-ttu-id="ae7e2-144">Versión 2 del protocolo SSH es la versión actual de Hola que ofrece un servidor de tooyour tooSSH de forma segura.</span><span class="sxs-lookup"><span data-stu-id="ae7e2-144">SSH protocol version 2 is hello current version that offers a secure way tooSSH tooyour server.</span></span>  <span data-ttu-id="ae7e2-145">Deshabilitar SSH versión 1 deniega a los clientes SSH que están intentando tooestablish una conexión con el servidor SSH Hola con SSH versión 1.</span><span class="sxs-lookup"><span data-stu-id="ae7e2-145">Disabling SSH version 1 denies any SSH clients that are attempting tooestablish a connection with hello SSH server using SSH version 1.</span></span>  <span data-ttu-id="ae7e2-146">Solo se permiten conexiones de la versión 2 de SSH toonegotiate una conexión con el servidor de hello SSH.</span><span class="sxs-lookup"><span data-stu-id="ae7e2-146">Only SSH version 2 connections are allowed toonegotiate a connection with hello SSH server.</span></span>

```bash
Protocol 2
```

## <a name="minimum-key-bits"></a><span data-ttu-id="ae7e2-147">Bits de clave mínima</span><span class="sxs-lookup"><span data-stu-id="ae7e2-147">Minimum key bits</span></span>

<span data-ttu-id="ae7e2-148">Seguir prácticas recomendadas de seguridad, se deshabilitan los inicios de sesión de contraseña SSH y claves SSH solo se permiten toobe usa tooauthenticate con el servidor SSH de Hola.</span><span class="sxs-lookup"><span data-stu-id="ae7e2-148">Following security best practices, password SSH logins are disabled and only SSH keys are allowed toobe used tooauthenticate with hello SSH server.</span></span>  <span data-ttu-id="ae7e2-149">Estas claves SSH se pueden crear mediante claves de diferente longitud, medidas en bits.</span><span class="sxs-lookup"><span data-stu-id="ae7e2-149">These SSH keys can be created using different length keys, measured in bits.</span></span>  <span data-ttu-id="ae7e2-150">Los Estados que las claves de 2048 bits de longitud están Hola mínimo aceptable fuerza de la clave de procedimientos recomendados.</span><span class="sxs-lookup"><span data-stu-id="ae7e2-150">Best practices states that keys of 2048 bits in length are hello minimum acceptable key strength.</span></span>  <span data-ttu-id="ae7e2-151">Las claves de menos de 2048 bits teóricamente podrían no ser seguras.</span><span class="sxs-lookup"><span data-stu-id="ae7e2-151">Keys of less than 2048 bits could theoretically be broken.</span></span>  <span data-ttu-id="ae7e2-152">Hola configuración `ServerKeyBits` demasiado`2048` permite las conexiones con las claves de 2048 bits o superior y denegar las conexiones de menos de 2048 bits.</span><span class="sxs-lookup"><span data-stu-id="ae7e2-152">Setting hello `ServerKeyBits` too`2048` allows any connections using keys of 2048 bits or greater and deny connections of less than 2048 bits.</span></span>

```bash
ServerKeyBits 2048
```

## <a name="disconnect-idle-users"></a><span data-ttu-id="ae7e2-153">Desconexión de usuarios inactivos</span><span class="sxs-lookup"><span data-stu-id="ae7e2-153">Disconnect idle users</span></span>

<span data-ttu-id="ae7e2-154">SSH tiene usuarios de toodisconnect de capacidad de Hola que tengan conexiones abiertas que han permanecido inactivas durante más de un determinado intervalo de segundos.</span><span class="sxs-lookup"><span data-stu-id="ae7e2-154">SSH has hello ability toodisconnect users that have open connections that have remained idle for more than a set period of seconds.</span></span>  <span data-ttu-id="ae7e2-155">Mantener las sesiones abiertas tooonly los usuarios que sean active limita la exposición de Hola de hello VM de Linux.</span><span class="sxs-lookup"><span data-stu-id="ae7e2-155">Keeping open sessions tooonly those users who are active limits hello exposure of hello Linux VM.</span></span>

```bash
ClientAliveInterval 300
ClientAliveCountMax 0
```

## <a name="restart-sshd"></a><span data-ttu-id="ae7e2-156">Reinicio de SSHD</span><span class="sxs-lookup"><span data-stu-id="ae7e2-156">Restart SSHD</span></span>

<span data-ttu-id="ae7e2-157">configuración de hello tooenable en `/etc/ssh/sshd_config` reiniciar del proceso SSHD Hola que reinicia el servidor de hello SSH.</span><span class="sxs-lookup"><span data-stu-id="ae7e2-157">tooenable hello settings in `/etc/ssh/sshd_config` restart hello SSHD process which restarts hello SSH server.</span></span>  <span data-ttu-id="ae7e2-158">ventana de terminal de Hello usa toorestart Hola SSH servidor permanecen abiertas sin perder la sesión SSH de hello abierta.</span><span class="sxs-lookup"><span data-stu-id="ae7e2-158">hello terminal window you use toorestart hello SSH server remain open without losing hello open SSH session.</span></span>  <span data-ttu-id="ae7e2-159">configuración del servidor SSH de nuevo tootest Hola use una segunda ventana de terminal o ficha.  Usar una conexión SSH de hello tootest terminal independiente, podrá toogo volver y hacer cambios adicionales toohello `/etc/ssh/sshd_config` en terminal primera hello, sin que se bloquee por una novedad importante SSHD.</span><span class="sxs-lookup"><span data-stu-id="ae7e2-159">tootest hello new SSH server settings use a second terminal window or tab.  Using a separate terminal tootest hello SSH connection allows you toogo back and make additional changes toohello `/etc/ssh/sshd_config` in hello first terminal, without being locked out by a breaking SSHD change.</span></span>  

### <a name="on-redhat-centos-and-fedora"></a><span data-ttu-id="ae7e2-160">En Redhat, Centos y Fedora</span><span class="sxs-lookup"><span data-stu-id="ae7e2-160">On Redhat, Centos and Fedora</span></span>

```bash
service sshd restart
```

### <a name="on-debian--ubuntu"></a><span data-ttu-id="ae7e2-161">En Debian y Ubuntu</span><span class="sxs-lookup"><span data-stu-id="ae7e2-161">On Debian & Ubuntu</span></span>

```bash
service ssh restart
```

## <a name="reset-sshd-using-azure-reset-access"></a><span data-ttu-id="ae7e2-162">Restablecimiento de SSHD mediante acceso restablecido de Azure</span><span class="sxs-lookup"><span data-stu-id="ae7e2-162">Reset SSHD using Azure reset-access</span></span>

<span data-ttu-id="ae7e2-163">Si se bloquea de una configuración de separación de cambio toohello SSHD puede utilizar la configuración original del toohello back-de configuración de hello extensión de acceso de la máquina virtual de Azure tooreset Hola SSHD.</span><span class="sxs-lookup"><span data-stu-id="ae7e2-163">If you are locked out from a breaking change toohello SSHD configuration you can use hello Azure VM access-extension tooreset hello SSHD configuration back toohello original configuration.</span></span>

<span data-ttu-id="ae7e2-164">Reemplace los nombres de ejemplo por los suyos propios.</span><span class="sxs-lookup"><span data-stu-id="ae7e2-164">Replace any example names with your own.</span></span>

```azurecli
azure vm reset-access \
--resource-group myResourceGroup \
--name myVM \
--reset-ssh
```

## <a name="install-fail2ban"></a><span data-ttu-id="ae7e2-165">Instalación de Fail2ban</span><span class="sxs-lookup"><span data-stu-id="ae7e2-165">Install Fail2ban</span></span>

<span data-ttu-id="ae7e2-166">Se recomienda encarecidamente tooinstall y el programa de instalación de código abierto aplicación hello Fail2ban, qué bloques repiten intentos toologin tooyour VM de Linux a través de SSH mediante la fuerza bruta.</span><span class="sxs-lookup"><span data-stu-id="ae7e2-166">It is strongly recommended tooinstall and setup hello open source app Fail2ban, which blocks repeated attempts toologin tooyour Linux VM over SSH using brute force.</span></span>  <span data-ttu-id="ae7e2-167">Registros de Fail2ban repite conmutado intentos toologin SSH y, a continuación, crea reglas de firewall de dirección IP de tooblock Hola que se originan los intentos de Hola.</span><span class="sxs-lookup"><span data-stu-id="ae7e2-167">Fail2ban logs repeated failed attempts toologin over SSH and then creates firewall rules tooblock hello IP address that hello attempts are originating from.</span></span>

* [<span data-ttu-id="ae7e2-168">Página principal de Fail2ban</span><span class="sxs-lookup"><span data-stu-id="ae7e2-168">Fail2ban homepage</span></span>](http://www.fail2ban.org/wiki/index.php/Main_Page)

## <a name="next-steps"></a><span data-ttu-id="ae7e2-169">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="ae7e2-169">Next Steps</span></span>

<span data-ttu-id="ae7e2-170">Ahora que ha configurado y Hola SSH servidor bloqueado en la VM de Linux, hay prácticas recomendadas de seguridad adicional que puede seguir.</span><span class="sxs-lookup"><span data-stu-id="ae7e2-170">Now that you have configured and locked down hello SSH server on your Linux VM there are additional security best practices you can follow.</span></span>  

* [<span data-ttu-id="ae7e2-171">Administrar usuarios, SSH y verificación o reparación de discos sobre el uso de máquinas virtuales de Linux de Azure Hola VMAccess extensión</span><span class="sxs-lookup"><span data-stu-id="ae7e2-171">Manage users, SSH, and check or repair disks on Azure Linux VMs using hello VMAccess Extension</span></span>](using-vmaccess-extension.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

* [<span data-ttu-id="ae7e2-172">Cifrar discos en una VM de Linux con hello CLI de Azure</span><span class="sxs-lookup"><span data-stu-id="ae7e2-172">Encrypt disks on a Linux VM using hello Azure CLI</span></span>](encrypt-disks.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

* [<span data-ttu-id="ae7e2-173">Acceso y seguridad en plantillas de Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="ae7e2-173">Access and security in Azure Resource Manager templates</span></span>](dotnet-core-3-access-security.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
