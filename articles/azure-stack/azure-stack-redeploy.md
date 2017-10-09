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
# <a name="redeploy-azure-stack"></a>Nueva implementación de Azure Stack
tooredeploy pila de Azure, debe empezar de nuevo desde el principio tal y como se describe a continuación.

## <a name="steps-tooredeploy-azure-stack"></a>Pasos tooredeploy pila de Azure
1. En el host del kit de desarrollo de hello, abra una consola de PowerShell con privilegios elevados > Navegue toohello asdk installer.ps1 script > ejecutarlo > haga clic en **reiniciar**.
2. Seleccione Hola sistema operativo base (no **Azure pila**) y haga clic en **siguiente**.
3. Después de que se reinicie el host de kit de desarrollo de hello, elimine el archivo de CloudBuilder.vhdx de Hola que se usó como parte de la implementación anterior de Hola.
4. [Implementar el kit de desarrollo de hello](azure-stack-run-powershell-script.md).

## <a name="next-steps"></a>Pasos siguientes
[Conectar tooAzure pila](azure-stack-connect-azure-stack.md)

