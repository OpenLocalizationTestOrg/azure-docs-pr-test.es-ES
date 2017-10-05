---
title: "Creación de un contenedor de servicios en la nube con PowerShell | Microsoft Docs"
description: "En este artículo se explica cómo crear un contenedor de servicios en la nube con PowerShell. El contenedor hospeda roles web y roles de trabajo."
services: cloud-services
documentationcenter: .net
author: cawaMS
manager: timlt
editor: 
ms.assetid: c8f32469-610e-4f37-a3aa-4fac5c714e13
ms.service: cloud-services
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: powershell
ms.workload: na
ms.date: 11/18/2016
ms.author: cawa
ms.openlocfilehash: 2023fa7b318f9f76ce1e1ea0a46110297be9a001
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="use-an-azure-powershell-command-to-create-an-empty-cloud-service-container"></a><span data-ttu-id="ce3fb-104">Uso de un comando de Azure PowerShell para crear un contenedor vacío de servicios en la nube</span><span class="sxs-lookup"><span data-stu-id="ce3fb-104">Use an Azure PowerShell command to create an empty cloud service container</span></span>
<span data-ttu-id="ce3fb-105">En este artículo se explica cómo crear rápidamente un contenedor de servicios en la nube mediante cmdlets de Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="ce3fb-105">This article explains how to quickly create a Cloud Services container using Azure PowerShell cmdlets.</span></span> <span data-ttu-id="ce3fb-106">Siga estos pasos:</span><span class="sxs-lookup"><span data-stu-id="ce3fb-106">Please follow the steps below:</span></span>

1. <span data-ttu-id="ce3fb-107">Instale el cmdlet de Microsoft Azure PowerShell desde la página de [descargas de Azure PowerShell](http://aka.ms/webpi-azps) .</span><span class="sxs-lookup"><span data-stu-id="ce3fb-107">Install the Microsoft Azure PowerShell cmdlet from the [Azure PowerShell downloads](http://aka.ms/webpi-azps) page.</span></span>
2. <span data-ttu-id="ce3fb-108">Abra un símbolo del sistema de PowerShell.</span><span class="sxs-lookup"><span data-stu-id="ce3fb-108">Open the PowerShell command prompt.</span></span>
3. <span data-ttu-id="ce3fb-109">Use [Add-AzureAccount](https://msdn.microsoft.com/library/dn495128.aspx) para iniciar sesión.</span><span class="sxs-lookup"><span data-stu-id="ce3fb-109">Use the [Add-AzureAccount](https://msdn.microsoft.com/library/dn495128.aspx) to sign in.</span></span>

   > [!NOTE]
   > <span data-ttu-id="ce3fb-110">Para más instrucciones acerca de cómo instalar el cmdlet de Azure PowerShell y conectarse a la suscripción de Azure, consulte [Cómo instalar y configurar Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="ce3fb-110">For further instruction on installing the Azure PowerShell cmdlet and connecting to your Azure subscription, refer to [How to install and configure Azure PowerShell](/powershell/azure/overview).</span></span>
   >
   >
4. <span data-ttu-id="ce3fb-111">Use el cmdlet **New-AzureService** para crear un contenedor de servicios en la nube de Azure vacío.</span><span class="sxs-lookup"><span data-stu-id="ce3fb-111">Use the **New-AzureService** cmdlet to create an empty Azure cloud service container.</span></span>

    ```
    New-AzureService [-ServiceName] <String> [-AffinityGroup] <String> [[-Label] <String>] [[-Description] <String>] [[-ReverseDnsFqdn] <String>] [<CommonParameters>]
    New-AzureService [-ServiceName] <String> [-Location] <String> [[-Label] <String>] [[-Description] <String>] [[-ReverseDnsFqdn] <String>] [<CommonParameters>]
   ```
5. <span data-ttu-id="ce3fb-112">Para invocar el cmdlet, siga este ejemplo:</span><span class="sxs-lookup"><span data-stu-id="ce3fb-112">Follow this example to invoke the cmdlet:</span></span>

   ```
   New-AzureService -ServiceName "mytestcloudservice" -Location "Central US" -Label "mytestcloudservice"
   ```

<span data-ttu-id="ce3fb-113">Para obtener más información sobre cómo crear el servicio en la nube de Azure, ejecute:</span><span class="sxs-lookup"><span data-stu-id="ce3fb-113">For more information about creating the Azure cloud service, run:</span></span>

```
Get-help New-AzureService
```

### <a name="next-steps"></a><span data-ttu-id="ce3fb-114">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="ce3fb-114">Next steps</span></span>
* <span data-ttu-id="ce3fb-115">Para administrar la implementación de servicios en la nube, consulte los comandos [Get-AzureService](https://msdn.microsoft.com/library/azure/dn495131.aspx), [Remove-AzureService](https://msdn.microsoft.com/library/azure/dn495120.aspx) y [Set-AzureService](https://msdn.microsoft.com/library/azure/dn495242.aspx).</span><span class="sxs-lookup"><span data-stu-id="ce3fb-115">To manage the cloud service deployment, refer to the [Get-AzureService](https://msdn.microsoft.com/library/azure/dn495131.aspx), [Remove-AzureService](https://msdn.microsoft.com/library/azure/dn495120.aspx), and [Set-AzureService](https://msdn.microsoft.com/library/azure/dn495242.aspx) commands.</span></span> <span data-ttu-id="ce3fb-116">Para más información, también puede consultar [Configuración de servicios en la nube](cloud-services-how-to-configure.md) .</span><span class="sxs-lookup"><span data-stu-id="ce3fb-116">You may also refer to [How to configure cloud services](cloud-services-how-to-configure.md) for further information.</span></span>
* <span data-ttu-id="ce3fb-117">Para publicar el proyecto de servicio en la nube en Azure, consulte el código de ejemplo de **PublishCloudService.ps1** de [Entrega continua para Servicios en la nube de Azure](cloud-services-dotnet-continuous-delivery.md).</span><span class="sxs-lookup"><span data-stu-id="ce3fb-117">To publish your cloud service project to Azure, refer to the  **PublishCloudService.ps1** code sample from [Continuous delivery for cloud service in Azure](cloud-services-dotnet-continuous-delivery.md).</span></span>
