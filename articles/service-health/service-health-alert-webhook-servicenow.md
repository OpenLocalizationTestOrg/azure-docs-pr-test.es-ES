---
title: "Configuración de alertas de estado del servicio de Azure con ServiceNow | Microsoft Docs"
description: Obtenga notificaciones personalizadas sobre los eventos del estado de servicio en la instancia de ServiceNow.
author: shawntabrizi
services: service-health
documentationcenter: service-health
ms.assetid: 
ms.service: service-health
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/14/2017
ms.author: shtabriz
ms.openlocfilehash: 625718ab82443c897d1b15c2eac51dea3d0dfeb4
ms.sourcegitcommit: afc78e4fdef08e4ef75e3456fdfe3709d3c3680b
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 11/16/2017
---
# <a name="configure-service-health-alerts-with-servicenow"></a>Configuración de alertas de estado del servicio con ServiceNow

Este artículo muestra cómo integrar las alertas de estado del servicio de Azure con ServiceNow mediante un webhook. Después de configurar la integración de webhook con su instancia de ServiceNow, obtendrá alertas a través de la infraestructura de notificación existente cuando le afecten los problemas de servicio de Azure. Cada vez que se genera una alerta de Estado del servicio de Azure, llama a un webhook a través de la API de REST con script de ServiceNow.

