---
title: aaaInstall IIS en su primera VM de Windows | Documentos de Microsoft
description: "Experimentar con la primera máquina virtual de Windows mediante la instalación de IIS y abrir el puerto 80 mediante Hola portal de Azure."
keywords: 
services: virtual-machines-windows
documentationcenter: 
author: cynthn
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 6334ea45-db6b-4e08-abb5-1f98927ebc34
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 09/06/2016
ms.author: cynthn
ms.openlocfilehash: 7cfed6197df058c4569d111ee88961da7c6fe0b3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="experiment-with-installing-a-role-on-your-windows-vm"></a>Experimentación con la instalación de un rol en la máquina virtual Windows
Una vez que la máquina virtual (VM) la primera y en ejecución, puede mover en tooinstalling software y los servicios. Para este tutorial, vamos toouse administrador del servidor en VM de Windows Server de hello tooinstall IIS. A continuación, se creará un grupo de seguridad de red (NSG) mediante el puerto 80 tooIIS tráfico de hello tooopen de portal de Azure. 

Si aún no ha creado su primera máquina virtual, debe volver atrás demasiado[crear la primera máquina virtual de Windows en el portal de Azure hello](../virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) antes de continuar con este tutorial.

## <a name="make-sure-hello-vm-is-running"></a>Asegúrese de Hola que está ejecutando la máquina virtual
1. Abra hello [portal de Azure](https://portal.azure.com).
2. En el menú del concentrador hello, haga clic en **máquinas virtuales**. Seleccione la máquina virtual de Hola de lista de Hola.
3. Si el estado de hello es **detenido (desasignado)**, haga clic en hello **iniciar** botón en hello **Essentials** hoja de hello máquina virtual. Si el estado de hello es **ejecuta**, puede mover en toohello siguiente paso.

## <a name="connect-toohello-virtual-machine-and-sign-in"></a>Conectar máquina virtual de toohello e inicie sesión en
1. En el menú del concentrador hello, haga clic en **máquinas virtuales**. Seleccione la máquina virtual de Hola de lista de Hola.
2. En la hoja de hello para la máquina virtual de hello, haga clic en **conectar**. Esto crea y descarga un archivo de protocolo de escritorio remoto (archivo .rdp) que es similar a una máquina de tooyour tooconnect de método abreviado. Podría desea toosave Hola archivo tooyour escritorio para facilitar el acceso. **Abra** esta tooyour de tooconnect archivo máquina virtual.
   
    ![Captura de pantalla de hello Azure portal que se muestra cómo tooconnect tooyour VM](./media/hero-role/connect.png)
3. Obtendrá una advertencia que .rdp hello es de un publicador desconocido. Esto es normal. En la ventana de escritorio remoto de hello, haga clic en **conectar** toocontinue.
   
    ![Captura de pantalla de una advertencia sobre un editor desconocido](./media/hero-role/rdp-warn.png)
4. En la ventana de la seguridad de Windows hello, el nombre de usuario de tipo hello y la contraseña de cuenta local de Hola que creó al crear Hola máquina virtual. se ha introducido el nombre de usuario de Hello *vmname*&#92; *nombre de usuario*, a continuación, haga clic en **Aceptar**.
   
    ![Captura de pantalla de escribir el nombre de la máquina virtual de hello, nombre de usuario y contraseña](./media/hero-role/credentials.png)
5. Obtendrá una advertencia no se puede comprobar que el certificado Hola. Esto es normal. Haga clic en **Sí** tooverify Hola identidad de máquina virtual de Hola y finalizar la sesión.
   
   ![Captura de pantalla muestra un mensaje acerca de la verificación de identidad de Hola de hello VM](./media/hero-role/cert-warning.png)

Si se ejecuta en tootrouble cuando intente tooconnect, consulte [tooa de conexiones de escritorio remoto solucionar problemas de máquina Virtual de Azure basado en Windows](troubleshoot-rdp-connection.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).

## <a name="install-iis-on-your-vm"></a>Instalación de IIS en la máquina virtual
Ahora que ha iniciado sesión toohello VM, se instalará un rol de servidor para que pueda experimentar más.

1. Abra el **Administrador del servidor** si aún no está abierto. Haga clic en hello **iniciar** menú y, a continuación, haga clic en **el administrador del servidor**.
2. En **el administrador del servidor**, seleccione **servidor Local** en el panel izquierdo de Hola. 
3. En el menú de hello, seleccione **administrar** > **agregar Roles y características**.
4. En Administrador de hello agregar Roles y características, en hello **tipo de instalación** página, elija **instalación basada en roles o basada en características**y, a continuación, haga clic en **siguiente**.
   
    ![Pestaña captura de pantalla que muestra hello Agregar administrador de Roles y características de tipo de instalación](./media/hero-role/role-wizard.png)
5. Seleccione Hola VM Hola grupo de servidores y haga clic en **siguiente**.
6. En hello **Roles de servidor** página, seleccione **servidor Web (IIS)**.
   
    ![Pestaña captura de pantalla que muestra hello agregar Roles y características Asistente para Roles de servidor](./media/hero-role/add-iis.png)
7. Hola emergente acerca de cómo agregar características necesarias para IIS, asegúrese de que **incluir herramientas de administración** está seleccionada y, a continuación, haga clic en **agregar características**. Cuando se cierra Hola emergente, haga clic en **siguiente** Asistente Hola.
   
    ![Captura de pantalla muestra tooconfirm emergente Agregar rol IIS de Hola](./media/hero-role/confirm-add-feature.png)
8. En la página de características de hello, haga clic en **siguiente**.
9. En hello **rol de servidor Web (IIS)** página, haga clic en **siguiente**. 
10. En hello **servicios de rol** página, haga clic en **siguiente**. 
11. En hello **confirmación** página, haga clic en **instalar**. 
12. Una vez completada la instalación de hello, haga clic en **cerrar** Asistente Hola.

## <a name="open-port-80"></a>Apertura del puerto 80
En orden para la máquina virtual tooaccept el tráfico entrante en el puerto 80, deberá tooadd un grupo de seguridad de red de toohello de regla de entrada. 

1. Abra hello [portal de Azure](https://portal.azure.com).
2. En **máquinas virtuales** seleccione Hola máquina virtual que ha creado.
3. En configuración de máquinas virtuales de hello, seleccione **interfaces de red** y, a continuación, seleccione Hola interfaz de red existente.
   
    ![Captura de pantalla muestra a la configuración de máquina virtual de Hola para hello interfaces de red](./media/hero-role/network-interface.png)
4. En **Essentials** de interfaz de red de hello, haga clic en hello **grupo de seguridad de red**.
   
    ![Captura de pantalla muestra la sección de Essentials Hola de interfaz de red de Hola](./media/hero-role/select-nsg.png)
5. Hola **Essentials** hoja para hello NSG, debe tener un valor predeterminado existente regla de entrada de **rdp permitir predeterminado** que permite toolog en toohello máquina virtual. Va a agregar otro tráfico IIS de tooallow de regla de entrada. Haga clic en **Regla de seguridad de entrada**.
   
    ![Captura de pantalla muestra la sección de Essentials de Hola para hello NSG](./media/hero-role/inbound.png)
6. En **Reglas de seguridad de entrada**, haga clic en **Agregar**.
   
    ![Captura de pantalla muestra hello botón tooadd una regla de seguridad](./media/hero-role/add-rule.png)
7. En **Reglas de seguridad de entrada**, haga clic en **Agregar**. Tipo de **80** en Hola intervalo de puertos y asegúrese de que **permitir** está seleccionada. Cuando haya terminado, haga clic en **Aceptar**.
   
    ![Captura de pantalla muestra hello botón tooadd una regla de seguridad](./media/hero-role/port-80.png)

Para obtener más información acerca de los NSG, las reglas entrantes y salientes, vea [permitir acceso externo tooyour VM con Hola portal de Azure](nsg-quickstart-portal.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)

## <a name="connect-toohello-default-iis-website"></a>Conectar el sitio Web IIS de toohello predeterminado
1. Hola portal de Azure, haga clic en **máquinas virtuales** y, a continuación, seleccione la máquina virtual.
2. Hola **Essentials** hoja, copie su **dirección IP pública**.
   
    ![Captura de pantalla muestra donde toofind Hola dirección IP pública de la máquina virtual](./media/hero-role/ipaddress.png)
3. Abra un explorador y en la barra de direcciones de hello, escriba la dirección IP pública similar al siguiente: http://<publicIPaddress> y haga clic en **ENTRAR** toogo toothat dirección.
4. El explorador debe abrir la página de web IIS predeterminada de Hola. Se parece a lo siguiente:
   
    ![Captura de pantalla muestra qué página IIS predeterminada Hola aspecto en un explorador](./media/hero-role/iis-default.png)

## <a name="next-steps"></a>Pasos siguientes
* También puede experimentar con [adjuntar un disco de datos](attach-disk-portal.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) tooyour virtual machine. Los discos de datos proporcionan más espacio de almacenamiento para la máquina virtual.

