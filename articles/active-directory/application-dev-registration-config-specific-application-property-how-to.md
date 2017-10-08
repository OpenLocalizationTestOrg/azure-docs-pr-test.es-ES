---
title: "aaaHow toofill los campos específicos de una aplicación desarrollada internamente | Documentos de Microsoft"
description: "Instrucciones sobre cómo toofill out específicos de campos cuando va a registrar una aplicación desarrollada personalizada con Azure AD"
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
ms.openlocfilehash: 7e07bc45c58542edb3863db5aad7c845f1a1772e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="how-toofill-out-specific-fields-for-a-custom-developed-application"></a>¿Cómo toofill los campos específicos para una aplicación desarrollados de forma personalizada

En este artículo se proporciona una breve descripción de todos los campos disponibles de hello en el formulario de registro de aplicación Hola de hello [portal de Azure](https://portal.azure.com).

## <a name="register-a-new-application"></a>Registro de una nueva aplicación

-   tooregister una nueva aplicación, navegar toohello [portal de Azure](https://portal.azure.com).

-   En el panel de navegación izquierdo de hello, haga clic en **Azure Active Directory.**

-   Haga clic en **Registros de aplicaciones** y en **Agregar**.

-   Abra este formulario de registro de aplicación Hola.

## <a name="fields-in-hello-application-registration-form"></a>Campos de formulario de registro de aplicación Hola


| Campo            | Description                                                                              |
|------------------|------------------------------------------------------------------------------------------|
| Nombre             | nombre de Hola de aplicación hello. Debe tener un mínimo de cuatro caracteres.                |
| Tipo de aplicación | **Aplicación web / API web**: aplicación que representa una aplicación web, una API web o ambas cosas 
| |**Nativo**: aplicación que puede instalarse en el dispositivo o equipo de un usuario           |
| URL de inicio de sesión      | dirección URL de Hola donde los usuarios pueden iniciar sesión en toouse la aplicación                                  |

Una vez haya rellenado Hola por encima de los campos, aplicación hello esté registrado en hello portal de Azure, y se redirigirá toohello página de la aplicación. Hola **configuración** botón en el panel de la aplicación hello abre la página de configuración de hello, que tiene más campos que toocustomize la aplicación. Hola tabla siguiente describen todos los campos de hello en la página de configuración de Hola. Tenga en cuenta que, en función de si ha creado una aplicación web o una aplicación nativa, es posible que solo aparezca un subconjunto de estos campos.

| Campo           | Descripción                                                                                                                                                                                                                                                                                                     |
|-----------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Identificador de aplicación  | Cuando registra una aplicación, Azure AD le asigna un identificador de aplicación. puede utilizarse el identificador de la aplicación Hello toouniquely identificar la aplicación en las solicitudes de autenticación tooAzure AD, así como recursos de tooaccess como Hola API Graph.                                                          |
| URI del identificador de la aplicación      | Debe ser un URI único, normalmente del formulario de hello **https://&lt;inquilino\_nombre&gt;/&lt;aplicación\_nombre&gt;.** Se utiliza durante el flujo de concesión de autorización de hello, como un recurso de identificador único toospecify Hola qué token Hola se debe emitir para. También deja de estar aud' hello' notificación de token de acceso de hello emitido. |
| Cargar nuevo logotipo | Puede usar este tooupload un logotipo para su aplicación. logotipo de Hello debe estar en formato .bmp, .jpg o. png y tamaño de archivo de hello debe ser inferior a 100KB. dimensiones de Hello para la imagen de hello deben ser 215 x 215 píxeles, con dimensiones de la imagen central de 94 x 94 píxeles.                                                       |
| URL de página principal   | Se trata de hello sesión dirección URL especificada durante el registro de aplicación.                                                                                                                                                                                                                                              |
| URL de cierre de sesión      | Esta dirección de URL de cierre de sesión de cierre de sesión único de Hola. Azure AD envía una dirección URL toothis la solicitud de cierre de sesión cuando el usuario de hello elimina su sesión con Azure AD con cualquier otra aplicación registrado.                                                                                                                                       |
| Multiinquilino  | Este parámetro especifica si se puede usar la aplicación hello por varios inquilinos. Normalmente, esto significa que las organizaciones externas pueden usar su aplicación mediante el registro en su inquilino y conceder acceso tootheir datos de la organización.                                                                   |
| URL de respuesta      | direcciones URL de respuesta de Hello son puntos de conexión de hello en Azure AD devolver los tokens que solicita la aplicación.                                                                                                                                                                                                          |
| URI de redirección   | Para aplicaciones nativas, esto es donde el usuario Hola ser enviado toofollowing la autorización correctamente. Las fuentes de la aplicación Hola OAuth 2.0 solicitud coincide con uno de los valores de hello registrado en el portal de Hola URI de redireccionamiento de Azure verificación de AD que Hola.                                                            |
| simétricas            | Puede crear claves tooprogrammatically acceso web API protegidas por Azure AD sin ninguna interacción del usuario. De hello \* \*claves\* \* página, especifique una fecha de expiración de hello y descripción de la clave y guardar toogenerate Hola clave. Tome toosave seguro en algún lugar seguro, ya no será capaz de tooaccess, más adelante.             |

## <a name="next-steps"></a>Pasos siguientes
[Administración de aplicaciones con Azure Active Directory](active-directory-enable-sso-scenario.md)
