---
title: "recursos de plantilla de administración de API aaaAzure | Documentos de Microsoft"
description: "Obtenga información acerca de los tipos de Hola de recursos disponibles para su uso en plantillas del portal de desarrollador en la administración de API de Azure."
services: api-management
documentationcenter: 
author: miaojiang
manager: erikre
editor: 
ms.assetid: 51a1b4c6-a9fd-4524-9e0e-03a9800c3e94
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/09/2017
ms.author: apimpm
ms.openlocfilehash: 2221e3852986d485d13817b483e473dfe451d3c3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="azure-api-management-template-resources"></a>Recursos de plantilla de Azure API Management
Administración de API de Azure proporciona Hola siguientes tipos de recursos para su uso en plantillas del portal para desarrolladores de Hola.  
  
-   [Recursos de cadena](#strings)  
  
-   [Recursos de glifo](#glyphs)  
  
##  <a name="strings"></a> Recursos de cadena  
 Administración de API se proporciona un conjunto completo de recursos de cadena para su uso en el portal para desarrolladores de Hola. Estos recursos están localizados en todos los idiomas de hello admitidos por la API de administración. conjunto de plantillas de Hello predeterminado utiliza estos recursos para encabezados de página, las etiquetas y las cadenas constantes que se muestran en el portal para desarrolladores de Hola. toouse un recurso de cadena en las plantillas proporcionan el prefijo de cadena de recurso Hola seguido por el nombre de la cadena de hello, tal y como se muestra en el siguiente ejemplo de Hola.  
  
```  
{% localized "Prefix|Name" %}  
  
```  
  
 Hello en el ejemplo siguiente se es de plantilla de lista de productos de Hola y muestra **productos** al principio de Hola de página de Hola.  
  
```  
<h2>{% localized "ProductsStrings|PageTitleProducts" %}</h2>  
  
```  
  
 Consulte toohello siguientes tablas para los recursos de cadena Hola disponibles para su uso en las plantillas de portal para desarrolladores. Usar nombre de la tabla de hello como prefijo de Hola Hola recursos de cadena de esa tabla.  
  
-   [ApisStrings](#ApisStrings)  
  
-   [ApplicationListStrings](#ApplicationListStrings)  
  
-   [AppDetailsStrings](#AppDetailsStrings)  
  
-   [AppStrings](#AppStrings)  
  
-   [CommonResources](#CommonResources)  
  
-   [CommonStrings](#CommonStrings)  
  
-   [Documentación](#Documentation)  
  
-   [ErrorPageStrings](#ErrorPageStrings)  
  
-   [IssuesStrings](#IssuesStrings)  
  
-   [NotFoundStrings](#NotFoundStrings)  
  
-   [ProductDetailsStrings](#ProductDetailsStrings)  
  
-   [ProductsStrings](#ProductsStrings)  
  
-   [ProviderInfoStrings](#ProviderInfoStrings)  
  
-   [SigninResources](#SigninResources)  
  
-   [SigninStrings](#SigninStrings)  
  
-   [SignupStrings](#SignupStrings)  
  
-   [SubscriptionListStrings](#SubscriptionListStrings)  
  
-   [SubscriptionStrings](#SubscriptionStrings)  
  
-   [UpdateProfileStrings](#UpdateProfileStrings)  
  
-   [UserProfile](#UserProfile)  
  
###  <a name="ApisStrings"></a> ApisStrings  
  
|Nombre|Texto|  
|----------|----------|  
|PageTitleApis|API existentes|  
  
###  <a name="AppDetailsStrings"></a> AppDetailsStrings  
  
|Nombre|Texto|  
|----------|----------|  
|WebApplicationsDetailsTitle|Versión preliminar de la aplicación|  
|WebApplicationsRequirementsHeader|Requisitos|  
|WebApplicationsScreenshotAlt|Instantánea|  
|WebApplicationsScreenshotsHeader|Capturas de pantalla|  
  
###  <a name="ApplicationListStrings"></a> ApplicationListStrings  
  
|Nombre|Texto|  
|----------|----------|  
|WebDevelopersAppDeleteConfirmation|¿Está seguro de que desea tooremove aplicación?|  
|WebDevelopersAppNotPublished|No publicado|  
|WebDevelopersAppNotSubminted|No enviado|  
|WebDevelopersAppTableCategoryHeader|Categoría|  
|WebDevelopersAppTableNameHeader|Nombre|  
|WebDevelopersAppTableStateHeader|Estado|  
|WebDevelopersEditLink|Edit|  
|WebDevelopersRegisterAppLink|Registre la aplicación|  
|WebDevelopersRemoveLink|Remove|  
|WebDevelopersSubmitLink|Enviar|  
|WebDevelopersYourApplicationsHeader|Sus aplicaciones|  
  
###  <a name="AppStrings"></a> AppStrings  
  
|Nombre|Texto|  
|----------|----------|  
|WebApplicationsHeader|Aplicaciones|  
  
###  <a name="CommonResources"></a> CommonResources  
  
|Nombre|Texto|  
|----------|----------|  
|NoItemsToDisplay|No se encontró ningún resultado.|  
|GeneralExceptionMessage|Se ha producido algún problema. Podría ser un problema temporal o un error. Vuelva a intentarlo.|  
|GeneralJsonExceptionMessage|Se ha producido algún problema. Podría ser un problema temporal o un error. Por favor, vuelva a cargar la página de Hola y vuelva a intentarlo.|  
|ConfirmationMessageUnsavedChanges|Hay algunos cambios no guardados. ¿Está seguro de que desea toocancel y descarta los cambios de hello?|  
|AzureActiveDirectory|Azure Active Directory|  
|HttpLargeRequestMessage|El cuerpo de la solicitud HTTP es demasiado extenso.|  
  
###  <a name="CommonStrings"></a> CommonStrings  
  
|Nombre|Texto|  
|----------|----------|  
|ButtonLabelCancel|Cancelar|  
|ButtonLabelSave|Guardar|  
|GeneralExceptionMessage|Se ha producido algún problema. Podría ser un problema temporal o un error. Vuelva a intentarlo.|  
|NoItemsToDisplay|No hay ningún toodisplay elementos.|  
|PagerButtonLabelFirst|Primero|  
|PagerButtonLabelLast|Último|  
|PagerButtonLabelNext|Pasos siguientes|  
|PagerButtonLabelPrevious|Anterior|  
|PagerLabelPageNOfM|Página {0} de {1}|  
|PasswordTooShort|Hola contraseña es demasiado corta.|  
|EmailAsPassword|No use su correo electrónico como la contraseña.|  
|PasswordSameAsUserName|La contraseña no puede contener su nombre de usuario.|  
|PasswordTwoCharacterClasses|Utilice diferentes clases de caracteres.|  
|PasswordTooManyRepetitions|Hay demasiados caracteres repetidos.|  
|PasswordSequenceFound|La contraseña contiene secuencias.|  
|PagerLabelPageSize|Tamaño de página|  
|CurtainLabelLoading|Cargando...|  
|TablePlaceholderNothingToDisplay|No hay ningún dato para el ámbito y el período de hello seleccionado|  
|ButtonLabelClose|cierre|  
  
###  <a name="Documentation"></a> Documentation  
  
|Nombre|Texto|  
|----------|----------|  
|WebDocumentationInvalidHeaderErrorMessage|Encabezado no válido "{0}"|  
|WebDocumentationInvalidRequestErrorMessage|Dirección URL de solicitud no válida|  
|TextboxLabelAccessToken|Token de acceso*|  
|DropdownOptionPrimaryKeyFormat|Principal: {0}|  
|DropdownOptionSecondaryKeyFormat|Secundario: {0}|  
|WebDocumentationSubscriptionKeyText|Su clave de suscripción|  
|WebDocumentationTemplatesAddHeaders|Agregue los encabezados HTTP necesarios.|  
|WebDocumentationTemplatesBasicAuthSample|Ejemplo de autorización básica|  
|WebDocumentationTemplatesCurlForBasicAuth|Para la autorización básica, use lo siguiente: --user {nombre de usuario}: {contraseña}|  
|WebDocumentationTemplatesCurlValuesForPath|Especifique valores para los parámetros de ruta de acceso (que se muestran como {...}), la clave de la suscripción y valores para los parámetros de consulta.|  
|WebDocumentationTemplatesDeveloperKey|Especifique la clave de suscripción.|  
|WebDocumentationTemplatesJavaApache|Este ejemplo utiliza el cliente de Apache HTTP Hola de componentes de HTTP (http://hc.apache.org/httpcomponents-client-ga/)|  
|WebDocumentationTemplatesOptionalParams|Especifique valores para los parámetros opcionales, según se requiera.|  
|WebDocumentationTemplatesPhpPackage|Este ejemplo utiliza el paquete de hello HTTP_Request2. (Para obtener más información, visite http://pear.php.net/package/HTTP_Request2).|  
|WebDocumentationTemplatesPythonValuesForPath|Especifique valores para los parámetros de ruta de acceso (que se muestran como {...}) y el cuerpo de la solicitud, si así se requiere.|  
|WebDocumentationTemplatesRequestBody|Especifique el cuerpo de la solicitud.|  
|WebDocumentationTemplatesRequiredParams|Especificar valores para parámetros necesarios siguientes de Hola|  
|WebDocumentationTemplatesValuesForPath|Especifique valores para los parámetros de ruta de acceso (que se muestran como {...}).|  
|OAuth2AuthorizationEndpointDescription|extremo de autorización de Hello es toointeract usado con el propietario del recurso de Hola y obtener una concesión de autorización.|  
|OAuth2AuthorizationEndpointName|Punto de conexión de autorización|  
|OAuth2TokenEndpointDescription|extremo de token de Hola Hola cliente tooobtain un token de acceso al presentar su autorización conceder o token de actualización.|  
|OAuth2TokenEndpointName|Punto de conexión de token|  
|OAuth2Flow_AuthorizationCodeGrant_Step_AuthorizationRequest_Description|< p\> cliente hello inicia Hola flujo dirigiendo extremo de autorización de toohello de agente de usuario del propietario del recurso de Hola.  cliente de Hello incluye su identificador de cliente, el ámbito solicitado, el estado local y un servidor de autorización de redirección URI toowhich Hola enviará Hola de agente de usuario una vez concedido (o deniega el acceso).     < /p\> < p\> servidor de autorización de hello propietario del recurso de hello (a través de agente de usuario Hola) se autentica y establece si el propietario del recurso de hello concede o deniega la solicitud de acceso del cliente de Hola.     < /p\> < p\> suponiendo que el propietario del recurso de hello concede acceso, servidor de autorización de hello redirige el cliente de toohello atrás de agente de usuario de hello mediante el redireccionamiento de hello URI proporcionado anteriormente (en la solicitud de Hola o durante Permi registro de t).  identificador URI de redireccionamiento de Hello incluye un código de autorización y cualquier estado local proporcionado por el cliente de hello anteriormente.     </p\>|  
|OAuth2Flow_AuthorizationCodeGrant_Step_AuthorizationRequest_ErrorDescription|< p\> si el usuario de hello rechaza la solicitud de acceso de Hola de si Hola solicitud no es válida, cliente hello le informará mediante Hola después de parámetros que se agregan al redirigir toohello: < /p\>|  
|OAuth2Flow_AuthorizationCodeGrant_Step_AuthorizationRequest_Name|Solicitud de autorización|  
|OAuth2Flow_AuthorizationCodeGrant_Step_AuthorizationRequest_RequestDescription|< p\> aplicación de cliente de hello debe enviar el extremo de autorización de hello usuario toohello Hola de orden tooinitiate proceso OAuth.          En el extremo de autorización de hello, usuario Hola autentica y, a continuación, concede o deniega el acceso toohello aplicación.     </p\>|  
|OAuth2Flow_AuthorizationCodeGrant_Step_AuthorizationRequest_ResponseDescription|< p\> suponiendo que el propietario del recurso de hello concede acceso, servidor de autorización redirige el cliente de toohello atrás de agente de usuario de hello mediante el redireccionamiento de hello URI proporcionado anteriormente (en la solicitud de Hola o durante el registro de cliente).  identificador URI de redireccionamiento de Hello incluye un código de autorización y cualquier estado local proporcionado por el cliente de hello anteriormente. </p\>|  
|OAuth2Flow_AuthorizationCodeGrant_Step_TokenRequest_Description|< p\> cliente de hello solicita un token de acceso del servidor de autorización de Hola "extremo de token s mediante la inclusión de código de autorización de hello recibida en el paso anterior de Hola.  Al realizar la solicitud de Hola, cliente de Hola se autentica con el servidor de autorización de Hola.  cliente de Hello incluye código de autorización de la hello de la tooobtain URI usado Hola redirección para la comprobación. < /p\> < p\> servidor de autorización de hello autentica el cliente de hello, valida el código de autorización de Hola y garantiza que ese identificador URI de redireccionamiento de hello recibió coincidencias Hola URI usado tooredirect Hola cliente en el paso (C).  Si es válida, el servidor de autorización de Hola responde con un token de acceso y, opcionalmente, un token de actualización. </p\>|  
|OAuth2Flow_AuthorizationCodeGrant_Step_TokenRequest_ErrorDescription|< p\> si autenticación de cliente de solicitud de hello error o no es válida, servidor de autorización de hello responde con un código de estado HTTP 400 (solicitud incorrecta) (a menos que se especifique lo contrario) e incluye Hola parámetros con respuesta Hola siguientes. </p\>|  
|OAuth2Flow_AuthorizationCodeGrant_Step_TokenRequest_RequestDescription|< p\> cliente hello hace que un extremo de token de solicitud toohello mediante el envío de Hola Hola "application/x--www-form-urlencoded" formato con la codificación de caracteres de UTF-8 en el cuerpo de entidad de solicitud HTTP Hola de parámetros siguientes. </p\>|  
|OAuth2Flow_AuthorizationCodeGrant_Step_TokenRequest_ResponseDescription|< p\> servidor de autorización de hello emite un token de acceso y el token de actualización opcional, y construcciones Hola respuesta mediante la adición de hello después parámetros toohello-cuerpo de la entidad de respuesta de hello HTTP con un código de 200 estado (Aceptar). </p\>|  
|OAuth2Flow_ClientCredentialsGrant_Step_TokenRequest_Description|< p\> cliente Hola se autentica con el servidor de autorización de Hola y solicita un token de acceso de extremo de token de Hola. < /p\> < p\> servidor de autorización de hello autentica el cliente de hello y, si es válida, emite un token de acceso. </p\>|  
|OAuth2Flow_ClientCredentialsGrant_Step_TokenRequest_ErrorDescription|< p\> si la solicitud de hello errores de autenticación de cliente o no es válido servidor de autorización de hello responde con un código de estado HTTP 400 (solicitud incorrecta) (a menos que se especifique lo contrario) e incluye Hola parámetros con respuesta Hola siguientes. </p\>|  
|OAuth2Flow_ClientCredentialsGrant_Step_TokenRequest_RequestDescription|< p\> cliente hello hace que un extremo de token de solicitud toohello agregando Hola Hola "application/x--www-form-urlencoded" formato con la codificación de caracteres de UTF-8 en el cuerpo de entidad de solicitud HTTP Hola de parámetros siguientes. </p\>|  
|OAuth2Flow_ClientCredentialsGrant_Step_TokenRequest_ResponseDescription|< p\> si la solicitud de token de acceso de hello es válida y está autorizado, servidor de autorización de hello emite un token de acceso y el token de actualización opcional y construcciones Hola respuesta mediante la adición de hello después parámetros toohello cuerpo de entidad de hello HTTP respuesta con un código de 200 estado (Aceptar). </p\>|  
|OAuth2Flow_ImplicitGrant_Step_AuthorizationRequest_Description|< p\> cliente hello inicia Hola flujo dirigiendo propietario del recurso de Hola "extremo de autorización de toohello s agente de usuario.  cliente de Hello incluye su identificador de cliente, el ámbito solicitado, el estado local y un servidor de autorización de redirección URI toowhich Hola enviará Hola de agente de usuario una vez concedido (o deniega el acceso). < /p\> < p\> servidor de autorización de hello propietario del recurso de hello (a través de agente de usuario Hola) se autentica y establece si el propietario del recurso de hello concede o deniega el cliente de hello'' solicita acceso. < /p\> < p\> suponiendo que el propietario del recurso de hello concede acceso, servidor de autorización de hello redirige el cliente de toohello atrás de agente de usuario de hello mediante el redireccionamiento de hello URI proporcionado anteriormente.  identificador URI de redireccionamiento de Hello incluye token de acceso de hello en el fragmento de URI de Hola. </p\>|  
|OAuth2Flow_ImplicitGrant_Step_AuthorizationRequest_ErrorDescription|< p\> si el propietario del recurso de hello deniega la solicitud de acceso de Hola o si se produce un error en la solicitud de Hola por motivos distintos a un identificador URI de redireccionamiento no válida o ausente, servidor de autorización de hello informa a cliente hello agregando Hola después parámetros toohello fragme componente de NT del uso de URI de redirección de Hola Hola formato de "application/x--www-form-urlencoded". </p\>|  
|OAuth2Flow_ImplicitGrant_Step_AuthorizationRequest_RequestDescription|< p\> aplicación de cliente de hello debe enviar el extremo de autorización de hello usuario toohello Hola de orden tooinitiate proceso OAuth.      En el extremo de autorización de hello, usuario Hola autentica y, a continuación, concede o deniega el acceso toohello aplicación. </p\>|  
|OAuth2Flow_ImplicitGrant_Step_AuthorizationRequest_ResponseDescription|< p\> si el propietario del recurso de hello concede solicitud de acceso de hello, servidor de autorización de hello emite un token de acceso y lo entrega toohello cliente mediante la adición de hello parámetros toohello fragmento componente de la redirección de hello URI siguiente utilizando Hola "a aplicaciones/x--www-form-urlencoded"formato. </p\>|  
|OAuth2Flow_ObtainAuthorization_AuthorizationCodeGrant_Description|Flujo de código de autorización está optimizado para clientes con capacidad de mantener la confidencialidad de Hola de sus credenciales (por ejemplo, aplicaciones de servidor web implementadas mediante PHP, Java, Python, Ruby, ASP.NET, etcetera.).|  
|OAuth2Flow_ObtainAuthorization_AuthorizationCodeGrant_Name|Concesión del código de autorización|  
|OAuth2Flow_ObtainAuthorization_ClientCredentialsGrant_Description|Flujo de credenciales de cliente es el adecuado en casos donde el cliente de hello (la aplicación) solicita acceso a los recursos protegido de toohello bajo su control. Hola se considera como el propietario de un recurso, por lo que se requiere ninguna interacción del usuario final.|  
|OAuth2Flow_ObtainAuthorization_ClientCredentialsGrant_Name|Concesión de las credenciales de cliente|  
|OAuth2Flow_ObtainAuthorization_ImplicitGrant_Description|Flujo implícito está optimizado para clientes sin capacidad de mantener la confidencialidad de Hola de su toooperate conocidos un identificador URI de redireccionamiento determinado de credenciales. Estos clientes se suelen implementar en un explorador mediante un lenguaje de scripting como JavaScript.|  
|OAuth2Flow_ObtainAuthorization_ImplicitGrant_Name|Concesión implícita|  
|OAuth2Flow_ObtainAuthorization_ResourceOwnerPasswordCredentialsGrant_Description|Flujo de credenciales de contraseña de propietario de recurso es adecuado en casos donde el propietario del recurso de hello tiene una relación de confianza con el cliente de hello (la aplicación), como sistema operativo del dispositivo Hola o una aplicación con privilegios elevados. Este flujo es adecuado para clientes con capacidad de obtener las credenciales del propietario del recurso de hello (nombre de usuario y contraseña, normalmente mediante un formulario interactivo).|  
|OAuth2Flow_ObtainAuthorization_ResourceOwnerPasswordCredentialsGrant_Name|Concesión de credenciales de contraseña de propietario del recurso|  
|OAuth2Flow_ResourceOwnerPasswordCredentialsGrant_Step_TokenRequest_Description|< p\> propietario del recurso de hello proporciona cliente hello con su nombre de usuario y una contraseña. < /p\> < p\> cliente de hello solicita un token de acceso del servidor de autorización de Hola "extremo de token s mediante la inclusión de las credenciales de hello recibidas desde el propietario del recurso de Hola.  Al realizar la solicitud de Hola, cliente de Hola se autentica con el servidor de autorización de Hola. < /p\> < p\> servidor de autorización de hello autentica el cliente de Hola y valida las credenciales del propietario de recurso de Hola y si es válida, emite un token de acceso. </p\>|  
|OAuth2Flow_ResourceOwnerPasswordCredentialsGrant_Step_TokenRequest_ErrorDescription|< p\> si la solicitud de hello errores de autenticación de cliente o no es válido servidor de autorización de hello responde con un código de estado HTTP 400 (solicitud incorrecta) (a menos que se especifique lo contrario) e incluye Hola parámetros con respuesta Hola siguientes. </p\>|  
|OAuth2Flow_ResourceOwnerPasswordCredentialsGrant_Step_TokenRequest_RequestDescription|< p\> cliente hello hace que un extremo de token de solicitud toohello agregando Hola Hola "application/x--www-form-urlencoded" formato con la codificación de caracteres de UTF-8 en el cuerpo de entidad de solicitud HTTP Hola de parámetros siguientes. </p\>|  
|OAuth2Flow_ResourceOwnerPasswordCredentialsGrant_Step_TokenRequest_ResponseDescription|< p\> si la solicitud de token de acceso de hello es válida y está autorizado, servidor de autorización de hello emite un token de acceso y el token de actualización opcional y construcciones Hola respuesta agregando Hola después parámetros toohello-cuerpo de entidad de hello HTTP Responsibilities nSe con un código de 200 estado (Aceptar). </p\>|  
|OAuth2Step_AccessTokenRequest_Name|Solicitud de token de acceso|  
|OAuth2Step_AuthorizationRequest_Name|Solicitud de autorización|  
|OAuth2AccessToken_AuthorizationCodeGrant_TokenResponse|REQUERIDO. token de acceso de Hello emitido por el servidor de autorización de Hola.|  
|OAuth2AccessToken_ClientCredentialsGrant_TokenResponse|REQUERIDO. token de acceso de Hello emitido por el servidor de autorización de Hola.|  
|OAuth2AccessToken_ImplicitGrant_AuthorizationResponse|REQUERIDO. token de acceso de Hello emitido por el servidor de autorización de Hola.|  
|OAuth2AccessToken_ResourceOwnerPasswordCredentialsGrant_TokenResponse|REQUERIDO. token de acceso de Hello emitido por el servidor de autorización de Hola.|  
|OAuth2ClientId_AuthorizationCodeGrant_AuthorizationRequest|REQUERIDO. Identificador del cliente.|  
|OAuth2ClientId_AuthorizationCodeGrant_TokenRequest|NECESARIO si el cliente de hello no está autenticando con servidor de autorización de Hola.|  
|OAuth2ClientId_ImplicitGrant_AuthorizationRequest|REQUERIDO. identificador de cliente de Hola.|  
|OAuth2Code_AuthorizationCodeGrant_AuthorizationResponse|REQUERIDO. código de autorización de Hello generado por el servidor de autorización de Hola.|  
|OAuth2Code_AuthorizationCodeGrant_TokenRequest|REQUERIDO. código de autorización de Hello recibido del servidor de autorización de Hola.|  
|OAuth2ErrorDescription_AuthorizationCodeGrant_AuthorizationErrorResponse|OPCIONAL. Texto ASCII en lenguaje natural que proporciona información adicional.|  
|OAuth2ErrorDescription_AuthorizationCodeGrant_TokenErrorResponse|OPCIONAL. Texto ASCII en lenguaje natural que proporciona información adicional.|  
|OAuth2ErrorDescription_ClientCredentialsGrant_TokenErrorResponse|OPCIONAL. Texto ASCII en lenguaje natural que proporciona información adicional.|  
|OAuth2ErrorDescription_ImplicitGrant_AuthorizationErrorResponse|OPCIONAL. Texto ASCII en lenguaje natural que proporciona información adicional.|  
|OAuth2ErrorDescription_ResourceOwnerPasswordCredentialsGrant_TokenErrorResponse|OPCIONAL. Texto ASCII en lenguaje natural que proporciona información adicional.|  
|OAuth2ErrorUri_AuthorizationCodeGrant_AuthorizationErrorResponse|OPCIONAL. Un URI que identifica una página web legible con información sobre el error de Hola.|  
|OAuth2ErrorUri_AuthorizationCodeGrant_TokenErrorResponse|OPCIONAL. Un URI que identifica una página web legible con información sobre el error de Hola.|  
|OAuth2ErrorUri_ClientCredentialsGrant_TokenErrorResponse|OPCIONAL. Un URI que identifica una página web legible con información sobre el error de Hola.|  
|OAuth2ErrorUri_ImplicitGrant_AuthorizationErrorResponse|OPCIONAL. Un URI que identifica una página web legible con información sobre el error de Hola.|  
|OAuth2ErrorUri_ResourceOwnerPasswordCredentialsGrant_TokenErrorResponse|OPCIONAL. Un URI que identifica una página web legible con información sobre el error de Hola.|  
|OAuth2Error_AuthorizationCodeGrant_AuthorizationErrorResponse|REQUERIDO. Un código de error ASCII único desde siguientes hello: solicitud_no_válida, unauthorized_client, access_denied, unsupported_response_type, invalid_scope, server_error, error temporarily_unavailable.|  
|OAuth2Error_AuthorizationCodeGrant_TokenErrorResponse|REQUERIDO. Un código de error ASCII único desde siguientes hello: solicitud_no_válida, cliente_no_válido, concesión_no_válida, unauthorized_client, unsupported_grant_type, invalid_scope.|  
|OAuth2Error_ClientCredentialsGrant_TokenErrorResponse|REQUERIDO. Un código de error ASCII único desde siguientes hello: solicitud_no_válida, cliente_no_válido, concesión_no_válida, unauthorized_client, unsupported_grant_type, invalid_scope.|  
|OAuth2Error_ImplicitGrant_AuthorizationErrorResponse|REQUERIDO. Un código de error ASCII único desde siguientes hello: solicitud_no_válida, unauthorized_client, access_denied, unsupported_response_type, invalid_scope, server_error, error temporarily_unavailable.|  
|OAuth2Error_ResourceOwnerPasswordCredentialsGrant_TokenErrorResponse|REQUERIDO. Un código de error ASCII único desde siguientes hello: solicitud_no_válida, cliente_no_válido, concesión_no_válida, unauthorized_client, unsupported_grant_type, invalid_scope.|  
|OAuth2ExpiresIn_AuthorizationCodeGrant_TokenResponse|RECOMENDADO. duración de Hello en segundos del token de acceso de Hola.|  
|OAuth2ExpiresIn_ClientCredentialsGrant_TokenResponse|RECOMENDADO. duración de Hello en segundos del token de acceso de Hola.|  
|OAuth2ExpiresIn_ImplicitGrant_AuthorizationResponse|RECOMENDADO. duración de Hello en segundos del token de acceso de Hola.|  
|OAuth2ExpiresIn_ResourceOwnerPasswordCredentialsGrant_TokenResponse|RECOMENDADO. duración de Hello en segundos del token de acceso de Hola.|  
|OAuth2GrantType_AuthorizationCodeGrant_TokenRequest|REQUERIDO. Valor debe estar establecido demasiado "authorization_code".|  
|OAuth2GrantType_ClientCredentialsGrant_TokenRequest|REQUERIDO. Valor debe estar establecido demasiado "client_credentials".|  
|OAuth2GrantType_ResourceOwnerPasswordCredentialsGrant_TokenRequest|REQUERIDO. Valor debe estar establecido demasiado "password".|  
|OAuth2Password_ResourceOwnerPasswordCredentialsGrant_TokenRequest|REQUERIDO. contraseña de propietario del recurso de Hola.|  
|OAuth2RedirectUri_AuthorizationCodeGrant_AuthorizationRequest|OPCIONAL. URI del extremo de Hello redirección debe ser un URI absoluto.|  
|OAuth2RedirectUri_AuthorizationCodeGrant_TokenRequest|NECESARIO si el parámetro "redirect_uri" de Hola se incluyó en la solicitud de autorización de Hola y sus valores deben ser idénticos.|  
|OAuth2RedirectUri_ImplicitGrant_AuthorizationRequest|OPCIONAL. URI del extremo de Hello redirección debe ser un URI absoluto.|  
|OAuth2RefreshToken_AuthorizationCodeGrant_TokenResponse|OPCIONAL. token de actualización de Hello, que puede ser usado tooobtain nuevos tokens de acceso.|  
|OAuth2RefreshToken_ClientCredentialsGrant_TokenResponse|OPCIONAL. token de actualización de Hello, que puede ser usado tooobtain nuevos tokens de acceso.|  
|OAuth2RefreshToken_ResourceOwnerPasswordCredentialsGrant_TokenResponse|OPCIONAL. token de actualización de Hello, que puede ser usado tooobtain nuevos tokens de acceso.|  
|OAuth2ResponseType_AuthorizationCodeGrant_AuthorizationRequest|REQUERIDO. Se debe establecer el valor demasiado "código".|  
|OAuth2ResponseType_ImplicitGrant_AuthorizationRequest|REQUERIDO. Valor debe estar establecido demasiado "token".|  
|OAuth2Scope_AuthorizationCodeGrant_AuthorizationRequest|OPCIONAL. ámbito de saludo de solicitud de acceso de Hola.|  
|OAuth2Scope_AuthorizationCodeGrant_TokenResponse|Ámbito opcional si son idénticos toohello solicitada por el cliente de hello; en caso contrario, es necesario.|  
|OAuth2Scope_ClientCredentialsGrant_TokenRequest|OPCIONAL. ámbito de saludo de solicitud de acceso de Hola.|  
|OAuth2Scope_ClientCredentialsGrant_TokenResponse|Ámbito de toohello opcional, si son idénticos solicitada por el cliente de hello; en caso contrario, es necesario.|  
|OAuth2Scope_ImplicitGrant_AuthorizationRequest|OPCIONAL. ámbito de saludo de solicitud de acceso de Hola.|  
|OAuth2Scope_ImplicitGrant_AuthorizationResponse|Ámbito opcional si son idénticos toohello solicitada por el cliente de hello; en caso contrario, es necesario.|  
|OAuth2Scope_ResourceOwnerPasswordCredentialsGrant_TokenRequest|OPCIONAL. ámbito de saludo de solicitud de acceso de Hola.|  
|OAuth2Scope_ResourceOwnerPasswordCredentialsGrant_TokenResponse|Ámbito de toohello opcional, si son idénticos solicitada por el cliente de hello; en caso contrario, es necesario.|  
|OAuth2State_AuthorizationCodeGrant_AuthorizationErrorResponse|REQUERIDO si estaba presente en la solicitud de autorización de cliente de Hola Hola "parámetro"state.  valor exacto de Hello recibido de cliente de Hola.|  
|OAuth2State_AuthorizationCodeGrant_AuthorizationRequest|RECOMENDADO. Un valor opaco utilizado por el estado de toomaintain de cliente de hello entre la solicitud de Hola y devolución de llamada.  servidor de autorización de Hello incluye este valor al redirigir el cliente de hello usuario-agente toohello atrás.  Hola parámetro debe usarse para evitar la falsificación de solicitudes entre sitios.|  
|OAuth2State_AuthorizationCodeGrant_AuthorizationResponse|REQUERIDO si estaba presente en la solicitud de autorización de cliente de Hola Hola "parámetro"state.  valor exacto de Hello recibido de cliente de Hola.|  
|OAuth2State_ImplicitGrant_AuthorizationErrorResponse|REQUERIDO si estaba presente en la solicitud de autorización de cliente de Hola Hola "parámetro"state.  valor exacto de Hello recibido de cliente de Hola.|  
|OAuth2State_ImplicitGrant_AuthorizationRequest|RECOMENDADO. Un valor opaco utilizado por el estado de toomaintain de cliente de hello entre la solicitud de Hola y devolución de llamada.  servidor de autorización de Hello incluye este valor al redirigir el cliente de hello usuario-agente toohello atrás.  Hola parámetro debe usarse para evitar la falsificación de solicitudes entre sitios.|  
|OAuth2State_ImplicitGrant_AuthorizationResponse|REQUERIDO si estaba presente en la solicitud de autorización de cliente de Hola Hola "parámetro"state.  valor exacto de Hello recibido de cliente de Hola.|  
|OAuth2TokenType_AuthorizationCodeGrant_TokenResponse|REQUERIDO. tipo de Hola de hello símbolo (token) emitido.|  
|OAuth2TokenType_ClientCredentialsGrant_TokenResponse|REQUERIDO. tipo de Hola de hello símbolo (token) emitido.|  
|OAuth2TokenType_ImplicitGrant_AuthorizationResponse|REQUERIDO. tipo de Hola de hello símbolo (token) emitido.|  
|OAuth2TokenType_ResourceOwnerPasswordCredentialsGrant_TokenResponse|REQUERIDO. tipo de Hola de hello símbolo (token) emitido.|  
|OAuth2UserName_ResourceOwnerPasswordCredentialsGrant_TokenRequest|REQUERIDO. Hola nombre de usuario de propietario de recursos.|  
|OAuth2UnsupportedTokenType|El tipo de token "{0}" no se admite.|  
|OAuth2InvalidState|Respuesta no válida del servidor de autorización|  
|OAuth2GrantType_AuthorizationCode|Código de autorización|  
|OAuth2GrantType_Implicit|Implícita|  
|OAuth2GrantType_ClientCredentials|Credenciales de cliente|  
|OAuth2GrantType_ResourceOwnerPassword|Contraseña del propietario del recurso|  
|WebDocumentation302Code|302 (encontrado)|  
|WebDocumentation400Code|400 (solicitud incorrecta)|  
|OAuth2SendingMethod_AuthHeader|Encabezado de autorización|  
|OAuth2SendingMethod_QueryParam|Parámetro de consulta|  
|OAuth2AuthorizationServerGeneralException|Se ha producido un error al autorizar el acceso a través de {0}.|  
|OAuth2AuthorizationServerCommunicationException|No se pudo establecer un servidor de tooauthorization de conexión HTTP o que se ha cerrado inesperadamente.|  
|WebDocumentationOAuth2GeneralErrorMessage|Se ha producido un error inesperado.|  
|AuthorizationServerCommunicationException|Se ha producido una excepción de comunicación con el servidor de autorización. Póngase en contacto con el administrador.|  
|TextblockSubscriptionKeyHeaderDescription|Clave de suscripción que proporciona acceso toothis API. Se encontró en el <a href='/developer'\>perfil</a\>.|  
|TextblockOAuthHeaderDescription|Token de acceso OAuth 2.0 obtenido de <i\>{0}</i\>. Tipos de concesión admitidos: <i\>{1}</i\>.|  
|TextblockContentTypeHeaderDescription|Tipo de medio del cuerpo de hello enviado toohello API.|  
|ErrorMessageApiNotAccessible|Hola API que está tratando de toocall no es accesible en este momento. Póngase en contacto con el publicador de la API de Hola < un href = "/ emite"\>aquí < /a\>.|  
|ErrorMessageApiTimedout|Hola API que está tratando de toocall está tardando más de respuesta normal tooget atrás. Póngase en contacto con el publicador de la API de Hola < un href = "/ emite"\>aquí < /a\>.|  
|BadRequestParameterExpected|"Se espera el parámetro '{0}'"|  
|TooltipTextDoubleClickToSelectAll|Haga doble clic en todos los tooselect.|  
|TooltipTextHideRevealSecret|Mostrar/ocultar|  
|ButtonLinkOpenConsole|Pruébelo|  
|SectionHeadingRequestBody|Cuerpo de la solicitud|  
|SectionHeadingRequestParameters|Parámetros de solicitud|  
|SectionHeadingRequestUrl|URL de la solicitud|  
|SectionHeadingResponse|Response|  
|SectionHeadingRequestHeaders|Encabezados de solicitud|  
|FormLabelSubtextOptional|opcional|  
|SectionHeadingCodeSamples|Ejemplos de código|  
|TextblockOpenidConnectHeaderDescription|Token de identificador de OpenID Connect obtenido de <i\>{0}</i\>. Tipos de concesión admitidos: <i\>{1}</i\>.|  
  
###  <a name="ErrorPageStrings"></a> ErrorPageStrings  
  
|Nombre|Texto|  
|----------|----------|  
|LinkLabelBack|atrás|  
|LinkLabelHomePage|página principal|  
|LinkLabelSendUsEmail|Envíenos un correo electrónico|  
|PageTitleError|Lo sentimos, hubo una página solicitada de problema que se sirva Hola|  
|TextblockPotentialCauseIntermittentIssue|Esto puede ser un problema de acceso a los datos intermitente que ya ha pasado.|  
|TextblockPotentialCauseOldLink|puede ser anterior que haya hecho clic en el vínculo de Hola y toohello de punto no se ha corregido ubicación ya.|  
|TextblockPotentialCauseTechnicalProblem|Es posible que haya un problema técnico por nuestra parte.|  
|TextblockPotentialSolutionRefresh|Pruebe a actualizar la página de Hola.|  
|TextblockPotentialSolutionStartOver|Empiece de nuevo desde nuestro {0}.|  
|TextblockPotentialSolutionTryAgain|{0} e intenta la acción Hola que realizando de nuevo.|  
|TextReportProblem|{0} donde se describa el error y lo analizaremos lo antes posible.|  
|TitlePotentialCause|Causa posible|  
|TitlePotentialSolution|Posiblemente es simplemente un problema temporal, unos tootry cosas|  
  
###  <a name="IssuesStrings"></a> IssuesStrings  
  
|Nombre|Texto|  
|----------|----------|  
|WebIssuesIndexTitle|Problemas|  
|WebIssuesNoActiveSubscriptions|No tiene ninguna suscripción activa. Necesita toosubscribe para un tooreport producto un problema.|  
|WebIssuesNotSignin|No ha iniciado sesión. Intente {0} tooreport un problema o publicar un comentario.|  
|WebIssuesReportIssueButton|Informar sobre un problema|  
|WebIssuesSignIn|iniciar sesión|  
|WebIssuesStatusReportedBy|Estado: {0} &#124; Notificado por {1}|  
  
###  <a name="NotFoundStrings"></a> NotFoundStrings  
  
|Nombre|Texto|  
|----------|----------|  
|LinkLabelHomePage|página principal|  
|LinkLabelSendUsEmail|envíenos un correo electrónico|  
|PageTitleNotFound|Lo sentimos, no encontramos Hola página que está buscando|  
|TextblockPotentialCauseMisspelledUrl|Se puede haber escrito incorrectamente Hola URL si lo escribió en.|  
|TextblockPotentialCauseOldLink|puede ser anterior que haya hecho clic en el vínculo de Hola y toohello de punto no se ha corregido ubicación ya.|  
|TextblockPotentialSolutionRetype|Intente volver a escribir la dirección URL de Hola.|  
|TextblockPotentialSolutionStartOver|Empiece de nuevo desde nuestro {0}.|  
|TextReportProblem|{0} donde se describa el error y lo analizaremos lo antes posible.|  
|TitlePotentialCause|Causa posible|  
|TitlePotentialSolution|Posible solución|  
  
###  <a name="ProductDetailsStrings"></a> ProductDetailsStrings  
  
|Nombre|Texto|  
|----------|----------|  
|WebProductsAgreement|Si se suscribe demasiado {0} producto, muestro mi conformidad toohello `<a data-toggle='modal' href='#legal-terms'\>Terms of Use</a\>`.|  
|WebProductsLegalTermsLink|Términos de uso|  
|WebProductsSubscribeButton|Suscribirse|  
|WebProductsUsageLimitsHeader|Límites de uso|  
|WebProductsYouAreNotSubscribed|Está suscrito toothis producto.|  
|WebProductsYouRequestedSubscription|Había solicitado producto toothis de suscripción.|  
|ErrorYouNeedtoAgreeWithLegalTerms|Debe aceptar los términos de uso toohello antes de continuar.|  
|ButtonLabelAddSubscription|Agregar suscripción|  
|LinkLabelChangeSubscriptionName|cambiar|  
|ButtonLabelConfirm|Confirm|  
|TextblockMultipleSubscriptionsCount|Tiene productos de toothis de las suscripciones de {0}:|  
|TextblockSingleSubscriptionsCount|Tiene productos de toothis de suscripción de {0}:|  
|TextblockSingleApisCount|Este producto contiene {0} API:|  
|TextblockMultipleApisCount|Este producto contiene {0} API:|  
|TextblockHeaderSubscribe|Suscribirse tooproduct|  
|TextblockSubscriptionDescription|Se creará una nueva suscripción de la siguiente manera:|  
|TextblockSubscriptionLimitReached|Ha alcanzado el límite de suscripciones.|  
  
###  <a name="ProductsStrings"></a> ProductsStrings  
  
|Nombre|Texto|  
|----------|----------|  
|PageTitleProducts|Productos|  
  
###  <a name="ProviderInfoStrings"></a> ProviderInfoStrings  
  
|Nombre|Texto|  
|----------|----------|  
|TextboxExternalIdentitiesDisabled|Inicio de sesión está deshabilitada por los administradores de hello en el momento de Hola.|  
|TextboxExternalIdentitiesSigninInvitation|O bien inicie sesión con|  
|TextboxExternalIdentitiesSigninInvitationPrimary|Inicie sesión con:|  
  
###  <a name="SigninResources"></a> SigninResources  
  
|Nombre|Texto|  
|----------|----------|  
|PrincipalNotFound|No se encuentra la entidad de seguridad o la firma no es válida.|  
|ErrorSsoAuthenticationFailed|Error de autenticación SSO.|  
|ErrorSsoAuthenticationFailedDetailed|Se ha proporcionado un token no válido o no se ha podido comprobar la firma.|  
|ErrorSsoTokenInvalid|El token SSO no es válido.|  
|ValidationErrorSpecificEmailAlreadyExists|La dirección de correo electrónico "{0}" ya está registrada.|  
|ValidationErrorSpecificEmailInvalid|La dirección de correo electrónico "{0}" no es válida.|  
|ValidationErrorPasswordInvalid|La contraseña no es válida. Corrija los errores de Hola y vuelva a intentarlo.|  
|PropertyTooShort|La propiedad {0} es demasiado corta.|  
|WebAuthenticationAddresserEmailInvalidErrorMessage|La dirección de correo electrónico no es válida.|  
|ValidationMessageNewPasswordConfirmationRequired|Confirme la nueva contraseña.|  
|ValidationErrorPasswordConfirmationRequired|El campo de la contraseña de confirmación está vacío.|  
|WebAuthenticationEmailChangeNotice|Correo electrónico de confirmación del cambio es demasiado en Hola {0}. Siga las instrucciones dentro de él tooconfirm la nueva dirección de correo electrónico. Si correo electrónico hello no llegan a Bandeja de entrada de tooyour Hola próximos minutos, compruebe la carpeta de correo electrónico no deseado.|  
|WebAuthenticationEmailChangeNoticeHeader|Se ha procesado correctamente la solicitud de cambio de correo electrónico.|  
|WebAuthenticationEmailChangeNoticeTitle|Cambio de correo electrónico solicitado|  
|WebAuthenticationEmailHasBeenRevertedNotice|Su dirección de correo electrónico ya existe. Se ha revertido la solicitud.|  
|ValidationErrorEmailAlreadyExists|La dirección de correo electrónico ya existe.|  
|ValidationErrorEmailInvalid|Dirección de correo electrónico no válida|  
|TextboxLabelEmail|Email|  
|ValidationErrorEmailRequired|Debe especificar un correo electrónico.|  
|WebAuthenticationErrorNoticeHeader|Error|  
|WebAuthenticationFieldLengthErrorMessage|{0} debe tener una extensión máxima de {1}.|  
|TextboxLabelEmailFirstName|Nombre|  
|ValidationErrorFirstNameRequired|Debe especificar un nombre.|  
|ValidationErrorFirstNameInvalid|Nombre no válido|  
|NoticeInvalidInvitationToken|Tenga en cuenta que los vínculos de confirmación solo son válidos durante 48 horas. Si aún no ha superado ese plazo, asegúrese de que el vínculo sea correcto. Si ha expirado el vínculo, a continuación, repita la acción de Hola que está tratando de tooconfirm.|  
|NoticeHeaderInvalidInvitationToken|Token de invitación no válido|  
|NoticeTitleInvalidInvitationToken|Correo electrónico de confirmación|  
|WebAuthenticationLastNameInvalidErrorMessage|Apellidos no válidos|  
|TextboxLabelEmailLastName|Apellidos|  
|ValidationErrorLastNameRequired|Debe especificar un apellido.|  
|WebAuthenticationLinkExpiredNotice|Vínculo de confirmación enviado tooyou ha expirado. `<a href={0}?token={1}>Resend confirmation email.</a\>`|  
|NoticePasswordResetLinkInvalidOrExpired|El vínculo de restablecimiento de la contraseña no es válido o ha expirado.|  
|WebAuthenticationLinkExpiredNoticeTitle|Vínculo enviado|  
|WebAuthenticationNewPasswordLabel|Contraseña nueva|  
|ValidationMessageNewPasswordRequired|Se requiere una nueva contraseña.|  
|TextboxLabelNotificationsSenderEmail|Correo electrónico del remitente de las notificaciones|  
|TextboxLabelOrganizationName|Nombre de la organización|  
|WebAuthenticationOrganizationRequiredErrorMessage|El campo del nombre de la organización está vacío.|  
|WebAuthenticationPasswordChangedNotice|La contraseña se ha actualizado correctamente.|  
|WebAuthenticationPasswordChangedNoticeTitle|Contraseña actualizada|  
|WebAuthenticationPasswordCompareErrorMessage|Las contraseñas no coinciden.|  
|WebAuthenticationPasswordConfirmLabel|Confirmar contraseña|  
|ValidationErrorPasswordInvalidDetailed|La contraseña es demasiado poco segura.|  
|WebAuthenticationPasswordLabel|Password|  
|ValidationErrorPasswordRequired|Se requiere una contraseña.|  
|WebAuthenticationPasswordResetSendNotice|Correo electrónico de confirmación de contraseña de cambio es demasiado en Hola {0}. Siga las instrucciones de hello en toocontinue de correo electrónico de hello el proceso de cambio de contraseña.|  
|WebAuthenticationPasswordResetSendNoticeHeader|La solicitud de restablecimiento de contraseña se ha procesado correctamente.|  
|WebAuthenticationPasswordResetSendNoticeTitle|Se solicitó el restablecimiento de contraseña.|  
|WebAuthenticationRequestNotFoundNotice|Solicitud no encontrada|  
|WebAuthenticationSenderEmailRequiredErrorMessage|El campo del correo electrónico del remitente de las notificaciones está vacío.|  
|WebAuthenticationSigninPasswordLabel|Para confirmar el cambio de Hola especificando una contraseña|  
|WebAuthenticationSignupConfirmNotice|Correo electrónico de confirmación de registro se encuentra en su forma demasiado {0}. < br /\> vuelva siga las instrucciones dentro de saludo de correo electrónico tooactivate tu cuenta. < br /\> si correo electrónico hello no llega en la Bandeja de entrada en hello próximos minutos, compruebe la carpeta de correo electrónico no deseado.|  
|WebAuthenticationSignupConfirmNoticeHeader|La cuenta se ha creado correctamente.|  
|WebAuthenticationSignupConfirmNoticeRepeatHeader|Se ha vuelto a enviar el mensaje de correo electrónico de confirmación de registro.|  
|WebAuthenticationSignupConfirmNoticeTitle|Cuenta creada|  
|WebAuthenticationTokenRequiredErrorMessage|El token está vacío.|  
|WebAuthenticationUserAlreadyRegisteredNotice|Parece que un usuario con este correo electrónico ya está registrado en el sistema de Hola. Si ha olvidado su contraseña, vuelva intentarlo toorestore, o póngase en contacto con nuestro equipo de soporte técnico.|  
|WebAuthenticationUserAlreadyRegisteredNoticeHeader|El usuario ya está registrado.|  
|WebAuthenticationUserAlreadyRegisteredNoticeTitle|Ya registrado|  
|ButtonLabelChangePassword|Cambiar contraseña|  
|ButtonLabelChangeAccountInfo|Cambiar información de la cuenta|  
|ButtonLabelCloseAccount|Cerrar cuenta|  
|WebAuthenticationInvalidCaptchaErrorMessage|El texto escrito no coincide con el texto en la imagen de Hola. Vuelva a intentarlo.|  
|ValidationErrorCredentialsInvalid|El correo electrónico o la contraseña no son válidos. Corrija los errores de Hola y vuelva a intentarlo.|  
|WebAuthenticationRequestIsNotValid|La solicitud no es válida.|  
|WebAuthenticationUserIsNotConfirm|Para confirmar el registro antes de intentar toosign en.|  
|WebAuthenticationInvalidEmailFormated|El correo electrónico no es válido: {0}|  
|WebAuthenticationUserNotFound|Usuario no encontrado|  
|WebAuthenticationTenantNotRegistered|La cuenta pertenece a tooa inquilino de Azure Active Directory que no está autorizado tooaccess este portal.|  
|WebAuthenticationAuthenticationFailed|Error de autenticación.|  
|WebAuthenticationGooglePlusNotEnabled|Error de autenticación. Si autorizado aplicación hello, póngase en contacto con hello admin toomake seguro que la autenticación de Google está configurada correctamente.|  
|ValidationErrorAllowedTenantIsRequired|Se requiere un inquilino permitido.|  
|ValidationErrorTenantIsNotValid|inquilino de Azure Active Directory Hello '{0}' no es válido.|  
|WebAuthenticationActiveDirectoryTitle|Azure Active Directory|  
|WebAuthenticationLoginUsingYourProvider|Inicie sesión con su cuenta de {0}.|  
|WebAuthenticationUserLimitNotice|Este servicio ha alcanzado el número máximo de Hola de usuarios permitidos. Por favor, `<a href="mailto:{0}"\>contact hello administrator</a\>` tooupgrade su servicio y volver a habilitar el registro del usuario.|  
|WebAuthenticationUserLimitNoticeHeader|Registro de usuarios deshabilitado|  
|WebAuthenticationUserLimitNoticeTitle|Registro de usuarios deshabilitado|  
|WebAuthenticationUserRegistrationDisabledNotice|Se ha deshabilitado el registro de usuarios administrador Hola. Inicie sesión con el proveedor de identidades externo.|  
|WebAuthenticationUserRegistrationDisabledNoticeHeader|Registro de usuarios deshabilitado|  
|WebAuthenticationUserRegistrationDisabledNoticeTitle|Registro de usuarios deshabilitado|  
|WebAuthenticationSignupPendingConfirmationNotice|Antes de que podemos completar creación Hola de su cuenta, es necesario tooverify su dirección de correo electrónico. Hemos enviado un correo electrónico demasiado {0}. Siga las instrucciones de Hola Hola tooactivate de correo electrónico dentro de su cuenta. Si correo electrónico hello no llega en hello próximos minutos, compruebe la carpeta de correo electrónico no deseado.|  
|WebAuthenticationSignupPendingConfirmationAccountFoundNotice|Se encontró una cuenta sin confirmar dirección de correo electrónico de Hola {0}. creación de hello toocomplete de su cuenta que necesitamos tooverify su dirección de correo electrónico. Hemos enviado un correo electrónico demasiado {0}. Siga las instrucciones de Hola Hola tooactivate de correo electrónico dentro de su cuenta. Si correo electrónico hello no llega en hello próximos minutos, compruebe la carpeta de correo electrónico no deseado|  
|WebAuthenticationSignupConfirmationAlmostDone|Casi ha terminado.|  
|WebAuthenticationSignupConfirmationEmailSent|Hemos enviado un correo electrónico demasiado {0}. Siga las instrucciones de Hola Hola tooactivate de correo electrónico dentro de su cuenta. Si correo electrónico hello no llega en hello próximos minutos, compruebe la carpeta de correo electrónico no deseado.|  
|WebAuthenticationEmailSentNotificationMessage|Correo electrónico enviado correctamente demasiado {0}|  
|WebAuthenticationNoAadTenantConfigured|Ningún inquilino de Azure Active Directory configurado para el servicio de Hola.|  
|CheckboxLabelUserRegistrationTermsConsentRequired|Muestro mi conformidad toohello `<a data-toggle="modal" href="#" data-target="#terms"\>Terms of Use</a\>`.|  
|TextblockUserRegistrationTermsProvided|Revise los `<a data-toggle="modal" href="#" data-target="#terms"\>Terms of Use.</a\>`.|  
|DialogHeadingTermsOfUse|Términos de uso|  
|ValidationMessageConsentNotAccepted|Debe aceptar los términos de uso toohello antes de continuar.|  
  
###  <a name="SigninStrings"></a> SigninStrings  
  
|Nombre|Texto|  
|----------|----------|  
|WebAuthenticationForgotPassword|¿Ha olvidado la contraseña?|  
|WebAuthenticationIfAdministrator|Si es administrador, debe iniciar sesión en `<a href="{0}"\>here</a\>`.|  
|WebAuthenticationNotAMember|¿Aún no es miembro? `<a href="/signup"\>Sign up now</a\>`|  
|WebAuthenticationRemember|Recordarme en este equipo|  
|WebAuthenticationSigininWithPassword|Inicie sesión con su nombre de usuario y contraseña.|  
|WebAuthenticationSigninTitle|Iniciar sesión|  
|WebAuthenticationSignUpNow|Regístrese ahora|  
  
###  <a name="SignupStrings"></a> SignupStrings  
  
|Nombre|Texto|  
|----------|----------|  
|PageTitleSignup|Suscripción|  
|WebAuthenticationAlreadyAMember|¿Ya es miembro?|  
|WebAuthenticationCreateNewAccount|Cree una nueva cuenta de API Management.|  
|WebAuthenticationSigninNow|Inicie sesión ahora|  
|ButtonLabelSignup|Suscripción|  
  
###  <a name="SubscriptionListStrings"></a> SubscriptionListStrings  
  
|Nombre|Texto|  
|----------|----------|  
|SubscriptionCancelConfirmation|¿Está seguro de que desea toocancel esta suscripción?|  
|SubscriptionRenewConfirmation|¿Está seguro de que desea toorenew esta suscripción?|  
|WebDevelopersManageSubscriptions|Administrar suscripciones|  
|WebDevelopersPrimaryKey|Clave principal|  
|WebDevelopersRegenerateLink|Regenerar|  
|WebDevelopersSecondaryKey|Clave secundaria|  
|ButtonLabelShowKey|Presentación|  
|ButtonLabelRenewSubscription|Renovación|  
|WebDevelopersSubscriptionReqested|Solicitud realizada el {0}|  
|WebDevelopersSubscriptionRequestedState|Solicitada|  
|WebDevelopersSubscriptionTableNameHeader|Nombre|  
|WebDevelopersSubscriptionTableStateHeader|Estado|  
|WebDevelopersUsageStatisticsLink|Informes de análisis|  
|WebDevelopersYourSubscriptions|Sus suscripciones|  
|SubscriptionPropertyLabelRequestedDate|Solicitud realizada el|  
|SubscriptionPropertyLabelStartedDate|Iniciado el|  
|PageTitleRenameSubscription|Cambiar el nombre de la suscripción|  
|SubscriptionPropertyLabelName|Nombre de la suscripción|  
  
###  <a name="SubscriptionStrings"></a> SubscriptionStrings  
  
|Nombre|Texto|  
|----------|----------|  
|SectionHeadingCloseAccount|¿Buscar tooclose su cuenta?|  
|PageTitleDeveloperProfile|Perfil|  
|ButtonLabelHideKey|Ocultar|  
|ButtonLabelRegenerateKey|Regenerar|  
|InformationMessageKeyWasRegenerated|¿Está seguro de que desea tooregenerate esta clave?|  
|ButtonLabelShowKey|Presentación|  
  
###  <a name="UpdateProfileStrings"></a> UpdateProfileStrings  
  
|Nombre|Texto|  
|----------|----------|  
|ButtonLabelUpdateProfile|Actualizar perfil|  
|PageTitleUpdateProfile|Actualizar información de cuenta|  
  
###  <a name="UserProfile"></a> UserProfile  
  
|Nombre|Texto|  
|----------|----------|  
|ButtonLabelChangeAccountInfo|Cambiar información de la cuenta|  
|ButtonLabelChangePassword|Cambiar contraseña|  
|ButtonLabelCloseAccount|Cerrar cuenta|  
|TextboxLabelEmail|Email|  
|TextboxLabelEmailFirstName|Nombre|  
|TextboxLabelEmailLastName|Apellidos|  
|TextboxLabelNotificationsSenderEmail|Correo electrónico del remitente de las notificaciones|  
|TextboxLabelOrganizationName|Nombre de la organización|  
|SubscriptionStateActive|Active|  
|SubscriptionStateCancelled|Cancelado|  
|SubscriptionStateExpired|Expirada|  
|SubscriptionStateRejected|Rechazada|  
|SubscriptionStateRequested|Solicitada|  
|SubscriptionStateSuspended|Suspended|  
|DefaultSubscriptionNameTemplate|{0} (predeterminado)|  
|SubscriptionNameTemplate|Acceso de desarrollador n.º {0}|  
|TextboxLabelSubscriptionName|Nombre de la suscripción|  
|ValidationMessageSubscriptionNameRequired|El nombre de suscripción no puede estar vacío.|  
|ApiManagementUserLimitReached|Este servicio ha alcanzado el número máximo de Hola de usuarios permitidos. Actualice tooa cuanto mayor sea el nivel de precios.|  
  
##  <a name="glyphs"></a> Recursos de glifo  
 Plantillas del portal de administración de API para desarrolladores pueden usar glifos Hola de [Glyphicons de arranque](http://getbootstrap.com/components/#glyphicons). Este conjunto de glifos incluye más de 250 glifos en formato de fuente de hello [Glyphicon](http://glyphicons.com/) Halflings establecido. toouse un glifo de este conjunto, usar la sintaxis de hello.  
  
```html  
<span class="glyphicon glyphicon-user">  
```  
  
 Lista completa de Hola de glifos, encontrará [Glyphicons de arranque](http://getbootstrap.com/components/#glyphicons).

## <a name="next-steps"></a>Pasos siguientes
Para obtener más información sobre cómo trabajar con plantillas, consulte [cómo toocustomize Hola portal de administración de API para desarrolladores con plantillas de](api-management-developer-portal-templates.md).
