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
# <a name="disable-ssh-passwords-on-your-linux-vm-by-configuring-sshd"></a>Deshabilitación de las contraseñas SSH en la máquina virtual de Linux mediante la configuración de SSHD
En este artículo se centra en cómo toolock la seguridad de inicio de sesión de saludo de la VM de Linux.  En cuanto se abre el puerto SSH 22 hello toohello world bots empieza toologin al tratar de adivinar las contraseñas.  Lo que haremos en este artículo es deshabilitar los inicios de sesión de contraseña a través de SSH.  Quitando completamente la capacidad de hello contraseñas toouse protegemos Hola Linux VM de este tipo de ataques de ataque de fuerza.  Hola agregado bonificación es configuramos SSHD Linux tooonly permitir inicios de sesión a través de SSH claves públicas y privadas, con diferencia Hola tooLinux de toologin de manera más segura.  las posibles combinaciones de Hello del mismo requeriría clave privada de tooguess hello es inmensa y, por tanto, no recomienda: bots de molestarle incluso claves SSH de tootry toobrute force.

## <a name="goals"></a>Objetivos
* Configurar SSHD toodisallow:
  * Inicios de sesión de contraseña
  * Inicio de sesión de usuario raíz
  * Autenticación de desafío/respuesta
* Configurar SSHD tooallow:
  * solo inicios de sesión de claves de SSH
* Reiniciar SSHD mientras sigue conectado
* Configuración de prueba Hola nueva SSHD

## <a name="introduction"></a>Introducción
[SSH definido](https://en.wikipedia.org/wiki/Secure_Shell)

SSHD es hello servidor SSH que se ejecuta en hello VM de Linux.  SSH es un cliente que se ejecuta desde un shell en la estación de trabajo MacBook o Linux.  SSH es también protocolo hello usa toosecure y cifrar la comunicación de hello entre la estación de trabajo y Hola VM de Linux.

Para este artículo es muy importante tookeep un inicio de sesión tooyour recorrer Linux VM abierto para hello todo.  Por esta razón se abrirá dos terminales y SSH toohello VM Linux de ambos.  Se usará el archivo de configuración de hello primera terminal toomake Hola cambios tooSSHDs y reiniciar servicio de hello SSHD.  Usaremos Hola segundo terminal tootest los cambios una vez que se reinicie el servicio de Hola.  Ya se están deshabilitando las contraseñas SSH y basarse estrictamente en claves SSH, si las claves SSH no son correctas y cierra Hola conexión toohello VM, hello VM será permanentemente bloqueado y nadie será tooit toologin puede requerir toobe eliminado y vuelto a crear.

## <a name="prerequisites"></a>Requisitos previos
* [Creación de claves SSH en Linux y Mac para máquinas virtuales Linux en Azure](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* Cuenta de Azure
  * [registro de versión de prueba gratuita](https://azure.microsoft.com/pricing/free-trial/)
  * [Portal de Azure](http://portal.azure.com)
* Máquina virtual de Linux que se ejecuta en Azure
* Par de claves públicas y privadas SSH en `~/.ssh/`
* Clave pública SSH en `~/.ssh/authorized_keys` en hello VM de Linux
* Derechos de SUDO en hello VM
* Puerto 22 abierto

## <a name="quick-commands"></a>Comandos rápidos
*Los administradores de Linux hasta que solo desea versión de hello TLDR empiece aquí.  Para todos aquellos que desea Hola explicación detallada y recorrer omitir esta sección.*

```bash
sudo vim /etc/ssh/sshd_config
```

Edite el archivo de configuración de hello como sigue:

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

Reiniciar servicio de hello SSHD. En distribuciones basadas en Debian:

```bash
sudo service ssh restart
```

En distribuciones basada en Red Hat:

```bash
sudo service sshd restart
```

## <a name="detailed-walk-through"></a>Tutorial detallado
Inicio de sesión toohello VM de Linux en terminal 1 (T1).  Inicio de sesión toohello VM de Linux en 2 terminal (T2).

En T2 vamos archivo de configuración de tooedit Hola SSHD.  

```bash
sudo vim /etc/ssh/sshd_config
```

Desde aquí agregaremos editar simplemente las contraseñas de hello configuración toodisable y habilitar los inicios de sesión de claves de SSH.  Hay muchas configuraciones de este archivo que debería investigar y cambiar toomake Linux & SSH tan seguro como sea necesario.

#### <a name="disable-password-logins"></a>Desactivación de inicios de sesión de contraseña

```sh
# Change PasswordAuthentication toothis:
PasswordAuthentication no
```

#### <a name="enable-public-key-authentication"></a>Habilitación de la autenticación de clave pública

```sh
# Change PubkeyAuthentication toothis:
PubkeyAuthentication yes
```

#### <a name="disable-root-login"></a>Deshabilitación del inicio de sesión raíz

```sh
# Change PermitRootLogin toothis:
PermitRootLogin no
```

#### <a name="disable-challenge-response-authentication"></a>Deshabilitación de la autenticación de desafío/respuesta
```sh
# Change ChallengeResponseAuthentication toothis:
ChallengeResponseAuthentication no
```

### <a name="restart-sshd"></a>Reinicio de SSHD
Desde el shell de hello T1 comprobar que se siguen registrando.  Esto es importante, por lo que no bloquee la máquina virtual si las claves SSH no son correctas, ya que las contraseñas están ahora deshabilitadas.  Si cualquier configuración no es correcto en la VM de Linux que se puede utilizar T1 toofix sshd_config como que todavía se registrará en y SSH mantendrá conexión Hola activo durante Hola service SSHD reiniciar.

Desde la ejecución de T2:

##### <a name="on-hello-debian-family"></a>En la familia de Debian Hola
```bash
sudo service ssh restart
```

##### <a name="on-hello-redhat-family"></a>En la familia de RedHat Hola
```bash
sudo service sshd restart
```

Las contraseñas ahora están deshabilitadas en la máquina virtual, por lo que se protegen de los intentos de inicio de sesión de contraseña por fuerza bruta.  Con solo SSH claves permitidas será capaz de toologin más rápido y mucho más seguro.

