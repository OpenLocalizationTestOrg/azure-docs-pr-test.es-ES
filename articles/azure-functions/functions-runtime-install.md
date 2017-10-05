---
title: "Instalación del Sistema en ejecución de Azure Functions | Microsoft Docs"
description: "Cómo instalar el Sistema en ejecución de Azure Functions"
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
ms.openlocfilehash: 1e4188313a87d07f396e5f8edc8969dd5da2c436
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="install-the-azure-functions-runtime-preview"></a><span data-ttu-id="ec931-103">Instalación de la versión preliminar del Sistema en ejecución de Azure Functions</span><span class="sxs-lookup"><span data-stu-id="ec931-103">Install the Azure Functions Runtime Preview</span></span>

<span data-ttu-id="ec931-104">Si desea instalar la versión preliminar del Sistema en ejecución de Azure Functions, debe seguir estos pasos:</span><span class="sxs-lookup"><span data-stu-id="ec931-104">If you would like to install the Azure Functions Runtime preview, you must follow these steps:</span></span>

1. <span data-ttu-id="ec931-105">Asegúrese de que la máquina cumpla los requisitos mínimos.</span><span class="sxs-lookup"><span data-stu-id="ec931-105">Ensure your machine passes the minimum requirements</span></span>
1. <span data-ttu-id="ec931-106">Descargue el [instalador de la versión preliminar del Sistema en ejecución de Azure Functions](https://aka.ms/azafr).</span><span class="sxs-lookup"><span data-stu-id="ec931-106">Download the [Azure Functions Runtime Preview Installer](https://aka.ms/azafr).</span></span> 
1. <span data-ttu-id="ec931-107">Instale la versión preliminar del Sistema en ejecución de Azure Functions.</span><span class="sxs-lookup"><span data-stu-id="ec931-107">Install the Azure Functions Runtime preview</span></span>
1. <span data-ttu-id="ec931-108">Complete la configuración de la versión preliminar del Sistema en ejecución de Azure Functions.</span><span class="sxs-lookup"><span data-stu-id="ec931-108">Complete the configuration of the Azure Functions Runtime preview</span></span>

## <a name="prerequisites"></a><span data-ttu-id="ec931-109">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="ec931-109">Prerequisites</span></span>

<span data-ttu-id="ec931-110">Antes de instalar la versión preliminar del Sistema en ejecución de Azure Functions, debe tener lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="ec931-110">Before you install the Azure Functions Runtime preview, you must have the following:</span></span>

1. <span data-ttu-id="ec931-111">Un máquina donde se ejecute Microsoft Windows Server 2016 o Microsoft Windows 10 Creators Update (Professional o Enterprise Edition).</span><span class="sxs-lookup"><span data-stu-id="ec931-111">A machine running Microsoft Windows Server 2016 or Microsoft Windows 10 Creators Update (Professional or Enterprise Edition).</span></span>
1. <span data-ttu-id="ec931-112">Una instancia de SQL Server que se ejecute dentro de la red.</span><span class="sxs-lookup"><span data-stu-id="ec931-112">A SQL Server instance running within your network.</span></span>  <span data-ttu-id="ec931-113">El requisito mínimo de edición es SQL Server Express.</span><span class="sxs-lookup"><span data-stu-id="ec931-113">Minimum edition requirement is SQL Server Express.</span></span>

## <a name="install-the-azure-functions-runtime-preview"></a><span data-ttu-id="ec931-114">Instalación de la versión preliminar del Sistema en ejecución de Azure Functions</span><span class="sxs-lookup"><span data-stu-id="ec931-114">Install the Azure Functions Runtime Preview</span></span>

<span data-ttu-id="ec931-115">El instalador de la versión preliminar del Sistema en ejecución de Azure Functions le guía por la instalación de los roles de administración y de trabajo de la versión preliminar del Sistema en ejecución de Azure Functions.</span><span class="sxs-lookup"><span data-stu-id="ec931-115">The Azure Functions Runtime preview installer guides you through the installation of the Azure Functions Runtime preview Management and Worker Roles.</span></span>  <span data-ttu-id="ec931-116">Es posible instalar el rol de administración y el de trabajo en la misma máquina.</span><span class="sxs-lookup"><span data-stu-id="ec931-116">It is possible to install the Management and Worker role on the same machine.</span></span>  <span data-ttu-id="ec931-117">Sin embargo, a medida que agregue más funciones, debe implementar más roles de trabajo más en máquinas adicionales para poder escalar sus funciones a varios trabajos.</span><span class="sxs-lookup"><span data-stu-id="ec931-117">However, as you add more Functions, you must deploy more worker roles on additional machines to be able to scale your functions onto multiple workers.</span></span>

## <a name="install-the-management-and-worker-role-on-the-same-machine"></a><span data-ttu-id="ec931-118">Instalación del rol de administración y el de trabajo en la misma máquina</span><span class="sxs-lookup"><span data-stu-id="ec931-118">Install the Management and Worker Role on the same machine</span></span>

1. <span data-ttu-id="ec931-119">Ejecute el instalador de la versión preliminar del Sistema en ejecución de Azure Functions.</span><span class="sxs-lookup"><span data-stu-id="ec931-119">Run the Azure Functions Runtime Preview Installer.</span></span>

    ![Instalador de la versión preliminar del Sistema en ejecución de Azure Functions][1]

1. <span data-ttu-id="ec931-121">**Haga clic en Siguiente** para pasar la primera fase del instalador.</span><span class="sxs-lookup"><span data-stu-id="ec931-121">**Click Next** advance past the first stage of the installer</span></span>
1. <span data-ttu-id="ec931-122">Una vez que haya leído los términos del **CLUF**, **active la casilla** para aceptar los términos y **haga clic en Siguiente** para avanzar.</span><span class="sxs-lookup"><span data-stu-id="ec931-122">Once you have read the terms of the **EULA**, **check the box** to accept the terms and **click Next** to advance.</span></span>
1. <span data-ttu-id="ec931-123">Ahora seleccione los roles que desea instalar en esta máquina, **Functions Management Role** (Rol de administración de Functions) o **Functions Worker Role** (Rol de trabajo de Functions), y **haga clic en Siguiente**.</span><span class="sxs-lookup"><span data-stu-id="ec931-123">Now select the roles you want to install on this machine **Functions Management Role** and/or **Functions Worker Role** and **Click Next**</span></span>

    ![Instalador de la versión preliminar del Sistema en ejecución de Azure Functions: selección de roles][3]

    > [!NOTE]
    > <span data-ttu-id="ec931-125">Puede instalar **Functions Worker Role** (Rol de trabajo de Functions) en muchas otras máquinas; para hacerlo, siga estas instrucciones y seleccione solo **Functions Worker Role** en el instalador.</span><span class="sxs-lookup"><span data-stu-id="ec931-125">You can install the **Functions Worker Role** on many other machines to do so, follow these instructions, and only select **Functions Worker Role** in the installer.</span></span>

1. <span data-ttu-id="ec931-126">**Haga clic en Siguiente** para que el **instalador del Sistema en ejecución de Azure Functions** lleve a cabo la instalación en su máquina.</span><span class="sxs-lookup"><span data-stu-id="ec931-126">**Click Next** to have the **Azure Functions Runtime Installer** install on your machine.</span></span>
1. <span data-ttu-id="ec931-127">Una vez completado el instalador, se iniciará la **herramienta de configuración del Sistema en ejecución de Azure Functions**.</span><span class="sxs-lookup"><span data-stu-id="ec931-127">Once complete the installer will launch the **Azure Functions Runtime Configuration tool**.</span></span>

    ![Instalador de la versión preliminar del Sistema en ejecución de Azure Functions completado][5]

    > [!NOTE]
    > <span data-ttu-id="ec931-129">Si está instalando en **Windows 10** y la característica **Contenedor** no se ha habilitado previamente, el instalador del **Sistema en ejecución de Azure Functions** le pide que reinicie la máquina para completar la instalación.</span><span class="sxs-lookup"><span data-stu-id="ec931-129">If you are installing on **Windows 10** and the **Container** feature has not been previously enabled, the **Azure Functions Runtime** Installer prompts you to reboot your machine to complete the install.</span></span>

## <a name="configure-the-azure-functions-runtime"></a><span data-ttu-id="ec931-130">Configuración del Sistema en ejecución de Azure Functions</span><span class="sxs-lookup"><span data-stu-id="ec931-130">Configure the Azure Functions Runtime</span></span>

<span data-ttu-id="ec931-131">Para completar la instalación del Sistema en ejecución de Azure Functions, debe completar la configuración.</span><span class="sxs-lookup"><span data-stu-id="ec931-131">To complete the Azure Functions Runtime installation you must complete the configuration.</span></span>

1. <span data-ttu-id="ec931-132">El **herramienta de configuración del Sistema en ejecución de Azure Functions** muestra qué roles están instalados en su máquina.</span><span class="sxs-lookup"><span data-stu-id="ec931-132">The **Azure Functions Runtime Configuration Tool** shows which roles are installed on your machine.</span></span>

    ![Herramienta de configuración de la versión preliminar del Sistema en ejecución de Azure Functions][6]

1. <span data-ttu-id="ec931-134">Haga clic en la pestaña **Base de datos**, especifique los **detalles de conexión para la instancia de SQL Server** y **haga clic en Aplicar**.</span><span class="sxs-lookup"><span data-stu-id="ec931-134">Click the **Database** tab, enter the **connection details for your SQL Server Instance** and **click Apply**.</span></span>  <span data-ttu-id="ec931-135">Esto es necesario para que el Sistema en ejecución de Azure Functions cree una base de datos que admita el sistema en tiempo de ejecución.</span><span class="sxs-lookup"><span data-stu-id="ec931-135">This is required in order to the Azure Functions Runtime to create a database to support the Runtime.</span></span>
    
    ![Configuración de la base de datos en la versión preliminar del Sistema en ejecución de Azure Functions][7]

1. <span data-ttu-id="ec931-137">Haga clic en la pestaña **Credenciales**.</span><span class="sxs-lookup"><span data-stu-id="ec931-137">Click the **Credentials** tab.</span></span>  <span data-ttu-id="ec931-138">En esta pantalla debe crear dos credenciales que usará con un recurso compartido de archivos para hospedar todas las funciones de Azure.</span><span class="sxs-lookup"><span data-stu-id="ec931-138">On this screen you must create two new credentials for use with a FileShare for hosting all your Azure Functions.</span></span>  <span data-ttu-id="ec931-139">**Especifique el nombre de usuario y la contraseña** para el **propietario del recurso compartido de archivos** y para el **usuario del recurso compartido de archivos**, y haga clic en **Aplicar**.</span><span class="sxs-lookup"><span data-stu-id="ec931-139">**Specify Username and Password** combinations for the **File Share Owner** and for the **File Share User** and click **Apply**.</span></span>

    ![Credenciales en la versión preliminar del Sistema en ejecución de Azure Functions][8]

1. <span data-ttu-id="ec931-141">Haga clic en la pestaña **Recurso compartido de archivos**.</span><span class="sxs-lookup"><span data-stu-id="ec931-141">Click the **File Share** tab.</span></span>  <span data-ttu-id="ec931-142">En esta pantalla debe especificar los detalles de la **ubicación del recurso compartido de archivos**.</span><span class="sxs-lookup"><span data-stu-id="ec931-142">In this screen you must specify the details of the **File Share location**.</span></span>  <span data-ttu-id="ec931-143">Se puede crear automáticamente o puede usar un recurso compartido de archivos existente; haga clic en **Aplicar**.</span><span class="sxs-lookup"><span data-stu-id="ec931-143">This can be created for you or you can use an existing File Share and click **Apply**.</span></span>  <span data-ttu-id="ec931-144">Si selecciona una nueva ubicación de recurso compartido de archivos, debe especificar un directorio que usará el Sistema en ejecución de Azure Functions.</span><span class="sxs-lookup"><span data-stu-id="ec931-144">If you select a new File Share location, you must specify a directory for use by the Azure Functions Runtime.</span></span>
    
    ![Recurso compartido de archivos en la versión preliminar del Sistema en ejecución de Azure Functions][9]

1. <span data-ttu-id="ec931-146">Haga clic en la pestaña **IIS**.</span><span class="sxs-lookup"><span data-stu-id="ec931-146">Click the **IIS** tab.</span></span>  <span data-ttu-id="ec931-147">En esta pestaña se muestran los detalles de los sitios web en IIS que la instalación del Sistema en ejecución de Azure Functions creará.</span><span class="sxs-lookup"><span data-stu-id="ec931-147">This tab shows the details of the websites in IIS that the Azure Functions Runtime Installation will create.</span></span>  <span data-ttu-id="ec931-148">**Haga clic en Aplicar** para completarlo.</span><span class="sxs-lookup"><span data-stu-id="ec931-148">**Click Apply** to complete.</span></span>

    ![IIS en la versión preliminar del Sistema en ejecución de Azure Functions][10]

1. <span data-ttu-id="ec931-150">Haga clic en la pestaña **Servicios**.</span><span class="sxs-lookup"><span data-stu-id="ec931-150">Click the **Services** tab.</span></span>  <span data-ttu-id="ec931-151">En esta pestaña se muestra el estado de los servicios en la instalación del Sistema en ejecución de Azure Functions.</span><span class="sxs-lookup"><span data-stu-id="ec931-151">This tab shows the status of the services in your Azure Functions Runtime installation.</span></span>  <span data-ttu-id="ec931-152">Si después de la configuración inicial, el **servicio de activación de host de Azure Functions** no se está ejecutando, haga clic en **Iniciar servicio**.</span><span class="sxs-lookup"><span data-stu-id="ec931-152">If after initial configuration the **Azure Functions Host Activation Service** is not running click **Start Service**</span></span>

    ![Configuración de la versión preliminar del Sistema en ejecución de Azure Functions completada][11]

1. <span data-ttu-id="ec931-154">Por último, vaya al **portal del Sistema en ejecución de Azure Functions** como `https://<machinename>/`.</span><span class="sxs-lookup"><span data-stu-id="ec931-154">Finally browse to the **Azure Functions Runtime Portal** as `https://<machinename>/`</span></span>

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