## <a name="creating-a-scripted-rest-api-in-servicenow"></a>Creación de una API de REST con script en ServiceNow
1.  Asegúrese de que se ha registrado y ha iniciado sesión en su cuenta de [ServiceNow](https://www.servicenow.com/).

2.  Vaya hasta la sección **System Web Services** (Servicios web del sistema) en ServiceNow y seleccione **Scripted REST APIs** (API de REST con script).

    ![La sección "Scripted Web Service" (Servicio web con script) en ServiceNow](./media/webhook-alerts/servicenow-sws-section.png)

3.  Seleccione **New** (Nuevo) para crear un nuevo servicio de REST con script.
 
    ![El botón "New Scripted REST API" (Nueva API de REST con script) en ServiceNow](./media/webhook-alerts/servicenow-new-button.png)

4.  Agregue un **nombre** a la API de REST y establezca el **identificador de la API** en `azureservicehealth`.

5.  Seleccione **Submit** (Enviar).

    !["REST API Settings" (Configuración de la API de REST) en ServiceNow](./media/webhook-alerts/servicenow-restapi-settings.png)

6.  Seleccione la API de REST que creó, y, en la pestaña **Resources** (Recursos), seleccione **New** (Nuevo).

    ![La pestaña "Resources" (Recursos) en ServiceNow](./media/webhook-alerts/servicenow-resources-tab.png)

7.  **Nombre** el nuevo recurso `event` y cambie el **método HTTP** a `POST`.

8.  En la sección **Script**, agregue el siguiente código JavaScript:

    >[!NOTE]
    >Debe actualizar los valores `<secret>`, `<group>` y `<email>` en el siguiente script.
    >* `<secret>` debe ser una cadena aleatoria, como un GUID.
    >* `<group>` debe ser el grupo de ServiceNow al que desea asignar el incidente.
    >* `<email>` debe ser la persona específica a la que desea asignar el incidente (opcional).
    >

    ```javascript
    (function process( /*RESTAPIRequest*/ request, /*RESTAPIResponse*/ response) {
        var apiKey = request.queryParams['apiKey'];
        var secret = '<secret>';
        if (apiKey == secret) {
            var event = request.body.data;
            var responseBody = {};
            if (event.data.context.activityLog.operationName == 'Microsoft.ServiceHealth/incident/action') {
                var inc = new GlideRecord('incident');
                var incidentExists = false;
                inc.addQuery('number', event.data.context.activityLog.properties.trackingId);
                inc.query();
                if (inc.hasNext()) {
                    incidentExists = true;
                    inc.next();
                } else {
                    inc.initialize();
                }
                var short_description = "Azure Service Health";
                if (event.data.context.activityLog.properties.incidentType == "Incident") {
                    short_description += " - Service Issue - ";
                } else if (event.data.context.activityLog.properties.incidentType == "Maintenance") {
                    short_description += " - Planned Maintenance - ";
                } else if (event.data.context.activityLog.properties.incidentType == "Information" || event.data.context.activityLog.properties.incidentType == "ActionRequired") {
                    short_description += " - Health Advisory - ";
                }
                short_description += event.data.context.activityLog.properties.title;
                inc.short_description = short_description;
                inc.description = event.data.context.activityLog.properties.communication;
                inc.work_notes = "Impacted subscription: " + event.data.context.activityLog.subscriptionId;
                if (incidentExists) {
                    if (event.data.context.activityLog.properties.stage == 'Active') {
                        inc.state = 2;
                    } else if (event.data.context.activityLog.properties.stage == 'Resolved') {
                        inc.state = 6;
                    } else if (event.data.context.activityLog.properties.stage == 'Closed') {
                        inc.state = 7;
                    }
                    inc.update();
                    responseBody.message = "Incident updated.";
                } else {
                    inc.number = event.data.context.activityLog.properties.trackingId;
                    inc.state = 1;
                    inc.impact = 2;
                    inc.urgency = 2;
                    inc.priority = 2;
                    inc.assigned_to = '<email>';
                    inc.assignment_group.setDisplayValue('<group>');
                    var subscriptionId = event.data.context.activityLog.subscriptionId;
                    var comments = "Azure portal Link: https://app.azure.com/h";
                    comments += "/" + event.data.context.activityLog.properties.trackingId;
                    comments += "/" + subscriptionId.substring(0, 3) + subscriptionId.slice(-3);
                    var impactedServices = JSON.parse(event.data.context.activityLog.properties.impactedServices);
                    var impactedServicesFormatted = "";
                    for (var i = 0; i < impactedServices.length; i++) {
                        impactedServicesFormatted += impactedServices[i].ServiceName + ": ";
                        for (var j = 0; j < impactedServices[i].ImpactedRegions.length; j++) {
                            if (j != 0) {
                                impactedServicesFormatted += ", ";
                            }
                            impactedServicesFormatted += impactedServices[i].ImpactedRegions[j].RegionName;
                        }

                        impactedServicesFormatted += "\n";

                    }
                    comments += "\n\nImpacted Services:\n" + impactedServicesFormatted;
                    inc.comments = comments;
                    inc.insert();
                    responseBody.message = "Incident created.";
                }
            } else {
                responseBody.message = "Hello from the other side!";
            }
            response.setBody(responseBody);
        } else {
            var unauthorized = new sn_ws_err.ServiceError();
            unauthorized.setStatus(401);
            unauthorized.setMessage('Invalid apiKey');
            response.setError(unauthorized);
        }
    })(request, response);
    ```

9.  En la pestaña de seguridad, desactive la opción **Requires authentication** (Requiere autenticación) y seleccione **Submit** (Enviar). El `<secret>` establecido protege esta API.

    ![La casilla "Requires Authentication" (Requiere autenticación) en ServiceNow](./media/webhook-alerts/servicenow-resource-settings.png)

10.  Si volvemos a la sección Scripted REST APIs (API de REST con script), debe encontrar la **ruta de la API base** para la nueva API de REST:

     ![La "ruta de la API base" in ServiceNow](./media/webhook-alerts/servicenow-base-api-path.png)

11.  La dirección URL completa de integración tiene el siguiente aspecto:
        
         https://<yourInstanceName>.service-now.com/<baseApiPath>?apiKey=<secret>


## <a name="create-an-alert-using-servicenow-in-the-azure-portal"></a>Creación de una alerta con ServiceNow en Azure Portal
### <a name="for-a-new-action-group"></a>Para un nuevo grupo de acciones:
1. Siga los pasos del 1 al 8 en [este artículo](../monitoring-and-diagnostics/monitoring-activity-log-alerts-on-service-notifications.md) para crear una alerta con un nuevo grupo de acciones.

2. Defina la lista de **acciones**:

    a. **Tipo de acción**: *webhook*

    b. **Detalles**: la **dirección URL de integración** de ServiceNow guardada anteriormente.

    c. **Nombre**: el identificador, alias o nombre de webhook.

3. Seleccione **Guardar** cuando termine para crear la alerta.

### <a name="for-an-existing-action-group"></a>Para un grupo de acciones existentes:
1. En [Azure Portal](https://portal.azure.com/), seleccione **Supervisión**.

2. En la sección **Configuración**, seleccione **Grupos de acciones**.

3. Busque el grupo de acciones que desee editar.

4. Defina la lista de **acciones**:

    a. **Tipo de acción**: *webhook*

    b. **Detalles**: la **dirección URL de integración** de ServiceNow guardada anteriormente.

    c. **Nombre**: el identificador, alias o nombre de webhook.

5. Cuando termine de actualizar el grupo de acciones, seleccione **Guardar**.

## <a name="testing-your-webhook-integration-via-an-http-post-request"></a>Prueba de la integración de webhook a través de una solicitud HTTP POST
1. Creae la carga de estado del servicio que desee enviar. Puede encontrar una carga de webhook de estado del servicio de ejemplo en [Webhooks para alertas del registro de actividad de Azure](../monitoring-and-diagnostics/monitoring-activity-log-alerts-webhook.md).

2. Cree una solicitud HTTP POST de la siguiente manera:

    ```
    POST        https://<yourInstanceName>.service-now.com/<baseApiPath>?apiKey=<secret>

    HEADERS     Content-Type: application/json

    BODY        <Service Health payload>
    ```
3. Debe recibir una respuesta `200 OK` con el mensaje "Incident created" (Incidente creado).

4. Vaya a [ServiceNow](https://www.servicenow.com/) para confirmar que la integración se ha configurado correctamente.

## <a name="next-steps"></a>Pasos siguientes
- Obtenga información acerca de cómo [configurar notificaciones de webhook para los sistemas de administración de problemas existentes](service-health-alert-webhook-guide.md).
- Revise el [Esquema de webhook de alertas del registro de actividad](../monitoring-and-diagnostics/monitoring-activity-log-alerts-webhook.md). 
- Más información acerca de las [Notificaciones del estado del servicio](../monitoring-and-diagnostics/monitoring-service-notifications.md).
- Más información sobre los [grupos de acciones](../monitoring-and-diagnostics/monitoring-action-groups.md).