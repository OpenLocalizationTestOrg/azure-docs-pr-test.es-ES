---
title: Acceso seguro a Azure Logic Apps | Microsoft Docs
description: "Aumente la seguridad para proteger el acceso a desencadenadores, entradas y salidas, parámetros de acción y servicios que se utilizan con flujos de trabajo en Azure Logic Apps."
services: logic-apps
documentationcenter: .net,nodejs,java
author: jeffhollan
manager: anneta
editor: 
ms.assetid: 9fab1050-cfbc-4a8b-b1b3-5531bee92856
ms.service: logic-apps
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: integration
ms.date: 11/22/2016
ms.author: LADocs; jehollan
ms.openlocfilehash: 0528d660f590e106f61729f10f8f68da3fe58cb7
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/29/2017
---
# <a name="secure-access-to-your-logic-apps"></a><span data-ttu-id="15198-103">Acceso seguro a aplicaciones lógicas</span><span class="sxs-lookup"><span data-stu-id="15198-103">Secure access to your logic apps</span></span>

<span data-ttu-id="15198-104">Hay muchas herramientas disponibles que le ayudarán a proteger la aplicación lógica.</span><span class="sxs-lookup"><span data-stu-id="15198-104">There are many tools available to help you secure your logic app.</span></span>

* <span data-ttu-id="15198-105">Protección del acceso para desencadenar una aplicación lógica (desencadenador de solicitud de HTTP)</span><span class="sxs-lookup"><span data-stu-id="15198-105">Securing access to trigger a logic app (HTTP Request Trigger)</span></span>
* <span data-ttu-id="15198-106">Protección del acceso para administrar, editar o leer una aplicación lógica</span><span class="sxs-lookup"><span data-stu-id="15198-106">Securing access to manage, edit, or read a logic app</span></span>
* <span data-ttu-id="15198-107">Protección del acceso al contenido de entradas y salidas para una ejecución</span><span class="sxs-lookup"><span data-stu-id="15198-107">Securing access to contents of inputs and outputs for a run</span></span>
* <span data-ttu-id="15198-108">Protección de parámetros o entradas en las acciones de un flujo de trabajo</span><span class="sxs-lookup"><span data-stu-id="15198-108">Securing parameters or inputs within actions in a workflow</span></span>
* <span data-ttu-id="15198-109">Protección del acceso a los servicios que reciben solicitudes de un flujo de trabajo</span><span class="sxs-lookup"><span data-stu-id="15198-109">Securing access to services that receive requests from a workflow</span></span>

## <a name="secure-access-to-trigger"></a><span data-ttu-id="15198-110">Acceso seguro al desencadenador</span><span class="sxs-lookup"><span data-stu-id="15198-110">Secure access to trigger</span></span>

<span data-ttu-id="15198-111">Cuando se trabaja con una aplicación lógica que se activa con una solicitud HTTP ([solicitud](../connectors/connectors-native-reqres.md) o [webhook](../connectors/connectors-native-webhook.md)), puede restringir el acceso a aquellos clientes autorizados que pueden activar la aplicación lógica.</span><span class="sxs-lookup"><span data-stu-id="15198-111">When you work with a logic app that fires on an HTTP Request ([Request](../connectors/connectors-native-reqres.md) or [Webhook](../connectors/connectors-native-webhook.md)), you can restrict access so that only authorized clients can fire the logic app.</span></span> <span data-ttu-id="15198-112">Todas las solicitudes en una aplicación lógica se cifrarán y se protegerán mediante SSL.</span><span class="sxs-lookup"><span data-stu-id="15198-112">All requests into a logic app are encrypted and secured via SSL.</span></span>

### <a name="shared-access-signature"></a><span data-ttu-id="15198-113">Firma de acceso compartido</span><span class="sxs-lookup"><span data-stu-id="15198-113">Shared Access Signature</span></span>

<span data-ttu-id="15198-114">Cada punto de conexión de la solicitud para una aplicación lógica incluye una [Firma de acceso compartido](../storage/common/storage-dotnet-shared-access-signature-part-1.md) (SAS) como parte de la dirección URL.</span><span class="sxs-lookup"><span data-stu-id="15198-114">Every request endpoint for a logic app includes a [Shared Access Signature (SAS)](../storage/common/storage-dotnet-shared-access-signature-part-1.md) as part of the URL.</span></span> <span data-ttu-id="15198-115">Cada dirección URL contiene un parámetro de consulta `sp`, `sv` y `sig`.</span><span class="sxs-lookup"><span data-stu-id="15198-115">Each URL contains a `sp`, `sv`, and `sig` query parameter.</span></span> <span data-ttu-id="15198-116">Los permisos se especifican mediante `sp` y se corresponden a los métodos HTTP permitidos, `sv` es la versión utilizada para generar y `sig` se usa para autenticar el acceso al desencadenador.</span><span class="sxs-lookup"><span data-stu-id="15198-116">Permissions are specified by `sp`, and correspond to HTTP methods allowed, `sv` is the version used to generate, and `sig` is used to authenticate access to trigger.</span></span> <span data-ttu-id="15198-117">La firma se genera mediante el algoritmo SHA256 con una clave secreta en todas las rutas de acceso de direcciones URL y propiedades.</span><span class="sxs-lookup"><span data-stu-id="15198-117">The signature is generated using the SHA256 algorithm with a secret key on all the URL paths and properties.</span></span> <span data-ttu-id="15198-118">La clave secreta nunca se expone ni se publica, y se mantiene cifrada y almacenada como parte de la aplicación lógica.</span><span class="sxs-lookup"><span data-stu-id="15198-118">The secret key is never exposed and published, and is kept encrypted and stored as part of the logic app.</span></span> <span data-ttu-id="15198-119">La aplicación lógica solo autoriza desencadenadores que contienen una firma válida creada con la clave secreta.</span><span class="sxs-lookup"><span data-stu-id="15198-119">Your logic app only authorizes triggers that contain a valid signature created with the secret key.</span></span>

