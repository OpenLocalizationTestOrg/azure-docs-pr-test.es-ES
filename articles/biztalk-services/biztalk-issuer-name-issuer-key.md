---
title: Nombre del emisor y clave del emisor en BizTalk Services | Microsoft Azure
description: "Obtenga información acerca de cómo recuperar el Nombre del emisor y la Clave de emisor para el Bus de servicio o Control de acceso (ACS) en Servicios de BizTalk. MABS, WABS"
services: biztalk-services
documentationcenter: 
author: MandiOhlinger
manager: anneta
editor: 
ms.assetid: 067fe356-d1aa-420f-b2f2-1a418686470a
ms.service: biztalk-services
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/07/2016
ms.author: mandia
ms.openlocfilehash: b9fd985c23558596408e78eadae00dd0f95c4214
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="biztalk-services-issuer-name-and-issuer-key"></a><span data-ttu-id="06e2d-104">Servicios de BizTalk: nombre del emisor y clave del emisor</span><span class="sxs-lookup"><span data-stu-id="06e2d-104">BizTalk Services: Issuer Name and Issuer Key</span></span>

> [!INCLUDE [BizTalk Services is being retired, and replaced with Azure Logic Apps](../../includes/biztalk-services-retirement.md)]

<span data-ttu-id="06e2d-105">Los servicios de BizTalk de Azure usan el nombre y la clave de emisor del bus de servicio, además del nombre y la clave de emisor del servicio de control de acceso.</span><span class="sxs-lookup"><span data-stu-id="06e2d-105">Azure BizTalk Services uses the Service Bus Issuer Name and Issuer Key, and the Access Control Issuer Name and Issuer Key.</span></span> <span data-ttu-id="06e2d-106">Concretamente:</span><span class="sxs-lookup"><span data-stu-id="06e2d-106">Specifically:</span></span>

| <span data-ttu-id="06e2d-107">Tarea</span><span class="sxs-lookup"><span data-stu-id="06e2d-107">Task</span></span> | <span data-ttu-id="06e2d-108">Nombre de emisor y clave de emisor</span><span class="sxs-lookup"><span data-stu-id="06e2d-108">Which Issuer Name and Issuer Key</span></span> |
| --- | --- |
| <span data-ttu-id="06e2d-109">Implementación de la aplicación desde Visual Studio</span><span class="sxs-lookup"><span data-stu-id="06e2d-109">Deploying your application from Visual Studio</span></span> |<span data-ttu-id="06e2d-110">Nombre y clave de emisor del servicio de control de acceso</span><span class="sxs-lookup"><span data-stu-id="06e2d-110">Access Control Issuer Name and Issuer Key</span></span> |
| <span data-ttu-id="06e2d-111">Configuración del Portal de servicios de BizTalk de Azure</span><span class="sxs-lookup"><span data-stu-id="06e2d-111">Configuring the Azure BizTalk Services Portal</span></span> |<span data-ttu-id="06e2d-112">Nombre y clave de emisor del servicio de control de acceso</span><span class="sxs-lookup"><span data-stu-id="06e2d-112">Access Control Issuer Name and Issuer Key</span></span> |
| <span data-ttu-id="06e2d-113">Creación de relés de LOB con los servicios de adaptador de BizTalk en Visual Studio</span><span class="sxs-lookup"><span data-stu-id="06e2d-113">Creating LOB Relays with the BizTalk Adapter Services in Visual Studio</span></span> |<span data-ttu-id="06e2d-114">Nombre de emisor y clave de emisor del bus de servicio</span><span class="sxs-lookup"><span data-stu-id="06e2d-114">Service Bus Issuer Name and Issuer Key</span></span> |

<span data-ttu-id="06e2d-115">Este tema incluye los pasos necesarios para recuperar el nombre y la clave de emisor.</span><span class="sxs-lookup"><span data-stu-id="06e2d-115">This topic lists the steps to retrieve the Issuer Name and Issuer Key.</span></span> 

## <a name="access-control-issuer-name-and-issuer-key"></a><span data-ttu-id="06e2d-116">Nombre y clave de emisor del servicio de control de acceso</span><span class="sxs-lookup"><span data-stu-id="06e2d-116">Access Control Issuer Name and Issuer Key</span></span>
<span data-ttu-id="06e2d-117">Los siguientes elementos usan el nombre y la clave de emisor del servicio de control de acceso:</span><span class="sxs-lookup"><span data-stu-id="06e2d-117">The Access Control Issuer Name and Issuer Key are used by the following:</span></span>

