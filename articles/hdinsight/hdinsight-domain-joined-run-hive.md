---
title: aaaConfigure directivas de Hive en HDInsight Unidos a un dominio - Azure | Documentos de Microsoft
description: Aprenda a...
services: hdinsight
documentationcenter: 
author: saurinsh
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 3fade1e5-c2e1-4ad5-b371-f95caea23f6d
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 10/25/2016
ms.author: saurinsh
ms.openlocfilehash: 56f2bf9d872abc5f772b886fcf91c2e2422092f4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="configure-hive-policies-in-domain-joined-hdinsight-preview"></a>Configuración de directivas de Hive en HDInsight unido a un dominio (versión preliminar)
Obtenga información acerca de cómo las directivas de Apache Cazador tooconfigure de Hive. En este artículo, cree dos Cazador directivas toorestrict acceso toohello hivesampletable. Hola hivesampletable viene con clústeres de HDInsight. Después de haber configurado las directivas de hello, use Excel y ODBC driver tooconnect tooHive las tablas de HDInsight.

## <a name="prerequisites"></a>Requisitos previos
* Un clúster de HDInsight unido a un dominio. Consulte [Configure Domain-joined HDInsight clusters](hdinsight-domain-joined-configure.md) (Configuración de clústeres de HDInsight unidos a un dominio).
* Un equipo con Office 2016, Office 2013 Professional Plus, Office 2013 Pro Plus, Excel 365 Standalone u Office 2010 Professional Plus.

## <a name="connect-tooapache-ranger-admin-ui"></a>Conectar tooApache interfaz de usuario de administrador de Cazador
**tooconnect tooRanger administrador UI**

1. En un explorador, conéctese tooRanger administrador UI. Hola URL es https://&lt;ClusterName >.azurehdinsight.net/Ranger/.

   > [!NOTE]
   > Ranger usa credenciales diferentes de clúster de Hadoop. exploradores tooprevent utilizando credenciales almacenadas en caché de Hadoop, utilice nuevo navegador inprivate ventana tooconnect toohello interfaz de usuario de administrador de Cazador.
   >
   >
2. Inicie sesión con la contraseña y nombre de usuario de dominio de administrador de clúster de hello:

    ![Página principal de Ranger unido a un dominio de HDInsight](./media/hdinsight-domain-joined-run-hive/hdinsight-domain-joined-ranger-home-page.png)

    Actualmente, Ranger solo funciona con Yarn y Hive.

