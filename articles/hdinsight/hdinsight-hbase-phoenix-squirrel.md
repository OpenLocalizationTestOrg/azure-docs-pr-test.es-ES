---
title: "Uso de Apache Phoenix y SQuirreL con clústeres de Azure HDInsight basados en Windows | Microsoft Docs"
description: "Aprenda a usar Apache Phoenix en HDInsight y cómo instalar y configurar SQuirreL en su estación de trabajo para conectarse a un clúster de HBase en HDInsight."
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
ms.openlocfilehash: 024b70df99fdefa1598225ebb1fbfee85ea375d0
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/03/2017
---
# <a name="use-apache-phoenix-and-squirrel-with-windows-based-hbase-clusters-in-hdinsight"></a><span data-ttu-id="43290-103">Uso de Apache Phoenix y SQuirreL con clústeres de HBase basados en Windows en HDinsight</span><span class="sxs-lookup"><span data-stu-id="43290-103">Use Apache Phoenix and SQuirreL with Windows-based HBase clusters in HDInsight</span></span>
<span data-ttu-id="43290-104">Aprenda a usar [Apache Phoenix](http://phoenix.apache.org/) en HDInsight y cómo instalar y configurar SQuirreL en su estación de trabajo para conectarse a un clúster de HBase en HDInsight.</span><span class="sxs-lookup"><span data-stu-id="43290-104">Learn how to use [Apache Phoenix](http://phoenix.apache.org/) in HDInsight, and how to install and configure SQuirreL on your workstation to connect to an HBase cluster in HDInsight.</span></span> <span data-ttu-id="43290-105">Para obtener más información acerca de Phoenix, consulte [Phoenix en 15 minutos o menos](http://phoenix.apache.org/Phoenix-in-15-minutes-or-less.html).</span><span class="sxs-lookup"><span data-stu-id="43290-105">For more information about Phoenix, see [Phoenix in 15 minutes or less](http://phoenix.apache.org/Phoenix-in-15-minutes-or-less.html).</span></span> <span data-ttu-id="43290-106">Para la gramática de Phoenix, vea [Gramática de Phoenix](http://phoenix.apache.org/language/index.html).</span><span class="sxs-lookup"><span data-stu-id="43290-106">For the Phoenix grammar, see [Phoenix Grammar](http://phoenix.apache.org/language/index.html).</span></span>

> [!NOTE]
> <span data-ttu-id="43290-107">Para obtener información de la versión de Phoenix en HDInsight, consulte [Novedades en las versiones de clústeres de Hadoop proporcionadas por HDInsight](hdinsight-component-versioning.md).</span><span class="sxs-lookup"><span data-stu-id="43290-107">For the Phoenix version information in HDInsight, see [What's new in the Hadoop cluster versions provided by HDInsight?](hdinsight-component-versioning.md).</span></span>
>

> [!IMPORTANT]
> <span data-ttu-id="43290-108">Los pasos de este tutorial solo se aplican a clústeres de HDInsight basados en Windows.</span><span class="sxs-lookup"><span data-stu-id="43290-108">The steps in this document only work for Windows-based HDInsight clusters.</span></span> <span data-ttu-id="43290-109">HDInsight solo está disponible en Windows en versiones inferiores a la 3.4.</span><span class="sxs-lookup"><span data-stu-id="43290-109">HDInsight is only available on Windows for versions lower than HDInsight 3.4.</span></span> <span data-ttu-id="43290-110">Linux es el único sistema operativo que se usa en la versión 3.4 de HDInsight, o en las superiores.</span><span class="sxs-lookup"><span data-stu-id="43290-110">Linux is the only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="43290-111">Consulte la información sobre la [retirada de HDInsight en Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="43290-111">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span> <span data-ttu-id="43290-112">Para más información sobre el uso de Phoenix en HDInsight basado en Linux, consulte [Use Apache Phoenix with Linux-based HBase clusters in HDinsight](hdinsight-hbase-phoenix-squirrel-linux.md)(Uso de Apache Phoenix con clústeres de HBase basados en Linux en HDinsight).</span><span class="sxs-lookup"><span data-stu-id="43290-112">For information on using Phoenix on Linux-based HDInsight, see [Use Apache Phoenix with Linux-based HBase clusters in HDInsight](hdinsight-hbase-phoenix-squirrel-linux.md).</span></span>
>



## <a name="use-sqlline"></a><span data-ttu-id="43290-113">Uso de SQLLine</span><span class="sxs-lookup"><span data-stu-id="43290-113">Use SQLLine</span></span>
<span data-ttu-id="43290-114">[SQLLine](http://sqlline.sourceforge.net/) es una utilidad de línea de comandos para ejecutar SQL.</span><span class="sxs-lookup"><span data-stu-id="43290-114">[SQLLine](http://sqlline.sourceforge.net/) is a command line utility to execute SQL.</span></span>

### <a name="prerequisites"></a><span data-ttu-id="43290-115">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="43290-115">Prerequisites</span></span>
<span data-ttu-id="43290-116">Antes de usar SQLLine, debe tener lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="43290-116">Before you can use SQLLine, you must have the following:</span></span>

* <span data-ttu-id="43290-117">**Un clúster de HBase en HDInsight**.</span><span class="sxs-lookup"><span data-stu-id="43290-117">**A HBase cluster in HDInsight**.</span></span> <span data-ttu-id="43290-118">Para obtener información sobre el aprovisionamiento del clúster de HBase, consulte [Introducción a HBase Apache en HDInsight][hdinsight-hbase-get-started].</span><span class="sxs-lookup"><span data-stu-id="43290-118">For information on provision HBase cluster, see [Get started with Apache HBase in HDInsight][hdinsight-hbase-get-started].</span></span>
* <span data-ttu-id="43290-119">**Conexión al clúster de HBase a través del protocolo de escritorio remoto**.</span><span class="sxs-lookup"><span data-stu-id="43290-119">**Connect to the HBase cluster via the remote desktop protocol**.</span></span> <span data-ttu-id="43290-120">Para conocer las instrucciones, consulte [Administración de clústeres de Hadoop en HDInsight mediante el Portal de Azure clásico][hdinsight-manage-portal].</span><span class="sxs-lookup"><span data-stu-id="43290-120">For instructions, see [Manage Hadoop clusters in HDInsight by using the Azure Classic Portal][hdinsight-manage-portal].</span></span>

<span data-ttu-id="43290-121">**Para averiguar el nombre de host**</span><span class="sxs-lookup"><span data-stu-id="43290-121">**To find out the host name**</span></span>

1. <span data-ttu-id="43290-122">Abra la **línea de comandos de Hadoop** desde el escritorio.</span><span class="sxs-lookup"><span data-stu-id="43290-122">Open **Hadoop Command Line** from the desktop.</span></span>
2. <span data-ttu-id="43290-123">Ejecute el siguiente comando para obtener el sufijo de DNS:</span><span class="sxs-lookup"><span data-stu-id="43290-123">Run the following command to get the DNS suffix:</span></span>

        ipconfig

    <span data-ttu-id="43290-124">Escriba el **sufijo DNS específico de la conexión**.</span><span class="sxs-lookup"><span data-stu-id="43290-124">Write down **Connection-specific DNS Suffix**.</span></span> <span data-ttu-id="43290-125">Por ejemplo, *myhbasecluster.f5.internal.cloudapp.net*.</span><span class="sxs-lookup"><span data-stu-id="43290-125">For example, *myhbasecluster.f5.internal.cloudapp.net*.</span></span> <span data-ttu-id="43290-126">Cuando se conecta a un clúster de HBase, necesitará conectarse a uno de los Zookeepers mediante FQDN.</span><span class="sxs-lookup"><span data-stu-id="43290-126">When you connect to an HBase cluster, you will need to connect to one of the Zookeepers using FQDN.</span></span> <span data-ttu-id="43290-127">Cada clúster de HDInsight tiene 3 Zookeepers.</span><span class="sxs-lookup"><span data-stu-id="43290-127">Each HDInsight cluster has 3 Zookeepers.</span></span> <span data-ttu-id="43290-128">Son *zookeeper0*, *zookeeper1* y *zookeeper2*.</span><span class="sxs-lookup"><span data-stu-id="43290-128">They are *zookeeper0*, *zookeeper1*, and *zookeeper2*.</span></span> <span data-ttu-id="43290-129">El FQDN será algo parecido a *zookeeper2.myhbasecluster.f5.internal.cloudapp.net*.</span><span class="sxs-lookup"><span data-stu-id="43290-129">The FQDN will be something like *zookeeper2.myhbasecluster.f5.internal.cloudapp.net*.</span></span>

<span data-ttu-id="43290-130">**Para usar SQLLine**</span><span class="sxs-lookup"><span data-stu-id="43290-130">**To use SQLLine**</span></span>

1. <span data-ttu-id="43290-131">Abra la **línea de comandos de Hadoop** desde el escritorio.</span><span class="sxs-lookup"><span data-stu-id="43290-131">Open **Hadoop Command Line** from the desktop.</span></span>
2. <span data-ttu-id="43290-132">Ejecute los siguientes comandos para abrir SQLLine:</span><span class="sxs-lookup"><span data-stu-id="43290-132">Run the following commands to open SQLLine:</span></span>

        cd %phoenix_home%\bin
        sqlline.py [The FQDN of one of the Zookeepers]

    ![HDInsight hbase phoenix sqlline][hdinsight-hbase-phoenix-sqlline]

    <span data-ttu-id="43290-134">Los comandos usados en el ejemplo:</span><span class="sxs-lookup"><span data-stu-id="43290-134">The commands used in the sample:</span></span>

        CREATE TABLE Company (COMPANY_ID INTEGER PRIMARY KEY, NAME VARCHAR(225));

        !tables

        UPSERT INTO Company VALUES(1, 'Microsoft');

        SELECT * FROM Company;

<span data-ttu-id="43290-135">Para más información, consulte el [manual de SQLLine](http://sqlline.sourceforge.net/#manual) y la [gramática de Phoenix](http://phoenix.apache.org/language/index.html).</span><span class="sxs-lookup"><span data-stu-id="43290-135">For more information, see [SQLLine manual](http://sqlline.sourceforge.net/#manual) and [Phoenix Grammar](http://phoenix.apache.org/language/index.html).</span></span>

## <a name="use-squirrel"></a><span data-ttu-id="43290-136">Uso de SQuirreL</span><span class="sxs-lookup"><span data-stu-id="43290-136">Use SQuirreL</span></span>
<span data-ttu-id="43290-137">[Cliente SQL SQuirreL](http://squirrel-sql.sourceforge.net/) es un programa gráfico de Java que le permitirá ver la estructura de una base de datos compatible con JDBC, examinar los datos de tablas, emitir comandos SQL etc. Se puede usar para conectarse a Apache Phoenix en HDInsight.</span><span class="sxs-lookup"><span data-stu-id="43290-137">[SQuirreL SQL Client](http://squirrel-sql.sourceforge.net/) is a graphical Java program that will allow you to view the structure of a JDBC compliant database, browse the data in tables, issue SQL commands etc. It can be used to connect to Apache Phoenix on HDInsight.</span></span>

<span data-ttu-id="43290-138">En esta sección se muestra cómo instalar y configurar SQuirreL en su estación de trabajo para conectarse al clúster de HBase en HDInsight a través de VPN.</span><span class="sxs-lookup"><span data-stu-id="43290-138">This section shows you how to install and configure SQuirreL on your workstation to connect to an HBase cluster in HDInsight via VPN.</span></span>

### <a name="prerequisites"></a><span data-ttu-id="43290-139">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="43290-139">Prerequisites</span></span>
<span data-ttu-id="43290-140">Antes de seguir los procedimientos, debe disponer de lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="43290-140">Before following the procedures, you must have the following:</span></span>

* <span data-ttu-id="43290-141">Un clúster de HBase implementado en una red virtual de Azure con una máquina virtual DNS.</span><span class="sxs-lookup"><span data-stu-id="43290-141">An HBase cluster deployed to an Azure virtual network with a DNS virtual machine.</span></span>  <span data-ttu-id="43290-142">Para obtener instrucciones, consulte [Creación de clústeres de HBase en Azure Virtual Network][hdinsight-hbase-provision-vnet].</span><span class="sxs-lookup"><span data-stu-id="43290-142">For instructions, see [Create HBase clusters on Azure Virtual Network][hdinsight-hbase-provision-vnet].</span></span>

* <span data-ttu-id="43290-143">Obtenga el sufijo DNS específico de la conexión del clúster de HBase.</span><span class="sxs-lookup"><span data-stu-id="43290-143">Get the HBase cluster cluster Connection-specific DNS suffix.</span></span> <span data-ttu-id="43290-144">Para obtenerlo, establezca RDP en el clúster y, a continuación, ejecute IPConfig.</span><span class="sxs-lookup"><span data-stu-id="43290-144">To get it, RDP into the cluster, and then run IPConfig.</span></span>  <span data-ttu-id="43290-145">El sufijo DNS es similar a:</span><span class="sxs-lookup"><span data-stu-id="43290-145">The DNS suffix is similar to:</span></span>

        myhbase.b7.internal.cloudapp.net
* <span data-ttu-id="43290-146">Descargue e instale [Microsoft Visual Studio Express para escritorio de Windows](https://www.visualstudio.com/products/visual-studio-express-vs.aspx) en la estación de trabajo.</span><span class="sxs-lookup"><span data-stu-id="43290-146">Download and install [Microsoft Visual Studio Express for Windows Desktop](https://www.visualstudio.com/products/visual-studio-express-vs.aspx) on your workstation.</span></span> <span data-ttu-id="43290-147">Necesitará makecert del paquete para crear un certificado.</span><span class="sxs-lookup"><span data-stu-id="43290-147">You will need makecert from the package to create your certificate.</span></span>  
* <span data-ttu-id="43290-148">Descargue e instale [Java Runtime Environment](http://www.oracle.com/technetwork/java/javase/downloads/jre7-downloads-1880261.html) en su estación de trabajo.</span><span class="sxs-lookup"><span data-stu-id="43290-148">Download and install [Java Runtime Environment](http://www.oracle.com/technetwork/java/javase/downloads/jre7-downloads-1880261.html) on your workstation.</span></span>  <span data-ttu-id="43290-149">La versión de cliente SQL SQuirreL 3.0 y superiores requieren la versión 1.6 o superior de JRE.</span><span class="sxs-lookup"><span data-stu-id="43290-149">SQuirreL SQL client version 3.0 and higher requires JRE version 1.6 or higher.</span></span>  

### <a name="configure-a-point-to-site-vpn-connection-to-the-azure-virtual-network"></a><span data-ttu-id="43290-150">Configuración de una conexión VPN de punto a sitio a la red virtual de Azure</span><span class="sxs-lookup"><span data-stu-id="43290-150">Configure a Point-to-Site VPN connection to the Azure virtual network</span></span>
<span data-ttu-id="43290-151">Hay tres pasos implicados en la configuración de una conexión VPN de punto a sitio:</span><span class="sxs-lookup"><span data-stu-id="43290-151">There are 3 steps involved configuring a point-to-site VPN connection:</span></span>

1. [<span data-ttu-id="43290-152">Configuración de una red virtual y una puerta de enlace de enrutamiento dinámico</span><span class="sxs-lookup"><span data-stu-id="43290-152">Configure a virtual network and a dynamic routing gateway</span></span>](#Configure-a-virtual-network-and-a-dynamic-routing-gateway)
2. [<span data-ttu-id="43290-153">Creación de certificados</span><span class="sxs-lookup"><span data-stu-id="43290-153">Create your certificates</span></span>](#Create-your-certificates)
3. [<span data-ttu-id="43290-154">Configuración del cliente VPN</span><span class="sxs-lookup"><span data-stu-id="43290-154">Configure your VPN client</span></span>](#Configure-your-VPN-client)

<span data-ttu-id="43290-155">Consulte [Configuración de una conexión VPN de punto a sitio a la red virtual de Azure](../vpn-gateway/vpn-gateway-point-to-site-create.md) para obtener más información.</span><span class="sxs-lookup"><span data-stu-id="43290-155">See [Configure a Point-to-Site VPN connection to an Azure Virtual Network](../vpn-gateway/vpn-gateway-point-to-site-create.md) for more information.</span></span>

#### <a name="configure-a-virtual-network-and-a-dynamic-routing-gateway"></a><span data-ttu-id="43290-156">Configuración de una red virtual y una puerta de enlace de enrutamiento dinámico</span><span class="sxs-lookup"><span data-stu-id="43290-156">Configure a virtual network and a dynamic routing gateway</span></span>
<span data-ttu-id="43290-157">Asegúrese de que ha realizado el aprovisionamiento de un clúster de HBase en una red virtual de Azure (consulte los requisitos previos de esta sección).</span><span class="sxs-lookup"><span data-stu-id="43290-157">Assure you have provisioned an HBase cluster in an Azure virtual network (see the prerequisites for this section).</span></span> <span data-ttu-id="43290-158">El siguiente paso es configurar una conexión punto a sitio.</span><span class="sxs-lookup"><span data-stu-id="43290-158">The next step is to configure a point-to-site connection.</span></span>

<span data-ttu-id="43290-159">**Para configurar la conectividad punto a sitio**</span><span class="sxs-lookup"><span data-stu-id="43290-159">**To configure the point-to-site connectivity**</span></span>

1. <span data-ttu-id="43290-160">Inicie sesión en el [Portal de Azure clásico][azure-portal].</span><span class="sxs-lookup"><span data-stu-id="43290-160">Sign in to the [Azure Classic Portal][azure-portal].</span></span>
2. <span data-ttu-id="43290-161">A la izquierda, haga clic en **REDES**.</span><span class="sxs-lookup"><span data-stu-id="43290-161">On the left, click **NETWORKS**.</span></span>
3. <span data-ttu-id="43290-162">Haga clic en la red virtual que ha creado (consulte [Aprovisionamiento de clústeres de HBase en Azure Virtual Network][hdinsight-hbase-provision-vnet]).</span><span class="sxs-lookup"><span data-stu-id="43290-162">Click the virtual network you have created (see [Provision HBase clusters on Azure Virtual Network][hdinsight-hbase-provision-vnet]).</span></span>
4. <span data-ttu-id="43290-163">Haga clic en **CONFIGURAR** en la parte superior.</span><span class="sxs-lookup"><span data-stu-id="43290-163">Click **CONFIGURE** from the top.</span></span>
5. <span data-ttu-id="43290-164">En la sección **Conectividad punto a sitio**, seleccione **Configurar la conectividad punto a sitio**.</span><span class="sxs-lookup"><span data-stu-id="43290-164">In the **point-to-site connectivity** section, select **Configure point-to-site connectivity**.</span></span>
6. <span data-ttu-id="43290-165">Configure **DIRECCIÓN IP DE INICIO** y **CIDR** para especificar el intervalo de direcciones IP desde el que los clientes de VPN recibirán una dirección IP cuando se conecten.</span><span class="sxs-lookup"><span data-stu-id="43290-165">Configure **STARTING IP** and **CIDR** to specify the IP address range from which your VPN clients will receive an IP address when connected.</span></span> <span data-ttu-id="43290-166">El intervalo no puede coincidir con cualquiera de los intervalos de la red local y la red virtual de Azure a la que se va a conectar.</span><span class="sxs-lookup"><span data-stu-id="43290-166">The range cannot overlap with any of the ranges located on your on-premises network and the Azure virtual network you will be connecting to.</span></span> <span data-ttu-id="43290-167">Por ejemplo.</span><span class="sxs-lookup"><span data-stu-id="43290-167">For example.</span></span> <span data-ttu-id="43290-168">Si selecciona 10.0.0.0/20 para la red virtual, puede seleccionar 10.1.0.0/24 para el espacio de direcciones de cliente.</span><span class="sxs-lookup"><span data-stu-id="43290-168">if you selected 10.0.0.0/20 for the virtual network, you can select 10.1.0.0/24 for the client address space.</span></span> <span data-ttu-id="43290-169">Consulte la página [Conectividad punto a sitio][vnet-point-to-site-connectivity] para obtener más información.</span><span class="sxs-lookup"><span data-stu-id="43290-169">See the [Point-To-Site Connectivity][vnet-point-to-site-connectivity] page for more information.</span></span>
7. <span data-ttu-id="43290-170">En la sección de espacios de direcciones de red virtual, haga clic en **Agregar subred de puerta de enlace**.</span><span class="sxs-lookup"><span data-stu-id="43290-170">In the virtual network address spaces section, click **add gateway subnet**.</span></span>
8. <span data-ttu-id="43290-171">Haga clic en **GUARDAR** en la parte inferior de la página.</span><span class="sxs-lookup"><span data-stu-id="43290-171">Click **SAVE** on the bottom of the page.</span></span>
9. <span data-ttu-id="43290-172">Haga clic en **SÍ** para continuar.</span><span class="sxs-lookup"><span data-stu-id="43290-172">Click **YES** to confirm the change.</span></span> <span data-ttu-id="43290-173">Espere hasta que el sistema haya terminado de realizar el cambio antes de continuar con el siguiente procedimiento.</span><span class="sxs-lookup"><span data-stu-id="43290-173">Wait until the system has finished making the change before you proceed to the next procedure.</span></span>

<span data-ttu-id="43290-174">**Para crear una puerta de enlace de enrutamiento dinámico**</span><span class="sxs-lookup"><span data-stu-id="43290-174">**To create a dynamic routing gateway**</span></span>

1. <span data-ttu-id="43290-175">En el Portal de Azure clásico, haga clic en **PANEL** en la parte superior de la página.</span><span class="sxs-lookup"><span data-stu-id="43290-175">From the Azure Classic Portal, click **DASHBOARD** from the top of the page.</span></span>
2. <span data-ttu-id="43290-176">Haga clic en **CREAR PUERTA DE ENLACE** desde la parte inferior de la página.</span><span class="sxs-lookup"><span data-stu-id="43290-176">Click **CREATE GATEWAY** from the bottom of the page.</span></span>
3. <span data-ttu-id="43290-177">Haga clic en **SÍ** para continuar.</span><span class="sxs-lookup"><span data-stu-id="43290-177">Click **YES** to confirm.</span></span> <span data-ttu-id="43290-178">Espere hasta que se cree la puerta de enlace.</span><span class="sxs-lookup"><span data-stu-id="43290-178">Wait until the gateway is created.</span></span>
4. <span data-ttu-id="43290-179">Haga clic en **PANEL** en la parte superior.</span><span class="sxs-lookup"><span data-stu-id="43290-179">Click **DASHBOARD** from the top.</span></span>  <span data-ttu-id="43290-180">Verá un diagrama visual de la red virtual:</span><span class="sxs-lookup"><span data-stu-id="43290-180">You will see a visual diagram of the virtual network:</span></span>

    ![Diagrama virtual de punto a sitio de red virtual de Azure][img-vnet-diagram]

    <span data-ttu-id="43290-182">El diagrama muestra 0 conexiones de cliente.</span><span class="sxs-lookup"><span data-stu-id="43290-182">The diagram shows 0 client connections.</span></span> <span data-ttu-id="43290-183">Después de realizar una conexión a la red virtual, se actualizará el número a uno.</span><span class="sxs-lookup"><span data-stu-id="43290-183">After you make a connection to the virtual network, the number will be updated to one.</span></span>

#### <a name="create-your-certificates"></a><span data-ttu-id="43290-184">Creación de certificados</span><span class="sxs-lookup"><span data-stu-id="43290-184">Create your certificates</span></span>
<span data-ttu-id="43290-185">Una forma de crear un certificado X.509 es mediante la herramienta de creación de certificados (makecert.exe) que se incluye con [Microsoft Visual Studio Express para escritorio de Windows](https://www.visualstudio.com/products/visual-studio-express-vs.aspx).</span><span class="sxs-lookup"><span data-stu-id="43290-185">One way to create an X.509 certificate is by using the Certificate Creation Tool (makecert.exe) that comes with [Microsoft Visual Studio Express for Windows Desktop](https://www.visualstudio.com/products/visual-studio-express-vs.aspx).</span></span>

<span data-ttu-id="43290-186">**Para crear un certificado raíz autofirmado**</span><span class="sxs-lookup"><span data-stu-id="43290-186">**To create a self-signed root certificate**</span></span>

1. <span data-ttu-id="43290-187">Abra la ventana del símbolo del sistema desde la estación de trabajo.</span><span class="sxs-lookup"><span data-stu-id="43290-187">From your workstation, open a command prompt window.</span></span>
2. <span data-ttu-id="43290-188">Navegue hasta la carpeta de herramientas de Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="43290-188">Navigate to the Visual Studio tools folder.</span></span>
3. <span data-ttu-id="43290-189">El siguiente comando del siguiente ejemplo creará e instalará un certificado raíz en el almacén de certificados Personal de su estación de trabajo, y también creará un archivo .cer correspondiente que podrá cargar más adelante en el Portal de Azure clásico.</span><span class="sxs-lookup"><span data-stu-id="43290-189">The following command in the example below will create and install a root certificate in the Personal certificate store on your workstation and also create a corresponding .cer file that you’ll later upload to the Azure Classic Portal.</span></span>

        makecert -sky exchange -r -n "CN=HBaseVnetVPNRootCertificate" -pe -a sha1 -len 2048 -ss My "C:\Users\JohnDole\Desktop\HBaseVNetVPNRootCertificate.cer"

    <span data-ttu-id="43290-190">Cambie al directorio en el que desee que se encuentre el archivo .cer, donde HBaseVnetVPNRootCertificate es el nombre que desea usar para el certificado.</span><span class="sxs-lookup"><span data-stu-id="43290-190">Change to the directory that you want the .cer file to be located in, where HBaseVnetVPNRootCertificate is the name that you want to use for the certificate.</span></span>

    <span data-ttu-id="43290-191">No cierre el símbolo del sistema.</span><span class="sxs-lookup"><span data-stu-id="43290-191">Don't close the command prompt.</span></span>  <span data-ttu-id="43290-192">Lo necesitará en el siguiente procedimiento.</span><span class="sxs-lookup"><span data-stu-id="43290-192">You will need it in the next procedure.</span></span>

   > [!NOTE]
   > <span data-ttu-id="43290-193">Puesto que ha creado un certificado raíz desde el que se generarán los certificados de cliente, puede que desee exportar este certificado junto con su clave privada y guardarlo en una ubicación segura donde se pueda recuperar.</span><span class="sxs-lookup"><span data-stu-id="43290-193">Because you have created a root certificate from which client certificates will be generated, you may want to export this certificate along with its private key and save it to a safe location where it may be recovered.</span></span>
   >
   >

<span data-ttu-id="43290-194">**Para crear un certificado de cliente**</span><span class="sxs-lookup"><span data-stu-id="43290-194">**To create a client certificate**</span></span>

* <span data-ttu-id="43290-195">Desde el mismo símbolo del sistema (debe estar en el mismo equipo donde ha creado el certificado raíz.</span><span class="sxs-lookup"><span data-stu-id="43290-195">From the same command prompt (It has to be on the same computer where you created the root certificate.</span></span> <span data-ttu-id="43290-196">Se debe generar el certificado de cliente desde el certificado raíz), ejecute el siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="43290-196">The client certificate must be generated from the root certificate), run the following command:</span></span>

          makecert.exe -n "CN=HBaseVnetVPNClientCertificate" -pe -sky exchange -m 96 -ss My -in "HBaseVnetVPNRootCertificate" -is my -a sha1

    <span data-ttu-id="43290-197">HBaseVnetVPNRootCertificate es el nombre del certificado raíz.</span><span class="sxs-lookup"><span data-stu-id="43290-197">HBaseVnetVPNRootCertificate is the root certificate name.</span></span>  <span data-ttu-id="43290-198">Tiene que coincidir con el nombre del certificado raíz.</span><span class="sxs-lookup"><span data-stu-id="43290-198">It has to match the root certificate name.</span></span>  

    <span data-ttu-id="43290-199">Tanto el certificado raíz como el certificado cliente se almacenan en el almacén de certificados personales del equipo.</span><span class="sxs-lookup"><span data-stu-id="43290-199">Both the root certificate and the client certificate are stored in your Personal certificate store on your computer.</span></span> <span data-ttu-id="43290-200">Use certmgr.msc para comprobar.</span><span class="sxs-lookup"><span data-stu-id="43290-200">Use certmgr.msc to verify.</span></span>

    ![Certificado VPN de punto a sitio de red virtual de Azure][img-certificate]

    <span data-ttu-id="43290-202">Se debe instalar un certificado de cliente en cada equipo que desee conectar a la red virtual.</span><span class="sxs-lookup"><span data-stu-id="43290-202">A client certificate must be installed on each computer that you want to connect to the virtual network.</span></span> <span data-ttu-id="43290-203">Se recomienda crear certificados de cliente único para cada equipo que desee conectar a la red virtual.</span><span class="sxs-lookup"><span data-stu-id="43290-203">We recommend that you create unique client certificates for each computer that you want to connect to the virtual network.</span></span> <span data-ttu-id="43290-204">Para exportar los certificados de cliente, use certmgr.msc.</span><span class="sxs-lookup"><span data-stu-id="43290-204">To export the client certificates, use certmgr.msc.</span></span>

<span data-ttu-id="43290-205">**Para cargar el certificado raíz en el Portal de Azure clásico**</span><span class="sxs-lookup"><span data-stu-id="43290-205">**To upload the root certificate to the Azure Classic Portal**</span></span>

1. <span data-ttu-id="43290-206">En el Portal de Azure clásico, haga clic en **REDES** en la parte izquierda.</span><span class="sxs-lookup"><span data-stu-id="43290-206">From the Azure Classic Portal, click **NETWORK** on the left.</span></span>
2. <span data-ttu-id="43290-207">Haga clic en la red virtual en la que se implementa el clúster de HBase.</span><span class="sxs-lookup"><span data-stu-id="43290-207">Click the virtual network where your HBase cluster is deployed to.</span></span>
3. <span data-ttu-id="43290-208">Haga clic en **CERTIFICADOS** en la parte superior.</span><span class="sxs-lookup"><span data-stu-id="43290-208">Click **CERTIFICATES** from the top.</span></span>
4. <span data-ttu-id="43290-209">Haga clic en **CARGAR** desde la parte inferior y especifique el archivo de certificado raíz que ha creado en el procedimiento antes del último.</span><span class="sxs-lookup"><span data-stu-id="43290-209">Click **UPLOAD** from the bottom, and specify the root certificate file you have created in the procedure before last.</span></span> <span data-ttu-id="43290-210">Espere hasta que el certificado se importe.</span><span class="sxs-lookup"><span data-stu-id="43290-210">Wait until the certificate got imported.</span></span>
5. <span data-ttu-id="43290-211">En la parte superior, haga clic en **PANEL** .</span><span class="sxs-lookup"><span data-stu-id="43290-211">Click **DASHBOARD** on the top.</span></span>  <span data-ttu-id="43290-212">El diagrama virtual muestra el estado.</span><span class="sxs-lookup"><span data-stu-id="43290-212">The virtual diagram shows the status.</span></span>

#### <a name="configure-your-vpn-client"></a><span data-ttu-id="43290-213">Configuración del cliente VPN</span><span class="sxs-lookup"><span data-stu-id="43290-213">Configure your VPN client</span></span>
<span data-ttu-id="43290-214">**Para descargar e instalar el paquete VPN cliente**</span><span class="sxs-lookup"><span data-stu-id="43290-214">**To download and install the client VPN package**</span></span>

1. <span data-ttu-id="43290-215">Desde la página PANEL de la red virtual, en la sección de vista rápida, haga clic en **Descargar paquete de VPN de cliente de 64 bits** o **Download the 32-bit Client VPN Package** (Descargar el paquete de VPN de cliente de 32 bits) según la versión de sistema operativo de la estación de trabajo.</span><span class="sxs-lookup"><span data-stu-id="43290-215">From the DASHBOARD page of the virtual network, in the quick glance section, click either **Download the 64-bit Client VPN Package** or **Download the 32-bit Client VPN Package** based on your workstation OS version.</span></span>
2. <span data-ttu-id="43290-216">Haga clic en **Ejecutar** para instalar el paquete.</span><span class="sxs-lookup"><span data-stu-id="43290-216">Click **Run** to install the package.</span></span>
3. <span data-ttu-id="43290-217">En el símbolo del sistema de seguridad, haga clic en **More info** (Más información), y, a continuación, haga clic en **Run anyway** (Ejecutar de todas formas).</span><span class="sxs-lookup"><span data-stu-id="43290-217">At the security prompt, click **More info**, and then click **Run anyway**.</span></span>
4. <span data-ttu-id="43290-218">Haga clic en **Sí**</span><span class="sxs-lookup"><span data-stu-id="43290-218">Click **Yes** twice.</span></span>

<span data-ttu-id="43290-219">**Para conectarse a VPN**</span><span class="sxs-lookup"><span data-stu-id="43290-219">**To connect to VPN**</span></span>

1. <span data-ttu-id="43290-220">En el escritorio de la estación de trabajo, haga clic en el icono Redes en la barra de tareas.</span><span class="sxs-lookup"><span data-stu-id="43290-220">On the desktop of your workstation, click the Networks icon on the Task bar.</span></span> <span data-ttu-id="43290-221">Verá una conexión VPN con el nombre de red virtual.</span><span class="sxs-lookup"><span data-stu-id="43290-221">You shall see a VPN connection with your virtual network name.</span></span>
2. <span data-ttu-id="43290-222">Haga clic en el nombre de la conexión VPN.</span><span class="sxs-lookup"><span data-stu-id="43290-222">Click the VPN connection name.</span></span>
3. <span data-ttu-id="43290-223">Haga clic en **Conectar**.</span><span class="sxs-lookup"><span data-stu-id="43290-223">Click **Connect**.</span></span>

<span data-ttu-id="43290-224">**Para probar la conexión VPN y la resolución de nombre de dominio**</span><span class="sxs-lookup"><span data-stu-id="43290-224">**To test the VPN connection and domain name resolution**</span></span>

* <span data-ttu-id="43290-225">Desde la estación de trabajo, abra un símbolo del sistema y haga ping en uno de los siguientes nombres teniendo en cuenta que el sufijo DNS del clúster de HBase es myhbase.b7.internal.cloudapp.net:</span><span class="sxs-lookup"><span data-stu-id="43290-225">From the workstation, open a command prompt and ping one of the following names given the HBase cluster's DNS suffix is myhbase.b7.internal.cloudapp.net:</span></span>

        zookeeper0.myhbase.b7.internal.cloudapp.net
        zookeeper0.myhbase.b7.internal.cloudapp.net
        zookeeper0.myhbase.b7.internal.cloudapp.net
        headnode0.myhbase.b7.internal.cloudapp.net
        headnode1.myhbase.b7.internal.cloudapp.net
        workernode0.myhbase.b7.internal.cloudapp.net

### <a name="install-and-configure-squirrel-on-your-workstation"></a><span data-ttu-id="43290-226">Instalación y configuración de SQuirreL en su estación de trabajo</span><span class="sxs-lookup"><span data-stu-id="43290-226">Install and configure SQuirreL on your workstation</span></span>
<span data-ttu-id="43290-227">**Para instalar SQuirreL**</span><span class="sxs-lookup"><span data-stu-id="43290-227">**To install SQuirreL**</span></span>

1. <span data-ttu-id="43290-228">Descargue el archivo jar de cliente SQL SQuirreL de [http://squirrel-sql.sourceforge.net/#installation](http://squirrel-sql.sourceforge.net/#installation).</span><span class="sxs-lookup"><span data-stu-id="43290-228">Download the SQuirreL SQL client jar file from [http://squirrel-sql.sourceforge.net/#installation](http://squirrel-sql.sourceforge.net/#installation).</span></span>
2. <span data-ttu-id="43290-229">Abra/ejecute el archivo jar.</span><span class="sxs-lookup"><span data-stu-id="43290-229">Open/run the jar file.</span></span> <span data-ttu-id="43290-230">Requiere [Java Runtime Environment](http://www.oracle.com/technetwork/java/javase/downloads/jre7-downloads-1880261.html).</span><span class="sxs-lookup"><span data-stu-id="43290-230">It requires the [Java Runtime Environment](http://www.oracle.com/technetwork/java/javase/downloads/jre7-downloads-1880261.html).</span></span>
3. <span data-ttu-id="43290-231">Haga clic en **Siguiente** dos veces.</span><span class="sxs-lookup"><span data-stu-id="43290-231">Click **Next** twice.</span></span>
4. <span data-ttu-id="43290-232">Especifique una ruta de acceso donde tenga permiso de escritura y, a continuación, haga clic en **Siguiente**.</span><span class="sxs-lookup"><span data-stu-id="43290-232">Specify a path where you have the write permission, and then click **Next**.</span></span>

  > [!NOTE]
  > <span data-ttu-id="43290-233">La carpeta de instalación predeterminada es C:\Archivos de programa\squirrel-sql-3.6.</span><span class="sxs-lookup"><span data-stu-id="43290-233">The default installation folder is in the C:\Program Files\squirrel-sql-3.6 folder.</span></span>  <span data-ttu-id="43290-234">Para poder escribir en esta ruta de acceso, el programa de instalación debe disponer de privilegios de administrador.</span><span class="sxs-lookup"><span data-stu-id="43290-234">In order to write to this path, the installer must be granted the administrator privilege.</span></span> <span data-ttu-id="43290-235">Puede abrir un símbolo del sistema como administrador, ir a la carpeta bin de Java y, luego, ejecutar el siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="43290-235">You can open a command prompt as administrator, navigate to Java's bin folder, and then run:</span></span>
  >
  >     <span data-ttu-id="43290-236">java.exe -jar [la ruta de acceso del archivo jar de SQuirreL]</span><span class="sxs-lookup"><span data-stu-id="43290-236">java.exe -jar [the path of the SQuirreL jar file]</span></span>
5. <span data-ttu-id="43290-237">Haga clic en **Aceptar** para confirmar la creación del directorio de destino.</span><span class="sxs-lookup"><span data-stu-id="43290-237">Click **OK** to confirm creating the target directory.</span></span>
6. <span data-ttu-id="43290-238">El valor predeterminado es instalar los paquetes Standard y Base.</span><span class="sxs-lookup"><span data-stu-id="43290-238">The default setting is to install the Base and Standard packages.</span></span>  <span data-ttu-id="43290-239">Haga clic en **Siguiente**.</span><span class="sxs-lookup"><span data-stu-id="43290-239">Click **Next**.</span></span>
7. <span data-ttu-id="43290-240">Haga clic en **Siguiente** dos veces y, a continuación, en **Hecho**.</span><span class="sxs-lookup"><span data-stu-id="43290-240">Click **Next** twice, and then click **Done**.</span></span>

<span data-ttu-id="43290-241">**Para instalar al controlador de Phoenix**</span><span class="sxs-lookup"><span data-stu-id="43290-241">**To install the Phoenix driver**</span></span>

<span data-ttu-id="43290-242">El archivo jar del controlador de Phoenix se encuentra en el clúster de HBase.</span><span class="sxs-lookup"><span data-stu-id="43290-242">The phoenix driver jar file is located on the HBase cluster.</span></span> <span data-ttu-id="43290-243">La ruta de acceso es similar a la siguiente según las versiones:</span><span class="sxs-lookup"><span data-stu-id="43290-243">The path is similar to the following based on the versions:</span></span>

    C:\apps\dist\phoenix-4.0.0.2.1.11.0-2316\phoenix-4.0.0.2.1.11.0-2316-client.jar
<span data-ttu-id="43290-244">Debe copiarla en la estación de trabajo en la ruta de acceso [carpeta de instalación de SQuirreL]/lib.</span><span class="sxs-lookup"><span data-stu-id="43290-244">You need to copy it to your workstation under the [SQuirreL installation folder]/lib path.</span></span>  <span data-ttu-id="43290-245">La forma más sencilla es aplicar RDP en el clúster y, a continuación, usar las tareas de copia y pega de archivos (CTRL+C y CTRL+V) para copiarlo en su estación de trabajo.</span><span class="sxs-lookup"><span data-stu-id="43290-245">The easiest way is to RDP into the cluster, and then use file copy/paste (CTRL+C and CTRL+V) to copy it to your workstation.</span></span>

<span data-ttu-id="43290-246">**Para agregar un controlador de Phoenix a SQuirreL**</span><span class="sxs-lookup"><span data-stu-id="43290-246">**To add a Phoenix driver to SQuirreL**</span></span>

1. <span data-ttu-id="43290-247">Abra el cliente SQL SQuirreL desde la estación de trabajo.</span><span class="sxs-lookup"><span data-stu-id="43290-247">Open SQuirreL SQL Client from your workstation.</span></span>
2. <span data-ttu-id="43290-248">Haga clic en la ficha **Controlador** a la izquierda.</span><span class="sxs-lookup"><span data-stu-id="43290-248">Click the **Driver** tab on the left.</span></span>
3. <span data-ttu-id="43290-249">Desde el menú **Controladores**, haga clic en **Nuevo controlador**.</span><span class="sxs-lookup"><span data-stu-id="43290-249">From the **Drivers** menu, click **New Driver**.</span></span>
4. <span data-ttu-id="43290-250">Escriba la siguiente información:</span><span class="sxs-lookup"><span data-stu-id="43290-250">Enter the following information:</span></span>

   * <span data-ttu-id="43290-251">**Nombre**: Phoenix</span><span class="sxs-lookup"><span data-stu-id="43290-251">**Name**: Phoenix</span></span>
   * <span data-ttu-id="43290-252">**Dirección URL de ejemplo**: jdbc:phoenix:zookeeper2.contoso-hbase-eu.f5.internal.cloudapp.net</span><span class="sxs-lookup"><span data-stu-id="43290-252">**Example URL**: jdbc:phoenix:zookeeper2.contoso-hbase-eu.f5.internal.cloudapp.net</span></span>
   * <span data-ttu-id="43290-253">**Nombre de la clase**: org.apache.phoenix.jdbc.PhoenixDriver</span><span class="sxs-lookup"><span data-stu-id="43290-253">**Class Name**: org.apache.phoenix.jdbc.PhoenixDriver</span></span>

     > [!WARNING]
     > <span data-ttu-id="43290-254">Usuario todo en minúsculas en la dirección URL de ejemplo.</span><span class="sxs-lookup"><span data-stu-id="43290-254">User all lower case in the Example URL.</span></span> <span data-ttu-id="43290-255">Puede usar el cuórum de zookeeper completo en caso de que uno de ellos esté inactivo.</span><span class="sxs-lookup"><span data-stu-id="43290-255">You can use they full zookeeper quorum in case one of them is down.</span></span>  <span data-ttu-id="43290-256">Los nombres de host son zookeeper0, zookeeper1 y zookeeper2.</span><span class="sxs-lookup"><span data-stu-id="43290-256">The hostnames are zookeeper0, zookeeper1, and zookeeper2.</span></span>
     >
     >

     ![Controlador SQuirreL de HBase Phoenix para HDInsight][img-squirrel-driver]
5. <span data-ttu-id="43290-258">Haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="43290-258">Click **OK**.</span></span>

<span data-ttu-id="43290-259">**Para crear un alias para el clúster de HBase**</span><span class="sxs-lookup"><span data-stu-id="43290-259">**To create an alias to the HBase cluster**</span></span>

1. <span data-ttu-id="43290-260">Desde SQuirreL, haga clic en la pestaña **Alias** de la izquierda.</span><span class="sxs-lookup"><span data-stu-id="43290-260">From SQuirreL, Click the **Aliases** tab on the left.</span></span>
2. <span data-ttu-id="43290-261">Desde el menú **Alias**, haga clic en **Nuevo alias**.</span><span class="sxs-lookup"><span data-stu-id="43290-261">From the **Aliases** menu, click **New Alias**.</span></span>
3. <span data-ttu-id="43290-262">Escriba la siguiente información:</span><span class="sxs-lookup"><span data-stu-id="43290-262">Enter the following information:</span></span>

   * <span data-ttu-id="43290-263">**Nombre**: el nombre del clúster de HBase o de cualquier nombre que prefiera.</span><span class="sxs-lookup"><span data-stu-id="43290-263">**Name**: The name of the HBase cluster or any name you prefer.</span></span>
   * <span data-ttu-id="43290-264">**Controlador**: Phoenix.</span><span class="sxs-lookup"><span data-stu-id="43290-264">**Driver**: Phoenix.</span></span>  <span data-ttu-id="43290-265">Debe coincidir con el nombre del controlador que creó en el último procedimiento.</span><span class="sxs-lookup"><span data-stu-id="43290-265">This must match the driver name you created in the last procedure.</span></span>
   * <span data-ttu-id="43290-266">**Dirección URL**: se copia la dirección URL de la configuración del controlador.</span><span class="sxs-lookup"><span data-stu-id="43290-266">**URL**: The URL is copied from your driver configuration.</span></span> <span data-ttu-id="43290-267">Asegúrese de que al usuario está todo en minúsculas.</span><span class="sxs-lookup"><span data-stu-id="43290-267">Make sure to user all lower case.</span></span>
   * <span data-ttu-id="43290-268">**Nombre de usuario**: puede ser cualquier texto.</span><span class="sxs-lookup"><span data-stu-id="43290-268">**User name**: It can be any text.</span></span>  <span data-ttu-id="43290-269">Debido a que usa conectividad VPN aquí, el nombre de usuario no se usa en absoluto.</span><span class="sxs-lookup"><span data-stu-id="43290-269">Because you use VPN connectivity here, the user name is not used at all.</span></span>
   * <span data-ttu-id="43290-270">**Contraseña**: puede ser cualquier texto.</span><span class="sxs-lookup"><span data-stu-id="43290-270">**Password**: It can be any text.</span></span>

     ![Controlador SQuirreL de HBase Phoenix para HDInsight][img-squirrel-alias]
4. <span data-ttu-id="43290-272">Haga clic en **Probar**.</span><span class="sxs-lookup"><span data-stu-id="43290-272">Click **Test**.</span></span>
5. <span data-ttu-id="43290-273">Haga clic en **Conectar**.</span><span class="sxs-lookup"><span data-stu-id="43290-273">Click **Connect**.</span></span> <span data-ttu-id="43290-274">Cuando realiza la conexión, SQuirreL tendrá este aspecto:</span><span class="sxs-lookup"><span data-stu-id="43290-274">When it makes the connection, SQuirreL looks like:</span></span>

    ![SQuirreL de Phoenix HBase][img-squirrel]

<span data-ttu-id="43290-276">**Para ejecutar una prueba**</span><span class="sxs-lookup"><span data-stu-id="43290-276">**To run a test**</span></span>

1. <span data-ttu-id="43290-277">Haga clic en la pestaña **SQL** derecha junto a la pestaña **Objetos**.</span><span class="sxs-lookup"><span data-stu-id="43290-277">Click the **SQL** tab right next to the **Objects** tab.</span></span>
2. <span data-ttu-id="43290-278">Copie y pegue el código siguiente:</span><span class="sxs-lookup"><span data-stu-id="43290-278">Copy and paste the following code:</span></span>

        CREATE TABLE IF NOT EXISTS us_population (state CHAR(2) NOT NULL, city VARCHAR NOT NULL, population BIGINT  CONSTRAINT my_pk PRIMARY KEY (state, city))
3. <span data-ttu-id="43290-279">Haga clic en el botón Ejecutar.</span><span class="sxs-lookup"><span data-stu-id="43290-279">Click the run button.</span></span>

    ![SQuirreL de Phoenix HBase][img-squirrel-sql]
4. <span data-ttu-id="43290-281">Vuelva a la ficha **Objetos** .</span><span class="sxs-lookup"><span data-stu-id="43290-281">Switch back to the **Objects** tab.</span></span>
5. <span data-ttu-id="43290-282">Expanda el nombre de alias y, a continuación, expanda **TABLA**.</span><span class="sxs-lookup"><span data-stu-id="43290-282">Expand the alias name, and then expand **TABLE**.</span></span>  <span data-ttu-id="43290-283">Verá la nueva tabla que aparece debajo.</span><span class="sxs-lookup"><span data-stu-id="43290-283">You shall see the new table listed under.</span></span>

## <a name="next-steps"></a><span data-ttu-id="43290-284">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="43290-284">Next steps</span></span>
<span data-ttu-id="43290-285">En este artículo, ha aprendido cómo utilizar Phoenix Apache en HDInsight.</span><span class="sxs-lookup"><span data-stu-id="43290-285">In this article, you have learned how to use Apache Phoenix in HDInsight.</span></span>  <span data-ttu-id="43290-286">Para obtener más información, consulte:</span><span class="sxs-lookup"><span data-stu-id="43290-286">To learn more, see</span></span>

* <span data-ttu-id="43290-287">[Información general de HBase de HDInsight][hdinsight-hbase-overview]: HBase es una base de datos NoSQL de código abierto Apache basada en Hadoop que proporciona acceso aleatorio y una coherencia sólida para grandes cantidades de datos no estructurados y semiestructurados.</span><span class="sxs-lookup"><span data-stu-id="43290-287">[HDInsight HBase overview][hdinsight-hbase-overview]: HBase is an Apache, open-source, NoSQL database built on Hadoop that provides random access and strong consistency for large amounts of unstructured and semistructured data.</span></span>
* <span data-ttu-id="43290-288">[Aprovisionamiento de clústeres de HBase en Azure Virtual Network][hdinsight-hbase-provision-vnet]: con la integración de redes virtuales, los clústeres de HBase se pueden implementar en la misma red virtual que sus aplicaciones para que estas puedan comunicarse directamente con HBase.</span><span class="sxs-lookup"><span data-stu-id="43290-288">[Provision HBase clusters on Azure Virtual Network][hdinsight-hbase-provision-vnet]: With virtual network integration, HBase clusters can be deployed to the same virtual network as your applications so that applications can communicate with HBase directly.</span></span>
* <span data-ttu-id="43290-289">[Configuración de la replicación de HBase en HDInsight](hdinsight-hbase-replication.md): aprenda a configurar la replicación de HBase entre dos centros de datos de Azure.</span><span class="sxs-lookup"><span data-stu-id="43290-289">[Configure HBase replication in HDInsight](hdinsight-hbase-replication.md): Learn how to configure HBase replication across two Azure datacenters.</span></span>
* <span data-ttu-id="43290-290">[Análisis de sentimiento de Twitter con HBase en HDInsight][hbase-twitter-sentiment]: descubra cómo realizar [análisis de sentimiento](http://en.wikipedia.org/wiki/Sentiment_analysis) en tiempo real de macrodatos con HBase en un clúster de Hadoop en HDInsight.</span><span class="sxs-lookup"><span data-stu-id="43290-290">[Analyze Twitter sentiment with HBase in HDInsight][hbase-twitter-sentiment]: Learn how to do real-time [sentiment analysis](http://en.wikipedia.org/wiki/Sentiment_analysis) of big data by using HBase in a Hadoop cluster in HDInsight.</span></span>

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
