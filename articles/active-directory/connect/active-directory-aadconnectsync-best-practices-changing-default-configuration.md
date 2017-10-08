---
title: "Azure AD Connect sync: cambiar la configuración predeterminada de hello | Documentos de Microsoft"
description: "Proporciona prácticas recomendadas para cambiar la configuración predeterminada de Hola de sincronización de Azure AD Connect."
services: active-directory
documentationcenter: 
author: andkjell
manager: femila
editor: 
ms.assetid: 7638a031-1635-4942-94c3-fce8f09eed5e
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: billmath
ms.openlocfilehash: aa05e935edd02c49c3c3fdc198b854f50327847c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-connect-sync-best-practices-for-changing-hello-default-configuration"></a>Azure AD Connect sync: las prácticas recomendadas para cambiar la configuración predeterminada de Hola
Hola de este tema sirve toodescribe admiten y cuáles no cambios tooAzure AD Connect sync.

configuración de Hello creado por Azure AD Connect funciona "tal cual" para la mayoría de los entornos que se sincronizan en local de Active Directory con Azure AD. Sin embargo, en algunos casos, es necesario tooapply necesita algunos toosatisfy de configuración de tooa un determinado de cambios o requisito.

## <a name="changes-toohello-service-account"></a>Cuenta de servicio de toohello de cambios
Azure AD Connect sync se ejecuta bajo una cuenta de servicio creada por el Asistente para la instalación de Hola. Esta cuenta de servicio contiene Hola cifrado claves toohello base de datos utilizada por la sincronización. Se crea con una contraseña larga de 127 caracteres y la contraseña de Hola se establece toonot expire.

* Es **no compatible** toochange o el restablecimiento de contraseña de Hola de cuenta de servicio de Hola. Si lo hace, destruye claves de cifrado de hello y no se base de datos de tooaccess capaz de hello y no es capaz de toostart de servicio de Hola.

## <a name="changes-toohello-scheduler"></a>Programador de toohello de cambios
A partir de versiones de Hola de compilación 1.1 (febrero de 2016) puede configurar hello [programador](active-directory-aadconnectsync-feature-scheduler.md) toohave una sincronización diferentes ciclo predeterminado Hola de 30 minutos.

## <a name="changes-toosynchronization-rules"></a>Reglas de tooSynchronization de cambios
Asistente para la instalación de Hello proporciona una configuración que se supone toowork para escenarios más comunes de Hola. En caso de que necesite toomake cambios toohello configuración, debe seguir estas reglas toostill tienen una configuración admitida.

* También puede [cambiar los flujos de atributo](active-directory-aadconnectsync-change-the-configuration.md#other-common-attribute-flow-changes) si flujos de atributos directas de hello predeterminado no son adecuados para su organización.
* Si desea demasiado[flujo no de un atributo](active-directory-aadconnectsync-change-the-configuration.md#do-not-flow-an-attribute) y quitar los valores de cualquier atributo existente en Azure AD, deberá toocreate una regla para este escenario.
* [Deshabilite una regla de sincronización no deseada](#disable-an-unwanted-sync-rule) en lugar de eliminarla. Una regla eliminada se vuelve a crear durante una actualización.
* demasiado[cambiar una regla de out-of-box](#change-an-out-of-box-rule), debe realizar una copia de hello original regla y se deshabilita la regla de out-of-box Hola. Hola Editor de reglas de sincronización le solicita y le ayuda a.
* Exportar las reglas de sincronización personalizadas con hello Editor de reglas de sincronización. editor de Hello proporciona con una secuencia de comandos de PowerShell que puede usar tooeasily volver a crearlos en un escenario de recuperación ante desastres.

> [!WARNING]
> las reglas de sincronización de out-of-box Hola tienen una huella digital. Si realiza un cambio de reglas de toothese, ya no es coinciden con la huella digital de Hola. Podría tener problemas en hello futuras cuando intente tooapply una nueva versión de Azure AD Connect. Solo lleguen cambios Hola se describe en este artículo.

### <a name="disable-an-unwanted-sync-rule"></a>Deshabilite una regla de sincronización no deseada
No elimine una regla de sincronización lista para usar. Esta se vuelve a crear durante la siguiente actualización.

En algunos casos, el Asistente para la instalación de hello ha generado una configuración que no funciona para la topología. Por ejemplo, si tiene una topología de bosque de recursos de la cuenta pero tienes esquema extendido Hola Hola bosque de cuenta con el esquema de Exchange de hello, reglas de Exchange se crean para el bosque de cuentas de Hola y de bosque de recursos de Hola. En este caso, debe toodisable Hola la regla de sincronización de Exchange.

![Regla de sincronización deshabilitada](./media/active-directory-aadconnectsync-best-practices-changing-default-configuration/exchangedisabledrule.png)

En la imagen anterior de hello, Asistente para la instalación de Hola ha encontrado un esquema anterior de Exchange 2003 en el bosque de cuenta de hello. Esta extensión de esquema se agrega antes de bosque de recursos de Hola se introdujo en el entorno de Fabrikam. tooensure ningún atributo de implementación de Exchange antiguo Hola está sincronizada, se debe deshabilitar la regla de sincronización Hola tal como se muestra.

### <a name="change-an-out-of-box-rule"></a>cambiar una regla lista para usar
debe cambiar una regla de out-of-box de única vez de Hello es cuando se necesita la regla de unión toochange Hola. Si necesita toochange un flujo de atributo, debe crear una regla de sincronización con mayor prioridad que las reglas de out-of-box Hola. Hola solo regla prácticamente necesita tooclone es hello **en desde AD - User Join**. Puede invalidar el resto de reglas con una regla de prioridad superior.

Si tiene reglas de toomake cambios tooan out-of-box, debe realizar una copia de la regla de out-of-box hello y deshabilita la regla original Hola. A continuación, asegúrese de regla clonado de hello cambios toohello. Hola Editor de reglas de sincronización es ayudar con estos pasos. Cuando se abre una regla lista para usar, se presenta este cuadro de diálogo:   
![Regla lista para usar de advertencia](./media/active-directory-aadconnectsync-best-practices-changing-default-configuration/warningoutofboxrule.png)

Seleccione **Sí** toocreate una copia de la regla de Hola. a continuación, se abre la regla clonado Hola.  
![Regla clonada](./media/active-directory-aadconnectsync-best-practices-changing-default-configuration/clonedrule.png)

En esta regla clonada, realice los cambios necesarios tooscope, combinación y transformaciones.

## <a name="next-steps"></a>Pasos siguientes
**Temas de introducción**

* [Sincronización de Azure AD Connect: comprender y personalizar la sincronización](active-directory-aadconnectsync-whatis.md)
* [Integración de las identidades locales con Azure Active Directory](active-directory-aadconnect.md)
