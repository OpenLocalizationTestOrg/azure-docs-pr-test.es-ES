---
title: "Solución de problemas de conexión de SSH a una máquina virtual de Azure | Microsoft Docs"
description: "Cómo solucionar problemas de error de conexión SSH o de conexión SSH rechazada en una máquina virtual de Azure que ejecuta Lunux."
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
ms.openlocfilehash: 3a282c8b2c2ba2749de6a2d3688bd57d75703b22
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/18/2017
---
# <a name="troubleshoot-ssh-connections-to-an-azure-linux-vm-that-fails-errors-out-or-is-refused"></a><span data-ttu-id="78d7e-104">Solución de problemas de conexiones SSH a una máquina virtual Linux de Azure que producen error o se rechazan.</span><span class="sxs-lookup"><span data-stu-id="78d7e-104">Troubleshoot SSH connections to an Azure Linux VM that fails, errors out, or is refused</span></span>
<span data-ttu-id="78d7e-105">Hay varias razones por las que podrían producirse errores de Secure Shell (SSH), errores de conexión de SSH o que se rechace SSH al intentar conectarse a una máquina virtual (VM) Linux.</span><span class="sxs-lookup"><span data-stu-id="78d7e-105">There are various reasons that you encounter Secure Shell (SSH) errors, SSH connection failures, or SSH is refused when you try to connect to a Linux virtual machine (VM).</span></span> <span data-ttu-id="78d7e-106">Este artículo le ayudará a identificar esos problemas y corregirlos.</span><span class="sxs-lookup"><span data-stu-id="78d7e-106">This article helps you find and correct the problems.</span></span> <span data-ttu-id="78d7e-107">Para solucionar problemas de conexión, puede usar Azure Portal, la CLI de Azure o la extensión de acceso de máquina virtual para Linux.</span><span class="sxs-lookup"><span data-stu-id="78d7e-107">You can use the Azure portal, Azure CLI, or VM Access Extension for Linux to troubleshoot and resolve connection problems.</span></span>

[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-both-include.md)]

