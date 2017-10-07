---
title: "aaaManage la primera API de administración de API de Azure | Documentos de Microsoft"
description: "Obtenga información acerca de cómo agregar operaciones toocreate API y empezar a trabajar con administración de API."
services: api-management
documentationcenter: 
author: steved0x
manager: erikre
editor: 
ms.assetid: 51b7df8b-1c43-43c6-90c9-0aa24f48206b
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: hero-article
ms.date: 12/15/2016
ms.author: apimpm
ms.openlocfilehash: 7d43f33aa359c4d1e605e9fb41e43d323ca6a777
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="manage-your-first-api-in-azure-api-management"></a>Administración de su primera API en Administración de API de Azure
## <a name="overview"></a>Información general
Esta guía muestra cómo tooquickly empezar a trabajar en el uso de administración de API de Azure y realizar la primera llamada de API.

## <a name="concepts"></a>¿Qué es la Administración de API de Azure?
Puede usar Administración de API de Azure tootake cualquier back-end e iniciar un programa completo de API basado en él.

Entre los escenarios habituales se incluyen los siguientes:

* **Protección de la infraestructura móvil** mediante el control de acceso con claves de API, la prevención de ataques de denegación de servicio mediante la limitación o el uso de directivas de seguridad avanzadas como la validación de tokens JWT.
* **Habilitación de ecosistemas de socio comercial de ISV** , ya que ofrece la incorporación de socios rápido por un desarrollador de hello portal y generar un toodecouple de fachada de API de las implementaciones internas que no son listo para consumo partner.
* **Ejecutar un programa de API interno** , ya que ofrece una ubicación centralizada para hello organización toocommunicate sobre la disponibilidad de Hola y la versión más reciente de tooAPIs los cambios, el control de acceso en función de las cuentas organizativas, basadas en un canal seguro entre puerta de enlace de API de Hola y Hola back-end.

sistema de Hola se compone de Hola de los componentes siguientes:

* Hola **puerta de enlace de API** es el punto de conexión de Hola que:
  
  * Acepta llamadas API y los enruta tooyour back-ends.
  * Comprueba las claves de API, los tokens JWT, los certificados y otras credenciales.
  * Aplica cuotas de uso y límites de frecuencia.
  * Transforma la API en marcha Hola sin modificaciones en el código.
  * Almacena en caché las respuestas de back-end donde se instalaron.
  * Registra los metadatos de llamada para fines de análisis.
* Hola **portal para desarrolladores de** es la interfaz administrativa de Hola donde configuró el programa de API. Utilícelo para:
  
  * definir o importar el esquema de API
  * empaquetar las API en productos
  * Configure directivas como las cuotas o transformaciones en hello API.
  * obtener información del análisis
  * administrar usuarios
* Hola **portal para desarrolladores de** actúa como la presencia de hello web principal para los desarrolladores, siempre sea posible:
  
  * leer documentación de la API
  * Pruebe una API a través de la consola interactiva Hola.
  * Crear una cuenta y suscribirse tooget API claves.
  * obtener acceso a análisis sobre su propio uso

## <a name="create-service-instance"></a>Creación de una instancia de Administración de API
> [!NOTE]
> toocomplete este tutorial, necesita una cuenta de Azure. En caso de no tener ninguna, puede crear una cuenta gratuita en tan solo unos minutos. Para más información, consulte la [evaluación gratuita de Azure][Azure Free Trial].
> 
> 

primer paso para trabajar con la API de administración de Hello es toocreate una instancia de servicio. Inicie sesión en toohello [Portal de Azure] [ Azure Portal] y haga clic en **New**, **Web y móvil**, **administración de API**.

![API Management new instance][api-management-create-instance-menu]

Para **nombre**, especifique un toouse de nombre de subdominio único para la dirección URL del servicio de Hola.

Elija Hola deseado **suscripción**, **grupo de recursos** y **ubicación** para la instancia de servicio.

Escriba **Contoso Ltd.** para hello **nombreDeOrganización**y escriba la dirección de correo electrónico en hello **correo electrónico del administrador** campo.

> [!NOTE]
> Esta dirección de correo electrónico se usa para recibir notificaciones del sistema de administración de API de Hola. Para obtener más información, consulte [cómo tooconfigure notificaciones y plantillas en la administración de API de Azure de correo electrónico][How tooconfigure notifications and email templates in Azure API Management].
> 
> 

