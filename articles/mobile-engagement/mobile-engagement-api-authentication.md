---
title: aaaAuthenticate con las API de REST de Mobile Engagement
description: "Describe cómo tooauthenticate con API de REST de Azure Mobile Engagement"
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: da82cb36-957a-4e19-a805-b44733cf6597
ms.service: mobile-engagement
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: mobile-multiple
ms.workload: mobile
ms.date: 10/05/2016
ms.author: wesmc;ricksal
ms.openlocfilehash: 9b54aa5ec3da4bcf55ffe5b7e8d1759095d0c486
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="authenticate-with-mobile-engagement-rest-apis"></a>Autenticación con las API de REST de Mobile Engagement
## <a name="overview"></a>Información general
Este documento describe cómo tooget un Oauth de AAD válido token tooauthenticate con hello las API de REST de Mobile Engagement. 

Se supone que tiene una suscripción válida a Azure y que ha creado una aplicación de Mobile Engagement con uno de nuestros [tutoriales para desarrolladores](mobile-engagement-windows-store-dotnet-get-started.md).

## <a name="authentication"></a>Autenticación
Se usa un token de OAuth basado en Microsoft Azure Active Directory para la autenticación. 

En la solicitud de pedido de tooauthentication una API, un encabezado de autorización debe agregarse solicitud tooevery que es de hello siguiente forma:

    Authorization: Bearer eyJ0eXAiOiJKV1QiLCJhbGmJlNmV2ZWJPamg2TTNXR1E...

> [!NOTE]
> Los tokens de Azure Active Directory caducan en 1 hora.
> 
> 

Hay varias tooget formas un token. Desde Hola que suele llamar a las API de un servicio de nube que desee toouse una clave de API. En la terminología de Azure, a una clave de API se la conoce como contraseña de entidad de servicio. Hello siguiente procedimiento describe una manera de toosetting una copia de seguridad manualmente.

### <a name="one-time-setup-using-script"></a>Instalación única (mediante script)
Conjunto de Hola de instrucciones que aparecen debajo de la instalación de hello tooperform mediante un script de PowerShell que lleva tiempo mínimo de hello para el programa de instalación, pero utiliza valores predeterminados más admisibles de hello debe seguir. Si lo desea, también puede seguir las instrucciones de Hola Hola [el programa de instalación manual](mobile-engagement-api-authentication-manual.md) para hacer esto desde Hola directamente portal de Azure y la configuración más preciso de. 

