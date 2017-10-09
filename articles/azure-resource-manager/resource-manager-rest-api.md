---
title: aaaResource API de REST del administrador | Documentos de Microsoft
description: "Información general de hello autenticación de las API de REST del Administrador de recursos y ejemplos de uso"
services: azure-resource-manager
documentationcenter: na
author: navalev
manager: timlt
editor: 
ms.assetid: e8d7a1d2-1e82-4212-8288-8697341408c5
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 01/13/2017
ms.author: navale;tomfitz;
ms.openlocfilehash: 3ccc3575c5e06c41f2fdc5317711980fc6a2f649
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="resource-manager-rest-apis"></a>API de REST de Resource Manager
> [!div class="op_single_selector"]
> * [Azure PowerShell](powershell-azure-resource-manager.md)
> * [CLI de Azure](xplat-cli-azure-resource-manager.md)
> * [Portal](resource-group-portal.md) 
> * [API DE REST](resource-manager-rest-api.md)
> 
> 

Detrás de cada llamada tooAzure Administrador de recursos, detrás de cada plantilla de implementada, detrás de cada cuenta de almacenamiento configurada existen API de REST de uno o más llamadas toohello Azure Resource Manager. Este tema es toothose destinado API y cómo se puede llamar sin usar ningún SDK en absoluto. Este enfoque es útil si desea un control total de solicitudes tooAzure u Hola SDK para su idioma preferido no está disponible o no es compatible con operaciones de Hola que necesita.

