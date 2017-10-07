---
title: versiones MFA de aaaAzure y el consumo de planes | Documentos de Microsoft
description: "Información sobre el cliente de la autenticación multifactor de Hola y Hola métodos y diferentes versiones disponibles. Detalles sobre cada plan de consumo"
keywords: 
services: multi-factor-authentication
documentationcenter: 
author: kgremban
manager: femila
editor: yossib
ms.assetid: 
ms.service: multi-factor-authentication
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/26/2017
ms.author: kgremban
ms.openlocfilehash: 4914747e435531b9f950356d23aa386f3d9585d2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooget-azure-multi-factor-authentication"></a>¿Cómo tooget la autenticación multifactor Azure

Cuando se trata de tooprotecting sus cuentas, debe ser verificacion estándar en toda la organización. Esta característica es especialmente importante para las cuentas administrativas que tienen privilegiado tooresources de acceso. Por esta razón, Microsoft ofrece dos pasos básicos comprobación características tooOffice 365 y administradores de Azure. Si desea características de hello tooupgrade para los administradores, o extender el resto de toohello de comprobación de dos pasos de los usuarios, puede comprar Azure la autenticación multifactor. 

Este artículo se tratan explica Hola diferencia entre las versiones de hello ofrecidas hello y tooadministrators versión completa de MFA de Azure y especifica qué características están disponibles en cada uno. Si está listo toodeploy Hola completar oferta de Azure MFA, Hola posteriores opciones de implementación de portadas de secciones y cómo Microsoft calcula el consumo.

