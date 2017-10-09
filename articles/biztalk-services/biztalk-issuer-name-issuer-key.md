---
title: aaaIssuer nombre y clave del emisor en servicios de BizTalk | Documentos de Microsoft
description: "Obtenga información acerca de cómo tooretrieve nombre de emisor y clave del emisor de Bus de servicio o de Control de acceso (ACS) en servicios de BizTalk. MABS, WABS"
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
ms.openlocfilehash: cc84c2820724ae3e7fc7c40ddbcd83a169add911
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="biztalk-services-issuer-name-and-issuer-key"></a><span data-ttu-id="b5789-104">Servicios de BizTalk: nombre del emisor y clave del emisor</span><span class="sxs-lookup"><span data-stu-id="b5789-104">BizTalk Services: Issuer Name and Issuer Key</span></span>

> [!INCLUDE [BizTalk Services is being retired, and replaced with Azure Logic Apps](../../includes/biztalk-services-retirement.md)]

<span data-ttu-id="b5789-105">Servicios de BizTalk de Azure usa Hola nombre de emisor de Bus de servicio y clave del emisor y Hola nombre del emisor de Control de acceso y clave del emisor.</span><span class="sxs-lookup"><span data-stu-id="b5789-105">Azure BizTalk Services uses hello Service Bus Issuer Name and Issuer Key, and hello Access Control Issuer Name and Issuer Key.</span></span> <span data-ttu-id="b5789-106">Concretamente:</span><span class="sxs-lookup"><span data-stu-id="b5789-106">Specifically:</span></span>

| <span data-ttu-id="b5789-107">Tarea</span><span class="sxs-lookup"><span data-stu-id="b5789-107">Task</span></span> | <span data-ttu-id="b5789-108">Nombre de emisor y clave de emisor</span><span class="sxs-lookup"><span data-stu-id="b5789-108">Which Issuer Name and Issuer Key</span></span> |
| --- | --- |
| <span data-ttu-id="b5789-109">Implementación de la aplicación desde Visual Studio</span><span class="sxs-lookup"><span data-stu-id="b5789-109">Deploying your application from Visual Studio</span></span> |<span data-ttu-id="b5789-110">Nombre y clave de emisor del servicio de control de acceso</span><span class="sxs-lookup"><span data-stu-id="b5789-110">Access Control Issuer Name and Issuer Key</span></span> |
| <span data-ttu-id="b5789-111">Hola configurar Portal de servicios de BizTalk de Azure</span><span class="sxs-lookup"><span data-stu-id="b5789-111">Configuring hello Azure BizTalk Services Portal</span></span> |<span data-ttu-id="b5789-112">Nombre y clave de emisor del servicio de control de acceso</span><span class="sxs-lookup"><span data-stu-id="b5789-112">Access Control Issuer Name and Issuer Key</span></span> |
| <span data-ttu-id="b5789-113">Crear retransmisiones de LOB con hello servicios del adaptador de BizTalk en Visual Studio</span><span class="sxs-lookup"><span data-stu-id="b5789-113">Creating LOB Relays with hello BizTalk Adapter Services in Visual Studio</span></span> |<span data-ttu-id="b5789-114">Nombre de emisor y clave de emisor del bus de servicio</span><span class="sxs-lookup"><span data-stu-id="b5789-114">Service Bus Issuer Name and Issuer Key</span></span> |

<span data-ttu-id="b5789-115">Este tema enumeran Hola pasos tooretrieve Hola nombre del emisor y clave del emisor.</span><span class="sxs-lookup"><span data-stu-id="b5789-115">This topic lists hello steps tooretrieve hello Issuer Name and Issuer Key.</span></span> 

## <a name="access-control-issuer-name-and-issuer-key"></a><span data-ttu-id="b5789-116">Nombre y clave de emisor del servicio de control de acceso</span><span class="sxs-lookup"><span data-stu-id="b5789-116">Access Control Issuer Name and Issuer Key</span></span>
<span data-ttu-id="b5789-117">Hola, nombre del emisor de Control de acceso y la clave de emisor se utilizan siguiendo hello:</span><span class="sxs-lookup"><span data-stu-id="b5789-117">hello Access Control Issuer Name and Issuer Key are used by hello following:</span></span>

