---
title: "aaaDashboard, Monitor, escala, configurar y las conexiones híbridas en servicios de BizTalk | Documentos de Microsoft"
description: "Obtenga información acerca de los controles de Hola y supervisar el rendimiento en las pestañas de portal clásico de hello de servicios de BizTalk: panel, Monitor, escala, configurar y las conexiones híbridas. MABS, WABS"
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
ms.openlocfilehash: c9fafdad20489571ee3849bbacd2c2b10933154f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="review-hello-dashboard-monitor-scale-configure-and-hybrid-connection-tabs"></a><span data-ttu-id="b4b1a-104">Revise las pestañas de panel, Monitor, escala, configurar y conexión híbrida de Hola</span><span class="sxs-lookup"><span data-stu-id="b4b1a-104">Review hello Dashboard, Monitor, Scale, Configure, and Hybrid Connection tabs</span></span>

> [!INCLUDE [BizTalk Services is being retired, and replaced with Azure Logic Apps](../../includes/biztalk-services-retirement.md)]

<span data-ttu-id="b4b1a-105">Después de crear su BizTalk Service e implementar la aplicación, puede cambiar parte de configuración de servicio de BizTalk de Hola y supervisar el rendimiento de la aplicación hello.</span><span class="sxs-lookup"><span data-stu-id="b4b1a-105">After you create your BizTalk Service and deploy your application, you can change some of hello BizTalk Service settings and monitor hello application performance.</span></span> 

<span data-ttu-id="b4b1a-106">Cuando se abre Hola portal de Azure clásico, se colocan automáticamente en hello **todos los elementos** tooview de pestaña. su BizTalk Service, seleccione su BizTalk Service en hello **todos los elementos** tab o seleccione hello **Servicios de BIZTALK** pestaña; y, a continuación, seleccione el nombre de BizTalk Service.</span><span class="sxs-lookup"><span data-stu-id="b4b1a-106">When you open hello Azure classic portal, you are automatically placed at hello **ALL ITEMS** tab. tooview your BizTalk Service, select your BizTalk Service in hello **ALL ITEMS** tab or select hello **BIZTALK SERVICES** tab; and then select your BizTalk Service name.</span></span>

<span data-ttu-id="b4b1a-107">Se abrirá una nueva ventana con hello después de pestañas.</span><span class="sxs-lookup"><span data-stu-id="b4b1a-107">This opens a new window with hello following tabs.</span></span> <span data-ttu-id="b4b1a-108">En el tema se describen estas pestañas.</span><span class="sxs-lookup"><span data-stu-id="b4b1a-108">This topic describes these tabs.</span></span>

## <a name="quickstart-quickstartquickstart"></a><span data-ttu-id="b4b1a-109">Guía de inicio rápido</span><span class="sxs-lookup"><span data-stu-id="b4b1a-109">Quickstart (</span></span>![Guía de inicio rápido][Quickstart]<span data-ttu-id="b4b1a-111">)</span><span class="sxs-lookup"><span data-stu-id="b4b1a-111">)</span></span>
<span data-ttu-id="b4b1a-112">Función hello BizTalk Services Edition, todas las opciones enumeradas no estén disponibles.</span><span class="sxs-lookup"><span data-stu-id="b4b1a-112">Depending on hello BizTalk Services Edition, all options listed may not be available.</span></span> 

<table border="1">
    <tr>
        <td><span data-ttu-id="b4b1a-113"><strong>Obtener herramientas de Hola</strong></span><span class="sxs-lookup"><span data-stu-id="b4b1a-113"><strong>Get hello tools</strong></span></span></td>
        <td><span data-ttu-id="b4b1a-114">Descargar plantillas de proyecto de Visual Studio hello tooinstall de SDK de servicios de BizTalk hello en el equipo de desarrollo local.</span><span class="sxs-lookup"><span data-stu-id="b4b1a-114">Download hello BizTalk Services SDK tooinstall hello Visual Studio project templates on your on-premises development computer.</span></span> <span data-ttu-id="b4b1a-115">Estas plantillas crean hello <strong>servicios de BizTalk</strong> (puente) hello y <strong>artefactos de servicios de BizTalk</strong> proyectos de Visual Studio de (transformación) que están implementado tooyour BizTalk Service.</span><span class="sxs-lookup"><span data-stu-id="b4b1a-115">These templates create hello <strong>BizTalk Services</strong> (bridge) and hello <strong>BizTalk Service Artifacts</strong> (Transform) Visual Studio projects that are deployed tooyour BizTalk Service.</span></span>
        <br/><br/><span data-ttu-id="b4b1a-116">
        <a HREF="http://go.microsoft.com/fwlink/p/?LinkID=302335">¿Cómo puedo comenzar a utilizar Hola SDK de servicios de BizTalk de Azure </a> y <a HREF="http://go.microsoft.com/fwlink/p/?LinkID=241589">Hola instalar SDK de servicios de BizTalk de Azure</a> listas Hola tooget de pasos que se inició.</span><span class="sxs-lookup"><span data-stu-id="b4b1a-116">
        <a HREF="http://go.microsoft.com/fwlink/p/?LinkID=302335"> How do I Start Using hello Azure BizTalk Services SDK </a> and <a HREF="http://go.microsoft.com/fwlink/p/?LinkID=241589">Installing hello Azure BizTalk Services SDK</a> lists hello steps tooget started.</span></span>
        </td>
    </tr>
    <tr>
        <td><span data-ttu-id="b4b1a-117"><strong>Crear acuerdos de asociados comerciales</strong></span><span class="sxs-lookup"><span data-stu-id="b4b1a-117"><strong>Create partner agreements</strong></span></span></td>
        <td><span data-ttu-id="b4b1a-118">Se abre Hola Portal de servicios de BizTalk de Azure hospedado en Azure donde agregar asociados y crear X12, AS2 y acuerdos EDIFACT EDI.</span><span class="sxs-lookup"><span data-stu-id="b4b1a-118">Opens hello Azure BizTalk Services Portal hosted on Azure where you add partners and create X12, AS2, and EDIFACT EDI agreements.</span></span>
        <br/><br/><span data-ttu-id="b4b1a-119">
        <a HREF="http://go.microsoft.com/fwlink/p/?LinkID=303653">Configurar componentes de mensajería de EDI en BizTalk Services Portal</a> listas Hola tooget de pasos que se inició.</span><span class="sxs-lookup"><span data-stu-id="b4b1a-119">
        <a HREF="http://go.microsoft.com/fwlink/p/?LinkID=303653">Configuring Components for EDI Messaging on BizTalk Services Portal</a> lists hello steps tooget started.</span></span>
        </td>
    </tr>

<tr>
        <td><span data-ttu-id="b4b1a-120"><strong>Más información sobre BizTalk Services</strong></span><span class="sxs-lookup"><span data-stu-id="b4b1a-120"><strong>Learn more about BizTalk Services</strong></span></span></td>
        <td><span data-ttu-id="b4b1a-121">Vaya toohello <a HREF="http://azure.microsoft.com/documentation/services/biztalk-services/">centro de aprendizaje</a> toolearn más información acerca de los servicios de BizTalk de Azure.</span><span class="sxs-lookup"><span data-stu-id="b4b1a-121">Go toohello <a HREF="http://azure.microsoft.com/documentation/services/biztalk-services/">learning center</a> toolearn more about Azure BizTalk Services.</span></span></td>
</tr>
</table>


<span data-ttu-id="b4b1a-122">En la barra de tareas de hello en parte inferior de hello, puede:</span><span class="sxs-lookup"><span data-stu-id="b4b1a-122">In hello task bar at hello bottom, you can:</span></span>

<table border="1">

<tr>
<td><span data-ttu-id="b4b1a-123"><strong>Administrar</strong> la implementación de la aplicación</span><span class="sxs-lookup"><span data-stu-id="b4b1a-123"><strong>Manage</strong> your application deployment</span></span></td>
<td><span data-ttu-id="b4b1a-124">Abre el portal de servicios de BizTalk de Azure de Hola.</span><span class="sxs-lookup"><span data-stu-id="b4b1a-124">Opens hello Azure BizTalk Services portal.</span></span> <span data-ttu-id="b4b1a-125">Hola Portal de servicios de BizTalk es la configuración de tooEDI de entrada de hello, incluida la adición de asociados y crear X12, AS2 y acuerdos EDIFACT.</span><span class="sxs-lookup"><span data-stu-id="b4b1a-125">hello BizTalk Services Portal is hello entrance tooEDI configuration, including adding partners and creating X12, AS2, and EDIFACT agreements.</span></span>
<br/><br/>
<span data-ttu-id="b4b1a-126">Esto es Hola igual <strong>crear acuerdos entre socios</strong> en hello <strong>inicio rápido</strong> ficha.</span><span class="sxs-lookup"><span data-stu-id="b4b1a-126">This is hello same as <strong>Create partner agreements</strong> on hello <strong>Quick Start</strong> tab.</span></span>
<br/><br/><span data-ttu-id="b4b1a-127">
<a HREF="http://go.microsoft.com/fwlink/p/?LinkID=303653">Configurar componentes de mensajería de EDI en BizTalk Services Portal</a> proporciona más información sobre Hola Portal de servicios de BizTalk.</span><span class="sxs-lookup"><span data-stu-id="b4b1a-127">
<a HREF="http://go.microsoft.com/fwlink/p/?LinkID=303653">Configuring Components for EDI Messaging on BizTalk Services Portal</a> provides more information on hello BizTalk Services Portal.</span></span></td>
</tr>

