---
title: "aaaException control & escenario de registro de error: las aplicaciones lógicas de Azure | Documentos de Microsoft"
description: Describe un caso de uso real sobre control de excepciones y registro de errores avanzados para Azure Logic Apps
keywords: 
services: logic-apps
author: hedidin
manager: anneta
editor: 
documentationcenter: 
ms.assetid: 63b0b843-f6b0-4d9a-98d0-17500be17385
ms.service: logic-apps
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.custom: H1Hack27Feb2017
ms.date: 07/29/2016
ms.author: LADocs; b-hoedid
ms.openlocfilehash: e893a7b652254dca7b8a82398e8afd571f6ccd25
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="scenario-exception-handling-and-error-logging-for-logic-apps"></a>Escenario: control de excepciones y registro de errores para aplicaciones lógicas

Este escenario describe cómo puede ampliar un control de excepciones de lógica aplicación toobetter soporte técnico. Hemos usado una pregunta de hello tooanswer casos de uso real: "¿las aplicaciones lógicas de Azure admite excepciones y control de errores?"

> [!NOTE]
> esquema de Azure Logic Apps actual Hola proporciona una plantilla estándar para las respuestas de acción. Esta incluye la validación interna y las respuestas de error devueltas desde una aplicación de API.

## <a name="scenario-and-use-case-overview"></a>Información general de escenarios y casos de uso

Aquí es el caso de hello como caso de uso de Hola para este escenario: 