En este artículo no pasa por todas las API que se expone en Azure, sino que usa algunas operaciones como ejemplos de cómo conectar toothem. Una vez que comprenda los conceptos básicos de hello, puede leer hello [Azure Resource Manager REST API Reference](https://docs.microsoft.com/rest/api/resources/) toofind información detallada sobre cómo rest de hello toouse de Hola API.

## <a name="authentication"></a>Autenticación
La autenticación para Resource Manager se controla mediante Azure Active Directory (AD). tooconnect tooany API, primero debe tooauthenticate con Azure AD tooreceive un token de autenticación que se puede pasar en tooevery solicitud. Como describimos una llamada pura directamente toohello las API de REST, suponemos que no quiere tooauthenticate, que se le pida un nombre de usuario y una contraseña. También se supone que no usa dos mecanismos de autenticación en dos fases. Por lo tanto, creamos lo que se conoce como una aplicación de Azure AD y una entidad de servicio que son toolog usado en. Pero recuerde que Azure AD admite varios procedimientos de autenticación y todas ellas podría ser tooretrieve usa ese token de autenticación que necesitamos para las solicitudes posteriores de API.
Siga las instrucciones paso a paso disponibles en [Uso del portal para crear una aplicación de Active Directory y una entidad de servicio con acceso a los recursos](resource-group-create-service-principal-portal.md).

### <a name="generating-an-access-token"></a>Generación de un token de acceso
Autenticación en Azure AD se realiza llamando al exterior tooAzure AD, ubicado en login.microsoftonline.com. tooauthenticate, necesita hello toohave siguiente información:

* Id. de inquilino de Azure AD (Hola nombre de que Azure AD que usa toolog en, a menudo Hola igual que su empresa, pero no es necesario)
* Identificador de la aplicación (realizada durante el paso de creación de la aplicación hello Azure AD)
* Contraseña (que seleccionó durante la creación de hello aplicación de Azure AD)

Hola después de la solicitud HTTP, asegúrese de tooreplace seguro "Identificador de inquilino de Azure AD," "Id. de aplicación" y "Contraseña" con los valores correctos de Hola.

**Solicitud HTTP genérica:**

```HTTP
POST /<Azure AD Tenant ID>/oauth2/token?api-version=1.0 HTTP/1.1 HTTP/1.1
Host: login.microsoftonline.com
Cache-Control: no-cache
Content-Type: application/x-www-form-urlencoded

grant_type=client_credentials&resource=https%3A%2F%2Fmanagement.core.windows.net%2F&client_id=<Application ID>&client_secret=<Password>
```

... will (si la autenticación se realiza correctamente) como resultado un toohello similar de respuesta después de respuesta:

```json
{
  "token_type": "Bearer",
  "expires_in": "3600",
  "expires_on": "1448199959",
  "not_before": "1448196059",
  "resource": "https://management.core.windows.net/",
  "access_token": "eyJ0eXAiOiJKV1QiLCJhb...86U3JI_0InPUk_lZqWvKiEWsayA"
}
```
(access_token Hola Hola anterior respuesta ha sido tooincrease abreviado legibilidad)

**Generación del token de acceso con Bash:**

```console
curl -X POST -H "Content-Type: application/x-www-form-urlencoded" -d "grant_type=client_credentials&resource=https://management.core.windows.net/&client_id=<application id>&client_secret=<password you selected for authentication>" https://login.microsoftonline.com/<Azure AD Tenant ID>/oauth2/token?api-version=1.0
```

**Generación del token de acceso con PowerShell:**

```powershell
Invoke-RestMethod -Uri https://login.microsoftonline.com/<Azure AD Tenant ID>/oauth2/token?api-version=1.0 -Method Post
 -Body @{"grant_type" = "client_credentials"; "resource" = "https://management.core.windows.net/"; "client_id" = "<application id>"; "client_secret" = "<password you selected for authentication>" }
```

respuesta de Hello contiene un token de acceso, la información sobre cuánto tiempo ese token es válido y la información sobre qué recursos puede usar ese token para.
token de acceso de Hola que recibiste por llamada HTTP anterior Hola debe pasarse en para todos los toohello de solicitud API del Administrador de recursos. Pasa dicho valor como un valor de encabezado denominado "Autorización" con el valor de Hola "Portador YOUR_ACCESS_TOKEN". Observe el espacio de hello entre "Portador" y el token de acceso.

Como puede ver de Hola por encima del resultado de HTTP, el token de hello es válido durante un período de tiempo durante el cual se debe almacenar en caché y volver a ese mismo token específico. Aunque es posible tooauthenticate en Azure AD para cada llamada API, sería muy ineficiente.

## <a name="calling-resource-manager-rest-apis"></a>Llamada a las API de REST de Resource Manager
Este tema utiliza sólo algunas API tooexplain Hola uso básico de operaciones de REST de Hola. Para obtener información acerca de todas las operaciones de hello, consulte [API de REST del Administrador de recursos de Azure](https://docs.microsoft.com/rest/api/resources/).

### <a name="list-all-subscriptions"></a>Enumeración de todas las suscripciones
Uno de operaciones más sencillas de hello que puede realizar es toolist Hola disponibles las suscripciones que pueda tener acceso. Hola después de la solicitud, verá cómo se pasa el token de acceso de Hola como un encabezado:

(Reemplace YOUR_ACCESS_TOKEN por el token de acceso real).

```HTTP
GET /subscriptions?api-version=2015-01-01 HTTP/1.1
Host: management.azure.com
Authorization: Bearer YOUR_ACCESS_TOKEN
Content-Type: application/json
```

... y como resultado, obtendrá una lista de suscripciones que esta entidad de servicio se permite tooaccess

(Los identificadores de suscripción se han abreviado para mejorar la legibilidad).

```json
{
  "value": [
    {
      "id": "/subscriptions/3a8555...555995",
      "subscriptionId": "3a8555...555995",
      "displayName": "Azure Subscription",
      "state": "Enabled",
      "subscriptionPolicies": {
        "locationPlacementId": "Internal_2014-09-01",
        "quotaId": "Internal_2014-09-01"
      }
    }
  ]
}
```

### <a name="list-all-resource-groups-in-a-specific-subscription"></a>Enumeración de todos los grupos de recursos en una suscripción específica
Todos los recursos disponibles con las API del Administrador de recursos de hello están anidados dentro de un grupo de recursos. Puede consultar el Administrador de recursos para los grupos de recursos existentes en su suscripción mediante Hola después de la solicitud HTTP GET. Tenga en cuenta cómo Id. de suscripción de Hola se pasa como parte de la dirección URL de hello este momento.

(Reemplace YOUR_ACCESS_TOKEN y SUBSCRIPTION_ID por su token de acceso e identificador de suscripción reales).

```HTTP
GET /subscriptions/SUBSCRIPTION_ID/resourcegroups?api-version=2015-01-01 HTTP/1.1
Host: management.azure.com
Authorization: Bearer YOUR_ACCESS_TOKEN
Content-Type: application/json
```

Hello respuesta obtendrá depende de si tiene algún grupo de recursos definido y si es así, ¿cuántos.

(Los identificadores de suscripción se han abreviado para mejorar la legibilidad).

```json
{
    "value": [
        {
            "id": "/subscriptions/3a8555...555995/resourceGroups/myfirstresourcegroup",
            "name": "myfirstresourcegroup",
            "location": "eastus",
            "properties": {
                "provisioningState": "Succeeded"
            }
        },
        {
            "id": "/subscriptions/3a8555...555995/resourceGroups/mysecondresourcegroup",
            "name": "mysecondresourcegroup",
            "location": "northeurope",
            "tags": {
                "tagname1": "My first tag"
            },
            "properties": {
                "provisioningState": "Succeeded"
            }
        }
    ]
}
```

### <a name="create-a-resource-group"></a>Crear un grupo de recursos
Hasta ahora, nos hemos solo ha consultar Hola API del Administrador de recursos para obtener información. Es hora de crear algunos recursos y Empecemos por hello más simple de todos ellos, un grupo de recursos. Hola solicitud HTTP siguiente crea un grupo de recursos en una región o ubicación de su elección y agrega una etiqueta tooit.

(Reemplace YOUR_ACCESS_TOKEN, SUBSCRIPTION_ID, RESOURCE_GROUP_NAME por su real del Token de acceso, Id. de suscripción y nombre del grupo de recursos que desee toocreate Hola)

```HTTP
PUT /subscriptions/SUBSCRIPTION_ID/resourcegroups/RESOURCE_GROUP_NAME?api-version=2015-01-01 HTTP/1.1
Host: management.azure.com
Authorization: Bearer YOUR_ACCESS_TOKEN
Content-Type: application/json

{
  "location": "northeurope",
  "tags": {
    "tagname1": "test-tag"
  }
}
```

Si se realiza correctamente, obtendrá una respuesta similar toohello después de respuesta:

```json
{
  "id": "/subscriptions/3a8555...555995/resourceGroups/RESOURCE_GROUP_NAME",
  "name": "RESOURCE_GROUP_NAME",
  "location": "northeurope",
  "tags": {
    "tagname1": "test-tag"
  },
  "properties": {
    "provisioningState": "Succeeded"
  }
}
```

Ha creado correctamente un grupo de recursos en Azure. ¡Enhorabuena!

### <a name="deploy-resources-tooa-resource-group-using-a-resource-manager-template"></a>Implementar grupo de recursos de tooa de recursos utilizando una plantilla de administrador de recursos
Con Resource Manager, puede implementar los recursos mediante plantillas. Una plantilla define varios recursos y sus dependencias. En esta sección se supone está familiarizado con las plantillas de administrador de recursos y simplemente le mostraremos cómo toomake Hola API llamar a la implementación de toostart. Para obtener más información sobre la creación de plantillas, consulte [Authoring Azure Resource Manager templates](resource-group-authoring-templates.md) (Creación de plantillas de Azure Resource Manager).

Implementación de una plantilla no difieren mucho toohow llamar a otras API. Un aspecto importante es que la implementación de una plantilla puede tardar bastante tiempo. simplemente devuelve la llamada de API de Hola y es una tooyou como tooquery de desarrollador para estado de hello implementación toofind espera cuando se realice la implementación de Hola. Para obtener más información, consulte [Seguimiento de las operaciones asincrónicas de Azure](resource-manager-async-operations.md).

En este ejemplo, se usa una plantilla publicada y disponible en [GitHub](https://github.com/Azure/azure-quickstart-templates). plantilla de Hello que usamos implementa una región de VM de Linux toohello oeste de Estados Unidos. Aunque este ejemplo usa una plantilla disponible en un repositorio público como GitHub, puede pasar en su lugar plantilla completa hello como parte de la solicitud de saludo. Tenga en cuenta que se proporcionan valores de parámetro de solicitud de Hola que se utilizan dentro de hello implementa la plantilla.

(Reemplace SUBSCRIPTION_ID, RESOURCE_GROUP_NAME, DEPLOYMENT_NAME, YOUR_ACCESS_TOKEN, GLOBALY_UNIQUE_STORAGE_ACCOUNT_NAME, ADMIN_USER_NAME, ADMIN_PASSWORD y DNS_NAME_FOR_PUBLIC_IP toovalues adecuado para su solicitud)

```HTTP
PUT /subscriptions/SUBSCRIPTION_ID/resourcegroups/RESOURCE_GROUP_NAME/providers/microsoft.resources/deployments/DEPLOYMENT_NAME?api-version=2015-01-01 HTTP/1.1
Host: management.azure.com
Authorization: Bearer YOUR_ACCESS_TOKEN
Content-Type: application/json

{
  "properties": {
    "templateLink": {
      "uri": "https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-simple-linux-vm/azuredeploy.json",
      "contentVersion": "1.0.0.0",
    },
    "mode": "Incremental",
    "parameters": {
        "newStorageAccountName": {
          "value": "GLOBALY_UNIQUE_STORAGE_ACCOUNT_NAME"
        },
        "adminUsername": {
          "value": "ADMIN_USER_NAME"
        },
        "adminPassword": {
          "value": "ADMIN_PASSWORD"
        },
        "dnsNameForPublicIP": {
          "value": "DNS_NAME_FOR_PUBLIC_IP"
        },
        "ubuntuOSVersion": {
          "value": "15.04"
        }
    }
  }
}
```

respuesta JSON largos de Hola para esta solicitud ha sido omitido tooimprove facilitar la lectura de esta documentación. respuesta de Hello contiene información acerca de la implementación de plantillas de Hola que ha creado.

## <a name="next-steps"></a>Pasos siguientes

- toolearn sobre el control de operaciones asincrónicas de REST, consulte [realizar un seguimiento de las operaciones asincrónicas de Azure](resource-manager-async-operations.md).
