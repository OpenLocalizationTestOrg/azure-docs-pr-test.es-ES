---
title: "problemas de conexión de SSH de aaaTroubleshoot tooan máquina virtual de Azure | Documentos de Microsoft"
description: "¿Cómo tootroubleshoot problemas, como errores de conexión SSH o 'SSH rechazó la conexión' para una máquina virtual de Azure ejecutan Linux."
keywords: "conexión ssh rechazada, error de ssh azure ssh, error de conexión ssh"
services: virtual-machines-linux
documentationcenter: 
author: iainfoulds
manager: timlt
editor: 
tags: top-support-issue,azure-service-management,azure-resource-manager
ms.assetid: dcb82e19-29b2-47bb-99f2-900d4cfb5bbb
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 05/30/2017
ms.author: iainfou
ms.openlocfilehash: dfb4e75e571c8306edf5f300c4e0f07a5fe7750a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-ssh-connections-tooan-azure-linux-vm-that-fails-errors-out-or-is-refused"></a><span data-ttu-id="00b87-104">Solucionar problemas de SSH conexiones tooan VM de Linux de Azure que se produce un error, errores, o se rechaza</span><span class="sxs-lookup"><span data-stu-id="00b87-104">Troubleshoot SSH connections tooan Azure Linux VM that fails, errors out, or is refused</span></span>
<span data-ttu-id="00b87-105">Hay varias razones que se producen errores de Shell seguro (SSH), errores de conexión de SSH, o SSH se rechazó al tratar de máquina virtual de Linux de tooa tooconnect (VM).</span><span class="sxs-lookup"><span data-stu-id="00b87-105">There are various reasons that you encounter Secure Shell (SSH) errors, SSH connection failures, or SSH is refused when you try tooconnect tooa Linux virtual machine (VM).</span></span> <span data-ttu-id="00b87-106">En este artículo le ayuda a buscar y problemas de hello correcto.</span><span class="sxs-lookup"><span data-stu-id="00b87-106">This article helps you find and correct hello problems.</span></span> <span data-ttu-id="00b87-107">Puede usar hello portal de Azure, Azure CLI o extensión de acceso de máquina virtual para Linux tootroubleshoot y resolver problemas de conexión.</span><span class="sxs-lookup"><span data-stu-id="00b87-107">You can use hello Azure portal, Azure CLI, or VM Access Extension for Linux tootroubleshoot and resolve connection problems.</span></span>

[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-both-include.md)]

