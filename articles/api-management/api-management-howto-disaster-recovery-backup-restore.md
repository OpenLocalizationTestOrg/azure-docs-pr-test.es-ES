---
title: "recuperación ante desastres de aaaImplement mediante una copia de seguridad y restauración en la administración de API de Azure | Documentos de Microsoft"
description: "Obtenga información acerca de cómo toouse copias de seguridad y restaura tooperform de recuperación ante desastres en la administración de API de Azure."
services: api-management
documentationcenter: 
author: steved0x
manager: erikre
editor: 
ms.assetid: 6f10be3c-f796-4a6c-bacd-7931b6aa82af
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: apimpm
ms.openlocfilehash: 058bfb579e3a3f51fb1dac8ea37eb4fdbc83a4ad
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooimplement-disaster-recovery-using-service-backup-and-restore-in-azure-api-management"></a><span data-ttu-id="1ab49-103">¿Cómo tooimplement ante desastres recuperación mediante copia de seguridad de servicio y restaurar en la administración de API de Azure</span><span class="sxs-lookup"><span data-stu-id="1ab49-103">How tooimplement disaster recovery using service backup and restore in Azure API Management</span></span>
<span data-ttu-id="1ab49-104">Mediante la elección de toopublish y administrar las API a través de administración de API de Azure se sacar partido de las muchas capacidades de tolerancia y la infraestructura del error que, de lo contrario tendría toodesign, implementar y administrar.</span><span class="sxs-lookup"><span data-stu-id="1ab49-104">By choosing toopublish and manage your APIs via Azure API Management you are taking advantage of many fault tolerance and infrastructure capabilities that you would otherwise have toodesign, implement, and manage.</span></span> <span data-ttu-id="1ab49-105">Hola plataforma Windows Azure, mitiga una gran parte de los posibles errores en una fracción del costo de Hola.</span><span class="sxs-lookup"><span data-stu-id="1ab49-105">hello Azure platform mitigates a large fraction of potential failures at a fraction of hello cost.</span></span>

<span data-ttu-id="1ab49-106">toorecover de problemas de disponibilidad que afectan a Hola región donde reside el servicio de administración de API hospedadas debe ser tooreconstitute preparado su servicio en una región diferente en cualquier momento.</span><span class="sxs-lookup"><span data-stu-id="1ab49-106">toorecover from availability problems affecting hello region where your API Management service is hosted you should be ready tooreconstitute your service in a different region at any time.</span></span> <span data-ttu-id="1ab49-107">Según los objetivos de disponibilidad y el objetivo de tiempo de recuperación podría desea tooreserve un servicio de copia de seguridad en una o varias regiones e intente toomaintain su configuración y contenido sincronizado con el servicio activo de Hola.</span><span class="sxs-lookup"><span data-stu-id="1ab49-107">Depending on your availability goals and recovery time objective  you might want tooreserve a backup service in one or more regions and try toomaintain their configuration and content in sync with hello active service.</span></span> <span data-ttu-id="1ab49-108">copia de seguridad de servicio de Hola y la característica de restauración proporciona Hola bloques de creación necesarios para implementar la estrategia de recuperación ante desastres.</span><span class="sxs-lookup"><span data-stu-id="1ab49-108">hello service backup and restore feature provides hello necessary building block for implementing your disaster recovery strategy.</span></span>

<span data-ttu-id="1ab49-109">Esta guía le mostrará cómo tooauthenticate Azure Resource Manager solicita y cómo toobackup y restaurar las instancias de servicio de administración de API.</span><span class="sxs-lookup"><span data-stu-id="1ab49-109">This guide shows how tooauthenticate Azure Resource Manager requests, and how toobackup and restore your API Management service instances.</span></span>

