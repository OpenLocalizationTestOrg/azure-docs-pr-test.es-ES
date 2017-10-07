---
title: "aaaProtect un back-end de API Web con Azure Active Directory y administración de API | Documentos de Microsoft"
description: "Obtenga información acerca de cómo tooprotect un back-end de API Web con Azure Active Directory y administración de API."
services: api-management
documentationcenter: 
author: steved0x
manager: erikre
editor: 
ms.assetid: f856ff03-64a1-4548-9ec4-c0ec4cc1600f
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: apimpm
ms.openlocfilehash: f4b323034354aa09579c643bade47257fbf1e5c3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooprotect-a-web-api-backend-with-azure-active-directory-and-api-management"></a>¿Cómo tooprotect un back-end de API Web con Azure Active Directory y administración de API
Hola siguiendo el vídeo muestra cómo toobuild un API Web de back-end y la protección mediante el protocolo OAuth 2.0 con Azure Active Directory y administración de API.  Este artículo proporciona información general y los pasos de información adicional de hello en vídeo de Hola. Este vídeo de 24 minutos le muestra cómo:

* Crear un back-end de API web y protegerlo con AAD, a partir de la 1:30
* Importar Hola API Administración de API - empezando a las 7:10
* Configurar Hola Developer portal toocall Hola API - a partir de 9:09
* Configurar un hello toocall de aplicación de escritorio API - a partir de 18:08
* Configurar una toopre de directiva de validación de JWT-autorizar las solicitudes - a partir de 20:47

