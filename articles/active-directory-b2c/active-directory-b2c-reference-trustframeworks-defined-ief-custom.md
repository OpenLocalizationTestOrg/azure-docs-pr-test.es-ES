---
title: 'Referencia de Azure Active Directory B2C: marcos de confianza | Microsoft Docs'
description: Un tema sobre hello Identity Framework de la experiencia y las directivas personalizadas de Azure Active Directory B2C
services: active-directory-b2c
documentationcenter: 
author: rojasja
manager: krassk
editor: rojasja
ms.assetid: 
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.topic: article
ms.devlang: na
ms.date: 08/04/2017
ms.author: joroja
ms.openlocfilehash: d9634da72cb136ac165dd32e735622b5d0e22ec3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="define-trust-frameworks-with-azure-ad-b2c-identity-experience-framework"></a>Definir marcos de confianza con el marco de experiencia de identidad de Azure AD B2C

Azure B2C de directorio activo (Azure AD B2C) las directivas personalizadas que utilizan Hola Identity Framework de la experiencia de proporcionan a su organización con un servicio centralizado. Este servicio reduce la complejidad de Hola de federación de identidades en una gran comunidad de interés. complejidad de Hello es reducida tooa sola relación de confianza y un intercambio de metadatos único.

Directivas personalizadas de Azure AD B2C que use Hola identidad experiencia Framework tooenable tooanswer Hola siguientes preguntas:

- ¿Qué Hola legal, seguridad, privacidad y las directivas de protección de datos que se deben cumplir para?
- ¿Quiénes son los contactos de Hola y ¿cuáles son los procesos de Hola para convertirse en un participante acreditado?
- ¿Quién es Hola accredited proveedores de información de identidad (también conocido como "proveedores de notificaciones") y lo que ofrecen?
- ¿Quiénes son Hola accredited usuarios de confianza (y si lo desea, ¿qué ¿necesitan)?
- ¿Qué técnica "en el cable Hola" hello requisitos de interoperabilidad participantes?
- ¿Qué son las reglas de operativa "tiempo de ejecución" de Hola que deben aplicarse para intercambiar información de identidades digitales?

construcción de tooanswer todas estas preguntas, Azure AD B2C directivas personalizadas que utilizan Hola Hola de uso de Framework de la experiencia de identidad Framework confiar (TF). Vamos a considerar esta construcción y lo que proporciona.

## <a name="understand-hello-trust-framework-and-federation-management-foundation"></a>Entender los fundamentos de administración de Framework de confianza y la federación de Hola

Hola confiar Framework es una especificación escrita de hello identidad, seguridad, privacidad y datos de directivas de protección deben cumplir toowhich participantes en una comunidad de interés.

La identidad federada proporciona una base para conseguir la garantía de identidad del usuario final a escala de Internet. Mediante la delegación de partes de toothird de administración de identidades, se puede reutilizar una sola identidad digital para el usuario final con varios usuarios de confianza.  

Verificación de la identidad requiere que los proveedores de identidades (IdPs) y proveedores de atributo (AtPs) cumplan toospecific seguridad, privacidad y directivas operativas y procedimientos recomendados.  Si no se realizan inspecciones directa, usuarios de confianza (RP) debe desarrollar hello IdPs y AtPs deciden toowork con relaciones de confianza.  

A medida que aumenta el número de Hola de consumidores y proveedores de información de identidades digitales, es difícil toocontinue management en pares de estas relaciones de confianza o incluso Hola exchange en pares de hello metadatos técnica necesaria para la conectividad de red .  Los centros de federación solo han logrado un éxito limitado a la hora de resolver estos problemas.

### <a name="what-a-trust-framework-specification-defines"></a>Qué define una especificación de marco de confianza
TFs son linchpins Hola Hola abierto identidad Exchange (OIX) de confianza del modelo de Framework, donde cada comunidad de interés se rige por una especificación de TF determinada. Esta especificación de TF define:

- **Hola métricas de seguridad y privacidad para la Comunidad de Hola de interés con la definición de Hola de:**
    - niveles de Hola de seguridad (equilibrio de carga) que se ofrecen / / / requerida por los participantes. Por ejemplo, un conjunto ordenado de las clasificaciones de confianza de autenticidad de Hola de información de identidades digitales.
    - Hola niveles de protección (LOP) que ofrece / / / requerida por los participantes. Por ejemplo, un conjunto ordenado de las clasificaciones de confianza para la protección de Hola de información de identidades digitales que esté controlada por los participantes de la Comunidad de Hola de interés.

- **Descripción de la información de identidades digitales de Hola que ha ofrecido/requerida por los participantes de Hola**.

