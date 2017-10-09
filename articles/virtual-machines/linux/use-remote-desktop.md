---
title: tooa de escritorio remoto aaaUse VM de Linux en Azure | Documentos de Microsoft
description: "Obtenga información acerca de cómo tooinstall y configurar Escritorio remoto (xrdp) tooconnect tooa VM de Linux en Azure con las herramientas gráficas"
services: virtual-machines-linux
documentationcenter: 
author: iainfoulds
manager: timlt
editor: 
ms.assetid: 
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 06/22/2017
ms.author: iainfou
ms.openlocfilehash: 64d30be101ceeb49fc05bb10293ad63db358efe3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="install-and-configure-remote-desktop-tooconnect-tooa-linux-vm-in-azure"></a>Instalar y configurar Escritorio remoto tooconnect tooa VM de Linux en Azure
Máquinas virtuales de Linux (VM) en Azure normalmente se administran desde la línea de comandos de hello mediante una conexión de shell seguro (SSH). Cuando tooLinux nueva, o para escenarios de solución de problemas rápidos, probablemente sea más fácil usar Hola de escritorio remoto. Este artículo detalles de cómo tooinstall y configurar un entorno de escritorio ([xfce](https://www.xfce.org)) y el escritorio remoto ([xrdp](http://www.xrdp.org)) para la VM de Linux con el modelo de implementación del Administrador de recursos de Hola.


## <a name="prerequisites"></a>Requisitos previos
Este artículo requiere una máquina virtual de Linux existente en Azure. Si necesita toocreate una máquina virtual, utilice uno de los siguientes métodos de hello:

- Hola [2.0 de CLI de Azure](quick-create-cli.md)
- Hola [portal de Azure](quick-create-portal.md)


## <a name="install-a-desktop-environment-on-your-linux-vm"></a>Instalar un entorno de escritorio en la máquina virtual Linux
La mayoría de las máquinas virtuales Linux en Azure no tienen un entorno de escritorio instalado de forma predeterminada. Las máquinas virtuales Linux normalmente se administran mediante conexiones SSH en lugar de con un entorno de escritorio. Existen varios entornos de escritorio en Linux que puede elegir. Según la elección del entorno de escritorio, puede consumir una GB too2 de espacio en disco y toman 5 too10 minutos tooinstall y configurar todos los paquetes de saludo necesario.

Hello en el ejemplo siguiente se instala ligero hello [xfce4](https://www.xfce.org/) entorno de escritorio en una VM Ubuntu. Comandos para otras distribuciones varían ligeramente (usar `yum` tooinstall en Red Hat Enterprise Linux y configurar adecuado `selinux` reglas o use `zypper` tooinstall en SUSE, por ejemplo).

En primer lugar, SSH tooyour máquina virtual. Hello en el ejemplo siguiente se conecta toohello máquina virtual denominada *myvm.westus.cloudapp.azure.com* con el nombre de usuario de Hola de *azureuser*:

```bash
ssh azureuser@myvm.westus.cloudapp.azure.com
```

Si está utilizando Windows y necesita más información sobre el uso de SSH, consulte [cómo toouse SSH claves con Windows](ssh-from-windows.md).

A continuación, instale xfce con `apt` como se indica a continuación:

```bash
sudo apt-get update
sudo apt-get install xfce4
```

## <a name="install-and-configure-a-remote-desktop-server"></a>Instalar y configurar un servidor de escritorio remoto
Ahora que tiene instalado un entorno de escritorio, configure un toolisten de servicios de escritorio remoto para las conexiones entrantes. [xrdp](http://xrdp.org) es un servidor de protocolo de escritorio remoto (RDP) de código abierto que está disponible en la mayoría de las distribuciones de Linux y funciona bien con xfce. Instalar xrdp en la máquina virtual de Ubuntu de la siguiente forma:

```bash
sudo apt-get install xrdp
```

Indicar xrdp qué toouse del entorno de escritorio cuando se inicia la sesión. Configure xrdp toouse xfce como el entorno de escritorio de la manera siguiente:

```bash
echo xfce4-session >~/.xsession
```

Reinicie el servicio de xrdp de Hola Hola cambios tootake efecto como sigue:

```bash
sudo service xrdp restart
```


## <a name="set-a-local-user-account-password"></a>Establecer una contraseña de cuenta de usuario
Si ha creado una contraseña para su cuenta de usuario cuando se creó la máquina virtual, omita este paso. Si solo usa la autenticación de clave SSH y no tiene una contraseña de cuenta local establecido, especifique una contraseña antes de usar xrdp toolog en tooyour máquina virtual. xrdp no puede aceptar las claves SSH para la autenticación. Hello en el ejemplo siguiente se especifica una contraseña para la cuenta de usuario de hello *azureuser*:

```bash
sudo passwd azureuser
```

> [!NOTE]
> Especificando una contraseña no actualiza sus inicios de sesión de contraseña SSHD configuración toopermit si actualmente no es así. Desde la perspectiva de seguridad, puede desea tooconnect tooyour máquina virtual con un túnel SSH mediante la autenticación basada en claves y, a continuación, conectarse tooxrdp. Si es así, omitir Hola siguiendo el paso sobre la creación de un seguridad grupo regla tooallow remoto escritorio tráfico de red.


## <a name="create-a-network-security-group-rule-for-remote-desktop-traffic"></a>Crear una regla de grupo de seguridad de red para el tráfico de escritorio remoto
tooreach de tráfico de escritorio remoto de tooallow la VM de Linux, una regla de grupo de seguridad de red debe toobe creado que permite TCP en el puerto 3389 tooreach la máquina virtual. Para más información acerca de las reglas de grupos de seguridad de red, consulte [¿Qué es un grupo de seguridad de red?](../../virtual-network/virtual-networks-nsg.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) También puede [uso Hola toocreate portal Azure de una regla de grupo de seguridad de red](../windows/nsg-quickstart-portal.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

en los ejemplos siguientes Hello crean una regla de grupo de seguridad de red con [crear regla de nsg de red az](/cli/azure/network/nsg/rule#create) denominado *myNetworkSecurityGroupRule* demasiado*permitir* tráfico en *tcp* puerto *3389*.

```azurecli
az network nsg rule create \
    --resource-group myResourceGroup \
    --nsg-name myNetworkSecurityGroup \
    --name myNetworkSecurityGroupRule \
    --protocol tcp \
    --priority 1010 \
    --destination-port-range 3389
```


## <a name="connect-your-linux-vm-with-a-remote-desktop-client"></a>Conectar la máquina virtual Linux con un cliente de escritorio remoto
Abra al cliente de escritorio remoto local y conéctese toohello dirección IP o nombre DNS de la VM de Linux. Escriba Hola nombre de usuario y la contraseña de cuenta de usuario de hello en su máquina virtual como se indica a continuación:

![Conectar tooxrdp mediante el cliente de escritorio remoto](./media/use-remote-desktop/remote-desktop-client.png)

Después de autenticar, entorno de escritorio de hello xfce se cargarán y buscar similar toohello siguiente ejemplo:

![entorno de escritorio xfce a través de xrdp](./media/use-remote-desktop/xfce-desktop-environment.png)


## <a name="troubleshoot"></a>Solución de problemas
Si no se puede conectar tooyour VM de Linux con un cliente de escritorio remoto, use `netstat` en su tooverify de VM de Linux que la máquina virtual está realizando escuchas para las conexiones RDP como sigue:

```bash
sudo netstat -plnt | grep rdp
```

Hola siguiente ejemplo se muestra hello VM escuchando en el puerto TCP 3389 según lo esperado:

```bash
tcp     0     0      127.0.0.1:3350     0.0.0.0:*     LISTEN     53192/xrdp-sesman
tcp     0     0      0.0.0.0:3389       0.0.0.0:*     LISTEN     53188/xrdp
```

Si no está escuchando el servicio de xrdp hello, en una VM Ubuntu reinicie Hola servicio como se indica a continuación:

```bash
sudo service xrdp restart
```

Revisar registros en */var/log*Thug en la VM Ubuntu para obtener indicaciones sobre como servicio de hello toowhy posible no responda. También puede supervisar syslog de Hola durante un tooview de intento de conexión a Escritorio remoto los errores:

```bash
tail -f /var/log/syslog
```

Pueden tener otras distribuciones de Linux como Red Hat Enterprise Linux y SUSE tooreview de ubicaciones de archivo de registro alternativo y servicios de toorestart de maneras diferentes.

Si no se recibe ninguna respuesta en el cliente de escritorio remoto y no ve todos los eventos de registro del sistema hello, este comportamiento indica que el tráfico de escritorio remoto no puede llegar a Hola VM. Revise su tooensure de reglas de grupo de seguridad de red que tienen un toopermit regla TCP en el puerto 3389. Para obtener más información, consulte [Solucionar problemas de conectividad de la aplicación](../windows/troubleshoot-app-connection.md).


## <a name="next-steps"></a>Pasos siguientes
Para obtener más información sobre cómo crear y utilizar claves de SSH con máquinas virtuales Linux, consulte [Crear claves SSH para máquinas virtuales de Linux en Azure](mac-create-ssh-keys.md).

Para obtener información sobre el uso de SSH de Windows, vea [cómo toouse SSH claves con Windows](ssh-from-windows.md).

