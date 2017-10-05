---
title: "Implementación de la recuperación ante desastres mediante copias de seguridad y restauración en Azure API Management | Microsoft Docs"
description: "Obtenga información acerca de cómo usar las tareas de copias de seguridad y restauración para llevar a cabo la recuperación ante desastres en Administración de API de Azure."
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
ms.openlocfilehash: 07c0265490cfae733133b6e0c938f90f9b392da4
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/18/2017
---
# <a name="how-to-implement-disaster-recovery-using-service-backup-and-restore-in-azure-api-management"></a><span data-ttu-id="9b1b0-103">Procedimiento para implementar la recuperación ante desastres mediante copias de seguridad y restauración del servicio en Administración de API de Azure</span><span class="sxs-lookup"><span data-stu-id="9b1b0-103">How to implement disaster recovery using service backup and restore in Azure API Management</span></span>
<span data-ttu-id="9b1b0-104">Si decide publicar y administrar las API a través de Administración de API de Azure, podrá aprovechar numerosas capacidades de infraestructura y tolerancia a errores que con otros recursos tendría que diseñar, implementar y administrar.</span><span class="sxs-lookup"><span data-stu-id="9b1b0-104">By choosing to publish and manage your APIs via Azure API Management you are taking advantage of many fault tolerance and infrastructure capabilities that you would otherwise have to design, implement, and manage.</span></span> <span data-ttu-id="9b1b0-105">La plataforma Azure mitiga una gran cantidad de posibles errores a un costo reducido.</span><span class="sxs-lookup"><span data-stu-id="9b1b0-105">The Azure platform mitigates a large fraction of potential failures at a fraction of the cost.</span></span>

<span data-ttu-id="9b1b0-106">Para poder recuperarse de problemas de disponibilidad que afecten a la región donde se hospeda el servicio Administración de API, debe estar preparado para reconstituir el servicio en una región diferente en cualquier momento.</span><span class="sxs-lookup"><span data-stu-id="9b1b0-106">To recover from availability problems affecting the region where your API Management service is hosted you should be ready to reconstitute your service in a different region at any time.</span></span> <span data-ttu-id="9b1b0-107">En función de sus objetivos de disponibilidad y tiempo de recuperación, tal vez desee reservar un servicio de copia de seguridad en una o varias regiones e intentar mantener sincronizados con el servicio activo el contenido y la configuración correspondientes.</span><span class="sxs-lookup"><span data-stu-id="9b1b0-107">Depending on your availability goals and recovery time objective  you might want to reserve a backup service in one or more regions and try to maintain their configuration and content in sync with the active service.</span></span> <span data-ttu-id="9b1b0-108">La característica de copia de seguridad y restauración del servicio ofrece el apoyo necesario para implementar una estrategia de recuperación ante desastres.</span><span class="sxs-lookup"><span data-stu-id="9b1b0-108">The service backup and restore feature provides the necessary building block for implementing your disaster recovery strategy.</span></span>

<span data-ttu-id="9b1b0-109">Esta guía muestra cómo autenticar las solicitudes del Administrador de recursos de Azure y cómo realizar copias de seguridad y restauraciones de las instancias de servicio de administración de API.</span><span class="sxs-lookup"><span data-stu-id="9b1b0-109">This guide shows how to authenticate Azure Resource Manager requests, and how to backup and restore your API Management service instances.</span></span>

> [!NOTE]
> <span data-ttu-id="9b1b0-110">El proceso de copia de seguridad y restauración de una instancia del servicio de administración de API para recuperación ante desastres también puede utilizarse para replicar las instancias de servicio de administración de API para escenarios como almacenamiento provisional.</span><span class="sxs-lookup"><span data-stu-id="9b1b0-110">The process for backing up and restoring an API Management service instance for disaster recovery can also be used for replicating API Management service instances for scenarios such as staging.</span></span>
>
> <span data-ttu-id="9b1b0-111">Tenga en cuenta que cada copia de seguridad expira después de 30 días.</span><span class="sxs-lookup"><span data-stu-id="9b1b0-111">Note that each backup expires after 30 days.</span></span> <span data-ttu-id="9b1b0-112">Si intenta restaurar una copia de seguridad una vez transcurrido el período de expiración de 30 días, se producirá un error en la restauración con un mensaje `Cannot restore: backup expired`.</span><span class="sxs-lookup"><span data-stu-id="9b1b0-112">If you attempt to restore a backup after the 30 day expiration period has expired, the restore will fail with a `Cannot restore: backup expired` message.</span></span>
>
>

