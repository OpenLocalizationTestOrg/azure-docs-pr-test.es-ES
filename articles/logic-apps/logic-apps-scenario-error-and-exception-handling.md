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
# <a name="scenario-exception-handling-and-error-logging-for-logic-apps"></a><span data-ttu-id="2248b-103">Escenario: control de excepciones y registro de errores para aplicaciones lógicas</span><span class="sxs-lookup"><span data-stu-id="2248b-103">Scenario: Exception handling and error logging for logic apps</span></span>

<span data-ttu-id="2248b-104">Este escenario describe cómo puede ampliar un control de excepciones de lógica aplicación toobetter soporte técnico.</span><span class="sxs-lookup"><span data-stu-id="2248b-104">This scenario describes how you can extend a logic app toobetter support exception handling.</span></span> <span data-ttu-id="2248b-105">Hemos usado una pregunta de hello tooanswer casos de uso real: "¿las aplicaciones lógicas de Azure admite excepciones y control de errores?"</span><span class="sxs-lookup"><span data-stu-id="2248b-105">We've used a real-life use case tooanswer hello question: "Does Azure Logic Apps support exception and error handling?"</span></span>

> [!NOTE]
> <span data-ttu-id="2248b-106">esquema de Azure Logic Apps actual Hola proporciona una plantilla estándar para las respuestas de acción.</span><span class="sxs-lookup"><span data-stu-id="2248b-106">hello current Azure Logic Apps schema provides a standard template for action responses.</span></span> <span data-ttu-id="2248b-107">Esta incluye la validación interna y las respuestas de error devueltas desde una aplicación de API.</span><span class="sxs-lookup"><span data-stu-id="2248b-107">This template includes both internal validation and error responses returned from an API app.</span></span>

## <a name="scenario-and-use-case-overview"></a><span data-ttu-id="2248b-108">Información general de escenarios y casos de uso</span><span class="sxs-lookup"><span data-stu-id="2248b-108">Scenario and use case overview</span></span>

<span data-ttu-id="2248b-109">Aquí es el caso de hello como caso de uso de Hola para este escenario:</span><span class="sxs-lookup"><span data-stu-id="2248b-109">Here's hello story as hello use case for this scenario:</span></span> 

