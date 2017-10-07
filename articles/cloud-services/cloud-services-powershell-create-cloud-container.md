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
# <a name="use-an-azure-powershell-command-toocreate-an-empty-cloud-service-container"></a>Usar un toocreate de comandos de PowerShell de Azure un contenedor de servicios de nube vacío
Este artículo explica cómo tooquickly crear un contenedor de servicios en la nube mediante cmdlets de PowerShell de Azure. Siga estos pasos hello:

1. Instalar cmdlet de PowerShell de Microsoft Azure Hola de hello [descargas de Azure PowerShell](http://aka.ms/webpi-azps) página.
2. Abra el símbolo del sistema de PowerShell de Hola.
3. Hola de uso [Add-AzureAccount](https://msdn.microsoft.com/library/dn495128.aspx) toosign en.

   > [!NOTE]
   > Para obtener más instrucciones sobre cómo instalar Hola cmdlet de PowerShell de Azure y conectar tooyour suscripción de Azure, consulte demasiado[cómo tooinstall y configurar Azure PowerShell](/powershell/azure/overview).
   >
   >
4. Hola de uso **New-AzureService** cmdlet toocreate un contenedor de servicios de nube de Azure vacío.

    ```
    New-AzureService [-ServiceName] <String> [-AffinityGroup] <String> [[-Label] <String>] [[-Description] <String>] [[-ReverseDnsFqdn] <String>] [<CommonParameters>]
    New-AzureService [-ServiceName] <String> [-Location] <String> [[-Label] <String>] [[-Description] <String>] [[-ReverseDnsFqdn] <String>] [<CommonParameters>]
   ```
5. Siga este cmdlet de hello tooinvoke de ejemplo:

   ```
   New-AzureService -ServiceName "mytestcloudservice" -Location "Central US" -Label "mytestcloudservice"
   ```

Para obtener más información acerca de cómo crear el servicio de nube de Azure de hello, ejecute:

```
Get-help New-AzureService
```

### <a name="next-steps"></a>Pasos siguientes
* Hola toomanage implementación del servicio en la nube, consulte toohello [Get-AzureService](https://msdn.microsoft.com/library/azure/dn495131.aspx), [Remove-AzureService](https://msdn.microsoft.com/library/azure/dn495120.aspx), y [Set-AzureService](https://msdn.microsoft.com/library/azure/dn495242.aspx) comandos. También puede hacer referencia demasiado[tooconfigure cómo los servicios de nube](cloud-services-how-to-configure.md) para obtener más información.
* toopublish su servicio de nube tooAzure del proyecto, consulte toohello **PublishCloudService.ps1** código de ejemplo de [la entrega continua para servicio de nube en Azure](cloud-services-dotnet-continuous-delivery.md).