## <a name="authenticating-azure-resource-manager-requests"></a><span data-ttu-id="9b1b0-113">Solicitudes de autenticación del Administrador de recursos de Azure</span><span class="sxs-lookup"><span data-stu-id="9b1b0-113">Authenticating Azure Resource Manager requests</span></span>
> [!IMPORTANT]
> <span data-ttu-id="9b1b0-114">La API de REST para copia de seguridad y restauración utiliza el Administrador de recursos de Azure y tiene un mecanismo de autenticación diferente que las API de REST para administrar las entidades de la administración de API.</span><span class="sxs-lookup"><span data-stu-id="9b1b0-114">The REST API for backup and restore uses Azure Resource Manager and has a different authentication mechanism than the REST APIs for managing your API Management entities.</span></span> <span data-ttu-id="9b1b0-115">Los pasos de esta sección describen cómo autenticar las solicitudes del Administrador de recursos de Azure.</span><span class="sxs-lookup"><span data-stu-id="9b1b0-115">The steps in this section describe how to authenticate Azure Resource Manager requests.</span></span> <span data-ttu-id="9b1b0-116">Par obtener más información, consulte [Solicitudes de autenticación del Administrador de recursos de Azure](http://msdn.microsoft.com/library/azure/dn790557.aspx).</span><span class="sxs-lookup"><span data-stu-id="9b1b0-116">For more information, see [Authenticating Azure Resource Manager requests](http://msdn.microsoft.com/library/azure/dn790557.aspx).</span></span>
>
>

<span data-ttu-id="9b1b0-117">Todas las tareas que se realizan en los recursos mediante el Administrador de recursos de Azure deben autenticarse con Azure Active Directory mediante los siguientes pasos.</span><span class="sxs-lookup"><span data-stu-id="9b1b0-117">All of the tasks that you do on resources using the Azure Resource Manager must be authenticated with Azure Active Directory using the following steps.</span></span>

* <span data-ttu-id="9b1b0-118">Agregue una aplicación al inquilino de Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="9b1b0-118">Add an application to the Azure Active Directory tenant.</span></span>
* <span data-ttu-id="9b1b0-119">Establezca permisos para la aplicación que ha agregado.</span><span class="sxs-lookup"><span data-stu-id="9b1b0-119">Set permissions for the application that you added.</span></span>
* <span data-ttu-id="9b1b0-120">Obtenga el token para autenticar solicitudes al Administrador de recursos de Azure.</span><span class="sxs-lookup"><span data-stu-id="9b1b0-120">Get the token for authenticating requests to Azure Resource Manager.</span></span>

<span data-ttu-id="9b1b0-121">El primer paso es crear una aplicación de Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="9b1b0-121">The first step is to create an Azure Active Directory application.</span></span> <span data-ttu-id="9b1b0-122">Inicie sesión en el [Portal de Azure clásico](http://manage.windowsazure.com/) mediante la suscripción que contiene la instancia del servicio Administración de API y navegue hasta la pestaña **Aplicaciones** para su Azure Active Directory predeterminado.</span><span class="sxs-lookup"><span data-stu-id="9b1b0-122">Log into the [Azure Classic Portal](http://manage.windowsazure.com/) using the subscription that contains your API Management service instance and navigate to the **Applications** tab for your default Azure Active Directory.</span></span>

> [!NOTE]
> <span data-ttu-id="9b1b0-123">Si el directorio predeterminado de Azure Active Directory no está visible en su cuenta, póngase en contacto con el administrador de la suscripción de Azure para que le conceda los permisos necesarios para su cuenta.</span><span class="sxs-lookup"><span data-stu-id="9b1b0-123">If the Azure Active Directory default directory is not visible to your account, contact the administrator of the Azure subscription to grant the required permissions to your account.</span></span>

![Creación de una aplicación de Azure Active Directory][api-management-add-aad-application]

<span data-ttu-id="9b1b0-125">Haga clic en **Agregar**, **Agregar una aplicación que mi organización está desarrollando** y elija **Aplicación de cliente nativo**.</span><span class="sxs-lookup"><span data-stu-id="9b1b0-125">Click **Add**, **Add an application my organization is developing**, and choose **Native client application**.</span></span> <span data-ttu-id="9b1b0-126">Escriba un nombre descriptivo y haga clic en la flecha siguiente.</span><span class="sxs-lookup"><span data-stu-id="9b1b0-126">Enter a descriptive name, and click the next arrow.</span></span> <span data-ttu-id="9b1b0-127">Escriba una dirección URL de marcador de posición como `http://resources` para el **URI de redireccionamiento**, ya que es un campo obligatorio, pero el valor no se utiliza más adelante.</span><span class="sxs-lookup"><span data-stu-id="9b1b0-127">Enter a placeholder URL such as `http://resources` for the **Redirect URI**, as it is a required field, but the value is not used later.</span></span> <span data-ttu-id="9b1b0-128">Haga clic en la casilla para guardar la aplicación.</span><span class="sxs-lookup"><span data-stu-id="9b1b0-128">Click the check box to save the application.</span></span>

<span data-ttu-id="9b1b0-129">Una vez que se guarda la aplicación, haga clic en **Configurar**, desplácese hacia abajo a la sección **Permisos para otras aplicaciones** y haga clic en **Agregar aplicación**.</span><span class="sxs-lookup"><span data-stu-id="9b1b0-129">Once the application is saved, click **Configure**, scroll down to the **permissions to other applications** section, and click **Add application**.</span></span>

![Adición de permisos][api-management-aad-permissions-add]

<span data-ttu-id="9b1b0-131">Seleccione **Windows** **Azure Service Management API** y haga clic en la casilla para agregar la aplicación.</span><span class="sxs-lookup"><span data-stu-id="9b1b0-131">Select **Windows** **Azure Service Management API** and click the checkbox to add the application.</span></span>

![Adición de permisos][api-management-aad-permissions]

<span data-ttu-id="9b1b0-133">Haga clic en **Permisos delegados** al lado de la aplicación recién agregada **Windows** **Azure Service Management API**, active la casilla para **Acceso a Azure Service Management (vista previa)** y haga clic en **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="9b1b0-133">Click **Delegated Permissions** beside the newly added **Windows** **Azure Service Management API** application, check the box for **Access Azure Service Management (preview)**, and click **Save**.</span></span>

![Adición de permisos][api-management-aad-delegated-permissions]

<span data-ttu-id="9b1b0-135">Antes de invocar las API que generan la copia de seguridad y la restauran, es necesario obtener un token.</span><span class="sxs-lookup"><span data-stu-id="9b1b0-135">Prior to invoking the APIs that generate the backup and restore it, it is necessary to get a token.</span></span> <span data-ttu-id="9b1b0-136">En el ejemplo siguiente se utiliza el paquete de nuget [Microsoft.IdentityModel.Clients.ActiveDirectory](https://www.nuget.org/packages/Microsoft.IdentityModel.Clients.ActiveDirectory) para recuperar el token.</span><span class="sxs-lookup"><span data-stu-id="9b1b0-136">The following example uses the [Microsoft.IdentityModel.Clients.ActiveDirectory](https://www.nuget.org/packages/Microsoft.IdentityModel.Clients.ActiveDirectory) nuget package to retrieve the token.</span></span>

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
                throw new InvalidOperationException("Failed to obtain the JWT token");
            }

            Console.WriteLine(result.AccessToken);

            Console.ReadLine();
        }
    }
}
```

<span data-ttu-id="9b1b0-137">Reemplace `{tentand id}`, `{application id}` y `{redirect uri}` mediante las siguientes instrucciones.</span><span class="sxs-lookup"><span data-stu-id="9b1b0-137">Replace `{tentand id}`, `{application id}`, and `{redirect uri}` using the following instructions.</span></span>

<span data-ttu-id="9b1b0-138">Reemplace `{tenant id}` con el identificador del inquilino de la aplicación de Azure Active Directory que acaba de crear.</span><span class="sxs-lookup"><span data-stu-id="9b1b0-138">Replace `{tenant id}` with the tenant id of the Azure Active Directory application you just created.</span></span> <span data-ttu-id="9b1b0-139">Para tener acceso al Id. haga clic en **Ver extremos**.</span><span class="sxs-lookup"><span data-stu-id="9b1b0-139">You can access the id by clicking **View endpoints**.</span></span>

![Puntos de conexión][api-management-aad-default-directory]

![Puntos de conexión][api-management-endpoint]

<span data-ttu-id="9b1b0-142">Reemplace `{application id}` y `{redirect uri}` mediante el **Id. de cliente** y la dirección URL de la sección **URI de redirección** desde la pestaña **Configurar** de su aplicación de Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="9b1b0-142">Replace `{application id}` and `{redirect uri}` using the **Client Id** and  the URL from the **Redirect Uris** section from your Azure Active Directory application's **Configure** tab.</span></span>

![Recursos][api-management-aad-resources]

<span data-ttu-id="9b1b0-144">Una vez que se especifican los valores, el ejemplo de código debe devolver un token similar al ejemplo siguiente.</span><span class="sxs-lookup"><span data-stu-id="9b1b0-144">Once the values are specified, the code example should return a token similar to the following example.</span></span>

![SWT][api-management-arm-token]

<span data-ttu-id="9b1b0-146">Antes de llamar a las operaciones de copia de seguridad y restauración descritas en las secciones siguientes, establezca el encabezado de solicitud de autorización para la llamada REST.</span><span class="sxs-lookup"><span data-stu-id="9b1b0-146">Before calling the backup and restore operations described in the following sections, set the authorization request header for your REST call.</span></span>

```c#
request.Headers.Add(HttpRequestHeader.Authorization, "Bearer " + token);
```

## <span data-ttu-id="9b1b0-147"><a name="step1"> </a>Crear una copia de seguridad del servicio API Management</span><span class="sxs-lookup"><span data-stu-id="9b1b0-147"><a name="step1"> </a>Back up an API Management service</span></span>
<span data-ttu-id="9b1b0-148">Para crear una copia de seguridad del servicio API Management, emita esta solicitud HTTP:</span><span class="sxs-lookup"><span data-stu-id="9b1b0-148">To back up an API Management service issue the following HTTP request:</span></span>

`POST https://management.azure.com/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ApiManagement/service/{serviceName}/backup?api-version={api-version}`

