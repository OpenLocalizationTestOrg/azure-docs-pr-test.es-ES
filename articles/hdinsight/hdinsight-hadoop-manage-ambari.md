---
title: aaaMonitor y administrar mediante la interfaz de usuario de Ambari Web de HDInsight de Azure | Documentos de Microsoft
description: "Obtenga información acerca de cómo toouse Ambari toomonitor y administrar clústeres de HDInsight basados en Linux. En este documento, aprenderá cómo clústeres toouse hello Ambari de interfaz de usuario Web incluido con HDInsight."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 4787f3cc-a650-4dc3-9d96-a19a67aad046
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 07/31/2017
ms.author: larryfr
ms.openlocfilehash: d422c40e63345d7054839a625e115c50dad040f9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="manage-hdinsight-clusters-by-using-hello-ambari-web-ui"></a><span data-ttu-id="a8df8-104">Administrar clústeres de HDInsight con Ambari Web UI Hola</span><span class="sxs-lookup"><span data-stu-id="a8df8-104">Manage HDInsight clusters by using hello Ambari Web UI</span></span>

[!INCLUDE [ambari-selector](../../includes/hdinsight-ambari-selector.md)]

<span data-ttu-id="a8df8-105">Apache Ambari simplifica la administración de Hola y supervisión de un clúster de Hadoop proporcionando fácil toouse web API de REST y de interfaz de usuario.</span><span class="sxs-lookup"><span data-stu-id="a8df8-105">Apache Ambari simplifies hello management and monitoring of a Hadoop cluster by providing an easy toouse web UI and REST API.</span></span> <span data-ttu-id="a8df8-106">Ambari se incluye en clústeres de HDInsight basados en Linux y es usado toomonitor Hola clúster y realizar cambios de configuración.</span><span class="sxs-lookup"><span data-stu-id="a8df8-106">Ambari is included on Linux-based HDInsight clusters, and is used toomonitor hello cluster and make configuration changes.</span></span>

<span data-ttu-id="a8df8-107">En este documento, aprenderá cómo toouse Hola Ambari Web UI con un clúster de HDInsight.</span><span class="sxs-lookup"><span data-stu-id="a8df8-107">In this document, you learn how toouse hello Ambari Web UI with an HDInsight cluster.</span></span>

## <span data-ttu-id="a8df8-108"><a id="whatis"></a> ¿Qué es Ambari?</span><span class="sxs-lookup"><span data-stu-id="a8df8-108"><a id="whatis"></a>What is Ambari?</span></span>