#### <a name="regenerate-access-keys"></a><span data-ttu-id="15198-120">Regenerar las claves de acceso</span><span class="sxs-lookup"><span data-stu-id="15198-120">Regenerate access keys</span></span>

<span data-ttu-id="15198-121">Puede volver a generar una nueva clave segura en cualquier momento mediante la API de REST o Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="15198-121">You can regenerate a new secure key at anytime through the REST API or Azure portal.</span></span> <span data-ttu-id="15198-122">Todas las direcciones URL actuales generadas anteriormente con la clave antigua se invalidan y dejan de estar autorizadas para activar la aplicación lógica.</span><span class="sxs-lookup"><span data-stu-id="15198-122">All current URLs that were generated previously using the old key are invalidated and no longer authorized to fire the logic app.</span></span>

1. <span data-ttu-id="15198-123">En Azure Portal, abra la aplicación lógica para la que desea volver a generar una clave.</span><span class="sxs-lookup"><span data-stu-id="15198-123">In the Azure portal, open the logic app you want to regenerate a key</span></span>
1. <span data-ttu-id="15198-124">Haga clic en el elemento de menú **Access Keys** (Claves de acceso) en **Settings** (Configuración).</span><span class="sxs-lookup"><span data-stu-id="15198-124">Click the **Access Keys** menu item under **Settings**</span></span>
1. <span data-ttu-id="15198-125">Elija la clave que se va a regenerar y complete el proceso.</span><span class="sxs-lookup"><span data-stu-id="15198-125">Choose the key to regenerate and complete the process</span></span>

<span data-ttu-id="15198-126">Las direcciones URL que se recuperan tras la regeneración se firman con la nueva clave de acceso.</span><span class="sxs-lookup"><span data-stu-id="15198-126">URLs you retrieve after regeneration are signed with the new access key.</span></span>

#### <a name="creating-callback-urls-with-an-expiration-date"></a><span data-ttu-id="15198-127">Creación de direcciones URL de devolución de llamada con una fecha de expiración</span><span class="sxs-lookup"><span data-stu-id="15198-127">Creating callback URLs with an expiration date</span></span>