<span data-ttu-id="9b1b0-149">donde:</span><span class="sxs-lookup"><span data-stu-id="9b1b0-149">where:</span></span>

* <span data-ttu-id="9b1b0-150">`subscriptionId`: identificador de la suscripción que contiene el servicio Administración de API del que desea crear una copia de seguridad.</span><span class="sxs-lookup"><span data-stu-id="9b1b0-150">`subscriptionId` - id of the subscription containing the API Management service you are attempting to backup</span></span>
* <span data-ttu-id="9b1b0-151">`resourceGroupName`: una cadena de tipo "Api-Default-{service-region}", donde `service-region` identifica la región de Azure donde se hospeda el servicio Administración de API del que desea crear una copia de seguridad (por ejemplo, `North-Central-US`).</span><span class="sxs-lookup"><span data-stu-id="9b1b0-151">`resourceGroupName` - a string in the form of 'Api-Default-{service-region}' where `service-region` identifies the Azure region where the API Management service you are trying to backup is hosted, e.g. `North-Central-US`</span></span>
* <span data-ttu-id="9b1b0-152">`serviceName` : el nombre del servicio Administración de API del que desea crear una copia de seguridad que se especificó durante su creación.</span><span class="sxs-lookup"><span data-stu-id="9b1b0-152">`serviceName` - the name of the API Management service you are making a backup of specified at the time of its creation</span></span>
* <span data-ttu-id="9b1b0-153">`api-version`: reemplazar por `2014-02-14`</span><span class="sxs-lookup"><span data-stu-id="9b1b0-153">`api-version` - replace  with `2014-02-14`</span></span>