> [!VIDEO https://channel9.msdn.com/Blogs/AzureApiMgmt/Protecting-Web-API-Backend-with-Azure-Active-Directory-and-API-Management/player]
> 
> 

## <a name="create-an-azure-ad-directory"></a>Crear un directorio de Azure AD
toosecure su API Web realizar una copia de Azure Active Directory, debe tener un un inquilino de AAD. En este vídeo se usa un inquilino denominado **APIMDemo** . toocreate un inquilino de AAD, inicio de sesión toohello [Portal clásico de Azure](https://manage.windowsazure.com) y haga clic en **New**->**servicios de aplicaciones**->**Active Directorio**->**directorio**->**creación personalizada**. 

![Azure Active Directory][api-management-create-aad-menu]

En este ejemplo, se crea un directorio denominado **APIMDemo** con un dominio predeterminado denominado **DemoAPIM.onmicrosoft.com**. Este directorio se utiliza a lo largo de vídeo de Hola.

![Azure Active Directory][api-management-create-aad]

## <a name="create-a-web-api-service-secured-by-azure-active-directory"></a>Crear un servicio de API web protegido con Azure Active Directory
En este paso, se crea un back-end API Web con Visual Studio 2013. Este paso de hello vídeo comienza en 1:30. proyecto de back-end de API Web toocreate en haga clic en Visual Studio **archivo**->**New**->**proyecto**y elija **Web de ASP.NET Aplicación** de hello **Web** lista de plantillas. En este vídeo Hola se denomina proyecto **APIMAADDemo**. Haga clic en **Aceptar** proyecto de hello toocreate. 

![Visual Studio][api-management-new-web-app]

Haga clic en **API Web** de hello **seleccionar una lista de plantilla** toocreate un proyecto de API Web. Haga clic en autenticación de Azure Directory tooconfigure **Cambiar autenticación**.

![Nuevo proyecto][api-management-new-project]

Haga clic en **cuentas organizativas**y especifique hello **dominio** de su inquilino de AAD. En este Hola de ejemplo es dominio **DemoAPIM.onmicrosoft.com**. dominio hello del directorio puede obtenerse de hello **dominios** pestaña del directorio.

![Dominios][api-management-aad-domains]

Configurar opciones de hello deseado en hello **Cambiar autenticación** cuadro de diálogo y haga clic en **Aceptar**.

![Cambiar autenticación][api-management-change-authentication]

Al hacer clic en **Aceptar** Visual Studio intentará tooregister la aplicación con su directorio Azure AD y es posible que toosign solicitada en Visual Studio. Inicie sesión con una cuenta administrativa para el directorio.

![Inicie sesión en tooVisual Studio][api-management-sign-in-vidual-studio]

cuadro de tooconfigure este proyecto como un Hola de comprobación de la API Web de Azure para **Host en la nube de hello** y, a continuación, haga clic en **Aceptar**.

![Nuevo proyecto][api-management-new-project-cloud]

Es posible que toosign solicitada en tooAzure y, a continuación, puede configurar Hola aplicación Web.

![Configuración][api-management-configure-web-app]

En este ejemplo se especifica un nuevo **plan de App Service** denominado **APIMAADDemo**.

Haga clic en **Aceptar** tooconfigure Hola aplicación Web y crear el proyecto de Hola.

## <a name="add-hello-code-toohello-web-api-project"></a>Agregar proyecto de API Web de hello código toohello
paso siguiente de Hello en vídeo de hello agrega proyecto de API Web de hello código toohello. Este paso empieza en 4:35.

Hola API Web en este ejemplo implementa un servicio de calculadora básica mediante un modelo y un controlador. Pulse el botón derecho en el modelo de hello tooadd para el servicio de hello, **modelos** en **el Explorador de soluciones** y elija **agregar**, **clase**. Nombre de la clase hello `CalcInput` y haga clic en **agregar**.

Agregue Hola siguiente `using` arriba toohello de instrucción de hello `CalcInput.cs` archivo.

```c#
using Newtonsoft.Json;
```

Reemplace clase hello generado con el siguiente código de hello.

```c#
public class CalcInput
{
    [JsonProperty(PropertyName = "a")]
    public int a;

    [JsonProperty(PropertyName = "b")]
    public int b;
}
```

Haga clic con el botón derecho en **Controladores** en el **Explorador de soluciones** y elija **Agregar**->**Controlador**. Elija **Controlador Web API 2 - Vacío** y haga clic en **Agregar**. Tipo de **CalcController** para hello controlador el nombre y haga clic en **agregar**.

![Agregar controlador][api-management-add-controller]

Agregue Hola siguiente `using` arriba toohello de instrucción de hello `CalcController.cs` archivo.

```c#
using System.IO;
using System.Web;
using APIMAADDemo.Models;
```

Reemplace la clase de controlador de Hola generado con el siguiente código de hello. Este código implementa hello `Add`, `Subtract`, `Multiply`, y `Divide` las operaciones de hello API calculadora básica.

```c#
[Authorize]
public class CalcController : ApiController
{
    [Route("api/add")]
    [HttpGet]
    public HttpResponseMessage GetSum([FromUri]int a, [FromUri]int b)
    {
        string xml = string.Format("<result><value>{0}</value><broughtToYouBy>Azure API Management - http://azure.microsoft.com/apim/ </broughtToYouBy></result>", a + b);
        HttpResponseMessage response = Request.CreateResponse();
        response.Content = new StringContent(xml, System.Text.Encoding.UTF8, "application/xml");
        return response;
    }

    [Route("api/sub")]
    [HttpGet]
    public HttpResponseMessage GetDiff([FromUri]int a, [FromUri]int b)
    {
        string xml = string.Format("<result><value>{0}</value><broughtToYouBy>Azure API Management - http://azure.microsoft.com/apim/ </broughtToYouBy></result>", a - b);
        HttpResponseMessage response = Request.CreateResponse();
        response.Content = new StringContent(xml, System.Text.Encoding.UTF8, "application/xml");
        return response;
    }

    [Route("api/mul")]
    [HttpGet]
    public HttpResponseMessage GetProduct([FromUri]int a, [FromUri]int b)
    {
        string xml = string.Format("<result><value>{0}</value><broughtToYouBy>Azure API Management - http://azure.microsoft.com/apim/ </broughtToYouBy></result>", a * b);
        HttpResponseMessage response = Request.CreateResponse();
        response.Content = new StringContent(xml, System.Text.Encoding.UTF8, "application/xml");
        return response;
    }

    [Route("api/div")]
    [HttpGet]
    public HttpResponseMessage GetDiv([FromUri]int a, [FromUri]int b)
    {
        string xml = string.Format("<result><value>{0}</value><broughtToYouBy>Azure API Management - http://azure.microsoft.com/apim/ </broughtToYouBy></result>", a / b);
        HttpResponseMessage response = Request.CreateResponse();
        response.Content = new StringContent(xml, System.Text.Encoding.UTF8, "application/xml");
        return response;
    }
}
```

Presione **F6** toobuild y compruebe la solución de Hola.

## <a name="publish-hello-project-tooazure"></a>Publicar Hola proyecto tooAzure
En este Hola paso Visual Studio proyecto es tooAzure publicado. Este paso de hello vídeo comienza en 5:45.

toopublish Hola tooAzure de proyecto, haga clic en hello **APIMAADDemo** proyecto en Visual Studio y elija **publicar**. Mantener la configuración predeterminada de Hola en hello **Publicar Web** cuadro de diálogo y haga clic en **publicar**.

![Publicación web][api-management-web-publish]

## <a name="grant-permissions-toohello-azure-ad-backend-service-application"></a>Conceder permisos de aplicación de servicio de back-end de toohello Azure AD
Se crea una nueva aplicación de servicio de back-end de hello en su directorio de Azure AD como parte de la configuración de Hola y el proceso de publicación de su proyecto de API Web. En este paso de hello vídeo, a partir de 6:13, se conceden permisos back-end de toohello API Web.

![Application][api-management-aad-backend-app]

Haga clic en el nombre de Hola de permisos de hello aplicación tooconfigure Hola necesario. Navegue toohello **configurar** ficha y desplácese hacia abajo toohello **permisos tooother aplicaciones** sección. Haga clic en hello **permisos de aplicación** lista desplegable situada junto a **Windows** **Azure Active Directory**, casilla Hola para **leer datos de directorio**y haga clic en **guardar**.

![Adición de permisos][api-management-aad-add-permissions]

> [!NOTE]
> Si **Windows** **Azure Active Directory** no es aparecen en las aplicaciones de tooother de permisos, haga clic en **Agregar aplicación** y agréguelo desde la lista de Hola.
> 
> 

Tome nota de hello **App Id URI** para su uso en un paso posterior cuando se configura una aplicación de Azure AD para el portal para desarrolladores de administración de API de Hola.

![URI de id. de aplicación][api-management-aad-sso-uri]

## <a name="import-hello-web-api-into-api-management"></a>Importar Hola API Web en administración de API
Se configuran las API de portal para desarrolladores de API hello, que se obtiene acceso a través de hello Portal de Azure. tooreach, haga clic en **portal para desarrolladores de** de barra de herramientas de Hola de su servicio de administración de API. Si aún no ha creado una instancia de servicio de administración de API, consulte [crear una instancia de servicio de administración de API] [ Create an API Management service instance] en hello [administrar su primera API] [ Manage your first API] tutorial.

![Portal del publicador][api-management-management-console]

Las operaciones se pueden [agregado manualmente tooAPIs](api-management-howto-add-operations.md), o se pueden importar. En este vídeo, las operaciones se importan en formato Swagger empezando en 6:40.

Cree un archivo denominado `calcapi.json` con después de contenido y guárdelo tooyour equipo. Asegúrese de que hello `host` atributo apunta back-end de tooyour API Web. En este ejemplo se usa `"host": "apimaaddemo.azurewebsites.net"` .

```json
{
  "swagger": "2.0",
  "info": {
    "title": "Calculator",
    "description": "Arithmetics over HTTP!",
    "version": "1.0"
  },
  "host": "apimaaddemo.azurewebsites.net",
  "basePath": "/api",
  "schemes": [
    "http"
  ],
  "paths": {
    "/add?a={a}&b={b}": {
      "get": {
        "description": "Responds with a sum of two numbers.",
        "operationId": "Add two integers",
        "parameters": [
          {
            "name": "a",
            "in": "query",
            "description": "First operand. Default value is <code>51</code>.",
            "required": true,
            "type": "string",
            "default": "51",
            "enum": [
              "51"
            ]
          },
          {
            "name": "b",
            "in": "query",
            "description": "Second operand. Default value is <code>49</code>.",
            "required": true,
            "type": "string",
            "default": "49",
            "enum": [
              "49"
            ]
          }
        ],
        "responses": { }
      }
    },
    "/sub?a={a}&b={b}": {
      "get": {
        "description": "Responds with a difference between two numbers.",
        "operationId": "Subtract two integers",
        "parameters": [
          {
            "name": "a",
            "in": "query",
            "description": "First operand. Default value is <code>100</code>.",
            "required": true,
            "type": "string",
            "default": "100",
            "enum": [
              "100"
            ]
          },
          {
            "name": "b",
            "in": "query",
            "description": "Second operand. Default value is <code>50</code>.",
            "required": true,
            "type": "string",
            "default": "50",
            "enum": [
              "50"
            ]
          }
        ],
        "responses": { }
      }
    },
    "/div?a={a}&b={b}": {
      "get": {
        "description": "Responds with a quotient of two numbers.",
        "operationId": "Divide two integers",
        "parameters": [
          {
            "name": "a",
            "in": "query",
            "description": "First operand. Default value is <code>100</code>.",
            "required": true,
            "type": "string",
            "default": "100",
            "enum": [
              "100"
            ]
          },
          {
            "name": "b",
            "in": "query",
            "description": "Second operand. Default value is <code>20</code>.",
            "required": true,
            "type": "string",
            "default": "20",
            "enum": [
              "20"
            ]
          }
        ],
        "responses": { }
      }
    },
    "/mul?a={a}&b={b}": {
      "get": {
        "description": "Responds with a product of two numbers.",
        "operationId": "Multiply two integers",
        "parameters": [
          {
            "name": "a",
            "in": "query",
            "description": "First operand. Default value is <code>20</code>.",
            "required": true,
            "type": "string",
            "default": "20",
            "enum": [
              "20"
            ]
          },
          {
            "name": "b",
            "in": "query",
            "description": "Second operand. Default value is <code>5</code>.",
            "required": true,
            "type": "string",
            "default": "5",
            "enum": [
              "5"
            ]
          }
        ],
        "responses": { }
      }
    }
  }
}
```

Calculadora de hello tooimport API, haga clic en **API** de hello **administración de API** menú Hola izquierda y, a continuación, haga clic en **API de importación**.

![Botón Importar API][api-management-import-api]

Realizar Hola siguiendo los pasos tooconfigure Hola calculadora API.

1. Haga clic en **archivo**, examinar toohello `calculator.json` archivo guardado y haga clic en hello **Swagger** botón de radio.
2. Tipo de **calc** en hello **sufijo de URL de la API de Web** cuadro de texto.
3. Haga clic en hello **productos (opcionales)** cuadro y elija **Starter**.
4. Haga clic en **guardar** tooimport Hola API.

![Add new API][api-management-import-new-api]

Una vez que se importa la API de hello, hello página de resumen de la API de Hola se muestra en portal para desarrolladores de Hola.

## <a name="call-hello-api-unsuccessfully-from-hello-developer-portal"></a>Llamar a API de hello correctamente desde el portal para desarrolladores de Hola
En este momento, Hola API se ha importado a la API de administración, pero no se puede aún puede llamar correctamente desde el portal para desarrolladores de hello porque el servicio de back-end de hello está protegido con autenticación de Azure AD. Esto se demuestra en vídeo de Hola a partir de 7:40 con hello pasos.

Haga clic en **portal para desarrolladores de** de hello parte superior derecha del portal para desarrolladores de Hola.

![portal para desarrolladores][api-management-developer-portal-menu]

Haga clic en **API** y haga clic en hello **calculadora** API.

![portal para desarrolladores][api-management-dev-portal-apis]

Haga clic en **Pruébelo**.

![Pruébelo][api-management-dev-portal-try-it]

Haga clic en **enviar** y observe el estado de la respuesta de Hola de **401 no autorizado**.

![Los métodos Send][api-management-dev-portal-send-401]

Hola solicitud no está autorizada porque Hola back-end API está protegido por Azure Active Directory. Antes de llamar correctamente a la API de hello portal para desarrolladores de hello debe estar configurado tooauthorize a los desarrolladores mediante OAuth 2.0. Este proceso se describe en las secciones siguientes de Hola.

## <a name="register-hello-developer-portal-as-an-aad-application"></a>Registrar el portal para desarrolladores de hello como una aplicación de AAD
Hola primer paso para configurar Hola developer portal tooauthorize a los desarrolladores mediante OAuth 2.0 es portal para desarrolladores de tooregister hello como una aplicación de AAD. Esto último se muestra a partir de 8:27 en vídeo de Hola.

Navegar por el inquilino de Azure AD toohello desde el primer paso de este vídeo, en este ejemplo de Hola **APIMDemo** y navegue toohello **aplicaciones** ficha.

![Nueva aplicación][api-management-aad-new-application-devportal]

Haga clic en hello **agregar** toocreate una nueva aplicación de Azure Active Directory de botón y elija **agregar una aplicación que mi organización está desarrollando**.

![Nueva aplicación][api-management-new-aad-application-menu]

Elija **Web de aplicación o Web API**, escriba un nombre y haga clic en la flecha siguiente Hola. En este ejemplo se usa **APIMDeveloperPortal** .

![Nueva aplicación][api-management-aad-new-application-devportal-1]

Para **dirección URL de inicio de sesión** escriba Hola URL de su servicio de administración de API y anexe `/signin`. En este ejemplo se usa `https://contoso5.portal.azure-api.net/signin` .

Para **URL de Id. de aplicación** escriba Hola URL de su servicio de administración de API y anexe algunos caracteres únicos. Puede tratarse de cualquier carácter que se desee y en este ejemplo se usa `https://contoso5.portal.azure-api.net/dp`. Cuando desea hello **propiedades de la aplicación** están configurados, haga clic en la aplicación hello de hello marca de verificación toocreate.

![Nueva aplicación][api-management-aad-new-application-devportal-2]

## <a name="configure-an-api-management-oauth-20-authorization-server"></a>Configurar un servidor de autorización OAuth 2.0 en la administración de API
Hola siguiente paso es tooconfigure un servidor de autorización de OAuth 2.0 en administración de API. Este paso se demuestra en hello vídeo a partir de 9:43.

Haga clic en **seguridad** Hola administración de API en menú Hola izquierda, haga clic en **OAuth 2.0**y, a continuación, haga clic en **agrega autorización** server.

![Agregar servidor de autorización][api-management-add-authorization-server]

Escriba un nombre y una descripción opcional en hello **nombre** y **descripción** campos. Estos campos son servidor de autorización de hello OAuth 2.0 tooidentify utilizados dentro de la instancia de servicio de administración de API de Hola. En este ejemplo se usa la **demostración del servidor de autorización** . Más adelante al especificar un toobe de servidor de OAuth 2.0 utilizado para la autenticación de una API, seleccionará este nombre.

Para hello **dirección URL de página de registro de cliente** escriba un valor de marcador de posición como `http://localhost`.  Hola **dirección URL de página de registro de cliente** puntos de toohello página que los usuarios pueden usar toocreate y configurar sus propias cuentas para los proveedores de OAuth 2.0 que admiten la administración de usuarios de cuentas. En este ejemplo los usuarios no crean ni configuran sus propias cuentas, por lo que se usa un marcador de posición.

![Agregar servidor de autorización][api-management-add-authorization-server-1]

A continuación, especifique la **URL del punto de conexión de autorización** y la **URL del punto de conexión de token**.

![Servidor de autorización][api-management-add-authorization-server-1a]

Estos valores se pueden recuperar de hello **extremos de la aplicación** página de aplicación de AAD que ha creado para el portal para desarrolladores de Hola Hola. los extremos de hello tooaccess navegue toohello **configurar** pestaña aplicación AAD de hello y haga clic en **ver extremos**.

![Application][api-management-aad-devportal-application]

![Ver extremos][api-management-aad-view-endpoints]

Hola copia **extremo de autorización de OAuth 2.0** y péguelo en hello **dirección URL del extremo de autorización** cuadro de texto.

![Agregar servidor de autorización][api-management-add-authorization-server-2]

Hola copia **extremo de token de OAuth 2.0** y péguelo en hello **dirección URL del extremo de Token** cuadro de texto.

![Agregar servidor de autorización][api-management-add-authorization-server-2a]

Además toopasting en extremo de token de Hola y agregar un parámetro de cuerpo adicional denominado **recursos** y use hello para el valor de hello **App Id URI** de hello aplicación AAD para el servicio de back-end de Hola que estaba se crea cuando se publicó el proyecto de Visual Studio Hola.

![URI de id. de aplicación][api-management-aad-sso-uri]

A continuación, especifique las credenciales del cliente Hola. Estas son las credenciales de hello para el recurso de Hola que desee tooaccess, en este caso Hola portal para desarrolladores.

![Credenciales de cliente][api-management-client-credentials]

Hola tooget **Id. de cliente**, navegue toohello **configurar** ficha de hello aplicación AAD para Hola Hola de portal y copia de desarrollador **Id. de cliente**.

Hola tooget **secreto de cliente** haga clic en hello **seleccione duración** desplegable Hola **claves** sección y especificar un intervalo. En este ejemplo se usa el año 1.

![id. de cliente][api-management-aad-client-id]

Haga clic en **guardar** toosave Hola configuración y mostrar hello la clave. 

> [!IMPORTANT]
> Anote esta clave. Una vez que cierre la ventana de configuración de Azure Active Directory de hello, no se puede mostrar clave Hola de nuevo.
> 
> 

Pegado desde el Portapapeles de toohello clave de copia hello, portal para desarrolladores de conmutador toohello atrás, clave de hello en hello **secreto de cliente** cuadro de texto y haga clic en **guardar**.

![Agregar servidor de autorización][api-management-add-authorization-server-3]

Inmediatamente después de las credenciales del cliente hello es una concesión de código de autorización. Copie este código de autorización y conmutador atrás tooyour aplicación de portal de Azure AD para desarrolladores Configurar página y pegue la concesión de autorización de hello en hello **dirección URL de respuesta** campo y haga clic en **guardar** nuevo.

![URL de respuesta][api-management-aad-reply-url]

Hola siguiente paso es tooconfigure permisos de hello para el portal para desarrolladores de hello aplicación AAD. Haga clic en **permisos de aplicación** y casilla de Hola para **leer datos de directorio**. Haga clic en **guardar** toosave esto cambiar y, a continuación, haga clic en **Agregar aplicación**.

![Adición de permisos][api-management-add-devportal-permissions]

Haga clic en el icono de búsqueda de hello, tipo **APIM** en hello a partir de cuadro, seleccione **APIMAADDemo**y haga clic en hello toosave de marca de verificación.

![Adición de permisos][api-management-aad-add-app-permissions]

Haga clic en **permisos delegados** para **APIMAADDemo** y casilla de Hola para **acceso APIMAADDemo**y haga clic en **guardar**. Esto permite al desarrollador Hola servicio back-end de aplicación de portal tooaccess Hola.

![Adición de permisos][api-management-aad-add-delegated-permissions]

## <a name="enable-oauth-20-user-authorization-for-hello-calculator-api"></a>Habilitar la autorización de usuario de OAuth 2.0 para hello API de calculadora
Ahora que hello OAuth 2.0 servidor está configurado, puede especificar en la configuración de seguridad de saludo de la API. Este paso se demuestra en hello vídeo a partir de 14:30.

Haga clic en **API** en Hola menú izquierdo y haga clic en **calculadora** tooview y configurar sus valores.

![API de calculadora][api-management-calc-api]

Navegue toohello **seguridad** ficha, compruebe hello **OAuth 2.0** casilla de verificación, servidor de autorización deseado seleccione Hola de hello **servidor de autorización** lista desplegable y haga clic en **Guardar**.

![API de calculadora][api-management-enable-aad-calculator]

## <a name="successfully-call-hello-calculator-api-from-hello-developer-portal"></a>Llamar correctamente a Hola calculadora API desde portal para desarrolladores de Hola
Ahora que autorización hello OAuth 2.0 está configurada en hello API, se pueden llamar correctamente sus operaciones del Centro para desarrolladores de Hola. Este paso se demuestra en hello vídeo a partir de 15:00.

Desplácese atrás toohello **agrega dos enteros** operación del servicio de calculadora de hello en el portal para desarrolladores de Hola y haga clic en **Pruébelo**. Nuevo elemento de Hola de nota en hello **autorización** sección servidor de autorización toohello correspondiente que acaba de agregar.

![API de calculadora][api-management-calc-authorization-server]

Seleccione **código de autorización** de autorización de hello desplegable lista y escriba las credenciales de Hola de hello cuenta toouse. Si ya inició sesión con la cuenta de hello que no se le pedirá.

![API de calculadora][api-management-devportal-authorization-code]

Haga clic en **enviar** Nota hello y **estado de respuesta** de **200 Aceptar** y resultados de Hola de operación de hello en el contenido de la respuesta de Hola.

![API de calculadora][api-management-devportal-response]

## <a name="configure-a-desktop-application-toocall-hello-api"></a>Configurar un Hola de toocall API de aplicación de escritorio
procedimiento siguiente de Hola Hola vídeo comienza a las 16:30 y configura un hello toocall de aplicación de escritorio simple API. primer paso de Hello es aplicación de escritorio de hello tooregister en Azure AD y asígnele el servicio de back-end de directorio y toohello de toohello de acceso. No hay una demostración de la aplicación de escritorio de hello llamar a una operación de calculadora de hello API a 18:25.

## <a name="configure-a-jwt-validation-policy-toopre-authorize-requests"></a>Configurar una toopre de directiva de validación de JWT-autorizar las solicitudes
comienza en 20:48 Hello procedimiento final en vídeo de Hola y muestra cómo hello toouse [validar JWT](https://msdn.microsoft.com/library/azure/034febe3-465f-4840-9fc6-c448ef520b0f#ValidateJWT) toopre directiva-autorizar las solicitudes mediante la validación de tokens de acceso de Hola de cada solicitud entrante. Si Hola directiva validar JWT no valida las solicitudes de hello, solicitud de hello está bloqueado por la API de administración y no se pasa a lo largo de toohello back-end.

```xml
<validate-jwt header-name="Authorization" failed-validation-httpcode="401" failed-validation-error-message="Unauthorized. Access token is missing or invalid.">
    <openid-config url="https://login.microsoftonline.com/DemoAPIM.onmicrosoft.com/.well-known/openid-configuration" />
    <required-claims>
        <claim name="aud">
            <value>https://DemoAPIM.NOTonmicrosoft.com/APIMAADDemo</value>
        </claim>
    </required-claims>
</validate-jwt>
```

Para otra demostración de cómo configurar y usar esta directiva, consulte [177 episodio abarcan de nube: más características de administración de API](https://azure.microsoft.com/documentation/videos/episode-177-more-api-management-features-with-vlad-vinogradsky/) y avancemos too13:50. Avance rápido too15:00 las directivas de hello toosee configuradas en el editor de directiva de hello y, a continuación, too18:50 para ver una demostración de la llamada a una operación de portal para desarrolladores de hello con y sin Hola necesario token de autorización.

## <a name="next-steps"></a>Pasos siguientes
* Consulte más [vídeos](https://azure.microsoft.com/documentation/videos/index/?services=api-management) sobre la administración de API.
* Para otro toosecure formas el servicio back-end, vea [autenticación de certificado mutua](api-management-howto-mutual-certificates.md).

[api-management-management-console]: ./media/api-management-howto-protect-backend-with-aad/api-management-management-console.png

[api-management-import-api]: ./media/api-management-howto-protect-backend-with-aad/api-management-import-api.png
[api-management-import-new-api]: ./media/api-management-howto-protect-backend-with-aad/api-management-import-new-api.png
[api-management-create-aad-menu]: ./media/api-management-howto-protect-backend-with-aad/api-management-create-aad-menu.png
[api-management-create-aad]: ./media/api-management-howto-protect-backend-with-aad/api-management-create-aad.png
[api-management-new-web-app]: ./media/api-management-howto-protect-backend-with-aad/api-management-new-web-app.png
[api-management-new-project]: ./media/api-management-howto-protect-backend-with-aad/api-management-new-project.png
[api-management-new-project-cloud]: ./media/api-management-howto-protect-backend-with-aad/api-management-new-project-cloud.png
[api-management-change-authentication]: ./media/api-management-howto-protect-backend-with-aad/api-management-change-authentication.png
[api-management-sign-in-vidual-studio]: ./media/api-management-howto-protect-backend-with-aad/api-management-sign-in-vidual-studio.png
[api-management-configure-web-app]: ./media/api-management-howto-protect-backend-with-aad/api-management-configure-web-app.png
[api-management-aad-domains]: ./media/api-management-howto-protect-backend-with-aad/api-management-aad-domains.png
[api-management-add-controller]: ./media/api-management-howto-protect-backend-with-aad/api-management-add-controller.png
[api-management-web-publish]: ./media/api-management-howto-protect-backend-with-aad/api-management-web-publish.png
[api-management-aad-backend-app]: ./media/api-management-howto-protect-backend-with-aad/api-management-aad-backend-app.png
[api-management-aad-add-permissions]: ./media/api-management-howto-protect-backend-with-aad/api-management-aad-add-permissions.png
[api-management-developer-portal-menu]: ./media/api-management-howto-protect-backend-with-aad/api-management-developer-portal-menu.png
[api-management-dev-portal-apis]: ./media/api-management-howto-protect-backend-with-aad/api-management-dev-portal-apis.png
[api-management-dev-portal-try-it]: ./media/api-management-howto-protect-backend-with-aad/api-management-dev-portal-try-it.png
[api-management-dev-portal-send-401]: ./media/api-management-howto-protect-backend-with-aad/api-management-dev-portal-send-401.png
[api-management-aad-new-application-devportal]: ./media/api-management-howto-protect-backend-with-aad/api-management-aad-new-application-devportal.png
[api-management-aad-new-application-devportal-1]: ./media/api-management-howto-protect-backend-with-aad/api-management-aad-new-application-devportal-1.png
[api-management-aad-new-application-devportal-2]: ./media/api-management-howto-protect-backend-with-aad/api-management-aad-new-application-devportal-2.png
[api-management-aad-devportal-application]: ./media/api-management-howto-protect-backend-with-aad/api-management-aad-devportal-application.png
[api-management-add-authorization-server]: ./media/api-management-howto-protect-backend-with-aad/api-management-add-authorization-server.png
[api-management-aad-sso-uri]: ./media/api-management-howto-protect-backend-with-aad/api-management-aad-sso-uri.png
[api-management-aad-view-endpoints]: ./media/api-management-howto-protect-backend-with-aad/api-management-aad-view-endpoints.png
[api-management-aad-client-id]: ./media/api-management-howto-protect-backend-with-aad/api-management-aad-client-id.png
[api-management-add-authorization-server-1]: ./media/api-management-howto-protect-backend-with-aad/api-management-add-authorization-server-1.png
[api-management-add-authorization-server-2]: ./media/api-management-howto-protect-backend-with-aad/api-management-add-authorization-server-2.png
[api-management-add-authorization-server-2a]: ./media/api-management-howto-protect-backend-with-aad/api-management-add-authorization-server-2a.png
[api-management-add-authorization-server-3]: ./media/api-management-howto-protect-backend-with-aad/api-management-add-authorization-server-3.png
[api-management-aad-reply-url]: ./media/api-management-howto-protect-backend-with-aad/api-management-aad-reply-url.png
[api-management-add-devportal-permissions]: ./media/api-management-howto-protect-backend-with-aad/api-management-add-devportal-permissions.png
[api-management-aad-add-app-permissions]: ./media/api-management-howto-protect-backend-with-aad/api-management-aad-add-app-permissions.png
[api-management-aad-add-delegated-permissions]: ./media/api-management-howto-protect-backend-with-aad/api-management-aad-add-delegated-permissions.png
[api-management-calc-api]: ./media/api-management-howto-protect-backend-with-aad/api-management-calc-api.png
[api-management-enable-aad-calculator]: ./media/api-management-howto-protect-backend-with-aad/api-management-enable-aad-calculator.png
[api-management-devportal-authorization-code]: ./media/api-management-howto-protect-backend-with-aad/api-management-devportal-authorization-code.png
[api-management-devportal-response]: ./media/api-management-howto-protect-backend-with-aad/api-management-devportal-response.png
[api-management-calc-authorization-server]: ./media/api-management-howto-protect-backend-with-aad/api-management-calc-authorization-server.png
[api-management-add-authorization-server-1a]: ./media/api-management-howto-protect-backend-with-aad/api-management-add-authorization-server-1a.png
[api-management-client-credentials]: ./media/api-management-howto-protect-backend-with-aad/api-management-client-credentials.png
[api-management-new-aad-application-menu]: ./media/api-management-howto-protect-backend-with-aad/api-management-new-aad-application-menu.png

[Create an API Management service instance]: api-management-get-started.md#create-service-instance
[Manage your first API]: api-management-get-started.md
