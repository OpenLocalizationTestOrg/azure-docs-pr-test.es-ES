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
# <a name="microsoft-power-bi-embedded-preview-troubleshooting"></a>Solución de problemas de la versión preliminar de Microsoft Power BI Embedded
Este artículo ofrecen respuestas acerca de cómo tootroubleshoot **Power BI Embedded**.

<a name="connection-string"/>

## <a name="setting-sql-server-connection-strings"></a>Configuración de cadenas de conexión de SQL Server
tooset una cadena de conexión de SQL Server, deberá toofollow un formato concreto. A continuación se muestra una cadena de conexión de ejemplo para SQL Server.

```
"Persist Security Info=False;Integrated Security=true;Initial Catalog=Northwind;server=(local)"
```

toolearn más información acerca de las cadenas de conexión de SQL Server, vea Hola siguientes artículos:

* [SQL Server Connection Strings](https://msdn.microsoft.com/library/jj653752.aspx)
* [SqlConnection.ConnectionString](https://msdn.microsoft.com/library/system.data.sqlclient.sqlconnection.connectionstring.aspx)

<a name="credentials"/>

## <a name="setting-credentials"></a>Configuración de credenciales
En caso de Hola que tenga las credenciales para un desarrollo o el entorno de ensayo, como nombre de usuario y la contraseña que tenga credenciales de tooupdate que coinciden con una solución de producción.

## <a name="see-also"></a>Otras referencias
* [Get started with Microsoft Power BI Embedded sample (Introducción a Microsoft Power BI Embedded: ejemplo)](power-bi-embedded-get-started-sample.md)
* [What is Microsoft Power BI Embedded (¿Qué es Microsoft Power BI Embedded?)](power-bi-embedded-what-is-power-bi-embedded.md)

