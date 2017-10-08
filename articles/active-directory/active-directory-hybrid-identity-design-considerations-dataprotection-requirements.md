---
title: "Consideraciones de diseño de identidad de aaaAzure Active Directory híbrida - determinar los requisitos de protección de datos | Documentos de Microsoft"
description: "Cuando planifique la solución de identidad híbrida, identificar los requisitos de protección de datos de Hola para su empresa y qué opciones están disponible toobest cumplan estos requisitos."
documentationcenter: 
services: active-directory
author: billmath
manager: femila
editor: 
ms.assetid: 40dc4baa-fe82-4ab6-a3e4-f36fa9dcd0df
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/18/2017
ms.author: billmath
ms.openlocfilehash: 189abf9affbc2894c322f362d84222d4e33d472e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="plan-for-enhancing-data-security-through-strong-identity-solution"></a>Plan para mejorar la seguridad de los datos mediante una solución de identidad sólida
Hola primer paso tooprotect Hola datos están identificar quién puede tener acceso a esos datos y como parte de este proceso es necesario toohave una solución de identidad que se integra con sus capacidades de autenticación y autorización de tooprovide de sistema. Con frecuencia la autenticación y la autorización se confunden y no se comprende bien su función. En realidad son muy diferentes, como se muestra en la siguiente ilustración de hello:

![](./media/hybrid-id-design-considerations/mobile-devicemgt-lifecycle.png)

**Fases del ciclo de vida de administración de dispositivos móviles**

Al planear la solución de identidad híbrida debe entender requisitos de protección de datos de Hola para su empresa y qué opciones están disponible toobest cumplan estos requisitos.

> [!NOTE]
> Después de finalizar la planeación de seguridad de los datos, revise [determinar los requisitos de la autenticación multifactor](active-directory-hybrid-identity-design-considerations-multifactor-auth-requirements.md) tooensure que las selecciones realizadas con respecto a los requisitos de la autenticación multifactor no resultaron afectadas por las decisiones de Hola que haya realizado en esta sección.
> 
> 

## <a name="determine-data-protection-requirements"></a>Determinación de los requisitos de protección de datos
En edad Hola de movilidad, mayoría de las empresas tiene un objetivo común: habilitar su toobe de los usuarios más productivo en sus dispositivos móviles al local o de forma remota desde cualquier parte en la productividad de tooincrease del orden. Aunque esto podría ser un objetivo común, las compañías que tienen este requisito también será preocupación con respecto a la cantidad de Hola de amenazas que se deben mitigar en datos de la compañía de orden tookeep seguros y mantendrán la privacidad del usuario. Cada compañía puede tener requisitos diferentes en este sentido; las reglas de cumplimiento diferentes variarán empresa de Hola de sector toowhich correspondiente está actuando will provocar toodifferent decisiones de diseño. 

Sin embargo, hay algunos aspectos de seguridad que se deben explorar y validar, independientemente del sector de hello, que se explican en la sección siguiente Hola.

## <a name="data-protection-paths"></a>Rutas de protección de datos
![](./media/hybrid-id-design-considerations/data-protection-paths.png)

**Rutas de protección de datos**

Hola diagrama anterior, el componente de identidad de hello estará hello primero toobe comprobado antes de que se tiene acceso a datos. Sin embargo, estos datos pueden ser en diferentes estados durante el tiempo de Hola que se obtuvo acceso. Cada número de este diagrama representa una ruta en la que se pueden encontrar los datos en algún momento en el tiempo. Estos números se explican a continuación:

1. Protección de datos en el nivel de dispositivo de Hola.
2. Protección de datos en tránsito.
3. Protección de datos en reposo en el entorno local.
4. Protección de datos mientras están en reposo en la nube de Hola.

Aunque la solución de identidad híbrida de hello directamente no ofrece controles técnicos Hola que permiten TI tooprotect Hola propios datos en cada una de estas fases, es necesario que la solución de identidad híbrida de hello es capaz de aprovechando tanto de forma local y usuario hello tooidentify de recursos de administración de identidad antes de conceder acceso a los datos toohello en la nube. Cuando planifique la solución de identidad híbrida asegurarse de esa Hola después se responden preguntas según los requisitos de la organización tooyour:

## <a name="data-protection-at-rest"></a>Protección de datos en reposo
Independientemente de donde hello datos en reposo (dispositivo, en la nube o local), es importante tooperform una organización de evaluación toounderstand Hola necesita en este sentido. Para esta área, asegúrese de que le pide que Hola siguientes preguntas:

* ¿La compañía necesita tooprotect datos en reposo?
  * ¿Si es así, es Hola híbrida identidad solución capaz de toointegrate con la infraestructura local actual?
  * ¿Si es así, es Hola híbrida identidad solución capaz de toointegrate con las cargas de trabajo que se encuentra en la nube de hello?
* ¿Es credenciales del usuario de hello en la nube identity management tooprotect capaz de Hola y otros datos almacenados en la nube de hello?

## <a name="data-protection-in-transit"></a>Protección de datos en tránsito
Se deben proteger los datos en tránsito entre el dispositivo de Hola y Hola centro de datos o entre dispositivos de Hola y de nube de Hola. Sin embargo, estar en tránsito no significa necesariamente que el proceso de comunicaciones con un componente se produzca fuera del servicio en la nube; también se mueve internamente, por ejemplo, entre dos redes virtuales. Para esta área, asegúrese de que le pide que Hola siguientes preguntas:

* ¿La compañía necesita tooprotect datos en tránsito?
  * ¿Si es así, es Hola híbrida identidad solución capaz de toointegrate con controles seguros, como SSL/TLS?
* ¿Administración de identidades de nube de hello mantener Hola tráfico tooand en almacén de directorio de hello (dentro y entre los centros de datos) firmado?

## <a name="compliance"></a>Cumplimiento normativo
Normas, leyes y los requisitos de cumplimiento de normas variará sector toohello correspondiente que pertenece su empresa. Las empresas en industrias reguladas alta deben resolver problemas de administración de identidades preocupaciones relacionadas toocompliance. Normas como Sarbanes-Oxley (SOX), Health Insurance Portability hello y Accountability Act (HIPPA) Hola Gramm-Leach-Bliley Act (GLBA) y Hola tarjeta sector datos estándar de seguridad pago (PCI DSS) son muy estrictos con respecto a la extensión identity and access. solución de identidad híbrida de Hola que adopte la empresa debe tener capacidades básicas de Hola que cumplirán los requisitos de Hola de una o varias de estas normas. Para esta área, asegúrese de que le pide que Hola siguientes preguntas:

* ¿Es la solución de identidad híbrida de hello cumple los requisitos de regulación de Hola para su empresa?
* ¿Solución de identidad híbrida hace Hola ha generado en funciones que permiten a los requisitos de regulación de empresa toobe conforme? 

> [!NOTE]
> Hacer notas de tootake seguro de cada respuesta y entender el razonamiento de hello detrás de respuesta de Hola. [Definir la estrategia de protección de datos](active-directory-hybrid-identity-design-considerations-data-protection-strategy.md) irá Hola opciones disponibles y las ventajas y desventajas de cada opción.  Las respuestas que obtenga partir de estas preguntas le servirán para seleccionar la opción que mejor se adapte a sus necesidades empresariales.
> 
> 

## <a name="next-steps"></a>Pasos siguientes
 [Determinación de los requisitos de administración de contenido](active-directory-hybrid-identity-design-considerations-contentmgt-requirements.md)

## <a name="see-also"></a>Otras referencias
[Información general sobre las consideraciones de diseño](active-directory-hybrid-identity-design-considerations-overview.md)

