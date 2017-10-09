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
# <a name="configure-sshd-on-azure-linux-vms"></a>Configuración de SSHD en Azure Linux Virtual Machines

Este artículo muestra cómo toolockdown Hola servidor SSH en Linux, la seguridad de las prácticas recomendada tooprovide y la toospeed proceso de inicio de sesión SSH de hello mediante el uso de claves de SSH en lugar de contraseñas.  bloqueo toofurther SSHD vamos a usuario de toodisable Hola raíz que se pueda toologin, limitar los usuarios de Hola que pueden toologin a través de una lista de grupos aprobados, deshabilitar la versión 1 del protocolo SSH, establecer un bit de clave mínima y configurar el cierre de sesión automático de usuarios en espera.  requisitos de Hola para este artículo son: una cuenta de Azure ([obtener una evaluación gratuita](https://azure.microsoft.com/pricing/free-trial/)) y [archivos claves SSH pública y privada](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

## <a name="quick-commands"></a>Comandos rápidos

Configurar `/etc/ssh/sshd_config` con hello después de configuración:

### <a name="disable-password-logins"></a>Deshabilitación de inicios de sesión con contraseña

```bash
PasswordAuthentication no
```

### <a name="disable-login-by-hello-root-user"></a>Deshabilitar inicio de sesión de usuario de la raíz de Hola

```bash
PermitRootLogin no
```

### <a name="allowed-groups-list"></a>Lista de grupos permitidos

```bash
AllowGroups wheel
```

### <a name="allowed-users-list"></a>Lista de usuarios permitidos

```bash
AllowUsers ahmet ralph
```

### <a name="disable-ssh-protocol-version-1"></a>Deshabilitación del protocolo SSH versión 1

```bash
Protocol 2
```

### <a name="minimum-key-bits"></a>Bits de clave mínima

```bash
ServerKeyBits 2048
```

### <a name="disconnect-idle-users"></a>Desconexión de usuarios inactivos

```bash
ClientAliveInterval 300
ClientAliveCountMax 0
```

## <a name="detailed-walkthrough"></a>Tutorial detallado

SSHD es hello servidor SSH que se ejecuta en hello VM de Linux.  SSH es un cliente que se ejecuta desde un shell en la estación de trabajo MacBook o Linux o desde un Bash en Windows.  SSH también es el protocolo de hello usa toosecure y cifrar la comunicación de hello entre la estación de trabajo y Hola VM de Linux que realiza SSH también una VPN (red privada Virtual).

En este artículo, es muy importante tookeep un inicio de sesión tooyour abrir VM de Linux para ver tutorial completo de Hola.  Una vez establecida una conexión SSH, permanece como una sesión abierta siempre y cuando no se cierra la ventana hello.  Tener un terminal conectado permite cambios toobe realizado toohello service SSHD sin que se bloquee si se realiza un cambio importante.  Si ve bloqueada su VM de Linux con una configuración SSHD dañada, Azure ofrece Hola capacidad tooreset una configuración SSHD dañada con hello [extensión de acceso de VM de Azure](using-vmaccess-extension.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

Por esta razón se abra dos terminales y SSH toohello VM Linux de ambos.  Se utilizar archivo de configuración de hello primera terminal toomake Hola cambios tooSSHDs y reinicia el servicio de hello SSHD.  Utilizamos Hola segundo terminal tootest los cambios una vez que se reinicie el servicio de Hola.  Ya se están deshabilitando las contraseñas SSH y basarse estrictamente en claves SSH, si las claves SSH no son correctas y cierra Hola conexión toohello VM, hello VM será permanentemente bloqueado y nadie será tooit toologin puede requerir toobe eliminado y vuelto a crear.

## <a name="disable-password-logins"></a>Deshabilitación de inicios de sesión con contraseña

Hola toosecure de manera más rápida que VM de Linux es inicios de sesión de contraseña toodisable.  Cuando se habilitan los inicios de sesión de contraseña, bots rastreo web Hola iniciará inmediatamente a intentar toobrute forzar contraseña de Hola de estimación de la VM de Linux mediante SSH.  Deshabilitar completamente los inicios de sesión de contraseña, permite Hola SSH server tooignore todos los intentos de inicio de sesión de contraseña.

```bash
PasswordAuthentication no
```

## <a name="disable-login-by-hello-root-user"></a>Deshabilitar inicio de sesión de usuario de la raíz de Hola

Procedimientos recomendados de Linux, hello `root` usuario nunca se debe registrar a través de SSH o mediante `sudo su`.  Siempre se deben ejecutar todos los comandos que necesitan permisos de nivel de raíz a través de hello `sudo` comando, que registra todas las acciones de auditoría futura.  Deshabilitar hello `root` usuario de inicio de sesión mediante SSH es un paso de prácticas recomendado de seguridad que garantiza que sólo los usuarios autorizados pueden tooSSH.

```bash
PermitRootLogin no
```

## <a name="allowed-groups-list"></a>Lista de grupos permitidos

SSH ofrece un método para restringir los usuarios y grupos a los que se permite o deniega el inicio de sesión mediante SSH.  Esta característica utiliza listas tooapprove o denegar usuarios y grupos concretos desde el inicio de sesión.  Establecer Hola rueda grupo toohello `AllowGroups` lista restringe los inicios de sesión aprobados a través de SSH toojust las cuentas de usuario que se encuentran en el grupo de rueda Hola.

```bash
AllowGroups wheel
```

## <a name="allowed-users-list"></a>Lista de usuarios permitidos

Restringir que los usuarios de toojust de inicios de sesión SSH es una manera más específica tooaccomplish Hola igual de tareas que `AllowGroups` es.  

```bash
AllowUsers ahmet ralph
```

## <a name="disable-ssh-protocol-version-1"></a>Deshabilitación del protocolo SSH versión 1

La versión 1 del protocolo SSH no es segura y debería estar deshabilitada.  Versión 2 del protocolo SSH es la versión actual de Hola que ofrece un servidor de tooyour tooSSH de forma segura.  Deshabilitar SSH versión 1 deniega a los clientes SSH que están intentando tooestablish una conexión con el servidor SSH Hola con SSH versión 1.  Solo se permiten conexiones de la versión 2 de SSH toonegotiate una conexión con el servidor de hello SSH.

```bash
Protocol 2
```

## <a name="minimum-key-bits"></a>Bits de clave mínima

Seguir prácticas recomendadas de seguridad, se deshabilitan los inicios de sesión de contraseña SSH y claves SSH solo se permiten toobe usa tooauthenticate con el servidor SSH de Hola.  Estas claves SSH se pueden crear mediante claves de diferente longitud, medidas en bits.  Los Estados que las claves de 2048 bits de longitud están Hola mínimo aceptable fuerza de la clave de procedimientos recomendados.  Las claves de menos de 2048 bits teóricamente podrían no ser seguras.  Hola configuración `ServerKeyBits` demasiado`2048` permite las conexiones con las claves de 2048 bits o superior y denegar las conexiones de menos de 2048 bits.

```bash
ServerKeyBits 2048
```

## <a name="disconnect-idle-users"></a>Desconexión de usuarios inactivos

SSH tiene usuarios de toodisconnect de capacidad de Hola que tengan conexiones abiertas que han permanecido inactivas durante más de un determinado intervalo de segundos.  Mantener las sesiones abiertas tooonly los usuarios que sean active limita la exposición de Hola de hello VM de Linux.

```bash
ClientAliveInterval 300
ClientAliveCountMax 0
```

## <a name="restart-sshd"></a>Reinicio de SSHD

configuración de hello tooenable en `/etc/ssh/sshd_config` reiniciar del proceso SSHD Hola que reinicia el servidor de hello SSH.  ventana de terminal de Hello usa toorestart Hola SSH servidor permanecen abiertas sin perder la sesión SSH de hello abierta.  configuración del servidor SSH de nuevo tootest Hola use una segunda ventana de terminal o ficha.  Usar una conexión SSH de hello tootest terminal independiente, podrá toogo volver y hacer cambios adicionales toohello `/etc/ssh/sshd_config` en terminal primera hello, sin que se bloquee por una novedad importante SSHD.  

### <a name="on-redhat-centos-and-fedora"></a>En Redhat, Centos y Fedora

```bash
service sshd restart
```

### <a name="on-debian--ubuntu"></a>En Debian y Ubuntu

```bash
service ssh restart
```

## <a name="reset-sshd-using-azure-reset-access"></a>Restablecimiento de SSHD mediante acceso restablecido de Azure

Si se bloquea de una configuración de separación de cambio toohello SSHD puede utilizar la configuración original del toohello back-de configuración de hello extensión de acceso de la máquina virtual de Azure tooreset Hola SSHD.

Reemplace los nombres de ejemplo por los suyos propios.

```azurecli
azure vm reset-access \
--resource-group myResourceGroup \
--name myVM \
--reset-ssh
```

## <a name="install-fail2ban"></a>Instalación de Fail2ban

Se recomienda encarecidamente tooinstall y el programa de instalación de código abierto aplicación hello Fail2ban, qué bloques repiten intentos toologin tooyour VM de Linux a través de SSH mediante la fuerza bruta.  Registros de Fail2ban repite conmutado intentos toologin SSH y, a continuación, crea reglas de firewall de dirección IP de tooblock Hola que se originan los intentos de Hola.

* [Página principal de Fail2ban](http://www.fail2ban.org/wiki/index.php/Main_Page)

## <a name="next-steps"></a>Pasos siguientes

Ahora que ha configurado y Hola SSH servidor bloqueado en la VM de Linux, hay prácticas recomendadas de seguridad adicional que puede seguir.  

* [Administrar usuarios, SSH y verificación o reparación de discos sobre el uso de máquinas virtuales de Linux de Azure Hola VMAccess extensión](using-vmaccess-extension.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

* [Cifrar discos en una VM de Linux con hello CLI de Azure](encrypt-disks.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

* [Acceso y seguridad en plantillas de Azure Resource Manager](dotnet-core-3-access-security.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
