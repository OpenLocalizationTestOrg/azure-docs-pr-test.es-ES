---
title: aaaAuthenticating y autorizar con Power BI Embedded
description: "Autenticación y autorización con Power BI Embedded"
services: power-bi-embedded
documentationcenter: 
author: guyinacube
manager: erikre
editor: 
tags: 
ms.assetid: 1c1369ea-7dfd-4b6e-978b-8f78908fd6f6
ms.service: power-bi-embedded
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: powerbi
ms.date: 03/11/2017
ms.author: asaxton
ms.openlocfilehash: 483ca0499e8d03584e1151d3d278c0179d4b8fbe
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="authenticating-and-authorizing-with-power-bi-embedded"></a>Autenticación y autorización con Power BI Embedded

Hola servicio Power BI Embedded usa **claves** y **aplicación Tokens** para la autenticación y autorización, en lugar de autenticación explícita del usuario final. En este modelo, la aplicación, la aplicación administra la autenticación y la autorización de sus usuarios finales. Cuando sea necesario, la aplicación crea y envía los Tokens de aplicación Hola que indica a nuestro servicio toorender Hola informe solicitado. Este diseño no requiere la toouse aplicación Azure Active Directory para la autenticación y autorización, aunque puede seguir.

## <a name="two-ways-tooauthenticate"></a>Dos formas tooauthenticate

**Clave**: puede usar claves para todas las llamadas de API de REST de Power BI Embedded. Hola claves pueden encontrarse en hello **portal de Azure** haciendo clic en **toda la configuración de** y, a continuación, **las claves de acceso**. Debe tratar siempre la clave como si fuese una contraseña. Estas claves tienen toomake permisos llamar cualquier API de REST en una colección de área de trabajo determinada.

toouse una clave en una llamada REST, agregue Hola siguiente encabezado de autorización:            

    Authorization: AppKey {your key}

**Token de aplicación** : los tokens de aplicación se utilizan para todas las solicitudes de inserción. Están diseñadas toobe ejecutar de cliente, por lo que están restringidos tooa único informe y sus tooset prácticas recomendada un tiempo de expiración.

Los tokens de aplicación son un JWT (JSON Web Token) que está firmado por una de sus claves.

El token de aplicación puede contener Hola siguientes notificaciones:

| Notificación | Description |
| --- | --- |
| **ver** |versión de Hola de token de aplicación Hola. 0.2.0 es la versión actual de Hola. |
| **aud** |Hola destinatario del token de Hola. Para usar Power BI Embedded: "https://analysis.windows.net/powerbi/api". |
| **iss** |Una cadena que indica la aplicación hello que Hola token emitido. |
| **type** |tipo de Hello del token de aplicación que se va a crear. Tipo de hello solo admitido actual es **incrustar**. |
| **wcn** |Se está emitiendo el token de Hola de nombre de colección de área de trabajo para. |
| **wid** |Se está emitiendo el token de Hola de Id. de área de trabajo para. |
| **rid** |Se está emitiendo el token de Hola de Id. de informe para. |
| **username** (opcional) |Se utiliza con RLS, esto es una cadena que puede ayudar a identificar usuario Hola al aplicar reglas RLS. |
| **roles** (opcional) |Una cadena que contiene Hola roles tooselect al aplicar las reglas de seguridad de nivel de fila. Si se pasa más de un rol, se deben pasar como una matriz de cadenas. |
| **scp** (opcional) |Una cadena que contiene ámbitos de permisos de Hola. Si se pasa más de un rol, se deben pasar como una matriz de cadenas. |
| **exp** (opcional) |Indica el tiempo de hello en qué Hola token expirará. Se deben pasar como marcas de tiempo de Unix. |
| **nbf** (opcional) |Indica el tiempo de hello en qué Hola token inicia no es válida. Se deben pasar como marcas de tiempo de Unix. |

Un ejemplo de token de aplicación tendrá este aspecto:

```
eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJ2ZXIiOiIwLjIuMCIsInR5cGUiOiJlbWJlZCIsIndjbiI6Ikd1eUluQUN1YmUiLCJ3aWQiOiJkNGZlMWViMS0yNzEwLTRhNDctODQ3Yy0xNzZhOTU0NWRhZDgiLCJyaWQiOiIyNWMwZDQwYi1kZTY1LTQxZDItOTMyYy0wZjE2ODc2ZTNiOWQiLCJzY3AiOiJSZXBvcnQuUmVhZCIsImlzcyI6IlBvd2VyQklTREsiLCJhdWQiOiJodHRwczovL2FuYWx5c2lzLndpbmRvd3MubmV0L3Bvd2VyYmkvYXBpIiwiZXhwIjoxNDg4NTAyNDM2LCJuYmYiOjE0ODg0OTg4MzZ9.v1znUaXMrD1AdMz6YjywhJQGY7MWjdCR3SmUSwWwIiI
```

Cuando se descodifica, tendrá un aspecto similar al siguiente:

```
Header

{
    typ: "JWT",
    alg: "HS256:
}

Body

{
  "ver": "0.2.0",
  "wcn": "SupportDemo",
  "wid": "ca675b19-6c3c-4003-8808-1c7ddc6bd809",
  "rid": "96241f0f-abae-4ea9-a065-93b428eddb17",
  "iss": "PowerBISDK",
  "aud": "https://analysis.windows.net/powerbi/api",
  "exp": 1360047056,
  "nbf": 1360043456
}

```