* <span data-ttu-id="b5789-118">La aplicación de servicio de BizTalk de Azure creada en Visual Studio: toosuccessfully implementar la aplicación de BizTalk Service en Visual Studio tooAzure, escriba Hola nombre del emisor de Control de acceso y la clave de emisor.</span><span class="sxs-lookup"><span data-stu-id="b5789-118">Your Azure BizTalk Service application created in Visual Studio: toosuccessfully deploy your BizTalk Service application in Visual Studio tooAzure, you enter hello Access Control Issuer Name and Issuer Key.</span></span> 
* <span data-ttu-id="b5789-119">Hola Portal de servicios de BizTalk de Azure: al crear un BizTalk Service y abra Hola Portal de servicios de BizTalk, el nombre del emisor de Control de acceso y clave del emisor se registra automáticamente para las implementaciones con Hola mismos valores de Control de acceso.</span><span class="sxs-lookup"><span data-stu-id="b5789-119">hello Azure BizTalk Services  Portal: When you create a BizTalk Service and open hello BizTalk Services Portal, your Access Control Issuer Name and Issuer Key are automatically registered for your deployments with hello same Access Control values.</span></span>

### <a name="get-hello-access-control-issuer-name-and-issuer-key"></a><span data-ttu-id="b5789-120">Obtener Hola nombre del emisor de Control de acceso y la clave de emisor</span><span class="sxs-lookup"><span data-stu-id="b5789-120">Get hello Access Control Issuer Name and Issuer Key</span></span>

<span data-ttu-id="b5789-121">ACS toouse para la autenticación y get Hola valores de nombre del emisor y clave del emisor, incluyen hello pasos generales:</span><span class="sxs-lookup"><span data-stu-id="b5789-121">toouse ACS for authentication, and get hello Issuer Name and Issuer Key values, hello overall steps include:</span></span>

