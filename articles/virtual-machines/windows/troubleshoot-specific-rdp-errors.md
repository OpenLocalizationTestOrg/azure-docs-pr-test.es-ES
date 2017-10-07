---
title: "mensajes de error RDP aaaSpecific para máquinas virtuales de Azure | Documentos de Microsoft"
description: "Comprender los mensajes de error específicos que pueden aparecer al intentar usar la máquina virtual de escritorio remoto conexión tooa Windows en Azure"
keywords: "Error de escritorio remoto, error de conexión a Escritorio remoto, no se puede conectar tooVM, solución de problemas de escritorio remoto"
services: virtual-machines-windows
documentationcenter: 
author: genlin
manager: timlt
editor: 
tags: top-support-issue,azure-service-management,azure-resource-manager
ms.assetid: 5feb1d64-ee6f-4907-949a-a7cffcbc6153
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: support-article
ms.date: 05/26/2017
ms.author: genli
ms.openlocfilehash: 8e1551be23e696bd60adbd76c3e1ea86d9dd11aa
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting-specific-rdp-error-messages-tooa-windows-vm-in-azure"></a>Solución de problemas específico tooa de mensajes de error RDP VM de Windows en Azure
Puede recibir un mensaje de error específico cuando se usa la máquina virtual de Windows de escritorio remoto conexión tooa (VM) en Azure. Este artículo se detallan Hola encontrados, junto con tooresolve de pasos de solución de problemas de mensajes de error más comunes a algunos de ellos. Si tiene problemas para conectarse tooyour VM mediante RDP pero no no aparezca un mensaje de error específico, vea hello [guía para escritorio remoto para solucionar problemas](troubleshoot-rdp-connection.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).

Para obtener información sobre mensajes de error específicos, vea Hola siguiente:

* [se desconectó la sesión remota de Hello porque no hay ningún tooprovide disponible servidores de licencias de escritorio remoto una licencia](#rdplicense).
* [Escritorio remoto no puede encontrar Hola "nombre" del equipo](#rdpname).
* [Se ha producido un error de autenticación. Hello autoridad de seguridad Local no se puede establecer contacto con](#rdpauth).
* [Error de Seguridad de Windows: Las credenciales no funcionaron](#wincred).
* [Este equipo no puede conectar el equipo remoto toohello](#rdpconnect).

<a id="rdplicense"></a>

## <a name="hello-remote-session-was-disconnected-because-there-are-no-remote-desktop-license-servers-available-tooprovide-a-license"></a>se desconectó la sesión remota de Hello porque no hay ningún tooprovide disponible una licencia de servidores de licencias de escritorio remoto.
Causa: Hola período de gracia de licencias del 120 días para el rol de servidor de escritorio remoto de hello ha caducado y necesita licencias tooinstall.

Como alternativa, guarde una copia local del archivo RDP de Hola desde el portal de Hola y ejecute este comando en un tooconnect de línea de comandos de PowerShell. Con este paso se deshabilita la obtención de licencias solo de esa conexión:

        mstsc <File name>.RDP /admin

Si realmente no tiene más de dos toohello de conexiones de escritorio remoto simultáneas VM, puede usar el rol de servidor de escritorio remoto de hello tooremove de administrador del servidor.

Para obtener más información, consulte el blog de hello [se produce un error en la máquina virtual de Azure con "Sin remoto escritorio servidores de licencias disponibles"](https://blogs.msdn.microsoft.com/mast/2014/01/21/rdp-to-azure-vm-fails-with-no-remote-desktop-license-servers-available/).

<a id="rdpname"></a>

## <a name="remote-desktop-cant-find-hello-computer-name"></a>Escritorio remoto no puede encontrar el equipo de Hola "name".
Causa: cliente de escritorio remoto de hello en el equipo no puede resolver el nombre de hello del equipo de hello en valores de hello del archivo RDP de Hola.

Posibles soluciones:

* Si se encuentra en la intranet de una organización, asegúrese de que el equipo tiene el servidor proxy de acceso toohello y puede enviar tooit de tráfico HTTPS.
* Si está usando un archivo RDP almacenado localmente, pruebe a usar Hola uno generado por el portal de Hola. Este paso garantiza que tiene el nombre DNS correcto de Hola para máquina virtual de hello, o servicio de nube de Hola y el puerto de extremo de Hola de hello VM. Este es un archivo RDP de ejemplo generado por el portal de hello:
  
        full address:s:tailspin-azdatatier.cloudapp.net:55919
        prompt for credentials:i:1

parte de la dirección de Hola de este archivo RDP tiene:

* Hola completo nombre de dominio del servicio de nube de Hola que contiene Hola VM ("tailspin-azdatatier.cloudapp.net" en este ejemplo).
* Hola externo el puerto TCP del extremo de hello para el tráfico de escritorio remoto (55919).

<a id="rdpauth"></a>

## <a name="an-authentication-error-has-occurred-hello-local-security-authority-cannot-be-contacted"></a>Error de autenticación. no se puede contactar Hola autoridad de seguridad Local.
Causa: destino Hola VM no encuentra la autoridad de seguridad hello en parte del nombre de usuario de Hola de sus credenciales.

Cuando es el nombre de usuario en forma de hello *SecurityAuthority*\\*nombre de usuario* (ejemplo: CORP\User1), hello *SecurityAuthority* parte es cualquier hello VM nombre del equipo (de autoridad de seguridad local de hello) o un nombre de dominio de Active Directory.

Posibles soluciones:

* Si se utiliza una cuenta de hello toohello local VM, asegúrese de que ese nombre VM de hello está escrito correctamente.
* Si la cuenta de hello se encuentra en un dominio de Active Directory, compruebe la ortografía de Hola Hola del nombre de dominio.
* Si es una cuenta de dominio de Active Directory y nombre de dominio de hello está escrito correctamente, compruebe que está disponible un controlador de dominio en ese dominio. Un problema común de las redes virtuales de Azure que contienen controladores de dominio es que un controlador de dominio no está disponible porque no se ha iniciado. Como solución alternativa, puede usar una cuenta de administrador local, en lugar de una cuenta de dominio.

<a id="wincred"></a>

## <a name="windows-security-error-your-credentials-did-not-work"></a>Error de Seguridad de Windows: Las credenciales no funcionaron.
Causa: el destino Hola VM no puede validar el nombre de cuenta y la contraseña.

Un equipo basado en Windows puede validar las credenciales de Hola de una cuenta local o una cuenta de dominio.

* Para las cuentas locales, usar hello *ComputerName*\\*nombre de usuario* sintaxis (ejemplo: SQL1\Admin4798).
* Para las cuentas de dominio, use hello *DomainName*\\*nombre de usuario* sintaxis (ejemplo: CONTOSO\peterodman).

Si ha promovido el controlador de dominio de tooa de máquina virtual en un nuevo bosque de Active Directory, se convierte la cuenta de administrador local de Hola que ha iniciado sesión con tooan equivalente cuenta con hello misma contraseña en hello nuevo bosque y dominio. a continuación, se elimina la cuenta local de Hola.

Por ejemplo, si inició sesión con la cuenta local de hello DC1\DCAdmin y, a continuación, promocionar máquina virtual de Hola como un controlador de dominio en un nuevo bosque de dominio de corp.contoso.com hello, Hola DC1\DCAdmin se elimina la cuenta local y una nueva cuenta de dominio (CORP\DCAdmin ) se crea con hello misma contraseña.

Asegúrese de que ese nombre de cuenta de hello es un nombre que puede comprobar la máquina virtual de hello como una cuenta válida, y esa contraseña hello es correcta.

Si necesita toochange Hola contraseña de cuenta de administrador local de hello, consulte [cómo service tooreset una contraseña o hello escritorio remoto para máquinas virtuales de Windows](reset-rdp.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).

<a id="rdpconnect"></a>

## <a name="this-computer-cant-connect-toohello-remote-computer"></a>Este equipo no puede conectar el equipo remoto toohello.
Causa: cuenta de hello que ha usado tooconnect no tiene derechos de inicio de sesión de escritorio remoto.

Cada equipo de Windows tiene un grupo local de usuarios de escritorio remoto, que contiene cuentas de Hola y grupos que pueden iniciar sesión en él de forma remota. Los miembros del grupo de administradores locales de hello también tienen acceso, incluso si esas cuentas no aparecen en el grupo local de usuarios de escritorio remoto de Hola. Para los equipos unidos a un dominio, grupo de administradores locales de hello contiene los administradores de dominio de hello para el dominio de Hola.

Asegúrese de que cuenta de hello con que usa tooconnect tiene derechos de inicio de sesión de escritorio remoto. Como alternativa, utilice un dominio o tooconnect de la cuenta de administrador local a través de escritorio remoto. tooadd Hola grupo local de usuarios de escritorio remoto de cuenta deseada toohello, usar el complemento Microsoft Management Console hello (**herramientas del sistema > usuarios y grupos locales > grupos > usuarios de escritorio remoto**).

## <a name="next-steps"></a>Pasos siguientes
Si ninguno de estos errores se produjeron y tiene un problema desconocido con la conexión mediante RDP, consulte hello [guía para escritorio remoto para solucionar problemas](troubleshoot-rdp-connection.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).

* Para solucionar problemas de pasos al obtener acceso a aplicaciones que se ejecutan en una máquina virtual, consulte [aplicación tooan solucionar access que ejecuta en una VM de Azure](../linux/troubleshoot-app-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).
* Si tiene problemas con el Shell seguro (SSH) tooconnect tooa VM de Linux en Azure, consulte [solucionar problemas de SSH conexiones tooa VM de Linux en Azure](../linux/troubleshoot-ssh-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

