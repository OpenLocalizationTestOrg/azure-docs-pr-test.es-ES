---
title: "aaaManage la configuración de comprobación de dos pasos | Documentos de Microsoft"
description: "Administre cómo usar Azure Multi-Factor Authentication, incluida la modificación de la información de contacto o la configuración de los dispositivos."
services: multi-factor-authentication
keywords: "cliente de multi-factor authentication, problema de autenticación, identificador de correlación"
documentationcenter: 
author: kgremban
manager: femila
editor: yossib
ms.assetid: d3372d9a-9ad1-4609-bdcf-2c4ca9679a3b
ms.service: multi-factor-authentication
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/23/2017
ms.author: kgremban
ms.custom: end-user
ms.openlocfilehash: 2c974b08c584943f3c5a6b9bf16497d1706e8329
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="manage-your-settings-for-two-step-verification"></a>Administración de la configuración de la comprobación en dos pasos
Este artículo ofrece respuestas a preguntas acerca de cómo tooupdate configuración para la autenticación de dos pasos de verificación o multifactor. Si tiene problemas para iniciar sesión en la cuenta de tooyour, consulte demasiado[tiene problemas con la verificacion](multi-factor-authentication-end-user-troubleshoot.md) de ayuda para solucionar problemas.

## <a name="where-toofind-hello-settings-page"></a>Donde toofind Hola página de configuración
Según cómo su compañía configure Azure Multi-Factor Authentication, existen algunos lugares donde puede cambiar los ajustes, como su número de teléfono.

Si el Administrador de TI envía una dirección URL específica o verificacion de pasos toomanage, siga estas instrucciones. En caso contrario, debería funcionar Hola siguiendo las instrucciones para los demás. Si se siguen estos pasos, pero no ve hello las mismas opciones, lo que significa que su trabajo o escuela personaliza su propio portal. Pida al administrador de portal de Azure la autenticación multifactor de hello vínculo tooyour.

1. Inicie sesión en demasiado[https://myapps.microsoft.com](https://myapps.microsoft.com)  
2. Seleccione el nombre de cuenta en hello parte superior derecha, a continuación, seleccione **perfil**.  
3. Seleccione **Comprobación de seguridad adicional**.  

    ![MyApps](./media/multi-factor-authentication-end-user-manage/myapps1.png)
4. página de comprobación de seguridad adicionales de Hello carga con la configuración.

    ![Página de proofup](./media/multi-factor-authentication-end-user-manage/proofup.png)

## <a name="i-want-toochange-my-phone-number-or-add-a-secondary-number"></a>Desea toochange mi número de teléfono o agregar un número secundario
Es importante tooconfigure un número de teléfono de autenticación secundaria.  Dado que su aplicación móvil y número de teléfono de su objeto principal son probablemente en hello igual de teléfono, número de teléfono secundario de hello es una única manera de hello estará tooget pueda volver a tu cuenta si se pierde o le roban el teléfono.

> [!NOTE]
> Si no tiene el número de teléfono principal de acceso tooyour y necesita ayuda para obtener en tooyour cuenta, consulte nuestro temas de ayuda en [tiene problemas con la verificacion](multi-factor-authentication-end-user-troubleshoot.md).  

**toochange número de teléfono principal:**  

1. En la página de comprobación de seguridad adicionales de hello, seleccione el cuadro de texto de hello con el número de teléfono actual y modifíquelo con el nuevo número de teléfono.  
2. Seleccione **Guardar**.  
3. Si este es el número de Hola que utiliza para la opción de comprobación preferida, tendrá nuevo número de tooverify Hola antes de que se puede guardar.  

**tooadd un número de teléfono secundario:**  

1. En la página de comprobación de seguridad adicionales de hello, casilla Hola junto demasiado**teléfono de autenticación alternativo.**  
2. Escriba el número de teléfono secundario en el cuadro de texto de Hola.  
3. Seleccione **Guardar** y los cambios habrán finalizado.  

## <a name="require-two-step-verification-again-on-a-device-youve-marked-as-trusted"></a>Requisito de nueva verificación en dos pasos en un dispositivo marcado como de confianza

Dependiendo de la configuración de la organización, es posible que tenga una casilla que indica "Don't ask again for **X** days" (No volver a preguntar en X días) al realizar la verificación en dos pasos en el explorador. Si esta casilla de verificación y, a continuación, pierden su dispositivo o cree que su cuenta se ve comprometida, debe restaurar tooall de comprobación de dos pasos los dispositivos. 

1. En la página de comprobación de seguridad adicionales de hello, seleccione **restaurar la autenticación multifactor en dispositivos de confianza anteriormente**.
2. Hello próxima vez que inicie sesión en cualquier dispositivo, podrá verificacion de tooperform solicitadas. 

## <a name="how-do-i-clean-up-microsoft-authenticator-from-my-old-device-and-move-tooa-new-one"></a>¿Cómo limpiar Microsoft Authenticator desde mi dispositivo anterior y mover tooa uno nuevo?
Cuando se desinstala la aplicación hello desde su dispositivo o restablecer Hola dispositivo, no quita la activación de hello en back-end de Hola. Para más información, vea [Microsoft Authenticator](microsoft-authenticator-app-how-to.md).

## <a name="next-steps"></a>Pasos siguientes
* Obtener sugerencias para solucionar problemas y necesita ayuda [Problemas con la comprobación en dos pasos](multi-factor-authentication-end-user-troubleshoot.md)
* Configure [contraseñas de aplicación](multi-factor-authentication-end-user-app-passwords.md) para las aplicaciones que no admiten la comprobación en dos pasos.
