---
title: "aaaQuery Hive a través del controlador JDBC hello - HDInsight de Azure | Documentos de Microsoft"
description: "Usar el controlador JDBC de Hola desde un tooHadoop de las consultas de Java aplicación toosubmit Hive en HDInsight. Conectar mediante programación y de cliente de SQL ardilla Hola."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 928f8d2a-684d-48cb-894c-11c59a5599ae
ms.service: hdinsight
ms.custom: hdinsightactive,hdiseo17may2017
ms.devlang: java
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 08/14/2017
ms.author: larryfr
ms.openlocfilehash: 93178da3b8d497faa4c788e91dba89c4e45d3fff
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="query-hive-through-hello-jdbc-driver-in-hdinsight"></a><span data-ttu-id="18e60-104">Consulta de Hive a través del controlador JDBC de hello en HDInsight</span><span class="sxs-lookup"><span data-stu-id="18e60-104">Query Hive through hello JDBC driver in HDInsight</span></span>

[!INCLUDE [ODBC-JDBC-selector](../../includes/hdinsight-selector-odbc-jdbc.md)]

<span data-ttu-id="18e60-105">Obtenga información acerca de cómo toouse controlador JDBC Hola desde un toosubmit de aplicación de Java Hive las consultas tooHadoop en HDInsight de Azure.</span><span class="sxs-lookup"><span data-stu-id="18e60-105">Learn how toouse hello JDBC driver from a Java application toosubmit Hive queries tooHadoop in Azure HDInsight.</span></span> <span data-ttu-id="18e60-106">información de Hello en este documento se muestra cómo tooconnect mediante programación y de hello ardilla SQL client.</span><span class="sxs-lookup"><span data-stu-id="18e60-106">hello information in this document demonstrates how tooconnect programmatically and from hello SQuirrel SQL client.</span></span>

