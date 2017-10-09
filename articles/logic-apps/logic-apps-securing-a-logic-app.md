---
title: "aaaSecure tener acceso a las aplicaciones lógicas tooAzure | Documentos de Microsoft"
description: "Aumenta la seguridad para la protección de acceso tootriggers, entradas y salidas, parámetros de acción y servicios que se utilizan con flujos de trabajo en las aplicaciones lógicas de Azure."
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
ms.openlocfilehash: abda2179e4cc2d2295cd8332ec017c848a456264
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="secure-access-tooyour-logic-apps"></a><span data-ttu-id="f279b-103">Proteger el acceso a las aplicaciones lógicas tooyour</span><span class="sxs-lookup"><span data-stu-id="f279b-103">Secure access tooyour logic apps</span></span>

<span data-ttu-id="f279b-104">Hay muchas herramientas toohelp disponibles que proteja la aplicación lógica.</span><span class="sxs-lookup"><span data-stu-id="f279b-104">There are many tools available toohelp you secure your logic app.</span></span>

* <span data-ttu-id="f279b-105">Protección de acceso tootrigger una aplicación lógica (desencadenador de solicitud de HTTP)</span><span class="sxs-lookup"><span data-stu-id="f279b-105">Securing access tootrigger a logic app (HTTP Request Trigger)</span></span>
* <span data-ttu-id="f279b-106">Protección de acceso toomanage, editar o leer una lógica de aplicación</span><span class="sxs-lookup"><span data-stu-id="f279b-106">Securing access toomanage, edit, or read a logic app</span></span>
* <span data-ttu-id="f279b-107">Protección de acceso toocontents de entradas y salidas para una ejecución</span><span class="sxs-lookup"><span data-stu-id="f279b-107">Securing access toocontents of inputs and outputs for a run</span></span>
* <span data-ttu-id="f279b-108">Protección de parámetros o entradas en las acciones de un flujo de trabajo</span><span class="sxs-lookup"><span data-stu-id="f279b-108">Securing parameters or inputs within actions in a workflow</span></span>
* <span data-ttu-id="f279b-109">Protección de acceso tooservices que reciben las solicitudes de un flujo de trabajo</span><span class="sxs-lookup"><span data-stu-id="f279b-109">Securing access tooservices that receive requests from a workflow</span></span>

## <a name="secure-access-tootrigger"></a><span data-ttu-id="f279b-110">Acceso seguro tootrigger</span><span class="sxs-lookup"><span data-stu-id="f279b-110">Secure access tootrigger</span></span>

<span data-ttu-id="f279b-111">Cuando se trabaja con una aplicación de la lógica que se activa en una solicitud HTTP ([solicitar](../connectors/connectors-native-reqres.md) o [Webhook](../connectors/connectors-native-webhook.md)), puede restringir el acceso para que solo los clientes autorizados pueden activar la aplicación de la lógica de hello.</span><span class="sxs-lookup"><span data-stu-id="f279b-111">When you work with a logic app that fires on an HTTP Request ([Request](../connectors/connectors-native-reqres.md) or [Webhook](../connectors/connectors-native-webhook.md)), you can restrict access so that only authorized clients can fire hello logic app.</span></span> <span data-ttu-id="f279b-112">Todas las solicitudes en una aplicación lógica se cifrarán y se protegerán mediante SSL.</span><span class="sxs-lookup"><span data-stu-id="f279b-112">All requests into a logic app are encrypted and secured via SSL.</span></span>

### <a name="shared-access-signature"></a><span data-ttu-id="f279b-113">Firma de acceso compartido</span><span class="sxs-lookup"><span data-stu-id="f279b-113">Shared Access Signature</span></span>

<span data-ttu-id="f279b-114">Cada extremo de la solicitud para una aplicación de lógica incluye un [firma de acceso compartido (SAS)](../storage/common/storage-dotnet-shared-access-signature-part-1.md) como parte de la dirección URL de Hola.</span><span class="sxs-lookup"><span data-stu-id="f279b-114">Every request endpoint for a logic app includes a [Shared Access Signature (SAS)](../storage/common/storage-dotnet-shared-access-signature-part-1.md) as part of hello URL.</span></span> <span data-ttu-id="f279b-115">Cada dirección URL contiene un parámetro de consulta `sp`, `sv` y `sig`.</span><span class="sxs-lookup"><span data-stu-id="f279b-115">Each URL contains a `sp`, `sv`, and `sig` query parameter.</span></span> <span data-ttu-id="f279b-116">Los permisos se especifican mediante `sp`, y corresponden a los métodos de tooHTTP permitidos, `sv` es toogenerate de la versión utilizada de hello, y `sig` es tooauthenticate usa acceso tootrigger.</span><span class="sxs-lookup"><span data-stu-id="f279b-116">Permissions are specified by `sp`, and correspond tooHTTP methods allowed, `sv` is hello version used toogenerate, and `sig` is used tooauthenticate access tootrigger.</span></span> <span data-ttu-id="f279b-117">firma de Hola se genera mediante el algoritmo de hello SHA256 con una clave secreta en todas las rutas de acceso de dirección URL de Hola y propiedades.</span><span class="sxs-lookup"><span data-stu-id="f279b-117">hello signature is generated using hello SHA256 algorithm with a secret key on all hello URL paths and properties.</span></span> <span data-ttu-id="f279b-118">clave secreta de Hello nunca se exponen y se publica y se mantienen cifrados y almacenados como parte de la aplicación de la lógica de hello.</span><span class="sxs-lookup"><span data-stu-id="f279b-118">hello secret key is never exposed and published, and is kept encrypted and stored as part of hello logic app.</span></span> <span data-ttu-id="f279b-119">La aplicación lógica sólo autoriza a los desencadenadores que contienen una firma válida creada con la clave secreta de Hola.</span><span class="sxs-lookup"><span data-stu-id="f279b-119">Your logic app only authorizes triggers that contain a valid signature created with hello secret key.</span></span>

