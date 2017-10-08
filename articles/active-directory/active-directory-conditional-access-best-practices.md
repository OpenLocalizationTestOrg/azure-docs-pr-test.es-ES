---
title: "prácticas recomendadas de aaaBest para el acceso condicional en Active Directory de Azure | Documentos de Microsoft"
description: "Obtenga información acerca de las cosas que debe saber y lo que se debe evitar hacer al configurar directivas de acceso condicional."
services: active-directory
keywords: tooapps de acceso condicional, el acceso condicional con Azure AD, proteger el acceso toocompany recursos, las directivas de acceso condicional
documentationcenter: 
author: MarkusVi
manager: femila
editor: 
ms.assetid: 8c1d978f-e80b-420e-853a-8bbddc4bcdad
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/12/2017
ms.author: markvi
ms.reviewer: calebb
ms.openlocfilehash: 4952f8746a2e583380b3bb99cfe2fbdae1c07b08
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="best-practices-for-conditional-access-in-azure-active-directory"></a>Procedimientos recomendados para el acceso condicional en Azure Active Directory

En este tema se proporciona información acerca de las cosas que debe saber y lo que se debe evitar hacer al configurar directivas de acceso condicional. Antes de leer este tema, debe familiarizarse con los conceptos de Hola y terminología de Hola que se describe en [acceso condicional en Azure Active Directory](active-directory-conditional-access-azure-portal.md)

## <a name="what-you-should-know"></a>Qué debería saber

### <a name="whats-required-toomake-a-policy-work"></a>¿Qué le ha exigido toomake un trabajo de directiva?

Cuando crea una nueva directiva, no hay usuarios, grupos, aplicaciones o controles de acceso seleccionados.

![Aplicaciones de nube](./media/active-directory-conditional-access-best-practices/02.png)


toomake funcionan de la directiva, debe configurar los siguientes hello:


|Qué           | Cómo                                  | Porqué|
|:--            | :--                                  | :-- |
|**Aplicaciones en la nube** |Debe tooselect una o más aplicaciones.  | objetivo de Hola de una directiva de acceso condicional es tooenable toofine optimizar cómo los usuarios autorizados pueden tener acceso a las aplicaciones.|
| **Usuarios y grupos** | Necesita tooselect al menos un usuario o grupo que está autorizado tooaccess hello las aplicaciones de nube que seleccionó. | Una directiva de acceso condicional que no tiene usuarios ni grupos asignados nunca se desencadena. |
| **Controles de acceso** | Necesita tooselect al menos un control de acceso. | El procesador de directivas necesita tooknow qué toodo si se cumplen las condiciones.|


Suma toothese básica en requisitos en, en muchos casos, también debe configurar una condición. Mientras una directiva también funcionará sin una condición configurada, las condiciones son un factor determinante para optimizar las aplicaciones de acceso tooyour Hola.


![Aplicaciones de nube](./media/active-directory-conditional-access-best-practices/04.png)



### <a name="how-are-assignments-evaluated"></a>¿Cómo se evalúan las asignaciones?

A todas las asignaciones se les asigna **la operación lógica AND**. Si tiene más de una asignación configurada, tootrigger una directiva, deben cumplirse todas las asignaciones.  

Si necesita tooconfigure una condición de ubicación que se aplica a las conexiones de tooall realizadas desde fuera de la red de su organización, puede hacerlo mediante:

- Incluir **todas las ubicaciones**.
- Excluir **todas las direcciones IP de confianza**.

### <a name="what-happens-if-you-have-policies-in-hello-azure-classic-portal-and-azure-portal-configured"></a>¿Qué ocurre si tiene las directivas de hello portal de Azure clásico y portal de Azure configurado?  
Las dos directivas se aplican mediante Azure Active Directory usuario hello, obteniendo así acceso únicamente cuando se cumplen todos los requisitos.

### <a name="what-happens-if-you-have-policies-in-hello-intune-silverlight-portal-and-hello-azure-portal"></a>¿Qué ocurre si tiene las directivas de Intune Silverlight portal Hola y Hola Portal de Azure?
Las dos directivas se aplican mediante Azure Active Directory usuario hello, obteniendo así acceso únicamente cuando se cumplen todos los requisitos.

