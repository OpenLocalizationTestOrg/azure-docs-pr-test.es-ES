---
title: "aaaHow toofind una API específica necesaria para que una aplicación desarrollados de forma personalizada | Documentos de Microsoft"
description: "Cómo permisos de hello tooconfigure necesita tooaccess una API determinada en su personalizado desarrollan aplicación de Azure AD"
services: active-directory
documentationcenter: 
author: ajamess
manager: femila
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/11/2017
ms.author: asteen
ms.openlocfilehash: 7331129204d8b34b4ef9671749bd702f893768ff
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="how-toofind-a-specific-api-needed-for-a-custom-developed-application"></a>¿Cómo toofind una API específica necesaria para una aplicación desarrollados de forma personalizada

Acceso tooAPIs requieren la configuración de roles y ámbitos de acceso. Si desea tooexpose las aplicaciones de tooclient de las API de recursos aplicación web, necesitará roles y ámbitos de acceso de tooconfigure para hello API. Si desea que un tooaccess de aplicación cliente una API web, deberá tooconfigure permisos tooaccess Hola API en el registro de una aplicación Hola.

## <a name="configuring-a-resource-application-tooexpose-web-apis"></a>Configuración de una aplicación de recursos tooexpose web API

Al exponer su API, web Hola API se muestran en hello **seleccionar una API** lista al agregar el registro de la aplicación de permisos tooan. ámbitos de acceso tooadd, siga los pasos de hello descritos en [agregar acceso establece el ámbito de aplicación de recursos de tooyour](https://docs.microsoft.com/azure/active-directory/develop/active-directory-integrating-applications#adding-access-scopes-to-your-resource-application).

## <a name="configuring-a-client-application-tooaccess-web-apis"></a>Configurar una aplicación de cliente tooaccess web API

Cuando se agrega el registro de la aplicación de permisos tooyour, puede **agregar acceso de API** tooexposed web API. tooaccess las API web, siga los pasos de hello descritos en [agregar las API web de las credenciales o permisos tooaccess](https://docs.microsoft.com/azure/active-directory/develop/active-directory-integrating-applications#to-add-credentials-or-permissions-to-access-web-apis).

## <a name="next-steps"></a>Pasos siguientes

-   [Integración de aplicaciones con Azure Active Directory](https://docs.microsoft.com/azure/active-directory/develop/active-directory-integrating-applications)

-   [Descripción de manifiesto de aplicación de Azure Active Directory Hola](https://docs.microsoft.com/azure/active-directory/develop/active-directory-application-manifest)


