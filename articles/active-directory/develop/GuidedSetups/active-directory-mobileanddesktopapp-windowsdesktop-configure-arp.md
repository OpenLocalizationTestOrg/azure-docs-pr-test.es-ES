---
title: "aaaAzure AD v2 escritorio Introducción a Windows - Configuración | Documentos de Microsoft"
description: "Cómo puede obtener una aplicación .NET de escritorio de Windows (XAML) un token de acceso y llamar a una API protegida por un punto de conexión de Azure Active Directory v2."
services: active-directory
documentationcenter: dev-center-name
author: andretms
manager: mbaldwin
editor: 
ms.assetid: 820acdb7-d316-4c3b-8de9-79df48ba3b06
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 05/09/2017
ms.author: andret
ms.custom: aaddev
ms.openlocfilehash: d96d9eded200824a6f7ee234009dd0bb11b18b39
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
## <a name="add-hello-applications-registration-information-tooyour-app"></a>Agregar aplicación de tooyour de información de registro de la aplicación hello
En este paso, necesita proyecto tooyour de tooadd Hola Id. de aplicación.

1.  Abra `App.xaml.cs` y reemplace la línea de Hola que contiene hello `ClientId` con:

```csharp
private static string ClientId = "[Enter hello application Id here]";
```

### <a name="what-is-next"></a>Pasos siguientes

[Probar y validar](active-directory-mobileanddesktopapp-windowsdesktop-test.md)
