---
title: "Panel, Monitor, Escala, Configurar y Conexiones híbridas en BizTalk Services | Microsoft Docs"
description: "Obtenga información acerca de los controles y la supervisión del rendimiento en las pestañas del Portal de Azure clásico para Servicios de BizTalk: Panel, Monitor, Escala, Configurar y Conexiones híbridas. MABS, WABS"
services: biztalk-services
documentationcenter: 
author: MandiOhlinger
manager: anneta
editor: 
ms.assetid: 7a1815db-0de2-4274-8be0-198c1b077324
ms.service: biztalk-services
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/07/2016
ms.author: mandia
ms.openlocfilehash: 4ec88d9a681a5692b31f7e3990d1c153296b18ed
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="review-the-dashboard-monitor-scale-configure-and-hybrid-connection-tabs"></a><span data-ttu-id="69d28-104">Revise las pestañas Panel, Monitor, Escala, Configurar y Conexiones híbridas</span><span class="sxs-lookup"><span data-stu-id="69d28-104">Review the Dashboard, Monitor, Scale, Configure, and Hybrid Connection tabs</span></span>

> [!INCLUDE [BizTalk Services is being retired, and replaced with Azure Logic Apps](../../includes/biztalk-services-retirement.md)]

<span data-ttu-id="69d28-105">Después de crear su servicio de  BizTalk e implementar su aplicación, puede cambiar algunas de las configuraciones del servicio de  BizTalk y supervisar el rendimiento de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="69d28-105">After you create your BizTalk Service and deploy your application, you can change some of the BizTalk Service settings and monitor the application performance.</span></span> 

<span data-ttu-id="69d28-106">Al abrir el Portal de Azure clásico, entrará automáticamente en la pestaña **TODOS LOS ELEMENTOS** .</span><span class="sxs-lookup"><span data-stu-id="69d28-106">When you open the Azure classic portal, you are automatically placed at the **ALL ITEMS** tab.</span></span> <span data-ttu-id="69d28-107">Para ver el servicio de BizTalk Services, selecciónelo en la pestaña **TODOS LOS ELEMENTOS** o acceda a la pestaña **BIZTALK SERVICES** y haga clic en el nombre del servicio de BizTalk Services.</span><span class="sxs-lookup"><span data-stu-id="69d28-107">To view your BizTalk Service, select your BizTalk Service in the **ALL ITEMS** tab or select the **BIZTALK SERVICES** tab; and then select your BizTalk Service name.</span></span>

<span data-ttu-id="69d28-108">De este modo se abre una nueva ventana con las pestañas siguientes.</span><span class="sxs-lookup"><span data-stu-id="69d28-108">This opens a new window with the following tabs.</span></span> <span data-ttu-id="69d28-109">En el tema se describen estas pestañas.</span><span class="sxs-lookup"><span data-stu-id="69d28-109">This topic describes these tabs.</span></span>

## <a name="quickstart-quickstartquickstart"></a><span data-ttu-id="69d28-110">Guía de inicio rápido</span><span class="sxs-lookup"><span data-stu-id="69d28-110">Quickstart (</span></span>![Guía de inicio rápido][Quickstart]<span data-ttu-id="69d28-112">)</span><span class="sxs-lookup"><span data-stu-id="69d28-112">)</span></span>
<span data-ttu-id="69d28-113">En función de la edición de Servicios de BizTalk, puede que no estén disponibles todas las opciones mostradas.</span><span class="sxs-lookup"><span data-stu-id="69d28-113">Depending on the BizTalk Services Edition, all options listed may not be available.</span></span> 

<table border="1">
    <tr>
        <td><span data-ttu-id="69d28-114"><strong>Obtener las herramientas</strong></span><span class="sxs-lookup"><span data-stu-id="69d28-114"><strong>Get the tools</strong></span></span></td>
        <td><span data-ttu-id="69d28-115">Descargue el SDK de los servicios de BizTalk para instalar las plantillas del proyecto de Visual Studio en su equipo de desarrollo local.</span><span class="sxs-lookup"><span data-stu-id="69d28-115">Download the BizTalk Services SDK to install the Visual Studio project templates on your on-premises development computer.</span></span> <span data-ttu-id="69d28-116">Estas plantillas crean los proyectos de Visual Studio <strong>BizTalk Services</strong> (puente) y <strong>Artefactos de BizTalk Services</strong> (transformación), que se implementan en el servicio de BizTalk Services.</span><span class="sxs-lookup"><span data-stu-id="69d28-116">These templates create the <strong>BizTalk Services</strong> (bridge) and the <strong>BizTalk Service Artifacts</strong> (Transform) Visual Studio projects that are deployed to your BizTalk Service.</span></span>
        <br/><br/><span data-ttu-id="69d28-117">En 
        <a HREF="http://go.microsoft.com/fwlink/p/?LinkID=302335">Introducción al uso del SDK de Azure BizTalk Services</a> e <a HREF="http://go.microsoft.com/fwlink/p/?LinkID=241589">Instalación del SDK de Azure BizTalk Services</a>, se incluyen los pasos para empezar.</span><span class="sxs-lookup"><span data-stu-id="69d28-117">
        <a HREF="http://go.microsoft.com/fwlink/p/?LinkID=302335"> How do I Start Using the Azure BizTalk Services SDK </a> and <a HREF="http://go.microsoft.com/fwlink/p/?LinkID=241589">Installing the Azure BizTalk Services SDK</a> lists the steps to get started.</span></span>
        </td>
    </tr>
    <tr>
        <td><span data-ttu-id="69d28-118"><strong>Crear acuerdos de asociados comerciales</strong></span><span class="sxs-lookup"><span data-stu-id="69d28-118"><strong>Create partner agreements</strong></span></span></td>
        <td><span data-ttu-id="69d28-119">Abre el Portal de los servicios de BizTalk de Azure hospedados en Azure, donde se agregan socios y se crean los acuerdos X12, AS2 y EDIFACT EDI.</span><span class="sxs-lookup"><span data-stu-id="69d28-119">Opens the Azure BizTalk Services Portal hosted on Azure where you add partners and create X12, AS2, and EDIFACT EDI agreements.</span></span>
        <br/><br/><span data-ttu-id="69d28-120">En 
        <a HREF="http://go.microsoft.com/fwlink/p/?LinkID=303653">Configuración de los componentes de mensajería EDI en el portal de BizTalk Services</a>, se incluyen los pasos para empezar.</span><span class="sxs-lookup"><span data-stu-id="69d28-120">
        <a HREF="http://go.microsoft.com/fwlink/p/?LinkID=303653">Configuring Components for EDI Messaging on BizTalk Services Portal</a> lists the steps to get started.</span></span>
        </td>
    </tr>

<tr>
        <td><span data-ttu-id="69d28-121"><strong>Más información sobre BizTalk Services</strong></span><span class="sxs-lookup"><span data-stu-id="69d28-121"><strong>Learn more about BizTalk Services</strong></span></span></td>
        <td><span data-ttu-id="69d28-122">Para más información sobre Azure BizTalk Services, vaya al <a HREF="http://azure.microsoft.com/documentation/services/biztalk-services/">centro de aprendizaje</a>.</span><span class="sxs-lookup"><span data-stu-id="69d28-122">Go to the <a HREF="http://azure.microsoft.com/documentation/services/biztalk-services/">learning center</a> to learn more about Azure BizTalk Services.</span></span></td>
</tr>
</table>


<span data-ttu-id="69d28-123">En la barra de tareas de la parte inferior, puede:</span><span class="sxs-lookup"><span data-stu-id="69d28-123">In the task bar at the bottom, you can:</span></span>

<table border="1">