<span data-ttu-id="9b1b0-154">En el cuerpo de la solicitud, especifique el nombre de la copia de seguridad, el nombre del contenedor de blobs, la clave de acceso y el nombre de la cuenta de almacenamiento de Azure de destino:</span><span class="sxs-lookup"><span data-stu-id="9b1b0-154">In the body of the request, specify the target Azure storage account name, access key, blob container name, and backup name:</span></span>

```
'{  
    storageAccount : {storage account name for the backup},  
    accessKey : {access key for the account},  
    containerName : {backup container name},  
    backupName : {backup blob name}  
}'
```

<span data-ttu-id="9b1b0-155">Establezca el valor del encabezado de solicitud `Content-Type` en `application/json`.</span><span class="sxs-lookup"><span data-stu-id="9b1b0-155">Set the value of the `Content-Type` request header to `application/json`.</span></span>

<span data-ttu-id="9b1b0-156">La creación de una copia de seguridad es una operación de larga duración que puede tardar varios minutos en completarse.</span><span class="sxs-lookup"><span data-stu-id="9b1b0-156">Backup is a long running operation that may take multiple minutes to complete.</span></span>  <span data-ttu-id="9b1b0-157">Si la solicitud es correcta y el proceso de copia de seguridad se inicia, recibirá un código de estado de respuesta `202 Accepted` con el encabezado `Location`.</span><span class="sxs-lookup"><span data-stu-id="9b1b0-157">If the request was successful and the backup process was initiated you’ll receive a `202 Accepted` response status code with a `Location` header.</span></span>  <span data-ttu-id="9b1b0-158">Realice solicitudes "GET" en la URL del encabezado `Location` para averiguar el estado de la operación.</span><span class="sxs-lookup"><span data-stu-id="9b1b0-158">Make 'GET' requests to the URL in the `Location` header to find out the status of the operation.</span></span> <span data-ttu-id="9b1b0-159">Mientras se crea la copia de seguridad, recibirá el código de estado "202 Aceptado".</span><span class="sxs-lookup"><span data-stu-id="9b1b0-159">While the backup is in progress you will continue to receive a '202 Accepted' status code.</span></span> <span data-ttu-id="9b1b0-160">El código de respuesta `200 OK` indica que la operación de copia de seguridad se ha completado correctamente.</span><span class="sxs-lookup"><span data-stu-id="9b1b0-160">A Response code of `200 OK` will indicate successful completion of the backup operation.</span></span>

