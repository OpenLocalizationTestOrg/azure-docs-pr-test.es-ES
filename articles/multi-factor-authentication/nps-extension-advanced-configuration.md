---
title: "Hola aaaConfigure extensión de NPS de MFA de Azure | Documentos de Microsoft"
description: "Después de instalar la extensión NPS hello, siga estos pasos para la configuración avanzada como la creación de listas blancas IP y el reemplazo de UPN."
services: multi-factor-authentication
documentationcenter: 
author: kgremban
manager: femila
ms.assetid: 
ms.service: multi-factor-authentication
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/14/2017
ms.author: kgremban
ms.reviewer: yossib
ms.custom: it-pro
ms.openlocfilehash: c3aed077b23c95f874861eb00c8e6dca668329c1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="advanced-configuration-options-for-hello-nps-extension-for-multi-factor-authentication"></a>Configuración las opciones avanzadas para hello extensión NPS para la autenticación multifactor

Hola extensión de servidor de directivas de redes (NPS) amplía las características de la autenticación multifactor Azure basada en la nube a la infraestructura local. En este artículo se da por supuesto que ya tienen la extensión de hello instalado y ahora desea tooknow cómo debe extensión de hello toocustomize para usted. 

## <a name="alternate-login-id"></a>Identificador de inicio de sesión alternativo

Puesto que Hola extensión NPS conecta tooboth su en la nube local y directorios, puede producirse un problema donde los nombres de entidad de seguridad de usuario (UPN) local no coinciden con los nombres de hello en la nube de Hola. toosolve este problema, el inicio de sesión use alternativo identificadores. 

Dentro de hello extensión NPS, puede designar un toobe de atributo de Active Directory usado en lugar de hello UPN para la autenticación multifactor Azure. Esto permite tooprotect sus recursos locales con la verificacion sin modificar los UPN local. 

inicio de sesión tooconfigure alternativo identificadores, vaya demasiado`HKLM\SOFTWARE\Microsoft\AzureMfa` y editar los siguientes valores del registro de hello:

| Nombre | Escriba | Valor predeterminado | Descripción |
| ---- | ---- | ------------- | ----------- |
| LDAP_ALTERNATE_LOGINID_ATTRIBUTE | cadena | Vacío | Designar Hola nombre del atributo de Active Directory que desea que toouse en lugar de hello UPN. Este atributo se utiliza como atributo de AlternateLoginId Hola. Si este valor del registro se establece tooa [atributo de Active Directory válido](https://msdn.microsoft.com/library/ms675090.aspx) (por ejemplo, correo electrónico o displayName), a continuación, valor del atributo de Hola se utiliza en lugar UPN del usuario de hello para la autenticación. Si este valor del registro está vacío o no configurado, a continuación, se deshabilita AlternateLoginId y UPN del usuario de Hola se utiliza para la autenticación. |
| LDAP_FORCE_GLOBAL_CATALOG | boolean | False | Utilice esta marca tooforce Hola de catálogo Global para búsquedas LDAP al buscar AlternateLoginId. Configurar un controlador de dominio como catálogo Global, agregue hello AlternateLoginId atributo toohello catálogo Global y, a continuación, habilite esta marca. <br><br> Si se ha configurado (no vacíos), LDAP_LOOKUP_FORESTS **esta marca se aplica como true**, independientemente del valor de Hola de configuración del registro de hello. En este caso, Hola extensión NPS requiere hello toobe de catálogo Global configurado con hello AlternateLoginId atributo para cada bosque. |
| LDAP_LOOKUP_FORESTS | cadena | Vacío | Proporcionar una lista separada por punto y coma de toosearch de bosques. Por ejemplo, *contoso.com;foobar.com*. Si se configura este valor del registro, Hola extensión NPS busca iterativa todos los bosques de hello en el orden de hello en el que se muestran y devuelve el primer valor correcta AlternateLoginId Hola. Si este valor del registro no está configurada, búsqueda de hello AlternateLoginId es toohello reducidos actual.|

problemas de tootroubleshoot con inicio de sesión alternativo identificadores, use Hola pasos recomendado para [alternativas errores de Id. de inicio de sesión](multi-factor-authentication-nps-errors.md#alternate-login-id-errors).

## <a name="ip-exceptions"></a>Excepciones de dirección IP

Si necesita toomonitor disponibilidad del servidor, como si los equilibradores de carga compruebe qué servidores se ejecutan antes de enviar las cargas de trabajo, no desea que estos toobe comprobaciones bloqueando las solicitudes de comprobación. En su lugar, cree una lista de direcciones IP que sepa que las cuentas de servicio las utilizan y deshabilite los requisitos de Multi-Factor Authentication en esa lista. 

tooconfigure una lista blanca de direcciones IP, vaya demasiado`HKLM\SOFTWARE\Microsoft\AzureMfa` y configurar Hola siguiente valor del registro: 

| Nombre | Escriba | Valor predeterminado | Descripción |
| ---- | ---- | ------------- | ----------- |
| IP_WHITELIST | cadena | Vacío | Proporcione una lista separada por puntos y coma de direcciones IP. Incluir las direcciones IP de los equipos donde se originan las solicitudes de servicio, como Hola servidor NAS/VPN Hola. Los intervalos de direcciones IP y las subredes no se admiten. <br><br> Por ejemplo, *10.0.0.1;10.0.0.2;10.0.0.3*.

Cuando llega una solicitud de una dirección IP que existe en la lista blanca de hello, se omite la verificación en dos pasos. Hola lista aprobada de IP es comparados toohello dirección IP que se proporciona en hello *ratNASIPAddress* atributos de solicitud RADIUS Hola. Si llega una solicitud RADIUS sin atributo ratNASIPAddress de hello, se registra Hola siguiente advertencia: "Lista blanca de direcciones P_WHITE_LIST_WARNING::IP se ha omitido porque falta en la solicitud RADIUS en el atributo NasIpAddress la dirección IP de origen."

## <a name="next-steps"></a>Pasos siguientes

[Resolver mensajes de error de hello extensión NPS para la autenticación multifactor de Azure](multi-factor-authentication-nps-errors.md)