#### <a name="regenerate-access-keys"></a><span data-ttu-id="f279b-120">Regenerar las claves de acceso</span><span class="sxs-lookup"><span data-stu-id="f279b-120">Regenerate access keys</span></span>

<span data-ttu-id="f279b-121">Puede volver a generar una nueva clave segura en cualquier momento a través del portal de Azure o la API de REST de Hola.</span><span class="sxs-lookup"><span data-stu-id="f279b-121">You can regenerate a new secure key at anytime through hello REST API or Azure portal.</span></span> <span data-ttu-id="f279b-122">Todas las direcciones URL actuales que se generaron anteriormente usando Hola antigua clave son aplicación de lógica de hello toofire invalidado y ya no está autorizado.</span><span class="sxs-lookup"><span data-stu-id="f279b-122">All current URLs that were generated previously using hello old key are invalidated and no longer authorized toofire hello logic app.</span></span>

1. <span data-ttu-id="f279b-123">Hola portal de Azure, abra la aplicación de lógica de hello desea tooregenerate una clave</span><span class="sxs-lookup"><span data-stu-id="f279b-123">In hello Azure portal, open hello logic app you want tooregenerate a key</span></span>
1. <span data-ttu-id="f279b-124">Haga clic en hello **teclas de acceso** elemento de menú en **configuración**</span><span class="sxs-lookup"><span data-stu-id="f279b-124">Click hello **Access Keys** menu item under **Settings**</span></span>
1. <span data-ttu-id="f279b-125">Elegir tooregenerate clave hello y proceso de hello completa</span><span class="sxs-lookup"><span data-stu-id="f279b-125">Choose hello key tooregenerate and complete hello process</span></span>

<span data-ttu-id="f279b-126">Recuperar después de la regeneración de las direcciones URL se firman con la nueva clave de acceso Hola.</span><span class="sxs-lookup"><span data-stu-id="f279b-126">URLs you retrieve after regeneration are signed with hello new access key.</span></span>

#### <a name="creating-callback-urls-with-an-expiration-date"></a><span data-ttu-id="f279b-127">Creación de direcciones URL de devolución de llamada con una fecha de expiración</span><span class="sxs-lookup"><span data-stu-id="f279b-127">Creating callback URLs with an expiration date</span></span>