- **Hola las directivas técnicas de producción y el consumo de la información de identidades digitales y, por tanto, para medir el equilibrio de carga y LOP. Escriben directivas normalmente incluyen hello siguientes categorías de directivas:**
    - Directivas de corrección de identidad, por ejemplo: *lo fuerte que se examina la información de identidad de una persona*.
    - Directivas de seguridad, por ejemplo: *lo fuerte que se protege la integridad y la confidencialidad de la información*.
    - Directivas de privacidad, por ejemplo: *el control que tiene un usuario sobre la información personal identificable (PII)*.
    - Directivas de supervivencia, por ejemplo: *el funcionamiento de la continuidad y la protección de PII en caso de que un proveedor suspenda sus operaciones*.

- **perfiles de técnica de Hola para producción y el consumo de la información de identidades digitales. Estos perfiles incluyen:**
    - Interfaces de ámbito para las que la información de identidad digital está disponible en el LOA especificado.
    - Requisitos técnicos para la interoperabilidad en la red.

- **Hola descripciones de hello diversas funciones que los participantes en la Comunidad de hello pueden realizar y Hola calificaciones toofulfill requiere estos roles.**

Por lo tanto una especificación de TF rige cómo se intercambia información de identidad entre los participantes de Hola de comunidad Hola de interés: usuarios de confianza, identidad y proveedores de atributo y comprobadores de atributo.

Una especificación de TF es uno o varios documentos que sirven como referencia para el gobierno Hola de comunidad Hola de interés que regula la aserción de Hola y el consumo de la información de identidades digitales dentro de la Comunidad de Hola. Es un conjunto de directivas documentados y procedimientos diseñado tooestablish confianza en identidades digitales Hola que se usan para las transacciones en línea entre los miembros de una comunidad de interés.  

En otras palabras, una especificación de TF define las reglas de hello para la creación de un ecosistema de identidad federada viable para una comunidad.

Actualmente no hay acuerdo generalizada en beneficio de Hola de este enfoque. Sin duda hay que confianza especificaciones de framework facilitan el desarrollo de Hola de ecosistemas de identidades digitales con características de seguridad, seguridad y privacidad comprobables, lo que significa que puede reutilizar en varias comunidades de interés.

Por esa razón, directivas personalizadas de Azure AD B2C que usar hello identidad experiencia Framework utiliza especificación de hello como base de Hola de su representación de datos para una interoperabilidad de toofacilitate TF.  

Azure AD B2C las directivas personalizado que aprovechan Hola identidad experiencia Framework representan una especificación de TF como una combinación de datos para el usuarios y legible por máquina. Algunas secciones de este modelo (normalmente, las secciones que están más orientadas a la regulación) se representan como hace referencia a documentación de directiva de seguridad y privacidad de toopublished con el junto con hello procedimientos relacionados con (si existe). Otras secciones se describen en detalle Hola metadatos y tiempo de ejecución de reglas de configuración que facilitan la automatización de las operaciones.

## <a name="understand-trust-framework-policies"></a>Descripción de las directivas del marco de confianza

En cuanto a implementación, Hola especificación TF consta de un conjunto de directivas que permiten un control completo sobre los comportamientos de identidad y experiencias.  Directivas personalizadas de Azure AD B2C que aprovechan Hola Identity Framework de experiencia habilitar tooauthor y crear su propios TF a través de dichas directivas declarativas que se puede definir y configurar:

- referencia de documento de Hola o referencias que definen el ecosistema de identidad federada de Hola de comunidad de Hola que relaciona toohello TF. Únicamente son la documentación de vínculos toohello TF. Hola reglas (predefinido) operativa "tiempo de ejecución" o viajes de usuario de Hola que automatizan o controlan exchange Hola y el uso de notificaciones de Hola. Estos recorridos están asociados con un LOA (y un LOP). Por lo tanto, una directiva puede tener recorridos de usuario con LOA (y LOP) variables.

- proveedor de notificaciones de proveedores de identidad y atributo de Hola o hello, en la Comunidad de Hola de interés y Hola perfiles técnicas admiten junto con la autorización de equilibrio de carga/LOP (fuera de banda) de Hola que relaciona toothem.

- integración de Hello con comprobadores de atributo o proveedores de notificaciones.

- usuarios de confianza de Hello en la Comunidad de hello (mediante la inferencia).

- Hola metadatos para establecer comunicaciones de red entre los participantes. Estos metadatos, junto con perfiles técnica de hello, se usan durante una transacción tooplumb "en el cable Hola" interoperabilidad entre el usuario de confianza de Hola y otros participantes de la Comunidad.

- Hola conversión de protocolo, si existe (por ejemplo, SAML, OAuth2, WS-Federation y OpenID Connect).

