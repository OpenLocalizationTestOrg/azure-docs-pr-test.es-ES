---
title: "eventos de informe de auditoría de Active Directory aaaAzure | Documentos de Microsoft"
description: "Eventos auditados que están disponibles para ver y descargar desde Azure Active Directory"
services: active-directory
documentationcenter: 
author: dhanyahk
manager: femila
editor: 
ms.assetid: 307eedf7-05bc-448d-a84d-bead5a4c5770
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 06/16/2017
ms.author: dhanyahk;markvi
ms.openlocfilehash: 4a84cce2be56bde006164abf10ad1e72ca6e99bf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-audit-report-events"></a>Eventos del informe de auditoría de Azure Active Directory
*Esta documentación forma parte del programa Hola a [Azure Active Directory Reporting guía](active-directory-reporting-guide.md).*

Hola informe de auditoría de Azure Active Directory ayuda a los clientes a identificar las acciones con privilegios que se produzcan en su Azure Active Directory. Las acciones con privilegios incluyen cambios de elevación (por ejemplo, creación de roles o los restablecimientos de contraseña), cambiar las configuraciones de directiva (por ejemplo las directivas de contraseña), o la configuración de toodirectory de cambios (por ejemplo, configuración de federación de cambios toodomain). informes de Hello proporcionan registro de auditoría de Hola para nombre del evento hello, actor Hola que realiza la acción de hello, recurso de destino de hello afectado por el cambio de Hola y Hola fecha y hora (en UTC). Los clientes están lista de hello tooretrieve capaz de eventos de auditoría para su Azure Active Directory a través de hello [Portal de Azure](https://portal.azure.com/), tal y como se describe en [ver los registros de auditoría](active-directory-reporting-azure-portal.md).

## <a name="list-of-audit-report-events"></a>Lista de eventos del informe de auditoría
<!--- audit event descriptions should be in hello past tense --->

| Eventos | Descripción del evento |
| --- | --- |
| **Eventos de usuario** | |
| Agregar usuario |Agrega un directorio toohello de usuario. |
| Eliminar usuario |Eliminar un usuario del directorio de Hola. |
| Establecer propiedades de la licencia |Establecer propiedades de la licencia de Hola para un usuario en el directorio de Hola. |
| Restablecer contraseña de usuario |Restablecer la contraseña de Hola para un usuario en el directorio de Hola. |
| Cambiar la contraseña de usuario |Cambiar contraseña de Hola para un usuario en el directorio de Hola. |
| Cambiar la licencia de usuario |Cambiar una licencia de hello asignada a tooa usuario en el directorio de Hola. toosee qué licencias se han actualizado, busque en hello [actualizar usuario](#update-user-attributes) propiedades siguientes |
| Actualizar usuario |Actualiza un usuario en el directorio de Hola. [Consulte a continuación](#update-user-attributes) los atributos que se pueden actualizar. |
| Establecer el cambio forzado de la contraseña de usuario |Establecer propiedad de Hola que obliga a un usuario toochange su contraseña de inicio de sesión. |
| Actualizar credenciales de usuario |Contraseña de usuario Hola modificada |
| **Eventos de grupo** | |
| Agregar grupo |Crea un grupo en el directorio de Hola. |
| Actualizar grupo |Actualizar un grupo en el directorio de Hola. toosee se actualizaron las propiedades de grupo, consulte demasiado[audita el grupo de propiedades](#update-group-attributes) en la siguiente sección de Hola |
| Eliminar grupo |Eliminar un grupo del directorio de Hola. |
| CreateGroupSettings |Configuración de grupo creada. |
| UpdateGroupSettings |Configuración de grupo actualizada. toosee se actualizó la configuración de grupo, consulte demasiado[audita el grupo de propiedades](#update-group-attributes) en la siguiente sección de Hola |
| DeleteGroupSettings |Configuración de grupo eliminada. |
| SetGroupLicense |Establecer licencia de grupo. |
| SetGroupManagedBy |Establecer toobe grupo administrado por el usuario |
| AddGroupMember |Miembro agregado toogroup |
| RemoveGroupMember |Quitar miembro de grupo |
| AddGroupOwner |Propietario agregado toogroup |
| RemoveGroupOwner |Propietario quitado de grupo. |
| **Eventos de aplicación** | |
| Agregar entidad de servicio |Agrega un directorio toohello principal del servicio. |
| Quitar entidad de servicio |Quita a una entidad de servicio de directorio de Hola. |
| Agregar credenciales de la entidad de servicio |Entidad de servicio de tooa credenciales agregada. |
| Quitar credenciales de la entidad de servicio |Quitó las credenciales de una entidad de servicio. |
| Agregar entrada de delegación |Crea un [OAuth2PermissionGrant](https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/entity-and-complex-type-reference#oauth2permissiongrant-entity) en el directorio de Hola. |
| Establecer entrada de delegación |Actualiza un [OAuth2PermissionGrant](https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/entity-and-complex-type-reference#oauth2permissiongrant-entity) en el directorio de Hola. |
| Quitar entrada de delegación |Eliminar un [OAuth2PermissionGrant](https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/entity-and-complex-type-reference#oauth2permissiongrant-entity) en el directorio de Hola. |
| **Eventos de rol** | |
| Agregar la función miembro tooRole |Agrega un rol del directorio de tooa de usuario. |
| Quitar miembro de rol de Rol |Quitó un usuario de un rol del directorio. |
| AddRoleDefinition |Definición de rol agregada. |
| UpdateRoleDefinition |Definición de rol actualizada. toosee se actualizó la configuración de rol, consulte demasiado[auditar de propiedades de definición de rol](#update-role-definition-attributes) en la siguiente sección de Hola |
| DeleteRoleDefinition |Definición de rol eliminada. |
| AddRoleAssignmentToRoleDefinition |Agregar definición de toorole de asignación de roles. |
| RemoveRoleAssignmentFromRoleDefinition |Asignación de rol quitada de definición de rol. |
| AddRoleFromTemplate |Rola agregado desde plantilla. |
| UpdateRole |Rol actualizado. |
| AddRoleScopeMemberToRole |Agregar miembros con ámbito toorole. |
| RemoveRoleScopedMemberFromRole |Miembro con ámbito quitado de rol. |
| **Eventos de dispositivo (todos los eventos nuevos)** | |
| AddDevice |Dispositivo agregado. |
| UpdateDevice |Dispositivo actualizado. toosee se actualizaron las propiedades de dispositivo, consulte demasiado[propiedades del dispositivo auditada](#update-device-attributes) en la siguiente sección de Hola |
| DeleteDevice |Dispositivo eliminado. |
| AddDeviceConfiguration |Configuración de dispositivo agregada. |
| UpdateDeviceConfiguration |Configuración de dispositivo actualizada. toosee se actualizaron las propiedades de configuración de dispositivo, consulte demasiado[propiedades de configuración de dispositivo auditada](#update-device-configuration-attributes) en la siguiente sección de Hola |
| DeleteDeviceConfiguration |Configuración de dispositivo eliminada. |
| AddRegisteredOwner |Agregar toodevice propietario registrado. |
| AddRegisteredUsers |Agrega usuarios registrados toodevice. |
| RemoveRegisteredOwner |Quitar propietario registrado de dispositivo. |
| RemoveRegisteredUsers |Quitar usuarios registrados de dispositivo. |
| RemoveDeviceCredentials |Quitar credenciales de dispositivo. |
| **Eventos B2B** | |
| Invitaciones por lotes cargadas. |Un administrador ha cargado un archivo que contenga toobe invitaciones enviado toopartner a los usuarios. |
| Invitaciones por lotes procesadas. |Se ha procesado un archivo que contiene los usuarios toopartner de invitaciones. |
| Invitar a usuario externo. |Un usuario externo ha sido invitados toohello directory. |
| Canjear invitación a usuario externo. |Un usuario externo ha canjeado su directorio de toohello de invitación. |
| Agregar toogroup de usuario externo. |Un usuario externo se ha asignado el grupo de tooa de pertenencia en el directorio de Hola. |
| Asignar tooapplication de usuario externo. |Se ha asignado aplicación tooan de acceso directo a un usuario externo. |
| Creación de inquilinos viral. |Se creó un nuevo inquilino de Azure AD por canje de invitación de Hola. |
| Creación de usuarios viral. |Ha creado un usuario en un inquilino de Azure AD por canje de invitación de Hola. |
| **Unidades administrativas (todos los eventos nuevos)** | |
| AddAdministrativeUnit |Agregar unidad administrativa. |
| UpdateAdministrativeUnit |Actualizar unidad administrativa. toosee se actualizaron las propiedades de la unidad administrativa, consulte demasiado[propiedades de unidad administrativos audita](#update-administrative-unit-attributes) en la siguiente sección de Hola |
| DeleteAdministrativeUnit |Eliminar unidad administrativa. |
| AddMemberToAdministrativeUnit |Agregar miembro tooadministrative unidad. |
| RemoveMemberFromAdministrativeUnit |Quitar miembro de unidad administrativa. |
| **Eventos de directorio** | |
| Agregar toocompany de socios comerciales |Agrega un directorio de toohello asociado. |
| Quitar asociado de la compañía |Quitar a un socio de directorio Hola. |
| DemotePartner |Disminuir nivel de asociado. |
| Agregar dominio toocompany |Agrega un directorio de toohello de dominio. |
| Quitar dominio de la compañía |Quitar un dominio del directorio de Hola. |
|  Actualizar dominio |Actualizar un dominio en el directorio de Hola. toosee se actualizaron las propiedades de dominio, consulte demasiado[propiedades del dominio audita](#update-domain-attributes) en la siguiente sección de Hola |
| Establecer la autenticación de dominio |Cambiar configuración de dominio predeterminado de Hola para empresa Hola. |
| Establecer la información de contacto de la compañía |Establecer preferencias de contacto a nivel de compañía. Incluye direcciones de correo electrónico para marketing, así como  notificaciones técnicas sobre Microsoft Online Services. |
| Establecer la configuración de la federación en el dominio |Actualizar configuración de federación de Hola de un dominio. |
| Comprobar dominio |Comprobar un dominio en el directorio de Hola. |
| Comprobar dominio verificado por correo electrónico |Comprobar un dominio en el directorio de hello usando la comprobación de correo electrónico. |
| Establecer la marca DirSyncEnabled en la compañía |Establezca la propiedad de Hola que habilita un directorio en Azure AD Sync. |
| Establecer directiva de contraseñas |Estableció las restricciones de longitud y caracteres para las contraseñas de usuario. |
| Establecer información sobre la compañía |Información de nivel de empresa de hello actualizada. Vea hello [Get-MsolCompanyInformation](https://msdn.microsoft.com/library/azure/dn194126.aspx) cmdlet de PowerShell para obtener más detalles. |
| SetCompanyAllowedDataLocation |Establecer ubicación de datos permitida de empresa. |
| SetCompanyDirSyncEnabled |Establecer marca DirSyncEnabled. |
| SetCompanyDirSyncFeature |Establecer característica DirSync. |
| SetCompanyInformation |Establecer información sobre compañía. |
| SetCompanyMultiNationalEnabled |Establecer característica de empresa multinacional habilitada. |
| SetDirectoryFeatureOnTenant |Establecer característica de directorio en inquilino. |
| SetTenantLicenseProperties |Establecer propiedades de licencia de inquilino. |
| CreateCompanySettings |Crear configuración de compañía. |
| UpdateCompanySettings |Actualizar configuración de compañía. toosee se actualizaron las propiedades de la empresa, consulte demasiado[propiedades de la empresa audita](#update-company-attributes) en la siguiente sección de Hola |
| DeleteCompanySettings |Eliminar configuración de compañía. |
| SetAccidentalDeletionThreshold |Establecer umbral de eliminación accidental. |
| SetRightsManagementProperties |Establecer propiedades de administración de derechos. |
| PurgeRightsManagementProperties |Purgar propiedades de administración de derechos. |
| UpdateExternalSecrets |Actualizar secretos externos |
| **Eventos de directiva (todos los eventos nuevos)** | |
| AddPolicy |Agregar directiva. |
| UpdatePolicy |Actualizar directiva. |
| DeletePolicy |Eliminar directiva. |
| AddDefaultPolicyApplication |Agregar directiva tooapplication. |
| AddDefaultPolicyServicePrincipal |Agregar entidad de seguridad de directiva tooservice. |
| RemoveDefaultPolicyApplication |Quitar directiva de aplicación. |
| RemoveDefaultPolicyServicePrincipal |Quita directiva de entidad de servicio. |
| RemovePolicyCredentials |Quitar credenciales de directiva. |

## <a name="audit-report-retention"></a>Retención de informes de auditoría

Para hello información más reciente acerca de la retención, consulte [las directivas de retención de informes de Azure Active Directory](active-directory-reporting-retention.md).


Para clientes interesados en almacenar sus eventos de auditoría durante largos períodos de retención, hello API de informes puede ser eventos de auditoría de extracción tooregularly usado en un almacén de datos independiente. Vea [Getting Started with Hola API Reporting](active-directory-reporting-api-getting-started.md) para obtener más información.

## <a name="properties-included-with-each-audit-event"></a>Propiedades que se incluyen con cada evento de auditoría
| Propiedad | Description |
| --- | --- |
| Fecha y hora |fecha de Hola y hora en que Hola eventos de auditoría se ha producido |
| Actor |usuario de Hola o entidad de servicio que realiza la acción de Hola |
| Acción |acción de Hello realizada |
| Destino |usuario de Hola o entidad de servicio que se realizó la acción de hello en |

## <a name="update-user-attributes"></a>Atributos de "Actualizar usuario"
evento de auditoría de Hola "Update user" incluye información adicional sobre los atributos de usuario se actualizaron. Para cada atributo, ambos Hola valor anterior y nuevo valor de Hola se incluye.

| Atributo | Description |
| --- | --- |
| AccountEnabled |Hola usuario puede iniciar sesión. |
| AssignedLicense |Todas las licencias que se han asignado a toohello usuario. |
| AssignedPlan |Planes de servicio resultantes de licencias de hello asignan a toohello usuario. |
| LicenseAssignmentDetail |Obtener más información sobre licencias habían asignado a toohello usuario. Por ejemplo, si se participan basado en el grupo de licencias, esto incluiría grupo Hola Hola le concede la licencia. |
| Móvil |teléfono móvil del usuario de Hola. |
| OtherMail |Hola dirección de correo electrónico alternativa del usuario. |
| OtherMobile |Hola teléfono móvil del usuario. |
| StrongAuthenticationMethod |Una lista de métodos de comprobación configurado por el usuario de hello para la autenticación multifactor, como el código de llamada de voz, SMS o comprobación desde una aplicación móvil. |
| StrongAuthenticationRequirement |Si Multi-Factor Authentication se exige, habilita o deshabilita para este usuario. |
| StrongAuthenticationUserDetails |usuario de Hello correo electrónico y número de teléfono alternativo, número de teléfono dirección se usa para la autenticación multifactor y comprobación de restablecimiento de contraseña. |
| StrongAuthenticationPhoneAppDetail |Aplicaciones de detalle forof phone registrado el inicio de sesión de tooperform 2FA |
| TelephoneNumber |número de teléfono del usuario de Hola. |
| AlternativeSecurityId |Un identificador de seguridad alternativo para el objeto de Hola. |
| CreationType |Método de creación de usuario de hello (ya sea mediante invitación o virales). |
| InviteTicket |Lista de vales de invitación para usuario Hola. |
| InviteReplyUrl |Lista de direcciones URL tooreply tras la aceptación de la invitación. |
| InviteResources |Lista de los usuarios de recursos toowhich Hola se ha invitado. |
| LastDirSyncTime |Última hora de hello objeto se actualizó debido a sincronizar de hello autoritativo (cliente local) directory. |
| MSExchRemoteRecipientType |Asigna los tipos de destinatario tooMSO. Consulte demasiado https://msdn.microsoft.com/library/microsoft.office.interop.outlook.recipient.type.aspx [tipos de destinatarios de MSO] para los tipos de destinatario |
| PreferredDataLocation |Hola preferiblemente del usuario de hello, del grupo, del contacto, de la carpeta pública o datos del dispositivo. |
| ProxyAddresses |dirección de Hola por el que se reconoce un objeto de destinatario de Exchange Server en un sistema de correo electrónico externa. |
| StsRefreshTokensValidFrom |Lleva información de revocación del token de actualización (se considera que los tokens de actualización de STS emitidos antes este momento han expirado). |
| UserPrincipalName |Hola UPN que es un nombre de inicio de sesión estilo Internet para un usuario. |
| UserState |Estado de usuario PendingApproval/PendingAcceptance/Accepted/PendingVerification. |
| UserStateChangedOn |Marca de tiempo del último tooUserState de cambio. Usar flujos de trabajo de tootrigger del ciclo de vida. |
| UserType |Tipo de usuario. Miembro (0), Invitado (1), Viral (2). |

## <a name="update-group-attributes"></a>Atributos de "Actualizar grupo"
| Atributo | Description |
| --- | --- |
| Clasificación |clasificación de Hola para un grupo unificado (HBI, MBI, etcetera). |
| Descripción |Frases descriptivos legible para el usuario sobre el objeto de Hola. |
| DisplayName |nombre para mostrar de un objeto Hola |
| DirSyncEnabled |Indica si la sincronización se produce desde un directorio relevante (cliente, local). |
| GroupLicenseAssignment |Asignación de licencias de un grupo |
| GroupType |Tipo de grupo, unificado (0) |
| IsMembershipRuleLocked |Indica que hello MembershipRule propiedad se establece por el servicio de administración de grupos de autoservicio de hello y no se puede cambiar los usuarios. Toogroups solo es aplicable cuando GroupType incluya GroupType.DynamicMembership |
| IsPublic |Marca tooindicate si el grupo de hello es pública y privada. |
| LastDirSyncTime |Última hora de hello actualización del objeto como resultado de la sincronización de hello autoritativo (cliente local) directory. |
| Mail |Dirección de correo electrónico principal |
| MailEnabled |Indica si este grupo tiene funcionalidad de correo electrónico. |
| MailNickname |Moniker para un objeto de la libreta de direcciones, que suele ser parte de Hola de su nombre de correo electrónico anterior Hola "@" símbolos. |
| MembershipRule |Una cadena de criterios de hello utilizado por toodetermine de servicio de administración de grupos de autoservicio de Hola de expresar los miembros deben pertenecer toothis grupo. Consulte también IsMembershipRuleLocked. Donde GroupType incluye GroupType.DynamicMembership un toogroups solo es aplicable. |
| MembershipRuleProcessingState |Un valor de enumeración definido por el servicio de administración de grupos de autoservicio de hello definir estado de Hola de procesamiento para este grupo de pertenencia. Donde GroupType incluye GroupType.DynamicMembership un toogroups solo es aplicable. |
| ProxyAddresses |dirección de Hola por el que se reconoce un objeto de destinatario de Exchange Server en un sistema de correo electrónico externa. |
| RenewedDateTime |Registro de marca de tiempo de cuándo fue la última vez que se renovó un grupo. |
| SecurityEnabled |Indica si la pertenencia a grupo de hello puede influir en las decisiones de autorización. |
| WellKnownObject |Etiqueta un objeto de directorio, que lo designa como uno de un conjunto predefinido. |

## <a name="update-device-attributes"></a>Atributos de "Actualizar dispositivo"
| Atributo | Description |
| --- | --- |
| AccountEnabled |Indica si se puede autenticar una entidad de seguridad. |
| CloudAccountEnabled |Indica si se puede autenticar una entidad de seguridad. Escribe InTune cuando el dispositivo de Hola se controla de manera local. |
| CloudDeviceOSType |Tipo de dispositivo de hello en función de hello SO, por ejemplo, Windows RT, iOS. Cuando se establece por un servicio de nube (por ejemplo, Intune), este atributo se convierte en autoritativo en el directorio de Hola para DeviceOSType. |
| CloudDeviceOSVersion |Versión de SO Hola. Cuando se establece por un servicio de nube (por ejemplo, Intune), este atributo se convierte en autoritativo en el directorio de Hola para DeviceOSVersion. |
| CloudDisplayName |Valor del atributo LDAP de hello displayName. Cuando se establece por un servicio de nube (por ejemplo, Intune), este atributo se convierte en autoritativo en directorio de Hola de displayName. |
| CloudCreated |Indica si el objeto de hello fue creado por servicios en la nube. |
| CompliantUntil |Hasta qué momento el dispositivo se considera compatible. |
| DeviceMetadata |Metadatos personalizados para el dispositivo de Hola |
| DeviceObjectVersion |Este atributo es la versión del esquema tooidentify usado hello de dispositivo de Hola. |
| DeviceOSType |Tipo de dispositivo de hello en función de hello SO, por ejemplo, Windows RT, iOS. Escribiendo hello servicio de registro y toobe previsto actualizan Hola servicio de administración de MDM o STS claro el servicio de administración. |
| DeviceOSVersion |Versión de SO Hola. Escribiendo hello servicio de registro y toobe previsto actualizan Hola servicio de administración de MDM o STS claro el servicio de administración. |
| DevicePhysicalIds |Atributo multivalor pensado toostore identificadores de dispositivo físico de Hola. Esto puede incluir identificadores de BIOS, huellas digitales de TPM, identificadores específicos del hardware, etc. |
| DirSyncEnabled |Indica si la sincronización se produce desde un directorio relevante (cliente, local). |
| DisplayName |nombre para mostrar de un objeto Hola |
| IsCompliant |Este atributo es toomanage usado Hola el estado de administración de dispositivos móviles del dispositivo de Hola. |
| IsManaged |Este atributo se usa dispositivos de hello tooindicate está administrado por una nube de MDM. |
| LastDirSyncTime |Última hora de hello objeto se actualizó debido a sincronizar de hello autoritativo (cliente local) directory. |

## <a name="update-device-configuration-attributes"></a>Atributos de "Actualizar configuración de dispositivo"
| Atributo | Description |
| --- | --- |
| MaximumRegistrationInactivityPeriod |número máximo de Hola de días de un dispositivo puede estar inactivo antes de que se considere para su eliminación. |
| RegistrationQuota |Directiva de usa toolimit Hola un número de registros de dispositivos permitido para un único usuario. |

## <a name="update-service-principal-configuration-attributes"></a>Atributos de "Actualizar configuración de entidad de servicio"
| Atributo | Description |
| --- | --- |
| AccountEnabled |Indica si se puede autenticar una entidad de seguridad. |
| AppPrincipalId |Identidad externa y definida por la aplicación para una entidad de seguridad. |
| DisplayName |nombre para mostrar de un objeto Hola |
| ServicePrincipalName |Un nombre principal de servicio, que contiene "nombre/authority" donde name especifica un valor de la clase de aplicación y entidad contiene al menos nombre de host [: puerto] o "name" que especifica un identificador de entidad de servicio de Hola. |

## <a name="update-app-attributes"></a>Atributos de "Actualizar aplicación"
| Atributo | Description |
| --- | --- |
| AppAddress |conjunto de Hola de direcciones (redirigir direcciones URL) que se asignan a tooa entidad de servicio. |
| AppId |Identificador de aplicación de la aplicación hello |
| AppIdentifierUri |URI de aplicación, que identifica la aplicación hello.  Normalmente es la dirección URL de la aplicación hello acceso. |
| AppLogoUrl |Hola dirección url de imagen de logotipo de aplicación Hola almacenada en una red CDN. |
| AvailableToOtherTenants |Aplicación hello True es aplicación multiempresa (es decir, puede utilizar otros inquilinos). |
| DisplayName |nombre para mostrar Hello para un nombre de aplicación |
| Entitlement |Lista de derechos de la aplicación. |
| ExternalUserAccountDelegationsAllowed |Marca que indica si una aplicación de recursos es da confianza y puede crear entradas de delegación para cuentas de usuario externas. |
| GroupMembershipClaims |Directiva de notificaciones de pertenencia de grupos de Hola. |
| PublicClient |True si el cliente de hello no se puede mantener en secreto (es decir, el cliente no confidencial de OAuth2.0) |
| RecordConsentConditions |Tipos de condiciones de consentimiento, tal como se define por hello términos del contrato: ninguno (0), SilentConsentForPartnerManagedApp(1). Este valor se expondrá en el esquema de la API de gráficos de Hola y solo se pueden establecer o cambiar por administradores de inquilinos. |
| RequiredResourceAccess |Contenido XML de un valor de propiedad RequiredResourceAccess Hola. |
| WebApp |Si es true, indica que esta aplicación es una aplicación web. |
| WwwHomepage |página Web principal de Hola. |

## <a name="update-role-attributes"></a>Atributos de "Actualizar rol"
| Atributo | Description |
| --- | --- |
| AppAddress |conjunto de Hola de direcciones (redirigir direcciones URL) que se asignan a tooa entidad de servicio. |
| BelongsToFirstLoginObjectSet |Si es true, indica que pertenece este objeto de conjunto de toohello de inicio de sesión de objetos tooenable necesarios de hello primer administrador de un nuevo inquilino. |
| Builtin |Indica si el sistema de hello pertenece duración Hola de un objeto. |
| Descripción |Frases descriptivos legible para el usuario sobre el objeto de Hola. |
| DisplayName |nombre para mostrar de un objeto Hola |
| MailNickname |Moniker para un objeto de la libreta de direcciones, que suele ser parte de Hola de su nombre de correo electrónico anterior Hola "@" símbolos. |
| RoleDisabled |Indica si se debe omitir el rol de Hola para fines de comprobaciones de acceso. |
| RoleTemplateId |Identidad de plantilla de rol de Hola. |
| ServiceInfo |Información que se puede utilizar en otras instancias de servicios o MOAC de aprovisionamiento específico de servicio (de hello iguales o distinto tipos de servicio). |
| TaskSetScopeReference |Identifica una instancia de TaskSet y un conjunto de ámbitos asociados a un rol o RoleTemplate. |
| ValidationError |Información publicada por un servicio federado que describe un error no transitorio, específicos del servicio con respecto a las propiedades de Hola o vínculo desde un tooresolve de acción del Administrador de objetos. |
| WellKnownObject |Etiqueta un objeto de directorio, que lo designa como uno de un conjunto predefinido. |

## <a name="update-role-definition-attributes"></a>Atributos de "Actualizar definición de rol"
| Atributo | Description |
| --- | --- |
| Ámbitos asignables |Colección de ámbitos de autorización que se puede hacer referencia al asignar a esta entidad de seguridad de tooa RoleDefinition. |
| DisplayName |nombre para mostrar de un objeto Hola |
| GrantedPermissions |Permisos otorgados por esta propiedad RoleDefinition. |

## <a name="update-administrative-unit-attributes"></a>Atributos de "Actualizar unidad administrativa"
| Atributo | Description |
| --- | --- |
| Descripción |Esta propiedad se actualiza cuando se cambia la descripción de Hola de una unidad administrativa. |
| DisplayName |Esta propiedad se actualiza cuando se cambia el nombre de Hola de una unidad administrativa. |

## <a name="update-company-attributes"></a>Atributos de "Actualizar empresa"
| Atributo | Description |
| --- | --- |
| AllowedDataLocation |Una ubicación en qué Hola los usuarios de la compañía pueden toobe aprovisionado. |
| AuthorizedServiceInstance |Nombres de toowhich de instancias de servicio que se puede implementar un plan. |
| DirSyncEnabled |Indica si la sincronización se produce desde un directorio relevante (cliente, local). |
| DirSyncStatus |Indica si se produce la sincronización de objetos de la libreta de direcciones en este contexto de inquilino de un autoridad (cliente, de manera local) directorio; una expansión de hello DirSyncEnabled propiedad en los objetos de la empresa. |
| DirSyncFeatures |Bit marca tookeep un seguimiento de conjunto de características de dirsync habilitados y deshabilitados para el inquilino de Hola. |
| DirectoryFeatures |Características del directorio habilitadas o deshabilitadas. |
| DirSyncConfiguration |Contiene a todos los inquilinos actual de DirSync configuración toohello específico. |
| DisplayName |nombre para mostrar de un objeto Hola |
| IsMnc |Una empresa de hello marca booleana conjunto demasiado "true" Si está habilitada para la característica de empresa multinacional de Hola. |
| ObjectSettings |Una colección de configuración del ámbito del objeto de hello toohello aplicables. |
| PartnerCommerceUrl |Sitio de comercio del socio de dirección URL toohello. |
| PartnerHelpUrl |Sitio de Ayuda de dirección URL toohello asociado. |
| PartnerSupportEmail |Correo electrónico de soporte técnico del asociado de dirección URL toohello. |
| PartnerSupportTelephone |Teléfono de soporte técnico del asociado de dirección URL toohello. |
| PartnerSupportUrl |Sitio de soporte técnico del asociado de dirección URL toohello. |
| StrongAuthenticationDetails |Detalles relacionados con la tooStrongAuthentication. |
| StrongAuthenticationPolicy |Directiva de autenticación sólida para la compañía Hola. |
| TechnicalNotificationMail |Correo electrónico dirección toonotify problemas técnicos relativos tooa empresa. |
| TelephoneNumber |Números de teléfono que cumplen con hello ITU recomendación E.123. |
| TenantType |tipo de Hola de inquilinos. Si no se especifica este valor, el inquilino de hello es una empresa. De lo contrario, los posibles valores son: MicrosoftSupport (0), SyndicatePartner (1), BreadthPartner (2) BreadthPartnerDelegatedAdmin (3) ResellerPartnerDelegatedAdmin (4) ValueAddedResellerPartnerDelegatedAdmin (5). |
| VerifiedDomain |Un conjunto de nombres de dominio DNS enlaza tooa empresa. |

## <a name="update-domain-attributes"></a>Atributos de "Actualizar dominio"
| Atributo | Description |
| --- | --- |
| Capacidades |Los marcadores de bits que describe las capacidades de hello del dominio de hello, si lo hay. |
| Valor predeterminado |Indica si el dominio de hello es valor predeterminado de hello; Por ejemplo, hello UserPrincipalName sufijo predeterminado cuando un administrador crea un nuevo usuario en MOAC. |
| Inicial |Indica si el dominio de hello es inicial del dominio de empresa de hello, Hola asignadas por OCP. dominio inicial de Hello es un subdominio único de un dominio de Microsoft Online; e.g.contoso3.microsoftonline.com. |
| LiveType |Tipo de hello Windows Live espacio de nombres correspondiente, si existe. |
| Nombre |Identificador de punto de conexión de Hola. |
| PasswordNotificationWindowDays |se notifica el número de Hola de días antes de que una contraseña expire usuario Hola. |
| PasswordValidityPeriodDays |Hola número de días que es adecuada para una contraseña antes de que deba cambiarse. |

Los registros de auditoría son un control necesario para muchas regulaciones de conformidad. Para los clientes que usan hello Azure Active Directory Audit informe toomeet sus normas de cumplimiento, se recomienda ese cliente hello enviar una copia de este tema de ayuda con copia de Hola del cliente de hello exporta informe de auditoría toohelp explican informe Hola detalles. Si auditor Hola desearía toounderstand Hola Reglamentos que Azure actualmente cumple, dirigir Hola auditor toohello [página de cumplimiento normativo](https://azure.microsoft.com/support/trust-center/compliance/) de hello Microsoft Azure Trust Center.

