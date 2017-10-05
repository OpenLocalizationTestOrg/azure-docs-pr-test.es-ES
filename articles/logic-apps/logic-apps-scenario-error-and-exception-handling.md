---
title: 'Escenario de control de excepciones y registro de errores: Azure Logic Apps | Microsoft Docs'
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
ms.openlocfilehash: 044de27c75da93c95609110d2b73336c42f746fe
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="scenario-exception-handling-and-error-logging-for-logic-apps"></a><span data-ttu-id="c9cbb-103">Escenario: control de excepciones y registro de errores para aplicaciones lógicas</span><span class="sxs-lookup"><span data-stu-id="c9cbb-103">Scenario: Exception handling and error logging for logic apps</span></span>

<span data-ttu-id="c9cbb-104">En este escenario se describe cómo extender una aplicación lógica para controlar mejor las excepciones.</span><span class="sxs-lookup"><span data-stu-id="c9cbb-104">This scenario describes how you can extend a logic app to better support exception handling.</span></span> <span data-ttu-id="c9cbb-105">Hemos usado un caso de uso real para responder a la pregunta: ¿Admite Azure Logic Apps control de excepciones y errores?</span><span class="sxs-lookup"><span data-stu-id="c9cbb-105">We've used a real-life use case to answer the question: "Does Azure Logic Apps support exception and error handling?"</span></span>

> [!NOTE]
> <span data-ttu-id="c9cbb-106">El esquema actual de Azure Logic Apps proporciona una plantilla estándar para las respuestas de acción.</span><span class="sxs-lookup"><span data-stu-id="c9cbb-106">The current Azure Logic Apps schema provides a standard template for action responses.</span></span> <span data-ttu-id="c9cbb-107">Esta incluye la validación interna y las respuestas de error devueltas desde una aplicación de API.</span><span class="sxs-lookup"><span data-stu-id="c9cbb-107">This template includes both internal validation and error responses returned from an API app.</span></span>

## <a name="scenario-and-use-case-overview"></a><span data-ttu-id="c9cbb-108">Información general de escenarios y casos de uso</span><span class="sxs-lookup"><span data-stu-id="c9cbb-108">Scenario and use case overview</span></span>

<span data-ttu-id="c9cbb-109">Esta es la historia del caso de uso de este escenario:</span><span class="sxs-lookup"><span data-stu-id="c9cbb-109">Here's the story as the use case for this scenario:</span></span> 