* <span data-ttu-id="06e2d-118">Su aplicación del servicio de BizTalk de Azure creada en Visual Studio: para implementar correctamente la aplicación del servicio de BizTalk de Visual Studio en Azure, debe escribir el nombre y la clave de emisor del servicio de control de acceso.</span><span class="sxs-lookup"><span data-stu-id="06e2d-118">Your Azure BizTalk Service application created in Visual Studio: To successfully deploy your BizTalk Service application in Visual Studio to Azure, you enter the Access Control Issuer Name and Issuer Key.</span></span> 
* <span data-ttu-id="06e2d-119">El Portal de Azure BizTalk Services: cuando se crea una instancia de BizTalk Services y se abre el Portal de BizTalk Services, tanto el nombre como la clave del emisor de Access Control se registran automáticamente para las implementaciones con los mismos valores de Access Control.</span><span class="sxs-lookup"><span data-stu-id="06e2d-119">The Azure BizTalk Services  Portal: When you create a BizTalk Service and open the BizTalk Services Portal, your Access Control Issuer Name and Issuer Key are automatically registered for your deployments with the same Access Control values.</span></span>

### <a name="get-the-access-control-issuer-name-and-issuer-key"></a><span data-ttu-id="06e2d-120">Obtención del nombre y la clave de emisor de Access Control</span><span class="sxs-lookup"><span data-stu-id="06e2d-120">Get the Access Control Issuer Name and Issuer Key</span></span>

<span data-ttu-id="06e2d-121">Para usar ACS para la autenticación y obtener los valores de Nombre de emisor y Clave de emisor, los pasos generales son:</span><span class="sxs-lookup"><span data-stu-id="06e2d-121">To use ACS for authentication, and get the Issuer Name and Issuer Key values, the overall steps include:</span></span>

