---
title: "aaaAzure inicio rápido: crear un Portal de VM de Windows | Documentos de Microsoft"
description: "Inicio rápido de Azure: creación de máquinas virtuales Windows con el Portal"
services: virtual-machines-windows
documentationcenter: virtual-machines
author: neilpeterson
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure
ms.date: 07/15/2017
ms.author: nepeters
ms.custom: mvc
ms.openlocfilehash: 5646ad51244db6d214c0121d1f7cc45c59f9a78b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-windows-virtual-machine-with-hello-azure-portal"></a>Crear una máquina virtual de Windows con hello portal de Azure

Máquinas virtuales de Azure se pueden crear a través de hello portal de Azure. Este método proporciona una interfaz de usuario basada en el explorador para crear y configurar máquinas virtuales y todos los recursos asociados. Este inicio rápido recorre crear una máquina virtual e instalar un servidor Web en hello máquina virtual.

Si no tiene una suscripción a Azure, cree una [cuenta gratuita](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) antes de empezar.

## <a name="log-in-tooazure"></a>Inicie sesión en tooAzure

Inicie sesión en toohello portal de Azure en http://portal.azure.com.

## <a name="create-virtual-machine"></a>Create virtual machine

1. Haga clic en hello **New** encontró el botón en la esquina izquierda superior de Hola de hello portal de Azure.

2. Seleccione **Compute**y, después, seleccione **Windows Server 2016 Datacenter**. 

3. Escriba la información de la máquina virtual de Hola. nombre de usuario de Hello y una contraseña escritos aquí es toolog usado en la máquina virtual de toohello. Cuando haya terminado, haga clic en **Aceptar**.

    ![Especificar información básica acerca de la máquina virtual en la hoja de portal de Hola](./media/quick-create-portal/create-windows-vm-portal-basic-blade.png)  

4. Seleccione un tamaño para hello máquina virtual. toosee tamaños más, seleccione **todas las ver** o cambiar hello **admite el tipo de disco** filtro. 

    ![Captura de pantalla que muestra los tamaños de máquina virtual](./media/quick-create-portal/create-windows-vm-portal-sizes.png)  

5. En la hoja de configuración de hello, mantenga los valores predeterminados de Hola y haga clic en **Aceptar**.

6. En la página de resumen de hello, haga clic en **Aceptar** implementación de máquina virtual de toostart Hola.

7. Hola VM será toohello anclado Azure panel del portal. Cuando haya completado la implementación de hello, hoja de resumen de VM de Hola se abre automáticamente.


## <a name="connect-toovirtual-machine"></a>Conectar máquina toovirtual

Crear una máquina virtual de toohello de conexión a Escritorio remoto.

1. Haga clic en hello **conectar** botón de propiedades de la máquina virtual de Hola. Se crea y se descarga un archivo de Protocolo de Escritorio remoto (archivo .rdp).

    ![Portal 9](./media/quick-create-portal/quick-create-portal/portal-quick-start-9.png) 

2. tooconnect tooyour máquina virtual, abra Hola descarga archivo RDP. Cuando se le solicite, haga clic en **Conectar**. En un equipo Mac, necesita un cliente RDP como este [cliente de escritorio remoto](https://itunes.apple.com/us/app/microsoft-remote-desktop/id715768417?mt=12) de hello Mac App Store.

3. Escriba el nombre de usuario de Hola y la contraseña que especificó al crear la máquina virtual de hello, a continuación, haga clic en **Aceptar**.

4. Recibirá una advertencia de certificado durante el proceso de inicio de sesión Hola. Haga clic en **Sí** o **continuar** tooproceed con conexión Hola.


## <a name="install-iis-using-powershell"></a>Instalación de IIS mediante PowerShell

En la máquina virtual de hello, iniciar una sesión de PowerShell y ejecute hello después comando tooinstall IIS.

```powershell
Install-WindowsFeature -name Web-Server -IncludeManagementTools
```

Cuando haya finalizado, salga de la sesión RDP de Hola y devolver propiedades de la máquina virtual de Hola Hola portal de Azure.

## <a name="open-port-80-for-web-traffic"></a>Apertura del puerto 80 para el tráfico web 

Los grupos de seguridad de red (NSG) protegen el tráfico entrante y saliente. Cuando se crea una máquina virtual de hello portal de Azure, se crea una regla de entrada en el puerto 3389 para las conexiones RDP. Debido a esta máquina virtual hospeda un servidor Web, una regla de NSG necesario toobe creado para el puerto 80.

1. En la máquina virtual de hello, haga clic en nombre de Hola de hello **grupo de recursos**.
2. Seleccione hello **grupo de seguridad de red**. Hello NSG puede identificarse mediante el uso hello **tipo** columna. 
3. En el menú izquierdo de hello, en configuración, haga clic en **reglas de seguridad de entrada**.
4. Haga clic en **Agregar**.
5. En **Nombre**, escriba **http**. Asegúrese de que **intervalo de puertos** se establece too80 y **acción** se establece demasiado**permitir**. 
6. Haga clic en **Aceptar**.


## <a name="view-hello-iis-welcome-page"></a>Hola de vista Página de bienvenida de IIS

Con IIS instalado y el puerto 80 abra tooyour VM, Hola webserver ahora puede tener acceso desde Hola internet. Abra un explorador web y escriba la dirección IP pública de Hola de hello máquina virtual. la dirección IP pública Hola puede encontrarse en la hoja de la máquina virtual de Hola Hola portal de Azure.

![Sitio predeterminado de IIS](./media/quick-create-powershell/default-iis-website.png) 

## <a name="clean-up-resources"></a>Limpieza de recursos

Cuando ya no es necesario, eliminar el grupo de recursos de hello, máquina virtual y todos los recursos relacionados. toodo por lo tanto, seleccione el grupo de recursos de Hola de hoja de la máquina virtual de Hola y haga clic en **eliminar**.

## <a name="next-steps"></a>Pasos siguientes

En esta guía de inicio rápido, ha implementado una máquina virtual simple y una regla de grupo de seguridad de red, y ha instalado un servidor web. toolearn más información acerca de máquinas virtuales de Azure, continuar con tutorial toohello para máquinas virtuales de Windows.

> [!div class="nextstepaction"]
> [Tutoriales de máquinas virtuales Windows de Azure](./tutorial-manage-vm.md)
