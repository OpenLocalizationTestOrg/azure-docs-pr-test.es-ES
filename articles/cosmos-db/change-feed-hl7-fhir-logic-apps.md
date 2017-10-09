---
title: aaaChange fuente para que los recursos de HL7 FHIR - base de datos de Azure Cosmos | Documentos de Microsoft
description: "Obtenga información acerca de cómo tooset seguridad cambiar las notificaciones para HL7 FHIR sanitarios registros de los pacientes con lógica de aplicaciones de Azure, base de datos de Azure Cosmos y Service Bus."
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
ms.openlocfilehash: d2809bf5c6d8c193c49438d20684c56caea646bb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="notifying-patients-of-hl7-fhir-health-care-record-changes-using-logic-apps-and-azure-cosmos-db"></a><span data-ttu-id="90965-104">Notificación a los pacientes de cambios en los registros de asistencia sanitaria de HL7 FHIR con Logic Apps y Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="90965-104">Notifying patients of HL7 FHIR health care record changes using Logic Apps and Azure Cosmos DB</span></span>

<span data-ttu-id="90965-105">Azure MVP Howard Edidin recientemente se puso en contacto por una organización de servicios de salud que deseaba tooadd nuevo funcionalidad tootheir paciente portal.</span><span class="sxs-lookup"><span data-stu-id="90965-105">Azure MVP Howard Edidin was recently contacted by a healthcare organization that wanted tooadd new functionality tootheir patient portal.</span></span> <span data-ttu-id="90965-106">Necesitaban toosend notificaciones toopatients cuando se ha actualizado su registro de mantenimiento y que necesitan las actualizaciones de los pacientes toobe toosubscribe capaz de toothese.</span><span class="sxs-lookup"><span data-stu-id="90965-106">They needed toosend notifications toopatients when their health record was updated, and they needed patients toobe able toosubscribe toothese updates.</span></span> 

<span data-ttu-id="90965-107">Este artículo le guía a través de solución de fuente notificación de cambio Hola creado para esta organización de atención médica con base de datos de Azure Cosmos, Logic Apps y Bus de servicio.</span><span class="sxs-lookup"><span data-stu-id="90965-107">This article walks through hello change feed notification solution created for this healthcare organization using Azure Cosmos DB, Logic Apps, and Service Bus.</span></span> 

