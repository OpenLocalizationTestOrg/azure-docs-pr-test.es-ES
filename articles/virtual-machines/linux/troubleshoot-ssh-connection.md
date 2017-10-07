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
# <a name="troubleshoot-ssh-connections-tooan-azure-linux-vm-that-fails-errors-out-or-is-refused"></a>Solucionar problemas de SSH conexiones tooan VM de Linux de Azure que se produce un error, errores, o se rechaza
Hay varias razones que se producen errores de Shell seguro (SSH), errores de conexión de SSH, o SSH se rechazó al tratar de máquina virtual de Linux de tooa tooconnect (VM). En este artículo le ayuda a buscar y problemas de hello correcto. Puede usar hello portal de Azure, Azure CLI o extensión de acceso de máquina virtual para Linux tootroubleshoot y resolver problemas de conexión.

[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-both-include.md)]

Si necesita más ayuda en cualquier momento en este artículo, puede ponerse en contacto con hello Azure expertos en [Hola foros de Azure de MSDN y el desbordamiento de la pila](http://azure.microsoft.com/support/forums/). Como alternativa, puede registrar un incidente de soporte técnico de Azure. Vaya toohello [sitio de soporte técnico de Azure](http://azure.microsoft.com/support/options/) y seleccione **obtener asistencia**. Para obtener información acerca del uso de soporte técnico de Azure, lea hello [P+F de soporte de Microsoft Azure](http://azure.microsoft.com/support/faq/).

## <a name="quick-troubleshooting-steps"></a>Pasos rápidos para solucionar problemas
Después de cada paso de la solución de problemas, intente volver a conectarse toohello máquina virtual.

1. Restablecer configuración de SSH de Hola.
2. Restablecer credenciales de hello para el usuario de Hola.
3. Comprobar hello [grupo de seguridad de red](../../virtual-network/virtual-networks-nsg.md) reglas de permitan el tráfico SSH.
   * Asegúrese de que el tráfico SSH toopermit existe una regla de grupo de seguridad de red (de forma predeterminada, el puerto TCP 22).
   * No se puede usar el redireccionamiento o la asignación de puertos sin utilizar un equilibrador de carga de Azure.
4. Comprobar hello [mantenimiento de recursos de máquina virtual](../../resource-health/resource-health-overview.md). 
   * Asegúrese de que Hola VM informes como correcto.
   * Si tiene habilitado el diagnóstico de arranque, compruebe Hola VM no informa de errores de arranque en los registros de Hola.
5. Reinicie Hola máquina virtual.
6. Volver a implementar Hola máquina virtual.

Siga leyendo para conocer pasos y soluciones más detallados de solución de problemas.

## <a name="available-methods-tootroubleshoot-ssh-connection-issues"></a>Problemas de conexión de métodos disponibles tootroubleshoot SSH
Puede restablecer las credenciales o la configuración de SSH mediante uno de los siguientes métodos de hello:

* [Portal de Azure](#use-the-azure-portal) : great si necesita tooquickly restablece configuración de SSH de Hola o la clave SSH y no haya Hola instaladas herramientas de Azure.
* [Azure 2.0 CLI](#use-the-azure-cli-20) : si ya está en línea de comandos de hello rápidamente restablecer la configuración de SSH de Hola o las credenciales. También puede usar hello [1.0 de CLI de Azure](#use-the-azure-cli-10)
* [Extensión VMAccessForLinux Azure](#use-the-vmaccess-extension) : crear y volver a json definición archivos tooreset Hola SSH configuración o credenciales de usuario.

Después de cada paso de la solución de problemas, intente conectarse de nuevo tooyour máquina virtual. Si sigue sin poder conectarse, pruebe el paso siguiente Hola.

## <a name="use-hello-azure-portal"></a>Usar hello portal de Azure
Hola portal de Azure proporciona un hello tooreset de forma rápida las credenciales de usuario o configuración de SSH sin necesidad de instalar las herramientas en el equipo local.

Seleccione la máquina virtual en hello portal de Azure. Desplácese hacia abajo toohello **soporte técnico y solución de problemas** sección y seleccione **de restablecimiento de contraseña** como en el siguiente ejemplo de Hola:

![Restablecer la configuración de SSH o credenciales de hello portal de Azure](./media/troubleshoot-ssh-connection/reset-credentials-using-portal.png)

### <a name="reset-hello-ssh-configuration"></a>Restablecer configuración de SSH Hola
Como primer paso, seleccione `Reset configuration only` de hello **modo** menú desplegable como en hello anterior captura de pantalla, a continuación, haga clic en hello **restablecer** botón. Una vez completada esta acción, tooaccess la máquina virtual vuelva a intentarlo.

### <a name="reset-ssh-credentials-for-a-user"></a>Restablecimiento de las credenciales de SSH de un usuario
las credenciales de hello tooreset de un usuario existente, seleccione `Reset SSH public key` o `Reset password` de hello **modo** Hola anterior captura de pantalla en el menú desplegable. Especifique el nombre de usuario de hello y una clave SSH o una nueva contraseña, haga clic en hello **restablecer** botón.

También puede crear un usuario con privilegios de sudo en hello VM desde este menú. Escriba un nuevo nombre de usuario y la contraseña asociada o la clave SSH y, a continuación, haga clic en hello **restablecer** botón.

## <a name="use-hello-azure-cli-20"></a>Usar hello 2.0 de CLI de Azure
Si no lo ha hecho ya, instale hello más reciente [CLI de Azure 2.0](/cli/azure/install-az-cli2) e inicie sesión con cuenta de Azure de tooan [inicio de sesión de az](/cli/azure/#login).

Si ha creado y cargado una imagen de disco Linux personalizada, que seguro Hola [agente Linux de Microsoft Azure](../windows/agent-user-guide.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) versión 2.0.5 o posterior está instalado. Para máquinas virtuales creadas mediante imágenes de la galería, esta extensión de acceso ya está instalada y configurada automáticamente.

### <a name="reset-ssh-configuration"></a>Restablecer la configuración de SSH
Puede inicialmente try restableciendo Hola SSH toodefault los valores de configuración y el servidor SSH de hello reiniciándose en hello máquina virtual. Tenga en cuenta que esto no cambia nombre de cuenta de usuario de hello, contraseñas o claves de SSH.
Hello siguiente ejemplo se utiliza [az vm usuario restablecer-ssh](/cli/azure/vm/user#reset-ssh) tooreset configuración de SSH de hello en máquina virtual denominada hello `myVM` en `myResourceGroup`. Use sus propios valores, como se indica a continuación:

```azurecli
az vm user reset-ssh --resource-group myResourceGroup --name myVM
```

### <a name="reset-ssh-credentials-for-a-user"></a>Restablecimiento de las credenciales de SSH de un usuario
Hello siguiente ejemplo se utiliza [actualización de usuario de vm az](/cli/azure/vm/user#update) tooreset hello las credenciales para `myUsername` valor toohello especificado en `myPassword`, en la máquina virtual denominada hello `myVM` en `myResourceGroup`. Use sus propios valores, como se indica a continuación:

```azurecli
az vm user update --resource-group myResourceGroup --name myVM \
     --username myUsername --password myPassword
```

Si utiliza la autenticación de clave SSH, puede restablecer la clave SSH de Hola para un usuario determinado. Hello siguiente ejemplo se utiliza **az vm acceder a usuario de linux de conjunto** tooupdate Hola SSH clave almacenada en `~/.ssh/id_rsa.pub` con el nombre de usuario de hello `myUsername`, en hello máquina virtual denominada `myVM` en `myResourceGroup`. Use sus propios valores, como se indica a continuación:

```azurecli
az vm user update --resource-group myResourceGroup --name myVM \
    --username myUsername --ssh-key-value ~/.ssh/id_rsa.pub
```

## <a name="use-hello-vmaccess-extension"></a>Use la extensión VMAccess Hola
Hola extensión de acceso de máquina virtual para Linux se lee en un archivo json que define acciones toocarry out. Estas acciones incluyen el restablecimiento de SSHD o de una clave SSH o la adición de un usuario. Seguir usando toocall Hola extensión VMAccess de hello CLI de Azure, pero pueda reutilizar archivos json de hello en varias máquinas virtuales si lo desea. Este enfoque permite toocreate un repositorio de archivos json que, a continuación, se pueden llamar para especificado escenarios.

### <a name="reset-sshd"></a>Restablecer SSHD
Cree un archivo denominado `settings.json` con hello siguen contenido:

```json
{  
    "reset_ssh":"True"
}
```

Con hello CLI de Azure,, a continuación, llame a hello `VMAccessForLinux` extensión tooreset su conexión SSHD especificando el archivo json. Hello siguiente ejemplo se utiliza [conjunto de extensión de vm az](/cli/azure/vm/extension#set) tooreset SSHD en máquina virtual denominada hello `myVM` en `myResourceGroup`. Use sus propios valores, como se indica a continuación:

```azurecli
az vm extension set --resource-group philmea --vm-name Ubuntu \
    --name VMAccessForLinux --publisher Microsoft.OSTCExtensions --version 1.2 --settings settings.json
```

### <a name="reset-ssh-credentials-for-a-user"></a>Restablecimiento de las credenciales de SSH de un usuario
Si SSHD aparece toofunction correctamente, puede restablecer las credenciales de Hola para un usuario giver. contraseña de hello tooreset para un usuario, cree un archivo denominado `settings.json`. Hello en el ejemplo siguiente se restablece las credenciales de Hola para `myUsername` valor toohello especificado en `myPassword`. Escriba Hola siguiendo las líneas en la `settings.json` de archivos, con sus propios valores:

```json
{
    "username":"myUsername", "password":"myPassword"
}
```

O tooreset Hola clave SSH para un usuario, primero cree un archivo denominado `settings.json`. Hello en el ejemplo siguiente se restablece las credenciales de Hola para `myUsername` valor toohello especificado en `myPassword`, en la máquina virtual denominada hello `myVM` en `myResourceGroup`. Escriba Hola siguiendo las líneas en la `settings.json` de archivos, con sus propios valores:

```json
{
    "username":"myUsername", "ssh_key":"mySSHKey"
}
```

Después de crear el archivo json, usar Hola de hello Azure CLI toocall `VMAccessForLinux` tooreset extensión las credenciales de su usuario SSH especificando el archivo json. Hello en el ejemplo siguiente se restablece las credenciales en la máquina virtual denominada hello `myVM` en `myResourceGroup`. Use sus propios valores, como se indica a continuación:

```azurecli
az vm extension set --resource-group philmea --vm-name Ubuntu \
    --name VMAccessForLinux --publisher Microsoft.OSTCExtensions --version 1.2 --settings settings.json
```

## <a name="use-hello-azure-cli-10"></a>Usar hello Azure CLI 1.0
Si no lo ha hecho ya, [instalar Hola 1.0 de CLI de Azure y conectar tooyour suscripción de Azure](../../cli-install-nodejs.md). Asegúrese de que está usando el modo de Resource Manager como se indica:

```azurecli
azure config mode arm
```

Si ha creado y cargado una imagen de disco Linux personalizada, que seguro Hola [agente Linux de Microsoft Azure](../windows/agent-user-guide.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) versión 2.0.5 o posterior está instalado. Para máquinas virtuales creadas mediante imágenes de la galería, esta extensión de acceso ya está instalada y configurada automáticamente.

### <a name="reset-ssh-configuration"></a>Restablecer la configuración de SSH
configuración SSHD Hello en sí puede estar mal configurada u Hola servicio detectó un error. Puede restablecer SSHD toomake seguro de configuración de SSH Hola sí es válida. Restablecer SSHD debe ser Hola primer paso para solucionarlos que realizar.

Hello en el ejemplo siguiente se restablece SSHD en una máquina virtual denominada `myVM` en grupo de recursos de hello llamado `myResourceGroup`. Use sus propios nombres de grupo de recursos y máquina virtual, como se indica a continuación:

```azurecli
azure vm reset-access --resource-group myResourceGroup --name myVM \
    --reset-ssh
```

### <a name="reset-ssh-credentials-for-a-user"></a>Restablecimiento de las credenciales de SSH de un usuario
Si SSHD aparece toofunction correctamente, puede restablecer contraseña de Hola para un usuario giver. Hello en el ejemplo siguiente se restablece las credenciales de Hola para `myUsername` valor toohello especificado en `myPassword`, en la máquina virtual denominada hello `myVM` en `myResourceGroup`. Use sus propios valores, como se indica a continuación:

```azurecli
azure vm reset-access --resource-group myResourceGroup --name myVM \
     --user-name myUsername --password myPassword
```

Si utiliza la autenticación de clave SSH, puede restablecer la clave SSH de Hola para un usuario determinado. Después de las actualizaciones de ejemplo de Hola Hola almacenada en la clave SSH `~/.ssh/id_rsa.pub` con el nombre de usuario de hello `myUsername`, en la máquina virtual denominada hello `myVM` en `myResourceGroup`. Use sus propios valores, como se indica a continuación:

```azurecli
azure vm reset-access --resource-group myResourceGroup --name myVM \
    --user-name myUsername --ssh-key-file ~/.ssh/id_rsa.pub
```


## <a name="restart-a-vm"></a>Reinicio de una máquina virtual
Si dispone de restablecer credenciales de usuario y la configuración de SSH de Hola o encontró un error al hacerlo, puede intentar reiniciar Hola VM tooaddress subyacente problemas de cálculo.

### <a name="azure-portal"></a>Azure Portal
toorestart una VM con hello Azure seleccione portal, el Hola de máquina virtual y haga clic en **reiniciar** botón como en el siguiente ejemplo de Hola:

![Reiniciar una máquina virtual en hello portal de Azure](./media/troubleshoot-ssh-connection/restart-vm-using-portal.png)

### <a name="azure-cli-10"></a>CLI de Azure 1.0
Después de reinicios del ejemplo de Hola Hola máquina virtual denominada `myVM` en grupo de recursos de hello llamado `myResourceGroup`. Use sus propios valores, como se indica a continuación:

```azurecli
azure vm restart --resource-group myResourceGroup --name myVM
```

### <a name="azure-cli-20"></a>CLI de Azure 2.0
Hello siguiente ejemplo se utiliza [reinicio de la máquina virtual de az](/cli/azure/vm#restart) toorestart Hola máquina virtual denominada `myVM` en grupo de recursos de hello llamado `myResourceGroup`. Use sus propios valores, como se indica a continuación:

```azurecli
az vm restart --resource-group myResourceGroup --name myVM
```


## <a name="redeploy-a-vm"></a>Reimplementación de una máquina virtual
Puede volver a implementar un nodo de tooanother de máquina virtual dentro de Azure, que puede corregir los problemas de red subyacentes. Para obtener información acerca de cómo volver a implementar una máquina virtual, consulte [volver a implementar la máquina virtual toonew nodo Azure](../windows/redeploy-to-new-node.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).

> [!NOTE]
> Una vez finalizada esta operación, se perderán los datos de disco efímeros y direcciones IP dinámicas que están asociadas a la máquina virtual de Hola se actualizará.
> 
> 

### <a name="azure-portal"></a>Azure Portal
tooredeploy una VM con hello Azure seleccione portal, la máquina virtual y desplácese hacia abajo toohello **soporte técnico y solución de problemas** sección. Haga clic en hello **volver a implementar** botón como en el siguiente ejemplo de Hola:

![Volver a implementar una máquina virtual en hello portal de Azure](./media/troubleshoot-ssh-connection/redeploy-vm-using-portal.png)

### <a name="azure-cli-10"></a>CLI de Azure 1.0
Después de nuevas implementaciones de ejemplo de Hola Hola máquina virtual denominada `myVM` en grupo de recursos de hello llamado `myResourceGroup`. Use sus propios valores, como se indica a continuación:

```azurecli
azure vm redeploy --resource-group myResourceGroup --name myVM
```

### <a name="azure-cli-20"></a>CLI de Azure 2.0
Hola después de ejemplo de uso [volver a implementar vm de az](/cli/azure/vm#redeploy) tooredeploy Hola máquina virtual denominada `myVM` en grupo de recursos de hello llamado `myResourceGroup`. Use sus propios valores, como se indica a continuación:

```azurecli
az vm redeploy --resource-group myResourceGroup --name myVM
```

## <a name="vms-created-by-using-hello-classic-deployment-model"></a>Máquinas virtuales creadas con el modelo de implementación de hello clásico
Probar estos pasos tooresolve hello más comunes SSH errores de conexión para las máquinas virtuales que se crearon con el modelo de implementación clásica de Hola. Después de cada paso, intente volver a conectarse toohello máquina virtual.

* Restablecer el acceso remoto de hello [portal de Azure](https://portal.azure.com). En Hola portal de Azure, seleccione la máquina virtual y haga clic en hello **restablecer remoto...**  botón.
* Reinicie Hola máquina virtual. En hello [portal de Azure](https://portal.azure.com), seleccione la máquina virtual y haga clic en hello **reiniciar** botón.
    
* Volver a implementar nodos de Azure nuevo tooa Hola máquina virtual. Para obtener información acerca de cómo tooredeploy una máquina virtual, consulte [volver a implementar la máquina virtual toonew nodo Azure](../windows/redeploy-to-new-node.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).
  
    Una vez finalizada esta operación, se perderán los datos de disco efímeros y direcciones IP dinámicas que están asociadas a la máquina virtual de Hola se actualizará.
* Siga las instrucciones de hello en [cómo tooreset una contraseña o SSH para máquinas virtuales basadas en Linux](classic/reset-access.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json) para:
  
  * Hola de restablecimiento de contraseña o clave SSH.
  * Crear una nueva cuenta de usuario de *sudo*.
  * Restablecer configuración de SSH de Hola.
* Compruebe el estado de los recursos de máquina virtual de Hola para cualquier problema de plataforma.<br>
     Seleccione la máquina virtual y desplácese hacia abajo hasta **Configuración** > **Comprobar estado**.

## <a name="additional-resources"></a>Recursos adicionales
* Si se sigue sin tooSSH tooyour VM después de Hola siguiente después de los pasos, consulte [más pasos para solucionar problemas](detailed-troubleshoot-ssh-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) tooreview adicional pasos tooresolve su problema.
* Para obtener más información sobre cómo solucionar problemas de acceso a la aplicación, consulte [aplicación tooan solucionar access que ejecuta en una máquina virtual de Azure](../windows/troubleshoot-app-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* Para obtener más información sobre cómo solucionar problemas de máquinas virtuales que se crearon con el modelo de implementación clásica de hello, consulte [cómo tooreset una contraseña o SSH para máquinas virtuales basadas en Linux](classic/reset-access.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json).

