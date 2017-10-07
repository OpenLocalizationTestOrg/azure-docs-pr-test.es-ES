---
title: "Consideraciones de diseño de identidad de aaaAzure Active Directory híbrida - información general | Documentos de Microsoft"
description: "Información general y mapa de contenido de la guía de consideraciones de diseño de identidad híbrida"
documentationcenter: 
services: active-directory
author: billmath
manager: femila
editor: 
ms.assetid: 100509c4-0b83-4207-90c8-549ba8372cf7
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/18/2017
ms.author: billmath
ms.openlocfilehash: 10aacb04c90abd100eb56d7c44d590946b052f18
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-hybrid-identity-design-considerations"></a>Consideraciones de diseño de identidad híbrida de Azure Active Directory
Dispositivos basados en el consumidor proliferan Hola a todos corporativa y basada en la nube aplicaciones de software como servicio (SaaS) son tooadopt fácil. Como resultado, resulta difícil mantener el control de acceso a las aplicaciones de los usuarios entre centros de datos internos y plataformas en la nube.  

Soluciones de identidad de Microsoft abarcan local y capacidades en la nube, crear una identidad de usuario único para la autenticación y autorización de recursos de tooall, independientemente de su ubicación. A esto le llamamos identidad híbrida. Hay diseños y las opciones de configuración de identidad híbrida con soluciones de Windows y, en algunos casos puede que sea difícil toodetermine qué combinación satisfará mejor las necesidades de Hola de su organización. 

Esta guía de consideraciones de diseño de identidad híbrida le ayudará a toounderstand cómo toodesign una solución de identidad híbrida que mejor se adapte a la tecnología y negocio Hola necesidades de su organización.  Esta guía detalla una serie de pasos y tareas que puede seguir toohelp se diseña una solución de identidad híbrida que cumpla los requisitos exclusivos de su organización. En todos los pasos de Hola y tareas, Guía de hello presentará las tecnologías relevantes de Hola y característica opciones disponibles tooorganizations toomeet funcional y calidad de servicio (por ejemplo, disponibilidad, escalabilidad, rendimiento, capacidad de administración y seguridad) requisitos de nivel. 

En concreto, objetivos de guía de consideraciones de diseño de hello híbrida identidad son hello tooanswer siguientes preguntas: 

* ¿Qué preguntas necesita tooask y responder toodrive un diseño de identidad específica híbrido para un dominio del problema o tecnología que mejor adapte a mis necesidades?
* ¿Qué secuencia de actividades debe completar la toodesign una solución de identidad híbrida de dominio del problema o tecnología de hello? 
* ¿Qué opciones de configuración y tecnología de identidad híbrida están disponible toohelp me satisfacer mis necesidades? ¿Cuáles son Hola ventajas y desventajas de las opciones para poder seleccionar mejor opción de Hola para mi empresa?

## <a name="who-is-this-guide-intended-for"></a>¿A quién va dirigida esta guía?
 CIO, CITO, arquitectos de identidad jefe, arquitectos de empresa y arquitectos de TI responsables de diseñar una solución de identidad híbrida para organizaciones medianas o grandes.

## <a name="how-can-this-guide-help-you"></a>¿Cómo puede ayudarle esta guía?
Puede usar esta guía toounderstand cómo toodesign una solución de identidad híbrida que es capaz de toointegrate una nube según el sistema de administración de identidad con la actual identidad solución local. 

Hola siguiente gráfico muestra un ejemplo de una solución de identidad híbrida que permite a los administradores de TI toomanage toointegrate sus actual Windows Server Active Directory solución encuentra de forma local con Microsoft Azure Active Directory tooenable usuarios toouse único Inicio de sesión (SSO) en todas las aplicaciones que se encuentra en la nube de Hola y local.

![](./media/hybrid-id-design-considerations/hybridID-example.png)

