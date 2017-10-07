---
title: "Azure Active Directory B2C: solución de problemas de directivas personalizadas | Microsoft Docs"
description: "Obtenga información acerca de métodos toosolving errores cuando se trabaja con las directivas personalizadas en Azure Active Directory."
services: active-directory-b2c
documentationcenter: 
author: rojasja
manager: krassk
editor: rojasja
ms.assetid: 
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/07/2017
ms.author: joroja
ms.openlocfilehash: b9e1b46df1ddb29cdb90953e4a0d6f1dd085441f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-azure-ad-b2c-custom-policies-and-identity-experience-framework"></a>Solución de problemas de directivas personalizadas de Azure AD B2C y el marco de experiencia de identidad

Si utiliza Azure Active Directory B2C (Azure AD B2C) directivas personalizadas, es posible que experimente desafíos configurar Hola Identity Framework de experiencia en el formato XML de lenguaje de directiva.  Directivas personalizadas de aprendizaje toowrite pueden ser como un nuevo lenguaje de aprendizaje. En este artículo se describen las herramientas y las sugerencias que pueden ayudarle a detectar y solucionar problemas rápidamente. 

> [!NOTE]
> Este artículo se centra en la solución de problemas de configuración de directivas personalizadas de Azure AD B2C. No aborda Hola su biblioteca de identidad o aplicación de usuario de confianza.

## <a name="xml-editing"></a>Edición de XML

Hola error más comunes de configuración de directivas personalizadas es incorrecto con formato XML. Es fundamental contar con un buen editor XML. Un buen editor XML muestra XML nativo y contenido codificado por colores, rellena previamente términos comunes, mantiene los elementos XML indexados y puede validar con esquemas. Dos de nuestros editores XML favoritos son:

* [código de Visual Studio](https://code.visualstudio.com/)
* [Notepad++](https://notepad-plus-plus.org/)

La validación del esquema XML identifica los errores antes de cargar el archivo XML. En la carpeta raíz de Hola de módulo de inicio de hello, obtener definición de esquemas XML de hello TrustFrameworkPolicy_0.3.0.0.xsd. Para obtener más información, en la documentación de Hola de su editor XML, busque *herramientas XML* y *validación XML*.

Podría resultarle útil revisar las reglas del código XML. Azure AD B2C rechaza todos los errores de formato XML que detecta. En ocasiones, un formato XML incorrecto puede dar lugar a mensajes de error que resultan engañosos.

## <a name="upload-policies-and-policy-validation"></a>Validación de directivas y directivas de carga

 La validación de la carga de archivos XML es automática. Mayoría de los errores provocar Hola carga toofail. Validación incluye el archivo de directiva de Hola que va a cargar. También incluye la cadena de Hola de archivos de archivo de carga de hello hace referencia demasiado (Hola archivo de directiva de entidad de confianza, archivo de extensiones de hello y archivo de base de hello). 
 
 Errores de validación comunes siguientes Hola.

Fragmento de código de error: `... makes a reference tooClaimType with id "displaName" but neither hello policy nor any of its base policies contain such an element`
* Hola ClaimType valor podría estar mal escrito, o no existe en el esquema de Hola.
* ClaimType valores deben definirse en al menos uno de los archivos de hello en la directiva de Hola. 
    Por ejemplo: ` <ClaimType Id="socialIdpUserId">`
* Si ClaimType se define en el archivo de extensiones de hello, pero también se utiliza un valor de TechnicalProfile en el archivo de base de hello, cargar el archivo de base de hello produce un error.

Fragmento de código de error: `...makes a reference tooa ClaimsTransformation with id...`
* Hola causas de error Hola podría ser Hola igual para error de ClaimType Hola.

Fragmento de código de error: `Reason: User is currently logged as a user of 'yourtenant.onmicrosoft.com' tenant. In order toomanage 'yourtenant.onmicrosoft.com', please login as a user of 'yourtenant.onmicrosoft.com' tenant`
* Compruebe ese valor de TenantId de Hola Hola  **\<TrustFrameworkPolicy\>**  y  **\<BasePolicy\>**  elementos coinciden con el destino de Azure AD B2C inquilino.  

## <a name="troubleshoot-hello-runtime"></a>Solucionar problemas en tiempo de ejecución de Hola

* Use `Run Now` y `https://jwt.io` tootest las directivas independientemente de la web o aplicaciones móviles. Este sitio web actúa como una aplicación de usuario de confianza. Muestra el contenido de Hola de hello JSON Web Token (JWT) que se genera mediante la directiva de Azure AD B2C. toocreate una aplicación de prueba de identidad experiencia Framework, Hola de uso después de valores:
    * Nombre: TestApp
    * Aplicación web/API web: No
    * Cliente nativo: No

* intercambio de hello tootrace de mensajes entre el explorador del cliente y Azure AD B2C, use [Fiddler](http://www.telerik.com/fiddler). Puede ayudarle a detectar un error en el recorrido del usuario en los pasos de la orquestación.

* En **modo de desarrollo**, use **Application Insights** actividad de hello tootrace de su viaje de usuario de marco de la experiencia de identidad. En **modo de desarrollo**, puede observar exchange Hola de notificaciones entre Hola Framework de la experiencia de identidad y hello distintos proveedor de notificaciones que se define mediante perfiles técnicos, como proveedores de identidades, servicios basados en la API directorio de usuarios de Azure AD B2C Hello y otros servicios, como varios-Factor-autenticación de Azure.  

## <a name="recommended-practices"></a>Procedimientos recomendados

**Mantenga varias versiones de los escenarios. Agrúpelas en un proyecto con la aplicación.** base de Hello, extensiones y archivos de entidad de confianza dependen directamente entre sí. Guárdelos como un grupo. Tal y como se agregaron características nuevas directivas de tooyour, mantener versiones distintas de trabajo. Versiones de trabajo de la fase en su propio sistema con código de la aplicación hello interactúan de archivos.  Las aplicaciones pueden invocar muchas directivas de usuario de confianza diferentes en un inquilino. Estén depende de las notificaciones de Hola que esperan desde sus directivas de Azure AD B2C.

**Desarrolle y pruebe perfiles técnicos con recorridos de usuario conocidos.** Directivas de uso probado starter pack tooset sus perfiles técnicos de. Pruébelas por separado antes de incorporarlas a sus propios recorridos de usuario.

**Desarrolle y pruebe recorridos de usuario con perfiles técnicos conocidos.** Cambiar los pasos de orquestación Hola de un viaje de usuario de forma incremental. Compile progresivamente los escenarios previstos.

## <a name="next-steps"></a>Pasos siguientes

* En GitHub, descargue el archivo de .zip (https://github.com/Azure-Samples/active-directory-b2c-custom-policy-starterpack/archive/master.zip) [active-directory-b2c-custom-policy-starterpack] de Hola.
