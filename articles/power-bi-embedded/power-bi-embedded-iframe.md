---
title: aaaHow toouse Power BI Embedded con REST | Documentos de Microsoft
description: "Obtenga información acerca de cómo toouse Power BI Embedded con REST "
services: power-bi-embedded
documentationcenter: 
author: guyinacube
manager: erikre
editor: 
tags: 
ms.assetid: 8bcef780-cca0-4f30-9a9b-9daa1a7ae865
ms.service: power-bi-embedded
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: powerbi
ms.date: 02/06/2017
ms.author: asaxton
ms.openlocfilehash: 98057724e60ba868f9c93de8c50383569eb8852d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-power-bi-embedded-with-rest"></a>¿Cómo toouse Power BI Embedded con REST

## <a name="power-bi-embedded-what-it-is-and-what-its-for"></a>Power BI Embedded: qué es y para qué sirve

Información general sobre Power BI Embedded se describe en oficial de hello [sitio Power BI Embedded](https://azure.microsoft.com/services/power-bi-embedded/), pero vamos a echar un vistazo rápido antes de entrar en detalles de hello sobre el uso con REST.

Es bastante sencillo. Puede que desee visualizaciones de datos dinámicos de hello toouse de [Power BI](https://powerbi.microsoft.com) en su propia aplicación.

La mayoría de las aplicaciones personalizadas necesitan datos de hello toodeliver para sus propios clientes, no necesariamente a los usuarios de su propia organización. Por ejemplo, si está entrega algún servicio de la compañía A y B de la empresa, los usuarios de la compañía A solo deben ver datos de su propia empresa A. Es decir, la arquitectura multiempresa de Hola es necesario para la entrega de Hola.

aplicación personalizada Hello también podría ofrecer sus propios métodos de autenticación, como autenticación de formularios, la autenticación básica etcetera... A continuación, Hola incrustar solución debe colaborar con este método de autenticación existente sin ningún riesgo. También es necesario para los usuarios toobe pueda toouse esas aplicaciones de ISV sin Hola compra adicional o las licencias de una suscripción de Power BI.

 **Power BI Embedded** se ha diseñado, precisamente, para estos tipos de escenario. Por lo tanto, ahora que tenemos que introducción rápida fuera de hello, vamos a profundizar algunos detalles

Puede usar .NET hello \(C#) o Node.js SDK, tooeasily Compile su aplicación con Power BI Embedded. Sin embargo, en este artículo explicaremos el flujo HTTP \(incluida la autorización) de Power BI sin los SDK. Descripción de este flujo, puede compilar su aplicación **con cualquier lenguaje de programación**, y puede comprender profundamente esencia Hola de Power BI Embedded.

## <a name="create-power-bi-workspace-collection-and-get-access-key-provisioning"></a>Creación de una colección de áreas de trabajo de Power BI y obtención de la clave de acceso \(aprovisionamiento)

Power BI Embedded es uno de hello servicios de Azure. Hola solo ISV que usa el Portal de Azure se cobra por las cuotas de uso \(por sesión de usuario cada hora), y el usuario de Hola que informe de hello vistas no está cargada o incluso requieren una suscripción de Azure.
Antes de iniciar el desarrollo de aplicaciones, debemos crear hello **colección del área de trabajo de Power BI** mediante el Portal de Azure.

Cada área de trabajo de Power BI Embedded es el área de trabajo de Hola para cada cliente (inquilino) y que podemos agregar muchas áreas de trabajo en cada colección de área de trabajo. Hola se utiliza la misma clave de acceso de cada colección de área de trabajo. En efecto, colección de área de trabajo de Hola es el límite de seguridad de Hola para Power BI Embedded.

![](media/power-bi-embedded-iframe/create-workspace.png)

Cuando se termine de crear la colección de área de trabajo de hello, copie la clave de acceso de Hola desde el Portal de Azure.

![](media/power-bi-embedded-iframe/copy-access-key.png)

> [!NOTE]
> También podemos aprovisionar la colección del área de trabajo de Hola y obtener la clave de acceso a través de la API de REST. más información, consulte toolearn [API de proveedor de recursos de Power BI](https://msdn.microsoft.com/library/azure/mt712306.aspx).

## <a name="create-pbix-file-with-power-bi-desktop"></a>Creación del archivo .pbix con Power BI Desktop

A continuación, que debemos crear la conexión de datos de Hola y toobe informes incrustados.
Para esta tarea no hay que agregar código ni realizar trabajos de programación; basta con usar Power BI Desktop.
En este artículo, no entraremos en detalles de hello acerca de cómo toouse Power BI Desktop. Si necesita más ayuda con este tema, consulte [Introducción a Power BI Desktop](https://powerbi.microsoft.com/documentation/powerbi-desktop-getting-started/). En nuestro ejemplo, vamos a usar solo hello [ejemplo de análisis de minoristas](https://powerbi.microsoft.com/documentation/powerbi-sample-datasets/).

![](media/power-bi-embedded-iframe/power-bi-desktop-1.png)

## <a name="create-a-power-bi-workspace"></a>Creación de un área de trabajo de Power BI

Ahora que el aprovisionamiento de hello todo se hace, vamos a empezar a crear área de trabajo de un cliente en la colección del área de trabajo de Hola a través de las API de REST. Hello solicitud de POST de HTTP siguiente (REST) es crear nueva área de trabajo de hello en la colección de área de trabajo existente. Se trata de hello [API de área de trabajo de POST](https://msdn.microsoft.com/library/azure/mt711503.aspx). En nuestro ejemplo, es el nombre de colección del área de trabajo de hello **mypbiapp**. Se acaba de establecer tecla de acceso de hello, que se copió anteriormente, como **AppKey**. Como podrá comprobar, se trata de una autenticación muy sencilla.

**Solicitud HTTP**

```
POST https://api.powerbi.com/v1.0/collections/mypbiapp/workspaces
Authorization: AppKey MpaUgrTv5e...
```

**Respuesta HTTP**

```
HTTP/1.1 201 Created
Content-Type: application/json; odata.metadata=minimal; odata.streaming=true
Location: https://wabi-us-east2-redirect.analysis.windows.net/v1.0/collections/mypbiapp/workspaces
RequestId: 4220d385-2fb3-406b-8901-4ebe11a5f6da

{
  "@odata.context": "http://wabi-us-east2-redirect.analysis.windows.net/v1.0/collections/mypbiapp/$metadata#workspaces/$entity",
  "workspaceId": "32960a09-6366-4208-a8bb-9e0678cdbb9d",
  "workspaceCollectionName": "mypbiapp"
}
```

Hola devuelve **workspaceId** se usa para hello siguiendo las subsiguientes llamadas a la API. Nuestra aplicación debe conservar este valor.

## <a name="import-pbix-file-into-hello-workspace"></a>Importar archivo .pbix en el área de trabajo de Hola

Cada informe en un área de trabajo corresponde tooa único archivo de Power BI Desktop con un conjunto de datos \(incluida la configuración del origen de datos). Podemos importar nuestro .pbix archivo toohello área de trabajo como se muestra en el siguiente código de hello. Como puede ver, hemos podemos cargar binario Hola de archivo .pbix con varias partes MIME en http.

fragmento de uri de Hello **32960a09-6366-4208-a8bb-9e0678cdbb9d** es workspaceId Hola y el parámetro de consulta **datasetDisplayName** es toocreate de nombre de conjunto de datos de Hola. Hola crear conjunto de datos contiene todos los datos relacionados con artefactos de archivo .pbix como datos importados, Hola origen de datos de puntero toohello, etcetera...

```
POST https://api.powerbi.com/v1.0/collections/mypbiapp/workspaces/32960a09-6366-4208-a8bb-9e0678cdbb9d/imports?datasetDisplayName=mydataset01
Authorization: AppKey MpaUgrTv5e...
Content-Type: multipart/form-data; boundary="A300testx"

--A300testx
Content-Disposition: form-data

{hello content (binary) of .pbix file}
--A300testx--
```

La ejecución de esta tarea de importación puede durar unos instantes. Cuando haya finalizado, nuestra aplicación puede solicitar el estado de la tarea de hello con el Id. de importación. En nuestro ejemplo, es el Id. de importación de hello **4eec64dd-533b-47c3-a72c-6508ad854659**.

```
HTTP/1.1 202 Accepted
Content-Type: application/json; charset=utf-8
Location: https://wabi-us-east2-redirect.analysis.windows.net/v1.0/collections/mypbiapp/workspaces/32960a09-6366-4208-a8bb-9e0678cdbb9d/imports/4eec64dd-533b-47c3-a72c-6508ad854659?tenantId=myorg
RequestId: 658bd6b4-b68d-4ec3-8818-2a94266dc220

{"id":"4eec64dd-533b-47c3-a72c-6508ad854659"}
```

siguiente Hola pide estado utilizando este identificador de importación:

```
GET https://api.powerbi.com/v1.0/collections/mypbiapp/workspaces/32960a09-6366-4208-a8bb-9e0678cdbb9d/imports/4eec64dd-533b-47c3-a72c-6508ad854659
Authorization: AppKey MpaUgrTv5e...
```

Si no está completa la tarea hello, Hola respuesta HTTP podría ser similar al siguiente:

```
HTTP/1.1 200 OK
Content-Type: application/json; charset=utf-8
RequestId: 614a13a5-4de7-43e8-83c9-9cd225535136

{
  "id": "4eec64dd-533b-47c3-a72c-6508ad854659",
  "importState": "Publishing",
  "createdDateTime": "2016-07-19T07:36:06.227",
  "updatedDateTime": "2016-07-19T07:36:06.227",
  "name": "mydataset01"
}
```

Si está completa la tarea hello, Hola respuesta HTTP podría ser parecido a lo siguiente:

```
HTTP/1.1 200 OK
Content-Type: application/json; charset=utf-8
RequestId: eb2c5a85-4d7d-4cc2-b0aa-0bafee4b1606

{
  "id": "4eec64dd-533b-47c3-a72c-6508ad854659",
  "importState": "Succeeded",
  "createdDateTime": "2016-07-19T07:36:06.227",
  "updatedDateTime": "2016-07-19T07:36:06.227",
  "reports": [
    {
      "id": "2027efc6-a308-4632-a775-b9a9186f087c",
      "name": "mydataset01",
      "webUrl": "https://app.powerbi.com/reports/2027efc6-a308-4632-a775-b9a9186f087c",
      "embedUrl": "https://app.powerbi.com/appTokenReportEmbed?reportId=2027efc6-a308-4632-a775-b9a9186f087c"
    }
  ],
  "datasets": [
    {
      "id": "458e0451-7215-4029-80b3-9627bf3417b0",
      "name": "mydataset01",
      "tables": [
      ],
      "webUrl": "https://app.powerbi.com/datasets/458e0451-7215-4029-80b3-9627bf3417b0"
    }
  ],
  "name": "mydataset01"
}
```

## <a name="data-source-connectivity-and-multi-tenancy-of-data"></a>Conectividad de los orígenes de datos \(y servicio multiinquilino de datos)

Mientras casi todos los artefactos de hello en el archivo .pbix se importan en el área de trabajo, no son credenciales de Hola para orígenes de datos. Como resultado, cuando se usa **directquerymode**, hello informes incrustados no se puede mostrar correctamente. Pero, si se usa **modo de importación**, podemos ver informes de hello con los datos importados existentes Hola. En tal caso, debemos establecemos la credencial de hello utilizando Hola siguiendo los pasos a través de llamadas de REST.

En primer lugar, debemos obtenemos el origen de datos de puerta de enlace de Hola. Sabemos que el conjunto de datos de hello **identificador** Hola previamente aparece Id. de.

**Solicitud HTTP**

```
GET https://api.powerbi.com/v1.0/collections/mypbiapp/workspaces/32960a09-6366-4208-a8bb-9e0678cdbb9d/datasets/458e0451-7215-4029-80b3-9627bf3417b0/Default.GetBoundGatewayDatasources
Authorization: AppKey MpaUgrTv5e...
```

**Respuesta HTTP**

```
GET HTTP/1.1 200 OK
Content-Type: application/json; odata.metadata=minimal; odata.streaming=true
RequestId: 574b0b18-a6fa-46a6-826c-e65840cf6e15

{
  "@odata.context": "http://wabi-us-east2-redirect.analysis.windows.net/v1.0/collections/mypbiapp/workspaces/32960a09-6366-4208-a8bb-9e0678cdbb9d/$metadata#gatewayDatasources",
  "value": [
    {
      "id": "5f7ee2e7-4851-44a1-8b75-3eb01309d0ea",
      "gatewayId": "ca17e77f-1b51-429b-b059-6b3e3e9685d1",
      "datasourceType": "Sql",
      "connectionDetails": "{\"server\":\"testserver.database.windows.net\",\"database\":\"testdb01\"}"
    }
  ]
}
```

Usar Hola devolvió el Id. de puerta de enlace y el Id. de origen de datos \(vea Hola anterior **gatewayId** y **Id. de** en hello devuelven resultados), podemos cambiar credenciales Hola de este origen de datos como se indica a continuación:

**Solicitud HTTP**

```
PATCH https://api.powerbi.com/v1.0/collections/mypbiapp/workspaces/32960a09-6366-4208-a8bb-9e0678cdbb9d/gateways/ca17e77f-1b51-429b-b059-6b3e3e9685d1/datasources/5f7ee2e7-4851-44a1-8b75-3eb01309d0ea
Authorization: AppKey MpaUgrTv5e...
Content-Type: application/json; charset=utf-8

{
  "credentialType": "Basic",
  "basicCredentials": {
    "username": "demouser",
    "password": "P@ssw0rd"
  }
}
```

**Respuesta HTTP**

```
HTTP/1.1 200 OK
Content-Type: application/octet-stream
RequestId: 0e533c13-266a-4a9d-8718-fdad90391099
```

En producción, también podemos establecer cadena de conexión diferentes de Hola para cada área de trabajo mediante API de REST. \(es decir, se puede separar base de datos de Hola para cada cliente.)

siguiente Hello es cambiar la cadena de conexión de Hola de origen de datos a través de REST.

```
POST https://api.powerbi.com/v1.0/collections/mypbiapp/workspaces/32960a09-6366-4208-a8bb-9e0678cdbb9d/datasets/458e0451-7215-4029-80b3-9627bf3417b0/Default.SetAllConnections
Authorization: AppKey MpaUgrTv5e...
Content-Type: application/json; charset=utf-8

{
  "connectionString": "data source=testserver02.database.windows.net;initial catalog=testdb02;persist security info=True;encrypt=True;trustservercertificate=False"
}
```

O bien, se puede usar seguridad de nivel de fila en Power BI Embedded y se pueden separar los datos de Hola para los usuarios en un informe. Como resultado, podemos aprovisionar cada informe de cliente con el mismo archivo .pbix \(interfaz de usuario, etc.) y distintos orígenes de datos.

> [!NOTE]
> Si usas **modo de importación** en lugar de **directquerymode**, no hay ningún modelo de toorefresh de manera a través de API. Además, en Power BI Embedded todavía no se admiten orígenes de datos locales a través de la puerta de enlace de Power BI. Sin embargo, realmente desea tookeep un ojo en hello [blog de Power BI](https://powerbi.microsoft.com/blog/) what's new y qué viene a continuación en futuras versiones.

## <a name="authentication-and-hosting-embedding-reports-in-our-web-page"></a>Autenticación y hospedaje de informes (incrustación) en nuestra página web

En Hola anterior API de REST, podemos usar la clave de acceso hello **AppKey** como encabezado de autorización de Hola. Dado que estas llamadas pueden controlarse en el lado de servidor de back-end de hello, es seguro para la ejecución.

Pero, cuando se incrusta informe hello en nuestra página web, este tipo de información de seguridad tratar con JavaScript \(front-end). A continuación, el valor de encabezado de autorización de hello debe estar protegido. Si un código o un usuario malintencionados averiguan nuestra clave de acceso, pueden llamar a cualquier operación con esta clave.

Cuando se incrusta informe hello en nuestra página web, debemos usar Hola calculada símbolo (token) en lugar de la clave de acceso **AppKey**. Nuestra aplicación debe crear hello OAuth Json Web Token \(JWT) que consta de notificaciones de Hola y firma digital de hello calculada. Tal y como se muestra a continuación, este JWT de OAuth es un token de cadena codificada delimitada por puntos.

![](media/power-bi-embedded-iframe/oauth-jwt.png)

En primer lugar, debemos preparamos el valor de entrada de hello, que está firmada más adelante. Este valor es la cadena de dirección url codificada (rfc4648) de base64 de Hola de hello después de json y estos están delimitados por punto de hello \(.) caracteres. Más adelante, explicaremos cómo tooget Hola Id. de informe.

> [!NOTE]
> Si queremos toouse seguridad de nivel de fila (RLS) con Power BI Embedded, debemos también especificamos **nombre de usuario** y **roles** en las notificaciones de Hola.

```
{
  "typ":"JWT",
  "alg":"HS256"
}
```

```
{
  "wid":"{workspace id}",
  "rid":"{report id}",
  "wcn":"{workspace collection name}",
  "iss":"PowerBISDK",
  "ver":"0.2.0",
  "aud":"https://analysis.windows.net/powerbi/api",
  "nbf":{start time of token expiration},
  "exp":{end time of token expiration}
}
```

A continuación, debemos crear cadena codificada en base64 de Hola de HMAC \(firma hello) con el algoritmo SHA256. Este valor de entrada con signo es cadena anterior Hola.

Por último, se deben combinar valor de entrada de Hola y cadena de firma con punto \(.) caracteres. cadena de Hello completado es token de aplicación Hola Hola inserción de informes. Incluso si un usuario malintencionado detectan un token de aplicación hello, no pueden obtener clave de acceso original de Hola. Este token de aplicación expira rápidamente.

Este es un ejemplo PHP de estos pasos:

```
<?php
// 1. power bi access key
$accesskey = "MpaUgrTv5e...";

// 2. construct input value
$token1 = "{" .
  "\"typ\":\"JWT\"," .
  "\"alg\":\"HS256\"" .
  "}";
$token2 = "{" .
  "\"wid\":\"32960a09-6366-4208-a8bb-9e0678cdbb9d\"," . // workspace id
  "\"rid\":\"2027efc6-a308-4632-a775-b9a9186f087c\"," . // report id
  "\"wcn\":\"mypbiapp\"," . // workspace collection name
  "\"iss\":\"PowerBISDK\"," .
  "\"ver\":\"0.2.0\"," .
  "\"aud\":\"https://analysis.windows.net/powerbi/api\"," .
  "\"nbf\":" . date("U") . "," .
  "\"exp\":" . date("U" , strtotime("+1 hour")) .
  "}";
$inputval = rfc4648_base64_encode($token1) .
  "." .
  rfc4648_base64_encode($token2);

// 3. get encoded signature
$hash = hash_hmac("sha256",
    $inputval,
    $accesskey,
    true);
$sig = rfc4648_base64_encode($hash);

// 4. show result (which is hello apptoken)
$apptoken = $inputval . "." . $sig;
echo($apptoken);

// helper functions
function rfc4648_base64_encode($arg) {
  $res = $arg;
  $res = base64_encode($res);
  $res = str_replace("/", "_", $res);
  $res = str_replace("+", "-", $res);
  $res = rtrim($res, "=");
  return $res;
}
?>
```

## <a name="finally-embed-hello-report-into-hello-web-page"></a>Por último, incrustar informes de hello en la página web de Hola

Para incrustar el informe, debemos obtener Hola incrustar la dirección url y el informe **identificador** mediante Hola después de la API de REST.

**Solicitud HTTP**

```
GET https://api.powerbi.com/v1.0/collections/mypbiapp/workspaces/32960a09-6366-4208-a8bb-9e0678cdbb9d/reports
Authorization: AppKey MpaUgrTv5e...
```

**Respuesta HTTP**

```
HTTP/1.1 200 OK
Content-Type: application/json; odata.metadata=minimal; odata.streaming=true
RequestId: d4099022-405b-49d3-b3b7-3c60cf675958

{
  "@odata.context": "http://wabi-us-east2-redirect.analysis.windows.net/v1.0/collections/mypbiapp/workspaces/32960a09-6366-4208-a8bb-9e0678cdbb9d/$metadata#reports",
  "value": [
    {
      "id": "2027efc6-a308-4632-a775-b9a9186f087c",
      "name": "mydataset01",
      "webUrl": "https://app.powerbi.com/reports/2027efc6-a308-4632-a775-b9a9186f087c",
      "embedUrl": "https://embedded.powerbi.com/appTokenReportEmbed?reportId=2027efc6-a308-4632-a775-b9a9186f087c",
      "isFromPbix": false
    }
  ]
}
```

Se puedan incrustar informes de hello en nuestra aplicación web con token de aplicación anterior de Hola.
Si miramos siguiente código de ejemplo Hola, parte anterior hello es Hola igual que el anterior ejemplo de Hola. En la última parte de hello, este ejemplo muestra hello **embedUrl** \(ver Hola de resultados anterior) en Hola iframe y está enviando el token de aplicación hello en hello iframe.

> [!NOTE]
> Necesitará tooone toochange Hola informe Id. valor de su elección. Además, debido a errores de tooa en nuestro sistema de administración de contenido, se lee literalmente etiqueta de iframe de hello en el ejemplo de código de hello. Quitar texto hello limitado de etiqueta de hello si copia y pega este código de ejemplo.

```
    <?php
    // 1. power bi access key
    $accesskey = "MpaUgrTv5e...";

    // 2. construct input value
    $token1 = "{" .
      "\"typ\":\"JWT\"," .
      "\"alg\":\"HS256\"" .
      "}";
    $token2 = "{" .
      "\"wid\":\"32960a09-6366-4208-a8bb-9e0678cdbb9d\"," . // workspace id
      "\"rid\":\"2027efc6-a308-4632-a775-b9a9186f087c\"," . // report id
      "\"wcn\":\"mypbiapp\"," . // workspace collection name
      "\"iss\":\"PowerBISDK\"," .
      "\"ver\":\"0.2.0\"," .
      "\"aud\":\"https://analysis.windows.net/powerbi/api\"," .
      "\"nbf\":" . date("U") . "," .
      "\"exp\":" . date("U" , strtotime("+1 hour")) .
      "}";
    $inputval = rfc4648_base64_encode($token1) .
      "." .
      rfc4648_base64_encode($token2);

    // 3. get encoded signature value
    $hash = hash_hmac("sha256",
        $inputval,
        $accesskey,
        true);
    $sig = rfc4648_base64_encode($hash);

    // 4. get apptoken
    $apptoken = $inputval . "." . $sig;

    // helper functions
    function rfc4648_base64_encode($arg) {
      $res = $arg;
      $res = base64_encode($res);
      $res = str_replace("/", "_", $res);
      $res = str_replace("+", "-", $res);
      $res = rtrim($res, "=");
      return $res;
    }
    ?>
    <!DOCTYPE html>
    <html>
    <head>
      <meta charset="utf-8" />
      <meta http-equiv="X-UA-Compatible" content="IE=edge">
      <title>Test page</title>
      <meta name="viewport" content="width=device-width, initial-scale=1">
    </head>
    <body>
      <button id="btnView">View Report !</button>
      <div id="divView">
        <**REMOVE THIS CAPPED TEXT IF COPIED** iframe id="ifrTile" width="100%" height="400"></iframe>
      </div>
      <script>
        (function () {
          document.getElementById('btnView').onclick = function() {
            var iframe = document.getElementById('ifrTile');
            iframe.src = 'https://embedded.powerbi.com/appTokenReportEmbed?reportId=2027efc6-a308-4632-a775-b9a9186f087c';
            iframe.onload = function() {
              var msgJson = {
                action: "loadReport",
                accessToken: "<?=$apptoken?>",
                height: 500,
                width: 722
              };
              var msgTxt = JSON.stringify(msgJson);
              iframe.contentWindow.postMessage(msgTxt, "*");
            };
          };
        }());
      </script>
    </body>
```

Este es el resultado:

![](media/power-bi-embedded-iframe/view-report.png)

En este momento, Power BI Embedded solo muestra hello informe en hello iframe. Pero, esté atento hello [Blog de Power BI](https://powerbi.microsoft.com/blog/). Mejoras futuras pudieron utilizar cliente nueva API que se Permítanos enviar información en hello iframe así como para obtener información de. Sin duda, una característica realmente útil.

## <a name="see-also"></a>Otras referencias
* [Autenticación y autorización con Power BI Embedded](power-bi-embedded-app-token-flow.md)

¿Tiene más preguntas? [Intente Hola Comunidad de Power BI](http://community.powerbi.com/)

