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
# <a name="schema-updates-for-azure-logic-apps---august-1-2015-preview"></a>Actualizaciones de esquema para Azure Logic Apps de la versión preliminar del 1 de agosto de 2015

Este nuevo esquema y la API de la versión para las aplicaciones lógicas de Azure incluye mejoras claves que hacen que las aplicaciones lógicas más toouse más fácil y confiable:

*   Hola **APIApp** tipo de acción es actualizada tooa nueva [ **APIConnection** ](#api-connections) tipo de acción.
*   **Repita** se cambia el nombre demasiado[**Foreach**](#foreach).
*   Hola [ **escucha HTTP** API App](#http-listener) ya no es necesario.
*   En la llamada a los flujos de trabajo secundarios se usa un [nuevo esquema](#child-workflows).

<a name="api-connections"></a>
## <a name="move-tooapi-connections"></a>Mover las conexiones de tooAPI

Hola mayor cambio es que ya no tienen aplicaciones de API de toodeploy en su suscripción de Azure para que pueda usar las API. Estas son formas de Hola que puede usar las API:

* API administradas
* Sus API web personalizadas

Cada una se controla de forma algo distinta, ya que sus modelos de administración y hospedaje son diferentes. Una ventaja de este modelo es que ya no está restringido tooresources que se implementan en el grupo de recursos de Azure. 

### <a name="managed-apis"></a>API administradas

Algunas API se administran de forma automática, como Office 365, Salesforce, Twitter y FTP. Puede usar algunas API administradas tal y como están, como en el caso de Bing Translate, mientras que otras requieren configuración. Esta configuración se conoce como *conexión*.

Por ejemplo, cuando use Office 365, debe crear una conexión que contenga el token de inicio de sesión de Office 365. Este token de forma segura se almacenan y se actualiza para que la aplicación lógica siempre puede llamar a Hola API de Office 365. O bien, si desea tooconnect tooyour FTP o SQL server, debe crear una conexión que tiene la cadena de conexión de Hola. 

En esta definición, estas acciones se denominan `APIConnection`. Este es un ejemplo de una conexión que llama a Office 365 toosend un correo electrónico:

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

Hola `host` objeto es parte de las entradas que es único tooAPI conexiones y contiene elementos de fila: `api` y `connection`.

Hola `api` tiene hello en tiempo de ejecución se hospeda la dirección URL de donde que administra la API. Puede ver todos los Hola disponibles API administradas mediante una llamada a `GET https://management.azure.com/subscriptions/{subid}/providers/Microsoft.Web/managedApis/?api-version=2015-08-01-preview`.

Cuando se usa una API, Hola API que no tenga o cualquier *parámetros de conexión* definido. Si no Hola API, no *conexión* es necesario. Si no Hola API, debe crear una conexión. conexión de Hello creado tiene nombre hello que elija. A continuación, hacer referencia a nombre de Hola Hola `connection` objeto dentro de hello `host` objeto. toocreate una conexión en un grupo de recursos, llamada:

```
PUT https://management.azure.com/subscriptions/{subid}/resourceGroups/{rgname}/providers/Microsoft.Web/connections/{name}?api-version=2015-08-01-preview
```

Con hello siguiente cuerpo:

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

### <a name="deploy-managed-apis-in-an-azure-resource-manager-template"></a>Implementación de API administradas en una plantilla de Azure Resource Manager

Puede crear una aplicación completa en una plantilla de Azure Resource Manager siempre que no se requiera inicio de sesión interactivo.
Si el inicio de sesión es necesario, puede configurar todo el contenido con plantilla de Azure Resource Manager hello, pero tiene toovisit hello tooauthorize portal Hola conexiones. 

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

Puede ver en este ejemplo que las conexiones de hello son simplemente los recursos a los que viven en el grupo de recursos. Hacen referencia a tooyou disponible de API de hello administrado en su suscripción.

### <a name="your-custom-web-apis"></a>Sus API web personalizadas

Si usa su propia API, las no administrada por Microsoft, usar integrada de hello **HTTP** acción toocall ellos. Para tener una experiencia ideal, debe exponer un punto de conexión de Swagger para la API. Este extremo permite entradas de hello Diseñador de la aplicación lógica toorender hello y salidas de la API. Sin Swagger, Diseñador de hello solo puede mostrar hello entradas y salidas como objetos JSON opacos.

Aquí es un Hola de ejemplo que muestra nueva `metadata.apiDefinitionUrl` propiedad:

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

Si hospeda su API Web en el servicio de aplicaciones de Azure, la API Web aparece automáticamente en lista de Hola de acciones disponibles en el Diseñador de Hola. Si no es así, tienen toopaste en dirección URL de hello directamente. extremo de Swagger de Hello debe ser toobe no autenticada se puede usar en hello Diseñador de la lógica de aplicaciones, aunque puede proteger Hola propia API con los métodos que admite Swagger.

### <a name="call-deployed-api-apps-with-2015-08-01-preview"></a>Llamada a las aplicaciones de API implementadas con 2015-08-01-preview

Si previamente ha implementado una API App, puede llamar a la aplicación hello con hello **HTTP** acción.

Por ejemplo, si utiliza archivos de toolist de Dropbox, su **2014-12-01-versión preliminar** definición de la versión de esquema puede tener algo parecido:

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

Puede construir acción HTTP equivalente de hello mostrado en este ejemplo, mientras permanece sin modificar sección de parámetros de Hola de hello definición de la aplicación lógica:

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

Vamos a recorrer estas propiedades una a una:

| Propiedad de acción | Descripción |
| --- | --- |
| `type` |`Http` en lugar de `APIapp` |
| `metadata.apiDefinitionUrl` |toouse esta acción en hello Diseñador de la lógica de aplicaciones, incluir el extremo de metadatos de hello, que se construye a partir:`{api app host.gateway}/api/service/apidef/{last segment of hello api app host.id}/?api-version=2015-01-14&format=swagger-2.0-standard` |
| `inputs.uri` |Se construye a partir de: `{api app host.gateway}/api/service/invoke/{last segment of hello api app host.id}/{api app operation}?api-version=2015-01-14` |
| `inputs.method` |Siempre `POST` |
| `inputs.body` |Parámetros de la aplicación idéntico toohello API |
| `inputs.authentication` |Toohello idéntico autenticación API App |

Este enfoque debería funcionar para todas las acciones de aplicación de API. Sin embargo, recuerde que estas aplicaciones de API anteriores ya no se admiten. Por lo que debe mover tooone de hello dos otras opciones anteriores, una API administrada u hospeda su API Web personalizado.

<a name="foreach"></a>
## <a name="renamed-repeat-tooforeach"></a>Cambiar el nombre 'repeat' too'foreach'

Para la versión de esquema anterior hello, hemos recibido la máxima cantidad de información del cliente que **repita** dio lugar a confusión y no captura correctamente que **repita** era un bucle for-each. Como resultado, hemos hemos cambiado el nombre `repeat` demasiado`foreach`. Por ejemplo, anteriormente escribiría:

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

Ahora debe escribir:

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

Hola función `@repeatItem()` se elemento actual de hello tooreference usadas previamente que se recorre en iteración. Esta función se reducen ahora demasiado`@item()`. 

### <a name="reference-outputs-from-foreach"></a>Salidas de referencia de "foreach"

Para simplificar, Hola genera de `foreach` acciones no se ajustan en un objeto denominado `repeatItems`. Mientras genera Hola de hello anterior `repeat` ejemplo fuera:

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

Ahora, estas salidas son:

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

Anteriormente, tooget toohello cuerpo de acción de hello al hacer referencia a estas salidas:

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

Ahora puede hacer esto en su lugar:

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

Con estos cambios, Hola funciones `@repeatItem()`, `@repeatBody()`, y `@repeatOutputs()` se quitan.

<a name="http-listener"></a>
## <a name="native-http-listener"></a>Agente de escucha HTTP nativo

Hola capacidades ahora están integradas en un agente de escucha de HTTP. Por lo que ya no necesita toodeploy una aplicación de API del agente de escucha de HTTP. Vea [Hola a todos los detalles acerca de cómo toomake su aquí invocable del punto de conexión de lógica aplicación](../logic-apps/logic-apps-http-endpoint.md). 

Con estos cambios, eliminamos hello `@accessKeys()` función, que se sustituye por hello `@listCallbackURL()` función para obtener el punto de conexión de hello cuando sea necesario. Además, ahora debe definir al menos un desencadenador en la aplicación lógica. Si desea demasiado`/run` Hola de flujo de trabajo, debe tener uno de estos desencadenadores: `manual`, `apiConnectionWebhook`, o `httpWebhook`.

<a name="child-workflows"></a>
## <a name="call-child-workflows"></a>Llamada a flujos de trabajo secundarios

Anteriormente, al llamar a los flujos de trabajo secundarios requería va toohello flujo de trabajo, obtener token de acceso de Hola y pegado de token de hello en la definición de aplicación lógica de hello en el que desea toocall ese flujo de trabajo secundario. Con el nuevo esquema de hello, motor genera automáticamente una SAS en tiempo de ejecución para las aplicaciones lógicas de Hola Hola flujo de trabajo secundario por lo que no haya demasiado pegar los secretos en la definición de Hola. Aquí tiene un ejemplo:

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

Una segunda mejora es que le estamos ofreciendo a secundarios Hola solicitud entrante de toohello de acceso completo de los flujos de trabajo. Esto significa que puede pasar parámetros en hello *consultas* sección y en hello *encabezados* objeto y que se puede definir completamente Hola cuerpo completo.

Por último, hay flujo de trabajo de cambios necesarios toohello secundario. Ahora mientras previamente podría llamar directamente un flujo de trabajo secundario, debe definir un extremo de desencadenador con el flujo de trabajo de Hola para hello primario toocall. Por lo general, debe agregar un desencadenador que tiene `manual` escriba y, a continuación, usar ese desencadenador en definición de hello primario. Hola Nota `host` propiedad específicamente tiene un `triggerName` porque siempre debe especificar qué desencadenador que se está invocando.

## <a name="other-changes"></a>Otros cambios

### <a name="new-queries-property"></a>Nueva propiedad "queries"

Todos los tipos de acción admiten ahora una nueva entrada llamada `queries`. Esta entrada puede ser un objeto estructurado, en lugar de tener la cadena de hello tooassemble a mano.

### <a name="renamed-parse-function-toojson"></a>Cambiar el nombre 'parse()' función too'json()'

Vamos a agregar tipos de contenido más pronto, por lo que hemos cambiado el nombre hello `parse()` función demasiado`json()`.

## <a name="coming-soon-enterprise-integration-apis"></a>Próximamente: API de Enterprise Integration

No tenemos versiones administradas todavía de hello las API de integración de Enterprise, como AS2. Mientras tanto, puede usar su APIs BizTalk implementada existente a través de hello acción HTTP. Para obtener más información, vea "Usar las aplicaciones ya implementadas de API" Hola [plan de integración](http://www.zdnet.com/article/microsoft-outlines-its-cloud-and-server-integration-roadmap-for-2016/). 