> [!NOTE]
> <span data-ttu-id="1ab49-110">proceso de Hola para realizar copias de seguridad y restauración de una instancia de servicio de administración de API para la recuperación ante desastres puede utilizarse también para la replicación de instancias de servicio de administración de API para escenarios, como el almacenamiento provisional.</span><span class="sxs-lookup"><span data-stu-id="1ab49-110">hello process for backing up and restoring an API Management service instance for disaster recovery can also be used for replicating API Management service instances for scenarios such as staging.</span></span>
>
> <span data-ttu-id="1ab49-111">Tenga en cuenta que cada copia de seguridad expira después de 30 días.</span><span class="sxs-lookup"><span data-stu-id="1ab49-111">Note that each backup expires after 30 days.</span></span> <span data-ttu-id="1ab49-112">Si intentas toorestore una copia de seguridad después de que ha expirado el período de expiración de 30 días de hello, se producirá un error de restauración de hello con un `Cannot restore: backup expired` mensaje.</span><span class="sxs-lookup"><span data-stu-id="1ab49-112">If you attempt toorestore a backup after hello 30 day expiration period has expired, hello restore will fail with a `Cannot restore: backup expired` message.</span></span>
>
>

## <a name="authenticating-azure-resource-manager-requests"></a><span data-ttu-id="1ab49-113">Solicitudes de autenticación del Administrador de recursos de Azure</span><span class="sxs-lookup"><span data-stu-id="1ab49-113">Authenticating Azure Resource Manager requests</span></span>
> [!IMPORTANT]
> <span data-ttu-id="1ab49-114">Hello API de REST para copia de seguridad y restauración usa Azure Resource Manager y tiene un mecanismo de autenticación distinto de hello las API de REST para administrar las entidades de la administración de API.</span><span class="sxs-lookup"><span data-stu-id="1ab49-114">hello REST API for backup and restore uses Azure Resource Manager and has a different authentication mechanism than hello REST APIs for managing your API Management entities.</span></span> <span data-ttu-id="1ab49-115">pasos de Hello en esta sección describe cómo solicita tooauthenticate Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="1ab49-115">hello steps in this section describe how tooauthenticate Azure Resource Manager requests.</span></span> <span data-ttu-id="1ab49-116">Par obtener más información, consulte [Solicitudes de autenticación del Administrador de recursos de Azure](http://msdn.microsoft.com/library/azure/dn790557.aspx).</span><span class="sxs-lookup"><span data-stu-id="1ab49-116">For more information, see [Authenticating Azure Resource Manager requests](http://msdn.microsoft.com/library/azure/dn790557.aspx).</span></span>
>
>

<span data-ttu-id="1ab49-117">Todas las tareas de Hola que realice en los recursos con hello Azure Resource Manager deben autenticarse con Azure Active Directory con hello pasos.</span><span class="sxs-lookup"><span data-stu-id="1ab49-117">All of hello tasks that you do on resources using hello Azure Resource Manager must be authenticated with Azure Active Directory using hello following steps.</span></span>

* <span data-ttu-id="1ab49-118">Agregar a un inquilino de Azure Active Directory de toohello de aplicación.</span><span class="sxs-lookup"><span data-stu-id="1ab49-118">Add an application toohello Azure Active Directory tenant.</span></span>
* <span data-ttu-id="1ab49-119">Establecer permisos para la aplicación hello que agregó.</span><span class="sxs-lookup"><span data-stu-id="1ab49-119">Set permissions for hello application that you added.</span></span>
* <span data-ttu-id="1ab49-120">Obtener token de Hola para autenticar las solicitudes tooAzure el Administrador de recursos.</span><span class="sxs-lookup"><span data-stu-id="1ab49-120">Get hello token for authenticating requests tooAzure Resource Manager.</span></span>

<span data-ttu-id="1ab49-121">Hola primer paso es toocreate una aplicación de Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="1ab49-121">hello first step is toocreate an Azure Active Directory application.</span></span> <span data-ttu-id="1ab49-122">Inicie sesión en hello [Portal clásico de Azure](http://manage.windowsazure.com/) usando suscripción Hola que contiene el servicio de administración de API de instancia y navegue toohello **aplicaciones** ficha para su Azure Active Directory de manera predeterminada.</span><span class="sxs-lookup"><span data-stu-id="1ab49-122">Log into hello [Azure Classic Portal](http://manage.windowsazure.com/) using hello subscription that contains your API Management service instance and navigate toohello **Applications** tab for your default Azure Active Directory.</span></span>

> [!NOTE]
> <span data-ttu-id="1ab49-123">Si directorio predeterminado de hello Azure Active Directory no es visible tooyour cuenta, Administrador de contacto Hola de Hola Hola de toogrant de suscripción de Azure requiere una cuenta con permisos tooyour.</span><span class="sxs-lookup"><span data-stu-id="1ab49-123">If hello Azure Active Directory default directory is not visible tooyour account, contact hello administrator of hello Azure subscription toogrant hello required permissions tooyour account.</span></span>

![Creación de una aplicación de Azure Active Directory][api-management-add-aad-application]

<span data-ttu-id="1ab49-125">Haga clic en **Agregar**, **Agregar una aplicación que mi organización está desarrollando** y elija **Aplicación de cliente nativo**.</span><span class="sxs-lookup"><span data-stu-id="1ab49-125">Click **Add**, **Add an application my organization is developing**, and choose **Native client application**.</span></span> <span data-ttu-id="1ab49-126">Escriba un nombre descriptivo y haga clic en la flecha siguiente Hola.</span><span class="sxs-lookup"><span data-stu-id="1ab49-126">Enter a descriptive name, and click hello next arrow.</span></span> <span data-ttu-id="1ab49-127">Escriba una dirección URL de marcador de posición como `http://resources` para hello **URI de redireccionamiento**, tal y como es un campo obligatorio, pero no se usa el valor de hello más tarde.</span><span class="sxs-lookup"><span data-stu-id="1ab49-127">Enter a placeholder URL such as `http://resources` for hello **Redirect URI**, as it is a required field, but hello value is not used later.</span></span> <span data-ttu-id="1ab49-128">Haga clic en la aplicación de hello casilla toosave Hola.</span><span class="sxs-lookup"><span data-stu-id="1ab49-128">Click hello check box toosave hello application.</span></span>

<span data-ttu-id="1ab49-129">Una vez que se guarda la aplicación hello, haga clic en **configurar**, desplácese hacia abajo toohello **permisos tooother aplicaciones** sección y haga clic en **Agregar aplicación**.</span><span class="sxs-lookup"><span data-stu-id="1ab49-129">Once hello application is saved, click **Configure**, scroll down toohello **permissions tooother applications** section, and click **Add application**.</span></span>

![Adición de permisos][api-management-aad-permissions-add]

<span data-ttu-id="1ab49-131">Seleccione **Windows** **API de administración de servicios de Azure** y haga clic en la aplicación de hello casilla tooadd Hola.</span><span class="sxs-lookup"><span data-stu-id="1ab49-131">Select **Windows** **Azure Service Management API** and click hello checkbox tooadd hello application.</span></span>

![Adición de permisos][api-management-aad-permissions]

<span data-ttu-id="1ab49-133">Haga clic en **permisos delegados** lateral Hola recién agregado **Windows** **API de administración de servicios de Azure** aplicación, casilla Hola para **acceso de Azure Administración de servicios (versión preliminar)**y haga clic en **guardar**.</span><span class="sxs-lookup"><span data-stu-id="1ab49-133">Click **Delegated Permissions** beside hello newly added **Windows** **Azure Service Management API** application, check hello box for **Access Azure Service Management (preview)**, and click **Save**.</span></span>

![Adición de permisos][api-management-aad-delegated-permissions]

<span data-ttu-id="1ab49-135">Tooinvoking anterior hello las API que generan Hola copia de seguridad y restaurarlo, es necesario tooget un token.</span><span class="sxs-lookup"><span data-stu-id="1ab49-135">Prior tooinvoking hello APIs that generate hello backup and restore it, it is necessary tooget a token.</span></span> <span data-ttu-id="1ab49-136">Hello en el ejemplo siguiente se usa hello [Microsoft.IdentityModel.Clients.ActiveDirectory](https://www.nuget.org/packages/Microsoft.IdentityModel.Clients.ActiveDirectory) token de Hola de tooretrieve de paquete de nuget.</span><span class="sxs-lookup"><span data-stu-id="1ab49-136">hello following example uses hello [Microsoft.IdentityModel.Clients.ActiveDirectory](https://www.nuget.org/packages/Microsoft.IdentityModel.Clients.ActiveDirectory) nuget package tooretrieve hello token.</span></span>

```c#
using Microsoft.IdentityModel.Clients.ActiveDirectory;
using System;

namespace GetTokenResourceManagerRequests
{
    class Program
    {
        static void Main(string[] args)
        {
            var authenticationContext = new AuthenticationContext("https://login.microsoftonline.com/{tenant id}");
            var result = authenticationContext.AcquireToken("https://management.azure.com/", {application id}, new Uri({redirect uri});

            if (result == null) {
                throw new InvalidOperationException("Failed tooobtain hello JWT token");
            }

            Console.WriteLine(result.AccessToken);

            Console.ReadLine();
        }
    }
}
```

<span data-ttu-id="1ab49-137">Reemplace `{tentand id}`, `{application id}`, y `{redirect uri}` Hola siguiendo las instrucciones de uso.</span><span class="sxs-lookup"><span data-stu-id="1ab49-137">Replace `{tentand id}`, `{application id}`, and `{redirect uri}` using hello following instructions.</span></span>

<span data-ttu-id="1ab49-138">Reemplace `{tenant id}` con el identificador de inquilino de Hola de hello aplicación de Azure Active Directory que acaba de crear.</span><span class="sxs-lookup"><span data-stu-id="1ab49-138">Replace `{tenant id}` with hello tenant id of hello Azure Active Directory application you just created.</span></span> <span data-ttu-id="1ab49-139">Puede tener acceso a identificador hello haciendo clic en **ver extremos**.</span><span class="sxs-lookup"><span data-stu-id="1ab49-139">You can access hello id by clicking **View endpoints**.</span></span>

![Puntos de conexión][api-management-aad-default-directory]

![Puntos de conexión][api-management-endpoint]

<span data-ttu-id="1ab49-142">Reemplace `{application id}` y `{redirect uri}` con hello **Id. de cliente** y Hola dirección URL de hello **URI de redireccionamiento** sección de la aplicación de Azure Active Directory **configurar**  ficha.</span><span class="sxs-lookup"><span data-stu-id="1ab49-142">Replace `{application id}` and `{redirect uri}` using hello **Client Id** and  hello URL from hello **Redirect Uris** section from your Azure Active Directory application's **Configure** tab.</span></span>

![Recursos][api-management-aad-resources]

<span data-ttu-id="1ab49-144">Una vez que se especifican valores de hello, ejemplo de código de hello debe devolver un token toohello similar siguiente ejemplo.</span><span class="sxs-lookup"><span data-stu-id="1ab49-144">Once hello values are specified, hello code example should return a token similar toohello following example.</span></span>

![SWT][api-management-arm-token]

<span data-ttu-id="1ab49-146">Antes de llamar a Hola copia de seguridad y restaurar las operaciones que se describe en las secciones siguientes de hello, establezca el encabezado de solicitud de autorización de hello para la llamada de REST.</span><span class="sxs-lookup"><span data-stu-id="1ab49-146">Before calling hello backup and restore operations described in hello following sections, set hello authorization request header for your REST call.</span></span>

```c#
request.Headers.Add(HttpRequestHeader.Authorization, "Bearer " + token);
```

## <span data-ttu-id="1ab49-147"><a name="step1"></a>Crear una copia de seguridad del servicio API Management</span><span class="sxs-lookup"><span data-stu-id="1ab49-147"><a name="step1"> </a>Back up an API Management service</span></span>
<span data-ttu-id="1ab49-148">tooback seguridad un Hola de problema de servicio de administración de API después de la solicitud HTTP:</span><span class="sxs-lookup"><span data-stu-id="1ab49-148">tooback up an API Management service issue hello following HTTP request:</span></span>

`POST https://management.azure.com/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ApiManagement/service/{serviceName}/backup?api-version={api-version}`

<span data-ttu-id="1ab49-149">donde:</span><span class="sxs-lookup"><span data-stu-id="1ab49-149">where:</span></span>

* <span data-ttu-id="1ab49-150">`subscriptionId`-Id. de suscripción de Hola que contiene el servicio de administración de API de hello estás intentando toobackup</span><span class="sxs-lookup"><span data-stu-id="1ab49-150">`subscriptionId` - id of hello subscription containing hello API Management service you are attempting toobackup</span></span>
* <span data-ttu-id="1ab49-151">`resourceGroupName`-una cadena con formato hello 'Api - Default: {región del servicio}' donde `service-region` identifica Hola región de Azure donde se hospeda el servicio de administración de API que estamos toobackup Hola, p. ej.`North-Central-US`</span><span class="sxs-lookup"><span data-stu-id="1ab49-151">`resourceGroupName` - a string in hello form of 'Api-Default-{service-region}' where `service-region` identifies hello Azure region where hello API Management service you are trying toobackup is hosted, e.g. `North-Central-US`</span></span>
* <span data-ttu-id="1ab49-152">`serviceName`-nombre de Hola de hello servicio de administración de API que se está realizando una copia de seguridad especificado en tiempo de presentación de su creación</span><span class="sxs-lookup"><span data-stu-id="1ab49-152">`serviceName` - hello name of hello API Management service you are making a backup of specified at hello time of its creation</span></span>
* <span data-ttu-id="1ab49-153">`api-version`: reemplazar por `2014-02-14`</span><span class="sxs-lookup"><span data-stu-id="1ab49-153">`api-version` - replace  with `2014-02-14`</span></span>

<span data-ttu-id="1ab49-154">En el cuerpo de saludo de solicitud de hello, especifique el nombre de cuenta de almacenamiento de Azure de destino de hello, clave de acceso, el nombre del contenedor de blob y nombre de la copia de seguridad:</span><span class="sxs-lookup"><span data-stu-id="1ab49-154">In hello body of hello request, specify hello target Azure storage account name, access key, blob container name, and backup name:</span></span>

```
'{  
    storageAccount : {storage account name for hello backup},  
    accessKey : {access key for hello account},  
    containerName : {backup container name},  
    backupName : {backup blob name}  
}'
```

<span data-ttu-id="1ab49-155">Establecer valor de Hola de hello `Content-Type` encabezado de solicitud demasiado`application/json`.</span><span class="sxs-lookup"><span data-stu-id="1ab49-155">Set hello value of hello `Content-Type` request header too`application/json`.</span></span>

<span data-ttu-id="1ab49-156">Copia de seguridad es una operación larga que puede tardar varios toocomplete minutos.</span><span class="sxs-lookup"><span data-stu-id="1ab49-156">Backup is a long running operation that may take multiple minutes toocomplete.</span></span>  <span data-ttu-id="1ab49-157">Si se completó la solicitud de Hola y se inició el proceso de copia de seguridad de hello recibirá un `202 Accepted` código de estado de respuesta con un `Location` encabezado.</span><span class="sxs-lookup"><span data-stu-id="1ab49-157">If hello request was successful and hello backup process was initiated you’ll receive a `202 Accepted` response status code with a `Location` header.</span></span>  <span data-ttu-id="1ab49-158">Asegúrese de 'GET'. las solicitudes URL toohello Hola `Location` toofind encabezado estado Hola de operación de Hola.</span><span class="sxs-lookup"><span data-stu-id="1ab49-158">Make 'GET' requests toohello URL in hello `Location` header toofind out hello status of hello operation.</span></span> <span data-ttu-id="1ab49-159">Mientras se realiza la copia de seguridad de hello continuará tooreceive un código de estado '202 aceptado'.</span><span class="sxs-lookup"><span data-stu-id="1ab49-159">While hello backup is in progress you will continue tooreceive a '202 Accepted' status code.</span></span> <span data-ttu-id="1ab49-160">El código de respuesta `200 OK` indicará la finalización correcta de la operación de copia de seguridad de Hola.</span><span class="sxs-lookup"><span data-stu-id="1ab49-160">A Response code of `200 OK` will indicate successful completion of hello backup operation.</span></span>

<span data-ttu-id="1ab49-161">Tenga en cuenta las siguientes restricciones cuando se realiza una solicitud de copia de seguridad de Hola.</span><span class="sxs-lookup"><span data-stu-id="1ab49-161">Please note hello following constraints when making a backup request.</span></span>

* <span data-ttu-id="1ab49-162">**Contenedor** especificado en el cuerpo de la solicitud de hello **debe existir**.</span><span class="sxs-lookup"><span data-stu-id="1ab49-162">**Container** specified in hello request body **must exist**.</span></span>
* <span data-ttu-id="1ab49-163">Mientras se crea la copia de seguridad, **no realice ninguna operación de administración del servicio** (por ejemplo, una actualización o degradación de SKU o un cambio de nombre de dominio).</span><span class="sxs-lookup"><span data-stu-id="1ab49-163">While backup is in progress you **should not attempt any service management operations** such as SKU upgrade or downgrade, domain name change, etc.</span></span>
* <span data-ttu-id="1ab49-164">Restauración de un **copia de seguridad se garantiza que sólo durante 30 días** desde el momento de Hola de su creación.</span><span class="sxs-lookup"><span data-stu-id="1ab49-164">Restore of a **backup is guaranteed only for 30 days** since hello moment of its creation.</span></span>
* <span data-ttu-id="1ab49-165">**Datos de uso** utiliza para crear informes de análisis **no se incluye** en copia de seguridad de Hola.</span><span class="sxs-lookup"><span data-stu-id="1ab49-165">**Usage data** used for creating analytics reports **is not included** in hello backup.</span></span> <span data-ttu-id="1ab49-166">Use [API de REST de administración de API de Azure] [ Azure API Management REST API] tooperiodically recuperar informes de análisis por motivos de seguridad.</span><span class="sxs-lookup"><span data-stu-id="1ab49-166">Use [Azure API Management REST API][Azure API Management REST API] tooperiodically retrieve analytics reports for safekeeping.</span></span>
* <span data-ttu-id="1ab49-167">frecuencia de Hello con el que realizar copias de seguridad de servicio afectará a su objetivo de punto de recuperación.</span><span class="sxs-lookup"><span data-stu-id="1ab49-167">hello frequency with which you perform service backups will affect your recovery point objective.</span></span> <span data-ttu-id="1ab49-168">toominimize, se recomienda implementar copias de seguridad periódicas, así como realizar copias de seguridad a petición después de realizar importante cambia tooyour servicio de administración de API.</span><span class="sxs-lookup"><span data-stu-id="1ab49-168">toominimize it we advise implementing regular backups as well as performing on-demand backups after making important changes tooyour API Management service.</span></span>
* <span data-ttu-id="1ab49-169">**Cambios** configuración del servicio realizadas toohello (p. ej., API, las directivas de apariencia portal para desarrolladores) durante la operación de copia de seguridad está en curso **no pueden incluirse en la copia de seguridad de hello y, por tanto, se perderán**.</span><span class="sxs-lookup"><span data-stu-id="1ab49-169">**Changes** made toohello service configuration (e.g. APIs, policies, developer portal appearance) while backup operation is in process **might not be included in hello backup and therefore will be lost**.</span></span>

## <span data-ttu-id="1ab49-170"><a name="step2"></a>Restaurar el servicio Administración de API</span><span class="sxs-lookup"><span data-stu-id="1ab49-170"><a name="step2"> </a>Restore an API Management service</span></span>
<span data-ttu-id="1ab49-171">toorestore un servicio de administración de API desde una copia de seguridad creado anteriormente que Hola después de la solicitud HTTP:</span><span class="sxs-lookup"><span data-stu-id="1ab49-171">toorestore an API Management service from a previously created backup make hello following HTTP request:</span></span>

`POST https://management.azure.com/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ApiManagement/service/{serviceName}/restore?api-version={api-version}`

<span data-ttu-id="1ab49-172">donde:</span><span class="sxs-lookup"><span data-stu-id="1ab49-172">where:</span></span>

* <span data-ttu-id="1ab49-173">`subscriptionId`-Id. de suscripción de Hola que contiene el servicio de administración de API de hello va a restaurar una copia de seguridad en</span><span class="sxs-lookup"><span data-stu-id="1ab49-173">`subscriptionId` - id of hello subscription containing hello API Management service you are restoring a backup into</span></span>
* <span data-ttu-id="1ab49-174">`resourceGroupName`-una cadena con formato hello 'Api - Default: {región del servicio}' donde `service-region` identifica Hola región de Azure donde se hospeda Hola va a restaurar una copia de seguridad en el servicio de administración de API, p. ej.`North-Central-US`</span><span class="sxs-lookup"><span data-stu-id="1ab49-174">`resourceGroupName` - a string in hello form of 'Api-Default-{service-region}' where `service-region` identifies hello Azure region where hello API Management service you are restoring a backup into is hosted, e.g. `North-Central-US`</span></span>
* <span data-ttu-id="1ab49-175">`serviceName`-nombre de Hola de hello administración de API se restauran en el servicio especificado en tiempo de presentación de su creación</span><span class="sxs-lookup"><span data-stu-id="1ab49-175">`serviceName` - hello name of hello API Management service being restored into specified at hello time of its creation</span></span>
* <span data-ttu-id="1ab49-176">`api-version`: reemplazar por `2014-02-14`</span><span class="sxs-lookup"><span data-stu-id="1ab49-176">`api-version` - replace  with `2014-02-14`</span></span>

<span data-ttu-id="1ab49-177">En el cuerpo de saludo de solicitud de hello, especificar ubicación del archivo de copia de seguridad de hello, es decir, nombre de la cuenta de almacenamiento de Azure, la clave de acceso, el nombre del contenedor de blob y nombre de copia de seguridad:</span><span class="sxs-lookup"><span data-stu-id="1ab49-177">In hello body of hello request, specify hello backup file location, i.e. Azure storage account name, access key, blob container name, and backup name:</span></span>

```
'{  
    storageAccount : {storage account name for hello backup},  
    accessKey : {access key for hello account},  
    containerName : {backup container name},  
    backupName : {backup blob name}  
}'
```

<span data-ttu-id="1ab49-178">Establecer valor de Hola de hello `Content-Type` encabezado de solicitud demasiado`application/json`.</span><span class="sxs-lookup"><span data-stu-id="1ab49-178">Set hello value of hello `Content-Type` request header too`application/json`.</span></span>

<span data-ttu-id="1ab49-179">Restauración es una operación larga que puede llevar hasta too30 o toocomplete de minutos más.</span><span class="sxs-lookup"><span data-stu-id="1ab49-179">Restore is a long running operation that may take up too30 or more minutes toocomplete.</span></span>  <span data-ttu-id="1ab49-180">Si se completó la solicitud de Hola y se inició el proceso de restauración de hello recibirá un `202 Accepted` código de estado de respuesta con un `Location` encabezado.</span><span class="sxs-lookup"><span data-stu-id="1ab49-180">If hello request was successful and hello restore process was initiated you’ll receive a `202 Accepted` response status code with a `Location` header.</span></span>  <span data-ttu-id="1ab49-181">Asegúrese de 'GET'. las solicitudes URL toohello Hola `Location` toofind encabezado estado Hola de operación de Hola.</span><span class="sxs-lookup"><span data-stu-id="1ab49-181">Make 'GET' requests toohello URL in hello `Location` header toofind out hello status of hello operation.</span></span> <span data-ttu-id="1ab49-182">Mientras se realiza la restauración de hello continuará tooreceive código de estado de "202 Accepted".</span><span class="sxs-lookup"><span data-stu-id="1ab49-182">While hello restore is in progress you will continue tooreceive '202 Accepted' status code.</span></span> <span data-ttu-id="1ab49-183">El código de respuesta `200 OK` indicará la finalización correcta de la operación de restauración de Hola.</span><span class="sxs-lookup"><span data-stu-id="1ab49-183">A response code of `200 OK` will indicate successful completion of hello restore operation.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="1ab49-184">**Hola SKU** del servicio de Hola se restauran en **debe coincidir con** Hola SKU de hello copia de seguridad que se están restaurando el servicio.</span><span class="sxs-lookup"><span data-stu-id="1ab49-184">**hello SKU** of hello service being restored into **must match** hello SKU of hello backed up service being restored.</span></span>
>
> <span data-ttu-id="1ab49-185">**Cambios** toohello realizadas servicio configuración (por ejemplo, API, directivas, apariencia portal para desarrolladores) durante la operación de restauración está en curso **podría sobrescribirse**.</span><span class="sxs-lookup"><span data-stu-id="1ab49-185">**Changes** made toohello service configuration (e.g. APIs, policies, developer portal appearance) while restore operation is in progress **could be overwritten**.</span></span>
>
>

## <a name="next-steps"></a><span data-ttu-id="1ab49-186">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="1ab49-186">Next steps</span></span>
<span data-ttu-id="1ab49-187">Extraer del repositorio Hola después de blogs de Microsoft para los dos tutoriales diferentes del proceso de copia de seguridad/restauración Hola.</span><span class="sxs-lookup"><span data-stu-id="1ab49-187">Check out hello following Microsoft blogs for two different walkthroughs of hello backup/restore process.</span></span>

* [<span data-ttu-id="1ab49-188">Replicate Azure API Management Accounts (Réplica de cuentas de Administración de API de Azure)</span><span class="sxs-lookup"><span data-stu-id="1ab49-188">Replicate Azure API Management Accounts</span></span>](https://www.returngis.net/en/2015/06/replicate-azure-api-management-accounts/)
  * <span data-ttu-id="1ab49-189">Gracias tooGisela para su artículo de toothis contribución.</span><span class="sxs-lookup"><span data-stu-id="1ab49-189">Thank you tooGisela for her contribution toothis article.</span></span>
* [<span data-ttu-id="1ab49-190">Azure API Management: Backing Up and Restoring Configuration (Administración de API de Azure: copia de seguridad y restauración de la configuración)</span><span class="sxs-lookup"><span data-stu-id="1ab49-190">Azure API Management: Backing Up and Restoring Configuration</span></span>](http://blogs.msdn.com/b/stuartleeks/archive/2015/04/29/azure-api-management-backing-up-and-restoring-configuration.aspx)
  * <span data-ttu-id="1ab49-191">enfoque de Hello detallado por Stuart no coincide con la orientación oficial de Hola pero es muy interesante.</span><span class="sxs-lookup"><span data-stu-id="1ab49-191">hello approach detailed by Stuart does not match hello official guidance but it is very interesting.</span></span>

[Backup an API Management service]: #step1
[Restore an API Management service]: #step2


[Azure API Management REST API]: http://msdn.microsoft.com/library/azure/dn781421.aspx

[api-management-add-aad-application]: ./media/api-management-howto-disaster-recovery-backup-restore/api-management-add-aad-application.png

[api-management-aad-permissions]: ./media/api-management-howto-disaster-recovery-backup-restore/api-management-aad-permissions.png
[api-management-aad-permissions-add]: ./media/api-management-howto-disaster-recovery-backup-restore/api-management-aad-permissions-add.png
[api-management-aad-delegated-permissions]: ./media/api-management-howto-disaster-recovery-backup-restore/api-management-aad-delegated-permissions.png
[api-management-aad-default-directory]: ./media/api-management-howto-disaster-recovery-backup-restore/api-management-aad-default-directory.png
[api-management-aad-resources]: ./media/api-management-howto-disaster-recovery-backup-restore/api-management-aad-resources.png
[api-management-arm-token]: ./media/api-management-howto-disaster-recovery-backup-restore/api-management-arm-token.png
[api-management-endpoint]: ./media/api-management-howto-disaster-recovery-backup-restore/api-management-endpoint.png
