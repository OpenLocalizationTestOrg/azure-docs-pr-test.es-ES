---
title: aaaLearn sobre verificacion de MFA de Azure | Documentos de Microsoft
description: "¿Qué es la autenticación multifactor Azure, ¿por qué usar MFA, obtener más información sobre el cliente de la autenticación multifactor de Hola y Hola métodos y diferentes versiones disponibles. "
keywords: "Introducción tooMFA, información general de mfa, ¿qué es mfa"
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
ms.openlocfilehash: a91b8d6941d2b6ce72a789a97c57e10e594e7ada
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="what-is-azure-multi-factor-authentication"></a>¿Qué es Azure Multi-Factor Authentication?
Verificación en dos pasos es un método de autenticación que requiere más de un método de comprobación y agrega una segunda capa crítica de inicios de sesión de seguridad toouser y las transacciones. Funciona solicitando dos o más de hello siguiendo métodos de comprobación:

* Un elemento que conoce (normalmente una contraseña).
* Un elemento del que dispone (un dispositivo de confianza que no se puede duplicar con facilidad, como un teléfono).
* Un elemento físico que le identifica (biométrica).

<center>![Nombre de usuario y contraseña](./media/multi-factor-authentication/pword.png)&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;![Certificados](./media/multi-factor-authentication/phone.png)&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;![Smartphone](./media/multi-factor-authentication/hware.png)&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;![Tarjeta inteligente](./media/multi-factor-authentication/smart.png)&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;![Tarjeta inteligente virtual](./media/multi-factor-authentication/vsmart.png)&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;![Nombre de usuario y contraseña](./media/multi-factor-authentication/cert.png)</center>

Azure Multi-Factor Authentication (MFA) es la solución de Microsoft de comprobación de dos pasos. Azure MFA ayuda a proteger acceso toodata y las aplicaciones al tiempo que satisface la demanda de los usuarios de un proceso de inicio de sesión simple. Ofrece una autenticación segura a través de una gran variedad de métodos de comprobación (como la comprobación mediante llamadas telefónicas, mensajes de texto o aplicaciones móviles).

> [!VIDEO https://channel9.msdn.com/Blogs/Azure/WA-MFA-Overview/player]
>
>

## <a name="why-use-azure-multi-factor-authentication"></a>¿Por qué usar Azure Multi-Factor Authentication?
Hoy en día, ahora más que nunca, las personas están cada vez más conectadas. Con los smartphones, tabletas, equipos portátiles y equipos, personas tienen varias opciones diferentes acerca de cómo va a tooconnect y permanecer conectados en cualquier momento. Pueden acceder a sus cuentas y las aplicaciones desde cualquier lugar, lo que significa que pueden ser más productivos y atender mejor a sus clientes.

La autenticación multifactor Azure es una sencilla toouse, escalable, y solución confiable que proporciona un segundo método de autenticación para que los usuarios siempre están protegidos.

| ![TooUse fácil](./media/multi-factor-authentication/simple.png) | ![Escalable](./media/multi-factor-authentication/scalable.png) | ![Siempre protegido](./media/multi-factor-authentication/protected.png) | ![Confiable](./media/multi-factor-authentication/reliable.png) |
|:---:|:---:|:---:|:---:|
| **Toouse fácil** |**Escalable** |**Siempre protegido** |**Confiable** |

* **Fácil tooUse** -Azure la autenticación multifactor está tooset simple seguridad y el uso. Hello obtener protección adicional que se incluye con la autenticación multifactor Azure permite a los usuarios toomanage sus propios dispositivos. Y lo mejor de todo es que en muchos casos se puede configurar con unos pocos clics.
* **Escalable** -la autenticación multifactor Azure usa la energía de Hola de nube de Hola y se integra con sus instalaciones de AD y aplicaciones personalizadas. Esta protección se ha ampliado incluso tooyour escenarios de gran volumen, una importancia decisiva.
* **Siempre protegido** -la autenticación multifactor Azure proporciona una autenticación segura con hello más altos estándares del sector.
* **Confiable** : se garantiza la disponibilidad del 99,9% de Azure Multi-Factor Authenticaton. Hello servicio se considera no disponible cuando no puede tooreceive o proceso de solicitudes de comprobación para la comprobación de dos pasos de Hola.

> [!VIDEO https://channel9.msdn.com/Blogs/Azure/Windows-Azure-Multi-Factor-Authentication/player]


## <a name="next-steps"></a>Pasos siguientes

- Lea [Cómo funciona Azure Multi-Factor Authentication](multi-factor-authentication-how-it-works.md).

- Hola diferentes que conozca [versiones y los métodos de consumo para la autenticación multifactor de Azure](multi-factor-authentication-versions-plans.md)
