---
title: "Consideraciones de diseño de identidad de aaaAzure Active Directory híbrida - determinar los requisitos de la autenticación multifactor"
description: "Con control de acceso condicional, Azure Active Directory comprueba las condiciones específicas de Hola que elegir al autenticar usuario hello y antes de permitir el acceso toohello aplicación. Una vez que se cumplen estas condiciones, usuario de hello es autenticado y acceso toohello aplicación permitida."
documentationcenter: 
services: active-directory
author: femila
manager: billmath
editor: 
ms.assetid: 9c59fda9-47d0-4c7e-b3e7-3575c29beabe
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/18/2017
ms.author: billmath
ms.openlocfilehash: 49fa7b43772fb3a2d6664747477c60a34cddde2b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="determine-multi-factor-authentication-requirements-for-your-hybrid-identity-solution"></a>Determinación de los requisitos de autenticación multifactor para la solución de identidad híbrida
En este mundo de la movilidad, con usuarios que acceden a datos y aplicaciones en la nube de Hola y desde cualquier dispositivo, proteger esta información se ha convertido en gran importancia.  Todos los días hay un nuevo titular sobre una infracción de la seguridad.  Sin embargo, no hay ninguna garantía en brechas de seguridad, la autenticación multifactor, proporciona una capa adicional de seguridad toohelp evitar estas infracciones.
Iniciar mediante la evaluación de los requisitos de las organizaciones de hello para la autenticación multifactor. Es decir, ¿qué es Hola organización tratar toosecure.  Esta evaluación es requisitos técnicos de hello toodefine importante para configurar y permitir que los usuarios de organizaciones de hello para la autenticación multifactor.

> [!NOTE]
> Si no está familiarizado con MFA y lo que hace, se recomienda encarecidamente que lea el artículo hello [¿qué es la autenticación multifactor Azure?](../multi-factor-authentication/multi-factor-authentication.md) toocontinue anterior leer esta sección.
> 
> 

Realice el siguiente de hello tooanswer seguro:

* ¿Su empresa está tratando de aplicaciones de Microsoft toosecure? 
* ¿Cómo se publican estas aplicaciones?
* ¿La compañía proporcionará acceso remoto tooallow empleados tooaccess local aplicaciones?

¿En caso afirmativo, qué tipo de acceso remoto? También debe tooevaluate donde se ubicarán los usuarios de Hola que obtiene acceso a estas aplicaciones. Esta evaluación es otra estrategia de autenticación multifactor correcta de Hola de toodefine paso importante. Asegúrese de seguro hello tooanswer siguientes preguntas:

* ¿Dónde se encuentran los usuarios de hello va toobe?
* ¿Pueden estar en cualquier parte?
* ¿Su compañía quiere restricciones tooestablish según la ubicación del usuario toohello?

Una vez que comprenda estos requisitos, es importante tooalso evaluar los requisitos del usuario de hello para la autenticación multifactor. Esta evaluación es importante porque definirá los requisitos de Hola para implementar la autenticación multifactor. Asegúrese de seguro hello tooanswer siguientes preguntas:

* ¿Está familiarizado con la autenticación multifactor a los usuarios de hello?
* ¿Algunos usos puede tooprovide requiere la autenticación adicional?  
  * ¿En caso afirmativo, todos Hola tiempo, al proceder de redes externas o acceso a aplicaciones específicas, o en otras condiciones?
* Hola ¿necesitarán los usuarios entrenamiento acerca de cómo toosetup e implementar la autenticación multifactor?
* ¿Cuáles son los escenarios clave de Hola que su compañía desea tooenable la autenticación multifactor para sus usuarios?

Después de responder a preguntas anteriores de hello, podrán capaz de toounderstand si no hay ya ha implementado la autenticación multifactor local. Esta evaluación es requisitos técnicos de hello toodefine importante para configurar y permitir que los usuarios de organizaciones de hello para la autenticación multifactor. Asegúrese de seguro hello tooanswer siguientes preguntas:

* ¿La compañía necesita cuentas con privilegios de tooprotect con MFA?
* ¿La compañía necesita tooenable MFA para ciertas aplicaciones por motivos de cumplimiento?
* ¿La compañía necesita tooenable MFA para todos los usuarios válidos de estas aplicaciones o solo los administradores?
* ¿Necesita tener MFA siempre habilitado o solo cuando inician sesión los usuarios de hello fuera de la red corporativa?

## <a name="next-steps"></a>Pasos siguientes
[Definición de una estrategia de adopción de identidad híbrida](active-directory-hybrid-identity-design-considerations-identity-adoption-strategy.md)

## <a name="see-also"></a>Otras referencias
[Información general sobre las consideraciones de diseño](active-directory-hybrid-identity-design-considerations-overview.md)

