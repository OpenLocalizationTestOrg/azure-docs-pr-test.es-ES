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
## <a name="add-hello-applications-registration-information-tooyour-app"></a><span data-ttu-id="f8000-103">Agregar aplicación de tooyour de información de registro de la aplicación hello</span><span class="sxs-lookup"><span data-stu-id="f8000-103">Add hello application’s registration information tooyour app</span></span>
<span data-ttu-id="f8000-104">En este paso, necesita proyecto tooyour de tooadd Hola Id. de aplicación.</span><span class="sxs-lookup"><span data-stu-id="f8000-104">In this step, you need tooadd hello Application Id tooyour project.</span></span>

1.  <span data-ttu-id="f8000-105">Abra `App.xaml.cs` y reemplace la línea de Hola que contiene hello `ClientId` con:</span><span class="sxs-lookup"><span data-stu-id="f8000-105">Open `App.xaml.cs` and replace hello line containing hello `ClientId` with:</span></span>

```csharp
private static string ClientId = "[Enter hello application Id here]";
```

### <a name="what-is-next"></a><span data-ttu-id="f8000-106">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="f8000-106">What is Next</span></span>

[<span data-ttu-id="f8000-107">Probar y validar</span><span class="sxs-lookup"><span data-stu-id="f8000-107">Test and Validate</span></span>](active-directory-mobileanddesktopapp-windowsdesktop-test.md)