<span data-ttu-id="2248b-110">Las organizaciones sanitarias conocida nos ocupa toodevelop una solución de Azure que crearía un paciente portal mediante el uso de Microsoft Dynamics CRM Online.</span><span class="sxs-lookup"><span data-stu-id="2248b-110">A well-known healthcare organization engaged us toodevelop an Azure solution that would create a patient portal by using Microsoft Dynamics CRM Online.</span></span> <span data-ttu-id="2248b-111">Necesitan registros de cita toosend entre portal paciente de Dynamics CRM Online de Hola y Salesforce.</span><span class="sxs-lookup"><span data-stu-id="2248b-111">They needed toosend appointment records between hello Dynamics CRM Online patient portal and Salesforce.</span></span> <span data-ttu-id="2248b-112">Se nos pidió hello toouse [FHIR HL7](http://www.hl7.org/implement/standards/fhir/) estándar para los registros de todos los pacientes.</span><span class="sxs-lookup"><span data-stu-id="2248b-112">We were asked toouse hello [HL7 FHIR](http://www.hl7.org/implement/standards/fhir/) standard for all patient records.</span></span>

<span data-ttu-id="2248b-113">proyecto de Hello tenía dos requisitos principales:</span><span class="sxs-lookup"><span data-stu-id="2248b-113">hello project had two major requirements:</span></span>  

* <span data-ttu-id="2248b-114">Un método toolog registros enviarán desde Hola portal de Dynamics CRM Online</span><span class="sxs-lookup"><span data-stu-id="2248b-114">A method toolog records sent from hello Dynamics CRM Online portal</span></span>
* <span data-ttu-id="2248b-115">Una manera tooview los errores que se produjeron dentro del flujo de trabajo de Hola</span><span class="sxs-lookup"><span data-stu-id="2248b-115">A way tooview any errors that occurred within hello workflow</span></span>

> [!TIP]
> <span data-ttu-id="2248b-116">Para ver un vídeo de alto nivel acerca de este proyecto, [grupo de usuarios de la integración de](http://www.integrationusergroup.com/logic-apps-support-error-handling/ "grupo de usuarios de la integración de").</span><span class="sxs-lookup"><span data-stu-id="2248b-116">For a high-level video about this project, see [Integration User Group](http://www.integrationusergroup.com/logic-apps-support-error-handling/ "Integration User Group").</span></span>

## <a name="how-we-solved-hello-problem"></a><span data-ttu-id="2248b-117">Cómo se ha resuelto el problema de Hola</span><span class="sxs-lookup"><span data-stu-id="2248b-117">How we solved hello problem</span></span>

<span data-ttu-id="2248b-118">Elegimos [base de datos de Azure Cosmos](https://azure.microsoft.com/services/documentdb/ "base de datos de Azure Cosmos") como repositorio para los registros de error y registro de hello (Cosmos DB hace referencia toorecords como documentos).</span><span class="sxs-lookup"><span data-stu-id="2248b-118">We chose [Azure Cosmos DB](https://azure.microsoft.com/services/documentdb/ "Azure Cosmos DB") As a repository for hello log and error records (Cosmos DB refers toorecords as documents).</span></span> <span data-ttu-id="2248b-119">Dado que las aplicaciones lógicas de Azure tiene una plantilla estándar para todas las respuestas, no tendríamos toocreate un esquema personalizado.</span><span class="sxs-lookup"><span data-stu-id="2248b-119">Because Azure Logic Apps has a standard template for all responses, we would not have toocreate a custom schema.</span></span> <span data-ttu-id="2248b-120">Podríamos crear una aplicación de API demasiado**insertar** y **consulta** para los registros de error y de registro.</span><span class="sxs-lookup"><span data-stu-id="2248b-120">We could create an API app too**Insert** and **Query** for both error and log records.</span></span> <span data-ttu-id="2248b-121">También podemos definir un esquema para cada una en la aplicación de API de hello.</span><span class="sxs-lookup"><span data-stu-id="2248b-121">We could also define a schema for each within hello API app.</span></span>  

<span data-ttu-id="2248b-122">Otro requisito estaba toopurge registros después de una fecha determinada.</span><span class="sxs-lookup"><span data-stu-id="2248b-122">Another requirement was toopurge records after a certain date.</span></span> <span data-ttu-id="2248b-123">COSMOS DB tiene una propiedad denominada [tiempo tooLive](https://azure.microsoft.com/blog/documentdb-now-supports-time-to-live-ttl/ "tiempo tooLive") (TTL), que permitía tooset una **tiempo tooLive** valor de cada registro o la colección.</span><span class="sxs-lookup"><span data-stu-id="2248b-123">Cosmos DB has a property called [Time tooLive](https://azure.microsoft.com/blog/documentdb-now-supports-time-to-live-ttl/ "Time tooLive") (TTL), which allowed us tooset a **Time tooLive** value for each record or collection.</span></span> <span data-ttu-id="2248b-124">Esta función elimina Hola necesidad toomanually elimine los registros en la base de datos de Cosmos.</span><span class="sxs-lookup"><span data-stu-id="2248b-124">This capability eliminated hello need toomanually delete records in Cosmos DB.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="2248b-125">toocomplete este tutorial, necesita una base de datos de la base de datos de Cosmos toocreate y dos colecciones (registro y errores).</span><span class="sxs-lookup"><span data-stu-id="2248b-125">toocomplete this tutorial, you need toocreate a Cosmos DB database and two collections (Logging and Errors).</span></span>

## <a name="create-hello-logic-app"></a><span data-ttu-id="2248b-126">Crear aplicación de lógica de hello</span><span class="sxs-lookup"><span data-stu-id="2248b-126">Create hello logic app</span></span>

<span data-ttu-id="2248b-127">Hola primer paso es aplicación de lógica de hello toocreate y aplicación Hola abierto en el Diseñador de la lógica de aplicación.</span><span class="sxs-lookup"><span data-stu-id="2248b-127">hello first step is toocreate hello logic app and open hello app in Logic App Designer.</span></span> <span data-ttu-id="2248b-128">En este ejemplo, vamos a usar aplicaciones lógicas primarias y secundarias.</span><span class="sxs-lookup"><span data-stu-id="2248b-128">In this example, we are using parent-child logic apps.</span></span> <span data-ttu-id="2248b-129">Supongamos que ya se ha creado el elemento primario de Hola y va toocreate una aplicación de lógica de secundarios.</span><span class="sxs-lookup"><span data-stu-id="2248b-129">Let's assume that we have already created hello parent and are going toocreate one child logic app.</span></span>

<span data-ttu-id="2248b-130">Dado que vamos a registro de hello toolog que salen de Dynamics CRM Online, puede empezar en la parte superior de Hola.</span><span class="sxs-lookup"><span data-stu-id="2248b-130">Because we are going toolog hello record coming out of Dynamics CRM Online, let's start at hello top.</span></span> <span data-ttu-id="2248b-131">Debemos usar un **solicitar** desencadenador porque la aplicación lógica de hello primario desencadena este elemento secundario.</span><span class="sxs-lookup"><span data-stu-id="2248b-131">We must use a **Request** trigger because hello parent logic app triggers this child.</span></span>

### <a name="logic-app-trigger"></a><span data-ttu-id="2248b-132">Desencadenador de aplicación lógica</span><span class="sxs-lookup"><span data-stu-id="2248b-132">Logic app trigger</span></span>

<span data-ttu-id="2248b-133">Estamos usando un **solicitar** desencadenar tal y como se muestra en el siguiente ejemplo de Hola:</span><span class="sxs-lookup"><span data-stu-id="2248b-133">We are using a **Request** trigger as shown in hello following example:</span></span>

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


## <a name="steps"></a><span data-ttu-id="2248b-134">Pasos</span><span class="sxs-lookup"><span data-stu-id="2248b-134">Steps</span></span>

<span data-ttu-id="2248b-135">Debemos registramos origen hello (solicitud) del registro de hello paciente de portal de Dynamics CRM Online Hola.</span><span class="sxs-lookup"><span data-stu-id="2248b-135">We must log hello source (request) of hello patient record from hello Dynamics CRM Online portal.</span></span>

1. <span data-ttu-id="2248b-136">Debemos obtener un registro de nueva cita de Dynamics CRM Online.</span><span class="sxs-lookup"><span data-stu-id="2248b-136">We must get a new appointment record from Dynamics CRM Online.</span></span>

   <span data-ttu-id="2248b-137">desencadenador Hola procedentes de CRM nos ofrece hello **CRM PatentId**, **tipo de registro**, **nuevo o actualizado registro** (nueva o actualizar el valor booleano), y  **SalesforceId**.</span><span class="sxs-lookup"><span data-stu-id="2248b-137">hello trigger coming from CRM provides us with hello **CRM PatentId**, **record type**, **New or Updated Record** (new or update Boolean value), and **SalesforceId**.</span></span> <span data-ttu-id="2248b-138">Hola **SalesforceId** puede ser null porque solo se usa para una actualización.</span><span class="sxs-lookup"><span data-stu-id="2248b-138">hello **SalesforceId** can be null because it's only used for an update.</span></span>
   <span data-ttu-id="2248b-139">Obtenemos registro de hello CRM mediante el uso de hello CRM **PatientID** hello y **tipo de registro**.</span><span class="sxs-lookup"><span data-stu-id="2248b-139">We get hello CRM record by using hello CRM **PatientID** and hello **Record Type**.</span></span>

2. <span data-ttu-id="2248b-140">A continuación, necesitamos tooadd nuestra aplicación de API de DocumentDB **InsertLogEntry** operación tal y como se muestra en el Diseñador de la lógica de aplicación.</span><span class="sxs-lookup"><span data-stu-id="2248b-140">Next, we need tooadd our DocumentDB API app **InsertLogEntry** operation as shown here in Logic App Designer.</span></span>

   <span data-ttu-id="2248b-141">**Inserción de entrada de registro**</span><span class="sxs-lookup"><span data-stu-id="2248b-141">**Insert log entry**</span></span>

   ![Insertar entrada de registro](media/logic-apps-scenario-error-and-exception-handling/lognewpatient.png)

   <span data-ttu-id="2248b-143">**Inserción de entrada de error**</span><span class="sxs-lookup"><span data-stu-id="2248b-143">**Insert error entry**</span></span>

   ![Insertar entrada de registro](media/logic-apps-scenario-error-and-exception-handling/insertlogentry.png)

   <span data-ttu-id="2248b-145">**Comprobación de errores en la creación de registro**</span><span class="sxs-lookup"><span data-stu-id="2248b-145">**Check for create record failure**</span></span>

   ![Condición](media/logic-apps-scenario-error-and-exception-handling/condition.png)

## <a name="logic-app-source-code"></a><span data-ttu-id="2248b-147">Código fuente de la aplicación lógica</span><span class="sxs-lookup"><span data-stu-id="2248b-147">Logic app source code</span></span>

> [!NOTE]
> <span data-ttu-id="2248b-148">Hello en los ejemplos siguientes es solamente ejemplos.</span><span class="sxs-lookup"><span data-stu-id="2248b-148">hello following examples are samples only.</span></span> <span data-ttu-id="2248b-149">Dado que este tutorial se basa en una implementación en producción, Hola valor de un **nodo de origen** no puede mostrar las propiedades que están relacionada tooscheduling una cita. ></span><span class="sxs-lookup"><span data-stu-id="2248b-149">Because this tutorial is based on an implementation now in production, hello value of a **Source Node** might not display properties that are related tooscheduling an appointment.></span></span> 

### <a name="logging"></a><span data-ttu-id="2248b-150">Registro</span><span class="sxs-lookup"><span data-stu-id="2248b-150">Logging</span></span>

<span data-ttu-id="2248b-151">Hola después del código de aplicación lógica de ejemplo se muestra cómo toohandle el registro.</span><span class="sxs-lookup"><span data-stu-id="2248b-151">hello following logic app code sample shows how toohandle logging.</span></span>

#### <a name="log-entry"></a><span data-ttu-id="2248b-152">Entrada de registro</span><span class="sxs-lookup"><span data-stu-id="2248b-152">Log entry</span></span>

<span data-ttu-id="2248b-153">Este es el código fuente de la aplicación de la lógica Hola para insertar una entrada de registro.</span><span class="sxs-lookup"><span data-stu-id="2248b-153">Here is hello logic app source code for inserting a log entry.</span></span>

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

#### <a name="log-request"></a><span data-ttu-id="2248b-154">Solicitud de registro</span><span class="sxs-lookup"><span data-stu-id="2248b-154">Log request</span></span>

<span data-ttu-id="2248b-155">Este es el mensaje de solicitud de registro de hello registrado la aplicación de API de toohello.</span><span class="sxs-lookup"><span data-stu-id="2248b-155">Here is hello log request message posted toohello API app.</span></span>

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


#### <a name="log-response"></a><span data-ttu-id="2248b-156">Respuesta de registro</span><span class="sxs-lookup"><span data-stu-id="2248b-156">Log response</span></span>

<span data-ttu-id="2248b-157">Este es el mensaje de respuesta de registro de hello de aplicación de API de hello.</span><span class="sxs-lookup"><span data-stu-id="2248b-157">Here is hello log response message from hello API app.</span></span>

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

<span data-ttu-id="2248b-158">Ahora Echemos un vistazo a los pasos de control de errores de Hola.</span><span class="sxs-lookup"><span data-stu-id="2248b-158">Now let's look at hello error handling steps.</span></span>

### <a name="error-handling"></a><span data-ttu-id="2248b-159">Control de errores</span><span class="sxs-lookup"><span data-stu-id="2248b-159">Error handling</span></span>

<span data-ttu-id="2248b-160">Hello siguiente ejemplo de código de aplicación lógica muestra cómo puede implementar el control de errores.</span><span class="sxs-lookup"><span data-stu-id="2248b-160">hello following logic app code sample shows how you can implement error handling.</span></span>

#### <a name="create-error-record"></a><span data-ttu-id="2248b-161">Creación de un registro de errores</span><span class="sxs-lookup"><span data-stu-id="2248b-161">Create error record</span></span>

<span data-ttu-id="2248b-162">Este es el código fuente de la aplicación de la lógica Hola para crear un registro de error.</span><span class="sxs-lookup"><span data-stu-id="2248b-162">Here is hello logic app source code for creating an error record.</span></span>

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

#### <a name="insert-error-into-cosmos-db--request"></a><span data-ttu-id="2248b-163">Insertar error en Cosmos DB: solicitud</span><span class="sxs-lookup"><span data-stu-id="2248b-163">Insert error into Cosmos DB--request</span></span>

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

#### <a name="insert-error-into-cosmos-db--response"></a><span data-ttu-id="2248b-164">Insertar error en Cosmos DB: respuesta</span><span class="sxs-lookup"><span data-stu-id="2248b-164">Insert error into Cosmos DB--response</span></span>

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

#### <a name="salesforce-error-response"></a><span data-ttu-id="2248b-165">Respuesta de error de Salesforce</span><span class="sxs-lookup"><span data-stu-id="2248b-165">Salesforce error response</span></span>

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

### <a name="return-hello-response-back-tooparent-logic-app"></a><span data-ttu-id="2248b-166">Devolver la aplicación de lógica de hello respuesta tooparent atrás</span><span class="sxs-lookup"><span data-stu-id="2248b-166">Return hello response back tooparent logic app</span></span>

<span data-ttu-id="2248b-167">Después de obtener respuesta de hello, puede pasar la respuesta de hello aplicación lógica de retroceso toohello primario.</span><span class="sxs-lookup"><span data-stu-id="2248b-167">After you get hello response, you can pass hello response back toohello parent logic app.</span></span>

#### <a name="return-success-response-tooparent-logic-app"></a><span data-ttu-id="2248b-168">Aplicación de lógica de tooparent de respuesta de éxito de valor devuelto</span><span class="sxs-lookup"><span data-stu-id="2248b-168">Return success response tooparent logic app</span></span>

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

#### <a name="return-error-response-tooparent-logic-app"></a><span data-ttu-id="2248b-169">Aplicación de lógica de tooparent de respuesta de error de retorno</span><span class="sxs-lookup"><span data-stu-id="2248b-169">Return error response tooparent logic app</span></span>

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


## <a name="cosmos-db-repository-and-portal"></a><span data-ttu-id="2248b-170">Portal y repositorio de Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="2248b-170">Cosmos DB repository and portal</span></span>

<span data-ttu-id="2248b-171">Nuestra solución agregó funcionalidades con [Cosmos DB](https://azure.microsoft.com/services/documentdb).</span><span class="sxs-lookup"><span data-stu-id="2248b-171">Our solution added capabilities with [Cosmos DB](https://azure.microsoft.com/services/documentdb).</span></span>

### <a name="error-management-portal"></a><span data-ttu-id="2248b-172">Portal de administración de errores</span><span class="sxs-lookup"><span data-stu-id="2248b-172">Error management portal</span></span>

<span data-ttu-id="2248b-173">errores de hello tooview, puede crear un registros de error MVC web app toodisplay Hola de base de datos de Cosmos.</span><span class="sxs-lookup"><span data-stu-id="2248b-173">tooview hello errors, you can create an MVC web app toodisplay hello error records from Cosmos DB.</span></span> <span data-ttu-id="2248b-174">Hola **lista**, **detalles**, **editar**, y **eliminar** operaciones se incluyen en la versión actual de Hola.</span><span class="sxs-lookup"><span data-stu-id="2248b-174">hello **List**, **Details**, **Edit**, and **Delete** operations are included in hello current version.</span></span>

> [!NOTE]
> <span data-ttu-id="2248b-175">Operación de edición: Cosmos DB reemplaza todo el documento Hola.</span><span class="sxs-lookup"><span data-stu-id="2248b-175">Edit operation: Cosmos DB replaces hello entire document.</span></span> <span data-ttu-id="2248b-176">Hola registros mostrados en hello **lista** y **detalle** vistas son solamente ejemplos.</span><span class="sxs-lookup"><span data-stu-id="2248b-176">hello records shown in hello **List** and **Detail** views are samples only.</span></span> <span data-ttu-id="2248b-177">No son registros reales de citas de pacientes.</span><span class="sxs-lookup"><span data-stu-id="2248b-177">They are not actual patient appointment records.</span></span>

<span data-ttu-id="2248b-178">Estos son ejemplos de nuestra aplicación MVC detalles creados previamente con hello describen enfoque.</span><span class="sxs-lookup"><span data-stu-id="2248b-178">Here are examples of our MVC app details created with hello previously described approach.</span></span>

#### <a name="error-management-list"></a><span data-ttu-id="2248b-179">Lista de administración de errores</span><span class="sxs-lookup"><span data-stu-id="2248b-179">Error management list</span></span>
![Lista de errores](media/logic-apps-scenario-error-and-exception-handling/errorlist.png)

#### <a name="error-management-detail-view"></a><span data-ttu-id="2248b-181">Vista de detalles de administración de errores</span><span class="sxs-lookup"><span data-stu-id="2248b-181">Error management detail view</span></span>
![Detalles del error](media/logic-apps-scenario-error-and-exception-handling/errordetails.png)

### <a name="log-management-portal"></a><span data-ttu-id="2248b-183">Portal de administración de registros</span><span class="sxs-lookup"><span data-stu-id="2248b-183">Log management portal</span></span>

<span data-ttu-id="2248b-184">registros de hello tooview, también creamos una aplicación web MVC.</span><span class="sxs-lookup"><span data-stu-id="2248b-184">tooview hello logs, we also created an MVC web app.</span></span> <span data-ttu-id="2248b-185">Estos son ejemplos de nuestra aplicación MVC detalles creados previamente con hello describen enfoque.</span><span class="sxs-lookup"><span data-stu-id="2248b-185">Here are examples of our MVC app details created with hello previously described approach.</span></span>

#### <a name="sample-log-detail-view"></a><span data-ttu-id="2248b-186">Vista de detalles del registro de ejemplo</span><span class="sxs-lookup"><span data-stu-id="2248b-186">Sample log detail view</span></span>
![Vista de detalles del registro](media/logic-apps-scenario-error-and-exception-handling/samplelogdetail.png)

### <a name="api-app-details"></a><span data-ttu-id="2248b-188">Detalles de la aplicación de API</span><span class="sxs-lookup"><span data-stu-id="2248b-188">API app details</span></span>

#### <a name="logic-apps-exception-management-api"></a><span data-ttu-id="2248b-189">API de administración de excepciones de Logic Apps</span><span class="sxs-lookup"><span data-stu-id="2248b-189">Logic Apps exception management API</span></span>

<span data-ttu-id="2248b-190">Nuestra aplicación de API de administración de excepciones de Azure Logic Apps, de código abierto, proporciona la funcionalidad que se describe aquí. Hay dos controladores:</span><span class="sxs-lookup"><span data-stu-id="2248b-190">Our open-source Azure Logic Apps exception management API app provides functionality as described here - there are two controllers:</span></span>

* <span data-ttu-id="2248b-191">**ErrorController** inserta un registro de error (documento) en una colección de DocumentDB.</span><span class="sxs-lookup"><span data-stu-id="2248b-191">**ErrorController** inserts an error record (document) in a DocumentDB collection.</span></span>
* <span data-ttu-id="2248b-192">**LogController** inserta una entrada de registro (documento) en una colección de DocumentDB.</span><span class="sxs-lookup"><span data-stu-id="2248b-192">**LogController** Inserts a log record (document) in a DocumentDB collection.</span></span>

> [!TIP]
> <span data-ttu-id="2248b-193">Usan ambos controladores `async Task<dynamic>` Hola de operaciones, lo que permite operaciones tooresolve en tiempo de ejecución, por lo que podemos crear documentos de esquema en el cuerpo de Hola de operación de Hola.</span><span class="sxs-lookup"><span data-stu-id="2248b-193">Both controllers use `async Task<dynamic>` operations, allowing operations tooresolve at runtime, so we can create hello DocumentDB schema in hello body of hello operation.</span></span> 
> 

<span data-ttu-id="2248b-194">Todos los documentos de DocumentDB deben tener un identificador único.</span><span class="sxs-lookup"><span data-stu-id="2248b-194">Every document in DocumentDB must have a unique ID.</span></span> <span data-ttu-id="2248b-195">Estamos usando `PatientId` y agregar una marca de tiempo que sea convertir el valor de marca de tiempo de Unix tooa (double).</span><span class="sxs-lookup"><span data-stu-id="2248b-195">We are using `PatientId` and adding a timestamp that is converted tooa Unix timestamp value (double).</span></span> <span data-ttu-id="2248b-196">Se trunca hello tooremove Hola fracciones valor.</span><span class="sxs-lookup"><span data-stu-id="2248b-196">We truncate hello value tooremove hello fractional value.</span></span>

<span data-ttu-id="2248b-197">Puede ver código fuente de Hola de nuestro controlador de error API [desde GitHub](https://github.com/HEDIDIN/LogicAppsExceptionManagementApi/blob/master/Logic App Exception Management API/Controllers/ErrorController.cs).</span><span class="sxs-lookup"><span data-stu-id="2248b-197">You can view hello source code of our error controller API [from GitHub](https://github.com/HEDIDIN/LogicAppsExceptionManagementApi/blob/master/Logic App Exception Management API/Controllers/ErrorController.cs).</span></span>

<span data-ttu-id="2248b-198">Llamamos a Hola API desde una aplicación de lógica mediante el uso de hello según la sintaxis:</span><span class="sxs-lookup"><span data-stu-id="2248b-198">We call hello API from a logic app by using hello following syntax:</span></span>

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

<span data-ttu-id="2248b-199">Hola expresión Hola anteriores comprobaciones de ejemplo de código de hello *Create_NewPatientRecord* estado de **error**.</span><span class="sxs-lookup"><span data-stu-id="2248b-199">hello expression in hello preceding code sample checks for hello *Create_NewPatientRecord* status of **Failed**.</span></span>

## <a name="summary"></a><span data-ttu-id="2248b-200">Resumen</span><span class="sxs-lookup"><span data-stu-id="2248b-200">Summary</span></span>

* <span data-ttu-id="2248b-201">Puede implementar fácilmente el registro y control de errores en una aplicación lógica.</span><span class="sxs-lookup"><span data-stu-id="2248b-201">You can easily implement logging and error handling in a logic app.</span></span>
* <span data-ttu-id="2248b-202">Puede usar documentos como repositorio de Hola para los registros de error y registro (documentos).</span><span class="sxs-lookup"><span data-stu-id="2248b-202">You can use DocumentDB as hello repository for log and error records (documents).</span></span>
* <span data-ttu-id="2248b-203">Puede usar MVC toocreate un registro toodisplay portal y registros de error.</span><span class="sxs-lookup"><span data-stu-id="2248b-203">You can use MVC toocreate a portal toodisplay log and error records.</span></span>

### <a name="source-code"></a><span data-ttu-id="2248b-204">Código fuente</span><span class="sxs-lookup"><span data-stu-id="2248b-204">Source code</span></span>

<span data-ttu-id="2248b-205">código de origen de Hola de hello aplicación API de administración de excepción de aplicaciones de lógica está disponible en este [repositorio de GitHub](https://github.com/HEDIDIN/LogicAppsExceptionManagementApi "API de administración de excepciones de aplicación lógica").</span><span class="sxs-lookup"><span data-stu-id="2248b-205">hello source code for hello Logic Apps exception management API application is available in this [GitHub repository](https://github.com/HEDIDIN/LogicAppsExceptionManagementApi "Logic App Exception Management API").</span></span>

## <a name="next-steps"></a><span data-ttu-id="2248b-206">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="2248b-206">Next steps</span></span>

* [<span data-ttu-id="2248b-207">Ver más ejemplos y escenarios de aplicaciones Logic Apps</span><span class="sxs-lookup"><span data-stu-id="2248b-207">View more logic app examples and scenarios</span></span>](../logic-apps/logic-apps-examples-and-scenarios.md)
* [<span data-ttu-id="2248b-208">Obtener más información sobre supervisión de Logic Apps</span><span class="sxs-lookup"><span data-stu-id="2248b-208">Learn about monitoring logic apps</span></span>](../logic-apps/logic-apps-monitor-your-logic-apps.md)
* [<span data-ttu-id="2248b-209">Creación de plantillas de implementación automatizadas de Logic Apps</span><span class="sxs-lookup"><span data-stu-id="2248b-209">Create automated deployment templates for logic apps</span></span>](../logic-apps/logic-apps-create-deploy-template.md)
