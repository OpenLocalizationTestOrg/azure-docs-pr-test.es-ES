---
title: "Actualizaciones del esquema de versión preliminar del 1 de agosto de 2015: Azure Logic Apps | Microsoft Docs"
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
ms.openlocfilehash: 35d7a56d5607dcc18a4407c65b92962d3d0dcd1d
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="schema-updates-for-azure-logic-apps---august-1-2015-preview"></a><span data-ttu-id="74233-103">Actualizaciones de esquema para Azure Logic Apps de la versión preliminar del 1 de agosto de 2015</span><span class="sxs-lookup"><span data-stu-id="74233-103">Schema updates for Azure Logic Apps - August 1, 2015 preview</span></span>

<span data-ttu-id="74233-104">Esta nueva versión de esquema y API de Azure Logic Apps incluye importantes mejoras que aportan una mayor confiabilidad a las aplicaciones lógicas y facilitan su uso:</span><span class="sxs-lookup"><span data-stu-id="74233-104">This new schema and API version for Azure Logic Apps includes key improvements that make logic apps more reliable and easier to use:</span></span>

*   <span data-ttu-id="74233-105">El tipo de acción **APIApp** se actualizó a un nuevo tipo de acción [**APIConnection**](#api-connections).</span><span class="sxs-lookup"><span data-stu-id="74233-105">The **APIApp** action type is updated to a new [**APIConnection**](#api-connections) action type.</span></span>
*   <span data-ttu-id="74233-106">Cambio de nombre de **Repeat** a [**Foreach**](#foreach).</span><span class="sxs-lookup"><span data-stu-id="74233-106">**Repeat** is renamed to [**Foreach**](#foreach).</span></span>
*   <span data-ttu-id="74233-107">La aplicación de API [**Agente de escucha HTTP**](#http-listener) ya no es necesaria.</span><span class="sxs-lookup"><span data-stu-id="74233-107">The [**HTTP Listener** API App](#http-listener) is no longer required.</span></span>
*   <span data-ttu-id="74233-108">En la llamada a los flujos de trabajo secundarios se usa un [nuevo esquema](#child-workflows).</span><span class="sxs-lookup"><span data-stu-id="74233-108">Calling child workflows uses a [new schema](#child-workflows).</span></span>

<a name="api-connections"></a>
## <a name="move-to-api-connections"></a><span data-ttu-id="74233-109">Paso a las conexiones de API</span><span class="sxs-lookup"><span data-stu-id="74233-109">Move to API connections</span></span>

<span data-ttu-id="74233-110">El cambio más importante es que ya no es necesario implementar aplicaciones de API en la suscripción de Azure para poder usar las API.</span><span class="sxs-lookup"><span data-stu-id="74233-110">The biggest change is that you no longer have to deploy API Apps into your Azure subscription so you can use APIs.</span></span> <span data-ttu-id="74233-111">Estas son las formas en que puede usar las API:</span><span class="sxs-lookup"><span data-stu-id="74233-111">Here are the ways that you can use APIs:</span></span>

* <span data-ttu-id="74233-112">API administradas</span><span class="sxs-lookup"><span data-stu-id="74233-112">Managed APIs</span></span>
* <span data-ttu-id="74233-113">Sus API web personalizadas</span><span class="sxs-lookup"><span data-stu-id="74233-113">Your custom Web APIs</span></span>

<span data-ttu-id="74233-114">Cada una se controla de forma algo distinta, ya que sus modelos de administración y hospedaje son diferentes.</span><span class="sxs-lookup"><span data-stu-id="74233-114">Each way is handled slightly differently because their management and hosting models are different.</span></span> <span data-ttu-id="74233-115">Una ventaja de este modelo es que ya no está limitado a los recursos que se implementan en el grupo de recursos de Azure.</span><span class="sxs-lookup"><span data-stu-id="74233-115">One advantage of this model is you're no longer constrained to resources that are deployed in your Azure resource group.</span></span> 

### <a name="managed-apis"></a><span data-ttu-id="74233-116">API administradas</span><span class="sxs-lookup"><span data-stu-id="74233-116">Managed APIs</span></span>

<span data-ttu-id="74233-117">Algunas API se administran de forma automática, como Office 365, Salesforce, Twitter y FTP.</span><span class="sxs-lookup"><span data-stu-id="74233-117">Microsoft manages some APIs on your behalf, such as Office 365, Salesforce, Twitter, and FTP.</span></span> <span data-ttu-id="74233-118">Puede usar algunas API administradas tal y como están, como en el caso de Bing Translate, mientras que otras requieren configuración.</span><span class="sxs-lookup"><span data-stu-id="74233-118">You can use some managed APIs as-is, such as Bing Translate, while others require configuration.</span></span> <span data-ttu-id="74233-119">Esta configuración se conoce como *conexión*.</span><span class="sxs-lookup"><span data-stu-id="74233-119">This configuration is called a *connection*.</span></span>

<span data-ttu-id="74233-120">Por ejemplo, cuando use Office 365, debe crear una conexión que contenga el token de inicio de sesión de Office 365.</span><span class="sxs-lookup"><span data-stu-id="74233-120">For example, when you use Office 365, you must create a connection that contains your Office 365 sign-in token.</span></span> <span data-ttu-id="74233-121">Este token se almacena y actualiza de forma segura para que la aplicación lógica pueda llamar siempre a la API de Office 365.</span><span class="sxs-lookup"><span data-stu-id="74233-121">This token is securely stored and refreshed so that your logic app can always call the Office 365 API.</span></span> <span data-ttu-id="74233-122">Como alternativa, si quiere conectarse a su servidor SQL o FTP, debe crear una conexión que tenga la cadena de conexión.</span><span class="sxs-lookup"><span data-stu-id="74233-122">Alternatively, if you want to connect to your SQL or FTP server, you must create a connection that has the connection string.</span></span> 

<span data-ttu-id="74233-123">En esta definición, estas acciones se denominan `APIConnection`.</span><span class="sxs-lookup"><span data-stu-id="74233-123">In this definition, these actions are called `APIConnection`.</span></span> <span data-ttu-id="74233-124">A continuación se muestra un ejemplo de una conexión que llama a Office 365 para enviar un correo electrónico:</span><span class="sxs-lookup"><span data-stu-id="74233-124">Here is an example of a connection that calls Office 365 to send an email:</span></span>

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

<span data-ttu-id="74233-125">El objeto `host` es una parte de las entradas que es exclusiva de las conexiones de API y contiene dos partes: `api` y `connection`.</span><span class="sxs-lookup"><span data-stu-id="74233-125">The `host` object is portion of inputs that is unique to API connections, and contains tow parts: `api` and `connection`.</span></span>

<span data-ttu-id="74233-126">La parte `api` contiene la URL de tiempo de ejecución del lugar donde se hospeda la API administrada.</span><span class="sxs-lookup"><span data-stu-id="74233-126">The `api` has the runtime URL of where that managed API is hosted.</span></span> <span data-ttu-id="74233-127">Puede ver todas las API administradas disponibles mediante una llamada a `GET https://management.azure.com/subscriptions/{subid}/providers/Microsoft.Web/managedApis/?api-version=2015-08-01-preview`.</span><span class="sxs-lookup"><span data-stu-id="74233-127">You can see all the available managed APIs by calling `GET https://management.azure.com/subscriptions/{subid}/providers/Microsoft.Web/managedApis/?api-version=2015-08-01-preview`.</span></span>

<span data-ttu-id="74233-128">Al usar una API, esta puede o no tener *parámetros de conexión* definidos.</span><span class="sxs-lookup"><span data-stu-id="74233-128">When you use an API, the API might or might not have any *connection parameters* defined.</span></span> <span data-ttu-id="74233-129">Si no los tiene, no se requiere ninguna *conexión*.</span><span class="sxs-lookup"><span data-stu-id="74233-129">If the API doesn't, no *connection* is required.</span></span> <span data-ttu-id="74233-130">Si los tienes, tiene que crear una conexión.</span><span class="sxs-lookup"><span data-stu-id="74233-130">If the API does, you must create a connection.</span></span> <span data-ttu-id="74233-131">La conexión creada tendrá el nombre que elija.</span><span class="sxs-lookup"><span data-stu-id="74233-131">The created connection has the name that you choose.</span></span> <span data-ttu-id="74233-132">Haga referencia al nombre del objeto `connection` dentro del objeto `host`.</span><span class="sxs-lookup"><span data-stu-id="74233-132">You then reference the name in the `connection` object inside the `host` object.</span></span> <span data-ttu-id="74233-133">Para crear una conexión en un grupo de recursos, llame a:</span><span class="sxs-lookup"><span data-stu-id="74233-133">To create a connection in a resource group, call:</span></span>

```
PUT https://management.azure.com/subscriptions/{subid}/resourceGroups/{rgname}/providers/Microsoft.Web/connections/{name}?api-version=2015-08-01-preview
```

<span data-ttu-id="74233-134">Con el siguiente cuerpo:</span><span class="sxs-lookup"><span data-stu-id="74233-134">With the following body:</span></span>

```
{
  "properties": {
    "api": {
      "id": "/subscriptions/{subid}/providers/Microsoft.Web/managedApis/azureblob"
    },
    "parameterValues": {
        "accountName": "{The name of the storage account -- the set of parameters is different for each API}"
    }
  },
  "location": "{Logic app's location}"
}
```

### <a name="deploy-managed-apis-in-an-azure-resource-manager-template"></a><span data-ttu-id="74233-135">Implementación de API administradas en una plantilla de Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="74233-135">Deploy managed APIs in an Azure Resource Manager template</span></span>

<span data-ttu-id="74233-136">Puede crear una aplicación completa en una plantilla de Azure Resource Manager siempre que no se requiera inicio de sesión interactivo.</span><span class="sxs-lookup"><span data-stu-id="74233-136">You can create a full application in an Azure Resource Manager template as long as interactive sign-in isn't required.</span></span>
<span data-ttu-id="74233-137">Si se requiere inicio de sesión, puede configurar todo con la plantilla de Azure Resource Manager, pero aun así tendrá que visitar el portal para autorizar las conexiones.</span><span class="sxs-lookup"><span data-stu-id="74233-137">If sign-in is required, you can set up everything with the Azure Resource Manager template, but you still have to visit the portal to authorize the connections.</span></span> 

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

<span data-ttu-id="74233-138">En este ejemplo puede ver que las conexiones son solo recursos que residen en su grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="74233-138">You can see in this example that the connections are just resources that live in your resource group.</span></span> <span data-ttu-id="74233-139">Haga referencia a las API administradas disponibles en su suscripción.</span><span class="sxs-lookup"><span data-stu-id="74233-139">They reference the managed APIs available to you in your subscription.</span></span>

### <a name="your-custom-web-apis"></a><span data-ttu-id="74233-140">Sus API web personalizadas</span><span class="sxs-lookup"><span data-stu-id="74233-140">Your custom Web APIs</span></span>

<span data-ttu-id="74233-141">Si usa sus propias API, las no administradas por Microsoft, use la acción integrada **HTTP** para llamarlas.</span><span class="sxs-lookup"><span data-stu-id="74233-141">If you use your own APIs, not Microsoft-managed ones, use the built-in **HTTP** action to call them.</span></span> <span data-ttu-id="74233-142">Para tener una experiencia ideal, debe exponer un punto de conexión de Swagger para la API.</span><span class="sxs-lookup"><span data-stu-id="74233-142">For an ideal experience, you should expose a Swagger endpoint for your API.</span></span> <span data-ttu-id="74233-143">Este punto de conexión permite al Diseñador de aplicación lógica representar las entradas y salidas de la API.</span><span class="sxs-lookup"><span data-stu-id="74233-143">This endpoint enables the Logic App Designer to render the inputs and outputs for your API.</span></span> <span data-ttu-id="74233-144">Sin Swagger, el diseñador solo puede mostrar las entradas y salidas como objetos JSON opacos.</span><span class="sxs-lookup"><span data-stu-id="74233-144">Without Swagger, the designer can only show the inputs and outputs as opaque JSON objects.</span></span>

<span data-ttu-id="74233-145">Este es un ejemplo que muestra la nueva propiedad `metadata.apiDefinitionUrl` :</span><span class="sxs-lookup"><span data-stu-id="74233-145">Here is an example showing the new `metadata.apiDefinitionUrl` property:</span></span>

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

<span data-ttu-id="74233-146">Si hospeda su API web en Azure App Service, esta se muestra automáticamente en la lista de acciones disponibles en el diseñador.</span><span class="sxs-lookup"><span data-stu-id="74233-146">If you host your Web API on Azure App Service, your Web API automatically appears in the list of actions available in the designer.</span></span> <span data-ttu-id="74233-147">De lo contrario, tiene que pegar la dirección URL directamente.</span><span class="sxs-lookup"><span data-stu-id="74233-147">If not, you have to paste in the URL directly.</span></span> <span data-ttu-id="74233-148">El punto de conexión de Swagger debe estar sin autenticar para que se pueda usar dentro del Diseñador de aplicación lógica, aunque puede proteger la API propiamente dicha con cualquier método que admita Swagger.</span><span class="sxs-lookup"><span data-stu-id="74233-148">The Swagger endpoint must be unauthenticated to be usable in the Logic App Designer, although you can secure the API itself with whatever methods that Swagger supports.</span></span>

### <a name="call-deployed-api-apps-with-2015-08-01-preview"></a><span data-ttu-id="74233-149">Llamada a las aplicaciones de API implementadas con 2015-08-01-preview</span><span class="sxs-lookup"><span data-stu-id="74233-149">Call deployed API apps with 2015-08-01-preview</span></span>

<span data-ttu-id="74233-150">Si anteriormente implementó una aplicación de API, puede llamarla mediante la acción **HTTP**.</span><span class="sxs-lookup"><span data-stu-id="74233-150">If you previously deployed an API App, you can call the app with the **HTTP** action.</span></span>

<span data-ttu-id="74233-151">Por ejemplo, si utiliza Dropbox para enumerar archivos, la definición de la versión de esquema **2014-12-01-preview** puede presentarse de manera similar a:</span><span class="sxs-lookup"><span data-stu-id="74233-151">For example, if you use Dropbox to list files, your **2014-12-01-preview** schema version definition might have something like:</span></span>

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

<span data-ttu-id="74233-152">Puede construir la acción HTTP equivalente como en este ejemplo (la sección de parámetros de la definición de aplicación lógica permanece sin cambios):</span><span class="sxs-lookup"><span data-stu-id="74233-152">You can construct the equivalent HTTP action like this example, while the parameters section of the Logic app definition remains unchanged:</span></span>

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

<span data-ttu-id="74233-153">Vamos a recorrer estas propiedades una a una:</span><span class="sxs-lookup"><span data-stu-id="74233-153">Walking through these properties one-by-one:</span></span>

| <span data-ttu-id="74233-154">Propiedad de acción</span><span class="sxs-lookup"><span data-stu-id="74233-154">Action property</span></span> | <span data-ttu-id="74233-155">Descripción</span><span class="sxs-lookup"><span data-stu-id="74233-155">Description</span></span> |
| --- | --- |
| `type` |<span data-ttu-id="74233-156">`Http` en lugar de `APIapp`</span><span class="sxs-lookup"><span data-stu-id="74233-156">`Http` instead of `APIapp`</span></span> |
| `metadata.apiDefinitionUrl` |<span data-ttu-id="74233-157">Para usar esta acción en el Diseñador de aplicación lógica, incluya el punto de conexión de metadatos, que se construye a partir de: `{api app host.gateway}/api/service/apidef/{last segment of the api app host.id}/?api-version=2015-01-14&format=swagger-2.0-standard`</span><span class="sxs-lookup"><span data-stu-id="74233-157">To use this action in the Logic App Designer, include the metadata endpoint, which is constructed from: `{api app host.gateway}/api/service/apidef/{last segment of the api app host.id}/?api-version=2015-01-14&format=swagger-2.0-standard`</span></span> |
| `inputs.uri` |<span data-ttu-id="74233-158">Se construye a partir de: `{api app host.gateway}/api/service/invoke/{last segment of the api app host.id}/{api app operation}?api-version=2015-01-14`</span><span class="sxs-lookup"><span data-stu-id="74233-158">Constructed from: `{api app host.gateway}/api/service/invoke/{last segment of the api app host.id}/{api app operation}?api-version=2015-01-14`</span></span> |
| `inputs.method` |<span data-ttu-id="74233-159">Siempre `POST`</span><span class="sxs-lookup"><span data-stu-id="74233-159">Always `POST`</span></span> |
| `inputs.body` |<span data-ttu-id="74233-160">Idéntico a los parámetros de la aplicación de API</span><span class="sxs-lookup"><span data-stu-id="74233-160">Identical to the API App parameters</span></span> |
| `inputs.authentication` |<span data-ttu-id="74233-161">Idéntico a la autenticación de la aplicación de API</span><span class="sxs-lookup"><span data-stu-id="74233-161">Identical to the API App authentication</span></span> |

<span data-ttu-id="74233-162">Este enfoque debería funcionar para todas las acciones de aplicación de API.</span><span class="sxs-lookup"><span data-stu-id="74233-162">This approach should work for all API App actions.</span></span> <span data-ttu-id="74233-163">Sin embargo, recuerde que estas aplicaciones de API anteriores ya no se admiten.</span><span class="sxs-lookup"><span data-stu-id="74233-163">However, remember that these previous API Apps are no longer supported.</span></span> <span data-ttu-id="74233-164">Por lo que debe mover una API administrada a una de las dos opciones anteriores u hospedar su propia API web personalizada.</span><span class="sxs-lookup"><span data-stu-id="74233-164">So you should move to one of the two other previous options, a managed API or hosting your custom Web API.</span></span>

<a name="foreach"></a>
## <a name="renamed-repeat-to-foreach"></a><span data-ttu-id="74233-165">Cambio de nombre de "repeat" a "foreach"</span><span class="sxs-lookup"><span data-stu-id="74233-165">Renamed 'repeat' to 'foreach'</span></span>

<span data-ttu-id="74233-166">En la versión de esquema anterior, se recibieron numerosos comentarios de los clientes en que se indicaba que la instrucción **Repeat** era confusa y no captaba adecuadamente que **Repeat** era realmente para cada bucle.</span><span class="sxs-lookup"><span data-stu-id="74233-166">For the previous schema version, we received much customer feedback that **Repeat** was confusing and didn't properly capture that **Repeat** was really a for-each loop.</span></span> <span data-ttu-id="74233-167">Como resultado, hemos cambiado el nombre `repeat` por `foreach`.</span><span class="sxs-lookup"><span data-stu-id="74233-167">As a result, we have renamed `repeat` to `foreach`.</span></span> <span data-ttu-id="74233-168">Por ejemplo, anteriormente escribiría:</span><span class="sxs-lookup"><span data-stu-id="74233-168">For example, previously you would write:</span></span>

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

<span data-ttu-id="74233-169">Ahora debe escribir:</span><span class="sxs-lookup"><span data-stu-id="74233-169">Now you would write:</span></span>

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

<span data-ttu-id="74233-170">Anteriormente, la función `@repeatItem()` se utilizaba para hacer referencia al elemento actual que se itera.</span><span class="sxs-lookup"><span data-stu-id="74233-170">The function `@repeatItem()` was previously used to reference the current item being iterated over.</span></span> <span data-ttu-id="74233-171">Esta función ahora se reduce a `@item()`.</span><span class="sxs-lookup"><span data-stu-id="74233-171">This function is now simplified to `@item()`.</span></span> 

### <a name="reference-outputs-from-foreach"></a><span data-ttu-id="74233-172">Salidas de referencia de "foreach"</span><span class="sxs-lookup"><span data-stu-id="74233-172">Reference outputs from 'foreach'</span></span>

<span data-ttu-id="74233-173">Por motivos de simplificación, los resultados de las acciones `foreach` no se ajustan en un objeto denominado `repeatItems`.</span><span class="sxs-lookup"><span data-stu-id="74233-173">For simplification, the outputs from `foreach` actions are not wrapped in an object called `repeatItems`.</span></span> <span data-ttu-id="74233-174">Mientras que las salidas del ejemplo anterior de `repeat` eran:</span><span class="sxs-lookup"><span data-stu-id="74233-174">While the outputs from the previous `repeat` example were:</span></span>

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

<span data-ttu-id="74233-175">Ahora, estas salidas son:</span><span class="sxs-lookup"><span data-stu-id="74233-175">Now these outputs are:</span></span>

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

<span data-ttu-id="74233-176">Anteriormente, para obtener el cuerpo de la acción al hacer referencia a estas salidas, debía hacer lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="74233-176">Previously, to get to the body of the action when referencing these outputs:</span></span>

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

<span data-ttu-id="74233-177">Ahora puede hacer esto en su lugar:</span><span class="sxs-lookup"><span data-stu-id="74233-177">Now you can do instead:</span></span>

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

<span data-ttu-id="74233-178">Con estos cambios se eliminan las funciones `@repeatItem()`, `@repeatBody()` y `@repeatOutputs()`.</span><span class="sxs-lookup"><span data-stu-id="74233-178">With these changes, the functions `@repeatItem()`, `@repeatBody()`, and `@repeatOutputs()` are removed.</span></span>

<a name="http-listener"></a>
## <a name="native-http-listener"></a><span data-ttu-id="74233-179">Agente de escucha HTTP nativo</span><span class="sxs-lookup"><span data-stu-id="74233-179">Native HTTP listener</span></span>

<span data-ttu-id="74233-180">Las funcionalidades de la escucha HTTP ahora están integradas.</span><span class="sxs-lookup"><span data-stu-id="74233-180">The HTTP Listener capabilities are now built in.</span></span> <span data-ttu-id="74233-181">Así que ya no necesita implementar una aplicación de API de escucha HTTP.</span><span class="sxs-lookup"><span data-stu-id="74233-181">So you no longer need to deploy an HTTP Listener API App.</span></span> <span data-ttu-id="74233-182">Consulte aquí [los detalles completos de cómo hacer que los puntos de conexión de aplicación lógica](../logic-apps/logic-apps-http-endpoint.md).</span><span class="sxs-lookup"><span data-stu-id="74233-182">See [the full details for how to make your Logic app endpoint callable here](../logic-apps/logic-apps-http-endpoint.md).</span></span> 

<span data-ttu-id="74233-183">Con estos cambios, eliminamos la función `@accessKeys()`, que sustituimos por la función `@listCallbackURL()` para obtener el punto de conexión cuando sea necesario.</span><span class="sxs-lookup"><span data-stu-id="74233-183">With these changes, we removed the `@accessKeys()` function, which we replaced with the `@listCallbackURL()` function for getting the endpoint when necessary.</span></span> <span data-ttu-id="74233-184">Además, ahora debe definir al menos un desencadenador en la aplicación lógica.</span><span class="sxs-lookup"><span data-stu-id="74233-184">Also, you must now define at least one trigger in your logic app.</span></span> <span data-ttu-id="74233-185">Si desea `/run` el flujo de trabajo, debe tener uno de estos desencadenadores: `manual`, `apiConnectionWebhook` o `httpWebhook`.</span><span class="sxs-lookup"><span data-stu-id="74233-185">If you want to `/run` the workflow, you must have one of these triggers: `manual`, `apiConnectionWebhook`, or `httpWebhook`.</span></span>

<a name="child-workflows"></a>
## <a name="call-child-workflows"></a><span data-ttu-id="74233-186">Llamada a flujos de trabajo secundarios</span><span class="sxs-lookup"><span data-stu-id="74233-186">Call child workflows</span></span>

<span data-ttu-id="74233-187">Anteriormente, para llamar a los flujos de trabajo secundarios era necesario ir al flujo de trabajo, obtener el token de acceso y luego pegarlo en la definición de la aplicación lógica donde quiere llamar a ese flujo de trabajo secundario.</span><span class="sxs-lookup"><span data-stu-id="74233-187">Previously, calling child workflows required going to the workflow, getting the access token, and pasting the token in the logic app definition where you want to call that child workflow.</span></span> <span data-ttu-id="74233-188">Con la nueva versión de esquema, el motor de Logic Apps genera automáticamente una firma SAS en tiempo de ejecución para el flujo de trabajo secundario, lo que significa que no tiene que pegar ningún secreto en la definición.</span><span class="sxs-lookup"><span data-stu-id="74233-188">With the new schema, the Logic Apps engine automatically generates a SAS at runtime for the child workflow so you don't have to paste any secrets into the definition.</span></span> <span data-ttu-id="74233-189">Aquí tiene un ejemplo:</span><span class="sxs-lookup"><span data-stu-id="74233-189">Here is an example:</span></span>

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

<span data-ttu-id="74233-190">Una segunda mejora es se va a proporcionar a los flujos de trabajo secundarios acceso completo a la solicitud entrante.</span><span class="sxs-lookup"><span data-stu-id="74233-190">A second improvement is we are giving the child workflows full access to the incoming request.</span></span> <span data-ttu-id="74233-191">Eso significa que puede pasar parámetros en la sección *queries* y en el objeto *headers*, y que puede definir completamente todo el cuerpo.</span><span class="sxs-lookup"><span data-stu-id="74233-191">That means that you can pass parameters in the *queries* section and in the *headers* object and that you can fully define the entire body.</span></span>

<span data-ttu-id="74233-192">Por último, hay cambios necesarios en el flujo de trabajo secundario.</span><span class="sxs-lookup"><span data-stu-id="74233-192">Finally, there are required changes to the child workflow.</span></span> <span data-ttu-id="74233-193">Mientras que antes podía llamar a un flujo de trabajo secundario directamente, ahora debe definir un punto de conexión de desencadenador en el flujo de trabajo para que el elemento primario realice la llamada.</span><span class="sxs-lookup"><span data-stu-id="74233-193">While you could previously call a child workflow directly, now you must define a trigger endpoint in the workflow for the parent to call.</span></span> <span data-ttu-id="74233-194">Por lo general, agrega un desencadenador que tiene el tipo `manual` y luego usa desencadenador en la definición del elemento primario.</span><span class="sxs-lookup"><span data-stu-id="74233-194">Generally, you would add a trigger that has `manual` type, and then use that trigger in the parent definition.</span></span> <span data-ttu-id="74233-195">Tenga en cuenta que la propiedad `host` tiene un valor `triggerName`, ya que siempre debe especificar el desencadenador que va a invocar.</span><span class="sxs-lookup"><span data-stu-id="74233-195">Note the `host` property specifically has a `triggerName` because you must always specify which trigger you are invoking.</span></span>

## <a name="other-changes"></a><span data-ttu-id="74233-196">Otros cambios</span><span class="sxs-lookup"><span data-stu-id="74233-196">Other changes</span></span>

### <a name="new-queries-property"></a><span data-ttu-id="74233-197">Nueva propiedad "queries"</span><span class="sxs-lookup"><span data-stu-id="74233-197">New 'queries' property</span></span>

<span data-ttu-id="74233-198">Todos los tipos de acción admiten ahora una nueva entrada llamada `queries`.</span><span class="sxs-lookup"><span data-stu-id="74233-198">All action types now support a new input called `queries`.</span></span> <span data-ttu-id="74233-199">Esta entrada puede ser un objeto estructurado en lugar de tener que ensamblar la cadena a mano.</span><span class="sxs-lookup"><span data-stu-id="74233-199">This input can be a structured object, rather than you having to assemble the string by hand.</span></span>

### <a name="renamed-parse-function-to-json"></a><span data-ttu-id="74233-200">Cambio de nombre de la función "parse()" a "json()"</span><span class="sxs-lookup"><span data-stu-id="74233-200">Renamed 'parse()' function to 'json()'</span></span>

<span data-ttu-id="74233-201">Pronto se agregarán más tipos de contenido, por lo que hemos cambiado el nombre de la función `parse()` a `json()`.</span><span class="sxs-lookup"><span data-stu-id="74233-201">We are adding more content types soon, so we renamed the `parse()` function to `json()`.</span></span>

## <a name="coming-soon-enterprise-integration-apis"></a><span data-ttu-id="74233-202">Próximamente: API de Enterprise Integration</span><span class="sxs-lookup"><span data-stu-id="74233-202">Coming soon: Enterprise Integration APIs</span></span>

<span data-ttu-id="74233-203">Aún no disponemos de versiones administradas de las API de integración empresarial, como AS2.</span><span class="sxs-lookup"><span data-stu-id="74233-203">We don't have managed versions yet of the Enterprise Integration APIs, like AS2.</span></span> <span data-ttu-id="74233-204">Mientras tanto, puede usar sus API de BizTalk implementadas existentes a través de la acción HTTP.</span><span class="sxs-lookup"><span data-stu-id="74233-204">Meanwhile, you can use your existing deployed BizTalk APIs through the HTTP action.</span></span> <span data-ttu-id="74233-205">Para más información, consulte el uso de aplicaciones de API ya administradas en el [plan de integración](http://www.zdnet.com/article/microsoft-outlines-its-cloud-and-server-integration-roadmap-for-2016/).</span><span class="sxs-lookup"><span data-stu-id="74233-205">For details, see "Using your already deployed API apps" in the [integration roadmap](http://www.zdnet.com/article/microsoft-outlines-its-cloud-and-server-integration-roadmap-for-2016/).</span></span> 
