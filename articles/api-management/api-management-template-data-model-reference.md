---
title: "referencia de modelo de datos de la plantilla de aaaAzure administración de API | Documentos de Microsoft"
description: "Obtenga información acerca de las representaciones de entidad y tipo de Hola para elementos comunes utilizados en modelos de datos de Hola para plantillas del portal para desarrolladores de hello en la administración de API de Azure."
services: api-management
documentationcenter: 
author: miaojiang
manager: erikre
editor: 
ms.assetid: b0ad7e15-9519-4517-bb73-32e593ed6380
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/09/2017
ms.author: apimpm
ms.openlocfilehash: 7d049d8ecc9e597cf48ce0c820c172798bcf86de
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="azure-api-management-template-data-model-reference"></a>Referencia de modelo de datos de la plantilla de Azure API Management
Este tema describen las representaciones de entidad y tipo de Hola para elementos comunes utilizadas en modelos de datos de Hola para plantillas del portal para desarrolladores de hello en la administración de API de Azure.  
  
 Para obtener más información sobre cómo trabajar con plantillas, consulte [cómo toocustomize Hola portal de administración de API para desarrolladores con plantillas de](https://azure.microsoft.com/documentation/articles/api-management-developer-portal-templates/).  
  
-   [API](#API)  
-   [Resumen de API](#APISummary)  
-   [Aplicación](#Application)  
-   [Datos adjuntos](#Attachment)  
-   [Código de ejemplo](#Sample)  
-   [Comment](#Comment)  
-   [Filtrado](#Filtering)  
-   [Encabezado](#Header)  
-   [Solicitud HTTP](#HTTPRequest)  
-   [Respuesta HTTP](#HTTPResponse)  
-   [Problema](#Issue)  
-   [Operación](#Operation)  
-   [Menú de operaciones](#Menu)  
-   [Elemento de menú de operaciones](#MenuItem)  
-   [Paginación](#Paging)  
-   [Parámetro](#Parameter)  
-   [Producto](#Product)  
-   [Proveedor](#Provider)  
-   [Representación](#Representation)  
-   [Suscripción](#Subscription)  
-   [Resumen de suscripción](#SubscriptionSummary)  
-   [Información de cuenta de usuario](#UserAccountInfo)  
-   [Inicio de sesión de usuario](#UseSignIn)  
-   [Suscripción de usuario](#UserSignUp)  
  
##  <a name="API"></a> API  
 Hola `API` entidad tiene Hola propiedades siguientes.  
  
|Propiedad|Escriba|Descripción|  
|--------------|----------|-----------------|  
|id|string|Identificador de recursos. Identifica de forma única API de hello dentro de la instancia de servicio de administración de API actual Hola. valor de Hello es una URL relativa válida con formato hello `apis/{id}` donde `{id}` es un identificador de API. Esta propiedad es de solo lectura.|  
|name|cadena|Nombre del programa Hola a API. No debe estar vacía. La longitud máxima es de 100 caracteres.|  
|Description|cadena|Descripción de hello API. No debe estar vacía. Puede incluir etiquetas de formato HTML. La longitud máxima es de 1000 caracteres.|  
|serviceUrl|cadena|Dirección URL absoluta del servicio de back-end de hello implementa esta API.|  
|path|cadena|Dirección URL relativa que identifica de forma única esta API y todos sus rutas de acceso de recursos dentro de la instancia de servicio de administración de API de Hola. Se anexa toohello API dirección URL base del extremo especificado durante la tooform de creación de instancia de servicio de hello una dirección URL pública para esta API.|  
|protocols|matriz de número|Describe en qué Hola protocolos se pueden invocar operaciones en esta API. Los valores permitidos son `1 - http` y `2 - https`, o ambos.|  
|authenticationSettings|[Configuración de autenticación del servidor de autorización](https://docs.microsoft.com/rest/api/apimanagement/apimanagementrest/azure-api-management-rest-api-contract-reference#AuthenticationSettings)|Colección de ajustes de autenticación que se incluyen en esta API.|  
|subscriptionKeyParameterNames|objeto|Propiedad opcional que puede ser usado toospecify nombres personalizados para los parámetros de consulta o de encabezado que contiene la clave de la suscripción de Hola. Cuando esta propiedad está presente debe contener al menos uno de los dos siguientes propiedades de Hola.<br /><br /> `{   "subscriptionKeyParameterNames":   {     "query": “customQueryParameterName",     "header": “customHeaderParameterName"   } }`|  
  
##  <a name="APISummary"></a> Resumen de API  
 Hola `API summary` entidad tiene Hola propiedades siguientes.  
  
|Propiedad|Escriba|Descripción|  
|--------------|----------|-----------------|  
|id|string|Identificador de recursos. Identifica de forma única API de hello dentro de la instancia de servicio de administración de API actual Hola. valor de Hello es una URL relativa válida con formato hello `apis/{id}` donde `{id}` es un identificador de API. Esta propiedad es de solo lectura.|  
|name|cadena|Nombre del programa Hola a API. No debe estar vacía. La longitud máxima es de 100 caracteres.|  
|Description|cadena|Descripción de hello API. No debe estar vacía. Puede incluir etiquetas de formato HTML. La longitud máxima es de 1000 caracteres.|  
  
##  <a name="Application"></a> Application  
 Hola `application` entidad tiene Hola propiedades siguientes.  
  
|Propiedad|Escriba|Descripción|  
|--------------|----------|-----------------|  
|Id|cadena|Hola identificador único de la aplicación hello.|  
|Título|cadena|título de Hola de aplicación hello.|  
|Descripción|cadena|Descripción de Hola de aplicación hello.|  
|URL|URI|Hola URI para la aplicación hello.|  
|Versión|cadena|Información de versión de la aplicación hello.|  
|Requisitos|cadena|Una descripción de los requisitos para la aplicación hello.|  
|Estado|número|estado actual de Hola de aplicación hello.<br /><br /> -0 - registrada<br /><br /> -1 - enviada<br /><br /> -2 - publicada<br /><br /> -3 - rechazada<br /><br /> -4 - no publicada|  
|RegistrationDate|DateTime|se registró la aplicación hello de fecha y hora de Hello.|  
|CategoryId|número|categoría de Hola de aplicación hello (Finanzas, entretenimiento, etcetera).|  
|DeveloperId|cadena|Identificador único de Hola de desarrollador de Hola que envía la aplicación hello.|  
|Datos adjuntos|Colección de entidades [Attachment](#Attachment).|Los datos adjuntos para la aplicación hello como capturas de pantalla o iconos.|  
|Icono|[Datos adjuntos](#Attachment)|Hola Hola de icono para aplicación hello.|  
  
##  <a name="Attachment"></a> Datos adjuntos  
 Hola `attachment` entidad tiene Hola propiedades siguientes.  
  
|Propiedad|Escriba|Descripción|  
|--------------|----------|-----------------|  
|UniqueId|cadena|Identificador único de Hola para datos adjuntos de Hola.|  
|URL|cadena|Hola dirección URL del recurso de Hola.|  
|Tipo|cadena|tipo de Hola de datos adjuntos.|  
|ContentType|cadena|tipo de medio de Hola de datos adjuntos de Hola.|  
  
##  <a name="Sample"></a> Código de ejemplo  
  
|Propiedad|Escriba|Descripción|  
|--------------|----------|-----------------|  
|título|cadena|nombre de Hola de operación de Hola.|  
|snippet|string|Esta propiedad está en desuso y no debe utilizarse.|  
|brush|cadena|Que el código de color toobe de plantilla utilizado para mostrar el ejemplo de código de hello de sintaxis. Los valores permitidos son `plain`, `php`, `java`, `xml`, `objc`, `python`, `ruby` y `csharp`.|  
|template|cadena|nombre de Hola de esta plantilla de ejemplo de código.|  
|body|cadena|Un marcador de posición para parte de ejemplo de código de hello de fragmento de código de hello.|  
|estático|cadena|método HTTP de la operación de Hola Hola.|  
|scheme|cadena|Hola toouse de protocolo para la solicitud de operación de Hola.|  
|path|cadena|ruta de acceso de Hola de operación de Hola.|  
|query|string|Ejemplo de cadena de consulta con parámetros definidos.|  
|host|cadena|dirección URL de Hola de puerta de enlace del servicio de administración de API de Hola para hello API que contiene esta operación.|  
|encabezados|Colección de entidades [Header](#Header).|Encabezados de esta operación.|  
|parameters|Colección de entidades [Parameter](#Parameter).|Los parámetros definidos para esta operación.|  
  
##  <a name="Comment"></a> Comment  
 Hola `API` entidad tiene Hola propiedades siguientes.  
  
|Propiedad|Escriba|Descripción|  
|--------------|----------|-----------------|  
|Id|número|Id. de Hola de comentario de Hola.|  
|CommentText|cadena|cuerpo de Hola de comentario de Hola. Puede incluir HTML.|  
|DeveloperCompany|cadena|nombre de la compañía de Hola de desarrollador de Hola.|  
|PostedOn|DateTime|comentario de Hola de fecha y hora de Hola se ha registrado.|  
  
##  <a name="Issue"></a> Issue  
 Hola `issue` entidad tiene Hola propiedades siguientes.  
  
|Propiedad|Escriba|Descripción|  
|--------------|----------|-----------------|  
|Id|cadena|Identificador único de Hello para el problema de Hola.|  
|ApiID|cadena|Id. de Hello para la API de hello para el que se notificó este problema.|  
|Título|cadena|Título del problema de Hola.|  
|Descripción|cadena|Descripción del problema de Hola.|  
|SubscriptionDeveloperName|cadena|Nombre del desarrollador de Hola que Hola problemas notificados.|  
|IssueState|cadena|estado actual de Hello del problema de Hola. Los valores posibles son Proposed (Propuesto), Opened (Abierto), Closed (Cerrado).|  
|ReportedOn|DateTime|se detectó el problema de Hola de fecha y hora de Hola.|  
|Comentarios|Colección de entidades [Comment](#Comment).|Comentarios sobre este problema.|  
|Datos adjuntos|Colección de entidades [Attachment](api-management-template-data-model-reference.md#Attachment).|Cualquier problema de toohello los datos adjuntos.|  
|Services|Colección de entidades [API](#API).|Hola API suscrito usuario de hello tooby que archivó problema Hola.|  
  
##  <a name="Filtering"></a> Filtrado  
 Hola `filtering` entidad tiene Hola propiedades siguientes.  
  
|Propiedad|Escriba|Descripción|  
|--------------|----------|-----------------|  
|Patrón|cadena|término de búsqueda actual de Hola o `null` si no hay ningún término de búsqueda.|  
|Placeholder|cadena|Hola toodisplay de texto en el cuadro de búsqueda de hello cuando no hay ningún término de búsqueda especificado.|  
  
##  <a name="Header"></a> Header  
 Esta sección describen hello `parameter` representación.  
  
|Propiedad|Descripción|Escriba|  
|--------------|-----------------|----------|  
|name|string|Nombre del parámetro.|  
|Description|string|Descripción del parámetro.|  
|value|string|Valor del encabezado.|  
|typeName|string|Tipo de datos del valor del encabezado.|  
|options|string|Opciones.|  
|requerido|boolean|Si el encabezado de hello es obligatorio.|  
|readOnly|boolean|Si el encabezado de hello es de solo lectura.|  
  
##  <a name="HTTPRequest"></a> HTTP Request  
 Esta sección describen hello `request` representación.  
  
|Propiedad|Escriba|Descripción|  
|--------------|----------|-----------------|  
|Description|string|Descripción de la solicitud de operación.|  
|Encabezados|matriz de entidades [Header](#Header).|Encabezados de solicitud.|  
|parameters|matriz de [Parameter](#Parameter)|Colección de parámetros de solicitud de operación.|  
|representations|matriz de [Representation](#Representation)|Colección de representaciones de solicitud de operación.|  
  
##  <a name="HTTPResponse"></a> HTTP Response  
 Esta sección describen hello `response` representación.  
  
|Propiedad|Escriba|Descripción|  
|--------------|----------|-----------------|  
|statusCode|número entero positivo|Código de estado de la respuesta de la operación.|  
|Description|string|Descripción de la respuesta de la operación.|  
|representations|matriz de [Representation](#Representation)|Colección de representaciones de respuesta de operación.|  
  
##  <a name="Operation"></a> Operation  
 Hola `operation` entidad tiene Hola propiedades siguientes.  
  
|Propiedad|Escriba|Descripción|  
|--------------|----------|-----------------|  
|id|string|Identificador de recursos. Identifica de forma única operación Hola dentro de la instancia de servicio de administración de API actual Hola. valor de Hello es una URL relativa válida con formato hello `apis/{aid}/operations/{id}` donde `{aid}` es un identificador de API y `{id}` es un identificador de operación. Esta propiedad es de solo lectura.|  
|name|cadena|Nombre de operación de Hola. No debe estar vacía. La longitud máxima es de 100 caracteres.|  
|Description|cadena|Descripción de operación de Hola. No debe estar vacía. Puede incluir etiquetas de formato HTML. La longitud máxima es de 1000 caracteres.|  
|scheme|cadena|Describe en qué Hola protocolos se pueden invocar operaciones en esta API. Los valores permitidos son `http`, `https` o tanto `http` como `https`.|  
|uriTemplate|cadena|Plantilla de dirección URL relativa identifica el recurso de destino de Hola para esta operación. Puede incluir parámetros. Ejemplo: `customers/{cid}/orders/{oid}/?date={date}`|  
|host|cadena|Hola dirección URL de puerta de enlace de administración de API que hospeda la API de Hola.|  
|httpMethod|string|Método HTTP de la operación.|  
|request|[Solicitud HTTP](#HTTPRequest)|Una entidad que contiene los detalles de la solicitud.|  
|responses|matriz de [HTTP Response](#HTTPResponse)|Matriz de entidades [HTTP Response](#HTTPResponse) de la operación.|  
  
##  <a name="Menu"></a> Menú de operaciones  
 Hola `operation menu` entidad tiene Hola propiedades siguientes.  
  
|Propiedad|Escriba|Descripción|  
|--------------|----------|-----------------|  
|ApiId|cadena|Id. de Hola de API actual Hola.|  
|CurrentOperationId|cadena|Hola Id. de operación actual Hola.|  
|Acción|cadena|Hola menu (tipo).|  
|MenuItems|Colección de entidades [Operation menu item](#MenuItem).|operaciones de Hola de API actual de Hola.|  
  
##  <a name="MenuItem"></a> Elemento de menú de operaciones  
 Hola `operation menu item` entidad tiene Hola propiedades siguientes.  
  
|Propiedad|Escriba|Descripción|  
|--------------|----------|-----------------|  
|Id|cadena|Hola Id. de operación de Hola.|  
|Título|cadena|Descripción de Hola de operación de Hola.|  
|HttpMethod|cadena|método Http de la operación de Hola Hola.|  
  
##  <a name="Paging"></a> Paginación  
 Hola `paging` entidad tiene Hola propiedades siguientes.  
  
|Propiedad|Escriba|Descripción|  
|--------------|----------|-----------------|  
|Page|número|número de página actual de Hola.|  
|PageSize|número|Hola toobe de número máximo de resultados que se muestran en una sola página.|  
|TotalItemCount|número|número de Hola de elementos para su presentación.|  
|ShowAll|boolean|Si toosho todos los resultados en una sola página.|  
|PageCount|número|número de Hola de páginas de resultados.|  
  
##  <a name="Parameter"></a> Parameter  
 Esta sección describen hello `parameter` representación.  
  
|Propiedad|Descripción|Escriba|  
|--------------|-----------------|----------|  
|name|string|Nombre del parámetro.|  
|Description|string|Descripción del parámetro.|  
|value|string|Valor del parámetro.|  
|options|matriz de cadena|Valores definidos para los valores de parámetro de consulta.|  
|requerido|boolean|Especifica si el parámetro es necesario o no.|  
|kind|número|Determina si este parámetro es un parámetro de ruta de acceso (1) o un parámetro de cadena de consulta (2).|  
|typeName|string|Tipo de parámetro.|  
  
##  <a name="Product"></a> Product  
 Hola `product` entidad tiene Hola propiedades siguientes.  
  
|Propiedad|Escriba|Descripción|  
|--------------|----------|-----------------|  
|Id|string|Identificador de recursos. Identifica de forma única el producto de hello dentro de la instancia de servicio de administración de API actual Hola. valor de Hello es una URL relativa válida con formato hello `products/{pid}` donde `{pid}` es un identificador de producto. Esta propiedad es de solo lectura.|  
|Título|cadena|Nombre del producto de Hola. No debe estar vacía. La longitud máxima es de 100 caracteres.|  
|Descripción|cadena|Descripción del producto de Hola. No debe estar vacía. Puede incluir etiquetas de formato HTML. La longitud máxima es de 1000 caracteres.|  
|Términos|string|Términos de uso del producto. Los desarrolladores que traten toosubscribe toohello producto aparecerá y necesario tooaccept estos términos antes de completar el proceso de suscripción de Hola.|  
|ProductState|número|Especifica si se publica el producto de Hola o no. Productos publicados son reconocibles de los desarrolladores en el portal para desarrolladores de Hola. Los productos no publicados son visibles tooadministrators única.<br /><br /> Hola valores permitidos para el estado del producto son:<br /><br /> - `0 - Not Published`<br /><br /> - `1 - Published`<br /><br /> - `2 - Deleted`|  
|AllowMultipleSubscriptions|boolean|Especifica si un usuario puede tener varios productos de toothis de suscripciones en hello mismo tiempo.|  
|MultipleSubscriptionsCount|número|número de Hola de producto de toothis de suscripciones por el usuario actual de Hola.|  
  
##  <a name="Provider"></a> Provider  
 Hola `provider` entidad tiene Hola propiedades siguientes.  
  
|Propiedad|Escriba|Descripción|  
|--------------|----------|-----------------|  
|Propiedades|diccionario de cadenas|Propiedades de este proveedor de autenticación.|  
|AuthenticationType|cadena|tipo de proveedor de Hola. (Azure Active Directory, inicio de sesión de Facebook, cuenta de Google, cuenta de Microsoft, Twitter).|  
|Caption|cadena|Nombre para mostrar del proveedor de Hola.|  
  
##  <a name="Representation"></a> Representación  
 En esta sección se describe `representation`.  
  
|Propiedad|Escriba|Descripción|  
|--------------|----------|-----------------|  
|contentType|string|Especifica un tipo de contenido personalizado o registrado para esta representación, por ejemplo, `application/xml`.|  
|de Pi|cadena|Un ejemplo de representación de Hola.|  
  
##  <a name="Subscription"></a> Subscription  
 Hola `subscription` entidad tiene Hola propiedades siguientes.  
  
|Propiedad|Escriba|Descripción|  
|--------------|----------|-----------------|  
|Id|string|Identificador de recursos. Identifica de forma única suscripción Hola dentro de la instancia de servicio de administración de API actual Hola. valor de Hello es una URL relativa válida con formato hello `subscriptions/{sid}` donde `{sid}` es un identificador de suscripción. Esta propiedad es de solo lectura.|  
|ProductId|cadena|identificador de recurso de producto de Hola de hello suscrito el producto. valor de Hello es una URL relativa válida con formato hello `products/{pid}` donde `{pid}` es un identificador de producto.|  
|ProductTitle|cadena|Nombre del producto de Hola. No debe estar vacía. La longitud máxima es de 100 caracteres.|  
|ProductDescription|cadena|Descripción del producto de Hola. No debe estar vacía. Puede incluir etiquetas de formato HTML. La longitud máxima es de 1000 caracteres.|  
|ProductDetailsUrl|cadena|Detalles del producto toohello dirección URL relativos.|  
|state|cadena|estado de Hola de suscripción de Hola. Los estados posibles son:<br /><br /> - `0 - suspended`: Hola suscripción está bloqueada y suscriptor hello no puede llamar a las API del producto de Hola.<br /><br /> - `1 - active`: Hola suscripción está activa.<br /><br /> - `2 - expired`– suscripción Hola alcanza su fecha de expiración y se ha desactivado.<br /><br /> - `3 - submitted`: solicitud de suscripción de Hola se ha realizado por el desarrollador de hello, pero ha aún no aprobado o rechazados.<br /><br /> - `4 - rejected`: un administrador ha denegado la solicitud de suscripción de Hola.<br /><br /> - `5 - cancelled`: se ha cancelado la suscripción Hola programador de Hola o el administrador.|  
|DisplayName|cadena|Nombre para mostrar de la suscripción de Hola.|  
|CreatedDate|dateTime|se creó la suscripción de Hello fecha hello, en formato ISO 8601: `2014-06-24T16:25:00Z`.|  
|CanBeCancelled|boolean|Si se puede cancelar la suscripción de Hola por el usuario actual de Hola.|  
|IsAwaitingApproval|boolean|Si la suscripción de hello está esperando aprobación.|  
|StartDate|dateTime|Hola fecha inicial para la suscripción de hello, en formato ISO 8601: `2014-06-24T16:25:00Z`.|  
|ExpirationDate|dateTime|fecha de expiración de Hello para la suscripción de hello, en formato ISO 8601: `2014-06-24T16:25:00Z`.|  
|NotificationDate|dateTime|fecha de notificación de Hello para la suscripción de hello, en formato ISO 8601: `2014-06-24T16:25:00Z`.|  
|primaryKey|cadena|clave de suscripción principal Hola. La longitud máxima es de 256 caracteres.|  
|secondaryKey|cadena|clave de suscripción secundaria Hola. La longitud máxima es de 256 caracteres.|  
|CanBeRenewed|boolean|Si se puede renovar la suscripción de Hola por el usuario actual de Hola.|  
|HasExpired|boolean|Si la suscripción de hello ha expirado.|  
|IsRejected|boolean|Si se ha denegado la solicitud de suscripción de Hola.|  
|CancelUrl|cadena|Hola relativa Url toocancel Hola suscripción.|  
|RenewUrl|cadena|Hola relativa Url toorenew Hola suscripción.|  
  
##  <a name="SubscriptionSummary"></a> Resumen de suscripción  
 Hola `subscription summary` entidad tiene Hola propiedades siguientes.  
  
|Propiedad|Escriba|Descripción|  
|--------------|----------|-----------------|  
|Id|string|Identificador de recursos. Identifica de forma única suscripción Hola dentro de la instancia de servicio de administración de API actual Hola. valor de Hello es una URL relativa válida con formato hello `subscriptions/{sid}` donde `{sid}` es un identificador de suscripción. Esta propiedad es de solo lectura.|  
|DisplayName|cadena|nombre de suscripción de Hola para mostrar Hello|  
  
##  <a name="UserAccountInfo"></a> Información de cuenta de usuario  
 Hola `user account info` entidad tiene Hola propiedades siguientes.  
  
|Propiedad|Escriba|Descripción|  
|--------------|----------|-----------------|  
|Nombre|string|Nombre. No debe estar vacía. La longitud máxima es de 100 caracteres.|  
|Apellidos|string|Apellidos. No debe estar vacía. La longitud máxima es de 100 caracteres.|  
|Email|string|Dirección de correo electrónico. No debe estar vacío y debe ser único dentro de la instancia de servicio de Hola. La longitud máxima es de 254 caracteres.|  
|Password|string|Contraseña de la cuenta de usuario.|  
|NameIdentifier|cadena|Identificador de cuenta, hello igual que el correo electrónico del usuario Hola.|  
|ProviderName|string|Nombre del proveedor de autenticación.|  
|IsBasicAccount|boolean|Es True si esta cuenta se registró mediante correo electrónico y una contraseña; False si la cuenta de hello se registró con un proveedor.|  
  
##  <a name="UseSignIn"></a> Inicio de sesión de usuario  
 Hola `user sign in` entidad tiene Hola propiedades siguientes.  
  
|Propiedad|Escriba|Descripción|  
|--------------|----------|-----------------|  
|Email|string|Dirección de correo electrónico. No debe estar vacío y debe ser único dentro de la instancia de servicio de Hola. La longitud máxima es de 254 caracteres.|  
|Password|string|Contraseña de la cuenta de usuario.|  
|ReturnUrl|cadena|Hola dirección URL de página de Hola donde el usuario Hola hace clic en Inicio de sesión.|  
|RememberMe|boolean|Si toosave Hola información del usuario actual.|  
|RegistrationEnabled|boolean|Especifica si el registro se ha habilitado.|  
|DelegationEnabled|boolean|Especifica si está habilitado el inicio de sesión delegado.|  
|DelegationUrl|cadena|Hola delegados de dirección url de inicio de sesión si habilitado.|  
|SsoSignUpUrl|cadena|Hola único de sesión en la dirección URL para el usuario de hello, si está presente.|  
|AuxServiceUrl|cadena|Si el usuario actual de hello es un administrador, ésta es una instancia de servicio de vínculo toohello Hola Portal clásico de Azure.|  
|Proveedores|Colección de entidades [Provider](#Provider).|Hola proveedores de autenticación para este usuario.|  
|UserRegistrationTerms|cadena|Condiciones que un usuario debe aceptar toobefore inicio de sesión.|  
|UserRegistrationTermsEnabled|boolean|Especifica si las condiciones están habilitadas.|  
  
##  <a name="UserSignUp"></a> Suscripción de usuario  
 Hola `user sign up` entidad tiene Hola propiedades siguientes.  
  
|Propiedad|Escriba|Descripción|  
|--------------|----------|-----------------|  
|PasswordConfirm|boolean|Valor usado por hello [registro](api-management-page-controls.md#sign-up)control de inicio de sesión.|  
|Password|string|Contraseña de la cuenta de usuario.|  
|PasswordVerdictLevel|número|Valor usado por hello [registro](api-management-page-controls.md#sign-up)control de inicio de sesión.|  
|UserRegistrationTerms|cadena|Condiciones que un usuario debe aceptar toobefore inicio de sesión.|  
|UserRegistrationTermsOptions|número|Valor usado por hello [registro](api-management-page-controls.md#sign-up)control de inicio de sesión.|  
|ConsentAccepted|boolean|Valor usado por hello [registro](api-management-page-controls.md#sign-up)control de inicio de sesión.|  
|Email|string|Dirección de correo electrónico. No debe estar vacío y debe ser único dentro de la instancia de servicio de Hola. La longitud máxima es de 254 caracteres.|  
|Nombre|string|Nombre. No debe estar vacía. La longitud máxima es de 100 caracteres.|  
|Apellidos|string|Apellidos. No debe estar vacía. La longitud máxima es de 100 caracteres.|  
|UserData|cadena|Valor usado por hello [suscripción](api-management-page-controls.md#sign-up) control.|  
|NameIdentifier|cadena|Valor usado por hello [registro](api-management-page-controls.md#sign-up)control de inicio de sesión.|  
|ProviderName|string|Nombre del proveedor de autenticación.|

## <a name="next-steps"></a>Pasos siguientes
Para obtener más información sobre cómo trabajar con plantillas, consulte [cómo toocustomize Hola portal de administración de API para desarrolladores con plantillas de](api-management-developer-portal-templates.md).