<tr>
<td><span data-ttu-id="b4b1a-128"><strong>Información de conexión</strong> de hello Namespace de Control de acceso</span><span class="sxs-lookup"><span data-stu-id="b4b1a-128"><strong>Connection Information</strong> of hello Access Control Namespace</span></span></td>
<td><span data-ttu-id="b4b1a-129">Cuando se selecciona información de conexión, a continuación, Hola Namespace de Control de acceso, emisor predeterminado, y se muestran clave predeterminada.</span><span class="sxs-lookup"><span data-stu-id="b4b1a-129">When you select Connection Information, then hello Access Control Namespace, Default Issuer, and Default Key are displayed.</span></span> <span data-ttu-id="b4b1a-130">Estos valores se pueden copiar.</span><span class="sxs-lookup"><span data-stu-id="b4b1a-130">You can copy these values.</span></span>
<br/><br/>
<span data-ttu-id="b4b1a-131">También puede abrir Hola Portal de Control de acceso.</span><span class="sxs-lookup"><span data-stu-id="b4b1a-131">You can also open hello Access Control Portal.</span></span> <span data-ttu-id="b4b1a-132"><a HREF="http://go.microsoft.com/fwlink/p/?LinkID=285670">Crear un control de acceso Namespace</a> proporciona más información sobre Hola Portal de Control de acceso.</span><span class="sxs-lookup"><span data-stu-id="b4b1a-132"><a HREF="http://go.microsoft.com/fwlink/p/?LinkID=285670">Create an Access control Namespace</a> provides more information on hello Access Control Portal.</span></span></td>
</tr>

<tr>
<td><span data-ttu-id="b4b1a-133"><strong>Sincronizar las claves</strong> Hola cuenta de almacenamiento</span><span class="sxs-lookup"><span data-stu-id="b4b1a-133"><strong>Sync Keys</strong> in hello Storage Account</span></span></td>
<td><span data-ttu-id="b4b1a-134">Cuando crea una cuenta de almacenamiento, se crean automáticamente una clave primaria y una clave secundaria.</span><span class="sxs-lookup"><span data-stu-id="b4b1a-134">When you create a Storage account, a Primary Key and Secondary Key are automatically created.</span></span> <span data-ttu-id="b4b1a-135">Estas claves de cifrado controlan acceso tooyour cuenta de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="b4b1a-135">These encryption Keys control access tooyour Storage Account.</span></span> <span data-ttu-id="b4b1a-136">Su BizTalk Service usa automáticamente Hola Primary Key.</span><span class="sxs-lookup"><span data-stu-id="b4b1a-136">Your BizTalk Service automatically uses hello Primary Key.</span></span> <span data-ttu-id="b4b1a-137"><strong>Sincronizar las claves</strong> habilitar usuarios tooswitch entre clave principal de Hola y Hola clave secundaria sin interrumpir Hola BizTalk Service.</span><span class="sxs-lookup"><span data-stu-id="b4b1a-137"><strong>Sync Keys</strong> enable users tooswitch between hello Primary Key and hello Secondary Key without disrupting hello BizTalk Service.</span></span>
<br/><br/>
<span data-ttu-id="b4b1a-138">Por ejemplo, desea Hola BizTalk Service toouse una nueva clave principal para hello cuenta de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="b4b1a-138">For example, you want hello BizTalk Service toouse a new Primary Key for hello Storage Account.</span></span> <span data-ttu-id="b4b1a-139">toodo esto:</span><span class="sxs-lookup"><span data-stu-id="b4b1a-139">toodo this:</span></span>
<br/><br/>
<ol>
<li><span data-ttu-id="b4b1a-140">Seleccione el servicio de BizTalk y después <strong>Sincronizar claves</strong>.</span><span class="sxs-lookup"><span data-stu-id="b4b1a-140">Select your BizTalk Service and select <strong>Sync Keys</strong>.</span></span> <span data-ttu-id="b4b1a-141">Seleccione Hola clave secundaria.</span><span class="sxs-lookup"><span data-stu-id="b4b1a-141">Select hello Secondary Key.</span></span> <span data-ttu-id="b4b1a-142">Al hacerlo, Hola BizTalk Service inicia utilizando Hola clave secundaria.</span><span class="sxs-lookup"><span data-stu-id="b4b1a-142">When you do this, hello BizTalk Service starts using hello Secondary Key.</span></span></li>
<li><span data-ttu-id="b4b1a-143">Hola portal de Azure clásico, seleccione la cuenta de almacenamiento y volver a generar Hola Primary Key.</span><span class="sxs-lookup"><span data-stu-id="b4b1a-143">In hello Azure classic portal, select your Storage account and Regenerate hello Primary Key.</span></span> <span data-ttu-id="b4b1a-144">Recuerde que su BizTalk Service está usando Hola clave secundaria.</span><span class="sxs-lookup"><span data-stu-id="b4b1a-144">Remember, your BizTalk Service is using hello Secondary Key.</span></span></li>
<li><span data-ttu-id="b4b1a-145">Seleccione el servicio de BizTalk y después <strong>Sincronizar claves</strong>.</span><span class="sxs-lookup"><span data-stu-id="b4b1a-145">Select your BizTalk Service and select <strong>Sync Keys</strong>.</span></span> <span data-ttu-id="b4b1a-146">Ahora, seleccione Hola Primary Key.</span><span class="sxs-lookup"><span data-stu-id="b4b1a-146">Now, select hello Primary Key.</span></span> <span data-ttu-id="b4b1a-147">Esto es Hola nueva clave principal vuelve a generar.</span><span class="sxs-lookup"><span data-stu-id="b4b1a-147">This is hello new Primary Key you regenerated.</span></span></li>
<li><span data-ttu-id="b4b1a-148">Hola portal de Azure clásico, seleccione la cuenta de almacenamiento y volver a generar Hola clave secundaria.</span><span class="sxs-lookup"><span data-stu-id="b4b1a-148">In hello Azure classic portal, select your Storage account and Regenerate hello Secondary Key.</span></span></li>
</ol>
<br/>
<span data-ttu-id="b4b1a-149">Este proceso se llama "claves de sustitución".</span><span class="sxs-lookup"><span data-stu-id="b4b1a-149">This process is called "rollover keys".</span></span> <span data-ttu-id="b4b1a-150">Hola sirve tooenable usuarios tooswitch entre clave principal de Hola y Hola clave secundaria sin interrumpir Hola BizTalk Service.</span><span class="sxs-lookup"><span data-stu-id="b4b1a-150">hello purpose is tooenable users tooswitch between hello Primary Key and hello Secondary Key without disrupting hello BizTalk Service.</span></span></td>
</tr>

<tr>
<td><span data-ttu-id="b4b1a-151"><strong>Eliminar</strong> la aplicación</span><span class="sxs-lookup"><span data-stu-id="b4b1a-151"><strong>Delete</strong> your application</span></span></td>
<td><span data-ttu-id="b4b1a-152">Cuando se selecciona eliminar su BizTalk Service y se quitan tooit de todos los elementos implementados.</span><span class="sxs-lookup"><span data-stu-id="b4b1a-152">When you select Delete, your BizTalk Service and all items deployed tooit are removed.</span></span></td>
</tr>
</table>


## <a name="dashboard"></a><span data-ttu-id="b4b1a-153">Panel</span><span class="sxs-lookup"><span data-stu-id="b4b1a-153">Dashboard</span></span>
<span data-ttu-id="b4b1a-154">Función hello BizTalk Services Edition, todas las opciones enumeradas no estén disponibles.</span><span class="sxs-lookup"><span data-stu-id="b4b1a-154">Depending on hello BizTalk Services Edition, all options listed may not be available.</span></span> 

