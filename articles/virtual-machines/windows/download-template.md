---
title: "plantilla de hello aaaDownload para una máquina virtual de Azure | Documentos de Microsoft"
description: "Descargar plantilla de hello formularioPor un toohelp VM con la automatización de las implementaciones en el modelo de implementación del Administrador de recursos de Hola"
services: virtual-machines-windows
documentationcenter: 
author: cynthn
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 51ef4f51-0942-4249-afea-4a3f87ce1ff8
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 03/22/2017
ms.author: cynthn
ms.openlocfilehash: 86fd05f67409019b5e5c9023881745047860eee1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="download-hello-template-for-a-vm"></a><span data-ttu-id="7bf68-103">Descargue la plantilla de Hola para una máquina virtual</span><span class="sxs-lookup"><span data-stu-id="7bf68-103">Download hello template for a VM</span></span>
<span data-ttu-id="7bf68-104">Cuando se crea una máquina virtual en Azure mediante el portal de Hola o PowerShell, un administrador de recursos plantilla se crea automáticamente.</span><span class="sxs-lookup"><span data-stu-id="7bf68-104">When you create a VM in Azure using hello portal or PowerShell, a Resource Manager template is automatically created for you.</span></span> <span data-ttu-id="7bf68-105">Puede usar este duplicado de tooquickly una implementación de plantilla.</span><span class="sxs-lookup"><span data-stu-id="7bf68-105">You can use this template tooquickly duplicate a deployment.</span></span> <span data-ttu-id="7bf68-106">plantilla de Hello contiene información acerca de todos los recursos de hello en un grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="7bf68-106">hello template contains information about all of hello resources in a resource group.</span></span> <span data-ttu-id="7bf68-107">Para una máquina virtual, esto significa plantilla hello contiene todo lo que se crea para admitir Hola VM en ese grupo de recursos, incluidos los recursos de red de Hola.</span><span class="sxs-lookup"><span data-stu-id="7bf68-107">For a virtual machine, this means hello template contains everything that is created in support of hello VM in that resource group, including hello networking resources.</span></span>

## <a name="download-hello-template-using-hello-portal"></a><span data-ttu-id="7bf68-108">Descargar plantilla de hello mediante el portal de Hola</span><span class="sxs-lookup"><span data-stu-id="7bf68-108">Download hello template using hello portal</span></span>
1. <span data-ttu-id="7bf68-109">Inicie sesión en toohello [portal de Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="7bf68-109">Log in toohello [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="7bf68-110">Menú del concentrador uno Hola, seleccione **máquinas virtuales**.</span><span class="sxs-lookup"><span data-stu-id="7bf68-110">One hello hub menu, select **Virtual Machines**.</span></span>
3. <span data-ttu-id="7bf68-111">Seleccione la máquina virtual de Hola de lista de Hola.</span><span class="sxs-lookup"><span data-stu-id="7bf68-111">Select hello virtual machine from hello list.</span></span>
4. <span data-ttu-id="7bf68-112">Seleccione **Script de Automation**.</span><span class="sxs-lookup"><span data-stu-id="7bf68-112">Select **Automation script**.</span></span>
5. <span data-ttu-id="7bf68-113">Seleccione **descargar** y guarde el equipo local del tooyour de archivo .zip Hola.</span><span class="sxs-lookup"><span data-stu-id="7bf68-113">Select **Download** and save hello .zip file tooyour local computer.</span></span>
6. <span data-ttu-id="7bf68-114">Abra el archivo .zip de hello y extraer carpeta tooa Hola.</span><span class="sxs-lookup"><span data-stu-id="7bf68-114">Open hello .zip file and extract hello files tooa folder.</span></span> <span data-ttu-id="7bf68-115">archivo .zip de Hello contendrá:</span><span class="sxs-lookup"><span data-stu-id="7bf68-115">hello .zip file will contain:</span></span>
   
   * <span data-ttu-id="7bf68-116">deploy.ps1</span><span class="sxs-lookup"><span data-stu-id="7bf68-116">deploy.ps1</span></span>
   * <span data-ttu-id="7bf68-117">deploy.sh</span><span class="sxs-lookup"><span data-stu-id="7bf68-117">deploy.sh</span></span> 
   * <span data-ttu-id="7bf68-118">deployer.rb</span><span class="sxs-lookup"><span data-stu-id="7bf68-118">deployer.rb</span></span>
   * <span data-ttu-id="7bf68-119">DeploymentHelper.cs</span><span class="sxs-lookup"><span data-stu-id="7bf68-119">DeploymentHelper.cs</span></span>
   * <span data-ttu-id="7bf68-120">parameters.json</span><span class="sxs-lookup"><span data-stu-id="7bf68-120">parameters.json</span></span>
   * <span data-ttu-id="7bf68-121">template.json</span><span class="sxs-lookup"><span data-stu-id="7bf68-121">template.json</span></span>

<span data-ttu-id="7bf68-122">archivo de template.json Hello es la plantilla de Hola.</span><span class="sxs-lookup"><span data-stu-id="7bf68-122">hello template.json file is hello template.</span></span>

## <a name="download-hello-template-using-powershell"></a><span data-ttu-id="7bf68-123">Descargar plantilla de hello mediante PowerShell</span><span class="sxs-lookup"><span data-stu-id="7bf68-123">Download hello template using PowerShell</span></span>
<span data-ttu-id="7bf68-124">También puede descargar el archivo de plantilla de hello .json con hello [AzureRMResourceGroup de exportación](https://msdn.microsoft.com/library/mt715427.aspx) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="7bf68-124">You can also download hello .json template file using hello [Export-AzureRMResourceGroup](https://msdn.microsoft.com/library/mt715427.aspx) cmdlet.</span></span> <span data-ttu-id="7bf68-125">Puede usar hello `-path` parámetro tooprovide Hola filename y ruta de acceso de archivo de .json Hola.</span><span class="sxs-lookup"><span data-stu-id="7bf68-125">You can use hello `-path` parameter tooprovide hello filename and path for hello .json file.</span></span> <span data-ttu-id="7bf68-126">Este ejemplo muestra cómo se denomina plantilla de hello toodownload para el grupo de recursos de hello **myResourceGroup** toohello **C:\users\public\downloads** carpeta en el equipo local.</span><span class="sxs-lookup"><span data-stu-id="7bf68-126">This example shows how toodownload hello template for hello resource group named **myResourceGroup** toohello **C:\users\public\downloads** folder on your local computer.</span></span>

```powershell
    Export-AzureRmResourceGroup -ResourceGroupName "myResourceGroup" -Path "C:\users\public\downloads"
```

## <a name="next-steps"></a><span data-ttu-id="7bf68-127">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="7bf68-127">Next steps</span></span>
<span data-ttu-id="7bf68-128">toolearn más información acerca de implementar los recursos con plantillas, consulte [tutorial de la plantilla de administrador de recursos](../../azure-resource-manager/resource-manager-template-walkthrough.md).</span><span class="sxs-lookup"><span data-stu-id="7bf68-128">toolearn more about deploying resources using templates, see [Resource Manager template walkthrough](../../azure-resource-manager/resource-manager-template-walkthrough.md).</span></span>