Las organizaciones sanitarias conocida nos ocupa toodevelop una solución de Azure que crearía un paciente portal mediante el uso de Microsoft Dynamics CRM Online. Necesitan registros de cita toosend entre portal paciente de Dynamics CRM Online de Hola y Salesforce. Se nos pidió hello toouse [FHIR HL7](http://www.hl7.org/implement/standards/fhir/) estándar para los registros de todos los pacientes.

proyecto de Hello tenía dos requisitos principales:  

* Un método toolog registros enviarán desde Hola portal de Dynamics CRM Online
* Una manera tooview los errores que se produjeron dentro del flujo de trabajo de Hola

> [!TIP]
> Para ver un vídeo de alto nivel acerca de este proyecto, [grupo de usuarios de la integración de](http://www.integrationusergroup.com/logic-apps-support-error-handling/ "grupo de usuarios de la integración de").

## <a name="how-we-solved-hello-problem"></a>Cómo se ha resuelto el problema de Hola

Elegimos [base de datos de Azure Cosmos](https://azure.microsoft.com/services/documentdb/ "base de datos de Azure Cosmos") como repositorio para los registros de error y registro de hello (Cosmos DB hace referencia toorecords como documentos). Dado que las aplicaciones lógicas de Azure tiene una plantilla estándar para todas las respuestas, no tendríamos toocreate un esquema personalizado. Podríamos crear una aplicación de API demasiado**insertar** y **consulta** para los registros de error y de registro. También podemos definir un esquema para cada una en la aplicación de API de hello.  

Otro requisito estaba toopurge registros después de una fecha determinada. COSMOS DB tiene una propiedad denominada [tiempo tooLive](https://azure.microsoft.com/blog/documentdb-now-supports-time-to-live-ttl/ "tiempo tooLive") (TTL), que permitía tooset una **tiempo tooLive** valor de cada registro o la colección. Esta función elimina Hola necesidad toomanually elimine los registros en la base de datos de Cosmos.

> [!IMPORTANT]
> toocomplete este tutorial, necesita una base de datos de la base de datos de Cosmos toocreate y dos colecciones (registro y errores).

## <a name="create-hello-logic-app"></a>Crear aplicación de lógica de hello

Hola primer paso es aplicación de lógica de hello toocreate y aplicación Hola abierto en el Diseñador de la lógica de aplicación. En este ejemplo, vamos a usar aplicaciones lógicas primarias y secundarias. Supongamos que ya se ha creado el elemento primario de Hola y va toocreate una aplicación de lógica de secundarios.

Dado que vamos a registro de hello toolog que salen de Dynamics CRM Online, puede empezar en la parte superior de Hola. Debemos usar un **solicitar** desencadenador porque la aplicación lógica de hello primario desencadena este elemento secundario.

### <a name="logic-app-trigger"></a>Desencadenador de aplicación lógica

Estamos usando un **solicitar** desencadenar tal y como se muestra en el siguiente ejemplo de Hola:

```` json
"triggers": {
        "request": {
          "type": "request",
          "kind": "http",
          "inputs": {
            "schema": {
              "properties": {
                "CRMid": {
                  "type": "string"
                },
                "recordType": {
                  "type": "string"
                },
                "salesforceID": {
                  "type": "string"
                },
                "update": {
                  "type": "boolean"
                }
              },
              "required": [
                "CRMid",
                "recordType",
                "salesforceID",
                "update"
              ],
              "type": "object"
            }
          }
        }
      },

````


## <a name="steps"></a>Pasos

Debemos registramos origen hello (solicitud) del registro de hello paciente de portal de Dynamics CRM Online Hola.

1. Debemos obtener un registro de nueva cita de Dynamics CRM Online.

   desencadenador Hola procedentes de CRM nos ofrece hello **CRM PatentId**, **tipo de registro**, **nuevo o actualizado registro** (nueva o actualizar el valor booleano), y  **SalesforceId**. Hola **SalesforceId** puede ser null porque solo se usa para una actualización.
   Obtenemos registro de hello CRM mediante el uso de hello CRM **PatientID** hello y **tipo de registro**.

2. A continuación, necesitamos tooadd nuestra aplicación de API de DocumentDB **InsertLogEntry** operación tal y como se muestra en el Diseñador de la lógica de aplicación.

   **Inserción de entrada de registro**

   ![Insertar entrada de registro](media/logic-apps-scenario-error-and-exception-handling/lognewpatient.png)

   **Inserción de entrada de error**

   ![Insertar entrada de registro](media/logic-apps-scenario-error-and-exception-handling/insertlogentry.png)

   **Comprobación de errores en la creación de registro**

   ![Condición](media/logic-apps-scenario-error-and-exception-handling/condition.png)

## <a name="logic-app-source-code"></a>Código fuente de la aplicación lógica

> [!NOTE]
> Hello en los ejemplos siguientes es solamente ejemplos. Dado que este tutorial se basa en una implementación en producción, Hola valor de un **nodo de origen** no puede mostrar las propiedades que están relacionada tooscheduling una cita. > 

### <a name="logging"></a>Registro

Hola después del código de aplicación lógica de ejemplo se muestra cómo toohandle el registro.

#### <a name="log-entry"></a>Entrada de registro

Este es el código fuente de la aplicación de la lógica Hola para insertar una entrada de registro.

``` json
"InsertLogEntry": {
        "metadata": {
        "apiDefinitionUrl": "https://.../swagger/docs/v1",
        "swaggerSource": "website"
        },
        "type": "Http",
        "inputs": {
        "body": {
            "date": "@{outputs('Gets_NewPatientRecord')['headers']['Date']}",
            "operation": "New Patient",
            "patientId": "@{triggerBody()['CRMid']}",
            "providerId": "@{triggerBody()['providerID']}",
            "source": "@{outputs('Gets_NewPatientRecord')['headers']}"
        },
        "method": "post",
        "uri": "https://.../api/Log"
        },
        "runAfter":    {
            "Gets_NewPatientecord": ["Succeeded"]
        }
}
```

#### <a name="log-request"></a>Solicitud de registro

Este es el mensaje de solicitud de registro de hello registrado la aplicación de API de toohello.

``` json
    {
    "uri": "https://.../api/Log",
    "method": "post",
    "body": {
        "date": "Fri, 10 Jun 2016 22:31:56 GMT",
        "operation": "New Patient",
        "patientId": "6b115f6d-a7ee-e511-80f5-3863bb2eb2d0",
        "providerId": "",
        "source": "{/"Pragma/":/"no-cache/",/"x-ms-request-id/":/"e750c9a9-bd48-44c4-bbba-1688b6f8a132/",/"OData-Version/":/"4.0/",/"Cache-Control/":/"no-cache/",/"Date/":/"Fri, 10 Jun 2016 22:31:56 GMT/",/"Set-Cookie/":/"ARRAffinity=785f4334b5e64d2db0b84edcc1b84f1bf37319679aefce206b51510e56fd9770;Path=/;Domain=127.0.0.1/",/"Server/":/"Microsoft-IIS/8.0,Microsoft-HTTPAPI/2.0/",/"X-AspNet-Version/":/"4.0.30319/",/"X-Powered-By/":/"ASP.NET/",/"Content-Length/":/"1935/",/"Content-Type/":/"application/json; odata.metadata=minimal; odata.streaming=true/",/"Expires/":/"-1/"}"
        }
    }

```


#### <a name="log-response"></a>Respuesta de registro

Este es el mensaje de respuesta de registro de hello de aplicación de API de hello.

``` json
{
    "statusCode": 200,
    "headers": {
        "Pragma": "no-cache",
        "Cache-Control": "no-cache",
        "Date": "Fri, 10 Jun 2016 22:32:17 GMT",
        "Server": "Microsoft-IIS/8.0",
        "X-AspNet-Version": "4.0.30319",
        "X-Powered-By": "ASP.NET",
        "Content-Length": "964",
        "Content-Type": "application/json; charset=utf-8",
        "Expires": "-1"
    },
    "body": {
        "ttl": 2592000,
        "id": "6b115f6d-a7ee-e511-80f5-3863bb2eb2d0_1465597937",
        "_rid": "XngRAOT6IQEHAAAAAAAAAA==",
        "_self": "dbs/XngRAA==/colls/XngRAOT6IQE=/docs/XngRAOT6IQEHAAAAAAAAAA==/",
        "_ts": 1465597936,
        "_etag": "/"0400fc2f-0000-0000-0000-575b3ff00000/"",
        "patientID": "6b115f6d-a7ee-e511-80f5-3863bb2eb2d0",
        "timestamp": "2016-06-10T22:31:56Z",
        "source": "{/"Pragma/":/"no-cache/",/"x-ms-request-id/":/"e750c9a9-bd48-44c4-bbba-1688b6f8a132/",/"OData-Version/":/"4.0/",/"Cache-Control/":/"no-cache/",/"Date/":/"Fri, 10 Jun 2016 22:31:56 GMT/",/"Set-Cookie/":/"ARRAffinity=785f4334b5e64d2db0b84edcc1b84f1bf37319679aefce206b51510e56fd9770;Path=/;Domain=127.0.0.1/",/"Server/":/"Microsoft-IIS/8.0,Microsoft-HTTPAPI/2.0/",/"X-AspNet-Version/":/"4.0.30319/",/"X-Powered-By/":/"ASP.NET/",/"Content-Length/":/"1935/",/"Content-Type/":/"application/json; odata.metadata=minimal; odata.streaming=true/",/"Expires/":/"-1/"}",
        "operation": "New Patient",
        "salesforceId": "",
        "expired": false
    }
}

```

Ahora Echemos un vistazo a los pasos de control de errores de Hola.

### <a name="error-handling"></a>Control de errores

Hello siguiente ejemplo de código de aplicación lógica muestra cómo puede implementar el control de errores.

#### <a name="create-error-record"></a>Creación de un registro de errores

Este es el código fuente de la aplicación de la lógica Hola para crear un registro de error.

``` json
"actions": {
    "CreateErrorRecord": {
        "metadata": {
        "apiDefinitionUrl": "https://.../swagger/docs/v1",
        "swaggerSource": "website"
        },
        "type": "Http",
        "inputs": {
        "body": {
            "action": "New_Patient",
            "isError": true,
            "crmId": "@{triggerBody()['CRMid']}",
            "patientID": "@{triggerBody()['CRMid']}",
            "message": "@{body('Create_NewPatientRecord')['message']}",
            "providerId": "@{triggerBody()['providerId']}",
            "severity": 4,
            "source": "@{actions('Create_NewPatientRecord')['inputs']['body']}",
            "statusCode": "@{int(outputs('Create_NewPatientRecord')['statusCode'])}",
            "salesforceId": "",
            "update": false
        },
        "method": "post",
        "uri": "https://.../api/CrMtoSfError"
        },
        "runAfter":
        {
            "Create_NewPatientRecord": ["Failed" ]
        }
    }
}             
```

#### <a name="insert-error-into-cosmos-db--request"></a>Insertar error en Cosmos DB: solicitud

``` json

{
    "uri": "https://.../api/CrMtoSfError",
    "method": "post",
    "body": {
        "action": "New_Patient",
        "isError": true,
        "crmId": "6b115f6d-a7ee-e511-80f5-3863bb2eb2d0",
        "patientId": "6b115f6d-a7ee-e511-80f5-3863bb2eb2d0",
        "message": "Salesforce failed toocomplete task: Message: duplicate value found: Account_ID_MED__c duplicates value on record with id: 001U000001c83gK",
        "providerId": "",
        "severity": 4,
        "salesforceId": "",
        "update": false,
        "source": "{/"Account_Class_vod__c/":/"PRAC/",/"Account_Status_MED__c/":/"I/",/"CRM_HUB_ID__c/":/"6b115f6d-a7ee-e511-80f5-3863bb2eb2d0/",/"Credentials_vod__c/",/"DTC_ID_MED__c/":/"/",/"Fax/":/"/",/"FirstName/":/"A/",/"Gender_vod__c/":/"/",/"IMS_ID__c/":/"/",/"LastName/":/"BAILEY/",/"MasterID_mp__c/":/"/",/"C_ID_MED__c/":/"851588/",/"Middle_vod__c/":/"/",/"NPI_vod__c/":/"/",/"PDRP_MED__c/":false,/"PersonDoNotCall/":false,/"PersonEmail/":/"/",/"PersonHasOptedOutOfEmail/":false,/"PersonHasOptedOutOfFax/":false,/"PersonMobilePhone/":/"/",/"Phone/":/"/",/"Practicing_Specialty__c/":/"FM - FAMILY MEDICINE/",/"Primary_City__c/":/"/",/"Primary_State__c/":/"/",/"Primary_Street_Line2__c/":/"/",/"Primary_Street__c/":/"/",/"Primary_Zip__c/":/"/",/"RecordTypeId/":/"012U0000000JaPWIA0/",/"Request_Date__c/":/"2016-06-10T22:31:55.9647467Z/",/"ONY_ID__c/":/"/",/"Specialty_1_vod__c/":/"/",/"Suffix_vod__c/":/"/",/"Website/":/"/"}",
        "statusCode": "400"
    }
}
```

#### <a name="insert-error-into-cosmos-db--response"></a>Insertar error en Cosmos DB: respuesta

``` json
{
    "statusCode": 200,
    "headers": {
        "Pragma": "no-cache",
        "Cache-Control": "no-cache",
        "Date": "Fri, 10 Jun 2016 22:31:57 GMT",
        "Server": "Microsoft-IIS/8.0",
        "X-AspNet-Version": "4.0.30319",
        "X-Powered-By": "ASP.NET",
        "Content-Length": "1561",
        "Content-Type": "application/json; charset=utf-8",
        "Expires": "-1"
    },
    "body": {
        "id": "6b115f6d-a7ee-e511-80f5-3863bb2eb2d0-1465597917",
        "_rid": "sQx2APhVzAA8AAAAAAAAAA==",
        "_self": "dbs/sQx2AA==/colls/sQx2APhVzAA=/docs/sQx2APhVzAA8AAAAAAAAAA==/",
        "_ts": 1465597912,
        "_etag": "/"0c00eaac-0000-0000-0000-575b3fdc0000/"",
        "prescriberId": "6b115f6d-a7ee-e511-80f5-3863bb2eb2d0",
        "timestamp": "2016-06-10T22:31:57.3651027Z",
        "action": "New_Patient",
        "salesforceId": "",
        "update": false,
        "body": "CRM failed toocomplete task: Message: duplicate value found: CRM_HUB_ID__c duplicates value on record with id: 001U000001c83gK",
        "source": "{/"Account_Class_vod__c/":/"PRAC/",/"Account_Status_MED__c/":/"I/",/"CRM_HUB_ID__c/":/"6b115f6d-a7ee-e511-80f5-3863bb2eb2d0/",/"Credentials_vod__c/":/"DO - Degree level is DO/",/"DTC_ID_MED__c/":/"/",/"Fax/":/"/",/"FirstName/":/"A/",/"Gender_vod__c/":/"/",/"IMS_ID__c/":/"/",/"LastName/":/"BAILEY/",/"MterID_mp__c/":/"/",/"Medicis_ID_MED__c/":/"851588/",/"Middle_vod__c/":/"/",/"NPI_vod__c/":/"/",/"PDRP_MED__c/":false,/"PersonDoNotCall/":false,/"PersonEmail/":/"/",/"PersonHasOptedOutOfEmail/":false,/"PersonHasOptedOutOfFax/":false,/"PersonMobilePhone/":/"/",/"Phone/":/"/",/"Practicing_Specialty__c/":/"FM - FAMILY MEDICINE/",/"Primary_City__c/":/"/",/"Primary_State__c/":/"/",/"Primary_Street_Line2__c/":/"/",/"Primary_Street__c/":/"/",/"Primary_Zip__c/":/"/",/"RecordTypeId/":/"012U0000000JaPWIA0/",/"Request_Date__c/":/"2016-06-10T22:31:55.9647467Z/",/"XXXXXXX/":/"/",/"Specialty_1_vod__c/":/"/",/"Suffix_vod__c/":/"/",/"Website/":/"/"}",
        "code": 400,
        "errors": null,
        "isError": true,
        "severity": 4,
        "notes": null,
        "resolved": 0
        }
}
```

#### <a name="salesforce-error-response"></a>Respuesta de error de Salesforce

``` json
{
    "statusCode": 400,
    "headers": {
        "Pragma": "no-cache",
        "x-ms-request-id": "3e8e4884-288e-4633-972c-8271b2cc912c",
        "X-Content-Type-Options": "nosniff",
        "Cache-Control": "no-cache",
        "Date": "Fri, 10 Jun 2016 22:31:56 GMT",
        "Set-Cookie": "ARRAffinity=785f4334b5e64d2db0b84edcc1b84f1bf37319679aefce206b51510e56fd9770;Path=/;Domain=127.0.0.1",
        "Server": "Microsoft-IIS/8.0,Microsoft-HTTPAPI/2.0",
        "X-AspNet-Version": "4.0.30319",
        "X-Powered-By": "ASP.NET",
        "Content-Length": "205",
        "Content-Type": "application/json; charset=utf-8",
        "Expires": "-1"
    },
    "body": {
        "status": 400,
        "message": "Salesforce failed toocomplete task: Message: duplicate value found: Account_ID_MED__c duplicates value on record with id: 001U000001c83gK",
        "source": "Salesforce.Common",
        "errors": []
    }
}

```

### <a name="return-hello-response-back-tooparent-logic-app"></a>Devolver la aplicación de lógica de hello respuesta tooparent atrás

Después de obtener respuesta de hello, puede pasar la respuesta de hello aplicación lógica de retroceso toohello primario.

#### <a name="return-success-response-tooparent-logic-app"></a>Aplicación de lógica de tooparent de respuesta de éxito de valor devuelto

``` json
"SuccessResponse": {
    "runAfter":
        {
            "UpdateNew_CRMPatientResponse": ["Succeeded"]
        },
    "inputs": {
        "body": {
            "status": "Success"
    },
    "headers": {
    "    Content-type": "application/json",
        "x-ms-date": "@utcnow()"
    },
    "statusCode": 200
    },
    "type": "Response"
}
```

#### <a name="return-error-response-tooparent-logic-app"></a>Aplicación de lógica de tooparent de respuesta de error de retorno

``` json
"ErrorResponse": {
    "runAfter":
        {
            "Create_NewPatientRecord": ["Failed"]
        },
    "inputs": {
        "body": {
            "status": "BadRequest"
        },
        "headers": {
            "Content-type": "application/json",
            "x-ms-date": "@utcnow()"
        },
        "statusCode": 400
    },
    "type": "Response"
}

```


## <a name="cosmos-db-repository-and-portal"></a>Portal y repositorio de Cosmos DB

Nuestra solución agregó funcionalidades con [Cosmos DB](https://azure.microsoft.com/services/documentdb).

### <a name="error-management-portal"></a>Portal de administración de errores

errores de hello tooview, puede crear un registros de error MVC web app toodisplay Hola de base de datos de Cosmos. Hola **lista**, **detalles**, **editar**, y **eliminar** operaciones se incluyen en la versión actual de Hola.

> [!NOTE]
> Operación de edición: Cosmos DB reemplaza todo el documento Hola. Hola registros mostrados en hello **lista** y **detalle** vistas son solamente ejemplos. No son registros reales de citas de pacientes.

Estos son ejemplos de nuestra aplicación MVC detalles creados previamente con hello describen enfoque.

#### <a name="error-management-list"></a>Lista de administración de errores
![Lista de errores](media/logic-apps-scenario-error-and-exception-handling/errorlist.png)

#### <a name="error-management-detail-view"></a>Vista de detalles de administración de errores
![Detalles del error](media/logic-apps-scenario-error-and-exception-handling/errordetails.png)

### <a name="log-management-portal"></a>Portal de administración de registros

registros de hello tooview, también creamos una aplicación web MVC. Estos son ejemplos de nuestra aplicación MVC detalles creados previamente con hello describen enfoque.

#### <a name="sample-log-detail-view"></a>Vista de detalles del registro de ejemplo
![Vista de detalles del registro](media/logic-apps-scenario-error-and-exception-handling/samplelogdetail.png)

### <a name="api-app-details"></a>Detalles de la aplicación de API

#### <a name="logic-apps-exception-management-api"></a>API de administración de excepciones de Logic Apps

Nuestra aplicación de API de administración de excepciones de Azure Logic Apps, de código abierto, proporciona la funcionalidad que se describe aquí. Hay dos controladores:

* **ErrorController** inserta un registro de error (documento) en una colección de DocumentDB.
* **LogController** inserta una entrada de registro (documento) en una colección de DocumentDB.

> [!TIP]
> Usan ambos controladores `async Task<dynamic>` Hola de operaciones, lo que permite operaciones tooresolve en tiempo de ejecución, por lo que podemos crear documentos de esquema en el cuerpo de Hola de operación de Hola. 
> 

Todos los documentos de DocumentDB deben tener un identificador único. Estamos usando `PatientId` y agregar una marca de tiempo que sea convertir el valor de marca de tiempo de Unix tooa (double). Se trunca hello tooremove Hola fracciones valor.

Puede ver código fuente de Hola de nuestro controlador de error API [desde GitHub](https://github.com/HEDIDIN/LogicAppsExceptionManagementApi/blob/master/Logic App Exception Management API/Controllers/ErrorController.cs).

Llamamos a Hola API desde una aplicación de lógica mediante el uso de hello según la sintaxis:

``` json
 "actions": {
        "CreateErrorRecord": {
          "metadata": {
            "apiDefinitionUrl": "https://.../swagger/docs/v1",
            "swaggerSource": "website"
          },
          "type": "Http",
          "inputs": {
            "body": {
              "action": "New_Patient",
              "isError": true,
              "crmId": "@{triggerBody()['CRMid']}",
              "prescriberId": "@{triggerBody()['CRMid']}",
              "message": "@{body('Create_NewPatientRecord')['message']}",
              "salesforceId": "@{triggerBody()['salesforceID']}",
              "severity": 4,
              "source": "@{actions('Create_NewPatientRecord')['inputs']['body']}",
              "statusCode": "@{int(outputs('Create_NewPatientRecord')['statusCode'])}",
              "update": false
            },
            "method": "post",
            "uri": "https://.../api/CrMtoSfError"
          },
          "runAfter": {
              "Create_NewPatientRecord": ["Failed"]
            }
        }
 }
```

Hola expresión Hola anteriores comprobaciones de ejemplo de código de hello *Create_NewPatientRecord* estado de **error**.

## <a name="summary"></a>Resumen

* Puede implementar fácilmente el registro y control de errores en una aplicación lógica.
* Puede usar documentos como repositorio de Hola para los registros de error y registro (documentos).
* Puede usar MVC toocreate un registro toodisplay portal y registros de error.

### <a name="source-code"></a>Código fuente

código de origen de Hola de hello aplicación API de administración de excepción de aplicaciones de lógica está disponible en este [repositorio de GitHub](https://github.com/HEDIDIN/LogicAppsExceptionManagementApi "API de administración de excepciones de aplicación lógica").

## <a name="next-steps"></a>Pasos siguientes

* [Ver más ejemplos y escenarios de aplicaciones Logic Apps](../logic-apps/logic-apps-examples-and-scenarios.md)
* [Obtener más información sobre supervisión de Logic Apps](../logic-apps/logic-apps-monitor-your-logic-apps.md)
* [Creación de plantillas de implementación automatizadas de Logic Apps](../logic-apps/logic-apps-create-deploy-template.md)