>[!IMPORTANT]
>El objetivo de este artículo se toobe un toohelp de guía que comprenda Hola toobuy Azure la autenticación multifactor de maneras diferentes. Para obtener detalles específicos sobre los precios y facturación, siempre debería consultar toohello [la autenticación multifactor página de precios](https://azure.microsoft.com/pricing/details/multi-factor-authentication/).

## <a name="available-versions-of-azure-multi-factor-authentication"></a>Versiones disponibles de Azure Multi-Factor Authentication

Hello tabla siguiente describen las diferencias de hello entre las tres versiones de la autenticación multifactor:

| Versión | Description |
| --- | --- |
| Multi-Factor Authentication para Office 365 |Esta versión funciona exclusivamente con aplicaciones de Office 365 y se administra desde el portal de Office 365 Hola. Los administradores pueden [proteger los recursos de Office 365 con la comprobación en dos pasos](https://support.office.com/article/Set-up-multi-factor-authentication-for-Office-365-users-8f0454b2-f51a-4d9c-bcde-2c48e41621c6). Esta versión forma parte de una suscripción a Office 365. |
| Multi-Factor Authentication para administradores de Azure | Los administradores globales de inquilinos de Azure pueden habilitar la comprobación en dos pasos para sus cuentas de administrador globales sin costo adicional.|
| Azure Multi-Factor Authentication | Lo que se conoce a menudo tooas Hola "versión"completa, la autenticación multifactor Azure"ofrece Hola conjunto de numerosas capacidades. Proporciona opciones de configuración adicionales a través de hello [portal de Azure clásico](https://manage.windowsazure.com), informes avanzados y compatibilidad para una gama de local y las aplicaciones en la nube. La autenticación multifactor Azure se incluye en Azure Active Directory Premium (planes P1 y P2) y Enterprise Mobility + Security (planes E3 y E5) y puede ser implementado en [en la nube de Hola o de forma local](multi-factor-authentication-get-started.md). |

## <a name="feature-comparison-of-versions"></a>Comparación de características de las versiones
Hello tabla siguiente proporciona una lista de características de Hola que están disponibles en hello distintas versiones de autenticación multifactor de Azure.

> [!NOTE]
> Esta tabla de comparación describe las características de Hola que forman parte de cada versión de la autenticación multifactor. Si tiene el servicio de autenticación multifactor de Azure completo de hello, algunas características no estén disponibles dependiendo de si utiliza [MFA en la nube de Hola o MFA local](multi-factor-authentication-get-started.md).


| Característica | Multi-Factor Authentication para Office 365 | Multi-Factor Authentication para administradores de Azure | Azure Multi-Factor Authentication |
| --- |:---:|:---:|:---:|
| Protección de cuentas de administrador con MFA |● |● (Solo cuentas de administrador global) |● |
| Aplicación móvil como segundo factor |● |● |● |
| Llamada de teléfono como segundo factor |● |● |● |
| SMS como segundo factor |● |● |● |
| Contraseñas de aplicación para clientes que no admiten MFA |● |● |● |
| Control administrativo sobre métodos de comprobación |● |● |● |
| Modo de PIN | | |● |
| Alerta de fraude | | |● |
| Informes de MFA | | |● |
| Omisión por única vez | | |● |
| Saludos personalizados para las llamadas de teléfono | | |● |
| Identificador de llamada personalizado para llamadas telefónicas | | |● |
| IP de confianza | | |● |
| Recordar MFA para dispositivos de confianza |● |● |● |
| SDK de MFA | | |● (Requiere el proveedor de Multi-Factor Authentication y la suscripción completa a Azure) |
| MFA para aplicaciones locales | | |● |

## <a name="how-tooget-azure-multi-factor-authentication"></a>¿Cómo tooget la autenticación multifactor Azure
Si desea que la funcionalidad completa de Hola que ofrece la autenticación multifactor Azure, hay varias opciones:

### <a name="option-1---mfa-licenses"></a>Opción 1: Licencias de MFA

Comprar licencias de Azure la autenticación multifactor y asignarlos a los usuarios de tooyour en Azure Active Directory. 

Si utiliza esta opción, debe crear un proveedor de autenticación multifactor de Azure solo si también necesita tooprovide verificacion de algunos usuarios que no tienen licencias. Si no lo hace, le podrían facturar dos veces.

### <a name="option-2---bundled-licenses-that-include-mfa"></a>Opción 2: Paquete de licencias que incluyen MFA

Adquisición de licencias que incluyen la autenticación multifactor de Azure, como Azure Active Directory Premium (P1 o P2) o Enterprise Mobility + Security (E3 o E5) y asignarlos a los usuarios de tooyour en Azure Active Directory. 

Si utiliza esta opción, debe crear un proveedor de autenticación multifactor de Azure solo si también necesita tooprovide verificacion de algunos usuarios que no tienen licencias. Si no lo hace, le podrían facturar dos veces. 

### <a name="option-3---mfa-consumption-based-model"></a>Opción 3: Modelo basado en el consumo de MFA

Crear un proveedor de Azure Multi-Factor Authentication dentro de una suscripción a Azure. Los proveedores de Azure MFA son recursos de Azure que se facturan según el contrato Enterprise, el compromiso monetario de Azure o con tarjeta de crédito, igual que todos los demás recursos de Azure. Estos proveedores solo pueden crearse en suscripciones completas de Azure, y no en suscripciones limitadas que tienen un límite de gasto de 0 $. Las suscripciones limitadas se crean cuando se activan licencias, como en las opciones 1 y 2. 

Si se utiliza un proveedor de Azure Multi-Factor Authentication, hay dos modelos de uso disponibles que se facturan a través de la suscripción a Azure:  

1. **Por usuario** : para empresas que quieren tooenable verificacion de un número fijo de empleados que necesitan la autenticación de forma regular. Facturación por usuario se basa en el número de Hola de usuarios habilitados para MFA en su inquilino de Azure AD y en el servidor de MFA de Azure. Si los usuarios están habilitados para MFA en ambos Azure AD y el servidor de MFA de Azure y se habilita la sincronización de dominio (Azure AD Connect), a continuación, se cuenta conjunto mayor de Hola de usuarios. Si no está habilitada la sincronización de dominio, el recuento de suma de Hola de todos los usuarios habilitados para MFA de Azure AD y el servidor de MFA de Azure. La facturación es sistema de comercio toohello prorrateados y se notificará diaria. 

  > [!NOTE]
  > Ejemplo de facturación 1: hoy tiene 5000 usuarios habilitados para MFA. Hola sistema MFA divide ese número entre 31 y 161.29 usuarios de informes para ese día. Mañana se habilita a 15 más usuarios, por lo que Hola sistema MFA informes 161.77 a los usuarios de ese día. Extremo de Hola de hello ciclo de facturación, número total de Hola de usuarios que se facturan con su suscripción de Azure suma tooaround 5.000. 
  >
  > Ejemplo de facturación 2: tiene una mezcla de los usuarios con licencias y los usuarios no tienen, por lo que tendrá un toomake de proveedor de MFA de Azure por usuario diferencia Hola. Hay 4500 licencias de Enterprise Mobility + Security en el inquilino, pero 5000 usuarios habilitados para MFA. En su suscripción de Azure se facturan 500 usuarios, y se prorratean y notifican diariamente como 16,13 usuarios. 

2. **Por autenticación** : para empresas que quieren verificacion de tooenable para un gran número de usuarios que necesitan autenticación en ocasiones. Facturación se basa en el número de Hola de las solicitudes de comprobación de dos pasos recibidas por hello servicio de nube de Azure MFA, independientemente de si esas comprobaciones correctamente o se deniegan. Este facturación aparece en el extracto de uso de Azure en los módulos de 10 autenticaciones y es el sistema de comercio de toohello notificado diariamente. 

  > [!NOTE]
  > Ejemplo 3 de facturación: en la actualidad, Hola servicio Azure MFA recibido 3,105 solicitudes de verificación de dos pasos. En su suscripción de Azure se facturan 310,5 paquetes autenticación. 

Es importante toonote que puede tener licencias de MFA de Azure, pero cobrarle para configuración basada en el consumo. Si configura un proveedor de Azure MFA por autenticación, se le factura cada solicitud de comprobación en dos pasos, aunque las hayan realizado usuarios con licencia. Si ha configurado un proveedor de MFA de Azure por usuario en un dominio que no está vinculado tooyour inquilino de Azure AD, se le facturará por usuario habilitado, incluso si los usuarios tienen licencias en Azure AD. 

## <a name="next-steps"></a>Pasos siguientes

- Para más información sobre los precios, consulte [Precios de Azure MFA](https://azure.microsoft.com/pricing/details/multi-factor-authentication/).

- Elija si toodeploy Azure MFA [en la nube de Hola o de forma local](multi-factor-authentication-get-started.md)
