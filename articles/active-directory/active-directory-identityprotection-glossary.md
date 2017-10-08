---
title: "Glosario de protección de identidad de Active Directory aaaAzure | Documentos de Microsoft"
description: Glosario de Azure Active Directory Identity Protection
services: active-directory
keywords: "azure active directory identity protection, detección de aplicaciones en la nube, administración de aplicaciones, seguridad, riesgo, nivel de riesgo, punto vulnerable, directiva de seguridad, glosario"
documentationcenter: 
author: MarkusVi
manager: femila
ms.assetid: 833119a5-33d6-4482-adda-fa35218c72c3
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: markvi
ms.reviewer: nigu
ms.openlocfilehash: ff2e96d20e2a3f1df24b78e66be5a0c6807e60a3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-identity-protection-glossary"></a>Glosario de Azure Active Directory Identity Protection
### <a name="at-risk-user"></a>En riesgo (usuario)
Usuario con uno o más eventos de riesgo activos. 

### <a name="atypical-sign-in-location"></a>Ubicación de inicio de sesión inusual
Un inicio de sesión de desde una ubicación geográfica que no es típico de usuario específico de hello, similares a los usuarios o inquilinos de Hola.

### <a name="azure-ad-identity-protection"></a>Azure AD Identity Protection
Módulo de seguridad de Azure Active Directory que proporciona una vista consolidada de los eventos de riesgo y posibles puntos vulnerables que afectan a las identidades de una organización.

### <a name="conditional-access"></a>Acceso condicional
Una directiva de protección de acceso tooresources. Reglas de acceso condicional se almacenan en hello Azure Active Directory y se evalúan por Azure AD antes de conceder acceso a recursos de toohello.  Reglas de ejemplo son la restricción de acceso según la ubicación del usuario, el estado del dispositivo o el método de autenticación de usuario.

### <a name="credentials"></a>Credenciales
Información que incluye la identificación y prueba de identificación que es usado toogain acceder a los recursos toolocal y red. Ejemplos de credenciales son nombres de usuario, contraseñas, tarjetas inteligentes y certificados.

### <a name="event"></a>Evento
Registro de una actividad en Azure Active Directory.

### <a name="false-positive-risk-event"></a>Falso positivo (evento de riesgo)
Estado de evento de riesgo establecer manualmente un usuario de la protección de identidad, que indica ese evento de riesgo Hola se investigó y estaba marcado incorrectamente como un evento de riesgo.

### <a name="identity"></a>Identidad
Persona o entidad que se debe comprobar mediante autenticación, basándose en criterios como contraseñas o certificados.

### <a name="identity-risk-event"></a>Evento de riesgo de identidad
Evento de AAD marcado como anómalo por Identity Protection, que puede indicar que una identidad está en peligro.

### <a name="ignored-risk-event"></a>Omitido (evento de riesgo)
Estado de evento de riesgo establecer manualmente un usuario de la protección de identidad, que indica que ese evento de riesgo Hola se cierra sin llevar a cabo una acción de corrección.

### <a name="impossible-travel-from-atypical-locations"></a>Viaje imposible desde ubicaciones inusuales
Un evento de riesgo que se desencadena cuando dos inicios de sesión para hello mismo usuario se detectan, donde al menos uno de ellos es desde una ubicación poco frecuente en el inicio de sesión y donde hello tiempo que transcurre entre inicios de sesión de hello es más corto que Hola mínima de tiempo que tardaría toophysically viajar entre estas ubicaciones.  

### <a name="investigation"></a>Investigación
Hello proceso de revisión de las actividades de hello, los registros y otra información relevante relacionada con tooa riesgo eventos toodecide si son necesarios pasos de mitigación o corrección, comprender si y cómo identidad Hola se pone en peligro y comprender cómo Hola se usó la identidad en peligro.

### <a name="leaked-credentials"></a>Credenciales con fugas
Un evento de riesgo que se desencadena cuando se encuentran las credenciales de usuario actuales (nombre de usuario y contraseña) publicado en web oscuro de hello nuestro investigadores.