## <a name="project-requirements"></a><span data-ttu-id="90965-108">Requisitos de proyecto</span><span class="sxs-lookup"><span data-stu-id="90965-108">Project requirements</span></span>
- <span data-ttu-id="90965-109">Los proveedores envían documentos de arquitectura de documento clínico consolidado (C-CDA) HL7 en formato XML.</span><span class="sxs-lookup"><span data-stu-id="90965-109">Providers send HL7 Consolidated-Clinical Document Architecture (C-CDA) documents in XML format.</span></span> <span data-ttu-id="90965-110">Los documentos C-CDA comprenden prácticamente todos los tipos de documentos clínicos, incluidos entre otros historiales de familia y registros de inmunización, así como documentos administrativos, de flujo de trabajo y financieros.</span><span class="sxs-lookup"><span data-stu-id="90965-110">C-CDA documents encompass just about every type of clinical document, including clinical documents such as family histories and immunization records, as well as administrative, workflow, and financial documents.</span></span> 
- <span data-ttu-id="90965-111">Documentos de C CDA se convierten demasiado[HL7 FHIR recursos](http://hl7.org/fhir/2017Jan/resourcelist.html) en formato JSON.</span><span class="sxs-lookup"><span data-stu-id="90965-111">C-CDA documents are converted too[HL7 FHIR Resources](http://hl7.org/fhir/2017Jan/resourcelist.html) in JSON format.</span></span>
- <span data-ttu-id="90965-112">Los documentos de recursos FHIR modificados se envían por correo electrónico en formato JSON.</span><span class="sxs-lookup"><span data-stu-id="90965-112">Modified FHIR resource documents are sent by email in JSON format.</span></span>

## <a name="solution-workflow"></a><span data-ttu-id="90965-113">Flujo de trabajo de la solución</span><span class="sxs-lookup"><span data-stu-id="90965-113">Solution workflow</span></span> 

<span data-ttu-id="90965-114">En un nivel alto, Hola Hola de proyecto necesarios pasos de flujo de trabajo:</span><span class="sxs-lookup"><span data-stu-id="90965-114">At a high level, hello project required hello following workflow steps:</span></span> 
1. <span data-ttu-id="90965-115">Convertir recursos tooFHIR de C CDA documentos.</span><span class="sxs-lookup"><span data-stu-id="90965-115">Convert C-CDA documents tooFHIR resources.</span></span>
2. <span data-ttu-id="90965-116">Realizar sondeos periódicos con desencadenadores para localizar recursos FHIR modificados.</span><span class="sxs-lookup"><span data-stu-id="90965-116">Perform recurring trigger polling for modified FHIR resources.</span></span> 
2. <span data-ttu-id="90965-117">Llamar a una aplicación personalizada, FhirNotificationApi, tooconnect tooAzure DB Cosmos y consulta para documentos nuevos o modificados.</span><span class="sxs-lookup"><span data-stu-id="90965-117">Call a custom app, FhirNotificationApi, tooconnect tooAzure Cosmos DB and query for new or modified documents.</span></span>
3. <span data-ttu-id="90965-118">Guarde la cola de Bus de servicio de hello respuesta tootoohello.</span><span class="sxs-lookup"><span data-stu-id="90965-118">Save hello response tootoohello Service Bus queue.</span></span>
4. <span data-ttu-id="90965-119">Sondeo de nuevos mensajes en cola de Bus de servicio de Hola.</span><span class="sxs-lookup"><span data-stu-id="90965-119">Poll for new messages in hello Service Bus queue.</span></span>
5. <span data-ttu-id="90965-120">Enviar toopatients de notificaciones de correo electrónico.</span><span class="sxs-lookup"><span data-stu-id="90965-120">Send email notifications toopatients.</span></span>

## <a name="solution-architecture"></a><span data-ttu-id="90965-121">Arquitectura de la solución</span><span class="sxs-lookup"><span data-stu-id="90965-121">Solution architecture</span></span>
<span data-ttu-id="90965-122">Esta solución requiere tres Hola de toomeet Logic Apps por encima de los requisitos y flujo de trabajo de solución de hello completa.</span><span class="sxs-lookup"><span data-stu-id="90965-122">This solution requires three Logic Apps toomeet hello above requirements and complete hello solution workflow.</span></span> <span data-ttu-id="90965-123">las aplicaciones lógicas de Hello tres son:</span><span class="sxs-lookup"><span data-stu-id="90965-123">hello three logic apps are:</span></span>
1. <span data-ttu-id="90965-124">**Aplicación de la asignación de FHIR HL7**: recibe Hola HL7 C-CDA documento, lo transforma toohello FHIR recursos y, a continuación, guarda tooAzure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="90965-124">**HL7-FHIR-Mapping app**: Receives hello HL7 C-CDA document, transforms it toohello FHIR Resource, then saves it tooAzure Cosmos DB.</span></span>
2. <span data-ttu-id="90965-125">**Aplicación EHR**: consulta repositorio de FHIR de base de datos de Azure Cosmos hello y guarda la cola de Bus de servicio de hello respuesta tooa.</span><span class="sxs-lookup"><span data-stu-id="90965-125">**EHR app**: Queries hello Azure Cosmos DB FHIR repository and saves hello response tooa Service Bus queue.</span></span> <span data-ttu-id="90965-126">Esta lógica de aplicación utiliza un [aplicación de API](#api-app) tooretrieve nuevas y modificadas documentos.</span><span class="sxs-lookup"><span data-stu-id="90965-126">This logic app uses an [API app](#api-app) tooretrieve new and changed documents.</span></span>
3. <span data-ttu-id="90965-127">**Aplicación de notificación de proceso**: envía una notificación por correo electrónico con documentos de hello FHIR recursos en el cuerpo de Hola.</span><span class="sxs-lookup"><span data-stu-id="90965-127">**Process notification app**: Sends an email notification with hello FHIR resource documents in hello body.</span></span>

![Hola tres Logic Apps utilizados en esta solución de servicios de salud FHIR HL7](./media/change-feed-hl7-fhir-logic-apps/health-care-solution-hl7-fhir.png)



### <a name="azure-services-used-in-hello-solution"></a><span data-ttu-id="90965-129">Servicios de Azure usa en soluciones de Hola</span><span class="sxs-lookup"><span data-stu-id="90965-129">Azure services used in hello solution</span></span>

#### <a name="azure-cosmos-db-documentdb-api"></a><span data-ttu-id="90965-130">API de DocumentDB de Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="90965-130">Azure Cosmos DB DocumentDB API</span></span>
<span data-ttu-id="90965-131">Azure DB Cosmos es el repositorio de Hola para recursos de hello FHIR tal y como se muestra en la figura siguiente de Hola.</span><span class="sxs-lookup"><span data-stu-id="90965-131">Azure Cosmos DB is hello repository for hello FHIR resources as shown in hello following figure.</span></span>

![cuenta de base de datos de Azure Cosmos Hola usada en este tutorial sanitarios FHIR HL7](./media/change-feed-hl7-fhir-logic-apps/account.png)

#### <a name="logic-apps"></a><span data-ttu-id="90965-133">Logic Apps</span><span class="sxs-lookup"><span data-stu-id="90965-133">Logic Apps</span></span>
<span data-ttu-id="90965-134">Las aplicaciones lógicas de controlen el proceso de flujo de trabajo de Hola.</span><span class="sxs-lookup"><span data-stu-id="90965-134">Logic Apps handle hello workflow process.</span></span> <span data-ttu-id="90965-135">Hello capturas de pantalla siguientes muestran Hola lógica las aplicaciones creadas para esta solución.</span><span class="sxs-lookup"><span data-stu-id="90965-135">hello following screenshots show hello Logic apps created for this solution.</span></span> 


1. <span data-ttu-id="90965-136">**Aplicación de la asignación de FHIR HL7**: recibir Hola HL7 C-CDA documento y para transformarlos recursos FHIR tooan con hello paquete de integración empresarial para las aplicaciones lógicas.</span><span class="sxs-lookup"><span data-stu-id="90965-136">**HL7-FHIR-Mapping app**: Receive hello HL7 C-CDA document and transform it tooan FHIR resource using hello Enterprise Integration Pack for Logic Apps.</span></span> <span data-ttu-id="90965-137">Hola paquete de integración empresarial controla Hola asignación a partir de hello recursos de C CDA tooFHIR.</span><span class="sxs-lookup"><span data-stu-id="90965-137">hello Enterprise Integration Pack handles hello mapping from hello C-CDA tooFHIR resources.</span></span>

    ![Hola lógica de aplicación utiliza registros de servicios de salud tooreceive FHIR HL7](./media/change-feed-hl7-fhir-logic-apps/hl7-fhir-logic-apps-json-transform.png)


2. <span data-ttu-id="90965-139">**Aplicación EHR**: hello Azure Cosmos DB FHIR repositorio de consultas y guardar Hola respuesta tooa Bus de servicio cola.</span><span class="sxs-lookup"><span data-stu-id="90965-139">**EHR app**: Query hello Azure Cosmos DB FHIR repository and save hello response tooa Service Bus queue.</span></span> <span data-ttu-id="90965-140">código de Hello para la aplicación de hello GetNewOrModifiedFHIRDocuments es menor que.</span><span class="sxs-lookup"><span data-stu-id="90965-140">hello code for hello GetNewOrModifiedFHIRDocuments app is below.</span></span>

    ![Hola lógica de aplicación usa tooquery base de datos de Azure Cosmos](./media/change-feed-hl7-fhir-logic-apps/hl7-fhir-logic-apps-api-app.png)

3. <span data-ttu-id="90965-142">**Aplicación de notificación de proceso**: enviar una notificación por correo electrónico con documentos de hello FHIR recursos en el cuerpo de Hola.</span><span class="sxs-lookup"><span data-stu-id="90965-142">**Process notification app**: Send an email notification with hello FHIR resource documents in hello body.</span></span>

    ![Hola lógica de aplicación que se envía correo paciente con recursos de HL7 FHIR hello en el cuerpo de Hola](./media/change-feed-hl7-fhir-logic-apps/hl7-fhir-logic-apps-send-email.png)

#### <a name="service-bus"></a><span data-ttu-id="90965-144">Bus de servicio</span><span class="sxs-lookup"><span data-stu-id="90965-144">Service Bus</span></span>
<span data-ttu-id="90965-145">Hola siguiente figura muestra hello pacientes cola.</span><span class="sxs-lookup"><span data-stu-id="90965-145">hello following figure shows hello patients queue.</span></span> <span data-ttu-id="90965-146">Hola valor de la propiedad de etiqueta se utiliza para el asunto del correo electrónico de Hola.</span><span class="sxs-lookup"><span data-stu-id="90965-146">hello Tag property value is used for hello email subject.</span></span>

![Hola cola de Bus de servicio usado en este tutorial FHIR HL7](./media/change-feed-hl7-fhir-logic-apps/hl7-fhir-service-bus-queue.png)

<a id="api-app"></a>

#### <a name="api-app"></a><span data-ttu-id="90965-148">Aplicación de API</span><span class="sxs-lookup"><span data-stu-id="90965-148">API app</span></span>
<span data-ttu-id="90965-149">Conecta una aplicación de API tooAzure DB Cosmos y consultas para los documentos FHIR nuevos o modificados por tipo de recurso.</span><span class="sxs-lookup"><span data-stu-id="90965-149">An API app connects tooAzure Cosmos DB and queries for new or modified FHIR documents By resource type.</span></span> <span data-ttu-id="90965-150">Esta aplicación tiene un controlador, **FhirNotificationApi** con una sola operación **GetNewOrModifiedFhirDocuments**, consulte [Origen de la aplicación de API](#api-app-source).</span><span class="sxs-lookup"><span data-stu-id="90965-150">This app has one controller, **FhirNotificationApi** with a one operation **GetNewOrModifiedFhirDocuments**, see [source for API app](#api-app-source).</span></span>

<span data-ttu-id="90965-151">Estamos usando hello [ `CreateDocumentChangeFeedQuery` ](https://msdn.microsoft.com/library/azure/microsoft.azure.documents.client.documentclient.createdocumentchangefeedquery.aspx) clase a partir de la API de .NET de documentos de base de datos de Azure Cosmos Hola.</span><span class="sxs-lookup"><span data-stu-id="90965-151">We are using hello [`CreateDocumentChangeFeedQuery`](https://msdn.microsoft.com/library/azure/microsoft.azure.documents.client.documentclient.createdocumentchangefeedquery.aspx) class from hello Azure Cosmos DB DocumentDB .NET API.</span></span> <span data-ttu-id="90965-152">Para obtener más información, vea hello [Cambiar fuente artículo](change-feed.md).</span><span class="sxs-lookup"><span data-stu-id="90965-152">For more information, see hello [change feed article](change-feed.md).</span></span> 

##### <a name="getnewormodifiedfhirdocuments-operation"></a><span data-ttu-id="90965-153">Operación GetNewOrModifiedFhirDocuments</span><span class="sxs-lookup"><span data-stu-id="90965-153">GetNewOrModifiedFhirDocuments operation</span></span>

<span data-ttu-id="90965-154">**Entradas**</span><span class="sxs-lookup"><span data-stu-id="90965-154">**Inputs**</span></span>
- <span data-ttu-id="90965-155">DatabaseId</span><span class="sxs-lookup"><span data-stu-id="90965-155">DatabaseId</span></span>
- <span data-ttu-id="90965-156">CollectionId</span><span class="sxs-lookup"><span data-stu-id="90965-156">CollectionId</span></span>
- <span data-ttu-id="90965-157">Nombre de tipo de recurso de HL7 FHIR</span><span class="sxs-lookup"><span data-stu-id="90965-157">HL7 FHIR Resource Type name</span></span>
- <span data-ttu-id="90965-158">Un valor booleano: Iniciar desde el principio</span><span class="sxs-lookup"><span data-stu-id="90965-158">Boolean: Start from Beginning</span></span>
- <span data-ttu-id="90965-159">Int: Número de documentos procesados</span><span class="sxs-lookup"><span data-stu-id="90965-159">Int: Number of documents returned</span></span>

<span data-ttu-id="90965-160">**Outputs**</span><span class="sxs-lookup"><span data-stu-id="90965-160">**Outputs**</span></span>
- <span data-ttu-id="90965-161">Correcto: Código de estado: 200, Respuesta: lista de documentos (matriz JSON)</span><span class="sxs-lookup"><span data-stu-id="90965-161">Success: Status Code: 200, Response: List of Documents (JSON Array)</span></span>
- <span data-ttu-id="90965-162">Error: Código de estado: 404, Respuesta: "No se han encontrado documentos del tipo de recurso '*nombre de recurso '*"</span><span class="sxs-lookup"><span data-stu-id="90965-162">Failure: Status Code: 404, Response: "No Documents found for '*resource name'* Resource Type"</span></span>

<a id="api-app-source"></a>

<span data-ttu-id="90965-163">**Origen para la aplicación hello API**</span><span class="sxs-lookup"><span data-stu-id="90965-163">**Source for hello API app**</span></span>

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
            ///     Gets hello new or modified FHIR documents from Last Run Date 
            ///     or create date of hello collection
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

### <a name="testing-hello-fhirnotificationapi"></a><span data-ttu-id="90965-164">Pruebas hello FhirNotificationApi</span><span class="sxs-lookup"><span data-stu-id="90965-164">Testing hello FhirNotificationApi</span></span> 

<span data-ttu-id="90965-165">Hello imagen siguiente muestra cómo swagger fue tootootest usado hello [FhirNotificationApi](#api-app-source).</span><span class="sxs-lookup"><span data-stu-id="90965-165">hello following image demonstrates how swagger was used tootootest hello [FhirNotificationApi](#api-app-source).</span></span>

![archivo Swagger de Hello usa la aplicación de API de hello tootest](./media/change-feed-hl7-fhir-logic-apps/hl7-fhir-testing-app.png)


### <a name="azure-portal-dashboard"></a><span data-ttu-id="90965-167">Panel de Portal de Azure</span><span class="sxs-lookup"><span data-stu-id="90965-167">Azure portal dashboard</span></span>

<span data-ttu-id="90965-168">Hola siguiente imagen muestra todas Hola servicios de Azure para esta solución se ejecuta en hello portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="90965-168">hello following image shows all of hello Azure services for this solution running in hello Azure portal.</span></span>

![Hola portal de Azure que muestra todos los servicios de hello utilizados en este tutorial FHIR HL7](./media/change-feed-hl7-fhir-logic-apps/hl7-fhir-portal.png)


## <a name="summary"></a><span data-ttu-id="90965-170">Resumen</span><span class="sxs-lookup"><span data-stu-id="90965-170">Summary</span></span>

- <span data-ttu-id="90965-171">Ha aprendido que base de datos de Azure Cosmos tiene soporte técnico nativo para las notificaciones para el nuevo o modificar documentos y lo fácil que es toouse.</span><span class="sxs-lookup"><span data-stu-id="90965-171">You have learned that Azure Cosmos DB has native suppport for notifications for new or modifed documents and how easy it is toouse.</span></span> 
- <span data-ttu-id="90965-172">Ha visto como aprovechando Logic Apps puede crear flujos de trabajo sin escribir ningún código.</span><span class="sxs-lookup"><span data-stu-id="90965-172">By leveraging Logic Apps, you can create workflows without writing any code.</span></span>
- <span data-ttu-id="90965-173">Usando la distribución de Hola de toohandle de colas de Bus de servicio de Azure para los documentos de HL7 FHIR Hola.</span><span class="sxs-lookup"><span data-stu-id="90965-173">Using Azure Service Bus Queues toohandle hello distribution for hello HL7 FHIR documents.</span></span>

## <a name="next-steps"></a><span data-ttu-id="90965-174">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="90965-174">Next steps</span></span>
<span data-ttu-id="90965-175">Para obtener más información acerca de la base de datos de Azure Cosmos, vea hello [página principal de base de datos de Azure Cosmos](https://azure.microsoft.com/services/cosmos-db/).</span><span class="sxs-lookup"><span data-stu-id="90965-175">For more information about Azure Cosmos DB, see hello [Azure Cosmos DB home page](https://azure.microsoft.com/services/cosmos-db/).</span></span> <span data-ttu-id="90965-176">Para más información acerca de Logic Apps, consulte [Logic Apps](https://azure.microsoft.com/services/logic-apps/).</span><span class="sxs-lookup"><span data-stu-id="90965-176">For more informaiton about Logic Apps, see [Logic Apps](https://azure.microsoft.com/services/logic-apps/).</span></span>


