---
title: "Consideraciones de diseño de identidad de aaaAzure Active Directory híbrida - determinar los requisitos de administración de contenido | Documentos de Microsoft"
description: "Proporciona una visión general de cómo toodetermine Hola requerimientos de administración de contenido de su negocio. Normalmente cuando un usuario tiene su propio dispositivo puede tener también varias credenciales que se pueden alternar aplicación toohello correspondiente que se utiliza. Es importante toodifferentiate el contenido que se creó mediante credenciales personales frente a hello las siguieron credenciales corporativas. La solución de identidad debe ser capaz de toointeract con tooprovide de servicios de nube un experiencia perfecta toohello final de usuario mientras se garantiza su privacidad y aumentar la protección de hello contra la pérdida de datos."
documentationcenter: 
services: active-directory
author: billmath
manager: femila
editor: 
ms.assetid: dd1ef776-db4d-4ab8-9761-2adaa5a4f004
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/18/2017
ms.author: billmath
ms.openlocfilehash: 607d366633c37b65ec5cf8ae5c64d73ca1cc96b7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="determine-content-management-requirements-for-your-hybrid-identity-solution"></a>Determinación de los requisitos de administración de contenido para la solución de identidad híbrida
Descripción Hola administración de contenido de los requisitos de su empresa puedan dirigir afectan a la decisión sobre qué toouse de solución de identidad híbrida. Con Hola proliferación de varios dispositivos y la capacidad de Hola de usuarios toobring sus propios dispositivos ([BYOD](http://aka.ms/byodcg)), empresa Hola debe proteger sus propios datos sin embargo también debe tener privacidad del usuario intacta. Normalmente cuando un usuario tiene su propio dispositivo puede tener también varias credenciales que se pueden alternar aplicación toohello correspondiente que se utiliza. Es importante toodifferentiate el contenido que se creó mediante credenciales personales frente a hello las siguieron credenciales corporativas. La solución de identidad debe ser capaz de toointeract con tooprovide de servicios de nube un experiencia perfecta toohello final de usuario mientras se garantiza su privacidad y aumentar la protección de hello contra la pérdida de datos. 

La solución de identidad se aprovecharán por los diferentes controles técnicos en administración de contenido de orden tooprovide tal y como se muestra en la siguiente ilustración de hello:

![](./media/hybrid-id-design-considerations/securitycontrols.png)

**Controles de seguridad que aprovecharán su sistema de administración de identidad**

En general, los requisitos de administración de contenido aprovecharán su sistema de administración de identidades en hello siguientes áreas:

* Privacidad: identificación de usuario de Hola que posee un recurso y aplicar la integridad de toomaintain de hello controles adecuados.
* Clasificación de datos: identificar usuario Hola o de grupo y de nivel de objeto de tooan de acceso según la clasificación de tooits. 
* Protección contra la pérdida de datos: controles de seguridad responsables de proteger la pérdida de datos tooavoid deberá toointeract con la identidad del usuario de hello identidad sistema toovalidate Hola. Esto también es importante para los fines de seguimiento de auditoría.

> [!NOTE]
> Lea [Clasificación de los datos para prepararlos para la nube](http://download.microsoft.com/download/0/A/3/0A3BE969-85C5-4DD2-83B6-366AA71D1FE3/Data-Classification-for-Cloud-Readiness.pdf) para obtener más información sobre los procedimientos recomendados e instrucciones para la clasificación de los datos.
> 
> 

Cuando planifique la solución de identidad híbrida asegurarse de esa Hola después se responden preguntas según los requisitos de la organización tooyour:

* ¿La compañía tiene controles de seguridad en lugar tooenforce privacidad de los datos?
  * ¿Si es así, los controles de seguridad será capaz de toointegrate con la solución de identidad híbrida de Hola que son tooadopt continua?
* ¿Usa su empresa clasificación de los datos?
  * ¿Si es así, es toointegrate capaz de hello actual de solución con la solución de identidad híbrida de Hola que son tooadopt continuo?
* ¿Tiene su empresa actualmente una solución para hacer frente a la pérdida de datos? 
  * ¿Si es así, es toointegrate capaz de hello actual de solución con la solución de identidad híbrida de Hola que son tooadopt continuo?
* ¿La compañía necesita tooaudit acceso tooresources?
  * En caso afirmativo, ¿para qué tipo de recursos?
  * En caso afirmativo, ¿qué nivel de información es necesario?
  * ¿En caso afirmativo, donde debe residir registro de auditoría de hello? ¿Local o en la nube de hello?
* ¿La compañía necesita tooencrypt los mensajes de correo electrónico que contengan datos confidenciales (números de seguridad social, números de tarjeta de crédito, etcetera)?
* ¿La compañía necesita tooencrypt todos los documentos o contenido compartido con socios comerciales externos?
* ¿La compañía necesita las directivas corporativas de tooenforce en ciertos tipos de mensajes de correo electrónico (sin responder a todos, no reenviar)?

> [!NOTE]
> Hacer notas de tootake seguro de cada respuesta y entender el razonamiento de hello detrás de respuesta de Hola. [Definir la estrategia de protección de datos](active-directory-hybrid-identity-design-considerations-data-protection-strategy.md) irá Hola opciones disponibles y las ventajas y desventajas de cada opción.  Las respuestas que obtenga partir de estas preguntas le servirán para seleccionar la opción que mejor se adapte a sus necesidades empresariales.
> 
> 

## <a name="next-steps"></a>Pasos siguientes
[Determinación de los requisitos de control de acceso](active-directory-hybrid-identity-design-considerations-accesscontrol-requirements.md)

## <a name="see-also"></a>Otras referencias
[Información general sobre las consideraciones de diseño](active-directory-hybrid-identity-design-considerations-overview.md)