### <a name="mitigation"></a>Mitigación
Una acción toolimit o eliminar capacidad de Hola de un atacante tooexploit una identidad en peligro o un dispositivo sin estado de restauración Hola identidad o dispositivo tooa seguro. Una mitigación no resuelve los eventos de riesgo anteriores asociados con la identidad de Hola o dispositivo.

### <a name="multi-factor-authentication"></a>Multi-Factor Authentication
Un método de autenticación que requiere dos o más métodos de autenticación, que pueden incluir algo Hola usuario tiene, este tipo de certificado; un usuario de hello conoce, como nombres de usuario, contraseñas o frases de contraseña; atributos físicos, como una huella digital; y atributos personales, como una firma personal.

### <a name="offline-detection"></a>Detección sin conexión
detección de Hola de anomalías y evaluación del riesgo de Hola de un evento, como el intento de inicio de sesión después de hechos de hello, para un evento que ya se ha producido.

### <a name="policy-condition"></a>Condición de directiva
Una parte de una directiva de seguridad que define las entidades de hello (grupos, usuarios, aplicaciones, plataformas de dispositivos, Estados de los dispositivos, intervalos de IP, los tipos de cliente) incluida en la directiva de Hola o excluir de ella.

### <a name="policy-rule"></a>Regla de directiva
parte de Hola de una directiva de seguridad que describe las circunstancias de Hola que desencadenarán directiva hello y acciones de hello llevadas a cabo cuando se desencadene la directiva de Hola.

### <a name="prevention"></a>Prevención
Acción tooprevent daños toohello mediante el abuso de un dispositivo o identidad sospecha o a la organización saber toobe puesto en peligro. Una acción de prevención no protege la identidad o dispositivo de hello y no resuelve los eventos de riesgo anteriores.

### <a name="privileged-user"></a>Con privilegios (usuario)
Un usuario que en tiempo de presentación de un evento de riesgo, tooone de permisos de administrador permanentes o temporales o más recursos en Azure Active Directory, por ejemplo, un administrador Global, Administrador de facturación, Administrador de servicios, el Administrador de usuario y contraseña Administrador. 

### <a name="real-time"></a>Tiempo real
Ver Detección en tiempo real.

### <a name="real-time-detection"></a>Detección en tiempo real
la detección de anomalías de Hola y de evaluación del riesgo de Hola de un evento, como el intento de inicio de sesión antes del evento de Hola se permiten tooproceed.

### <a name="remediated-risk-event"></a>Corregido (evento de riesgo)
Estado de evento de riesgo establece automáticamente protección de identidad, que indica que ese evento de riesgo Hola fue corregido con ninguna acción de corrección estándar Hola para este tipo de evento de riesgo. Por ejemplo, cuando se restablece la contraseña de usuario de hello, se corrigen automáticamente muchos eventos de riesgo que indiquen que esa contraseña anterior Hola se pone en peligro.

### <a name="remediation"></a>Corrección
Una acción toosecure una identidad o un dispositivo que previamente se sospecha o conoce toobe en peligro. Una acción correctora restaura Hola identidad o dispositivo tooa seguro estado y resuelve los eventos de riesgo anteriores asociados con la identidad de Hola o dispositivo.

### <a name="resolved-risk-event"></a>Resuelto (evento de riesgo)
Establecer manualmente un usuario de la protección de identidad, que indica que una acción de corrección adecuado fuera Identity Protection había realizada por usuario de Hola y ese evento de riesgo Hola debe tenerse en cuenta un estado de evento de riesgo cerrado.

### <a name="risk-event-status"></a>Estado de evento de riesgo
Una propiedad de un evento de riesgo, que indica si el evento de hello está activo y, si cierra, motivo de Hola para cerrarla.

### <a name="risk-event-type"></a>Tipo de evento de riesgo
Una categoría para hello el riesgo de evento, que indica el tipo de saludo de anomalías que produjo Hola eventos toobe arriesgado.

### <a name="risk-level-risk-event"></a>Nivel de riesgo (evento de riesgo)
Una indicación (alto, medio o bajo) de gravedad de Hola de los usuarios la protección de la identidad de hello riesgo eventos toohelp dé prioridad a acciones de Hola que tomar organización tootheir de tooreduce Hola riesgo. 