### <a name="what-happens-if-i-have-multiple-policies-for-hello-same-user-configured"></a>¿Qué ocurre si tengo varias directivas para hello configurada por el mismo usuario?  
Para cada inicio de sesión, Azure Active Directory evalúa todas las directivas y se asegura de que se cumplen todos los requisitos antes de concedidos a los usuarios acceso toohello.


### <a name="does-conditional-access-work-with-exchange-activesync"></a>¿Funciona el acceso condicional con Exchange ActiveSync?

Sí, se puede usar Exchange ActiveSync en una directiva de acceso condicional.


## <a name="what-you-should-avoid-doing"></a>¿Qué no debería hacer?

marco de trabajo de acceso condicional de Hello proporciona una flexibilidad de configuración excelente. Sin embargo, gran flexibilidad significa también que debe revisar cuidadosamente cada tooreleasing anteriores de directiva de configuración tooavoid de resultados no deseados. En este contexto, debe prestar tooassignments atención especial que afecte a los conjuntos completos como **todos los usuarios / grupos y aplicaciones de la nube**.

En su entorno, debería evitar Hola siguiendo configuraciones:


**Para todos los usuarios, todas las aplicaciones en la nube:**

- **Bloquear acceso**: esta configuración bloquea toda la organización, lo cual no es en absoluto una buena idea.

- **Esta opción requiere un dispositivo compatible con** : para los usuarios que no se han inscrito sus dispositivos aún, esta directiva bloquea todo el acceso incluido acceso toohello Intune portal. Si eres un administrador sin un dispositivo inscrito, esta directiva bloquea de vuelta a la directiva de hello toochange portal Azure Hola.

- **Requerir unión a un dominio** : este bloque de directivas acceso tiene también Hola posibles tooblock acceso para todos los usuarios de su organización si todavía no tienes un dispositivo unido al dominio.


**Para todos los usuarios, todas las aplicaciones en la nube, todas las plataformas de dispositivos:**

- **Bloquear acceso**: esta configuración bloquea toda la organización, lo cual no es en absoluto una buena idea.


## <a name="common-scenarios"></a>Escenarios comunes

### <a name="requiring-multi-factor-authentication-for-apps"></a>Exigir autenticación multifactor para las aplicaciones

Muchos entornos tienen las aplicaciones que requieren un mayor nivel de protección que Hola otros usuarios.
Esto sucede, por ejemplo, hello para aplicaciones que tienen acceso a los datos toosensitive.
Si desea tooadd otro nivel de protección toothese aplicaciones, puede configurar una directiva de acceso condicional que requiere la autenticación multifactor cuando los usuarios tienen acceso a estas aplicaciones.


### <a name="requiring-multi-factor-authentication-for-access-from-networks-that-are-not-trusted"></a>Exigir autenticación multifactor para el acceso desde redes que no son de confianza

Este escenario es similar toohello anterior porque agrega un requisito para la autenticación multifactor.
Sin embargo, Hola principal diferencia es condición Hola para este requisito.  
Mientras se estaba foco Hola del escenario anterior hello en aplicaciones con acceso a los datos toosensitve, Hola de este escenario es ubicaciones de confianza.  
En otras palabras, podría tener un requisito de autenticación multifactor si un usuario accede a una aplicación desde una red que no es de confianza.


### <a name="only-trusted-devices-can-access-office-365-services"></a>Solo los dispositivos de confianza pueden acceder a servicios de Office 365

Si usa Intune en su entorno, inmediatamente puede comenzar a usar la interfaz de directiva de acceso condicional de Hola Hola consola de Azure.

Muchos clientes de Intune usa tooensure de acceso condicional que solo los dispositivos de confianza pueden tener acceso a servicios de Office 365. Esto significa que los dispositivos móviles inscriben con Intune y cumplan los requisitos de directiva de cumplimiento de normas y que los equipos con Windows son tooan Unidos a un dominio de local. Una importante mejora es que no haya tooset Hola misma directiva para cada uno de los servicios de hello Office 365.  Cuando se crea una nueva directiva, configure hello en la nube aplicaciones tooinclude cada de las aplicaciones de Office 365 Hola que desee tooprotect con el acceso condicional.

## <a name="next-steps"></a>Pasos siguientes

Si desea tooknow tooconfigure una directiva de acceso condicional, vea [empezar a trabajar con el acceso condicional en Azure Active Directory](active-directory-conditional-access-azure-portal-get-started.md).
