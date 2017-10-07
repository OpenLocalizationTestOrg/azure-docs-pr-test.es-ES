---
title: "solución de problemas de vista previa de Power BI Embedded aaaMicrosoft"
description: "Solución de problemas de la versión preliminar de Microsoft Power BI Embedded"
services: power-bi-embedded
documentationcenter: 
author: guyinacube
manager: erikre
editor: 
tags: 
ms.assetid: c8aee652-ed8b-4c66-9c63-f798b7a655b4
ms.service: power-bi-embedded
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: powerbi
ms.date: 01/06/2017
ms.author: asaxton
ms.openlocfilehash: a0a25cd73977c0ea0bd6b7c82e215412245771bc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="microsoft-power-bi-embedded-preview-troubleshooting"></a><span data-ttu-id="ff28b-103">Solución de problemas de la versión preliminar de Microsoft Power BI Embedded</span><span class="sxs-lookup"><span data-stu-id="ff28b-103">Microsoft Power BI Embedded Preview troubleshooting</span></span>
<span data-ttu-id="ff28b-104">Este artículo ofrecen respuestas acerca de cómo tootroubleshoot **Power BI Embedded**.</span><span class="sxs-lookup"><span data-stu-id="ff28b-104">This article provides answers for how  tootroubleshoot **Power BI Embedded**.</span></span>

<a name="connection-string"/>

## <a name="setting-sql-server-connection-strings"></a><span data-ttu-id="ff28b-105">Configuración de cadenas de conexión de SQL Server</span><span class="sxs-lookup"><span data-stu-id="ff28b-105">Setting SQL Server connection strings</span></span>
<span data-ttu-id="ff28b-106">tooset una cadena de conexión de SQL Server, deberá toofollow un formato concreto.</span><span class="sxs-lookup"><span data-stu-id="ff28b-106">tooset a SQL Server connecting string, you need toofollow a specific format.</span></span> <span data-ttu-id="ff28b-107">A continuación se muestra una cadena de conexión de ejemplo para SQL Server.</span><span class="sxs-lookup"><span data-stu-id="ff28b-107">Below is an example connection string for SQL Server.</span></span>

```
"Persist Security Info=False;Integrated Security=true;Initial Catalog=Northwind;server=(local)"
```

<span data-ttu-id="ff28b-108">toolearn más información acerca de las cadenas de conexión de SQL Server, vea Hola siguientes artículos:</span><span class="sxs-lookup"><span data-stu-id="ff28b-108">toolearn more about SQL Server connection strings, see hello following articles:</span></span>

* [<span data-ttu-id="ff28b-109">SQL Server Connection Strings</span><span class="sxs-lookup"><span data-stu-id="ff28b-109">SQL Server Connection Strings</span></span>](https://msdn.microsoft.com/library/jj653752.aspx)
* [<span data-ttu-id="ff28b-110">SqlConnection.ConnectionString</span><span class="sxs-lookup"><span data-stu-id="ff28b-110">SqlConnection.ConnectionString</span></span>](https://msdn.microsoft.com/library/system.data.sqlclient.sqlconnection.connectionstring.aspx)

<a name="credentials"/>

## <a name="setting-credentials"></a><span data-ttu-id="ff28b-111">Configuración de credenciales</span><span class="sxs-lookup"><span data-stu-id="ff28b-111">Setting credentials</span></span>
<span data-ttu-id="ff28b-112">En caso de Hola que tenga las credenciales para un desarrollo o el entorno de ensayo, como nombre de usuario y la contraseña que tenga credenciales de tooupdate que coinciden con una solución de producción.</span><span class="sxs-lookup"><span data-stu-id="ff28b-112">In hello case where you have credentials for a development or staging environment, such as user name and password, you might need tooupdate credentials that match a production solution.</span></span>

## <a name="see-also"></a><span data-ttu-id="ff28b-113">Otras referencias</span><span class="sxs-lookup"><span data-stu-id="ff28b-113">See Also</span></span>
* [<span data-ttu-id="ff28b-114">Get started with Microsoft Power BI Embedded sample (Introducción a Microsoft Power BI Embedded: ejemplo)</span><span class="sxs-lookup"><span data-stu-id="ff28b-114">Get started with sample</span></span>](power-bi-embedded-get-started-sample.md)
* [<span data-ttu-id="ff28b-115">What is Microsoft Power BI Embedded (¿Qué es Microsoft Power BI Embedded?)</span><span class="sxs-lookup"><span data-stu-id="ff28b-115">What is Power BI Embedded</span></span>](power-bi-embedded-what-is-power-bi-embedded.md)

