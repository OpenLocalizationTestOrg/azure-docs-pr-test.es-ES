---
title: "Descarga de la plantilla para una máquina virtual de Azure | Microsoft Docs"
description: "Descarga de la plantilla para una máquina virtual con el objetivo de ayudar a automatizar las implementaciones en el modelo de implementación de Resource Manager"
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
ms.openlocfilehash: 9e4c0c3cf0e233447369a24b1d5fe27495abd1cf
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="download-the-template-for-a-vm"></a><span data-ttu-id="fef3f-103">Descargar la plantilla para una máquina virtual</span><span class="sxs-lookup"><span data-stu-id="fef3f-103">Download the template for a VM</span></span>
<span data-ttu-id="fef3f-104">Cuando se crea una máquina virtual en Azure mediante el portal o PowerShell, se crea automáticamente una plantilla de Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="fef3f-104">When you create a VM in Azure using the portal or PowerShell, a Resource Manager template is automatically created for you.</span></span> <span data-ttu-id="fef3f-105">Puede usar esta plantilla para duplicar rápidamente una implementación.</span><span class="sxs-lookup"><span data-stu-id="fef3f-105">You can use this template to quickly duplicate a deployment.</span></span> <span data-ttu-id="fef3f-106">La plantilla contiene información acerca de todos los recursos de un grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="fef3f-106">The template contains information about all of the resources in a resource group.</span></span> <span data-ttu-id="fef3f-107">En el caso de una máquina virtual, significa que la plantilla contiene todo lo que se crea para ayudar a la máquina virtual de ese grupo de recursos, incluidos los recursos de red.</span><span class="sxs-lookup"><span data-stu-id="fef3f-107">For a virtual machine, this means the template contains everything that is created in support of the VM in that resource group, including the networking resources.</span></span>

## <a name="download-the-template-using-the-portal"></a><span data-ttu-id="fef3f-108">Descarga de la plantilla mediante el portal</span><span class="sxs-lookup"><span data-stu-id="fef3f-108">Download the template using the portal</span></span>
1. <span data-ttu-id="fef3f-109">Inicie sesión en el [Portal de Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="fef3f-109">Log in to the [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="fef3f-110">En el menú del concentrador, haga clic en **Virtual Machines**.</span><span class="sxs-lookup"><span data-stu-id="fef3f-110">One the hub menu, select **Virtual Machines**.</span></span>
3. <span data-ttu-id="fef3f-111">Seleccione la máquina virtual en la lista.</span><span class="sxs-lookup"><span data-stu-id="fef3f-111">Select the virtual machine from the list.</span></span>
4. <span data-ttu-id="fef3f-112">Seleccione **Script de Automation**.</span><span class="sxs-lookup"><span data-stu-id="fef3f-112">Select **Automation script**.</span></span>
5. <span data-ttu-id="fef3f-113">Seleccione **Descargar** y guarde el archivo .zip en el equipo local.</span><span class="sxs-lookup"><span data-stu-id="fef3f-113">Select **Download** and save the .zip file to your local computer.</span></span>
6. <span data-ttu-id="fef3f-114">Abra el archivo .zip y extraiga los archivos en una carpeta.</span><span class="sxs-lookup"><span data-stu-id="fef3f-114">Open the .zip file and extract the files to a folder.</span></span> <span data-ttu-id="fef3f-115">El archivo .zip contendrá:</span><span class="sxs-lookup"><span data-stu-id="fef3f-115">The .zip file will contain:</span></span>
   
   * <span data-ttu-id="fef3f-116">deploy.ps1</span><span class="sxs-lookup"><span data-stu-id="fef3f-116">deploy.ps1</span></span>
   * <span data-ttu-id="fef3f-117">deploy.sh</span><span class="sxs-lookup"><span data-stu-id="fef3f-117">deploy.sh</span></span> 
   * <span data-ttu-id="fef3f-118">deployer.rb</span><span class="sxs-lookup"><span data-stu-id="fef3f-118">deployer.rb</span></span>
   * <span data-ttu-id="fef3f-119">DeploymentHelper.cs</span><span class="sxs-lookup"><span data-stu-id="fef3f-119">DeploymentHelper.cs</span></span>
   * <span data-ttu-id="fef3f-120">parameters.json</span><span class="sxs-lookup"><span data-stu-id="fef3f-120">parameters.json</span></span>
   * <span data-ttu-id="fef3f-121">template.json</span><span class="sxs-lookup"><span data-stu-id="fef3f-121">template.json</span></span>

<span data-ttu-id="fef3f-122">El archivo template.json es la plantilla.</span><span class="sxs-lookup"><span data-stu-id="fef3f-122">The template.json file is the template.</span></span>

## <a name="download-the-template-using-powershell"></a><span data-ttu-id="fef3f-123">Descarga de la plantilla mediante PowerShell</span><span class="sxs-lookup"><span data-stu-id="fef3f-123">Download the template using PowerShell</span></span>
<span data-ttu-id="fef3f-124">También puede descargar el archivo de plantilla .json mediante el cmdlet [Export-AzureRMResourceGroup](https://msdn.microsoft.com/library/mt715427.aspx).</span><span class="sxs-lookup"><span data-stu-id="fef3f-124">You can also download the .json template file using the [Export-AzureRMResourceGroup](https://msdn.microsoft.com/library/mt715427.aspx) cmdlet.</span></span> <span data-ttu-id="fef3f-125">Puede usar el parámetro `-path` para proporcionar el nombre de archivo y la ruta de acceso del archivo .json.</span><span class="sxs-lookup"><span data-stu-id="fef3f-125">You can use the `-path` parameter to provide the filename and path for the .json file.</span></span> <span data-ttu-id="fef3f-126">En este ejemplo se muestra cómo descargar la plantilla para el grupo de recursos denominado **myResourceGroup** en la carpeta **C:\users\public\downloads** del equipo local.</span><span class="sxs-lookup"><span data-stu-id="fef3f-126">This example shows how to download the template for the resource group named **myResourceGroup** to the **C:\users\public\downloads** folder on your local computer.</span></span>

```powershell
    Export-AzureRmResourceGroup -ResourceGroupName "myResourceGroup" -Path "C:\users\public\downloads"
```

## <a name="next-steps"></a><span data-ttu-id="fef3f-127">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="fef3f-127">Next steps</span></span>
<span data-ttu-id="fef3f-128">Para más información sobre la implementación de recursos mediante plantillas, consulte el [tutorial de plantillas de Resource Manager](../../azure-resource-manager/resource-manager-template-walkthrough.md).</span><span class="sxs-lookup"><span data-stu-id="fef3f-128">To learn more about deploying resources using templates, see [Resource Manager template walkthrough](../../azure-resource-manager/resource-manager-template-walkthrough.md).</span></span>

