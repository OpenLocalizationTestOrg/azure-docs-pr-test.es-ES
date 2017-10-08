---
title: Active Directory Identity Protection aaaAzure | Documentos de Microsoft
description: "Obtenga información acerca de cómo Azure AD Identity Protection permite capacidad de hello toolimit de un tooexploit atacante una identidad en peligro o el dispositivo y toosecure una identidad o un dispositivo que era toobe sospechosa o conocido en peligro."
services: active-directory
keywords: "azure active directory identity protection, detección de aplicaciones en la nube, administración de aplicaciones, seguridad, riesgo, nivel de riesgo, punto vulnerable, directiva de seguridad"
documentationcenter: 
author: MarkusVi
manager: femila
ms.assetid: e7434eeb-4e98-4b6b-a895-b5598a6cccf1
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/15/2017
ms.author: markvi
ms.reviewer: nigu
ms.openlocfilehash: ecca4f3cdb65585687cf44a80024f26c7cab22ca
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-identity-protection"></a>Azure Active Directory Identity Protection

Azure Active Directory Identity Protection es una característica de edición de hello Azure AD Premium P2 que le permite:

- Detectar posibles vulnerabilidades que afectan a las identidades de la organización

- Configurar respuestas automatizadas toodetected sospechosa acciones de identidades de la organización de tooyour relacionados  

- Investigar incidentes sospechosos y tome las medidas adecuadas tooresolve ellos   


## <a name="getting-started"></a>Introducción

Microsoft protege identidades basadas en la nube desde hace más de una década. Con Azure Active Directory Identity Protection, en su entorno, puede usar Hola mismos sistemas de protección Microsoft utiliza identidades toosecure.

mayoría de Hola de toman las infracciones de seguridad colocar cuando los atacantes tuvieran el entorno de acceso tooan por robo de identidad de un usuario. En años de hello, los atacantes han convertido en cada vez más eficaces para aprovechar las infracciones de otros fabricantes y usen ataques de phishing sofisticadas. En cuanto un atacante obtiene acceso a las cuentas de usuario con pocos privilegios tooeven, es relativamente fácil para ellos toogain acceder a los recursos de empresa de tooimportant a través de un movimiento lateral.

Como consecuencia de esto, debe:

- Proteger todas las identidades independientemente de su nivel de privilegios

- Evitar de forma proactiva que se haga mal uso de las identidades que están en peligro.

Descubrir las identidades en peligro no es tarea fácil. Azure Active Directory utiliza algoritmos de aprendizaje automático adaptable y las anomalías de toodetect heurística e incidentes sospechosos que indican potencialmente en riesgo identidades. Con estos datos, Identity Protection genera informes y alertas que permiten tooevaluate Hola detectan problemas y toman mitigación adecuada o acciones correctoras.

Azure Active Directory Identity Protection es más que una herramienta de supervisión e informes. tooprotect las identidades de su organización, puede configurar las directivas basadas en el riesgo que responden automáticamente toodetected problemas cuando se ha alcanzado un nivel de riesgo especificado. Estas directivas además tooother condicional tener acceso a controles proporcionados por Azure Active Directory y EMS, puede bloquear de forma automática o iniciar acciones de corrección adaptable entre ellos los restablecimientos de contraseña y la aplicación de la autenticación multifactor.


#### <a name="identity-protection-capabilities"></a>Funcionalidades de Identity Protection

**Detección de vulnerabilidades y cuentas peligrosas:**  

* Proporcionar recomendaciones personalizadas tooimprove condiciones globales de seguridad resaltando las vulnerabilidades
* Cálculo de los niveles de riesgo de inicio de sesión
* Calcular los niveles de riesgo del usuario


**Investigación de los eventos de riesgo:**

* Enviar notificaciones de los eventos de riesgo
* Investigar los eventos de riesgo con información pertinente y contextual
* Proporcionar flujos de trabajo básicos de las investigaciones de tootrack
* Proporciona un acceso sencillo tooremediation acciones como el restablecimiento de contraseña

