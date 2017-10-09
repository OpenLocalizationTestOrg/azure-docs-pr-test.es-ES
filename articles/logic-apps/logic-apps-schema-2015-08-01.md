---
title: "aaaSchema actualiza la vista previa del 1 de agosto de 2015: las aplicaciones lógicas de Azure | Documentos de Microsoft"
description: "Creación de definiciones de JSON para Azure Logic Apps con la versión de esquema 2015-08-01-preview"
author: stepsic-microsoft-com
manager: anneta
editor: 
services: logic-apps
documentationcenter: 
ms.assetid: 0d03a4d4-e8a8-4c81-aed5-bfd2a28c7f0c
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.custom: H1Hack27Feb2017
ms.date: 05/31/2016
ms.author: LADocs; stepsic
ms.openlocfilehash: 950cd18a27aa1859c4f0b6116de3fb8699d746c4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="schema-updates-for-azure-logic-apps---august-1-2015-preview"></a><span data-ttu-id="be28c-103">Actualizaciones de esquema para Azure Logic Apps de la versión preliminar del 1 de agosto de 2015</span><span class="sxs-lookup"><span data-stu-id="be28c-103">Schema updates for Azure Logic Apps - August 1, 2015 preview</span></span>

<span data-ttu-id="be28c-104">Este nuevo esquema y la API de la versión para las aplicaciones lógicas de Azure incluye mejoras claves que hacen que las aplicaciones lógicas más toouse más fácil y confiable:</span><span class="sxs-lookup"><span data-stu-id="be28c-104">This new schema and API version for Azure Logic Apps includes key improvements that make logic apps more reliable and easier toouse:</span></span>