<span data-ttu-id="78d7e-108">Si necesita más ayuda con cualquier aspecto de este artículo, puede ponerse en contacto con los expertos de Azure en [los foros de MSDN Azure o Stack Overflow](http://azure.microsoft.com/support/forums/).</span><span class="sxs-lookup"><span data-stu-id="78d7e-108">If you need more help at any point in this article, you can contact the Azure experts on [the MSDN Azure and Stack Overflow forums](http://azure.microsoft.com/support/forums/).</span></span> <span data-ttu-id="78d7e-109">Como alternativa, puede registrar un incidente de soporte técnico de Azure.</span><span class="sxs-lookup"><span data-stu-id="78d7e-109">Alternatively, you can file an Azure support incident.</span></span> <span data-ttu-id="78d7e-110">Vaya al [sitio de soporte técnico de Azure](http://azure.microsoft.com/support/options/) y seleccione **Obtener soporte**.</span><span class="sxs-lookup"><span data-stu-id="78d7e-110">Go to the [Azure support site](http://azure.microsoft.com/support/options/) and select **Get support**.</span></span> <span data-ttu-id="78d7e-111">Para obtener información sobre el uso del soporte técnico, lea las [Preguntas más frecuentes de soporte técnico de Microsoft Azure](http://azure.microsoft.com/support/faq/).</span><span class="sxs-lookup"><span data-stu-id="78d7e-111">For information about using Azure Support, read the [Microsoft Azure support FAQ](http://azure.microsoft.com/support/faq/).</span></span>

## <a name="quick-troubleshooting-steps"></a><span data-ttu-id="78d7e-112">Pasos rápidos para solucionar problemas</span><span class="sxs-lookup"><span data-stu-id="78d7e-112">Quick troubleshooting steps</span></span>
<span data-ttu-id="78d7e-113">Después de cada paso de solución de problemas, intente volver a conectarse a la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="78d7e-113">After each troubleshooting step, try reconnecting to the VM.</span></span>

1. <span data-ttu-id="78d7e-114">Restablecer la configuración de SSH.</span><span class="sxs-lookup"><span data-stu-id="78d7e-114">Reset the SSH configuration.</span></span>
2. <span data-ttu-id="78d7e-115">Restablezca las credenciales del usuario.</span><span class="sxs-lookup"><span data-stu-id="78d7e-115">Reset the credentials for the user.</span></span>
3. <span data-ttu-id="78d7e-116">Compruebe las reglas del [grupo de seguridad de red](../../virtual-network/virtual-networks-nsg.md) que permitan el tráfico SSH.</span><span class="sxs-lookup"><span data-stu-id="78d7e-116">Verify the [Network Security Group](../../virtual-network/virtual-networks-nsg.md) rules permit SSH traffic.</span></span>
   * <span data-ttu-id="78d7e-117">Asegúrese de que existe una regla de grupo de seguridad de red para permitir el tráfico SSH (de forma predeterminada, el puerto TCP 22).</span><span class="sxs-lookup"><span data-stu-id="78d7e-117">Ensure that a Network Security Group rule exists to permit SSH traffic (by default, TCP port 22).</span></span>
   * <span data-ttu-id="78d7e-118">No se puede usar el redireccionamiento o la asignación de puertos sin utilizar un equilibrador de carga de Azure.</span><span class="sxs-lookup"><span data-stu-id="78d7e-118">You cannot use port redirection / mapping without using an Azure load balancer.</span></span>
4. <span data-ttu-id="78d7e-119">Compruebe el [estado de los recursos de la máquina virtual](../../resource-health/resource-health-overview.md).</span><span class="sxs-lookup"><span data-stu-id="78d7e-119">Check the [VM resource health](../../resource-health/resource-health-overview.md).</span></span> 
   * <span data-ttu-id="78d7e-120">Asegúrese de que el estado de la máquina virtual se notifica como correcto.</span><span class="sxs-lookup"><span data-stu-id="78d7e-120">Ensure that the VM reports as being healthy.</span></span>
   * <span data-ttu-id="78d7e-121">Si tiene habilitado el diagnóstico de arranque, compruebe que la máquina virtual no notifica errores de arranque en los registros.</span><span class="sxs-lookup"><span data-stu-id="78d7e-121">If you have boot diagnostics enabled, verify the VM is not reporting boot errors in the logs.</span></span>
5. <span data-ttu-id="78d7e-122">Reinicie la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="78d7e-122">Restart the VM.</span></span>
6. <span data-ttu-id="78d7e-123">Vuelva a implementar la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="78d7e-123">Redeploy the VM.</span></span>

<span data-ttu-id="78d7e-124">Siga leyendo para conocer pasos y soluciones más detallados de solución de problemas.</span><span class="sxs-lookup"><span data-stu-id="78d7e-124">Continue reading for more detailed troubleshooting steps and explanations.</span></span>

## <a name="available-methods-to-troubleshoot-ssh-connection-issues"></a><span data-ttu-id="78d7e-125">Métodos disponibles para la solución de problemas de conexiones de SSH</span><span class="sxs-lookup"><span data-stu-id="78d7e-125">Available methods to troubleshoot SSH connection issues</span></span>
<span data-ttu-id="78d7e-126">Puede restablecer las credenciales o la configuración de SSH mediante uno de los métodos siguientes:</span><span class="sxs-lookup"><span data-stu-id="78d7e-126">You can reset credentials or SSH configuration using one of the following methods:</span></span>

* <span data-ttu-id="78d7e-127">[Azure Portal](#use-the-azure-portal): este método funciona muy bien si necesita restablecer rápidamente la configuración o la clave de SSH y no tiene instaladas las herramientas de Azure.</span><span class="sxs-lookup"><span data-stu-id="78d7e-127">[Azure portal](#use-the-azure-portal) - great if you need to quickly reset the SSH configuration or SSH key and you don't have the Azure tools installed.</span></span>
* <span data-ttu-id="78d7e-128">[CLI de Azure 2.0](#use-the-azure-cli-20): si ya está en la línea de comandos, restablezca rápidamente la configuración o las credenciales de SSH.</span><span class="sxs-lookup"><span data-stu-id="78d7e-128">[Azure CLI 2.0](#use-the-azure-cli-20) - if you are already on the command line, quickly reset the SSH configuration or credentials.</span></span> <span data-ttu-id="78d7e-129">También puede usar la [CLI de Azure 1.0](#use-the-azure-cli-10).</span><span class="sxs-lookup"><span data-stu-id="78d7e-129">You can also use the [Azure CLI 1.0](#use-the-azure-cli-10)</span></span>
* <span data-ttu-id="78d7e-130">[Extensión Azure VMAccessForLinux](#use-the-vmaccess-extension): permite crear y reutilizar archivos de definición json para restablecer la configuración o las credenciales de usuario de SSH.</span><span class="sxs-lookup"><span data-stu-id="78d7e-130">[Azure VMAccessForLinux extension](#use-the-vmaccess-extension) - create and reuse json definition files to reset the SSH configuration or user credentials.</span></span>

<span data-ttu-id="78d7e-131">Después de cada paso de solución de problemas, intente conectarse de nuevo a la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="78d7e-131">After each troubleshooting step, try connecting to your VM again.</span></span> <span data-ttu-id="78d7e-132">Si sigue sin poder conectarse, pruebe el paso siguiente.</span><span class="sxs-lookup"><span data-stu-id="78d7e-132">If you still cannot connect, try the next step.</span></span>

## <a name="use-the-azure-portal"></a><span data-ttu-id="78d7e-133">Uso de Azure Portal</span><span class="sxs-lookup"><span data-stu-id="78d7e-133">Use the Azure portal</span></span>
<span data-ttu-id="78d7e-134">Azure Portal proporciona una forma rápida de restablecer la configuración o las credenciales de usuario de SSH sin necesidad de instalar ninguna herramienta en el equipo local.</span><span class="sxs-lookup"><span data-stu-id="78d7e-134">The Azure portal provides a quick way to reset the SSH configuration or user credentials without installing any tools on your local computer.</span></span>

<span data-ttu-id="78d7e-135">Seleccione la máquina virtual en Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="78d7e-135">Select your VM in the Azure portal.</span></span> <span data-ttu-id="78d7e-136">Desplácese hacia abajo hasta la sección **Soporte técnico y solución de problemas** y seleccione **Restablecer contraseña** como en el ejemplo siguiente:</span><span class="sxs-lookup"><span data-stu-id="78d7e-136">Scroll down to the **Support + Troubleshooting** section and select **Reset password** as in the following example:</span></span>

![Restablecer la configuración o las credenciales de SSH en Azure Portal](./media/troubleshoot-ssh-connection/reset-credentials-using-portal.png)

### <a name="reset-the-ssh-configuration"></a><span data-ttu-id="78d7e-138">Restablecer la configuración de SSH</span><span class="sxs-lookup"><span data-stu-id="78d7e-138">Reset the SSH configuration</span></span>
<span data-ttu-id="78d7e-139">Como primer paso, seleccione `Reset configuration only` en el menú desplegable **Modo** como en la captura de pantalla anterior y luego haga clic en el botón **Restablecer**.</span><span class="sxs-lookup"><span data-stu-id="78d7e-139">As a first step, select `Reset configuration only` from the **Mode** drop-down menu as in the preceding screenshot, then click the **Reset** button.</span></span> <span data-ttu-id="78d7e-140">Una vez completada esta acción, intente acceder de nuevo a la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="78d7e-140">Once this action has completed, try to access your VM again.</span></span>

### <a name="reset-ssh-credentials-for-a-user"></a><span data-ttu-id="78d7e-141">Restablecimiento de las credenciales de SSH de un usuario</span><span class="sxs-lookup"><span data-stu-id="78d7e-141">Reset SSH credentials for a user</span></span>
<span data-ttu-id="78d7e-142">Para restablecer las credenciales de un usuario existente, seleccione `Reset SSH public key` o `Reset password` en el menú desplegable **Modo** como en la captura de pantalla anterior.</span><span class="sxs-lookup"><span data-stu-id="78d7e-142">To reset the credentials of an existing user, select either `Reset SSH public key` or `Reset password` from the **Mode** drop-down menu as in the preceding screenshot.</span></span> <span data-ttu-id="78d7e-143">Especifique el nombre de usuario y una clave de SSH o una nueva contraseña y haga clic en el botón **Restablecer**.</span><span class="sxs-lookup"><span data-stu-id="78d7e-143">Specify the username and an SSH key or new password, then click the **Reset** button.</span></span>

<span data-ttu-id="78d7e-144">Desde este menú también puede crear un usuario con privilegios de sudo en la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="78d7e-144">You can also create a user with sudo privileges on the VM from this menu.</span></span> <span data-ttu-id="78d7e-145">Escriba un nuevo nombre de usuario y la contraseña o la clave SSH asociada y luego haga clic en el botón **Restablecer**.</span><span class="sxs-lookup"><span data-stu-id="78d7e-145">Enter a new username and associated password or SSH key, and then click the **Reset** button.</span></span>

## <a name="use-the-azure-cli-20"></a><span data-ttu-id="78d7e-146">Uso de la CLI de Azure 2.0</span><span class="sxs-lookup"><span data-stu-id="78d7e-146">Use the Azure CLI 2.0</span></span>
<span data-ttu-id="78d7e-147">Si todavía no la tiene, instale la [CLI de Azure 2.0](/cli/azure/install-az-cli2) más reciente e inicie sesión en una cuenta de Azure con [az login](/cli/azure/#login).</span><span class="sxs-lookup"><span data-stu-id="78d7e-147">If you haven't already, install the latest [Azure CLI 2.0](/cli/azure/install-az-cli2) and log in to an Azure account using [az login](/cli/azure/#login).</span></span>

<span data-ttu-id="78d7e-148">Si ha creado y cargado una imagen de disco Linux personalizada, asegúrese de que el [agente Linux de Microsoft Azure](../windows/agent-user-guide.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) versión 2.0.5 o posterior esté instalado.</span><span class="sxs-lookup"><span data-stu-id="78d7e-148">If you created and uploaded a custom Linux disk image, make sure the [Microsoft Azure Linux Agent](../windows/agent-user-guide.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) version 2.0.5 or later is installed.</span></span> <span data-ttu-id="78d7e-149">Para máquinas virtuales creadas mediante imágenes de la galería, esta extensión de acceso ya está instalada y configurada automáticamente.</span><span class="sxs-lookup"><span data-stu-id="78d7e-149">For VMs created using Gallery images, this access extension is already installed and configured for you.</span></span>

### <a name="reset-ssh-configuration"></a><span data-ttu-id="78d7e-150">Restablecer la configuración de SSH</span><span class="sxs-lookup"><span data-stu-id="78d7e-150">Reset SSH configuration</span></span>
<span data-ttu-id="78d7e-151">Incialmente también puede tratar de restablecer la configuración de SSH a los valores predeterminados y reiniciar el servidor SSH en la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="78d7e-151">You can initially try resetting the SSH configuration to default values and rebooting the SSH server on the VM.</span></span> <span data-ttu-id="78d7e-152">Tenga en cuenta que esto no cambia el nombre de la cuenta de usuario, la contraseña ni las claves SSH.</span><span class="sxs-lookup"><span data-stu-id="78d7e-152">Note that this does not change the user account name, password, or SSH keys.</span></span>
<span data-ttu-id="78d7e-153">En el ejemplo siguiente se utiliza [az vm user reset-ssh](/cli/azure/vm/user#reset-ssh) para restablecer la configuración de SSH en la máquina virtual denominada `myVM` en `myResourceGroup`.</span><span class="sxs-lookup"><span data-stu-id="78d7e-153">The following example uses [az vm user reset-ssh](/cli/azure/vm/user#reset-ssh) to reset the SSH configuration on the VM named `myVM` in `myResourceGroup`.</span></span> <span data-ttu-id="78d7e-154">Use sus propios valores, como se indica a continuación:</span><span class="sxs-lookup"><span data-stu-id="78d7e-154">Use your own values as follows:</span></span>

```azurecli
az vm user reset-ssh --resource-group myResourceGroup --name myVM
```

### <a name="reset-ssh-credentials-for-a-user"></a><span data-ttu-id="78d7e-155">Restablecimiento de las credenciales de SSH de un usuario</span><span class="sxs-lookup"><span data-stu-id="78d7e-155">Reset SSH credentials for a user</span></span>
<span data-ttu-id="78d7e-156">En el ejemplo siguiente se usa [az vm user update](/cli/azure/vm/user#update) para restablecer las credenciales de `myUsername` al valor especificado en `myPassword`, en la máquina virtual llamada `myVM` en `myResourceGroup`.</span><span class="sxs-lookup"><span data-stu-id="78d7e-156">The following example uses [az vm user update](/cli/azure/vm/user#update) to reset the credentials for `myUsername` to the value specified in `myPassword`, on the VM named `myVM` in `myResourceGroup`.</span></span> <span data-ttu-id="78d7e-157">Use sus propios valores, como se indica a continuación:</span><span class="sxs-lookup"><span data-stu-id="78d7e-157">Use your own values as follows:</span></span>

```azurecli
az vm user update --resource-group myResourceGroup --name myVM \
     --username myUsername --password myPassword
```

<span data-ttu-id="78d7e-158">Si usa la autenticación de claves SSH, puede restablecer la clave SSH de un usuario determinado:</span><span class="sxs-lookup"><span data-stu-id="78d7e-158">If using SSH key authentication, you can reset the SSH key for a given user.</span></span> <span data-ttu-id="78d7e-159">En el ejemplo siguiente se usa **az vm access set-linux-user** para actualizar la clave SSH almacenada en `~/.ssh/id_rsa.pub` para el usuario llamado `myUsername`, en la máquina virtual llamada `myVM` en `myResourceGroup`.</span><span class="sxs-lookup"><span data-stu-id="78d7e-159">The following example uses **az vm access set-linux-user** to update the SSH key stored in `~/.ssh/id_rsa.pub` for the user named `myUsername`, on the VM named `myVM` in `myResourceGroup`.</span></span> <span data-ttu-id="78d7e-160">Use sus propios valores, como se indica a continuación:</span><span class="sxs-lookup"><span data-stu-id="78d7e-160">Use your own values as follows:</span></span>

```azurecli
az vm user update --resource-group myResourceGroup --name myVM \
    --username myUsername --ssh-key-value ~/.ssh/id_rsa.pub
```

## <a name="use-the-vmaccess-extension"></a><span data-ttu-id="78d7e-161">Uso de la extensión VMAccess</span><span class="sxs-lookup"><span data-stu-id="78d7e-161">Use the VMAccess extension</span></span>
<span data-ttu-id="78d7e-162">La extensión de acceso de máquina virtual de Linux lee un archivo json que define las acciones que se llevarán a cabo. Estas acciones incluyen el restablecimiento de SSHD o de una clave SSH o la adición de un usuario.</span><span class="sxs-lookup"><span data-stu-id="78d7e-162">The VM Access Extension for Linux reads in a json file that defines actions to carry out. These actions include resetting SSHD, resetting an SSH key, or adding a user.</span></span> <span data-ttu-id="78d7e-163">Seguirá usando la CLI de Azure para llamar a la extensión VMAccess, pero puede reutilizar los archivos json entre varias máquinas virtuales si así lo desea.</span><span class="sxs-lookup"><span data-stu-id="78d7e-163">You still use the Azure CLI to call the VMAccess extension, but you can reuse the json files across multiple VMs if desired.</span></span> <span data-ttu-id="78d7e-164">Este enfoque permite crear un repositorio de archivos json que luego se pueden llamar en escenarios determinados.</span><span class="sxs-lookup"><span data-stu-id="78d7e-164">This approach allows you to create a repository of json files that can then be called for given scenarios.</span></span>

### <a name="reset-sshd"></a><span data-ttu-id="78d7e-165">Restablecer SSHD</span><span class="sxs-lookup"><span data-stu-id="78d7e-165">Reset SSHD</span></span>
<span data-ttu-id="78d7e-166">Cree un archivo llamado `settings.json` con el siguiente contenido:</span><span class="sxs-lookup"><span data-stu-id="78d7e-166">Create a file named `settings.json` with the following content:</span></span>

```json
{  
    "reset_ssh":"True"
}
```

<span data-ttu-id="78d7e-167">Con la CLI de Azure, luego puede llamar a la extensión `VMAccessForLinux` para restablecer la conexión de SSHD mediante la especificación de archivo json.</span><span class="sxs-lookup"><span data-stu-id="78d7e-167">Using the Azure CLI, you then call the `VMAccessForLinux` extension to reset your SSHD connection by specifying your json file.</span></span> <span data-ttu-id="78d7e-168">En el ejemplo siguiente se utiliza [az vm extension set](/cli/azure/vm/extension#set) para restablecer SSHD en la máquina virtual denominada `myVM` en `myResourceGroup`.</span><span class="sxs-lookup"><span data-stu-id="78d7e-168">The following example uses [az vm extension set](/cli/azure/vm/extension#set) to reset SSHD on the VM named `myVM` in `myResourceGroup`.</span></span> <span data-ttu-id="78d7e-169">Use sus propios valores, como se indica a continuación:</span><span class="sxs-lookup"><span data-stu-id="78d7e-169">Use your own values as follows:</span></span>

```azurecli
az vm extension set --resource-group philmea --vm-name Ubuntu \
    --name VMAccessForLinux --publisher Microsoft.OSTCExtensions --version 1.2 --settings settings.json
```

### <a name="reset-ssh-credentials-for-a-user"></a><span data-ttu-id="78d7e-170">Restablecimiento de las credenciales de SSH de un usuario</span><span class="sxs-lookup"><span data-stu-id="78d7e-170">Reset SSH credentials for a user</span></span>
<span data-ttu-id="78d7e-171">Si SSHD parece funcionar correctamente, puede restablecer las credenciales de un usuario dado.</span><span class="sxs-lookup"><span data-stu-id="78d7e-171">If SSHD appears to function correctly, you can reset the credentials for a giver user.</span></span> <span data-ttu-id="78d7e-172">Para restablecer la contraseña de un usuario, cree un archivo llamado `settings.json`.</span><span class="sxs-lookup"><span data-stu-id="78d7e-172">To reset the password for a user, create a file named `settings.json`.</span></span> <span data-ttu-id="78d7e-173">En el ejemplo siguiente se restablecen las credenciales de `myUsername` en el valor especificado en `myPassword`.</span><span class="sxs-lookup"><span data-stu-id="78d7e-173">The following example resets the credentials for `myUsername` to the value specified in `myPassword`.</span></span> <span data-ttu-id="78d7e-174">Escriba las líneas siguientes en el archivo `settings.json`, usando sus propios valores:</span><span class="sxs-lookup"><span data-stu-id="78d7e-174">Enter the following lines into your `settings.json` file, using your own values:</span></span>

```json
{
    "username":"myUsername", "password":"myPassword"
}
```

<span data-ttu-id="78d7e-175">O bien, para restablecer la clave SSH de un usuario, primero cree un archivo llamado `settings.json`.</span><span class="sxs-lookup"><span data-stu-id="78d7e-175">Or to reset the SSH key for a user, first create a file named `settings.json`.</span></span> <span data-ttu-id="78d7e-176">En el ejemplo siguiente se restablecen las credenciales para `myUsername` al valor especificado en `myPassword`, en la máquina virtual llamada `myVM` en `myResourceGroup`.</span><span class="sxs-lookup"><span data-stu-id="78d7e-176">The following example resets the credentials for `myUsername` to the value specified in `myPassword`, on the VM named `myVM` in `myResourceGroup`.</span></span> <span data-ttu-id="78d7e-177">Escriba las líneas siguientes en el archivo `settings.json`, usando sus propios valores:</span><span class="sxs-lookup"><span data-stu-id="78d7e-177">Enter the following lines into your `settings.json` file, using your own values:</span></span>

```json
{
    "username":"myUsername", "ssh_key":"mySSHKey"
}
```

<span data-ttu-id="78d7e-178">Después de crear el archivo json, use la CLI de Azure para llamar a la extensión `VMAccessForLinux` y restablecer las credenciales de usuario SSH mediante la especificación del archivo json.</span><span class="sxs-lookup"><span data-stu-id="78d7e-178">After creating your json file, use the Azure CLI to call the `VMAccessForLinux` extension to reset your SSH user credentials by specifying your json file.</span></span> <span data-ttu-id="78d7e-179">En el ejemplo siguiente se restablecen las credenciales en la máquina virtual llamada `myVM` en `myResourceGroup`.</span><span class="sxs-lookup"><span data-stu-id="78d7e-179">The following example resets credentials on the VM named `myVM` in `myResourceGroup`.</span></span> <span data-ttu-id="78d7e-180">Use sus propios valores, como se indica a continuación:</span><span class="sxs-lookup"><span data-stu-id="78d7e-180">Use your own values as follows:</span></span>

```azurecli
az vm extension set --resource-group philmea --vm-name Ubuntu \
    --name VMAccessForLinux --publisher Microsoft.OSTCExtensions --version 1.2 --settings settings.json
```

## <a name="use-the-azure-cli-10"></a><span data-ttu-id="78d7e-181">Uso de la CLI de Azure 1.0</span><span class="sxs-lookup"><span data-stu-id="78d7e-181">Use the Azure CLI 1.0</span></span>
<span data-ttu-id="78d7e-182">Si todavía no la tiene, [instale la CLI de Azure 1.0 y conéctese a su suscripción de Azure](../../cli-install-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="78d7e-182">If you haven't already, [install the Azure CLI 1.0 and connect to your Azure subscription](../../cli-install-nodejs.md).</span></span> <span data-ttu-id="78d7e-183">Asegúrese de que está usando el modo de Resource Manager como se indica:</span><span class="sxs-lookup"><span data-stu-id="78d7e-183">Make sure that you are using Resource Manager mode as follows:</span></span>

```azurecli
azure config mode arm
```

<span data-ttu-id="78d7e-184">Si ha creado y cargado una imagen de disco Linux personalizada, asegúrese de que el [agente Linux de Microsoft Azure](../windows/agent-user-guide.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) versión 2.0.5 o posterior esté instalado.</span><span class="sxs-lookup"><span data-stu-id="78d7e-184">If you created and uploaded a custom Linux disk image, make sure the [Microsoft Azure Linux Agent](../windows/agent-user-guide.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) version 2.0.5 or later is installed.</span></span> <span data-ttu-id="78d7e-185">Para máquinas virtuales creadas mediante imágenes de la galería, esta extensión de acceso ya está instalada y configurada automáticamente.</span><span class="sxs-lookup"><span data-stu-id="78d7e-185">For VMs created using Gallery images, this access extension is already installed and configured for you.</span></span>

### <a name="reset-ssh-configuration"></a><span data-ttu-id="78d7e-186">Restablecer la configuración de SSH</span><span class="sxs-lookup"><span data-stu-id="78d7e-186">Reset SSH configuration</span></span>
<span data-ttu-id="78d7e-187">La configuración de SSHD podría no ser correcta o que el servicio haya encontrado un error.</span><span class="sxs-lookup"><span data-stu-id="78d7e-187">The SSHD configuration itself may be misconfigured or the service encountered an error.</span></span> <span data-ttu-id="78d7e-188">Puede restablecer SSHD para asegurarse de que la configuración de SSH sea válida.</span><span class="sxs-lookup"><span data-stu-id="78d7e-188">You can reset SSHD to make sure the SSH configuration itself is valid.</span></span> <span data-ttu-id="78d7e-189">El restablecimiento de SSHD debe ser el primer paso de solución de problemas que debe realizar.</span><span class="sxs-lookup"><span data-stu-id="78d7e-189">Resetting SSHD should be the first troubleshooting step you take.</span></span>

<span data-ttu-id="78d7e-190">En el ejemplo siguiente se restablece SSHD en una máquina virtual llamada `myVM` en el grupo de recursos llamado `myResourceGroup`.</span><span class="sxs-lookup"><span data-stu-id="78d7e-190">The following example resets SSHD on a VM named `myVM` in the resource group named `myResourceGroup`.</span></span> <span data-ttu-id="78d7e-191">Use sus propios nombres de grupo de recursos y máquina virtual, como se indica a continuación:</span><span class="sxs-lookup"><span data-stu-id="78d7e-191">Use your own VM and resource group names as follows:</span></span>

```azurecli
azure vm reset-access --resource-group myResourceGroup --name myVM \
    --reset-ssh
```

### <a name="reset-ssh-credentials-for-a-user"></a><span data-ttu-id="78d7e-192">Restablecimiento de las credenciales de SSH de un usuario</span><span class="sxs-lookup"><span data-stu-id="78d7e-192">Reset SSH credentials for a user</span></span>
<span data-ttu-id="78d7e-193">Si SSHD parece funcionar correctamente, puede restablecer la contraseña de un usuario dado.</span><span class="sxs-lookup"><span data-stu-id="78d7e-193">If SSHD appears to function correctly, you can reset the password for a giver user.</span></span> <span data-ttu-id="78d7e-194">En el ejemplo siguiente se restablecen las credenciales para `myUsername` al valor especificado en `myPassword`, en la máquina virtual llamada `myVM` en `myResourceGroup`.</span><span class="sxs-lookup"><span data-stu-id="78d7e-194">The following example resets the credentials for `myUsername` to the value specified in `myPassword`, on the VM named `myVM` in `myResourceGroup`.</span></span> <span data-ttu-id="78d7e-195">Use sus propios valores, como se indica a continuación:</span><span class="sxs-lookup"><span data-stu-id="78d7e-195">Use your own values as follows:</span></span>

```azurecli
azure vm reset-access --resource-group myResourceGroup --name myVM \
     --user-name myUsername --password myPassword
```

<span data-ttu-id="78d7e-196">Si usa la autenticación de claves SSH, puede restablecer la clave SSH de un usuario determinado:</span><span class="sxs-lookup"><span data-stu-id="78d7e-196">If using SSH key authentication, you can reset the SSH key for a given user.</span></span> <span data-ttu-id="78d7e-197">En el ejemplo siguiente se actualiza la clave SSH almacenada en `~/.ssh/id_rsa.pub` para el usuario llamado `myUsername`, en la máquina virtual llamada `myVM` en `myResourceGroup`.</span><span class="sxs-lookup"><span data-stu-id="78d7e-197">The following example updates the SSH key stored in `~/.ssh/id_rsa.pub` for the user named `myUsername`, on the VM named `myVM` in `myResourceGroup`.</span></span> <span data-ttu-id="78d7e-198">Use sus propios valores, como se indica a continuación:</span><span class="sxs-lookup"><span data-stu-id="78d7e-198">Use your own values as follows:</span></span>

```azurecli
azure vm reset-access --resource-group myResourceGroup --name myVM \
    --user-name myUsername --ssh-key-file ~/.ssh/id_rsa.pub
```


## <a name="restart-a-vm"></a><span data-ttu-id="78d7e-199">Reinicio de una máquina virtual</span><span class="sxs-lookup"><span data-stu-id="78d7e-199">Restart a VM</span></span>
<span data-ttu-id="78d7e-200">Si ha restablecido la configuración y las credenciales de usuario de SSH, o ha encontrado un error al hacerlo, puede intentar reiniciar la máquina virtual para solucionar los problemas de procesos subyacentes.</span><span class="sxs-lookup"><span data-stu-id="78d7e-200">If you have reset the SSH configuration and user credentials, or encountered an error in doing so, you can try restarting the VM to address underlying compute issues.</span></span>

### <a name="azure-portal"></a><span data-ttu-id="78d7e-201">Azure Portal</span><span class="sxs-lookup"><span data-stu-id="78d7e-201">Azure portal</span></span>
<span data-ttu-id="78d7e-202">Para reiniciar una máquina virtual mediante Azure Portal, seleccione la máquina virtual y haga clic en el botón **Reiniciar**, como en el ejemplo siguiente:</span><span class="sxs-lookup"><span data-stu-id="78d7e-202">To restart a VM using the Azure portal, select your VM and click the **Restart** button as in the following example:</span></span>

![Reiniciar una máquina virtual en Azure Portal](./media/troubleshoot-ssh-connection/restart-vm-using-portal.png)

### <a name="azure-cli-10"></a><span data-ttu-id="78d7e-204">CLI de Azure 1.0</span><span class="sxs-lookup"><span data-stu-id="78d7e-204">Azure CLI 1.0</span></span>
<span data-ttu-id="78d7e-205">En el ejemplo siguiente se reinicia la máquina virtual llamada `myVM` en el grupo de recursos llamado `myResourceGroup`:</span><span class="sxs-lookup"><span data-stu-id="78d7e-205">The following example restarts the VM named `myVM` in the resource group named `myResourceGroup`.</span></span> <span data-ttu-id="78d7e-206">Use sus propios valores, como se indica a continuación:</span><span class="sxs-lookup"><span data-stu-id="78d7e-206">Use your own values as follows:</span></span>

```azurecli
azure vm restart --resource-group myResourceGroup --name myVM
```

### <a name="azure-cli-20"></a><span data-ttu-id="78d7e-207">CLI de Azure 2.0</span><span class="sxs-lookup"><span data-stu-id="78d7e-207">Azure CLI 2.0</span></span>
<span data-ttu-id="78d7e-208">En el ejemplo siguiente se usa [az vm restart](/cli/azure/vm#restart) para reiniciar la máquina virtual llamada `myVM` en el grupo de recursos llamado `myResourceGroup`.</span><span class="sxs-lookup"><span data-stu-id="78d7e-208">The following example uses [az vm restart](/cli/azure/vm#restart) to restart the VM named `myVM` in the resource group named `myResourceGroup`.</span></span> <span data-ttu-id="78d7e-209">Use sus propios valores, como se indica a continuación:</span><span class="sxs-lookup"><span data-stu-id="78d7e-209">Use your own values as follows:</span></span>

```azurecli
az vm restart --resource-group myResourceGroup --name myVM
```


## <a name="redeploy-a-vm"></a><span data-ttu-id="78d7e-210">Reimplementación de una máquina virtual</span><span class="sxs-lookup"><span data-stu-id="78d7e-210">Redeploy a VM</span></span>
<span data-ttu-id="78d7e-211">Puede volver a implementar una máquina virtual en otro nodo dentro de Azure, lo que podría corregir los problemas de red subyacentes.</span><span class="sxs-lookup"><span data-stu-id="78d7e-211">You can redeploy a VM to another node within Azure, which may correct any underlying networking issues.</span></span> <span data-ttu-id="78d7e-212">Para más información sobre cómo volver a implementar una máquina virtual, consulte [Nueva implementación de la máquina virtual en un nuevo nodo de Azure](../windows/redeploy-to-new-node.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="78d7e-212">For information about redeploying a VM, see [Redeploy virtual machine to new Azure node](../windows/redeploy-to-new-node.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

> [!NOTE]
> <span data-ttu-id="78d7e-213">Cuando finalice esta operación, se perderán los datos de disco efímeros y se actualizarán las direcciones IP dinámicas que están asociadas a la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="78d7e-213">After this operation finishes, ephemeral disk data will be lost and dynamic IP addresses that are associated with the virtual machine will be updated.</span></span>
> 
> 

### <a name="azure-portal"></a><span data-ttu-id="78d7e-214">Azure Portal</span><span class="sxs-lookup"><span data-stu-id="78d7e-214">Azure portal</span></span>
<span data-ttu-id="78d7e-215">Para volver a implementar una máquina virtual mediante Azure Portal, seleccione la máquina virtual y desplácese hacia abajo hasta la sección **Soporte técnico y solución de problemas**.</span><span class="sxs-lookup"><span data-stu-id="78d7e-215">To redeploy a VM using the Azure portal, select your VM and scroll down to the **Support + Troubleshooting** section.</span></span> <span data-ttu-id="78d7e-216">Haga clic en el botón **Redeploy** (Volver a implementar), como en el ejemplo siguiente:</span><span class="sxs-lookup"><span data-stu-id="78d7e-216">Click the **Redeploy** button as in the following example:</span></span>

![Nueva implementación de una máquina virtual en Azure Portal](./media/troubleshoot-ssh-connection/redeploy-vm-using-portal.png)

### <a name="azure-cli-10"></a><span data-ttu-id="78d7e-218">CLI de Azure 1.0</span><span class="sxs-lookup"><span data-stu-id="78d7e-218">Azure CLI 1.0</span></span>
<span data-ttu-id="78d7e-219">En el ejemplo siguiente se vuelve a implementar la máquina virtual llamada `myVM` en el grupo de recursos llamado `myResourceGroup`.</span><span class="sxs-lookup"><span data-stu-id="78d7e-219">The following example redeploys the VM named `myVM` in the resource group named `myResourceGroup`.</span></span> <span data-ttu-id="78d7e-220">Use sus propios valores, como se indica a continuación:</span><span class="sxs-lookup"><span data-stu-id="78d7e-220">Use your own values as follows:</span></span>

```azurecli
azure vm redeploy --resource-group myResourceGroup --name myVM
```

### <a name="azure-cli-20"></a><span data-ttu-id="78d7e-221">CLI de Azure 2.0</span><span class="sxs-lookup"><span data-stu-id="78d7e-221">Azure CLI 2.0</span></span>
<span data-ttu-id="78d7e-222">En el ejemplo siguiente se usa [az vm redeploy](/cli/azure/vm#redeploy) para volver a implementar la máquina virtual llamada `myVM` en el grupo de recursos llamado `myResourceGroup`.</span><span class="sxs-lookup"><span data-stu-id="78d7e-222">The following example use [az vm redeploy](/cli/azure/vm#redeploy) to redeploy the VM named `myVM` in the resource group named `myResourceGroup`.</span></span> <span data-ttu-id="78d7e-223">Use sus propios valores, como se indica a continuación:</span><span class="sxs-lookup"><span data-stu-id="78d7e-223">Use your own values as follows:</span></span>

```azurecli
az vm redeploy --resource-group myResourceGroup --name myVM
```

## <a name="vms-created-by-using-the-classic-deployment-model"></a><span data-ttu-id="78d7e-224">Máquinas virtuales creadas con el modelo de implementación clásica</span><span class="sxs-lookup"><span data-stu-id="78d7e-224">VMs created by using the Classic deployment model</span></span>
<span data-ttu-id="78d7e-225">Siga estos pasos para intentar resolver los errores de conexión SSH más habituales en las máquinas virtuales creadas con el modelo de implementación clásica:</span><span class="sxs-lookup"><span data-stu-id="78d7e-225">Try these steps to resolve the most common SSH connection failures for VMs that were created by using the classic deployment model.</span></span> <span data-ttu-id="78d7e-226">Después de cada paso, pruebe a conectarse a la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="78d7e-226">After each step, try reconnecting to the VM.</span></span>

* <span data-ttu-id="78d7e-227">Restablezca el acceso remoto desde [Azure Portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="78d7e-227">Reset remote access from the [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="78d7e-228">En Azure Portal, seleccione su máquina virtual y haga clic en el botón **Restablecer**.</span><span class="sxs-lookup"><span data-stu-id="78d7e-228">On the Azure portal, select your VM and click the **Reset Remote...** button.</span></span>
* <span data-ttu-id="78d7e-229">Reinicie la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="78d7e-229">Restart the VM.</span></span> <span data-ttu-id="78d7e-230">En [Azure Portal](https://portal.azure.com), seleccione la máquina virtual y haga clic en el botón **Reiniciar**.</span><span class="sxs-lookup"><span data-stu-id="78d7e-230">On the [Azure portal](https://portal.azure.com), select your VM and click the **Restart** button.</span></span>
    
* <span data-ttu-id="78d7e-231">Implemente de nuevo la máquina virtual en un nuevo nodo de Azure.</span><span class="sxs-lookup"><span data-stu-id="78d7e-231">Redeploy the VM to a new Azure node.</span></span> <span data-ttu-id="78d7e-232">Para más información sobre cómo volver a implementar una máquina virtual, consulte [Nueva implementación de la máquina virtual en un nuevo nodo de Azure](../windows/redeploy-to-new-node.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="78d7e-232">For information about how to redeploy a VM, see [Redeploy virtual machine to new Azure node](../windows/redeploy-to-new-node.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>
  
    <span data-ttu-id="78d7e-233">Cuando finalice esta operación, se perderán los datos de disco efímeros y se actualizarán las direcciones IP dinámicas que están asociadas a la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="78d7e-233">After this operation finishes, ephemeral disk data will be lost and dynamic IP addresses that are associated with the virtual machine will be updated.</span></span>
* <span data-ttu-id="78d7e-234">Siga las instrucciones que se indican en [Restablecimiento de una contraseña o SSH para máquinas virtuales Linux](classic/reset-access.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json) para:</span><span class="sxs-lookup"><span data-stu-id="78d7e-234">Follow the instructions in [How to reset a password or SSH for Linux-based virtual machines](classic/reset-access.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json) to:</span></span>
  
  * <span data-ttu-id="78d7e-235">Restablecer la contraseña o la clave de SSH.</span><span class="sxs-lookup"><span data-stu-id="78d7e-235">Reset the password or SSH key.</span></span>
  * <span data-ttu-id="78d7e-236">Crear una nueva cuenta de usuario de *sudo*.</span><span class="sxs-lookup"><span data-stu-id="78d7e-236">Create a *sudo* user account.</span></span>
  * <span data-ttu-id="78d7e-237">Restablecer la configuración de SSH.</span><span class="sxs-lookup"><span data-stu-id="78d7e-237">Reset the SSH configuration.</span></span>
* <span data-ttu-id="78d7e-238">Compruebe el estado de los recursos de la máquina virtual para ver si hay algún problema en la plataforma.</span><span class="sxs-lookup"><span data-stu-id="78d7e-238">Check the VM's resource health for any platform issues.</span></span><br>
     <span data-ttu-id="78d7e-239">Seleccione la máquina virtual y desplácese hacia abajo hasta **Configuración** > **Comprobar estado**.</span><span class="sxs-lookup"><span data-stu-id="78d7e-239">Select your VM and scroll down **Settings** > **Check Health**.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="78d7e-240">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="78d7e-240">Additional resources</span></span>
* <span data-ttu-id="78d7e-241">Si sigue sin poder establecer una conexión SSH a su máquina virtual después de seguir los pasos anteriores, puede examinar [pasos más detallados de solución de problemas](detailed-troubleshoot-ssh-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) para ver pasos adicionales para resolver su problema.</span><span class="sxs-lookup"><span data-stu-id="78d7e-241">If you are still unable to SSH to your VM after following the after steps, see [more detailed troubleshooting steps](detailed-troubleshoot-ssh-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) to review additional steps to resolve your issue.</span></span>
* <span data-ttu-id="78d7e-242">Para más información sobre cómo solucionar problemas de acceso a las aplicaciones, consulte [Solución de problemas de acceso a una aplicación que se ejecuta en una máquina virtual de Azure](../windows/troubleshoot-app-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="78d7e-242">For more information about troubleshooting application access, see [Troubleshoot access to an application running on an Azure virtual machine](../windows/troubleshoot-app-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)</span></span>
* <span data-ttu-id="78d7e-243">Para más información sobre cómo solucionar problemas de máquinas virtuales que se crearon mediante el modelo de implementación clásica, consulte [Restablecimiento de una contraseña o clave SSH para máquinas virtuales Linux](classic/reset-access.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="78d7e-243">For more information about troubleshooting virtual machines that were created by using the classic deployment model, see [How to reset a password or SSH for Linux-based virtual machines](classic/reset-access.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json).</span></span>

