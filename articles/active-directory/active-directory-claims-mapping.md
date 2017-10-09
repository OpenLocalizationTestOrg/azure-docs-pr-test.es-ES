---
title: "Asignación de notificaciones en Azure Active Directory (versión preliminar pública) | Microsoft Docs"
description: "En esta página se describe la asignación de notificaciones de Azure Active Directory."
services: active-directory
author: billmath
manager: femila
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/14/2017
ms.author: billmath
ms.openlocfilehash: ff07b9954d5c2ce71ab0ffd0db49fde15f323586
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="claims-mapping-in-azure-active-directory-public-preview"></a>Asignación de notificaciones en Azure Active Directory (versión preliminar pública)

>[!NOTE]
>Esta característica reemplaza y reemplaza a hello [notificaciones personalización](https://docs.microsoft.com/azure/active-directory/develop/active-directory-saml-claims-customization) ofrecen a través de portal de hello hoy en día. Si personaliza notificaciones mediante el portal de hello además toohello método gráfico/PowerShell detalla en este documento en hello misma aplicación, los tokens emitidos para esa aplicación pasará por alto la configuración de hello en el portal de Hola.
Las configuraciones realizadas a través de métodos de hello detallados en este documento no se verán reflejadas en el portal de Hola.

Esta característica se usa por inquilino administradores toocustomize Hola notificaciones emitidos en tokens para una aplicación específica en su inquilino. Puede usar directivas de asignación de notificaciones para:

- Seleccionar las notificaciones que se incluyen en tokens.
- Crear tipos de notificación que aún no existen.
- Elegir o cambiar origen de Hola de datos que se emite en notificaciones específicas.

>[!NOTE]
>Esta funcionalidad se encuentra actualmente en versión preliminar pública. Prepararán toorevert o quitar los cambios. Hola característica está disponible en ninguna suscripción de Azure Active Directory (Azure AD) durante la vista previa pública. Sin embargo, cuando característica Hola deja de estar disponible con carácter general, algunos aspectos de la característica de hello pueden requerir una suscripción premium a Azure Active Directory.

## <a name="claims-mapping-policy-type"></a>Tipo de directiva de asignación de notificaciones
En Azure AD, un objeto de **directiva** representa un conjunto de reglas que se exigen en algunas o todas las aplicaciones de una organización. Cada tipo de directiva tiene una estructura única, con un conjunto de propiedades que son, a continuación, aplica toowhich tooobjects que están asignados.

Notificaciones de una asignación de directiva es un tipo de **directiva** objeto que modifica Hola notificaciones emite en los tokens emitidos para aplicaciones específicas.

## <a name="claim-sets"></a>Conjuntos de notificaciones
Hay determinados conjuntos de notificaciones que definen cómo y cuándo se usan en los tokens.

### <a name="core-claim-set"></a>Conjunto de notificaciones principales
Notificaciones en core Hola notificaciones están presentes en cada token, independientemente de la directiva. Estas notificaciones se consideran también restringidas y no se pueden modificar.

### <a name="basic-claim-set"></a>Conjunto de notificaciones básicas
conjunto de notificaciones básico de Hello incluye notificaciones de Hola que se emiten de forma predeterminada para los tokens (en el conjunto de notificaciones de adición toohello core). Estas notificaciones se omite o modificar mediante las directivas de asignación de notificaciones de Hola.

### <a name="restricted-claim-set"></a>Conjunto de notificaciones restringidas
Las notificaciones restringidas no se pueden modificar mediante una directiva. no se puede cambiar el origen de datos de Hola y ninguna transformación se aplica al generar estas notificaciones.

#### <a name="table-1-json-web-token-jwt-restricted-claim-set"></a>Tabla 1: Conjunto de notificaciones restringidas de JSON Web Token (JWT)
|Tipo de notificación (nombre)|
| ----- |
|_claim_names|
|_claim_sources|
|access_token|
|account_type|
|acr|
|actor|
|actortoken|
|aio|
|altsecid|
|amr|
|app_chain|
|app_displayname|
|app_res|
|appctx|
|appctxsender|
|appid|
|appidacr|
|Aserción|
|at_hash|
|aud|
|auth_data|
|auth_time|
|authorization_code|
|azp|
|azpacr|
|c_hash|
|ca_enf|
|cc|
|cert_token_use|
|client_id|
|cloud_graph_host_name|
|cloud_instance_name|
|cnf|
|código|
|controls|
|credential_keys|
|csr|
|csr_type|
|deviceid|
|dns_names|
|domain_dns_name|
|domain_netbios_name|
|e_exp|
|email|
|endpoint|
|enfpolids|
|exp|
|expires_on|
|grant_type|
|graph|
|group_sids|
|groups|
|hasgroups|
|hash_alg|
|home_oid|
|http://schemas.microsoft.com/ws/2008/06/identity/claims/authenticationinstant|
|http://schemas.microsoft.com/ws/2008/06/identity/claims/authenticationmethod|
|http://schemas.microsoft.com/ws/2008/06/identity/claims/expiration|
|http://schemas.microsoft.com/ws/2008/06/identity/claims/expired|
|http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress|
|http://schemas.xmlsoap.org/ws/2005/05/identity/claims/name|
|http://schemas.xmlsoap.org/ws/2005/05/identity/claims/nameidentifier|
|iat|
|identityprovider|
|idp|
|in_corp|
|instance|
|ipaddr|
|isbrowserhostedapp|
|iss|
|jwk|
|key_id|
|key_type|
|mam_compliance_url|
|mam_enrollment_url|
|mam_terms_of_use_url|
|mdm_compliance_url|
|mdm_enrollment_url|
|mdm_terms_of_use_url|
|nameid|
|nbf|
|netbios_name|
|valor de seguridad|
|oid|
|on_prem_id|
|onprem_sam_account_name|
|onprem_sid|
|openid2_id|
|Contraseña|
|platf|
|polids|
|pop_jwk|
|preferred_username|
|previous_refresh_token|
|primary_sid|
|puid|
|pwd_exp|
|pwd_url|
|redirect_uri|
|refresh_token|
|refreshtoken|
|request_nonce|
|resource|
|role|
|roles|
|ámbito|
|scp|
|sid|
|signature|
|signin_state|
|src1|
|src2|
|sub|
|tbid|
|tenant_display_name|
|tenant_region_scope|
|thumbnail_photo|
|tid|
|tokenAutologonEnabled|
|trustedfordelegation|
|unique_name|
|upn|
|user_setting_sync_url|
|nombre de usuario|
|uti|
|ver|
|verified_primary_email|
|verified_secondary_email|
|wids|
|win_ver|

#### <a name="table-2-security-assertion-markup-language-saml-restricted-claim-set"></a>Tabla 2: Conjunto de notificaciones restringidas de Lenguaje de marcado de aserción de seguridad (SAML)
|Tipo de notificación (URI)|
| ----- |
|http://schemas.microsoft.com/ws/2008/06/identity/claims/expiration|
|http://schemas.microsoft.com/ws/2008/06/identity/claims/expired|
|http://schemas.microsoft.com/identity/claims/accesstoken|
|http://schemas.microsoft.com/identity/claims/openid2_id|
|http://schemas.microsoft.com/identity/claims/identityprovider|
|http://schemas.microsoft.com/identity/claims/objectidentifier|
|http://schemas.microsoft.com/identity/claims/puid|
|http://schemas.xmlsoap.org/ws/2005/05/identity/claims/nameidentifier[MR1] |
|http://schemas.microsoft.com/identity/claims/tenantid|
|http://schemas.microsoft.com/ws/2008/06/identity/claims/authenticationinstant|
|http://schemas.microsoft.com/ws/2008/06/identity/claims/authenticationmethod|
|http://schemas.microsoft.com/accesscontrolservice/2010/07/claims/identityprovider|
|http://schemas.microsoft.com/ws/2008/06/identity/claims/groups|
|http://schemas.microsoft.com/claims/groups.link|
|http://schemas.microsoft.com/ws/2008/06/identity/claims/role|
|http://schemas.microsoft.com/ws/2008/06/identity/claims/wids|
|http://schemas.microsoft.com/2014/09/devicecontext/claims/iscompliant|
|http://schemas.microsoft.com/2014/02/devicecontext/claims/isknown|
|http://schemas.microsoft.com/2012/01/devicecontext/claims/ismanaged|
|http://schemas.microsoft.com/2014/03/psso|
|http://schemas.microsoft.com/claims/authnmethodsreferences|
|http://schemas.xmlsoap.org/ws/2009/09/identity/claims/actor|
|http://schemas.microsoft.com/ws/2008/06/identity/claims/samlissuername|
|http://schemas.microsoft.com/ws/2008/06/identity/claims/confirmationkey|
|http://schemas.microsoft.com/ws/2008/06/identity/claims/windowsaccountname|
|http://schemas.microsoft.com/ws/2008/06/identity/claims/primarygroupsid|
|http://schemas.microsoft.com/ws/2008/06/identity/claims/primarysid|
|http://schemas.xmlsoap.org/ws/2005/05/identity/claims/authorizationdecision|
|http://schemas.xmlsoap.org/ws/2005/05/identity/claims/authentication|
|http://schemas.xmlsoap.org/ws/2005/05/identity/claims/sid|
|http://schemas.microsoft.com/ws/2008/06/identity/claims/denyonlyprimarygroupsid|
|http://schemas.microsoft.com/ws/2008/06/identity/claims/denyonlyprimarysid|
|http://schemas.xmlsoap.org/ws/2005/05/identity/claims/denyonlysid|
|http://schemas.microsoft.com/ws/2008/06/identity/claims/denyonlywindowsdevicegroup|
|http://schemas.microsoft.com/ws/2008/06/identity/claims/windowsdeviceclaim|
|http://schemas.microsoft.com/ws/2008/06/identity/claims/windowsdevicegroup|
|http://schemas.microsoft.com/ws/2008/06/identity/claims/windowsfqbnversion|
|http://schemas.microsoft.com/ws/2008/06/identity/claims/windowssubauthority|
|http://schemas.microsoft.com/ws/2008/06/identity/claims/windowsuserclaim|
|http://schemas.xmlsoap.org/ws/2005/05/identity/claims/x500distinguishedname|
|http://schemas.xmlsoap.org/ws/2005/05/identity/claims/upn|
|http://schemas.microsoft.com/ws/2008/06/identity/claims/groupsid|
|http://schemas.xmlsoap.org/ws/2005/05/identity/claims/spn|
|http://schemas.microsoft.com/ws/2008/06/identity/claims/ispersistent|
|http://schemas.xmlsoap.org/ws/2005/05/identity/claims/privatepersonalidentifier|
|http://schemas.microsoft.com/identity/claims/scope|

## <a name="claims-mapping-policy-properties"></a>Propiedades de la directiva de asignación de notificaciones
Utilizar propiedades de Hola de una asignación de directiva toocontrol se emiten las notificaciones y donde se origen datos Hola de notificaciones. Si no se establece ninguna directiva, sistema Hola emite tokens que contiene el conjunto de notificaciones de núcleo de hello, conjunto de notificaciones de hello básico y las notificaciones opcionales que Hola aplicación elegida tooreceive.

### <a name="include-basic-claim-set"></a>Inclusión del conjunto de notificaciones básicas

**Cadena:** IncludeBasicClaimSet

**Tipo de datos:** valor booleano (True o False)

**Resumen:** esta propiedad determina si el conjunto de notificaciones básico de Hola se incluye en tokens afectados por esta directiva. 

- Si set tooTrue, todas las notificaciones en el conjunto de notificaciones básico de Hola se emite en símbolos (tokens), afectadas por la directiva de Hola. 
- Si tooFalse de conjunto, las notificaciones en el conjunto de notificaciones básico de hello no está en tokens de hello, a menos que se individualmente agreguen en hello notificaciones esquema propiedad de hello misma directiva.

>[!NOTE] 
>Notificaciones en core Hola notificaciones están presentes en cada token, independientemente de lo que esta propiedad se establece en conjunto. 

### <a name="claims-schema"></a>Esquema de notificaciones

**Cadena:** ClaimsSchema

**Tipo de datos:** blob de JSON con una o más entradas de esquema de notificación

**Resumen:** esta propiedad define qué notificaciones están presentes en tokens de hello afectados por la directiva de hello, además el conjunto de notificaciones toohello básica y conjunto de notificaciones de núcleo de Hola.
Para cada entrada de esquema de notificación definida en esta propiedad, se requiere cierta información. Debe especificar de donde provienen los datos de hello (**valor** o **par origen/identificador**), y que los datos de Hola de notificación se emite como (**tipo de notificación de**).

### <a name="claim-schema-entry-elements"></a>Elementos de entrada de esquema de notificación

**Valor:** Value (elemento) Hola define un valor estático como Hola datos toobe emitida en hello notificación.

**Par de origen/ID:** Hola origen y un identificador elementos definen donde tiene como el origen de datos hello en hello notificación de. 

elemento de origen de Hello debe establecerse tooone de siguientes hello: 


- "usuario": datos de Hola Hola de notificación es una propiedad de objeto de usuario de Hola. 
- "aplicación": datos de Hola Hola de notificación es una propiedad de entidad de servicio de aplicación (cliente) de Hola. 
- "recurso": datos de Hola Hola de notificación es una propiedad de entidad de servicio de recurso de Hola.
- "público": datos hello en hello notificación están una propiedad de entidad de seguridad de servicio de hello es Hola audiencia del token de hello (ya sea Hola cliente o recurso de entidad de servicio).
- "company": datos de Hola Hola de notificación es una propiedad de objeto de empresa del inquilino de hello recursos.
- "transformación": datos de Hola Hola de notificación es de transformación de notificaciones (vea la sección de Hola "transformación de notificaciones" más adelante en este artículo). 

Si el origen de hello es la transformación, Hola **TransformationID** elemento debe incluirse en esta definición de la notificación.

elemento de identificador de Hello identifica qué propiedad de origen de hello proporciona el valor de Hola para notificación de Hola. Hello siguiente tabla enumera los valores de hello de Id. válido para cada valor de origen.

#### <a name="table-3-valid-id-values-per-source"></a>Tabla 3: Valores de ID válidos por origen
|Origen|ID|Descripción|
|-----|-----|-----|
|Usuario|surname|Nombre de familia|
|Usuario|givenname|Nombre propio|
|Usuario|displayname|Display Name (Nombre para mostrar)|
|Usuario|objectid|ObjectID|
|Usuario|mail|Dirección de correo electrónico|
|Usuario|userprincipalname|Nombre principal de usuario|
|Usuario|department|department|
|Usuario|onpremisessamaccountname|Nombre de cuenta SAM local|
|Usuario|netbiosname|Nombre de NetBios|
|Usuario|dnsdomainname|Nombre de dominio DNS|
|Usuario|onpremisesecurityidentifier|Identificador de seguridad local|
|Usuario|companyname|Nombre de la organización|
|Usuario|streetaddress|Dirección|
|Usuario|postalcode|Código postal|
|Usuario|preferredlanguange|Idioma preferido|
|Usuario|onpremisesuserprincipalname|UPN local|
|Usuario|mailNickname|Alias de correo|
|Usuario|extensionattribute1|Atributo de extensión 1|
|Usuario|extensionattribute2|Atributo de extensión 2|
|Usuario|extensionattribute3|Atributo de extensión 3|
|Usuario|extensionattribute4|Atributo de extensión 4|
|Usuario|extensionattribute5|Atributo de extensión 5|
|Usuario|extensionattribute6|Atributo de extensión 6|
|Usuario|extensionattribute7|Atributo de extensión 7|
|Usuario|extensionattribute8|Atributo de extensión 8|
|Usuario|extensionattribute9|Atributo de extensión 9|
|Usuario|extensionattribute10|Atributo de extensión 10|
|Usuario|extensionattribute11|Atributo de extensión 11|
|Usuario|extensionattribute12|Atributo de extensión 12|
|Usuario|extensionattribute13|Atributo de extensión 13|
|Usuario|extensionattribute14|Atributo de extensión 14|
|Usuario|extensionattribute15|Atributo de extensión 15|
|Usuario|othermail|Otro correo|
|Usuario|country|País|
|Usuario|city|City|
|Usuario|state|Estado|
|Usuario|jobtitle|Puesto|
|Usuario|employeeid|Id. de empleado|
|Usuario|facsimiletelephonenumber|Número de teléfono de fax|
|application, resource, audience|displayname|Display Name (Nombre para mostrar)|
|application, resource, audience|objected|ObjectID|
|application, resource, audience|etiquetas|Etiqueta de entidad de servicio|
|Compañía|tenantcountry|País del inquilino|

**TransformationID:** elemento TransformationID de hello debe proporcionarse la solo si hello elemento de origen se establece demasiado "transformación".

- Este elemento debe coincidir con el elemento de identificador de Hola de entrada de transformación de hello en hello **ClaimsTransformation** propiedad que define cómo se generan datos de Hola para esta notificación.

**Tipo de notificación:** hello **JwtClaimType** y **SamlClaimType** que notificación esta entrada de esquema de notificación se refiere a los elementos definen.

- Hola JwtClaimType debe contener el nombre de Hola de hello notificación toobe emitida en los Jwt.
- Hola SamlClaimType debe contener Hola URI de hello notificación toobe emite en tokens SAML.

>[!NOTE]
>Nombres e identificadores URI de notificaciones de hello restringido no se puede usar el conjunto de elementos de tipo de notificación de Hola de notificación. Para obtener más información, vea la sección de "Excepciones y restricciones" de hello más adelante en este artículo.

### <a name="claims-transformation"></a>Transformación de notificaciones

**Cadena:** ClaimsTransformation

**Tipo de datos:** blob de JSON, con una o más entradas de transformación 

**Resumen:** usar esta propiedad tooapply transformaciones toosource los datos comunes, datos de salida de hello toogenerate para notificaciones se especifican en Hola esquema de notificaciones.

**Id.:** uso Hola ID elemento tooreference esta entrada de transformación en hello entrada de esquema de notificaciones de TransformationID. Este valor debe ser único para cada entrada de transformación comprendida en la directiva.

**TransformationMethod:** elemento de TransformationMethod de hello identifica qué operación es toogenerate realizada Hola datos para notificación de Hola.

En función de método hello elegido, se espera que un conjunto de entradas y salidas. Se definen mediante el uso de hello **InputClaims**, **InputParameters** y **OutputClaims** elementos.

#### <a name="table-4-transformation-methods-and-expected-inputs-and-outputs"></a>Tabla 4: Métodos de transformación y entradas y salidas previstas
|TransformationMethod|Entrada prevista|Salida prevista|Descripción|
|-----|-----|-----|-----|
|Unión|string1, string2, separator|outputClaim|Se combinan las cadenas de entrada mediante un separador entre ellas. Por ejemplo: string1:"foo@bar.com" , string2:"sandbox" , separator:"." da como resultado outputClaim:"foo@bar.com.sandbox"|
|ExtractMailPrefix|mail|outputClaim|Extrae la parte local de Hola de una dirección de correo electrónico. Por ejemplo: mail:"foo@bar.com" da como resultado outputClaim:"foo". Si no @ inicio de sesión está presente, se devuelve la cadena de entrada original Hola tal cual.|

**InputClaims:** usa una InputClaims elemento toopass Hola datos desde una transformación de tooa de entrada de esquema de notificación. Tiene dos atributos: **ClaimTypeReferenceId** y **TransformationClaimType**.

- **ClaimTypeReferenceId** se combina con el elemento ID de hello notificación esquema entrada toofind Hola adecuado notificación de entrada. 
- **TransformationClaimType** es toogive usa una entrada de toothis de nombre único. Este nombre debe coincidir con una de las entradas de hello esperada para el método de transformación de hello.

**InputParameters:** usar un toopass de elemento InputParameters una transformación de tooa valor constante. Tiene dos atributos: **Value** e **ID**.

- **Valor** se pasa de hello real valor constante toobe.
- **Id. de** es toogive usa una entrada de toothis de nombre único. Este nombre debe coincidir con una de las entradas de hello esperada para el método de transformación de hello.

**OutputClaims:** usa una OutputClaims elemento toohold Hola datos generados por una transformación y asociarla tooa entrada de esquema de notificación. Tiene dos atributos: **ClaimTypeReferenceId** y **TransformationClaimType**.

- **ClaimTypeReferenceId** se combina con el Id. de Hola de notificación de hello notificación esquema entrada toofind Hola salida correspondiente.
- **TransformationClaimType** es toogive usa una salida de toothis de nombre único. Este nombre debe coincidir con una de las salidas de hello esperada para el método de transformación de hello.

### <a name="exceptions-and-restrictions"></a>Excepciones y restricciones

**NameID de SAML y UPN:** Hola atributos desde el que origen valores NameID y UPN de Hola y Hola notificaciones transformaciones que se permiten, están limitados.

#### <a name="table-5-attributes-allowed-as-a-data-source-for-saml-nameid"></a>Tabla 5: Atributos permitidos como origen de datos en NameID de SAML
|Origen|ID|Descripción|
|-----|-----|-----|
|Usuario|mail|Dirección de correo electrónico|
|Usuario|userprincipalname|Nombre principal de usuario|
|Usuario|onpremisessamaccountname|Nombre de cuenta SAM local|
|Usuario|employeeid|Id. de empleado|
|Usuario|extensionattribute1|Atributo de extensión 1|
|Usuario|extensionattribute2|Atributo de extensión 2|
|Usuario|extensionattribute3|Atributo de extensión 3|
|Usuario|extensionattribute4|Atributo de extensión 4|
|Usuario|extensionattribute5|Atributo de extensión 5|
|Usuario|extensionattribute6|Atributo de extensión 6|
|Usuario|extensionattribute7|Atributo de extensión 7|
|Usuario|extensionattribute8|Atributo de extensión 8|
|Usuario|extensionattribute9|Atributo de extensión 9|
|Usuario|extensionattribute10|Atributo de extensión 10|
|Usuario|extensionattribute11|Atributo de extensión 11|
|Usuario|extensionattribute12|Atributo de extensión 12|
|Usuario|extensionattribute13|Atributo de extensión 13|
|Usuario|extensionattribute14|Atributo de extensión 14|
|Usuario|extensionattribute15|Atributo de extensión 15|

#### <a name="table-6-transformation-methods-allowed-for-saml-nameid"></a>Tabla 6: Métodos de transformación permitidos en NameID de SAML
|TransformationMethod|Restricciones|
| ----- | ----- |
|ExtractMailPrefix|None|
|Unión|sufijo de Hola que se están combinando debe ser un dominio comprobado del inquilino de recursos de Hola.|

### <a name="custom-signing-key"></a>Clave de firma de personalizada
Una clave de firma personalizada debe asignarse como objeto de entidad de servicio de toohello un efecto de tootake de directiva de asignación de notificaciones. Todos los tokens emitidos que se han visto afectados por la directiva de Hola se firman con esta clave. Aplicaciones deben ser tokens de tooaccept configurado firmados con esta clave. Esto garantiza que la directiva de asignación de notificaciones de confirmación que se han modificado los tokens creador de Hola de Hola. Protege a las aplicaciones de directivas de asignación de notificaciones creadas por actores malintencionados.

### <a name="cross-tenant-scenarios"></a>Escenarios de varios inquilinos
Las directivas de asignación no aplican a los usuarios de tooguest de notificaciones. Si un usuario invitado intentos tooaccess una aplicación con una notificación de asignación directiva asignada tooits servicio entidad de seguridad, se emite el token de hello predeterminado (directiva de hello no tiene ningún efecto).

## <a name="claims-mapping-policy-assignment"></a>Asignación de directivas de asignación de notificaciones
Las directivas de asignación solo se puede asignar objetos de entidad de tooservice de notificaciones.

### <a name="example-claims-mapping-policies"></a>Directivas de asignación de notificaciones de ejemplo

En Azure AD hay muchos escenarios posibles en los que se pueden personalizar las notificaciones emitidas en tokens para entidades de servicio concretas. En esta sección se abordan algunos escenarios comunes que pueden ayudarle a entender cómo toouse Hola el tipo de directiva de asignación de notificaciones.

#### <a name="prerequisites"></a>Requisitos previos
Hola en los ejemplos siguientes, crear, actualizar, vincular y eliminar directivas para las entidades de servicio. Si es nuevo tooAzure AD, se recomienda que desea obtener información sobre cómo tooget un Azure AD inquilino antes de continuar con estos ejemplos. 

Hola tooget iniciado, siga los pasos:


1. Descargar más reciente hello [versión de vista previa de módulo de PowerShell de Azure AD](https://www.powershellgallery.com/packages/AzureADPreview/2.0.0.127).
2.  Ejecute hello conectar comando toosign en tooyour cuenta de administrador de Azure AD. Ejecute este comando cada vez que inicie una nueva sesión.
    
     ``` powershell
    Connect-AzureAD -Confirm
    
    ```
3.  toosee todas las directivas que se han creado en su organización, ejecución Hola siguiendo este comando. Se recomienda ejecutar este comando después de la mayoría de las operaciones en hello siguientes escenarios, toocheck que las directivas se crean como se esperaba.
   
    ``` powershell
        Get-AzureADPolicy
    
    ```
#### <a name="example-create-and-assign-a-policy-tooomit-hello-basic-claims-from-tokens-issued-tooa-service-principal"></a>Ejemplo: Crear y asignar una directiva tooomit Hola afirmaciones básico, versión de entidad de servicio de tokens emitidos tooa.
En este ejemplo, cree una directiva que quita el conjunto de notificaciones básico de Hola de tokens emitidos toolinked entidades de servicio.


1. Cree una directiva de asignación de notificaciones. Esta directiva, las entidades de servicio vinculado toospecific, quita conjunto de notificaciones básico de Hola de símbolos (tokens).
    1. Directiva de hello toocreate, ejecute este comando: 
    
     ``` powershell
    New-AzureADPolicy -Definition @('{"ClaimsMappingPolicy":{"Version":1,"IncludeBasicClaimSet":"false"}}') -DisplayName "OmitBasicClaims” -Type "ClaimsMappingPolicy"
    ```
    2. toosee de comandos de la nueva directiva y directiva de hello tooget ObjectId, Hola ejecución después de:
    
     ``` powershell
    Get-AzureADPolicy
    ```
2.  Asignar la entidad de servicio de hello directiva tooyour. También debe tooget Hola ObjectId de la entidad de servicio. 
    1.  toosee entidades de servicio de todos los de su organización, puede consultar Microsoft Graph. O bien, en el Explorador de Azure AD Graph, inicie sesión en tooyour cuenta de Azure AD.
    2.  Una vez Hola ObjectId de su servicio principal, ejecute ¡hello siguiente comando:  
     
     ``` powershell
    Add-AzureADServicePrincipalPolicy -Id <ObjectId of hello ServicePrincipal> -RefObjectId <ObjectId of hello Policy>
    ```
#### <a name="example-create-and-assign-a-policy-tooinclude-hello-employeeid-and-tenantcountry-as-claims-in-tokens-issued-tooa-service-principal"></a>Ejemplo: Crear y asignar una directiva tooinclude Hola EmployeeID y TenantCountry notificaciones en tokens emitidos tooa entidad de servicio.
En este ejemplo, se crea una directiva que agrega Hola EmployeeID y TenantCountry tootokens emitido toolinked entidades de servicio. Hola EmployeeID se genera como tipo de notificación de nombre de hello en tokens SAML y Jwt. Hola TenantCountry se genera como tipo de tokens SAML y Jwt de notificación de país de Hola. En este ejemplo, seguimos establecidas en tokens de hello las afirmaciones de tooinclude hello básico.

1. Cree una directiva de asignación de notificaciones. Esta directiva, las entidades de servicio vinculado toospecific, agrega Hola EmployeeID y TenantCountry tootokens de notificaciones.
    1. Directiva de hello toocreate, ejecute este comando:  
     
     ``` powershell
    New-AzureADPolicy -Definition @('{"ClaimsMappingPolicy":{"Version":1,"IncludeBasicClaimSet":"true", "ClaimsSchema": [{"Source":"user","ID":"employeeid","SamlClaimType":"http://schemas.xmlsoap.org/ws/2005/05/identity/claims/name","JwtClaimType":"name"},{"Source":"company","ID":" tenantcountry ","SamlClaimType":" http://schemas.xmlsoap.org/ws/2005/05/identity/claims/country ","JwtClaimType":"country"}]}}') -DisplayName "ExtraClaimsExample” -Type "ClaimsMappingPolicy"
    ```
    
    2. toosee de comandos de la nueva directiva y directiva de hello tooget ObjectId, Hola ejecución después de:
     
     ``` powershell  
    Get-AzureADPolicy
    ```
2.  Asignar la entidad de servicio de hello directiva tooyour. También debe tooget Hola ObjectId de la entidad de servicio. 
    1.  toosee entidades de servicio de todos los de su organización, puede consultar Microsoft Graph. O bien, en el Explorador de Azure AD Graph, inicie sesión en tooyour cuenta de Azure AD.
    2.  Una vez Hola ObjectId de su servicio principal, ejecute ¡hello siguiente comando:  
     
     ``` powershell
    Add-AzureADServicePrincipalPolicy -Id <ObjectId of hello ServicePrincipal> -RefObjectId <ObjectId of hello Policy>
    ```
#### <a name="example-create-and-assign-a-policy-that-uses-a-claims-transformation-in-tokens-issued-tooa-service-principal"></a>Ejemplo: Crear y asignar una directiva que usa una transformación de notificaciones de tokens emitidos tooa entidad de servicio.
En este ejemplo, cree una directiva que emite una notificación personalizada "JoinedData" tooJWTs emitido a toolinked entidades de servicio. Esta notificación contiene un valor que se crea mediante la combinación de datos de hello almacenados en el atributo de atributodeextensión1 hello en el objeto de usuario de hello con ".sandbox". En este ejemplo, excluimos notificaciones básica hello establecidos en tokens de Hola.


1. Cree una directiva de asignación de notificaciones. Esta directiva, las entidades de servicio vinculado toospecific, agrega Hola EmployeeID y TenantCountry tootokens de notificaciones.
    1. Directiva de hello toocreate, ejecute este comando: 
     
     ``` powershell
    New-AzureADPolicy -Definition @('{"ClaimsMappingPolicy":{"Version":1,"IncludeBasicClaimSet":"true", "ClaimsSchema":[{"Source":"user","ID":"extensionattribute1"},{"Source":"transformation","ID":"DataJoin","TransformationId":"JoinTheData","JwtClaimType":"JoinedData"}],"ClaimsTransformation":[{"ID":"JoinTheData","TransformationMethod":"Join","InputClaims":[{"ClaimTypeReferenceId":"extensionattribute1","TransformationClaimType":"string1"}], "InputParameters": [{"Id":"string2","Value":"sandbox"},{"Id":"separator","Value":"."}],"OutputClaims":[{"ClaimTypeReferenceId":"DataJoin","TransformationClaimType":"outputClaim"}]}]}}') -DisplayName "TransformClaimsExample” -Type "ClaimsMappingPolicy"
    ```
    
    2. toosee de comandos de la nueva directiva y directiva de hello tooget ObjectId, Hola ejecución después de: 
     
     ``` powershell
    Get-AzureADPolicy
    ```
2.  Asignar la entidad de servicio de hello directiva tooyour. También debe tooget Hola ObjectId de la entidad de servicio. 
    1.  toosee entidades de servicio de todos los de su organización, puede consultar Microsoft Graph. O bien, en el Explorador de Azure AD Graph, inicie sesión en tooyour cuenta de Azure AD.
    2.  Una vez Hola ObjectId de su servicio principal, ejecute ¡hello siguiente comando: 
     
     ``` powershell
    Add-AzureADServicePrincipalPolicy -Id <ObjectId of hello ServicePrincipal> -RefObjectId <ObjectId of hello Policy>
    ```
