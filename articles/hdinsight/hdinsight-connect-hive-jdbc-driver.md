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
# <a name="query-hive-through-hello-jdbc-driver-in-hdinsight"></a>Consulta de Hive a través del controlador JDBC de hello en HDInsight

[!INCLUDE [ODBC-JDBC-selector](../../includes/hdinsight-selector-odbc-jdbc.md)]

Obtenga información acerca de cómo toouse controlador JDBC Hola desde un toosubmit de aplicación de Java Hive las consultas tooHadoop en HDInsight de Azure. información de Hello en este documento se muestra cómo tooconnect mediante programación y de hello ardilla SQL client.

Para obtener más información sobre Hola Hive interfaz de JDBC, consulte [HiveJDBCInterface](https://cwiki.apache.org/confluence/display/Hive/HiveJDBCInterface).

## <a name="prerequisites"></a>Requisitos previos

* Hadoop en un clúster de HDInsight. Se admiten tantos los clústeres basados en Windows como en Linux.

  > [!IMPORTANT]
  > Linux es Hola único sistema operativo usado en HDInsight versión 3.4 o superior. Para más información, vea la sección [Retirada de HDInsight 3.3](hdinsight-component-versioning.md#hdinsight-windows-retirement).

* [SQL SQuirreL](http://squirrel-sql.sourceforge.net/). SQuirreL es una aplicación de cliente JDBC.

* Hola [Kit de desarrollador de Java (JDK) versión 7](https://www.oracle.com/technetwork/java/javase/downloads/jdk7-downloads-1880260.html) o superior.

* [Apache Maven](https://maven.apache.org). Maven es un proyecto de compilar el sistema de proyectos de Java que se usa por proyecto Hola asociado a este artículo.

## <a name="jdbc-connection-string"></a>Cadena de conexión JDBC

Clúster de HDInsight de tooan de conexiones de JDBC en Azure se realizan en 443 y tráfico de Hola se protege utilizando SSL. Hola pública puerta de enlace que clústeres Hola se colocan detrás de redirige Hola tráfico toohello de puerto que está escuchando en HiveServer2. Hola te mostramos un ejemplo de cadena de conexión:

    jdbc:hive2://CLUSTERNAME.azurehdinsight.net:443/default;transportMode=http;ssl=true;httpPath=/hive2

Reemplace `CLUSTERNAME` con el nombre de Hola de su clúster de HDInsight.

## <a name="authentication"></a>Autenticación

Al establecer la conexión de hello, debe usar hello HDInsight clúster administración nombre y la contraseña tooauthenticate toohello clúster puerta de enlace. Cuando se conecta desde los clientes JDBC como ardilla SQL, debe escribir Hola nombre de administrador y la contraseña en la configuración de cliente.

Desde una aplicación Java, deberá usar Hola nombre y la contraseña al establecer una conexión. Por ejemplo, hello código Java siguiente abre una nueva conexión mediante la cadena de conexión de hello, nombre de administrador y contraseña:

```java
DriverManager.getConnection(connectionString,clusterAdmin,clusterPassword);
```

## <a name="connect-with-squirrel-sql-client"></a>Conexión con el cliente SQL SQuirreL

Ardilla SQL es un cliente JDBC que puede ser utilizados tooremotely ejecutar consultas de Hive con el clúster de HDInsight. Hello siguientes pasos se supone que ya ha instalado SQL ardilla.

1. Copie los controladores JDBC Hive Hola desde el clúster de HDInsight.

    * Para **HDInsight basados en Linux**, use Hola siguientes pasos le indican archivos jar de toodownload Hola necesario.

        1. Cree un directorio que contiene archivos de Hola. Por ejemplo: `mkdir hivedriver`.

        2. Desde una línea de comandos siguiente de hello use comandos toocopy los archivos de Hola de clúster de HDInsight de hello:

            ```bash
            scp USERNAME@CLUSTERNAME:/usr/hdp/current/hive-client/lib/hive-jdbc*standalone.jar .
            scp USERNAME@CLUSTERNAME:/usr/hdp/current/hadoop-client/hadoop-common.jar .
            scp USERNAME@CLUSTERNAME:/usr/hdp/current/hadoop-client/hadoop-auth.jar .
            ```

            Reemplace `USERNAME` con el nombre de cuenta de usuario SSH de hello para el clúster de Hola. Reemplace `CLUSTERNAME` con el nombre de clúster de HDInsight Hola.

    * Para **HDInsight basados en Windows**, use Hola siguientes pasos le indican archivos jar de toodownload Hola.

        1. En hello portal de Azure, seleccione el clúster de HDInsight y, a continuación, seleccione hello **escritorio remoto** icono.

            ![Icono de escritorio remoto](./media/hdinsight-connect-hive-jdbc-driver/remotedesktopicon.png)

        2. En la hoja de escritorio remoto de hello, utilice hello **conectar** tooconnect toohello grupo. Si no está habilitado Escritorio remoto hello, utilizar Hola formulario tooprovide un nombre de usuario y una contraseña, a continuación, seleccione **habilitar** tooenable escritorio remoto para el clúster de Hola.

            ![Hoja de escritorio remoto](./media/hdinsight-connect-hive-jdbc-driver/remotedesktopblade.png)

            Después de seleccionar **Conectar**, se descargará un archivo .rdp. Utilice a este cliente de escritorio remoto de archivo toolaunch Hola. Cuando se le solicite, utilice el nombre de usuario de Hola y la contraseña que especificó para el acceso de escritorio remoto.

        3. Una vez conectado, copie Hola siguientes archivos desde el equipo local del tooyour de sesión de hello escritorio remoto. Póngalos en un directorio local denominado `hivedriver`.

            * C:\apps\dist\hive-0.14.0.2.2.9.1-7\lib\hive-jdbc-0.14.0.2.2.9.1-7-standalone.jar
            * C:\apps\dist\hadoop-2.6.0.2.2.9.1-7\share\hadoop\common\hadoop-common-2.6.0.2.2.9.1-7.jar
            * C:\apps\dist\hadoop-2.6.0.2.2.9.1-7\share\hadoop\common\lib\hadoop-auth-2.6.0.2.2.9.1-7.jar

            > [!NOTE]
            > versión de Hola números incluidos en las rutas de acceso de Hola y nombres de archivo pueden ser diferentes para el clúster.

        4. Desconectar la sesión de escritorio remoto de hello cuando haya terminado de copiar los archivos de saludo.

2. Iniciar aplicación de hello ardilla SQL. Desde la izquierda de Hola de ventana hello, seleccione **controladores**.

    ![Ficha controladores en hello izquierda de la ventana hello](./media/hdinsight-connect-hive-jdbc-driver/squirreldrivers.png)

3. Entre los iconos de hello en parte superior de Hola de hello **controladores** cuadro de diálogo, seleccione hello  **+**  icono toocreate un controlador.

    ![Iconos de controladores](./media/hdinsight-connect-hive-jdbc-driver/driversicons.png)

4. En el cuadro de diálogo de Agregar controlador hello, agregue Hola siguiente información:

    * **Name** (Nombre): Hive.
    * **Example URL** (URL de ejemplo): `jdbc:hive2://localhost:443/default;transportMode=http;ssl=true;httpPath=/hive2`
    * **Ruta de acceso de clase adicional**: archivos de uso Hola Agregar botón tooadd Hola jar descargan anteriormente
    * **Class Name** (Nombre de clase): org.apache.hive.jdbc.HiveDriver.

   ![cuadro de diálogo para agregar controlador](./media/hdinsight-connect-hive-jdbc-driver/adddriver.png)

   Haga clic en **Aceptar** toosave esta configuración.

5. Hola izquierda de la ventana de hello ardilla SQL, selecciona **alias**. A continuación, haga clic en hello  **+**  toocreate icono un alias de conexión.

    ![agregar nuevo alias](./media/hdinsight-connect-hive-jdbc-driver/aliases.png)

6. Los valores siguientes de Hola de uso para hello **agregar Alias** cuadro de diálogo.

    * **Name** (Nombre): Hive en HDInsight.

    * **Controlador**: Hola de uso Hola desplegable tooselect **Hive** controlador

    * **Dirección URL**: jdbc:hive2://CLUSTERNAME.azurehdinsight.net:443/default;transportMode=http;ssl=true;httpPath=/hive2

        Reemplace **CLUSTERNAME** con el nombre de Hola de su clúster de HDInsight.

    * **Nombre de usuario**: nombre de cuenta de inicio de sesión de clúster de hello para el clúster de HDInsight. valor predeterminado de Hello es `admin`.

    * **Contraseña**: contraseña de Hola de cuenta de inicio de sesión de clúster de Hola.

 ![cuadro de diálogo para agregar alias](./media/hdinsight-connect-hive-jdbc-driver/addalias.png)

    Hola de uso **prueba** tooverify de botón que Hola conexión funciona. Cuando **conectarse: Hive en HDInsight** aparece el cuadro de diálogo, seleccione **conectar** prueba de hello tooperform. Si prueba Hola se realiza correctamente, verá un **conexión correcta** cuadro de diálogo.

    conexión de hello toosave usar alias, hello **Aceptar** situado en la parte inferior de Hola de hello **agregar Alias** cuadro de diálogo.

7. De hello **conectarse a** seleccione de la lista desplegable situada en la parte superior de Hola de SQL ardilla, **Hive en HDInsight**. Cuando se le pida, seleccione **Connect** (Conectar).

    ![cuadro de diálogo de conexión](./media/hdinsight-connect-hive-jdbc-driver/connect.png)

8. Una vez conectado, escriba Hola siguiente consulta en el cuadro de diálogo de consulta SQL de hello y, a continuación, seleccione hello **ejecutar** icono. área de resultados de Hola debe mostrar resultados de Hola de consulta de Hola.

        select * from hivesampletable limit 10;

    ![cuadro de diálogo de consulta de SQL, incluidos los resultados](./media/hdinsight-connect-hive-jdbc-driver/sqlquery.png)

## <a name="connect-from-an-example-java-application"></a>Conexión desde una aplicación de Java de ejemplo

Un ejemplo del uso de un tooquery de cliente de Java Hive en HDInsight está disponible en [https://github.com/Azure-Samples/hdinsight-java-hive-jdbc](https://github.com/Azure-Samples/hdinsight-java-hive-jdbc). Siga las instrucciones de hello en hello repositorio toobuild y ejecutar el ejemplo de Hola.

## <a name="troubleshooting"></a>Solución de problemas

### <a name="unexpected-error-occurred-attempting-tooopen-an-sql-connection"></a>Produjo un Error inesperado tooopen intenta una conexión de SQL

**Síntomas**: cuando se conecta el clúster de HDInsight de tooan es la versión 3.3 o 3.4, recibirá un error que se produjo un error inesperado. seguimiento de la pila de Hola para este error comienza con hello siguientes líneas:

```java
java.util.concurrent.ExecutionException: java.lang.RuntimeException: java.lang.NoSuchMethodError: org.apache.commons.codec.binary.Base64.<init>(I)V
at java.util.concurrent.FutureTas...(FutureTask.java:122)
at java.util.concurrent.FutureTask.get(FutureTask.java:206)
```

**Causa**: este error se debe a una incoherencia en la versión de Hola de hello commons codec.jar archivo utilizado por hello uno requerido por componentes de JDBC Hive hello y ardilla.

**Resolución**: toofix este error, Hola uso siguiendo los pasos:

1. Descargar archivo jar de hello commons códec de su clúster de HDInsight.

        scp USERNAME@CLUSTERNAME:/usr/hdp/current/hive-client/lib/commons-codec*.jar ./commons-codec.jar

2. Salir ardilla y, a continuación, vaya a directorio toohello donde ardilla está instalado en el sistema. En hello ardilla directorio, hello `lib` directorio, replace Hola existente commons-codec.jar con hello una descarga desde el clúster de HDInsight de Hola.

3. Reinicie SQuirreL. error de Hello ya no debería producirse cuando se conecta tooHive en HDInsight.

## <a name="next-steps"></a>Pasos siguientes

Ahora que ha aprendido cómo toouse JDBC toowork con Hive, Hola de uso siguiente vincula tooexplore otro toowork maneras con HDInsight de Azure.

* [Cargar datos tooHDInsight](hdinsight-upload-data.md)
* [Uso de Hive con HDInsight](hdinsight-use-hive.md)
* [Uso de Pig con HDInsight](hdinsight-use-pig.md)
* [Uso de trabajos de MapReduce con HDInsight](hdinsight-use-mapreduce.md)
