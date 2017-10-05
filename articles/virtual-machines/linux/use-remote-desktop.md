---
title: "Uso del escritorio remoto a una máquina virtual Linux en Azure | Microsoft Docs"
description: "Obtenga información acerca de cómo instalar y configurar el escritorio remoto (xrdp) para conectarse a una máquina virtual Linux en Azure con herramientas gráficas"
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
ms.openlocfilehash: d8d6130a270285c84c1dd057a3512cdeb39287f6
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/18/2017
---
# <a name="install-and-configure-remote-desktop-to-connect-to-a-linux-vm-in-azure"></a><span data-ttu-id="827dd-103">Instalación y configuración del escritorio remoto para conectarse a una máquina virtual Linux en Azure</span><span class="sxs-lookup"><span data-stu-id="827dd-103">Install and configure Remote Desktop to connect to a Linux VM in Azure</span></span>
<span data-ttu-id="827dd-104">Las máquinas virtuales de Linux (VM) en Azure normalmente se administran desde la línea de comandos mediante una conexión de shell seguro (SSH).</span><span class="sxs-lookup"><span data-stu-id="827dd-104">Linux virtual machines (VMs) in Azure are usually managed from the command line using a secure shell (SSH) connection.</span></span> <span data-ttu-id="827dd-105">Cuando sean nuevas en Linux, o para escenarios de solución de problemas rápidos, el uso del escritorio remoto puede ser más fácil.</span><span class="sxs-lookup"><span data-stu-id="827dd-105">When new to Linux, or for quick troubleshooting scenarios, the use of remote desktop may be easier.</span></span> <span data-ttu-id="827dd-106">En este artículo se detalla cómo instalar y configurar un entorno de escritorio ([xfce](https://www.xfce.org)) y el escritorio remoto ([xrdp](http://www.xrdp.org)) para la máquina virtual Linux con el modelo de implementación de Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="827dd-106">This article details how to install and configure a desktop environment ([xfce](https://www.xfce.org)) and remote desktop ([xrdp](http://www.xrdp.org)) for your Linux VM using the Resource Manager deployment model.</span></span>


## <a name="prerequisites"></a><span data-ttu-id="827dd-107">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="827dd-107">Prerequisites</span></span>
<span data-ttu-id="827dd-108">Este artículo requiere una máquina virtual de Linux existente en Azure.</span><span class="sxs-lookup"><span data-stu-id="827dd-108">This article requires an existing Linux VM in Azure.</span></span> <span data-ttu-id="827dd-109">Si necesita crear una máquina virtual, utilice uno de los métodos siguientes:</span><span class="sxs-lookup"><span data-stu-id="827dd-109">If you need to create a VM, use one of the following methods:</span></span>

- <span data-ttu-id="827dd-110">La [CLI de Azure 2.0](quick-create-cli.md)</span><span class="sxs-lookup"><span data-stu-id="827dd-110">The [Azure CLI 2.0](quick-create-cli.md)</span></span>
- <span data-ttu-id="827dd-111">[Azure Portal](quick-create-portal.md)</span><span class="sxs-lookup"><span data-stu-id="827dd-111">The [Azure portal](quick-create-portal.md)</span></span>


## <a name="install-a-desktop-environment-on-your-linux-vm"></a><span data-ttu-id="827dd-112">Instalar un entorno de escritorio en la máquina virtual Linux</span><span class="sxs-lookup"><span data-stu-id="827dd-112">Install a desktop environment on your Linux VM</span></span>
<span data-ttu-id="827dd-113">La mayoría de las máquinas virtuales Linux en Azure no tienen un entorno de escritorio instalado de forma predeterminada.</span><span class="sxs-lookup"><span data-stu-id="827dd-113">Most Linux VMs in Azure do not have a desktop environment installed by default.</span></span> <span data-ttu-id="827dd-114">Las máquinas virtuales Linux normalmente se administran mediante conexiones SSH en lugar de con un entorno de escritorio.</span><span class="sxs-lookup"><span data-stu-id="827dd-114">Linux VMs are commonly managed using SSH connections rather than a desktop environment.</span></span> <span data-ttu-id="827dd-115">Existen varios entornos de escritorio en Linux que puede elegir.</span><span class="sxs-lookup"><span data-stu-id="827dd-115">There are various desktop environments in Linux that you can choose.</span></span> <span data-ttu-id="827dd-116">Según la elección del entorno de escritorio, se puede utilizar de 1 a 2 GB de espacio en disco y tardar de 5 a 10 minutos en instalar y configurar todos los paquetes necesarios.</span><span class="sxs-lookup"><span data-stu-id="827dd-116">Depending on your choice of desktop environment, it may consume one to 2 GB of disk space, and take 5 to 10 minutes to install and configure all the required packages.</span></span>

<span data-ttu-id="827dd-117">En el ejemplo siguiente se instala el entorno de escritorio [xfce4](https://www.xfce.org/) ligero en una máquina virtual de Ubuntu.</span><span class="sxs-lookup"><span data-stu-id="827dd-117">The following example installs the lightweight [xfce4](https://www.xfce.org/) desktop environment on an Ubuntu VM.</span></span> <span data-ttu-id="827dd-118">Los comandos para otras distribuciones varían ligeramente (use `yum` para realizar la instalación en Red Hat Enterprise Linux y configurar las reglas de `selinux` adecuadas o use `zypper` para realizar la instalación en SUSE, por ejemplo).</span><span class="sxs-lookup"><span data-stu-id="827dd-118">Commands for other distributions vary slightly (use `yum` to install on Red Hat Enterprise Linux and configure appropriate `selinux` rules, or use `zypper` to install on SUSE, for example).</span></span>

<span data-ttu-id="827dd-119">Primero, SSH en la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="827dd-119">First, SSH to your VM.</span></span> <span data-ttu-id="827dd-120">El ejemplo siguiente se conecta a la máquina virtual denominada *myvm.westus.cloudapp.azure.com* con el nombre de usuario *azureuser*:</span><span class="sxs-lookup"><span data-stu-id="827dd-120">The following example connects to the VM named *myvm.westus.cloudapp.azure.com* with the username of *azureuser*:</span></span>

```bash
ssh azureuser@myvm.westus.cloudapp.azure.com
```

<span data-ttu-id="827dd-121">Si está utilizando Windows y necesita más información sobre el uso de SSH, consulte [Uso de claves SSH con Windows](ssh-from-windows.md).</span><span class="sxs-lookup"><span data-stu-id="827dd-121">If you are using Windows and need more information on using SSH, see [How to use SSH keys with Windows](ssh-from-windows.md).</span></span>

<span data-ttu-id="827dd-122">A continuación, instale xfce con `apt` como se indica a continuación:</span><span class="sxs-lookup"><span data-stu-id="827dd-122">Next, install xfce using `apt` as follows:</span></span>

```bash
sudo apt-get update
sudo apt-get install xfce4
```

## <a name="install-and-configure-a-remote-desktop-server"></a><span data-ttu-id="827dd-123">Instalar y configurar un servidor de escritorio remoto</span><span class="sxs-lookup"><span data-stu-id="827dd-123">Install and configure a remote desktop server</span></span>
<span data-ttu-id="827dd-124">Ahora que tiene instalado un entorno de escritorio, configure un servicio de escritorio remoto para escuchar las conexiones entrantes.</span><span class="sxs-lookup"><span data-stu-id="827dd-124">Now that you have a desktop environment installed, configure a remote desktop service to listen for incoming connections.</span></span> <span data-ttu-id="827dd-125">[xrdp](http://xrdp.org) es un servidor de protocolo de escritorio remoto (RDP) de código abierto que está disponible en la mayoría de las distribuciones de Linux y funciona bien con xfce.</span><span class="sxs-lookup"><span data-stu-id="827dd-125">[xrdp](http://xrdp.org) is an open source Remote Desktop Protocol (RDP) server that is available on most Linux distributions, and works well with xfce.</span></span> <span data-ttu-id="827dd-126">Instalar xrdp en la máquina virtual de Ubuntu de la siguiente forma:</span><span class="sxs-lookup"><span data-stu-id="827dd-126">Install xrdp on your Ubuntu VM as follows:</span></span>

```bash
sudo apt-get install xrdp
```

<span data-ttu-id="827dd-127">Indique a xrdp qué entorno de escritorio utilizar al iniciar la sesión.</span><span class="sxs-lookup"><span data-stu-id="827dd-127">Tell xrdp what desktop environment to use when you start your session.</span></span> <span data-ttu-id="827dd-128">Configure xrdp para usar xfce como el entorno de escritorio de la siguiente forma:</span><span class="sxs-lookup"><span data-stu-id="827dd-128">Configure xrdp to use xfce as your desktop environment as follows:</span></span>

```bash
echo xfce4-session >~/.xsession
```

<span data-ttu-id="827dd-129">Reinicie el servicio xrdp para que los cambios surtan efecto de la siguiente forma:</span><span class="sxs-lookup"><span data-stu-id="827dd-129">Restart the xrdp service for the changes to take effect as follows:</span></span>

```bash
sudo service xrdp restart
```


## <a name="set-a-local-user-account-password"></a><span data-ttu-id="827dd-130">Establecer una contraseña de cuenta de usuario</span><span class="sxs-lookup"><span data-stu-id="827dd-130">Set a local user account password</span></span>
<span data-ttu-id="827dd-131">Si ha creado una contraseña para su cuenta de usuario cuando se creó la máquina virtual, omita este paso.</span><span class="sxs-lookup"><span data-stu-id="827dd-131">If you created a password for your user account when you created your VM, skip this step.</span></span> <span data-ttu-id="827dd-132">Si solo usa la autenticación de clave SSH y no tiene una contraseña de cuenta local establecida, especifique una contraseña antes de utilizar xrdp para iniciar sesión en la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="827dd-132">If you only use SSH key authentication and do not have a local account password set, specify a password before you use xrdp to log in to your VM.</span></span> <span data-ttu-id="827dd-133">xrdp no puede aceptar las claves SSH para la autenticación.</span><span class="sxs-lookup"><span data-stu-id="827dd-133">xrdp cannot accept SSH keys for authentication.</span></span> <span data-ttu-id="827dd-134">En el ejemplo siguiente se especifica una contraseña para la cuenta de usuario *azureuser*:</span><span class="sxs-lookup"><span data-stu-id="827dd-134">The following example specifies a password for the user account *azureuser*:</span></span>

```bash
sudo passwd azureuser
```

> [!NOTE]
> <span data-ttu-id="827dd-135">Si especifica una contraseña, no se actualizará la configuración SSHD para permitir los inicios de sesión de contraseña si actualmente no es así.</span><span class="sxs-lookup"><span data-stu-id="827dd-135">Specifying a password does not update your SSHD configuration to permit password logins if it currently does not.</span></span> <span data-ttu-id="827dd-136">Desde la perspectiva de seguridad, puede que desee conectarse a la máquina virtual con un túnel SSH mediante la autenticación basada en claves y, a continuación, conectarse a xrdp.</span><span class="sxs-lookup"><span data-stu-id="827dd-136">From a security perspective, you may wish to connect to your VM with an SSH tunnel using key-based authentication and then connect to xrdp.</span></span> <span data-ttu-id="827dd-137">Si es así, omita el paso siguiente acerca de cómo crear una regla de grupo de seguridad de red para permitir el tráfico de escritorio remoto.</span><span class="sxs-lookup"><span data-stu-id="827dd-137">If so, skip the following step on creating a network security group rule to allow remote desktop traffic.</span></span>


## <a name="create-a-network-security-group-rule-for-remote-desktop-traffic"></a><span data-ttu-id="827dd-138">Crear una regla de grupo de seguridad de red para el tráfico de escritorio remoto</span><span class="sxs-lookup"><span data-stu-id="827dd-138">Create a Network Security Group rule for Remote Desktop traffic</span></span>
<span data-ttu-id="827dd-139">Para permitir que el tráfico de escritorio remoto llegue a la máquina virtual Linux, tiene que crearse una regla del grupo de seguridad de red que permita que el TCP del puerto 3389 llegue a la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="827dd-139">To allow Remote Desktop traffic to reach your Linux VM, a network security group rule needs to be created that allows TCP on port 3389 to reach your VM.</span></span> <span data-ttu-id="827dd-140">Para más información acerca de las reglas de grupos de seguridad de red, consulte [¿Qué es un grupo de seguridad de red?](../../virtual-network/virtual-networks-nsg.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)</span><span class="sxs-lookup"><span data-stu-id="827dd-140">For more information about network security group rules, see [What is a Network Security Group?](../../virtual-network/virtual-networks-nsg.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)</span></span> <span data-ttu-id="827dd-141">También puede [usar Azure Portal para crear una regla de grupos de seguridad de red](../windows/nsg-quickstart-portal.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="827dd-141">You can also [use the Azure portal to create a network security group rule](../windows/nsg-quickstart-portal.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

<span data-ttu-id="827dd-142">En los ejemplos siguientes se crea una regla de grupo de seguridad de red con [az network nsg rule create](/cli/azure/network/nsg/rule#create) denominada *myNetworkSecurityGroupRule* para *permitir* el tráfico en el puerto *tcp* *3389*.</span><span class="sxs-lookup"><span data-stu-id="827dd-142">The following examples create a network security group rule with [az network nsg rule create](/cli/azure/network/nsg/rule#create) named *myNetworkSecurityGroupRule* to *allow* traffic on *tcp* port *3389*.</span></span>

```azurecli
az network nsg rule create \
    --resource-group myResourceGroup \
    --nsg-name myNetworkSecurityGroup \
    --name myNetworkSecurityGroupRule \
    --protocol tcp \
    --priority 1010 \
    --destination-port-range 3389
```


## <a name="connect-your-linux-vm-with-a-remote-desktop-client"></a><span data-ttu-id="827dd-143">Conectar la máquina virtual Linux con un cliente de escritorio remoto</span><span class="sxs-lookup"><span data-stu-id="827dd-143">Connect your Linux VM with a Remote Desktop client</span></span>
<span data-ttu-id="827dd-144">Abra el cliente de escritorio remoto local y conéctese a la dirección IP o nombre DNS de la máquina virtual Linux.</span><span class="sxs-lookup"><span data-stu-id="827dd-144">Open your local remote desktop client and connect to the IP address or DNS name of your Linux VM.</span></span> <span data-ttu-id="827dd-145">Escriba el nombre de usuario y la contraseña para la cuenta de usuario en la máquina virtual como se indica a continuación:</span><span class="sxs-lookup"><span data-stu-id="827dd-145">Enter the username and password for the user account on your VM as follows:</span></span>

![Conectarse a xrdp mediante el cliente de escritorio remoto](./media/use-remote-desktop/remote-desktop-client.png)

<span data-ttu-id="827dd-147">Tras la autenticación, el entorno de escritorio de xfce se cargará y tendrá un aspecto similar al ejemplo siguiente:</span><span class="sxs-lookup"><span data-stu-id="827dd-147">After authenticating, the xfce desktop environment will load and look similar to the following example:</span></span>

![entorno de escritorio xfce a través de xrdp](./media/use-remote-desktop/xfce-desktop-environment.png)


## <a name="troubleshoot"></a><span data-ttu-id="827dd-149">Solución de problemas</span><span class="sxs-lookup"><span data-stu-id="827dd-149">Troubleshoot</span></span>
<span data-ttu-id="827dd-150">Si no se puede conectar a la máquina virtual de Linux con un cliente de escritorio remoto, use `netstat` en la máquina virtual Linux para comprobar que la máquina virtual está realizando escuchas para las conexiones RDP de la siguiente forma:</span><span class="sxs-lookup"><span data-stu-id="827dd-150">If you cannot connect to your Linux VM using a Remote Desktop client, use `netstat` on your Linux VM to verify that your VM is listening for RDP connections  as follows:</span></span>

```bash
sudo netstat -plnt | grep rdp
```

<span data-ttu-id="827dd-151">En el ejemplo siguiente se muestran las escuchas de la máquina virtual en el puerto TCP 3389 según lo esperado:</span><span class="sxs-lookup"><span data-stu-id="827dd-151">The following example shows the VM listening on TCP port 3389 as expected:</span></span>

```bash
tcp     0     0      127.0.0.1:3350     0.0.0.0:*     LISTEN     53192/xrdp-sesman
tcp     0     0      0.0.0.0:3389       0.0.0.0:*     LISTEN     53188/xrdp
```

<span data-ttu-id="827dd-152">Si el servicio xrdp no está escuchando, en una máquina virtual de Ubuntu, reinicie el servicio como se indica a continuación:</span><span class="sxs-lookup"><span data-stu-id="827dd-152">If the xrdp service is not listening, on an Ubuntu VM restart the service as follows:</span></span>

```bash
sudo service xrdp restart
```

<span data-ttu-id="827dd-153">Revise los registros en */var/log*Thug en la máquina virtual de Ubuntu para obtener indicaciones sobre el motivo por el que puede que el servicio no responda.</span><span class="sxs-lookup"><span data-stu-id="827dd-153">Review logs in */var/log*Thug  on your Ubuntu VM for indications as to why the service may not be responding.</span></span> <span data-ttu-id="827dd-154">También puede supervisar el registro del sistema durante un intento de conexión al escritorio remoto para ver los errores:</span><span class="sxs-lookup"><span data-stu-id="827dd-154">You can also monitor the syslog during a remote desktop connection attempt to view any errors:</span></span>

```bash
tail -f /var/log/syslog
```

<span data-ttu-id="827dd-155">Otras distribuciones de Linux como Red Hat Enterprise Linux y SUSE pueden tener diferentes maneras de reiniciar los servicios y alternar las ubicaciones de archivo de registro que revisar.</span><span class="sxs-lookup"><span data-stu-id="827dd-155">Other Linux distributions such as Red Hat Enterprise Linux and SUSE may have different ways to restart services and alternate log file locations to review.</span></span>

<span data-ttu-id="827dd-156">Si no recibe ninguna respuesta en el cliente de escritorio remoto y no ve todos los eventos de registro del sistema, este comportamiento indica que el tráfico de escritorio remoto no puede llegar a la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="827dd-156">If you do not receive any response in your remote desktop client and do not see any events in the system log, this behavior indicates that remote desktop traffic cannot reach the VM.</span></span> <span data-ttu-id="827dd-157">Revise las reglas de grupo de seguridad de red para asegurarse de que tiene una regla para permitir el TCP en el puerto 3389.</span><span class="sxs-lookup"><span data-stu-id="827dd-157">Review your network security group rules to ensure that you have a rule to permit TCP on port 3389.</span></span> <span data-ttu-id="827dd-158">Para obtener más información, consulte [Solucionar problemas de conectividad de la aplicación](../windows/troubleshoot-app-connection.md).</span><span class="sxs-lookup"><span data-stu-id="827dd-158">For more information, see [Troubleshoot application connectivity issues](../windows/troubleshoot-app-connection.md).</span></span>


## <a name="next-steps"></a><span data-ttu-id="827dd-159">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="827dd-159">Next steps</span></span>
<span data-ttu-id="827dd-160">Para obtener más información sobre cómo crear y utilizar claves de SSH con máquinas virtuales Linux, consulte [Crear claves SSH para máquinas virtuales de Linux en Azure](mac-create-ssh-keys.md).</span><span class="sxs-lookup"><span data-stu-id="827dd-160">For more information about creating and using SSH keys with Linux VMs, see [Create SSH keys for Linux VMs in Azure](mac-create-ssh-keys.md).</span></span>

<span data-ttu-id="827dd-161">Para obtener información sobre el uso de SSH de Windows, vea [Uso de claves SSH con Windows](ssh-from-windows.md).</span><span class="sxs-lookup"><span data-stu-id="827dd-161">For information on using SSH from Windows, see [How to use SSH keys with Windows](ssh-from-windows.md).</span></span>

