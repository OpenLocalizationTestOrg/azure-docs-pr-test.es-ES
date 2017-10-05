---
title: "Información acerca de la verificación en dos pasos de Azure MFA | Microsoft Docs"
description: "En este tema se explica qué es Azure Multi-factor Authentication, por qué usar MFA, aporta más información sobre el cliente de Multi-Factor Authentication y los distintos métodos y versiones disponibles. "
keywords: "introducción a MFA, introducción general a mfa, qué es mfa"
services: multi-factor-authentication
documentationcenter: 
author: kgremban
manager: femila
editor: yossib
ms.assetid: c40d7a34-1274-4496-96b0-784850c06e9b
ms.service: multi-factor-authentication
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/03/2017
ms.author: kgremban
ms.openlocfilehash: 7334ab5b278c3339fdbc2e363fd5c609604d3e14
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="what-is-azure-multi-factor-authentication"></a>¿Qué es Azure Multi-Factor Authentication?
La verificación en dos pasos es un método de autenticación que requiere más de un método de comprobación y agrega un segundo nivel importante de seguridad crítico a las transacciones e inicios de sesión del usuario. Funciona mediante la solicitud de dos o más de los siguientes métodos de verificación:

* Un elemento que conoce (normalmente una contraseña).
* Un elemento del que dispone (un dispositivo de confianza que no se puede duplicar con facilidad, como un teléfono).
* Un elemento físico que le identifica (biométrica).

<center>![Nombre de usuario y contraseña](./media/multi-factor-authentication/pword.png) &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;![Certificados](./media/multi-factor-authentication/phone.png) &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;![Smartphone](./media/multi-factor-authentication/hware.png) &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;![Tarjeta inteligente](./media/multi-factor-authentication/smart.png) &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;![Tarjeta inteligente virtual](./media/multi-factor-authentication/vsmart.png) &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;![Nombre de usuario y contraseña](./media/multi-factor-authentication/cert.png)</center>

Azure Multi-Factor Authentication (MFA) es la solución de Microsoft de comprobación de dos pasos. Azure MFA ayuda a proteger el acceso a los datos y las aplicaciones, al tiempo que satisface la demanda de los usuarios de un proceso de inicio de sesión simple. Ofrece una autenticación segura a través de una gran variedad de métodos de comprobación (como la comprobación mediante llamadas telefónicas, mensajes de texto o aplicaciones móviles).

> [!VIDEO https://channel9.msdn.com/Blogs/Azure/WA-MFA-Overview/player]
>
>

## <a name="why-use-azure-multi-factor-authentication"></a>¿Por qué usar Azure Multi-Factor Authentication?
Hoy en día, ahora más que nunca, las personas están cada vez más conectadas. Con los smartphones, tabletas, equipos portátiles y equipos de sobremesa, las personas tienen varias opciones para conectarse y permanecer conectados en cualquier momento. Pueden acceder a sus cuentas y las aplicaciones desde cualquier lugar, lo que significa que pueden ser más productivos y atender mejor a sus clientes.

Azure Multi-Factor Authentication es una solución fácil de usar, escalable y confiable que proporciona un segundo método de autenticación para que los usuarios siempre estén protegidos.

| ![Fácil de usar](./media/multi-factor-authentication/simple.png) | ![Escalable](./media/multi-factor-authentication/scalable.png) | ![Siempre protegido](./media/multi-factor-authentication/protected.png) | ![Confiable](./media/multi-factor-authentication/reliable.png) |
|:---:|:---:|:---:|:---:|
| **Fácil de usar** |**Escalable** |**Siempre protegido** |**Confiable** |

* **Fácil de usar** : Azure Multi-Factor Authenticaton es fácil de configurar y utilizar. La protección adicional que se incluye con Azure Multi-Factor Authentication permite a los usuarios administrar sus propios dispositivos. Y lo mejor de todo es que en muchos casos se puede configurar con unos pocos clics.
* **Escalable** : Azure Multi-Factor Authenticaton utiliza la potencia de la nube y se integra con la instancia local de Active Directory y aplicaciones personalizadas. Esta protección se extiende incluso a los escenarios críticos de gran volumen.
* **Siempre protegido** Azure Multi-Factor Authenticaton ofrece autenticación segura mediante los más elevados estándares del sector.
* **Confiable** : se garantiza la disponibilidad del 99,9% de Azure Multi-Factor Authenticaton. Se considera que el servicio no está disponible cuando no puede recibir ni procesar las solicitudes de comprobación para la comprobación en dos pasos.

> [!VIDEO https://channel9.msdn.com/Blogs/Azure/Windows-Azure-Multi-Factor-Authentication/player]


## <a name="next-steps"></a>Pasos siguientes

- Lea [Cómo funciona Azure Multi-Factor Authentication](multi-factor-authentication-how-it-works.md).

- Obtenga información sobre las diferentes [versiones y métodos de utilización de Azure Multi-Factor Authentication](multi-factor-authentication-versions-plans.md).