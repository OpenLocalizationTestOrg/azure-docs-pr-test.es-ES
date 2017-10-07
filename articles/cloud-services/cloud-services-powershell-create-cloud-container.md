---
title: aaaCreate un contenedor de servicios de nube con PowerShell | Documentos de Microsoft
description: "Este artículo explica cómo toocreate una nube service contenedor con PowerShell. contenedor de Hello hospeda roles web y de trabajo."
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
ms.openlocfilehash: 4c47b10b5ba1f9cc39594a45cd869bf04fcaadf6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="use-an-azure-powershell-command-toocreate-an-empty-cloud-service-container"></a><span data-ttu-id="f06e8-104">Usar un toocreate de comandos de PowerShell de Azure un contenedor de servicios de nube vacío</span><span class="sxs-lookup"><span data-stu-id="f06e8-104">Use an Azure PowerShell command toocreate an empty cloud service container</span></span>
<span data-ttu-id="f06e8-105">Este artículo explica cómo tooquickly crear un contenedor de servicios en la nube mediante cmdlets de PowerShell de Azure.</span><span class="sxs-lookup"><span data-stu-id="f06e8-105">This article explains how tooquickly create a Cloud Services container using Azure PowerShell cmdlets.</span></span> <span data-ttu-id="f06e8-106">Siga estos pasos hello:</span><span class="sxs-lookup"><span data-stu-id="f06e8-106">Please follow hello steps below:</span></span>

1. <span data-ttu-id="f06e8-107">Instalar cmdlet de PowerShell de Microsoft Azure Hola de hello [descargas de Azure PowerShell](http://aka.ms/webpi-azps) página.</span><span class="sxs-lookup"><span data-stu-id="f06e8-107">Install hello Microsoft Azure PowerShell cmdlet from hello [Azure PowerShell downloads](http://aka.ms/webpi-azps) page.</span></span>
2. <span data-ttu-id="f06e8-108">Abra el símbolo del sistema de PowerShell de Hola.</span><span class="sxs-lookup"><span data-stu-id="f06e8-108">Open hello PowerShell command prompt.</span></span>
3. <span data-ttu-id="f06e8-109">Hola de uso [Add-AzureAccount](https://msdn.microsoft.com/library/dn495128.aspx) toosign en.</span><span class="sxs-lookup"><span data-stu-id="f06e8-109">Use hello [Add-AzureAccount](https://msdn.microsoft.com/library/dn495128.aspx) toosign in.</span></span>

   > [!NOTE]
   > <span data-ttu-id="f06e8-110">Para obtener más instrucciones sobre cómo instalar Hola cmdlet de PowerShell de Azure y conectar tooyour suscripción de Azure, consulte demasiado[cómo tooinstall y configurar Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="f06e8-110">For further instruction on installing hello Azure PowerShell cmdlet and connecting tooyour Azure subscription, refer too[How tooinstall and configure Azure PowerShell](/powershell/azure/overview).</span></span>
   >
   >
4. <span data-ttu-id="f06e8-111">Hola de uso **New-AzureService** cmdlet toocreate un contenedor de servicios de nube de Azure vacío.</span><span class="sxs-lookup"><span data-stu-id="f06e8-111">Use hello **New-AzureService** cmdlet toocreate an empty Azure cloud service container.</span></span>

    ```
    New-AzureService [-ServiceName] <String> [-AffinityGroup] <String> [[-Label] <String>] [[-Description] <String>] [[-ReverseDnsFqdn] <String>] [<CommonParameters>]
    New-AzureService [-ServiceName] <String> [-Location] <String> [[-Label] <String>] [[-Description] <String>] [[-ReverseDnsFqdn] <String>] [<CommonParameters>]
   ```
5. <span data-ttu-id="f06e8-112">Siga este cmdlet de hello tooinvoke de ejemplo:</span><span class="sxs-lookup"><span data-stu-id="f06e8-112">Follow this example tooinvoke hello cmdlet:</span></span>

   ```
   New-AzureService -ServiceName "mytestcloudservice" -Location "Central US" -Label "mytestcloudservice"
   ```

<span data-ttu-id="f06e8-113">Para obtener más información acerca de cómo crear el servicio de nube de Azure de hello, ejecute:</span><span class="sxs-lookup"><span data-stu-id="f06e8-113">For more information about creating hello Azure cloud service, run:</span></span>

```
Get-help New-AzureService
```

### <a name="next-steps"></a><span data-ttu-id="f06e8-114">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="f06e8-114">Next steps</span></span>
* <span data-ttu-id="f06e8-115">Hola toomanage implementación del servicio en la nube, consulte toohello [Get-AzureService](https://msdn.microsoft.com/library/azure/dn495131.aspx), [Remove-AzureService](https://msdn.microsoft.com/library/azure/dn495120.aspx), y [Set-AzureService](https://msdn.microsoft.com/library/azure/dn495242.aspx) comandos.</span><span class="sxs-lookup"><span data-stu-id="f06e8-115">toomanage hello cloud service deployment, refer toohello [Get-AzureService](https://msdn.microsoft.com/library/azure/dn495131.aspx), [Remove-AzureService](https://msdn.microsoft.com/library/azure/dn495120.aspx), and [Set-AzureService](https://msdn.microsoft.com/library/azure/dn495242.aspx) commands.</span></span> <span data-ttu-id="f06e8-116">También puede hacer referencia demasiado[tooconfigure cómo los servicios de nube](cloud-services-how-to-configure.md) para obtener más información.</span><span class="sxs-lookup"><span data-stu-id="f06e8-116">You may also refer too[How tooconfigure cloud services](cloud-services-how-to-configure.md) for further information.</span></span>
* <span data-ttu-id="f06e8-117">toopublish su servicio de nube tooAzure del proyecto, consulte toohello **PublishCloudService.ps1** código de ejemplo de [la entrega continua para servicio de nube en Azure](cloud-services-dotnet-continuous-delivery.md).</span><span class="sxs-lookup"><span data-stu-id="f06e8-117">toopublish your cloud service project tooAzure, refer toohello  **PublishCloudService.ps1** code sample from [Continuous delivery for cloud service in Azure](cloud-services-dotnet-continuous-delivery.md).</span></span>
