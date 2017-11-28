---
title: aaaUse Phoenix Apache y ardilla con basados en Windows Azure HDInsight | Documentos de Microsoft
description: "Obtenga información acerca de cómo toouse Phoenix Apache en HDInsight y cómo tooinstall y configurar ardilla en el clúster de estación de trabajo tooconnect tooan HBase en HDInsight."
services: hdinsight
documentationcenter: 
author: mumian
manager: jhubbard
editor: cgronlun
ms.assetid: 1a756e98-75c1-44cd-a178-c5119683b7b7
ms.service: hdinsight
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 05/25/2017
ms.author: jgao
ROBOTS: NOINDEX
ms.openlocfilehash: 147ac35fa882fd1bedbc5361ac804c36a4d56de1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="use-apache-phoenix-and-squirrel-with-windows-based-hbase-clusters-in-hdinsight"></a><span data-ttu-id="eff41-103">Uso de Apache Phoenix y SQuirreL con clústeres de HBase basados en Windows en HDinsight</span><span class="sxs-lookup"><span data-stu-id="eff41-103">Use Apache Phoenix and SQuirreL with Windows-based HBase clusters in HDInsight</span></span>
<span data-ttu-id="eff41-104">Obtenga información acerca de cómo toouse [Apache Phoenix](http://phoenix.apache.org/) en HDInsight y cómo tooinstall y configurar ardilla en el clúster de estación de trabajo tooconnect tooan HBase en HDInsight.</span><span class="sxs-lookup"><span data-stu-id="eff41-104">Learn how toouse [Apache Phoenix](http://phoenix.apache.org/) in HDInsight, and how tooinstall and configure SQuirreL on your workstation tooconnect tooan HBase cluster in HDInsight.</span></span> <span data-ttu-id="eff41-105">Para obtener más información acerca de Phoenix, consulte [Phoenix en 15 minutos o menos](http://phoenix.apache.org/Phoenix-in-15-minutes-or-less.html).</span><span class="sxs-lookup"><span data-stu-id="eff41-105">For more information about Phoenix, see [Phoenix in 15 minutes or less](http://phoenix.apache.org/Phoenix-in-15-minutes-or-less.html).</span></span> <span data-ttu-id="eff41-106">Hola gramática de Phoenix, encontrará [gramática de Phoenix](http://phoenix.apache.org/language/index.html).</span><span class="sxs-lookup"><span data-stu-id="eff41-106">For hello Phoenix grammar, see [Phoenix Grammar](http://phoenix.apache.org/language/index.html).</span></span>

> [!NOTE]
> <span data-ttu-id="eff41-107">Para obtener información de versión de Phoenix en HDInsight de hello, consulte [cuáles son las novedades en las versiones de clúster de Hadoop Hola proporcionadas por HDInsight?](hdinsight-component-versioning.md).</span><span class="sxs-lookup"><span data-stu-id="eff41-107">For hello Phoenix version information in HDInsight, see [What's new in hello Hadoop cluster versions provided by HDInsight?](hdinsight-component-versioning.md).</span></span>
>

> [!IMPORTANT]
> <span data-ttu-id="eff41-108">Hola pasos de este trabajo sólo de documento para clústeres de HDInsight basados en Windows.</span><span class="sxs-lookup"><span data-stu-id="eff41-108">hello steps in this document only work for Windows-based HDInsight clusters.</span></span> <span data-ttu-id="eff41-109">HDInsight solo está disponible en Windows en versiones inferiores a la 3.4.</span><span class="sxs-lookup"><span data-stu-id="eff41-109">HDInsight is only available on Windows for versions lower than HDInsight 3.4.</span></span> <span data-ttu-id="eff41-110">Linux es Hola único sistema operativo usado en HDInsight versión 3.4 o superior.</span><span class="sxs-lookup"><span data-stu-id="eff41-110">Linux is hello only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="eff41-111">Consulte la información sobre la [retirada de HDInsight en Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="eff41-111">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span> <span data-ttu-id="eff41-112">Para más información sobre el uso de Phoenix en HDInsight basado en Linux, consulte [Use Apache Phoenix with Linux-based HBase clusters in HDinsight](hdinsight-hbase-phoenix-squirrel-linux.md)(Uso de Apache Phoenix con clústeres de HBase basados en Linux en HDinsight).</span><span class="sxs-lookup"><span data-stu-id="eff41-112">For information on using Phoenix on Linux-based HDInsight, see [Use Apache Phoenix with Linux-based HBase clusters in HDInsight](hdinsight-hbase-phoenix-squirrel-linux.md).</span></span>
>



## <a name="use-sqlline"></a><span data-ttu-id="eff41-113">Uso de SQLLine</span><span class="sxs-lookup"><span data-stu-id="eff41-113">Use SQLLine</span></span>
<span data-ttu-id="eff41-114">[SQLLine](http://sqlline.sourceforge.net/) es un tooexecute de utilidad de línea de comandos SQL.</span><span class="sxs-lookup"><span data-stu-id="eff41-114">[SQLLine](http://sqlline.sourceforge.net/) is a command line utility tooexecute SQL.</span></span>

### <a name="prerequisites"></a><span data-ttu-id="eff41-115">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="eff41-115">Prerequisites</span></span>
<span data-ttu-id="eff41-116">Para poder usar SQLLine, debe tener el siguiente hello:</span><span class="sxs-lookup"><span data-stu-id="eff41-116">Before you can use SQLLine, you must have hello following:</span></span>

* <span data-ttu-id="eff41-117">**Un clúster de HBase en HDInsight**.</span><span class="sxs-lookup"><span data-stu-id="eff41-117">**A HBase cluster in HDInsight**.</span></span> <span data-ttu-id="eff41-118">Para obtener información sobre el aprovisionamiento del clúster de HBase, consulte [Introducción a HBase Apache en HDInsight][hdinsight-hbase-get-started].</span><span class="sxs-lookup"><span data-stu-id="eff41-118">For information on provision HBase cluster, see [Get started with Apache HBase in HDInsight][hdinsight-hbase-get-started].</span></span>
* <span data-ttu-id="eff41-119">**Conectar el clúster de HBase toohello a través del protocolo de escritorio remoto de hello**.</span><span class="sxs-lookup"><span data-stu-id="eff41-119">**Connect toohello HBase cluster via hello remote desktop protocol**.</span></span> <span data-ttu-id="eff41-120">Para obtener instrucciones, consulte [Hadoop administrar clústeres de HDInsight mediante el uso de hello Portal clásico de Azure][hdinsight-manage-portal].</span><span class="sxs-lookup"><span data-stu-id="eff41-120">For instructions, see [Manage Hadoop clusters in HDInsight by using hello Azure Classic Portal][hdinsight-manage-portal].</span></span>

<span data-ttu-id="eff41-121">**toofind el nombre de host de Hola**</span><span class="sxs-lookup"><span data-stu-id="eff41-121">**toofind out hello host name**</span></span>

1. <span data-ttu-id="eff41-122">Abra **línea de comandos de Hadoop** de escritorio de Hola.</span><span class="sxs-lookup"><span data-stu-id="eff41-122">Open **Hadoop Command Line** from hello desktop.</span></span>
2. <span data-ttu-id="eff41-123">Ejecute hello después de sufijo DNS de comando tooget hello:</span><span class="sxs-lookup"><span data-stu-id="eff41-123">Run hello following command tooget hello DNS suffix:</span></span>

        ipconfig

    <span data-ttu-id="eff41-124">Escriba el **sufijo DNS específico de la conexión**.</span><span class="sxs-lookup"><span data-stu-id="eff41-124">Write down **Connection-specific DNS Suffix**.</span></span> <span data-ttu-id="eff41-125">Por ejemplo, *myhbasecluster.f5.internal.cloudapp.net*.</span><span class="sxs-lookup"><span data-stu-id="eff41-125">For example, *myhbasecluster.f5.internal.cloudapp.net*.</span></span> <span data-ttu-id="eff41-126">Cuando se conecta el clúster de HBase tooan, necesitará tooconnect tooone de Zookeepers hello mediante FQDN.</span><span class="sxs-lookup"><span data-stu-id="eff41-126">When you connect tooan HBase cluster, you will need tooconnect tooone of hello Zookeepers using FQDN.</span></span> <span data-ttu-id="eff41-127">Cada clúster de HDInsight tiene 3 Zookeepers.</span><span class="sxs-lookup"><span data-stu-id="eff41-127">Each HDInsight cluster has 3 Zookeepers.</span></span> <span data-ttu-id="eff41-128">Son *zookeeper0*, *zookeeper1* y *zookeeper2*.</span><span class="sxs-lookup"><span data-stu-id="eff41-128">They are *zookeeper0*, *zookeeper1*, and *zookeeper2*.</span></span> <span data-ttu-id="eff41-129">Hello FQDN será similar a *zookeeper2.myhbasecluster.f5.internal.cloudapp.net*.</span><span class="sxs-lookup"><span data-stu-id="eff41-129">hello FQDN will be something like *zookeeper2.myhbasecluster.f5.internal.cloudapp.net*.</span></span>

<span data-ttu-id="eff41-130">**toouse SQLLine**</span><span class="sxs-lookup"><span data-stu-id="eff41-130">**toouse SQLLine**</span></span>

1. <span data-ttu-id="eff41-131">Abra **línea de comandos de Hadoop** de escritorio de Hola.</span><span class="sxs-lookup"><span data-stu-id="eff41-131">Open **Hadoop Command Line** from hello desktop.</span></span>
2. <span data-ttu-id="eff41-132">Ejecute hello después comandos tooopen SQLLine:</span><span class="sxs-lookup"><span data-stu-id="eff41-132">Run hello following commands tooopen SQLLine:</span></span>

        cd %phoenix_home%\bin
        sqlline.py [hello FQDN of one of hello Zookeepers]

    ![HDInsight hbase phoenix sqlline][hdinsight-hbase-phoenix-sqlline]

    <span data-ttu-id="eff41-134">comandos de Hola que se usan en el ejemplo hello:</span><span class="sxs-lookup"><span data-stu-id="eff41-134">hello commands used in hello sample:</span></span>

        CREATE TABLE Company (COMPANY_ID INTEGER PRIMARY KEY, NAME VARCHAR(225));

        !tables

        UPSERT INTO Company VALUES(1, 'Microsoft');

        SELECT * FROM Company;

<span data-ttu-id="eff41-135">Para más información, consulte el [manual de SQLLine](http://sqlline.sourceforge.net/#manual) y la [gramática de Phoenix](http://phoenix.apache.org/language/index.html).</span><span class="sxs-lookup"><span data-stu-id="eff41-135">For more information, see [SQLLine manual](http://sqlline.sourceforge.net/#manual) and [Phoenix Grammar](http://phoenix.apache.org/language/index.html).</span></span>

## <a name="use-squirrel"></a><span data-ttu-id="eff41-136">Uso de SQuirreL</span><span class="sxs-lookup"><span data-stu-id="eff41-136">Use SQuirreL</span></span>
<span data-ttu-id="eff41-137">[Ardilla SQL Client](http://squirrel-sql.sourceforge.net/) es un programa Java gráfico que le permiten tooview estructura de Hola de una base de datos compatible con JDBC, examinar los datos de hello en tablas, emitir comandos SQL etcetera. Puede ser usado tooconnect tooApache Phoenix en HDInsight.</span><span class="sxs-lookup"><span data-stu-id="eff41-137">[SQuirreL SQL Client](http://squirrel-sql.sourceforge.net/) is a graphical Java program that will allow you tooview hello structure of a JDBC compliant database, browse hello data in tables, issue SQL commands etc. It can be used tooconnect tooApache Phoenix on HDInsight.</span></span>

<span data-ttu-id="eff41-138">Esta sección muestra cómo tooinstall y configurar ardilla en su estación de trabajo tooconnect tooan clúster de HBase en HDInsight a través de VPN.</span><span class="sxs-lookup"><span data-stu-id="eff41-138">This section shows you how tooinstall and configure SQuirreL on your workstation tooconnect tooan HBase cluster in HDInsight via VPN.</span></span>

### <a name="prerequisites"></a><span data-ttu-id="eff41-139">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="eff41-139">Prerequisites</span></span>
<span data-ttu-id="eff41-140">Antes de seguir los procedimientos de hello, debe tener el siguiente hello:</span><span class="sxs-lookup"><span data-stu-id="eff41-140">Before following hello procedures, you must have hello following:</span></span>

* <span data-ttu-id="eff41-141">Un clúster de HBase implementa tooan red virtual de Azure con una máquina virtual DNS.</span><span class="sxs-lookup"><span data-stu-id="eff41-141">An HBase cluster deployed tooan Azure virtual network with a DNS virtual machine.</span></span>  <span data-ttu-id="eff41-142">Para obtener instrucciones, consulte [Creación de clústeres de HBase en Azure Virtual Network][hdinsight-hbase-provision-vnet].</span><span class="sxs-lookup"><span data-stu-id="eff41-142">For instructions, see [Create HBase clusters on Azure Virtual Network][hdinsight-hbase-provision-vnet].</span></span>

* <span data-ttu-id="eff41-143">Obtiene el sufijo DNS específico de la conexión de hello HBase clúster clúster.</span><span class="sxs-lookup"><span data-stu-id="eff41-143">Get hello HBase cluster cluster Connection-specific DNS suffix.</span></span> <span data-ttu-id="eff41-144">tooget lo, RDP en clúster de hello, y, a continuación, ejecutar IPConfig.</span><span class="sxs-lookup"><span data-stu-id="eff41-144">tooget it, RDP into hello cluster, and then run IPConfig.</span></span>  <span data-ttu-id="eff41-145">sufijo DNS de Hello es similar a:</span><span class="sxs-lookup"><span data-stu-id="eff41-145">hello DNS suffix is similar to:</span></span>

        myhbase.b7.internal.cloudapp.net
* <span data-ttu-id="eff41-146">Descargue e instale [Microsoft Visual Studio Express para escritorio de Windows](https://www.visualstudio.com/products/visual-studio-express-vs.aspx) en la estación de trabajo.</span><span class="sxs-lookup"><span data-stu-id="eff41-146">Download and install [Microsoft Visual Studio Express for Windows Desktop](https://www.visualstudio.com/products/visual-studio-express-vs.aspx) on your workstation.</span></span> <span data-ttu-id="eff41-147">Necesitará makecert de hello paquete toocreate su certificado.</span><span class="sxs-lookup"><span data-stu-id="eff41-147">You will need makecert from hello package toocreate your certificate.</span></span>  
* <span data-ttu-id="eff41-148">Descargue e instale [Java Runtime Environment](http://www.oracle.com/technetwork/java/javase/downloads/jre7-downloads-1880261.html) en su estación de trabajo.</span><span class="sxs-lookup"><span data-stu-id="eff41-148">Download and install [Java Runtime Environment](http://www.oracle.com/technetwork/java/javase/downloads/jre7-downloads-1880261.html) on your workstation.</span></span>  <span data-ttu-id="eff41-149">La versión de cliente SQL SQuirreL 3.0 y superiores requieren la versión 1.6 o superior de JRE.</span><span class="sxs-lookup"><span data-stu-id="eff41-149">SQuirreL SQL client version 3.0 and higher requires JRE version 1.6 or higher.</span></span>  

### <a name="configure-a-point-to-site-vpn-connection-toohello-azure-virtual-network"></a><span data-ttu-id="eff41-150">Configurar una toohello de conexión de Point-to-Site VPN red virtual de Azure</span><span class="sxs-lookup"><span data-stu-id="eff41-150">Configure a Point-to-Site VPN connection toohello Azure virtual network</span></span>
<span data-ttu-id="eff41-151">Hay tres pasos implicados en la configuración de una conexión VPN de punto a sitio:</span><span class="sxs-lookup"><span data-stu-id="eff41-151">There are 3 steps involved configuring a point-to-site VPN connection:</span></span>

1. [<span data-ttu-id="eff41-152">Configuración de una red virtual y una puerta de enlace de enrutamiento dinámico</span><span class="sxs-lookup"><span data-stu-id="eff41-152">Configure a virtual network and a dynamic routing gateway</span></span>](#Configure-a-virtual-network-and-a-dynamic-routing-gateway)
2. [<span data-ttu-id="eff41-153">Creación de certificados</span><span class="sxs-lookup"><span data-stu-id="eff41-153">Create your certificates</span></span>](#Create-your-certificates)
3. [<span data-ttu-id="eff41-154">Configuración del cliente VPN</span><span class="sxs-lookup"><span data-stu-id="eff41-154">Configure your VPN client</span></span>](#Configure-your-VPN-client)

<span data-ttu-id="eff41-155">Vea [configurar una tooan de conexión de Point-to-Site VPN red Virtual de Azure](../vpn-gateway/vpn-gateway-point-to-site-create.md) para obtener más información.</span><span class="sxs-lookup"><span data-stu-id="eff41-155">See [Configure a Point-to-Site VPN connection tooan Azure Virtual Network](../vpn-gateway/vpn-gateway-point-to-site-create.md) for more information.</span></span>

#### <a name="configure-a-virtual-network-and-a-dynamic-routing-gateway"></a><span data-ttu-id="eff41-156">Configuración de una red virtual y una puerta de enlace de enrutamiento dinámico</span><span class="sxs-lookup"><span data-stu-id="eff41-156">Configure a virtual network and a dynamic routing gateway</span></span>
<span data-ttu-id="eff41-157">Asegurarse de haber aprovisionado un clúster de HBase en una red virtual de Azure (consulte requisitos previos de Hola de esta sección).</span><span class="sxs-lookup"><span data-stu-id="eff41-157">Assure you have provisioned an HBase cluster in an Azure virtual network (see hello prerequisites for this section).</span></span> <span data-ttu-id="eff41-158">Hola siguiente paso es tooconfigure una conexión punto a sitio.</span><span class="sxs-lookup"><span data-stu-id="eff41-158">hello next step is tooconfigure a point-to-site connection.</span></span>

<span data-ttu-id="eff41-159">**conectividad de punto a sitio hello tooconfigure**</span><span class="sxs-lookup"><span data-stu-id="eff41-159">**tooconfigure hello point-to-site connectivity**</span></span>

1. <span data-ttu-id="eff41-160">Inicie sesión en toohello [Portal clásico de Azure][azure-portal].</span><span class="sxs-lookup"><span data-stu-id="eff41-160">Sign in toohello [Azure Classic Portal][azure-portal].</span></span>
2. <span data-ttu-id="eff41-161">Hola izquierda, haga clic en **redes**.</span><span class="sxs-lookup"><span data-stu-id="eff41-161">On hello left, click **NETWORKS**.</span></span>
3. <span data-ttu-id="eff41-162">Haga clic en la red virtual de Hola que ha creado (consulte [HBase aprovisionar clústeres en la red Virtual de Azure][hdinsight-hbase-provision-vnet]).</span><span class="sxs-lookup"><span data-stu-id="eff41-162">Click hello virtual network you have created (see [Provision HBase clusters on Azure Virtual Network][hdinsight-hbase-provision-vnet]).</span></span>
4. <span data-ttu-id="eff41-163">Haga clic en **configurar** desde la parte superior de Hola.</span><span class="sxs-lookup"><span data-stu-id="eff41-163">Click **CONFIGURE** from hello top.</span></span>
5. <span data-ttu-id="eff41-164">Hola **conectividad punto a sitio** sección, seleccione **configurar la conectividad punto a sitio**.</span><span class="sxs-lookup"><span data-stu-id="eff41-164">In hello **point-to-site connectivity** section, select **Configure point-to-site connectivity**.</span></span>
6. <span data-ttu-id="eff41-165">Configurar **IP de inicio** y **CIDR** intervalo de direcciones IP toospecify Hola desde el que los clientes VPN recibirán una dirección IP de direcciones cuando se conecta.</span><span class="sxs-lookup"><span data-stu-id="eff41-165">Configure **STARTING IP** and **CIDR** toospecify hello IP address range from which your VPN clients will receive an IP address when connected.</span></span> <span data-ttu-id="eff41-166">intervalo de Hello no puede solaparse con cualquiera de hello intervalos en sus instalaciones de red y Hola red virtual de Azure que se conectará a.</span><span class="sxs-lookup"><span data-stu-id="eff41-166">hello range cannot overlap with any of hello ranges located on your on-premises network and hello Azure virtual network you will be connecting to.</span></span> <span data-ttu-id="eff41-167">Por ejemplo.</span><span class="sxs-lookup"><span data-stu-id="eff41-167">For example.</span></span> <span data-ttu-id="eff41-168">Si seleccionó 10.0.0.0/20 para la red virtual de hello, puede seleccionar 10.1.0.0/24 de espacios de direcciones de cliente de Hola.</span><span class="sxs-lookup"><span data-stu-id="eff41-168">if you selected 10.0.0.0/20 for hello virtual network, you can select 10.1.0.0/24 for hello client address space.</span></span> <span data-ttu-id="eff41-169">Vea hello [conectividadpuntoasitiode] [ vnet-point-to-site-connectivity] página para obtener más información.</span><span class="sxs-lookup"><span data-stu-id="eff41-169">See hello [Point-To-Site Connectivity][vnet-point-to-site-connectivity] page for more information.</span></span>
7. <span data-ttu-id="eff41-170">En la sección de espacios de direcciones de red virtual de hello, haga clic en **Agregar subred de puerta de enlace**.</span><span class="sxs-lookup"><span data-stu-id="eff41-170">In hello virtual network address spaces section, click **add gateway subnet**.</span></span>
8. <span data-ttu-id="eff41-171">Haga clic en **guardar** en parte inferior de Hola de página de Hola.</span><span class="sxs-lookup"><span data-stu-id="eff41-171">Click **SAVE** on hello bottom of hello page.</span></span>
9. <span data-ttu-id="eff41-172">Haga clic en **Sí** cambio de hello tooconfirm.</span><span class="sxs-lookup"><span data-stu-id="eff41-172">Click **YES** tooconfirm hello change.</span></span> <span data-ttu-id="eff41-173">Espere hasta que Hola sistema haya terminado de realizar cambios antes de continuar el procedimiento siguiente toohello de Hola.</span><span class="sxs-lookup"><span data-stu-id="eff41-173">Wait until hello system has finished making hello change before you proceed toohello next procedure.</span></span>

<span data-ttu-id="eff41-174">**toocreate una puerta de enlace de enrutamiento dinámico**</span><span class="sxs-lookup"><span data-stu-id="eff41-174">**toocreate a dynamic routing gateway**</span></span>

1. <span data-ttu-id="eff41-175">En hello Portal de Azure clásico, haga clic en **panel** de arriba Hola de página Hola.</span><span class="sxs-lookup"><span data-stu-id="eff41-175">From hello Azure Classic Portal, click **DASHBOARD** from hello top of hello page.</span></span>
2. <span data-ttu-id="eff41-176">Haga clic en **crear puerta de enlace** desde el final Hola Hola.</span><span class="sxs-lookup"><span data-stu-id="eff41-176">Click **CREATE GATEWAY** from hello bottom of hello page.</span></span>
3. <span data-ttu-id="eff41-177">Haga clic en **Sí** tooconfirm.</span><span class="sxs-lookup"><span data-stu-id="eff41-177">Click **YES** tooconfirm.</span></span> <span data-ttu-id="eff41-178">Espere hasta que se cree la puerta de enlace de Hola.</span><span class="sxs-lookup"><span data-stu-id="eff41-178">Wait until hello gateway is created.</span></span>
4. <span data-ttu-id="eff41-179">Haga clic en **panel** desde la parte superior de Hola.</span><span class="sxs-lookup"><span data-stu-id="eff41-179">Click **DASHBOARD** from hello top.</span></span>  <span data-ttu-id="eff41-180">Verá un diagrama visual de la red virtual de hello:</span><span class="sxs-lookup"><span data-stu-id="eff41-180">You will see a visual diagram of hello virtual network:</span></span>

    ![Diagrama virtual de punto a sitio de red virtual de Azure][img-vnet-diagram]

    <span data-ttu-id="eff41-182">diagrama de Hello muestra 0 conexiones de cliente.</span><span class="sxs-lookup"><span data-stu-id="eff41-182">hello diagram shows 0 client connections.</span></span> <span data-ttu-id="eff41-183">Después de realizar una red virtual de toohello de conexión, el número de hello será tooone actualizada.</span><span class="sxs-lookup"><span data-stu-id="eff41-183">After you make a connection toohello virtual network, hello number will be updated tooone.</span></span>

#### <a name="create-your-certificates"></a><span data-ttu-id="eff41-184">Creación de certificados</span><span class="sxs-lookup"><span data-stu-id="eff41-184">Create your certificates</span></span>
<span data-ttu-id="eff41-185">Una manera de toocreate está usando un certificado X.509 Hola herramienta de creación de certificados (makecert.exe) que se incluye con [Microsoft Visual Studio Express para Windows Desktop](https://www.visualstudio.com/products/visual-studio-express-vs.aspx).</span><span class="sxs-lookup"><span data-stu-id="eff41-185">One way toocreate an X.509 certificate is by using hello Certificate Creation Tool (makecert.exe) that comes with [Microsoft Visual Studio Express for Windows Desktop](https://www.visualstudio.com/products/visual-studio-express-vs.aspx).</span></span>

<span data-ttu-id="eff41-186">**toocreate un certificado raíz autofirmado**</span><span class="sxs-lookup"><span data-stu-id="eff41-186">**toocreate a self-signed root certificate**</span></span>

1. <span data-ttu-id="eff41-187">Abra la ventana del símbolo del sistema desde la estación de trabajo.</span><span class="sxs-lookup"><span data-stu-id="eff41-187">From your workstation, open a command prompt window.</span></span>
2. <span data-ttu-id="eff41-188">Desplazarse por las carpetas de herramientas de Visual Studio toohello.</span><span class="sxs-lookup"><span data-stu-id="eff41-188">Navigate toohello Visual Studio tools folder.</span></span>
3. <span data-ttu-id="eff41-189">Hola siguiente comando en el siguiente ejemplo de Hola creará e instalar un certificado raíz en el almacén de certificados personales de hello en la estación de trabajo y crear un archivo .cer correspondiente más adelante cargará toohello Portal clásico de Azure.</span><span class="sxs-lookup"><span data-stu-id="eff41-189">hello following command in hello example below will create and install a root certificate in hello Personal certificate store on your workstation and also create a corresponding .cer file that you’ll later upload toohello Azure Classic Portal.</span></span>

        makecert -sky exchange -r -n "CN=HBaseVnetVPNRootCertificate" -pe -a sha1 -len 2048 -ss My "C:\Users\JohnDole\Desktop\HBaseVNetVPNRootCertificate.cer"

    <span data-ttu-id="eff41-190">Cambie el directorio de toohello que desea Hola toobe de archivo .cer ubicado en, donde HBaseVnetVPNRootCertificate es el nombre de Hola que deseas toouse certificado Hola.</span><span class="sxs-lookup"><span data-stu-id="eff41-190">Change toohello directory that you want hello .cer file toobe located in, where HBaseVnetVPNRootCertificate is hello name that you want toouse for hello certificate.</span></span>

    <span data-ttu-id="eff41-191">No cierre el símbolo del sistema Hola.</span><span class="sxs-lookup"><span data-stu-id="eff41-191">Don't close hello command prompt.</span></span>  <span data-ttu-id="eff41-192">Lo necesitará en el procedimiento siguiente Hola.</span><span class="sxs-lookup"><span data-stu-id="eff41-192">You will need it in hello next procedure.</span></span>

   > [!NOTE]
   > <span data-ttu-id="eff41-193">Como ha creado un certificado de raíz desde el que se generará certificados de cliente, puede desea tooexport este certificado junto con su clave privada y guardarlo tooa ubicación segura donde se pueda recuperar.</span><span class="sxs-lookup"><span data-stu-id="eff41-193">Because you have created a root certificate from which client certificates will be generated, you may want tooexport this certificate along with its private key and save it tooa safe location where it may be recovered.</span></span>
   >
   >

<span data-ttu-id="eff41-194">**toocreate un certificado de cliente**</span><span class="sxs-lookup"><span data-stu-id="eff41-194">**toocreate a client certificate**</span></span>

* <span data-ttu-id="eff41-195">De hello mismo símbolo (tiene toobe en hello mismo equipo donde se creó el certificado de raíz de Hola.</span><span class="sxs-lookup"><span data-stu-id="eff41-195">From hello same command prompt (It has toobe on hello same computer where you created hello root certificate.</span></span> <span data-ttu-id="eff41-196">certificado de cliente de Hello debe generarse de certificado de raíz de hello), ejecución hello comando siguiente:</span><span class="sxs-lookup"><span data-stu-id="eff41-196">hello client certificate must be generated from hello root certificate), run hello following command:</span></span>

          makecert.exe -n "CN=HBaseVnetVPNClientCertificate" -pe -sky exchange -m 96 -ss My -in "HBaseVnetVPNRootCertificate" -is my -a sha1

    <span data-ttu-id="eff41-197">HBaseVnetVPNRootCertificate es el nombre de certificado de raíz de Hola.</span><span class="sxs-lookup"><span data-stu-id="eff41-197">HBaseVnetVPNRootCertificate is hello root certificate name.</span></span>  <span data-ttu-id="eff41-198">Tiene el nombre del certificado de raíz de toomatch Hola.</span><span class="sxs-lookup"><span data-stu-id="eff41-198">It has toomatch hello root certificate name.</span></span>  

    <span data-ttu-id="eff41-199">Certificado de raíz de Hola y el certificado de cliente de Hola se almacenan en el almacén de certificados personales en el equipo.</span><span class="sxs-lookup"><span data-stu-id="eff41-199">Both hello root certificate and hello client certificate are stored in your Personal certificate store on your computer.</span></span> <span data-ttu-id="eff41-200">Utilice certmgr.msc tooverify.</span><span class="sxs-lookup"><span data-stu-id="eff41-200">Use certmgr.msc tooverify.</span></span>

    ![Certificado VPN de punto a sitio de red virtual de Azure][img-certificate]

    <span data-ttu-id="eff41-202">Un certificado de cliente debe instalarse en cada equipo que desea que la red virtual de tooconnect toohello.</span><span class="sxs-lookup"><span data-stu-id="eff41-202">A client certificate must be installed on each computer that you want tooconnect toohello virtual network.</span></span> <span data-ttu-id="eff41-203">Le recomendamos que cree a cliente único certificados para cada equipo que desea que la red virtual de tooconnect toohello.</span><span class="sxs-lookup"><span data-stu-id="eff41-203">We recommend that you create unique client certificates for each computer that you want tooconnect toohello virtual network.</span></span> <span data-ttu-id="eff41-204">los certificados de cliente hello tooexport, utilice certmgr.msc.</span><span class="sxs-lookup"><span data-stu-id="eff41-204">tooexport hello client certificates, use certmgr.msc.</span></span>

<span data-ttu-id="eff41-205">**tooupload Hola raíz certificado toohello Portal clásico de Azure**</span><span class="sxs-lookup"><span data-stu-id="eff41-205">**tooupload hello root certificate toohello Azure Classic Portal**</span></span>

1. <span data-ttu-id="eff41-206">En hello Portal de Azure clásico, haga clic en **red** de hello izquierda.</span><span class="sxs-lookup"><span data-stu-id="eff41-206">From hello Azure Classic Portal, click **NETWORK** on hello left.</span></span>
2. <span data-ttu-id="eff41-207">Haga clic en la red virtual de Hola donde se implementa el clúster de HBase en.</span><span class="sxs-lookup"><span data-stu-id="eff41-207">Click hello virtual network where your HBase cluster is deployed to.</span></span>
3. <span data-ttu-id="eff41-208">Haga clic en **certificados** desde la parte superior de Hola.</span><span class="sxs-lookup"><span data-stu-id="eff41-208">Click **CERTIFICATES** from hello top.</span></span>
4. <span data-ttu-id="eff41-209">Haga clic en **cargar** de hello abajo y especifique el archivo de certificado raíz de hello ha creado en el procedimiento de hello penúltimo.</span><span class="sxs-lookup"><span data-stu-id="eff41-209">Click **UPLOAD** from hello bottom, and specify hello root certificate file you have created in hello procedure before last.</span></span> <span data-ttu-id="eff41-210">Espere hasta que se obtuvo importar el certificado de Hola.</span><span class="sxs-lookup"><span data-stu-id="eff41-210">Wait until hello certificate got imported.</span></span>
5. <span data-ttu-id="eff41-211">Haga clic en **panel** en la parte superior de Hola.</span><span class="sxs-lookup"><span data-stu-id="eff41-211">Click **DASHBOARD** on hello top.</span></span>  <span data-ttu-id="eff41-212">diagrama de Hello virtual muestra el estado de Hola.</span><span class="sxs-lookup"><span data-stu-id="eff41-212">hello virtual diagram shows hello status.</span></span>

#### <a name="configure-your-vpn-client"></a><span data-ttu-id="eff41-213">Configuración del cliente VPN</span><span class="sxs-lookup"><span data-stu-id="eff41-213">Configure your VPN client</span></span>
<span data-ttu-id="eff41-214">**paquete de VPN de cliente hello toodownload e instalar**</span><span class="sxs-lookup"><span data-stu-id="eff41-214">**toodownload and install hello client VPN package**</span></span>

1. <span data-ttu-id="eff41-215">Desde la página del panel Hola de red virtual de hello, en la sección de vista rápida de hello, haga clic en **descarga Hola paquete de VPN de cliente de 64 bits** o **descarga Hola paquete de VPN de cliente de 32 bits** en función de su versión de sistema operativo de la estación de trabajo.</span><span class="sxs-lookup"><span data-stu-id="eff41-215">From hello DASHBOARD page of hello virtual network, in hello quick glance section, click either **Download hello 64-bit Client VPN Package** or **Download hello 32-bit Client VPN Package** based on your workstation OS version.</span></span>
2. <span data-ttu-id="eff41-216">Haga clic en **ejecutar** tooinstall paquetes de saludo.</span><span class="sxs-lookup"><span data-stu-id="eff41-216">Click **Run** tooinstall hello package.</span></span>
3. <span data-ttu-id="eff41-217">En el símbolo del sistema de seguridad hello, haga clic en **obtener más información**y, a continuación, haga clic en **ejecutar de todas maneras**.</span><span class="sxs-lookup"><span data-stu-id="eff41-217">At hello security prompt, click **More info**, and then click **Run anyway**.</span></span>
4. <span data-ttu-id="eff41-218">Haga clic en **Sí**</span><span class="sxs-lookup"><span data-stu-id="eff41-218">Click **Yes** twice.</span></span>

<span data-ttu-id="eff41-219">**tooconnect tooVPN**</span><span class="sxs-lookup"><span data-stu-id="eff41-219">**tooconnect tooVPN**</span></span>

1. <span data-ttu-id="eff41-220">En el escritorio de saludo de la estación de trabajo, haga clic en el icono de redes de hello en la barra de tareas de Hola.</span><span class="sxs-lookup"><span data-stu-id="eff41-220">On hello desktop of your workstation, click hello Networks icon on hello Task bar.</span></span> <span data-ttu-id="eff41-221">Verá una conexión VPN con el nombre de red virtual.</span><span class="sxs-lookup"><span data-stu-id="eff41-221">You shall see a VPN connection with your virtual network name.</span></span>
2. <span data-ttu-id="eff41-222">Haga clic en el nombre de la conexión VPN Hola.</span><span class="sxs-lookup"><span data-stu-id="eff41-222">Click hello VPN connection name.</span></span>
3. <span data-ttu-id="eff41-223">Haga clic en **Conectar**.</span><span class="sxs-lookup"><span data-stu-id="eff41-223">Click **Connect**.</span></span>

<span data-ttu-id="eff41-224">**Hola tootest resolución de nombres de dominio y de conexión VPN**</span><span class="sxs-lookup"><span data-stu-id="eff41-224">**tootest hello VPN connection and domain name resolution**</span></span>

* <span data-ttu-id="eff41-225">Desde la estación de trabajo de hello, abra un símbolo del sistema y ping de hello siguiendo los nombres de sufijo DNS del clúster de HBase hello es myhbase.b7.internal.cloudapp.net:</span><span class="sxs-lookup"><span data-stu-id="eff41-225">From hello workstation, open a command prompt and ping one of hello following names given hello HBase cluster's DNS suffix is myhbase.b7.internal.cloudapp.net:</span></span>

        zookeeper0.myhbase.b7.internal.cloudapp.net
        zookeeper0.myhbase.b7.internal.cloudapp.net
        zookeeper0.myhbase.b7.internal.cloudapp.net
        headnode0.myhbase.b7.internal.cloudapp.net
        headnode1.myhbase.b7.internal.cloudapp.net
        workernode0.myhbase.b7.internal.cloudapp.net

### <a name="install-and-configure-squirrel-on-your-workstation"></a><span data-ttu-id="eff41-226">Instalación y configuración de SQuirreL en su estación de trabajo</span><span class="sxs-lookup"><span data-stu-id="eff41-226">Install and configure SQuirreL on your workstation</span></span>
<span data-ttu-id="eff41-227">**tooinstall ardilla**</span><span class="sxs-lookup"><span data-stu-id="eff41-227">**tooinstall SQuirreL**</span></span>

1. <span data-ttu-id="eff41-228">Descargar archivo de hello ardilla SQL cliente jar de [http://squirrel-sql.sourceforge.net/#installation](http://squirrel-sql.sourceforge.net/#installation).</span><span class="sxs-lookup"><span data-stu-id="eff41-228">Download hello SQuirreL SQL client jar file from [http://squirrel-sql.sourceforge.net/#installation](http://squirrel-sql.sourceforge.net/#installation).</span></span>
2. <span data-ttu-id="eff41-229">Archivo jar de hello abrir o ejecutar.</span><span class="sxs-lookup"><span data-stu-id="eff41-229">Open/run hello jar file.</span></span> <span data-ttu-id="eff41-230">Requiere hello [Java Runtime Environment](http://www.oracle.com/technetwork/java/javase/downloads/jre7-downloads-1880261.html).</span><span class="sxs-lookup"><span data-stu-id="eff41-230">It requires hello [Java Runtime Environment](http://www.oracle.com/technetwork/java/javase/downloads/jre7-downloads-1880261.html).</span></span>
3. <span data-ttu-id="eff41-231">Haga clic en **Siguiente** dos veces.</span><span class="sxs-lookup"><span data-stu-id="eff41-231">Click **Next** twice.</span></span>
4. <span data-ttu-id="eff41-232">Especifique una ruta de acceso donde haya Hola permiso de escritura y, a continuación, haga clic en **siguiente**.</span><span class="sxs-lookup"><span data-stu-id="eff41-232">Specify a path where you have hello write permission, and then click **Next**.</span></span>

  > [!NOTE]
  > <span data-ttu-id="eff41-233">carpeta de instalación predeterminada de Hello está en la carpeta C:\Program Files\squirrel-sql-3.6 de Hola.</span><span class="sxs-lookup"><span data-stu-id="eff41-233">hello default installation folder is in hello C:\Program Files\squirrel-sql-3.6 folder.</span></span>  <span data-ttu-id="eff41-234">En orden toowrite toothis ruta de acceso instalador Hola debe tener privilegios de administrador de Hola.</span><span class="sxs-lookup"><span data-stu-id="eff41-234">In order toowrite toothis path, hello installer must be granted hello administrator privilege.</span></span> <span data-ttu-id="eff41-235">Puede abrir un símbolo del sistema como administrador, desplazarse por las carpetas de la Papelera de tooJava y, a continuación, ejecute:</span><span class="sxs-lookup"><span data-stu-id="eff41-235">You can open a command prompt as administrator, navigate tooJava's bin folder, and then run:</span></span>
  >
  >     <span data-ttu-id="eff41-236">Java.exe-jar [ruta de acceso de hello del archivo jar de hello ardilla]</span><span class="sxs-lookup"><span data-stu-id="eff41-236">java.exe -jar [hello path of hello SQuirreL jar file]</span></span>
5. <span data-ttu-id="eff41-237">Haga clic en **Aceptar** tooconfirm crear el directorio de destino de Hola.</span><span class="sxs-lookup"><span data-stu-id="eff41-237">Click **OK** tooconfirm creating hello target directory.</span></span>
6. <span data-ttu-id="eff41-238">saludo predeterminado es tooinstall Hola Base y los paquetes estándares.</span><span class="sxs-lookup"><span data-stu-id="eff41-238">hello default setting is tooinstall hello Base and Standard packages.</span></span>  <span data-ttu-id="eff41-239">Haga clic en **Siguiente**.</span><span class="sxs-lookup"><span data-stu-id="eff41-239">Click **Next**.</span></span>
7. <span data-ttu-id="eff41-240">Haga clic en **Siguiente** dos veces y, a continuación, en **Hecho**.</span><span class="sxs-lookup"><span data-stu-id="eff41-240">Click **Next** twice, and then click **Done**.</span></span>

<span data-ttu-id="eff41-241">**controlador de Phoenix hello tooinstall**</span><span class="sxs-lookup"><span data-stu-id="eff41-241">**tooinstall hello Phoenix driver**</span></span>

<span data-ttu-id="eff41-242">archivo jar de Hello phoenix controlador se encuentra en clúster de HBase Hola.</span><span class="sxs-lookup"><span data-stu-id="eff41-242">hello phoenix driver jar file is located on hello HBase cluster.</span></span> <span data-ttu-id="eff41-243">ruta de acceso de Hello es similar toohello siguiente basados en versiones de hello:</span><span class="sxs-lookup"><span data-stu-id="eff41-243">hello path is similar toohello following based on hello versions:</span></span>

    C:\apps\dist\phoenix-4.0.0.2.1.11.0-2316\phoenix-4.0.0.2.1.11.0-2316-client.jar
<span data-ttu-id="eff41-244">Necesita toocopy, estación de trabajo de tooyour en hello [carpeta de instalación de ardilla] / ruta de acceso de lib.</span><span class="sxs-lookup"><span data-stu-id="eff41-244">You need toocopy it tooyour workstation under hello [SQuirreL installation folder]/lib path.</span></span>  <span data-ttu-id="eff41-245">Hello más sencillo es tooRDP en clúster de hello y, a continuación, utilice Copiar y pegar (CTRL+C y CTRL+V) toocopy del archivo se tooyour estación de trabajo.</span><span class="sxs-lookup"><span data-stu-id="eff41-245">hello easiest way is tooRDP into hello cluster, and then use file copy/paste (CTRL+C and CTRL+V) toocopy it tooyour workstation.</span></span>

<span data-ttu-id="eff41-246">**tooadd un tooSQuirreL de controlador de Phoenix**</span><span class="sxs-lookup"><span data-stu-id="eff41-246">**tooadd a Phoenix driver tooSQuirreL**</span></span>

1. <span data-ttu-id="eff41-247">Abra el cliente SQL SQuirreL desde la estación de trabajo.</span><span class="sxs-lookup"><span data-stu-id="eff41-247">Open SQuirreL SQL Client from your workstation.</span></span>
2. <span data-ttu-id="eff41-248">Haga clic en hello **controlador** ficha Hola izquierda.</span><span class="sxs-lookup"><span data-stu-id="eff41-248">Click hello **Driver** tab on hello left.</span></span>
3. <span data-ttu-id="eff41-249">De hello **controladores** menú, haga clic en **nuevo controlador**.</span><span class="sxs-lookup"><span data-stu-id="eff41-249">From hello **Drivers** menu, click **New Driver**.</span></span>
4. <span data-ttu-id="eff41-250">Escriba Hola siguiente información:</span><span class="sxs-lookup"><span data-stu-id="eff41-250">Enter hello following information:</span></span>

   * <span data-ttu-id="eff41-251">**Nombre**: Phoenix</span><span class="sxs-lookup"><span data-stu-id="eff41-251">**Name**: Phoenix</span></span>
   * <span data-ttu-id="eff41-252">**Dirección URL de ejemplo**: jdbc:phoenix:zookeeper2.contoso-hbase-eu.f5.internal.cloudapp.net</span><span class="sxs-lookup"><span data-stu-id="eff41-252">**Example URL**: jdbc:phoenix:zookeeper2.contoso-hbase-eu.f5.internal.cloudapp.net</span></span>
   * <span data-ttu-id="eff41-253">**Nombre de la clase**: org.apache.phoenix.jdbc.PhoenixDriver</span><span class="sxs-lookup"><span data-stu-id="eff41-253">**Class Name**: org.apache.phoenix.jdbc.PhoenixDriver</span></span>

     > [!WARNING]
     > <span data-ttu-id="eff41-254">Usuario todas las minúsculas en la dirección URL de ejemplo de Hola.</span><span class="sxs-lookup"><span data-stu-id="eff41-254">User all lower case in hello Example URL.</span></span> <span data-ttu-id="eff41-255">Puede usar el cuórum de zookeeper completo en caso de que uno de ellos esté inactivo.</span><span class="sxs-lookup"><span data-stu-id="eff41-255">You can use they full zookeeper quorum in case one of them is down.</span></span>  <span data-ttu-id="eff41-256">los nombres de host de Hello son zookeeper0, zookeeper1 y zookeeper2.</span><span class="sxs-lookup"><span data-stu-id="eff41-256">hello hostnames are zookeeper0, zookeeper1, and zookeeper2.</span></span>
     >
     >

     ![Controlador SQuirreL de HBase Phoenix para HDInsight][img-squirrel-driver]
5. <span data-ttu-id="eff41-258">Haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="eff41-258">Click **OK**.</span></span>

<span data-ttu-id="eff41-259">**toocreate un clúster de HBase de toohello de alias**</span><span class="sxs-lookup"><span data-stu-id="eff41-259">**toocreate an alias toohello HBase cluster**</span></span>

1. <span data-ttu-id="eff41-260">En ardilla, haga clic en hello **alias** ficha Hola izquierda.</span><span class="sxs-lookup"><span data-stu-id="eff41-260">From SQuirreL, Click hello **Aliases** tab on hello left.</span></span>
2. <span data-ttu-id="eff41-261">De hello **alias** menú, haga clic en **nuevo Alias**.</span><span class="sxs-lookup"><span data-stu-id="eff41-261">From hello **Aliases** menu, click **New Alias**.</span></span>
3. <span data-ttu-id="eff41-262">Escriba Hola siguiente información:</span><span class="sxs-lookup"><span data-stu-id="eff41-262">Enter hello following information:</span></span>

   * <span data-ttu-id="eff41-263">**Nombre**: nombre de Hola de clúster de HBase de Hola o cualquier nombre que prefiera.</span><span class="sxs-lookup"><span data-stu-id="eff41-263">**Name**: hello name of hello HBase cluster or any name you prefer.</span></span>
   * <span data-ttu-id="eff41-264">**Controlador**: Phoenix.</span><span class="sxs-lookup"><span data-stu-id="eff41-264">**Driver**: Phoenix.</span></span>  <span data-ttu-id="eff41-265">Esto debe coincidir con el nombre del controlador de Hola que creó en el último procedimiento de Hola.</span><span class="sxs-lookup"><span data-stu-id="eff41-265">This must match hello driver name you created in hello last procedure.</span></span>
   * <span data-ttu-id="eff41-266">**Dirección URL**: Hola se copia la dirección URL de la configuración del controlador.</span><span class="sxs-lookup"><span data-stu-id="eff41-266">**URL**: hello URL is copied from your driver configuration.</span></span> <span data-ttu-id="eff41-267">Poner en toouser seguro todas las minúsculas.</span><span class="sxs-lookup"><span data-stu-id="eff41-267">Make sure toouser all lower case.</span></span>
   * <span data-ttu-id="eff41-268">**Nombre de usuario**: puede ser cualquier texto.</span><span class="sxs-lookup"><span data-stu-id="eff41-268">**User name**: It can be any text.</span></span>  <span data-ttu-id="eff41-269">Dado que usa aquí conectividad VPN, nombre de usuario de hello no se utiliza en absoluto.</span><span class="sxs-lookup"><span data-stu-id="eff41-269">Because you use VPN connectivity here, hello user name is not used at all.</span></span>
   * <span data-ttu-id="eff41-270">**Contraseña**: puede ser cualquier texto.</span><span class="sxs-lookup"><span data-stu-id="eff41-270">**Password**: It can be any text.</span></span>

     ![Controlador SQuirreL de HBase Phoenix para HDInsight][img-squirrel-alias]
4. <span data-ttu-id="eff41-272">Haga clic en **Probar**.</span><span class="sxs-lookup"><span data-stu-id="eff41-272">Click **Test**.</span></span>
5. <span data-ttu-id="eff41-273">Haga clic en **Conectar**.</span><span class="sxs-lookup"><span data-stu-id="eff41-273">Click **Connect**.</span></span> <span data-ttu-id="eff41-274">Cuando realiza la conexión de hello, ardilla tendrá este aspecto:</span><span class="sxs-lookup"><span data-stu-id="eff41-274">When it makes hello connection, SQuirreL looks like:</span></span>

    ![SQuirreL de Phoenix HBase][img-squirrel]

<span data-ttu-id="eff41-276">**toorun una prueba**</span><span class="sxs-lookup"><span data-stu-id="eff41-276">**toorun a test**</span></span>

1. <span data-ttu-id="eff41-277">Haga clic en hello **SQL** pestaña derecha siguiente toohello **objetos** ficha.</span><span class="sxs-lookup"><span data-stu-id="eff41-277">Click hello **SQL** tab right next toohello **Objects** tab.</span></span>
2. <span data-ttu-id="eff41-278">Copie y pegue el siguiente código de hello:</span><span class="sxs-lookup"><span data-stu-id="eff41-278">Copy and paste hello following code:</span></span>

        CREATE TABLE IF NOT EXISTS us_population (state CHAR(2) NOT NULL, city VARCHAR NOT NULL, population BIGINT  CONSTRAINT my_pk PRIMARY KEY (state, city))
3. <span data-ttu-id="eff41-279">Haga clic en el botón de ejecución de Hola.</span><span class="sxs-lookup"><span data-stu-id="eff41-279">Click hello run button.</span></span>

    ![SQuirreL de Phoenix HBase][img-squirrel-sql]
4. <span data-ttu-id="eff41-281">Cambiar atrás toohello **objetos** ficha.</span><span class="sxs-lookup"><span data-stu-id="eff41-281">Switch back toohello **Objects** tab.</span></span>
5. <span data-ttu-id="eff41-282">Expanda el nombre de alias de hello y, a continuación, expanda **tabla**.</span><span class="sxs-lookup"><span data-stu-id="eff41-282">Expand hello alias name, and then expand **TABLE**.</span></span>  <span data-ttu-id="eff41-283">Verá la nueva tabla de hello aparecen en.</span><span class="sxs-lookup"><span data-stu-id="eff41-283">You shall see hello new table listed under.</span></span>

## <a name="next-steps"></a><span data-ttu-id="eff41-284">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="eff41-284">Next steps</span></span>
<span data-ttu-id="eff41-285">En este artículo, ha aprendido cómo toouse Phoenix Apache en HDInsight.</span><span class="sxs-lookup"><span data-stu-id="eff41-285">In this article, you have learned how toouse Apache Phoenix in HDInsight.</span></span>  <span data-ttu-id="eff41-286">toolearn más información, vea</span><span class="sxs-lookup"><span data-stu-id="eff41-286">toolearn more, see</span></span>

* <span data-ttu-id="eff41-287">[Información general de HBase de HDInsight][hdinsight-hbase-overview]: HBase es una base de datos NoSQL de código abierto Apache basada en Hadoop que proporciona acceso aleatorio y una coherencia sólida para grandes cantidades de datos no estructurados y semiestructurados.</span><span class="sxs-lookup"><span data-stu-id="eff41-287">[HDInsight HBase overview][hdinsight-hbase-overview]: HBase is an Apache, open-source, NoSQL database built on Hadoop that provides random access and strong consistency for large amounts of unstructured and semistructured data.</span></span>
* <span data-ttu-id="eff41-288">[Aprovisionar clústeres de HBase en red Virtual de Azure][hdinsight-hbase-provision-vnet]: con la integración de red virtual, clústeres de HBase pueden ser implementado toohello mismo virtual de red así como las aplicaciones que las aplicaciones pueden comunicarse con HBase directamente.</span><span class="sxs-lookup"><span data-stu-id="eff41-288">[Provision HBase clusters on Azure Virtual Network][hdinsight-hbase-provision-vnet]: With virtual network integration, HBase clusters can be deployed toohello same virtual network as your applications so that applications can communicate with HBase directly.</span></span>
* <span data-ttu-id="eff41-289">[Configurar la replicación de HBase en HDInsight](hdinsight-hbase-replication.md): Obtenga información acerca de cómo tooconfigure HBase replicación entre dos centros de datos de Azure.</span><span class="sxs-lookup"><span data-stu-id="eff41-289">[Configure HBase replication in HDInsight](hdinsight-hbase-replication.md): Learn how tooconfigure HBase replication across two Azure datacenters.</span></span>
* <span data-ttu-id="eff41-290">[Analizar la opinión de Twitter con HBase en HDInsight][hbase-twitter-sentiment]: Obtenga información acerca de cómo toodo en tiempo real [análisis de opiniones](http://en.wikipedia.org/wiki/Sentiment_analysis) de grandes cantidades de datos mediante el uso de HBase en un clúster de Hadoop en HDInsight.</span><span class="sxs-lookup"><span data-stu-id="eff41-290">[Analyze Twitter sentiment with HBase in HDInsight][hbase-twitter-sentiment]: Learn how toodo real-time [sentiment analysis](http://en.wikipedia.org/wiki/Sentiment_analysis) of big data by using HBase in a Hadoop cluster in HDInsight.</span></span>

[azure-portal]: https://portal.azure.com
[vnet-point-to-site-connectivity]: https://msdn.microsoft.com/library/azure/09926218-92ab-4f43-aa99-83ab4d355555#BKMK_VNETPT

[hdinsight-versions]: hdinsight-component-versioning.md
[hdinsight-hbase-get-started]: hdinsight-hbase-tutorial-get-started.md
[hdinsight-manage-portal]: hdinsight-administer-use-management-portal.md#connect-to-clusters-using-rdp
[hdinsight-hbase-provision-vnet]: hdinsight-hbase-provision-vnet.md
[hdinsight-hbase-overview]: hdinsight-hbase-overview.md
[hbase-twitter-sentiment]: hdinsight-hbase-analyze-twitter-sentiment.md

[hdinsight-hbase-phoenix-sqlline]: ./media/hdinsight-hbase-phoenix-squirrel/hdinsight-hbase-phoenix-sqlline.png
[img-certificate]: ./media/hdinsight-hbase-phoenix-squirrel/hdinsight-hbase-vpn-certificate.png
[img-vnet-diagram]: ./media/hdinsight-hbase-phoenix-squirrel/hdinsight-hbase-vnet-point-to-site.png
[img-squirrel-driver]: ./media/hdinsight-hbase-phoenix-squirrel/hdinsight-hbase-squirrel-driver.png
[img-squirrel-alias]: ./media/hdinsight-hbase-phoenix-squirrel/hdinsight-hbase-squirrel-alias.png
[img-squirrel]: ./media/hdinsight-hbase-phoenix-squirrel/hdinsight-hbase-squirrel.png
[img-squirrel-sql]: ./media/hdinsight-hbase-phoenix-squirrel/hdinsight-hbase-squirrel-sql.png