- requisitos de autenticación de Hola.

- Hola multifactor ninguna orquestación si existe.

- Un esquema compartido para todas las notificaciones de Hola que están disponibles y tooparticipants de asignaciones de una comunidad de interés.

- Hola todas las notificaciones de transformaciones, junto con la minimización de datos posibles de hello en este contexto, el intercambio de hello toosustain y el uso de hello notificaciones.

- enlace de Hola y el cifrado.

- Hola notificaciones de almacenamiento.

### <a name="understand-claims"></a>Descripción de las notificaciones

> [!NOTE]
> Nos referimos colectivamente tipos posibles de hello tooall de información de identidad que se pueden intercambiar como "notificaciones": notificaciones acerca de la credencial de autenticación de un usuario final, control de identidad, dispositivos de comunicación, ubicación física, identificar personalmente atributos y así sucesivamente.  
>
> Utilizamos Hola término "notificaciones", en lugar de "atributos", porque en las transacciones en línea, estos artefactos de datos no son hechos que se pueden comprobar directamente Hola para usuario autenticado. En su lugar son aserciones o notificaciones, sobre los hechos para qué hello usuario de confianza debe desarrollar transacción solicitado suficiente confianza toogrant Hola del usuario final.  
>
> También utilizamos término Hola "notificaciones" porque Azure AD B2C las directivas personalizadas que utilizan Hola Framework de la experiencia de identidad son diseñado exchange de hello toosimplify de todos los tipos de información de identidades digitales de una manera coherente independientemente de si Hola subyacente Protocolo se define para la recuperación de autenticación o un atributo de usuario.  Del mismo modo, usamos el término de hello toocollectively "proveedor de notificaciones" consulte tooidentity proveedores y proveedores de atributo, comprobadores de atributo cuando deseamos toodistinguish entre sus funciones específicas.   

Por lo tanto, estas determinan cómo la información se intercambia entre un usuario de confianza, los proveedores de identidades y atributos y los comprobadores de atributos. Controlan qué proveedores de identidades y atributos se requieren para la autenticación de un usuario de confianza. Se deben considerar como un lenguaje específico del dominio (DSL), es decir, un lenguaje informático especializado para un dominio de aplicación particular con herencia, instrucciones *if* y polimorfismo.

Estas directivas constituyen parte legible por máquina de Hola de hello TF construir en las directivas de Azure AD B2C personalizado aprovechando Hola Framework de la experiencia de identidad. Incluyen todos los detalles operativos de hello, incluir metadatos proveedores de notificaciones y perfiles técnicos, definiciones de esquema de notificaciones, las funciones de transformación de notificaciones y viajes de usuario que se rellenan en toofacilitate operativa orquestación y automatización.  

Se supone que toobe *documentos de la vida* porque no hay una gran probabilidad de que su contenido cambiará con el tiempo relativas a los participantes activos Hola declarados en las directivas de Hola. También hay posibilidad de Hola que podrían cambiar Hola términos y condiciones para ser un participante.  

El programa de instalación de la federación y el mantenimiento se ha simplificado por usuarios de confianza de reconfiguraciones en curso de confianza y la conectividad de blindaje como proveedores de notificaciones diferentes/comprobadores unirse o abandonar (representada por la Comunidad de hello) Hola conjunto de directivas.

La interoperabilidad es otro desafío importante. Debe estar integrados comprobadores/proveedores de notificaciones adicionales, como usuarios de confianza son toosupport poco probable Hola a todos los protocolos necesarios. Las directivas personalizadas de Azure AD B2C resolución este problema si la compatibilidad de protocolos estándar del sector y mediante la aplicación de viajes de usuario específico tootranspose solicitudes cuando no son compatibles con usuarios de confianza y los proveedores de atributo Hola mismo protocolo.  

Viajes de usuario incluyen perfiles de protocolo y los metadatos que están tooplumb usado "en el cable Hola" interoperabilidad entre el usuario de confianza de Hola y otros posibles participantes. También hay reglas operativa en tiempo de ejecución que son mensajes de solicitud/respuesta de tooidentity aplicado información exchange para exigir el cumplimiento de directivas publicadas como parte de la especificación de TF Hola. idea Hola de viajes de usuario es clave toohello una personalización de la experiencia del cliente Hola. También luz sobre el funcionamiento del sistema de hello en nivel de protocolo de Hola.

En esta base, portales y aplicaciones de usuario de confianza pueden, dependiendo de su contexto, invocar directivas personalizadas de Azure AD B2C que aproveche la Hola identidad experiencia Framework pasando Hola nombre de una directiva específica y obtener con precisión el comportamiento de hello e información intercambio que deseen sin cualquiera muss, toquetee o riesgo.
