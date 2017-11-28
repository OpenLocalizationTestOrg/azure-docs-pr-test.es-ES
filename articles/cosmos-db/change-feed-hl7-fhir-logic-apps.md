---
title: 'Fuente de cambios para recursos de HL7 FHIR: Azure Cosmos DB | Microsoft Docs'
description: Aprenda a configurar notificaciones de cambio para los registros de asistencia sanitaria de paciente de HL7 FHIR con Azure Logic Apps, Azure Cosmos DB y Service Bus.
keywords: hl7 fhir
services: cosmos-db
author: hedidin
manager: jhubbard
editor: mimig
documentationcenter: 
ms.assetid: 0d25c11f-9197-419a-aa19-4614c6ab2d06
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/08/2017
ms.author: b-hoedid
ms.openlocfilehash: d2b50c0b6864af41fb9cfa051721c432772b228d
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="notifying-patients-of-hl7-fhir-health-care-record-changes-using-logic-apps-and-azure-cosmos-db"></a><span data-ttu-id="cea9c-104">Notificación a los pacientes de cambios en los registros de asistencia sanitaria de HL7 FHIR con Logic Apps y Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="cea9c-104">Notifying patients of HL7 FHIR health care record changes using Logic Apps and Azure Cosmos DB</span></span>

<span data-ttu-id="cea9c-105">Recientemente un organización que proporciona asistencia sanitaria se puso en contacto con Azure MVP Howard Edidin, porque deseaba agregar una nueva funcionalidad a su portal de pacientes.</span><span class="sxs-lookup"><span data-stu-id="cea9c-105">Azure MVP Howard Edidin was recently contacted by a healthcare organization that wanted to add new functionality to their patient portal.</span></span> <span data-ttu-id="cea9c-106">Querían enviar notificaciones a los pacientes cuando había una actualización en sus registros sanitarios y que los pacientes pudieran suscribirse a estas actualizaciones.</span><span class="sxs-lookup"><span data-stu-id="cea9c-106">They needed to send notifications to patients when their health record was updated, and they needed patients to be able to subscribe to these updates.</span></span> 

<span data-ttu-id="cea9c-107">Este artículo le guía a través de la solución de notificación de fuente de cambios creada para esta organización de asistencia sanitaria mediante Azure Cosmos DB, Logic Apps y Service Bus.</span><span class="sxs-lookup"><span data-stu-id="cea9c-107">This article walks through the change feed notification solution created for this healthcare organization using Azure Cosmos DB, Logic Apps, and Service Bus.</span></span> 