<span data-ttu-id="15198-128">Si va a compartir la dirección URL con terceros, puede generar direcciones URL con claves específicas y fechas de caducidad según sea necesario.</span><span class="sxs-lookup"><span data-stu-id="15198-128">If you are sharing the URL with other parties, you can generate URLs with specific keys and expiration dates as needed.</span></span> <span data-ttu-id="15198-129">De esta forma puede acumular claves sin problema, o asegurarse de que el acceso para activar una aplicación está restringido a un determinado intervalo de tiempo.</span><span class="sxs-lookup"><span data-stu-id="15198-129">You can then seamlessly roll keys, or ensure access to fire an app is restricted to a certain timespan.</span></span> <span data-ttu-id="15198-130">Puede especificar una fecha de expiración para una dirección URL a través de la [API de REST de Logic Apps](https://docs.microsoft.com/rest/api/logic/workflowtriggers):</span><span class="sxs-lookup"><span data-stu-id="15198-130">You can specify an expiration date for a URL through the [logic apps REST API](https://docs.microsoft.com/rest/api/logic/workflowtriggers):</span></span>

``` http
POST 
/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Logic/workflows/{workflowName}/triggers/{triggerName}/listCallbackUrl?api-version=2016-06-01
```

<span data-ttu-id="15198-131">En el cuerpo, incluya la propiedad `NotAfter` como una cadena de fecha JSON, que devuelve una dirección URL de devolución de llamada que solo es válida hasta la fecha y hora `NotAfter`.</span><span class="sxs-lookup"><span data-stu-id="15198-131">In the body, include the property `NotAfter` as a JSON date string, which returns a callback URL that is only valid until the `NotAfter` date and time.</span></span>

#### <a name="creating-urls-with-primary-or-secondary-secret-key"></a><span data-ttu-id="15198-132">Creación de direcciones URL con clave secreta principal o secundaria</span><span class="sxs-lookup"><span data-stu-id="15198-132">Creating URLs with primary or secondary secret key</span></span>

<span data-ttu-id="15198-133">Al generar o enumerar direcciones URL de devolución de llamada para desencadenadores basados en solicitud, también puede especificar qué clave se va a usar para firmar la dirección URL.</span><span class="sxs-lookup"><span data-stu-id="15198-133">When you generate or list callback URLs for request-based triggers, you can also specify which key to use to sign the URL.</span></span>  <span data-ttu-id="15198-134">Puede generar una dirección URL firmada por una clave específica a través de la [API de REST de Logic Apps](https://docs.microsoft.com/rest/api/logic/workflowtriggers), tal como se indica a continuación:</span><span class="sxs-lookup"><span data-stu-id="15198-134">You can generate a URL signed by a specific key through the [logic apps REST API](https://docs.microsoft.com/rest/api/logic/workflowtriggers) as follows:</span></span>

``` http
POST 
/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Logic/workflows/{workflowName}/triggers/{triggerName}/listCallbackUrl?api-version=2016-06-01
```

<span data-ttu-id="15198-135">En el cuerpo, incluya la propiedad `KeyType` como `Primary` o `Secondary`.</span><span class="sxs-lookup"><span data-stu-id="15198-135">In the body, include the property `KeyType` as either `Primary` or `Secondary`.</span></span>  <span data-ttu-id="15198-136">Esto devuelve una dirección URL firmada por la clave segura especificada.</span><span class="sxs-lookup"><span data-stu-id="15198-136">This returns a URL signed by the secure key specified.</span></span>

### <a name="restrict-incoming-ip-addresses"></a><span data-ttu-id="15198-137">Restricción de las direcciones IP entrantes</span><span class="sxs-lookup"><span data-stu-id="15198-137">Restrict incoming IP addresses</span></span>

<span data-ttu-id="15198-138">Además de la Firma de acceso compartido, es posible que desee restringir las llamadas a una aplicación lógica solo desde clientes específicos.</span><span class="sxs-lookup"><span data-stu-id="15198-138">In addition to the Shared Access Signature, you may wish to restrict calling a logic app only from specific clients.</span></span>  <span data-ttu-id="15198-139">Por ejemplo, si administra el punto de conexión a través de Azure API Management, puede restringir la aplicación lógica para que acepte únicamente la solicitud cuando esta provenga de la dirección IP de la instancia de API Management.</span><span class="sxs-lookup"><span data-stu-id="15198-139">For example, if you manage your endpoint through Azure API Management, you can restrict the logic app to only accept the request when the request comes from the API Management instance IP address.</span></span>

<span data-ttu-id="15198-140">Esta opción se puede configurar en la configuración de la aplicación lógica:</span><span class="sxs-lookup"><span data-stu-id="15198-140">This setting can be configured within the logic app settings:</span></span>

1. <span data-ttu-id="15198-141">En Azure Portal, abra la aplicación lógica a la que desea agregar las restricciones de dirección IP</span><span class="sxs-lookup"><span data-stu-id="15198-141">In the Azure portal, open the logic app you want to add IP address restrictions</span></span>
1. <span data-ttu-id="15198-142">Haga clic en el elemento de menú **Access control configuration** (Configuración de control de acceso) en **Settings** (Configuración).</span><span class="sxs-lookup"><span data-stu-id="15198-142">Click the **Access control configuration** menu item under **Settings**</span></span>
1. <span data-ttu-id="15198-143">Especifique la lista de intervalos de direcciones IP que van a ser aceptados por el desencadenador.</span><span class="sxs-lookup"><span data-stu-id="15198-143">Specify the list of IP address ranges to be accepted by the trigger</span></span>

<span data-ttu-id="15198-144">Un intervalo IP válido adopta el formato `192.168.1.1/255`.</span><span class="sxs-lookup"><span data-stu-id="15198-144">A valid IP range takes the format `192.168.1.1/255`.</span></span> <span data-ttu-id="15198-145">Si quiere que la aplicación lógica solo se active como una aplicación lógica anidada, seleccione la opción **Solo otras aplicaciones lógicas**.</span><span class="sxs-lookup"><span data-stu-id="15198-145">If you want the logic app to only fire as a nested logic app, select the **Only other logic apps** option.</span></span> <span data-ttu-id="15198-146">Esta opción escribe una matriz vacía en el recurso, lo que significa que solo las llamadas realizadas desde el mismo servicio (aplicaciones lógicas principales) se activan correctamente.</span><span class="sxs-lookup"><span data-stu-id="15198-146">This option writes an empty array to the resource, meaning only calls from the service itself (parent logic apps) fire successfully.</span></span>

> [!NOTE]
> <span data-ttu-id="15198-147">Todavía puede ejecutar una aplicación de lógica con un desencadenador de solicitud a través de la API de REST/Management `/triggers/{triggerName}/run`, con independencia de la IP.</span><span class="sxs-lookup"><span data-stu-id="15198-147">You can still run a logic app with a request trigger through the REST API / Management `/triggers/{triggerName}/run` regardless of IP.</span></span> <span data-ttu-id="15198-148">Este escenario requiere la autenticación con la API de REST de Azure y todos los eventos podrían aparecer en el registro de auditoría de Azure.</span><span class="sxs-lookup"><span data-stu-id="15198-148">This scenario requires authentication against the Azure REST API, and all events would appear in the Azure Audit Log.</span></span> <span data-ttu-id="15198-149">Establezca las directivas de control de acceso en consecuencia.</span><span class="sxs-lookup"><span data-stu-id="15198-149">Set access control policies accordingly.</span></span>

#### <a name="setting-ip-ranges-on-the-resource-definition"></a><span data-ttu-id="15198-150">Establecimiento de los intervalos de IP en la definición de recursos</span><span class="sxs-lookup"><span data-stu-id="15198-150">Setting IP ranges on the resource definition</span></span>

<span data-ttu-id="15198-151">Si está usando una [plantilla de implementación](logic-apps-create-deploy-template.md) para automatizar las implementaciones, los valores del intervalo de IP pueden configurarse en la plantilla de recursos.</span><span class="sxs-lookup"><span data-stu-id="15198-151">If you are using a [deployment template](logic-apps-create-deploy-template.md) to automate your deployments, the IP range settings can be configured on the resource template.</span></span>  

``` json
{
    "properties": {
        "definition": {
        },
        "parameters": {},
        "accessControl": {
            "triggers": {
                "allowedCallerIpAddresses": [
                    {
                        "addressRange": "192.168.12.0/23"
                    },
                    {
                        "addressRange": "2001:0db8::/64"
                    }
                ]
            }
        }
    },
    "type": "Microsoft.Logic/workflows"
}

```

### <a name="adding-azure-active-directory-oauth-or-other-security"></a><span data-ttu-id="15198-152">Adición de Azure Active Directory, OAuth u otra seguridad</span><span class="sxs-lookup"><span data-stu-id="15198-152">Adding Azure Active Directory, OAuth, or other security</span></span>

<span data-ttu-id="15198-153">Para agregar más protocolos de autorización basados en una aplicación lógica, [Azure API Management](https://azure.microsoft.com/services/api-management/) ofrece supervisión enriquecida, seguridad, directivas y documentación para cualquier punto de conexión con la funcionalidad de exponer una aplicación lógica como una API.</span><span class="sxs-lookup"><span data-stu-id="15198-153">To add more authorization protocols on top of a logic app, [Azure API Management](https://azure.microsoft.com/services/api-management/) offers rich monitoring, security, policy, and documentation for any endpoint with the capability to expose a logic app as an API.</span></span> <span data-ttu-id="15198-154">Azure API Management puede exponer un punto de conexión público o privado para la aplicación lógica, que podría usar Azure Active Directory, certificados, OAuth u otros estándares de seguridad.</span><span class="sxs-lookup"><span data-stu-id="15198-154">Azure API Management can expose a public or private endpoint for the logic app, which could use Azure Active Directory, certificate, OAuth, or other security standards.</span></span> <span data-ttu-id="15198-155">Cuando se recibe una solicitud, Azure API Management la reenvía a la aplicación lógica (realizando las transformaciones o restricciones necesarias sobre la marcha).</span><span class="sxs-lookup"><span data-stu-id="15198-155">When a request is received, Azure API Management forwards the request to the logic app (performing any needed transformations or restrictions in-flight).</span></span> <span data-ttu-id="15198-156">Puede usar los valores del intervalo IP entrantes en la aplicación lógica para permitir solo que la aplicación lógica se desencadene desde API Management.</span><span class="sxs-lookup"><span data-stu-id="15198-156">You can use the incoming IP range settings on the logic app to only allow the logic app to be triggered from API Management.</span></span>

## <a name="secure-access-to-manage-or-edit-logic-apps"></a><span data-ttu-id="15198-157">Protección del acceso para administrar o modificar aplicaciones lógicas</span><span class="sxs-lookup"><span data-stu-id="15198-157">Secure access to manage or edit logic apps</span></span>

<span data-ttu-id="15198-158">Puede restringir el acceso a las operaciones de administración en una aplicación lógica para que solo determinados usuarios o grupos puedan realizar operaciones en el recurso.</span><span class="sxs-lookup"><span data-stu-id="15198-158">You can restrict access to management operations on a logic app so that only specific users or groups are able to perform operations on the resource.</span></span> <span data-ttu-id="15198-159">Las aplicaciones lógicas usan la característica de Azure [Control de acceso basado en rol (RBAC)](../active-directory/role-based-access-control-configure.md), y se puede personalizar con las mismas herramientas.</span><span class="sxs-lookup"><span data-stu-id="15198-159">Logic apps use the Azure [Role-Based Access Control (RBAC)](../active-directory/role-based-access-control-configure.md) feature, and can be customized with the same tools.</span></span>  <span data-ttu-id="15198-160">Hay algunas funciones integradas que puede asignar también a los miembros de la suscripción:</span><span class="sxs-lookup"><span data-stu-id="15198-160">There are a few built-in roles you can assign members of your subscription to as well:</span></span>

* <span data-ttu-id="15198-161">**Colaborador de aplicación lógica**: proporciona acceso para consultar, modificar y actualizar una aplicación lógica.</span><span class="sxs-lookup"><span data-stu-id="15198-161">**Logic App Contributor** - Provides access to view, edit, and update a logic app.</span></span>  <span data-ttu-id="15198-162">No puede quitar el recurso ni realizar operaciones de administración.</span><span class="sxs-lookup"><span data-stu-id="15198-162">Cannot remove the resource or perform admin operations.</span></span>
* <span data-ttu-id="15198-163">**Operador de aplicación lógica**: puede consultar la aplicación lógica y el historial de ejecución, así como habilitarla o deshabilitarla.</span><span class="sxs-lookup"><span data-stu-id="15198-163">**Logic App Operator** - Can view the logic app and run history, and enable/disable.</span></span>  <span data-ttu-id="15198-164">No puede modificar ni actualizar la definición.</span><span class="sxs-lookup"><span data-stu-id="15198-164">Cannot edit or update the definition.</span></span>

<span data-ttu-id="15198-165">También puede usar el [bloqueo de recurso de Azure](../azure-resource-manager/resource-group-lock-resources.md) para evitar cambiar o eliminar aplicaciones lógicas.</span><span class="sxs-lookup"><span data-stu-id="15198-165">You can also use [Azure Resource Lock](../azure-resource-manager/resource-group-lock-resources.md) to prevent changing or deleting logic apps.</span></span> <span data-ttu-id="15198-166">Esta funcionalidad es útil para evitar que los recursos de producción se modifiquen o eliminen.</span><span class="sxs-lookup"><span data-stu-id="15198-166">This capability is valuable to prevent production resources from changes or deletions.</span></span>

## <a name="secure-access-to-contents-of-the-run-history"></a><span data-ttu-id="15198-167">Protección del acceso al contenido del historial de ejecución</span><span class="sxs-lookup"><span data-stu-id="15198-167">Secure access to contents of the run history</span></span>

<span data-ttu-id="15198-168">Puede restringir el acceso al contenido de entradas o salidas de ejecuciones anteriores a intervalos de direcciones IP específicos.</span><span class="sxs-lookup"><span data-stu-id="15198-168">You can restrict access to contents of inputs or outputs from previous runs to specific IP address ranges.</span></span>  

<span data-ttu-id="15198-169">Todos los datos dentro de una ejecución de flujo de trabajo se cifran en tránsito y en reposo.</span><span class="sxs-lookup"><span data-stu-id="15198-169">All data within a workflow run is encrypted in transit and at rest.</span></span> <span data-ttu-id="15198-170">Cuando se realiza una llamada al historial de ejecución, el servicio autentica la solicitud y proporciona vínculos a las entradas y salidas de las solicitudes y respuestas.</span><span class="sxs-lookup"><span data-stu-id="15198-170">When a call to run history is made, the service authenticates the request and provides links to the request and response inputs and outputs.</span></span> <span data-ttu-id="15198-171">Este vínculo se puede proteger para que solo las solicitudes para consultar contenido de un intervalo de direcciones IP designado devuelvan contenido.</span><span class="sxs-lookup"><span data-stu-id="15198-171">This link can be protected so only requests to view content from a designated IP address range return the contents.</span></span> <span data-ttu-id="15198-172">Puede utilizar esta funcionalidad para el control de acceso adicional.</span><span class="sxs-lookup"><span data-stu-id="15198-172">You can use this capability for additional access control.</span></span> <span data-ttu-id="15198-173">Incluso puede especificar una dirección IP como `0.0.0.0` para que nadie tenga acceso a las entradas o salidas.</span><span class="sxs-lookup"><span data-stu-id="15198-173">You could even specify an IP address like `0.0.0.0` so no one could access inputs/outputs.</span></span> <span data-ttu-id="15198-174">Solo un usuario con permisos de administrador puede quitar esta restricción, ofreciendo la posibilidad de un acceso 'Just-in-time' al contenido de flujo de trabajo.</span><span class="sxs-lookup"><span data-stu-id="15198-174">Only someone with admin permissions could remove this restriction, providing the possibility for 'just-in-time' access to workflow contents.</span></span>

<span data-ttu-id="15198-175">Esta opción se puede configurar en la configuración de los recursos de Azure Portal:</span><span class="sxs-lookup"><span data-stu-id="15198-175">This setting can be configured within the resource settings of the Azure portal:</span></span>

1. <span data-ttu-id="15198-176">En Azure Portal, abra la aplicación lógica a la que desea agregar las restricciones de dirección IP</span><span class="sxs-lookup"><span data-stu-id="15198-176">In the Azure portal, open the logic app you want to add IP address restrictions</span></span>
1. <span data-ttu-id="15198-177">Haga clic en el elemento de menú **Access control configuration** (Configuración de control de acceso) en **Settings** (Configuración).</span><span class="sxs-lookup"><span data-stu-id="15198-177">Click the **Access control configuration** menu item under **Settings**</span></span>
1. <span data-ttu-id="15198-178">Especifique la lista de intervalos de direcciones IP para acceder al contenido.</span><span class="sxs-lookup"><span data-stu-id="15198-178">Specify the list of IP address ranges for access to content</span></span>

#### <a name="setting-ip-ranges-on-the-resource-definition"></a><span data-ttu-id="15198-179">Establecimiento de los intervalos de IP en la definición de recursos</span><span class="sxs-lookup"><span data-stu-id="15198-179">Setting IP ranges on the resource definition</span></span>

<span data-ttu-id="15198-180">Si está usando una [plantilla de implementación](logic-apps-create-deploy-template.md) para automatizar las implementaciones, los valores del intervalo de IP pueden configurarse en la plantilla de recursos.</span><span class="sxs-lookup"><span data-stu-id="15198-180">If you are using a [deployment template](logic-apps-create-deploy-template.md) to automate your deployments, the IP range settings can be configured on the resource template.</span></span>  

``` json
{
    "properties": {
        "definition": {
        },
        "parameters": {},
        "accessControl": {
            "contents": {
                "allowedCallerIpAddresses": [
                    {
                        "addressRange": "192.168.12.0/23"
                    },
                    {
                        "addressRange": "2001:0db8::/64"
                    }
                ]
            }
        }
    },
    "type": "Microsoft.Logic/workflows"
}
```

## <a name="secure-parameters-and-inputs-within-a-workflow"></a><span data-ttu-id="15198-181">Parámetros seguros y entradas dentro de un flujo de trabajo</span><span class="sxs-lookup"><span data-stu-id="15198-181">Secure parameters and inputs within a workflow</span></span>

<span data-ttu-id="15198-182">Puede desear parametrizar algunos aspectos de una definición de flujo de trabajo para una implementación a través de entornos.</span><span class="sxs-lookup"><span data-stu-id="15198-182">You might want to parameterize some aspects of a workflow definition for deployment across environments.</span></span> <span data-ttu-id="15198-183">Además, algunos parámetros pueden ser parámetros seguros que no desea que aparezcan al editar un flujo de trabajo, como un identificador de cliente y el secreto del cliente para la [autenticación de Azure Active Directory](../connectors/connectors-native-http.md#authentication) de una acción HTTP.</span><span class="sxs-lookup"><span data-stu-id="15198-183">Also, some parameters might be secure parameters you don't want to appear when editing a workflow, such as a client ID and client secret for [Azure Active Directory authentication](../connectors/connectors-native-http.md#authentication) of an HTTP action.</span></span>

### <a name="using-parameters-and-secure-parameters"></a><span data-ttu-id="15198-184">Uso de parámetros y parámetros seguros</span><span class="sxs-lookup"><span data-stu-id="15198-184">Using parameters and secure parameters</span></span>

<span data-ttu-id="15198-185">Para acceder al valor de un parámetro de recurso en tiempo de ejecución, el [lenguaje de definición de flujo de trabajo](http://aka.ms/logicappsdocs) proporciona una operación `@parameters()`.</span><span class="sxs-lookup"><span data-stu-id="15198-185">To access the value of a resource parameter at runtime, the [workflow definition language](http://aka.ms/logicappsdocs) provides a `@parameters()` operation.</span></span> <span data-ttu-id="15198-186">Además, puede [especificar parámetros en la plantilla de implementación de recursos](../azure-resource-manager/resource-group-authoring-templates.md#parameters).</span><span class="sxs-lookup"><span data-stu-id="15198-186">Also, you can [specify parameters in the resource deployment template](../azure-resource-manager/resource-group-authoring-templates.md#parameters).</span></span> <span data-ttu-id="15198-187">No obstante, si especifica el tipo de parámetro como `securestring`, el parámetro no se devolverá con el resto de la definición de recurso, lo que significa que no será accesible al visualizar el recurso después de la implementación.</span><span class="sxs-lookup"><span data-stu-id="15198-187">But if you specify the parameter type as `securestring`, the parameter won't be returned with the rest of the resource definition, and won't be accessible by viewing the resource after deployment.</span></span>

> [!NOTE]
> <span data-ttu-id="15198-188">Si el parámetro se usa en los encabezados o en el cuerpo de una solicitud, el parámetro se puede ver al acceder al historial de ejecución y a la solicitud HTTP saliente.</span><span class="sxs-lookup"><span data-stu-id="15198-188">If your parameter is used in the headers or body of a request, the parameter might be visible by accessing the run history and outgoing HTTP request.</span></span> <span data-ttu-id="15198-189">Asegúrese de configurar las directivas de acceso al contenido en consecuencia.</span><span class="sxs-lookup"><span data-stu-id="15198-189">Make sure to set your content access policies accordingly.</span></span>
> <span data-ttu-id="15198-190">Los encabezados de autorización nunca son visibles a través de entradas o salidas.</span><span class="sxs-lookup"><span data-stu-id="15198-190">Authorization headers are never visible through inputs or outputs.</span></span> <span data-ttu-id="15198-191">Por tanto, si el secreto se usa ahí, este no se puede recuperar.</span><span class="sxs-lookup"><span data-stu-id="15198-191">So if the secret is being used there, the secret is not retrievable.</span></span>

#### <a name="resource-deployment-template-with-secrets"></a><span data-ttu-id="15198-192">Plantilla de implementación de recursos con secretos</span><span class="sxs-lookup"><span data-stu-id="15198-192">Resource deployment template with secrets</span></span>

<span data-ttu-id="15198-193">A continuación se presenta un ejemplo en que se muestra una implementación que hace referencia a un parámetro seguro de `secret` en tiempo de ejecución.</span><span class="sxs-lookup"><span data-stu-id="15198-193">The following example shows a deployment that references a secure parameter of `secret` at runtime.</span></span> <span data-ttu-id="15198-194">En un archivo de parámetros independiente podría especificar el valor de entorno para `secret` o usar el [almacén de claves de Azure Resource Manager](../azure-resource-manager/resource-manager-keyvault-parameter.md) para recuperar los secretos en tiempo de implementación.</span><span class="sxs-lookup"><span data-stu-id="15198-194">In a separate parameters file, you could specify the environment value for the `secret`, or use [Azure Resource Manager KeyVault](../azure-resource-manager/resource-manager-keyvault-parameter.md) to retrieve secrets at deploy time.</span></span>

``` json
{
  "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
  "contentVersion": "1.0.0.0",
  "parameters": {
    "secretDeploymentParam": {
      "type": "securestring"
    }
  },
  "variables": {},
  "resources": [
    {
      "name": "secret-deploy",
      "type": "Microsoft.Logic/workflows",
      "location": "westus",
      "tags": {
        "displayName": "LogicApp"
      },
      "apiVersion": "2016-06-01",
      "properties": {
        "definition": {
          "$schema": "https://schema.management.azure.com/providers/Microsoft.Logic/schemas/2016-06-01/workflowdefinition.json#",
          "actions": {
            "Call_External_API": {
              "type": "http",
              "inputs": {
                "headers": {
                  "Authorization": "@parameters('secret')"
                },
                "body": "This is the request"
              },
              "runAfter": {}
            }
          },
          "parameters": {
            "secret": {
              "type": "SecureString"
            }
          },
          "triggers": {
            "manual": {
              "type": "Request",
              "kind": "Http",
              "inputs": {
                "schema": {}
              }
            }
          },
          "contentVersion": "1.0.0.0",
          "outputs": {}
        },
        "parameters": {
          "secret": {
            "value": "[parameters('secretDeploymentParam')]"
          }
        }
      }
    }
  ],
  "outputs": {}
}
```

## <a name="secure-access-to-services-receiving-requests-from-a-workflow"></a><span data-ttu-id="15198-195">Protección del acceso a los servicios mediante solicitudes de un flujo de trabajo</span><span class="sxs-lookup"><span data-stu-id="15198-195">Secure access to services receiving requests from a workflow</span></span>

<span data-ttu-id="15198-196">Hay muchas maneras de ayudar a proteger los puntos de conexión a los que la aplicación lógica necesita acceder.</span><span class="sxs-lookup"><span data-stu-id="15198-196">There are many ways to help secure any endpoint the logic app needs to access.</span></span>

### <a name="using-authentication-on-outbound-requests"></a><span data-ttu-id="15198-197">Uso de la autenticación en las solicitudes salientes</span><span class="sxs-lookup"><span data-stu-id="15198-197">Using authentication on outbound requests</span></span>

<span data-ttu-id="15198-198">Cuando se trabaja con una acción HTTP, HTTP + Swagger (Open API) o webhook acción, puede agregar autenticación a la solicitud que se envía.</span><span class="sxs-lookup"><span data-stu-id="15198-198">When working with an HTTP, HTTP + Swagger (Open API), or Webhook action, you can add authentication to the request being sent.</span></span> <span data-ttu-id="15198-199">Podría incluir la autenticación básica, la autenticación de certificados o la autenticación de Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="15198-199">You could include basic authentication, certificate authentication, or Azure Active Directory authentication.</span></span> <span data-ttu-id="15198-200">Encontrará detalles sobre cómo configurar esta autenticación [en este artículo](../connectors/connectors-native-http.md#authentication).</span><span class="sxs-lookup"><span data-stu-id="15198-200">Details on how to configure this authentication can be found [in this article](../connectors/connectors-native-http.md#authentication).</span></span>

### <a name="restricting-access-to-logic-app-ip-addresses"></a><span data-ttu-id="15198-201">Restricción del acceso a direcciones IP de aplicación lógica</span><span class="sxs-lookup"><span data-stu-id="15198-201">Restricting access to logic app IP addresses</span></span>

<span data-ttu-id="15198-202">Todas las llamadas de las aplicaciones lógicas proceden de un conjunto específico de direcciones IP por región.</span><span class="sxs-lookup"><span data-stu-id="15198-202">All calls from logic apps come from a specific set of IP addresses per region.</span></span> <span data-ttu-id="15198-203">Puede agregar filtrado adicional para aceptar solo las solicitudes procedentes de esas direcciones IP designadas.</span><span class="sxs-lookup"><span data-stu-id="15198-203">You can add additional filtering to only accept requests from those designated IP addresses.</span></span> <span data-ttu-id="15198-204">Para obtener una lista de esas direcciones IP, vea [Límites y configuración de Logic Apps](logic-apps-limits-and-config.md#configuration).</span><span class="sxs-lookup"><span data-stu-id="15198-204">For a list of those IP addresses, see [logic app limits and configuration](logic-apps-limits-and-config.md#configuration).</span></span>

### <a name="on-premises-connectivity"></a><span data-ttu-id="15198-205">Conectividad local</span><span class="sxs-lookup"><span data-stu-id="15198-205">On-premises connectivity</span></span>

<span data-ttu-id="15198-206">Las aplicaciones lógicas proporcionan integración con varios servicios para ofrecer una comunicación local segura y de confianza.</span><span class="sxs-lookup"><span data-stu-id="15198-206">Logic apps provide integration with several services to provide secure and reliable on-premises communication.</span></span>

#### <a name="on-premises-data-gateway"></a><span data-ttu-id="15198-207">Puerta de enlace de datos local</span><span class="sxs-lookup"><span data-stu-id="15198-207">On-premises data gateway</span></span>

<span data-ttu-id="15198-208">Muchos de los conectores administrados de las aplicaciones lógicas proporcionan conectividad segura a sistemas locales, como el sistema de archivos, SQL, SharePoint o DB2, entre otros.</span><span class="sxs-lookup"><span data-stu-id="15198-208">Many managed connectors for logic apps provide secure connectivity to on-premises systems, including File System, SQL, SharePoint, DB2, and more.</span></span> <span data-ttu-id="15198-209">La puerta de enlace retransmite datos desde orígenes locales en canales cifrados hasta Azure Service Bus.</span><span class="sxs-lookup"><span data-stu-id="15198-209">The gateway relays data from on-premises sources on encrypted channels through the Azure Service Bus.</span></span> <span data-ttu-id="15198-210">Todo el tráfico se origina como tráfico de salida seguro desde el agente de puerta de enlace.</span><span class="sxs-lookup"><span data-stu-id="15198-210">All traffic originates as secure outbound traffic from the gateway agent.</span></span> <span data-ttu-id="15198-211">Más información sobre [cómo funciona la puerta de enlace de datos](logic-apps-gateway-install.md#gateway-cloud-service).</span><span class="sxs-lookup"><span data-stu-id="15198-211">Learn more about [how the data gateway works](logic-apps-gateway-install.md#gateway-cloud-service).</span></span>

#### <a name="azure-api-management"></a><span data-ttu-id="15198-212">Administración de API de Azure</span><span class="sxs-lookup"><span data-stu-id="15198-212">Azure API Management</span></span>

<span data-ttu-id="15198-213">[Azure API Management](https://azure.microsoft.com/services/api-management/) tiene opciones de conectividad local, incluida la integración de ExpressRoute y VPN de sitio a sitio para el proxy protegido y la comunicación en los sistemas locales.</span><span class="sxs-lookup"><span data-stu-id="15198-213">[Azure API Management](https://azure.microsoft.com/services/api-management/) has on-premises connectivity options, including site-to-site VPN and ExpressRoute integration for secured proxy and communication to on-premises systems.</span></span> <span data-ttu-id="15198-214">En el Diseñador de aplicación lógica, puede seleccionar rápidamente una API expuesta desde Azure API Management dentro de un flujo de trabajo, proporcionando acceso rápido a los sistemas locales.</span><span class="sxs-lookup"><span data-stu-id="15198-214">In the Logic App Designer, you can quickly select an API exposed from Azure API Management within a workflow, providing quick access to on-premises systems.</span></span>

#### <a name="hybrid-connections-from-azure-app-service"></a><span data-ttu-id="15198-215">Conexiones híbridas desde Azure App Service</span><span class="sxs-lookup"><span data-stu-id="15198-215">Hybrid connections from Azure App Service</span></span>

<span data-ttu-id="15198-216">Puede usar la característica de conexión híbrida local para las aplicaciones Web y API de Azure para la comunicación local.</span><span class="sxs-lookup"><span data-stu-id="15198-216">You can use the on-premises hybrid connection feature for Azure API and Web apps to communicate on-premises.</span></span>  <span data-ttu-id="15198-217">[En este artículo ](../app-service-web/web-sites-hybrid-connection-get-started.md) encontrará información sobre las conexiones híbridas y cómo configurarlas.</span><span class="sxs-lookup"><span data-stu-id="15198-217">Details on hybrid connections and how to configure can be found [in this article](../app-service-web/web-sites-hybrid-connection-get-started.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="15198-218">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="15198-218">Next steps</span></span>
[<span data-ttu-id="15198-219">Creación de una plantilla de implementación</span><span class="sxs-lookup"><span data-stu-id="15198-219">Create a deployment template</span></span>](logic-apps-create-deploy-template.md)  
[<span data-ttu-id="15198-220">Control de excepciones</span><span class="sxs-lookup"><span data-stu-id="15198-220">Exception handling</span></span>](logic-apps-exception-handling.md)  
[<span data-ttu-id="15198-221">Supervisar las aplicaciones lógicas</span><span class="sxs-lookup"><span data-stu-id="15198-221">Monitor your logic apps</span></span>](logic-apps-monitor-your-logic-apps.md)  
[<span data-ttu-id="15198-222">Diagnóstico de errores y problemas de las aplicaciones lógicas</span><span class="sxs-lookup"><span data-stu-id="15198-222">Diagnosing logic app failures and issues</span></span>](logic-apps-diagnosing-failures.md)  
