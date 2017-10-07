---
title: aaaExporting un tooPowerApps API hospedada en Azure y Microsoft Flow | Documentos de Microsoft
description: "Información general sobre cómo se hospeda tooexpose una API de servicio de aplicaciones tooPowerApps y Microsoft Flow"
services: app-service
documentationcenter: 
author: mattchenderson
manager: erikre
editor: 
ms.assetid: 
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: multiple
ms.topic: article
ms.date: 06/20/2017
ms.author: mahender
ms.openlocfilehash: 285b6efa3af5b0feac1ee2f617c0dc56dc3fd198
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="exporting-an-azure-hosted-api-toopowerapps-and-microsoft-flow"></a>Exportar un tooPowerApps API hospedada en Azure y Microsoft Flow

## <a name="creating-custom-connectors-for-powerapps-and-microsoft-flow"></a>Creación de conectores personalizados para PowerApps y Microsoft Flow

[PowerApps](https://powerapps.com) es un servicio para generar y utilizar aplicaciones empresariales personalizadas que conectan datos tooyour y funcionan en otras plataformas. [Microsoft Flow](https://flow.microsoft.com) resulta fácil tooautomate flujos de trabajo y procesos de negocios entre sus servicios y aplicaciones favoritas. PowerApps y Microsoft Flow vienen con una variedad de orígenes de toodata conectores integrados, como Office 365, Dynamics 365, Salesforce y mucho más. Sin embargo, los usuarios también necesitan toobe tooleverage capaz de los orígenes de datos y las API que se está generadas por su organización.

De igual forma, los programadores que deseen tooexpose sus API más ampliamente dentro de hello organización puede querer toomake sus tooPowerApps disponibles de API y los usuarios de Microsoft Flow. En este tema le mostrará cómo tooexpose una API se creó con tooPowerApps de servicio de aplicaciones de Azure o funciones de Azure y Microsoft Flow. [Servicio de aplicaciones de Azure](https://azure.microsoft.com/services/app-service/) es una oferta de plataforma como servicio que permite a los desarrolladores tooquickly y fácilmente compilación empresarial web, móviles y las aplicaciones de API. [Las funciones de Azure](https://azure.microsoft.com/services/functions/) es una solución de proceso sin servidor basado en eventos que permite el código de autor de tooquickly que puedan reaccionar de tooother partes de su sistema y la escala según la demanda.

toolearn más información acerca de estos servicios, vea:
- [PowerApps Guided Learning](https://powerapps.microsoft.com/guided-learning/learning-introducing-powerapps/) (Aprendizaje guiado de PowerApps) 
- [Aprendizaje guiado de Microsoft Flow](https://flow.microsoft.com/guided-learning/learning-introducing-flow/)
- [¿Qué es App Service?](https://docs.microsoft.com/azure/app-service/app-service-value-prop-what-is)
- [Qué es Azure Functions](https://docs.microsoft.com/azure/azure-functions/functions-overview)

## <a name="sharing-an-api-definition"></a>Uso compartido de una definición de API

Las API a menudo se describen mediante un [OpenAPI documento](https://www.openapis.org/) (a veces denominada tooas un documento de "Swagger"). Contiene toda información de hello sobre qué operaciones están disponibles y cómo se estructura el datos Hola. PowerApps y Microsoft Flow pueden crear conectores personalizados para cualquier documento de Open API 2.0. Una vez creado un conector personalizado, se puede utilizar en hello exactamente igual que uno de Hola conectores integrados y rápidamente se puede integrar en una aplicación.

Azure App Service y Azure Functions tienen [compatibilidad integrada](https://docs.microsoft.com/azure/app-service-api/app-service-api-metadata) para crear, hospedar y administrar un documento de Open API. En orden toocreate un conector personalizado para un sitio web, móvil, una API o aplicación de función, PowerApps y flujo deben toobe tiene una copia de la definición de Hola.

> [!NOTE]
> Ya se está usando una copia de la definición de la API de hello, PowerApps y Microsoft Flow no podrá inmediatamente saber acerca de las actualizaciones o una aplicación de toohello cambios importantes. Si está disponible una nueva versión de API de hello, estos pasos deben repetirse para la nueva versión de hello. 

tooprovide PowerApps y Microsoft Flow con la definición de la API de hello hospedado para su aplicación, siga estos pasos:

1. Abra hello [Portal de Azure](https://portal.azure.com) y navegue tooyour aplicación de servicio de aplicaciones o funciones de Azure.

    Si usa el servicio de aplicaciones de Azure, seleccione **definición de la API** de lista de valores de hello. 
    
    Si usa Azure Functions, seleccione la aplicación de función y después elija **Características de la plataforma** y **Definición de la API**. También puede elegir hello tooopen **(vista previa) de la definición de API** pestaña en su lugar.

2. Si se ha proporcionado una definición de la API, verá un **exportar tooPowerApps + Microsoft Flow** botón. Haga clic en este proceso de exportación de botón toobegin Hola.

3. Seleccione hello **modo de exportación**. Esto determina los pasos de Hola que deberá toofollow toocreate un conector. App Service ofrece dos opciones para proporcionar a PowerApps y Microsoft Flow la definición de la API:

    **Express** permite crear conector personalizado Hola desde dentro de Hola portal de Azure. Requiere que Hola actual ha iniciado la sesión el usuario tiene conectores de toocreate de permiso en el entorno de destino de Hola. Se trata de hello enfoque recomendado si ese requisito se cumple. Si utiliza este modo, siga hello [Express exportación](#express) estas instrucciones.

    **Manual** permite exportar una copia de la definición de la API de Hola que puede importarse mediante Hola PowerApps o Microsoft Flow portales. Se trata de hello enfoque recomendado si hello usuario Hola con conectores de toocreate de permiso y Azure son distintas personas o conector Hola necesita toobe creado en otro inquilino. Si utiliza este modo, siga hello [importación y exportación Manual](#manual) estas instrucciones.

<a name="express"></a>
## <a name="express-export"></a>Exportación rápida

En esta sección, creará un nuevo conector personalizado desde dentro de hello portal de Azure. Debe haber iniciado en hello inquilino toowhich desea tooexport y debe tener permiso toocreate un conector personalizado en el entorno de destino de Hola.

1. Seleccione entorno hello en el que le gustaría conector de hello toocreate. Después, proporcione un nombre para el conector personalizado.

2. Si la definición de la API incluye cualquier definición de seguridad, estas se indicarán en el paso 2. Si es necesario, proporcionar seguridad Hola detalles de configuración necesarios toogrant a los usuarios tener acceso a API de tooyour. Para más información, vea el apartado [Autenticación](#auth) más abajo. 

3. Haga clic en **Aceptar** toocreate el conector personalizado.


<a name="manual"></a>
## <a name="manual-export-and-import"></a>Exportación e importación manual

En orden toocreate un conector personalizado para un sitio web, móvil, una API o aplicación de la función, se necesitarán dos pasos:

1. [Recuperar la definición de la API de Hola de servicio de aplicaciones o funciones de Azure](#export)
2. [Importar definición de la API de hello en PowerApps y Microsoft Flow](#import)

Es posible que estos dos pasos necesitará toobe realizada por los usuarios independientes dentro de una organización, como un usuario determinado no puede tener permiso tooperform ambas acciones. En este caso, un programador que tiene acceso de colaborador toohello aplicación de servicio de aplicaciones o funciones de Azure necesitará definición de hello API tooobtain (un único archivo JSON) o un tooit de vínculo. A continuación, necesitará tooprovide definición tooa PowerApps o Microsoft Flow propietario. Propietario puede usar el conector personalizado de hello metadatos toocreate Hola.

<a name="export"></a>
### <a name="retrieving-hello-api-definition-from-app-service-or-azure-functions"></a>Recuperar la definición de la API de Hola de servicio de aplicaciones o funciones de Azure

En esta sección, se exportará la definición de la API de hello de la API de servicio de aplicación, toobe usará más adelante en el portal de PowerApps o Microsoft Flow Hola.

1. Puede elegir tooeither **descargar definición Hola API** o **obtener un vínculo**. Lo que elija, se proporcionará el resultado de hello en la sección siguiente de Hola. Seleccione una de estas opciones y siga las instrucciones de Hola.
 
2. Si la definición de la API incluye cualquier definición de seguridad, estas se indicarán en el paso 2. Durante la importación, PowerApps y Microsoft Flow las detectarán y solicitarán información de seguridad. Recopilar Hola credenciales relacionadas tooeach definición para su uso en la sección siguiente Hola. Para más información, vea el apartado [Autenticación](#auth) más abajo. 

<a name="import"></a>
### <a name="importing-hello-api-definition-into-powerapps-and-microsoft-flow"></a>Importar definición de la API de hello en PowerApps y Microsoft Flow

En esta sección, creará un conector personalizado en PowerApps y Microsoft Flow mediante definición de hello API obtenido anteriormente. Conectores personalizada se comparten entre dos servicios hello, para que solo tenga una vez la definición de Hola de tooimport. Para más información sobre los conectores personalizados, consulte [registrar y utilizar conectores personalizada en PowerApps] y [registrar y utilizar conectores personalizada en Microsoft Flow].

1. Abra hello [portal web de Powerapps](https://web.powerapps.com) o hello [portal web de Microsoft Flow](https://flow.microsoft.com/)e inicie sesión. 

2. Haga clic en hello **configuración** botón (icono de engranaje de Hola) en la esquina superior derecha de la página de Hola y seleccione de hello **conectores personalizada**. 

3. Haga clic en **Create custom connector** (Crear conector personalizado).

4. En hello **General** pestaña, proporcione un nombre de la API y, a continuación, cargar la definición de OpenAPI de Hola o pegar en la dirección URL de metadatos de Hola. Haga clic en **Continue**.

4. En hello **seguridad** ficha, si está tooprovide solicitadas detalles de autenticación, escriba los valores de hello obtenidos en la sección anterior de Hola. De lo contrario, continúe toohello siguiente paso.

5. En hello **definiciones** ficha, todas las operaciones de hello definidas en el archivo OpenAPI están rellena automáticamente. Si se definen todas las operaciones necesarias, pueden ir toohello siguiente paso. Si no es así, puede agregar y modificar las operaciones aquí.

6. Haga clic en **Crear conector**. Si desea que las llamadas API tootest, vaya toohello siguiente paso.

7. En hello **prueba** ficha, crear una conexión, seleccione una operación tootest y escriba los datos requeridos por la operación de Hola.

8. Haga clic en **Operación de prueba**.


<a name="auth"></a>
## <a name="authentication"></a>Autenticación

PowerApps y Microsoft Flow admiten de forma nativa a una colección de proveedores de identidades que pueden ser toolog usado en los usuarios de su conector personalizado. Si la API requiere autenticación, asegúrese de que se captura como _definición de seguridad_ en el documento Open API. Durante la exportación, deberá tooprovide valores de configuración que permiten a una acción de inicio de sesión de Microsoft Flow tooperform PowerApps.

Esta sección describen los tipos de autenticación de Hola que son compatibles con el flujo de express hello: genérico OAuth 2.0, Azure Active Directory y clave de API. Para obtener una lista completa de los proveedores y las credenciales de hello cada una requiere, consulte [registrar y utilizar conectores personalizada en PowerApps] y [registrar y utilizar conectores personalizada en Microsoft Flow].

### <a name="api-key"></a>Clave de API
Cuando se usa este esquema de seguridad, los usuarios de Hola de su conector se convertirá en tooprovide solicitadas Hola tecla cuando crea una conexión. Puede proporcionar un toohelp de nombre de clave de API que les saber qué clave se necesita. Para las funciones de Azure, esto normalmente será una de las claves de host de hello, que abarcan varias funciones dentro de la aplicación de la función de hello.

### <a name="azure-active-directory"></a>Azure Active Directory
Al configurar un conector personalizado que requiere inicio de sesión AAD, se requieren dos registros de aplicación AAD: una API de back-end de hello toomodel y un conector de hello toomodel en PowerApps y el flujo.

La API debe ser toowork configurado con el primer registro de hello y esto ya nos ocuparemos de si usa hello [autenticación/autorización del servicio de aplicación](https://docs.microsoft.com/azure/app-service-mobile/app-service-mobile-how-to-configure-active-directory-authentication) característica.

Tendrá toomanually crear segundo registro de hello para el conector de hello, siguiendo los pasos de hello cubiertos en [agregar una aplicación de AAD](https://docs.microsoft.com/azure/active-directory/develop/active-directory-integrating-applications#adding-an-application). Hello registro necesita toohave delegado acceso tooyour API y una dirección URL de respuesta de `https://msmanaged-na.consent.azure-apim.net/redirect`. Vea [en este ejemplo](
https://powerapps.microsoft.com/tutorials/customapi-azure-resource-manager-tutorial/) para obtener información más detallada, sustituyendo su API para hello Azure Resource Manager.

Hola después de los valores de configuración es necesario:
- **Id. de cliente** -Hola Id. de cliente de su registro AAD de conector
- **Secreto del cliente** -secreto de cliente hello de su registro AAD de conector
- **Dirección URL de inicio de sesión** : hello dirección URL base para AAD. En Azure público, normalmente será `https://login.windows.net`.
- **Identificador de inquilino** -Hola Id. de hello inquilino toobe utilizado para el inicio de sesión de Hola. Esto debería "comunes" u Hola Id. de inquilino de hello en qué Hola se va a crear el conector.
- **Dirección URL del recurso** -Hola dirección URL del recurso de su registro AAD de back-end de API

> [!IMPORTANT]
> Si otra persona va a importar definición de API de hello en PowerApps y Microsoft Flow como parte del flujo de hello manual, deberá tooprovide con el secreto del cliente y el Id. de cliente hello **de registro del conector hello**, así como como dirección URL de recurso hello de la API. Asegúrese de que estos secretos se administran de forma segura. **No comparta las credenciales de seguridad de Hola de hello propia API.**

### <a name="generic-oauth-20"></a>OAuth 2.0 genérico
soporte de Hello genérico OAuth 2.0 permite toointegrate con cualquier proveedor de OAuth 2.0. Esto le permite toobring en cualquier proveedor personalizado que no se admite de forma nativa.

Hola después de los valores de configuración es necesario:
- **Id. de cliente** -Hola Id. de cliente de OAuth 2.0
- **Secreto del cliente** -secreto de cliente hello OAuth 2.0
- **Dirección URL de autorización** -Hola dirección URL de autorización de OAuth 2.0
- **Dirección URL de token** -Hola URL del token de OAuth 2.0
- **Actualizar la dirección URL** -Hola dirección URL de actualización de OAuth 2.0



[registrar y utilizar conectores personalizada en PowerApps]: https://powerapps.microsoft.com/tutorials/register-custom-api/
[registrar y utilizar conectores personalizada en Microsoft Flow]: https://flow.microsoft.com/documentation/register-custom-api/