<span data-ttu-id="b4b1a-155">Cuando se selecciona el nombre de BizTalk Service, se muestra la pestaña panel Hola.</span><span class="sxs-lookup"><span data-stu-id="b4b1a-155">When you select your BizTalk Service name, hello Dashboard tab is displayed.</span></span> <span data-ttu-id="b4b1a-156">En el Panel, existen las siguientes opciones:</span><span class="sxs-lookup"><span data-stu-id="b4b1a-156">In Dashboard, you can:</span></span>

##### <a name="usage-overview-shows-hello-number-of-used-hybrid-connections"></a><span data-ttu-id="b4b1a-157">Información general del uso: Muestra el número de Hola de conexiones híbridas usadas</span><span class="sxs-lookup"><span data-stu-id="b4b1a-157">Usage Overview: Shows hello number of used Hybrid Connections</span></span>
<span data-ttu-id="b4b1a-158">También muestra el uso de datos de hello en GB.</span><span class="sxs-lookup"><span data-stu-id="b4b1a-158">Also displays hello data usage in GB.</span></span> 

##### <a name="metric-graph-shows-a-fixed-list-of-performance-metrics"></a><span data-ttu-id="b4b1a-159">Gráfico de métrica: muestra una lista fija de métricas de rendimiento</span><span class="sxs-lookup"><span data-stu-id="b4b1a-159">Metric Graph: Shows a fixed list of performance metrics</span></span>
<span data-ttu-id="b4b1a-160">Estas métricas proporcionan valores en tiempo real con respecto a mantenimiento Hola de hello BizTalk Service.</span><span class="sxs-lookup"><span data-stu-id="b4b1a-160">These metrics provide real-time values regarding hello health of hello BizTalk Service.</span></span> <span data-ttu-id="b4b1a-161">También puede elegir hello **relativa** o **absoluta** hello y valores de intervalo de tiempo **intervalo** de métricas de Hola que se muestran en el gráfico de Hola.</span><span class="sxs-lookup"><span data-stu-id="b4b1a-161">You can also choose hello **Relative** or **Absolute** values and hello time range **Interval** of hello metrics that are displayed in hello graph.</span></span> 

