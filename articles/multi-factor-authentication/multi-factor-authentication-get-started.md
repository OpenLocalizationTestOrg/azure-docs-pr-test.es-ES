---
title: aaaChoose entre el servidor o en la nube MFA de Azure | Documentos de Microsoft
description: "Elegir la solución de seguridad de la autenticación multifactor de Hola que más le conviene pidiendo, qué am se intentaba toosecure y dónde están mis usuarios ubicado.  A continuación, elija la nube, Servidor MFA o AD FS."
services: multi-factor-authentication
documentationcenter: 
author: kgremban
manager: femila
editor: yossib
ms.assetid: ec2270ea-13d7-4ebc-8a00-fa75ce6c746d
ms.service: multi-factor-authentication
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 04/23/2017
ms.author: kgremban
ms.openlocfilehash: bd9639e5f744f586d9143c6e90b105ed645eecb6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="choose-hello-azure-multi-factor-authentication-solution-for-you"></a>Elegir la solución de Azure la autenticación multifactor de Hola para usted
Dado que hay varias versiones de Azure la autenticación multifactor (MFA), debemos respondemos a unos toofigure preguntas qué versión es uno toouse adecuado de Hola.  Estas preguntas son:

* [¿Qué estoy tratando la toosecure](#what-am-i-trying-to-secure)
* [Donde se encuentran los usuarios de Hola](#where-are-the-users-located)
* [¿Qué características necesito?](#what-featured-do-i-need)

Hello las secciones siguientes proporcionan instrucciones acerca de cómo determinar cada una de estas respuestas.

## <a name="what-am-i-trying-toosecure"></a>¿Qué estoy tratando la toosecure?
solución de comprobación de toodetermine Hola correcto en dos pasos, primero que debemos respondamos pregunta de Hola de lo que se está probando toosecure con un segundo método de autenticación.  ¿Es una aplicación que está en Azure?  ¿O un sistema de acceso remoto?  Mediante la determinación de lo que estemos tratando toosecure, podemos responder Hola pregunta que se necesita la autenticación multifactor toobe habilitado.  

| ¿Qué se está probando toosecure | MFA en la nube de Hola | Servidor MFA |
| --- |:---:|:---:|
| Aplicaciones propias de Microsoft |● |● |
| Aplicaciones de SaaS en Galería de aplicaciones de Hola |● |  |
| Aplicaciones web que se publican a través del proxy de aplicación de Azure AD |● |  |
| Aplicaciones de IIS que no se publican a través del proxy de aplicación de Azure AD | |● |
| Acceso remoto como VPN, RDG | ● | ● |

## <a name="where-are-hello-users-located"></a>Donde se encuentran los usuarios de Hola
A continuación, donde se encuentran los usuarios observando toodetermine Hola solución correcta toouse, ya sea en la nube de Hola o de manera local mediante Hola servidor MFA.

| Ubicación del usuario | MFA en la nube de Hola | Servidor MFA |
| --- |:---:|:---:|
| Azure Active Directory |● | |
| Azure AD y AD local mediante la federación con AD FS |● |● |
| Azure AD y AD local a través de DirSync, Azure AD Sync, Azure AD Connect - sin sincronización de contraseñas |● |● |
| Azure AD y AD local a través de DirSync, Azure AD Sync, Azure AD Connect - con sincronización de contraseñas |● | |
| Active Directory local | |● |

## <a name="what-features-do-i-need"></a>¿Qué características necesito?
Hello tabla siguiente compara las características de Hola que están disponibles con la autenticación multifactor en la nube de Hola y Hola servidor Multi-factor Authentication.

| Característica | MFA en la nube de Hola | Servidor MFA |
| --- |:---:|:---:|
| Notificación de aplicación móvil como segundo factor | ● | ● |
| Código de comprobación de aplicación móvil como segundo factor | ● | ● |
| Llamada de teléfono como segundo factor | ● | ● |
| SMS unidireccional como segundo factor | ● | ● |
| SMS bidireccional como segundo factor | | ● |
| Tokens de hardware como segundo factor | | ● |
| Contraseñas de aplicaciones para clientes de Office 365 que no admiten MFA | ● | |
| Control de administración sobre los métodos de autenticación | ● | ● |
| Modo de PIN | | ● |
| Alerta de fraude |● | ● |
| Informes de MFA |● | ● |
| Omisión por única vez | | ● |
| Saludos personalizados para las llamadas de teléfono | ● | ● |
| Identificador de llamada personalizable para llamadas telefónicas | ● | ● |
| IP de confianza | ● | ● |
| Recordar MFA para dispositivos de confianza | ● | |
| Acceso condicional | ● | ● |
| Memoria caché |  | ● |

## <a name="next-steps"></a>Pasos siguientes

Ahora que hemos determinado si la autenticación multifactor u Hola servidor MFA de forma local en la nube toouse, podemos comenzar cómo configurar y usar la autenticación multifactor Azure. **Seleccione el icono de Hola que representa el escenario**

<center>




[![Nube](./media/multi-factor-authentication-get-started/cloud2.png)](multi-factor-authentication-get-started-cloud.md)&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[![Servidor](./media/multi-factor-authentication-get-started/server2.png)](multi-factor-authentication-get-started-server.md)&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;</center>
