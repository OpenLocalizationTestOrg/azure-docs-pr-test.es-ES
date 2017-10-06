---
title: "una aplicación con el punto de conexión de v2.0 de hello Azure AD mediante el portal de hello aaaRegister | Documentos de Microsoft"
description: "Cómo tooregister una aplicación con Microsoft para habilitar el inicio de sesión y acceder a Microsoft services utilizando el punto de conexión de hello v2.0"
services: active-directory
documentationcenter: 
author: lnalepa
manager: mbaldwin
editor: 
ms.assetid: bb2f701f-3bc3-4759-94a5-8b9d53a8a0b6
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/01/2017
ms.author: lenalepa
ms.custom: aaddev
ms.openlocfilehash: c56c98906656062435516e820cb318a04c03149c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooregister-an-app-with-hello-v20-endpoint"></a>¿Cómo tooregister una aplicación con el punto de conexión de hello v2.0
toobuild una aplicación que acepta MSA & Azure AD iniciar sesión, primero deberá tooregister una aplicación con Microsoft.  En este momento, no ser capaz de toouse las aplicaciones existentes que pueda tener con Azure AD o MSA - deberá toocreate una marca de nuevo.

> [!NOTE]
> No todas las características y escenarios de Azure Active Directory son compatibles con el punto de conexión de hello v2.0.  toodetermine si debe utilizar Hola v2.0 extremo, que conozca [v2.0 limitaciones](active-directory-v2-limitations.md).
> 
> 

## <a name="visit-hello-microsoft-app-registration-portal"></a>Visite el portal de registro de aplicación de Microsoft de Hola
Lo primero es lo primero: Navegue demasiado[https://apps.dev.microsoft.com/?deeplink=/appList](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList).  Este es un nuevo portal de registro para aplicaciones donde puede administrar sus aplicaciones de Microsoft.

Inicie sesión con una cuenta personal o una cuenta profesional o educativa de Microsoft.  Si no tiene ninguna de ellas, suscríbase para una nueva cuenta personal. Adelante, no le llevará mucho tiempo; aquí le esperamos.

¿Ha acabado? Ahora debería estar viendo su lista de aplicaciones de Microsoft, que probablemente esté vacía.  Cambiemos eso.

Haga clic en **Agregar una aplicación** y asígnele un nombre.  portal de Hello asignará a la aplicación un identificador único global de aplicación que va a utilizar más adelante en el código.  Si la aplicación incluye un componente de servidor que necesita tokens de acceso para llamar a las API (pensar: Office, Azure o su propia API web), le interesará toocreate una **secreto de aplicación** aquí también.

A continuación, agregue Hola plataformas que se va a usar la aplicación.

* Para las aplicaciones basadas en web, proporcione un **URI de redirección** adonde se puedan enviar los mensajes de inicio de sesión.
* Para las aplicaciones móviles, copia profundidad predeterminada de hello crea automáticamente de uri de redireccionamiento.

Si lo desea, puede personalizar Hola apariencia y comportamiento de la página de inicio de sesión en hello perfil.  Asegúrese de que tooclick **guardar** antes de continuar.

> [!NOTE]
> Cuando se crea una aplicación con [https://apps.dev.microsoft.com/?deeplink=/appList](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList), se registrará la aplicación hello en particular inquilinos de Hola de cuenta de hello que usa toosign en el portal de Hola.  Esto significa que no se puede registrar una aplicación en el inquilino de Azure AD con una cuenta personal de Microsoft.  Si explícitamente desea tooregister una aplicación en un inquilino determinado, inicie sesión con una cuenta que se creó originalmente en ese inquilino.
> 
> 

## <a name="build-a-quick-start-app"></a>Compilar una aplicación de inicio rápido
Ahora que tiene una aplicación de Microsoft, puede completar uno de nuestros tutoriales de inicio rápido de v2.0.  Estas son algunas recomendaciones:

[!INCLUDE [active-directory-v2-quickstart-table](../../../includes/active-directory-v2-quickstart-table.md)]