<span data-ttu-id="a8df8-109">[Apache Ambari](http://ambari.apache.org) simplifica la administración de Hadoop al proporcionar una interfaz de usuario de web fácil de usar.</span><span class="sxs-lookup"><span data-stu-id="a8df8-109">[Apache Ambari](http://ambari.apache.org) simplifies Hadoop management by providing an easy-to-use web UI.</span></span> <span data-ttu-id="a8df8-110">Puede usar Ambari para crear, administrar y supervisar clústeres de Hadoop.</span><span class="sxs-lookup"><span data-stu-id="a8df8-110">You can use Ambari create, manage, and monitor Hadoop clusters.</span></span> <span data-ttu-id="a8df8-111">Los desarrolladores pueden integrar estas capacidades en sus aplicaciones mediante el uso de hello [API de REST de Ambari](https://github.com/apache/ambari/blob/trunk/ambari-server/docs/api/v1/index.md).</span><span class="sxs-lookup"><span data-stu-id="a8df8-111">Developers can integrate these capabilities into their applications by using hello [Ambari REST APIs](https://github.com/apache/ambari/blob/trunk/ambari-server/docs/api/v1/index.md).</span></span>

<span data-ttu-id="a8df8-112">Hola Ambari Web UI se proporciona de forma predeterminada con los clústeres de HDInsight que usan el sistema operativo de Linux de Hola.</span><span class="sxs-lookup"><span data-stu-id="a8df8-112">hello Ambari Web UI is provided by default with HDInsight clusters that use hello Linux operating system.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="a8df8-113">Linux es Hola único sistema operativo usado en HDInsight versión 3.4 o superior.</span><span class="sxs-lookup"><span data-stu-id="a8df8-113">Linux is hello only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="a8df8-114">Consulte la información sobre la [retirada de HDInsight en Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="a8df8-114">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span> 

## <a name="connectivity"></a><span data-ttu-id="a8df8-115">Conectividad</span><span class="sxs-lookup"><span data-stu-id="a8df8-115">Connectivity</span></span>

<span data-ttu-id="a8df8-116">Hola interfaz de usuario de Ambari Web está disponible en el clúster de HDInsight en HTTPS://CLUSTERNAME.azurehdidnsight.net, donde **CLUSTERNAME** es Hola nombre del clúster.</span><span class="sxs-lookup"><span data-stu-id="a8df8-116">hello Ambari Web UI is available on your HDInsight cluster at HTTPS://CLUSTERNAME.azurehdidnsight.net, where **CLUSTERNAME** is hello name of your cluster.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="a8df8-117">Conexión tooAmbari en HDInsight requiere HTTPS.</span><span class="sxs-lookup"><span data-stu-id="a8df8-117">Connecting tooAmbari on HDInsight requires HTTPS.</span></span> <span data-ttu-id="a8df8-118">Cuando se le solicite para la autenticación, utilice nombre de cuenta de administrador de Hola y la contraseña que proporcionó cuando se creó el clúster de Hola.</span><span class="sxs-lookup"><span data-stu-id="a8df8-118">When prompted for authentication, use hello admin account name and password you provided when hello cluster was created.</span></span>

## <a name="ssh-tunnel-proxy"></a><span data-ttu-id="a8df8-119">Túnel SSH (proxy)</span><span class="sxs-lookup"><span data-stu-id="a8df8-119">SSH tunnel (proxy)</span></span>

<span data-ttu-id="a8df8-120">Mientras Ambari para el clúster es accesible directamente a través de Internet de hello, algunos vínculos de hello Ambari la interfaz de usuario de Web (por ejemplo, toohello JobTracker) no se exponen en Hola internet.</span><span class="sxs-lookup"><span data-stu-id="a8df8-120">While Ambari for your cluster is accessible directly over hello Internet, some links from hello Ambari Web UI (such as toohello JobTracker) are not exposed on hello internet.</span></span> <span data-ttu-id="a8df8-121">tooaccess estos servicios, debe crear un túnel SSH.</span><span class="sxs-lookup"><span data-stu-id="a8df8-121">tooaccess these services, you must create an SSH tunnel.</span></span> <span data-ttu-id="a8df8-122">Para más información, consulte el documento [Uso de un túnel SSH con HDInsight](hdinsight-linux-ambari-ssh-tunnel.md).</span><span class="sxs-lookup"><span data-stu-id="a8df8-122">For more information, see [Use SSH Tunneling with HDInsight](hdinsight-linux-ambari-ssh-tunnel.md).</span></span>

## <a name="ambari-web-ui"></a><span data-ttu-id="a8df8-123">Interfaz de usuario web de Ambari</span><span class="sxs-lookup"><span data-stu-id="a8df8-123">Ambari Web UI</span></span>

<span data-ttu-id="a8df8-124">Cuando se conecte toohello Ambari Web UI, son tooauthenticate solicitadas toohello página.</span><span class="sxs-lookup"><span data-stu-id="a8df8-124">When connecting toohello Ambari Web UI, you are prompted tooauthenticate toohello page.</span></span> <span data-ttu-id="a8df8-125">Usar usuario de administrador de clúster de hello (el valor predeterminado es administrador) y la contraseña que usó durante la creación del clúster.</span><span class="sxs-lookup"><span data-stu-id="a8df8-125">Use hello cluster admin user (default Admin) and password you used during cluster creation.</span></span>

<span data-ttu-id="a8df8-126">Cuando se abre la página de hello, tenga en cuenta barra hello en la parte superior de Hola.</span><span class="sxs-lookup"><span data-stu-id="a8df8-126">When hello page opens, note hello bar at hello top.</span></span> <span data-ttu-id="a8df8-127">Esta barra contiene los siguientes Hola información y los controles:</span><span class="sxs-lookup"><span data-stu-id="a8df8-127">This bar contains hello following information and controls:</span></span>

![ambari-nav](./media/hdinsight-hadoop-manage-ambari/ambari-nav.png)

* <span data-ttu-id="a8df8-129">**Logotipo de Ambari** -panel de Hola se abre, que puede ser usado toomonitor Hola clúster.</span><span class="sxs-lookup"><span data-stu-id="a8df8-129">**Ambari logo** - Opens hello dashboard, which can be used toomonitor hello cluster.</span></span>

* <span data-ttu-id="a8df8-130">**Operaciones de # nombre de clúster** -muestra el número de Hola de las operaciones en curso de Ambari.</span><span class="sxs-lookup"><span data-stu-id="a8df8-130">**Cluster name # ops** - Displays hello number of ongoing Ambari operations.</span></span> <span data-ttu-id="a8df8-131">Seleccionar nombre de clúster de Hola o **ops #** muestra una lista de operaciones en segundo plano.</span><span class="sxs-lookup"><span data-stu-id="a8df8-131">Selecting hello cluster name or **# ops** displays a list of background operations.</span></span>

* <span data-ttu-id="a8df8-132">**alertas de #** -muestra las advertencias o alertas críticas, si existe, de clúster de Hola.</span><span class="sxs-lookup"><span data-stu-id="a8df8-132">**# alerts** - Displays warnings or critical alerts, if any, for hello cluster.</span></span>

* <span data-ttu-id="a8df8-133">**Panel** -panel de Hola de muestra.</span><span class="sxs-lookup"><span data-stu-id="a8df8-133">**Dashboard** - Displays hello dashboard.</span></span>

* <span data-ttu-id="a8df8-134">**Servicios** -configuración de información y configuración de servicios de hello en clúster Hola.</span><span class="sxs-lookup"><span data-stu-id="a8df8-134">**Services** - Information and configuration settings for hello services in hello cluster.</span></span>

* <span data-ttu-id="a8df8-135">**Hosts** -información y opciones de configuración para los nodos de hello en clúster de Hola.</span><span class="sxs-lookup"><span data-stu-id="a8df8-135">**Hosts** - Information and configuration settings for hello nodes in hello cluster.</span></span>

* <span data-ttu-id="a8df8-136">**Alerts** : un registro de información, advertencias y alertas críticas.</span><span class="sxs-lookup"><span data-stu-id="a8df8-136">**Alerts** - A log of information, warnings, and critical alerts.</span></span>

* <span data-ttu-id="a8df8-137">**Administración** -pila/servicios de Software que están instalados en el clúster de hello, información de la cuenta de servicio y la seguridad de Kerberos.</span><span class="sxs-lookup"><span data-stu-id="a8df8-137">**Admin** - Software stack/services that are installed on hello cluster, service account information, and Kerberos security.</span></span>

* <span data-ttu-id="a8df8-138">**Botón Admin** : administración de Ambari, configuración del usuario y cierre de sesión.</span><span class="sxs-lookup"><span data-stu-id="a8df8-138">**Admin button** - Ambari management, user settings, and logout.</span></span>

## <a name="monitoring"></a><span data-ttu-id="a8df8-139">Supervisión</span><span class="sxs-lookup"><span data-stu-id="a8df8-139">Monitoring</span></span>

### <a name="alerts"></a><span data-ttu-id="a8df8-140">Alertas</span><span class="sxs-lookup"><span data-stu-id="a8df8-140">Alerts</span></span>

<span data-ttu-id="a8df8-141">Hello siguiente lista contiene Estados de alertas comunes hello usa Ambari:</span><span class="sxs-lookup"><span data-stu-id="a8df8-141">hello following list contains hello common alert statuses used by Ambari:</span></span>

* <span data-ttu-id="a8df8-142">**OK (CORRECTO)**</span><span class="sxs-lookup"><span data-stu-id="a8df8-142">**OK**</span></span>
* <span data-ttu-id="a8df8-143">**Warning (ADVERTENCIA)**</span><span class="sxs-lookup"><span data-stu-id="a8df8-143">**Warning**</span></span>
* <span data-ttu-id="a8df8-144">**CRITICAL (CRÍTICA)**</span><span class="sxs-lookup"><span data-stu-id="a8df8-144">**CRITICAL**</span></span>
* <span data-ttu-id="a8df8-145">**UNKNOWN (DESCONOCIDO)**</span><span class="sxs-lookup"><span data-stu-id="a8df8-145">**UNKNOWN**</span></span>

<span data-ttu-id="a8df8-146">Las alertas excepto **Aceptar** provocar hello **alertas #** entrada en la parte superior de Hola Hola toodisplay Hola del número de página de alertas.</span><span class="sxs-lookup"><span data-stu-id="a8df8-146">Alerts other than **OK** cause hello **# alerts** entry at hello top of hello page toodisplay hello number of alerts.</span></span> <span data-ttu-id="a8df8-147">Al seleccionar esta entrada, muestran las alertas de Hola y su estado.</span><span class="sxs-lookup"><span data-stu-id="a8df8-147">Selecting this entry displays hello alerts and their status.</span></span>

<span data-ttu-id="a8df8-148">Las alertas se organizan en varios grupos predeterminados, que pueden verse desde hello **alertas** página.</span><span class="sxs-lookup"><span data-stu-id="a8df8-148">Alerts are organized into several default groups, which can be viewed from hello **Alerts** page.</span></span>

![página de alertas](./media/hdinsight-hadoop-manage-ambari/alerts.png)

<span data-ttu-id="a8df8-150">Puede administrar los grupos de hello mediante el uso de hello **acciones** menú y seleccionando **administrar grupos de alerta**.</span><span class="sxs-lookup"><span data-stu-id="a8df8-150">You can manage hello groups by using hello **Actions** menu and selecting **Manage Alert Groups**.</span></span>

![administrar cuadro de diálogo de grupos de alertas](./media/hdinsight-hadoop-manage-ambari/manage-alerts.png)

<span data-ttu-id="a8df8-152">También puede administrar los métodos de alerta y crear notificaciones de alerta de hello **acciones** menú seleccionando __Administrar notificaciones de alerta__.</span><span class="sxs-lookup"><span data-stu-id="a8df8-152">You can also manage alerting methods, and create alert notifications from hello **Actions** menu by selecting __Manage Alert Notifications__.</span></span> <span data-ttu-id="a8df8-153">Se muestran las notificaciones actuales.</span><span class="sxs-lookup"><span data-stu-id="a8df8-153">Any current notifications are displayed.</span></span> <span data-ttu-id="a8df8-154">También puede crear notificaciones desde aquí.</span><span class="sxs-lookup"><span data-stu-id="a8df8-154">You can also create notifications from here.</span></span> <span data-ttu-id="a8df8-155">Se pueden enviar notificaciones a través de **CORREO ELECTRÓNICO** o **SNMP** cuando se producen combinaciones de alerta/gravedad específicas.</span><span class="sxs-lookup"><span data-stu-id="a8df8-155">Notifications can be sent via **EMAIL** or **SNMP** when specific alert/severity combinations occur.</span></span> <span data-ttu-id="a8df8-156">Por ejemplo, puede enviar un mensaje de correo electrónico cuando se da alguna de las alertas de Hola Hola **YARN predeterminado** grupo se establece demasiado**crítico**.</span><span class="sxs-lookup"><span data-stu-id="a8df8-156">For example, you can send an email message when any of hello alerts in hello **YARN Default** group is set too**Critical**.</span></span>

![cuadro de diálogo Crear alerta](./media/hdinsight-hadoop-manage-ambari/create-alert-notification.png)

<span data-ttu-id="a8df8-158">Por último, al seleccionar __Administrar configuración de la alerta__ de hello __acciones__ menú permite un número de hello tooset de veces que debe aparecer una alerta antes de enviar una notificación.</span><span class="sxs-lookup"><span data-stu-id="a8df8-158">Finally, selecting __Manage Alert Settings__ from hello __Actions__ menu allows you tooset hello number of times an alert must occur before a notification is sent.</span></span> <span data-ttu-id="a8df8-159">Esta configuración puede ser notificaciones tooprevent usado para errores transitorios.</span><span class="sxs-lookup"><span data-stu-id="a8df8-159">This setting can be used tooprevent notifications for transient errors.</span></span>

### <a name="cluster"></a><span data-ttu-id="a8df8-160">Clúster</span><span class="sxs-lookup"><span data-stu-id="a8df8-160">Cluster</span></span>

<span data-ttu-id="a8df8-161">Hola **métricas** ficha del panel de hello contiene una serie de widgets que hacen que sea fácil toomonitor estado de hello del clúster de un vistazo.</span><span class="sxs-lookup"><span data-stu-id="a8df8-161">hello **Metrics** tab of hello dashboard contains a series of widgets that make it easy toomonitor hello status of your cluster at a glance.</span></span> <span data-ttu-id="a8df8-162">Varios widgets, como **CPU Usage**(Uso de CPU), proporcionan información adicional al hacer clic en ellos.</span><span class="sxs-lookup"><span data-stu-id="a8df8-162">Several widgets, such as **CPU Usage**, provide additional information when clicked.</span></span>

![panel con métricas](./media/hdinsight-hadoop-manage-ambari/metrics.png)

<span data-ttu-id="a8df8-164">Hola **Heatmaps** ficha muestra las métricas como color heatmaps, desde la toored verde.</span><span class="sxs-lookup"><span data-stu-id="a8df8-164">hello **Heatmaps** tab displays metrics as colored heatmaps, going from green toored.</span></span>

![panel con mapas térmicos](./media/hdinsight-hadoop-manage-ambari/heatmap.png)

<span data-ttu-id="a8df8-166">Para obtener más información sobre los nodos de hello en clúster de hello, seleccione **Hosts**.</span><span class="sxs-lookup"><span data-stu-id="a8df8-166">For more information on hello nodes within hello cluster, select **Hosts**.</span></span> <span data-ttu-id="a8df8-167">A continuación, seleccione el nodo específico de Hola que le interesen.</span><span class="sxs-lookup"><span data-stu-id="a8df8-167">Then select hello specific node you are interested in.</span></span>

![detalles del host](./media/hdinsight-hadoop-manage-ambari/host-details.png)

### <a name="services"></a><span data-ttu-id="a8df8-169">Services</span><span class="sxs-lookup"><span data-stu-id="a8df8-169">Services</span></span>

<span data-ttu-id="a8df8-170">Hola **servicios** sidebar en el panel de hello proporciona una perspectiva rápida de estado de hello de servicios de Hola que se ejecutan en el clúster de Hola.</span><span class="sxs-lookup"><span data-stu-id="a8df8-170">hello **Services** sidebar on hello dashboard provides quick insight into hello status of hello services running on hello cluster.</span></span> <span data-ttu-id="a8df8-171">Varios iconos son utilizados tooindicate estado o las acciones que se deben realizar.</span><span class="sxs-lookup"><span data-stu-id="a8df8-171">Various icons are used tooindicate status or actions that should be taken.</span></span> <span data-ttu-id="a8df8-172">Por ejemplo, se muestra un símbolo de reciclaje amarillo si un servicio necesita toobe recicla.</span><span class="sxs-lookup"><span data-stu-id="a8df8-172">For example, a yellow recycle symbol is displayed if a service needs toobe recycled.</span></span>

![barra lateral de servicios](./media/hdinsight-hadoop-manage-ambari/service-bar.png)

> [!NOTE]
> <span data-ttu-id="a8df8-174">Servicios de Hello muestra difieren entre las versiones y tipos de clúster de HDInsight.</span><span class="sxs-lookup"><span data-stu-id="a8df8-174">hello services displayed differ between HDInsight cluster types and versions.</span></span> <span data-ttu-id="a8df8-175">Servicios de Hello mostrados aquí pueden ser diferentes de servicios de Hola que se muestran para el clúster.</span><span class="sxs-lookup"><span data-stu-id="a8df8-175">hello services displayed here may be different than hello services displayed for your cluster.</span></span>

<span data-ttu-id="a8df8-176">Al seleccionar un servicio muestra la información más detallada en el servicio de Hola.</span><span class="sxs-lookup"><span data-stu-id="a8df8-176">Selecting a service displays more detailed information on hello service.</span></span>

![información de resumen de servicio](./media/hdinsight-hadoop-manage-ambari/service-details.png)

#### <a name="quick-links"></a><span data-ttu-id="a8df8-178">Vínculos rápidos</span><span class="sxs-lookup"><span data-stu-id="a8df8-178">Quick links</span></span>

<span data-ttu-id="a8df8-179">Algunos servicios de mostrar una **vínculos rápidos** vínculo situado en la parte superior de Hola de página de Hola.</span><span class="sxs-lookup"><span data-stu-id="a8df8-179">Some services display a **Quick Links** link at hello top of hello page.</span></span> <span data-ttu-id="a8df8-180">Esto puede resultar web específicos del servicio de tooaccess usa interfaces de usuario, como:</span><span class="sxs-lookup"><span data-stu-id="a8df8-180">This can be used tooaccess service-specific web UIs, such as:</span></span>

* <span data-ttu-id="a8df8-181">**Job History** : el historial de trabajos de MapReduce.</span><span class="sxs-lookup"><span data-stu-id="a8df8-181">**Job History** - MapReduce job history.</span></span>
* <span data-ttu-id="a8df8-182">**Resource Manager** : la interfaz de usuario del administrador de recursos de YARN.</span><span class="sxs-lookup"><span data-stu-id="a8df8-182">**Resource Manager** - YARN ResourceManager UI.</span></span>
* <span data-ttu-id="a8df8-183">**NameNode** : la interfaz de usuario de NameNode del Sistema de archivos distribuido de Hadoop (HDFS).</span><span class="sxs-lookup"><span data-stu-id="a8df8-183">**NameNode** - Hadoop Distributed File System (HDFS) NameNode UI.</span></span>
* <span data-ttu-id="a8df8-184">**Oozie Web UI** : interfaz de usuario de Oozie.</span><span class="sxs-lookup"><span data-stu-id="a8df8-184">**Oozie Web UI** - Oozie UI.</span></span>

<span data-ttu-id="a8df8-185">Si se selecciona cualquiera de estos vínculos, abre una nueva pestaña en el explorador, que muestra la página seleccionada Hola.</span><span class="sxs-lookup"><span data-stu-id="a8df8-185">Selecting any of these links opens a new tab in your browser, which displays hello selected page.</span></span>

> [!NOTE]
> <span data-ttu-id="a8df8-186">Seleccionar hello **vínculos rápidos** entrada para un servicio puede devolver un error "no se encontró el servidor".</span><span class="sxs-lookup"><span data-stu-id="a8df8-186">Selecting hello **Quick Links** entry for a service may return a "server not found" error.</span></span> <span data-ttu-id="a8df8-187">Si se produce este error, debe usar un túnel SSH al usar hello **vínculos rápidos** entrada para este servicio.</span><span class="sxs-lookup"><span data-stu-id="a8df8-187">If you encounter this error, you must use an SSH tunnel when using hello **Quick Links** entry for this service.</span></span> <span data-ttu-id="a8df8-188">Para más información, consulte [Uso de la tunelización SSH con HDInsight](hdinsight-linux-ambari-ssh-tunnel.md).</span><span class="sxs-lookup"><span data-stu-id="a8df8-188">For information, see [Use SSH Tunneling with HDInsight](hdinsight-linux-ambari-ssh-tunnel.md)</span></span>

## <a name="management"></a><span data-ttu-id="a8df8-189">Administración</span><span class="sxs-lookup"><span data-stu-id="a8df8-189">Management</span></span>

### <a name="ambari-users-groups-and-permissions"></a><span data-ttu-id="a8df8-190">Usuarios, grupos y permisos de Ambari</span><span class="sxs-lookup"><span data-stu-id="a8df8-190">Ambari users, groups, and permissions</span></span>

<span data-ttu-id="a8df8-191">Se puede trabajar con usuarios, grupos y permisos cuando se usa un clúster de HDInsight [unido a un dominio](hdinsight-domain-joined-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="a8df8-191">Working with users, groups, and permissions are supported when using a [domain joined](hdinsight-domain-joined-introduction.md) HDInsight cluster.</span></span> <span data-ttu-id="a8df8-192">Para obtener información sobre el uso de hello Ambari IU de administración en un clúster Unidos a un dominio, consulte [administrar clústeres de HDInsight Unidos al dominio](hdinsight-domain-joined-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="a8df8-192">For information on using hello Ambari Management UI on a domain-joined cluster, see [Manage domain-joined HDInsight clusters](hdinsight-domain-joined-introduction.md).</span></span>

> [!WARNING]
> <span data-ttu-id="a8df8-193">No se cambie la contraseña de Hola de guardián de hello Ambari (hdinsightwatchdog) en el clúster de HDInsight basados en Linux.</span><span class="sxs-lookup"><span data-stu-id="a8df8-193">Do not change hello password of hello Ambari watchdog (hdinsightwatchdog) on your Linux-based HDInsight cluster.</span></span> <span data-ttu-id="a8df8-194">Cambiar los saltos de contraseña Hola Hola acciones de script de capacidad toouse o realizar operaciones de escala con el clúster.</span><span class="sxs-lookup"><span data-stu-id="a8df8-194">Changing hello password breaks hello ability toouse script actions or perform scaling operations with your cluster.</span></span>

### <a name="hosts"></a><span data-ttu-id="a8df8-195">Hosts</span><span class="sxs-lookup"><span data-stu-id="a8df8-195">Hosts</span></span>

<span data-ttu-id="a8df8-196">Hola **Hosts** página enumera todos los hosts en clúster de Hola.</span><span class="sxs-lookup"><span data-stu-id="a8df8-196">hello **Hosts** page lists all hosts in hello cluster.</span></span> <span data-ttu-id="a8df8-197">toomanage hosts, siga estos pasos.</span><span class="sxs-lookup"><span data-stu-id="a8df8-197">toomanage hosts, follow these steps.</span></span>

![página de hosts](./media/hdinsight-hadoop-manage-ambari/hosts.png)

> [!NOTE]
> <span data-ttu-id="a8df8-199">No se debe agregar, retirar o volver a programar un host con los clústeres de HDInsight.</span><span class="sxs-lookup"><span data-stu-id="a8df8-199">Adding, decommissioning, and recommissioning a host should not be used with HDInsight clusters.</span></span>

1. <span data-ttu-id="a8df8-200">Seleccione un host de Hola que desea toomanage.</span><span class="sxs-lookup"><span data-stu-id="a8df8-200">Select hello host that you wish toomanage.</span></span>

2. <span data-ttu-id="a8df8-201">Hola de uso **acciones** acción de hello tooselect de menú que desea tooperform:</span><span class="sxs-lookup"><span data-stu-id="a8df8-201">Use hello **Actions** menu tooselect hello action that you wish tooperform:</span></span>

   * <span data-ttu-id="a8df8-202">**Iniciar todos los componentes** -iniciar todos los componentes en el host de Hola.</span><span class="sxs-lookup"><span data-stu-id="a8df8-202">**Start all components** - Start all components on hello host.</span></span>

   * <span data-ttu-id="a8df8-203">**Detener todos los componentes** -detener todos los componentes en el host de Hola.</span><span class="sxs-lookup"><span data-stu-id="a8df8-203">**Stop all components** - Stop all components on hello host.</span></span>

   * <span data-ttu-id="a8df8-204">**Reinicie todos los componentes** : detener e iniciar todos los componentes de host de Hola.</span><span class="sxs-lookup"><span data-stu-id="a8df8-204">**Restart all components** - Stop and start all components on hello host.</span></span>

   * <span data-ttu-id="a8df8-205">**Activar el modo de mantenimiento** -suprime las alertas para el host de Hola.</span><span class="sxs-lookup"><span data-stu-id="a8df8-205">**Turn on maintenance mode** - Suppresses alerts for hello host.</span></span> <span data-ttu-id="a8df8-206">Este modo se debería habilitar si va a realizar acciones que generan alertas.</span><span class="sxs-lookup"><span data-stu-id="a8df8-206">This mode should be enabled if you are performing actions that generate alerts.</span></span> <span data-ttu-id="a8df8-207">Por ejemplo, detener e iniciar un servicio.</span><span class="sxs-lookup"><span data-stu-id="a8df8-207">For example, stopping and starting a service.</span></span>

   * <span data-ttu-id="a8df8-208">**Desactiva el modo de mantenimiento** -devuelve Hola toonormal las alertas de host.</span><span class="sxs-lookup"><span data-stu-id="a8df8-208">**Turn off maintenance mode** - Returns hello host toonormal alerting.</span></span>

   * <span data-ttu-id="a8df8-209">**Detener** -DataNode se detiene o NodeManagers en host Hola.</span><span class="sxs-lookup"><span data-stu-id="a8df8-209">**Stop** - Stops DataNode or NodeManagers on hello host.</span></span>

   * <span data-ttu-id="a8df8-210">**Iniciar** -inicia DataNode o NodeManagers en host Hola.</span><span class="sxs-lookup"><span data-stu-id="a8df8-210">**Start** - Starts DataNode or NodeManagers on hello host.</span></span>

   * <span data-ttu-id="a8df8-211">**Reinicie** -detiene e inicia DataNode o NodeManagers en host Hola.</span><span class="sxs-lookup"><span data-stu-id="a8df8-211">**Restart** - Stops and starts DataNode or NodeManagers on hello host.</span></span>

   * <span data-ttu-id="a8df8-212">**Retirar** -quita un host de clúster de Hola.</span><span class="sxs-lookup"><span data-stu-id="a8df8-212">**Decommission** - Removes a host from hello cluster.</span></span>

     > [!NOTE]
     > <span data-ttu-id="a8df8-213">No use esta acción en clústeres de HDInsight.</span><span class="sxs-lookup"><span data-stu-id="a8df8-213">Do not use this action on HDInsight clusters.</span></span>

   * <span data-ttu-id="a8df8-214">**Recommission** -agrega un clúster de toohello host previamente dado de baja.</span><span class="sxs-lookup"><span data-stu-id="a8df8-214">**Recommission** - Adds a previously decommissioned host toohello cluster.</span></span>

     > [!NOTE]
     > <span data-ttu-id="a8df8-215">No use esta acción en clústeres de HDInsight.</span><span class="sxs-lookup"><span data-stu-id="a8df8-215">Do not use this action on HDInsight clusters.</span></span>

### <span data-ttu-id="a8df8-216"><a id="service"></a>Servicios</span><span class="sxs-lookup"><span data-stu-id="a8df8-216"><a id="service"></a>Services</span></span>

<span data-ttu-id="a8df8-217">De hello **panel** o **servicios** , utilice hello **acciones** situado en la parte inferior de Hola de lista de hello de servicios toostop e iniciar los servicios.</span><span class="sxs-lookup"><span data-stu-id="a8df8-217">From hello **Dashboard** or **Services** page, use hello **Actions** button at hello bottom of hello list of services toostop and start all services.</span></span>

![Service Actions](./media/hdinsight-hadoop-manage-ambari/service-actions.png)

> [!WARNING]
> <span data-ttu-id="a8df8-219">Mientras **Agregar servicio** aparece en este menú, no debe ser clúster de HDInsight de toohello de servicios de tooadd usado.</span><span class="sxs-lookup"><span data-stu-id="a8df8-219">While **Add Service** is listed in this menu, it should not be used tooadd services toohello HDInsight cluster.</span></span> <span data-ttu-id="a8df8-220">Se deben agregar nuevos servicios deben mediante una acción de script durante el aprovisionamiento del clúster.</span><span class="sxs-lookup"><span data-stu-id="a8df8-220">New services should be added using a Script Action during cluster provisioning.</span></span> <span data-ttu-id="a8df8-221">Para obtener más información sobre el uso de las acciones de script, consulte [Personalización de clústeres de HDInsight mediante la acción de script](hdinsight-hadoop-customize-cluster-linux.md).</span><span class="sxs-lookup"><span data-stu-id="a8df8-221">For more information on using Script Actions, see [Customize HDInsight clusters using Script Actions](hdinsight-hadoop-customize-cluster-linux.md).</span></span>

<span data-ttu-id="a8df8-222">Mientras hello **acciones** botón puede reiniciar todos los servicios, a menudo desea toostart, detener o reiniciar un servicio específico.</span><span class="sxs-lookup"><span data-stu-id="a8df8-222">While hello **Actions** button can restart all services, often you want toostart, stop, or restart a specific service.</span></span> <span data-ttu-id="a8df8-223">Use Hola siguientes pasos se tooperform acciones en un servicio individual:</span><span class="sxs-lookup"><span data-stu-id="a8df8-223">Use hello following steps tooperform actions on an individual service:</span></span>

1. <span data-ttu-id="a8df8-224">De hello **panel** o **Services** , seleccione un servicio.</span><span class="sxs-lookup"><span data-stu-id="a8df8-224">From hello **Dashboard** or **Services** page, select a service.</span></span>

2. <span data-ttu-id="a8df8-225">De arriba Hola de hello **resumen** , utilice hello **acciones de servicio** botón y seleccione Hola acción tootake.</span><span class="sxs-lookup"><span data-stu-id="a8df8-225">From hello top of hello **Summary** tab, use hello **Service Actions** button and select hello action tootake.</span></span> <span data-ttu-id="a8df8-226">Esto reinicia el servicio de hello en todos los nodos.</span><span class="sxs-lookup"><span data-stu-id="a8df8-226">This restarts hello service on all nodes.</span></span>

    ![acción de servicio](./media/hdinsight-hadoop-manage-ambari/individual-service-actions.png)

   > [!NOTE]
   > <span data-ttu-id="a8df8-228">Reiniciar algunos servicios mientras se está ejecutando el clúster de hello puede generar alertas.</span><span class="sxs-lookup"><span data-stu-id="a8df8-228">Restarting some services while hello cluster is running may generate alerts.</span></span> <span data-ttu-id="a8df8-229">tooavoid de alertas, puede usar hello **acciones de servicio** botón tooenable **modo de mantenimiento** para servicio de hello antes de realizar el reinicio de Hola.</span><span class="sxs-lookup"><span data-stu-id="a8df8-229">tooavoid alerts, you can use hello **Service Actions** button tooenable **Maintenance mode** for hello service before performing hello restart.</span></span>

3. <span data-ttu-id="a8df8-230">Una vez que se ha seleccionado una acción, Hola **op #** entrada en la parte superior de Hola de hello página incrementos tooshow que está en curso una operación en segundo plano.</span><span class="sxs-lookup"><span data-stu-id="a8df8-230">Once an action has been selected, hello **# op** entry at hello top of hello page increments tooshow that a background operation is occurring.</span></span> <span data-ttu-id="a8df8-231">Si configura toodisplay, se muestra la lista de Hola de operaciones en segundo plano.</span><span class="sxs-lookup"><span data-stu-id="a8df8-231">If configured toodisplay, hello list of background operations is displayed.</span></span>

   > [!NOTE]
   > <span data-ttu-id="a8df8-232">Si habilitó **modo de mantenimiento** para el servicio de hello, recuerde toodisable mediante hello **acciones de servicio** botón una vez que haya finalizado la operación de Hola.</span><span class="sxs-lookup"><span data-stu-id="a8df8-232">If you enabled **Maintenance mode** for hello service, remember toodisable it by using hello **Service Actions** button once hello operation has finished.</span></span>

<span data-ttu-id="a8df8-233">tooconfigure un servicio, utilice Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="a8df8-233">tooconfigure a service, use hello following steps:</span></span>

1. <span data-ttu-id="a8df8-234">De hello **panel** o **Services** , seleccione un servicio.</span><span class="sxs-lookup"><span data-stu-id="a8df8-234">From hello **Dashboard** or **Services** page, select a service.</span></span>

2. <span data-ttu-id="a8df8-235">Seleccione hello **configuraciones** muestra la configuración actual de Hola de ficha.</span><span class="sxs-lookup"><span data-stu-id="a8df8-235">Select hello **Configs** tab. hello current configuration is displayed.</span></span> <span data-ttu-id="a8df8-236">También aparecerá una lista de las configuraciones anteriores.</span><span class="sxs-lookup"><span data-stu-id="a8df8-236">A list of previous configurations is also displayed.</span></span>

    ![configuraciones](./media/hdinsight-hadoop-manage-ambari/service-configs.png)

3. <span data-ttu-id="a8df8-238">Usar configuración de hello toomodify de hello campos que se muestran y, a continuación, seleccione **guardar**.</span><span class="sxs-lookup"><span data-stu-id="a8df8-238">Use hello fields displayed toomodify hello configuration, and then select **Save**.</span></span> <span data-ttu-id="a8df8-239">O seleccione una configuración anterior y, a continuación, seleccione **convertir en actual** tooroll realizar copia de toohello de configuración anterior.</span><span class="sxs-lookup"><span data-stu-id="a8df8-239">Or select a previous configuration and then select **Make current** tooroll back toohello previous settings.</span></span>

## <a name="ambari-views"></a><span data-ttu-id="a8df8-240">Vistas de Ambari</span><span class="sxs-lookup"><span data-stu-id="a8df8-240">Ambari views</span></span>

<span data-ttu-id="a8df8-241">Ambari vistas permiten a los desarrolladores tooplug elementos de interfaz de usuario en hello Ambari Web UI con hello [Ambari vistas Framework](https://cwiki.apache.org/confluence/display/AMBARI/Views).</span><span class="sxs-lookup"><span data-stu-id="a8df8-241">Ambari Views allow developers tooplug UI elements into hello Ambari Web UI using hello [Ambari Views Framework](https://cwiki.apache.org/confluence/display/AMBARI/Views).</span></span> <span data-ttu-id="a8df8-242">HDInsight proporciona Hola siguientes vistas con tipos de clúster de Hadoop:</span><span class="sxs-lookup"><span data-stu-id="a8df8-242">HDInsight provides hello following views with Hadoop cluster types:</span></span>

* <span data-ttu-id="a8df8-243">Administrador de cola de hilo: Administrador de cola de hello proporciona una interfaz de usuario simple para ver y modificar las colas YARN.</span><span class="sxs-lookup"><span data-stu-id="a8df8-243">Yarn Queue Manager: hello queue manager provides a simple UI for viewing and modifying YARN queues.</span></span>

* <span data-ttu-id="a8df8-244">Vista de Hive: Hola Hive vista permite consultas de Hive toorun directamente desde el explorador web.</span><span class="sxs-lookup"><span data-stu-id="a8df8-244">Hive View: hello Hive View allows you toorun Hive queries directly from your web browser.</span></span> <span data-ttu-id="a8df8-245">Puede guardar consultas, ver los resultados, guardar los resultados de almacenamiento del clúster toohello o descargar el sistema local de tooyour de resultados.</span><span class="sxs-lookup"><span data-stu-id="a8df8-245">You can save queries, view results, save results toohello cluster storage, or download results tooyour local system.</span></span> <span data-ttu-id="a8df8-246">Para más información sobre el uso de vistas de Hive, consulte [Uso de vistas de Hive con HDInsight](hdinsight-hadoop-use-hive-ambari-view.md).</span><span class="sxs-lookup"><span data-stu-id="a8df8-246">For more information on using Hive Views, see [Use Hive Views with HDInsight](hdinsight-hadoop-use-hive-ambari-view.md).</span></span>

* <span data-ttu-id="a8df8-247">La vista Tez: Hola Tez vista permite toobetter entender y optimizar los trabajos.</span><span class="sxs-lookup"><span data-stu-id="a8df8-247">Tez View: hello Tez View allows you toobetter understand and optimize jobs.</span></span> <span data-ttu-id="a8df8-248">Puede ver información sobre cómo se ejecutan los trabajos de Tez y qué recursos se usan.</span><span class="sxs-lookup"><span data-stu-id="a8df8-248">You can view information on how Tez jobs are executed and what resources are used.</span></span>