<tr>
<td><span data-ttu-id="69d28-124"><strong>Administrar</strong> la implementación de la aplicación</span><span class="sxs-lookup"><span data-stu-id="69d28-124"><strong>Manage</strong> your application deployment</span></span></td>
<td><span data-ttu-id="69d28-125">Abre el portal de Servicios de BizTalk de Azure.</span><span class="sxs-lookup"><span data-stu-id="69d28-125">Opens the Azure BizTalk Services portal.</span></span> <span data-ttu-id="69d28-126">El Portal de Servicios de BizTalk es la entrada a la configuración EDI, incluyendo la incorporación de socios y la creación de los acuerdos X12, AS2 y EDIFACT.</span><span class="sxs-lookup"><span data-stu-id="69d28-126">The BizTalk Services Portal is the entrance to EDI configuration, including adding partners and creating X12, AS2, and EDIFACT agreements.</span></span>
<br/><br/>
<span data-ttu-id="69d28-127">La operación es la misma que si selecciona <strong>Crear acuerdos de asociado</strong> en la pestaña <strong>Inicio rápido</strong>.</span><span class="sxs-lookup"><span data-stu-id="69d28-127">This is the same as <strong>Create partner agreements</strong> on the <strong>Quick Start</strong> tab.</span></span>
<br/><br/><span data-ttu-id="69d28-128">En 
<a HREF="http://go.microsoft.com/fwlink/p/?LinkID=303653">Configuración de los componentes de mensajería EDI en el portal de BizTalk Services</a>, encontrará más información sobre el portal de BizTalk Services.</span><span class="sxs-lookup"><span data-stu-id="69d28-128">
<a HREF="http://go.microsoft.com/fwlink/p/?LinkID=303653">Configuring Components for EDI Messaging on BizTalk Services Portal</a> provides more information on the BizTalk Services Portal.</span></span></td>
</tr>

<tr>
<td><span data-ttu-id="69d28-129"><strong>Información de conexión</strong> del espacio de nombres de Access Control</span><span class="sxs-lookup"><span data-stu-id="69d28-129"><strong>Connection Information</strong> of the Access Control Namespace</span></span></td>
<td><span data-ttu-id="69d28-130">Al seleccionar Información de conexión, aparecen el espacio de nombres del servicio de control de acceso, el emisor predeterminado y la clave predeterminada.</span><span class="sxs-lookup"><span data-stu-id="69d28-130">When you select Connection Information, then the Access Control Namespace, Default Issuer, and Default Key are displayed.</span></span> <span data-ttu-id="69d28-131">Estos valores se pueden copiar.</span><span class="sxs-lookup"><span data-stu-id="69d28-131">You can copy these values.</span></span>
<br/><br/>
<span data-ttu-id="69d28-132">Además, puede abrir el Portal de control de acceso.</span><span class="sxs-lookup"><span data-stu-id="69d28-132">You can also open the Access Control Portal.</span></span> <span data-ttu-id="69d28-133">En <a HREF="http://go.microsoft.com/fwlink/p/?LinkID=285670">Creación de un espacio de nombres de Access Control</a>, encontrará más información sobre el portal de Access Control.</span><span class="sxs-lookup"><span data-stu-id="69d28-133"><a HREF="http://go.microsoft.com/fwlink/p/?LinkID=285670">Create an Access control Namespace</a> provides more information on the Access Control Portal.</span></span></td>
</tr>

<tr>
<td><span data-ttu-id="69d28-134"><strong>Sincronizar claves</strong> en la cuenta de almacenamiento</span><span class="sxs-lookup"><span data-stu-id="69d28-134"><strong>Sync Keys</strong> in the Storage Account</span></span></td>
<td><span data-ttu-id="69d28-135">Cuando crea una cuenta de almacenamiento, se crean automáticamente una clave primaria y una clave secundaria.</span><span class="sxs-lookup"><span data-stu-id="69d28-135">When you create a Storage account, a Primary Key and Secondary Key are automatically created.</span></span> <span data-ttu-id="69d28-136">Estas claves de cifrado controlan el acceso a su cuenta de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="69d28-136">These encryption Keys control access to your Storage Account.</span></span> <span data-ttu-id="69d28-137">Su servicio de BizTalk utiliza automáticamente la clave principal.</span><span class="sxs-lookup"><span data-stu-id="69d28-137">Your BizTalk Service automatically uses the Primary Key.</span></span> <span data-ttu-id="69d28-138"><strong>Sincronizar claves</strong> permite al usuario alternar entre la clave principal y la clave secundaria sin interrumpir el servicio de BizTalk.</span><span class="sxs-lookup"><span data-stu-id="69d28-138"><strong>Sync Keys</strong> enable users to switch between the Primary Key and the Secondary Key without disrupting the BizTalk Service.</span></span>
<br/><br/>
<span data-ttu-id="69d28-139">Por ejemplo, en caso de que desee que el servicio de BizTalk use una nueva clave principal para la cuenta de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="69d28-139">For example, you want the BizTalk Service to use a new Primary Key for the Storage Account.</span></span> <span data-ttu-id="69d28-140">Para ello, siga estos pasos:</span><span class="sxs-lookup"><span data-stu-id="69d28-140">To do this:</span></span>
<br/><br/>
<ol>
<li><span data-ttu-id="69d28-141">Seleccione el servicio de BizTalk y después <strong>Sincronizar claves</strong>.</span><span class="sxs-lookup"><span data-stu-id="69d28-141">Select your BizTalk Service and select <strong>Sync Keys</strong>.</span></span> <span data-ttu-id="69d28-142">Seleccione la clave secundaria.</span><span class="sxs-lookup"><span data-stu-id="69d28-142">Select the Secondary Key.</span></span> <span data-ttu-id="69d28-143">Al hacer esto, el servicio de BizTalk se inicia usando la clave secundaria.</span><span class="sxs-lookup"><span data-stu-id="69d28-143">When you do this, the BizTalk Service starts using the Secondary Key.</span></span></li>
<li><span data-ttu-id="69d28-144">En el Portal de Azure clásico, seleccione la cuenta de almacenamiento y Regenerar la clave principal.</span><span class="sxs-lookup"><span data-stu-id="69d28-144">In the Azure classic portal, select your Storage account and Regenerate the Primary Key.</span></span> <span data-ttu-id="69d28-145">Recuerde que su servicio de BizTalk usa la clave secundaria.</span><span class="sxs-lookup"><span data-stu-id="69d28-145">Remember, your BizTalk Service is using the Secondary Key.</span></span></li>
<li><span data-ttu-id="69d28-146">Seleccione el servicio de BizTalk y después <strong>Sincronizar claves</strong>.</span><span class="sxs-lookup"><span data-stu-id="69d28-146">Select your BizTalk Service and select <strong>Sync Keys</strong>.</span></span> <span data-ttu-id="69d28-147">Ahora, seleccione la clave principal.</span><span class="sxs-lookup"><span data-stu-id="69d28-147">Now, select the Primary Key.</span></span> <span data-ttu-id="69d28-148">Esta es la nueva clave principal que ha regenerado.</span><span class="sxs-lookup"><span data-stu-id="69d28-148">This is the new Primary Key you regenerated.</span></span></li>
<li><span data-ttu-id="69d28-149">En el Portal de Azure clásico, seleccione la cuenta de almacenamiento y Regenerar la clave secundaria.</span><span class="sxs-lookup"><span data-stu-id="69d28-149">In the Azure classic portal, select your Storage account and Regenerate the Secondary Key.</span></span></li>
</ol>
<br/>
<span data-ttu-id="69d28-150">Este proceso se llama "claves de sustitución".</span><span class="sxs-lookup"><span data-stu-id="69d28-150">This process is called "rollover keys".</span></span> <span data-ttu-id="69d28-151">Su finalidad es permitir al usuario alternar entre la clave principal y la clave secundaria sin interrumpir el servicio de BizTalk.</span><span class="sxs-lookup"><span data-stu-id="69d28-151">The purpose is to enable users to switch between the Primary Key and the Secondary Key without disrupting the BizTalk Service.</span></span></td>
</tr>

<tr>
<td><span data-ttu-id="69d28-152"><strong>Eliminar</strong> la aplicación</span><span class="sxs-lookup"><span data-stu-id="69d28-152"><strong>Delete</strong> your application</span></span></td>
<td><span data-ttu-id="69d28-153">Al seleccionar en Eliminar, se elimina su servicio de BizTalk y todos los elementos implementados en él.</span><span class="sxs-lookup"><span data-stu-id="69d28-153">When you select Delete, your BizTalk Service and all items deployed to it are removed.</span></span></td>
</tr>
</table>


## <a name="dashboard"></a><span data-ttu-id="69d28-154">Panel</span><span class="sxs-lookup"><span data-stu-id="69d28-154">Dashboard</span></span>
<span data-ttu-id="69d28-155">En función de la edición de Servicios de BizTalk, puede que no estén disponibles todas las opciones mostradas.</span><span class="sxs-lookup"><span data-stu-id="69d28-155">Depending on the BizTalk Services Edition, all options listed may not be available.</span></span> 

