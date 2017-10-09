---
title: aaaEnable FTP en el servicio de aplicaciones en la pila de Azure | Documentos de Microsoft
description: Pasos toocomplete tooenable FTP en el servicio de aplicaciones en la pila de Azure
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
ms.date: 4/6/2017
ms.author: anwestg
ms.openlocfilehash: 9c02da6362085fdd9f8d285da04efe85cf352398
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="enable-ftp-in-app-service-on-azure-stack"></a>Habilitación del FTP en App Service en Azure Stack

Una vez que ha implementado correctamente el servicio de aplicaciones en la pila de Azure si desea que la publicación tooenable FTP, para que los inquilinos pueden cargar sus archivos de la aplicación y el contenido, hay algunos pasos adicionales que necesitan toobe completado.  Estos pasos se automatizarán en futuras versiones.

> [!NOTE]
> Además, están dirigidos a los administradores de empresas o servicios que configuran una instancia de App Service en el proveedor de recursos de Azure Stack.

## <a name="enable-ftp"></a>Habilitación del FTP

1.  Inicie sesión en el portal de Azure pila toohello como administrador de servicios de Hola.
2.  Examinar demasiado**interfaces de red** seleccione hello y **FTP NIC** en **grupo de recursos** - **AppService LOCAL**. ![Interfaces de red de Azure Stack][1]
3.  Hola Nota **dirección IP pública** de hello **FTP NIC**. 
![Detalles de la interfaz de red de Azure Stack][2]
4.  A continuación vaya demasiado**máquinas virtuales** y seleccione hello **FTP0-VM**. ![Máquinas virtuales de Azure Stack][3]
5.  Abra una VM de toohello de sesión de escritorio remoto con hello **conectar** sesión de toohello botón e inicie sesión con credenciales de administrador de hello establecido durante la implementación del servicio de aplicación.  
![Detalles de la máquina virtual de Azure Stack][4]
6.  Abra **servicios de Internet Information Server (IIS) Manager** en hello FTP VM (FTP0-VM).
7.  En **Sitios**, seleccione **Hospedaje de sitio FTP**.
8.  Abra **Compatibilidad con el FTP Firewall**. ![Administrador de IIS en la máquina virtual FTP0-VM de App Service][5]
9.  Escriba Hola dirección IP pública de hello NIC de FTP y haga clic en **aplicar** ![soporte de Firewall de FTP de IIS Manager][6]

## <a name="validate-hello-enabling-of-ftp"></a>Validar Hola habilitación de FTP

1.  Inicie sesión en toohello portal de Azure pila como cualquier administrador de servicios de Hola o como un inquilino.
2.  Examinar demasiado**servicios de aplicaciones** y seleccione una Web, móviles o App API que haya creado. ![App Services][7]
3.  En la aplicación hello detalles Observe hello **nombre de host FTP** y **nombre de usuario FTP e implementación**. ![Detalles de la aplicación de App Service][8]
> [!NOTE]
> Si no ve una entrada en **nombre de usuario FTP e implementación**, necesita las credenciales de implementación de hello tooset usar primero Hola **las credenciales de implementación** hoja.

4.  Abra el Explorador de Windows, escriba el nombre de host de hello FTP en dirección del archivo hello barra ftp://ftp.appservice.azurestack.local por ejemplo,
5.  Cuando se le solicite escribir hello **las credenciales de implementación** que anotó en el paso 3, si se ha habilitado la característica de hello, verá una lista de directorios de contenido de la aplicación de servicio de aplicación Hola. ![Lista de archivos de FTP][9]
<!--Image references-->
[1]: ./media/azure-stack-app-service-enable-ftp/azure-stack-app-service-enable-ftp-network-interfaces.png
[2]: ./media/azure-stack-app-service-enable-ftp/azure-stack-app-service-enable-ftp-network-interface-details.png
[3]: ./media/azure-stack-app-service-enable-ftp/azure-stack-app-service-enable-ftp-virtual-machines.png
[4]: ./media/azure-stack-app-service-enable-ftp/azure-stack-app-service-enable-ftp-virtual-machines-FTP0-VM.png
[5]: ./media/azure-stack-app-service-enable-ftp/azure-stack-app-service-enable-ftp-IIS-Manager.png
[6]: ./media/azure-stack-app-service-enable-ftp/azure-stack-app-service-enable-ftp-IIS-Manager-FTP-Firewall-Support.png
[7]: ./media/azure-stack-app-service-enable-ftp/azure-stack-app-service-enable-ftp-validate-app-services.png
[8]: ./media/azure-stack-app-service-enable-ftp/azure-stack-app-service-enable-ftp-validate-app-service-app-detail.png
[9]: ./media/azure-stack-app-service-enable-ftp/azure-stack-app-service-enable-ftp-validate-ftp-file-listing.png
