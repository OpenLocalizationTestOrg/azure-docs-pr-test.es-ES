---
title: "aaaAzure AD v2 ASP.NET Web Server Introducción - Config | Documentos de Microsoft"
description: "Implementación de inicio de sesión de Microsoft en una solución ASP.NET con una aplicación basada en un explorador web tradicional mediante el estándar OpenID Connect"
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
ms.openlocfilehash: e666be4622ad30aaa1e12e49ae56bbe1e129b2a9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
## <a name="create-an-application-express"></a>Creación de una aplicación (proceso rápido)
Ahora deberá tooregister la aplicación Hola *Portal de registro de aplicación de Microsoft*:
1. Registrar la aplicación a través de hello [Portal de registro de aplicación de Microsoft](https://apps.dev.microsoft.com/portal/register-app?appType=serverSideWebApp&appTech=aspNetWebAppOwin&step=configure)
2.  Escriba el nombre de la aplicación y su correo electrónico.
3.  Asegúrese de que está activada la opción de hello para el programa de instalación interactiva
4.  Siga las instrucciones de hello tooadd una aplicación de tooyour de dirección URL de redireccionamiento

## <a name="add-your-application-registration-information-tooyour-solution-advanced"></a>Agregar la solución de tooyour información de registro de aplicación (avanzado)
Ahora deberá tooregister la aplicación Hola *Portal de registro de aplicación de Microsoft*:
1. Vaya toohello [Portal de registro de aplicación de Microsoft](https://apps.dev.microsoft.com/portal/register-app) tooregister una aplicación
2. Escriba el nombre de la aplicación y su correo electrónico. 
3.  Asegúrese de que está desactivada la opción de hello para el programa de instalación interactiva
4.  Haga clic en `Add Platform` y luego en `Web`.
5.  Volver atrás tooVisual Studio y, en el Explorador de soluciones, seleccione el proyecto de Hola y mire la ventana de propiedades de hello (si no ve una ventana de propiedades, presione F4)
6.  Cambiar también SSL habilitado`True`
7.  Copiar dirección URL de SSL de Hola y agregar esta lista de toohello de dirección URL de URL de redireccionamiento en la lista del Portal de registro de hello de URL de redireccionamiento:<br/><br/>![Propiedades del proyecto](media/active-directory-serversidewebapp-aspnetwebappowin-configure/vsprojectproperties.png)<br />
8.  Agregue los siguiente hello en `web.config` ubicado en carpeta de raíz de hello en sección Hola `configuration\appSettings`:

```xml
<add key="ClientId" value="Enter_the_Application_Id_here" />
<add key="redirectUri" value="Enter_the_Redirect_URL_here" />
<add key="Tenant" value="common" />
<add key="Authority" value="https://login.microsoftonline.com/{0}/v2.0" /> 
```
<!-- Workaround for Docs conversion bug -->
<ol start="9">
<li>
Reemplace `ClientId` con hello que acaba de registrar el identificador de aplicación
</li>
<li>
Reemplace `redirectUri` con hello dirección URL de SSL del proyecto
</li>
</ol>
<!-- End Docs -->
