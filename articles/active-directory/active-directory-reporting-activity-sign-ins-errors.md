---
title: "códigos de error de informe de aaaSign de actividad en el portal de Azure Active Directory Hola | Documentos de Microsoft"
description: "Referencia sobre los códigos de error de los informes de actividad de inicio de sesión."
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
editor: 
ms.assetid: 4b18127b-d1d0-4bdc-8f9c-6a4c991c5f75
ms.service: active-directory
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/12/2017
ms.author: markvi
ms.reviewer: dhanyahk
ms.openlocfilehash: a0ca5b706bfeb0c7ce669712468a083a394712b4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="sign-in-activity-report-error-codes-in-hello-azure-active-directory-portal"></a>Códigos de error de informe de actividad de inicio de sesión en el portal de Azure Active Directory Hola

Con información de hello proporcionada por informe de inicios de sesión de usuario de hello, encontrar respuestas tooquestions como:

- ¿Quién ha iniciado sesión mediante Azure Active Directory?
- ¿En qué aplicaciones se inició sesión?
- ¿En qué inicios de sesión se produjeron errores y cuál fue la causa?

Códigos de este error de Hola de listas de tema y Hola descripciones relacionadas. 

## <a name="how-can-i-display-failed-sign-ins"></a>¿Cómo puedo mostrar los inicios de sesión en los que se produjeron errores? 