1. <span data-ttu-id="b5789-122">Instalar hello [cmdlets de Powershell de Azure](https://azure.microsoft.com/documentation/articles/powershell-install-configure/).</span><span class="sxs-lookup"><span data-stu-id="b5789-122">Install hello [Azure Powershell cmdlets](https://azure.microsoft.com/documentation/articles/powershell-install-configure/).</span></span>
2. <span data-ttu-id="b5789-123">Agregue su cuenta de Azure: `Add-AzureAccount`</span><span class="sxs-lookup"><span data-stu-id="b5789-123">Add your Azure account: `Add-AzureAccount`</span></span>
3. <span data-ttu-id="b5789-124">Devuelva el nombre de su suscripción: `get-azuresubscription`</span><span class="sxs-lookup"><span data-stu-id="b5789-124">Return your subscription name: `get-azuresubscription`</span></span>
4. <span data-ttu-id="b5789-125">Seleccione su suscripción: `select-azuresubscription <name of your subscription>`</span><span class="sxs-lookup"><span data-stu-id="b5789-125">Select your subscription: `select-azuresubscription <name of your subscription>`</span></span> 
5. <span data-ttu-id="b5789-126">Creación de un espacio de nombres nuevo: `new-azuresbnamespace <name for hello service bus> "Location" -CreateACSNamespace $true -NamespaceType Messaging`</span><span class="sxs-lookup"><span data-stu-id="b5789-126">Create a new namespace: `new-azuresbnamespace <name for hello service bus> "Location" -CreateACSNamespace $true -NamespaceType Messaging`</span></span>

    <span data-ttu-id="b5789-127">Ejemplo:`new-azuresbnamespace biztalksbnamespace "South Central US" -CreateACSNamespace $true -NamespaceType Messaging`</span><span class="sxs-lookup"><span data-stu-id="b5789-127">Example:    `new-azuresbnamespace biztalksbnamespace "South Central US" -CreateACSNamespace $true -NamespaceType Messaging`</span></span>
      
5. <span data-ttu-id="b5789-128">Cuando se crea Hola nuevo espacio de nombres ACS (que puede tardar varios minutos), valores de nombre del emisor y clave del emisor de Hola se muestran en la cadena de conexión de hello:</span><span class="sxs-lookup"><span data-stu-id="b5789-128">When hello new ACS namespace is created (which can take several minutes), hello Issuer Name and Issuer Key values are listed in hello connection string:</span></span> 

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

<span data-ttu-id="b5789-129">toosummarize:</span><span class="sxs-lookup"><span data-stu-id="b5789-129">toosummarize:</span></span>  
<span data-ttu-id="b5789-130">Nombre de emisor = SharedSecretIssuer</span><span class="sxs-lookup"><span data-stu-id="b5789-130">Issuer Name = SharedSecretIssuer</span></span>  
<span data-ttu-id="b5789-131">Clave de emisor = SharedSecretKey</span><span class="sxs-lookup"><span data-stu-id="b5789-131">Issuer Key = SharedSecretKey</span></span>

<span data-ttu-id="b5789-132">Más información sobre la hello [New-AzureSBNamespace](https://msdn.microsoft.com/library/dn495165.aspx) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="b5789-132">More on hello [New-AzureSBNamespace](https://msdn.microsoft.com/library/dn495165.aspx) cmdlet.</span></span> 

## <a name="service-bus-issuer-name-and-issuer-key"></a><span data-ttu-id="b5789-133">Nombre de emisor y clave de emisor del bus de servicio</span><span class="sxs-lookup"><span data-stu-id="b5789-133">Service Bus Issuer Name and Issuer Key</span></span>
<span data-ttu-id="b5789-134">Los servicios de adaptador de BizTalk usan el nombre y la clave de emisor del bus de servicio.</span><span class="sxs-lookup"><span data-stu-id="b5789-134">Service Bus Issuer Name and Issuer Key are used by BizTalk Adapter Services.</span></span> <span data-ttu-id="b5789-135">En el proyecto de servicios de BizTalk en Visual Studio, utilice sistema de línea de negocio (LOB) de hello servicios del adaptador BizTalk tooconnect tooan local.</span><span class="sxs-lookup"><span data-stu-id="b5789-135">In your BizTalk Services project in Visual Studio, you use hello BizTalk Adapter Services tooconnect tooan on-premises Line-of-Business (LOB) system.</span></span> <span data-ttu-id="b5789-136">tooconnect, crear hello retransmisión de LOB y escriba los detalles del sistema LOB.</span><span class="sxs-lookup"><span data-stu-id="b5789-136">tooconnect, you create hello LOB Relay and enter your LOB system details.</span></span> <span data-ttu-id="b5789-137">Al hacerlo, también escriba Hola nombre de emisor de Bus de servicio y la clave de emisor.</span><span class="sxs-lookup"><span data-stu-id="b5789-137">When doing this, you also enter hello Service Bus Issuer Name and Issuer Key.</span></span>

### <a name="tooretrieve-hello-service-bus-issuer-name-and-issuer-key"></a><span data-ttu-id="b5789-138">Hola tooretrieve nombre de emisor de Bus de servicio y la clave de emisor</span><span class="sxs-lookup"><span data-stu-id="b5789-138">tooretrieve hello Service Bus Issuer Name and Issuer Key</span></span>
1. <span data-ttu-id="b5789-139">Inicie sesión en toohello [portal de Azure clásico](http://go.microsoft.com/fwlink/p/?LinkID=213885).</span><span class="sxs-lookup"><span data-stu-id="b5789-139">Sign in toohello [Azure classic portal](http://go.microsoft.com/fwlink/p/?LinkID=213885).</span></span>
2. <span data-ttu-id="b5789-140">En el panel de navegación izquierdo de hello, seleccione **Bus de servicio**.</span><span class="sxs-lookup"><span data-stu-id="b5789-140">In hello left navigation pane, select **Service Bus**.</span></span>
3. <span data-ttu-id="b5789-141">Seleccione su espacio de nombres.</span><span class="sxs-lookup"><span data-stu-id="b5789-141">Select your namespace.</span></span> <span data-ttu-id="b5789-142">En la barra de tareas de hello, seleccione **información de conexión**.</span><span class="sxs-lookup"><span data-stu-id="b5789-142">In hello task bar, select **Connection Information**.</span></span> <span data-ttu-id="b5789-143">Esto muestra hello **emisor predeterminado** (nombre del emisor) y **clave predeterminada** (clave del emisor).</span><span class="sxs-lookup"><span data-stu-id="b5789-143">This displays hello **Default Issuer** (Issuer Name) and **Default Key** (Issuer Key).</span></span> <span data-ttu-id="b5789-144">Sus valores se pueden copiar.</span><span class="sxs-lookup"><span data-stu-id="b5789-144">Their values can be copied.</span></span>  

<span data-ttu-id="b5789-145">toosummarize:</span><span class="sxs-lookup"><span data-stu-id="b5789-145">toosummarize:</span></span>  
<span data-ttu-id="b5789-146">Nombre de emisor = Emisor predeterminado</span><span class="sxs-lookup"><span data-stu-id="b5789-146">Issuer Name = Default Issuer</span></span>  
<span data-ttu-id="b5789-147">Clave de emisor = Clave predeterminada</span><span class="sxs-lookup"><span data-stu-id="b5789-147">Issuer Key = Default Key</span></span>

## <a name="next"></a><span data-ttu-id="b5789-148">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="b5789-148">Next</span></span>
<span data-ttu-id="b5789-149">Otros temas acerca de los servicios de BizTalk de Azure:</span><span class="sxs-lookup"><span data-stu-id="b5789-149">Additional Azure BizTalk Services topics:</span></span>

* [<span data-ttu-id="b5789-150">Hola instalar SDK de servicios de BizTalk de Azure</span><span class="sxs-lookup"><span data-stu-id="b5789-150">Installing hello Azure BizTalk Services SDK</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=241589)<br/>
* [<span data-ttu-id="b5789-151">Tutoriales: Azure BizTalk Services</span><span class="sxs-lookup"><span data-stu-id="b5789-151">Tutorials: Azure BizTalk Services</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=236944)<br/>
* [<span data-ttu-id="b5789-152">¿Cómo puedo comenzar a utilizar Hola SDK de servicios de BizTalk de Azure</span><span class="sxs-lookup"><span data-stu-id="b5789-152">How do I Start Using hello Azure BizTalk Services SDK</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=302335)<br/>
* [<span data-ttu-id="b5789-153">Servicios de BizTalk de Azure</span><span class="sxs-lookup"><span data-stu-id="b5789-153">Azure BizTalk Services</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=303664)<br/>

## <a name="see-also"></a><span data-ttu-id="b5789-154">Otras referencias</span><span class="sxs-lookup"><span data-stu-id="b5789-154">See Also</span></span>
* [<span data-ttu-id="b5789-155">Cómo: usar el servicio de administración de ACS tooConfigure las identidades de servicio</span><span class="sxs-lookup"><span data-stu-id="b5789-155">How to: Use ACS Management Service tooConfigure Service Identities</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=303942)<br/>
* [<span data-ttu-id="b5789-156">Servicios de BizTalk: gráfico de las ediciones Developer, Basic, Standard y Premium</span><span class="sxs-lookup"><span data-stu-id="b5789-156">BizTalk Services: Developer, Basic, Standard and Premium Editions Chart</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=302279)<br/>
* [<span data-ttu-id="b5789-157">Servicios de BizTalk: aprovisionamiento con el Portal de Azure clásico</span><span class="sxs-lookup"><span data-stu-id="b5789-157">BizTalk Services: Provisioning Using Azure classic portal</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=302280)<br/>
* [<span data-ttu-id="b5789-158">Servicios de BizTalk: gráfico del estado de aprovisionamiento</span><span class="sxs-lookup"><span data-stu-id="b5789-158">BizTalk Services: Provisioning Status Chart</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=329870)<br/>
* [<span data-ttu-id="b5789-159">Servicios de BizTalk: pestañas Panel, Monitor y Escala</span><span class="sxs-lookup"><span data-stu-id="b5789-159">BizTalk Services: Dashboard, Monitor and Scale tabs</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=302281)<br/>
* [<span data-ttu-id="b5789-160">Servicios de BizTalk: copias de seguridad y restauración</span><span class="sxs-lookup"><span data-stu-id="b5789-160">BizTalk Services: Backup and Restore</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=329873)<br/>
* [<span data-ttu-id="b5789-161">Servicios de BizTalk: limitaciones</span><span class="sxs-lookup"><span data-stu-id="b5789-161">BizTalk Services: Throttling</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=302282)<br/>

