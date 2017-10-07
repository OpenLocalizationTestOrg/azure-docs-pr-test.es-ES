---
title: 'Azure Active Directory B2C: notas del desarrollador acerca del uso de directivas personalizadas|Microsoft Docs'
description: "Notas para los desarrolladores sobre configuración y mantenimiento de Azure AD B2C con directivas personalizadas"
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
ms.date: 05/05/2017
ms.author: joroja
ms.openlocfilehash: 979b8a264eb819ee4a208b9171a53a5ffbf062c3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="release-notes-for-azure-active-directory-b2c-custom-policy-public-preview"></a>Notas de la versión preliminar de la directiva personalizada de Azure Active Directory B2C
Hello conjunto de características de directiva personalizada está ahora disponible para su evaluación en versión preliminar pública de todos los B2C Directory activa de Azure (Azure AD B2C) clientes. Este conjunto de características está destinada a desarrolladores de avanzado de identidades compilar soluciones de identidad de hello más complejas.  

En la actualidad, este conjunto de características requiere que los desarrolladores tooconfigure Hola identidad experiencia Framework directamente a través de la edición de archivos XML. Este método de configuración es eficaz y complejo. Los programadores de identidad mediante Hola avanzados identidad experiencia Framework debe planear tooinvest algún tiempo completar los tutoriales y lectura de los documentos de referencia. 

## <a name="features-included-in-this-public-preview"></a>Características que se incluyen en la versión preliminar pública
Con hello nuevas características introducidas en versión preliminar pública de hello, los desarrolladores pueden realizar Hola siguiente las tareas:<br>

* Crear y cargar recorridos del usuario de autenticación personalizada mediante directivas personalizadas. 
   * Describir los recorridos del usuario paso a paso como intercambios entre proveedores de notificaciones. 
   * Definir la creación de ramas condicional en recorridos del usuario. 
* Integrar servicios con la API de REST habilitada en los recorridos del usuario de autenticación personalizada.  
* Agregue la federación con proveedores de identidades que son compatibles con hello OpenIDConnect estándar. <br>
* Agregue la federación con proveedores de identidades que cumplen el protocolo toohello SAML 2.0. 

## <a name="terms-of-hello-public-preview"></a>Términos de vista previa pública de Hola

* Le recomendamos que características nuevas de hello toouse solo con fines de evaluación.<br>
* Las nuevas características no están pensadas para que se usen en entornos de producción.<br>
* Contratos de nivel de servicio (SLA) no aplican toohello nuevas características. <br>
* Las solicitudes de soporte técnico pueden enviarse a través de los canales de soporte técnico habituales. <br>
* No se puede garantizar ninguna fecha de disponibilidad general.<br>
* A su discreción y por cualquier motivo, Microsoft puede marcar y rechazar o restringir los escenarios y los viajes de usuario que superan el ámbito de Hola de hello Azure AD B2C producto carta tooserve como una plataforma de administración (CIAM) de identidad y acceso de cliente.

## <a name="responsibilities-of-custom-policy-feature-set-developers"></a>Responsabilidades de los desarrolladores de conjunto de características de directivas personalizadas
Configuración de directiva manual concede toohello de acceso de nivel inferior subyacente de la plataforma de Azure AD B2C y tiene como resultado Hola creación de una plataforma de confianza único totalmente personalizables. Las permutaciones posibles de proveedores de identidades personalizados, las relaciones de confianza, integraciones con servicios externos y los flujos de trabajo de paso a paso peticiones mayores colocar en hello avanzada a los desarrolladores consumirlos.

beneficio de toofully de versión preliminar pública de hello, se recomienda que los desarrolladores que consumen el conjunto de características de directiva personalizada de hello seguirán toohello siguientes instrucciones:
* Familiarizarse con el lenguaje de configuración de Hola de hello motor de la experiencia de identidad y administración de claves y secretos.
* Tomar posesión de escenarios e integraciones personalizadas.
* Realizar pruebas metódicas de los escenarios.
* Seguir los procedimientos recomendados de desarrollo de software y almacenamiento provisional con un mínimo de un entorno de desarrollo y prueba, y un entorno de producción.
* Manténgase informado sobre los nuevos desarrollos desde proveedores de identidades de Hola y servicios de con que integración. Por ejemplo, realizar un seguimiento de cambios en los secretos y del servicio de toohello programado y cambios.
* Configurar la supervisión activa y supervisar la capacidad de respuesta de Hola de entornos de producción.
* Mantener las direcciones de correo electrónico de contacto actual así como los correos electrónicos de toohello responde Microsoft equipo del sitio dinámico.
* Realizar acción oportuna cuando toodo aconsejable Hola así por equipo de sitio en directo de Microsoft. 


>[!NOTE]
>Estas características podrían incluirse finalmente en directivas integradas de Azure AD, lo que los desarrolladores de tooall sea más accesibles.

## <a name="next-steps"></a>Pasos siguientes
[Introducción a las directivas personalizadas](active-directory-b2c-get-started-custom.md).
