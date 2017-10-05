---
title: "Introducción al escritorio de Windows en Azure AD v2: configuración | Microsoft Docs"
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
ms.openlocfilehash: 5e83171846517496e221f0a84565cdf7b77514df
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
## <a name="add-the-applications-registration-information-to-your-app"></a><span data-ttu-id="df013-103">Adición de información de registro de la aplicación a su aplicación</span><span class="sxs-lookup"><span data-stu-id="df013-103">Add the application’s registration information to your app</span></span>
<span data-ttu-id="df013-104">En este paso, debe agregar el identificador de aplicación a su proyecto.</span><span class="sxs-lookup"><span data-stu-id="df013-104">In this step, you need to add the Application Id to your project.</span></span>

1.  <span data-ttu-id="df013-105">Abra `App.xaml.cs` y reemplace la línea que contiene el `ClientId` con:</span><span class="sxs-lookup"><span data-stu-id="df013-105">Open `App.xaml.cs` and replace the line containing the `ClientId` with:</span></span>

```csharp
private static string ClientId = "[Enter the application Id here]";
```

### <a name="what-is-next"></a><span data-ttu-id="df013-106">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="df013-106">What is Next</span></span>

[<span data-ttu-id="df013-107">Probar y validar</span><span class="sxs-lookup"><span data-stu-id="df013-107">Test and Validate</span></span>](active-directory-mobileanddesktopapp-windowsdesktop-test.md)