![New API Management service][api-management-create-instance-step1]

Las instancias de servicio de Administración de API están disponibles en tres niveles: Desarrollador, Estándar y Premium.

> [!NOTE]
> Hola nivel desarrollador es para el desarrollo, prueba y pilotos programas de API que la alta disponibilidad no es un problema. En hello estándar y niveles de Premium, puede escalar su toohandle de recuento de unidad reservada más tráfico. niveles de Standard y Premium de Hello proporcionan el servicio de administración de API con hello mayoría potencia de procesamiento y el rendimiento. Puede completar este tutorial mediante cualquier nivel. Para más información acerca de los niveles de API Management, consulte [Precios de API Management][API Management pricing].
> 
> 

Haga clic en **crear** toostart aprovisionamiento de la instancia del servicio.

![New API Management service][api-management-instance-created]

Una vez creada la instancia de servicio de hello, paso siguiente hello es toocreate o importar una API.

## <a name="create-api"></a>Importación de una API
Una API consta de un conjunto de operaciones que se pueden invocar desde una aplicación cliente. Las operaciones de API son servicios de tooexisting procesadas por el proxy web.

Las API se pueden crear (y las operaciones se pueden agregar) manualmente o se pueden importar. En este tutorial, se importará Hola API para un servicio de web de calculadora de ejemplo proporcionados por Microsoft y hospedadas en Azure.

> [!NOTE]
> Para obtener instrucciones sobre cómo crear una API y agregar manualmente las operaciones, vea [cómo toocreate API](api-management-howto-create-apis.md) y [cómo tooadd operaciones tooan API](api-management-howto-add-operations.md).
> 
> 

Se configuran las API de portal para desarrolladores de Hola. tooreach, haga clic en **portal para desarrolladores de** de barra de herramientas de servicio de Hola.

![Portal del publicador][api-management-management-console]

Calculadora de hello tooimport API, haga clic en **API** de hello **administración de API** menú Hola izquierda y, a continuación, haga clic en **API de importación**.

![Botón Importar API][api-management-import-api]

Lleve a cabo Hola siguiendo los pasos tooconfigure Hola calculadora API:

1. Haga clic en **From URL**, escriba **http://calcapi.cloudapp.net/calcapi.json** en hello **dirección URL del documento de especificación** texto cuadro y haga clic en hello **Swagger**  botón de radio.
2. Tipo de **calc** en hello **sufijo de URL de la API de Web** cuadro de texto.
3. Haga clic en hello **productos (opcionales)** cuadro y elija **Starter**.
4. Haga clic en **guardar** tooimport Hola API.

![Add new API][api-management-import-new-api]