<span data-ttu-id="9b1b0-161">Tenga en cuenta las siguientes restricciones al realizar una solicitud de copia de seguridad.</span><span class="sxs-lookup"><span data-stu-id="9b1b0-161">Please note the following constraints when making a backup request.</span></span>

* <span data-ttu-id="9b1b0-162">El **contenedor** que se especifique en el cuerpo de la solicitud **debe ser real**.</span><span class="sxs-lookup"><span data-stu-id="9b1b0-162">**Container** specified in the request body **must exist**.</span></span>
* <span data-ttu-id="9b1b0-163">Mientras se crea la copia de seguridad, **no realice ninguna operación de administración del servicio** (por ejemplo, una actualización o degradación de SKU o un cambio de nombre de dominio).</span><span class="sxs-lookup"><span data-stu-id="9b1b0-163">While backup is in progress you **should not attempt any service management operations** such as SKU upgrade or downgrade, domain name change, etc.</span></span>
* <span data-ttu-id="9b1b0-164">La restauración de una **copia de seguridad se garantiza solo durante 30 días** a partir del momento en que esta se crea.</span><span class="sxs-lookup"><span data-stu-id="9b1b0-164">Restore of a **backup is guaranteed only for 30 days** since the moment of its creation.</span></span>
* <span data-ttu-id="9b1b0-165">Los **datos de uso** con los que se crean informes de análisis **no se incluyen** en la copia de seguridad.</span><span class="sxs-lookup"><span data-stu-id="9b1b0-165">**Usage data** used for creating analytics reports **is not included** in the backup.</span></span> <span data-ttu-id="9b1b0-166">La [API de REST de Azure API Management][Azure API Management REST API] permite recibir de forma periódica informes de análisis para guardarlos en un lugar seguro.</span><span class="sxs-lookup"><span data-stu-id="9b1b0-166">Use [Azure API Management REST API][Azure API Management REST API] to periodically retrieve analytics reports for safekeeping.</span></span>
* <span data-ttu-id="9b1b0-167">La frecuencia con la que se crean las copias de seguridad afecta al objetivo de punto de recuperación.</span><span class="sxs-lookup"><span data-stu-id="9b1b0-167">The frequency with which you perform service backups will affect your recovery point objective.</span></span> <span data-ttu-id="9b1b0-168">Para minimizarlo, se recomienda crear las copias de seguridad de forma periódica y también a petición tras realizar cambios importantes en el servicio Administración de API.</span><span class="sxs-lookup"><span data-stu-id="9b1b0-168">To minimize it we advise implementing regular backups as well as performing on-demand backups after making important changes to your API Management service.</span></span>
* <span data-ttu-id="9b1b0-169">Es posible que los **cambios** que se realicen en la configuración del servicio (por ejemplo, en la API, las directivas o la apariencia del portal para desarrolladores) mientras se está realizando la copia de seguridad **no se incluyan en la copia de seguridad y se pierdan**.</span><span class="sxs-lookup"><span data-stu-id="9b1b0-169">**Changes** made to the service configuration (e.g. APIs, policies, developer portal appearance) while backup operation is in process **might not be included in the backup and therefore will be lost**.</span></span>

