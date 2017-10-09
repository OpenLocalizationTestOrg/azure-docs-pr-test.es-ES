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
# <a name="notifying-patients-of-hl7-fhir-health-care-record-changes-using-logic-apps-and-azure-cosmos-db"></a>Notificación a los pacientes de cambios en los registros de asistencia sanitaria de HL7 FHIR con Logic Apps y Azure Cosmos DB

Azure MVP Howard Edidin recientemente se puso en contacto por una organización de servicios de salud que deseaba tooadd nuevo funcionalidad tootheir paciente portal. Necesitaban toosend notificaciones toopatients cuando se ha actualizado su registro de mantenimiento y que necesitan las actualizaciones de los pacientes toobe toosubscribe capaz de toothese. 

Este artículo le guía a través de solución de fuente notificación de cambio Hola creado para esta organización de atención médica con base de datos de Azure Cosmos, Logic Apps y Bus de servicio. 

## <a name="project-requirements"></a>Requisitos de proyecto
- Los proveedores envían documentos de arquitectura de documento clínico consolidado (C-CDA) HL7 en formato XML. Los documentos C-CDA comprenden prácticamente todos los tipos de documentos clínicos, incluidos entre otros historiales de familia y registros de inmunización, así como documentos administrativos, de flujo de trabajo y financieros. 
- Documentos de C CDA se convierten demasiado[HL7 FHIR recursos](http://hl7.org/fhir/2017Jan/resourcelist.html) en formato JSON.
- Los documentos de recursos FHIR modificados se envían por correo electrónico en formato JSON.

## <a name="solution-workflow"></a>Flujo de trabajo de la solución 

En un nivel alto, Hola Hola de proyecto necesarios pasos de flujo de trabajo: 
1. Convertir recursos tooFHIR de C CDA documentos.
2. Realizar sondeos periódicos con desencadenadores para localizar recursos FHIR modificados. 
2. Llamar a una aplicación personalizada, FhirNotificationApi, tooconnect tooAzure DB Cosmos y consulta para documentos nuevos o modificados.
3. Guarde la cola de Bus de servicio de hello respuesta tootoohello.
4. Sondeo de nuevos mensajes en cola de Bus de servicio de Hola.
5. Enviar toopatients de notificaciones de correo electrónico.

## <a name="solution-architecture"></a>Arquitectura de la solución
Esta solución requiere tres Hola de toomeet Logic Apps por encima de los requisitos y flujo de trabajo de solución de hello completa. las aplicaciones lógicas de Hello tres son:
1. **Aplicación de la asignación de FHIR HL7**: recibe Hola HL7 C-CDA documento, lo transforma toohello FHIR recursos y, a continuación, guarda tooAzure Cosmos DB.
2. **Aplicación EHR**: consulta repositorio de FHIR de base de datos de Azure Cosmos hello y guarda la cola de Bus de servicio de hello respuesta tooa. Esta lógica de aplicación utiliza un [aplicación de API](#api-app) tooretrieve nuevas y modificadas documentos.
3. **Aplicación de notificación de proceso**: envía una notificación por correo electrónico con documentos de hello FHIR recursos en el cuerpo de Hola.

![Hola tres Logic Apps utilizados en esta solución de servicios de salud FHIR HL7](./media/change-feed-hl7-fhir-logic-apps/health-care-solution-hl7-fhir.png)



### <a name="azure-services-used-in-hello-solution"></a>Servicios de Azure usa en soluciones de Hola

#### <a name="azure-cosmos-db-documentdb-api"></a>API de DocumentDB de Azure Cosmos DB
Azure DB Cosmos es el repositorio de Hola para recursos de hello FHIR tal y como se muestra en la figura siguiente de Hola.

![cuenta de base de datos de Azure Cosmos Hola usada en este tutorial sanitarios FHIR HL7](./media/change-feed-hl7-fhir-logic-apps/account.png)

#### <a name="logic-apps"></a>Logic Apps
Las aplicaciones lógicas de controlen el proceso de flujo de trabajo de Hola. Hello capturas de pantalla siguientes muestran Hola lógica las aplicaciones creadas para esta solución. 


1. **Aplicación de la asignación de FHIR HL7**: recibir Hola HL7 C-CDA documento y para transformarlos recursos FHIR tooan con hello paquete de integración empresarial para las aplicaciones lógicas. Hola paquete de integración empresarial controla Hola asignación a partir de hello recursos de C CDA tooFHIR.

    ![Hola lógica de aplicación utiliza registros de servicios de salud tooreceive FHIR HL7](./media/change-feed-hl7-fhir-logic-apps/hl7-fhir-logic-apps-json-transform.png)


2. **Aplicación EHR**: hello Azure Cosmos DB FHIR repositorio de consultas y guardar Hola respuesta tooa Bus de servicio cola. código de Hello para la aplicación de hello GetNewOrModifiedFHIRDocuments es menor que.

    ![Hola lógica de aplicación usa tooquery base de datos de Azure Cosmos](./media/change-feed-hl7-fhir-logic-apps/hl7-fhir-logic-apps-api-app.png)

3. **Aplicación de notificación de proceso**: enviar una notificación por correo electrónico con documentos de hello FHIR recursos en el cuerpo de Hola.

    ![Hola lógica de aplicación que se envía correo paciente con recursos de HL7 FHIR hello en el cuerpo de Hola](./media/change-feed-hl7-fhir-logic-apps/hl7-fhir-logic-apps-send-email.png)

#### <a name="service-bus"></a>Bus de servicio
Hola siguiente figura muestra hello pacientes cola. Hola valor de la propiedad de etiqueta se utiliza para el asunto del correo electrónico de Hola.

![Hola cola de Bus de servicio usado en este tutorial FHIR HL7](./media/change-feed-hl7-fhir-logic-apps/hl7-fhir-service-bus-queue.png)

<a id="api-app"></a>

#### <a name="api-app"></a>Aplicación de API
Conecta una aplicación de API tooAzure DB Cosmos y consultas para los documentos FHIR nuevos o modificados por tipo de recurso. Esta aplicación tiene un controlador, **FhirNotificationApi** con una sola operación **GetNewOrModifiedFhirDocuments**, consulte [Origen de la aplicación de API](#api-app-source).

Estamos usando hello [ `CreateDocumentChangeFeedQuery` ](https://msdn.microsoft.com/library/azure/microsoft.azure.documents.client.documentclient.createdocumentchangefeedquery.aspx) clase a partir de la API de .NET de documentos de base de datos de Azure Cosmos Hola. Para obtener más información, vea hello [Cambiar fuente artículo](change-feed.md). 

##### <a name="getnewormodifiedfhirdocuments-operation"></a>Operación GetNewOrModifiedFhirDocuments

**Entradas**
- DatabaseId
- CollectionId
- Nombre de tipo de recurso de HL7 FHIR
- Un valor booleano: Iniciar desde el principio
- Int: Número de documentos procesados

**Outputs**
- Correcto: Código de estado: 200, Respuesta: lista de documentos (matriz JSON)
- Error: Código de estado: 404, Respuesta: "No se han encontrado documentos del tipo de recurso '*nombre de recurso '*"

<a id="api-app-source"></a>

**Origen para la aplicación hello API**

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

### <a name="testing-hello-fhirnotificationapi"></a>Pruebas hello FhirNotificationApi 

Hello imagen siguiente muestra cómo swagger fue tootootest usado hello [FhirNotificationApi](#api-app-source).

![archivo Swagger de Hello usa la aplicación de API de hello tootest](./media/change-feed-hl7-fhir-logic-apps/hl7-fhir-testing-app.png)


### <a name="azure-portal-dashboard"></a>Panel de Portal de Azure

Hola siguiente imagen muestra todas Hola servicios de Azure para esta solución se ejecuta en hello portal de Azure.

![Hola portal de Azure que muestra todos los servicios de hello utilizados en este tutorial FHIR HL7](./media/change-feed-hl7-fhir-logic-apps/hl7-fhir-portal.png)


## <a name="summary"></a>Resumen

- Ha aprendido que base de datos de Azure Cosmos tiene soporte técnico nativo para las notificaciones para el nuevo o modificar documentos y lo fácil que es toouse. 
- Ha visto como aprovechando Logic Apps puede crear flujos de trabajo sin escribir ningún código.
- Usando la distribución de Hola de toohandle de colas de Bus de servicio de Azure para los documentos de HL7 FHIR Hola.

## <a name="next-steps"></a>Pasos siguientes
Para obtener más información acerca de la base de datos de Azure Cosmos, vea hello [página principal de base de datos de Azure Cosmos](https://azure.microsoft.com/services/cosmos-db/). Para más información acerca de Logic Apps, consulte [Logic Apps](https://azure.microsoft.com/services/logic-apps/).