1. Obtener la versión más reciente de Hola de PowerShell de Azure desde [aquí](http://aka.ms/webpi-azps). Para obtener más información sobre las instrucciones de descarga de hello, puede ver esto [vínculo](/powershell/azure/overview).  
2. Una vez instalado Azure PowerShell, siguiente Hola de uso comandos tooensure que tengan hello **módulo de Azure** instalado:
   
    a. Asegúrese de que el módulo de Azure PowerShell Hola está disponible en la lista Hola de los módulos disponibles. 
   
        Get-Module –ListAvailable 
   
    ![Módulos de Azure disponibles][1]
   
    b. Si no encontró el módulo de PowerShell de Azure de Hola Hola por encima de la lista, a continuación, necesita toorun Hola siguiente:
   
        Import-Module Azure 
3. Inicio de sesión toohello Azure Resource Manager desde PowerShell mediante la ejecución de Hola siguiente comando y proporcionar su nombre de usuario y contraseña para su cuenta de Azure: 
   
        Login-AzureRmAccount
4. Si tiene varias suscripciones, a continuación, se deben ejecutar siguientes de hello:
   
    a. Obtener una lista de todas las suscripciones y Hola copia SubscriptionId de suscripción de hello que desea toouse. Asegúrese de que esta suscripción es igual a uno que tenga Hola aplicación de interacción móvil que va de hello toointeract con el uso de las API de Hola. 
   
        Get-AzureRmSubscription
   
    b. Siguiente ejecución Hola comando proporcionando Hola SubscriptionId tooconfigure Hola suscripción toobe usa.
   
        Select-AzureRmSubscription –SubscriptionId <subscriptionId>
5. Copiar texto de Hola de hello [New-AzureRmServicePrincipalOwner.ps1](https://raw.githubusercontent.com/matt-gibbs/azbits/master/src/New-AzureRmServicePrincipalOwner.ps1) equipo local tooyour de script y guárdelo como un cmdlet de PowerShell (p. ej. `APIAuth.ps1`) y lo ejecuta `.\APIAuth.ps1`. 
6. Hello script le pedirá que tooprovide una entrada de **principalName**. Proporcionar un nombre adecuado que desea toouse toocreate la aplicación de Active Directory (por ejemplo, APIAuth). 
7. Una vez completado el script de Hola, mostrará Hola después de cuatro valores que necesitará tooauthenticate mediante programación con AD, así que haga toocopy seguro de ellos. 
   
    **TenantId**, **SubscriptionId**, **ApplicationId** y **Secret**.
   
    Usará TenantId como `{TENANT_ID}`, ApplicationId como `{CLIENT_ID}` y Secret como `{CLIENT_SECRET}`.
   
   > [!NOTE]
   > Es posible que la directiva de seguridad predeterminada le impida ejecutar scripts de PowerShell. Si es así, configure temporalmente la ejecución de secuencia de comandos tooallow de la directiva de ejecución mediante el siguiente comando de hello:
   > 
   > Set-ExecutionPolicy RemoteSigned
   > 
   > 
8. Este es el aspecto que tendría el conjunto de cmdlets de PS de hello como. 
   
    ![][3]
9. Compruebe en el portal de administración de Azure de Hola que una nueva aplicación de AD se creó con el nombre de Hola siempre toohello script llama **principalName** en **mostrar aplicaciones que tiene mi compañía**.
   
    ![][4]

#### <a name="steps-tooget-a-valid-token"></a>Pasos tooget un token válido
1. Llamada API de hello con hello parámetros siguientes y realizar seguro tooreplace Hola INQUILINO\_Id., cliente\_identificador y el cliente\_secreto:
   
   * **URL de solicitud** como *https://login.microsoftonline.com/{TENANT\_ID}/oauth2/token*
   * **Encabezado Content-Type HTTP** como *application/x-www-form-urlencoded*
   * **Cuerpo de solicitud HTTP** como *grant\_type=client\_credentials&amp;client_id={CLIENT\_ID}&amp;client_secret={CLIENT\_SECRET}&amp;resource=https%3A%2F%2Fmanagement.core.windows.net%2F*
     
     Hola te mostramos una solicitud de ejemplo:
     
       POST /{TENANT_ID}/oauth2/token HTTP/1.1   Host: login.microsoftonline.com   Content-Type: application/x-www-form-urlencoded   grant_type=client_credentials&client_id={CLIENT_ID}&client_secret={CLIENT_SECRET}&reso   urce=https%3A%2F%2Fmanagement.core.windows.net%2F
     
     Este es un ejemplo de respuesta:
     
       HTTP/1.1 200 OK   Content-Type: application/json; charset=utf-8   Content-Length: 1234
     
       {"token_type":"Bearer","expires_in":"3599","expires_on":"1445395811","not_before":"144   5391911","resource":"https://management.core.windows.net/","access_token":{ACCESS_TOKEN}}
     
     Este ejemplo incluye codificación URL de los parámetros de envío de hello, `resource` valor es realmente `https://management.core.windows.net/`. Tenga cuidado de codificar como dirección URL de tooalso `{CLIENT_SECRET}` ya que puede contener caracteres especiales.
     
     > [!NOTE]
     > Para las pruebas, puede usar una herramienta de cliente HTTP, como [Fiddler](http://www.telerik.com/fiddler) o la extensión [Postman de Chrome](https://chrome.google.com/webstore/detail/postman/fhbjgbiflinjbdggehcddcbncdddomop). 
     > 
     > 
2. Ahora en cada llamada API, incluya el encabezado de solicitud de autorización de Hola:
   
        Authorization: Bearer {ACCESS_TOKEN}
   
    Si recibe un código de 401 estado devuelve, cuerpo de respuesta de comprobación de hello, podría indicarle Hola token ha caducado. En ese caso, obtenga un nuevo token.

## <a name="using-hello-apis"></a>Usar las API de Hola
Ahora que tiene un token válido, está listo toomake Hola API llamadas.

1. En cada solicitud de API, deberá toopass un token válido y vigente que obtuvo en la sección anterior de Hola.
2. Necesitará tooplug algunos parámetros en la solicitud de hello URI que identifica la aplicación. URI de solicitud de Hello aspecto Hola siguiente
   
        https://management.azure.com/subscriptions/{subscription-id}/resourcegroups/{resource-group-name}/
        providers/Microsoft.MobileEngagement/appcollections/{app-collection}/apps/{app-resource-name}/
   
    parámetros de hello tooget, haga clic en el nombre de la aplicación y haga clic en el panel y verá una página como siguiente de Hola a todos Hola 3 parámetros.
   
   * **1**`{subscription-id}`
   * **2**`{app-collection}`
   * **3**`{app-resource-name}`
   * **4** nombre de su grupo de recursos va toobe **MobileEngagement** a menos que cree uno nuevo. 
     
     ![Parámetros de URI de la API de Mobile Engagement][2]

> [!NOTE]
> <br/>
> 
> 1. Omitir Hola API raíz dirección tal y como se trataba de hello API anteriores.<br/>
> 2. Si ha creado la aplicación hello mediante el portal de Azure clásico, a continuación, necesita nombre de recurso de la aplicación de hello toouse que es diferente del nombre de la aplicación hello propio. Si ha creado la aplicación hello en hello Portal de Azure, a continuación, debe usar Hola nombre de aplicación (no hay ningún diferenciación entre el nombre del recurso de aplicación y el nombre de aplicación para las aplicaciones creadas en el nuevo portal de hello).  
> 
> 

<!-- Images -->
[1]: ./media/mobile-engagement-api-authentication/azure-module.png
[2]: ./media/mobile-engagement-api-authentication/mobile-engagement-api-uri-params.png
[3]: ./media/mobile-engagement-api-authentication/ps-cmdlets.png
[4]: ./media/mobile-engagement-api-authentication/ad-app-creation.png