<span data-ttu-id="f279b-128">Si va a compartir la dirección URL de hello con otras entidades, puede generar direcciones URL con determinadas claves y fechas de caducidad según sea necesario.</span><span class="sxs-lookup"><span data-stu-id="f279b-128">If you are sharing hello URL with other parties, you can generate URLs with specific keys and expiration dates as needed.</span></span> <span data-ttu-id="f279b-129">Puede, a continuación, perfectamente recorrer las claves, o asegúrese de toofire de acceso a una aplicación está restringido tooa cierto timespan.</span><span class="sxs-lookup"><span data-stu-id="f279b-129">You can then seamlessly roll keys, or ensure access toofire an app is restricted tooa certain timespan.</span></span> <span data-ttu-id="f279b-130">Puede especificar una fecha de expiración para una dirección URL a través de hello [las aplicaciones lógicas de API de REST](https://docs.microsoft.com/rest/api/logic/workflowtriggers):</span><span class="sxs-lookup"><span data-stu-id="f279b-130">You can specify an expiration date for a URL through hello [logic apps REST API](https://docs.microsoft.com/rest/api/logic/workflowtriggers):</span></span>

``` http
POST 
/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Logic/workflows/{workflowName}/triggers/{triggerName}/listCallbackUrl?api-version=2016-06-01
```

<span data-ttu-id="f279b-131">En el cuerpo de hello, incluir propiedad hello `NotAfter` como una cadena de fecha JSON, que devuelve una dirección URL de devolución de llamada que solo es válida hasta hello `NotAfter` fecha y hora.</span><span class="sxs-lookup"><span data-stu-id="f279b-131">In hello body, include hello property `NotAfter` as a JSON date string, which returns a callback URL that is only valid until hello `NotAfter` date and time.</span></span>

#### <a name="creating-urls-with-primary-or-secondary-secret-key"></a><span data-ttu-id="f279b-132">Creación de direcciones URL con clave secreta principal o secundaria</span><span class="sxs-lookup"><span data-stu-id="f279b-132">Creating URLs with primary or secondary secret key</span></span>

<span data-ttu-id="f279b-133">Cuando se genera o lista de direcciones URL de devolución de llamada para los desencadenadores basados en la solicitud, también puede especificar la dirección URL de toouse clave toosign Hola.</span><span class="sxs-lookup"><span data-stu-id="f279b-133">When you generate or list callback URLs for request-based triggers, you can also specify which key toouse toosign hello URL.</span></span>  <span data-ttu-id="f279b-134">Puede generar una dirección URL firmada por una clave específica a través de hello [las aplicaciones lógicas de API de REST](https://docs.microsoft.com/rest/api/logic/workflowtriggers) como se indica a continuación:</span><span class="sxs-lookup"><span data-stu-id="f279b-134">You can generate a URL signed by a specific key through hello [logic apps REST API](https://docs.microsoft.com/rest/api/logic/workflowtriggers) as follows:</span></span>

``` http
POST 
/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Logic/workflows/{workflowName}/triggers/{triggerName}/listCallbackUrl?api-version=2016-06-01
```

<span data-ttu-id="f279b-135">En el cuerpo de hello, incluir propiedad hello `KeyType` como `Primary` o `Secondary`.</span><span class="sxs-lookup"><span data-stu-id="f279b-135">In hello body, include hello property `KeyType` as either `Primary` or `Secondary`.</span></span>  <span data-ttu-id="f279b-136">Esto devuelve una dirección URL firmada por la clave segura Hola especificada.</span><span class="sxs-lookup"><span data-stu-id="f279b-136">This returns a URL signed by hello secure key specified.</span></span>

### <a name="restrict-incoming-ip-addresses"></a><span data-ttu-id="f279b-137">Restricción de las direcciones IP entrantes</span><span class="sxs-lookup"><span data-stu-id="f279b-137">Restrict incoming IP addresses</span></span>

<span data-ttu-id="f279b-138">Además toohello firma de acceso compartido, puede llamar toorestrict llamar a una aplicación lógica solo desde clientes específicos.</span><span class="sxs-lookup"><span data-stu-id="f279b-138">In addition toohello Shared Access Signature, you may wish toorestrict calling a logic app only from specific clients.</span></span>  <span data-ttu-id="f279b-139">Por ejemplo, si administra el punto de conexión a través de administración de API de Azure, puede restringir la lógica de hello tooonly aplicación aceptar la solicitud de hello cuando solicitud de hello provenga de hello dirección IP de instancia de administración de API.</span><span class="sxs-lookup"><span data-stu-id="f279b-139">For example, if you manage your endpoint through Azure API Management, you can restrict hello logic app tooonly accept hello request when hello request comes from hello API Management instance IP address.</span></span>

<span data-ttu-id="f279b-140">Esta configuración se puede configurar en la configuración de la aplicación hello lógica:</span><span class="sxs-lookup"><span data-stu-id="f279b-140">This setting can be configured within hello logic app settings:</span></span>

1. <span data-ttu-id="f279b-141">Hola portal de Azure, abra la aplicación de lógica de hello desea tooadd restricciones de dirección IP</span><span class="sxs-lookup"><span data-stu-id="f279b-141">In hello Azure portal, open hello logic app you want tooadd IP address restrictions</span></span>
1. <span data-ttu-id="f279b-142">Haga clic en hello **configuración de control de acceso** elemento de menú en **configuración**</span><span class="sxs-lookup"><span data-stu-id="f279b-142">Click hello **Access control configuration** menu item under **Settings**</span></span>
1. <span data-ttu-id="f279b-143">Especificar lista de Hola de toobe de intervalos de direcciones IP aceptada por el desencadenador de Hola</span><span class="sxs-lookup"><span data-stu-id="f279b-143">Specify hello list of IP address ranges toobe accepted by hello trigger</span></span>

<span data-ttu-id="f279b-144">Un intervalo IP válido toma el formato de hello `192.168.1.1/255`.</span><span class="sxs-lookup"><span data-stu-id="f279b-144">A valid IP range takes hello format `192.168.1.1/255`.</span></span> <span data-ttu-id="f279b-145">Si desea que Hola lógica aplicación tooonly incendio como una aplicación de lógica anidadas, seleccione hello **otras aplicaciones de la lógica** opción.</span><span class="sxs-lookup"><span data-stu-id="f279b-145">If you want hello logic app tooonly fire as a nested logic app, select hello **Only other logic apps** option.</span></span> <span data-ttu-id="f279b-146">Esta opción escribe un recurso de toohello matriz vacía, lo que significa que sólo las llamadas realizadas desde Hola propio servicio incendio (aplicaciones de la lógica principal) correctamente.</span><span class="sxs-lookup"><span data-stu-id="f279b-146">This option writes an empty array toohello resource, meaning only calls from hello service itself (parent logic apps) fire successfully.</span></span>

> [!NOTE]
> <span data-ttu-id="f279b-147">Todavía puede ejecutar una aplicación de lógica con un desencadenador de solicitud a través de la API de REST de Hola / administración `/triggers/{triggerName}/run` independientemente de IP.</span><span class="sxs-lookup"><span data-stu-id="f279b-147">You can still run a logic app with a request trigger through hello REST API / Management `/triggers/{triggerName}/run` regardless of IP.</span></span> <span data-ttu-id="f279b-148">Este escenario requiere autenticación contra Hola API de REST de Azure, y todos los eventos aparecería en hello registro de auditoría de Azure.</span><span class="sxs-lookup"><span data-stu-id="f279b-148">This scenario requires authentication against hello Azure REST API, and all events would appear in hello Azure Audit Log.</span></span> <span data-ttu-id="f279b-149">Establezca las directivas de control de acceso en consecuencia.</span><span class="sxs-lookup"><span data-stu-id="f279b-149">Set access control policies accordingly.</span></span>

#### <a name="setting-ip-ranges-on-hello-resource-definition"></a><span data-ttu-id="f279b-150">Establecer los intervalos de IP en la definición de recursos de Hola</span><span class="sxs-lookup"><span data-stu-id="f279b-150">Setting IP ranges on hello resource definition</span></span>

<span data-ttu-id="f279b-151">Si usas un [plantilla de implementación](logic-apps-create-deploy-template.md) tooautomate las implementaciones, la configuración de intervalos IP de hello pueden configurarse en la plantilla de recursos de Hola.</span><span class="sxs-lookup"><span data-stu-id="f279b-151">If you are using a [deployment template](logic-apps-create-deploy-template.md) tooautomate your deployments, hello IP range settings can be configured on hello resource template.</span></span>  

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

### <a name="adding-azure-active-directory-oauth-or-other-security"></a><span data-ttu-id="f279b-152">Adición de Azure Active Directory, OAuth u otra seguridad</span><span class="sxs-lookup"><span data-stu-id="f279b-152">Adding Azure Active Directory, OAuth, or other security</span></span>

<span data-ttu-id="f279b-153">tooadd autorización más protocolos encima de una aplicación lógica, [administración de API de Azure](https://azure.microsoft.com/services/api-management/) ofrece enriquecido supervisión, seguridad, directivas y documentación para cualquier extremo con hello capacidad tooexpose una aplicación lógica como una API.</span><span class="sxs-lookup"><span data-stu-id="f279b-153">tooadd more authorization protocols on top of a logic app, [Azure API Management](https://azure.microsoft.com/services/api-management/) offers rich monitoring, security, policy, and documentation for any endpoint with hello capability tooexpose a logic app as an API.</span></span> <span data-ttu-id="f279b-154">Administración de API de Azure puede exponer un punto de conexión público o privado para la aplicación de lógica de hello, que puede usar Azure Active Directory, certificado, OAuth u otros estándares de seguridad.</span><span class="sxs-lookup"><span data-stu-id="f279b-154">Azure API Management can expose a public or private endpoint for hello logic app, which could use Azure Active Directory, certificate, OAuth, or other security standards.</span></span> <span data-ttu-id="f279b-155">Cuando se recibe una solicitud, administración de API de Azure reenvía Hola solicitud toohello lógica aplicación (realizando las transformaciones necesarias o restricciones sobre la marcha).</span><span class="sxs-lookup"><span data-stu-id="f279b-155">When a request is received, Azure API Management forwards hello request toohello logic app (performing any needed transformations or restrictions in-flight).</span></span> <span data-ttu-id="f279b-156">Puede usar el intervalo de IP entrante Hola configuración en tooonly de aplicación lógica de hello permite desencadena toobe de aplicación lógica de hello de la API de administración de.</span><span class="sxs-lookup"><span data-stu-id="f279b-156">You can use hello incoming IP range settings on hello logic app tooonly allow hello logic app toobe triggered from API Management.</span></span>

## <a name="secure-access-toomanage-or-edit-logic-apps"></a><span data-ttu-id="f279b-157">Proteger el acceso a las aplicaciones lógicas toomanage o editar</span><span class="sxs-lookup"><span data-stu-id="f279b-157">Secure access toomanage or edit logic apps</span></span>

<span data-ttu-id="f279b-158">Puede restringir las operaciones de toomanagement de acceso en una aplicación de la lógica para que sólo determinados usuarios o grupos estén tooperform capaz de operaciones en recursos de Hola.</span><span class="sxs-lookup"><span data-stu-id="f279b-158">You can restrict access toomanagement operations on a logic app so that only specific users or groups are able tooperform operations on hello resource.</span></span> <span data-ttu-id="f279b-159">Las aplicaciones lógicas usan hello Azure [Control de acceso basado en roles (RBAC)](../active-directory/role-based-access-control-configure.md) de características y puede personalizarse con hello mismas herramientas.</span><span class="sxs-lookup"><span data-stu-id="f279b-159">Logic apps use hello Azure [Role-Based Access Control (RBAC)](../active-directory/role-based-access-control-configure.md) feature, and can be customized with hello same tools.</span></span>  <span data-ttu-id="f279b-160">Hay algunas funciones integradas que puede asignar a los miembros de su suscripción tooas bien:</span><span class="sxs-lookup"><span data-stu-id="f279b-160">There are a few built-in roles you can assign members of your subscription tooas well:</span></span>

* <span data-ttu-id="f279b-161">**Colaborador de aplicación lógica** -proporciona acceso tooview, editar y actualizar una aplicación de lógica.</span><span class="sxs-lookup"><span data-stu-id="f279b-161">**Logic App Contributor** - Provides access tooview, edit, and update a logic app.</span></span>  <span data-ttu-id="f279b-162">No se puede quitar el recurso de Hola o realizar operaciones de administración.</span><span class="sxs-lookup"><span data-stu-id="f279b-162">Cannot remove hello resource or perform admin operations.</span></span>
* <span data-ttu-id="f279b-163">**Operador de aplicación lógica** : puede ver la aplicación de la lógica de Hola y el historial de ejecución y habilitar o deshabilitar.</span><span class="sxs-lookup"><span data-stu-id="f279b-163">**Logic App Operator** - Can view hello logic app and run history, and enable/disable.</span></span>  <span data-ttu-id="f279b-164">No se puede editar o actualizar la definición de Hola.</span><span class="sxs-lookup"><span data-stu-id="f279b-164">Cannot edit or update hello definition.</span></span>

<span data-ttu-id="f279b-165">También puede usar [bloqueo de recurso de Azure](../azure-resource-manager/resource-group-lock-resources.md) tooprevent cambiar o eliminar aplicaciones lógicas.</span><span class="sxs-lookup"><span data-stu-id="f279b-165">You can also use [Azure Resource Lock](../azure-resource-manager/resource-group-lock-resources.md) tooprevent changing or deleting logic apps.</span></span> <span data-ttu-id="f279b-166">Esta capacidad es tooprevent valiosos recursos de producción de cambios o eliminaciones.</span><span class="sxs-lookup"><span data-stu-id="f279b-166">This capability is valuable tooprevent production resources from changes or deletions.</span></span>

## <a name="secure-access-toocontents-of-hello-run-history"></a><span data-ttu-id="f279b-167">Acceso seguro toocontents de hello historial de ejecución</span><span class="sxs-lookup"><span data-stu-id="f279b-167">Secure access toocontents of hello run history</span></span>

<span data-ttu-id="f279b-168">Puede restringir el acceso toocontents de entradas o salidas de intervalos de direcciones IP de anterior se ejecuta toospecific.</span><span class="sxs-lookup"><span data-stu-id="f279b-168">You can restrict access toocontents of inputs or outputs from previous runs toospecific IP address ranges.</span></span>  

<span data-ttu-id="f279b-169">Todos los datos dentro de una ejecución de flujo de trabajo se cifran en tránsito y en reposo.</span><span class="sxs-lookup"><span data-stu-id="f279b-169">All data within a workflow run is encrypted in transit and at rest.</span></span> <span data-ttu-id="f279b-170">Cuando se realiza un historial de toorun de llamada, el servicio de hello autentica la solicitud de Hola y proporciona vínculos toohello solicitud y respuesta entradas y salidas de.</span><span class="sxs-lookup"><span data-stu-id="f279b-170">When a call toorun history is made, hello service authenticates hello request and provides links toohello request and response inputs and outputs.</span></span> <span data-ttu-id="f279b-171">Este vínculo puede ser protegidas solicitudes para que solamente tooview contenido de un intervalo de direcciones IP designado devolver el contenido de Hola.</span><span class="sxs-lookup"><span data-stu-id="f279b-171">This link can be protected so only requests tooview content from a designated IP address range return hello contents.</span></span> <span data-ttu-id="f279b-172">Puede utilizar esta funcionalidad para el control de acceso adicional.</span><span class="sxs-lookup"><span data-stu-id="f279b-172">You can use this capability for additional access control.</span></span> <span data-ttu-id="f279b-173">Incluso puede especificar una dirección IP como `0.0.0.0` para que nadie tenga acceso a las entradas o salidas.</span><span class="sxs-lookup"><span data-stu-id="f279b-173">You could even specify an IP address like `0.0.0.0` so no one could access inputs/outputs.</span></span> <span data-ttu-id="f279b-174">Sólo un usuario con permisos de administrador puede quitar esta restricción, proporcionando la posibilidad de Hola para contenido de acceso 'just-in-time' tooworkflow.</span><span class="sxs-lookup"><span data-stu-id="f279b-174">Only someone with admin permissions could remove this restriction, providing hello possibility for 'just-in-time' access tooworkflow contents.</span></span>

<span data-ttu-id="f279b-175">Este valor se puede configurar en la configuración de recursos de Hola de hello portal de Azure:</span><span class="sxs-lookup"><span data-stu-id="f279b-175">This setting can be configured within hello resource settings of hello Azure portal:</span></span>

1. <span data-ttu-id="f279b-176">Hola portal de Azure, abra la aplicación de lógica de hello desea tooadd restricciones de dirección IP</span><span class="sxs-lookup"><span data-stu-id="f279b-176">In hello Azure portal, open hello logic app you want tooadd IP address restrictions</span></span>
1. <span data-ttu-id="f279b-177">Haga clic en hello **configuración de control de acceso** elemento de menú en **configuración**</span><span class="sxs-lookup"><span data-stu-id="f279b-177">Click hello **Access control configuration** menu item under **Settings**</span></span>
1. <span data-ttu-id="f279b-178">Especificar lista de Hola de intervalos de direcciones IP para toocontent de acceso</span><span class="sxs-lookup"><span data-stu-id="f279b-178">Specify hello list of IP address ranges for access toocontent</span></span>

#### <a name="setting-ip-ranges-on-hello-resource-definition"></a><span data-ttu-id="f279b-179">Establecer los intervalos de IP en la definición de recursos de Hola</span><span class="sxs-lookup"><span data-stu-id="f279b-179">Setting IP ranges on hello resource definition</span></span>

<span data-ttu-id="f279b-180">Si usas un [plantilla de implementación](logic-apps-create-deploy-template.md) tooautomate las implementaciones, la configuración de intervalos IP de hello pueden configurarse en la plantilla de recursos de Hola.</span><span class="sxs-lookup"><span data-stu-id="f279b-180">If you are using a [deployment template](logic-apps-create-deploy-template.md) tooautomate your deployments, hello IP range settings can be configured on hello resource template.</span></span>  

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

## <a name="secure-parameters-and-inputs-within-a-workflow"></a><span data-ttu-id="f279b-181">Parámetros seguros y entradas dentro de un flujo de trabajo</span><span class="sxs-lookup"><span data-stu-id="f279b-181">Secure parameters and inputs within a workflow</span></span>

<span data-ttu-id="f279b-182">Puede ser conveniente tooparameterize algunos aspectos de una definición de flujo de trabajo para la implementación a través de entornos.</span><span class="sxs-lookup"><span data-stu-id="f279b-182">You might want tooparameterize some aspects of a workflow definition for deployment across environments.</span></span> <span data-ttu-id="f279b-183">Además, algunos parámetros pueden ser parámetros de seguros no desea tooappear al editar un flujo de trabajo, como un identificador de cliente y el secreto del cliente para [autenticación de Azure Active Directory](../connectors/connectors-native-http.md#authentication) de una acción HTTP.</span><span class="sxs-lookup"><span data-stu-id="f279b-183">Also, some parameters might be secure parameters you don't want tooappear when editing a workflow, such as a client ID and client secret for [Azure Active Directory authentication](../connectors/connectors-native-http.md#authentication) of an HTTP action.</span></span>

### <a name="using-parameters-and-secure-parameters"></a><span data-ttu-id="f279b-184">Uso de parámetros y parámetros seguros</span><span class="sxs-lookup"><span data-stu-id="f279b-184">Using parameters and secure parameters</span></span>

<span data-ttu-id="f279b-185">Hola tooaccess valor de un parámetro de recurso en tiempo de ejecución, hello [lenguaje de definición de flujo de trabajo](http://aka.ms/logicappsdocs) proporciona un `@parameters()` operación.</span><span class="sxs-lookup"><span data-stu-id="f279b-185">tooaccess hello value of a resource parameter at runtime, hello [workflow definition language](http://aka.ms/logicappsdocs) provides a `@parameters()` operation.</span></span> <span data-ttu-id="f279b-186">Asimismo, puede [especificar parámetros de plantilla de implementación de recursos de hello](../azure-resource-manager/resource-group-authoring-templates.md#parameters).</span><span class="sxs-lookup"><span data-stu-id="f279b-186">Also, you can [specify parameters in hello resource deployment template](../azure-resource-manager/resource-group-authoring-templates.md#parameters).</span></span> <span data-ttu-id="f279b-187">Sin embargo, si especifica el tipo de parámetro hello como `securestring`, parámetro hello no se devolverá con rest Hola Hola de definición de recurso y no será accesible mediante la visualización de los recursos de hello después de la implementación.</span><span class="sxs-lookup"><span data-stu-id="f279b-187">But if you specify hello parameter type as `securestring`, hello parameter won't be returned with hello rest of hello resource definition, and won't be accessible by viewing hello resource after deployment.</span></span>

> [!NOTE]
> <span data-ttu-id="f279b-188">Si el parámetro se utiliza en encabezados de Hola o el cuerpo de una solicitud, parámetro hello puede verse obtengan acceso al historial de hello ejecutar y solicitud HTTP de salida.</span><span class="sxs-lookup"><span data-stu-id="f279b-188">If your parameter is used in hello headers or body of a request, hello parameter might be visible by accessing hello run history and outgoing HTTP request.</span></span> <span data-ttu-id="f279b-189">Asegúrese de tooset seguro de las directivas de acceso al contenido en consecuencia.</span><span class="sxs-lookup"><span data-stu-id="f279b-189">Make sure tooset your content access policies accordingly.</span></span>
> <span data-ttu-id="f279b-190">Los encabezados de autorización nunca son visibles a través de entradas o salidas.</span><span class="sxs-lookup"><span data-stu-id="f279b-190">Authorization headers are never visible through inputs or outputs.</span></span> <span data-ttu-id="f279b-191">Por lo que si se utiliza el secreto de hello no existe, secreto de hello no está recuperable.</span><span class="sxs-lookup"><span data-stu-id="f279b-191">So if hello secret is being used there, hello secret is not retrievable.</span></span>

#### <a name="resource-deployment-template-with-secrets"></a><span data-ttu-id="f279b-192">Plantilla de implementación de recursos con secretos</span><span class="sxs-lookup"><span data-stu-id="f279b-192">Resource deployment template with secrets</span></span>

<span data-ttu-id="f279b-193">Hello en el ejemplo siguiente se muestra una implementación que hace referencia a un parámetro de secure `secret` en tiempo de ejecución.</span><span class="sxs-lookup"><span data-stu-id="f279b-193">hello following example shows a deployment that references a secure parameter of `secret` at runtime.</span></span> <span data-ttu-id="f279b-194">En un archivo de parámetros separados, puede especificar valor de entorno de Hola para hello `secret`, o use [Azure Resource Manager KeyVault](../azure-resource-manager/resource-manager-keyvault-parameter.md) tooretrieve secretos en tiempo de implementación.</span><span class="sxs-lookup"><span data-stu-id="f279b-194">In a separate parameters file, you could specify hello environment value for hello `secret`, or use [Azure Resource Manager KeyVault](../azure-resource-manager/resource-manager-keyvault-parameter.md) tooretrieve secrets at deploy time.</span></span>

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
                "body": "This is hello request"
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

## <a name="secure-access-tooservices-receiving-requests-from-a-workflow"></a><span data-ttu-id="f279b-195">Proteger el acceso a las solicitudes de recepción de tooservices de un flujo de trabajo</span><span class="sxs-lookup"><span data-stu-id="f279b-195">Secure access tooservices receiving requests from a workflow</span></span>

<span data-ttu-id="f279b-196">Hay segura de que cualquier aplicación de lógica de hello de punto de conexión debe tooaccess toohelp de muchas maneras.</span><span class="sxs-lookup"><span data-stu-id="f279b-196">There are many ways toohelp secure any endpoint hello logic app needs tooaccess.</span></span>

### <a name="using-authentication-on-outbound-requests"></a><span data-ttu-id="f279b-197">Uso de la autenticación en las solicitudes salientes</span><span class="sxs-lookup"><span data-stu-id="f279b-197">Using authentication on outbound requests</span></span>

<span data-ttu-id="f279b-198">Cuando se trabaja con un HTTP, HTTP + Swagger (API abierta) o Webhook acción, puede agregar solicitud de toohello de autenticación que se envían.</span><span class="sxs-lookup"><span data-stu-id="f279b-198">When working with an HTTP, HTTP + Swagger (Open API), or Webhook action, you can add authentication toohello request being sent.</span></span> <span data-ttu-id="f279b-199">Podría incluir la autenticación básica, la autenticación de certificados o la autenticación de Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="f279b-199">You could include basic authentication, certificate authentication, or Azure Active Directory authentication.</span></span> <span data-ttu-id="f279b-200">Obtener más información sobre cómo tooconfigure esta autenticación puede encontrarse [en este artículo](../connectors/connectors-native-http.md#authentication).</span><span class="sxs-lookup"><span data-stu-id="f279b-200">Details on how tooconfigure this authentication can be found [in this article](../connectors/connectors-native-http.md#authentication).</span></span>

### <a name="restricting-access-toologic-app-ip-addresses"></a><span data-ttu-id="f279b-201">Restringir el acceso toologic aplicación las direcciones IP</span><span class="sxs-lookup"><span data-stu-id="f279b-201">Restricting access toologic app IP addresses</span></span>

<span data-ttu-id="f279b-202">Todas las llamadas de las aplicaciones lógicas proceden de un conjunto específico de direcciones IP por región.</span><span class="sxs-lookup"><span data-stu-id="f279b-202">All calls from logic apps come from a specific set of IP addresses per region.</span></span> <span data-ttu-id="f279b-203">Puede agregar un filtrado adicional tooonly Aceptar las solicitudes de los designa las direcciones IP.</span><span class="sxs-lookup"><span data-stu-id="f279b-203">You can add additional filtering tooonly accept requests from those designated IP addresses.</span></span> <span data-ttu-id="f279b-204">Para obtener una lista de esas direcciones IP, vea [Límites y configuración de Logic Apps](logic-apps-limits-and-config.md#configuration).</span><span class="sxs-lookup"><span data-stu-id="f279b-204">For a list of those IP addresses, see [logic app limits and configuration](logic-apps-limits-and-config.md#configuration).</span></span>

### <a name="on-premises-connectivity"></a><span data-ttu-id="f279b-205">Conectividad local</span><span class="sxs-lookup"><span data-stu-id="f279b-205">On-premises connectivity</span></span>

<span data-ttu-id="f279b-206">Las aplicaciones lógicas proporcionan integración con varios tooprovide de servicios seguras y confiables comunicación local.</span><span class="sxs-lookup"><span data-stu-id="f279b-206">Logic apps provide integration with several services tooprovide secure and reliable on-premises communication.</span></span>

#### <a name="on-premises-data-gateway"></a><span data-ttu-id="f279b-207">Puerta de enlace de datos local</span><span class="sxs-lookup"><span data-stu-id="f279b-207">On-premises data gateway</span></span>

<span data-ttu-id="f279b-208">Muchos conectores administrados para las aplicaciones lógicas proporcionan una conectividad segura sistemas de tooon locales, como sistema de archivos, SQL, SharePoint, DB2 etc..</span><span class="sxs-lookup"><span data-stu-id="f279b-208">Many managed connectors for logic apps provide secure connectivity tooon-premises systems, including File System, SQL, SharePoint, DB2, and more.</span></span> <span data-ttu-id="f279b-209">puerta de enlace de Hello transmite datos desde orígenes locales en los canales cifrados a través de hello Azure Service Bus.</span><span class="sxs-lookup"><span data-stu-id="f279b-209">hello gateway relays data from on-premises sources on encrypted channels through hello Azure Service Bus.</span></span> <span data-ttu-id="f279b-210">Todo el tráfico se origina como proteger el tráfico saliente desde el agente de puerta de enlace de Hola.</span><span class="sxs-lookup"><span data-stu-id="f279b-210">All traffic originates as secure outbound traffic from hello gateway agent.</span></span> <span data-ttu-id="f279b-211">Obtenga más información sobre [cómo funciona la puerta de enlace de datos de hello](logic-apps-gateway-install.md#gateway-cloud-service).</span><span class="sxs-lookup"><span data-stu-id="f279b-211">Learn more about [how hello data gateway works](logic-apps-gateway-install.md#gateway-cloud-service).</span></span>

#### <a name="azure-api-management"></a><span data-ttu-id="f279b-212">Administración de API de Azure</span><span class="sxs-lookup"><span data-stu-id="f279b-212">Azure API Management</span></span>

<span data-ttu-id="f279b-213">[Administración de API de Azure](https://azure.microsoft.com/services/api-management/) tiene opciones de conectividad local, incluida la integración de ExpressRoute y VPN de sitio a sitio para sistemas de tooon locales de proxy y la comunicación seguras.</span><span class="sxs-lookup"><span data-stu-id="f279b-213">[Azure API Management](https://azure.microsoft.com/services/api-management/) has on-premises connectivity options, including site-to-site VPN and ExpressRoute integration for secured proxy and communication tooon-premises systems.</span></span> <span data-ttu-id="f279b-214">Hola diseñador la lógica de aplicación, puede seleccionar rápidamente una API expuesta de administración de API de Azure dentro de un flujo de trabajo, proporciona acceso rápido sistemas tooon locales.</span><span class="sxs-lookup"><span data-stu-id="f279b-214">In hello Logic App Designer, you can quickly select an API exposed from Azure API Management within a workflow, providing quick access tooon-premises systems.</span></span>

#### <a name="hybrid-connections-from-azure-app-service"></a><span data-ttu-id="f279b-215">Conexiones híbridas desde Azure App Service</span><span class="sxs-lookup"><span data-stu-id="f279b-215">Hybrid connections from Azure App Service</span></span>

<span data-ttu-id="f279b-216">Puede usar características de conexión híbrida de hello locales para la API de Azure y Web aplicaciones toocommunicate en instalaciones locales.</span><span class="sxs-lookup"><span data-stu-id="f279b-216">You can use hello on-premises hybrid connection feature for Azure API and Web apps toocommunicate on-premises.</span></span>  <span data-ttu-id="f279b-217">Obtener más información sobre las conexiones híbridas y cómo puede encontrarse tooconfigure [en este artículo](../app-service-web/web-sites-hybrid-connection-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="f279b-217">Details on hybrid connections and how tooconfigure can be found [in this article](../app-service-web/web-sites-hybrid-connection-get-started.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="f279b-218">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="f279b-218">Next steps</span></span>
[<span data-ttu-id="f279b-219">Creación de una plantilla de implementación</span><span class="sxs-lookup"><span data-stu-id="f279b-219">Create a deployment template</span></span>](logic-apps-create-deploy-template.md)  
[<span data-ttu-id="f279b-220">Control de excepciones</span><span class="sxs-lookup"><span data-stu-id="f279b-220">Exception handling</span></span>](logic-apps-exception-handling.md)  
[<span data-ttu-id="f279b-221">Supervisar las aplicaciones lógicas</span><span class="sxs-lookup"><span data-stu-id="f279b-221">Monitor your logic apps</span></span>](logic-apps-monitor-your-logic-apps.md)  
[<span data-ttu-id="f279b-222">Diagnóstico de errores y problemas de las aplicaciones lógicas</span><span class="sxs-lookup"><span data-stu-id="f279b-222">Diagnosing logic app failures and issues</span></span>](logic-apps-diagnosing-failures.md)  
