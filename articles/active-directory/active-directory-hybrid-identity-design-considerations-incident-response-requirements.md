---
title: "Consideraciones de diseño de identidad de aaaAzure Active Directory híbrida - determinar los requisitos de incidentes rResponse | Documentos de Microsoft"
description: "Determinar las capacidades de supervisión e informes de solución de identidad híbrida de Hola que se pueden utilizar con TI tootake acciones tooidentify y mitigar una amenaza potencial"
documentationcenter: 
services: active-directory
author: billmath
manager: femila
editor: 
ms.assetid: a3d2a459-599b-4b67-8e51-7369ee25082d
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/18/2017
ms.author: billmath
ms.openlocfilehash: 7084096f318ef461e8331fb6edde1b77d4108466
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="determine-incident-response-requirements-for-your-hybrid-identity-solution"></a>Determinación de los requisitos de respuesta a incidentes para su solución de identidad híbrida
Las organizaciones medianas o grandes probablemente tendrá un [respuesta a incidentes seguridad](https://technet.microsoft.com/library/cc700825.aspx) en lugar toohelp TI actuar en consecuencia toohello nivel de incidente. sistema de administración de identidades de Hello es un componente importante en el proceso de respuesta a incidentes de hello porque puede ser usado toohelp identificar quién llevó a cabo una acción específica en el destino de Hola. solución de identidad híbrida de Hello debe ser capaz de tooprovide de supervisión e informes de las capacidades que se pueden utilizar con TI tootake acciones tooidentify y mitigar una amenaza potencial. En un plan de respuesta a incidentes típica tendrá Hola después fases como parte del plan de hello:

1. Evaluación inicial.
2. Comunicación de incidentes
3. Control de daños y reducción de riesgos
4. Identificación de lo que se ha puesto en peligro y la gravedad
5. Conservación de evidencias
6. Partes tooappropriate de notificación.
7. Recuperación del sistema
8. Documentación.
9. Evaluación de daños y costos
10. Revisión del proceso y el plan.

Durante la identificación de Hola de lo que era riesgos y fase de gravedad, será necesario tooidentify Hola sistemas que han estado en peligro, archivos que se ha obtenido acceso y determinan la confidencialidad de Hola de esos archivos. El sistema de identidad híbrida debe ser capaz de toofulfill tooassist de estos requisitos, identificación de usuario de Hola que realizó los cambios. 

## <a name="monitoring-and-reporting"></a>Supervisión e informes
Sistema de identidades de hello muchas veces también puede ayudar en la fase de evaluación inicial de principalmente si el sistema de hello ha creado en la auditoría y capacidades de reporting. Durante la evaluación inicial de Hola, Administrador de TI debe ser capaz de tooidentify una actividad sospechosa o sistema Hola debe ser capaz de tootrigger automáticamente basándose en una tarea configurada previamente. Muchas actividades podrían indicar un posible ataque, sin embargo, en otros casos, un sistema mal configurado podría provocar a tooa número de falsos positivos en un sistema de detección de intrusiones. 

sistema de administración de identidades de Hello debe ayudar a tooidentify de administradores de TI y esas actividades sospechosas de informes. Por lo habitual, estos requisitos técnicos se pueden satisfacer con la supervisión de todos los sistemas y una funcionalidad de informes que pueda resaltar las posibles amenazas. Usar preguntas de hello debajo toohelp diseñar la solución de identidad híbrida teniendo en requisitos de respuesta a incidentes de cuenta:

* ¿Tiene su empresa una respuesta a incidentes de seguridad?
  * ¿En caso afirmativo, hello sistema de administración de identidad actual sirve como parte del proceso de hello?
* ¿La compañía necesita tooidentify sospechosa sesión intentos de los usuarios en diferentes dispositivos?
* ¿La compañía necesita toodetect posibles en peligro las credenciales del usuario?
* ¿La compañía necesita el acceso y la acción del usuario de tooaudit?
* ¿La compañía necesita tooknow cuando un usuario restablece su contraseña?

## <a name="policy-enforcement"></a>Aplicación de directivas
Durante el control de daños y fase de reducción de riesgo, es importante tooquickly reducir los efectos de hello real y potencial de un ataque. Esa acción que va a realizar en este momento puede hacer diferencia de hello entre un menor y mayor importancia. respuesta exacta Hola dependerá de su organización y la naturaleza de Hola de ataque de Hola que enfrenta. Si la evaluación inicial de hello había finalizado que se ha puesto en peligro una cuenta, necesitará tooenforce directiva tooblock esta cuenta. Que es simplemente un ejemplo donde se aprovecharán sistema de administración de identidades de Hola. Usar preguntas de hello debajo toohelp que diseñar la solución de identidad híbrida mientras teniendo en cuenta cómo se van directivas aplica tooreact tooan en curso incidente:

* ¿Su empresa tiene directivas en lugar tooblock los usuarios tener acceso a la red de Hola si es necesario?
  * En caso afirmativo, ¿Hola actual solución se integra con sistema de administración de identidad híbrida de Hola que son tooadopt continuo?
* ¿La compañía necesita acceso condicional tooenforce para los usuarios que están en cuarentena? 

> [!NOTE]
> Hacer notas de tootake seguro de cada respuesta y entender el razonamiento de hello detrás de respuesta de Hola. [Definir la estrategia de protección de datos](active-directory-hybrid-identity-design-considerations-data-protection-strategy.md) irá Hola opciones disponibles y las ventajas y desventajas de cada opción.  Las respuestas que obtenga partir de estas preguntas le servirán para seleccionar la opción que mejor se adapte a sus necesidades empresariales.
> 
> 

## <a name="next-steps"></a>Pasos siguientes
[Definición de la estrategia de protección de datos](active-directory-hybrid-identity-design-considerations-data-protection-strategy.md)

## <a name="see-also"></a>Otras referencias
[Información general sobre las consideraciones de diseño](active-directory-hybrid-identity-design-considerations-overview.md)

