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
ms.openlocfilehash: badc47e131290a56a507592f944a0fc7093260a6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
## <a name="configure-your-aspnet-web-app-with-hello-applications-registration-information"></a>Configurar la aplicación Web ASP.NET con la información de registro de la aplicación hello

En este paso, configurará el toouse proyecto SSL y, a continuación, utilizar tooconfigure de dirección URL de SSL de hello información de registro de la aplicación. Después de esto, Agregar aplicación hello' solución de tooyour de información de registro a través de *web.config*.

1.  En el Explorador de soluciones, seleccione el proyecto de Hola y examine hello `Properties` ventana (si no ve una ventana de propiedades, presione F4)
2.  Cambio `SSL Enabled` demasiado`True`
3.  Copiar valor de Hola de `SSL URL` anterior y péguelo en hello `Redirect URL` campo en la parte superior de Hola de esta página, a continuación, haga clic en *actualización*:<br/><br/>![Propiedades del proyecto](media/active-directory-serversidewebapp-aspnetwebappowin-configure/vsprojectproperties.png)<br />
4.  Agregue los siguiente hello en `web.config` archivo se encuentra en la carpeta de la raíz, en la sección `configuration\appSettings`:

```xml
<add key="ClientId" value="[Enter hello application Id here]" />
<add key="RedirectUri" value="[Enter hello Redirect URL here]" />
<add key="Tenant" value="common" />
<add key="Authority" value="https://login.microsoftonline.com/{0}/v2.0" /> 
```
