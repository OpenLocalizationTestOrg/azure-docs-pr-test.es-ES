---
title: 'aaaScale los roles de trabajo de servicios de aplicaciones: pila de Azure | Documentos de Microsoft'
description: Instrucciones detalladas de escalado de App Services en Azure Stack
services: azure-stack
documentationcenter: 
author: kathm
manager: slinehan
editor: anwestg
ms.assetid: 3cbe87bd-8ae2-47dc-a367-51e67ed4b3c0
ms.service: azure-stack
ms.workload: app-service
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 4/6/2017
ms.author: kathm
ms.openlocfilehash: 252b4a531655e38f3a3747f8a04b16fc6303f9e1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="app-service-on-azure-stack-adding-more-worker-roles"></a>App Service en Azure Stack: incorporación de más roles de trabajo 

Este documento proporciona instrucciones sobre cómo tooscale servicio de aplicaciones en roles de trabajador de la pila de Azure. Contiene pasos para crear aplicaciones de toosupport de roles de trabajo adicional de cualquier tamaño.

> [!NOTE]
> Si su entorno de prueba de concepto de Azure Stack no tiene más de 96 GB de RAM, puede encontrar dificultades al agregar capacidad adicional.

App Service en Azure Stack, de forma predeterminada, es compatible con los niveles de trabajo gratuito y compartido. tooadd otros niveles de trabajo, deberá tooadd más roles de trabajo.

Si no estás seguro de lo que se implementó no tiene valor predeterminado de hello servicio de aplicaciones en la instalación de la pila de Azure, puede revisar la información adicional de hello [servicio de aplicaciones en información general de la pila de Azure](azure-stack-app-service-overview.md).

