---
title: "aaaUse SSH claves con Windows para máquinas virtuales Linux | Documentos de Microsoft"
description: "Obtenga información acerca de cómo toogenerate y uso SSH claves en una máquina virtual de Linux de Windows equipo tooconnect tooa en Azure."
services: virtual-machines-linux
documentationcenter: 
author: dlepow
manager: timlt
editor: 
tags: azure-service-management,azure-resource-manager
ms.assetid: 2cacda3b-7949-4036-bd5d-837e8b09a9c8
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 03/08/2017
ms.author: danlep
ms.openlocfilehash: 6c44217332538857cc2ca2e85de4b476aa71251c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-ssh-keys-with-windows-on-azure"></a>¿Cómo tooUse SSH claves con Windows en Azure
> [!div class="op_single_selector"]
> * [Windows](ssh-from-windows.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
> * [Linux/Mac](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
>
>

Cuando se conectan tooLinux las máquinas virtuales (VM) en Azure, debe usar [criptografía de clave pública](https://wikipedia.org/wiki/Public-key_cryptography) tooprovide un toolog de manera más segura en tooyour VM de Linux. Este proceso implica un intercambio de claves público y privado con tooauthenticate de comando de shell seguro (SSH) hello en lugar de un nombre de usuario y una contraseña. Las contraseñas son vulnerables toobrute los ataques, sobre todo en máquinas virtuales a través de Internet como los servidores web. Este artículo proporciona información general sobre las claves SSH y cómo toogenerate Hola claves apropiadas en un equipo Windows.

## <a name="overview-of-ssh-and-keys"></a>Información general sobre SSH y sus claves
Mediante el uso de claves públicas y privadas, segura puede iniciar sesión en tooyour VM de Linux:

* Hola **clave pública** se coloca en la VM de Linux o cualquier otro servicio que desea toouse con criptografía de clave pública.
* Hola **clave privada** es lo que se presente tooyour Linux VM cuando inicie sesión, tooverify tu identidad. Esta clave se debe proteger, por lo que no se debe compartir.

Las claves públicas y privadas se pueden usar en varias máquinas virtuales y servicios. No es necesario un par de claves para cada máquina virtual o servicio que se va tooaccess. Para más información, consulte el artículo de Wikipedia sobre [criptografía de clave pública](https://wikipedia.org/wiki/Public-key_cryptography).

SSH es un protocolo de conexión cifrada que permite inicios de sesión seguros sobre conexiones no seguras. Es el protocolo de conexión predeterminado de Hola para máquinas virtuales de Linux hospedadas en Azure. Aunque SSH propio proporciona una conexión cifrada, el uso de contraseñas con las conexiones SSH deja ataques de fuerza toobrute vulnerables de VM de Hola o la averiguación de contraseñas. Un método más seguro y preferido de tooa conectar máquinas virtuales que usan SSH es mediante el uso de estas claves públicas y privadas, también conocido como claves SSH.

Si no desea que las claves SSH de toouse, pueden seguir registrando en tooyour máquinas virtuales de Linux con una contraseña. Si la máquina virtual no está expuesto toohello Internet, el uso de contraseñas puede ser suficiente. Sin embargo, todavía necesita toomanage las contraseñas para cada VM de Linux pero mantener las directivas de contraseña correcto y procedimientos recomendados, como la longitud mínima de contraseña y la actualiza periódicamente. uso de Hola de claves SSH reduce la complejidad de Hola de administrar credenciales individuales a través de varias máquinas virtuales.

## <a name="windows-packages-and-ssh-clients"></a>Paquetes de Windows y los clientes SSH
Conectar tooand administrar máquinas virtuales de Linux en Azure mediante una **cliente SSH**. Normalmente, los equipos de Windows no tienen un cliente ssh instalado. Hola actualización de aniversario de Windows 10 agrega Bash para Windows, y hello más reciente Windows 10 creadores Update proporciona actualizaciones adicionales. Este subsistema de Windows para Linux permite utilidades toorun y acceso como un cliente de SSH de forma nativa dentro de un shell de Bash. Puede seguir cualquiera de los documentos de Linux de hello, como [cómo pares de clave SSH de toogenerate para Linux](mac-create-ssh-keys.md). Bash para Windows está aún en desarrollo y se considera una versión beta. Para más información acerca de Bash para Windows, consulte [Bash on Ubuntu on Windows](https://msdn.microsoft.com/commandline/wsl/about) (Bash en Ubuntu en Windows).

Si desea toouse algo distinto de Bash para Windows, Windows SSH clientes habituales que puede instalar se incluyen en hello siguientes paquetes:

* [Git para Windows](https://git-for-windows.github.io/)
* [puTTY](http://www.chiark.greenend.org.uk/~sgtatham/putty/)
* [MobaXterm](http://mobaxterm.mobatek.net/)
* [Cygwin](https://cygwin.com/)


## <a name="which-key-files-do-you-need-toocreate"></a>¿Archivos de clave que es necesario toocreate?
Azure requiere al menos claves públicas y privadas de 2048 bits con el formato **ssh-rsa**. Si va a administrar recursos de Azure mediante el modelo de implementación de hello clásico, también necesitará toogenerate un PEM (`.pem` archivo).

Estos son los escenarios de implementación de Hola y Hola tipos de archivos que se usan en cada uno:

1. **SSH-rsa** claves son necesarias para cualquier implementación mediante hello [portal de Azure](https://portal.azure.com)y las implementaciones de administrador de recursos mediante hello [CLI de Azure](../../cli-install-nodejs.md).
   * Normalmente estas claves son lo único que necesitan la mayoría de los usuarios.
2. Un `.pem` archivo es necesario toocreate las máquinas virtuales usando la implementación clásica de Hola. Estas claves se admiten en las implementaciones de clásico al usar hello [portal de Azure](https://portal.azure.com) o [CLI de Azure](../../cli-install-nodejs.md).
   * Solo necesita toocreate estos certificados y claves adicionales si va a administrar los recursos creados mediante el modelo de implementación clásica de Hola.

## <a name="install-git-for-windows"></a>Instalación de Git para Windows
sección anterior Hello muestran varios paquetes que incluyen hello `openssl` herramienta para Windows. Esta herramienta es claves públicas y privadas de toocreate necesarios. Hola después detalle de ejemplos de cómo tooinstall y usar **Git para Windows**, aunque puede elegir cualquier paquete que prefiera. **GIT para Windows** le proporcionan acceso software adicional de código abierto de toosome ([OSS](https://en.wikipedia.org/wiki/Open-source_software)) herramientas y utilidades que pueden ser útiles al trabajar con máquinas virtuales de Linux.

1. Descargue e instale **Git para Windows** de hello ubicación siguiente: [https://git-for-windows.github.io/](https://git-for-windows.github.io/).
2. Acepte las opciones predeterminadas de Hola Hola durante el proceso de instalación a menos que necesita específicamente que toochange ellos.
3. Ejecutar **Git Bash** de hello **menú Inicio** > **Git** > **Git Bash**. consola de Hello tiene un aspecto similar toohello siguiente ejemplo:

    ![Shell de Bash de Git para Windows](./media/ssh-from-windows/git-bash-window.png)

## <a name="create-a-private-key"></a>Creación de una clave privada
1. En su **Git Bash** ventana, utilice `openssl.exe` toocreate una clave privada. Hello en el ejemplo siguiente se crea una clave denominada `myPrivateKey` y certificado denominado `myCert.pem`:

    ```bash
    openssl.exe req -x509 -nodes -days 365 -newkey rsa:2048 \
        -keyout myPrivateKey.key -out myCert.pem
    ```

    salida de Hello tiene un aspecto similar toohello siguiente ejemplo:

    ```bash
    Generating a 2048 bit RSA private key
    .......................................+++
    .......................+++
    writing new private key too'myPrivateKey.key'
    -----
    You are about toobe asked tooenter information that will be incorporated
    into your certificate request.
    What you are about tooenter is what is called a Distinguished Name or a DN.
    There are quite a few fields but you can leave some blank
    For some fields there will be a default value,
    If you enter '.', hello field will be left blank.
    -----
    Country Name (2 letter code) [AU]:
    ```

   Si Bash informa de un error, pruebe a abrir una nueva ventana **Git Bash** con privilegios elevados. A continuación, vuelva a ejecutar hello `openssl` comando.

2. Hola de respuesta solicita el nombre de país, la ubicación, nombre de la organización, etcetera.
3. La clave privada y el certificado nuevos se crean en el directorio de trabajo actual. Como medida de seguridad, debes establecer los permisos de hello en su clave privada para que solo se puede obtener acceso a él:

    ```bash
    chmod 0600 myPrivateKey.key
    ```

4. Hola [próxima sección](#create-a-private-key-for-putty) detalles mediante PuTTYgen tooboth ver y usar la clave pública de Hola y crear una clave privada específica para el uso de PuTTY tooSSH tooLinux máquinas virtuales. Hello siguiente comando genera un archivo de clave público denominado `myPublicKey.key` que puede usar inmediatamente:

    ```bash
    openssl.exe rsa -pubout -in myPrivateKey.key -out myPublicKey.key
    ```

5. Si también necesita recursos de toomanage clásico, convertir hello `myCert.pem` demasiado`myCert.cer` (DER codificado X509 certificado). Realice este paso opcional solo si necesita toospecifically administrar recursos de clásico anteriores.

    Convertir el certificado de hello mediante Hola siguiente comando:

    ```bash
    openssl.exe  x509 -outform der -in myCert.pem -out myCert.cer
    ```

## <a name="create-a-private-key-for-putty"></a>Creación de una clave privada para PuTTY
PuTTY es un cliente SSH común para Windows. Se está toouse libre cualquier cliente SSH que desee. toouse PuTTY, deberá toocreate otro tipo de clave: una clave privada PuTTY (PPK). Si no desea toouse PuTTY, omita esta sección.

Hello en el ejemplo siguiente se crea esta clave privada adicional específicamente para toouse PuTTY:

1. Use **Git Bash** tooconvert su privada de clave en una clave privada RSA que se puede entender PuTTYgen. Hello en el ejemplo siguiente se crea una clave denominada `myPrivateKey_rsa` de clave existente de hello denominada `myPrivateKey`:

    ```bash
    openssl rsa -in ./myPrivateKey.key -out myPrivateKey_rsa
    ```

    Como medida de seguridad, debes establecer los permisos de hello en su clave privada para que solo se puede obtener acceso a él:

    ```bash
    chmod 0600 myPrivateKey_rsa
    ```
2. Descargue y ejecute PuTTYgen desde Hola ubicación siguiente: [http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html](http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html)
3. Haga clic en el menú de hello: **archivo** > **clave privada de carga**
4. Busque la clave privada (`myPrivateKey_rsa` en el ejemplo anterior de hello). directorio predeterminado de Hello al iniciar **Git Bash** es `C:\Users\%username%`. Cambiar Hola archivo filtro tooshow **todos los archivos (\*.\*)** :

    ![Cargar la clave privada existente de hello en PuTTYgen](./media/ssh-from-windows/load-private-key.png)
5. Haga clic en **Abrir**. Un símbolo del sistema indica que se ha importado correctamente esa clave hello:

    ![Clave tooPuTTYgen se importó correctamente](./media/ssh-from-windows/successfully-imported-key.png)
6. Haga clic en **Aceptar** el símbolo del sistema de tooclose Hola.
7. clave pública de Hola se muestra en la parte superior de Hola de hello **PuTTYgen** ventana. Copie y pegue esta clave pública en hello portal de Azure o una plantilla de Azure Resource Manager cuando se crea una VM de Linux. También puede hacer clic en **guardar de clave pública** toosave un equipo de tooyour de copia:

    ![Guardar archivo de clave pública de PuTTY](./media/ssh-from-windows/save-public-key.png)

    Hello en el ejemplo siguiente se muestra cómo se copie y pegue esta clave pública en hello portal de Azure cuando se crea una VM de Linux. clave pública de Hello normalmente se almacena en `~/.ssh/authorized_keys` en la nueva máquina virtual.

    ![Usar la clave pública al crear una máquina virtual en hello portal de Azure](./media/ssh-from-windows/use-public-key-azure-portal.png)
8. En **PuTTYgen**, haga clic en **Save private Key** (Guardar clave privada):

    ![Guarde el archivo de clave privada de PuTTY](./media/ssh-from-windows/save-ppk-file.png)

   > [!WARNING]
   > Un mensaje le pregunta si desea toocontinue sin escribir una frase de contraseña para la clave. Una frase de contraseña es similar a una clave privada de contraseña tooyour adjunto. Incluso si alguien lograra tooobtain su clave privada, todavía no sería capaz de tooauthenticate utilizando simplemente Hola clave. También necesitaría Hola frase de contraseña. Sin una frase de contraseña, si un usuario obtiene la clave privada, pueden iniciar sesión en tooany VM o servicio que utiliza esa clave. Por consiguiente, se recomienda crear una frase de contraseña. Sin embargo, si se olvida la frase de contraseña de hello, no hay ningún toorecover de manera.
   >
   >

    Si desea tooenter una frase de contraseña, haga clic en **No**, escriba una frase de contraseña en la ventana principal de PuTTYgen de hello y, a continuación, haga clic en **clave privada de guardar** nuevo. En caso contrario, haga clic en **Sí** toocontinue sin proporcionar la frase de contraseña opcional Hola.
9. Escriba un nombre y una ubicación toosave el archivo PPK.

## <a name="use-putty-toossh-tooa-linux-machine"></a>Usar Putty tooSSH tooa máquina Linux
PuTTY es un cliente SSH común para Windows. Se está toouse libre cualquier cliente SSH que desee. Hola siguientes detalles de pasos de cómo toouse su tooauthenticate clave privada con la máquina virtual de Azure mediante SSH. Hola pasos son similares en otros clientes de la claves SSH en cuanto a la necesidad de tooload la conexión SSH de hello tooauthenticate clave privada.

1. Descarga y ejecución putty de Hola siguiente ubicación: [http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html](http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html)
2. Rellene el nombre de host de Hola o dirección IP de la máquina virtual de hello portal de Azure:

    ![Abrir conexión nueva de PuTTY](./media/ssh-from-windows/putty-new-connection.png)
3. Antes de seleccionar **Open** (Abrir), haga clic en la pestaña **Connection** (Conexión) > **SSH** > **Auth** (Autorización). Examinar tooand seleccione su clave privada:

    ![Seleccionar la clave privada PuTTY para la autenticación](./media/ssh-from-windows/putty-auth-dialog.png)
4. Haga clic en **abiertos** tooconnect tooyour virtual machine

## <a name="next-steps"></a>Pasos siguientes
También puede generar claves públicas y privadas de hello [con OS X y Linux](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

Para obtener más información acerca de Bash para Windows y las ventajas de Hola de contar con herramientas de sistemas operativos disponibles en el equipo de Windows, vea [Bash en Ubuntu en Windows](https://msdn.microsoft.com/commandline/wsl/about).

Si tiene problemas al utilizar SSH tooconnect tooyour máquinas virtuales de Linux, consulte [solucionar problemas de SSH conexiones tooan VM de Linux de Azure](troubleshoot-ssh-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).
