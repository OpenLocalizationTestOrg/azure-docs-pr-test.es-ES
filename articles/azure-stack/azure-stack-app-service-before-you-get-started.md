---
title: aaaBefore implementar el servicio de aplicaciones en la pila de Azure | Documentos de Microsoft
description: Pasos toocomplete antes de implementar el servicio de aplicaciones en la pila de Azure
services: azure-stack
documentationcenter: 
author: apwestgarth
manager: stefsch
editor: 
ms.assetid: 
ms.service: azure-stack
ms.workload: app-service
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 7/3/2017
ms.author: anwestg
ms.openlocfilehash: fad758232ef2795105036640c2a26abf3fa2c3c8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="before-you-get-started-with-app-service-on-azure-stack"></a>Antes de empezar a trabajar con App Service en Azure Stack

Necesita unos elementos tooinstall servicio de aplicaciones de Azure en la pila de Azure:

- Una implementación completa de hello [kit de desarrollo de Azure pila](azure-stack-run-powershell-script.md).
- Suficiente espacio en el sistema de Azure Stack para una implementación pequeña de App Service en Azure Stack.  Hola se requiere espacio en aproximadamente 20 GB de espacio en disco.
- Una imagen de máquina virtual de Windows Server para usarla al crear máquinas virtuales para App Service en Azure Stack.
- [Un servidor que ejecute SQL Server](#SQL-Server).

>[!NOTE] 
> Hola lo siguiente *todos los* tienen lugar en la máquina de host de hello pila de Azure.

toodeploy un proveedor de recursos, debe ejecutar Hola entorno de Scripting integrado (ISE) de PowerShell como administrador. Por esta razón, necesita tooallow cookies y JavaScript de perfil de Internet Explorer de Hola que usas toosign en tooAzure Active Directory.

## <a name="turn-off-internet-explorer-enhanced-security"></a>Desactivación de la seguridad mejorada de Internet Explorer

1.  Inicie sesión en el equipo de kit de desarrollo de pila de Azure de toohello como **AzureStack/administrador**y, a continuación, abra **el administrador del servidor**.

2.  Desactive la **Configuración de seguridad mejorada de Internet Explorer** para los administradores y usuarios.

3.  Inicie sesión en el equipo de kit de desarrollo de toohello pila de Azure como administrador y, a continuación, abra **el administrador del servidor**.

4.  Desactive la **Configuración de seguridad mejorada de Internet Explorer** para los administradores y usuarios.

## <a name="enable-cookies"></a>Habilitación de las cookies

1.  Seleccione **Inicio** > **Todas las aplicaciones** > **Accesorios de Windows**. Haga clic con el botón derecho en **Internet Explorer** > **Más** > **Ejecutar como administrador**.

2.  Si se le pide, seleccione **Use recommended security** (Usar seguridad recomendada) y, a continuación, seleccione **Aceptar**.

3.  En Internet Explorer, seleccione **herramientas** (icono de engranaje de hello) > **opciones de Internet** > **privacidad** > **avanzadas**.

4.  Seleccione **Advanced** (Avanzadas). Asegúrese de que las dos casillas **Aceptar** estén activadas. Seleccione **Aceptar** dos veces.

5.  Cierre Internet Explorer y reinicie Hola PowerShell ISE como administrador.

## <a name="install-powershell-for-azure-stack"></a>Instalación de PowerShell para Azure Stack

tooinstall PowerShell para la pila de Azure, siga los pasos de hello en [instale PowerShell](azure-stack-powershell-install.md).

## <a name="use-visual-studio-with-azure-stack"></a>Uso de Visual Studio con Azure Stack

toouse Visual Studio con la pila de Azure, siga los pasos de hello en [instalar Visual Studio](azure-stack-install-visual-studio.md).

## <a name="add-a-windows-server-2016-vm-image-tooazure-stack"></a>Agregar un tooAzure de imagen de máquina virtual de Windows Server 2016 pila

Puesto que App Service implementa varias máquinas virtuales, requiere una imagen de máquina virtual de Windows Server 2016 en Azure Stack. tooinstall una imagen de máquina virtual, siga los pasos de hello en [agregar una imagen de máquina virtual predeterminada](azure-stack-add-default-image.md).

## <a name="SQL-Server"></a>SQL Server

Servicio de aplicaciones en la pila de Azure requiere acceso tooa SQL Server instancia toocreate y host dos bases de datos toorun Hola proveedor de recursos de servicio de aplicaciones.  Si decide toodeploy una VM de SQL Server en la pila de Azure debe tener el nivel de conectividad SQL Hola establecido demasiado**público**.  Puede elegir toouse de instancia de SQL Server de hello al completar las opciones de Hola Hola servicio de aplicaciones en el instalador de la pila de Azure.

## <a name="next-steps"></a>Pasos siguientes

- [Instalar el proveedor de recursos de servicio de aplicaciones de hello](azure-stack-app-service-deploy.md).

<!--Image references-->
[1]: ./media/azure-stack-app-service-before-you-get-started/PSGallery.png
[2]: ./media/azure-stack-app-service-before-you-get-started/WebPI_InstalledProducts.png
