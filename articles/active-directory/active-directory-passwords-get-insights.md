---
title: "Visión operativa con los informes de administración de contraseñas de Azure AD | Microsoft Docs"
description: "Este artículo describe cómo toouse notifica una visión general de tooget en las operaciones de administración de contraseñas en su organización."
services: active-directory
documentationcenter: 
author: MicrosoftGuyJFlo
manager: femila
ms.reviewer: gahug
ms.assetid: 1472b51d-53f4-4b0f-b1be-57f6fa88fa65
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/17/2017
ms.author: joflore
ms.custom: it-pro
ms.openlocfilehash: 90e0b8e621cdfe3e3a2f15df7b98115008855500
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooget-operational-insights-with-password-management-reports"></a>¿Cómo notifica tooget visión operativa con administración de contraseñas
> [!IMPORTANT]
> **¿Está aquí porque tiene problemas para iniciar sesión?** Si es así, [aquí aprenderá a cambiar y restablecer la contraseña](active-directory-passwords-update-your-own-password.md#reset-or-unlock-my-password-for-a-work-or-school-account).
>
>

Esta sección describe cómo puede usar Azure Active Directory tooview cómo los usuarios usan el restablecimiento de contraseña ni cambiar de su organización de informes de administración de contraseñas.

* [**Información general de los informes de administración de contraseñas**](#overview-of-password-management-reports)
* [**Cómo tooview la administración de contraseñas se notifica en el nuevo portal de Azure Hola**](#how-to-view-password-management-reports)
 * [Roles de directorio permitidos tooread informes](#directory-roles-allowed-to-read-reports)
* [**Hola de autoservicio a los tipos de actividad de administración de contraseñas en el nuevo Portal de Azure**](#self-service-password-management-activity-types)
 * [Bloqueado para el restablecimiento de contraseña de autoservicio](#activity-type-blocked-from-self-service-password-reset)
 * [Cambio de contraseña (autoservicio)](#activity-type-change-password-self-service)
 * [Restablecimiento de contraseña (de parte del administrador)](#activity-type-reset-password-by-admin)
 * [Restablecimiento de contraseña (autoservicio)](#activity-type-reset-password-self-service)
 * [Progreso de la actividad del flujo de restablecimiento de contraseña de autoservicio](#activity-type-self-serve-password-reset-flow-activity-progress)
 * [Desbloqueo de la cuenta de usuario (autoservicio)](#activity-type-unlock-user-account-self-service)
 * [Usuario registrado para el restablecimiento de contraseña de autoservicio](#activity-type-user-registered-for-self-service-password-reset)
* [**¿Cómo tooretrieve eventos de administración de contraseñas de hello Azure AD API de informes y eventos**](#how-to-retrieve-password-management-events-from-the-azure-ad-reports-and-events-api)
 * [Informes de las limitaciones de recuperación de datos de la API](#reporting-api-data-retrieval-limitations)
* [**Restablecimiento de contraseña de toodownload de cómo los eventos de registro rápidamente con PowerShell**](#how-to-download-password-reset-registration-events-quickly-with-powershell)
* [**Cómo informes de administración de contraseñas de tooview de portal clásico de Hola**](#how-to-view-password-management-reports-in-the-classic-portal)
* [**Actividad de registro de su organización en el portal clásico de Hola de restablecimiento de contraseña de vista**](#view-password-reset-registration-activity-in-the-classic-portal)
* [**Actividad de la organización en el portal clásico de hello restablecimiento de contraseña de vista**](#view-password-reset-activity-in-the-classic-portal)


## <a name="overview-of-password-management-reports"></a>Información general de los informes de administración de contraseñas
Después de implementar el restablecimiento de contraseña, uno de los siguientes pasos más comunes hello es toosee cómo porque se está usando en su organización.  Por ejemplo, puede que desee una visión general de tooget en cómo se registran los usuarios de restablecimiento de contraseña o la contraseña cuántos restablecimientos se han realizado en hello últimos días.  Estas son algunas preguntas comunes de Hola que será capaz de tooanswer con informes de administración de contraseñas de Hola que existen en hello [Portal de administración de Azure](https://manage.windowsazure.com) hoy en día:

* ¿Cuántas personas se han registrado para el restablecimiento de contraseña?
* ¿Quién se ha registrado para el restablecimiento de contraseña?
* ¿Qué datos está registrando la gente?
* ¿Cuántas personas restablecieron sus contraseñas en hello últimos 7 días?
* ¿Qué usuarios de métodos más comunes de Hola o administradores utilicen tooreset sus contraseñas?
* ¿Cuáles son comunes emite a los usuarios o administradores de cara al intentar restablecer la contraseña toouse?
* ¿Qué administradores restablecen sus propias contraseñas con frecuencia?
* ¿Hay alguna actividad sospechosa en relación con el restablecimiento de contraseña?

## <a name="how-tooview-password-management-reports"></a>Cómo tooview informes de administración de contraseñas
Hola nueva [Portal de Azure](https://portal.azure.com) experimenta, se tiene una forma mejorada tooview contraseña restablecimiento y la contraseña Restablecer registro actividad.  Siga los pasos de hello debajo de restablecimiento de contraseña de hello toofind y la contraseña restablecer los eventos de registro de hello nueva [Portal de Azure](https://portal.azure.com):

1. Navegue demasiado[**portal.azure.com**](https://portal.azure.com)
2. Haga clic en hello **más servicios** menú de navegación de mano izquierda Hola principal Portal de Azure
3. Busque **Azure Active Directory** en Hola lista de servicios y selecciónelo
4. Haga clic en **usuarios y grupos** del menú de navegación de hello Azure Active Directory
5. Haga clic en hello **los registros de auditoría** elemento de navegación del menú de navegación de usuarios y grupos de Hola. Esto le mostrará todas de que se produzca de eventos de auditoría de hello en todos los usuarios de hello en el directorio. Puede filtrar esta vista toosee todos los Hola relacionadas con contraseñas eventos, también.
6. toofilter esta administración de contraseñas de vista tooonly Hola relacionados con eventos, haga clic en hello **filtro** situado en la parte superior de Hola de hoja de Hola.
7. De hello **filtro** menú, seleccione hello **categoría** de lista desplegable y cambiarlo toohello **administración de contraseñas de autoservicio** tipo de categoría.
8. Opcionalmente, otra lista de Hola de filtro eligiendo específicos de hello **actividad** que le interesen
### <a name="direct-link-toouser-audit-blade"></a>Hoja de auditoría de vínculo directo tooUser
Si están firmadas en el portal de tooyour, aquí es una hoja de auditoría de vínculo directo toohello usuario donde puede ver estos eventos:

* [Vaya toouser administración audit vista directamente](https://portal.azure.com/#blade/Microsoft_AAD_IAM/UserManagementMenuBlade/Audit)

### <a name="directory-roles-allowed-tooread-reports"></a>Roles de directorio permiten tooread informes
Actualmente, hello siguientes roles del directorio pueden leer los informes de administración de contraseñas de Azure AD en el portal de Azure clásico hello:

* Administrador global

Antes de que se pueda tooread estos informes, un administrador global de la empresa de hello debe ha elegido para de este toobe datos recuperado en nombre de organización de hello visitando Hola reporting tab o auditoría de registros al menos una vez. Los datos de su organización no se recopilarán hasta que lo haga.

tooread más información acerca de los roles de directorio y qué puede, consulte [asignar roles de administrador en Azure Active Directory](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-assign-admin-roles).

## <a name="self-service-password-management-activity-types"></a>Tipos de actividad de administración de contraseñas de autoservicio
Hola siguientes tipos de actividad aparece en hello **administración de contraseñas de autoservicio** categoría de eventos de auditoría.  A continuación aparece una descripción de cada uno de ellos.

* [**Bloqueado de restablecimiento de contraseña de autoservicio** ](#activity-type-blocked-from-self-service-password-reset) -indica que un usuario intentó tooreset una contraseña, use una puerta específica, o validar un número de teléfono más de 5 veces total en 24 horas.
* [**Cambiar contraseña (autoservicio)** ](#activity-type-change-password-self-service) -indica un usuario realiza de forma voluntaria o forzada (due tooexpiry) cambio de contraseña.
* [**Restablecimiento de contraseña (admin)** ](#activity-type-reset-password-by-admin) -indica un administrador realiza una restablecimiento en nombre del usuario del Portal de Azure de Hola de contraseña.
* [**Restablecimiento de contraseñas (autoservicio)** ](#activity-type-reset-password-self-service) -indica que un usuario restableció correctamente la contraseña de hello [Portal de restablecimiento de contraseña de Azure AD](https://passwordreset.microsoftonline.com).
* [**Progreso de la actividad de flujo de restablecimiento de contraseña de autoservicio** ](#activity-type-self-serve-password-reset-flow-activity-progress) -indica cada paso específico procede de un usuario a través de (como puerta de autenticación de restablecimiento de pasar una contraseña específica) como parte de la contraseña de hello el proceso de restablecimiento.
* [**Desbloquear la cuenta de usuario (autoservicio)** ](#activity-type-unlock-user-account-self-service) -indica que un usuario desbloqueó correctamente su cuenta de Active Directory sin restablecer su contraseña de hello [Portal de restablecimiento de contraseña de Azure AD](https://passwordreset.microsoftonline.com) con hello [cuenta AD desbloquear sin restablecer](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-passwords-customize#allow-users-to-unlock-accounts-without-resetting-their-password) característica.
* [**Usuario registrado para restablecer la contraseña de autoservicio** ](#activity-type-user-registered-for-self-service-password-reset) -indica que un usuario ha registrado todos Hola requiere información toobe pueda tooreset la contraseña de acuerdo con la directiva de restablecimiento de contraseñas de Hola actualmente especificado por el inquilino.

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
* **Actividad Actor** -usuario de Hola que cambió su contraseña. Puede tratarse de un usuario final o un administrador.
* **Destino de la actividad** -usuario de Hola que cambió su contraseña. Puede tratarse de un usuario final o un administrador.
* **Estados permitidos de la actividad**
 * _Correcto_: indica que un usuario cambió correctamente la contraseña.
 * _Error_ -indica que un usuario no pudo toochange su contraseña. Al hacer clic en la fila de hello le permitirá hello toosee **razón del estado de actividad** categoría toolearn más información acerca de por qué se produjo el error de Hola.
* **Motivo del error del estado de la actividad** -
 * _FuzzyPolicyViolationInvalidPassword_ -usuario Hola seleccionó una contraseña que se prohibió automáticamente debido a las capacidades de detección de contraseña de prohibido del tooMicrosoft buscar toobe demasiado común o especialmente débil.

### <a name="activity-type-reset-password-by-admin"></a>Tipo de actividad: Restablecimiento de contraseña (de parte del administrador)
Hola lista siguiente explica esta actividad en detalle:

* **Descripción de la actividad** : indica un administrador realiza una restablecimiento en nombre del usuario del Portal de Azure de Hola de contraseña.
* **Actividad Actor** -Administrador de Hola que llevó a cabo Hola de restablecimiento de contraseña en nombre de otro usuario final o el administrador. Debe ser un administrador global, administrador de contraseñas, administrador de usuarios o administrador del departamento de soporte técnico.
* **Destino de la actividad** -usuario Hola cuya contraseña se ha restablecido. Puede tratarse de un usuario final u otro administrador.
* **Estados permitidos de la actividad**
 * _Correcto_: indica que un administrador restableció correctamente la contraseña de un usuario.
 * _Error_ -indica que un administrador no pudo toochange una contraseña de usuario. Al hacer clic en la fila de hello le permitirá hello toosee **razón del estado de actividad** categoría toolearn más información acerca de por qué se produjo el error de Hola.

### <a name="activity-type-reset-password-self-service"></a>Tipo de actividad: Restablecimiento de contraseña (autoservicio)
Hola lista siguiente explica esta actividad en detalle:

* **Descripción de la actividad** : indica que un usuario restableció correctamente la contraseña de hello [Portal de restablecimiento de contraseña de Azure AD](https://passwordreset.microsoftonline.com).
* **Actividad Actor** -usuario de Hola que restablezca su contraseña. Puede tratarse de un usuario final o un administrador.
* **Destino de la actividad** -usuario de Hola que restablezca su contraseña. Puede tratarse de un usuario final o un administrador.
* **Estados permitidos de la actividad**
 * _Correcto_: indica que un usuario restableció correctamente su propia contraseña.
 * _Error_ -indica que un usuario no pudo tooreset su contraseña. Al hacer clic en la fila de hello le permitirá hello toosee **razón del estado de actividad** categoría toolearn más información acerca de por qué se produjo el error de Hola.
* **Motivo del error del estado de la actividad** -
 * _FuzzyPolicyViolationInvalidPassword_ -Hola, administrador seleccionó una contraseña que se prohibió automáticamente debido a las capacidades de detección de contraseña de prohibido del tooMicrosoft buscar toobe demasiado común o especialmente débil.

### <a name="activity-type-self-serve-password-reset-flow-activity-progress"></a>Tipo de actividad: Progreso de la actividad del flujo de restablecimiento de contraseña de autoservicio
Hola lista siguiente explica esta actividad en detalle:

* **Descripción de la actividad** – indica cada paso específico un usuario avanza a través de (como puerta de autenticación de restablecimiento de pasar una contraseña específica) como parte de la contraseña de hello el proceso de restablecimiento.
* **Actividad Actor** -usuario de Hola que realizó la parte de la contraseña de hello restablece flujo. Puede tratarse de un usuario final o un administrador.
* **Destino de la actividad** -usuario de Hola que realizó la parte de la contraseña de hello restablece flujo. Puede tratarse de un usuario final o un administrador.
* **Estados permitidos de la actividad**
 * _Éxito_ -indica un usuario se ha completado correctamente un paso concreto de flujo de restablecimiento de contraseña de Hola.
 * _Error_ -indica un paso concreto de contraseña de hello restablece el flujo de error. Al hacer clic en la fila de hello le permitirá hello toosee **razón del estado de actividad** categoría toolearn más información acerca de por qué se produjo el error de Hola.
* **Motivos del estado permitido de la actividad**
 * Consulte la tabla siguiente para ver [todos los motivos del estado permitido de la actividad de restablecimiento](#allowed-values-for-details-column)

### <a name="activity-type-unlock-user-account-self-service"></a>Tipo de actividad: Desbloqueo de la cuenta de usuario (autoservicio)
Hola lista siguiente explica esta actividad en detalle:

* **Descripción de la actividad** : indica que un usuario desbloqueó correctamente su cuenta de Active Directory sin restablecer su contraseña de hello [Portal de restablecimiento de contraseña de Azure AD](https://passwordreset.microsoftonline.com) con hello [AD desbloqueo de cuentas sin restablecer](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-passwords-customize#allow-users-to-unlock-accounts-without-resetting-their-password) característica.
* **Actividad Actor** -usuario Hola que desbloquea su cuenta sin restablecer la contraseña. Puede tratarse de un usuario final o un administrador.
* **Destino de la actividad** -usuario Hola que desbloquea su cuenta sin restablecer la contraseña. Puede tratarse de un usuario final o un administrador.
* **Estados permitidos de la actividad**
 * _Correcto_: indica que un usuario desbloqueó correctamente su propia cuenta.
 * _Error_ -indica que un usuario no pudo toounlock su cuenta. Al hacer clic en la fila de hello le permitirá hello toosee **razón del estado de actividad** categoría toolearn más información acerca de por qué se produjo el error de Hola.

### <a name="activity-type-user-registered-for-self-service-password-reset"></a>Tipo de actividad: Usuario registrado para el restablecimiento de contraseña de autoservicio
Hola lista siguiente explica esta actividad en detalle:

* **Descripción de la actividad** : indica que un usuario ha registrado todos Hola requiere información toobe pueda tooreset la contraseña de acuerdo con la directiva de restablecimiento de contraseñas de Hola actualmente especificado por el inquilino.
* **Actividad Actor** -usuario Hola que se registraron para restablecer la contraseña. Puede tratarse de un usuario final o un administrador.
* **Destino de la actividad** -usuario Hola que se registraron para restablecer la contraseña. Puede tratarse de un usuario final o un administrador.
* **Estados permitidos de la actividad**
 * _Éxito_ -indica un registrada correctamente para restablecer la conformidad con la directiva actual Hola la contraseña del usuario.
 * _Error_ -indica una tooregister de usuario no se pudo para restablecer la contraseña. Al hacer clic en la fila de hello le permitirá hello toosee **razón del estado de actividad** categoría toolearn más información acerca de por qué se produjo el error de Hola. Nota: esto no significa que un usuario es no se puede tooreset su contraseña, al igual que no completó el proceso de registro de hello. Si no hay datos no comprobados en su cuenta de que es correcto (por ejemplo, un número de teléfono que no se valida), aunque no ha comprobado este número de teléfono, puede usarlo tooreset su contraseña. Para más información, consulte [¿Qué ocurre cuando se registra un usuario?](https://docs.microsoft.com/azure/active-directory/active-directory-passwords-learn-more#what-happens-when-a-user-registers)

## <a name="how-tooretrieve-password-management-events-from-hello-azure-ad-reports-and-events-api"></a>¿Cómo tooretrieve eventos de administración de contraseñas de hello Azure AD API de informes y eventos
A partir de agosto de 2015, hello Azure AD API de informes y eventos ahora admite la recuperación de información de hello incluida en hello contraseña restablecimiento y la contraseña restablecimiento de los informes de registro. Con esta API, puede descargar de restablecimiento de contraseña individuales y eventos de registro para la integración de restablecimiento de contraseña con hello reporting tecnología de su choce.

### <a name="how-tooget-started-with-hello-reporting-api"></a>¿Cómo tooget partió Hola API de informes
tooaccess estos datos, que necesita toowrite una pequeña aplicación o script tooretrieve desde nuestros servidores. [Obtenga información acerca de cómo tooget iniciado con hello API Reporting de Azure AD](active-directory-reporting-api-getting-started.md).

Una vez que tenga una secuencia de comandos de trabajo, a continuación deberá tooexamine Hola contraseña restablecimiento y registro de eventos que se pueden recuperar toomeet los escenarios.

* [SsprActivityEvent](https://msdn.microsoft.com/library/azure/mt126081.aspx#BKMK_SsprActivityEvent): listas de columnas de hello disponibles para eventos de restablecimiento de contraseña
* [SsprRegistrationActivityEvent](https://msdn.microsoft.com/library/azure/mt126081.aspx#BKMK_SsprRegistrationActivityEvent): listas de columnas Hola disponibles para los eventos de registro de restablecimiento de contraseña

### <a name="reporting-api-data-retrieval-limitations"></a>Informes de las limitaciones de recuperación de datos de la API
Actualmente, Hola informes de Azure AD y API de eventos recupera la demasiado**75.000 eventos individuales** de hello [SsprActivityEvent](https://msdn.microsoft.com/library/azure/mt126081.aspx#BKMK_SsprActivityEvent) y [SsprRegistrationActivityEvent](https://msdn.microsoft.com/library/azure/mt126081.aspx#BKMK_SsprRegistrationActivityEvent) tipos , que abarcan hello **últimos 30 días**.

Si necesita tooretrieve o almacenar datos más allá de esta ventana, se recomienda guardar en una base de datos externa y usar deltas de Hola de tooquery Hola API que son el resultado. Una práctica recomendada es toobegin recuperar estos datos cuando se inicia la contraseña restablece el proceso de registro en su organización, conservarlos externamente y, a continuación, continuar deltas de hello tootrack desde este punto.

## <a name="how-toodownload-password-reset-registration-events-quickly-with-powershell"></a>Restablecimiento de contraseña de toodownload de cómo los eventos de registro rápidamente con PowerShell
Además toousing Hola informes de Azure AD y API de eventos directamente, también puede usar Hola por debajo de los eventos de registro de toorecent de secuencias de comandos de PowerShell en el directorio. Esto es útil en caso de que desee toosee que se haya registrado recientemente, o desea tooensure que el restablecimiento de contraseñas implementación se está produciendo tal como se esperaba.

* [Script de PowerShell para la actividad de registro de SSPR de Azure AD](https://gallery.technet.microsoft.com/scriptcenter/azure-ad-self-service-e31b8aee)

## <a name="how-tooview-password-management-reports-in-hello-classic-portal"></a>Cómo informes de administración de contraseñas de tooview de portal clásico de Hola
toofind informes de administración de contraseñas de hello, siga estos pasos hello:

1. Haga clic en hello **Active Directory** extensión Hola [portal de Azure clásico](https://manage.windowsazure.com).
2. Seleccione el directorio de la lista de Hola que aparece en el portal de Hola.
3. Haga clic en hello **informes** ficha.
4. Busque en hello **registros de actividad** sección.
5. Seleccione cualquier hello **actividad de restablecimiento de contraseña** informes o hello **actividad de registro de restablecimiento de contraseña** informes.

## <a name="view-password-reset-registration-activity-in-hello-classic-portal"></a>Actividad de registro en el portal clásico de Hola de restablecimiento de contraseña de vista
informe de actividad de registro de restablecimiento de contraseña de Hello muestra que los registros que se han producido en su organización de restablecimiento de contraseña todos.  Un registro de restablecimiento de contraseña se muestra en este informe para cualquier usuario que ha registrado correctamente la información de autenticación de contraseña de Hola de restablecimiento del portal de registro ([http://aka.ms/ssprsetup](http://aka.ms/ssprsetup)).

* **Intervalo de tiempo máximo**: 30 días
* **Número máximo de filas**: 75 000
* **Se puede descargar**: Sí, en un archivo CSV

### <a name="description-of-report-columns"></a>Descripción de las columnas del informe
Hello siguiente lista explica cada una de las columnas del informe hello en detalle:

* **Usuario** : operación de registro de restablecimiento de usuario de Hola que intentó una contraseña.
* **Rol** : rol de Hola de usuario de hello en el directorio de Hola.
* **Fecha y hora** : Hola fecha y hora del intento de Hola.
* **Datos registrados** – registro qué usuario de Hola de datos de autenticación proporcionada durante la contraseña para el restablecimiento.

### <a name="description-of-report-values"></a>Descripción de los valores del informe
Hello tabla siguiente describen distintos valores de hello permitidos para cada columna:

| Columna | Valores permitidos y su significado |
| --- | --- |
| Datos registrados |**Correo electrónico alternativo** – usuario utiliza alternativo correo electrónico o la autenticación de correo electrónico tooauthenticate<p><p>**Teléfono del trabajo**– usuario utiliza office teléfono tooauthenticate<p>**Teléfono móvil** -usuario utiliza tooauthenticate de teléfono de autenticación o teléfono móvil<p>**Preguntas de seguridad** : tooauthenticate de preguntas de seguridad del usuario que se usa<p>**Cualquier combinación de hello anteriormente (por ejemplo, correo electrónico alternativo + teléfono móvil)** : se produce cuando se especifica de una directiva de 2 puertas y muestra los dos métodos que Hola tooauthentication de usuario utilizado solicitud para restablecer su contraseña. |

## <a name="view-password-reset-activity-in-hello-classic-portal"></a>Actividad en el portal clásico de hello restablecimiento de contraseña de vista
Este informe muestra todos los intentos de restablecimiento de contraseña que se han producido en su organización.

* **Intervalo de tiempo máximo**: 30 días
* **Número máximo de filas**: 75 000
* **Se puede descargar**: Sí, en un archivo CSV

### <a name="description-of-report-columns"></a>Descripción de las columnas del informe
Hello siguiente lista explica cada una de las columnas del informe hello en detalle:

1. **Usuario** – (basada en el campo de Id. de usuario de hello proporcionado al usuario Hola procede tooreset una contraseña) de la operación de restablecimiento de usuario de Hola que intentó una contraseña.
2. **Rol** : rol de Hola de usuario de hello en el directorio de Hola.
3. **Fecha y hora** : Hola fecha y hora del intento de Hola.
4. **Usar métodos** : Hola a qué métodos de autenticación de usuario utilizado para esta operación de restablecimiento.
5. **Resultado** : la operación de restablecimiento del resultado final de Hola de contraseña de Hola.
6. **Detalles** : Hola detalles de por qué de restablecimiento de contraseña de hello resultó en valor Hola lo hizo.  También incluye los pasos de mitigación que podría seguir tooresolve un error inesperado.

### <a name="description-of-report-values"></a>Descripción de los valores del informe
Hello tabla siguiente describen distintos valores de hello permitidos para cada columna:

| Columna | Valores permitidos y su significado |
| --- | --- |
| Métodos usados |**Correo electrónico alternativo** – usuario utiliza alternativo correo electrónico o la autenticación de correo electrónico tooauthenticate<p>**Teléfono del trabajo** – usuario utiliza office teléfono tooauthenticate<p>**Teléfono móvil** : utilizar tooauthenticate de teléfono móvil o la autenticación de usuario<p>**Preguntas de seguridad** : tooauthenticate de preguntas de seguridad del usuario que se usa<p>**Cualquier combinación de hello anteriormente (por ejemplo, correo electrónico alternativo + teléfono móvil)** : se produce cuando se especifica de una directiva de 2 puertas y muestra los dos métodos que Hola tooauthentication de usuario utilizado solicitud para restablecer su contraseña. |
| Resultado |**Abandonado**: el usuario ha iniciado un restablecimiento de contraseña, pero lo ha interrumpido antes de que finalizara.<p>**Bloquea** : cuenta de usuario se toouse ha impedido el restablecimiento debido a página de restablecimiento de contraseña de tooattempting toouse Hola de contraseña o puerta de restablecimiento de una sola contraseña demasiadas veces en un período de 24 horas<p>**Cancelar** – usuario inició un restablecimiento de contraseña pero, a continuación, hace clic en la sesión de hello toocancel Hola Cancelar botón mitad del proceso <p>**Administrador contactado** – usuario había tenido un problema durante su sesión que no pudo resolver, por lo que el usuario de hello hace clic en el vínculo "Póngase en contacto con el administrador" de hello en lugar de finalizar el flujo de restablecimiento de contraseña de Hola<p>**No se pudo** : usuario no era capaz de tooreset una contraseña, probablemente porque usuario hello no era característica de hello toouse configurado (por ejemplo, no hay ninguna licencia, falta información de autenticación, la contraseña se administra local pero la escritura diferida está desactivada).<p>**Correcto** : la contraseña se restableció correctamente. |
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
| El usuario canceló antes de pasar a métodos de autenticación de hello necesario |Cancelado |
| El usuario lo canceló antes de enviar una contraseña nueva. |Cancelado |
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

## <a name="next-steps"></a>Pasos siguientes
A continuación se muestran vínculos tooall de hello páginas de documentación de restablecimiento de contraseña de Azure AD:

* **¿Está aquí porque tiene problemas para iniciar sesión?** Si es así, [aquí aprenderá a cambiar y restablecer la contraseña](active-directory-passwords-update-your-own-password.md#reset-or-unlock-my-password-for-a-work-or-school-account).
* [**Cómo funciona** ](active-directory-passwords-how-it-works.md) -conocer Hola seis diferentes componentes de servicio de Hola y lo que hace cada uno
* [**Introducción a** ](active-directory-passwords-getting-started.md) -Obtenga información acerca de cómo tooallow los usuarios tooreset y cambiar sus contraseñas en la nube o local
* [**Personalizar** ](active-directory-passwords-customize.md) : Obtenga información acerca de cómo buscar toocustomize Hola & apariencia y comportamiento del programa Hola a las necesidades de organización tooyour de servicio
* [**Prácticas recomendadas** ](active-directory-passwords-best-practices.md) -Obtenga información acerca de cómo tooquickly implementar y administrar de forma eficaz las contraseñas de la organización
* [**Preguntas más frecuentes sobre** ](active-directory-passwords-faq.md) -Obtenga respuestas toofrequently preguntas más frecuentes
* [**Solución de problemas de** ](active-directory-passwords-troubleshoot.md) -Obtenga información acerca de cómo tooquickly solucionar problemas con el servicio de Hola
* [**Obtener más información** ](active-directory-passwords-learn-more.md) : vaya profundizar en los detalles técnicos de Hola de cómo funciona el servicio de Hola