1. <span data-ttu-id="06e2d-122">Instale los [cmdlets de Azure PowerShell](https://azure.microsoft.com/documentation/articles/powershell-install-configure/).</span><span class="sxs-lookup"><span data-stu-id="06e2d-122">Install the [Azure Powershell cmdlets](https://azure.microsoft.com/documentation/articles/powershell-install-configure/).</span></span>
2. <span data-ttu-id="06e2d-123">Agregue su cuenta de Azure: `Add-AzureAccount`</span><span class="sxs-lookup"><span data-stu-id="06e2d-123">Add your Azure account: `Add-AzureAccount`</span></span>
3. <span data-ttu-id="06e2d-124">Devuelva el nombre de su suscripción: `get-azuresubscription`</span><span class="sxs-lookup"><span data-stu-id="06e2d-124">Return your subscription name: `get-azuresubscription`</span></span>
4. <span data-ttu-id="06e2d-125">Seleccione su suscripción: `select-azuresubscription <name of your subscription>`</span><span class="sxs-lookup"><span data-stu-id="06e2d-125">Select your subscription: `select-azuresubscription <name of your subscription>`</span></span> 
5. <span data-ttu-id="06e2d-126">Creación de un espacio de nombres nuevo: `new-azuresbnamespace <name for the service bus> "Location" -CreateACSNamespace $true -NamespaceType Messaging`</span><span class="sxs-lookup"><span data-stu-id="06e2d-126">Create a new namespace: `new-azuresbnamespace <name for the service bus> "Location" -CreateACSNamespace $true -NamespaceType Messaging`</span></span>

    <span data-ttu-id="06e2d-127">Ejemplo:`new-azuresbnamespace biztalksbnamespace "South Central US" -CreateACSNamespace $true -NamespaceType Messaging`</span><span class="sxs-lookup"><span data-stu-id="06e2d-127">Example:    `new-azuresbnamespace biztalksbnamespace "South Central US" -CreateACSNamespace $true -NamespaceType Messaging`</span></span>
      
5. <span data-ttu-id="06e2d-128">Cuando se crea el nuevo espacio de nombres de ACS (que puede tardar varios minutos), los valores de Nombre de emisor y Clave de emisor se enumeran en la cadena de conexión:</span><span class="sxs-lookup"><span data-stu-id="06e2d-128">When the new ACS namespace is created (which can take several minutes), the Issuer Name and Issuer Key values are listed in the connection string:</span></span> 

    ```
    Name                  : biztalksbnamespace
    Region                : South Central US
    DefaultKey            : abcdefghijklmnopqrstuvwxyz
    Status                : Active
    CreatedAt             : 10/18/2016 9:36:30 PM
    AcsManagementEndpoint : https://biztalksbnamespace-sb.accesscontrol.windows.net/
    ServiceBusEndpoint    : https://biztalksbnamespace.servicebus.windows.net/
    ConnectionString      : Endpoint=sb://biztalksbnamespace.servicebus.windows.net/;SharedSecretIssuer=owner;SharedSecretValue=abcdefghijklmnopqrstuvwxyz
    NamespaceType         : Messaging
    ```

<span data-ttu-id="06e2d-129">Resumiendo:</span><span class="sxs-lookup"><span data-stu-id="06e2d-129">To summarize:</span></span>  
<span data-ttu-id="06e2d-130">Nombre de emisor = SharedSecretIssuer</span><span class="sxs-lookup"><span data-stu-id="06e2d-130">Issuer Name = SharedSecretIssuer</span></span>  
<span data-ttu-id="06e2d-131">Clave de emisor = SharedSecretKey</span><span class="sxs-lookup"><span data-stu-id="06e2d-131">Issuer Key = SharedSecretKey</span></span>

<span data-ttu-id="06e2d-132">Más información sobre el cmdlet [New-AzureSBNamespace](https://msdn.microsoft.com/library/dn495165.aspx).</span><span class="sxs-lookup"><span data-stu-id="06e2d-132">More on the [New-AzureSBNamespace](https://msdn.microsoft.com/library/dn495165.aspx) cmdlet.</span></span> 

## <a name="service-bus-issuer-name-and-issuer-key"></a><span data-ttu-id="06e2d-133">Nombre de emisor y clave de emisor del bus de servicio</span><span class="sxs-lookup"><span data-stu-id="06e2d-133">Service Bus Issuer Name and Issuer Key</span></span>
<span data-ttu-id="06e2d-134">Los servicios de adaptador de BizTalk usan el nombre y la clave de emisor del bus de servicio.</span><span class="sxs-lookup"><span data-stu-id="06e2d-134">Service Bus Issuer Name and Issuer Key are used by BizTalk Adapter Services.</span></span> <span data-ttu-id="06e2d-135">En su proyecto de los servicios de BizTalk en Visual Studio, se usan los servicios de adaptador de BizTalk para conectarse a un sistema local de línea de negocio (LOB).</span><span class="sxs-lookup"><span data-stu-id="06e2d-135">In your BizTalk Services project in Visual Studio, you use the BizTalk Adapter Services to connect to an on-premises Line-of-Business (LOB) system.</span></span> <span data-ttu-id="06e2d-136">Para conectarse, debe crear el relé de LOB y especificar los detalles de su sistema de LOB.</span><span class="sxs-lookup"><span data-stu-id="06e2d-136">To connect, you create the LOB Relay and enter your LOB system details.</span></span> <span data-ttu-id="06e2d-137">Para ello, debe especificar el nombre y la clave de emisor del bus de servicio.</span><span class="sxs-lookup"><span data-stu-id="06e2d-137">When doing this, you also enter the Service Bus Issuer Name and Issuer Key.</span></span>

### <a name="to-retrieve-the-service-bus-issuer-name-and-issuer-key"></a><span data-ttu-id="06e2d-138">Recuperación del nombre y la clave de emisor del bus de servicio</span><span class="sxs-lookup"><span data-stu-id="06e2d-138">To retrieve the Service Bus Issuer Name and Issuer Key</span></span>
1. <span data-ttu-id="06e2d-139">Inicie sesión en el [Portal de Azure clásico](http://go.microsoft.com/fwlink/p/?LinkID=213885).</span><span class="sxs-lookup"><span data-stu-id="06e2d-139">Sign in to the [Azure classic portal](http://go.microsoft.com/fwlink/p/?LinkID=213885).</span></span>
2. <span data-ttu-id="06e2d-140">En el panel de navegación izquierdo, haga clic en **Bus de servicio**.</span><span class="sxs-lookup"><span data-stu-id="06e2d-140">In the left navigation pane, select **Service Bus**.</span></span>
3. <span data-ttu-id="06e2d-141">Seleccione su espacio de nombres.</span><span class="sxs-lookup"><span data-stu-id="06e2d-141">Select your namespace.</span></span> <span data-ttu-id="06e2d-142">Seleccione **Información de conexión**en la barra de tareas.</span><span class="sxs-lookup"><span data-stu-id="06e2d-142">In the task bar, select **Connection Information**.</span></span> <span data-ttu-id="06e2d-143">De este modo se muestran el **emisor predeterminado** (nombre de emisor) y la **clave predeterminada** (clave de emisor).</span><span class="sxs-lookup"><span data-stu-id="06e2d-143">This displays the **Default Issuer** (Issuer Name) and **Default Key** (Issuer Key).</span></span> <span data-ttu-id="06e2d-144">Sus valores se pueden copiar.</span><span class="sxs-lookup"><span data-stu-id="06e2d-144">Their values can be copied.</span></span>  

<span data-ttu-id="06e2d-145">Resumiendo:</span><span class="sxs-lookup"><span data-stu-id="06e2d-145">To summarize:</span></span>  
<span data-ttu-id="06e2d-146">Nombre de emisor = Emisor predeterminado</span><span class="sxs-lookup"><span data-stu-id="06e2d-146">Issuer Name = Default Issuer</span></span>  
<span data-ttu-id="06e2d-147">Clave de emisor = Clave predeterminada</span><span class="sxs-lookup"><span data-stu-id="06e2d-147">Issuer Key = Default Key</span></span>

## <a name="next"></a><span data-ttu-id="06e2d-148">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="06e2d-148">Next</span></span>
<span data-ttu-id="06e2d-149">Otros temas acerca de los servicios de BizTalk de Azure:</span><span class="sxs-lookup"><span data-stu-id="06e2d-149">Additional Azure BizTalk Services topics:</span></span>

* [<span data-ttu-id="06e2d-150">Instalación del SDK de Azure BizTalk Services</span><span class="sxs-lookup"><span data-stu-id="06e2d-150">Installing the Azure BizTalk Services SDK</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=241589)<br/>
* [<span data-ttu-id="06e2d-151">Tutoriales: Azure BizTalk Services</span><span class="sxs-lookup"><span data-stu-id="06e2d-151">Tutorials: Azure BizTalk Services</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=236944)<br/>
* [<span data-ttu-id="06e2d-152">¿Cómo puedo comenzar a utilizar el SDK de Servicios de BizTalk de Azure?</span><span class="sxs-lookup"><span data-stu-id="06e2d-152">How do I Start Using the Azure BizTalk Services SDK</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=302335)<br/>
* [<span data-ttu-id="06e2d-153">Servicios de BizTalk de Azure</span><span class="sxs-lookup"><span data-stu-id="06e2d-153">Azure BizTalk Services</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=303664)<br/>

## <a name="see-also"></a><span data-ttu-id="06e2d-154">Otras referencias</span><span class="sxs-lookup"><span data-stu-id="06e2d-154">See Also</span></span>
* [<span data-ttu-id="06e2d-155">Uso del servicio de administración de ACS para configurar identidades de servicio</span><span class="sxs-lookup"><span data-stu-id="06e2d-155">How to: Use ACS Management Service to Configure Service Identities</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=303942)<br/>
* [<span data-ttu-id="06e2d-156">Servicios de BizTalk: gráfico de las ediciones Developer, Basic, Standard y Premium</span><span class="sxs-lookup"><span data-stu-id="06e2d-156">BizTalk Services: Developer, Basic, Standard and Premium Editions Chart</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=302279)<br/>
* [<span data-ttu-id="06e2d-157">Servicios de BizTalk: aprovisionamiento con el Portal de Azure clásico</span><span class="sxs-lookup"><span data-stu-id="06e2d-157">BizTalk Services: Provisioning Using Azure classic portal</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=302280)<br/>
* [<span data-ttu-id="06e2d-158">Servicios de BizTalk: gráfico del estado de aprovisionamiento</span><span class="sxs-lookup"><span data-stu-id="06e2d-158">BizTalk Services: Provisioning Status Chart</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=329870)<br/>
* [<span data-ttu-id="06e2d-159">Servicios de BizTalk: pestañas Panel, Monitor y Escala</span><span class="sxs-lookup"><span data-stu-id="06e2d-159">BizTalk Services: Dashboard, Monitor and Scale tabs</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=302281)<br/>
* [<span data-ttu-id="06e2d-160">Servicios de BizTalk: copias de seguridad y restauración</span><span class="sxs-lookup"><span data-stu-id="06e2d-160">BizTalk Services: Backup and Restore</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=329873)<br/>
* [<span data-ttu-id="06e2d-161">Servicios de BizTalk: limitaciones</span><span class="sxs-lookup"><span data-stu-id="06e2d-161">BizTalk Services: Throttling</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=302282)<br/>