### <a name="risk-level-sign-in"></a>Nivel de riesgo (inicio de sesión)
Una indicación (alto, medio o bajo) de probabilidad de Hola que para un específico inicio de sesión, otra persona está intentando toouse Hola identidad de usuario.

### <a name="risk-level-user-compromise"></a>Nivel de riesgo (compromiso de usuario)
Una indicación (alto, medio o bajo) de probabilidad de Hola que se ha puesto en peligro una identidad.

### <a name="risk-level-vulnerability"></a>Nivel de riesgo (vulnerabilidad)
Una indicación (alto, medio o bajo) de gravedad de Hola de usuarios de protección de la identidad de hello vulnerabilidad toohelp dé prioridad a acciones de Hola que tomar organización tootheir de tooreduce Hola riesgo.

### <a name="secure-identity"></a>Proteger (identidad)
Corrección de actuar como un cambio de contraseña o una máquina restablecer toorestore un estado de tooan sin problemas de identidad potencialmente comprometidos.

### <a name="security-policy"></a>Directiva de seguridad
Recopilación de reglas y condiciones de una directiva. Una directiva puede tener aplicado tooentities como usuarios, grupos, aplicaciones, dispositivos, plataformas de dispositivos, Estados de los dispositivos, intervalos de IP y los tipos de cliente Auth2.0. Cuando una directiva está habilitada, se evalúa cada vez que una entidad que se incluye en la directiva de hello emite un token para un recurso.

### <a name="sign-in-v"></a>Iniciar sesión
identidad de tooan tooauthenticate en Azure Active Directory.

### <a name="sign-in-n"></a>Inicio de sesión
proceso de Hola o acción de autenticar una identidad en Active Directory de Azure y eventos de Hola que esta operación de captura.

### <a name="sign-in-from-anonymous-ip-address"></a>Inicio de sesión desde dirección IP anónima
Evento de riesgo que se desencadena después de un inicio de sesión correcto desde una dirección IP identificada como una dirección IP de proxy anónima.

### <a name="sign-in-from-infected-device"></a>Inicio de sesión desde dispositivo infectado
Un evento de riesgo que se desencadena cuando un inicio de sesión de se origina desde una dirección IP conocida toobe utilizado por uno o varios dispositivos en peligro, que están intentando activamente toocommunicate con un servidor bot.

### <a name="sign-in-from-ip-address-with-suspicious-activity"></a>Inicio de sesión desde dirección IP con actividad sospechosa
Evento de riesgo que se desencadena después de un inicio de sesión correcto desde una dirección IP con un gran número de intentos de inicios de sesión erróneos entre varias cuentas de usuario durante un corto período de tiempo.

### <a name="sign-in-from-unfamiliar-location"></a>Inicio de sesión desde ubicación desconocida
Evento de riesgo que se desencadena cuando un usuario inicia sesión correctamente desde una nueva ubicación (IP, latitud/longitud y aviso de envío por adelantado).

### <a name="sign-in-risk"></a>Riesgo de inicio de sesión
Ver Nivel de riesgo (inicio de sesión)

### <a name="sign-in-risk-policy"></a>Directiva de riesgo de inicio de sesión
Una directiva de acceso condicional que evalúa Hola riesgo tooa inicio de sesión en concreta y se aplica a las mitigaciones según las reglas y condiciones predefinidas.

### <a name="user-compromise-risk"></a>Riesgo de compromiso de usuario
Ver Nivel de riesgo (compromiso de usuario).

### <a name="user-risk"></a>Riesgo de usuario
Ver Nivel de riesgo (compromiso de usuario).

### <a name="user-risk-policy"></a>Directiva de riesgo de usuario
Una directiva de acceso condicional que tiene en cuenta en el inicio de sesión de Hola y aplica las mitigaciones según las reglas y condiciones predefinidas.

### <a name="users-flagged-for-risk"></a>Usuarios marcados con riesgo
Usuarios con eventos de riesgo activos o corregidos.

### <a name="vulnerability"></a>Punto vulnerable
Una configuración o una condición en Azure Active Directory, lo que hace tooexploits susceptible de directorio de Hola o las amenazas.

## <a name="see-also"></a>Otras referencias
* [Azure Active Directory Identity Protection](active-directory-identityprotection.md)

