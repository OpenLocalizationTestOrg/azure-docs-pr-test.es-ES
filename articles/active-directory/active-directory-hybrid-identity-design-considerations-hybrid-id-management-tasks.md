---
title: "aaaAzure identidad híbrida de Active Directory consideraciones de diseño: determinación de las tareas de administración de identidades híbridas | Documentos de Microsoft"
description: "Con control de acceso condicional, Azure Active Directory comprueba las condiciones específicas de Hola que elegir al autenticar usuario hello y antes de permitir el acceso toohello aplicación. Una vez que se cumplen estas condiciones, usuario de hello es autenticado y acceso toohello aplicación permitida."
documentationcenter: 
services: active-directory
author: billmath
manager: femila
editor: 
ms.assetid: 65f80aea-0426-4072-83e1-faf5b76df034
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/18/2017
ms.author: billmath
ms.openlocfilehash: d3c0e9b23f43127b3d8e0b3a4e8f03d4bc148c27
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="plan-for-hybrid-identity-lifecycle"></a>Plan para el ciclo de vida de identidad híbrida
Identidad es una de las bases de Hola de su estrategia de acceso de aplicación y la movilidad empresarial. Si va a iniciar sesión en el dispositivo móvil tooyour o una aplicación de SaaS, su identidad es hello toogaining clave acceso tooeverything. En su nivel más alto, una solución de administración de identidades abarca unificación y sincronización entre los repositorios de identidad que incluye la automatización y centralizar el proceso de Hola de aprovisionamiento de recursos. solución de identidad de Hello debe puede ser una identidad centralizada la nube y locales y también utilizar alguna forma de autenticación centralizada de toomaintain de federación de identidades y segura comparten y colaboran con las empresas y los usuarios externos. Recursos oscilar entre sistemas operativos y aplicaciones toopeople en o afiliados a una organización. Estructura organizativa puede ser modificada tooaccommodate Hola aprovisionamiento directivas y procedimientos.

También es importante toohave una solución de identidad orientadas tooempower los usuarios al proporcionarles con experiencias de autoservicio tookeep ellos productivo. La solución de identidad es más estable si habilita el inicio de sesión único para los usuarios a través de todos los recursos de Hola que necesitan tener acceso a los administradores en todos los niveles pueden usar los procedimientos estándar para administrar las credenciales de usuario. Se reduce o elimina, dependiendo de la amplitud de Hola de hello aprovisionamiento de la solución de administración de algunos niveles de administración. Además, se pueden distribuir de manera segura funcionalidades de administración, manual o automáticamente, entre varias organizaciones. Por ejemplo, un administrador de dominio puede servir sólo personas hello y recursos de ese dominio. Este usuario puede realizar las tareas administrativas y aprovisionamiento, pero es no autorizado toodo tareas de configuración, como la creación de flujos de trabajo.

## <a name="determine-hybrid-identity-management-tasks"></a>Determinación de las tareas de administración de identidad híbrida
Distribuir las tareas administrativas en su organización mejora la precisión de Hola y la eficacia de la administración y mejora el saldo de Hola de carga de trabajo de Hola de una organización. Siguientes son los ejes de Hola que definen un sistema de administración de identidad sólida.

 ![](./media/hybrid-id-design-considerations/Identity_management_considerations.png)

las tareas de administración de identidad de toodefine híbrido, debe entender algunas características fundamentales de organización de Hola que estarán adoptando la identidad híbrida. Es repositorios actual del hello toounderstand importante que se usa para orígenes de identidades. Conociendo los principales elementos, deberá cumplir los requisitos fundamentales de Hola y en función de que necesite tooask más granular de preguntas que le llevará tooa mejor decisión de diseño para la solución de identidad.  

Al definir los requisitos, asegúrese de que al menos Hola después se responden preguntas

* Opciones de aprovisionamiento: 
  
  * ¿Solución de identidad híbrida de hello admite un sistema de aprovisionamiento y administración de cuentas robusto acceso?
  * ¿De qué usuarios, grupos y contraseñas van toobe administrado?
  * ¿Es la administración de ciclo de vida de identidades de hello respondiendo? 
    * ¿Cuánto tiempo tarda la suspensión de la cuenta de actualización de contraseña?
* Administración de licencias: 
  
  * ¿Hola administración híbrida identidad solución identificadores de licencia?
    * En caso afirmativo, ¿qué  funcionalidades están disponibles?
* ¿Hola administración de licencias basadas en grupos de identificador de solución? 
  
      - ¿Si es así, es posible tooassign un tooit de grupo de seguridad? 
       - ¿En caso afirmativo, directorio de la nube de hello asignará automáticamente licencias los miembros de hello tooall del grupo de hello? 
        - ¿Qué ocurre si un usuario posteriormente se agregan a o quitar del grupo de hello, se una licencia automáticamente asignada o se quitará según corresponda? 
* Integración con otros proveedores de identidades de terceros:
* ¿Esta solución híbrida se puede integrar con identidades de terceros proveedores tooimplement inicio de sesión único?
* ¿Es posible toounify todos Hola distintos proveedores de identidades en un sistema de identidad coherente?
* En caso afirmativo, ¿cómo y cuáles son y que funcionalidades hay disponibles?

## <a name="synchronization-management"></a>Administración de la sincronización
Uno de los objetivos de Hola de un administrador de identidades, toobe puede toobring Hola a todos los proveedores de identidades y mantenerlos sincronizados. Mantener datos Hola sincronizados en función de un proveedor de identidades maestro autoritativo. En un escenario de identidad híbrida, con un modelo de administración sincronizados, administrar todas las identidades de usuarios y dispositivos en un servidor local y sincronizar las cuentas de hello y, opcionalmente, en la nube toohello contraseñas. usuario de Hello escribe Hola misma contraseña local igual que en la nube hello y en iniciar sesión, contraseña de Hola se comprueba mediante soluciones de identidad de Hola. En este modelo se emplea una herramienta de sincronización de directorios.

![](./media/hybrid-id-design-considerations/Directory_synchronization.png)sincronización de hello tooproper diseño de la solución de identidad híbrida asegurarse de esa Hola después de preguntas se responden: • ¿qué soluciones de sincronización de hello disponibles para la solución de identidad híbrida de hello?
• ¿Qué inicio de sesión único de hello en capacidades disponibles?
• ¿Cuáles son las opciones de hello para la federación de identidades entre B2B y B2C?

## <a name="next-steps"></a>Pasos siguientes
[Determinación de la estrategia de adopción de administración de identidad híbrida](active-directory-hybrid-identity-design-considerations-lifecycle-adoption-strategy.md)

## <a name="see-also"></a>Otras referencias
[Información general sobre las consideraciones de diseño](active-directory-hybrid-identity-design-considerations-overview.md)