**Directivas de acceso condicional basadas en riesgos:**

* Directiva toomitigate arriesgados inicios de sesión bloqueando inicios de sesión o solicitando retos de la autenticación multifactor.
* Directiva tooblock o cuentas de usuario de riesgo segura
* Directiva toorequire usuarios tooregister para la autenticación multifactor



## <a name="identity-protection-roles"></a>Roles de Identity Protection

actividades de administración de tooload saldo Hola alrededor de su implementación de protección de identidad, puede asignar varios roles. Azure AD Identity Protection admite tres roles de directorio:

| Rol                         | Puede hacer                          | No puede hacer
| :--                          | ---                                |  ---   |
| Administrador global         | Acceso completo tooIdentity protección, incorporar Identity Protection| |
| Administrador de seguridad       | TooIdentity protección de acceso completo | Incorporar Identity Protection, restablecer contraseñas para un usuario |
| Lector de seguridad              | Protección del acceso de solo tooIdentity | Incorporar Identity Protection, remediar usuarios, configurar directivas, restablecer contraseñas |




Para obtener más detalles, consulte [Asignación de roles de administrador en Azure Active Directory](active-directory-assign-admin-roles-azure-portal.md)



## <a name="detection"></a>Detección

### <a name="vulnerabilities"></a>Puntos vulnerables

Azure Active Directory Identity Protection analiza la configuración y detecta las vulnerabilidades que pueden afectar a las identidades de usuario. Para conocer más detalles, consulte [Vulnerabilidades detectadas por Azure Active Directory Identity Protection](active-directory-identityprotection-vulnerabilities.md).

### <a name="risk-events"></a>Eventos de riesgo

Azure Active Directory utiliza algoritmos y heurística toodetect sospechosas acciones identidades del usuario tooyour relacionados de aprendizaje de automático adaptable. sistema de Hello crea un registro para cada acción sospechosa detectada. Estos registros se conocen también como eventos de riesgo.  
Para más información, consulte [Azure Active Directory risk events](active-directory-identity-protection-risk-events.md) (Eventos de riesgo de Azure Active Directory).


## <a name="investigation"></a>Investigación
Su viaje a través de la protección de identidad suele iniciarse con el panel de la protección de la identidad de Hola.

![Corrección](./media/active-directory-identityprotection/1000.png "Corrección")

panel de Hello le da acceso a:

* Informes como **Usuarios marcados en riesgo**, **Eventos de riesgo** y **Vulnerabilidades**.
* Configuración como la configuración de Hola de su **las directivas de seguridad**, **notificaciones** y **el registro de la autenticación multifactor**

Normalmente es el punto de partida para la investigación, que es el proceso de Hola de revisión de las actividades de hello, los registros y otra información relevante relacionado tooa el riesgo de evento toodecide si son necesarios pasos de mitigación o corrección, y la identidad de hello era en peligro y entender cómo hello en peligro la identidad se usó.

Se puede asociar su toohello de actividades de investigación [notificaciones](active-directory-identityprotection-notifications.md) protección de Azure Active Directory envía por correo electrónico.

Hello las secciones siguientes proporcionan más detalles y pasos de hello investigación tooan relacionados.  


## <a name="risky-sign-ins"></a>Inicios de sesión no seguros