<span data-ttu-id="00b87-108">Si necesita más ayuda en cualquier momento en este artículo, puede ponerse en contacto con hello Azure expertos en [Hola foros de Azure de MSDN y el desbordamiento de la pila](http://azure.microsoft.com/support/forums/).</span><span class="sxs-lookup"><span data-stu-id="00b87-108">If you need more help at any point in this article, you can contact hello Azure experts on [hello MSDN Azure and Stack Overflow forums](http://azure.microsoft.com/support/forums/).</span></span> <span data-ttu-id="00b87-109">Como alternativa, puede registrar un incidente de soporte técnico de Azure.</span><span class="sxs-lookup"><span data-stu-id="00b87-109">Alternatively, you can file an Azure support incident.</span></span> <span data-ttu-id="00b87-110">Vaya toohello [sitio de soporte técnico de Azure](http://azure.microsoft.com/support/options/) y seleccione **obtener asistencia**.</span><span class="sxs-lookup"><span data-stu-id="00b87-110">Go toohello [Azure support site](http://azure.microsoft.com/support/options/) and select **Get support**.</span></span> <span data-ttu-id="00b87-111">Para obtener información acerca del uso de soporte técnico de Azure, lea hello [P+F de soporte de Microsoft Azure](http://azure.microsoft.com/support/faq/).</span><span class="sxs-lookup"><span data-stu-id="00b87-111">For information about using Azure Support, read hello [Microsoft Azure support FAQ](http://azure.microsoft.com/support/faq/).</span></span>

## <a name="quick-troubleshooting-steps"></a><span data-ttu-id="00b87-112">Pasos rápidos para solucionar problemas</span><span class="sxs-lookup"><span data-stu-id="00b87-112">Quick troubleshooting steps</span></span>
<span data-ttu-id="00b87-113">Después de cada paso de la solución de problemas, intente volver a conectarse toohello máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="00b87-113">After each troubleshooting step, try reconnecting toohello VM.</span></span>

1. <span data-ttu-id="00b87-114">Restablecer configuración de SSH de Hola.</span><span class="sxs-lookup"><span data-stu-id="00b87-114">Reset hello SSH configuration.</span></span>
2. <span data-ttu-id="00b87-115">Restablecer credenciales de hello para el usuario de Hola.</span><span class="sxs-lookup"><span data-stu-id="00b87-115">Reset hello credentials for hello user.</span></span>
3. <span data-ttu-id="00b87-116">Comprobar hello [grupo de seguridad de red](../../virtual-network/virtual-networks-nsg.md) reglas de permitan el tráfico SSH.</span><span class="sxs-lookup"><span data-stu-id="00b87-116">Verify hello [Network Security Group](../../virtual-network/virtual-networks-nsg.md) rules permit SSH traffic.</span></span>
   * <span data-ttu-id="00b87-117">Asegúrese de que el tráfico SSH toopermit existe una regla de grupo de seguridad de red (de forma predeterminada, el puerto TCP 22).</span><span class="sxs-lookup"><span data-stu-id="00b87-117">Ensure that a Network Security Group rule exists toopermit SSH traffic (by default, TCP port 22).</span></span>
   * <span data-ttu-id="00b87-118">No se puede usar el redireccionamiento o la asignación de puertos sin utilizar un equilibrador de carga de Azure.</span><span class="sxs-lookup"><span data-stu-id="00b87-118">You cannot use port redirection / mapping without using an Azure load balancer.</span></span>
4. <span data-ttu-id="00b87-119">Comprobar hello [mantenimiento de recursos de máquina virtual](../../resource-health/resource-health-overview.md).</span><span class="sxs-lookup"><span data-stu-id="00b87-119">Check hello [VM resource health](../../resource-health/resource-health-overview.md).</span></span> 
   * <span data-ttu-id="00b87-120">Asegúrese de que Hola VM informes como correcto.</span><span class="sxs-lookup"><span data-stu-id="00b87-120">Ensure that hello VM reports as being healthy.</span></span>
   * <span data-ttu-id="00b87-121">Si tiene habilitado el diagnóstico de arranque, compruebe Hola VM no informa de errores de arranque en los registros de Hola.</span><span class="sxs-lookup"><span data-stu-id="00b87-121">If you have boot diagnostics enabled, verify hello VM is not reporting boot errors in hello logs.</span></span>
5. <span data-ttu-id="00b87-122">Reinicie Hola máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="00b87-122">Restart hello VM.</span></span>
6. <span data-ttu-id="00b87-123">Volver a implementar Hola máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="00b87-123">Redeploy hello VM.</span></span>

<span data-ttu-id="00b87-124">Siga leyendo para conocer pasos y soluciones más detallados de solución de problemas.</span><span class="sxs-lookup"><span data-stu-id="00b87-124">Continue reading for more detailed troubleshooting steps and explanations.</span></span>

## <a name="available-methods-tootroubleshoot-ssh-connection-issues"></a><span data-ttu-id="00b87-125">Problemas de conexión de métodos disponibles tootroubleshoot SSH</span><span class="sxs-lookup"><span data-stu-id="00b87-125">Available methods tootroubleshoot SSH connection issues</span></span>
<span data-ttu-id="00b87-126">Puede restablecer las credenciales o la configuración de SSH mediante uno de los siguientes métodos de hello:</span><span class="sxs-lookup"><span data-stu-id="00b87-126">You can reset credentials or SSH configuration using one of hello following methods:</span></span>

* <span data-ttu-id="00b87-127">[Portal de Azure](#use-the-azure-portal) : great si necesita tooquickly restablece configuración de SSH de Hola o la clave SSH y no haya Hola instaladas herramientas de Azure.</span><span class="sxs-lookup"><span data-stu-id="00b87-127">[Azure portal](#use-the-azure-portal) - great if you need tooquickly reset hello SSH configuration or SSH key and you don't have hello Azure tools installed.</span></span>
* <span data-ttu-id="00b87-128">[Azure 2.0 CLI](#use-the-azure-cli-20) : si ya está en línea de comandos de hello rápidamente restablecer la configuración de SSH de Hola o las credenciales.</span><span class="sxs-lookup"><span data-stu-id="00b87-128">[Azure CLI 2.0](#use-the-azure-cli-20) - if you are already on hello command line, quickly reset hello SSH configuration or credentials.</span></span> <span data-ttu-id="00b87-129">También puede usar hello [1.0 de CLI de Azure](#use-the-azure-cli-10)</span><span class="sxs-lookup"><span data-stu-id="00b87-129">You can also use hello [Azure CLI 1.0](#use-the-azure-cli-10)</span></span>
* <span data-ttu-id="00b87-130">[Extensión VMAccessForLinux Azure](#use-the-vmaccess-extension) : crear y volver a json definición archivos tooreset Hola SSH configuración o credenciales de usuario.</span><span class="sxs-lookup"><span data-stu-id="00b87-130">[Azure VMAccessForLinux extension](#use-the-vmaccess-extension) - create and reuse json definition files tooreset hello SSH configuration or user credentials.</span></span>

<span data-ttu-id="00b87-131">Después de cada paso de la solución de problemas, intente conectarse de nuevo tooyour máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="00b87-131">After each troubleshooting step, try connecting tooyour VM again.</span></span> <span data-ttu-id="00b87-132">Si sigue sin poder conectarse, pruebe el paso siguiente Hola.</span><span class="sxs-lookup"><span data-stu-id="00b87-132">If you still cannot connect, try hello next step.</span></span>

## <a name="use-hello-azure-portal"></a><span data-ttu-id="00b87-133">Usar hello portal de Azure</span><span class="sxs-lookup"><span data-stu-id="00b87-133">Use hello Azure portal</span></span>
<span data-ttu-id="00b87-134">Hola portal de Azure proporciona un hello tooreset de forma rápida las credenciales de usuario o configuración de SSH sin necesidad de instalar las herramientas en el equipo local.</span><span class="sxs-lookup"><span data-stu-id="00b87-134">hello Azure portal provides a quick way tooreset hello SSH configuration or user credentials without installing any tools on your local computer.</span></span>

<span data-ttu-id="00b87-135">Seleccione la máquina virtual en hello portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="00b87-135">Select your VM in hello Azure portal.</span></span> <span data-ttu-id="00b87-136">Desplácese hacia abajo toohello **soporte técnico y solución de problemas** sección y seleccione **de restablecimiento de contraseña** como en el siguiente ejemplo de Hola:</span><span class="sxs-lookup"><span data-stu-id="00b87-136">Scroll down toohello **Support + Troubleshooting** section and select **Reset password** as in hello following example:</span></span>

![Restablecer la configuración de SSH o credenciales de hello portal de Azure](./media/troubleshoot-ssh-connection/reset-credentials-using-portal.png)

### <a name="reset-hello-ssh-configuration"></a><span data-ttu-id="00b87-138">Restablecer configuración de SSH Hola</span><span class="sxs-lookup"><span data-stu-id="00b87-138">Reset hello SSH configuration</span></span>
<span data-ttu-id="00b87-139">Como primer paso, seleccione `Reset configuration only` de hello **modo** menú desplegable como en hello anterior captura de pantalla, a continuación, haga clic en hello **restablecer** botón.</span><span class="sxs-lookup"><span data-stu-id="00b87-139">As a first step, select `Reset configuration only` from hello **Mode** drop-down menu as in hello preceding screenshot, then click hello **Reset** button.</span></span> <span data-ttu-id="00b87-140">Una vez completada esta acción, tooaccess la máquina virtual vuelva a intentarlo.</span><span class="sxs-lookup"><span data-stu-id="00b87-140">Once this action has completed, try tooaccess your VM again.</span></span>

### <a name="reset-ssh-credentials-for-a-user"></a><span data-ttu-id="00b87-141">Restablecimiento de las credenciales de SSH de un usuario</span><span class="sxs-lookup"><span data-stu-id="00b87-141">Reset SSH credentials for a user</span></span>
<span data-ttu-id="00b87-142">las credenciales de hello tooreset de un usuario existente, seleccione `Reset SSH public key` o `Reset password` de hello **modo** Hola anterior captura de pantalla en el menú desplegable.</span><span class="sxs-lookup"><span data-stu-id="00b87-142">tooreset hello credentials of an existing user, select either `Reset SSH public key` or `Reset password` from hello **Mode** drop-down menu as in hello preceding screenshot.</span></span> <span data-ttu-id="00b87-143">Especifique el nombre de usuario de hello y una clave SSH o una nueva contraseña, haga clic en hello **restablecer** botón.</span><span class="sxs-lookup"><span data-stu-id="00b87-143">Specify hello username and an SSH key or new password, then click hello **Reset** button.</span></span>

<span data-ttu-id="00b87-144">También puede crear un usuario con privilegios de sudo en hello VM desde este menú.</span><span class="sxs-lookup"><span data-stu-id="00b87-144">You can also create a user with sudo privileges on hello VM from this menu.</span></span> <span data-ttu-id="00b87-145">Escriba un nuevo nombre de usuario y la contraseña asociada o la clave SSH y, a continuación, haga clic en hello **restablecer** botón.</span><span class="sxs-lookup"><span data-stu-id="00b87-145">Enter a new username and associated password or SSH key, and then click hello **Reset** button.</span></span>

## <a name="use-hello-azure-cli-20"></a><span data-ttu-id="00b87-146">Usar hello 2.0 de CLI de Azure</span><span class="sxs-lookup"><span data-stu-id="00b87-146">Use hello Azure CLI 2.0</span></span>
<span data-ttu-id="00b87-147">Si no lo ha hecho ya, instale hello más reciente [CLI de Azure 2.0](/cli/azure/install-az-cli2) e inicie sesión con cuenta de Azure de tooan [inicio de sesión de az](/cli/azure/#login).</span><span class="sxs-lookup"><span data-stu-id="00b87-147">If you haven't already, install hello latest [Azure CLI 2.0](/cli/azure/install-az-cli2) and log in tooan Azure account using [az login](/cli/azure/#login).</span></span>

<span data-ttu-id="00b87-148">Si ha creado y cargado una imagen de disco Linux personalizada, que seguro Hola [agente Linux de Microsoft Azure](../windows/agent-user-guide.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) versión 2.0.5 o posterior está instalado.</span><span class="sxs-lookup"><span data-stu-id="00b87-148">If you created and uploaded a custom Linux disk image, make sure hello [Microsoft Azure Linux Agent](../windows/agent-user-guide.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) version 2.0.5 or later is installed.</span></span> <span data-ttu-id="00b87-149">Para máquinas virtuales creadas mediante imágenes de la galería, esta extensión de acceso ya está instalada y configurada automáticamente.</span><span class="sxs-lookup"><span data-stu-id="00b87-149">For VMs created using Gallery images, this access extension is already installed and configured for you.</span></span>

### <a name="reset-ssh-configuration"></a><span data-ttu-id="00b87-150">Restablecer la configuración de SSH</span><span class="sxs-lookup"><span data-stu-id="00b87-150">Reset SSH configuration</span></span>
<span data-ttu-id="00b87-151">Puede inicialmente try restableciendo Hola SSH toodefault los valores de configuración y el servidor SSH de hello reiniciándose en hello máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="00b87-151">You can initially try resetting hello SSH configuration toodefault values and rebooting hello SSH server on hello VM.</span></span> <span data-ttu-id="00b87-152">Tenga en cuenta que esto no cambia nombre de cuenta de usuario de hello, contraseñas o claves de SSH.</span><span class="sxs-lookup"><span data-stu-id="00b87-152">Note that this does not change hello user account name, password, or SSH keys.</span></span>
<span data-ttu-id="00b87-153">Hello siguiente ejemplo se utiliza [az vm usuario restablecer-ssh](/cli/azure/vm/user#reset-ssh) tooreset configuración de SSH de hello en máquina virtual denominada hello `myVM` en `myResourceGroup`.</span><span class="sxs-lookup"><span data-stu-id="00b87-153">hello following example uses [az vm user reset-ssh](/cli/azure/vm/user#reset-ssh) tooreset hello SSH configuration on hello VM named `myVM` in `myResourceGroup`.</span></span> <span data-ttu-id="00b87-154">Use sus propios valores, como se indica a continuación:</span><span class="sxs-lookup"><span data-stu-id="00b87-154">Use your own values as follows:</span></span>

```azurecli
az vm user reset-ssh --resource-group myResourceGroup --name myVM
```

### <a name="reset-ssh-credentials-for-a-user"></a><span data-ttu-id="00b87-155">Restablecimiento de las credenciales de SSH de un usuario</span><span class="sxs-lookup"><span data-stu-id="00b87-155">Reset SSH credentials for a user</span></span>
<span data-ttu-id="00b87-156">Hello siguiente ejemplo se utiliza [actualización de usuario de vm az](/cli/azure/vm/user#update) tooreset hello las credenciales para `myUsername` valor toohello especificado en `myPassword`, en la máquina virtual denominada hello `myVM` en `myResourceGroup`.</span><span class="sxs-lookup"><span data-stu-id="00b87-156">hello following example uses [az vm user update](/cli/azure/vm/user#update) tooreset hello credentials for `myUsername` toohello value specified in `myPassword`, on hello VM named `myVM` in `myResourceGroup`.</span></span> <span data-ttu-id="00b87-157">Use sus propios valores, como se indica a continuación:</span><span class="sxs-lookup"><span data-stu-id="00b87-157">Use your own values as follows:</span></span>

```azurecli
az vm user update --resource-group myResourceGroup --name myVM \
     --username myUsername --password myPassword
```

<span data-ttu-id="00b87-158">Si utiliza la autenticación de clave SSH, puede restablecer la clave SSH de Hola para un usuario determinado.</span><span class="sxs-lookup"><span data-stu-id="00b87-158">If using SSH key authentication, you can reset hello SSH key for a given user.</span></span> <span data-ttu-id="00b87-159">Hello siguiente ejemplo se utiliza **az vm acceder a usuario de linux de conjunto** tooupdate Hola SSH clave almacenada en `~/.ssh/id_rsa.pub` con el nombre de usuario de hello `myUsername`, en hello máquina virtual denominada `myVM` en `myResourceGroup`.</span><span class="sxs-lookup"><span data-stu-id="00b87-159">hello following example uses **az vm access set-linux-user** tooupdate hello SSH key stored in `~/.ssh/id_rsa.pub` for hello user named `myUsername`, on hello VM named `myVM` in `myResourceGroup`.</span></span> <span data-ttu-id="00b87-160">Use sus propios valores, como se indica a continuación:</span><span class="sxs-lookup"><span data-stu-id="00b87-160">Use your own values as follows:</span></span>

```azurecli
az vm user update --resource-group myResourceGroup --name myVM \
    --username myUsername --ssh-key-value ~/.ssh/id_rsa.pub
```

## <a name="use-hello-vmaccess-extension"></a><span data-ttu-id="00b87-161">Use la extensión VMAccess Hola</span><span class="sxs-lookup"><span data-stu-id="00b87-161">Use hello VMAccess extension</span></span>
<span data-ttu-id="00b87-162">Hola extensión de acceso de máquina virtual para Linux se lee en un archivo json que define acciones toocarry out. Estas acciones incluyen el restablecimiento de SSHD o de una clave SSH o la adición de un usuario.</span><span class="sxs-lookup"><span data-stu-id="00b87-162">hello VM Access Extension for Linux reads in a json file that defines actions toocarry out. These actions include resetting SSHD, resetting an SSH key, or adding a user.</span></span> <span data-ttu-id="00b87-163">Seguir usando toocall Hola extensión VMAccess de hello CLI de Azure, pero pueda reutilizar archivos json de hello en varias máquinas virtuales si lo desea.</span><span class="sxs-lookup"><span data-stu-id="00b87-163">You still use hello Azure CLI toocall hello VMAccess extension, but you can reuse hello json files across multiple VMs if desired.</span></span> <span data-ttu-id="00b87-164">Este enfoque permite toocreate un repositorio de archivos json que, a continuación, se pueden llamar para especificado escenarios.</span><span class="sxs-lookup"><span data-stu-id="00b87-164">This approach allows you toocreate a repository of json files that can then be called for given scenarios.</span></span>

### <a name="reset-sshd"></a><span data-ttu-id="00b87-165">Restablecer SSHD</span><span class="sxs-lookup"><span data-stu-id="00b87-165">Reset SSHD</span></span>
<span data-ttu-id="00b87-166">Cree un archivo denominado `settings.json` con hello siguen contenido:</span><span class="sxs-lookup"><span data-stu-id="00b87-166">Create a file named `settings.json` with hello following content:</span></span>

```json
{  
    "reset_ssh":"True"
}
```

<span data-ttu-id="00b87-167">Con hello CLI de Azure,, a continuación, llame a hello `VMAccessForLinux` extensión tooreset su conexión SSHD especificando el archivo json.</span><span class="sxs-lookup"><span data-stu-id="00b87-167">Using hello Azure CLI, you then call hello `VMAccessForLinux` extension tooreset your SSHD connection by specifying your json file.</span></span> <span data-ttu-id="00b87-168">Hello siguiente ejemplo se utiliza [conjunto de extensión de vm az](/cli/azure/vm/extension#set) tooreset SSHD en máquina virtual denominada hello `myVM` en `myResourceGroup`.</span><span class="sxs-lookup"><span data-stu-id="00b87-168">hello following example uses [az vm extension set](/cli/azure/vm/extension#set) tooreset SSHD on hello VM named `myVM` in `myResourceGroup`.</span></span> <span data-ttu-id="00b87-169">Use sus propios valores, como se indica a continuación:</span><span class="sxs-lookup"><span data-stu-id="00b87-169">Use your own values as follows:</span></span>

```azurecli
az vm extension set --resource-group philmea --vm-name Ubuntu \
    --name VMAccessForLinux --publisher Microsoft.OSTCExtensions --version 1.2 --settings settings.json
```

### <a name="reset-ssh-credentials-for-a-user"></a><span data-ttu-id="00b87-170">Restablecimiento de las credenciales de SSH de un usuario</span><span class="sxs-lookup"><span data-stu-id="00b87-170">Reset SSH credentials for a user</span></span>
<span data-ttu-id="00b87-171">Si SSHD aparece toofunction correctamente, puede restablecer las credenciales de Hola para un usuario giver.</span><span class="sxs-lookup"><span data-stu-id="00b87-171">If SSHD appears toofunction correctly, you can reset hello credentials for a giver user.</span></span> <span data-ttu-id="00b87-172">contraseña de hello tooreset para un usuario, cree un archivo denominado `settings.json`.</span><span class="sxs-lookup"><span data-stu-id="00b87-172">tooreset hello password for a user, create a file named `settings.json`.</span></span> <span data-ttu-id="00b87-173">Hello en el ejemplo siguiente se restablece las credenciales de Hola para `myUsername` valor toohello especificado en `myPassword`.</span><span class="sxs-lookup"><span data-stu-id="00b87-173">hello following example resets hello credentials for `myUsername` toohello value specified in `myPassword`.</span></span> <span data-ttu-id="00b87-174">Escriba Hola siguiendo las líneas en la `settings.json` de archivos, con sus propios valores:</span><span class="sxs-lookup"><span data-stu-id="00b87-174">Enter hello following lines into your `settings.json` file, using your own values:</span></span>

```json
{
    "username":"myUsername", "password":"myPassword"
}
```

<span data-ttu-id="00b87-175">O tooreset Hola clave SSH para un usuario, primero cree un archivo denominado `settings.json`.</span><span class="sxs-lookup"><span data-stu-id="00b87-175">Or tooreset hello SSH key for a user, first create a file named `settings.json`.</span></span> <span data-ttu-id="00b87-176">Hello en el ejemplo siguiente se restablece las credenciales de Hola para `myUsername` valor toohello especificado en `myPassword`, en la máquina virtual denominada hello `myVM` en `myResourceGroup`.</span><span class="sxs-lookup"><span data-stu-id="00b87-176">hello following example resets hello credentials for `myUsername` toohello value specified in `myPassword`, on hello VM named `myVM` in `myResourceGroup`.</span></span> <span data-ttu-id="00b87-177">Escriba Hola siguiendo las líneas en la `settings.json` de archivos, con sus propios valores:</span><span class="sxs-lookup"><span data-stu-id="00b87-177">Enter hello following lines into your `settings.json` file, using your own values:</span></span>

```json
{
    "username":"myUsername", "ssh_key":"mySSHKey"
}
```

<span data-ttu-id="00b87-178">Después de crear el archivo json, usar Hola de hello Azure CLI toocall `VMAccessForLinux` tooreset extensión las credenciales de su usuario SSH especificando el archivo json.</span><span class="sxs-lookup"><span data-stu-id="00b87-178">After creating your json file, use hello Azure CLI toocall hello `VMAccessForLinux` extension tooreset your SSH user credentials by specifying your json file.</span></span> <span data-ttu-id="00b87-179">Hello en el ejemplo siguiente se restablece las credenciales en la máquina virtual denominada hello `myVM` en `myResourceGroup`.</span><span class="sxs-lookup"><span data-stu-id="00b87-179">hello following example resets credentials on hello VM named `myVM` in `myResourceGroup`.</span></span> <span data-ttu-id="00b87-180">Use sus propios valores, como se indica a continuación:</span><span class="sxs-lookup"><span data-stu-id="00b87-180">Use your own values as follows:</span></span>

```azurecli
az vm extension set --resource-group philmea --vm-name Ubuntu \
    --name VMAccessForLinux --publisher Microsoft.OSTCExtensions --version 1.2 --settings settings.json
```

## <a name="use-hello-azure-cli-10"></a><span data-ttu-id="00b87-181">Usar hello Azure CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="00b87-181">Use hello Azure CLI 1.0</span></span>
<span data-ttu-id="00b87-182">Si no lo ha hecho ya, [instalar Hola 1.0 de CLI de Azure y conectar tooyour suscripción de Azure](../../cli-install-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="00b87-182">If you haven't already, [install hello Azure CLI 1.0 and connect tooyour Azure subscription](../../cli-install-nodejs.md).</span></span> <span data-ttu-id="00b87-183">Asegúrese de que está usando el modo de Resource Manager como se indica:</span><span class="sxs-lookup"><span data-stu-id="00b87-183">Make sure that you are using Resource Manager mode as follows:</span></span>

```azurecli
azure config mode arm
```

<span data-ttu-id="00b87-184">Si ha creado y cargado una imagen de disco Linux personalizada, que seguro Hola [agente Linux de Microsoft Azure](../windows/agent-user-guide.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) versión 2.0.5 o posterior está instalado.</span><span class="sxs-lookup"><span data-stu-id="00b87-184">If you created and uploaded a custom Linux disk image, make sure hello [Microsoft Azure Linux Agent](../windows/agent-user-guide.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) version 2.0.5 or later is installed.</span></span> <span data-ttu-id="00b87-185">Para máquinas virtuales creadas mediante imágenes de la galería, esta extensión de acceso ya está instalada y configurada automáticamente.</span><span class="sxs-lookup"><span data-stu-id="00b87-185">For VMs created using Gallery images, this access extension is already installed and configured for you.</span></span>

### <a name="reset-ssh-configuration"></a><span data-ttu-id="00b87-186">Restablecer la configuración de SSH</span><span class="sxs-lookup"><span data-stu-id="00b87-186">Reset SSH configuration</span></span>
<span data-ttu-id="00b87-187">configuración SSHD Hello en sí puede estar mal configurada u Hola servicio detectó un error.</span><span class="sxs-lookup"><span data-stu-id="00b87-187">hello SSHD configuration itself may be misconfigured or hello service encountered an error.</span></span> <span data-ttu-id="00b87-188">Puede restablecer SSHD toomake seguro de configuración de SSH Hola sí es válida.</span><span class="sxs-lookup"><span data-stu-id="00b87-188">You can reset SSHD toomake sure hello SSH configuration itself is valid.</span></span> <span data-ttu-id="00b87-189">Restablecer SSHD debe ser Hola primer paso para solucionarlos que realizar.</span><span class="sxs-lookup"><span data-stu-id="00b87-189">Resetting SSHD should be hello first troubleshooting step you take.</span></span>

<span data-ttu-id="00b87-190">Hello en el ejemplo siguiente se restablece SSHD en una máquina virtual denominada `myVM` en grupo de recursos de hello llamado `myResourceGroup`.</span><span class="sxs-lookup"><span data-stu-id="00b87-190">hello following example resets SSHD on a VM named `myVM` in hello resource group named `myResourceGroup`.</span></span> <span data-ttu-id="00b87-191">Use sus propios nombres de grupo de recursos y máquina virtual, como se indica a continuación:</span><span class="sxs-lookup"><span data-stu-id="00b87-191">Use your own VM and resource group names as follows:</span></span>

```azurecli
azure vm reset-access --resource-group myResourceGroup --name myVM \
    --reset-ssh
```

### <a name="reset-ssh-credentials-for-a-user"></a><span data-ttu-id="00b87-192">Restablecimiento de las credenciales de SSH de un usuario</span><span class="sxs-lookup"><span data-stu-id="00b87-192">Reset SSH credentials for a user</span></span>
<span data-ttu-id="00b87-193">Si SSHD aparece toofunction correctamente, puede restablecer contraseña de Hola para un usuario giver.</span><span class="sxs-lookup"><span data-stu-id="00b87-193">If SSHD appears toofunction correctly, you can reset hello password for a giver user.</span></span> <span data-ttu-id="00b87-194">Hello en el ejemplo siguiente se restablece las credenciales de Hola para `myUsername` valor toohello especificado en `myPassword`, en la máquina virtual denominada hello `myVM` en `myResourceGroup`.</span><span class="sxs-lookup"><span data-stu-id="00b87-194">hello following example resets hello credentials for `myUsername` toohello value specified in `myPassword`, on hello VM named `myVM` in `myResourceGroup`.</span></span> <span data-ttu-id="00b87-195">Use sus propios valores, como se indica a continuación:</span><span class="sxs-lookup"><span data-stu-id="00b87-195">Use your own values as follows:</span></span>

```azurecli
azure vm reset-access --resource-group myResourceGroup --name myVM \
     --user-name myUsername --password myPassword
```

<span data-ttu-id="00b87-196">Si utiliza la autenticación de clave SSH, puede restablecer la clave SSH de Hola para un usuario determinado.</span><span class="sxs-lookup"><span data-stu-id="00b87-196">If using SSH key authentication, you can reset hello SSH key for a given user.</span></span> <span data-ttu-id="00b87-197">Después de las actualizaciones de ejemplo de Hola Hola almacenada en la clave SSH `~/.ssh/id_rsa.pub` con el nombre de usuario de hello `myUsername`, en la máquina virtual denominada hello `myVM` en `myResourceGroup`.</span><span class="sxs-lookup"><span data-stu-id="00b87-197">hello following example updates hello SSH key stored in `~/.ssh/id_rsa.pub` for hello user named `myUsername`, on hello VM named `myVM` in `myResourceGroup`.</span></span> <span data-ttu-id="00b87-198">Use sus propios valores, como se indica a continuación:</span><span class="sxs-lookup"><span data-stu-id="00b87-198">Use your own values as follows:</span></span>

```azurecli
azure vm reset-access --resource-group myResourceGroup --name myVM \
    --user-name myUsername --ssh-key-file ~/.ssh/id_rsa.pub
```


## <a name="restart-a-vm"></a><span data-ttu-id="00b87-199">Reinicio de una máquina virtual</span><span class="sxs-lookup"><span data-stu-id="00b87-199">Restart a VM</span></span>
<span data-ttu-id="00b87-200">Si dispone de restablecer credenciales de usuario y la configuración de SSH de Hola o encontró un error al hacerlo, puede intentar reiniciar Hola VM tooaddress subyacente problemas de cálculo.</span><span class="sxs-lookup"><span data-stu-id="00b87-200">If you have reset hello SSH configuration and user credentials, or encountered an error in doing so, you can try restarting hello VM tooaddress underlying compute issues.</span></span>

### <a name="azure-portal"></a><span data-ttu-id="00b87-201">Azure Portal</span><span class="sxs-lookup"><span data-stu-id="00b87-201">Azure portal</span></span>
<span data-ttu-id="00b87-202">toorestart una VM con hello Azure seleccione portal, el Hola de máquina virtual y haga clic en **reiniciar** botón como en el siguiente ejemplo de Hola:</span><span class="sxs-lookup"><span data-stu-id="00b87-202">toorestart a VM using hello Azure portal, select your VM and click hello **Restart** button as in hello following example:</span></span>

![Reiniciar una máquina virtual en hello portal de Azure](./media/troubleshoot-ssh-connection/restart-vm-using-portal.png)

### <a name="azure-cli-10"></a><span data-ttu-id="00b87-204">CLI de Azure 1.0</span><span class="sxs-lookup"><span data-stu-id="00b87-204">Azure CLI 1.0</span></span>
<span data-ttu-id="00b87-205">Después de reinicios del ejemplo de Hola Hola máquina virtual denominada `myVM` en grupo de recursos de hello llamado `myResourceGroup`.</span><span class="sxs-lookup"><span data-stu-id="00b87-205">hello following example restarts hello VM named `myVM` in hello resource group named `myResourceGroup`.</span></span> <span data-ttu-id="00b87-206">Use sus propios valores, como se indica a continuación:</span><span class="sxs-lookup"><span data-stu-id="00b87-206">Use your own values as follows:</span></span>

```azurecli
azure vm restart --resource-group myResourceGroup --name myVM
```

### <a name="azure-cli-20"></a><span data-ttu-id="00b87-207">CLI de Azure 2.0</span><span class="sxs-lookup"><span data-stu-id="00b87-207">Azure CLI 2.0</span></span>
<span data-ttu-id="00b87-208">Hello siguiente ejemplo se utiliza [reinicio de la máquina virtual de az](/cli/azure/vm#restart) toorestart Hola máquina virtual denominada `myVM` en grupo de recursos de hello llamado `myResourceGroup`.</span><span class="sxs-lookup"><span data-stu-id="00b87-208">hello following example uses [az vm restart](/cli/azure/vm#restart) toorestart hello VM named `myVM` in hello resource group named `myResourceGroup`.</span></span> <span data-ttu-id="00b87-209">Use sus propios valores, como se indica a continuación:</span><span class="sxs-lookup"><span data-stu-id="00b87-209">Use your own values as follows:</span></span>

```azurecli
az vm restart --resource-group myResourceGroup --name myVM
```


## <a name="redeploy-a-vm"></a><span data-ttu-id="00b87-210">Reimplementación de una máquina virtual</span><span class="sxs-lookup"><span data-stu-id="00b87-210">Redeploy a VM</span></span>
<span data-ttu-id="00b87-211">Puede volver a implementar un nodo de tooanother de máquina virtual dentro de Azure, que puede corregir los problemas de red subyacentes.</span><span class="sxs-lookup"><span data-stu-id="00b87-211">You can redeploy a VM tooanother node within Azure, which may correct any underlying networking issues.</span></span> <span data-ttu-id="00b87-212">Para obtener información acerca de cómo volver a implementar una máquina virtual, consulte [volver a implementar la máquina virtual toonew nodo Azure](../windows/redeploy-to-new-node.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="00b87-212">For information about redeploying a VM, see [Redeploy virtual machine toonew Azure node](../windows/redeploy-to-new-node.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

> [!NOTE]
> <span data-ttu-id="00b87-213">Una vez finalizada esta operación, se perderán los datos de disco efímeros y direcciones IP dinámicas que están asociadas a la máquina virtual de Hola se actualizará.</span><span class="sxs-lookup"><span data-stu-id="00b87-213">After this operation finishes, ephemeral disk data will be lost and dynamic IP addresses that are associated with hello virtual machine will be updated.</span></span>
> 
> 

### <a name="azure-portal"></a><span data-ttu-id="00b87-214">Azure Portal</span><span class="sxs-lookup"><span data-stu-id="00b87-214">Azure portal</span></span>
<span data-ttu-id="00b87-215">tooredeploy una VM con hello Azure seleccione portal, la máquina virtual y desplácese hacia abajo toohello **soporte técnico y solución de problemas** sección.</span><span class="sxs-lookup"><span data-stu-id="00b87-215">tooredeploy a VM using hello Azure portal, select your VM and scroll down toohello **Support + Troubleshooting** section.</span></span> <span data-ttu-id="00b87-216">Haga clic en hello **volver a implementar** botón como en el siguiente ejemplo de Hola:</span><span class="sxs-lookup"><span data-stu-id="00b87-216">Click hello **Redeploy** button as in hello following example:</span></span>

![Volver a implementar una máquina virtual en hello portal de Azure](./media/troubleshoot-ssh-connection/redeploy-vm-using-portal.png)

### <a name="azure-cli-10"></a><span data-ttu-id="00b87-218">CLI de Azure 1.0</span><span class="sxs-lookup"><span data-stu-id="00b87-218">Azure CLI 1.0</span></span>
<span data-ttu-id="00b87-219">Después de nuevas implementaciones de ejemplo de Hola Hola máquina virtual denominada `myVM` en grupo de recursos de hello llamado `myResourceGroup`.</span><span class="sxs-lookup"><span data-stu-id="00b87-219">hello following example redeploys hello VM named `myVM` in hello resource group named `myResourceGroup`.</span></span> <span data-ttu-id="00b87-220">Use sus propios valores, como se indica a continuación:</span><span class="sxs-lookup"><span data-stu-id="00b87-220">Use your own values as follows:</span></span>

```azurecli
azure vm redeploy --resource-group myResourceGroup --name myVM
```

### <a name="azure-cli-20"></a><span data-ttu-id="00b87-221">CLI de Azure 2.0</span><span class="sxs-lookup"><span data-stu-id="00b87-221">Azure CLI 2.0</span></span>
<span data-ttu-id="00b87-222">Hola después de ejemplo de uso [volver a implementar vm de az](/cli/azure/vm#redeploy) tooredeploy Hola máquina virtual denominada `myVM` en grupo de recursos de hello llamado `myResourceGroup`.</span><span class="sxs-lookup"><span data-stu-id="00b87-222">hello following example use [az vm redeploy](/cli/azure/vm#redeploy) tooredeploy hello VM named `myVM` in hello resource group named `myResourceGroup`.</span></span> <span data-ttu-id="00b87-223">Use sus propios valores, como se indica a continuación:</span><span class="sxs-lookup"><span data-stu-id="00b87-223">Use your own values as follows:</span></span>

```azurecli
az vm redeploy --resource-group myResourceGroup --name myVM
```

## <a name="vms-created-by-using-hello-classic-deployment-model"></a><span data-ttu-id="00b87-224">Máquinas virtuales creadas con el modelo de implementación de hello clásico</span><span class="sxs-lookup"><span data-stu-id="00b87-224">VMs created by using hello Classic deployment model</span></span>
<span data-ttu-id="00b87-225">Probar estos pasos tooresolve hello más comunes SSH errores de conexión para las máquinas virtuales que se crearon con el modelo de implementación clásica de Hola.</span><span class="sxs-lookup"><span data-stu-id="00b87-225">Try these steps tooresolve hello most common SSH connection failures for VMs that were created by using hello classic deployment model.</span></span> <span data-ttu-id="00b87-226">Después de cada paso, intente volver a conectarse toohello máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="00b87-226">After each step, try reconnecting toohello VM.</span></span>

* <span data-ttu-id="00b87-227">Restablecer el acceso remoto de hello [portal de Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="00b87-227">Reset remote access from hello [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="00b87-228">En Hola portal de Azure, seleccione la máquina virtual y haga clic en hello **restablecer remoto...**  botón.</span><span class="sxs-lookup"><span data-stu-id="00b87-228">On hello Azure portal, select your VM and click hello **Reset Remote...** button.</span></span>
* <span data-ttu-id="00b87-229">Reinicie Hola máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="00b87-229">Restart hello VM.</span></span> <span data-ttu-id="00b87-230">En hello [portal de Azure](https://portal.azure.com), seleccione la máquina virtual y haga clic en hello **reiniciar** botón.</span><span class="sxs-lookup"><span data-stu-id="00b87-230">On hello [Azure portal](https://portal.azure.com), select your VM and click hello **Restart** button.</span></span>
    
* <span data-ttu-id="00b87-231">Volver a implementar nodos de Azure nuevo tooa Hola máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="00b87-231">Redeploy hello VM tooa new Azure node.</span></span> <span data-ttu-id="00b87-232">Para obtener información acerca de cómo tooredeploy una máquina virtual, consulte [volver a implementar la máquina virtual toonew nodo Azure](../windows/redeploy-to-new-node.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="00b87-232">For information about how tooredeploy a VM, see [Redeploy virtual machine toonew Azure node](../windows/redeploy-to-new-node.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>
  
    <span data-ttu-id="00b87-233">Una vez finalizada esta operación, se perderán los datos de disco efímeros y direcciones IP dinámicas que están asociadas a la máquina virtual de Hola se actualizará.</span><span class="sxs-lookup"><span data-stu-id="00b87-233">After this operation finishes, ephemeral disk data will be lost and dynamic IP addresses that are associated with hello virtual machine will be updated.</span></span>
* <span data-ttu-id="00b87-234">Siga las instrucciones de hello en [cómo tooreset una contraseña o SSH para máquinas virtuales basadas en Linux](classic/reset-access.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json) para:</span><span class="sxs-lookup"><span data-stu-id="00b87-234">Follow hello instructions in [How tooreset a password or SSH for Linux-based virtual machines](classic/reset-access.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json) to:</span></span>
  
  * <span data-ttu-id="00b87-235">Hola de restablecimiento de contraseña o clave SSH.</span><span class="sxs-lookup"><span data-stu-id="00b87-235">Reset hello password or SSH key.</span></span>
  * <span data-ttu-id="00b87-236">Crear una nueva cuenta de usuario de *sudo*.</span><span class="sxs-lookup"><span data-stu-id="00b87-236">Create a *sudo* user account.</span></span>
  * <span data-ttu-id="00b87-237">Restablecer configuración de SSH de Hola.</span><span class="sxs-lookup"><span data-stu-id="00b87-237">Reset hello SSH configuration.</span></span>
* <span data-ttu-id="00b87-238">Compruebe el estado de los recursos de máquina virtual de Hola para cualquier problema de plataforma.</span><span class="sxs-lookup"><span data-stu-id="00b87-238">Check hello VM's resource health for any platform issues.</span></span><br>
     <span data-ttu-id="00b87-239">Seleccione la máquina virtual y desplácese hacia abajo hasta **Configuración** > **Comprobar estado**.</span><span class="sxs-lookup"><span data-stu-id="00b87-239">Select your VM and scroll down **Settings** > **Check Health**.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="00b87-240">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="00b87-240">Additional resources</span></span>
* <span data-ttu-id="00b87-241">Si se sigue sin tooSSH tooyour VM después de Hola siguiente después de los pasos, consulte [más pasos para solucionar problemas](detailed-troubleshoot-ssh-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) tooreview adicional pasos tooresolve su problema.</span><span class="sxs-lookup"><span data-stu-id="00b87-241">If you are still unable tooSSH tooyour VM after following hello after steps, see [more detailed troubleshooting steps](detailed-troubleshoot-ssh-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) tooreview additional steps tooresolve your issue.</span></span>
* <span data-ttu-id="00b87-242">Para obtener más información sobre cómo solucionar problemas de acceso a la aplicación, consulte [aplicación tooan solucionar access que ejecuta en una máquina virtual de Azure](../windows/troubleshoot-app-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)</span><span class="sxs-lookup"><span data-stu-id="00b87-242">For more information about troubleshooting application access, see [Troubleshoot access tooan application running on an Azure virtual machine](../windows/troubleshoot-app-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)</span></span>
* <span data-ttu-id="00b87-243">Para obtener más información sobre cómo solucionar problemas de máquinas virtuales que se crearon con el modelo de implementación clásica de hello, consulte [cómo tooreset una contraseña o SSH para máquinas virtuales basadas en Linux](classic/reset-access.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="00b87-243">For more information about troubleshooting virtual machines that were created by using hello classic deployment model, see [How tooreset a password or SSH for Linux-based virtual machines](classic/reset-access.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json).</span></span>

