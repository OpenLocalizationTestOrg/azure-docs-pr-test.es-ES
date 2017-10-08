---
title: aaaHow toogrant permisos tooa desarrollados de forma personalizada de aplicaciones | Documentos de Microsoft
description: "¿Cómo toogrant permisos tooyour aplicaciones personalizadas mediante Hola portal de Azure AD o un parámetro de dirección URL"
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
ms.openlocfilehash: e43a105fff60fbf912bdf4f60260f86ee289328d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="how-toogrant-permissions-tooa-custom-developed-application"></a>¿Cómo toogrant permisos tooa desarrollados de forma personalizada aplicación

Si desea toogrant consentimiento de forma preferente en la aplicación o se ejecuta en un error que no ha dado su consentimiento tooan aplicación, pruebe lo siguiente.

## <a name="how-tooperform-admin-consent-for-your-application"></a>¿Cómo tooperform consentimiento del Administrador de la aplicación

Esto tiene el efecto de hello de la concesión de consentimiento toohello aplicación para todos los usuarios de su organización.

1. Navegue toohello **registros de aplicaciones** hoja como una **administrador global**, a continuación, seleccione aplicación hello.

2. Seleccione **permisos necesarios**y por último, pulse hello **conceder permisos** situado en la parte superior de Hola de hoja de Hola.

Como alternativa, puede construir una solicitud demasiado*login.microsoftonline.com* con sus configuraciones de aplicación y anexar en *& prompt = admin\_consentimiento*. Después de iniciar sesión con credenciales de administrador, aplicación hello ha concedido consentimiento para todos los usuarios.

## <a name="how-tooforce-user-consent-for-your-application"></a>¿Cómo tooforce usuario dar su consentimiento para la aplicación

* Anexar a las solicitudes de autenticación *& prompt = consentimiento* que requiere que los usuarios finales tooconsent cada vez que se autentiquen.

## <a name="next-steps"></a>Pasos siguientes

[Integración de aplicaciones y consentimiento tooAzureAD](https://docs.microsoft.com/en-us/azure/active-directory/develop/active-directory-integrating-applications)

[Consentimiento y permisos para las aplicaciones convergentes v2.0 de Azure AD](https://docs.microsoft.com/en-us/azure/active-directory/develop/active-directory-v2-scopes)<br>

[Azure AD en StackOverflow](http://stackoverflow.com/questions/tagged/azure-active-directory)
