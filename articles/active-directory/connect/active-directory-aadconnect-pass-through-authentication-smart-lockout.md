---
title: "Azure AD Connect: Autenticación de paso a través - Bloqueo inteligente | Microsoft Docs"
description: "Este artículo describe cómo la autenticación de paso a través de Azure Active Directory (Azure AD) protege las cuentas locales de ataques por fuerza bruta de contraseñas en nube de Hola."
services: active-directory
keywords: "Autenticación de paso a través de Azure AD Connect, instalación de Active Directory, componentes necesarios para Azure AD, SSO, inicio de sesión único"
documentationcenter: 
author: swkrish
manager: femila
ms.assetid: 9f994aca-6088-40f5-b2cc-c753a4f41da7
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/02/2017
ms.author: billmath
ms.openlocfilehash: b02e315c3cc3eae00ca6408d735a416f34c2cdc3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-pass-through-authentication-smart-lockout"></a>Autenticación de paso a través de Azure Active Directory: Bloqueo inteligente

## <a name="overview"></a>Información general

Azure AD protege frente a los ataques de contraseña por fuerza bruta e impide que se bloquee a los usuarios originales de sus aplicaciones de Office 365 y SaaS. Esta capacidad, denominada **Bloqueo inteligente**, se admite cuando se usa la autenticación de paso a través como método de inicio de sesión. Bloqueo inteligente está habilitada de forma predeterminada para todos los inquilinos y se protegen las cuentas de usuario todo el tiempo de hello; No hay ninguna necesidad de tooturn en.

Bloqueo inteligente funciona mediante el seguimiento de los errores de inicio de sesión y después de un determinado **Umbral de bloqueo**, a partir de una **Duración del bloqueo**. Se rechazan los intentos de inicio de sesión del atacante Hola durante la duración del bloqueo de Hola. Si continúa el ataque de hello, Hola posteriores Error inicio de sesión intentos de una vez finalizado el Hola duración del bloqueo de resultados de mayor duración de bloqueo.

>[!NOTE]
>valor predeterminado de Hello umbral de bloqueo es 10 intentos fallidos y predeterminada de hello que duración del bloqueo es de 60 segundos.

Bloqueo inteligente también distingue entre inicios de sesión de usuarios originales y de los atacantes y sólo bloquea los atacantes hello en la mayoría de los casos. Esta funcionalidad impide que los atacantes bloqueen de forma malintencionada a los usuarios originales. Utilizamos más allá de inicio de sesión de comportamiento, los usuarios dispositivos y exploradores y otro toodistinguish señales entre usuarios originales y a los atacantes. Estamos mejorando constantemente nuestros algoritmos.

