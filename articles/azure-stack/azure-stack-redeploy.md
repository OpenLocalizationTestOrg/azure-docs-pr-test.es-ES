---
title: aaaRedeploy pila de Azure | Documentos de Microsoft
description: "Cree una nueva implementación de Azure Stack."
services: azure-stack
documentationcenter: 
author: ErikjeMS
manager: byronr
editor: 
ms.assetid: 795af5ea-892d-40b1-a080-42e4472e4bba
ms.service: azure-stack
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 7/10/2017
ms.author: erikje
ms.openlocfilehash: ec26745bcb54edd7c26960eec55d41504aff1911
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="redeploy-azure-stack"></a><span data-ttu-id="d5468-103">Nueva implementación de Azure Stack</span><span class="sxs-lookup"><span data-stu-id="d5468-103">Redeploy Azure Stack</span></span>
<span data-ttu-id="d5468-104">tooredeploy pila de Azure, debe empezar de nuevo desde el principio tal y como se describe a continuación.</span><span class="sxs-lookup"><span data-stu-id="d5468-104">tooredeploy Azure Stack, you must start over from scratch as described below.</span></span>

## <a name="steps-tooredeploy-azure-stack"></a><span data-ttu-id="d5468-105">Pasos tooredeploy pila de Azure</span><span class="sxs-lookup"><span data-stu-id="d5468-105">Steps tooredeploy Azure Stack</span></span>
1. <span data-ttu-id="d5468-106">En el host del kit de desarrollo de hello, abra una consola de PowerShell con privilegios elevados > Navegue toohello asdk installer.ps1 script > ejecutarlo > haga clic en **reiniciar**.</span><span class="sxs-lookup"><span data-stu-id="d5468-106">On hello development kit host, open an elevated PowerShell console > navigate toohello asdk-installer.ps1 script > run it > click **Reboot**.</span></span>
2. <span data-ttu-id="d5468-107">Seleccione Hola sistema operativo base (no **Azure pila**) y haga clic en **siguiente**.</span><span class="sxs-lookup"><span data-stu-id="d5468-107">Select hello base operating system (not **Azure Stack**) and click **Next**.</span></span>
3. <span data-ttu-id="d5468-108">Después de que se reinicie el host de kit de desarrollo de hello, elimine el archivo de CloudBuilder.vhdx de Hola que se usó como parte de la implementación anterior de Hola.</span><span class="sxs-lookup"><span data-stu-id="d5468-108">After hello development kit host reboots, delete hello CloudBuilder.vhdx file that was used as part of hello previous deployment.</span></span>
4. <span data-ttu-id="d5468-109">[Implementar el kit de desarrollo de hello](azure-stack-run-powershell-script.md).</span><span class="sxs-lookup"><span data-stu-id="d5468-109">[Deploy hello development kit](azure-stack-run-powershell-script.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="d5468-110">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="d5468-110">Next steps</span></span>
[<span data-ttu-id="d5468-111">Conectar tooAzure pila</span><span class="sxs-lookup"><span data-stu-id="d5468-111">Connect tooAzure Stack</span></span>](azure-stack-connect-azure-stack.md)

