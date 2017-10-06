---
title: aaaWhat produjo proyecto toomy ASP.NET 5 (servicios de Visual Studio conectados) | Documentos de Microsoft
description: "Describe lo que sucede después de conexión de cuenta de almacenamiento de Azure tooan en un proyecto de Visual Studio ASP.NET 5 mediante Visual Studio servicios conectados"
services: storage
documentationcenter: 
author: TomArcher
manager: douge
editor: 
ms.assetid: e7caa9fa-c780-45eb-a546-299fc1c68455
ms.service: storage
ms.workload: web
ms.tgt_pltfrm: vs-what-happened
ms.devlang: na
ms.topic: article
ms.date: 12/02/2016
ms.author: tarcher
ms.openlocfilehash: 9323bc5317fa2ba0cd42aecd01982f8c2b23d20a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="what-happened-toomy-aspnet-5-project-visual-studio-azure-storage-connected-services"></a>¿Qué proyecto toomy problema ASP.NET 5 (servicios de almacenamiento de Azure de Visual Studio conectados)?
## <a name="references-added"></a>Se han agregado referencias
paquete de NuGet de almacenamiento de Azure de Hola se agregó el proyecto de Visual Studio tooyour.  
Este paquete agrega Hola siguientes referencias de. NET:

* **Microsoft.Data.Edm**
* **Microsoft.Data.OData**
* **Microsoft.Data.Services.Client**
* **Microsoft.WindowsAzure.Configuration**
* **Microsoft.WindowsAzure.Storage**
* **Newtonsoft.Json**
* **System.Data**
* **System.Spatial**

Además, el paquete de NuGet hello **Microsoft.Framework.Configuration.Json** se ha agregado.

## <a name="connection-string-for-azure-storage-added"></a>Se ha agregado la cadena de conexión para Almacenamiento de Azure.
En archivo de hello config.json del proyecto, se crea un elemento con la cadena de conexión y la clave de la cuenta de almacenamiento de hello seleccionado.

Para más información, vea [ASP.NET 5](http://www.asp.net/vnext).