## <a name="create-domain-users"></a>Creación de usuarios del dominio
En [Configure Domain-joined HDInsight clusters](hdinsight-domain-joined-configure.md#create-and-configure-azure-ad-ds-for-your-azure-ad) (Configuración de clústeres de HDInsight unidos a un dominio), ha creado hiveruser1 y hiveuser2. Se usará la cuenta de usuario de dos de hello en este tutorial.

## <a name="create-ranger-policies"></a>Creación de directivas de Ranger
En esta sección creará dos directivas Ranger para acceder a hivesampletable. Se concede el permiso select en un conjunto diferente de columnas. Ambos usuarios se crearon en [Configure Domain-joined HDInsight clusters](hdinsight-domain-joined-configure.md#create-and-configure-azure-ad-ds-for-your-azure-ad) (Configuración de clústeres de HDInsight unidos a un dominio).  En la siguiente sección hello, probará dos directivas de hello en Excel.

**directivas de Cazador toocreate**

1. Abra la interfaz de usuario administrador de Ranger. Vea [conectar tooApache interfaz de usuario de administrador de Cazador](#connect-to-apache-ranager-admin-ui).
2. Haga clic en **&lt;nombreDeClúster>_hive**, en **Hive**. Deben aparecer dos directivas preconfiguradas.
3. Haga clic en **agregar nueva directiva**y, a continuación, escriba Hola siguientes valores:

   * Nombre de directiva: read-hivesampletable-all
   * Base de datos de Hive: default
   * tabla: hivesampletable
   * Columna de Hive: *
   * Seleccionar usuario: hiveuser1
   * Permisos: select

     ![Configuración de políticas de Hive para Ranger unido a un dominio de HDInsight](./media/hdinsight-domain-joined-run-hive/hdinsight-domain-joined-configure-ranger-policy.png).

     > [!NOTE]
     > Si un usuario de dominio no se rellena en Seleccionar usuarios, espere unos minutos para Cazador toosync con AAD.
     >
     >
4. Haga clic en **agregar** toosave directiva de Hola.
5. Repita Hola dos últimos pasos toocreate otra directiva con hello propiedades siguientes:

   * Nombre de directiva: read-hivesampletable-devicemake
   * Base de datos de Hive: default
   * tabla: hivesampletable
   * Columna de Hive: clientid, devicemake
   * Seleccionar usuario: hiveuser2
   * Permisos: select

## <a name="create-hive-odbc-data-source"></a>Creación de un origen de datos de Hive ODBC
Encontrará instrucciones de Hello en [origen de datos ODBC de Hive crear](hdinsight-connect-excel-hive-odbc-driver.md).  

    Propiedad|Description
    ---|---
    Data Source Name|Proporcionar a un origen de datos de nombre tooyour
    Host|Escriba &lt;NombreClústerHDInsight>.azurehdinsight.net. Por ejemplo, myHDICluster.azurehdinsight.net
    Port|Use <strong>443</strong>. (Este puerto se ha cambiado de too443 563).
    Base de datos|Use el <strong>valor predeterminado</strong>
    Hive Server Type|Seleccione <strong>Hive Server 2</strong>
    Mechanism|Seleccione <strong>Azure HDInsight Service</strong>
    HTTP Path|Deje este parámetro en blanco.
    User Name|Escriba hiveuser1@contoso158.onmicrosoft.com. Actualizar nombre de dominio de hello si es diferente.
    Password|Escriba la contraseña de Hola para hiveuser1.
    </table>

Asegúrese de que tooclick **prueba** antes de guardar el origen de datos de Hola.

## <a name="import-data-into-excel-from-hdinsight"></a>Importación de datos en Excel desde HDInsight
En la última sección de hello, configurar dos directivas.  hiveuser1 tiene Hola permiso select en todas las columnas de Hola y hiveuser2 tiene Hola permiso select en dos columnas. En esta sección, se suplantan Hola dos usuarios tooimport los datos en Excel.

1. Abra un libro de Excel nuevo o existente.
2. De hello **datos** , haga clic en **desde otros orígenes de datos**y, a continuación, haga clic en **desde el Asistente para la conexión de datos** toolaunch hello **Asistente para la conexión de datos**.

    ![Abrir el Asistente para la conexión de datos][img-hdi-simbahiveodbc.excel.dataconnection]
3. Seleccione **DSN de ODBC** como origen de datos de hello y, a continuación, haga clic en **siguiente**.
4. Orígenes de datos ODBC, Hola Seleccione origen de datos nombre que creó en el paso anterior de hello y, a continuación, haga clic en **siguiente**.
5. Volver a escribir contraseña de Hola para clúster hello en el Asistente de hello y, a continuación, haga clic en **Aceptar**. Espere hello **Seleccionar base de datos y tabla** tooopen del cuadro de diálogo. Esta operación puede tardar unos segundos.
6. Seleccione **hivesampletable** y haga clic en **Siguiente**.
7. Haga clic en **Finalizar**
8. Hola **importar datos** cuadro de diálogo, puede cambiar o especificar consultas Hola. por lo tanto, haga clic en la toodo **propiedades**. Esta operación puede tardar unos segundos.
9. Haga clic en hello **definición** texto del comando ficha hello es:

       SELECT * FROM "HIVE"."default"."hivesampletable"

   Directivas de Cazador Hola definiera, hiveuser1 tiene el permiso select en todas las columnas de Hola.  Por lo que esta consulta funciona con las credenciales del hiveuser1, pero no con las credenciales del hiveuser2.

   ![Propiedades de conexión][img-hdi-simbahiveodbc-excel-connectionproperties]
10. Haga clic en **Aceptar** cuadro de diálogo de propiedades de conexión de Hola de tooclose.
11. Haga clic en **Aceptar** tooclose hello **importar datos** cuadro de diálogo.  
12. Introducir la contraseña de Hola para hiveuser1 y, a continuación, haga clic en **Aceptar**. Tarda unos segundos antes de que los datos lleguen tooExcel importado. Cuando termine, verá 11 columnas de datos.

tootest Hola segunda directiva (lectura-hivesampletable-devicemake) que creó en la última sección de Hola

1. Agregue una nueva hoja de Excel.
2. Siga Hola último procedimiento tooimport Hola de datos.  deberá tomar único cambio de Hello es credenciales del toouse hiveuser2 en lugar de hiveuser1. Esto se producirá un error porque hiveuser2 sólo tiene dos columnas de toosee de permiso. Deberá obtener Hola siguiente error:

        [Microsoft][HiveODBC] (35) Error from Hive: error code: '40000' error message: 'Error while compiling statement: FAILED: HiveAccessControlException Permission denied: user [hiveuser2] does not have [SELECT] privilege on [default/hivesampletable/clientid,country ...]'.
3. Seguimiento Hola mismo datos tooimport de procedimiento. Esta vez, use las credenciales del hiveuser2 y modificar la instrucción select de Hola desde:

        SELECT * FROM "HIVE"."default"."hivesampletable"

    a:

        SELECT clientid, devicemake FROM "HIVE"."default"."hivesampletable"

    Cuando termine, verá dos columnas de datos importados.

## <a name="next-steps"></a>Pasos siguientes
* Para configurar un clúster de HDInsight unido a dominio, consulte [Configure Domain-joined HDInsight clusters](hdinsight-domain-joined-configure.md) (Configuración de clústeres de HDInsight unidos a un dominio).
* Para administrar los clústeres de HDInsight unidos a dominio, consulte [Manage Domain-joined HDInsight clusters](hdinsight-domain-joined-manage.md) (Administración de clústeres de HDInsight unidos a un dominio).
* Para ejecutar consultas de Hive mediante SSH en clústeres de HDInsight unidos a un dominio, consulte [Uso de SSH con HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md#domainjoined).
* Para conectarse de Hive mediante Hive JDBC, consulte [conectar tooHive en HDInsight de Azure con controlador de JDBC Hive Hola](hdinsight-connect-hive-jdbc-driver.md)
* Para conectar tooHadoop de Excel con ODBC Hive, consulte [tooHadoop Excel conectarse con hello unidad Microsoft Hive ODBC](hdinsight-connect-excel-hive-odbc-driver.md)
* Para conectar tooHadoop de Excel con Power Query, consulte [tooHadoop Excel conectarse mediante Power Query](hdinsight-connect-excel-power-query.md)
