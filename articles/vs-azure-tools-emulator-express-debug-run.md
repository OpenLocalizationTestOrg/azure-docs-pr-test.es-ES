---
title: servicio en un equipo local en la nube aaaUsing Emulator Express toorun y depurar un Azure | Documentos de Microsoft
description: Usar Emulator Express toorun y depurar un servicio de nube en un equipo local
services: visual-studio-online
documentationcenter: n/a
author: kraigb
manager: ghogen
editor: 
ms.assetid: 73108f98-a552-4817-b7a1-551367b71906
ms.service: visual-studio-online
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 03/06/2017
ms.author: kraigb
ms.openlocfilehash: d89a0fc2dce42b4a2d2f93f9c4ff0482af924ad4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="using-emulator-express-toorun-and-debug-an-azure-cloud-service-on-a-local-machine"></a><span data-ttu-id="08666-103">Con Emulator Express toorun y depurar un Azure servicio en la nube en un equipo local</span><span class="sxs-lookup"><span data-stu-id="08666-103">Using Emulator Express toorun and debug an Azure cloud service on a local machine</span></span>
<span data-ttu-id="08666-104">Con Emulator Express, puede probar y depurar un servicio en la nube sin ejecutar Visual Studio como administrador.</span><span class="sxs-lookup"><span data-stu-id="08666-104">By using Emulator Express, you can test and debug a cloud service without running Visual Studio as an administrator.</span></span> <span data-ttu-id="08666-105">Puede establecer el toouse de configuración de proyecto cualquier Emulator Express u Hola emulador completo, según los requisitos de Hola de servicio en la nube.</span><span class="sxs-lookup"><span data-stu-id="08666-105">You can set your project settings toouse either Emulator Express or hello full emulator, depending on hello requirements of your cloud service.</span></span> <span data-ttu-id="08666-106">Para obtener más información acerca del emulador completo hello, consulte [ejecutar una aplicación de Azure en hello emulador de proceso](storage/common/storage-use-emulator.md).</span><span class="sxs-lookup"><span data-stu-id="08666-106">For more information about hello full emulator, see [Run an Azure Application in hello Compute Emulator](storage/common/storage-use-emulator.md).</span></span>

## <a name="using-emulator-express-in-visual-studio"></a><span data-ttu-id="08666-107">Uso de Emulator Express en Visual Studio</span><span class="sxs-lookup"><span data-stu-id="08666-107">Using Emulator Express in Visual Studio</span></span>
<span data-ttu-id="08666-108">Al crear un proyecto de Azure en Azure SDK 2.3 o posterior, Emulator Express se usa automáticamente.</span><span class="sxs-lookup"><span data-stu-id="08666-108">When you create an Azure project in Azure SDK 2.3 or later, Emulator Express is automatically used.</span></span> <span data-ttu-id="08666-109">Para los proyectos existentes que se crearon con una versión anterior de hello Azure SDK, use Hola después tooselect pasos Emulator Express:</span><span class="sxs-lookup"><span data-stu-id="08666-109">For existing projects that were created with an earlier version of hello Azure SDK, use hello following steps tooselect Emulator Express:</span></span>

1. <span data-ttu-id="08666-110">Cree o abra un proyecto de servicio en la nube de Azure en Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="08666-110">Create or open an Azure cloud service project in Visual Studio.</span></span>

1. <span data-ttu-id="08666-111">En **el Explorador de soluciones**, haga clic en proyecto de hello y, en el menú contextual de hello, seleccione **propiedades**.</span><span class="sxs-lookup"><span data-stu-id="08666-111">In **Solution Explorer**, right-click hello project, and, from hello context menu, select **Properties**.</span></span>

1. <span data-ttu-id="08666-112">En las páginas de propiedades de proyectos de hello, seleccione hello **Web** ficha.</span><span class="sxs-lookup"><span data-stu-id="08666-112">In hello projects properties pages, select hello **Web** tab.</span></span>

    ![Propiedades de proyecto de servicio en la nube de Azure](./media/vs-azure-tools-emulator-express-debug-run/web-properties.png)

