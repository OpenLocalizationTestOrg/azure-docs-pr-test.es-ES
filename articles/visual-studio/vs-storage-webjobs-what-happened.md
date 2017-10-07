---
title: "¿aaaWhat produjo toomy proyecto de trabajo Web (servicio de almacenamiento de Azure de Visual Studio conectado)? | Microsoft Docs"
description: "Describe lo que sucedió en un proyecto WebJob de Azure después de conectar la cuenta de almacenamiento de tooa con Visual Studio servicios conectados"
services: storage
documentationcenter: 
author: kraigb
manager: ghogen
editor: 
ms.assetid: 36ae7ff7-c22c-47eb-b220-049d61618c74
ms.service: storage
ms.workload: web
ms.tgt_pltfrm: vs-what-happened
ms.devlang: na
ms.topic: article
ms.date: 12/02/2016
ms.author: kraigb
ms.openlocfilehash: ed0ce75f5b23eca3c41dacb48564d6e5b846f395
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="what-happened-toomy-webjob-project-visual-studio-azure-storage-connected-service"></a>¿Qué proyecto de WebJob toomy problema (servicio de almacenamiento de Azure de Visual Studio conectado)?
## <a name="references-added"></a>Se han agregado referencias
paquete de NuGet de almacenamiento de Azure de Hola se agregó tooor actualizado en el proyecto de Visual Studio.  
Este paquete agrega Hola siguientes referencias de. NET:

* **Microsoft.Data.Edm**
* **Microsoft.Data.OData**
* **Microsoft.Data.Services.Client**
* **Microsoft.WindowsAzure.ConfigurationManager**
* **Microsoft.WindowsAzure.Storage**
* **Newtonsoft.Json**
* **System.Data**
* **System.Spatial**

## <a name="connection-string-for-azure-storage-added"></a>Se ha agregado la cadena de conexión para Almacenamiento de Azure.
En el archivo App.config de hello del proyecto, Hola **AzureWebJobsStorage** y **AzureWebJobsDashboard** entradas se actualizaron con la cadena de conexión y la clave de la cuenta de almacenamiento de hello seleccionado.

Para obtener más información, consulte [Recursos de documentación de WebJobs de Azure](http://go.microsoft.com/fwlink/?linkid=390226).