<span data-ttu-id="18e60-107">Para obtener más información sobre Hola Hive interfaz de JDBC, consulte [HiveJDBCInterface](https://cwiki.apache.org/confluence/display/Hive/HiveJDBCInterface).</span><span class="sxs-lookup"><span data-stu-id="18e60-107">For more information on hello Hive JDBC Interface, see [HiveJDBCInterface](https://cwiki.apache.org/confluence/display/Hive/HiveJDBCInterface).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="18e60-108">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="18e60-108">Prerequisites</span></span>

* <span data-ttu-id="18e60-109">Hadoop en un clúster de HDInsight.</span><span class="sxs-lookup"><span data-stu-id="18e60-109">A Hadoop on HDInsight cluster.</span></span> <span data-ttu-id="18e60-110">Se admiten tantos los clústeres basados en Windows como en Linux.</span><span class="sxs-lookup"><span data-stu-id="18e60-110">Either Linux-based or Windows-based clusters work.</span></span>

  > [!IMPORTANT]
  > <span data-ttu-id="18e60-111">Linux es Hola único sistema operativo usado en HDInsight versión 3.4 o superior.</span><span class="sxs-lookup"><span data-stu-id="18e60-111">Linux is hello only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="18e60-112">Para más información, vea la sección [Retirada de HDInsight 3.3](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="18e60-112">For more information, see [HDInsight 3.3 retirement](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

* <span data-ttu-id="18e60-113">[SQL SQuirreL](http://squirrel-sql.sourceforge.net/).</span><span class="sxs-lookup"><span data-stu-id="18e60-113">[SQuirreL SQL](http://squirrel-sql.sourceforge.net/).</span></span> <span data-ttu-id="18e60-114">SQuirreL es una aplicación de cliente JDBC.</span><span class="sxs-lookup"><span data-stu-id="18e60-114">SQuirreL is a JDBC client application.</span></span>

* <span data-ttu-id="18e60-115">Hola [Kit de desarrollador de Java (JDK) versión 7](https://www.oracle.com/technetwork/java/javase/downloads/jdk7-downloads-1880260.html) o superior.</span><span class="sxs-lookup"><span data-stu-id="18e60-115">hello [Java Developer Kit (JDK) version 7](https://www.oracle.com/technetwork/java/javase/downloads/jdk7-downloads-1880260.html) or higher.</span></span>

* <span data-ttu-id="18e60-116">[Apache Maven](https://maven.apache.org).</span><span class="sxs-lookup"><span data-stu-id="18e60-116">[Apache Maven](https://maven.apache.org).</span></span> <span data-ttu-id="18e60-117">Maven es un proyecto de compilar el sistema de proyectos de Java que se usa por proyecto Hola asociado a este artículo.</span><span class="sxs-lookup"><span data-stu-id="18e60-117">Maven is a project build system for Java projects that is used by hello project associated with this article.</span></span>

## <a name="jdbc-connection-string"></a><span data-ttu-id="18e60-118">Cadena de conexión JDBC</span><span class="sxs-lookup"><span data-stu-id="18e60-118">JDBC connection string</span></span>

<span data-ttu-id="18e60-119">Clúster de HDInsight de tooan de conexiones de JDBC en Azure se realizan en 443 y tráfico de Hola se protege utilizando SSL.</span><span class="sxs-lookup"><span data-stu-id="18e60-119">JDBC connections tooan HDInsight cluster on Azure are made over 443, and hello traffic is secured using SSL.</span></span> <span data-ttu-id="18e60-120">Hola pública puerta de enlace que clústeres Hola se colocan detrás de redirige Hola tráfico toohello de puerto que está escuchando en HiveServer2.</span><span class="sxs-lookup"><span data-stu-id="18e60-120">hello public gateway that hello clusters sit behind redirects hello traffic toohello port that HiveServer2 is actually listening on.</span></span> <span data-ttu-id="18e60-121">Hola te mostramos un ejemplo de cadena de conexión:</span><span class="sxs-lookup"><span data-stu-id="18e60-121">hello following is an example connection string:</span></span>

    jdbc:hive2://CLUSTERNAME.azurehdinsight.net:443/default;transportMode=http;ssl=true;httpPath=/hive2

<span data-ttu-id="18e60-122">Reemplace `CLUSTERNAME` con el nombre de Hola de su clúster de HDInsight.</span><span class="sxs-lookup"><span data-stu-id="18e60-122">Replace `CLUSTERNAME` with hello name of your HDInsight cluster.</span></span>

## <a name="authentication"></a><span data-ttu-id="18e60-123">Autenticación</span><span class="sxs-lookup"><span data-stu-id="18e60-123">Authentication</span></span>

<span data-ttu-id="18e60-124">Al establecer la conexión de hello, debe usar hello HDInsight clúster administración nombre y la contraseña tooauthenticate toohello clúster puerta de enlace.</span><span class="sxs-lookup"><span data-stu-id="18e60-124">When establishing hello connection, you must use hello HDInsight cluster admin name and password tooauthenticate toohello cluster gateway.</span></span> <span data-ttu-id="18e60-125">Cuando se conecta desde los clientes JDBC como ardilla SQL, debe escribir Hola nombre de administrador y la contraseña en la configuración de cliente.</span><span class="sxs-lookup"><span data-stu-id="18e60-125">When connecting from JDBC clients such as SQuirreL SQL, you must enter hello admin name and password in client settings.</span></span>

<span data-ttu-id="18e60-126">Desde una aplicación Java, deberá usar Hola nombre y la contraseña al establecer una conexión.</span><span class="sxs-lookup"><span data-stu-id="18e60-126">From a Java application, you must use hello name and password when establishing a connection.</span></span> <span data-ttu-id="18e60-127">Por ejemplo, hello código Java siguiente abre una nueva conexión mediante la cadena de conexión de hello, nombre de administrador y contraseña:</span><span class="sxs-lookup"><span data-stu-id="18e60-127">For example, hello following Java code opens a new connection using hello connection string, admin name, and password:</span></span>

```java
DriverManager.getConnection(connectionString,clusterAdmin,clusterPassword);
```

## <a name="connect-with-squirrel-sql-client"></a><span data-ttu-id="18e60-128">Conexión con el cliente SQL SQuirreL</span><span class="sxs-lookup"><span data-stu-id="18e60-128">Connect with SQuirreL SQL client</span></span>

<span data-ttu-id="18e60-129">Ardilla SQL es un cliente JDBC que puede ser utilizados tooremotely ejecutar consultas de Hive con el clúster de HDInsight.</span><span class="sxs-lookup"><span data-stu-id="18e60-129">SQuirreL SQL is a JDBC client that can be used tooremotely run Hive queries with your HDInsight cluster.</span></span> <span data-ttu-id="18e60-130">Hello siguientes pasos se supone que ya ha instalado SQL ardilla.</span><span class="sxs-lookup"><span data-stu-id="18e60-130">hello following steps assume that you have already installed SQuirreL SQL.</span></span>

1. <span data-ttu-id="18e60-131">Copie los controladores JDBC Hive Hola desde el clúster de HDInsight.</span><span class="sxs-lookup"><span data-stu-id="18e60-131">Copy hello Hive JDBC drivers from your HDInsight cluster.</span></span>

    * <span data-ttu-id="18e60-132">Para **HDInsight basados en Linux**, use Hola siguientes pasos le indican archivos jar de toodownload Hola necesario.</span><span class="sxs-lookup"><span data-stu-id="18e60-132">For **Linux-based HDInsight**, use hello following steps toodownload hello required jar files.</span></span>

        1. <span data-ttu-id="18e60-133">Cree un directorio que contiene archivos de Hola.</span><span class="sxs-lookup"><span data-stu-id="18e60-133">Create a directory that contains hello files.</span></span> <span data-ttu-id="18e60-134">Por ejemplo: `mkdir hivedriver`.</span><span class="sxs-lookup"><span data-stu-id="18e60-134">For example, `mkdir hivedriver`.</span></span>

        2. <span data-ttu-id="18e60-135">Desde una línea de comandos siguiente de hello use comandos toocopy los archivos de Hola de clúster de HDInsight de hello:</span><span class="sxs-lookup"><span data-stu-id="18e60-135">From a command line, use hello following commands toocopy hello files from hello HDInsight cluster:</span></span>

            ```bash
            scp USERNAME@CLUSTERNAME:/usr/hdp/current/hive-client/lib/hive-jdbc*standalone.jar .
            scp USERNAME@CLUSTERNAME:/usr/hdp/current/hadoop-client/hadoop-common.jar .
            scp USERNAME@CLUSTERNAME:/usr/hdp/current/hadoop-client/hadoop-auth.jar .
            ```

            <span data-ttu-id="18e60-136">Reemplace `USERNAME` con el nombre de cuenta de usuario SSH de hello para el clúster de Hola.</span><span class="sxs-lookup"><span data-stu-id="18e60-136">Replace `USERNAME` with hello SSH user account name for hello cluster.</span></span> <span data-ttu-id="18e60-137">Reemplace `CLUSTERNAME` con el nombre de clúster de HDInsight Hola.</span><span class="sxs-lookup"><span data-stu-id="18e60-137">Replace `CLUSTERNAME` with hello HDInsight cluster name.</span></span>

    * <span data-ttu-id="18e60-138">Para **HDInsight basados en Windows**, use Hola siguientes pasos le indican archivos jar de toodownload Hola.</span><span class="sxs-lookup"><span data-stu-id="18e60-138">For **Windows-based HDInsight**, use hello following steps toodownload hello jar files.</span></span>

        1. <span data-ttu-id="18e60-139">En hello portal de Azure, seleccione el clúster de HDInsight y, a continuación, seleccione hello **escritorio remoto** icono.</span><span class="sxs-lookup"><span data-stu-id="18e60-139">From hello Azure portal, select your HDInsight cluster, and then select hello **Remote Desktop** icon.</span></span>

            ![Icono de escritorio remoto](./media/hdinsight-connect-hive-jdbc-driver/remotedesktopicon.png)

        2. <span data-ttu-id="18e60-141">En la hoja de escritorio remoto de hello, utilice hello **conectar** tooconnect toohello grupo.</span><span class="sxs-lookup"><span data-stu-id="18e60-141">On hello Remote Desktop blade, use hello **Connect** button tooconnect toohello cluster.</span></span> <span data-ttu-id="18e60-142">Si no está habilitado Escritorio remoto hello, utilizar Hola formulario tooprovide un nombre de usuario y una contraseña, a continuación, seleccione **habilitar** tooenable escritorio remoto para el clúster de Hola.</span><span class="sxs-lookup"><span data-stu-id="18e60-142">If hello Remote Desktop is not enabled, use hello form tooprovide a user name and password, then select **Enable** tooenable Remote Desktop for hello cluster.</span></span>

            ![Hoja de escritorio remoto](./media/hdinsight-connect-hive-jdbc-driver/remotedesktopblade.png)

            <span data-ttu-id="18e60-144">Después de seleccionar **Conectar**, se descargará un archivo .rdp.</span><span class="sxs-lookup"><span data-stu-id="18e60-144">After selecting **Connect**, a .rdp file is downloaded.</span></span> <span data-ttu-id="18e60-145">Utilice a este cliente de escritorio remoto de archivo toolaunch Hola.</span><span class="sxs-lookup"><span data-stu-id="18e60-145">Use this file toolaunch hello Remote Desktop client.</span></span> <span data-ttu-id="18e60-146">Cuando se le solicite, utilice el nombre de usuario de Hola y la contraseña que especificó para el acceso de escritorio remoto.</span><span class="sxs-lookup"><span data-stu-id="18e60-146">When prompted, use hello user name and password you entered for Remote Desktop access.</span></span>

        3. <span data-ttu-id="18e60-147">Una vez conectado, copie Hola siguientes archivos desde el equipo local del tooyour de sesión de hello escritorio remoto.</span><span class="sxs-lookup"><span data-stu-id="18e60-147">Once connected, copy hello following files from hello Remote Desktop session tooyour local machine.</span></span> <span data-ttu-id="18e60-148">Póngalos en un directorio local denominado `hivedriver`.</span><span class="sxs-lookup"><span data-stu-id="18e60-148">Put them in a local directory named `hivedriver`.</span></span>

            * <span data-ttu-id="18e60-149">C:\apps\dist\hive-0.14.0.2.2.9.1-7\lib\hive-jdbc-0.14.0.2.2.9.1-7-standalone.jar</span><span class="sxs-lookup"><span data-stu-id="18e60-149">C:\apps\dist\hive-0.14.0.2.2.9.1-7\lib\hive-jdbc-0.14.0.2.2.9.1-7-standalone.jar</span></span>
            * <span data-ttu-id="18e60-150">C:\apps\dist\hadoop-2.6.0.2.2.9.1-7\share\hadoop\common\hadoop-common-2.6.0.2.2.9.1-7.jar</span><span class="sxs-lookup"><span data-stu-id="18e60-150">C:\apps\dist\hadoop-2.6.0.2.2.9.1-7\share\hadoop\common\hadoop-common-2.6.0.2.2.9.1-7.jar</span></span>
            * <span data-ttu-id="18e60-151">C:\apps\dist\hadoop-2.6.0.2.2.9.1-7\share\hadoop\common\lib\hadoop-auth-2.6.0.2.2.9.1-7.jar</span><span class="sxs-lookup"><span data-stu-id="18e60-151">C:\apps\dist\hadoop-2.6.0.2.2.9.1-7\share\hadoop\common\lib\hadoop-auth-2.6.0.2.2.9.1-7.jar</span></span>

            > [!NOTE]
            > <span data-ttu-id="18e60-152">versión de Hola números incluidos en las rutas de acceso de Hola y nombres de archivo pueden ser diferentes para el clúster.</span><span class="sxs-lookup"><span data-stu-id="18e60-152">hello version numbers included in hello paths and file names may be different for your cluster.</span></span>

        4. <span data-ttu-id="18e60-153">Desconectar la sesión de escritorio remoto de hello cuando haya terminado de copiar los archivos de saludo.</span><span class="sxs-lookup"><span data-stu-id="18e60-153">Disconnect hello Remote Desktop session once you have finished copying hello files.</span></span>

2. <span data-ttu-id="18e60-154">Iniciar aplicación de hello ardilla SQL.</span><span class="sxs-lookup"><span data-stu-id="18e60-154">Start hello SQuirreL SQL application.</span></span> <span data-ttu-id="18e60-155">Desde la izquierda de Hola de ventana hello, seleccione **controladores**.</span><span class="sxs-lookup"><span data-stu-id="18e60-155">From hello left of hello window, select **Drivers**.</span></span>

    ![Ficha controladores en hello izquierda de la ventana hello](./media/hdinsight-connect-hive-jdbc-driver/squirreldrivers.png)

3. <span data-ttu-id="18e60-157">Entre los iconos de hello en parte superior de Hola de hello **controladores** cuadro de diálogo, seleccione hello  **+**  icono toocreate un controlador.</span><span class="sxs-lookup"><span data-stu-id="18e60-157">From hello icons at hello top of hello **Drivers** dialog, select hello **+** icon toocreate a driver.</span></span>

    ![Iconos de controladores](./media/hdinsight-connect-hive-jdbc-driver/driversicons.png)

4. <span data-ttu-id="18e60-159">En el cuadro de diálogo de Agregar controlador hello, agregue Hola siguiente información:</span><span class="sxs-lookup"><span data-stu-id="18e60-159">In hello Add Driver dialog, add hello following information:</span></span>

    * <span data-ttu-id="18e60-160">**Name** (Nombre): Hive.</span><span class="sxs-lookup"><span data-stu-id="18e60-160">**Name**: Hive</span></span>
    * <span data-ttu-id="18e60-161">**Example URL** (URL de ejemplo): `jdbc:hive2://localhost:443/default;transportMode=http;ssl=true;httpPath=/hive2`</span><span class="sxs-lookup"><span data-stu-id="18e60-161">**Example URL**: `jdbc:hive2://localhost:443/default;transportMode=http;ssl=true;httpPath=/hive2`</span></span>
    * <span data-ttu-id="18e60-162">**Ruta de acceso de clase adicional**: archivos de uso Hola Agregar botón tooadd Hola jar descargan anteriormente</span><span class="sxs-lookup"><span data-stu-id="18e60-162">**Extra Class Path**: Use hello Add button tooadd hello jar files downloaded earlier</span></span>
    * <span data-ttu-id="18e60-163">**Class Name** (Nombre de clase): org.apache.hive.jdbc.HiveDriver.</span><span class="sxs-lookup"><span data-stu-id="18e60-163">**Class Name**: org.apache.hive.jdbc.HiveDriver</span></span>

   ![cuadro de diálogo para agregar controlador](./media/hdinsight-connect-hive-jdbc-driver/adddriver.png)

   <span data-ttu-id="18e60-165">Haga clic en **Aceptar** toosave esta configuración.</span><span class="sxs-lookup"><span data-stu-id="18e60-165">Click **OK** toosave these settings.</span></span>

5. <span data-ttu-id="18e60-166">Hola izquierda de la ventana de hello ardilla SQL, selecciona **alias**.</span><span class="sxs-lookup"><span data-stu-id="18e60-166">On hello left of hello SQuirreL SQL window, select **Aliases**.</span></span> <span data-ttu-id="18e60-167">A continuación, haga clic en hello  **+**  toocreate icono un alias de conexión.</span><span class="sxs-lookup"><span data-stu-id="18e60-167">Then click hello **+** icon toocreate a connection alias.</span></span>

    ![agregar nuevo alias](./media/hdinsight-connect-hive-jdbc-driver/aliases.png)

6. <span data-ttu-id="18e60-169">Los valores siguientes de Hola de uso para hello **agregar Alias** cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="18e60-169">Use hello following values for hello **Add Alias** dialog.</span></span>

    * <span data-ttu-id="18e60-170">**Name** (Nombre): Hive en HDInsight.</span><span class="sxs-lookup"><span data-stu-id="18e60-170">**Name**: Hive on HDInsight</span></span>

    * <span data-ttu-id="18e60-171">**Controlador**: Hola de uso Hola desplegable tooselect **Hive** controlador</span><span class="sxs-lookup"><span data-stu-id="18e60-171">**Driver**: Use hello dropdown tooselect hello **Hive** driver</span></span>

    * <span data-ttu-id="18e60-172">**Dirección URL**: jdbc:hive2://CLUSTERNAME.azurehdinsight.net:443/default;transportMode=http;ssl=true;httpPath=/hive2</span><span class="sxs-lookup"><span data-stu-id="18e60-172">**URL**: jdbc:hive2://CLUSTERNAME.azurehdinsight.net:443/default;transportMode=http;ssl=true;httpPath=/hive2</span></span>

        <span data-ttu-id="18e60-173">Reemplace **CLUSTERNAME** con el nombre de Hola de su clúster de HDInsight.</span><span class="sxs-lookup"><span data-stu-id="18e60-173">Replace **CLUSTERNAME** with hello name of your HDInsight cluster.</span></span>

    * <span data-ttu-id="18e60-174">**Nombre de usuario**: nombre de cuenta de inicio de sesión de clúster de hello para el clúster de HDInsight.</span><span class="sxs-lookup"><span data-stu-id="18e60-174">**User Name**: hello cluster login account name for your HDInsight cluster.</span></span> <span data-ttu-id="18e60-175">valor predeterminado de Hello es `admin`.</span><span class="sxs-lookup"><span data-stu-id="18e60-175">hello default is `admin`.</span></span>

    * <span data-ttu-id="18e60-176">**Contraseña**: contraseña de Hola de cuenta de inicio de sesión de clúster de Hola.</span><span class="sxs-lookup"><span data-stu-id="18e60-176">**Password**: hello password for hello cluster login account.</span></span>

 ![cuadro de diálogo para agregar alias](./media/hdinsight-connect-hive-jdbc-driver/addalias.png)

    <span data-ttu-id="18e60-178">Hola de uso **prueba** tooverify de botón que Hola conexión funciona.</span><span class="sxs-lookup"><span data-stu-id="18e60-178">Use hello **Test** button tooverify that hello connection works.</span></span> <span data-ttu-id="18e60-179">Cuando **conectarse: Hive en HDInsight** aparece el cuadro de diálogo, seleccione **conectar** prueba de hello tooperform.</span><span class="sxs-lookup"><span data-stu-id="18e60-179">When **Connect to: Hive on HDInsight** dialog appears, select **Connect** tooperform hello test.</span></span> <span data-ttu-id="18e60-180">Si prueba Hola se realiza correctamente, verá un **conexión correcta** cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="18e60-180">If hello test succeeds, you see a **Connection successful** dialog.</span></span>

    <span data-ttu-id="18e60-181">conexión de hello toosave usar alias, hello **Aceptar** situado en la parte inferior de Hola de hello **agregar Alias** cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="18e60-181">toosave hello connection alias, use hello **Ok** button at hello bottom of hello **Add Alias** dialog.</span></span>

7. <span data-ttu-id="18e60-182">De hello **conectarse a** seleccione de la lista desplegable situada en la parte superior de Hola de SQL ardilla, **Hive en HDInsight**.</span><span class="sxs-lookup"><span data-stu-id="18e60-182">From hello **Connect to** dropdown at hello top of SQuirreL SQL, select **Hive on HDInsight**.</span></span> <span data-ttu-id="18e60-183">Cuando se le pida, seleccione **Connect** (Conectar).</span><span class="sxs-lookup"><span data-stu-id="18e60-183">When prompted, select **Connect**.</span></span>

    ![cuadro de diálogo de conexión](./media/hdinsight-connect-hive-jdbc-driver/connect.png)

8. <span data-ttu-id="18e60-185">Una vez conectado, escriba Hola siguiente consulta en el cuadro de diálogo de consulta SQL de hello y, a continuación, seleccione hello **ejecutar** icono.</span><span class="sxs-lookup"><span data-stu-id="18e60-185">Once connected, enter hello following query into hello SQL query dialog, and then select hello **Run** icon.</span></span> <span data-ttu-id="18e60-186">área de resultados de Hola debe mostrar resultados de Hola de consulta de Hola.</span><span class="sxs-lookup"><span data-stu-id="18e60-186">hello results area should show hello results of hello query.</span></span>

        select * from hivesampletable limit 10;

    ![cuadro de diálogo de consulta de SQL, incluidos los resultados](./media/hdinsight-connect-hive-jdbc-driver/sqlquery.png)

## <a name="connect-from-an-example-java-application"></a><span data-ttu-id="18e60-188">Conexión desde una aplicación de Java de ejemplo</span><span class="sxs-lookup"><span data-stu-id="18e60-188">Connect from an example Java application</span></span>

<span data-ttu-id="18e60-189">Un ejemplo del uso de un tooquery de cliente de Java Hive en HDInsight está disponible en [https://github.com/Azure-Samples/hdinsight-java-hive-jdbc](https://github.com/Azure-Samples/hdinsight-java-hive-jdbc).</span><span class="sxs-lookup"><span data-stu-id="18e60-189">An example of using a Java client tooquery Hive on HDInsight is available at [https://github.com/Azure-Samples/hdinsight-java-hive-jdbc](https://github.com/Azure-Samples/hdinsight-java-hive-jdbc).</span></span> <span data-ttu-id="18e60-190">Siga las instrucciones de hello en hello repositorio toobuild y ejecutar el ejemplo de Hola.</span><span class="sxs-lookup"><span data-stu-id="18e60-190">Follow hello instructions in hello repository toobuild and run hello sample.</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="18e60-191">Solución de problemas</span><span class="sxs-lookup"><span data-stu-id="18e60-191">Troubleshooting</span></span>

### <a name="unexpected-error-occurred-attempting-tooopen-an-sql-connection"></a><span data-ttu-id="18e60-192">Produjo un Error inesperado tooopen intenta una conexión de SQL</span><span class="sxs-lookup"><span data-stu-id="18e60-192">Unexpected Error occurred attempting tooopen an SQL connection</span></span>

<span data-ttu-id="18e60-193">**Síntomas**: cuando se conecta el clúster de HDInsight de tooan es la versión 3.3 o 3.4, recibirá un error que se produjo un error inesperado.</span><span class="sxs-lookup"><span data-stu-id="18e60-193">**Symptoms**: When connecting tooan HDInsight cluster that is version 3.3 or 3.4, you may receive an error that an unexpected error occurred.</span></span> <span data-ttu-id="18e60-194">seguimiento de la pila de Hola para este error comienza con hello siguientes líneas:</span><span class="sxs-lookup"><span data-stu-id="18e60-194">hello stack trace for this error begins with hello following lines:</span></span>

```java
java.util.concurrent.ExecutionException: java.lang.RuntimeException: java.lang.NoSuchMethodError: org.apache.commons.codec.binary.Base64.<init>(I)V
at java.util.concurrent.FutureTas...(FutureTask.java:122)
at java.util.concurrent.FutureTask.get(FutureTask.java:206)
```

<span data-ttu-id="18e60-195">**Causa**: este error se debe a una incoherencia en la versión de Hola de hello commons codec.jar archivo utilizado por hello uno requerido por componentes de JDBC Hive hello y ardilla.</span><span class="sxs-lookup"><span data-stu-id="18e60-195">**Cause**: This error is caused by a mismatch in hello version of hello commons-codec.jar file used by SQuirreL and hello one required by hello Hive JDBC components.</span></span>

<span data-ttu-id="18e60-196">**Resolución**: toofix este error, Hola uso siguiendo los pasos:</span><span class="sxs-lookup"><span data-stu-id="18e60-196">**Resolution**: toofix this error, use hello following steps:</span></span>

1. <span data-ttu-id="18e60-197">Descargar archivo jar de hello commons códec de su clúster de HDInsight.</span><span class="sxs-lookup"><span data-stu-id="18e60-197">Download hello commons-codec jar file from your HDInsight cluster.</span></span>

        scp USERNAME@CLUSTERNAME:/usr/hdp/current/hive-client/lib/commons-codec*.jar ./commons-codec.jar

2. <span data-ttu-id="18e60-198">Salir ardilla y, a continuación, vaya a directorio toohello donde ardilla está instalado en el sistema.</span><span class="sxs-lookup"><span data-stu-id="18e60-198">Exit SQuirreL, and then go toohello directory where SQuirreL is installed on your system.</span></span> <span data-ttu-id="18e60-199">En hello ardilla directorio, hello `lib` directorio, replace Hola existente commons-codec.jar con hello una descarga desde el clúster de HDInsight de Hola.</span><span class="sxs-lookup"><span data-stu-id="18e60-199">In hello SquirreL directory, under hello `lib` directory, replace hello existing commons-codec.jar with hello one downloaded from hello HDInsight cluster.</span></span>

3. <span data-ttu-id="18e60-200">Reinicie SQuirreL.</span><span class="sxs-lookup"><span data-stu-id="18e60-200">Restart SQuirreL.</span></span> <span data-ttu-id="18e60-201">error de Hello ya no debería producirse cuando se conecta tooHive en HDInsight.</span><span class="sxs-lookup"><span data-stu-id="18e60-201">hello error should no longer occur when connecting tooHive on HDInsight.</span></span>

## <a name="next-steps"></a><span data-ttu-id="18e60-202">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="18e60-202">Next steps</span></span>

<span data-ttu-id="18e60-203">Ahora que ha aprendido cómo toouse JDBC toowork con Hive, Hola de uso siguiente vincula tooexplore otro toowork maneras con HDInsight de Azure.</span><span class="sxs-lookup"><span data-stu-id="18e60-203">Now that you have learned how toouse JDBC toowork with Hive, use hello following links tooexplore other ways toowork with Azure HDInsight.</span></span>

* [<span data-ttu-id="18e60-204">Cargar datos tooHDInsight</span><span class="sxs-lookup"><span data-stu-id="18e60-204">Upload data tooHDInsight</span></span>](hdinsight-upload-data.md)
* [<span data-ttu-id="18e60-205">Uso de Hive con HDInsight</span><span class="sxs-lookup"><span data-stu-id="18e60-205">Use Hive with HDInsight</span></span>](hdinsight-use-hive.md)
* [<span data-ttu-id="18e60-206">Uso de Pig con HDInsight</span><span class="sxs-lookup"><span data-stu-id="18e60-206">Use Pig with HDInsight</span></span>](hdinsight-use-pig.md)
* [<span data-ttu-id="18e60-207">Uso de trabajos de MapReduce con HDInsight</span><span class="sxs-lookup"><span data-stu-id="18e60-207">Use MapReduce jobs with HDInsight</span></span>](hdinsight-use-mapreduce.md)
