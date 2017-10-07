---
title: "Creación de informes: SSPR de Azure AD | Microsoft Docs"
description: "Creación de informes sobre eventos de autoservicio de restablecimiento de contraseña de Azure AD"
services: active-directory
keywords: 
documentationcenter: 
author: MicrosoftGuyJFlo
manager: femila
ms.reviewer: gahug
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/17/2017
ms.author: joflore
ms.custom: it-pro
ms.openlocfilehash: af65b9be1e00c2819431694a5b0064b97b9e1867
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="reporting-options-for-azure-ad-password-management"></a>Opciones de creación de informes para la administración de contraseñas de Azure AD

Tras la implementación, muchas organizaciones desean tooknow cómo o si realmente se usa SSPR. Azure AD proporciona características de los informes que le ayudarán a preguntas tooanswer con predefinidos informes y si tiene licencia correctamente, permite consultas personalizadas de toocreate.

Hello siguientes preguntas técnicas pueden resolverse mediante informes que existen en hello [portal de Azure] (https://portal.azure.com/).

> [!NOTE]
> Debe ser [un administrador global](active-directory-assign-admin-roles.md#assign-or-remove-administrator-roles) y debe darse de alta para esto toobe datos recopilados en el nombre de su organización, visitando Hola reporting tab o auditoría registra al menos una vez. Los datos de su organización no se recopilarán hasta que lo haga.

* ¿Cuántas personas se han registrado para el restablecimiento de contraseña?
* ¿Quién se ha registrado para el restablecimiento de contraseña?
* ¿Qué datos está registrando la gente?
* ¿Cuántas personas restablecieron sus contraseñas en hello últimos siete días?
* ¿Qué usuarios de métodos más comunes de Hola o administradores utilicen tooreset sus contraseñas?
* ¿Cuáles son comunes emite a los usuarios o administradores de cara al intentar restablecer la contraseña toouse?
* ¿Qué administradores restablecen sus propias contraseñas con frecuencia?
* ¿Hay alguna actividad sospechosa en relación con el restablecimiento de contraseña?

## <a name="how-tooview-password-management-reports-in-hello-azure-portal"></a>Cómo informes de administración de contraseñas de tooview de hello portal de Azure

En hello Azure experiencia del portal, tenemos una manera mejorada tooview contraseña restablecimiento y la contraseña restablecimiento de actividad de registro.  Siga estos pasos hello toofind Hola contraseña restablecimiento y la contraseña registro los eventos de restablecimiento:

1. Navegue demasiado[**portal.azure.com**](https://portal.azure.com)
2. Haga clic en hello **más servicios** menú hello Azure portal izquierdo navegación principal
3. Busque **Azure Active Directory** en Hola lista de servicios y selecciónelo
4. Haga clic en **usuarios y grupos** del menú de navegación de hello Azure Active Directory
5. Haga clic en hello **los registros de auditoría** elemento de navegación del menú de navegación de usuarios y grupos de Hola. Esto muestra todos los eventos de auditoría de hello producen en todos los usuarios de hello en el directorio. Puede filtrar esta vista toosee todos los Hola relacionadas con contraseñas eventos, también.
6. toofilter esta visualización tooonly Hola restablecimiento de contraseña eventos relacionados, haga clic en hello **filtro** situado en la parte superior de Hola de hoja de Hola.
7. De hello **filtro** menú, seleccione hello **categoría** de lista desplegable y cambiarlo toohello **administración de contraseñas de autoservicio** tipo de categoría.
8. Opcionalmente, otra lista de Hola de filtro eligiendo específicos de hello **actividad** que le interesen

## <a name="how-tooretrieve-password-management-events-from-hello-azure-ad-reports-and-events-api"></a>¿Cómo tooretrieve eventos de administración de contraseñas de hello Azure AD API de informes y eventos

Hello Azure AD API de informes y eventos admite la recuperación de toda la información de hello incluida en los informes de registro de restablecimiento de restablecimiento y la contraseña contraseña. Con esta API, puede descargar de restablecimiento de contraseña individuales y eventos de registro para la integración de restablecimiento de contraseña con hello reporting tecnología de su elección.

### <a name="how-tooget-started-with-hello-reporting-api"></a>¿Cómo tooget partió Hola API de informes

tooaccess estos datos, necesita toowrite una pequeña aplicación o script tooretrieve desde nuestros servidores. [Obtenga información acerca de cómo tooget iniciado con hello API Reporting de Azure AD](active-directory-reporting-api-getting-started.md).

Una vez que tenga una secuencia de comandos de trabajo, a continuación deberá tooexamine Hola contraseña restablecimiento y registro de eventos que se pueden recuperar toomeet los escenarios.

* [SsprActivityEvent](https://msdn.microsoft.com/library/azure/mt126081.aspx#BKMK_SsprActivityEvent): listas de columnas de hello disponibles para eventos de restablecimiento de contraseña
* [SsprRegistrationActivityEvent](https://msdn.microsoft.com/library/azure/mt126081.aspx#BKMK_SsprRegistrationActivityEvent): listas de columnas Hola disponibles para los eventos de registro de restablecimiento de contraseña

### <a name="reporting-api-data-retrieval-limitations"></a>Informes de las limitaciones de recuperación de datos de la API

Actualmente, Hola informes de Azure AD y API de eventos recupera la demasiado**75.000 eventos individuales** de hello [SsprActivityEvent](https://msdn.microsoft.com/library/azure/mt126081.aspx#BKMK_SsprActivityEvent) y [SsprRegistrationActivityEvent](https://msdn.microsoft.com/library/azure/mt126081.aspx#BKMK_SsprRegistrationActivityEvent) tipos , que abarcan hello **últimos 30 días**.

Si necesita tooretrieve o almacenar datos más allá de esta ventana, se recomienda guardar en una base de datos externa y usar deltas de Hola de tooquery Hola API que son el resultado. Nuestra recomendación es toobegin recuperar estos datos cuando comience a usar SSPR en su organización, conservar de forma externa y, a continuación, continuar deltas de hello tootrack desde este punto.

## <a name="how-toodownload-password-reset-registration-events-quickly-with-powershell"></a>Restablecimiento de contraseña de toodownload de cómo los eventos de registro rápidamente con PowerShell

Además toousing Hola informes de Azure AD y API de eventos directamente, también puede usar Hola por debajo de los eventos de registro de toorecent de secuencias de comandos de PowerShell en el directorio. Esto es útil en caso de que desee toosee que se haya registrado recientemente, o desea tooensure que el restablecimiento de contraseñas implementación se está produciendo tal como se esperaba.

* [Script de PowerShell para la actividad de registro de SSPR de Azure AD](https://gallery.technet.microsoft.com/scriptcenter/azure-ad-self-service-e31b8aee)

### <a name="description-of-report-columns-in-azure-portal"></a>Descripción de las columnas del informe en Azure Portal

Hello siguiente lista explica cada una de las columnas del informe hello en detalle:

* **Usuario** : operación de registro de restablecimiento de usuario de Hola que intentó una contraseña.
* **Rol** : rol de Hola de usuario de hello en el directorio de Hola.
* **Fecha y hora** : Hola fecha y hora del intento de Hola.
* **Datos registrados** – registro qué usuario de Hola de datos de autenticación proporcionada durante la contraseña para el restablecimiento.

### <a name="description-of-report-values-in-azure-portal"></a>Descripción de los valores del informe en Azure Portal

Hello tabla siguiente describen distintos valores de hello permitidos para cada columna:

| Columna | Valores permitidos y su significado |
| --- | --- |
| Datos registrados |**Correo electrónico alternativo** – usuario utiliza alternativo correo electrónico o la autenticación de correo electrónico tooauthenticate<p><p>**Teléfono del trabajo**– usuario utiliza office teléfono tooauthenticate<p>**Teléfono móvil** -usuario utiliza tooauthenticate de teléfono de autenticación o teléfono móvil<p>**Preguntas de seguridad** : tooauthenticate de preguntas de seguridad del usuario que se usa<p>**Cualquier combinación de hello anteriormente (por ejemplo, correo electrónico alternativo + teléfono móvil)** : se produce cuando se especifica de una directiva de 2 puertas y muestra los dos métodos que Hola tooauthentication de usuario utilizado solicitud para restablecer su contraseña. |

## <a name="view-password-reset-activity-in-hello-classic-portal"></a>Actividad en el portal clásico de hello restablecimiento de contraseña de vista

Este informe muestra todos los intentos de restablecimiento de contraseña que se han producido en su organización.

* **Intervalo de tiempo máximo**: 30 días
* **Número máximo de filas**: 75 000
* **Se puede descargar**: Sí, en un archivo CSV

### <a name="description-of-report-columns-in-azure-classic-portal"></a>Descripción de las columnas del informe en el Portal de Azure clásico

Hello siguiente lista explica cada una de las columnas del informe hello en detalle:

1. **Usuario** – (basada en el campo de Id. de usuario de hello proporcionado al usuario Hola procede tooreset una contraseña) de la operación de restablecimiento de usuario de Hola que intentó una contraseña.
2. **Rol** : rol de Hola de usuario de hello en el directorio de Hola.
3. **Fecha y hora** : Hola fecha y hora del intento de Hola.
4. **Se usa métodos** : Hola a qué métodos de autenticación de usuario utilizado para esta operación de restablecimiento.
5. **Resultado** : la operación de restablecimiento de resultado de hello de contraseña de Hola.
6. **Detalles** : Hola detalles de por qué de restablecimiento de contraseña de hello resultó en valor Hola lo hizo.  También incluye los pasos de mitigación que podría seguir tooresolve un error inesperado.

### <a name="description-of-report-values-in-azure-classic-portal"></a>Descripción de los valores del informe en el Portal de Azure clásico

Hello tabla siguiente describen distintos valores de hello permitidos para cada columna:

| Columna | Valores permitidos y su significado |
| --- | --- |
| Métodos usados |**Correo electrónico alternativo** – usuario utiliza alternativo correo electrónico o la autenticación de correo electrónico tooauthenticate<p>**Teléfono del trabajo** – usuario utiliza office teléfono tooauthenticate<p>**Teléfono móvil** : utilizar tooauthenticate de teléfono móvil o la autenticación de usuario<p>**Preguntas de seguridad** : tooauthenticate de preguntas de seguridad del usuario que se usa<p>**Cualquier combinación de hello anteriormente (por ejemplo, correo electrónico alternativo + teléfono móvil)** : se produce cuando se especifica de una directiva de 2 puertas y muestra los dos métodos que Hola tooauthentication de usuario utilizado solicitud para restablecer su contraseña. |
| Resultado |**Abandonado**: el usuario ha iniciado un restablecimiento de contraseña, pero lo ha interrumpido antes de que finalizara.<p>**Bloquea** : cuenta de usuario se toouse ha impedido el restablecimiento debido a página de restablecimiento de contraseña de tooattempting toouse Hola de contraseña o puerta de restablecimiento de una sola contraseña demasiadas veces en un período de 24 horas<p>**Cancelar** – usuario inició un restablecimiento de contraseña pero, a continuación, hace clic en la sesión de hello toocancel Hola Cancelar botón mitad del proceso <p>**Administrador contactado** – usuario había tenido un problema durante su sesión que no pudo resolver, por lo que el usuario de hello hace clic en el vínculo "Póngase en contacto con el administrador" de hello en lugar de finalizar el flujo de restablecimiento de contraseña de Hola<p>**No se pudo** : usuario no era capaz de tooreset una contraseña, probablemente porque usuario hello no era característica de hello toouse configurado (por ejemplo, licencia, falta información de autenticación, administrados por contraseña local pero la escritura diferida no está desactivada).<p>**Correcto** : la contraseña se restableció correctamente. |
| Detalles |Consulte la tabla siguiente: |

### <a name="allowed-values-for-details-column"></a>Valores permitidos para la columna Detalles

Abajo aparece la lista de Hola de tipos de resultado, puede esperar cuando mediante una contraseña de hello restablezca el informe de actividad:

| Detalles | Tipo de resultado |
| --- | --- |
| Usuario abandonado tras completar la opción de comprobación de correo electrónico de Hola |Abandoned |
| Usuario abandonado tras completar la opción de verificación por SMS móvil Hola |Abandoned |
| Usuario abandonado tras completar la opción de comprobación de llamada de voz móviles de Hola |Abandoned |
| Usuario abandonado tras completar la opción de comprobación de llamada de voz de office de Hola |Abandoned |
| Usuario abandonado tras completar la opción de preguntas de seguridad de Hola |Abandoned |
| El usuario abandonó después de escribir su identificador de usuario. |Abandoned |
| Usuario abandonado tras iniciar la opción de comprobación de correo electrónico de Hola |Abandoned |
| Usuario abandonado tras iniciar la opción de verificación por SMS móvil Hola |Abandoned |
| Usuario abandonado tras iniciar la opción de comprobación de llamada de voz móviles de Hola |Abandoned |
| Usuario abandonado tras iniciar la opción de comprobación de llamada de voz de office de Hola |Abandoned |
| Usuario abandonado tras iniciar la opción de preguntas de seguridad de Hola |Abandoned |
| El usuario abandonó antes de seleccionar una nueva contraseña. |Abandonado |
| El usuario abandonó mientras seleccionaba una nueva contraseña. |Abandonado |
| El usuario escribió demasiados códigos de comprobación por SMS no válidos y se ha bloqueado durante 24 horas. |Bloqueado |
| El usuario intentó la comprobación por llamada de voz al teléfono móvil demasiadas veces y se ha bloqueado durante 24 horas. |Bloqueado |
| El usuario intentó la comprobación por llamada de voz al teléfono de la oficina demasiadas veces y se ha bloqueado durante 24 horas. |Bloqueado |
| El usuario intentó tooanswer preguntas de seguridad demasiadas veces y se ha bloqueado durante 24 horas |Bloqueado |
| El usuario intentó tooverify un número de teléfono demasiadas veces y se ha bloqueado durante 24 horas |Bloqueado |
| Usuario canceló la operación antes de pasar a métodos de autenticación de hello necesario |Canceled |
| El usuario lo canceló antes de enviar una contraseña nueva. |Canceled |
| Usuario establecer contacto con un administrador tras intentar la opción de comprobación de correo electrónico de Hola |Administrador contactado |
| Usuario establecer contacto con un administrador tras intentar la opción de verificación por SMS móvil Hola |Administrador contactado |
| Usuario establecer contacto con un administrador tras intentar la opción de comprobación de llamada de voz móviles de Hola |Administrador contactado |
| Usuario establecer contacto con un administrador tras intentar la opción de comprobación de llamada de voz de office de Hola |Administrador contactado |
| Usuario establecer contacto con un administrador tras intentar la opción de comprobación de pregunta de seguridad de Hola |Administrador contactado |
| El restablecimiento de contraseña no está habilitado para este usuario. Habilitar restablecimiento de contraseña en hello configurarlo tooresolve de pestaña |Con error |
| El usuario no tiene una licencia. Puede agregarse un tooresolve de usuario de toohello de licencia |Con error |
| Usuario intentó tooreset desde un dispositivo sin las cookies habilitadas |Con error |
| La cuenta del usuario no tiene definidos suficientes métodos de autenticación. Agregue el código tooresolve de información de autenticación |Con error |
| La contraseña del usuario se administra en el entorno local. Puede habilitar esta tooresolve de escritura diferida de contraseñas |Con error |
| No pudimos obtener acceso a su servicio de restablecimiento de contraseña local. Compruebe el registro de eventos de su máquina de sincronización. |Con error |
| Se encontró un problema al restablecer la contraseña en local del usuario de Hola. Compruebe el registro de eventos de su máquina de sincronización. |Con error |
| Este usuario no es un miembro del grupo de usuarios de restablecimiento de contraseña de Hola. Agregue este tooresolve de grupo de usuario toothat esto. |Con error |
| El restablecimiento de contraseña se ha deshabilitado por completo para este inquilino. Vea [aquí](http://aka.ms/ssprtroubleshoot) tooresolve esto. |Con error |
| El usuario restableció la contraseña correctamente. |Correcto |

## <a name="self-service-password-management-activity-types"></a>Tipos de actividad de administración de contraseñas de autoservicio

Hola siguientes tipos de actividad aparece en hello **administración de contraseñas de autoservicio** categoría de eventos de auditoría.  Una descripción de cada uno de ellos.

* [**Bloqueado de restablecimiento de contraseña de autoservicio** ](#activity-type-blocked-from-self-service-password-reset) -indica que un usuario intentó tooreset una contraseña, use una puerta específica, o validar un número de teléfono más de 5 veces total en 24 horas.
* [**Cambiar contraseña (autoservicio)** ](#activity-type-change-password-self-service) -indica un usuario realiza de forma voluntaria o forzada (due tooexpiry) cambio de contraseña.
* [**Restablecimiento de contraseña (admin)** ](#activity-type-reset-password-by-admin) -indica un administrador realiza una restablecimiento en nombre del usuario del portal de Azure Hola de contraseña.
* [**Restablecimiento de contraseñas (autoservicio)** ](#activity-type-reset-password-self-service) -indica que un usuario correctamente restablece su contraseña de hello [Portal de restablecimiento de contraseña de Azure AD](https://passwordreset.microsoftonline.com).
* [**Progreso de la actividad de flujo de restablecimiento de contraseña de autoservicio** ](#activity-type-self-serve-password-reset-flow-activity-progress) -indica cada paso específico procede de un usuario a través de (como puerta de autenticación de restablecimiento de pasar una contraseña específica) como parte de la contraseña de hello el proceso de restablecimiento.
* [**Desbloquear la cuenta de usuario (autoservicio)** ](#activity-type-unlock-user-account-self-service) -indica que un usuario desbloqueó correctamente su cuenta de Active Directory sin restablecer la contraseña de hello [Portal de restablecimiento de contraseña de Azure AD](https://passwordreset.microsoftonline.com) con Hola cuenta AD desbloquear sin la característica de restablecimiento.
* [**Usuario registrado para restablecer la contraseña de autoservicio** ](#activity-type-user-registered-for-self-service-password-reset) -indica que un usuario ha registrado todos Hola requiere información toobe capaz de tooreset su contraseña de acuerdo con hello actualmente especifica la directiva de restablecimiento de contraseña del inquilino.

### <a name="activity-type-blocked-from-self-service-password-reset"></a>Tipo de actividad: Bloqueado para el restablecimiento de contraseña de autoservicio

Hola lista siguiente explica esta actividad en detalle:

* **Descripción de la actividad** : indica que un usuario intentó tooreset una contraseña, use una puerta específica o validar un número de teléfono más de 5 veces total en 24 horas.
* **Actividad Actor** -usuario Hola que se limitó a realizar más operaciones de restablecimiento. Puede tratarse de un usuario final o un administrador.
* **Destino de la actividad** -usuario Hola que se limitó a realizar más operaciones de restablecimiento. Puede tratarse de un usuario final o un administrador.
* **Estados permitidos de la actividad**
  * _Éxito_ -indica que un usuario se limitó realice cualquier restablece adicional, intente los métodos de autenticación adicionales, o validar los números de teléfono adicionales para hello próximas 24 horas.
* **Motivo del error del estado de la actividad**: no aplicable

### <a name="activity-type-change-password-self-service"></a>Tipo de actividad: Cambio de contraseña (autoservicio)

Hola lista siguiente explica esta actividad en detalle:

* **Descripción de la actividad** : indica un usuario realiza de forma voluntaria o forzada (due tooexpiry) cambio de contraseña.
* **Actividad Actor** -usuario Hola que ha cambiado la contraseña. Puede tratarse de un usuario final o un administrador.
* **Destino de la actividad** -usuario Hola que ha cambiado la contraseña. Puede tratarse de un usuario final o un administrador.
* **Estados permitidos de la actividad**
  * _Correcto_: indica que un usuario cambió correctamente la contraseña.
  * _Error_ -indica que un usuario no pudo toochange su contraseña. Si hace clic en fila Hola permite hello toosee **razón del estado de actividad** categoría toolearn más información acerca de por qué se produjo el error de Hola.
* **Motivo del error del estado de la actividad** - 
  * _FuzzyPolicyViolationInvalidPassword_ -usuario Hola seleccionó una contraseña, que automáticamente se prohibió debido a las capacidades de detección de contraseña de prohibido del tooMicrosoft buscar toobe demasiado común o especialmente débil.

### <a name="activity-type-reset-password-by-admin"></a>Tipo de actividad: Restablecimiento de contraseña (de parte del administrador)

Hola lista siguiente explica esta actividad en detalle:

* **Descripción de la actividad** : indica un administrador realiza una restablecimiento en nombre del usuario del portal de Azure Hola de contraseña.
* **Actividad Actor** -Administrador de Hola que llevó a cabo Hola de restablecimiento de contraseña en nombre de otro usuario final o el administrador. Debe ser un administrador global, administrador de contraseñas, administrador de usuarios o administrador del departamento de soporte técnico.
* **Destino de la actividad** -usuario Hola cuya contraseña se ha restablecido. Puede tratarse de un usuario final u otro administrador.
* **Estados permitidos de la actividad**
  * _Correcto_: indica que un administrador restableció correctamente la contraseña de un usuario.
  * _Error_ -indica que un administrador no pudo toochange una contraseña de usuario. Si hace clic en fila Hola permite hello toosee **razón del estado de actividad** categoría toolearn más información acerca de por qué se produjo el error de Hola.

### <a name="activity-type-reset-password-self-service"></a>Tipo de actividad: Restablecimiento de contraseña (autoservicio)

Hola lista siguiente explica esta actividad en detalle:

* **Descripción de la actividad** : indica un usuario correctamente restablece su contraseña de hello [Portal de restablecimiento de contraseña de Azure AD](https://passwordreset.microsoftonline.com).
* **Actividad Actor** -usuario Hola que restablece su contraseña. Puede tratarse de un usuario final o un administrador.
* **Destino de la actividad** -usuario Hola que restablece su contraseña. Puede tratarse de un usuario final o un administrador.
* **Estados permitidos de la actividad**
  * _Correcto_: indica que un usuario restableció correctamente su propia contraseña.
  * _Error_ -indica que un usuario no pudo tooreset su propia contraseña. Si hace clic en fila Hola permite hello toosee **razón del estado de actividad** categoría toolearn más información acerca de por qué se produjo el error de Hola.
* **Motivo del error del estado de la actividad** -
  * _FuzzyPolicyViolationInvalidPassword_ -Hola, administrador seleccionó una contraseña, que automáticamente se prohibió debido a las capacidades de detección de contraseña de prohibido del tooMicrosoft buscar toobe demasiado común o especialmente débil.

### <a name="activity-type-self-serve-password-reset-flow-activity-progress"></a>Tipo de actividad: Progreso de la actividad del flujo de restablecimiento de contraseña de autoservicio

Hola lista siguiente explica esta actividad en detalle:

* **Descripción de la actividad** – indica cada paso específico un usuario avanza a través de (como puerta de autenticación de restablecimiento de pasar una contraseña específica) como parte de la contraseña de hello el proceso de restablecimiento.
* **Actividad Actor** -usuario de Hola que realizó la parte de la contraseña de hello restablece flujo. Puede tratarse de un usuario final o un administrador.
* **Destino de la actividad** -usuario de Hola que realizó la parte de la contraseña de hello restablece flujo. Puede tratarse de un usuario final o un administrador.
* **Estados permitidos de la actividad**
  * _Éxito_ -indica un usuario se ha completado correctamente un paso concreto de flujo de restablecimiento de contraseña de Hola.
  * _Error_ -indica un paso concreto de contraseña de hello restablece el flujo de error. Si hace clic en fila Hola permite hello toosee **razón del estado de actividad** categoría toolearn más información acerca de por qué se produjo el error de Hola.
* **Motivos del estado permitido de la actividad**
  * Consulte la tabla siguiente para ver [todos los motivos del estado permitido de la actividad de restablecimiento](#allowed-values-for-details-column)

### <a name="activity-type-unlock-user-account-self-service"></a>Tipo de actividad: Desbloqueo de la cuenta de usuario (autoservicio)

Hola lista siguiente explica esta actividad en detalle:

* **Descripción de la actividad** : indica que un usuario desbloqueó correctamente su cuenta de Active Directory sin restablecer la contraseña de hello [Portal de restablecimiento de contraseña de Azure AD](https://passwordreset.microsoftonline.com) con cuenta de hello AD desbloquear sin restablecer característica.
* **Actividad Actor** -usuario Hola que desbloquea sus cuentas sin restablecer la contraseña. Puede tratarse de un usuario final o un administrador.
* **Destino de la actividad** -usuario Hola que desbloquea sus cuentas sin restablecer la contraseña. Puede tratarse de un usuario final o un administrador.
* **Estados permitidos de la actividad**
  * _Correcto_: indica que un usuario desbloqueó correctamente su propia cuenta.
  * _Error_ -indica que un usuario no pudo toounlock su cuenta. Si hace clic en fila Hola permite hello toosee **razón del estado de actividad** categoría toolearn más información acerca de por qué se produjo el error de Hola.

### <a name="activity-type-user-registered-for-self-service-password-reset"></a>Tipo de actividad: Usuario registrado para el restablecimiento de contraseña de autoservicio

Hola lista siguiente explica esta actividad en detalle:

* **Descripción de la actividad** : indica que un usuario ha registrado todos Hola requiere información toobe capaz de tooreset su contraseña de acuerdo con hello actualmente especifica la directiva de restablecimiento de contraseña del inquilino. 
* **Actividad Actor** -usuario Hola que se registraron para restablecer la contraseña. Puede tratarse de un usuario final o un administrador.
* **Destino de la actividad** -usuario Hola que se registraron para restablecer la contraseña. Puede tratarse de un usuario final o un administrador.
* **Estados permitidos de la actividad**
  * _Éxito_ -indica un registrada correctamente para restablecer la conformidad con la directiva actual Hola la contraseña del usuario. 
  * _Error_ -indica una tooregister de usuario no se pudo para restablecer la contraseña. Si hace clic en fila Hola permite hello toosee **razón del estado de actividad** categoría toolearn más información acerca de por qué se produjo el error de Hola. Nota: esto no significa que un usuario es no se puede tooreset su propia contraseña, al igual que no se completó el proceso de registro de hello. Si no hay datos no comprobados en su cuenta de que es correcto (por ejemplo, un número de teléfono que no se valida), aunque no ha comprobado este número de teléfono, puede usarlo tooreset su contraseña. Para más información, consulte [¿Qué ocurre cuando se registra un usuario?](https://docs.microsoft.com/azure/active-directory/active-directory-passwords-learn-more#what-happens-when-a-user-registers)

## <a name="next-steps"></a>Pasos siguientes

Hola siguientes vínculos proporciona más información sobre el uso de Azure AD de restablecimiento de contraseña

* [Registros de auditoría de administración de acceso directo toouser](https://portal.azure.com/#blade/Microsoft_AAD_IAM/UserManagementMenuBlade/Audit) : vaya directamente registros de auditoría de administración de usuarios del inquilino de tooyour
* [**Inicio rápido**](active-directory-passwords-getting-started.md): preparativos para el autoservicio de administración de contraseñas de Azure AD 
* [**Licencias**](active-directory-passwords-licensing.md): configuración de licencias de Azure AD
* [**Datos** ](active-directory-passwords-data.md) : comprender los datos de Hola que es necesarios y cómo se utiliza para la administración de contraseñas
* [**Implementación** ](active-directory-passwords-best-practices.md) -planear e implementar a los usuarios de Autoservicio tooyour usando la orientación de hello encontrar aquí
* [**Personalizar** ](active-directory-passwords-customize.md) -personalizar Hola apariencia y funcionamiento del programa Hola a la experiencia de Autoservicio de su empresa.
* [**Profundización técnica** ](active-directory-passwords-how-it-works.md) -ir detrás de hello cortina toounderstand cómo funciona
* [**Preguntas más frecuentes**](active-directory-passwords-faq.md): ¿Cómo? ¿Por qué? ¿Qué? ¿Dónde? ¿Quién? ¿Cuándo? -Responde tooquestions siempre deseara tooask
* [**Solucionar problemas de** ](active-directory-passwords-troubleshoot.md) -Obtenga información acerca de cómo problemas comunes de tooresolve que vemos con SSPR
* [**Directiva**](active-directory-passwords-policy.md): información sobre las directivas de contraseñas de Azure AD y cómo establecerlas