## <a name="project-requirements"></a><span data-ttu-id="cea9c-108">Requisitos de proyecto</span><span class="sxs-lookup"><span data-stu-id="cea9c-108">Project requirements</span></span>
- <span data-ttu-id="cea9c-109">Los proveedores envían documentos de arquitectura de documento clínico consolidado (C-CDA) HL7 en formato XML.</span><span class="sxs-lookup"><span data-stu-id="cea9c-109">Providers send HL7 Consolidated-Clinical Document Architecture (C-CDA) documents in XML format.</span></span> <span data-ttu-id="cea9c-110">Los documentos C-CDA comprenden prácticamente todos los tipos de documentos clínicos, incluidos entre otros historiales de familia y registros de inmunización, así como documentos administrativos, de flujo de trabajo y financieros.</span><span class="sxs-lookup"><span data-stu-id="cea9c-110">C-CDA documents encompass just about every type of clinical document, including clinical documents such as family histories and immunization records, as well as administrative, workflow, and financial documents.</span></span> 
- <span data-ttu-id="cea9c-111">Los documentos C-CDA se convierten en [Recursos HL7 FHIR](http://hl7.org/fhir/2017Jan/resourcelist.html) en formato JSON.</span><span class="sxs-lookup"><span data-stu-id="cea9c-111">C-CDA documents are converted to [HL7 FHIR Resources](http://hl7.org/fhir/2017Jan/resourcelist.html) in JSON format.</span></span>
- <span data-ttu-id="cea9c-112">Los documentos de recursos FHIR modificados se envían por correo electrónico en formato JSON.</span><span class="sxs-lookup"><span data-stu-id="cea9c-112">Modified FHIR resource documents are sent by email in JSON format.</span></span>

## <a name="solution-workflow"></a><span data-ttu-id="cea9c-113">Flujo de trabajo de la solución</span><span class="sxs-lookup"><span data-stu-id="cea9c-113">Solution workflow</span></span> 

<span data-ttu-id="cea9c-114">En un nivel alto, el proyecto necesita los siguientes pasos de flujo de trabajo:</span><span class="sxs-lookup"><span data-stu-id="cea9c-114">At a high level, the project required the following workflow steps:</span></span> 
1. <span data-ttu-id="cea9c-115">Convertir documentos de C-CDA a recursos FHIR.</span><span class="sxs-lookup"><span data-stu-id="cea9c-115">Convert C-CDA documents to FHIR resources.</span></span>
2. <span data-ttu-id="cea9c-116">Realizar sondeos periódicos con desencadenadores para localizar recursos FHIR modificados.</span><span class="sxs-lookup"><span data-stu-id="cea9c-116">Perform recurring trigger polling for modified FHIR resources.</span></span> 
2. <span data-ttu-id="cea9c-117">Llamar a una aplicación personalizada, FhirNotificationApi, para conectarse a Azure Cosmos DB y consultar si hay documentos nuevos o modificados.</span><span class="sxs-lookup"><span data-stu-id="cea9c-117">Call a custom app, FhirNotificationApi, to connect to Azure Cosmos DB and query for new or modified documents.</span></span>
3. <span data-ttu-id="cea9c-118">Guardar la respuesta en la cola de Service Bus.</span><span class="sxs-lookup"><span data-stu-id="cea9c-118">Save the response to to the Service Bus queue.</span></span>
4. <span data-ttu-id="cea9c-119">Sondear para ver si hay nuevos mensajes en la cola de Service Bus.</span><span class="sxs-lookup"><span data-stu-id="cea9c-119">Poll for new messages in the Service Bus queue.</span></span>
5. <span data-ttu-id="cea9c-120">Enviar notificaciones por correo electrónico a los pacientes.</span><span class="sxs-lookup"><span data-stu-id="cea9c-120">Send email notifications to patients.</span></span>

## <a name="solution-architecture"></a><span data-ttu-id="cea9c-121">Arquitectura de la solución</span><span class="sxs-lookup"><span data-stu-id="cea9c-121">Solution architecture</span></span>
<span data-ttu-id="cea9c-122">Esta solución requiere que tres instancias de Logic Apps cumplan los requisitos anteriores y completen el flujo de trabajo de la solución.</span><span class="sxs-lookup"><span data-stu-id="cea9c-122">This solution requires three Logic Apps to meet the above requirements and complete the solution workflow.</span></span> <span data-ttu-id="cea9c-123">Las tres aplicaciones lógicas son:</span><span class="sxs-lookup"><span data-stu-id="cea9c-123">The three logic apps are:</span></span>
1. <span data-ttu-id="cea9c-124">**Aplicación HL7-FHIR-Mapping**: recibe el documento HL7 C-CDA, lo transforma en recurso FHIR y luego lo guarda en Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="cea9c-124">**HL7-FHIR-Mapping app**: Receives the HL7 C-CDA document, transforms it to the FHIR Resource, then saves it to Azure Cosmos DB.</span></span>
2. <span data-ttu-id="cea9c-125">**Aplicación EHR**: consulta el repositorio FHIR de Azure Cosmos DB y guarda la respuesta en una cola de Service Bus.</span><span class="sxs-lookup"><span data-stu-id="cea9c-125">**EHR app**: Queries the Azure Cosmos DB FHIR repository and saves the response to a Service Bus queue.</span></span> <span data-ttu-id="cea9c-126">Esta aplicación lógica utiliza una [aplicación de API](#api-app) para recuperar los documentos nuevos y cambiados.</span><span class="sxs-lookup"><span data-stu-id="cea9c-126">This logic app uses an [API app](#api-app) to retrieve new and changed documents.</span></span>
3. <span data-ttu-id="cea9c-127">**Aplicación de notificación de proceso**: envía una notificación por correo electrónico con los documentos de recursos FHIR en el cuerpo del mensaje.</span><span class="sxs-lookup"><span data-stu-id="cea9c-127">**Process notification app**: Sends an email notification with the FHIR resource documents in the body.</span></span>

![Las tres instancias de Logic Apps utilizadas en esta solución de servicios de asistencia sanitaria de HL7 FHIR](./media/change-feed-hl7-fhir-logic-apps/health-care-solution-hl7-fhir.png)



### <a name="azure-services-used-in-the-solution"></a><span data-ttu-id="cea9c-129">Servicios de Azure utilizados en la solución</span><span class="sxs-lookup"><span data-stu-id="cea9c-129">Azure services used in the solution</span></span>

#### <a name="azure-cosmos-db-documentdb-api"></a><span data-ttu-id="cea9c-130">API de DocumentDB de Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="cea9c-130">Azure Cosmos DB DocumentDB API</span></span>
<span data-ttu-id="cea9c-131">Azure Cosmos DB es el repositorio para los recursos FHIR tal y como se muestra en la ilustración siguiente.</span><span class="sxs-lookup"><span data-stu-id="cea9c-131">Azure Cosmos DB is the repository for the FHIR resources as shown in the following figure.</span></span>

![Cuenta de Azure Cosmos DB que se usa en este tutorial de asistencia sanitaria de FHIR HL7](./media/change-feed-hl7-fhir-logic-apps/account.png)

#### <a name="logic-apps"></a><span data-ttu-id="cea9c-133">Aplicaciones lógicas</span><span class="sxs-lookup"><span data-stu-id="cea9c-133">Logic Apps</span></span>
<span data-ttu-id="cea9c-134">Logic Apps controlan el proceso de flujo de trabajo.</span><span class="sxs-lookup"><span data-stu-id="cea9c-134">Logic Apps handle the workflow process.</span></span> <span data-ttu-id="cea9c-135">Las capturas de pantalla siguientes muestran las aplicaciones lógicas creadas para esta solución.</span><span class="sxs-lookup"><span data-stu-id="cea9c-135">The following screenshots show the Logic apps created for this solution.</span></span> 


1. <span data-ttu-id="cea9c-136">**Aplicación HL7-FHIR-Mapping**: recibe el documento HL7 C-CDA y lo transforma en recurso FHIR usando Enterprise Integration Pack para Logic Apps.</span><span class="sxs-lookup"><span data-stu-id="cea9c-136">**HL7-FHIR-Mapping app**: Receive the HL7 C-CDA document and transform it to an FHIR resource using the Enterprise Integration Pack for Logic Apps.</span></span> <span data-ttu-id="cea9c-137">Enterprise Integration Pack controla la asignación de la C-CDA a los recursos FHIR.</span><span class="sxs-lookup"><span data-stu-id="cea9c-137">The Enterprise Integration Pack handles the mapping from the C-CDA to FHIR resources.</span></span>

    ![La aplicación lógica que se usa para recibir los registros de los servicios de asistencia sanitaria FHIR HL7](./media/change-feed-hl7-fhir-logic-apps/hl7-fhir-logic-apps-json-transform.png)


2. <span data-ttu-id="cea9c-139">**Aplicación EHR**: consulta el repositorio FHIR de Azure Cosmos DB y guarda la respuesta en una cola de Service Bus.</span><span class="sxs-lookup"><span data-stu-id="cea9c-139">**EHR app**: Query the Azure Cosmos DB FHIR repository and save the response to a Service Bus queue.</span></span> <span data-ttu-id="cea9c-140">El código de la aplicación GetNewOrModifiedFHIRDocuments está a continuación.</span><span class="sxs-lookup"><span data-stu-id="cea9c-140">The code for the GetNewOrModifiedFHIRDocuments app is below.</span></span>

    ![Logic App que se usa para consultar Azure Cosmos DB](./media/change-feed-hl7-fhir-logic-apps/hl7-fhir-logic-apps-api-app.png)

3. <span data-ttu-id="cea9c-142">**Aplicación de notificación de proceso**: envía una notificación por correo electrónico con los documentos de recursos FHIR en el cuerpo del mensaje.</span><span class="sxs-lookup"><span data-stu-id="cea9c-142">**Process notification app**: Send an email notification with the FHIR resource documents in the body.</span></span>

    ![La aplicación lógica que envía correos electrónicos al paciente con el recurso de HL7 FHIR en el cuerpo del mensaje](./media/change-feed-hl7-fhir-logic-apps/hl7-fhir-logic-apps-send-email.png)

#### <a name="service-bus"></a><span data-ttu-id="cea9c-144">Service Bus</span><span class="sxs-lookup"><span data-stu-id="cea9c-144">Service Bus</span></span>
<span data-ttu-id="cea9c-145">La figura siguiente muestra la cola de pacientes.</span><span class="sxs-lookup"><span data-stu-id="cea9c-145">The following figure shows the patients queue.</span></span> <span data-ttu-id="cea9c-146">El valor de propiedad de etiqueta se utiliza para el asunto del correo electrónico.</span><span class="sxs-lookup"><span data-stu-id="cea9c-146">The Tag property value is used for the email subject.</span></span>

![La cola de Service Bus usada en este tutorial FHIR HL7](./media/change-feed-hl7-fhir-logic-apps/hl7-fhir-service-bus-queue.png)

<a id="api-app"></a>

#### <a name="api-app"></a><span data-ttu-id="cea9c-148">Aplicación de API</span><span class="sxs-lookup"><span data-stu-id="cea9c-148">API app</span></span>
<span data-ttu-id="cea9c-149">Una aplicación de API se conecta a Azure Cosmos DB y consulta si hay documentos FHIR nuevos o modificados por tipo de recurso.</span><span class="sxs-lookup"><span data-stu-id="cea9c-149">An API app connects to Azure Cosmos DB and queries for new or modified FHIR documents By resource type.</span></span> <span data-ttu-id="cea9c-150">Esta aplicación tiene un controlador, **FhirNotificationApi** con una sola operación **GetNewOrModifiedFhirDocuments**, consulte [Origen de la aplicación de API](#api-app-source).</span><span class="sxs-lookup"><span data-stu-id="cea9c-150">This app has one controller, **FhirNotificationApi** with a one operation **GetNewOrModifiedFhirDocuments**, see [source for API app](#api-app-source).</span></span>

<span data-ttu-id="cea9c-151">Usamos la clase [ `CreateDocumentChangeFeedQuery` ](https://msdn.microsoft.com/library/azure/microsoft.azure.documents.client.documentclient.createdocumentchangefeedquery.aspx) a partir de la API de .NET de DocumentDB de Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="cea9c-151">We are using the [`CreateDocumentChangeFeedQuery`](https://msdn.microsoft.com/library/azure/microsoft.azure.documents.client.documentclient.createdocumentchangefeedquery.aspx) class from the Azure Cosmos DB DocumentDB .NET API.</span></span> <span data-ttu-id="cea9c-152">Para obtener más información, consulte el artículo [Compatibilidad con la fuente de cambios en Azure DocumentDB](change-feed.md).</span><span class="sxs-lookup"><span data-stu-id="cea9c-152">For more information, see the [change feed article](change-feed.md).</span></span> 

##### <a name="getnewormodifiedfhirdocuments-operation"></a><span data-ttu-id="cea9c-153">Operación GetNewOrModifiedFhirDocuments</span><span class="sxs-lookup"><span data-stu-id="cea9c-153">GetNewOrModifiedFhirDocuments operation</span></span>

<span data-ttu-id="cea9c-154">**Entradas**</span><span class="sxs-lookup"><span data-stu-id="cea9c-154">**Inputs**</span></span>
- <span data-ttu-id="cea9c-155">DatabaseId</span><span class="sxs-lookup"><span data-stu-id="cea9c-155">DatabaseId</span></span>
- <span data-ttu-id="cea9c-156">CollectionId</span><span class="sxs-lookup"><span data-stu-id="cea9c-156">CollectionId</span></span>
- <span data-ttu-id="cea9c-157">Nombre de tipo de recurso de HL7 FHIR</span><span class="sxs-lookup"><span data-stu-id="cea9c-157">HL7 FHIR Resource Type name</span></span>
- <span data-ttu-id="cea9c-158">Un valor booleano: Iniciar desde el principio</span><span class="sxs-lookup"><span data-stu-id="cea9c-158">Boolean: Start from Beginning</span></span>
- <span data-ttu-id="cea9c-159">Int: Número de documentos procesados</span><span class="sxs-lookup"><span data-stu-id="cea9c-159">Int: Number of documents returned</span></span>

<span data-ttu-id="cea9c-160">**Outputs**</span><span class="sxs-lookup"><span data-stu-id="cea9c-160">**Outputs**</span></span>
- <span data-ttu-id="cea9c-161">Correcto: Código de estado: 200, Respuesta: lista de documentos (matriz JSON)</span><span class="sxs-lookup"><span data-stu-id="cea9c-161">Success: Status Code: 200, Response: List of Documents (JSON Array)</span></span>
- <span data-ttu-id="cea9c-162">Error: Código de estado: 404, Respuesta: "No se han encontrado documentos del tipo de recurso '*nombre de recurso '*"</span><span class="sxs-lookup"><span data-stu-id="cea9c-162">Failure: Status Code: 404, Response: "No Documents found for '*resource name'* Resource Type"</span></span>

<a id="api-app-source"></a>

<span data-ttu-id="cea9c-163">**Origen de la aplicación de API**</span><span class="sxs-lookup"><span data-stu-id="cea9c-163">**Source for the API app**</span></span>

```C#

    using System.Collections.Generic;
    using System.Linq;
    using System.Net;
    using System.Net.Http;
    using System.Threading.Tasks;
    using System.Web.Http;
    using Microsoft.Azure.Documents;
    using Microsoft.Azure.Documents.Client;
    using Swashbuckle.Swagger.Annotations;
    using TRex.Metadata;
    
    namespace FhirNotificationApi.Controllers
    {
        /// <summary>
        ///     FHIR Resource Type Controller
        /// </summary>
        /// <seealso cref="System.Web.Http.ApiController" />
        public class FhirResourceTypeController : ApiController
        {
            /// <summary>
            ///     Gets the new or modified FHIR documents from Last Run Date 
            ///     or create date of the collection
            /// </summary>
            /// <param name="databaseId"></param>
            /// <param name="collectionId"></param>
            /// <param name="resourceType"></param>
            /// <param name="startfromBeginning"></param>
            /// <param name="maximumItemCount">-1 returns all (default)</param>
            /// <returns></returns>
            [Metadata("Get New or Modified FHIR Documents",
                "Query for new or modifed FHIR Documents By Resource Type " +
                "from Last Run Date or Begining of Collection creation"
            )]
            [SwaggerResponse(HttpStatusCode.OK, type: typeof(Task<dynamic>))]
            [SwaggerResponse(HttpStatusCode.NotFound, "No New or Modifed Documents found")]
            [SwaggerOperation("GetNewOrModifiedFHIRDocuments")]
            public async Task<dynamic> GetNewOrModifiedFhirDocuments(
                [Metadata("Database Id", "Database Id")] string databaseId,
                [Metadata("Collection Id", "Collection Id")] string collectionId,
                [Metadata("Resource Type", "FHIR resource type name")] string resourceType,
                [Metadata("Start from Beginning ", "Change Feed Option")] bool startfromBeginning,
                [Metadata("Maximum Item Count", "Number of documents returned. '-1 returns all' (default)")] int maximumItemCount = -1
            )
            {
                var collectionLink = UriFactory.CreateDocumentCollectionUri(databaseId, collectionId);
    
                var context = new DocumentDbContext();  
    
                var docs = new List<dynamic>();
    
                var partitionKeyRanges = new List<PartitionKeyRange>();
                FeedResponse<PartitionKeyRange> pkRangesResponse;
    
                do
                {
                    pkRangesResponse = await context.Client.ReadPartitionKeyRangeFeedAsync(collectionLink);
                    partitionKeyRanges.AddRange(pkRangesResponse);
                } while (pkRangesResponse.ResponseContinuation != null);
    
                foreach (var pkRange in partitionKeyRanges)
                {
                    var changeFeedOptions = new ChangeFeedOptions
                    {
                        StartFromBeginning = startfromBeginning,
                        RequestContinuation = null,
                        MaxItemCount = maximumItemCount,
                        PartitionKeyRangeId = pkRange.Id
                    };
    
                    using (var query = context.Client.CreateDocumentChangeFeedQuery(collectionLink, changeFeedOptions))
                    {
                        do
                        {
                            if (query != null)
                            {
                                var results = await query.ExecuteNextAsync<dynamic>().ConfigureAwait(false);
                                if (results.Count > 0)
                                    docs.AddRange(results.Where(doc => doc.resourceType == resourceType));
                            }
                            else
                            {
                                throw new HttpResponseException(new HttpResponseMessage(HttpStatusCode.NotFound));
                            }
                        } while (query.HasMoreResults);
                    }
                }
                if (docs.Count > 0)
                    return docs;
                var msg = new StringContent("No documents found for " + resourceType + " Resource");
                var response = new HttpResponseMessage
                {
                    StatusCode = HttpStatusCode.NotFound,
                    Content = msg
                };
                return response;
            }
        }
    }
    
```

### <a name="testing-the-fhirnotificationapi"></a><span data-ttu-id="cea9c-164">Prueba de FhirNotificationApi</span><span class="sxs-lookup"><span data-stu-id="cea9c-164">Testing the FhirNotificationApi</span></span> 

<span data-ttu-id="cea9c-165">La imagen siguiente muestra cómo se usa Swagger para probar [FhirNotificationApi](#api-app-source).</span><span class="sxs-lookup"><span data-stu-id="cea9c-165">The following image demonstrates how swagger was used to to test the [FhirNotificationApi](#api-app-source).</span></span>

![El archivo Swagger que se usa para probar la aplicación de API](./media/change-feed-hl7-fhir-logic-apps/hl7-fhir-testing-app.png)


### <a name="azure-portal-dashboard"></a><span data-ttu-id="cea9c-167">Panel de Portal de Azure</span><span class="sxs-lookup"><span data-stu-id="cea9c-167">Azure portal dashboard</span></span>

<span data-ttu-id="cea9c-168">La siguiente imagen muestra todos los servicios de Azure para esta solución ejecutándose en Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="cea9c-168">The following image shows all of the Azure services for this solution running in the Azure portal.</span></span>

![Azure Portal mostrando todos los servicios que se usan en este tutorial FHIR HL7](./media/change-feed-hl7-fhir-logic-apps/hl7-fhir-portal.png)


## <a name="summary"></a><span data-ttu-id="cea9c-170">Resumen</span><span class="sxs-lookup"><span data-stu-id="cea9c-170">Summary</span></span>

- <span data-ttu-id="cea9c-171">Ha aprendido que Azure Cosmos DB tiene soporte técnico nativo para las notificaciones para documentos nuevos o modificados y ha visto lo fácil que es de usar.</span><span class="sxs-lookup"><span data-stu-id="cea9c-171">You have learned that Azure Cosmos DB has native suppport for notifications for new or modifed documents and how easy it is to use.</span></span> 
- <span data-ttu-id="cea9c-172">Ha visto como aprovechando Logic Apps puede crear flujos de trabajo sin escribir ningún código.</span><span class="sxs-lookup"><span data-stu-id="cea9c-172">By leveraging Logic Apps, you can create workflows without writing any code.</span></span>
- <span data-ttu-id="cea9c-173">Ha visto que usando las colas de Azure Service Bus puede controlar la distribución de los documentos de HL7 FHIR.</span><span class="sxs-lookup"><span data-stu-id="cea9c-173">Using Azure Service Bus Queues to handle the distribution for the HL7 FHIR documents.</span></span>

## <a name="next-steps"></a><span data-ttu-id="cea9c-174">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="cea9c-174">Next steps</span></span>
<span data-ttu-id="cea9c-175">Para más información sobre Azure Cosmos DB, consulte la [página principal de Azure Cosmos DB](https://azure.microsoft.com/services/cosmos-db/).</span><span class="sxs-lookup"><span data-stu-id="cea9c-175">For more information about Azure Cosmos DB, see the [Azure Cosmos DB home page](https://azure.microsoft.com/services/cosmos-db/).</span></span> <span data-ttu-id="cea9c-176">Para más información acerca de Logic Apps, consulte [Logic Apps](https://azure.microsoft.com/services/logic-apps/).</span><span class="sxs-lookup"><span data-stu-id="cea9c-176">For more informaiton about Logic Apps, see [Logic Apps](https://azure.microsoft.com/services/logic-apps/).</span></span>