## <span data-ttu-id="9b1b0-170"><a name="step2"> </a>Restaurar el servicio Administración de API</span><span class="sxs-lookup"><span data-stu-id="9b1b0-170"><a name="step2"> </a>Restore an API Management service</span></span>
<span data-ttu-id="9b1b0-171">Para restaurar el servicio Administración de API de una copia de seguridad anterior, realice esta solicitud HTTP:</span><span class="sxs-lookup"><span data-stu-id="9b1b0-171">To restore an API Management service from a previously created backup make the following HTTP request:</span></span>

`POST https://management.azure.com/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ApiManagement/service/{serviceName}/restore?api-version={api-version}`

<span data-ttu-id="9b1b0-172">donde:</span><span class="sxs-lookup"><span data-stu-id="9b1b0-172">where:</span></span>

* <span data-ttu-id="9b1b0-173">`subscriptionId`: identificador de la suscripción que contiene el servicio Administración de API en el que se restaura una copia de seguridad.</span><span class="sxs-lookup"><span data-stu-id="9b1b0-173">`subscriptionId` - id of the subscription containing the API Management service you are restoring a backup into</span></span>
* <span data-ttu-id="9b1b0-174">`resourceGroupName`: una cadena de tipo "Api-Default-{service-region}", donde `service-region` identifica la región de Azure donde se hospeda el servicio Administración de API en el que desea restaurar una copia de seguridad (por ejemplo, `North-Central-US`).</span><span class="sxs-lookup"><span data-stu-id="9b1b0-174">`resourceGroupName` - a string in the form of 'Api-Default-{service-region}' where `service-region` identifies the Azure region where the API Management service you are restoring a backup into is hosted, e.g. `North-Central-US`</span></span>
* <span data-ttu-id="9b1b0-175">`serviceName` : el nombre del servicio Administración de API que desea restaurar que se especificó durante su creación.</span><span class="sxs-lookup"><span data-stu-id="9b1b0-175">`serviceName` - the name of the API Management service being restored into specified at the time of its creation</span></span>
* <span data-ttu-id="9b1b0-176">`api-version`: reemplazar por `2014-02-14`</span><span class="sxs-lookup"><span data-stu-id="9b1b0-176">`api-version` - replace  with `2014-02-14`</span></span>

<span data-ttu-id="9b1b0-177">En el cuerpo de la solicitud, especifique la ubicación del archivo de copia de seguridad, es decir, el nombre de la copia de seguridad, el nombre del contenedor de blobs, la clave de acceso y el nombre de la cuenta de almacenamiento de Azure:</span><span class="sxs-lookup"><span data-stu-id="9b1b0-177">In the body of the request, specify the backup file location, i.e. Azure storage account name, access key, blob container name, and backup name:</span></span>

```
'{  
    storageAccount : {storage account name for the backup},  
    accessKey : {access key for the account},  
    containerName : {backup container name},  
    backupName : {backup blob name}  
}'
```

<span data-ttu-id="9b1b0-178">Establezca el valor del encabezado de solicitud `Content-Type` en `application/json`.</span><span class="sxs-lookup"><span data-stu-id="9b1b0-178">Set the value of the `Content-Type` request header to `application/json`.</span></span>

