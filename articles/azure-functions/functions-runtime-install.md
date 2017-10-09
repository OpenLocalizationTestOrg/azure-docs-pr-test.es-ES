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
# <a name="install-hello-azure-functions-runtime-preview"></a><span data-ttu-id="c8497-103">Instalar Hola vista previa en tiempo de ejecución de funciones de Azure</span><span class="sxs-lookup"><span data-stu-id="c8497-103">Install hello Azure Functions Runtime Preview</span></span>

<span data-ttu-id="c8497-104">Si desea que la vista previa de tooinstall hello en tiempo de ejecución de funciones de Azure, debe seguir estos pasos:</span><span class="sxs-lookup"><span data-stu-id="c8497-104">If you would like tooinstall hello Azure Functions Runtime preview, you must follow these steps:</span></span>

1. <span data-ttu-id="c8497-105">Asegúrese de que el equipo pasa los requisitos mínimos de Hola</span><span class="sxs-lookup"><span data-stu-id="c8497-105">Ensure your machine passes hello minimum requirements</span></span>
1. <span data-ttu-id="c8497-106">Descargar hello [instalador de vista previa de Azure funciones en tiempo de ejecución](https://aka.ms/azafr).</span><span class="sxs-lookup"><span data-stu-id="c8497-106">Download hello [Azure Functions Runtime Preview Installer](https://aka.ms/azafr).</span></span> 
1. <span data-ttu-id="c8497-107">Instalar vista previa de hello en tiempo de ejecución de funciones de Azure</span><span class="sxs-lookup"><span data-stu-id="c8497-107">Install hello Azure Functions Runtime preview</span></span>
1. <span data-ttu-id="c8497-108">Configuración de hello completa de una vista previa de hello en tiempo de ejecución de funciones de Azure</span><span class="sxs-lookup"><span data-stu-id="c8497-108">Complete hello configuration of hello Azure Functions Runtime preview</span></span>

## <a name="prerequisites"></a><span data-ttu-id="c8497-109">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="c8497-109">Prerequisites</span></span>

<span data-ttu-id="c8497-110">Antes de instalar hello en tiempo de ejecución de funciones de Azure preview, debe tener el siguiente hello:</span><span class="sxs-lookup"><span data-stu-id="c8497-110">Before you install hello Azure Functions Runtime preview, you must have hello following:</span></span>

1. <span data-ttu-id="c8497-111">Un máquina donde se ejecute Microsoft Windows Server 2016 o Microsoft Windows 10 Creators Update (Professional o Enterprise Edition).</span><span class="sxs-lookup"><span data-stu-id="c8497-111">A machine running Microsoft Windows Server 2016 or Microsoft Windows 10 Creators Update (Professional or Enterprise Edition).</span></span>
1. <span data-ttu-id="c8497-112">Una instancia de SQL Server que se ejecute dentro de la red.</span><span class="sxs-lookup"><span data-stu-id="c8497-112">A SQL Server instance running within your network.</span></span>  <span data-ttu-id="c8497-113">El requisito mínimo de edición es SQL Server Express.</span><span class="sxs-lookup"><span data-stu-id="c8497-113">Minimum edition requirement is SQL Server Express.</span></span>

## <a name="install-hello-azure-functions-runtime-preview"></a><span data-ttu-id="c8497-114">Instalar Hola vista previa en tiempo de ejecución de funciones de Azure</span><span class="sxs-lookup"><span data-stu-id="c8497-114">Install hello Azure Functions Runtime Preview</span></span>

<span data-ttu-id="c8497-115">instalador de vista previa de Hello en tiempo de ejecución de funciones de Azure le guía a través de la instalación de Hola de vista previa en tiempo de ejecución de funciones de Azure de hello administración y Roles de trabajo.</span><span class="sxs-lookup"><span data-stu-id="c8497-115">hello Azure Functions Runtime preview installer guides you through hello installation of hello Azure Functions Runtime preview Management and Worker Roles.</span></span>  <span data-ttu-id="c8497-116">Es posible tooinstall Hola administración y rol de trabajador de hello mismo equipo.</span><span class="sxs-lookup"><span data-stu-id="c8497-116">It is possible tooinstall hello Management and Worker role on hello same machine.</span></span>  <span data-ttu-id="c8497-117">Sin embargo, como agregar más funciones, debe implementar las funciones en varios trabajadores más roles de trabajo en equipos adicionales toobe capaz de tooscale.</span><span class="sxs-lookup"><span data-stu-id="c8497-117">However, as you add more Functions, you must deploy more worker roles on additional machines toobe able tooscale your functions onto multiple workers.</span></span>

## <a name="install-hello-management-and-worker-role-on-hello-same-machine"></a><span data-ttu-id="c8497-118">Instalar Administración de Hola y rol de trabajo en hello mismo equipo</span><span class="sxs-lookup"><span data-stu-id="c8497-118">Install hello Management and Worker Role on hello same machine</span></span>

1. <span data-ttu-id="c8497-119">Ejecute hello instalador de vista previa de Azure funciones en tiempo de ejecución.</span><span class="sxs-lookup"><span data-stu-id="c8497-119">Run hello Azure Functions Runtime Preview Installer.</span></span>

    ![Instalador de la versión preliminar del Sistema en ejecución de Azure Functions][1]

1. <span data-ttu-id="c8497-121">**Haga clic en siguiente** avanzar más allá de hello primera fase del instalador de Hola</span><span class="sxs-lookup"><span data-stu-id="c8497-121">**Click Next** advance past hello first stage of hello installer</span></span>
1. <span data-ttu-id="c8497-122">Una vez que haya leído los términos de Hola de hello **CLUF**, **casilla hello** tooaccept términos de Hola y **haga clic en siguiente** tooadvance.</span><span class="sxs-lookup"><span data-stu-id="c8497-122">Once you have read hello terms of hello **EULA**, **check hello box** tooaccept hello terms and **click Next** tooadvance.</span></span>
1. <span data-ttu-id="c8497-123">Ahora seleccione Hola roles desea tooinstall en esta máquina **rol de administración de funciones** o **rol de trabajo de funciones** y **haga clic en siguiente**</span><span class="sxs-lookup"><span data-stu-id="c8497-123">Now select hello roles you want tooinstall on this machine **Functions Management Role** and/or **Functions Worker Role** and **Click Next**</span></span>

    ![Instalador de la versión preliminar del Sistema en ejecución de Azure Functions: selección de roles][3]

    > [!NOTE]
    > <span data-ttu-id="c8497-125">Puede instalar hello **rol de trabajo de funciones** en muchos otro toodo máquinas por lo tanto, siga estas instrucciones y seleccione únicamente **rol de trabajo de funciones** en el programa de instalación de Hola.</span><span class="sxs-lookup"><span data-stu-id="c8497-125">You can install hello **Functions Worker Role** on many other machines toodo so, follow these instructions, and only select **Functions Worker Role** in hello installer.</span></span>

1. <span data-ttu-id="c8497-126">**Haga clic en siguiente** toohave hello **instalador de tiempo de ejecución de funciones de Azure** instalar en su equipo.</span><span class="sxs-lookup"><span data-stu-id="c8497-126">**Click Next** toohave hello **Azure Functions Runtime Installer** install on your machine.</span></span>
1. <span data-ttu-id="c8497-127">Una vez que el instalador de hello completa iniciará hello **herramienta de configuración de tiempo de ejecución de funciones de Azure**.</span><span class="sxs-lookup"><span data-stu-id="c8497-127">Once complete hello installer will launch hello **Azure Functions Runtime Configuration tool**.</span></span>

    ![Instalador de la versión preliminar del Sistema en ejecución de Azure Functions completado][5]

    > [!NOTE]
    > <span data-ttu-id="c8497-129">Si está instalando en **windows10** hello y **contenedor** característica no se previamente habilitó, hello **en tiempo de ejecución de funciones de Azure** instalador le preguntará tooreboot Instale su hello toocomplete de máquina.</span><span class="sxs-lookup"><span data-stu-id="c8497-129">If you are installing on **Windows 10** and hello **Container** feature has not been previously enabled, hello **Azure Functions Runtime** Installer prompts you tooreboot your machine toocomplete hello install.</span></span>

## <a name="configure-hello-azure-functions-runtime"></a><span data-ttu-id="c8497-130">Configurar hello en tiempo de ejecución de funciones de Azure</span><span class="sxs-lookup"><span data-stu-id="c8497-130">Configure hello Azure Functions Runtime</span></span>

<span data-ttu-id="c8497-131">Hola toocomplete instalación en tiempo de ejecución de funciones de Azure debe finalizar la configuración de Hola.</span><span class="sxs-lookup"><span data-stu-id="c8497-131">toocomplete hello Azure Functions Runtime installation you must complete hello configuration.</span></span>

1. <span data-ttu-id="c8497-132">Hola **herramienta de configuración de tiempo de ejecución de funciones de Azure** muestra qué funciones están instaladas en su equipo.</span><span class="sxs-lookup"><span data-stu-id="c8497-132">hello **Azure Functions Runtime Configuration Tool** shows which roles are installed on your machine.</span></span>

    ![Herramienta de configuración de la versión preliminar del Sistema en ejecución de Azure Functions][6]

1. <span data-ttu-id="c8497-134">Haga clic en hello **base de datos** ficha, escriba Hola **detalles de conexión para la instancia de SQL Server** y **haga clic en aplicar**.</span><span class="sxs-lookup"><span data-stu-id="c8497-134">Click hello **Database** tab, enter hello **connection details for your SQL Server Instance** and **click Apply**.</span></span>  <span data-ttu-id="c8497-135">Esto es necesario en orden toohello en tiempo de ejecución de funciones de Azure toocreate un hello toosupport de base de datos en tiempo de ejecución.</span><span class="sxs-lookup"><span data-stu-id="c8497-135">This is required in order toohello Azure Functions Runtime toocreate a database toosupport hello Runtime.</span></span>
    
    ![Configuración de la base de datos en la versión preliminar del Sistema en ejecución de Azure Functions][7]

1. <span data-ttu-id="c8497-137">Haga clic en hello **credenciales** ficha.  En esta pantalla debe crear dos credenciales que usará con un recurso compartido de archivos para hospedar todas las funciones de Azure.</span><span class="sxs-lookup"><span data-stu-id="c8497-137">Click hello **Credentials** tab.  On this screen you must create two new credentials for use with a FileShare for hosting all your Azure Functions.</span></span>  <span data-ttu-id="c8497-138">**Especifique el nombre de usuario y contraseña** combinaciones para hello **propietario del recurso compartido de archivo** y para hello **usuario del recurso compartido de archivos** y haga clic en **aplicar**.</span><span class="sxs-lookup"><span data-stu-id="c8497-138">**Specify Username and Password** combinations for hello **File Share Owner** and for hello **File Share User** and click **Apply**.</span></span>

    ![Credenciales en la versión preliminar del Sistema en ejecución de Azure Functions][8]

1. <span data-ttu-id="c8497-140">Haga clic en hello **recurso compartido de archivos** ficha.  En esta pantalla debe especificar detalles de Hola de hello **ubicación del recurso compartido de archivo**.</span><span class="sxs-lookup"><span data-stu-id="c8497-140">Click hello **File Share** tab.  In this screen you must specify hello details of hello **File Share location**.</span></span>  <span data-ttu-id="c8497-141">Se puede crear automáticamente o puede usar un recurso compartido de archivos existente; haga clic en **Aplicar**.</span><span class="sxs-lookup"><span data-stu-id="c8497-141">This can be created for you or you can use an existing File Share and click **Apply**.</span></span>  <span data-ttu-id="c8497-142">Si selecciona una nueva ubicación de recurso compartido de archivos, debe especificar un directorio para su uso por hello en tiempo de ejecución de funciones de Azure.</span><span class="sxs-lookup"><span data-stu-id="c8497-142">If you select a new File Share location, you must specify a directory for use by hello Azure Functions Runtime.</span></span>
    
    ![Recurso compartido de archivos en la versión preliminar del Sistema en ejecución de Azure Functions][9]

1. <span data-ttu-id="c8497-144">Haga clic en hello **IIS** ficha.  Esta pestaña muestra detalles de Hola de sitios Web de hello en IIS que Hola creará la instalación de en tiempo de ejecución de funciones de Azure.</span><span class="sxs-lookup"><span data-stu-id="c8497-144">Click hello **IIS** tab.  This tab shows hello details of hello websites in IIS that hello Azure Functions Runtime Installation will create.</span></span>  <span data-ttu-id="c8497-145">**Haga clic en aplicar** toocomplete.</span><span class="sxs-lookup"><span data-stu-id="c8497-145">**Click Apply** toocomplete.</span></span>

    ![IIS en la versión preliminar del Sistema en ejecución de Azure Functions][10]

1. <span data-ttu-id="c8497-147">Haga clic en hello **servicios** ficha.  Esta pestaña muestra el estado de saludo de los servicios de hello en la instalación en tiempo de ejecución de funciones de Azure.</span><span class="sxs-lookup"><span data-stu-id="c8497-147">Click hello **Services** tab.  This tab shows hello status of hello services in your Azure Functions Runtime installation.</span></span>  <span data-ttu-id="c8497-148">Si después de hello de configuración inicial **servicio de activación de Host de las funciones de Azure** no se está ejecutando haga clic en **iniciar el servicio**</span><span class="sxs-lookup"><span data-stu-id="c8497-148">If after initial configuration hello **Azure Functions Host Activation Service** is not running click **Start Service**</span></span>

    ![Configuración de la versión preliminar del Sistema en ejecución de Azure Functions completada][11]

1. <span data-ttu-id="c8497-150">Por último, vaya toohello **Portal de Azure funciones en tiempo de ejecución** como`https://<machinename>/`</span><span class="sxs-lookup"><span data-stu-id="c8497-150">Finally browse toohello **Azure Functions Runtime Portal** as `https://<machinename>/`</span></span>

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