<span data-ttu-id="c9cbb-110">Una conocida organización sanitaria nos contrató para que desarrolláramos una solución de Azure que crearía un portal para pacientes mediante Microsoft Dynamics CRM Online.</span><span class="sxs-lookup"><span data-stu-id="c9cbb-110">A well-known healthcare organization engaged us to develop an Azure solution that would create a patient portal by using Microsoft Dynamics CRM Online.</span></span> <span data-ttu-id="c9cbb-111">Necesitaban enviar registros de citas entre el portal para pacientes de Dynamics CRM Online y Salesforce.</span><span class="sxs-lookup"><span data-stu-id="c9cbb-111">They needed to send appointment records between the Dynamics CRM Online patient portal and Salesforce.</span></span> <span data-ttu-id="c9cbb-112">Se nos pidió que usáramos la norma [FHIR HL7](http://www.hl7.org/implement/standards/fhir/) para todos los registros de paciente.</span><span class="sxs-lookup"><span data-stu-id="c9cbb-112">We were asked to use the [HL7 FHIR](http://www.hl7.org/implement/standards/fhir/) standard for all patient records.</span></span>

<span data-ttu-id="c9cbb-113">El proyecto tenía dos requisitos principales:</span><span class="sxs-lookup"><span data-stu-id="c9cbb-113">The project had two major requirements:</span></span>  

* <span data-ttu-id="c9cbb-114">Un método para registrar las entradas enviadas desde el portal de Dynamics CRM Online</span><span class="sxs-lookup"><span data-stu-id="c9cbb-114">A method to log records sent from the Dynamics CRM Online portal</span></span>
* <span data-ttu-id="c9cbb-115">Una manera de ver todos los errores que se producían dentro del flujo de trabajo.</span><span class="sxs-lookup"><span data-stu-id="c9cbb-115">A way to view any errors that occurred within the workflow</span></span>

> [!TIP]
> <span data-ttu-id="c9cbb-116">Para ver un vídeo de alto nivel sobre este proyecto, vea [Integration User Group](http://www.integrationusergroup.com/logic-apps-support-error-handling/ "Integration User Group").</span><span class="sxs-lookup"><span data-stu-id="c9cbb-116">For a high-level video about this project, see [Integration User Group](http://www.integrationusergroup.com/logic-apps-support-error-handling/ "Integration User Group").</span></span>

## <a name="how-we-solved-the-problem"></a><span data-ttu-id="c9cbb-117">¿Cómo resolvimos el problema?</span><span class="sxs-lookup"><span data-stu-id="c9cbb-117">How we solved the problem</span></span>

<span data-ttu-id="c9cbb-118">Elegimos [Azure Cosmos DB](https://azure.microsoft.com/services/documentdb/ "Azure Cosmos DB") como repositorio para los registros y entradas de error (Cosmos DB hace referencia a los registros como documentos).</span><span class="sxs-lookup"><span data-stu-id="c9cbb-118">We chose [Azure Cosmos DB](https://azure.microsoft.com/services/documentdb/ "Azure Cosmos DB") As a repository for the log and error records (Cosmos DB refers to records as documents).</span></span> <span data-ttu-id="c9cbb-119">Puesto que Azure Logic Apps tiene una plantilla estándar para todas las respuestas, no sería necesario crear un esquema personalizado.</span><span class="sxs-lookup"><span data-stu-id="c9cbb-119">Because Azure Logic Apps has a standard template for all responses, we would not have to create a custom schema.</span></span> <span data-ttu-id="c9cbb-120">Podíamos crear una aplicación de API para **insertar** y **consultar** registros de errores y registros.</span><span class="sxs-lookup"><span data-stu-id="c9cbb-120">We could create an API app to **Insert** and **Query** for both error and log records.</span></span> <span data-ttu-id="c9cbb-121">También podíamos definir un esquema para cada uno de ellos dentro de la aplicación de API.</span><span class="sxs-lookup"><span data-stu-id="c9cbb-121">We could also define a schema for each within the API app.</span></span>  

<span data-ttu-id="c9cbb-122">Otro requisito era que se purgaran los registros después de una determinada fecha.</span><span class="sxs-lookup"><span data-stu-id="c9cbb-122">Another requirement was to purge records after a certain date.</span></span> <span data-ttu-id="c9cbb-123">Cosmos DB presenta una propiedad llamada [período de vida](https://azure.microsoft.com/blog/documentdb-now-supports-time-to-live-ttl/ "período de vida") (TTL), que nos permitió establecer un valor de **período de vida** para cada registro o colección.</span><span class="sxs-lookup"><span data-stu-id="c9cbb-123">Cosmos DB has a property called [Time to Live](https://azure.microsoft.com/blog/documentdb-now-supports-time-to-live-ttl/ "Time to Live") (TTL), which allowed us to set a **Time to Live** value for each record or collection.</span></span> <span data-ttu-id="c9cbb-124">Esta capacidad suprimía la necesidad de eliminar manualmente los registros en Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="c9cbb-124">This capability eliminated the need to manually delete records in Cosmos DB.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="c9cbb-125">Para completar este tutorial, debe crear una base de datos de Cosmos DB y dos colecciones (Registro y Errores).</span><span class="sxs-lookup"><span data-stu-id="c9cbb-125">To complete this tutorial, you need to create a Cosmos DB database and two collections (Logging and Errors).</span></span>

## <a name="create-the-logic-app"></a><span data-ttu-id="c9cbb-126">Creación de la aplicación lógica</span><span class="sxs-lookup"><span data-stu-id="c9cbb-126">Create the logic app</span></span>

<span data-ttu-id="c9cbb-127">El primer paso es crear una aplicación lógica y cargarla en Diseñador de aplicación lógica.</span><span class="sxs-lookup"><span data-stu-id="c9cbb-127">The first step is to create the logic app and open the app in Logic App Designer.</span></span> <span data-ttu-id="c9cbb-128">En este ejemplo, vamos a usar aplicaciones lógicas primarias y secundarias.</span><span class="sxs-lookup"><span data-stu-id="c9cbb-128">In this example, we are using parent-child logic apps.</span></span> <span data-ttu-id="c9cbb-129">Supongamos que ya ha creado la primaria y va a crear una aplicación lógica secundaria.</span><span class="sxs-lookup"><span data-stu-id="c9cbb-129">Let's assume that we have already created the parent and are going to create one child logic app.</span></span>

<span data-ttu-id="c9cbb-130">Puesto que vamos a registrar los registros procedentes de Dynamics CRM Online, vamos a comenzar por lo más importante.</span><span class="sxs-lookup"><span data-stu-id="c9cbb-130">Because we are going to log the record coming out of Dynamics CRM Online, let's start at the top.</span></span> <span data-ttu-id="c9cbb-131">Debemos usar un desencadenador de **solicitud**, ya que la aplicación lógica primaria desencadenará la secundaria.</span><span class="sxs-lookup"><span data-stu-id="c9cbb-131">We must use a **Request** trigger because the parent logic app triggers this child.</span></span>

### <a name="logic-app-trigger"></a><span data-ttu-id="c9cbb-132">Desencadenador de aplicación lógica</span><span class="sxs-lookup"><span data-stu-id="c9cbb-132">Logic app trigger</span></span>

<span data-ttu-id="c9cbb-133">Vamos a usar un desencadenador de **solicitud** tal como se muestra en el ejemplo siguiente:</span><span class="sxs-lookup"><span data-stu-id="c9cbb-133">We are using a **Request** trigger as shown in the following example:</span></span>

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


## <a name="steps"></a><span data-ttu-id="c9cbb-134">Pasos</span><span class="sxs-lookup"><span data-stu-id="c9cbb-134">Steps</span></span>

<span data-ttu-id="c9cbb-135">Es necesario registrar el origen (solicitud) del registro del paciente desde el portal de Dynamics CRM Online.</span><span class="sxs-lookup"><span data-stu-id="c9cbb-135">We must log the source (request) of the patient record from the Dynamics CRM Online portal.</span></span>

1. <span data-ttu-id="c9cbb-136">Debemos obtener un registro de nueva cita de Dynamics CRM Online.</span><span class="sxs-lookup"><span data-stu-id="c9cbb-136">We must get a new appointment record from Dynamics CRM Online.</span></span>

   <span data-ttu-id="c9cbb-137">El desencadenador procedente de CRM nos proporciona los valores de **CRM PatentId**, **record type**, **New or Updated Record** (valor booleano nuevo o actualizado) y **SalesforceId**.</span><span class="sxs-lookup"><span data-stu-id="c9cbb-137">The trigger coming from CRM provides us with the **CRM PatentId**, **record type**, **New or Updated Record** (new or update Boolean value), and **SalesforceId**.</span></span> <span data-ttu-id="c9cbb-138">El valor de **SalesforceId** puede ser null porque solo se utiliza para obtener una actualización.</span><span class="sxs-lookup"><span data-stu-id="c9cbb-138">The **SalesforceId** can be null because it's only used for an update.</span></span>
   <span data-ttu-id="c9cbb-139">Obtenemos el registro de CRM mediante los valores de **PatientID** y **Tipo de registro** de CRM.</span><span class="sxs-lookup"><span data-stu-id="c9cbb-139">We get the CRM record by using the CRM **PatientID** and the **Record Type**.</span></span>

2. <span data-ttu-id="c9cbb-140">A continuación, es necesario agregar a nuestra aplicación de API de DocumentDB la operación **InsertLogEntry**, tal y como se muestra aquí en el Diseñador de aplicaciones lógicas.</span><span class="sxs-lookup"><span data-stu-id="c9cbb-140">Next, we need to add our DocumentDB API app **InsertLogEntry** operation as shown here in Logic App Designer.</span></span>

   <span data-ttu-id="c9cbb-141">**Inserción de entrada de registro**</span><span class="sxs-lookup"><span data-stu-id="c9cbb-141">**Insert log entry**</span></span>

   ![Insertar entrada de registro](media/logic-apps-scenario-error-and-exception-handling/lognewpatient.png)

   <span data-ttu-id="c9cbb-143">**Inserción de entrada de error**</span><span class="sxs-lookup"><span data-stu-id="c9cbb-143">**Insert error entry**</span></span>

   ![Insertar entrada de registro](media/logic-apps-scenario-error-and-exception-handling/insertlogentry.png)

   <span data-ttu-id="c9cbb-145">**Comprobación de errores en la creación de registro**</span><span class="sxs-lookup"><span data-stu-id="c9cbb-145">**Check for create record failure**</span></span>

   ![Condición](media/logic-apps-scenario-error-and-exception-handling/condition.png)

## <a name="logic-app-source-code"></a><span data-ttu-id="c9cbb-147">Código fuente de la aplicación lógica</span><span class="sxs-lookup"><span data-stu-id="c9cbb-147">Logic app source code</span></span>

> [!NOTE]
> <span data-ttu-id="c9cbb-148">Los siguientes ejemplos son solo muestras.</span><span class="sxs-lookup"><span data-stu-id="c9cbb-148">The following examples are samples only.</span></span> <span data-ttu-id="c9cbb-149">Como este tutorial se basa en una implementación actualmente en producción, es posible que el valor de un **nodo de origen** no muestre las propiedades que están relacionadas con la programación de una cita.></span><span class="sxs-lookup"><span data-stu-id="c9cbb-149">Because this tutorial is based on an implementation now in production, the value of a **Source Node** might not display properties that are related to scheduling an appointment.></span></span> 

### <a name="logging"></a><span data-ttu-id="c9cbb-150">Registro</span><span class="sxs-lookup"><span data-stu-id="c9cbb-150">Logging</span></span>

<span data-ttu-id="c9cbb-151">El siguiente ejemplo de código de aplicación lógica muestra cómo controlar el registro.</span><span class="sxs-lookup"><span data-stu-id="c9cbb-151">The following logic app code sample shows how to handle logging.</span></span>

#### <a name="log-entry"></a><span data-ttu-id="c9cbb-152">Entrada de registro</span><span class="sxs-lookup"><span data-stu-id="c9cbb-152">Log entry</span></span>

<span data-ttu-id="c9cbb-153">Este es el código fuente de la aplicación lógica para insertar una entrada de registro.</span><span class="sxs-lookup"><span data-stu-id="c9cbb-153">Here is the logic app source code for inserting a log entry.</span></span>

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

#### <a name="log-request"></a><span data-ttu-id="c9cbb-154">Solicitud de registro</span><span class="sxs-lookup"><span data-stu-id="c9cbb-154">Log request</span></span>

<span data-ttu-id="c9cbb-155">Este es el mensaje de solicitud de registro publicado en la aplicación de API.</span><span class="sxs-lookup"><span data-stu-id="c9cbb-155">Here is the log request message posted to the API app.</span></span>

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


#### <a name="log-response"></a><span data-ttu-id="c9cbb-156">Respuesta de registro</span><span class="sxs-lookup"><span data-stu-id="c9cbb-156">Log response</span></span>

<span data-ttu-id="c9cbb-157">Este es el mensaje de respuesta de registro desde la aplicación de API.</span><span class="sxs-lookup"><span data-stu-id="c9cbb-157">Here is the log response message from the API app.</span></span>

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

<span data-ttu-id="c9cbb-158">Ahora veamos los pasos de control de errores:</span><span class="sxs-lookup"><span data-stu-id="c9cbb-158">Now let's look at the error handling steps.</span></span>

### <a name="error-handling"></a><span data-ttu-id="c9cbb-159">Control de errores</span><span class="sxs-lookup"><span data-stu-id="c9cbb-159">Error handling</span></span>

<span data-ttu-id="c9cbb-160">El siguiente ejemplo de código de aplicación lógica muestra cómo puede implementar el control de errores.</span><span class="sxs-lookup"><span data-stu-id="c9cbb-160">The following logic app code sample shows how you can implement error handling.</span></span>

#### <a name="create-error-record"></a><span data-ttu-id="c9cbb-161">Creación de un registro de errores</span><span class="sxs-lookup"><span data-stu-id="c9cbb-161">Create error record</span></span>

<span data-ttu-id="c9cbb-162">Este es el código fuente de la aplicación lógica para crear un registro de errores.</span><span class="sxs-lookup"><span data-stu-id="c9cbb-162">Here is the logic app source code for creating an error record.</span></span>

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

#### <a name="insert-error-into-cosmos-db--request"></a><span data-ttu-id="c9cbb-163">Insertar error en Cosmos DB: solicitud</span><span class="sxs-lookup"><span data-stu-id="c9cbb-163">Insert error into Cosmos DB--request</span></span>

``` json

{
    "uri": "https://.../api/CrMtoSfError",
    "method": "post",
    "body": {
        "action": "New_Patient",
        "isError": true,
        "crmId": "6b115f6d-a7ee-e511-80f5-3863bb2eb2d0",
        "patientId": "6b115f6d-a7ee-e511-80f5-3863bb2eb2d0",
        "message": "Salesforce failed to complete task: Message: duplicate value found: Account_ID_MED__c duplicates value on record with id: 001U000001c83gK",
        "providerId": "",
        "severity": 4,
        "salesforceId": "",
        "update": false,
        "source": "{/"Account_Class_vod__c/":/"PRAC/",/"Account_Status_MED__c/":/"I/",/"CRM_HUB_ID__c/":/"6b115f6d-a7ee-e511-80f5-3863bb2eb2d0/",/"Credentials_vod__c/",/"DTC_ID_MED__c/":/"/",/"Fax/":/"/",/"FirstName/":/"A/",/"Gender_vod__c/":/"/",/"IMS_ID__c/":/"/",/"LastName/":/"BAILEY/",/"MasterID_mp__c/":/"/",/"C_ID_MED__c/":/"851588/",/"Middle_vod__c/":/"/",/"NPI_vod__c/":/"/",/"PDRP_MED__c/":false,/"PersonDoNotCall/":false,/"PersonEmail/":/"/",/"PersonHasOptedOutOfEmail/":false,/"PersonHasOptedOutOfFax/":false,/"PersonMobilePhone/":/"/",/"Phone/":/"/",/"Practicing_Specialty__c/":/"FM - FAMILY MEDICINE/",/"Primary_City__c/":/"/",/"Primary_State__c/":/"/",/"Primary_Street_Line2__c/":/"/",/"Primary_Street__c/":/"/",/"Primary_Zip__c/":/"/",/"RecordTypeId/":/"012U0000000JaPWIA0/",/"Request_Date__c/":/"2016-06-10T22:31:55.9647467Z/",/"ONY_ID__c/":/"/",/"Specialty_1_vod__c/":/"/",/"Suffix_vod__c/":/"/",/"Website/":/"/"}",
        "statusCode": "400"
    }
}
```

#### <a name="insert-error-into-cosmos-db--response"></a><span data-ttu-id="c9cbb-164">Insertar error en Cosmos DB: respuesta</span><span class="sxs-lookup"><span data-stu-id="c9cbb-164">Insert error into Cosmos DB--response</span></span>

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
        "body": "CRM failed to complete task: Message: duplicate value found: CRM_HUB_ID__c duplicates value on record with id: 001U000001c83gK",
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

#### <a name="salesforce-error-response"></a><span data-ttu-id="c9cbb-165">Respuesta de error de Salesforce</span><span class="sxs-lookup"><span data-stu-id="c9cbb-165">Salesforce error response</span></span>

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
        "message": "Salesforce failed to complete task: Message: duplicate value found: Account_ID_MED__c duplicates value on record with id: 001U000001c83gK",
        "source": "Salesforce.Common",
        "errors": []
    }
}

```

### <a name="return-the-response-back-to-parent-logic-app"></a><span data-ttu-id="c9cbb-166">Devolución de la respuesta a la aplicación lógica primaria</span><span class="sxs-lookup"><span data-stu-id="c9cbb-166">Return the response back to parent logic app</span></span>

<span data-ttu-id="c9cbb-167">Una vez que obtiene la respuesta, puede pasarla a la aplicación lógica primaria.</span><span class="sxs-lookup"><span data-stu-id="c9cbb-167">After you get the response, you can pass the response back to the parent logic app.</span></span>

#### <a name="return-success-response-to-parent-logic-app"></a><span data-ttu-id="c9cbb-168">Devolución de respuesta satisfactoria a la aplicación lógica primaria</span><span class="sxs-lookup"><span data-stu-id="c9cbb-168">Return success response to parent logic app</span></span>

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

#### <a name="return-error-response-to-parent-logic-app"></a><span data-ttu-id="c9cbb-169">Devolución de respuesta de error a la aplicación lógica primaria</span><span class="sxs-lookup"><span data-stu-id="c9cbb-169">Return error response to parent logic app</span></span>

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


## <a name="cosmos-db-repository-and-portal"></a><span data-ttu-id="c9cbb-170">Portal y repositorio de Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="c9cbb-170">Cosmos DB repository and portal</span></span>

<span data-ttu-id="c9cbb-171">Nuestra solución agregó funcionalidades con [Cosmos DB](https://azure.microsoft.com/services/documentdb).</span><span class="sxs-lookup"><span data-stu-id="c9cbb-171">Our solution added capabilities with [Cosmos DB](https://azure.microsoft.com/services/documentdb).</span></span>

### <a name="error-management-portal"></a><span data-ttu-id="c9cbb-172">Portal de administración de errores</span><span class="sxs-lookup"><span data-stu-id="c9cbb-172">Error management portal</span></span>

<span data-ttu-id="c9cbb-173">Para ver los errores, puede crear una aplicación web de MVC que muestre los registros de error de Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="c9cbb-173">To view the errors, you can create an MVC web app to display the error records from Cosmos DB.</span></span> <span data-ttu-id="c9cbb-174">En la versión actual, se incluyen las operaciones de **lista**, **detalles**, **edición** y **eliminación**.</span><span class="sxs-lookup"><span data-stu-id="c9cbb-174">The **List**, **Details**, **Edit**, and **Delete** operations are included in the current version.</span></span>

> [!NOTE]
> <span data-ttu-id="c9cbb-175">Operación de edición: Cosmos DB reemplaza todo el documento.</span><span class="sxs-lookup"><span data-stu-id="c9cbb-175">Edit operation: Cosmos DB replaces the entire document.</span></span> <span data-ttu-id="c9cbb-176">Los registros que se muestran en las vistas de **lista** y **detalles** son solo ejemplos.</span><span class="sxs-lookup"><span data-stu-id="c9cbb-176">The records shown in the **List** and **Detail** views are samples only.</span></span> <span data-ttu-id="c9cbb-177">No son registros reales de citas de pacientes.</span><span class="sxs-lookup"><span data-stu-id="c9cbb-177">They are not actual patient appointment records.</span></span>

<span data-ttu-id="c9cbb-178">Aquí puede ver ejemplos de nuestros detalles de la aplicación de MVC creados con el enfoque descrito anteriormente.</span><span class="sxs-lookup"><span data-stu-id="c9cbb-178">Here are examples of our MVC app details created with the previously described approach.</span></span>

#### <a name="error-management-list"></a><span data-ttu-id="c9cbb-179">Lista de administración de errores</span><span class="sxs-lookup"><span data-stu-id="c9cbb-179">Error management list</span></span>
![Lista de errores](media/logic-apps-scenario-error-and-exception-handling/errorlist.png)

#### <a name="error-management-detail-view"></a><span data-ttu-id="c9cbb-181">Vista de detalles de administración de errores</span><span class="sxs-lookup"><span data-stu-id="c9cbb-181">Error management detail view</span></span>
![Detalles del error](media/logic-apps-scenario-error-and-exception-handling/errordetails.png)

### <a name="log-management-portal"></a><span data-ttu-id="c9cbb-183">Portal de administración de registros</span><span class="sxs-lookup"><span data-stu-id="c9cbb-183">Log management portal</span></span>

<span data-ttu-id="c9cbb-184">Para ver los registros, también creamos una aplicación web de MVC.</span><span class="sxs-lookup"><span data-stu-id="c9cbb-184">To view the logs, we also created an MVC web app.</span></span> <span data-ttu-id="c9cbb-185">Aquí puede ver ejemplos de nuestros detalles de la aplicación de MVC creados con el enfoque descrito anteriormente.</span><span class="sxs-lookup"><span data-stu-id="c9cbb-185">Here are examples of our MVC app details created with the previously described approach.</span></span>

#### <a name="sample-log-detail-view"></a><span data-ttu-id="c9cbb-186">Vista de detalles del registro de ejemplo</span><span class="sxs-lookup"><span data-stu-id="c9cbb-186">Sample log detail view</span></span>
![Vista de detalles del registro](media/logic-apps-scenario-error-and-exception-handling/samplelogdetail.png)

### <a name="api-app-details"></a><span data-ttu-id="c9cbb-188">Detalles de la aplicación de API</span><span class="sxs-lookup"><span data-stu-id="c9cbb-188">API app details</span></span>

#### <a name="logic-apps-exception-management-api"></a><span data-ttu-id="c9cbb-189">API de administración de excepciones de Logic Apps</span><span class="sxs-lookup"><span data-stu-id="c9cbb-189">Logic Apps exception management API</span></span>

<span data-ttu-id="c9cbb-190">Nuestra aplicación de API de administración de excepciones de Azure Logic Apps, de código abierto, proporciona la funcionalidad que se describe aquí. Hay dos controladores:</span><span class="sxs-lookup"><span data-stu-id="c9cbb-190">Our open-source Azure Logic Apps exception management API app provides functionality as described here - there are two controllers:</span></span>

* <span data-ttu-id="c9cbb-191">**ErrorController** inserta un registro de error (documento) en una colección de DocumentDB.</span><span class="sxs-lookup"><span data-stu-id="c9cbb-191">**ErrorController** inserts an error record (document) in a DocumentDB collection.</span></span>
* <span data-ttu-id="c9cbb-192">**LogController** inserta una entrada de registro (documento) en una colección de DocumentDB.</span><span class="sxs-lookup"><span data-stu-id="c9cbb-192">**LogController** Inserts a log record (document) in a DocumentDB collection.</span></span>

> [!TIP]
> <span data-ttu-id="c9cbb-193">Ambos controladores usan operaciones `async Task<dynamic>`, que permiten que las operaciones se resuelvan en tiempo de ejecución, por lo que podemos crear el esquema de DocumentDB en el cuerpo de la operación.</span><span class="sxs-lookup"><span data-stu-id="c9cbb-193">Both controllers use `async Task<dynamic>` operations, allowing operations to resolve at runtime, so we can create the DocumentDB schema in the body of the operation.</span></span> 
> 

<span data-ttu-id="c9cbb-194">Todos los documentos de DocumentDB deben tener un identificador único.</span><span class="sxs-lookup"><span data-stu-id="c9cbb-194">Every document in DocumentDB must have a unique ID.</span></span> <span data-ttu-id="c9cbb-195">Vamos a utilizar `PatientId` y a agregar una marca de tiempo que se convertirá en un valor de marca de tiempo de Unix (doble).</span><span class="sxs-lookup"><span data-stu-id="c9cbb-195">We are using `PatientId` and adding a timestamp that is converted to a Unix timestamp value (double).</span></span> <span data-ttu-id="c9cbb-196">Se trunca el valor para quitar el valor fraccionario.</span><span class="sxs-lookup"><span data-stu-id="c9cbb-196">We truncate the value to remove the fractional value.</span></span>

<span data-ttu-id="c9cbb-197">El código fuente de la API de nuestro controlador de error se puede ver [desde GitHub](https://github.com/HEDIDIN/LogicAppsExceptionManagementApi/blob/master/Logic App Exception Management API/Controllers/ErrorController.cs).</span><span class="sxs-lookup"><span data-stu-id="c9cbb-197">You can view the source code of our error controller API [from GitHub](https://github.com/HEDIDIN/LogicAppsExceptionManagementApi/blob/master/Logic App Exception Management API/Controllers/ErrorController.cs).</span></span>

<span data-ttu-id="c9cbb-198">Llamamos a la API desde una aplicación lógica mediante la sintaxis siguiente:</span><span class="sxs-lookup"><span data-stu-id="c9cbb-198">We call the API from a logic app by using the following syntax:</span></span>

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

<span data-ttu-id="c9cbb-199">La expresión del ejemplo de código anterior buscará el estado **Error** para *Create_NewPatientRecord*.</span><span class="sxs-lookup"><span data-stu-id="c9cbb-199">The expression in the preceding code sample checks for the *Create_NewPatientRecord* status of **Failed**.</span></span>

## <a name="summary"></a><span data-ttu-id="c9cbb-200">Resumen</span><span class="sxs-lookup"><span data-stu-id="c9cbb-200">Summary</span></span>

* <span data-ttu-id="c9cbb-201">Puede implementar fácilmente el registro y control de errores en una aplicación lógica.</span><span class="sxs-lookup"><span data-stu-id="c9cbb-201">You can easily implement logging and error handling in a logic app.</span></span>
* <span data-ttu-id="c9cbb-202">Puede usar DocumentDB como repositorio para entradas de registro y registros de error (documentos).</span><span class="sxs-lookup"><span data-stu-id="c9cbb-202">You can use DocumentDB as the repository for log and error records (documents).</span></span>
* <span data-ttu-id="c9cbb-203">Puede usar MVC para crear un portal que muestre las entradas de registro y los registros de error.</span><span class="sxs-lookup"><span data-stu-id="c9cbb-203">You can use MVC to create a portal to display log and error records.</span></span>

### <a name="source-code"></a><span data-ttu-id="c9cbb-204">Código fuente</span><span class="sxs-lookup"><span data-stu-id="c9cbb-204">Source code</span></span>

<span data-ttu-id="c9cbb-205">El código fuente de la aplicación de API de administración de excepciones de Logic Apps está disponible en este [repositorio de GitHub](https://github.com/HEDIDIN/LogicAppsExceptionManagementApi "API de administración de excepciones de Logic Apps").</span><span class="sxs-lookup"><span data-stu-id="c9cbb-205">The source code for the Logic Apps exception management API application is available in this [GitHub repository](https://github.com/HEDIDIN/LogicAppsExceptionManagementApi "Logic App Exception Management API").</span></span>

## <a name="next-steps"></a><span data-ttu-id="c9cbb-206">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="c9cbb-206">Next steps</span></span>

* [<span data-ttu-id="c9cbb-207">Ver más ejemplos y escenarios de aplicaciones Logic Apps</span><span class="sxs-lookup"><span data-stu-id="c9cbb-207">View more logic app examples and scenarios</span></span>](../logic-apps/logic-apps-examples-and-scenarios.md)
* [<span data-ttu-id="c9cbb-208">Obtener más información sobre supervisión de Logic Apps</span><span class="sxs-lookup"><span data-stu-id="c9cbb-208">Learn about monitoring logic apps</span></span>](../logic-apps/logic-apps-monitor-your-logic-apps.md)
* [<span data-ttu-id="c9cbb-209">Creación de plantillas de implementación automatizadas de Logic Apps</span><span class="sxs-lookup"><span data-stu-id="c9cbb-209">Create automated deployment templates for logic apps</span></span>](../logic-apps/logic-apps-create-deploy-template.md)
