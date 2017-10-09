---
title: "Instalación de funciones en tiempo de ejecución aaaAzure | Documentos de Microsoft"
description: "¿Cómo tooInstall Hola en tiempo de ejecución de funciones de Azure"
services: functions
documentationcenter: 
author: apwestgarth
manager: stefsch
editor: 
ms.assetid: 
ms.service: functions
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: multiple
ms.topic: article
ms.date: 05/08/2017
ms.author: anwestg
ms.openlocfilehash: 67c6d10b5c0ac43e880d29cff0ae7b099f82bdb5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="install-hello-azure-functions-runtime-preview"></a>Instalar Hola vista previa en tiempo de ejecución de funciones de Azure

Si desea que la vista previa de tooinstall hello en tiempo de ejecución de funciones de Azure, debe seguir estos pasos:

1. Asegúrese de que el equipo pasa los requisitos mínimos de Hola
1. Descargar hello [instalador de vista previa de Azure funciones en tiempo de ejecución](https://aka.ms/azafr). 
1. Instalar vista previa de hello en tiempo de ejecución de funciones de Azure
1. Configuración de hello completa de una vista previa de hello en tiempo de ejecución de funciones de Azure

## <a name="prerequisites"></a>Requisitos previos

Antes de instalar hello en tiempo de ejecución de funciones de Azure preview, debe tener el siguiente hello:

1. Un máquina donde se ejecute Microsoft Windows Server 2016 o Microsoft Windows 10 Creators Update (Professional o Enterprise Edition).
1. Una instancia de SQL Server que se ejecute dentro de la red.  El requisito mínimo de edición es SQL Server Express.

## <a name="install-hello-azure-functions-runtime-preview"></a>Instalar Hola vista previa en tiempo de ejecución de funciones de Azure

instalador de vista previa de Hello en tiempo de ejecución de funciones de Azure le guía a través de la instalación de Hola de vista previa en tiempo de ejecución de funciones de Azure de hello administración y Roles de trabajo.  Es posible tooinstall Hola administración y rol de trabajador de hello mismo equipo.  Sin embargo, como agregar más funciones, debe implementar las funciones en varios trabajadores más roles de trabajo en equipos adicionales toobe capaz de tooscale.

## <a name="install-hello-management-and-worker-role-on-hello-same-machine"></a>Instalar Administración de Hola y rol de trabajo en hello mismo equipo

1. Ejecute hello instalador de vista previa de Azure funciones en tiempo de ejecución.

    ![Instalador de la versión preliminar del Sistema en ejecución de Azure Functions][1]

1. **Haga clic en siguiente** avanzar más allá de hello primera fase del instalador de Hola
1. Una vez que haya leído los términos de Hola de hello **CLUF**, **casilla hello** tooaccept términos de Hola y **haga clic en siguiente** tooadvance.
1. Ahora seleccione Hola roles desea tooinstall en esta máquina **rol de administración de funciones** o **rol de trabajo de funciones** y **haga clic en siguiente**

    ![Instalador de la versión preliminar del Sistema en ejecución de Azure Functions: selección de roles][3]

    > [!NOTE]
    > Puede instalar hello **rol de trabajo de funciones** en muchos otro toodo máquinas por lo tanto, siga estas instrucciones y seleccione únicamente **rol de trabajo de funciones** en el programa de instalación de Hola.

1. **Haga clic en siguiente** toohave hello **instalador de tiempo de ejecución de funciones de Azure** instalar en su equipo.
1. Una vez que el instalador de hello completa iniciará hello **herramienta de configuración de tiempo de ejecución de funciones de Azure**.

    ![Instalador de la versión preliminar del Sistema en ejecución de Azure Functions completado][5]

    > [!NOTE]
    > Si está instalando en **windows10** hello y **contenedor** característica no se previamente habilitó, hello **en tiempo de ejecución de funciones de Azure** instalador le preguntará tooreboot Instale su hello toocomplete de máquina.

## <a name="configure-hello-azure-functions-runtime"></a>Configurar hello en tiempo de ejecución de funciones de Azure

Hola toocomplete instalación en tiempo de ejecución de funciones de Azure debe finalizar la configuración de Hola.

1. Hola **herramienta de configuración de tiempo de ejecución de funciones de Azure** muestra qué funciones están instaladas en su equipo.

    ![Herramienta de configuración de la versión preliminar del Sistema en ejecución de Azure Functions][6]

1. Haga clic en hello **base de datos** ficha, escriba Hola **detalles de conexión para la instancia de SQL Server** y **haga clic en aplicar**.  Esto es necesario en orden toohello en tiempo de ejecución de funciones de Azure toocreate un hello toosupport de base de datos en tiempo de ejecución.
    
    ![Configuración de la base de datos en la versión preliminar del Sistema en ejecución de Azure Functions][7]

1. Haga clic en hello **credenciales** ficha.  En esta pantalla debe crear dos credenciales que usará con un recurso compartido de archivos para hospedar todas las funciones de Azure.  **Especifique el nombre de usuario y contraseña** combinaciones para hello **propietario del recurso compartido de archivo** y para hello **usuario del recurso compartido de archivos** y haga clic en **aplicar**.

    ![Credenciales en la versión preliminar del Sistema en ejecución de Azure Functions][8]

1. Haga clic en hello **recurso compartido de archivos** ficha.  En esta pantalla debe especificar detalles de Hola de hello **ubicación del recurso compartido de archivo**.  Se puede crear automáticamente o puede usar un recurso compartido de archivos existente; haga clic en **Aplicar**.  Si selecciona una nueva ubicación de recurso compartido de archivos, debe especificar un directorio para su uso por hello en tiempo de ejecución de funciones de Azure.
    
    ![Recurso compartido de archivos en la versión preliminar del Sistema en ejecución de Azure Functions][9]

1. Haga clic en hello **IIS** ficha.  Esta pestaña muestra detalles de Hola de sitios Web de hello en IIS que Hola creará la instalación de en tiempo de ejecución de funciones de Azure.  **Haga clic en aplicar** toocomplete.

    ![IIS en la versión preliminar del Sistema en ejecución de Azure Functions][10]

1. Haga clic en hello **servicios** ficha.  Esta pestaña muestra el estado de saludo de los servicios de hello en la instalación en tiempo de ejecución de funciones de Azure.  Si después de hello de configuración inicial **servicio de activación de Host de las funciones de Azure** no se está ejecutando haga clic en **iniciar el servicio**

    ![Configuración de la versión preliminar del Sistema en ejecución de Azure Functions completada][11]

1. Por último, vaya toohello **Portal de Azure funciones en tiempo de ejecución** como`https://<machinename>/`

    ![Portal del Sistema en ejecución de Azure Functions (versión preliminar)][12]


<!--Image references-->
[1]: ./media/functions-runtime-install/AzureFunctionsRuntime_Installer1.png
[2]: ./media/functions-runtime-install/AzureFunctionsRuntime_Installer2-EULA.png
[3]: ./media/functions-runtime-install/AzureFunctionsRuntime_Installer3-ChooseRoles.png
[4]: ./media/functions-runtime-install/AzureFunctionsRuntime_Installer4-Install.png
[5]: ./media/functions-runtime-install/AzureFunctionsRuntime_Installer5-InstallComplete.png
[6]: ./media/functions-runtime-install/AzureFunctionsRuntime_Configuration1.png
[7]: ./media/functions-runtime-install/AzureFunctionsRuntime_Configuration2_SQL.png
[8]: ./media/functions-runtime-install/AzureFunctionsRuntime_Configuration3_Credentials.png
[9]: ./media/functions-runtime-install/AzureFunctionsRuntime_Configuration4_Fileshare.png
[10]: ./media/functions-runtime-install/AzureFunctionsRuntime_Configuration5_IIS.png
[11]: ./media/functions-runtime-install/AzureFunctionsRuntime_Configuration6_Services.png
[12]: ./media/functions-runtime-install/AzureFunctionsRuntime_Portal.png