> [!NOTE]
> **Administración de API** admite actualmente las versiones 1.2 y 2.0 del documento Swagger para la importación. Aunque la [especificación Swagger 2.0](http://swagger.io/specification) declara que las propiedades `host`, `basePath` y `schemes` son opcionales, el documento Swagger 2.0 **DEBE** contener esas propiedades; en caso contrario, no se importará. 
> 
> 

Una vez que se importa la API de hello, hello página de resumen de la API de Hola se muestra en portal para desarrolladores de Hola.

![API summary][api-management-imported-api-summary]

sección de la API de Hello tiene varias pestañas. Hola **resumen** ficha muestra métricas básicas e información sobre Hola API. Hola [configuración](api-management-howto-create-apis.md#configure-api-settings) ficha es configuración de hello tooview y editar utilizada para una API. Hola [Operations](api-management-howto-add-operations.md) ficha es operaciones hello toomanage usa la API. Hola **seguridad** ficha puede ser tooconfigure usa autenticación de puerta de enlace para el servidor back-end de hello mediante autenticación básica o [autenticación de certificado mutua](api-management-howto-mutual-certificates.md)y tooconfigure [ autorización del usuario mediante el uso de OAuth 2.0](api-management-howto-oauth2.md).  Hola **problemas** ficha es tooview usado los problemas notificados por los desarrolladores de Hola que usan las API. Hola **productos** ficha es productos de hello tooconfigure utilizadas que contienen esta API.

De forma predeterminada, cada instancia de Administración de API incluye dos productos de ejemplo:

* **Starter**
* **Sin límite**

En este tutorial, Hola API calculadora básica se agregó toohello producto de inicio cuando se importó Hola API.

En orden toomake llamadas tooan API, los desarrolladores en primer lugar deben suscribirse producto tooa que le da acceso tooit. Los desarrolladores pueden suscribirse tooproducts en el portal para desarrolladores de Hola o los administradores pueden suscribirse a los desarrolladores tooproducts en el portal para desarrolladores de Hola. Es un administrador como se ha creado instancia de administración de API de Hola Hola pasos anteriores en el tutorial de hello, por lo que ya está suscrito tooevery producto de forma predeterminada.

## <a name="call-operation"></a>Llamar a una operación de portal para desarrolladores de Hola
Las operaciones pueden llamarse directamente desde el portal para desarrolladores de hello, que proporciona una manera cómoda de tooview y pruebe las operaciones de Hola de una API. En este paso del tutorial, llamará hello básico calculadora API **agrega dos enteros** operación. Haga clic en **portal para desarrolladores de** desde el menú de Hola Hola parte superior derecha del portal para desarrolladores de Hola.

![portal para desarrolladores][api-management-developer-portal-menu]

Haga clic en **API** desde el menú superior de hello y, a continuación, haga clic en **calculadora básica** toosee Hola operaciones disponibles.

![portal para desarrolladores][api-management-developer-portal-calc-api]

Tenga en cuenta las descripciones de ejemplo de Hola y los parámetros que se importaron junto con hello API y operaciones, proporcionar documentación para desarrolladores de Hola que va a utilizar esta operación. Estas descripciones también pueden agregarse cuando las operaciones se agregan manualmente.

Hola toocall **agrega dos enteros** operación, haga clic en **Pruébelo**.

![Pruébelo][api-management-developer-portal-calc-api-console]

Puede especifique algunos valores para parámetros de Hola o mantener los valores predeterminados de hello y, a continuación, haga clic en **enviar**.

![HTTP Get][api-management-invoke-get]

Después de invoca una operación, el portal para desarrolladores de hello muestra hello **estado de respuesta**, hello **encabezados de respuesta**y cualquier **contenido de la respuesta**.

![Response][api-management-invoke-get-response]

## <a name="view-analytics"></a>Visualización de análisis
análisis de tooview de calculadora básica, el portal para desarrolladores de conmutador toohello atrás seleccionando **administrar** desde el menú de Hola Hola parte superior derecha del portal para desarrolladores de Hola.

![Administrar][api-management-manage-menu]

vista predeterminada para el portal para desarrolladores de hello Hello es hello **panel**, lo que proporciona una visión general de la instancia de la administración de API.

![Panel][api-management-dashboard]

Al mantener el mouse Hola mouse (ratón) sobre el gráfico de Hola para **calculadora básica** toosee hello las medidas específicas para el uso de Hola de hello API durante un período de tiempo determinado.

> [!NOTE]
> Si no ve todas las líneas del gráfico, cambie el portal para desarrolladores de toohello back- y realizar algunas llamadas en hello API, espere unos minutos y, a continuación, vuelven a estar toohello panel.
> 
> 

Haga clic en **ver detalles** página de resumen de Hola de tooview de API, incluidas las versiones más grandes de las métricas de muestra de Hola Hola.

![Análisis][api-management-mouse-over]

![Resumen][api-management-api-summary-metrics]

Para métricas detalladas e informes, haga clic en **análisis** de hello **administración de API** menú de hello izquierda.

![Información general][api-management-analytics-overview]

Hola **análisis** sección tiene Hola después de cuatro pestañas:

* **Un vistazo** proporciona el uso general y las métricas de mantenimiento, así como Hola superior a los desarrolladores, productos más vendidos, las API principales y las operaciones principales.
* **Uso** proporciona información detallada de las llamadas de API y del ancho de banda, incluida una representación geográfica.
* **Mantenimiento** se centra en los códigos de estado, las tasas de éxito de caché, los tiempos de respuesta y los tiempos de respuesta de la API y del servicio.
* **Actividad** proporciona informes que explorar en profundidad de la actividad específica de Hola por el desarrollador, producto, API y operación.

## <a name="next-steps"></a>Pasos siguientes
* Obtenga información acerca de cómo demasiado[proteger su API con límites de frecuencia](api-management-howto-product-with-rules.md).

[Azure Free Trial]: http://azure.microsoft.com/pricing/free-trial/?WT.mc_id=api_management_hero_a

[Create an API Management instance]: #create-service-instance
[Create an API]: #create-api
[Add an operation]: #add-operation
[Add hello new API tooa product]: #add-api-to-product
[Subscribe toohello product that contains hello API]: #subscribe
[Call an operation from hello Developer Portal]: #call-operation
[View analytics]: #view-analytics
[Next steps]: #next-steps


[How toomanage developer accounts in Azure API Management]: api-management-howto-create-or-invite-developers.md
[Configure API settings]: api-management-howto-create-apis.md#configure-api-settings
[How tooconfigure notifications and email templates in Azure API Management]: api-management-howto-configure-notifications.md
[Responses]: api-management-howto-add-operations.md#responses
[How create and publish a product]: api-management-howto-add-products.md
[API Management pricing]: http://azure.microsoft.com/pricing/details/api-management/

[Azure Portal]: https://portal.azure.com/

[api-management-management-console]: ./media/api-management-get-started/api-management-management-console.png
[api-management-create-instance-menu]: ./media/api-management-get-started/api-management-create-instance-menu.png
[api-management-create-instance-step1]: ./media/api-management-get-started/api-management-create-instance-step1.png
[api-management-create-instance-step2]: ./media/api-management-get-started/api-management-create-instance-step2.png
[api-management-instance-created]: ./media/api-management-get-started/api-management-instance-created.png
[api-management-import-api]: ./media/api-management-get-started/api-management-import-api.png
[api-management-import-new-api]: ./media/api-management-get-started/api-management-import-new-api.png
[api-management-imported-api-summary]: ./media/api-management-get-started/api-management-imported-api-summary.png
[api-management-calc-operations]: ./media/api-management-get-started/api-management-calc-operations.png
[api-management-list-products]: ./media/api-management-get-started/api-management-list-products.png
[api-management-add-api-to-product]: ./media/api-management-get-started/api-management-add-api-to-product.png
[api-management-add-myechoapi-to-product]: ./media/api-management-get-started/api-management-add-myechoapi-to-product.png
[api-management-api-added-to-product]: ./media/api-management-get-started/api-management-api-added-to-product.png
[api-management-developers]: ./media/api-management-get-started/api-management-developers.png
[api-management-add-subscription]: ./media/api-management-get-started/api-management-add-subscription.png
[api-management-add-subscription-window]: ./media/api-management-get-started/api-management-add-subscription-window.png
[api-management-subscription-added]: ./media/api-management-get-started/api-management-subscription-added.png
[api-management-developer-portal-menu]: ./media/api-management-get-started/api-management-developer-portal-menu.png
[api-management-developer-portal-calc-api]: ./media/api-management-get-started/api-management-developer-portal-calc-api.png
[api-management-developer-portal-calc-api-console]: ./media/api-management-get-started/api-management-developer-portal-calc-api-console.png
[api-management-invoke-get]: ./media/api-management-get-started/api-management-invoke-get.png
[api-management-invoke-get-response]: ./media/api-management-get-started/api-management-invoke-get-response.png
[api-management-manage-menu]: ./media/api-management-get-started/api-management-manage-menu.png
[api-management-dashboard]: ./media/api-management-get-started/api-management-dashboard.png

[api-management-add-response]: ./media/api-management-get-started/api-management-add-response.png
[api-management-add-response-window]: ./media/api-management-get-started/api-management-add-response-window.png
[api-management-developer-key]: ./media/api-management-get-started/api-management-developer-key.png
[api-management-mouse-over]: ./media/api-management-get-started/api-management-mouse-over.png
[api-management-api-summary-metrics]: ./media/api-management-get-started/api-management-api-summary-metrics.png
[api-management-analytics-overview]: ./media/api-management-get-started/api-management-analytics-overview.png
[api-management-analytics-usage]: ./media/api-management-get-started/api-management-analytics-usage.png
[api-management-]: ./media/api-management-get-started/api-management-.png
[api-management-]: ./media/api-management-get-started/api-management-.png
