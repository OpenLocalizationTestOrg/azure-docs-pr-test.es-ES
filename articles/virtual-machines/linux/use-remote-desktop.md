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
# <a name="install-and-configure-remote-desktop-tooconnect-tooa-linux-vm-in-azure"></a><span data-ttu-id="b8f87-103">Instalar y configurar Escritorio remoto tooconnect tooa VM de Linux en Azure</span><span class="sxs-lookup"><span data-stu-id="b8f87-103">Install and configure Remote Desktop tooconnect tooa Linux VM in Azure</span></span>
<span data-ttu-id="b8f87-104">Máquinas virtuales de Linux (VM) en Azure normalmente se administran desde la línea de comandos de hello mediante una conexión de shell seguro (SSH).</span><span class="sxs-lookup"><span data-stu-id="b8f87-104">Linux virtual machines (VMs) in Azure are usually managed from hello command line using a secure shell (SSH) connection.</span></span> <span data-ttu-id="b8f87-105">Cuando tooLinux nueva, o para escenarios de solución de problemas rápidos, probablemente sea más fácil usar Hola de escritorio remoto.</span><span class="sxs-lookup"><span data-stu-id="b8f87-105">When new tooLinux, or for quick troubleshooting scenarios, hello use of remote desktop may be easier.</span></span> <span data-ttu-id="b8f87-106">Este artículo detalles de cómo tooinstall y configurar un entorno de escritorio ([xfce](https://www.xfce.org)) y el escritorio remoto ([xrdp](http://www.xrdp.org)) para la VM de Linux con el modelo de implementación del Administrador de recursos de Hola.</span><span class="sxs-lookup"><span data-stu-id="b8f87-106">This article details how tooinstall and configure a desktop environment ([xfce](https://www.xfce.org)) and remote desktop ([xrdp](http://www.xrdp.org)) for your Linux VM using hello Resource Manager deployment model.</span></span>


## <a name="prerequisites"></a><span data-ttu-id="b8f87-107">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="b8f87-107">Prerequisites</span></span>
<span data-ttu-id="b8f87-108">Este artículo requiere una máquina virtual de Linux existente en Azure.</span><span class="sxs-lookup"><span data-stu-id="b8f87-108">This article requires an existing Linux VM in Azure.</span></span> <span data-ttu-id="b8f87-109">Si necesita toocreate una máquina virtual, utilice uno de los siguientes métodos de hello:</span><span class="sxs-lookup"><span data-stu-id="b8f87-109">If you need toocreate a VM, use one of hello following methods:</span></span>

- <span data-ttu-id="b8f87-110">Hola [2.0 de CLI de Azure](quick-create-cli.md)</span><span class="sxs-lookup"><span data-stu-id="b8f87-110">hello [Azure CLI 2.0](quick-create-cli.md)</span></span>
- <span data-ttu-id="b8f87-111">Hola [portal de Azure](quick-create-portal.md)</span><span class="sxs-lookup"><span data-stu-id="b8f87-111">hello [Azure portal](quick-create-portal.md)</span></span>


## <a name="install-a-desktop-environment-on-your-linux-vm"></a><span data-ttu-id="b8f87-112">Instalar un entorno de escritorio en la máquina virtual Linux</span><span class="sxs-lookup"><span data-stu-id="b8f87-112">Install a desktop environment on your Linux VM</span></span>
<span data-ttu-id="b8f87-113">La mayoría de las máquinas virtuales Linux en Azure no tienen un entorno de escritorio instalado de forma predeterminada.</span><span class="sxs-lookup"><span data-stu-id="b8f87-113">Most Linux VMs in Azure do not have a desktop environment installed by default.</span></span> <span data-ttu-id="b8f87-114">Las máquinas virtuales Linux normalmente se administran mediante conexiones SSH en lugar de con un entorno de escritorio.</span><span class="sxs-lookup"><span data-stu-id="b8f87-114">Linux VMs are commonly managed using SSH connections rather than a desktop environment.</span></span> <span data-ttu-id="b8f87-115">Existen varios entornos de escritorio en Linux que puede elegir.</span><span class="sxs-lookup"><span data-stu-id="b8f87-115">There are various desktop environments in Linux that you can choose.</span></span> <span data-ttu-id="b8f87-116">Según la elección del entorno de escritorio, puede consumir una GB too2 de espacio en disco y toman 5 too10 minutos tooinstall y configurar todos los paquetes de saludo necesario.</span><span class="sxs-lookup"><span data-stu-id="b8f87-116">Depending on your choice of desktop environment, it may consume one too2 GB of disk space, and take 5 too10 minutes tooinstall and configure all hello required packages.</span></span>

<span data-ttu-id="b8f87-117">Hello en el ejemplo siguiente se instala ligero hello [xfce4](https://www.xfce.org/) entorno de escritorio en una VM Ubuntu.</span><span class="sxs-lookup"><span data-stu-id="b8f87-117">hello following example installs hello lightweight [xfce4](https://www.xfce.org/) desktop environment on an Ubuntu VM.</span></span> <span data-ttu-id="b8f87-118">Comandos para otras distribuciones varían ligeramente (usar `yum` tooinstall en Red Hat Enterprise Linux y configurar adecuado `selinux` reglas o use `zypper` tooinstall en SUSE, por ejemplo).</span><span class="sxs-lookup"><span data-stu-id="b8f87-118">Commands for other distributions vary slightly (use `yum` tooinstall on Red Hat Enterprise Linux and configure appropriate `selinux` rules, or use `zypper` tooinstall on SUSE, for example).</span></span>

<span data-ttu-id="b8f87-119">En primer lugar, SSH tooyour máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="b8f87-119">First, SSH tooyour VM.</span></span> <span data-ttu-id="b8f87-120">Hello en el ejemplo siguiente se conecta toohello máquina virtual denominada *myvm.westus.cloudapp.azure.com* con el nombre de usuario de Hola de *azureuser*:</span><span class="sxs-lookup"><span data-stu-id="b8f87-120">hello following example connects toohello VM named *myvm.westus.cloudapp.azure.com* with hello username of *azureuser*:</span></span>

```bash
ssh azureuser@myvm.westus.cloudapp.azure.com
```

<span data-ttu-id="b8f87-121">Si está utilizando Windows y necesita más información sobre el uso de SSH, consulte [cómo toouse SSH claves con Windows](ssh-from-windows.md).</span><span class="sxs-lookup"><span data-stu-id="b8f87-121">If you are using Windows and need more information on using SSH, see [How toouse SSH keys with Windows](ssh-from-windows.md).</span></span>

<span data-ttu-id="b8f87-122">A continuación, instale xfce con `apt` como se indica a continuación:</span><span class="sxs-lookup"><span data-stu-id="b8f87-122">Next, install xfce using `apt` as follows:</span></span>

```bash
sudo apt-get update
sudo apt-get install xfce4
```

## <a name="install-and-configure-a-remote-desktop-server"></a><span data-ttu-id="b8f87-123">Instalar y configurar un servidor de escritorio remoto</span><span class="sxs-lookup"><span data-stu-id="b8f87-123">Install and configure a remote desktop server</span></span>
<span data-ttu-id="b8f87-124">Ahora que tiene instalado un entorno de escritorio, configure un toolisten de servicios de escritorio remoto para las conexiones entrantes.</span><span class="sxs-lookup"><span data-stu-id="b8f87-124">Now that you have a desktop environment installed, configure a remote desktop service toolisten for incoming connections.</span></span> <span data-ttu-id="b8f87-125">[xrdp](http://xrdp.org) es un servidor de protocolo de escritorio remoto (RDP) de código abierto que está disponible en la mayoría de las distribuciones de Linux y funciona bien con xfce.</span><span class="sxs-lookup"><span data-stu-id="b8f87-125">[xrdp](http://xrdp.org) is an open source Remote Desktop Protocol (RDP) server that is available on most Linux distributions, and works well with xfce.</span></span> <span data-ttu-id="b8f87-126">Instalar xrdp en la máquina virtual de Ubuntu de la siguiente forma:</span><span class="sxs-lookup"><span data-stu-id="b8f87-126">Install xrdp on your Ubuntu VM as follows:</span></span>

```bash
sudo apt-get install xrdp
```

<span data-ttu-id="b8f87-127">Indicar xrdp qué toouse del entorno de escritorio cuando se inicia la sesión.</span><span class="sxs-lookup"><span data-stu-id="b8f87-127">Tell xrdp what desktop environment toouse when you start your session.</span></span> <span data-ttu-id="b8f87-128">Configure xrdp toouse xfce como el entorno de escritorio de la manera siguiente:</span><span class="sxs-lookup"><span data-stu-id="b8f87-128">Configure xrdp toouse xfce as your desktop environment as follows:</span></span>

```bash
echo xfce4-session >~/.xsession
```

<span data-ttu-id="b8f87-129">Reinicie el servicio de xrdp de Hola Hola cambios tootake efecto como sigue:</span><span class="sxs-lookup"><span data-stu-id="b8f87-129">Restart hello xrdp service for hello changes tootake effect as follows:</span></span>

```bash
sudo service xrdp restart
```


## <a name="set-a-local-user-account-password"></a><span data-ttu-id="b8f87-130">Establecer una contraseña de cuenta de usuario</span><span class="sxs-lookup"><span data-stu-id="b8f87-130">Set a local user account password</span></span>
<span data-ttu-id="b8f87-131">Si ha creado una contraseña para su cuenta de usuario cuando se creó la máquina virtual, omita este paso.</span><span class="sxs-lookup"><span data-stu-id="b8f87-131">If you created a password for your user account when you created your VM, skip this step.</span></span> <span data-ttu-id="b8f87-132">Si solo usa la autenticación de clave SSH y no tiene una contraseña de cuenta local establecido, especifique una contraseña antes de usar xrdp toolog en tooyour máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="b8f87-132">If you only use SSH key authentication and do not have a local account password set, specify a password before you use xrdp toolog in tooyour VM.</span></span> <span data-ttu-id="b8f87-133">xrdp no puede aceptar las claves SSH para la autenticación.</span><span class="sxs-lookup"><span data-stu-id="b8f87-133">xrdp cannot accept SSH keys for authentication.</span></span> <span data-ttu-id="b8f87-134">Hello en el ejemplo siguiente se especifica una contraseña para la cuenta de usuario de hello *azureuser*:</span><span class="sxs-lookup"><span data-stu-id="b8f87-134">hello following example specifies a password for hello user account *azureuser*:</span></span>

```bash
sudo passwd azureuser
```

> [!NOTE]
> <span data-ttu-id="b8f87-135">Especificando una contraseña no actualiza sus inicios de sesión de contraseña SSHD configuración toopermit si actualmente no es así.</span><span class="sxs-lookup"><span data-stu-id="b8f87-135">Specifying a password does not update your SSHD configuration toopermit password logins if it currently does not.</span></span> <span data-ttu-id="b8f87-136">Desde la perspectiva de seguridad, puede desea tooconnect tooyour máquina virtual con un túnel SSH mediante la autenticación basada en claves y, a continuación, conectarse tooxrdp.</span><span class="sxs-lookup"><span data-stu-id="b8f87-136">From a security perspective, you may wish tooconnect tooyour VM with an SSH tunnel using key-based authentication and then connect tooxrdp.</span></span> <span data-ttu-id="b8f87-137">Si es así, omitir Hola siguiendo el paso sobre la creación de un seguridad grupo regla tooallow remoto escritorio tráfico de red.</span><span class="sxs-lookup"><span data-stu-id="b8f87-137">If so, skip hello following step on creating a network security group rule tooallow remote desktop traffic.</span></span>


## <a name="create-a-network-security-group-rule-for-remote-desktop-traffic"></a><span data-ttu-id="b8f87-138">Crear una regla de grupo de seguridad de red para el tráfico de escritorio remoto</span><span class="sxs-lookup"><span data-stu-id="b8f87-138">Create a Network Security Group rule for Remote Desktop traffic</span></span>
<span data-ttu-id="b8f87-139">tooreach de tráfico de escritorio remoto de tooallow la VM de Linux, una regla de grupo de seguridad de red debe toobe creado que permite TCP en el puerto 3389 tooreach la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="b8f87-139">tooallow Remote Desktop traffic tooreach your Linux VM, a network security group rule needs toobe created that allows TCP on port 3389 tooreach your VM.</span></span> <span data-ttu-id="b8f87-140">Para más información acerca de las reglas de grupos de seguridad de red, consulte [¿Qué es un grupo de seguridad de red?](../../virtual-network/virtual-networks-nsg.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)</span><span class="sxs-lookup"><span data-stu-id="b8f87-140">For more information about network security group rules, see [What is a Network Security Group?](../../virtual-network/virtual-networks-nsg.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)</span></span> <span data-ttu-id="b8f87-141">También puede [uso Hola toocreate portal Azure de una regla de grupo de seguridad de red](../windows/nsg-quickstart-portal.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="b8f87-141">You can also [use hello Azure portal toocreate a network security group rule](../windows/nsg-quickstart-portal.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

<span data-ttu-id="b8f87-142">en los ejemplos siguientes Hello crean una regla de grupo de seguridad de red con [crear regla de nsg de red az](/cli/azure/network/nsg/rule#create) denominado *myNetworkSecurityGroupRule* demasiado*permitir* tráfico en *tcp* puerto *3389*.</span><span class="sxs-lookup"><span data-stu-id="b8f87-142">hello following examples create a network security group rule with [az network nsg rule create](/cli/azure/network/nsg/rule#create) named *myNetworkSecurityGroupRule* too*allow* traffic on *tcp* port *3389*.</span></span>

```azurecli
az network nsg rule create \
    --resource-group myResourceGroup \
    --nsg-name myNetworkSecurityGroup \
    --name myNetworkSecurityGroupRule \
    --protocol tcp \
    --priority 1010 \
    --destination-port-range 3389
```


## <a name="connect-your-linux-vm-with-a-remote-desktop-client"></a><span data-ttu-id="b8f87-143">Conectar la máquina virtual Linux con un cliente de escritorio remoto</span><span class="sxs-lookup"><span data-stu-id="b8f87-143">Connect your Linux VM with a Remote Desktop client</span></span>
<span data-ttu-id="b8f87-144">Abra al cliente de escritorio remoto local y conéctese toohello dirección IP o nombre DNS de la VM de Linux.</span><span class="sxs-lookup"><span data-stu-id="b8f87-144">Open your local remote desktop client and connect toohello IP address or DNS name of your Linux VM.</span></span> <span data-ttu-id="b8f87-145">Escriba Hola nombre de usuario y la contraseña de cuenta de usuario de hello en su máquina virtual como se indica a continuación:</span><span class="sxs-lookup"><span data-stu-id="b8f87-145">Enter hello username and password for hello user account on your VM as follows:</span></span>

![Conectar tooxrdp mediante el cliente de escritorio remoto](./media/use-remote-desktop/remote-desktop-client.png)

<span data-ttu-id="b8f87-147">Después de autenticar, entorno de escritorio de hello xfce se cargarán y buscar similar toohello siguiente ejemplo:</span><span class="sxs-lookup"><span data-stu-id="b8f87-147">After authenticating, hello xfce desktop environment will load and look similar toohello following example:</span></span>

![entorno de escritorio xfce a través de xrdp](./media/use-remote-desktop/xfce-desktop-environment.png)


## <a name="troubleshoot"></a><span data-ttu-id="b8f87-149">Solución de problemas</span><span class="sxs-lookup"><span data-stu-id="b8f87-149">Troubleshoot</span></span>
<span data-ttu-id="b8f87-150">Si no se puede conectar tooyour VM de Linux con un cliente de escritorio remoto, use `netstat` en su tooverify de VM de Linux que la máquina virtual está realizando escuchas para las conexiones RDP como sigue:</span><span class="sxs-lookup"><span data-stu-id="b8f87-150">If you cannot connect tooyour Linux VM using a Remote Desktop client, use `netstat` on your Linux VM tooverify that your VM is listening for RDP connections  as follows:</span></span>

```bash
sudo netstat -plnt | grep rdp
```

<span data-ttu-id="b8f87-151">Hola siguiente ejemplo se muestra hello VM escuchando en el puerto TCP 3389 según lo esperado:</span><span class="sxs-lookup"><span data-stu-id="b8f87-151">hello following example shows hello VM listening on TCP port 3389 as expected:</span></span>

```bash
tcp     0     0      127.0.0.1:3350     0.0.0.0:*     LISTEN     53192/xrdp-sesman
tcp     0     0      0.0.0.0:3389       0.0.0.0:*     LISTEN     53188/xrdp
```

<span data-ttu-id="b8f87-152">Si no está escuchando el servicio de xrdp hello, en una VM Ubuntu reinicie Hola servicio como se indica a continuación:</span><span class="sxs-lookup"><span data-stu-id="b8f87-152">If hello xrdp service is not listening, on an Ubuntu VM restart hello service as follows:</span></span>

```bash
sudo service xrdp restart
```

<span data-ttu-id="b8f87-153">Revisar registros en */var/log*Thug en la VM Ubuntu para obtener indicaciones sobre como servicio de hello toowhy posible no responda.</span><span class="sxs-lookup"><span data-stu-id="b8f87-153">Review logs in */var/log*Thug  on your Ubuntu VM for indications as toowhy hello service may not be responding.</span></span> <span data-ttu-id="b8f87-154">También puede supervisar syslog de Hola durante un tooview de intento de conexión a Escritorio remoto los errores:</span><span class="sxs-lookup"><span data-stu-id="b8f87-154">You can also monitor hello syslog during a remote desktop connection attempt tooview any errors:</span></span>

```bash
tail -f /var/log/syslog
```

<span data-ttu-id="b8f87-155">Pueden tener otras distribuciones de Linux como Red Hat Enterprise Linux y SUSE tooreview de ubicaciones de archivo de registro alternativo y servicios de toorestart de maneras diferentes.</span><span class="sxs-lookup"><span data-stu-id="b8f87-155">Other Linux distributions such as Red Hat Enterprise Linux and SUSE may have different ways toorestart services and alternate log file locations tooreview.</span></span>

<span data-ttu-id="b8f87-156">Si no se recibe ninguna respuesta en el cliente de escritorio remoto y no ve todos los eventos de registro del sistema hello, este comportamiento indica que el tráfico de escritorio remoto no puede llegar a Hola VM.</span><span class="sxs-lookup"><span data-stu-id="b8f87-156">If you do not receive any response in your remote desktop client and do not see any events in hello system log, this behavior indicates that remote desktop traffic cannot reach hello VM.</span></span> <span data-ttu-id="b8f87-157">Revise su tooensure de reglas de grupo de seguridad de red que tienen un toopermit regla TCP en el puerto 3389.</span><span class="sxs-lookup"><span data-stu-id="b8f87-157">Review your network security group rules tooensure that you have a rule toopermit TCP on port 3389.</span></span> <span data-ttu-id="b8f87-158">Para obtener más información, consulte [Solucionar problemas de conectividad de la aplicación](../windows/troubleshoot-app-connection.md).</span><span class="sxs-lookup"><span data-stu-id="b8f87-158">For more information, see [Troubleshoot application connectivity issues](../windows/troubleshoot-app-connection.md).</span></span>


## <a name="next-steps"></a><span data-ttu-id="b8f87-159">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="b8f87-159">Next steps</span></span>
<span data-ttu-id="b8f87-160">Para obtener más información sobre cómo crear y utilizar claves de SSH con máquinas virtuales Linux, consulte [Crear claves SSH para máquinas virtuales de Linux en Azure](mac-create-ssh-keys.md).</span><span class="sxs-lookup"><span data-stu-id="b8f87-160">For more information about creating and using SSH keys with Linux VMs, see [Create SSH keys for Linux VMs in Azure](mac-create-ssh-keys.md).</span></span>

<span data-ttu-id="b8f87-161">Para obtener información sobre el uso de SSH de Windows, vea [cómo toouse SSH claves con Windows](ssh-from-windows.md).</span><span class="sxs-lookup"><span data-stu-id="b8f87-161">For information on using SSH from Windows, see [How toouse SSH keys with Windows](ssh-from-windows.md).</span></span>