Hay dos maneras tooadd capacidad adicional tooApp servicio en la pila de Azure:
1.  [Agregar trabajos adicionales directamente desde con dentro de hello App Admin de proveedor de recursos de servicio](#Add-additional-workers-directly-from-within-the-App-Service-Resource-Provider-Admin).
2.  [Crear máquinas virtuales adicionales manualmente y agregarlas toohello proveedor de recursos de servicio de aplicación](#Create-additional-VMs-manually-and-add-them-to-the-App-Service-Resource-Provider).

## <a name="add-additional-workers-directly-within-hello-app-service-resource-provider-admin"></a>Agregar trabajos adicionales directamente dentro de hello administrador. proveedor de recursos de servicio de aplicación

1.  Inicie sesión en toohello portal de la pila de Azure como administrador de servicios de hello;
2.  Examinar demasiado**proveedores de recursos** y seleccione hello **App Admin de proveedor de recursos de servicio**. ![Proveedores de recursos de Azure Stack][1]
3.  Haga clic en **Roles**.  Aquí verá desglose de Hola de todos los roles de servicio de aplicaciones implementadas.
4.  Haga clic en la opción de hello **nueva instancia de rol** ![agregar una nueva instancia de rol][2]
5.  Hola **nueva instancia de rol** hoja:
    1. Elija cuántos adicionales **instancias de rol** le gustaría tooadd.  En la vista previa de hello, hay un máximo de 10.
    2. Seleccione hello **tipo de función**.  En esta versión preliminar, esta opción está limitada tooWeb trabajo.
    3. Seleccione hello **nivel de trabajo** le gustaría toodeploy este trabajo en, las opciones predeterminadas son pequeño, mediano, grande o compartido.  Si ha creado sus propios niveles de trabajo, también estarán disponibles para la selección.
    4. Haga clic en **Aceptar** toodeploy Hola los trabajadores adicionales
6.  Servicio de aplicaciones de voluntad de pila de Azure ahora agregar Hola máquinas virtuales adicionales, configurarlos, instalar todo el software necesario de Hola y marcarlos como preparado para cuando se complete este proceso.  que puede tardar unos 80 minutos.
7.  Puede supervisar el progreso de Hola de preparación de Hola de nuevos subprocesos de trabajo Hola viendo los trabajadores de hello en hello **roles** hoja.

>[!NOTE]
>  En esta versión preliminar, hello integrado flujo de la nueva instancia de rol es limitado tooWorker Roles e implementar máquinas virtuales de tamaño A1.  Esta funcionalidad se ampliará en una versión futura.

## <a name="manually-adding-additional-capacity-tooapp-service-on-azure-stack"></a>Cómo agregar manualmente una capacidad adicional tooApp servicio en la pila de Azure.

Hello pasos siguientes son roles adicionales tooadd necesarios:

1. [Creación de una máquina virtual](#step-1-create-a-new-vm-to-support-the-new-instance-size)
2. [Configurar la máquina virtual de Hola](#step-2-configure-the-virtual-machine)
3. [Configure el rol de trabajador de web de hello en el portal de Azure pila Hola](#step-3-configure-the-web-worker-role-in-the-azure-stack-portal)
4. [Configuración de los planes de App Service](#step-4-configure-app-service-plans)

## <a name="step-1-create-a-new-vm-toosupport-hello-new-instance-size"></a>Paso 1: Crear un nueva VM toosupport Hola nuevo tamaño de instancia
Crear una máquina virtual como se describe en [este artículo](azure-stack-provision-vm.md), asegurándose de que siguiente Hola se realizan las selecciones:

* Nombre de usuario y contraseña: proporcionar Hola el mismo nombre de usuario y contraseña que especificó al instalar el servicio de aplicaciones en la pila de Azure.
* Suscripción: Suscripción de proveedor Use Hola predeterminada.
* Grupo de recursos: elija **AppService-LOCAL**.

> [!NOTE]
> Almacenar máquinas virtuales de Hola para roles de trabajo en hello al mismo grupo de recursos como servicio de aplicaciones en la pila de Azure se implementa en. (recomendación para esta versión).
> 
> 

## <a name="step-2-configure-hello-virtual-machine"></a>Paso 2: Configurar Hola Máquina Virtual
Cuando haya completado la implementación de hello, Hola siguiente configuración es rol de trabajo de toosupport necesario hello web:

1. Examinar toohello **AppService LOCAL** grupo de recursos en el portal de Hola y máquina nueva Hola select que creó en el paso 1.
2. Haga clic en conectar en hello VM hoja toodownload Hola escritorio perfil remoto.  Abra Hola perfil tooopen una VM de tooyour de sesión de escritorio remoto.
3. Inicie sesión en toohello VM con hello de usuario y contraseña que especificó en el paso 1.
4. Abra PowerShell haciendo clic en hello **iniciar** botón y escribiendo PowerShell. Haga clic en **PowerShell.exe**y seleccione **ejecutar como administrador** tooopen PowerShell en modo de administrador.
5. Copia y pegado de hello después de comandos (uno en uno) en la ventana de PowerShell de hello y presione ENTRAR:
   
   ```netsh advfirewall firewall set rule group="File and Printer Sharing" new enable=Yes```
   ```netsh advfirewall firewall set rule group="Windows Management Instrumentation (WMI)" new enable=yes```
   ```reg add HKLM\\SOFTWARE\\Microsoft\\Windows\\CurrentVersion\\Policies\\system /v LocalAccountTokenFilterPolicy /t REG\_DWORD /d 1 /f```
   
6. Cierre la sesión de escritorio remoto.
7. Reinicie Hola VM desde el portal de Hola.

> [!NOTE]
> Estos son los requisitos mínimos para App Service en Azure Stack. Son valores predeterminados de Hola de imagen de Windows 2012 R2 de hello incluida en la pila de Azure. se han proporcionado instrucciones Hello en el futuro y para los usuarios que utilicen otra imagen.
> 
> 

## <a name="step-3-configure-hello-worker-role-in-hello-azure-stack-portal"></a>Paso 3: Configurar el rol de trabajo de hello en el portal de Azure pila Hola
1. Portal de hello abra como administrador de servicios de hello en **ClientVM**.
2. Navegue demasiado**proveedores de recursos** &gt; **App Admin de proveedor de recursos de servicio**.![ Administración de proveedor de recursos de servicio de aplicaciones][3]
3. En la hoja de configuración de hello, haga clic en **Roles**.![ Roles de proveedor de recursos de servicio de aplicaciones][4]
4. Haga clic en **Agregar instancia de rol**.
5. En el cuadro de texto de Hola para **nombre del servidor** escriba hello **dirección IP** de servidor de Hola que creó anteriormente (en la sección 1).
6. Seleccione hello **tipo de rol** le gustaría tooadd - controlador, servidor de administración, Front-End, trabajo Web, publicador o servidor de archivos.  En este caso, seleccione Trabajo web.
7. Haga clic en hello **capa** para sería como toodeploy Hola de nuevo la instancia de demasiado (pequeño, mediano, grande o compartido).  Si ha creado sus propios niveles de trabajo, también estarán disponibles para la selección.
8. Haga clic en **Aceptar**.
9. Volver atrás toohello **Roles** vista
10. Haga clic en hello fila correspondiente toohello combinación de tipo de función y nivel de trabajo que asignó la máquina virtual a.
11. Busque Hola nombre del servidor que acaba de agregar. Revise la columna de estado de Hola y espere toomove toohello siguiente paso hasta que el estado de hello es "Listo". esto puede tardar unos 80 minutos. ![Rol de proveedor de recursos de App Service listo][5]

## <a name="step-4-configure-app-service-plans"></a>Paso 4: Configuración de los planes de App Service

1. Inicie sesión en el portal de toohello en hello ClientVM.
2. Navegue demasiado**New** &gt; **Web y móviles**.
3. Seleccione el tipo de saludo de aplicación le gustaría toodeploy.
4. Proporcionar información de hello para la aplicación hello y, a continuación, seleccione **Plan de servicio de aplicaciones / ubicación**.
    1. Haga clic en **Create New**.
    2. Crear un plan, seleccione tarifa correspondiente hello para el plan de Hola.

> [!NOTE]
> Puede crear varios planes en esta hoja. Antes de implementar, sin embargo, asegúrese de que seleccionó un plan adecuado de Hola.
> 
> 

Hola continuación muestra un ejemplo de Hola varios niveles de precios disponibles de forma predeterminada.  Observe que si no hay ningún trabajador disponibles para un nivel de trabajo concreto, Hola Hola de toochoose opción correspondiente nivel de precios no está disponible.![Planes de tarifa predeterminados para App Service en Azure Stack][6]

<!--Image references-->
[1]: ./media/azure-stack-app-service-add-worker-roles/azure-stack-resource-providers.png
[2]: ./media/azure-stack-app-service-add-worker-roles/app-service-new-role-instance.png
[3]: ./media/azure-stack-app-service-add-worker-roles/app-service-resource-provider-admin.png
[4]: ./media/azure-stack-app-service-add-worker-roles/app-service-resource-provider-roles.png
[5]: ./media/azure-stack-app-service-add-worker-roles/app-service-resource-provider-role-ready.png
[6]: ./media/azure-stack-app-service-add-worker-roles/app-service-resource-provider-pricing-tier.png
