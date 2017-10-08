---
title: eventos de riesgo de Active Directory aaaAzure | Documentos de Microsoft
description: "En este tema se explica detalladamente qué son los eventos de riesgo."
services: active-directory
keywords: azure active directory identity protection, seguridad, riesgo, nivel de riesgo, vulnerabilidad, directiva de seguridad
author: MarkusVi
manager: femila
ms.assetid: fa2c8b51-d43d-4349-8308-97e87665400b
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/15/2017
ms.author: markvi
ms.reviewer: dhanyahk
ms.openlocfilehash: d771c1f43707744aac728c4f72000d855cbd6e1d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-risk-events"></a>Eventos de riesgo de Azure Active Directory

mayoría de Hola de toman las infracciones de seguridad colocar cuando los atacantes tuvieran el entorno de acceso tooan por robo de identidad de un usuario. Descubrir las identidades en peligro no es tarea fácil. Azure Active Directory utiliza algoritmos y heurística acciones sospechosas toodetect que son cuentas de usuario de tooyour relacionados de aprendizaje de automático adaptable. Cada acción sospechosa detectada se almacena en un registro denominado *evento de riesgo*.

En la actualidad, Azure Active Directory detecta seis tipos de eventos de riesgo:

- [Usuarios con credenciales perdidas](#leaked-credentials) 
- [Inicios de sesión desde direcciones IP anónimas](#sign-ins-from-anonymous-ip-addresses) 
- [Viaje imposible tooatypical ubicaciones](#impossible-travel-to-atypical-locations) 
- [Inicios de sesión desde ubicaciones desconocidas](#sign-in-from-unfamiliar-locations)
- [Inicios de sesión desde dispositivos infectados](#sign-ins-from-infected-devices) 
- [Inicios de sesión desde direcciones IP con actividad sospechosa](#sign-ins-from-ip-addresses-with-suspicious-activity) 


![Evento de riesgo](./media/active-directory-reporting-risk-events/91.png)

Este tema proporciona también una descripción detallada de los eventos de riesgo son y cómo puede usarlos tooprotect las identidades de Azure AD.


## <a name="risk-event-types"></a>Tipo de evento de riesgo

propiedad de tipo de evento de riesgo de Hello es que un identificador para la acción sospechosa Hola un registro de eventos de riesgo se ha creado para.  
Crear las inversiones en continuo en el proceso de detección de Hola de Microsoft:

- Precisión de la detección de toohello mejoras de eventos de riesgo existentes 
- Nuevos tipos de eventos de riesgo que se agregarán en hello futuras

### <a name="leaked-credentials"></a>Credenciales con fugas

Si ciberdelincuentes poner en peligro las contraseñas válidas de los usuarios legítimos, delincuentes Hola compartirán a menudo esas credenciales. Esto se suele hacer publicándolas públicamente en sitios web o pegar oscuros del Hola o comerciales o las credenciales de hello en el mercado negro de Hola de venta. Microsoft Hello filtren las credenciales de servicio adquiere el nombre de usuario / contraseña pares mediante la supervisión de sitios web públicos y oscuro y el trabajo con:

- Investigadores
- Autoridades judiciales
- Equipos de seguridad de Microsoft
- Otros orígenes de confianza 

Si el servicio de Hola adquiere username / pares de contraseña, se comprueban con credenciales válidas actual de los usuarios de AAD. Cuando se encuentra una coincidencia, significa que la contraseña de un usuario está en peligro y se crea un *evento de riesgo de credenciales filtradas*.

### <a name="sign-ins-from-anonymous-ip-addresses"></a>Inicios de sesión desde direcciones IP anónimas

Este tipo de evento de riesgo identifica los usuarios que han iniciado sesión correctamente desde una dirección IP que se ha identificado como una dirección IP de proxy anónima. Estos servidores proxy son la utilizan los usuarios que quieran toohide dirección IP de su dispositivo y puede utilizarse de forma malintencionada.


### <a name="impossible-travel-tooatypical-locations"></a>Viaje imposible tooatypical ubicaciones

Este tipo de evento de riesgo identifica dos inicios de sesión que se originan desde ubicaciones distantes geográficamente, donde al menos una de las ubicaciones de hello también se pueden inusual para el usuario de hello, tiene más allá de comportamiento. Además, el tiempo de hello entre Hola dos inicios de sesión es menor que tiempo Hola Hola usuario tootravel de hello primera ubicación toohello le hubiera llevado segundo, que indica que está usando otro usuario Hola mismo credenciales. 

Este algoritmo de aprendizaje de máquina que no distingue entre obvio "*falsos positivos*" que han contribuido toohello viaje imposible condición, como las redes privadas virtuales y las ubicaciones que se usen con frecuencia otros usuarios de la organización de Hola.  sistema de Hello tiene un período de aprendizaje inicial de 14 días durante el cual aprende el comportamiento de inicio de sesión de un usuario nuevo.

### <a name="sign-in-from-unfamiliar-locations"></a>Inicio de sesión desde ubicaciones desconocidas

Este tipo de evento de riesgo se considera más allá de las ubicaciones de inicio de sesión (IP, latitud y longitud y ASN) toodetermine nuevo / familiarizado ubicaciones. sistema de Hello almacena información acerca de las ubicaciones anteriores utilizados por un usuario y considera que estas ubicaciones "conocidas". eventos de riesgo de Hola se desencadenan al inicio de sesión de Hola se produce desde una ubicación que no esté ya en la lista de Hola de ubicaciones conocidas. sistema de Hello tiene un período de aprendizaje inicial de 30 días, durante el cual no marca las nuevas ubicaciones como ubicaciones desconocidas. sistema de Hello también omite los inicios de sesión desde dispositivos conocidos y ubicaciones geográficamente cierre tooa familiarizado ubicación. 

### <a name="sign-ins-from-infected-devices"></a>Inicios de sesión desde dispositivos infectados

Este tipo de evento de riesgo identifica inicios de sesión desde dispositivos infectados con malware, que se conocen tooactively comunicarse con un servidor bot. Esto se determina mediante la correlación de direcciones IP de dispositivo del usuario de hello contra las direcciones IP que estuvieron en contacto con un servidor bot. 

### <a name="sign-ins-from-ip-addresses-with-suspicious-activity"></a>Inicios de sesión desde direcciones IP con actividad sospechosa
Este tipo de evento de riesgo identifica las direcciones IP desde las que se ha producido un gran número de intentos fallidos de inicio de sesión, en varias cuentas de usuario, durante un corto período de tiempo. Esto coincide con los patrones de tráfico de direcciones IP usadas por los atacantes y es un claro indicador de que las cuentas ya están bien o son toobe puesto en peligro. Se trata de un algoritmo de aprendizaje de máquina que no distingue entre obvio "*falsos positivos*", como direcciones IP que se usen con frecuencia otros usuarios de la organización de Hola.  sistema de Hello tiene un período de aprendizaje inicial de 14 días donde aprende Hola inicio de sesión de comportamiento de un nuevo usuario y el nuevo inquilino.


## <a name="detection-type"></a>Tipo de detección

propiedad de tipo de detección de Hello es un indicador (en tiempo real o sin conexión) para el período de tiempo de detección de Hola de un evento de riesgo.  
Actualmente, la mayoría de los eventos de riesgo se detectan sin conexión en una operación posterior al procesamiento después de que se ha producido el evento de riesgo de Hola.

Hello en la tabla siguiente muestra la cantidad de Hola de tiempo que tarda un tooshow del tipo de detección en un informe relacionado:

| Tipo de detección | Informes de latencia |
| --- | --- |
| Tiempo real | too10 5 minutos |
| Sin conexión | too4 2 horas |


Para los tipos de eventos de riesgo de hello que Azure Active Directory detecta, tipos de detección de hello son:

| Tipo de evento de riesgo | Tipo de detección |
| :-- | --- | 
| [Usuarios con credenciales perdidas](#leaked-credentials) | Sin conexión |
| [Inicios de sesión desde direcciones IP anónimas](#sign-ins-from-anonymous-ip-addresses) | Tiempo real |
| [Viaje imposible tooatypical ubicaciones](#impossible-travel-to-atypical-locations) | Sin conexión |
| [Inicios de sesión desde ubicaciones desconocidas](#sign-in-from-unfamiliar-locations) | Tiempo real |
| [Inicios de sesión desde dispositivos infectados](#sign-ins-from-infected-devices) | Sin conexión |
| [Inicios de sesión desde direcciones IP con actividad sospechosa](#sign-ins-from-ip-addresses-with-suspicious-activity) | Sin conexión|


## <a name="risk-level"></a>Nivel de riesgo

propiedad de nivel de riesgo de Hola de un evento de riesgo es un indicador (alto, medio o bajo) para la gravedad de Hola y confianza Hola de un evento de riesgo. Esta propiedad le ayuda a acciones de hello tooprioritize que debe realizar. 

gravedad de Hola de evento de riesgo de hello representa la importancia de Hola de señal de Hola como un predictor de riesgo de identidad.  
confianza de Hello es un indicador con posibilidad de Hola de falsos positivos. 

Por ejemplo, 

* **Alto**: evento de riesgo de gravedad alta y de alta confianza. Estos eventos son buenos indicadores que se ha puesto en peligro la identidad del usuario de Hola y las cuentas de usuario afectadas deben corregirse inmediatamente.

* **Medio**: evento de riesgo de gravedad alta, pero confianza inferior, o viceversa. Estos eventos son potencialmente peligrosos y las cuentas de usuario afectadas deben corregirse.

* **Bajo**: evento de riesgo de baja confianza y gravedad baja. Este evento no puede requerir una acción inmediata, pero cuando se combina con otros eventos de riesgo, puede proporcionar una indicación clara que Hola identidad está en peligro.

![Nivel de riesgo](./media/active-directory-reporting-risk-events/01.png)

### <a name="leaked-credentials"></a>Credenciales con fugas

Filtren las credenciales de eventos de riesgo se clasifican como un **alta**, ya que proporcionan una indicación clara que Hola nombre de usuario y la contraseña son atacante tooan disponible.

### <a name="sign-ins-from-anonymous-ip-addresses"></a>Inicios de sesión desde direcciones IP anónimas

es el nivel de riesgo de Hola para este tipo de evento de riesgo **medio** porque una dirección IP anónima no es una indicación clara de un ataque de cuenta.  
Se recomienda que se inmediatamente en contacto con hello usuario tooverify si estaban usando direcciones IP anónimas.


### <a name="impossible-travel-tooatypical-locations"></a>Viaje imposible tooatypical ubicaciones

Viaje imposible suele ser un buen indicador de que un hacker fue capaz de toosuccessfully sesión. Sin embargo, los falsos positivos pueden producirse cuando un usuario viaja con un dispositivo nuevo o con una VPN que normalmente no se utiliza por otros usuarios de la organización de Hola. Otra fuente de falsos positivos es aplicaciones que pasan incorrectamente direcciones IP de servidor como direcciones IP, que puede dar el aspecto de Hola de cliente de inicios de sesión se hospeda teniendo lugar desde el centro de datos de hello en esa aplicación del back-end (a menudo son los centros de datos de Microsoft que puede dar el aspecto de Hola de inicios de sesión tiene lugar de Microsoft propiedad direcciones IP). Como resultado de estos falsos positivos, es el nivel de riesgo de Hola para este evento de riesgo **medio**.

> [!TIP]
> Puede reducir cantidad de Hola de false-positves notificado para este tipo de evento de riesgo mediante la configuración de [ubicaciones con nombre](active-directory-named-locations.md). 

### <a name="sign-in-from-unfamiliar-locations"></a>Inicio de sesión desde ubicaciones desconocidas

Ubicaciones desconocidas pueden proporcionar una indicación clara que un atacante es capaz de toouse una identidad robada. Se pueden producir falsos positivos cuando un usuario está viajando o probando un nuevo dispositivo, o bien usando una VPN nueva. Como resultado de estos falsos positivos, es el nivel de riesgo de Hola para este tipo de evento **medio**.

### <a name="sign-ins-from-infected-devices"></a>Inicios de sesión desde dispositivos infectados

Este evento de riesgo identifica las direcciones IP, no los dispositivos de usuarios. Si varios dispositivos están detrás de una única dirección IP, y solo algunos son controlados por una red de robots, inicios de sesión de otros dispositivos mi desencadenador este evento innecesariamente, que es el motivo de Hola para clasificar este evento de riesgo como **bajo**.  

Se recomienda que ponerse en contacto con el usuario de Hola y dispositivos de todos los usuarios de Hola de digitalización. También es posible que un dispositivo de usuario personal está infectado o, como se mencionó anteriormente, que otra persona estaba usando un dispositivo infectado de hello igual de direcciones IP como usuario de Hola. Dispositivos infectados a menudo están infectados con malware que todavía no ha sido identificado por el software antivirus y también pueden indicar como hábitos de usuario incorrectos que pueden haber causado Hola dispositivo toobecome infectado.

Para obtener más información acerca de cómo tooaddress infecciones de malware, vea hello [Malware Protection Center](http://go.microsoft.com/fwlink/?linkid=335773&clcid=0x409).


### <a name="sign-ins-from-ip-addresses-with-suspicious-activity"></a>Inicios de sesión desde direcciones IP con actividad sospechosa

Se recomienda ponerse en contacto con hello usuario tooverify si realmente firmados desde una dirección IP que se marcó como sospechosa. nivel de riesgo de Hola para este tipo de evento es "**medio**" porque varios dispositivos pueden estar detrás de hello misma dirección IP, mientras que sólo algunos pueden ser responsables de cualquier actividad sospechosa Hola. 


 
## <a name="next-steps"></a>Pasos siguientes

Los eventos de riesgo son foundation Hola para proteger las identidades de Azure AD. Azure AD actualmente puede detectar seis eventos de riesgo: 


| Tipo de evento de riesgo | Nivel de riesgo | Tipo de detección |
| :-- | --- | --- |
| [Usuarios con credenciales perdidas](#leaked-credentials) | Alto | Sin conexión |
| [Inicios de sesión desde direcciones IP anónimas](#sign-ins-from-anonymous-ip-addresses) | Mediano | Tiempo real |
| [Viaje imposible tooatypical ubicaciones](#impossible-travel-to-atypical-locations) | Mediano | Sin conexión |
| [Inicios de sesión desde ubicaciones desconocidas](#sign-in-from-unfamiliar-locations) | Mediano | Tiempo real |
| [Inicios de sesión desde dispositivos infectados](#sign-ins-from-infected-devices) | Bajo | Sin conexión |
| [Inicios de sesión desde direcciones IP con actividad sospechosa](#sign-ins-from-ip-addresses-with-suspicious-activity) | Mediano | Sin conexión|

¿Dónde puede encontrar Hola eventos de riesgo que se han detectado en su entorno?
Hay dos lugares donde puede revisar los eventos de riesgo informados:

 - **Informes de Azure AD**: los eventos de riesgo forman parte de los informes de seguridad de Azure AD. Para obtener más información, vea hello [a los usuarios en el informe de seguridad de riesgo](active-directory-reporting-security-user-at-risk.md) hello y [informe de seguridad de los inicios de sesión arriesgado](active-directory-reporting-security-risky-sign-ins.md).

 - **Azure AD Identity Protection**: los eventos de riesgo también forman parte de las funcionalidades de informes de [Azure Active Directory Identity Protection](active-directory-identityprotection.md).
    

Mientras que la detección de Hola de eventos de riesgo ya representa un aspecto importante de la protección de las identidades, también tiene Hola opción tooeither tratarlas manualmente o incluso implementan respuestas automatizadas mediante la configuración de directivas de acceso condicional. Para más información, consulte [Azure Active Directory Identity Protection](active-directory-identityprotection.md).
 
