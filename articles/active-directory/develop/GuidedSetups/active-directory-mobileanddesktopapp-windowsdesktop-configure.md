---
title: "aaaAzure AD v2 escritorio Introducción a Windows - Configuración | Documentos de Microsoft"
description: "Cómo puede obtener una aplicación .NET de escritorio de Windows (XAML) un token de acceso y llamar a una API protegida por un punto de conexión de Azure Active Directory v2. | Microsoft Azure | Microsoft Azure"
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
ms.openlocfilehash: 39c257e3e0cb09491f6fe005877601bd46824d12
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
## <a name="create-an-application-express"></a>Creación de una aplicación (proceso rápido)
Ahora deberá tooregister la aplicación Hola *Portal de registro de aplicación de Microsoft*:
1. Registrar la aplicación a través de hello [Portal de registro de aplicación de Microsoft](https://apps.dev.microsoft.com/portal/register-app?appType=mobileAndDesktopApp&appTech=windowsDesktop&step=configure)
2.  Escriba el nombre de la aplicación y su correo electrónico.
3.  Asegúrese de que está activada la opción de hello para el programa de instalación interactiva
4.  Siga el identificador de la aplicación de hello instrucciones tooobtain hello y péguelo en el código

### <a name="add-your-application-registration-information-tooyour-solution-advanced"></a>Agregar la solución de tooyour información de registro de aplicación (avanzado)
Ahora deberá tooregister la aplicación Hola *Portal de registro de aplicación de Microsoft*:
1. Vaya toohello [Portal de registro de aplicación de Microsoft](https://apps.dev.microsoft.com/portal/register-app) tooregister una aplicación
2. Escriba el nombre de la aplicación y su correo electrónico. 
3. Asegúrese de que está desactivada la opción de hello para el programa de instalación interactiva
4. Haga clic en `Add Platform`, a continuación, seleccione `Native Application` y haga clic en Guardar.
5. Copiar Hola GUID de Id. de aplicación, vuelva tooVisual Studio, abra `App.xaml.cs` y reemplace `your_client_id_here` con hello que acaba de registrar el identificador de aplicación:

```csharp
private static string ClientId = "your_application_id_here";
```