Las primera entrada tooall de punto de inicio de sesión en las actividades datos están  **[inicios de sesión](https://portal.azure.com/#blade/Microsoft_AAD_IAM/ActiveDirectoryMenuBlade/SignIns)**  en hello **actividad** sección de **Azure Active**.


![Actividad de inicio de sesión](./media/active-directory-reporting-activity-sign-ins-errors/61.png "Actividad de inicio de sesión")


En los informes de inicios de sesión, puede mostrar todos los inicios de sesión en los que se produjeron errores seleccionando **Error** como **Estado de inicio de sesión**.


![Actividad de inicio de sesión](./media/active-directory-reporting-activity-sign-ins-errors/06.png "Actividad de inicio de sesión")

Haga clic en un elemento de lista de muestra de Hola, abrir hello **detalles de actividad: inicios de sesión** hoja. Esta vista proporciona todos los detalles de Hola que realiza un seguimiento de Azure Active Directory acerca de inicios de sesión, incluidos hello **código de error de inicio de sesión** y un **motivo del error**.

![Actividad de inicio de sesión](./media/active-directory-reporting-activity-sign-ins-errors/05.png "Actividad de inicio de sesión")


Como un hello toousing alternativo datos de Azure tooaccess portal Hola inicios de sesión, también puede utilizar hello [API de informes](active-directory-reporting-api-getting-started-azure-portal.md).


Hello siguiente sección proporciona información general completa de todos los posibles errores y Hola relacionados con las descripciones. 

## <a name="error-codes"></a>Códigos de error

| Error| Descripción |
| --- | --- |
| 50001| entidad de servicio de Hello denominado X no se encontró en el inquilino Hola denominado Y. Esto puede ocurrir si no se instaló aplicación hello que Administrador de hello del inquilino de Hola. O entidad de seguridad de recursos no se encontró en el directorio de Hola o no es válido|
| 50008| Aserción de SAML faltan o están mal configurados en el token de Hola.|
| 50011| dirección de respuesta de Hello falta, mal configurada o no coincide con las direcciones de respuesta configuradas para la aplicación hello.|
| 50053| Cuenta está bloqueada porque el usuario intentó toosign en demasiadas veces con un Id. de usuario incorrecta o la contraseña.|
| 50054| Se utilizó una contraseña antigua para realizar la autenticación.|
| 50055| La contraseña no es válida o ha expirado.|
| 50057| La cuenta de usuario está deshabilitada.|
| 50058| No hay información acerca de la identidad del usuario se encuentra entre proporcionado por el usuario o las credenciales no se encontró en el inquilino o se envió una solicitud de inicio de sesión en modo silenciosa, pero ningún usuario ha iniciado sesión o servicio era de usuario de Hola de tooauthenticate no se puede.|
| 50074| Se requiere una autenticación sólida (segundo factor)|
| 50079| Usuario necesita tooenroll para autenticación de segundo factor|
| 50126| Nombre de usuario o contraseña no válidos, o nombre de usuario o contraseña locales no válidos.|
| 50131| Se usa en varios errores de acceso condicional. Estado de dispositivo de Windows incorrecta por ejemplo, solicitud bloqueada debido a actividad toosuspicious, la directiva de acceso y la directiva de seguridad de decisiones.|
| 50133| Sesión no es válida debido tooexpiration o último cambio de contraseña.|
| 50144| Ha expirado la contraseña de Active Directory del usuario.|
| 65001| X de la aplicación no tiene la aplicación de tooaccess de permiso Y o se ha revocado el permiso de Hola. O bien, hello usuario o un administrador no ha consentido aplicación de hello toouse con identificador X. Send una solicitud de autorización interactivo de este usuario y recursos. U Hola usuario o un administrador no ha consentido en la aplicación de hello toouse con identificador X. Send un tooact de administrador de inquilinos de autorización solicitud tooyour en nombre de la aplicación hello: Y para el recurso: Z.|
| 65005| aplicación Hello requiere la lista de acceso de recursos no contiene aplicaciones reconocibles por recurso de Hola o aplicación de cliente de hello solicitó tooresource de acceso que no se especificó en su lista de acceso de recurso necesario o el servicio de Graph devuelve incorrecta solicitud o no se encuentra el recurso.|
| 70001| aplicación Hello denominado X no se encontró en el inquilino, Hola denominadas Y. Esto puede ocurrir si no se instaló la aplicación hello por Hola Administrador de inquilinos de Hola o tooby con consentimiento cualquier usuario inquilino Hola. Posible que haya enviado al inquilino en la toohello de solicitud de autenticación incorrecto.|
| 80001| No hay ningún agente de autenticación disponible.|
| 80002| El tiempo de espera se agotó para la solicitud de validación de contraseña del agente de autenticación.|
| 80003| El agente de autenticación recibió una respuesta no válida.|
| 80004| Se usó un nombre principal de usuario (UPN) incorrecto en una solicitud de inicio de sesión.|
| 80005| Error del agente de autenticación.|
| 80007| Autenticación agente no se puede tooconnect tooActive Directory.|
| 80010| Contraseña de no se puede toodecrypt de agente de autenticación.|
| 81001| El vale de Kerberos del usuario es demasiado grande.|
| 81002| Vale de Kerberos del usuario no se puede toovalidate.|
| 81003| Vale de Kerberos del usuario no se puede toovalidate.|
| 81004| Error al intentar la autenticación Kerberos.|
| 81008| Vale de Kerberos del usuario no se puede toovalidate.|
| 81009| Vale de Kerberos del usuario no se puede toovalidate.|
| 81010| No se pudo SSO sin problemas porque el vale de Kerberos del usuario de hello ha expirado o no es válido.|
| 81011| Objeto de usuario de toofind no se puede basado en la información de vale de Kerberos del usuario de Hola.|
| 81012| usuario de Hello intentar toosign en tooAzure AD es diferente de usuario Hola iniciado sesión en el dispositivo de Hola.|
| 81013| Objeto de usuario de toofind no se puede basado en la información de vale de Kerberos del usuario de Hola.|
| 90014| Se utiliza en varios casos cuando un campo esperado no está presente en la credencial de Hola.|
| 90093| Gráfico devuelto con código de error prohibido de solicitud de saludo.|



## <a name="next-steps"></a>Pasos siguientes

Para obtener más información, vea hello [informes de actividad de inicio de sesión en el portal de Azure Active Directory hello](active-directory-reporting-activity-sign-ins.md).