Hay métodos disponibles dentro de hello SDK que facilitan la creación de apptokens. Por ejemplo, para .NET puede mirar hello [Microsoft.PowerBI.Security.PowerBIToken](https://docs.microsoft.com/dotnet/api/microsoft.powerbi.security.powerbitoken) hello y clase [CreateReportEmbedToken](https://docs.microsoft.com/dotnet/api/microsoft.powerbi.security.powerbitoken?redirectedfrom=MSDN#methods_) métodos.

Para hello .NET SDK, puede remitir demasiado[ámbitos](https://docs.microsoft.com/dotnet/api/microsoft.powerbi.security.scopes).

## <a name="scopes"></a>Ámbitos

Cuando se usa tokens de insertar, puede que desee toorestrict uso de recursos de hello a que ofrecen acceso. Por este motivo, puede generar un token con permisos con ámbito.

siguiente Hola es Hola dos ámbitos disponibles para Power BI Embedded.

|Scope|Descripción|
|---|---|
|Dataset.Read|Proporciona permiso tooread Hola especifica el conjunto de datos.|
|Dataset.Write|Proporciona permiso toowrite toohello especificado conjunto de datos.|
|Dataset.ReadWrite|Proporciona permiso tooread y escritura toohello especificado conjunto de datos.|
|Report.Read|Proporciona permiso tooview Hola especifica el informe.|
|Report.ReadWrite|Proporciona la edición y permiso tooview Hola informe especificado.|
|Workspace.Report.Create|Proporciona permiso toocreate un nuevo informe en hello especificado área de trabajo.|
|Workspace.Report.Copy|Proporciona un informe existente en hello especificado de permiso tooclone área de trabajo.|

Puede proporcionar varios ámbitos mediante el uso de un espacio entre los ámbitos de hello como Hola siguiente.

```
string scopes = "Dataset.Read Workspace.Report.Create";
```

**Notificaciones necesarias: ámbitos**

SCP: {scopesClaim} scopesClaim puede ser una cadena o una matriz de cadenas, teniendo en cuenta permisos permitidos hello tooworkspace recursos (informe, conjunto de datos, etcetera.)

Un token descodificado, con ámbitos definidos, tendría un aspecto similar a continuación toohello.

```
Header

{
    typ: "JWT",
    alg: "HS256:
}

Body

{
  "ver": "0.2.0",
  "wcn": "SupportDemo",
  "wid": "ca675b19-6c3c-4003-8808-1c7ddc6bd809",
  "rid": "96241f0f-abae-4ea9-a065-93b428eddb17",
  "scp": "Report.Read",
  "iss": "PowerBISDK",
  "aud": "https://analysis.windows.net/powerbi/api",
  "exp": 1360047056,
  "nbf": 1360043456
}

```

### <a name="operations-and-scopes"></a>Operaciones y ámbitos

|Operación|Recurso de destino|Permisos de token|
|---|---|---|
|Crea (en memoria) un informe nuevo basado en un conjunto de datos.|Dataset|Dataset.Read|
|Crear un nuevo informe basado en un conjunto de datos de (en memoria) y guardar el informe de Hola.|Dataset|* Dataset.Read<br>* Workspace.Report.Create|
|Ve y explora o edite (en memoria) un informe existente. Report.Read implica Dataset.Read. Esto no le permitirá permisos toosave modificaciones.|Informe|Report.Read|
|Edita y guarda un informe existente.|Informe|Report.ReadWrite|
|Guarda una copie de un informe (Guardar como).|Informe|* Report.Read<br>* Workspace.Report.Copy|

## <a name="heres-how-hello-flow-works"></a>Aquí es cómo funciona el flujo de Hola
1. Copie la aplicación de tooyour de claves de API de hello. Puede obtener las claves de hello **Portal de Azure**.
   
    ![](media/powerbi-embedded-get-started-sample/azure-portal.png)
2. El token impone una notificación y tiene un tiempo de expiración.
   
    ![](media/powerbi-embedded-get-started-sample/power-bi-embedded-token-2.png)
3. El token se firma con las claves de acceso de la API.
   
    ![](media/powerbi-embedded-get-started-sample/power-bi-embedded-token-3.png)
4. El usuario solicita tooview un informe.
   
    ![](media/powerbi-embedded-get-started-sample/power-bi-embedded-token-4.png)
5. El token se valida con claves de acceso de una API.
   
   ![](media/powerbi-embedded-get-started-sample/power-bi-embedded-token-5.png)
6. Power BI Embedded envía un informe toouser.
   
   ![](media/powerbi-embedded-get-started-sample/power-bi-embedded-token-6.png)

Después de **Power BI Embedded** envía un usuario de toohello informes, usuario Hola puede ver el informe de hello en la aplicación personalizada. Por ejemplo, si importó hello [ejemplo de análisis de ventas datos PBIX](http://download.microsoft.com/download/1/4/E/14EDED28-6C58-4055-A65C-23B4DA81C4DE/Analyzing_Sales_Data.pbix), aplicación web de ejemplo de Hola sería similar al siguiente:

![](media/powerbi-embedded-get-started-sample/sample-web-app.png)

## <a name="see-also"></a>Otras referencias

[CreateReportEmbedToken](https://docs.microsoft.com/dotnet/api/microsoft.powerbi.security.powerbitoken?redirectedfrom=MSDN#methods_)  
[Get started with Microsoft Power BI Embedded sample (Introducción al ejemplo de Microsoft Power BI Embedded)](power-bi-embedded-get-started-sample.md)  
[Common Microsoft Power BI Embedded scenarios (Escenarios comunes de Microsoft Power BI Embedded)](power-bi-embedded-scenarios.md)  
[Introducción a Microsoft Power BI Embedded](power-bi-embedded-get-started.md)  
[Repositorio GIT PowerBI-CSharp](https://github.com/Microsoft/PowerBI-CSharp)  
¿Tiene más preguntas? [Intente Hola Comunidad de Power BI](http://community.powerbi.com/)