Dado que este tipo de autenticación se reenvía las solicitudes de validación de contraseña en su Active Directory local (AD), necesita los atacantes tooprevent bloquear cuentas de AD de sus usuarios. Puesto que tiene sus propias directivas de bloqueo de cuentas de AD (específicamente, [ **umbral de bloqueo de cuenta** ](https://technet.microsoft.com/library/hh994574(v=ws.11).aspx) y [ **Restablecer contador de bloqueo de cuenta después de las directivas** ](https://technet.microsoft.com/library/hh994568(v=ws.11).aspx)), necesita el umbral de bloqueo de tooconfigure de Azure AD y duración del bloqueo adecuadamente valores toofilter fuera de los ataques de nube de hello antes de alcanzar su local AD.

>[!NOTE]
>característica de bloqueo inteligente Hello es gratuito y está _en_ de forma predeterminada para todos los clientes. Sin embargo, la modificación del umbral de bloqueo y los valores de duración del bloqueo mediante la API Graph de Azure AD necesita su licencia de inquilino toohave al menos un Azure AD Premium P2. No necesita una licencia de Azure AD Premium P2 _por usuario_ característica de bloqueo inteligente de hello tooget con la autenticación de paso a través.

tooensure que los usuarios en AD cuentas locales están bien protegidos, deberá tooensure que:

1.  El umbral de bloqueo de Azure AD es _menos_ que el umbral de bloqueo de cuentas de AD. Se recomienda establecer valores de hello tal que el umbral de bloqueo de cuentas de AD es al menos dos o tres veces el umbral de bloqueo de Azure AD.
2.  La duración del bloqueo de Azure AD (representada en segundos) es _mayor_ que el valor de Restablecer el bloqueo de cuenta después de AD de (representado en minutos).

## <a name="verify-your-ad-account-lockout-policies"></a>Comprobar las directivas de bloqueo de cuentas de AD

Usar hello siguiendo las instrucciones tooverify las directivas de bloqueo de cuentas de AD:

1.  Abra la herramienta de administración de directivas de grupo de Hola.
2.  Editar Hola directiva de grupo que es usuarios de tooall aplicado, por ejemplo, hello directiva predeterminada de dominio.
3.  Navegue tooComputer Configuration\Policies\Windows Windows\Configuración seguridad\Directivas cuenta\Directiva directiva de bloqueo.
4.  Compruebe los valores de Umbral de bloqueo de cuenta y Restablecer contador de bloqueo de cuenta después de.

![Directivas de bloqueo de cuentas de AD](./media/active-directory-aadconnect-pass-through-authentication/pta5.png)

## <a name="use-hello-graph-api-toomanage-your-tenants-smart-lockout-values"></a>Usar Hola API Graph toomanage valores de bloqueo inteligentes de su inquilino

>[!IMPORTANT]
>Modificar los valores de umbral de bloqueo y duración del bloqueo de Azure AD mediante la API de Graph es una característica de Azure AD Premium P2. También debe toobe un administrador Global en su inquilino.

Puede usar [Explorador de gráficos](https://developer.microsoft.com/graph/graph-explorer) tooread, configurar y actualizar valores de bloqueo inteligente de Azure AD. Pero también puede realizar estas operaciones mediante programación.

### <a name="read-smart-lockout-values"></a>Leer valores de bloqueo de inteligente

Siga estos pasos tooread valores de bloqueo inteligentes de su inquilino:

1. Inicie sesión en el Explorador de gráficos como un administrador global del inquilino. Si se le solicita, conceder acceso para hello permisos solicitados.
2. Haga clic en "Modificar los permisos" y el permiso de "Directory.ReadWrite.All" hello select.
3. Configurar solicitud de API Graph hello como sigue: versión del juego demasiado "BETA", tipo de solicitud demasiado "GET" y la dirección URL demasiado`https://graph.microsoft.com/beta/<your-tenant-domain>/settings`.
4. Haga clic en "Ejecutar consulta" toosee valores de bloqueo inteligentes de su inquilino. Si no ha establecido los valores del inquilino antes, verá un conjunto vacío.

### <a name="set-smart-lockout-values"></a>Establecer valores de bloqueo de inteligente

Siga estos pasos tooset valores de bloqueo inteligentes de su inquilino (por Hola sólo la primera vez):

1. Inicie sesión en el Explorador de gráficos como un administrador global del inquilino. Si se le solicita, conceder acceso para hello permisos solicitados.
2. Haga clic en "Modificar los permisos" y el permiso de "Directory.ReadWrite.All" hello select.
3. Configurar solicitud de API Graph hello como sigue: versión del juego demasiado "BETA", tipo de solicitud demasiado "POST" y la dirección URL demasiado`https://graph.microsoft.com/beta/<your-tenant-domain>/settings`.
4. Copie y pegue Hola tras la solicitud JSON en el campo de "Cuerpo de la solicitud" Hola. Cambiar valores de bloqueo inteligente Hola según corresponda y usar un GUID aleatorio para `templateId`.
5. Haga clic en "Ejecutar consulta" tooset valores de bloqueo inteligentes de su inquilino.

```
{
  "templateId": "5cf42378-d67d-4f36-ba46-e8b86229381d",
  "values": [
    {
      "name": "LockoutDurationInSeconds",
      "value": "300"
    },
    {
      "name": "LockoutThreshold",
      "value": "5"
    },
    {
      "name" : "BannedPasswordList",
      "value": ""
    },
    {
      "name" : "EnableBannedPasswordCheck",
      "value": "false"
    }
  ]
}
```

>[!NOTE]
>Si no usas ellos, puede dejar hello **BannedPasswordList** y **EnableBannedPasswordCheck** valores como vacío ("") y "false" respectivamente.

Compruebe que ha establecido correctamente los valores de bloqueo inteligente del inquilino mediante [estos pasos](#read-smart-lockout-values).

### <a name="update-smart-lockout-values"></a>Actualizar los valores de bloqueo de inteligente

Siga estos pasos tooupdate valores de bloqueo inteligentes de su inquilino (si ya ha configurado antes):

1. Inicie sesión en el Explorador de gráficos como un administrador global del inquilino. Si se le solicita, conceder acceso para hello permisos solicitados.
2. Haga clic en "Modificar los permisos" y el permiso de "Directory.ReadWrite.All" hello select.
3. [Siga estos pasos tooread valores de bloqueo inteligentes de su inquilino](#read-smart-lockout-values). Hola copia `id` valor (GUID) del elemento de hello con "displayName" como "PasswordRuleSettings".
4. Configurar solicitud de API Graph hello como sigue: establecer la versión "BETA", tipo de solicitud demasiado "Revisión" y la dirección URL demasiado`https://graph.microsoft.com/beta/<your-tenant-domain>/settings/<id>` -usar Hola GUID en el paso 3 para `<id>`.
5. Copie y pegue Hola tras la solicitud JSON en el campo de "Cuerpo de la solicitud" Hola. Cambiar los valores de bloqueo inteligente Hola según corresponda.
6. Haga clic en "Ejecutar consulta" tooupdate valores de bloqueo inteligentes de su inquilino.

```
{
  "values": [
    {
      "name": "LockoutDurationInSeconds",
      "value": "30"
    },
    {
      "name": "LockoutThreshold",
      "value": "4"
    },
    {
      "name" : "BannedPasswordList",
      "value": ""
    },
    {
      "name" : "EnableBannedPasswordCheck",
      "value": "false"
    }
  ]
}
```

Compruebe que ha actualizado correctamente los valores de bloqueo inteligente del inquilino mediante [estos pasos](#read-smart-lockout-values).

## <a name="next-steps"></a>Pasos siguientes
- [**UserVoice**](https://feedback.azure.com/forums/169401-azure-active-directory/category/160611-directory-synchronization-aad-connect): para rellenar solicitudes de características nuevas.