1. <span data-ttu-id="08666-114">En **Servidor de desarrollo local**, seleccione la opción **Usar IIS Express**.</span><span class="sxs-lookup"><span data-stu-id="08666-114">Under **Local Development Server**, select **Use IIS Express option**.</span></span>

1. <span data-ttu-id="08666-115">En **Emulador**, seleccione **usar Emulator Express**.</span><span class="sxs-lookup"><span data-stu-id="08666-115">Under **Emulator**, select **Use Emulator Express**.</span></span>
   
1. <span data-ttu-id="08666-116">toolaunch Hola Emulator Express, ejecute hello siguiente comando en un símbolo del sistema:</span><span class="sxs-lookup"><span data-stu-id="08666-116">toolaunch hello Emulator Express, run hello following command at a command prompt:</span></span> 

    ```
    csrun.exe /useemulatorexpress
    ```

## <a name="emulator-express-limitations"></a><span data-ttu-id="08666-117">Limitaciones de Emulator Express</span><span class="sxs-lookup"><span data-stu-id="08666-117">Emulator Express limitations</span></span>
<span data-ttu-id="08666-118">Hola problemas siguientes se conoce las limitaciones de Emulator Express:</span><span class="sxs-lookup"><span data-stu-id="08666-118">hello following issues are known limitations of Emulator Express:</span></span> 

- <span data-ttu-id="08666-119">Emulator Express no es compatible con el servidor web de IIS.</span><span class="sxs-lookup"><span data-stu-id="08666-119">Emulator Express is not compatible with IIS Web Server.</span></span>
- <span data-ttu-id="08666-120">El servicio de nube puede contener varios roles, pero cada rol es instancia tooone limitado.</span><span class="sxs-lookup"><span data-stu-id="08666-120">Your cloud service can contain multiple roles, but each role is limited tooone instance.</span></span>
- <span data-ttu-id="08666-121">No puede tener acceso a los números de puerto inferiores a 1000.</span><span class="sxs-lookup"><span data-stu-id="08666-121">You can't access port numbers below 1000.</span></span> <span data-ttu-id="08666-122">Si utiliza un proveedor de autenticación que normalmente utiliza un puerto inferior a 1000, tendrá que toochange este número de puerto de tooa valor por encima de 1000.</span><span class="sxs-lookup"><span data-stu-id="08666-122">If you use an authentication provider that normally uses a port below 1000, you might need toochange this value tooa port number that's above 1000.</span></span>
- <span data-ttu-id="08666-123">Las limitaciones que se aplican toohello emulador de proceso de Azure también aplican tooEmulator Express.</span><span class="sxs-lookup"><span data-stu-id="08666-123">Any limitations that apply toohello Azure Compute Emulator also apply tooEmulator Express.</span></span> <span data-ttu-id="08666-124">Por ejemplo, no puede tener más de 50 instancias de rol por implementación.</span><span class="sxs-lookup"><span data-stu-id="08666-124">For example, you can't have more than 50 role instances per deployment.</span></span> <span data-ttu-id="08666-125">Para obtener más información acerca de hello emulador de proceso de Azure, consulte [ejecutar una aplicación de Azure en hello emulador de proceso](http://go.microsoft.com/fwlink/p/?LinkId=623050).</span><span class="sxs-lookup"><span data-stu-id="08666-125">For more information about hello Azure Compute Emulator, see [Run an Azure Application in hello Compute Emulator](http://go.microsoft.com/fwlink/p/?LinkId=623050).</span></span>

## <a name="next-steps"></a><span data-ttu-id="08666-126">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="08666-126">Next steps</span></span>
[<span data-ttu-id="08666-127">Depuración de servicios en la nube de Azure</span><span class="sxs-lookup"><span data-stu-id="08666-127">Debugging Azure cloud services</span></span>](https://msdn.microsoft.com/library/azure/ee405479.aspx)