*   <span data-ttu-id="be28c-105">Hola **APIApp** tipo de acción es actualizada tooa nueva [ **APIConnection** ](#api-connections) tipo de acción.</span><span class="sxs-lookup"><span data-stu-id="be28c-105">hello **APIApp** action type is updated tooa new [**APIConnection**](#api-connections) action type.</span></span>
*   <span data-ttu-id="be28c-106">**Repita** se cambia el nombre demasiado[**Foreach**](#foreach).</span><span class="sxs-lookup"><span data-stu-id="be28c-106">**Repeat** is renamed too[**Foreach**](#foreach).</span></span>
*   <span data-ttu-id="be28c-107">Hola [ **escucha HTTP** API App](#http-listener) ya no es necesario.</span><span class="sxs-lookup"><span data-stu-id="be28c-107">hello [**HTTP Listener** API App](#http-listener) is no longer required.</span></span>
*   <span data-ttu-id="be28c-108">En la llamada a los flujos de trabajo secundarios se usa un [nuevo esquema](#child-workflows).</span><span class="sxs-lookup"><span data-stu-id="be28c-108">Calling child workflows uses a [new schema](#child-workflows).</span></span>

<a name="api-connections"></a>
## <a name="move-tooapi-connections"></a><span data-ttu-id="be28c-109">Mover las conexiones de tooAPI</span><span class="sxs-lookup"><span data-stu-id="be28c-109">Move tooAPI connections</span></span>

<span data-ttu-id="be28c-110">Hola mayor cambio es que ya no tienen aplicaciones de API de toodeploy en su suscripción de Azure para que pueda usar las API.</span><span class="sxs-lookup"><span data-stu-id="be28c-110">hello biggest change is that you no longer have toodeploy API Apps into your Azure subscription so you can use APIs.</span></span> <span data-ttu-id="be28c-111">Estas son formas de Hola que puede usar las API:</span><span class="sxs-lookup"><span data-stu-id="be28c-111">Here are hello ways that you can use APIs:</span></span>

* <span data-ttu-id="be28c-112">API administradas</span><span class="sxs-lookup"><span data-stu-id="be28c-112">Managed APIs</span></span>
* <span data-ttu-id="be28c-113">Sus API web personalizadas</span><span class="sxs-lookup"><span data-stu-id="be28c-113">Your custom Web APIs</span></span>

<span data-ttu-id="be28c-114">Cada una se controla de forma algo distinta, ya que sus modelos de administración y hospedaje son diferentes.</span><span class="sxs-lookup"><span data-stu-id="be28c-114">Each way is handled slightly differently because their management and hosting models are different.</span></span> <span data-ttu-id="be28c-115">Una ventaja de este modelo es que ya no está restringido tooresources que se implementan en el grupo de recursos de Azure.</span><span class="sxs-lookup"><span data-stu-id="be28c-115">One advantage of this model is you're no longer constrained tooresources that are deployed in your Azure resource group.</span></span> 

### <a name="managed-apis"></a><span data-ttu-id="be28c-116">API administradas</span><span class="sxs-lookup"><span data-stu-id="be28c-116">Managed APIs</span></span>

<span data-ttu-id="be28c-117">Algunas API se administran de forma automática, como Office 365, Salesforce, Twitter y FTP.</span><span class="sxs-lookup"><span data-stu-id="be28c-117">Microsoft manages some APIs on your behalf, such as Office 365, Salesforce, Twitter, and FTP.</span></span> <span data-ttu-id="be28c-118">Puede usar algunas API administradas tal y como están, como en el caso de Bing Translate, mientras que otras requieren configuración.</span><span class="sxs-lookup"><span data-stu-id="be28c-118">You can use some managed APIs as-is, such as Bing Translate, while others require configuration.</span></span> <span data-ttu-id="be28c-119">Esta configuración se conoce como *conexión*.</span><span class="sxs-lookup"><span data-stu-id="be28c-119">This configuration is called a *connection*.</span></span>

<span data-ttu-id="be28c-120">Por ejemplo, cuando use Office 365, debe crear una conexión que contenga el token de inicio de sesión de Office 365.</span><span class="sxs-lookup"><span data-stu-id="be28c-120">For example, when you use Office 365, you must create a connection that contains your Office 365 sign-in token.</span></span> <span data-ttu-id="be28c-121">Este token de forma segura se almacenan y se actualiza para que la aplicación lógica siempre puede llamar a Hola API de Office 365.</span><span class="sxs-lookup"><span data-stu-id="be28c-121">This token is securely stored and refreshed so that your logic app can always call hello Office 365 API.</span></span> <span data-ttu-id="be28c-122">O bien, si desea tooconnect tooyour FTP o SQL server, debe crear una conexión que tiene la cadena de conexión de Hola.</span><span class="sxs-lookup"><span data-stu-id="be28c-122">Alternatively, if you want tooconnect tooyour SQL or FTP server, you must create a connection that has hello connection string.</span></span> 

<span data-ttu-id="be28c-123">En esta definición, estas acciones se denominan `APIConnection`.</span><span class="sxs-lookup"><span data-stu-id="be28c-123">In this definition, these actions are called `APIConnection`.</span></span> <span data-ttu-id="be28c-124">Este es un ejemplo de una conexión que llama a Office 365 toosend un correo electrónico:</span><span class="sxs-lookup"><span data-stu-id="be28c-124">Here is an example of a connection that calls Office 365 toosend an email:</span></span>

```
{
    "actions": {
        "Send_Email": {
            "type": "ApiConnection",
            "inputs": {
                "host": {
                    "api": {
                        "runtimeUrl": "https://msmanaged-na.azure-apim.net/apim/office365"
                    },
                    "connection": {
                        "name": "@parameters('$connections')['shared_office365']['connectionId']"
                    }
                },
                "method": "post",
                "body": {
                    "Subject": "Reminder",
                    "Body": "Don't forget!",
                    "To": "me@contoso.com"
                },
                "path": "/Mail"
            }
        }
    }
}
```

<span data-ttu-id="be28c-125">Hola `host` objeto es parte de las entradas que es único tooAPI conexiones y contiene elementos de fila: `api` y `connection`.</span><span class="sxs-lookup"><span data-stu-id="be28c-125">hello `host` object is portion of inputs that is unique tooAPI connections, and contains tow parts: `api` and `connection`.</span></span>

<span data-ttu-id="be28c-126">Hola `api` tiene hello en tiempo de ejecución se hospeda la dirección URL de donde que administra la API.</span><span class="sxs-lookup"><span data-stu-id="be28c-126">hello `api` has hello runtime URL of where that managed API is hosted.</span></span> <span data-ttu-id="be28c-127">Puede ver todos los Hola disponibles API administradas mediante una llamada a `GET https://management.azure.com/subscriptions/{subid}/providers/Microsoft.Web/managedApis/?api-version=2015-08-01-preview`.</span><span class="sxs-lookup"><span data-stu-id="be28c-127">You can see all hello available managed APIs by calling `GET https://management.azure.com/subscriptions/{subid}/providers/Microsoft.Web/managedApis/?api-version=2015-08-01-preview`.</span></span>

<span data-ttu-id="be28c-128">Cuando se usa una API, Hola API que no tenga o cualquier *parámetros de conexión* definido.</span><span class="sxs-lookup"><span data-stu-id="be28c-128">When you use an API, hello API might or might not have any *connection parameters* defined.</span></span> <span data-ttu-id="be28c-129">Si no Hola API, no *conexión* es necesario.</span><span class="sxs-lookup"><span data-stu-id="be28c-129">If hello API doesn't, no *connection* is required.</span></span> <span data-ttu-id="be28c-130">Si no Hola API, debe crear una conexión.</span><span class="sxs-lookup"><span data-stu-id="be28c-130">If hello API does, you must create a connection.</span></span> <span data-ttu-id="be28c-131">conexión de Hello creado tiene nombre hello que elija.</span><span class="sxs-lookup"><span data-stu-id="be28c-131">hello created connection has hello name that you choose.</span></span> <span data-ttu-id="be28c-132">A continuación, hacer referencia a nombre de Hola Hola `connection` objeto dentro de hello `host` objeto.</span><span class="sxs-lookup"><span data-stu-id="be28c-132">You then reference hello name in hello `connection` object inside hello `host` object.</span></span> <span data-ttu-id="be28c-133">toocreate una conexión en un grupo de recursos, llamada:</span><span class="sxs-lookup"><span data-stu-id="be28c-133">toocreate a connection in a resource group, call:</span></span>

```
PUT https://management.azure.com/subscriptions/{subid}/resourceGroups/{rgname}/providers/Microsoft.Web/connections/{name}?api-version=2015-08-01-preview
```

<span data-ttu-id="be28c-134">Con hello siguiente cuerpo:</span><span class="sxs-lookup"><span data-stu-id="be28c-134">With hello following body:</span></span>

```
{
  "properties": {
    "api": {
      "id": "/subscriptions/{subid}/providers/Microsoft.Web/managedApis/azureblob"
    },
    "parameterValues": {
        "accountName": "{hello name of hello storage account -- hello set of parameters is different for each API}"
    }
  },
  "location": "{Logic app's location}"
}
```

### <a name="deploy-managed-apis-in-an-azure-resource-manager-template"></a><span data-ttu-id="be28c-135">Implementación de API administradas en una plantilla de Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="be28c-135">Deploy managed APIs in an Azure Resource Manager template</span></span>

<span data-ttu-id="be28c-136">Puede crear una aplicación completa en una plantilla de Azure Resource Manager siempre que no se requiera inicio de sesión interactivo.</span><span class="sxs-lookup"><span data-stu-id="be28c-136">You can create a full application in an Azure Resource Manager template as long as interactive sign-in isn't required.</span></span>
<span data-ttu-id="be28c-137">Si el inicio de sesión es necesario, puede configurar todo el contenido con plantilla de Azure Resource Manager hello, pero tiene toovisit hello tooauthorize portal Hola conexiones.</span><span class="sxs-lookup"><span data-stu-id="be28c-137">If sign-in is required, you can set up everything with hello Azure Resource Manager template, but you still have toovisit hello portal tooauthorize hello connections.</span></span> 

```
    "resources": [{
        "apiVersion": "2015-08-01-preview",
        "name": "azureblob",
        "type": "Microsoft.Web/connections",
        "location": "[resourceGroup().location]",
        "properties": {
            "api": {
                "id": "[concat(subscription().id,'/providers/Microsoft.Web/locations/westus/managedApis/azureblob')]"
            },
            "parameterValues": {
                "accountName": "[parameters('storageAccountName')]",
                "accessKey": "[parameters('storageAccountKey')]"
            }
        }
    }, {
        "type": "Microsoft.Logic/workflows",
        "apiVersion": "2015-08-01-preview",
        "name": "[parameters('logicAppName')]",
        "location": "[resourceGroup().location]",
        "dependsOn": ["[resourceId('Microsoft.Web/connections', 'azureblob')]"
        ],
        "properties": {
            "sku": {
                "name": "[parameters('sku')]",
                "plan": {
                    "id": "[concat(resourceGroup().id, '/providers/Microsoft.Web/serverfarms/',parameters('svcPlanName'))]"
                }
            },
            "definition": {
                "$schema": "https://schema.management.azure.com/providers/Microsoft.Logic/schemas/2015-08-01-preview/workflowdefinition.json#",
                "actions": {
                    "Create_file": {
                        "type": "apiconnection",
                        "inputs": {
                            "host": {
                                "api": {
                                    "runtimeUrl": "https://logic-apis-westus.azure-apim.net/apim/azureblob"
                                },
                                "connection": {
                                    "name": "@parameters('$connections')['azureblob']['connectionId']"
                                }
                            },
                            "method": "post",
                            "queries": {
                                "folderPath": "[concat('/', parameters('containerName'))]",
                                "name": "helloworld.txt"
                            },
                            "body": "@decodeDataUri('data:, Hello+world!')",
                            "path": "/datasets/default/files"
                        },
                        "conditions": []
                    }
                },
                "contentVersion": "1.0.0.0",
                "outputs": {},
                "parameters": {
                    "$connections": {
                        "defaultValue": {},
                        "type": "Object"
                    }
                },
                "triggers": {
                    "recurrence": {
                        "type": "Recurrence",
                        "recurrence": {
                            "frequency": "Day",
                            "interval": 1
                        }
                    }
                }
            },
            "parameters": {
                "$connections": {
                    "value": {
                        "azureblob": {
                            "connectionId": "[concat(resourceGroup().id,'/providers/Microsoft.Web/connections/azureblob')]",
                            "connectionName": "azureblob",
                            "id": "[concat(subscription().id,'/providers/Microsoft.Web/locations/westus/managedApis/azureblob')]"
                        }

                    }
                }
            }
        }
    }]
```

<span data-ttu-id="be28c-138">Puede ver en este ejemplo que las conexiones de hello son simplemente los recursos a los que viven en el grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="be28c-138">You can see in this example that hello connections are just resources that live in your resource group.</span></span> <span data-ttu-id="be28c-139">Hacen referencia a tooyou disponible de API de hello administrado en su suscripción.</span><span class="sxs-lookup"><span data-stu-id="be28c-139">They reference hello managed APIs available tooyou in your subscription.</span></span>

### <a name="your-custom-web-apis"></a><span data-ttu-id="be28c-140">Sus API web personalizadas</span><span class="sxs-lookup"><span data-stu-id="be28c-140">Your custom Web APIs</span></span>

<span data-ttu-id="be28c-141">Si usa su propia API, las no administrada por Microsoft, usar integrada de hello **HTTP** acción toocall ellos.</span><span class="sxs-lookup"><span data-stu-id="be28c-141">If you use your own APIs, not Microsoft-managed ones, use hello built-in **HTTP** action toocall them.</span></span> <span data-ttu-id="be28c-142">Para tener una experiencia ideal, debe exponer un punto de conexión de Swagger para la API.</span><span class="sxs-lookup"><span data-stu-id="be28c-142">For an ideal experience, you should expose a Swagger endpoint for your API.</span></span> <span data-ttu-id="be28c-143">Este extremo permite entradas de hello Diseñador de la aplicación lógica toorender hello y salidas de la API.</span><span class="sxs-lookup"><span data-stu-id="be28c-143">This endpoint enables hello Logic App Designer toorender hello inputs and outputs for your API.</span></span> <span data-ttu-id="be28c-144">Sin Swagger, Diseñador de hello solo puede mostrar hello entradas y salidas como objetos JSON opacos.</span><span class="sxs-lookup"><span data-stu-id="be28c-144">Without Swagger, hello designer can only show hello inputs and outputs as opaque JSON objects.</span></span>

<span data-ttu-id="be28c-145">Aquí es un Hola de ejemplo que muestra nueva `metadata.apiDefinitionUrl` propiedad:</span><span class="sxs-lookup"><span data-stu-id="be28c-145">Here is an example showing hello new `metadata.apiDefinitionUrl` property:</span></span>

```
{
   "actions": {
        "mycustomAPI": {
            "type": "http",
            "metadata": {
              "apiDefinitionUrl": "https://mysite.azurewebsites.net/api/apidef/"  
            },
            "inputs": {
                "uri": "https://mysite.azurewebsites.net/api/getsomedata",
                "method": "GET"
            }
        }
    }
}
```

<span data-ttu-id="be28c-146">Si hospeda su API Web en el servicio de aplicaciones de Azure, la API Web aparece automáticamente en lista de Hola de acciones disponibles en el Diseñador de Hola.</span><span class="sxs-lookup"><span data-stu-id="be28c-146">If you host your Web API on Azure App Service, your Web API automatically appears in hello list of actions available in hello designer.</span></span> <span data-ttu-id="be28c-147">Si no es así, tienen toopaste en dirección URL de hello directamente.</span><span class="sxs-lookup"><span data-stu-id="be28c-147">If not, you have toopaste in hello URL directly.</span></span> <span data-ttu-id="be28c-148">extremo de Swagger de Hello debe ser toobe no autenticada se puede usar en hello Diseñador de la lógica de aplicaciones, aunque puede proteger Hola propia API con los métodos que admite Swagger.</span><span class="sxs-lookup"><span data-stu-id="be28c-148">hello Swagger endpoint must be unauthenticated toobe usable in hello Logic App Designer, although you can secure hello API itself with whatever methods that Swagger supports.</span></span>

### <a name="call-deployed-api-apps-with-2015-08-01-preview"></a><span data-ttu-id="be28c-149">Llamada a las aplicaciones de API implementadas con 2015-08-01-preview</span><span class="sxs-lookup"><span data-stu-id="be28c-149">Call deployed API apps with 2015-08-01-preview</span></span>

<span data-ttu-id="be28c-150">Si previamente ha implementado una API App, puede llamar a la aplicación hello con hello **HTTP** acción.</span><span class="sxs-lookup"><span data-stu-id="be28c-150">If you previously deployed an API App, you can call hello app with hello **HTTP** action.</span></span>

<span data-ttu-id="be28c-151">Por ejemplo, si utiliza archivos de toolist de Dropbox, su **2014-12-01-versión preliminar** definición de la versión de esquema puede tener algo parecido:</span><span class="sxs-lookup"><span data-stu-id="be28c-151">For example, if you use Dropbox toolist files, your **2014-12-01-preview** schema version definition might have something like:</span></span>

```
{
    "$schema": "https://schema.management.azure.com/providers/Microsoft.Logic/schemas/2014-12-01-preview/workflowdefinition.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "/subscriptions/423db32d-...-b59f14c962f1/resourcegroups/avdemo/providers/Microsoft.AppService/apiapps/dropboxconnector/token": {
            "defaultValue": "eyJ0eX...wCn90",
            "type": "String",
            "metadata": {
                "token": {
                    "name": "/subscriptions/423db32d-...-b59f14c962f1/resourcegroups/avdemo/providers/Microsoft.AppService/apiapps/dropboxconnector/token"
                }
            }
        }
    },
    "actions": {
        "dropboxconnector": {
            "type": "ApiApp",
            "inputs": {
                "apiVersion": "2015-01-14",
                "host": {
                    "id": "/subscriptions/423db32d-...-b59f14c962f1/resourcegroups/avdemo/providers/Microsoft.AppService/apiapps/dropboxconnector",
                    "gateway": "https://avdemo.azurewebsites.net"
                },
                "operation": "ListFiles",
                "parameters": {
                    "FolderPath": "/myfolder"
                },
                "authentication": {
                    "type": "Raw",
                    "scheme": "Zumo",
                    "parameter": "@parameters('/subscriptions/423db32d-...-b59f14c962f1/resourcegroups/avdemo/providers/Microsoft.AppService/apiapps/dropboxconnector/token')"
                }
            }
        }
    }
}
```

<span data-ttu-id="be28c-152">Puede construir acción HTTP equivalente de hello mostrado en este ejemplo, mientras permanece sin modificar sección de parámetros de Hola de hello definición de la aplicación lógica:</span><span class="sxs-lookup"><span data-stu-id="be28c-152">You can construct hello equivalent HTTP action like this example, while hello parameters section of hello Logic app definition remains unchanged:</span></span>

```
{
    "actions": {
        "dropboxconnector": {
            "type": "Http",
            "metadata": {
              "apiDefinitionUrl": "https://avdemo.azurewebsites.net/api/service/apidef/dropboxconnector/?api-version=2015-01-14&format=swagger-2.0-standard"  
            },
            "inputs": {
                "uri": "https://avdemo.azurewebsites.net/api/service/invoke/dropboxconnector/ListFiles?api-version=2015-01-14",
                "method": "POST",
                "body": {
                    "FolderPath": "/myfolder"
                },
                "authentication": {
                    "type": "Raw",
                    "scheme": "Zumo",
                    "parameter": "@parameters('/subscriptions/423db32d-...-b59f14c962f1/resourcegroups/avdemo/providers/Microsoft.AppService/apiapps/dropboxconnector/token')"
                }
            }
        }
    }
}
```

<span data-ttu-id="be28c-153">Vamos a recorrer estas propiedades una a una:</span><span class="sxs-lookup"><span data-stu-id="be28c-153">Walking through these properties one-by-one:</span></span>

| <span data-ttu-id="be28c-154">Propiedad de acción</span><span class="sxs-lookup"><span data-stu-id="be28c-154">Action property</span></span> | <span data-ttu-id="be28c-155">Descripción</span><span class="sxs-lookup"><span data-stu-id="be28c-155">Description</span></span> |
| --- | --- |
| `type` |<span data-ttu-id="be28c-156">`Http` en lugar de `APIapp`</span><span class="sxs-lookup"><span data-stu-id="be28c-156">`Http` instead of `APIapp`</span></span> |
| `metadata.apiDefinitionUrl` |<span data-ttu-id="be28c-157">toouse esta acción en hello Diseñador de la lógica de aplicaciones, incluir el extremo de metadatos de hello, que se construye a partir:`{api app host.gateway}/api/service/apidef/{last segment of hello api app host.id}/?api-version=2015-01-14&format=swagger-2.0-standard`</span><span class="sxs-lookup"><span data-stu-id="be28c-157">toouse this action in hello Logic App Designer, include hello metadata endpoint, which is constructed from: `{api app host.gateway}/api/service/apidef/{last segment of hello api app host.id}/?api-version=2015-01-14&format=swagger-2.0-standard`</span></span> |
| `inputs.uri` |<span data-ttu-id="be28c-158">Se construye a partir de: `{api app host.gateway}/api/service/invoke/{last segment of hello api app host.id}/{api app operation}?api-version=2015-01-14`</span><span class="sxs-lookup"><span data-stu-id="be28c-158">Constructed from: `{api app host.gateway}/api/service/invoke/{last segment of hello api app host.id}/{api app operation}?api-version=2015-01-14`</span></span> |
| `inputs.method` |<span data-ttu-id="be28c-159">Siempre `POST`</span><span class="sxs-lookup"><span data-stu-id="be28c-159">Always `POST`</span></span> |
| `inputs.body` |<span data-ttu-id="be28c-160">Parámetros de la aplicación idéntico toohello API</span><span class="sxs-lookup"><span data-stu-id="be28c-160">Identical toohello API App parameters</span></span> |
| `inputs.authentication` |<span data-ttu-id="be28c-161">Toohello idéntico autenticación API App</span><span class="sxs-lookup"><span data-stu-id="be28c-161">Identical toohello API App authentication</span></span> |

<span data-ttu-id="be28c-162">Este enfoque debería funcionar para todas las acciones de aplicación de API.</span><span class="sxs-lookup"><span data-stu-id="be28c-162">This approach should work for all API App actions.</span></span> <span data-ttu-id="be28c-163">Sin embargo, recuerde que estas aplicaciones de API anteriores ya no se admiten.</span><span class="sxs-lookup"><span data-stu-id="be28c-163">However, remember that these previous API Apps are no longer supported.</span></span> <span data-ttu-id="be28c-164">Por lo que debe mover tooone de hello dos otras opciones anteriores, una API administrada u hospeda su API Web personalizado.</span><span class="sxs-lookup"><span data-stu-id="be28c-164">So you should move tooone of hello two other previous options, a managed API or hosting your custom Web API.</span></span>

<a name="foreach"></a>
## <a name="renamed-repeat-tooforeach"></a><span data-ttu-id="be28c-165">Cambiar el nombre 'repeat' too'foreach'</span><span class="sxs-lookup"><span data-stu-id="be28c-165">Renamed 'repeat' too'foreach'</span></span>

<span data-ttu-id="be28c-166">Para la versión de esquema anterior hello, hemos recibido la máxima cantidad de información del cliente que **repita** dio lugar a confusión y no captura correctamente que **repita** era un bucle for-each.</span><span class="sxs-lookup"><span data-stu-id="be28c-166">For hello previous schema version, we received much customer feedback that **Repeat** was confusing and didn't properly capture that **Repeat** was really a for-each loop.</span></span> <span data-ttu-id="be28c-167">Como resultado, hemos hemos cambiado el nombre `repeat` demasiado`foreach`.</span><span class="sxs-lookup"><span data-stu-id="be28c-167">As a result, we have renamed `repeat` too`foreach`.</span></span> <span data-ttu-id="be28c-168">Por ejemplo, anteriormente escribiría:</span><span class="sxs-lookup"><span data-stu-id="be28c-168">For example, previously you would write:</span></span>

```
{
    "actions": {
        "pingBing": {
            "type": "Http",
            "repeat": "@range(0,2)",
            "inputs": {
                "method": "GET",
                "uri": "https://www.bing.com/search?q=@{repeatItem()}"
            }
        }
    }
}
```

<span data-ttu-id="be28c-169">Ahora debe escribir:</span><span class="sxs-lookup"><span data-stu-id="be28c-169">Now you would write:</span></span>

```
{
    "actions": {
        "pingBing": {
            "type": "Http",
            "foreach": "@range(0,2)",
            "inputs": {
                "method": "GET",
                "uri": "https://www.bing.com/search?q=@{item()}"
            }
        }
    }
}
```

<span data-ttu-id="be28c-170">Hola función `@repeatItem()` se elemento actual de hello tooreference usadas previamente que se recorre en iteración.</span><span class="sxs-lookup"><span data-stu-id="be28c-170">hello function `@repeatItem()` was previously used tooreference hello current item being iterated over.</span></span> <span data-ttu-id="be28c-171">Esta función se reducen ahora demasiado`@item()`.</span><span class="sxs-lookup"><span data-stu-id="be28c-171">This function is now simplified too`@item()`.</span></span> 

### <a name="reference-outputs-from-foreach"></a><span data-ttu-id="be28c-172">Salidas de referencia de "foreach"</span><span class="sxs-lookup"><span data-stu-id="be28c-172">Reference outputs from 'foreach'</span></span>

<span data-ttu-id="be28c-173">Para simplificar, Hola genera de `foreach` acciones no se ajustan en un objeto denominado `repeatItems`.</span><span class="sxs-lookup"><span data-stu-id="be28c-173">For simplification, hello outputs from `foreach` actions are not wrapped in an object called `repeatItems`.</span></span> <span data-ttu-id="be28c-174">Mientras genera Hola de hello anterior `repeat` ejemplo fuera:</span><span class="sxs-lookup"><span data-stu-id="be28c-174">While hello outputs from hello previous `repeat` example were:</span></span>

```
{
    "repeatItems": [
        {
            "name": "pingBing",
            "inputs": {
                "uri": "https://www.bing.com/search?q=0",
                "method": "GET"
            },
            "outputs": {
                "headers": { },
                "body": "<!DOCTYPE html><html lang=\"en\" xml:lang=\"en\" xmlns=\"http://www.w3.org/1999/xhtml\" xmlns:Web=\"http://schemas.live.com/Web/\">...</html>"
            }
            "status": "Succeeded"
        }
    ]
}
```

<span data-ttu-id="be28c-175">Ahora, estas salidas son:</span><span class="sxs-lookup"><span data-stu-id="be28c-175">Now these outputs are:</span></span>

```
[
    {
        "name": "pingBing",
        "inputs": {
            "uri": "https://www.bing.com/search?q=0",
            "method": "GET"
        },
        "outputs": {
            "headers": { },
            "body": "<!DOCTYPE html><html lang=\"en\" xml:lang=\"en\" xmlns=\"http://www.w3.org/1999/xhtml\" xmlns:Web=\"http://schemas.live.com/Web/\">...</html>"
        }
        "status": "Succeeded"
    }
]
```

<span data-ttu-id="be28c-176">Anteriormente, tooget toohello cuerpo de acción de hello al hacer referencia a estas salidas:</span><span class="sxs-lookup"><span data-stu-id="be28c-176">Previously, tooget toohello body of hello action when referencing these outputs:</span></span>

```
{
    "actions": {
        "secondAction": {
            "type": "Http",
            "repeat": "@outputs('pingBing').repeatItems",
            "inputs": {
                "method": "POST",
                "uri": "http://www.example.com",
                "body": "@repeatItem().outputs.body"
            }
        }
    }
}
```

<span data-ttu-id="be28c-177">Ahora puede hacer esto en su lugar:</span><span class="sxs-lookup"><span data-stu-id="be28c-177">Now you can do instead:</span></span>

```
{
    "actions": {
        "secondAction": {
            "type": "Http",
            "foreach": "@outputs('pingBing')",
            "inputs": {
                "method": "POST",
                "uri": "http://www.example.com",
                "body": "@item().outputs.body"
            }
        }
    }
}
```

<span data-ttu-id="be28c-178">Con estos cambios, Hola funciones `@repeatItem()`, `@repeatBody()`, y `@repeatOutputs()` se quitan.</span><span class="sxs-lookup"><span data-stu-id="be28c-178">With these changes, hello functions `@repeatItem()`, `@repeatBody()`, and `@repeatOutputs()` are removed.</span></span>

<a name="http-listener"></a>
## <a name="native-http-listener"></a><span data-ttu-id="be28c-179">Agente de escucha HTTP nativo</span><span class="sxs-lookup"><span data-stu-id="be28c-179">Native HTTP listener</span></span>

<span data-ttu-id="be28c-180">Hola capacidades ahora están integradas en un agente de escucha de HTTP.</span><span class="sxs-lookup"><span data-stu-id="be28c-180">hello HTTP Listener capabilities are now built in.</span></span> <span data-ttu-id="be28c-181">Por lo que ya no necesita toodeploy una aplicación de API del agente de escucha de HTTP.</span><span class="sxs-lookup"><span data-stu-id="be28c-181">So you no longer need toodeploy an HTTP Listener API App.</span></span> <span data-ttu-id="be28c-182">Vea [Hola a todos los detalles acerca de cómo toomake su aquí invocable del punto de conexión de lógica aplicación](../logic-apps/logic-apps-http-endpoint.md).</span><span class="sxs-lookup"><span data-stu-id="be28c-182">See [hello full details for how toomake your Logic app endpoint callable here](../logic-apps/logic-apps-http-endpoint.md).</span></span> 

<span data-ttu-id="be28c-183">Con estos cambios, eliminamos hello `@accessKeys()` función, que se sustituye por hello `@listCallbackURL()` función para obtener el punto de conexión de hello cuando sea necesario.</span><span class="sxs-lookup"><span data-stu-id="be28c-183">With these changes, we removed hello `@accessKeys()` function, which we replaced with hello `@listCallbackURL()` function for getting hello endpoint when necessary.</span></span> <span data-ttu-id="be28c-184">Además, ahora debe definir al menos un desencadenador en la aplicación lógica.</span><span class="sxs-lookup"><span data-stu-id="be28c-184">Also, you must now define at least one trigger in your logic app.</span></span> <span data-ttu-id="be28c-185">Si desea demasiado`/run` Hola de flujo de trabajo, debe tener uno de estos desencadenadores: `manual`, `apiConnectionWebhook`, o `httpWebhook`.</span><span class="sxs-lookup"><span data-stu-id="be28c-185">If you want too`/run` hello workflow, you must have one of these triggers: `manual`, `apiConnectionWebhook`, or `httpWebhook`.</span></span>

<a name="child-workflows"></a>
## <a name="call-child-workflows"></a><span data-ttu-id="be28c-186">Llamada a flujos de trabajo secundarios</span><span class="sxs-lookup"><span data-stu-id="be28c-186">Call child workflows</span></span>

<span data-ttu-id="be28c-187">Anteriormente, al llamar a los flujos de trabajo secundarios requería va toohello flujo de trabajo, obtener token de acceso de Hola y pegado de token de hello en la definición de aplicación lógica de hello en el que desea toocall ese flujo de trabajo secundario.</span><span class="sxs-lookup"><span data-stu-id="be28c-187">Previously, calling child workflows required going toohello workflow, getting hello access token, and pasting hello token in hello logic app definition where you want toocall that child workflow.</span></span> <span data-ttu-id="be28c-188">Con el nuevo esquema de hello, motor genera automáticamente una SAS en tiempo de ejecución para las aplicaciones lógicas de Hola Hola flujo de trabajo secundario por lo que no haya demasiado pegar los secretos en la definición de Hola.</span><span class="sxs-lookup"><span data-stu-id="be28c-188">With hello new schema, hello Logic Apps engine automatically generates a SAS at runtime for hello child workflow so you don't have too paste any secrets into hello definition.</span></span> <span data-ttu-id="be28c-189">Aquí tiene un ejemplo:</span><span class="sxs-lookup"><span data-stu-id="be28c-189">Here is an example:</span></span>

```
"mynestedwf": {
    "type": "workflow",
    "inputs": {
        "host": {
            "id": "/subscriptions/xxxxyyyyzzz/resourceGroups/rg001/providers/Microsoft.Logic/mywf001",
            "triggerName": "myendpointtrigger"
        },
        "queries": {
            "extrafield": "specialValue"
        },
        "headers": {
            "x-ms-date": "@utcnow()",
            "Content-type": "application/json"
        },
        "body": {
            "contentFieldOne": "value100",
            "anotherField": 10.001
        }
    },
    "conditions": []
}
```

<span data-ttu-id="be28c-190">Una segunda mejora es que le estamos ofreciendo a secundarios Hola solicitud entrante de toohello de acceso completo de los flujos de trabajo.</span><span class="sxs-lookup"><span data-stu-id="be28c-190">A second improvement is we are giving hello child workflows full access toohello incoming request.</span></span> <span data-ttu-id="be28c-191">Esto significa que puede pasar parámetros en hello *consultas* sección y en hello *encabezados* objeto y que se puede definir completamente Hola cuerpo completo.</span><span class="sxs-lookup"><span data-stu-id="be28c-191">That means that you can pass parameters in hello *queries* section and in hello *headers* object and that you can fully define hello entire body.</span></span>

<span data-ttu-id="be28c-192">Por último, hay flujo de trabajo de cambios necesarios toohello secundario.</span><span class="sxs-lookup"><span data-stu-id="be28c-192">Finally, there are required changes toohello child workflow.</span></span> <span data-ttu-id="be28c-193">Ahora mientras previamente podría llamar directamente un flujo de trabajo secundario, debe definir un extremo de desencadenador con el flujo de trabajo de Hola para hello primario toocall.</span><span class="sxs-lookup"><span data-stu-id="be28c-193">While you could previously call a child workflow directly, now you must define a trigger endpoint in hello workflow for hello parent toocall.</span></span> <span data-ttu-id="be28c-194">Por lo general, debe agregar un desencadenador que tiene `manual` escriba y, a continuación, usar ese desencadenador en definición de hello primario.</span><span class="sxs-lookup"><span data-stu-id="be28c-194">Generally, you would add a trigger that has `manual` type, and then use that trigger in hello parent definition.</span></span> <span data-ttu-id="be28c-195">Hola Nota `host` propiedad específicamente tiene un `triggerName` porque siempre debe especificar qué desencadenador que se está invocando.</span><span class="sxs-lookup"><span data-stu-id="be28c-195">Note hello `host` property specifically has a `triggerName` because you must always specify which trigger you are invoking.</span></span>

## <a name="other-changes"></a><span data-ttu-id="be28c-196">Otros cambios</span><span class="sxs-lookup"><span data-stu-id="be28c-196">Other changes</span></span>

### <a name="new-queries-property"></a><span data-ttu-id="be28c-197">Nueva propiedad "queries"</span><span class="sxs-lookup"><span data-stu-id="be28c-197">New 'queries' property</span></span>

<span data-ttu-id="be28c-198">Todos los tipos de acción admiten ahora una nueva entrada llamada `queries`.</span><span class="sxs-lookup"><span data-stu-id="be28c-198">All action types now support a new input called `queries`.</span></span> <span data-ttu-id="be28c-199">Esta entrada puede ser un objeto estructurado, en lugar de tener la cadena de hello tooassemble a mano.</span><span class="sxs-lookup"><span data-stu-id="be28c-199">This input can be a structured object, rather than you having tooassemble hello string by hand.</span></span>

### <a name="renamed-parse-function-toojson"></a><span data-ttu-id="be28c-200">Cambiar el nombre 'parse()' función too'json()'</span><span class="sxs-lookup"><span data-stu-id="be28c-200">Renamed 'parse()' function too'json()'</span></span>

<span data-ttu-id="be28c-201">Vamos a agregar tipos de contenido más pronto, por lo que hemos cambiado el nombre hello `parse()` función demasiado`json()`.</span><span class="sxs-lookup"><span data-stu-id="be28c-201">We are adding more content types soon, so we renamed hello `parse()` function too`json()`.</span></span>

## <a name="coming-soon-enterprise-integration-apis"></a><span data-ttu-id="be28c-202">Próximamente: API de Enterprise Integration</span><span class="sxs-lookup"><span data-stu-id="be28c-202">Coming soon: Enterprise Integration APIs</span></span>

<span data-ttu-id="be28c-203">No tenemos versiones administradas todavía de hello las API de integración de Enterprise, como AS2.</span><span class="sxs-lookup"><span data-stu-id="be28c-203">We don't have managed versions yet of hello Enterprise Integration APIs, like AS2.</span></span> <span data-ttu-id="be28c-204">Mientras tanto, puede usar su APIs BizTalk implementada existente a través de hello acción HTTP.</span><span class="sxs-lookup"><span data-stu-id="be28c-204">Meanwhile, you can use your existing deployed BizTalk APIs through hello HTTP action.</span></span> <span data-ttu-id="be28c-205">Para obtener más información, vea "Usar las aplicaciones ya implementadas de API" Hola [plan de integración](http://www.zdnet.com/article/microsoft-outlines-its-cloud-and-server-integration-roadmap-for-2016/).</span><span class="sxs-lookup"><span data-stu-id="be28c-205">For details, see "Using your already deployed API apps" in hello [integration roadmap](http://www.zdnet.com/article/microsoft-outlines-its-cloud-and-server-integration-roadmap-for-2016/).</span></span> 