Hola por encima de la ilustración es un ejemplo de una solución de identidad híbrida que usa en la nube y los servicios de toointegrate con capacidades locales en orden tooprovide un proceso de autenticación de usuario final de experiencia de inicio único toohello toofacilitate TI administrar esos recursos. Aunque esto puede ser un escenario muy común, diseño de identidad híbrida de las organizaciones es probable toobe diferente se muestra en la figura 1 debido a los requisitos de toodifferent de ejemplo de Hola. 

Esta guía proporciona una serie de pasos y tareas que puede seguir toodesign una solución de identidad híbrida que cumpla los requisitos exclusivos de su organización. A lo largo de hello siguientes pasos y tareas, Hola guía presenta hello las tecnologías relevantes y característica Opciones requisitos de nivel de calidad de servicio y funcionalidad de toomeet y tooyou disponibles para su organización.

**Suposiciones**: tiene algo de experiencia con Windows Server, Servicios de dominio de Active Directory y Azure Active Directory. En este documento, se supone que está buscando cómo estas soluciones pueden satisfacer sus necesidades de negocio por sí solas o en una solución integrada.

## <a name="design-considerations-overview"></a>Información general sobre las consideraciones de diseño
Este documento proporciona un conjunto de pasos y tareas que puede seguir toodesign una solución de identidad híbrida que mejor se adapte a sus requisitos. Hola pasos se presentan en una secuencia ordenada. Las consideraciones de diseño que aprenderá en pasos posteriores pueden requerir que las decisiones de toochange que tomó en los pasos anteriores, sin embargo, debido a las opciones de diseño de tooconflicting. Se realiza cada intento tooalert se toopotential conflictos de diseño a lo largo del documento de Hola. 

Llegarán en diseño de Hola que mejor adapte sus requisitos solo después de recorrer en iteración los pasos de hello tantas veces como necesario tooincorporate todas las consideraciones de hello en el documento de Hola. 

| Fase de identidad híbrida | Lista de temas |
| --- | --- |
| Determinación de los requisitos de identidad |[Determinación de las necesidades empresariales](active-directory-hybrid-identity-design-considerations-business-needs.md)<br> [Determinación de los requisitos de sincronización de directorios](active-directory-hybrid-identity-design-considerations-directory-sync-requirements.md)<br> [Determinación de los requisitos de autenticación multifactor](active-directory-hybrid-identity-design-considerations-multifactor-auth-requirements.md)<br> [Definición de una estrategia de adopción de identidad híbrida](active-directory-hybrid-identity-design-considerations-identity-adoption-strategy.md) |
| Plan para mejorar la seguridad de los datos mediante una solución de identidad sólida |[Determinación de los requisitos de protección de datos](active-directory-hybrid-identity-design-considerations-dataprotection-requirements.md) <br> [Determinación de los requisitos de administración de contenido](active-directory-hybrid-identity-design-considerations-contentmgt-requirements.md)<br> [Determinación de los requisitos de control de acceso](active-directory-hybrid-identity-design-considerations-accesscontrol-requirements.md)<br> [Determinación de los requisitos de respuesta a incidentes](active-directory-hybrid-identity-design-considerations-incident-response-requirements.md) <br> [Definición de la estrategia de protección de datos](active-directory-hybrid-identity-design-considerations-data-protection-strategy.md) |
| Plan para el ciclo de vida de identidad híbrida |[Determinación de las tareas de administración de identidades híbridas](active-directory-hybrid-identity-design-considerations-hybrid-id-management-tasks.md) <br> [Administración de la sincronización](active-directory-hybrid-identity-design-considerations-hybrid-id-management-tasks.md)<br> [Determinación de la estrategia de adopción de administración de identidad híbrida](active-directory-hybrid-identity-design-considerations-lifecycle-adoption-strategy.md) |

## <a name="download-this-guide"></a>Descargar esta guía
Puede descargar una versión pdf de guía de consideraciones de diseño de identidad híbrida de Hola de hello [Galería de Technet](https://gallery.technet.microsoft.com/Azure-Hybrid-Identity-b06c8288). 