<span data-ttu-id="9b1b0-179">La restauración es una operación de larga duración que puede tardar 30 minutos o más en completarse.</span><span class="sxs-lookup"><span data-stu-id="9b1b0-179">Restore is a long running operation that may take up to 30 or more minutes to complete.</span></span>  <span data-ttu-id="9b1b0-180">Si la solicitud es correcta y el proceso de restauración se inicia, recibirá un código de estado de respuesta `202 Accepted` con el encabezado `Location`.</span><span class="sxs-lookup"><span data-stu-id="9b1b0-180">If the request was successful and the restore process was initiated you’ll receive a `202 Accepted` response status code with a `Location` header.</span></span>  <span data-ttu-id="9b1b0-181">Realice solicitudes "GET" en la URL del encabezado `Location` para averiguar el estado de la operación.</span><span class="sxs-lookup"><span data-stu-id="9b1b0-181">Make 'GET' requests to the URL in the `Location` header to find out the status of the operation.</span></span> <span data-ttu-id="9b1b0-182">Mientras se realiza la restauración, recibirá el código de estado "202 Aceptado".</span><span class="sxs-lookup"><span data-stu-id="9b1b0-182">While the restore is in progress you will continue to receive '202 Accepted' status code.</span></span> <span data-ttu-id="9b1b0-183">El código de respuesta `200 OK` indica que la operación de restauración se ha completado correctamente.</span><span class="sxs-lookup"><span data-stu-id="9b1b0-183">A response code of `200 OK` will indicate successful completion of the restore operation.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="9b1b0-184">**La SKU** en la que desea restaurar el servicio **debe coincidir** con la SKU del servicio del que ha creado una copia de seguridad que desea restaurar.</span><span class="sxs-lookup"><span data-stu-id="9b1b0-184">**The SKU** of the service being restored into **must match** the SKU of the backed up service being restored.</span></span>
>
> <span data-ttu-id="9b1b0-185">Los **cambios** que se realicen en la configuración del servicio (por ejemplo, en la API, las directivas o la apariencia del portal para desarrolladores) con el proceso de restauración en curso **pueden sobrescribirse**.</span><span class="sxs-lookup"><span data-stu-id="9b1b0-185">**Changes** made to the service configuration (e.g. APIs, policies, developer portal appearance) while restore operation is in progress **could be overwritten**.</span></span>
>
>

## <a name="next-steps"></a><span data-ttu-id="9b1b0-186">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="9b1b0-186">Next steps</span></span>
<span data-ttu-id="9b1b0-187">Consulte los siguientes blogs de Microsoft para dos tutoriales diferentes del proceso de copia de seguridad y restauración.</span><span class="sxs-lookup"><span data-stu-id="9b1b0-187">Check out the following Microsoft blogs for two different walkthroughs of the backup/restore process.</span></span>

* [<span data-ttu-id="9b1b0-188">Replicate Azure API Management Accounts (Réplica de cuentas de Administración de API de Azure)</span><span class="sxs-lookup"><span data-stu-id="9b1b0-188">Replicate Azure API Management Accounts</span></span>](https://www.returngis.net/en/2015/06/replicate-azure-api-management-accounts/)
  * <span data-ttu-id="9b1b0-189">Gracias a Gisela por su colaboración en este artículo.</span><span class="sxs-lookup"><span data-stu-id="9b1b0-189">Thank you to Gisela for her contribution to this article.</span></span>
* [<span data-ttu-id="9b1b0-190">Azure API Management: Backing Up and Restoring Configuration (Administración de API de Azure: copia de seguridad y restauración de la configuración)</span><span class="sxs-lookup"><span data-stu-id="9b1b0-190">Azure API Management: Backing Up and Restoring Configuration</span></span>](http://blogs.msdn.com/b/stuartleeks/archive/2015/04/29/azure-api-management-backing-up-and-restoring-configuration.aspx)
  * <span data-ttu-id="9b1b0-191">El enfoque detallado por Stuart no coincide con la orientación oficial, pero es muy interesante.</span><span class="sxs-lookup"><span data-stu-id="9b1b0-191">The approach detailed by Stuart does not match the official guidance but it is very interesting.</span></span>

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
