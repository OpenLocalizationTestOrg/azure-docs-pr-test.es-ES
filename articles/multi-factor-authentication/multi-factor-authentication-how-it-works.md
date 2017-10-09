---
title: "aaaAzure la autenticación multifactor: cómo funciona"
description: "La autenticación multifactor Azure le ayuda a proteger acceso toodata y aplicaciones al tiempo que satisface la demanda de los usuarios de un proceso de inicio de sesión simple. Proporciona seguridad adicional al requerir una segunda forma de autenticación y ofrece autenticación segura a través de una gama de opciones de comprobación sencillas."
services: multi-factor-authentication
documentationcenter: 
author: kgremban
manager: femila
ms.assetid: d14db902-9afe-4fca-b3a5-4bd54b3d8ec5
ms.service: multi-factor-authentication
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/20/2017
ms.author: kgremban
ms.reviewer: yossib
ms.custom: it-pro
ms.openlocfilehash: 82f234fb86f145c42e8e56b8bdd2d61720c9ff2a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="how-azure-multi-factor-authentication-works"></a>Cómo funciona Azure Multi-Factor Authentication
seguridad de Hola de verificación en dos pasos se encuentra en su enfoque por capas. El uso de varias fases de autenticación supone un reto importante para los atacantes. Aunque un atacante administra la contraseña del usuario de toolearn hello, es inútil sin tiene en su posesión del dispositivo de confianza de Hola. 

![Página de proofup](./media/multi-factor-authentication-how-it-works/howitworks.png)

La autenticación multifactor Azure le ayuda a proteger acceso toodata y aplicaciones al tiempo que satisface la demanda de los usuarios de un proceso de inicio de sesión simple.  Proporciona seguridad adicional al requerir una segunda forma de autenticación y ofrece autenticación segura a través de una gama de opciones de comprobación sencillas.


## <a name="methods-available-for-two-step-verification"></a>Métodos disponibles para la verificación en dos pasos
Cuando un usuario inicia sesión, una comprobación adicional se envía toohello usuario.  siguiente Hola es una lista de métodos que puede utilizarse para esta comprobación de segundo.

| Método de comprobación | Descripción |
| --- | --- |
| llamada de teléfono |Se realiza una llamada telefónica registrada del usuario tooa. usuario de Hello escribe un PIN si es necesario, a continuación, presiona la tecla # de Hola. |
| mensaje de texto |Se envía un mensaje de texto móvil del usuario tooa con un código de seis dígitos. usuario de Hello escribe este código en la página de inicio de sesión de Hola. |
| Notificación en aplicación móvil |Teléfono inteligente del usuario tooa, se envía una solicitud de comprobación. Hello usuario escriba un PIN si es necesario, a continuación, selecciona **compruebe** en aplicaciones móviles de Hola. |
| Código de verificación de la aplicación móvil |aplicación móvil de Hello, que se ejecuta en el teléfono inteligente de un usuario, muestra un código de comprobación que cambia cada 30 segundos. usuario de Hello encuentra código más reciente de Hola y entra en la página de inicio de sesión de Hola. |
| Tokens OATH de terceros | Servidor de Azure Multi-factor Authentication pueden ser métodos de comprobación de terceros de tooaccept configurado. |

Azure Multi-Factor Authentication proporciona métodos de comprobación seleccionables tanto para la nube y como para servidor. Puede elegir qué métodos estarán disponibles para los usuarios: llamada telefónica, mensajes de texto, notificación en aplicación o códigos de aplicación. Para más información, vea [Métodos de comprobación seleccionables](multi-factor-authentication-whats-next.md#selectable-verification-methods).

## <a name="next-steps"></a>Pasos siguientes

- Hola diferentes que conozca [versiones y los métodos de consumo para la autenticación multifactor de Azure](multi-factor-authentication-versions-plans.md)

- Elija si toodeploy Azure MFA [en la nube de Hola o de forma local](multi-factor-authentication-get-started.md)

- Obtenga respuestas para las [Preguntas más frecuentes](multi-factor-authentication-faq.md).