<span data-ttu-id="69d28-156">Al seleccionar el nombre de su servicio de BizTalk, aparece la pestaña Panel.</span><span class="sxs-lookup"><span data-stu-id="69d28-156">When you select your BizTalk Service name, the Dashboard tab is displayed.</span></span> <span data-ttu-id="69d28-157">En el Panel, existen las siguientes opciones:</span><span class="sxs-lookup"><span data-stu-id="69d28-157">In Dashboard, you can:</span></span>

##### <a name="usage-overview-shows-the-number-of-used-hybrid-connections"></a><span data-ttu-id="69d28-158">Información general del uso: muestra el número de conexiones híbridas usadas</span><span class="sxs-lookup"><span data-stu-id="69d28-158">Usage Overview: Shows the number of used Hybrid Connections</span></span>
<span data-ttu-id="69d28-159">También muestra el uso de datos en GB.</span><span class="sxs-lookup"><span data-stu-id="69d28-159">Also displays the data usage in GB.</span></span> 

##### <a name="metric-graph-shows-a-fixed-list-of-performance-metrics"></a><span data-ttu-id="69d28-160">Gráfico de métrica: muestra una lista fija de métricas de rendimiento</span><span class="sxs-lookup"><span data-stu-id="69d28-160">Metric Graph: Shows a fixed list of performance metrics</span></span>
<span data-ttu-id="69d28-161">Estas métricas proporcionan valores en tiempo real relacionados con el estado de su servicio de BizTalk.</span><span class="sxs-lookup"><span data-stu-id="69d28-161">These metrics provide real-time values regarding the health of the BizTalk Service.</span></span> <span data-ttu-id="69d28-162">También puede elegir los valores **Relativo** o **Absoluto** y el valor de **Intervalo** de las métricas que aparecen en el gráfico.</span><span class="sxs-lookup"><span data-stu-id="69d28-162">You can also choose the **Relative** or **Absolute** values and the time range **Interval** of the metrics that are displayed in the graph.</span></span> 