<span data-ttu-id="b4b1a-162">Para obtener una descripción de estas métricas de rendimiento, vaya demasiado[métricas disponibles](#Metrics) en este tema.</span><span class="sxs-lookup"><span data-stu-id="b4b1a-162">For a description of these performance metrics, go too[Available Metrics](#Metrics) in this topic.</span></span>

##### <a name="quick-glance-lists-your-biztalk-service-properties"></a><span data-ttu-id="b4b1a-163">Vista rápida: muestra las propiedades del servicio de BizTalk</span><span class="sxs-lookup"><span data-stu-id="b4b1a-163">Quick Glance: Lists your BizTalk Service properties</span></span>
<table border="1">

<tr>
<td><span data-ttu-id="b4b1a-164"><strong>Actualizar credenciales de la base de datos de seguimiento</strong></span><span class="sxs-lookup"><span data-stu-id="b4b1a-164"><strong>Update Tracking Database credentials</strong></span></span></td>
<td><span data-ttu-id="b4b1a-165">Hola de cambios de nombre de usuario y contraseña utilizados toolog en hello base de datos de seguimiento.</span><span class="sxs-lookup"><span data-stu-id="b4b1a-165">Changes hello user name and password used toolog into hello Tracking Database.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="b4b1a-166"><strong>Actualizar certificado SSL</strong></span><span class="sxs-lookup"><span data-stu-id="b4b1a-166"><strong>Update SSL Certificate</strong></span></span></td>
<td><span data-ttu-id="b4b1a-167">Puede actualizar Hola BizTalk Service toouse un certificado SSL diferente.</span><span class="sxs-lookup"><span data-stu-id="b4b1a-167">Can update hello BizTalk Service toouse a different SSL certificate.</span></span> <span data-ttu-id="b4b1a-168">Automáticamente se crea un certificado SSL autofirmado cuando se <a HREF="http://go.microsoft.com/fwlink/p/?LinkID=302280">crear hello BizTalk Service</a>.</span><span class="sxs-lookup"><span data-stu-id="b4b1a-168">A self-signed SSL certificate is automatically created when you <a HREF="http://go.microsoft.com/fwlink/p/?LinkID=302280">create hello BizTalk Service</a>.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="b4b1a-169"><strong>Descarga del certificado</strong></span><span class="sxs-lookup"><span data-stu-id="b4b1a-169"><strong>Download Certificate</strong></span></span></td>
<td><span data-ttu-id="b4b1a-170">Puede descargar el certificado SSL de hello usado por el equipo local de BizTalk Service tooa.</span><span class="sxs-lookup"><span data-stu-id="b4b1a-170">You can download hello SSL certificate used by your BizTalk Service tooa local machine.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="b4b1a-171"><strong>Estado</strong></span><span class="sxs-lookup"><span data-stu-id="b4b1a-171"><strong>Status</strong></span></span></td>
<td><span data-ttu-id="b4b1a-172">Muestra el estado actual de Hola de su BizTalk Service.</span><span class="sxs-lookup"><span data-stu-id="b4b1a-172">Displays hello current status of your BizTalk Service.</span></span> <span data-ttu-id="b4b1a-173">Consulte <a HREF="http://go.microsoft.com/fwlink/p/?LinkID=329870">BizTalk Services: gráfico del estado del servicio de BizTalk</a>.</span><span class="sxs-lookup"><span data-stu-id="b4b1a-173">See <a HREF="http://go.microsoft.com/fwlink/p/?LinkID=329870">BizTalk Services: Service state chart</a>.</span></span> </td>
</tr>
<tr>
<td><span data-ttu-id="b4b1a-174"><strong>URL de servicio</strong></span><span class="sxs-lookup"><span data-stu-id="b4b1a-174"><strong>Service URL</strong></span></span></td>
<td><span data-ttu-id="b4b1a-175">dirección URL de Hola para su BizTalk Service.</span><span class="sxs-lookup"><span data-stu-id="b4b1a-175">hello URL for your BizTalk Service.</span></span> <span data-ttu-id="b4b1a-176">Esto mismo es Hola como hello <strong>dirección URL del dominio</strong> especificado cuando se crea el BizTalk Service.</span><span class="sxs-lookup"><span data-stu-id="b4b1a-176">This is hello same as hello <strong>Domain URL</strong> entered when your BizTalk Service is created.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="b4b1a-177"><strong>Dirección IP virtual (VIP) pública</strong></span><span class="sxs-lookup"><span data-stu-id="b4b1a-177"><strong>Public Virtual IP (VIP) Address</strong></span></span></td>
<td><span data-ttu-id="b4b1a-178">dirección IP de Hello asignado tooyour BizTalk Service.</span><span class="sxs-lookup"><span data-stu-id="b4b1a-178">hello IP address assigned tooyour BizTalk Service.</span></span> <span data-ttu-id="b4b1a-179">Se utiliza para todos los extremos de entrada y es la dirección de origen de hello para el tráfico saliente.</span><span class="sxs-lookup"><span data-stu-id="b4b1a-179">It is used for all input endpoints and is hello source address for outbound traffic.</span></span> <span data-ttu-id="b4b1a-180">Esta dirección IP pertenece tooyour BizTalk Service siempre y cuando se crea.</span><span class="sxs-lookup"><span data-stu-id="b4b1a-180">This IP address belongs tooyour BizTalk Service as long as it is created.</span></span> <span data-ttu-id="b4b1a-181">Si elimina Hola BizTalk Service, se asigna a dirección IP de hello tooanother BizTalk Service.</span><span class="sxs-lookup"><span data-stu-id="b4b1a-181">If you delete hello BizTalk Service, hello IP address is assigned tooanother BizTalk Service.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="b4b1a-182"><strong>ACS Namespace</strong></span><span class="sxs-lookup"><span data-stu-id="b4b1a-182"><strong>ACS Namespace</strong></span></span></td>
<td><span data-ttu-id="b4b1a-183">Se autentica con hello BizTalk Service.</span><span class="sxs-lookup"><span data-stu-id="b4b1a-183">Authenticates with hello BizTalk Service.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="b4b1a-184"><strong>Edición</strong></span><span class="sxs-lookup"><span data-stu-id="b4b1a-184"><strong>Edition</strong></span></span></td>
<td><span data-ttu-id="b4b1a-185">Hola que Edition especificado cuando se crea Hola BizTalk Service se enumeran.</span><span class="sxs-lookup"><span data-stu-id="b4b1a-185">Lists hello Edition entered when hello BizTalk Service is created.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="b4b1a-186"><strong>Ubicación</strong></span><span class="sxs-lookup"><span data-stu-id="b4b1a-186"><strong>Location</strong></span></span></td>
<td><span data-ttu-id="b4b1a-187">Muestra Hola región geográfica que hospeda su BizTalk Service.</span><span class="sxs-lookup"><span data-stu-id="b4b1a-187">Displays hello geographic region that hosts your BizTalk Service.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="b4b1a-188"><strong>Created</strong></span><span class="sxs-lookup"><span data-stu-id="b4b1a-188"><strong>Created</strong></span></span></td>
<td><span data-ttu-id="b4b1a-189">Hola de fecha y hora de hello muestra BizTalk Service se creó.</span><span class="sxs-lookup"><span data-stu-id="b4b1a-189">Displays hello date and time hello BizTalk Service was created.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="b4b1a-190"><strong>Tracking Database</strong></span><span class="sxs-lookup"><span data-stu-id="b4b1a-190"><strong>Tracking Database</strong></span></span></td>
<td><span data-ttu-id="b4b1a-191">nombre de base de datos de SQL Azure de Hola que almacena Hola utilizadas por su BizTalk Service de tablas de seguimiento.</span><span class="sxs-lookup"><span data-stu-id="b4b1a-191">hello Azure SQL Database name that stores hello tracking tables used by your BizTalk Service.</span></span> 
<br/><br/><span data-ttu-id="b4b1a-192">
<a HREF="http://go.microsoft.com/fwlink/p/?LinkID=302280">Requisitos sobre</a> proporciona información detallada sobre Hola base de datos de seguimiento.</span><span class="sxs-lookup"><span data-stu-id="b4b1a-192">
<a HREF="http://go.microsoft.com/fwlink/p/?LinkID=302280">Requirements Explained</a>  provides details on hello Tracking Database.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="b4b1a-193"><strong>Monitoring/Archiving Storage</strong></span><span class="sxs-lookup"><span data-stu-id="b4b1a-193"><strong>Monitoring/Archiving Storage</strong></span></span></td>
<td><span data-ttu-id="b4b1a-194">nombre de la cuenta de almacenamiento de Azure Hola que almacena Hola supervisando los resultados de su BizTalk Service.</span><span class="sxs-lookup"><span data-stu-id="b4b1a-194">hello Azure Storage account name that stores hello monitoring output of your BizTalk Service.</span></span>
<br/><br/><span data-ttu-id="b4b1a-195">
<a HREF="http://go.microsoft.com/fwlink/p/?LinkID=302280">Requisitos sobre</a> proporciona información detallada sobre Hola cuenta de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="b4b1a-195">
<a HREF="http://go.microsoft.com/fwlink/p/?LinkID=302280">Requirements Explained</a>  provides details on hello Storage account.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="b4b1a-196"><strong>Subscription Name</strong></span><span class="sxs-lookup"><span data-stu-id="b4b1a-196"><strong>Subscription Name</strong></span></span></td>
<td><span data-ttu-id="b4b1a-197">Suscripción de Hola que hospeda su BizTalk Service se enumeran.</span><span class="sxs-lookup"><span data-stu-id="b4b1a-197">Lists hello subscription that hosts your BizTalk Service.</span></span> <span data-ttu-id="b4b1a-198">suscripción de Hello rige acceso toohello portal de Azure clásico.</span><span class="sxs-lookup"><span data-stu-id="b4b1a-198">hello subscription governs access toohello Azure classic portal.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="b4b1a-199"><strong>Subscription ID</strong></span><span class="sxs-lookup"><span data-stu-id="b4b1a-199"><strong>Subscription ID</strong></span></span></td>
<td><span data-ttu-id="b4b1a-200">Cuando se crea una suscripción, se genera automáticamente un identificador de suscripción.</span><span class="sxs-lookup"><span data-stu-id="b4b1a-200">When a subscription is created, a subscription ID is automatically generated.</span></span> <span data-ttu-id="b4b1a-201">Al utilizar las API de REST, puede que necesite hello tooenter identificador de suscripción.</span><span class="sxs-lookup"><span data-stu-id="b4b1a-201">When using REST APIs, you may need tooenter hello Subscription ID.</span></span></td>
</tr>
</table>

<span data-ttu-id="b4b1a-202">[Servicios de BizTalk: Aprovisionamiento portal clásico con Azure](http://go.microsoft.com/fwlink/p/?LinkID=302280) listas Hola pasos toocreate un BizTalk Service.</span><span class="sxs-lookup"><span data-stu-id="b4b1a-202">[BizTalk Services: Provisioning Using Azure classic portal](http://go.microsoft.com/fwlink/p/?LinkID=302280) lists hello steps toocreate a BizTalk Service.</span></span>

##### <a name="manage-connection-information-sync-keys-and-delete-in-hello-task-bar"></a><span data-ttu-id="b4b1a-203">Administrar información de conexión, las claves de la sincronización y eliminar en la barra de tareas de hello:</span><span class="sxs-lookup"><span data-stu-id="b4b1a-203">Manage, Connection Information, Sync Keys, and Delete in hello task bar:</span></span>
<table border="1">

<tr>
<td><span data-ttu-id="b4b1a-204"><strong>Administrar</strong> la implementación de la aplicación</span><span class="sxs-lookup"><span data-stu-id="b4b1a-204"><strong>Manage</strong> your application deployment</span></span></td>
<td><span data-ttu-id="b4b1a-205">Se abre el Hola Portal de servicios de BizTalk de Azure.</span><span class="sxs-lookup"><span data-stu-id="b4b1a-205">Opens hello Azure BizTalk Services Portal.</span></span> <span data-ttu-id="b4b1a-206">Hola Portal de servicios de BizTalk es la configuración de tooEDI de entrada de hello, incluida la adición de asociados y crear X12, AS2 y acuerdos EDIFACT.</span><span class="sxs-lookup"><span data-stu-id="b4b1a-206">hello BizTalk Services Portal is hello entrance tooEDI configuration, including adding partners and creating X12, AS2, and EDIFACT agreements.</span></span>
<br/><br/>
<span data-ttu-id="b4b1a-207">Esto es Hola igual <strong>crear acuerdos entre socios</strong> en hello <strong>inicio rápido</strong> ficha.</span><span class="sxs-lookup"><span data-stu-id="b4b1a-207">This is hello same as <strong>Create partner agreements</strong> on hello <strong>Quick Start</strong> tab.</span></span>
<br/><br/><span data-ttu-id="b4b1a-208">
<a HREF="http://go.microsoft.com/fwlink/p/?LinkID=303653">Configurar componentes de mensajería de EDI en BizTalk Services Portal</a> proporciona más información sobre Hola Portal de servicios de BizTalk.</span><span class="sxs-lookup"><span data-stu-id="b4b1a-208">
<a HREF="http://go.microsoft.com/fwlink/p/?LinkID=303653">Configuring Components for EDI Messaging on BizTalk Services Portal</a> provides more information on hello BizTalk Services Portal.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="b4b1a-209"><strong>Información de conexión</strong> de hello Namespace de Control de acceso</span><span class="sxs-lookup"><span data-stu-id="b4b1a-209"><strong>Connection Information</strong> of hello Access Control Namespace</span></span></td>
<td><span data-ttu-id="b4b1a-210">Muestra Hola Namespace de Control de acceso, emisor predeterminado y valores de clave predeterminada; que se pueden copiar.</span><span class="sxs-lookup"><span data-stu-id="b4b1a-210">Displays hello Access Control Namespace, Default Issuer, and Default Key values; which can be copied.</span></span>
<br/><br/>
<span data-ttu-id="b4b1a-211">También puede abrir Hola Portal de Control de acceso.</span><span class="sxs-lookup"><span data-stu-id="b4b1a-211">You can also open hello Access Control Portal.</span></span> <span data-ttu-id="b4b1a-212">Este Portal de Control de acceso es Hola igual que con la opción de Active Directory de hello en el panel de navegación izquierdo de Hola.</span><span class="sxs-lookup"><span data-stu-id="b4b1a-212">This Access Control Portal is hello same as using hello Active Directory option in hello left navigation pane.</span></span>
<br/><br/><span data-ttu-id="b4b1a-213">
<a HREF="http://go.microsoft.com/fwlink/p/?LinkID=285670">Administrar su Namespace ACS</a> proporciona más información sobre Hola Portal de Control de acceso.</span><span class="sxs-lookup"><span data-stu-id="b4b1a-213">
<a HREF="http://go.microsoft.com/fwlink/p/?LinkID=285670">Managing Your ACS Namespace</a> provides more information on hello Access Control Portal.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="b4b1a-214"><strong>Sincronizar las claves</strong> Hola cuenta de almacenamiento</span><span class="sxs-lookup"><span data-stu-id="b4b1a-214"><strong>Sync Keys</strong> in hello Storage Account</span></span></td>
<td><span data-ttu-id="b4b1a-215">Cuando crea una cuenta de almacenamiento, se crean automáticamente una clave primaria y una clave secundaria.</span><span class="sxs-lookup"><span data-stu-id="b4b1a-215">When you create a Storage account, a Primary Key and Secondary Key are automatically created.</span></span> <span data-ttu-id="b4b1a-216">Estas claves de cifrado controlan acceso tooyour cuenta de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="b4b1a-216">These encryption Keys control access tooyour Storage Account.</span></span> <span data-ttu-id="b4b1a-217">Su BizTalk Service usa automáticamente Hola Primary Key.</span><span class="sxs-lookup"><span data-stu-id="b4b1a-217">Your BizTalk Service automatically uses hello Primary Key.</span></span> <span data-ttu-id="b4b1a-218"><strong>Sincronizar las claves</strong> habilitar usuarios tooswitch entre clave principal de Hola y Hola clave secundaria sin interrumpir Hola BizTalk Service.</span><span class="sxs-lookup"><span data-stu-id="b4b1a-218"><strong>Sync Keys</strong> enable users tooswitch between hello Primary Key and hello Secondary Key without disrupting hello BizTalk Service.</span></span>
<br/><br/>
<span data-ttu-id="b4b1a-219">Por ejemplo, desea Hola BizTalk Service toouse una nueva clave principal para hello cuenta de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="b4b1a-219">For example, you want hello BizTalk Service toouse a new Primary Key for hello Storage Account.</span></span> <span data-ttu-id="b4b1a-220">toodo esto:</span><span class="sxs-lookup"><span data-stu-id="b4b1a-220">toodo this:</span></span>
<br/><br/>
<ol>
<li><span data-ttu-id="b4b1a-221">Seleccione el servicio de BizTalk y después <strong>Sincronizar claves</strong>.</span><span class="sxs-lookup"><span data-stu-id="b4b1a-221">Select your BizTalk Service and select <strong>Sync Keys</strong>.</span></span> <span data-ttu-id="b4b1a-222">Seleccione Hola clave secundaria.</span><span class="sxs-lookup"><span data-stu-id="b4b1a-222">Select hello Secondary Key.</span></span> <span data-ttu-id="b4b1a-223">Al hacerlo, Hola BizTalk Service inicia utilizando Hola clave secundaria.</span><span class="sxs-lookup"><span data-stu-id="b4b1a-223">When you do this, hello BizTalk Service starts using hello Secondary Key.</span></span></li>
<li><span data-ttu-id="b4b1a-224">Hola portal de Azure clásico, seleccione la cuenta de almacenamiento y volver a generar Hola Primary Key.</span><span class="sxs-lookup"><span data-stu-id="b4b1a-224">In hello Azure classic portal, select your Storage account and Regenerate hello Primary Key.</span></span> <span data-ttu-id="b4b1a-225">Recuerde que su BizTalk Service está usando Hola clave secundaria.</span><span class="sxs-lookup"><span data-stu-id="b4b1a-225">Remember, your BizTalk Service is using hello Secondary Key.</span></span></li>
<li><span data-ttu-id="b4b1a-226">Seleccione el servicio de BizTalk y después <strong>Sincronizar claves</strong>.</span><span class="sxs-lookup"><span data-stu-id="b4b1a-226">Select your BizTalk Service and select <strong>Sync Keys</strong>.</span></span> <span data-ttu-id="b4b1a-227">Ahora, seleccione Hola Primary Key.</span><span class="sxs-lookup"><span data-stu-id="b4b1a-227">Now, select hello Primary Key.</span></span> <span data-ttu-id="b4b1a-228">Esto es Hola nueva clave principal vuelve a generar.</span><span class="sxs-lookup"><span data-stu-id="b4b1a-228">This is hello new Primary Key you regenerated.</span></span></li>
<li><span data-ttu-id="b4b1a-229">Hola portal de Azure clásico, seleccione la cuenta de almacenamiento y volver a generar Hola clave secundaria.</span><span class="sxs-lookup"><span data-stu-id="b4b1a-229">In hello Azure classic portal, select your Storage account and Regenerate hello Secondary Key.</span></span></li>
</ol>
<br/>
<span data-ttu-id="b4b1a-230">Este proceso se llama "claves de sustitución".</span><span class="sxs-lookup"><span data-stu-id="b4b1a-230">This process is called "rollover keys".</span></span> <span data-ttu-id="b4b1a-231">Hola sirve tooenable usuarios tooswitch entre clave principal de Hola y Hola clave secundaria sin interrumpir Hola BizTalk Service.</span><span class="sxs-lookup"><span data-stu-id="b4b1a-231">hello purpose is tooenable users tooswitch between hello Primary Key and hello Secondary Key without disrupting hello BizTalk Service.</span></span></td>
</tr>

<tr>
<td><span data-ttu-id="b4b1a-232"><strong>Eliminar</strong> la aplicación</span><span class="sxs-lookup"><span data-stu-id="b4b1a-232"><strong>Delete</strong> your application</span></span></td>
<td><span data-ttu-id="b4b1a-233">Se quitan los BizTalk Service y tooit de todos los elementos implementados.</span><span class="sxs-lookup"><span data-stu-id="b4b1a-233">Your BizTalk Service and all items deployed tooit are removed.</span></span></td>
</tr>
</table>


## <a name="monitor"></a><span data-ttu-id="b4b1a-234">Supervisión</span><span class="sxs-lookup"><span data-stu-id="b4b1a-234">Monitor</span></span>
<span data-ttu-id="b4b1a-235">No hay ningún toohello edición gratuita.</span><span class="sxs-lookup"><span data-stu-id="b4b1a-235">Does not apply toohello Free Edition.</span></span>

<span data-ttu-id="b4b1a-236">Cuando se selecciona el nombre de BizTalk Service, la pestaña Monitor Hola está disponible y muestra hello siguiente:</span><span class="sxs-lookup"><span data-stu-id="b4b1a-236">When you select your BizTalk Service name, hello Monitor tab is available and displays hello following:</span></span>

##### <a name="metric-graph-displays-hello-selected-performance-metrics"></a><span data-ttu-id="b4b1a-237">Gráfico de métrica: Hola muestra seleccionado las métricas de rendimiento</span><span class="sxs-lookup"><span data-stu-id="b4b1a-237">Metric Graph: Displays hello selected performance metrics</span></span>
<span data-ttu-id="b4b1a-238">Estas métricas proporcionan valores en tiempo real con respecto a mantenimiento Hola de hello BizTalk Service.</span><span class="sxs-lookup"><span data-stu-id="b4b1a-238">These metrics provide real-time values regarding hello health of hello BizTalk Service.</span></span> <span data-ttu-id="b4b1a-239">Se pueden elegir las métricas de rendimiento que mostrar.</span><span class="sxs-lookup"><span data-stu-id="b4b1a-239">You choose which performance metrics are displayed.</span></span> <span data-ttu-id="b4b1a-240">Se pueden mostrar seis métricas de rendimiento a la vez como máximo.</span><span class="sxs-lookup"><span data-stu-id="b4b1a-240">A maximum of six performance metrics can be displayed simultaneously.</span></span> 

<span data-ttu-id="b4b1a-241">También puede elegir hello **relativa** o **absoluta** hello y valores de intervalo de tiempo **intervalo** de métricas de Hola que se muestran.</span><span class="sxs-lookup"><span data-stu-id="b4b1a-241">You can also choose hello **Relative** or **Absolute** values and hello time range **Interval** of hello metrics that are displayed.</span></span> 

##### <a name="tooremove-or-display-metrics-in-hello-graph"></a><span data-ttu-id="b4b1a-242">métricas de tooremove o mostrar en gráfico de hello:</span><span class="sxs-lookup"><span data-stu-id="b4b1a-242">tooremove or display metrics in hello graph:</span></span>
1. <span data-ttu-id="b4b1a-243">Seleccione hello **Monitor** ficha.</span><span class="sxs-lookup"><span data-stu-id="b4b1a-243">Select hello **Monitor** tab.</span></span>
2. <span data-ttu-id="b4b1a-244">Seleccione **agregar métricas** en la barra de tareas de hello:</span><span class="sxs-lookup"><span data-stu-id="b4b1a-244">Select **Add Metrics** in hello task bar:</span></span>  
   <span data-ttu-id="b4b1a-245">![Seleccione Agregar métricas][AddMetrics]</span><span class="sxs-lookup"><span data-stu-id="b4b1a-245">![Select Add Metrics][AddMetrics]</span></span>
3. <span data-ttu-id="b4b1a-246">Compruebe las métricas de rendimiento de hello desea toodisplay.</span><span class="sxs-lookup"><span data-stu-id="b4b1a-246">Check hello performance metrics you want toodisplay.</span></span>
4. <span data-ttu-id="b4b1a-247">Seleccione Hola marca de verificación tooreturn toohello **Monitor** ficha.</span><span class="sxs-lookup"><span data-stu-id="b4b1a-247">Select hello checkmark tooreturn toohello **Monitor** tab.</span></span>
5. <span data-ttu-id="b4b1a-248">Seleccione Hola círculo siguiente toohello métrica toodisplay valor del esa métrica gráfico de Hola.</span><span class="sxs-lookup"><span data-stu-id="b4b1a-248">Select hello circle next toohello metric toodisplay that metric's value in hello graph.</span></span>  
   
    <span data-ttu-id="b4b1a-249">Por ejemplo, hello **el uso de CPU** métrica está atenuada; no se muestra su salida en el gráfico de hello:</span><span class="sxs-lookup"><span data-stu-id="b4b1a-249">For example, hello **CPU Usage** metric is grayed out; its output is not displayed in hello graph:</span></span>  
   <span data-ttu-id="b4b1a-250">![La métrica Uso de CPU está atenuada][GrayedMetric]</span><span class="sxs-lookup"><span data-stu-id="b4b1a-250">![CPU Usage metric is grayed out][GrayedMetric]</span></span>  
   
    <span data-ttu-id="b4b1a-251">Seleccione hello en gris Hola de círculo tooenable **el uso de CPU** toodisplay métrica sus resultados en el gráfico de hello:</span><span class="sxs-lookup"><span data-stu-id="b4b1a-251">Select hello grayed out circle tooenable hello **CPU Usage** metric toodisplay its output in hello graph:</span></span>  
   <span data-ttu-id="b4b1a-252">![La métrica Uso de CPU está habilitada][EnabledMetric]</span><span class="sxs-lookup"><span data-stu-id="b4b1a-252">![CPU Usage metric is enabled][EnabledMetric]</span></span>
6. <span data-ttu-id="b4b1a-253">Seleccione una métrica del gráfico de visualización de Hola y lista de hello, tooremove **eliminar métrica** en la barra de tareas de Hola.</span><span class="sxs-lookup"><span data-stu-id="b4b1a-253">tooremove a metric from hello display graph and hello list, select **Delete Metric** in hello task bar.</span></span> <span data-ttu-id="b4b1a-254">lista de métricas toohello atrás de hello tooadd, seleccione **agregar métricas** en la barra de tareas de hello, compruebe la métrica de Hola y Hola seleccione marca de verificación tooreturn toohello **Monitor** ficha. Seleccione Hola gris métrica de círculo tooenable Hola.</span><span class="sxs-lookup"><span data-stu-id="b4b1a-254">tooadd hello metric back toohello list, select **Add Metrics** in hello task bar, check hello metric, and select hello checkmark tooreturn toohello **Monitor** tab. Select hello grayed out circle tooenable hello metric.</span></span>

## <span data-ttu-id="b4b1a-255"><a name="Metrics"></a>Métricas disponibles</span><span class="sxs-lookup"><span data-stu-id="b4b1a-255"><a name="Metrics"></a>Available Metrics</span></span>
<span data-ttu-id="b4b1a-256">Hola siguiendo los contadores de rendimiento y las métricas está disponible:</span><span class="sxs-lookup"><span data-stu-id="b4b1a-256">hello following performance counters/metrics are available:</span></span>

<table border="1">

<tr>
<td><span data-ttu-id="b4b1a-257"><strong>Latencia de recorrido de ida y vuelta</strong></span><span class="sxs-lookup"><span data-stu-id="b4b1a-257"><strong>RountdTrip Latency</strong></span></span></td>
<td><span data-ttu-id="b4b1a-258">Muestra el tiempo medio de hello realizada en milisegundos tooprocess (ms) que se recibe un mensaje de mensaje de saludo de hello tiempo hasta que el mensaje Hola se procese por completo por hello BizTalk Service a través de todos los puentes de.</span><span class="sxs-lookup"><span data-stu-id="b4b1a-258">Displays hello average time taken in milliseconds (ms) tooprocess a message from hello time hello message is received until hello message is fully processed by hello BizTalk Service across all bridges.</span></span> <span data-ttu-id="b4b1a-259">Solo se cuentan los mensajes correctamente procesados.</span><span class="sxs-lookup"><span data-stu-id="b4b1a-259">Only messages successfully processed are counted.</span></span><br/><br/>
<span data-ttu-id="b4b1a-260">Cuando se produce Hola después de eventos, se crea una marca de tiempo:</span><span class="sxs-lookup"><span data-stu-id="b4b1a-260">When hello following events occur, a timestamp is created:</span></span>
<ul>
<li><span data-ttu-id="b4b1a-261">Mensaje entra en la puerta de enlace de Hola</span><span class="sxs-lookup"><span data-stu-id="b4b1a-261">Message enters hello gateway</span></span></li>
<li><span data-ttu-id="b4b1a-262">Mensaje es destino toohello enrutado</span><span class="sxs-lookup"><span data-stu-id="b4b1a-262">Message is routed toohello destination</span></span></li>
<li><span data-ttu-id="b4b1a-263">Se recibe la respuesta del destino</span><span class="sxs-lookup"><span data-stu-id="b4b1a-263">Destination response is received</span></span></li>
<li><span data-ttu-id="b4b1a-264">Puerta de enlace toohello enviado respuesta de confirmación de destino</span><span class="sxs-lookup"><span data-stu-id="b4b1a-264">Destination acknowledgement response sent toohello gateway</span></span></li>
</ul>
<br/>
<span data-ttu-id="b4b1a-265">Esta métrica muestra resultado de hello de hello siguiente cálculo:</span><span class="sxs-lookup"><span data-stu-id="b4b1a-265">This metric shows hello result of hello following calculation:</span></span>
<br/><br/>
<span data-ttu-id="b4b1a-266">[Destino acuse de recibo respuesta enviada toohello puerta de enlace] - [mensaje entra en puerta de enlace de hello]</span><span class="sxs-lookup"><span data-stu-id="b4b1a-266">[Destination acknowledgement response sent toohello gateway] - [Message enters hello gateway]</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="b4b1a-267"><strong>Errores en origen</strong></span><span class="sxs-lookup"><span data-stu-id="b4b1a-267"><strong>Failures At Source</strong></span></span></td>
<td><span data-ttu-id="b4b1a-268">Muestra el número total de Hola de mensajes que no se pudo por BizTalk Service al extraer los mensajes desde los puntos de conexión de origen de Hola Hola.</span><span class="sxs-lookup"><span data-stu-id="b4b1a-268">Displays hello total number of messages that failed by hello BizTalk Service when pulling messages from hello source endpoints.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="b4b1a-269"><strong>Uso de CPU</strong></span><span class="sxs-lookup"><span data-stu-id="b4b1a-269"><strong>CPU Usage</strong></span></span></td>
<td><span data-ttu-id="b4b1a-270">Enumera Hola % promedio de tiempo de procesador de todas las instancias de rol.</span><span class="sxs-lookup"><span data-stu-id="b4b1a-270">Lists hello average %Processor Time of all role instances.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="b4b1a-271"><strong>Latencia de procesamiento</strong></span><span class="sxs-lookup"><span data-stu-id="b4b1a-271"><strong>Processing Latency</strong></span></span></td>
<td><span data-ttu-id="b4b1a-272">Muestra el tiempo medio de hello realizada en un mensaje Hola BizTalk Service a través de todos los puentes, excluido el tiempo de hello empleado en destinos de tooprocess de milisegundos (ms).</span><span class="sxs-lookup"><span data-stu-id="b4b1a-272">Displays hello average time taken In milliseconds (ms) tooprocess a message by hello BizTalk Service across all bridges, excluding hello time spent in destinations.</span></span> <span data-ttu-id="b4b1a-273">Solo se cuentan los mensajes correctamente procesados.</span><span class="sxs-lookup"><span data-stu-id="b4b1a-273">Only messages successfully processed are counted.</span></span><br/><br/>
<span data-ttu-id="b4b1a-274">Cuando se producen cada uno de hello después de eventos, se crea una marca de tiempo:</span><span class="sxs-lookup"><span data-stu-id="b4b1a-274">When each of hello following events occur, a timestamp is created:</span></span>

<ul>
<li><span data-ttu-id="b4b1a-275">Mensaje entra en la puerta de enlace de Hola</span><span class="sxs-lookup"><span data-stu-id="b4b1a-275">Message enters hello gateway</span></span></li>
<li><span data-ttu-id="b4b1a-276">Mensaje es destino toohello enrutado</span><span class="sxs-lookup"><span data-stu-id="b4b1a-276">Message is routed toohello destination</span></span></li>
<li><span data-ttu-id="b4b1a-277">Se recibe la respuesta del destino</span><span class="sxs-lookup"><span data-stu-id="b4b1a-277">Destination response is received</span></span></li>
<li><span data-ttu-id="b4b1a-278">Puerta de enlace toohello enviado respuesta de confirmación de destino</span><span class="sxs-lookup"><span data-stu-id="b4b1a-278">Destination acknowledgement response sent toohello gateway</span></span></li>
</ul>
<br/><span data-ttu-id="b4b1a-279">Esta métrica muestra resultado de hello de hello siguiente cálculo:</span><span class="sxs-lookup"><span data-stu-id="b4b1a-279">This metric shows hello result of hello following calculation:</span></span><br/><br/>
<span data-ttu-id="b4b1a-280">[Destino acuse de recibo respuesta enviada toohello puerta de enlace] - [mensaje entra en puerta de enlace de hello] - [se recibió la respuesta de destino] + [mensaje enrutado toohello destino]</span><span class="sxs-lookup"><span data-stu-id="b4b1a-280">[Destination acknowledgement response sent toohello gateway] - [Message enters hello gateway] - [Destination response is received] + [Message is routed toohello destination]</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="b4b1a-281"><strong>Errores en proceso</strong></span><span class="sxs-lookup"><span data-stu-id="b4b1a-281"><strong>Failures In Process</strong></span></span></td>
<td><span data-ttu-id="b4b1a-282">Muestra el número total de Hola de mensajes con errores durante el procesamiento por hello BizTalk Service a través de todos los puentes de hello dentro de un intervalo de tiempo.</span><span class="sxs-lookup"><span data-stu-id="b4b1a-282">Displays hello total number of messages that failed during processing by hello BizTalk Service across all hello bridges within a time interval.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="b4b1a-283"><strong>Mensajes enviados</strong></span><span class="sxs-lookup"><span data-stu-id="b4b1a-283"><strong>Messages Sent</strong></span></span></td>
<td><span data-ttu-id="b4b1a-284">Muestra hello el número total de mensajes enviados por hello BizTalk Service a través de todos los puentes dentro de un intervalo de tiempo.</span><span class="sxs-lookup"><span data-stu-id="b4b1a-284">Displays hello total number of messages sent by hello BizTalk Service across all bridges within a time interval.</span></span> <span data-ttu-id="b4b1a-285">Esta métrica se incrementa cuando llegue a un mensaje enviado desde una canalización de destino de la ruta de Hola.</span><span class="sxs-lookup"><span data-stu-id="b4b1a-285">This metric is incremented when a message sent from a pipeline reaches hello route destination.</span></span> <span data-ttu-id="b4b1a-286">Esta métrica no indica el correcto procesamiento del mensaje.</span><span class="sxs-lookup"><span data-stu-id="b4b1a-286">This metric does not indicate that a message is successfully processed.</span></span><br/><br/>
<span data-ttu-id="b4b1a-287">En un escenario de solicitud y respuesta, métrica Hola se incrementa al destino de la ruta de hello envía una canalización de recepción confirmación toohello atrás.</span><span class="sxs-lookup"><span data-stu-id="b4b1a-287">In a Request-Reply scenario, hello metric is incremented when hello route destination sends a receipt acknowledgement back toohello pipeline.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="b4b1a-288"><strong>Mensajes recibidos</strong></span><span class="sxs-lookup"><span data-stu-id="b4b1a-288"><strong>Messages Received</strong></span></span></td>
<td><span data-ttu-id="b4b1a-289">Muestra hello el número total de mensajes recibidos por hello BizTalk Service a través de todos los puentes dentro de un intervalo de tiempo.</span><span class="sxs-lookup"><span data-stu-id="b4b1a-289">Displays hello total number of messages received by hello BizTalk Service across all bridges within a time interval.</span></span> <span data-ttu-id="b4b1a-290">Esta métrica se incrementa cuando se recibe un mensaje nuevo canalización Hola.</span><span class="sxs-lookup"><span data-stu-id="b4b1a-290">This metric is incremented when a new message is received by hello pipeline.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="b4b1a-291"><strong>Mensajes en proceso</strong></span><span class="sxs-lookup"><span data-stu-id="b4b1a-291"><strong>Messages In Process</strong></span></span></td>
<td><span data-ttu-id="b4b1a-292">Muestra Hola número total de mensajes que está procesando actualmente Hola BizTalk Service dentro de un intervalo de tiempo.</span><span class="sxs-lookup"><span data-stu-id="b4b1a-292">Displays hello total number of messages currently being processed by hello BizTalk Service within a time interval.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="b4b1a-293"><strong>Mensajes procesados</strong></span><span class="sxs-lookup"><span data-stu-id="b4b1a-293"><strong>Messages Processed</strong></span></span></td>
<td><span data-ttu-id="b4b1a-294">Muestra Hola número total de mensajes procesados correctamente por hello BizTalk Service a través de todos los puentes dentro de un intervalo de tiempo.</span><span class="sxs-lookup"><span data-stu-id="b4b1a-294">Displays hello total number of messages successfully processed by hello BizTalk Service across all bridges within a time interval.</span></span> <span data-ttu-id="b4b1a-295">Esta métrica se incrementa cuando un mensaje se recibe correctamente por la canalización de Hola y de destino de toohello enrutado correctamente.</span><span class="sxs-lookup"><span data-stu-id="b4b1a-295">This metric is incremented when a message is successfully received by hello pipeline and successfully routed toohello destination.</span></span></td>
</tr>
</table>


## <a name="scale"></a><span data-ttu-id="b4b1a-296">Escala</span><span class="sxs-lookup"><span data-stu-id="b4b1a-296">Scale</span></span>
<span data-ttu-id="b4b1a-297">En la pestaña escalar de hello, puede agregar o restar Hola número de unidades utilizadas por su BizTalk Service.</span><span class="sxs-lookup"><span data-stu-id="b4b1a-297">In hello Scale tab, you can add or subtract hello number of units used by your BizTalk Service.</span></span> <span data-ttu-id="b4b1a-298">De forma predeterminada, hay una unidad configurada.</span><span class="sxs-lookup"><span data-stu-id="b4b1a-298">By default, there is one Unit configured.</span></span> <span data-ttu-id="b4b1a-299">Unidades adicionales pueden agregarse tooscale su BizTalk Service.</span><span class="sxs-lookup"><span data-stu-id="b4b1a-299">Additional Units can be added tooscale your BizTalk Service.</span></span> <span data-ttu-id="b4b1a-300">Al aumentar la escala de hello, se aumenta el rendimiento.</span><span class="sxs-lookup"><span data-stu-id="b4b1a-300">When you increase hello scale, you are increasing throughput.</span></span> <span data-ttu-id="b4b1a-301">Hola de recursos también aumenta, incluidos los puentes implementados, contratos, las conexiones de LOB y capacidad de procesamiento.</span><span class="sxs-lookup"><span data-stu-id="b4b1a-301">hello amount of resources also increases, including deployed bridges, agreements, LOB connections, and processing power.</span></span> <span data-ttu-id="b4b1a-302">Por ejemplo, aumentar la escala Hola de unidades de 1 unidad too2.</span><span class="sxs-lookup"><span data-stu-id="b4b1a-302">For example, you increase hello scale from 1 Unit too2 Units.</span></span> <span data-ttu-id="b4b1a-303">En esta situación, puede implementar Hola dobles número de puentes, double contratos hello, double Hola LOB conexiones y potencia de procesamiento de hello dobles.</span><span class="sxs-lookup"><span data-stu-id="b4b1a-303">In this situation, you can deploy double hello number of bridges, double hello agreements, double hello LOB connections, and double hello processing power.</span></span>

<span data-ttu-id="b4b1a-304">Algunas ediciones de BizTalk no ofrecen la opción de escala.</span><span class="sxs-lookup"><span data-stu-id="b4b1a-304">Some BizTalk editions do not offer a scale option.</span></span> <span data-ttu-id="b4b1a-305">En esta situación, se admite una unidad.</span><span class="sxs-lookup"><span data-stu-id="b4b1a-305">In this situation, one Unit is permitted.</span></span> <span data-ttu-id="b4b1a-306">toodetermine cuántas unidades se puede escalar su edición, consulte demasiado[servicios de BizTalk: gráfico de ediciones](biztalk-editions-feature-chart.md).</span><span class="sxs-lookup"><span data-stu-id="b4b1a-306">toodetermine how many units your edition can be scaled, refer too[BizTalk Services: Editions Chart](biztalk-editions-feature-chart.md).</span></span>

<span data-ttu-id="b4b1a-307">Aumentar el número de Hola de unidades puede afectar el precio.</span><span class="sxs-lookup"><span data-stu-id="b4b1a-307">Increasing hello number of units may impact pricing.</span></span> <span data-ttu-id="b4b1a-308">Si aumenta las unidades de hello, seleccionar **guardar** muestra un mensaje que indica si se ve afectada la facturación.</span><span class="sxs-lookup"><span data-stu-id="b4b1a-308">If you increase hello Units, selecting **Save** displays a message that tells you if billing is impacted.</span></span> <span data-ttu-id="b4b1a-309">A continuación, elija toocontinue.</span><span class="sxs-lookup"><span data-stu-id="b4b1a-309">You then choose toocontinue.</span></span> <span data-ttu-id="b4b1a-310">Al aumentar el número de Hola de unidades, Hola estado BizTalk Service cambia de activo tooUpdating.</span><span class="sxs-lookup"><span data-stu-id="b4b1a-310">When you increase hello number of Units, hello BizTalk Service status changes from Active tooUpdating.</span></span> <span data-ttu-id="b4b1a-311">En el estado de actualización de hello, su BizTalk Service continúa toorun.</span><span class="sxs-lookup"><span data-stu-id="b4b1a-311">In hello Updating state, your BizTalk Service continues toorun.</span></span>

<span data-ttu-id="b4b1a-312">[Servicios de BizTalk: gráfico de ediciones](biztalk-editions-feature-chart.md) define una unidad.</span><span class="sxs-lookup"><span data-stu-id="b4b1a-312">[BizTalk Services: Editions Chart](biztalk-editions-feature-chart.md) defines a "Unit".</span></span>

## <a name="configure"></a><span data-ttu-id="b4b1a-313">Configuración</span><span class="sxs-lookup"><span data-stu-id="b4b1a-313">Configure</span></span>
<span data-ttu-id="b4b1a-314">No hay ningún tooHybrid conexiones.</span><span class="sxs-lookup"><span data-stu-id="b4b1a-314">Does not apply tooHybrid Connections.</span></span>

<span data-ttu-id="b4b1a-315">Establece tooNone de estado de copia de seguridad de Hola o automático.</span><span class="sxs-lookup"><span data-stu-id="b4b1a-315">Sets hello Backup Status tooNone or Automatic.</span></span> <span data-ttu-id="b4b1a-316">Cuando se establece tooNone, copias de seguridad no se crean automáticamente.</span><span class="sxs-lookup"><span data-stu-id="b4b1a-316">When set tooNone, no backups are automatically created.</span></span> <span data-ttu-id="b4b1a-317">Cuando se establece tooAutomatic, configurar la ubicación de copia de seguridad de hello, frecuencia de Hola de copia de seguridad de Hola y cuánto archivos de copia de seguridad de hello tookeep.</span><span class="sxs-lookup"><span data-stu-id="b4b1a-317">When set tooAutomatic, you configure hello backup location, hello frequency of hello backup, and how long tookeep hello backup files.</span></span> 

<span data-ttu-id="b4b1a-318">[Servicios de BizTalk: Backup y Restore](biztalk-backup-restore.md) proporciona detalles de Hola.</span><span class="sxs-lookup"><span data-stu-id="b4b1a-318">[BizTalk Services: Backup and Restore](biztalk-backup-restore.md) provides hello details.</span></span> 

## <span data-ttu-id="b4b1a-319"><a name="HybridConnections"></a>Conexiones híbridas</span><span class="sxs-lookup"><span data-stu-id="b4b1a-319"><a name="HybridConnections"></a>Hybrid Connections</span></span>
<span data-ttu-id="b4b1a-320">Las conexiones híbridas conectan una aplicación de Azure, como las aplicaciones Web o aplicaciones móviles en el servicio de aplicación de Azure, recurso local de tooan que usa un puerto TCP estático, como SQL Server, MySQL, las API Web de HTTP y mayoría de los servicios Web personalizados.</span><span class="sxs-lookup"><span data-stu-id="b4b1a-320">Hybrid Connections connect an Azure application, like Web Apps or Mobile Apps in Azure App Service, tooan on-premises resource that uses a static TCP port, such as SQL Server, MySQL, HTTP Web APIs, and most custom Web Services.</span></span> <span data-ttu-id="b4b1a-321">Las conexiones híbridas se administran en servicios de BizTalk en hello portal de Azure clásico.</span><span class="sxs-lookup"><span data-stu-id="b4b1a-321">Hybrid Connections are managed in  BizTalk Services in hello Azure classic portal.</span></span>

<span data-ttu-id="b4b1a-322">toocreate las conexiones híbridas en el servicio de aplicación de Azure, consulte [acceder a recursos usando conexiones híbridas en el servicio de aplicación de Azure local](../app-service-web/web-sites-hybrid-connection-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="b4b1a-322">toocreate Hybrid Connections in Azure App Service, see [Access on-premises resources using hybrid connections in Azure App Service](../app-service-web/web-sites-hybrid-connection-get-started.md).</span></span>

<span data-ttu-id="b4b1a-323">toocreate o administrar las conexiones híbridas en servicios de BizTalk de Azure, consulte [conexiones híbridas](integration-hybrid-connection-overview.md).</span><span class="sxs-lookup"><span data-stu-id="b4b1a-323">toocreate or manage Hybrid Connections in Azure BizTalk Services, see [Hybrid Connections](integration-hybrid-connection-overview.md).</span></span>

## <a name="next"></a><span data-ttu-id="b4b1a-324">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="b4b1a-324">Next</span></span>
<span data-ttu-id="b4b1a-325">Ahora que está familiarizado con las diferentes pestañas de hello, puede obtener más información acerca de las características de servicios de BizTalk de Azure de hello:</span><span class="sxs-lookup"><span data-stu-id="b4b1a-325">Now that you're familiar with hello different tabs, you can learn more about hello Azure BizTalk Services features:</span></span>

* [<span data-ttu-id="b4b1a-326">Servicios de BizTalk: limitaciones</span><span class="sxs-lookup"><span data-stu-id="b4b1a-326">BizTalk Services: Throttling</span></span>](biztalk-throttling-thresholds.md)  
* [<span data-ttu-id="b4b1a-327">Servicios de BizTalk: nombre del emisor y clave del emisor</span><span class="sxs-lookup"><span data-stu-id="b4b1a-327">BizTalk Services: Issuer Name and Issuer Key</span></span>](biztalk-issuer-name-issuer-key.md)  
* [<span data-ttu-id="b4b1a-328">Servicios de BizTalk: copias de seguridad y restauración</span><span class="sxs-lookup"><span data-stu-id="b4b1a-328">BizTalk Services: Backup and Restore</span></span>](biztalk-backup-restore.md)

## <a name="see-also"></a><span data-ttu-id="b4b1a-329">Otras referencias</span><span class="sxs-lookup"><span data-stu-id="b4b1a-329">See Also</span></span>
* [<span data-ttu-id="b4b1a-330">Conexiones híbridas</span><span class="sxs-lookup"><span data-stu-id="b4b1a-330">Hybrid Connections</span></span>](integration-hybrid-connection-overview.md)  
* [<span data-ttu-id="b4b1a-331">Servicios de BizTalk: gráfico de las ediciones Developer, Basic, Standard y Premium</span><span class="sxs-lookup"><span data-stu-id="b4b1a-331">BizTalk Services: Developer, Basic, Standard and Premium Editions Chart</span></span>](biztalk-editions-feature-chart.md)  
* [<span data-ttu-id="b4b1a-332">Servicios de BizTalk: aprovisionamiento con el Portal de Azure clásico</span><span class="sxs-lookup"><span data-stu-id="b4b1a-332">BizTalk Services: Provisioning Using Azure classic portal</span></span>](biztalk-provision-services.md)  
* [<span data-ttu-id="b4b1a-333">Servicios de BizTalk: gráfico de estado del servicio de BizTalk</span><span class="sxs-lookup"><span data-stu-id="b4b1a-333">BizTalk Services: BizTalk Service State Chart</span></span>](biztalk-service-state-chart.md)  
* [<span data-ttu-id="b4b1a-334">¿Cómo puedo comenzar a utilizar Hola SDK de servicios de BizTalk de Azure</span><span class="sxs-lookup"><span data-stu-id="b4b1a-334">How do I Start Using hello Azure BizTalk Services SDK</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=302335)

[Quickstart]: ./media/biztalk-dashboard-monitor-scale-tabs/QuickStartIcon.png
[AddMetrics]: ./media/biztalk-dashboard-monitor-scale-tabs/WABS_AddMetrics.png
[GrayedMetric]: ./media/biztalk-dashboard-monitor-scale-tabs/WABS_GrayedMetric.png
[EnabledMetric]: ./media/biztalk-dashboard-monitor-scale-tabs/WABS_EnabledMetric.png