Azure Active Directory detecta [tipos de eventos de riesgo](active-directory-reporting-risk-events.md#risk-event-types) en tiempo real y sin conexión. Cada evento de riesgo que se ha detectado para un inicio de sesión de un usuario contribuye tooa concepto lógico que se denomina sesión arriesgado. Un inicio de sesión de riesgo es un indicador de un intento de inicio de sesión que no es posible que se han realizado por propietario legítimo de Hola de una cuenta de usuario.


### <a name="sign-in-risk-level"></a>Nivel de riesgo del inicio de sesión

Un nivel de riesgo de inicio de sesión es una indicación (alto, medio o bajo) de probabilidad de Hola que no ha realizado un intento de inicio de sesión propietario legítimo de Hola de una cuenta de usuario.

### <a name="mitigating-sign-in-risk-events"></a>Mitigación de eventos de riesgo de inicio de sesión

Una mitigación es una capacidad de Hola de toolimit de acción de un atacante tooexploit una identidad en peligro o un dispositivo sin estado de restauración Hola identidad o dispositivo tooa seguro. Una mitigación no resuelve los eventos de inicio de sesión en riesgo anteriores asociados con la identidad de Hola o dispositivo.

inicios de sesión de riesgo toomitigate automáticamente, puede configurar policicies de seguridad de inicio de sesión en riesgo. Mediante estas directivas, considere la posibilidad de nivel de riesgo de saludo del usuario de Hola u Hola inicio de sesión tooblock de riesgo de inicios de sesión o requerir Hola usuario tooperform la autenticación multifactor. Estas acciones pueden evitar que un atacante use un daño toocause de robo de identidad y pueden provocar alguna identidad de hello toosecure de tiempo.

### <a name="sign-in-risk-security-policy"></a>Directiva de seguridad de riesgo de inicio de sesión
Una directiva de inicio de sesión riesgo es una directiva de acceso condicional que evalúa Hola riesgo tooa inicio de sesión en concreta y se aplica a las mitigaciones según las reglas y condiciones predefinidas.

![Directiva de riesgo de inicio de sesión](./media/active-directory-identityprotection/1014.png "Directiva de riesgo de inicio de sesión")

Azure AD Identity Protection ayuda a administrar mitigación Hola de riesgo de inicios de sesión por lo que le permite:

* Establecer Hola usuarios y grupos Hola la directiva se aplica a:

    ![Directiva de riesgo de inicio de sesión](./media/active-directory-identityprotection/1015.png "Directiva de riesgo de inicio de sesión")
* Establezca Hola riesgo de inicio de sesión de nivel umbral (bajo, medio o alto) que desencadena la directiva de hello:

    ![Directiva de riesgo de inicio de sesión](./media/active-directory-identityprotection/1016.png "Directiva de riesgo de inicio de sesión")
* Conjunto Hola controles toobe aplicado cuando la directiva de hello desencadena:  

    ![Directiva de riesgo de inicio de sesión](./media/active-directory-identityprotection/1017.png "Directiva de riesgo de inicio de sesión")
* Cambiar estado de saludo de la directiva:

    ![Registro MFA](./media/active-directory-identityprotection/403.png "Registro MFA")
* Revisar y evaluar el impacto de Hola de un cambio antes de activarlo:

    ![Directiva de riesgo de inicio de sesión](./media/active-directory-identityprotection/1018.png "Directiva de riesgo de inicio de sesión")

#### <a name="what-you-need-tooknow"></a>Lo que necesita tooknow
Puede configurar una inicio de sesión riesgo seguridad Directiva toorequire la autenticación multifactor:

![Directiva de riesgo de inicio de sesión](./media/active-directory-identityprotection/1017.png "Directiva de riesgo de inicio de sesión")

Sin embargo, por seguridad, esta configuración solo funciona para los usuarios que ya se hayan registrado para la autenticación multifactor. Si no se cumple Hola condición toorequire la autenticación multifactor para un usuario que no se ha registrado para la autenticación multifactor, usuario de hello está bloqueado.

Como práctica recomendada, si desea que toorequire la autenticación multifactor para inicios de sesión riesgos, debe:

1. Habilitar hello [directiva de registro de la autenticación multifactor](#multi-factor-authentication-registration-policy) Hola afecta a los usuarios.
2. Requerir Hola afectados toologin de usuarios en una sesión no es arriesgado tooperform un registro MFA

Tras completar estos pasos, se garantiza que la autenticación multifactor sea necesaria para un inicio de sesión de riesgo.

#### <a name="best-practices"></a>Prácticas recomendadas
Elegir un **alta** umbral reduce el número de Hola de veces que una directiva se desencadena y minimiza Hola impacto toousers.  

Sin embargo, excluye **bajo** y **medio** etiquetado como inicios de sesión para el riesgo de directiva de hello, que no se puede bloquear un atacante pueda aprovechar una identidad en peligro.

Cuando la configuración de Hola directiva,

* Excluya a los usuarios que no tengan o no puedan tener la autenticación multifactor.
* Exclusión de usuarios en configuraciones regionales donde no es práctico si quiere habilitar Directiva de hello (por ejemplo, no toohelpdesk de acceso)
* Excluir los usuarios que son probable toogenerate una gran cantidad de falsos positivos (los desarrolladores, analistas de seguridad)
* Utilice un umbral **Alto** durante la puesta en servicio inicial de la directiva, o bien si debe minimizar los desafíos que ven los usuarios finales.
* Use un umbral **Bajo** si su organización requiere un mayor grado de seguridad. Seleccionar un umbral **Bajo** presenta desafíos adicionales de inicio de sesión del usuario, pero aumenta la seguridad.

Hola, valor predeterminado recomendado para la mayoría de las organizaciones es tooconfigure una regla para un **medio** umbral toostrike un equilibrio entre la facilidad de uso y seguridad.

Directiva de inicio de sesión en riesgo de Hello es:

* El tráfico del explorador tooall aplicado y usan autenticación moderna de inicios de sesión.
* Tooapplications no aplicada mediante protocolos de seguridad anteriores al deshabilitar punto de conexión de WS-Trust de hello en IDP Hola federado, por ejemplo, AD FS.

Hola **eventos de riesgo** página en la consola de protección de la identidad de hello enumera todos los eventos:

* A los que se aplicó esta directiva.
* Puede revisar la actividad hello y determinar si la acción de hello fue adecuado o no

Para obtener información general de hello relacionados con la experiencia del usuario, consulte:

* [Recuperación de inicios de sesión peligrosos](active-directory-identityprotection-flows.md#risky-sign-in-recovery)
* [Inicios de sesión peligrosos bloqueados](active-directory-identityprotection-flows.md#risky-sign-in-blocked)  
* [Experiencias de inicio de sesión con Azure AD Identity Protection](active-directory-identityprotection-flows.md)  

**cuadro de diálogo de configuración relacionados de Hola de tooopen**:

- En hello **Azure AD Identity Protection** hoja en hello **configurar** sección, haga clic en **inicio de sesión de la directiva de riesgo**.

    ![Directiva de riesgo de usuario](./media/active-directory-identityprotection/1014.png "Directiva de riesgo de usuario")



## <a name="users-flagged-for-risk"></a>Usuarios marcados con riesgo

Todos los activos [el riesgo de eventos](active-directory-identity-protection-risk-events.md) que se detectaron por Azure Active Directory para un usuario contribuyen tooa concepto lógico llamada riesgo de usuario. Un usuario marcado como en peligro es un indicador de una cuenta de usuario que puede haber estado en peligro.

![Usuarios marcados con riesgo](./media/active-directory-identityprotection/1200.png)


### <a name="user-risk-level"></a>Nivel de riesgo del usuario

Un nivel de riesgo de usuario es una indicación (alto, medio o bajo) de probabilidad de Hola que está en peligro la identidad del usuario de Hola. Se calcula basándose en eventos de riesgo de usuario de Hola que están asociados con una identidad de usuario.

Hello estado de un evento de riesgo sea **Active** o **cerrado**. Solo el riesgo de eventos que son **Active** contribuir toohello cálculo de nivel de riesgo de usuario.

nivel de riesgo de usuario de Hola se calcula mediante Hola siguientes entradas:

* Eventos de los riesgos activos que afectan a los usuarios de Hola
* Nivel de riesgo de estos eventos
* Si se ha tomado alguna acción de corrección

![Riesgos de usuario](./media/active-directory-identityprotection/1031.png "Riesgos de usuario")

Puede usar Hola usuario riesgo niveles toocreate directivas de acceso condicional que bloquear arriesgado a los usuarios iniciar sesión en, u obligarlos toosecurely cambiar su contraseña.

### <a name="closing-risk-events-manually"></a>Cierre manual de eventos de riesgo

En la mayoría de los casos, ejecutará las acciones de corrección, como eventos de cierre de riesgo de tooautomatically de restablecimiento de una contraseña segura. Sin embargo, esto no siempre es posible.  
Esto sucede, por ejemplo, hello, cuando:

* Un usuario con eventos de riesgo en estado Activo se ha eliminado.
* Una investigación revela que se ha realizar un evento de riesgo notificado por usuario legítimo Hola

Dado que los eventos de riesgo que son **Active** contribuir cálculo de riesgo de usuario toohello, es posible que tenga toomanually disminuir un nivel de riesgo al cerrar manualmente los eventos de riesgo.  
Durante el transcurso de Hola de investigación, puede elegir tootake cualquiera de estas acciones toochange Hola estado de un riesgo evento:

![Acciones](./media/active-directory-identityprotection/34.png "Acciones")

* **Resolver** : Si después de investigar un evento de riesgo, ha realizado una acción de corrección adecuado fuera de la protección de identidad y cree ese evento de riesgo Hola debe tenerse en cuenta cerrada, eventos de hello marca como resuelto. Eventos resueltos establecerá tooClosed de estado del evento del riesgo de Hola y eventos de riesgo de hello ya no tendrá en cuenta toouser riesgo.
* **Marcar como falso positivo** : en algunos casos, puede investigar un evento de riesgo y detectar que se ha marcado incorrectamente como peligroso. Puede ayudar a reducir el número de Hola de estas situaciones marcando eventos de riesgo de hello como falsos positivos. Esto le ayudará a máquina Hola clasificación de hello tooimprove de algoritmos de eventos similares en hello futuras de aprendizaje. estado de Hola de eventos de falsos positivos es demasiado**cerrado** y ya no aportará toouser riesgo.
* **Omitir** : si no se ha realizado una acción de corrección, pero desea Hola a riesgo eventos toobe quitado de la lista activa de hello, puede marcar un evento de riesgo omitir y estado de evento Hola se cerrará. Eventos omitidos no contribuyen toouser riesgo. Esta opción solo debe utilizarse en circunstancias inusuales.
* **Reactivar** -el riesgo de eventos que se cierra manualmente (eligiendo **resolver**, **falso positivo**, o **omitir**) se pueden reactivar, establecer Hola estado de evento de vuelta demasiado**Active**. Eventos de riesgo reactivados contribuyen toohello cálculo de nivel de riesgo de usuario. Los eventos de riesgo cerrados mediante una corrección (como el restablecimiento de una contraseña segura) no se pueden reactivar.

**cuadro de diálogo de configuración relacionados de Hola de tooopen**:

1. En hello **Azure AD Identity Protection** hoja, en **investigar**, haga clic en **el riesgo de eventos**.

    ![Restablecimiento manual de la contraseña](./media/active-directory-identityprotection/1002.png "Restablecimiento manual de la contraseña")
2. Hola **el riesgo de eventos** lista, haga clic en un riesgo.

    ![Restablecimiento manual de la contraseña](./media/active-directory-identityprotection/1003.png "Restablecimiento manual de la contraseña")
3. En la hoja de riesgo de hello, haga clic en un usuario.

    ![Restablecimiento manual de la contraseña](./media/active-directory-identityprotection/1004.png "Restablecimiento manual de la contraseña")

### <a name="closing-all-risk-events-for-a-user-manually"></a>Cierre manual de todos los eventos de riesgo de un usuario
En lugar de manualmente cerrar individualmente los eventos de riesgo para un usuario, Azure Active Directory Identity Protection también proporciona un método tooclose todos los eventos para un usuario con un solo clic.

![Acciones](./media/active-directory-identityprotection/2222.png "Acciones")

Al hacer clic en **descartar todos los eventos**, se cierran todos los eventos y usuario Hola afectado ya no está en peligro.

### <a name="remediating-user-risk-events"></a>Corrección de eventos de riesgo del usuario

Una solución es un toosecure de acción en peligro una identidad o un dispositivo que se sospecha o conoce toobe anteriormente. Una acción correctora restaura Hola identidad o dispositivo tooa seguro estado y resuelve los eventos de riesgo anteriores asociados con la identidad de Hola o dispositivo.

eventos de riesgo de usuario de tooremediate, hacer lo siguiente:

* Realizar manualmente una eventos de riesgo de usuario de contraseña segura restablecimiento tooremediate
* Configurar una toomitigate de directiva de seguridad de usuario riesgo o corregir automáticamente los eventos de riesgo de usuario
* Dispositivo de hello infectado recrear la imagen  

#### <a name="manual-secure-password-reset"></a>Restablecimiento manual de una contraseña segura
Para restablecer una contraseña segura es una solución eficaz para muchos eventos de riesgo y cuando se lleva a cabo, automáticamente se cierra estos eventos de riesgo y vuelve a calcular el nivel de riesgo de usuario de Hola. Puede usar Hola Identity Protection panel tooinitiate restablezca la contraseña de un usuario de riesgo.

cuadro de diálogo relacionado Hola proporciona una contraseña de tooreset de dos métodos diferentes:

**Restablecimiento de contraseñas** : seleccione esta opción **requieren Hola usuario tooreset su contraseña** tooallow Hola tooself-recuperación de usuario si Hola usuario ha registrado para la autenticación multifactor. Durante el saludo siguiente inicio de sesión de usuario, usuario de hello será toosolve requiere una autenticación multifactor correctamente desafío y la contraseña de hello toochange forzado, a continuación. Esta opción no está disponible si la cuenta de usuario de hello ya no está registrada la autenticación multifactor.

**Contraseña temporal** : seleccione esta opción **generar una contraseña temporal** tooimmediately invalidar la contraseña existente de Hola y crear una nueva contraseña temporal para el usuario de Hola. Enviar Hola nueva contraseña temporal tooan dirección de correo alternativa para el usuario de Hola o administrador del usuario toohello. Como contraseña de hello es temporal, usuario de hello será toochange solicitadas Hola contraseña para inicio de sesión.

![Directiva](./media/active-directory-identityprotection/1005.png "Directiva")

**cuadro de diálogo de configuración relacionados de Hola de tooopen**:

1. En hello **Azure AD Identity Protection** hoja, haga clic en **usuarios marcan para su riesgo**.

    ![Restablecimiento manual de la contraseña](./media/active-directory-identityprotection/1006.png "Restablecimiento manual de la contraseña")
2. En la lista Hola de usuarios, seleccione un usuario con eventos de al menos un riesgo.

    ![Restablecimiento manual de la contraseña](./media/active-directory-identityprotection/1007.png "Restablecimiento manual de la contraseña")
3. En la hoja de usuario de hello, haga clic en **de restablecimiento de contraseña**.

    ![Restablecimiento manual de la contraseña](./media/active-directory-identityprotection/1008.png "Restablecimiento manual de la contraseña")

### <a name="user-risk-security-policy"></a>Directiva de seguridad de riesgo del usuario
Una directiva de seguridad de usuario riesgo es una directiva de acceso condicional que se evalúa como usuario específico de tooa nivel de riesgo de Hola y aplica acciones de corrección y mitigación según las reglas y condiciones predefinidas.

![Directiva de riesgo de usuario](./media/active-directory-identityprotection/1009.png "Directiva de riesgo de usuario")

Azure AD Identity Protection ayuda a administrar la mitigación de Hola y corrección de los usuarios marcados para riesgo por lo que le permite:

* Establecer Hola usuarios y grupos Hola la directiva se aplica a:

    ![Directiva de riesgo de usuario](./media/active-directory-identityprotection/1010.png "Directiva de riesgo de usuario")
* Establecer Hola usuario nivel umbral de riesgo (bajo, medio o alto) que desencadena la directiva de hello:

    ![Directiva de riesgo de usuario](./media/active-directory-identityprotection/1011.png "Directiva de riesgo de usuario")
* Conjunto Hola controles toobe aplicado cuando la directiva de hello desencadena:

    ![Directiva de riesgo de usuario](./media/active-directory-identityprotection/1012.png "Directiva de riesgo de usuario")
* Cambiar estado de saludo de la directiva:

    ![Directiva de riesgo de usuario](./media/active-directory-identityprotection/403.png "Registro MFA")
* Revisar y evaluar el impacto de Hola de un cambio antes de activarlo:

    ![Directiva de riesgo de usuario](./media/active-directory-identityprotection/1013.png "Directiva de riesgo de usuario")

Elegir un **alta** umbral reduce el número de Hola de veces que una directiva se desencadena y minimiza Hola impacto toousers.
Sin embargo, excluye **bajo** y **medio** usuarios marcados para el riesgo de directiva de hello, que puede no proteger identidades o dispositivos que previamente se sospecha o conocidos toobe puesto en peligro.

Cuando la configuración de Hola directiva,

* Excluir los usuarios que son probable toogenerate una gran cantidad de falsos positivos (los desarrolladores, analistas de seguridad)
* Exclusión de usuarios en configuraciones regionales donde no es práctico si quiere habilitar Directiva de hello (por ejemplo, no toohelpdesk de acceso)
* Utilice un umbral **Alto** durante la puesta en servicio inicial de la directiva, o bien si debe minimizar los desafíos que ven los usuarios finales.
* Utilice un umbral **Bajo** si su organización requiere un mayor grado de seguridad. Seleccionar un umbral **Bajo** presenta desafíos adicionales de inicio de sesión del usuario, pero aumenta la seguridad.

Hola, valor predeterminado recomendado para la mayoría de las organizaciones es tooconfigure una regla para un **medio** umbral toostrike un equilibrio entre la facilidad de uso y seguridad.

Para obtener información general de hello relacionados con la experiencia del usuario, consulte:

* [Flujo de recuperación de cuentas en peligro](active-directory-identityprotection-flows.md#compromised-account-recovery).  
* [Flujo de cuentas en peligro bloqueadas](active-directory-identityprotection-flows.md#compromised-account-blocked).  

**cuadro de diálogo de configuración relacionados de Hola de tooopen**:

- En hello **Azure AD Identity Protection** hoja en hello **configurar** sección, haga clic en **directiva de usuario de riesgo**.

    ![Directiva de riesgo de usuario](./media/active-directory-identityprotection/1009.png "Directiva de riesgo de usuario")

### <a name="mitigating-user-risk-events"></a>Mitigación de los eventos de riesgo del usuario
Los administradores pueden configurar un usuario riesgo directiva tooblock los usuarios de seguridad al inicio de sesión en función de nivel de riesgo de Hola.

El bloqueo de un inicio de sesión:

* Evita Hola generación de nuevos eventos de riesgo de usuario para el usuario de hello afectado
* Habilita los administradores toomanually corregir los eventos de riesgo de Hola que afectan a la identidad del usuario de Hola y restaurar estado seguro tooa



## <a name="multi-factor-authentication-registration-policy"></a>Directiva de registro de la autenticación multifactor
La autenticación multifactor Azure es un método para comprobar quién es usted que requiera el uso de Hola de algo más que un nombre de usuario y una contraseña. Proporciona una segunda capa de inicios de sesión de seguridad toouser y las transacciones.  
Se recomienda requerir Azure Multi-Factor Authentication en los inicios de sesión de usuario por los siguientes motivos:

* Ofrece autenticación segura con una gama de opciones de comprobación sencillas.
* Desempeña un papel fundamental en la preparación de su organización tooprotect y recuperarse de los peligros de cuenta

![Directiva de riesgo de usuario](./media/active-directory-identityprotection/1019.png "Directiva de riesgo de usuario")

Para obtener más información, consulte [Qué es Azure Multi-Factor Authentication](../multi-factor-authentication/multi-factor-authentication.md)

Azure AD Identity Protection ayuda a administrar Hola puesta en servicio de registro de la autenticación multifactor mediante la configuración de una directiva que le permite:

* Establecer Hola usuarios y grupos Hola la directiva se aplica a:

    ![Directiva de MFA](./media/active-directory-identityprotection/1020.png "Directiva de MFA")
* Conjunto Hola controles toobe aplicado cuando la directiva de hello desencadena::  

    ![Directiva de MFA](./media/active-directory-identityprotection/1021.png "Directiva de MFA")
* Cambiar estado de saludo de la directiva:

    ![Directiva de MFA](./media/active-directory-identityprotection/403.png "Directiva de MFA")
* Ver el estado de registro de hello actual:

    ![Directiva de MFA](./media/active-directory-identityprotection/1022.png "Directiva de MFA")

Para obtener información general de hello relacionados con la experiencia del usuario, consulte:

* [Flujo de registro de autenticación multifactor](active-directory-identityprotection-flows.md#multi-factor-authentication-registration).  
* [Experiencias de inicio de sesión con Azure AD Identity Protection](active-directory-identityprotection-flows.md).  

**cuadro de diálogo de configuración relacionados de Hola de tooopen**:

- En hello **Azure AD Identity Protection** hoja en hello **configurar** sección, haga clic en **registro de la autenticación multifactor**.

    ![Directiva de MFA](./media/active-directory-identityprotection/1019.png "Directiva de MFA")

## <a name="next-steps"></a>Pasos siguientes
* [Channel 9: Azure AD and Identity Show: Identity Protection Preview (Channel 9: Presentación de Azure AD e Identity: versión preliminar de Identity Protection)](https://channel9.msdn.com/Series/Azure-AD-Identity/Azure-AD-and-Identity-Show-Identity-Protection-Preview)

* [Habilitación de Azure Active Directory Identity Protection](active-directory-identityprotection-enable.md)

* [Vulnerabilities detected by Azure Active Directory Identity Protection (Vulnerabilidades detectadas por Azure Active Directory Identity Protection)](active-directory-identityprotection-vulnerabilities.md)

* [Eventos de riesgo de Azure Active Directory](active-directory-identity-protection-risk-events.md)

* [Azure Active Directory Identity Protection notifications (Notificaciones de Azure Active Directory Identity Protection)](active-directory-identityprotection-notifications.md)

* [Azure Active Directory Identity Protection playbook (Guía de Azure Active Directory Identity Protection)](active-directory-identityprotection-playbook.md)

* [Azure Active Directory Identity Protection glossary (Glosario de Azure Active Directory Identity Protection)](active-directory-identityprotection-glossary.md)

* [Experiencias de inicio de sesión con Azure AD Identity Protection](active-directory-identityprotection-flows.md)

* [Azure Active Directory Identity Protection - cómo los usuarios de toounblock](active-directory-identityprotection-unblock-howto.md)

* [Introducción a Azure Active Directory Identity Protection y Microsoft Graph](active-directory-identityprotection-graph-getting-started.md)