<span data-ttu-id="69d28-163">Para ver una descripción de estas métricas de rendimiento, vaya a la sección [Métricas disponibles](#Metrics) de este tema.</span><span class="sxs-lookup"><span data-stu-id="69d28-163">For a description of these performance metrics, go to [Available Metrics](#Metrics) in this topic.</span></span>

##### <a name="quick-glance-lists-your-biztalk-service-properties"></a><span data-ttu-id="69d28-164">Vista rápida: muestra las propiedades del servicio de BizTalk</span><span class="sxs-lookup"><span data-stu-id="69d28-164">Quick Glance: Lists your BizTalk Service properties</span></span>
<table border="1">

<tr>
<td><span data-ttu-id="69d28-165"><strong>Actualizar credenciales de la base de datos de seguimiento</strong></span><span class="sxs-lookup"><span data-stu-id="69d28-165"><strong>Update Tracking Database credentials</strong></span></span></td>
<td><span data-ttu-id="69d28-166">Cambia el nombre de usuario y la contraseña usados para iniciar sesión en la base de datos de seguimiento.</span><span class="sxs-lookup"><span data-stu-id="69d28-166">Changes the user name and password used to log into the Tracking Database.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="69d28-167"><strong>Actualizar certificado SSL</strong></span><span class="sxs-lookup"><span data-stu-id="69d28-167"><strong>Update SSL Certificate</strong></span></span></td>
<td><span data-ttu-id="69d28-168">Puede actualizar el servicio de BizTalk para que use un certificado SSL diferente.</span><span class="sxs-lookup"><span data-stu-id="69d28-168">Can update the BizTalk Service to use a different SSL certificate.</span></span> <span data-ttu-id="69d28-169">Al <a HREF="http://go.microsoft.com/fwlink/p/?LinkID=302280">crear el servicio de BizTalk</a>, se genera automáticamente un certificado SSL autofirmado.</span><span class="sxs-lookup"><span data-stu-id="69d28-169">A self-signed SSL certificate is automatically created when you <a HREF="http://go.microsoft.com/fwlink/p/?LinkID=302280">create the BizTalk Service</a>.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="69d28-170"><strong>Descarga del certificado</strong></span><span class="sxs-lookup"><span data-stu-id="69d28-170"><strong>Download Certificate</strong></span></span></td>
<td><span data-ttu-id="69d28-171">Puede descargar el certificado SSL usado por su Servicio de BizTalk en una máquina local.</span><span class="sxs-lookup"><span data-stu-id="69d28-171">You can download the SSL certificate used by your BizTalk Service to a local machine.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="69d28-172"><strong>Estado</strong></span><span class="sxs-lookup"><span data-stu-id="69d28-172"><strong>Status</strong></span></span></td>
<td><span data-ttu-id="69d28-173">Muestra el estado actual del Servicio de BizTalk.</span><span class="sxs-lookup"><span data-stu-id="69d28-173">Displays the current status of your BizTalk Service.</span></span> <span data-ttu-id="69d28-174">Consulte <a HREF="http://go.microsoft.com/fwlink/p/?LinkID=329870">BizTalk Services: gráfico del estado del servicio de BizTalk</a>.</span><span class="sxs-lookup"><span data-stu-id="69d28-174">See <a HREF="http://go.microsoft.com/fwlink/p/?LinkID=329870">BizTalk Services: Service state chart</a>.</span></span> </td>
</tr>
<tr>
<td><span data-ttu-id="69d28-175"><strong>URL de servicio</strong></span><span class="sxs-lookup"><span data-stu-id="69d28-175"><strong>Service URL</strong></span></span></td>
<td><span data-ttu-id="69d28-176">Dirección URL para el Servicio de BizTalk.</span><span class="sxs-lookup"><span data-stu-id="69d28-176">The URL for your BizTalk Service.</span></span> <span data-ttu-id="69d28-177">Es la misma que la dirección <strong>URL de dominio</strong> que se especificó al crear el servicio de BizTalk.</span><span class="sxs-lookup"><span data-stu-id="69d28-177">This is the same as the <strong>Domain URL</strong> entered when your BizTalk Service is created.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="69d28-178"><strong>Dirección IP virtual (VIP) pública</strong></span><span class="sxs-lookup"><span data-stu-id="69d28-178"><strong>Public Virtual IP (VIP) Address</strong></span></span></td>
<td><span data-ttu-id="69d28-179">La dirección IP asignada al Servicio de BizTalk.</span><span class="sxs-lookup"><span data-stu-id="69d28-179">The IP address assigned to your BizTalk Service.</span></span> <span data-ttu-id="69d28-180">Se usa para todos los extremos de entrada y es la dirección de origen para el tráfico saliente.</span><span class="sxs-lookup"><span data-stu-id="69d28-180">It is used for all input endpoints and is the source address for outbound traffic.</span></span> <span data-ttu-id="69d28-181">Esta dirección IP pertenece al servicio de BizTalk mientras esté creado.</span><span class="sxs-lookup"><span data-stu-id="69d28-181">This IP address belongs to your BizTalk Service as long as it is created.</span></span> <span data-ttu-id="69d28-182">Si elimina el servicio de BizTalk, la dirección IP se asigna a otro Servicios de BizTalk.</span><span class="sxs-lookup"><span data-stu-id="69d28-182">If you delete the BizTalk Service, the IP address is assigned to another BizTalk Service.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="69d28-183"><strong>ACS Namespace</strong></span><span class="sxs-lookup"><span data-stu-id="69d28-183"><strong>ACS Namespace</strong></span></span></td>
<td><span data-ttu-id="69d28-184">Se autentica con el servicio de BizTalk.</span><span class="sxs-lookup"><span data-stu-id="69d28-184">Authenticates with the BizTalk Service.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="69d28-185"><strong>Edición</strong></span><span class="sxs-lookup"><span data-stu-id="69d28-185"><strong>Edition</strong></span></span></td>
<td><span data-ttu-id="69d28-186">Muestra la edición especificada al crear el Servicio de BizTalk.</span><span class="sxs-lookup"><span data-stu-id="69d28-186">Lists the Edition entered when the BizTalk Service is created.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="69d28-187"><strong>Ubicación</strong></span><span class="sxs-lookup"><span data-stu-id="69d28-187"><strong>Location</strong></span></span></td>
<td><span data-ttu-id="69d28-188">Muestra la región geográfica donde se hospeda el Servicio de BizTalk.</span><span class="sxs-lookup"><span data-stu-id="69d28-188">Displays the geographic region that hosts your BizTalk Service.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="69d28-189"><strong>Created</strong></span><span class="sxs-lookup"><span data-stu-id="69d28-189"><strong>Created</strong></span></span></td>
<td><span data-ttu-id="69d28-190">Muestra la fecha y la hora en que se creó el Servicio de BizTalk.</span><span class="sxs-lookup"><span data-stu-id="69d28-190">Displays the date and time the BizTalk Service was created.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="69d28-191"><strong>Tracking Database</strong></span><span class="sxs-lookup"><span data-stu-id="69d28-191"><strong>Tracking Database</strong></span></span></td>
<td><span data-ttu-id="69d28-192">El nombre de la base de datos SQL de Azure que almacena las tablas de seguimiento usadas por su servicio de BizTalk.</span><span class="sxs-lookup"><span data-stu-id="69d28-192">The Azure SQL Database name that stores the tracking tables used by your BizTalk Service.</span></span> 
<br/><br/><span data-ttu-id="69d28-193">En esta 
<a HREF="http://go.microsoft.com/fwlink/p/?LinkID=302280">explicación de los requisitos</a>, encontrará más información sobre la base de datos de seguimiento.</span><span class="sxs-lookup"><span data-stu-id="69d28-193">
<a HREF="http://go.microsoft.com/fwlink/p/?LinkID=302280">Requirements Explained</a>  provides details on the Tracking Database.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="69d28-194"><strong>Monitoring/Archiving Storage</strong></span><span class="sxs-lookup"><span data-stu-id="69d28-194"><strong>Monitoring/Archiving Storage</strong></span></span></td>
<td><span data-ttu-id="69d28-195">La cuenta de almacenamiento de Azure que almacena el resultado de supervisión del servicio de BizTalk.</span><span class="sxs-lookup"><span data-stu-id="69d28-195">The Azure Storage account name that stores the monitoring output of your BizTalk Service.</span></span>
<br/><br/><span data-ttu-id="69d28-196">En esta 
<a HREF="http://go.microsoft.com/fwlink/p/?LinkID=302280">explicación de los requisitos</a>, encontrará más información sobre la cuenta de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="69d28-196">
<a HREF="http://go.microsoft.com/fwlink/p/?LinkID=302280">Requirements Explained</a>  provides details on the Storage account.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="69d28-197"><strong>Subscription Name</strong></span><span class="sxs-lookup"><span data-stu-id="69d28-197"><strong>Subscription Name</strong></span></span></td>
<td><span data-ttu-id="69d28-198">Muestra la suscripción que hospeda el Servicio de BizTalk.</span><span class="sxs-lookup"><span data-stu-id="69d28-198">Lists the subscription that hosts your BizTalk Service.</span></span> <span data-ttu-id="69d28-199">La suscripción rige el acceso al Portal de Azure clásico.</span><span class="sxs-lookup"><span data-stu-id="69d28-199">The subscription governs access to the Azure classic portal.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="69d28-200"><strong>Subscription ID</strong></span><span class="sxs-lookup"><span data-stu-id="69d28-200"><strong>Subscription ID</strong></span></span></td>
<td><span data-ttu-id="69d28-201">Cuando se crea una suscripción, se genera automáticamente un identificador de suscripción.</span><span class="sxs-lookup"><span data-stu-id="69d28-201">When a subscription is created, a subscription ID is automatically generated.</span></span> <span data-ttu-id="69d28-202">Cuando se usan las API REST, puede que tenga que especificar el identificador de suscripción.</span><span class="sxs-lookup"><span data-stu-id="69d28-202">When using REST APIs, you may need to enter the Subscription ID.</span></span></td>
</tr>
</table>

<span data-ttu-id="69d28-203">[Servicios de BizTalk: aprovisionamiento con el Portal de Azure clásico](http://go.microsoft.com/fwlink/p/?LinkID=302280) incluye los pasos para crear un servicio de BizTalk.</span><span class="sxs-lookup"><span data-stu-id="69d28-203">[BizTalk Services: Provisioning Using Azure classic portal](http://go.microsoft.com/fwlink/p/?LinkID=302280) lists the steps to create a BizTalk Service.</span></span>

##### <a name="manage-connection-information-sync-keys-and-delete-in-the-task-bar"></a><span data-ttu-id="69d28-204">Administrar, Información de conexión, Sincronizar claves y Eliminar en la barra de tareas:</span><span class="sxs-lookup"><span data-stu-id="69d28-204">Manage, Connection Information, Sync Keys, and Delete in the task bar:</span></span>
<table border="1">

<tr>
<td><span data-ttu-id="69d28-205"><strong>Administrar</strong> la implementación de la aplicación</span><span class="sxs-lookup"><span data-stu-id="69d28-205"><strong>Manage</strong> your application deployment</span></span></td>
<td><span data-ttu-id="69d28-206">Abre el portal de Servicios de BizTalk de Azure.</span><span class="sxs-lookup"><span data-stu-id="69d28-206">Opens the Azure BizTalk Services Portal.</span></span> <span data-ttu-id="69d28-207">El Portal de Servicios de BizTalk es la entrada a la configuración EDI, incluyendo la incorporación de socios y la creación de los acuerdos X12, AS2 y EDIFACT.</span><span class="sxs-lookup"><span data-stu-id="69d28-207">The BizTalk Services Portal is the entrance to EDI configuration, including adding partners and creating X12, AS2, and EDIFACT agreements.</span></span>
<br/><br/>
<span data-ttu-id="69d28-208">La operación es la misma que si selecciona <strong>Crear acuerdos de asociado</strong> en la pestaña <strong>Inicio rápido</strong>.</span><span class="sxs-lookup"><span data-stu-id="69d28-208">This is the same as <strong>Create partner agreements</strong> on the <strong>Quick Start</strong> tab.</span></span>
<br/><br/><span data-ttu-id="69d28-209">En 
<a HREF="http://go.microsoft.com/fwlink/p/?LinkID=303653">Configuración de los componentes de mensajería EDI en el portal de BizTalk Services</a>, encontrará más información sobre el portal de BizTalk Services.</span><span class="sxs-lookup"><span data-stu-id="69d28-209">
<a HREF="http://go.microsoft.com/fwlink/p/?LinkID=303653">Configuring Components for EDI Messaging on BizTalk Services Portal</a> provides more information on the BizTalk Services Portal.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="69d28-210"><strong>Información de conexión</strong> del espacio de nombres de Access Control</span><span class="sxs-lookup"><span data-stu-id="69d28-210"><strong>Connection Information</strong> of the Access Control Namespace</span></span></td>
<td><span data-ttu-id="69d28-211">Muestra los valores del espacio de nombres de control de acceso, el emisor predeterminado y la clave predeterminada, que se pueden copiar.</span><span class="sxs-lookup"><span data-stu-id="69d28-211">Displays the Access Control Namespace, Default Issuer, and Default Key values; which can be copied.</span></span>
<br/><br/>
<span data-ttu-id="69d28-212">Además, puede abrir el Portal de control de acceso.</span><span class="sxs-lookup"><span data-stu-id="69d28-212">You can also open the Access Control Portal.</span></span> <span data-ttu-id="69d28-213">Este portal de control de acceso es lo mismo que usar la opción de Active Directory en el panel de navegación izquierdo.</span><span class="sxs-lookup"><span data-stu-id="69d28-213">This Access Control Portal is the same as using the Active Directory option in the left navigation pane.</span></span>
<br/><br/><span data-ttu-id="69d28-214">En este artículo sobre la 
<a HREF="http://go.microsoft.com/fwlink/p/?LinkID=285670">administración del espacio de nombres ACS</a>, encontrará más información acerca del portal de Access Control.</span><span class="sxs-lookup"><span data-stu-id="69d28-214">
<a HREF="http://go.microsoft.com/fwlink/p/?LinkID=285670">Managing Your ACS Namespace</a> provides more information on the Access Control Portal.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="69d28-215"><strong>Sincronizar claves</strong> en la cuenta de almacenamiento</span><span class="sxs-lookup"><span data-stu-id="69d28-215"><strong>Sync Keys</strong> in the Storage Account</span></span></td>
<td><span data-ttu-id="69d28-216">Cuando crea una cuenta de almacenamiento, se crean automáticamente una clave primaria y una clave secundaria.</span><span class="sxs-lookup"><span data-stu-id="69d28-216">When you create a Storage account, a Primary Key and Secondary Key are automatically created.</span></span> <span data-ttu-id="69d28-217">Estas claves de cifrado controlan el acceso a su cuenta de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="69d28-217">These encryption Keys control access to your Storage Account.</span></span> <span data-ttu-id="69d28-218">Su servicio de BizTalk utiliza automáticamente la clave principal.</span><span class="sxs-lookup"><span data-stu-id="69d28-218">Your BizTalk Service automatically uses the Primary Key.</span></span> <span data-ttu-id="69d28-219"><strong>Sincronizar claves</strong> permite al usuario alternar entre la clave principal y la clave secundaria sin interrumpir el servicio de BizTalk.</span><span class="sxs-lookup"><span data-stu-id="69d28-219"><strong>Sync Keys</strong> enable users to switch between the Primary Key and the Secondary Key without disrupting the BizTalk Service.</span></span>
<br/><br/>
<span data-ttu-id="69d28-220">Por ejemplo, en caso de que desee que el servicio de BizTalk use una nueva clave principal para la cuenta de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="69d28-220">For example, you want the BizTalk Service to use a new Primary Key for the Storage Account.</span></span> <span data-ttu-id="69d28-221">Para ello, siga estos pasos:</span><span class="sxs-lookup"><span data-stu-id="69d28-221">To do this:</span></span>
<br/><br/>
<ol>
<li><span data-ttu-id="69d28-222">Seleccione el servicio de BizTalk y después <strong>Sincronizar claves</strong>.</span><span class="sxs-lookup"><span data-stu-id="69d28-222">Select your BizTalk Service and select <strong>Sync Keys</strong>.</span></span> <span data-ttu-id="69d28-223">Seleccione la clave secundaria.</span><span class="sxs-lookup"><span data-stu-id="69d28-223">Select the Secondary Key.</span></span> <span data-ttu-id="69d28-224">Al hacer esto, el servicio de BizTalk se inicia usando la clave secundaria.</span><span class="sxs-lookup"><span data-stu-id="69d28-224">When you do this, the BizTalk Service starts using the Secondary Key.</span></span></li>
<li><span data-ttu-id="69d28-225">En el Portal de Azure clásico, seleccione la cuenta de almacenamiento y Regenerar la clave principal.</span><span class="sxs-lookup"><span data-stu-id="69d28-225">In the Azure classic portal, select your Storage account and Regenerate the Primary Key.</span></span> <span data-ttu-id="69d28-226">Recuerde que su servicio de BizTalk usa la clave secundaria.</span><span class="sxs-lookup"><span data-stu-id="69d28-226">Remember, your BizTalk Service is using the Secondary Key.</span></span></li>
<li><span data-ttu-id="69d28-227">Seleccione el servicio de BizTalk y después <strong>Sincronizar claves</strong>.</span><span class="sxs-lookup"><span data-stu-id="69d28-227">Select your BizTalk Service and select <strong>Sync Keys</strong>.</span></span> <span data-ttu-id="69d28-228">Ahora, seleccione la clave principal.</span><span class="sxs-lookup"><span data-stu-id="69d28-228">Now, select the Primary Key.</span></span> <span data-ttu-id="69d28-229">Esta es la nueva clave principal que ha regenerado.</span><span class="sxs-lookup"><span data-stu-id="69d28-229">This is the new Primary Key you regenerated.</span></span></li>
<li><span data-ttu-id="69d28-230">En el Portal de Azure clásico, seleccione la cuenta de almacenamiento y Regenerar la clave secundaria.</span><span class="sxs-lookup"><span data-stu-id="69d28-230">In the Azure classic portal, select your Storage account and Regenerate the Secondary Key.</span></span></li>
</ol>
<br/>
<span data-ttu-id="69d28-231">Este proceso se llama "claves de sustitución".</span><span class="sxs-lookup"><span data-stu-id="69d28-231">This process is called "rollover keys".</span></span> <span data-ttu-id="69d28-232">Su finalidad es permitir al usuario alternar entre la clave principal y la clave secundaria sin interrumpir el servicio de BizTalk.</span><span class="sxs-lookup"><span data-stu-id="69d28-232">The purpose is to enable users to switch between the Primary Key and the Secondary Key without disrupting the BizTalk Service.</span></span></td>
</tr>

<tr>
<td><span data-ttu-id="69d28-233"><strong>Eliminar</strong> la aplicación</span><span class="sxs-lookup"><span data-stu-id="69d28-233"><strong>Delete</strong> your application</span></span></td>
<td><span data-ttu-id="69d28-234">Se elimina su Servicio de BizTalk y todos los elementos implementados en él.</span><span class="sxs-lookup"><span data-stu-id="69d28-234">Your BizTalk Service and all items deployed to it are removed.</span></span></td>
</tr>
</table>


## <a name="monitor"></a><span data-ttu-id="69d28-235">Supervisión</span><span class="sxs-lookup"><span data-stu-id="69d28-235">Monitor</span></span>
<span data-ttu-id="69d28-236">No se aplica a la versión gratuita.</span><span class="sxs-lookup"><span data-stu-id="69d28-236">Does not apply to the Free Edition.</span></span>

<span data-ttu-id="69d28-237">Al seleccionar el nombre de su Servicio de BizTalk, la pestaña Supervisar se vuelve disponible y muestra lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="69d28-237">When you select your BizTalk Service name, the Monitor tab is available and displays the following:</span></span>

##### <a name="metric-graph-displays-the-selected-performance-metrics"></a><span data-ttu-id="69d28-238">Gráfico de métrica: muestra las métricas de rendimiento seleccionadas.</span><span class="sxs-lookup"><span data-stu-id="69d28-238">Metric Graph: Displays the selected performance metrics</span></span>
<span data-ttu-id="69d28-239">Estas métricas proporcionan valores en tiempo real relacionados con el estado de su servicio de BizTalk.</span><span class="sxs-lookup"><span data-stu-id="69d28-239">These metrics provide real-time values regarding the health of the BizTalk Service.</span></span> <span data-ttu-id="69d28-240">Se pueden elegir las métricas de rendimiento que mostrar.</span><span class="sxs-lookup"><span data-stu-id="69d28-240">You choose which performance metrics are displayed.</span></span> <span data-ttu-id="69d28-241">Se pueden mostrar seis métricas de rendimiento a la vez como máximo.</span><span class="sxs-lookup"><span data-stu-id="69d28-241">A maximum of six performance metrics can be displayed simultaneously.</span></span> 

<span data-ttu-id="69d28-242">También puede elegir los valores **Relativo** o **Absoluto** y el valor de **Intervalo** de las métricas que aparecen.</span><span class="sxs-lookup"><span data-stu-id="69d28-242">You can also choose the **Relative** or **Absolute** values and the time range **Interval** of the metrics that are displayed.</span></span> 

##### <a name="to-remove-or-display-metrics-in-the-graph"></a><span data-ttu-id="69d28-243">Para eliminar o mostrar métricas en el gráfico:</span><span class="sxs-lookup"><span data-stu-id="69d28-243">To remove or display metrics in the graph:</span></span>
1. <span data-ttu-id="69d28-244">Seleccione la pestaña **Monitor** .</span><span class="sxs-lookup"><span data-stu-id="69d28-244">Select the **Monitor** tab.</span></span>
2. <span data-ttu-id="69d28-245">Seleccione **Agregar métricas** en la barra de tareas:</span><span class="sxs-lookup"><span data-stu-id="69d28-245">Select **Add Metrics** in the task bar:</span></span>  
   <span data-ttu-id="69d28-246">![Seleccione Agregar métricas][AddMetrics]</span><span class="sxs-lookup"><span data-stu-id="69d28-246">![Select Add Metrics][AddMetrics]</span></span>
3. <span data-ttu-id="69d28-247">Compruebe las métricas de rendimiento que quiera mostrar.</span><span class="sxs-lookup"><span data-stu-id="69d28-247">Check the performance metrics you want to display.</span></span>
4. <span data-ttu-id="69d28-248">Seleccione la marca de verificación para volver a la pestaña **Monitor** .</span><span class="sxs-lookup"><span data-stu-id="69d28-248">Select the checkmark to return to the **Monitor** tab.</span></span>
5. <span data-ttu-id="69d28-249">Seleccione el círculo situado junto a la métrica para mostrar el valor de dicha métrica en el gráfico.</span><span class="sxs-lookup"><span data-stu-id="69d28-249">Select the circle next to the metric to display that metric's value in the graph.</span></span>  
   
    <span data-ttu-id="69d28-250">Por ejemplo, la métrica de **Uso de CPU** está atenuada; su resultado no aparece en el gráfico:</span><span class="sxs-lookup"><span data-stu-id="69d28-250">For example, the **CPU Usage** metric is grayed out; its output is not displayed in the graph:</span></span>  
   <span data-ttu-id="69d28-251">![La métrica Uso de CPU está atenuada][GrayedMetric]</span><span class="sxs-lookup"><span data-stu-id="69d28-251">![CPU Usage metric is grayed out][GrayedMetric]</span></span>  
   
    <span data-ttu-id="69d28-252">Seleccione el círculo atenuado para habilitar la métrica de **Uso de CPU** y mostrar el resultado en el gráfico:</span><span class="sxs-lookup"><span data-stu-id="69d28-252">Select the grayed out circle to enable the **CPU Usage** metric to display its output in the graph:</span></span>  
   <span data-ttu-id="69d28-253">![La métrica Uso de CPU está habilitada][EnabledMetric]</span><span class="sxs-lookup"><span data-stu-id="69d28-253">![CPU Usage metric is enabled][EnabledMetric]</span></span>
6. <span data-ttu-id="69d28-254">Para eliminar una métrica del gráfico mostrado y de la lista, seleccione **Eliminar métrica** en la barra de tareas.</span><span class="sxs-lookup"><span data-stu-id="69d28-254">To remove a metric from the display graph and the list, select **Delete Metric** in the task bar.</span></span> <span data-ttu-id="69d28-255">Si desea agregar de nuevo la métrica a la lista, haga clic en **Agregar métricas** en la barra de tareas, active la métrica y seleccione la marca de verificación para volver a la pestaña **Supervisar**.</span><span class="sxs-lookup"><span data-stu-id="69d28-255">To add the metric back to the list, select **Add Metrics** in the task bar, check the metric, and select the checkmark to return to the **Monitor** tab.</span></span> <span data-ttu-id="69d28-256">Seleccione el círculo gris para habilitar la métrica.</span><span class="sxs-lookup"><span data-stu-id="69d28-256">Select the grayed out circle to enable the metric.</span></span>

## <span data-ttu-id="69d28-257"><a name="Metrics"></a>Métricas disponibles</span><span class="sxs-lookup"><span data-stu-id="69d28-257"><a name="Metrics"></a>Available Metrics</span></span>
<span data-ttu-id="69d28-258">Están disponibles las siguientes métricas y contadores de rendimiento:</span><span class="sxs-lookup"><span data-stu-id="69d28-258">The following performance counters/metrics are available:</span></span>

<table border="1">

<tr>
<td><span data-ttu-id="69d28-259"><strong>Latencia de recorrido de ida y vuelta</strong></span><span class="sxs-lookup"><span data-stu-id="69d28-259"><strong>RountdTrip Latency</strong></span></span></td>
<td><span data-ttu-id="69d28-260">Muestra el tiempo medio en milisegundos (ms) que se tarda en procesar un mensaje desde el momento en que se recibe hasta que el Servicio de BizTalk lo procesa por completo en todos los puentes.</span><span class="sxs-lookup"><span data-stu-id="69d28-260">Displays the average time taken in milliseconds (ms) to process a message from the time the message is received until the message is fully processed by the BizTalk Service across all bridges.</span></span> <span data-ttu-id="69d28-261">Solo se cuentan los mensajes correctamente procesados.</span><span class="sxs-lookup"><span data-stu-id="69d28-261">Only messages successfully processed are counted.</span></span><br/><br/>
<span data-ttu-id="69d28-262">Cuando se producen los eventos siguientes se crea una marca de tiempo:</span><span class="sxs-lookup"><span data-stu-id="69d28-262">When the following events occur, a timestamp is created:</span></span>
<ul>
<li><span data-ttu-id="69d28-263">El mensaje entra por la puerta de enlace</span><span class="sxs-lookup"><span data-stu-id="69d28-263">Message enters the gateway</span></span></li>
<li><span data-ttu-id="69d28-264">El mensaje se envía al destino</span><span class="sxs-lookup"><span data-stu-id="69d28-264">Message is routed to the destination</span></span></li>
<li><span data-ttu-id="69d28-265">Se recibe la respuesta del destino</span><span class="sxs-lookup"><span data-stu-id="69d28-265">Destination response is received</span></span></li>
<li><span data-ttu-id="69d28-266">La respuesta de confirmación de destino se envía a la puerta de enlace</span><span class="sxs-lookup"><span data-stu-id="69d28-266">Destination acknowledgement response sent to the gateway</span></span></li>
</ul>
<br/>
<span data-ttu-id="69d28-267">Esta métrica muestra el resultado del cálculo siguiente:</span><span class="sxs-lookup"><span data-stu-id="69d28-267">This metric shows the result of the following calculation:</span></span>
<br/><br/>
<span data-ttu-id="69d28-268">[Respuesta de confirmación de destino enviada a la puerta de enlace] - [El mensaje entra por la puerta de enlace]</span><span class="sxs-lookup"><span data-stu-id="69d28-268">[Destination acknowledgement response sent to the gateway] - [Message enters the gateway]</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="69d28-269"><strong>Errores en origen</strong></span><span class="sxs-lookup"><span data-stu-id="69d28-269"><strong>Failures At Source</strong></span></span></td>
<td><span data-ttu-id="69d28-270">Muestra el número total de mensajes que el Servicio de BizTalk no pudo extraer de los extremos de origen.</span><span class="sxs-lookup"><span data-stu-id="69d28-270">Displays the total number of messages that failed by the BizTalk Service when pulling messages from the source endpoints.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="69d28-271"><strong>Uso de CPU</strong></span><span class="sxs-lookup"><span data-stu-id="69d28-271"><strong>CPU Usage</strong></span></span></td>
<td><span data-ttu-id="69d28-272">Incluye el porcentaje de tiempo medio del procesador de todas las instancias de rol.</span><span class="sxs-lookup"><span data-stu-id="69d28-272">Lists the average %Processor Time of all role instances.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="69d28-273"><strong>Latencia de procesamiento</strong></span><span class="sxs-lookup"><span data-stu-id="69d28-273"><strong>Processing Latency</strong></span></span></td>
<td><span data-ttu-id="69d28-274">Muestra el tiempo medio en milisegundos (ms) que tarda el Servicio de BizTalk en procesar un mensaje en todos los puentes, excluyendo el tiempo empleado en los destinos.</span><span class="sxs-lookup"><span data-stu-id="69d28-274">Displays the average time taken In milliseconds (ms) to process a message by the BizTalk Service across all bridges, excluding the time spent in destinations.</span></span> <span data-ttu-id="69d28-275">Solo se cuentan los mensajes correctamente procesados.</span><span class="sxs-lookup"><span data-stu-id="69d28-275">Only messages successfully processed are counted.</span></span><br/><br/>
<span data-ttu-id="69d28-276">Cuando se produce cada uno de los eventos siguientes se crea una marca de tiempo:</span><span class="sxs-lookup"><span data-stu-id="69d28-276">When each of the following events occur, a timestamp is created:</span></span>

<ul>
<li><span data-ttu-id="69d28-277">El mensaje entra por la puerta de enlace</span><span class="sxs-lookup"><span data-stu-id="69d28-277">Message enters the gateway</span></span></li>
<li><span data-ttu-id="69d28-278">El mensaje se envía al destino</span><span class="sxs-lookup"><span data-stu-id="69d28-278">Message is routed to the destination</span></span></li>
<li><span data-ttu-id="69d28-279">Se recibe la respuesta del destino</span><span class="sxs-lookup"><span data-stu-id="69d28-279">Destination response is received</span></span></li>
<li><span data-ttu-id="69d28-280">La respuesta de confirmación de destino se envía a la puerta de enlace</span><span class="sxs-lookup"><span data-stu-id="69d28-280">Destination acknowledgement response sent to the gateway</span></span></li>
</ul>
<br/><span data-ttu-id="69d28-281">Esta métrica muestra el resultado del cálculo siguiente:</span><span class="sxs-lookup"><span data-stu-id="69d28-281">This metric shows the result of the following calculation:</span></span><br/><br/>
<span data-ttu-id="69d28-282">[Respuesta de confirmación de destino enviada a la puerta de enlace] - [Mensaje que entra por la puerta de enlace] - [Se recibe la respuesta del destino] + [El mensaje se envía al destino]</span><span class="sxs-lookup"><span data-stu-id="69d28-282">[Destination acknowledgement response sent to the gateway] - [Message enters the gateway] - [Destination response is received] + [Message is routed to the destination]</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="69d28-283"><strong>Errores en proceso</strong></span><span class="sxs-lookup"><span data-stu-id="69d28-283"><strong>Failures In Process</strong></span></span></td>
<td><span data-ttu-id="69d28-284">Muestra el número total de mensajes con error durante el procesamiento del Servicio BizTalk en todos los puentes dentro de un intervalo de tiempo.</span><span class="sxs-lookup"><span data-stu-id="69d28-284">Displays the total number of messages that failed during processing by the BizTalk Service across all the bridges within a time interval.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="69d28-285"><strong>Mensajes enviados</strong></span><span class="sxs-lookup"><span data-stu-id="69d28-285"><strong>Messages Sent</strong></span></span></td>
<td><span data-ttu-id="69d28-286">Muestra el número total de mensajes enviados por el Servicio de BizTalk en todos los puentes dentro de un intervalo de tiempo.</span><span class="sxs-lookup"><span data-stu-id="69d28-286">Displays the total number of messages sent by the BizTalk Service across all bridges within a time interval.</span></span> <span data-ttu-id="69d28-287">Esta métrica se incrementa cuando un mensaje enviado desde un proceso alcanza el destino de la ruta.</span><span class="sxs-lookup"><span data-stu-id="69d28-287">This metric is incremented when a message sent from a pipeline reaches the route destination.</span></span> <span data-ttu-id="69d28-288">Esta métrica no indica el correcto procesamiento del mensaje.</span><span class="sxs-lookup"><span data-stu-id="69d28-288">This metric does not indicate that a message is successfully processed.</span></span><br/><br/>
<span data-ttu-id="69d28-289">En un escenario de respuesta de solicitud, la métrica se incrementa cuando el destino de la ruta envía una confirmación de recibo al proceso.</span><span class="sxs-lookup"><span data-stu-id="69d28-289">In a Request-Reply scenario, the metric is incremented when the route destination sends a receipt acknowledgement back to the pipeline.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="69d28-290"><strong>Mensajes recibidos</strong></span><span class="sxs-lookup"><span data-stu-id="69d28-290"><strong>Messages Received</strong></span></span></td>
<td><span data-ttu-id="69d28-291">Muestra el número total de mensajes recibidos por el Servicio de BizTalk en todos los puentes dentro de un intervalo de tiempo.</span><span class="sxs-lookup"><span data-stu-id="69d28-291">Displays the total number of messages received by the BizTalk Service across all bridges within a time interval.</span></span> <span data-ttu-id="69d28-292">Esta métrica se incrementa cuando el proceso recibe un nuevo mensaje.</span><span class="sxs-lookup"><span data-stu-id="69d28-292">This metric is incremented when a new message is received by the pipeline.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="69d28-293"><strong>Mensajes en proceso</strong></span><span class="sxs-lookup"><span data-stu-id="69d28-293"><strong>Messages In Process</strong></span></span></td>
<td><span data-ttu-id="69d28-294">Muestra el número total de mensajes que el Servicio de BizTalk está procesando actualmente dentro de un intervalo de tiempo.</span><span class="sxs-lookup"><span data-stu-id="69d28-294">Displays the total number of messages currently being processed by the BizTalk Service within a time interval.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="69d28-295"><strong>Mensajes procesados</strong></span><span class="sxs-lookup"><span data-stu-id="69d28-295"><strong>Messages Processed</strong></span></span></td>
<td><span data-ttu-id="69d28-296">Muestra el número total de mensajes procesados correctamente por el Servicio de BizTalk en todos los puentes dentro de un intervalo de tiempo.</span><span class="sxs-lookup"><span data-stu-id="69d28-296">Displays the total number of messages successfully processed by the BizTalk Service across all bridges within a time interval.</span></span> <span data-ttu-id="69d28-297">Esta métrica se incrementa cuando el proceso recibe correctamente un mensaje y lo envía al destino.</span><span class="sxs-lookup"><span data-stu-id="69d28-297">This metric is incremented when a message is successfully received by the pipeline and successfully routed to the destination.</span></span></td>
</tr>
</table>


## <a name="scale"></a><span data-ttu-id="69d28-298">Escala</span><span class="sxs-lookup"><span data-stu-id="69d28-298">Scale</span></span>
<span data-ttu-id="69d28-299">En la pestaña Escala puede sumar o restar el número de unidades usadas por su servicio de BizTalk.</span><span class="sxs-lookup"><span data-stu-id="69d28-299">In the Scale tab, you can add or subtract the number of units used by your BizTalk Service.</span></span> <span data-ttu-id="69d28-300">De forma predeterminada, hay una unidad configurada.</span><span class="sxs-lookup"><span data-stu-id="69d28-300">By default, there is one Unit configured.</span></span> <span data-ttu-id="69d28-301">Se pueden agregar unidades adicionales para escalar su servicio de BizTalk.</span><span class="sxs-lookup"><span data-stu-id="69d28-301">Additional Units can be added to scale your BizTalk Service.</span></span> <span data-ttu-id="69d28-302">Cuando se incrementa la escala, se aumenta el rendimiento.</span><span class="sxs-lookup"><span data-stu-id="69d28-302">When you increase the scale, you are increasing throughput.</span></span> <span data-ttu-id="69d28-303">La cantidad de recursos también aumenta, incluyendo los puentes implementados, los acuerdos, las conexiones de LOB y la eficacia de procesamiento.</span><span class="sxs-lookup"><span data-stu-id="69d28-303">The amount of resources also increases, including deployed bridges, agreements, LOB connections, and processing power.</span></span> <span data-ttu-id="69d28-304">Por ejemplo, si aumenta la escala de 1 unidad a 2.</span><span class="sxs-lookup"><span data-stu-id="69d28-304">For example, you increase the scale from 1 Unit to 2 Units.</span></span> <span data-ttu-id="69d28-305">En esta situación, puede implementar el doble de puentes, acuerdos, conexiones de LOB y eficacia de procesamiento.</span><span class="sxs-lookup"><span data-stu-id="69d28-305">In this situation, you can deploy double the number of bridges, double the agreements, double the LOB connections, and double the processing power.</span></span>

<span data-ttu-id="69d28-306">Algunas ediciones de BizTalk no ofrecen la opción de escala.</span><span class="sxs-lookup"><span data-stu-id="69d28-306">Some BizTalk editions do not offer a scale option.</span></span> <span data-ttu-id="69d28-307">En esta situación, se admite una unidad.</span><span class="sxs-lookup"><span data-stu-id="69d28-307">In this situation, one Unit is permitted.</span></span> <span data-ttu-id="69d28-308">A fin de determinar cuántas unidades puede escalar su edición, consulte [Servicios de BizTalk: Gráfico de ediciones](biztalk-editions-feature-chart.md).</span><span class="sxs-lookup"><span data-stu-id="69d28-308">To determine how many units your edition can be scaled, refer to [BizTalk Services: Editions Chart](biztalk-editions-feature-chart.md).</span></span>

<span data-ttu-id="69d28-309">El aumento del número de unidades podría afectar al precio.</span><span class="sxs-lookup"><span data-stu-id="69d28-309">Increasing the number of units may impact pricing.</span></span> <span data-ttu-id="69d28-310">Si aumenta las unidades, al seleccionar **Guardar** aparece un mensaje que le indica si la facturación se ve afectada.</span><span class="sxs-lookup"><span data-stu-id="69d28-310">If you increase the Units, selecting **Save** displays a message that tells you if billing is impacted.</span></span> <span data-ttu-id="69d28-311">A continuación, seleccione Continue.</span><span class="sxs-lookup"><span data-stu-id="69d28-311">You then choose to continue.</span></span> <span data-ttu-id="69d28-312">Cuando aumente el número de unidades, el estado del servicio de BizTalk cambia de Activo a Actualizando.</span><span class="sxs-lookup"><span data-stu-id="69d28-312">When you increase the number of Units, the BizTalk Service status changes from Active to Updating.</span></span> <span data-ttu-id="69d28-313">En el estado Actualizando, su servicio de BizTalk continúa ejecutándose.</span><span class="sxs-lookup"><span data-stu-id="69d28-313">In the Updating state, your BizTalk Service continues to run.</span></span>

<span data-ttu-id="69d28-314">[Servicios de BizTalk: gráfico de ediciones](biztalk-editions-feature-chart.md) define una unidad.</span><span class="sxs-lookup"><span data-stu-id="69d28-314">[BizTalk Services: Editions Chart](biztalk-editions-feature-chart.md) defines a "Unit".</span></span>

## <a name="configure"></a><span data-ttu-id="69d28-315">Configuración</span><span class="sxs-lookup"><span data-stu-id="69d28-315">Configure</span></span>
<span data-ttu-id="69d28-316">No se aplica a conexiones híbridas.</span><span class="sxs-lookup"><span data-stu-id="69d28-316">Does not apply to Hybrid Connections.</span></span>

<span data-ttu-id="69d28-317">Establezca Estado de copia de seguridad en Ninguno o Automático.</span><span class="sxs-lookup"><span data-stu-id="69d28-317">Sets the Backup Status to None or Automatic.</span></span> <span data-ttu-id="69d28-318">Cuando se establezca en Ninguno, no se creará ninguna copia de seguridad automáticamente.</span><span class="sxs-lookup"><span data-stu-id="69d28-318">When set to None, no backups are automatically created.</span></span> <span data-ttu-id="69d28-319">Cuando se establece en Automático, configure la ubicación de la copia de seguridad, la frecuencia de la misma y cuánto tiempo quiere conservar los archivos de copia de seguridad.</span><span class="sxs-lookup"><span data-stu-id="69d28-319">When set to Automatic, you configure the backup location, the frequency of the backup, and how long to keep the backup files.</span></span> 

<span data-ttu-id="69d28-320">[Servicios de BizTalk: copias de seguridad y restauración](biztalk-backup-restore.md) proporciona los detalles.</span><span class="sxs-lookup"><span data-stu-id="69d28-320">[BizTalk Services: Backup and Restore](biztalk-backup-restore.md) provides the details.</span></span> 

## <span data-ttu-id="69d28-321"><a name="HybridConnections"></a>Conexiones híbridas</span><span class="sxs-lookup"><span data-stu-id="69d28-321"><a name="HybridConnections"></a>Hybrid Connections</span></span>
<span data-ttu-id="69d28-322">Las conexiones híbridas conectan una aplicación de Azure, como Web Apps o Mobile Apps de Azure App Service, a un recurso local que usa un puerto TCP estático (por ejemplo, SQL Server, MySQL, HTTP Web API y la mayoría de los servicios web personalizados).</span><span class="sxs-lookup"><span data-stu-id="69d28-322">Hybrid Connections connect an Azure application, like Web Apps or Mobile Apps in Azure App Service, to an on-premises resource that uses a static TCP port, such as SQL Server, MySQL, HTTP Web APIs, and most custom Web Services.</span></span> <span data-ttu-id="69d28-323">Las conexiones híbridas se administran en BizTalk Services mediante el Portal de Azure clásico.</span><span class="sxs-lookup"><span data-stu-id="69d28-323">Hybrid Connections are managed in  BizTalk Services in the Azure classic portal.</span></span>

<span data-ttu-id="69d28-324">Para crear conexión híbridas en Azure App Service, consulte [Acceso a recursos locales mediante conexiones híbridas en Azure App Service](../app-service-web/web-sites-hybrid-connection-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="69d28-324">To create Hybrid Connections in Azure App Service, see [Access on-premises resources using hybrid connections in Azure App Service](../app-service-web/web-sites-hybrid-connection-get-started.md).</span></span>

<span data-ttu-id="69d28-325">Para crear o administrar conexiones híbridas en Servicios de BizTalk de Azure, consulte [Conexiones híbridas](integration-hybrid-connection-overview.md).</span><span class="sxs-lookup"><span data-stu-id="69d28-325">To create or manage Hybrid Connections in Azure BizTalk Services, see [Hybrid Connections](integration-hybrid-connection-overview.md).</span></span>

## <a name="next"></a><span data-ttu-id="69d28-326">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="69d28-326">Next</span></span>
<span data-ttu-id="69d28-327">Ahora que ya se ha familiarizado con las diferentes pestañas, puede obtener más información acerca de las características de los servicios de BizTalk de Azure:</span><span class="sxs-lookup"><span data-stu-id="69d28-327">Now that you're familiar with the different tabs, you can learn more about the Azure BizTalk Services features:</span></span>

* [<span data-ttu-id="69d28-328">Servicios de BizTalk: limitaciones</span><span class="sxs-lookup"><span data-stu-id="69d28-328">BizTalk Services: Throttling</span></span>](biztalk-throttling-thresholds.md)  
* [<span data-ttu-id="69d28-329">Servicios de BizTalk: nombre del emisor y clave del emisor</span><span class="sxs-lookup"><span data-stu-id="69d28-329">BizTalk Services: Issuer Name and Issuer Key</span></span>](biztalk-issuer-name-issuer-key.md)  
* [<span data-ttu-id="69d28-330">Servicios de BizTalk: copias de seguridad y restauración</span><span class="sxs-lookup"><span data-stu-id="69d28-330">BizTalk Services: Backup and Restore</span></span>](biztalk-backup-restore.md)

## <a name="see-also"></a><span data-ttu-id="69d28-331">Otras referencias</span><span class="sxs-lookup"><span data-stu-id="69d28-331">See Also</span></span>
* [<span data-ttu-id="69d28-332">Conexiones híbridas</span><span class="sxs-lookup"><span data-stu-id="69d28-332">Hybrid Connections</span></span>](integration-hybrid-connection-overview.md)  
* [<span data-ttu-id="69d28-333">Servicios de BizTalk: gráfico de las ediciones Developer, Basic, Standard y Premium</span><span class="sxs-lookup"><span data-stu-id="69d28-333">BizTalk Services: Developer, Basic, Standard and Premium Editions Chart</span></span>](biztalk-editions-feature-chart.md)  
* [<span data-ttu-id="69d28-334">Servicios de BizTalk: aprovisionamiento con el Portal de Azure clásico</span><span class="sxs-lookup"><span data-stu-id="69d28-334">BizTalk Services: Provisioning Using Azure classic portal</span></span>](biztalk-provision-services.md)  
* [<span data-ttu-id="69d28-335">Servicios de BizTalk: gráfico de estado del servicio de BizTalk</span><span class="sxs-lookup"><span data-stu-id="69d28-335">BizTalk Services: BizTalk Service State Chart</span></span>](biztalk-service-state-chart.md)  
* [<span data-ttu-id="69d28-336">¿Cómo puedo comenzar a utilizar el SDK de Servicios de BizTalk de Azure?</span><span class="sxs-lookup"><span data-stu-id="69d28-336">How do I Start Using the Azure BizTalk Services SDK</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=302335)

[Quickstart]: ./media/biztalk-dashboard-monitor-scale-tabs/QuickStartIcon.png
[AddMetrics]: ./media/biztalk-dashboard-monitor-scale-tabs/WABS_AddMetrics.png
[GrayedMetric]: ./media/biztalk-dashboard-monitor-scale-tabs/WABS_GrayedMetric.png
[EnabledMetric]: ./media/biztalk-dashboard-monitor-scale-tabs/WABS_EnabledMetric.png

