---
title: "clústeres de hello aaaUse toocreate portal Azure HDInsight de Azure con el almacén de Data Lake | Documentos de Microsoft"
description: "Usar hello toocreate de portal de Azure y usar clústeres de HDInsight con el almacén de Azure Data Lake"
services: data-lake-store,hdinsight
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
ms.assetid: a8c45a83-a8e3-4227-8b02-1bc1e1de6767
ms.service: data-lake-store
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 08/14/2017
ms.author: nitinme
ms.openlocfilehash: f23113d444a3c5a01894dba29f75f3621b2d16bd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="create-hdinsight-clusters-with-data-lake-store-by-using-hello-azure-portal"></a>Crear clústeres de HDInsight con el almacén de Data Lake mediante Hola portal de Azure
> [!div class="op_single_selector"]
> * [Usar hello portal de Azure](data-lake-store-hdinsight-hadoop-use-portal.md)
> * [Uso de PowerShell (para el almacenamiento predeterminado)](data-lake-store-hdinsight-hadoop-use-powershell-for-default-storage.md)
> * [Uso de PowerShell (para almacenamiento adicional)](data-lake-store-hdinsight-hadoop-use-powershell.md)
> * [Uso de Resource Manager](data-lake-store-hdinsight-hadoop-use-resource-manager-template.md)
>
>

Obtenga información acerca de cómo toouse Hola toocreate portal Azure un clúster de HDInsight con una cuenta de almacén de Azure Data Lake como almacenamiento predeterminado de Hola o un almacenamiento adicional. Aunque es opcional para un clúster de HDInsight almacenamiento adicional, es recomendable toostore sus datos empresariales en las cuentas de almacenamiento adicional de Hola.

## <a name="prerequisites"></a>Requisitos previos
Antes de comenzar este tutorial, asegúrese de que se ha cumplido hello según los requisitos:

* **Una suscripción de Azure**. Vaya demasiado[evaluación gratuita de Azure obtener](https://azure.microsoft.com/pricing/free-trial/).
* **Una cuenta de Almacén de Azure Data Lake**. Siga las instrucciones de Hola de [empezar a trabajar con el almacén de Azure Data Lake utilizando Hola portal de Azure](data-lake-store-get-started-portal.md). También debe crear una carpeta raíz en la cuenta de hello.  En este tutorial se usa una carpeta raíz llamada __/clusters__.
* **Una entidad de servicio de Azure Active Directory**. Este tutorial proporciona instrucciones sobre cómo toocreate una entidad de servicio en Azure Active Directory (Azure AD). Sin embargo, toocreate una entidad de servicio, debe ser un administrador de Azure AD. Si es administrador, puede omitir este requisito previo y continuar con tutorial Hola.

    >[!NOTE]
    >Solamente puede crear una entidad de servicio si es administrador de Azure AD. Su administrador de Azure AD debe generar una entidad de servicio antes de crear un clúster de HDInsight con Data Lake Store. Además, entidad de servicio de hello debe crearse con un certificado, como se describe en [crear una entidad de servicio con el certificado](../azure-resource-manager/resource-group-authenticate-service-principal.md#create-service-principal-with-self-signed-certificate).
    >

## <a name="create-an-hdinsight-cluster"></a>Creación de un clúster de HDInsight

En esta sección, creará un clúster de HDInsight con las cuentas de almacén de Data Lake como valor predeterminado de Hola o almacenamiento adicional de Hola. Este artículo trata sólo parte de saludo de la configuración de cuentas de almacén de Data Lake.  Para obtener información de creación de clúster general de Hola y procedimientos, consulte [Hadoop crear clústeres de HDInsight](../hdinsight/hdinsight-hadoop-provision-linux-clusters.md).

### <a name="create-a-cluster-with-data-lake-store-as-default-storage"></a>Creación de un clúster con Data Lake Store como almacenamiento predeterminado

**toocreate HDInsight de un clúster con un almacén de Data Lake como cuenta de almacenamiento predeterminada de Hola**

1. Inicie sesión en toohello [portal de Azure](https://portal.azure.com).
2. Siga [crear clústeres](../hdinsight/hdinsight-hadoop-create-linux-clusters-portal.md#create-clusters) para obtener información general sobre la creación de clústeres de HDInsight Hola.
3. En hello **almacenamiento** hoja, en **tipo de almacenamiento principal**, seleccione **almacén de Data Lake**y, a continuación, escriba Hola siguiente información:

    ![Agregar servicio de cluster Server tooHDInsight principal](./media/data-lake-store-hdinsight-hadoop-use-portal/hdi.adl.1.adls.storage.png "Agregar servicio de cluster Server tooHDInsight principal")

    - **Seleccionar la cuenta de Data Lake Store**: seleccione una cuenta existente de Data Lake Store. Se necesita una cuenta existente de Data Lake Store.  Consulte [Requisitos previos](#prereuisites).
    - **Ruta de acceso raíz**: escriba una ruta de acceso donde archivos específicos para clúster de hello son toobe almacenado. En la captura de pantalla de hello, es __/clústeres/myhdiadlcluster/__, en qué hello __/clústeres__ carpeta debe existir y crea hello Portal *myhdicluster* carpeta.  Hola *myhdicluster* es el nombre del clúster de Hola.
    - **Acceso de almacén de Data Lake**: configurar el acceso entre cuentas de almacén de Data Lake hello y clúster de HDInsight. Para obtener instrucciones, consulte [Configuración del acceso a Data Lake Store](#configure-data-lake-store-access).
    - **Cuentas de almacenamiento adicionales**: cuentas de agregar cuentas de almacenamiento de Azure como almacenamiento adicional para clúster Hola. tooadd adicionales datos Lake almacenes se debe conceder permisos de clúster de hello en los datos en varias cuentas de almacén de Data Lake al configurar una cuenta de almacén de Data Lake como tipo de almacenamiento principal de Hola. Consulte [Configuración del acceso a Data Lake Store](#configure-data-lake-store-access).

4. En hello **acceso de almacén de Data Lake**, haga clic en **seleccione**y, a continuación, continuar con la creación del clúster tal y como se describe en [Hadoop crear clústeres de HDInsight](../hdinsight/hdinsight-hadoop-create-linux-clusters-portal.md).


### <a name="create-a-cluster-with-data-lake-store-as-additional-storage"></a>Creación de un clúster con Data Lake Store como almacenamiento adicional

Hello las instrucciones siguientes crear un clúster de HDInsight con una cuenta de almacenamiento de Azure como almacenamiento predeterminado de hello y una cuenta de almacén de Data Lake como un almacenamiento adicional.
**toocreate HDInsight de un clúster con un almacén de Data Lake como cuenta de almacenamiento predeterminada de Hola**

1. Inicie sesión en toohello [portal de Azure](https://portal.azure.com).
2. Siga [crear clústeres](../hdinsight/hdinsight-hadoop-create-linux-clusters-portal.md#create-clusters) para obtener información general sobre la creación de clústeres de HDInsight Hola.
3. En hello **almacenamiento** hoja, en **tipo de almacenamiento principal**, seleccione **el almacenamiento de Azure**y, a continuación, escriba Hola siguiente información:

    ![Agregar servicio de cluster Server tooHDInsight principal](./media/data-lake-store-hdinsight-hadoop-use-portal/hdi.adl.1.png "Agregar servicio de cluster Server tooHDInsight principal")

    - **Método de selección**: usar una de las siguientes opciones de hello:

        * Seleccione una cuenta de almacenamiento que forma parte de su suscripción de Azure, toospecify **Mis suscripciones**y, a continuación, seleccione la cuenta de almacenamiento de Hola.
        * una cuenta de almacenamiento que está fuera de su suscripción de Azure, seleccione toospecify **clave de acceso**y, a continuación, proporcionar información de Hola para hello fuera de la cuenta de almacenamiento.

    - **Contenedor predeterminado**: usar valor predeterminado Hola o especificar su propio nombre.

    - Cuentas de almacenamiento adicionales: agregar más cuentas de almacenamiento de Azure como almacenamiento adicional de Hola.
    - Acceso de almacén de Data Lake: configurar el acceso entre cuentas de almacén de Data Lake hello y clúster de HDInsight. Para obtener instrucciones, consulte [Configuración del acceso a Data Lake Store](#configure-data-lake-store-access).

## <a name="configure-data-lake-store-access"></a>Configuración del acceso a Data Lake Store 

En esta sección podrá configurar el acceso a Data Lake Store desde los clústeres de HDInsight mediante una entidad de servicio de Azure Active Directory. 

### <a name="specify-a-service-principal"></a>Especificar una entidad de servicio

De hello portal de Azure, puede usar a una entidad de servicio existente o cree uno nuevo.

**toocreate una entidad de servicio de hello portal de Azure**

1. Haga clic en **acceso de almacén de Data Lake** de hoja de almacén de Hola.
2. En hello **acceso de almacén de Data Lake** hoja, haga clic en **crear nuevo**.
3. Haga clic en **entidad de servicio**y, a continuación, siga Hola instrucciones toocreate una entidad de servicio.
4. Descargar certificado de hello si decide toouse en hello futuras. Descargando certificado de hello es útil que si desea toouse Hola mismo servicio de entidad de seguridad al crear clústeres de HDInsight adicionales.

    ![Agregar servicio de cluster Server tooHDInsight principal](./media/data-lake-store-hdinsight-hadoop-use-portal/hdi.adl.2.png "Agregar servicio de cluster Server tooHDInsight principal")

4. Haga clic en **acceso** acceso a la carpeta tooconfigure Hola.  Consulte [Configurar los permisos de los archivos](#configure-file-permissions).


**toouse un servicio existente principal de hello portal de Azure**

1. Haga clic en **Acceso a Data Lake Store**.
1. En hello **acceso de almacén de Data Lake** hoja, haga clic en **utilizar existente**.
2. Haga clic en **Entidad de servicio** y seleccione una entidad de servicio. 
3. Cargar certificado de hello (archivo .pfx) que está asociado con la entidad de seguridad de servicio seleccionado y, a continuación, escriba la contraseña del certificado Hola.

    ![Agregar servicio de cluster Server tooHDInsight principal](./media/data-lake-store-hdinsight-hadoop-use-portal/hdi.adl.5.png "Agregar servicio de cluster Server tooHDInsight principal")

4. Haga clic en **acceso** acceso a la carpeta tooconfigure Hola.  Consulte [Configurar los permisos de los archivos](#configure-file-permissions).


### <a name="configure-file-permissions"></a>Configurar los permisos de los archivos

Hola configura son diferentes dependiendo de si se utiliza la cuenta de hello como almacenamiento predeterminado de Hola o una cuenta de almacenamiento adicional:

- Uso como almacenamiento predeterminado

    - permiso de nivel de raíz de Hola de hello cuenta de almacén de Data Lake
    - permiso de nivel de raíz de Hola de hello almacenamiento de clúster de HDInsight. Por ejemplo, hello __/clústeres__ carpeta utilizada anteriormente en el tutorial Hola.
- Uso como almacenamiento adicional

    - Permiso en las carpetas de Hola donde se necesita acceso de archivo.

**tooassign permiso en el nivel de raíz de cuenta de almacén de Data Lake Hola**

1. En hello **acceso de almacén de Data Lake** hoja, haga clic en **acceso**. Hola **seleccionar los permisos de archivo** se abre la hoja. Muestra todas las cuentas de almacén de Data Lake hello en su suscripción.
2. Mantenga el mouse (no haga clic en) mouse Hola sobre nombre Hola de hello cuenta de almacén de Data Lake toomake Hola casilla visible, a continuación, seleccione Hola casilla de verificación.

    ![Agregar servicio de cluster Server tooHDInsight principal](./media/data-lake-store-hdinsight-hadoop-use-portal/hdi.adl.3.png "Agregar servicio de cluster Server tooHDInsight principal")

  De forma predeterminada, los permisos __LECTURA__, __ESCRITURA__ Y __EJECUCIÓN__ están seleccionados.

3. Haga clic en **seleccione** en parte inferior de Hola de página de Hola.
4. Haga clic en **ejecutar** tooassign permiso.
5. Haga clic en **Done**(Listo).

**permiso de tooassign en hello nivel de raíz del clúster de HDInsight**

1. En hello **acceso de almacén de Data Lake** hoja, haga clic en **acceso**. Hola **seleccionar los permisos de archivo** se abre la hoja. Muestra todas las cuentas de almacén de Data Lake hello en su suscripción.
1. De hello **seleccionar los permisos de archivo** hoja, haga clic en tooshow de nombre de almacén de Data Lake Hola su contenido.
2. Seleccione raíz de almacenamiento de clúster de HDInsight de hello seleccionando la casilla Hola izquierda Hola de carpeta de Hola. Según la captura de pantalla de toohello anteriormente, es de raíz de almacenamiento de clúster de hello __/clústeres__ carpeta que especificó al seleccionar almacén de Data Lake de hello como almacenamiento predeterminado.
3. Establecer permisos de hello en carpeta de Hola.  De forma predeterminada, los permisos LECTURA, ESCRITURA Y EJECUCIÓN están seleccionados.
4. Haga clic en **seleccione** en parte inferior de Hola de página de Hola.
5. Haga clic en **Ejecutar**.
6. Haga clic en **Done**(Listo).

Si está utilizando el almacén de Data Lake como almacenamiento adicional, debe asignar permiso únicamente para las carpetas de Hola que desea tooaccess de clúster de HDInsight Hola. Por ejemplo, en la siguiente captura de pantalla de hello, proporciona acceso sólo demasiado**hdiaddonstorage** carpeta en una cuenta de almacén de Data Lake.

![Asignar el clúster de HDInsight de toohello de permisos de entidad de seguridad de servicio](./media/data-lake-store-hdinsight-hadoop-use-portal/hdi.adl.3-1.png "clúster de HDInsight de toohello de permisos de entidad de seguridad de servicio de asignar")


## <a name="verify-cluster-set-up"></a>Comprobación de la configuración del clúster

Una vez completada la instalación de clúster de hello, en la hoja de clúster de hello, compruebe los resultados, realice una o ambas de hello pasos:

* tooverify Hola almacenamiento asociado para clúster hello es la cuenta de almacén de Data Lake Hola que especificó, haga clic en **cuentas de almacenamiento** en el panel izquierdo de Hola.

    ![Agregar servicio de cluster Server tooHDInsight principal](./media/data-lake-store-hdinsight-hadoop-use-portal/hdi.adl.6-1.png "Agregar servicio de cluster Server tooHDInsight principal")

* tooverify que Hola entidad de servicio está correctamente asociado con el clúster de HDInsight de hello, haga clic en **acceso de almacén de Data Lake** en el panel izquierdo de Hola.

    ![Agregar servicio de cluster Server tooHDInsight principal](./media/data-lake-store-hdinsight-hadoop-use-portal/hdi.adl.6.png "Agregar servicio de cluster Server tooHDInsight principal")


## <a name="examples"></a>Ejemplos

Una vez haya configurado el clúster de hello con almacén de Data Lake como su almacenamiento de información, consulte toothese entre los ejemplos de cómo toouse HDInsight el clúster tooanalyze Hola que se almacena en el almacén de Data Lake.

### <a name="run-a-hive-query-against-data-in-a-data-lake-store-as-primary-storage"></a>Ejecución de una consulta de Hive en datos de Data Lake Store (como almacenamiento principal)

toorun una consulta de Hive, utilice la interfaz de vistas de Hive de hello en el portal de Ambari Hola. Para obtener instrucciones sobre cómo se ve toouse Ambari Hive, consulte [Hola Use vista Hive con Hadoop en HDInsight](../hdinsight/hdinsight-hadoop-use-hive-ambari-view.md).

Cuando se trabaja con datos en un almacén de Data Lake, existen unos toochange de cadenas.

Si utiliza, por ejemplo, clúster de Hola que ha creado con el almacén de Data Lake como almacenamiento principal, datos de toohello de ruta de acceso de hello están: *adl: / / < data_lake_store_account_name > /azuredatalakestore.net/path/to/file*. Un toocreate de consulta de Hive una tabla de datos de ejemplo que se almacenan en la cuenta de almacén de Data Lake hello es similar a Hola siguiente instrucción:

    CREATE EXTERNAL TABLE websitelog (str string) LOCATION 'adl://hdiadlsstorage.azuredatalakestore.net/clusters/myhdiadlcluster/HdiSamples/HdiSamples/WebsiteLogSampleData/SampleLog/'

Descripciones:
* `adl://hdiadlstorage.azuredatalakestore.net/`es la raíz de Hola de hello cuenta de almacén de Data Lake.
* `/clusters/myhdiadlcluster`es la raíz de Hola Hola de datos de clúster que especificó al crear el clúster de Hola.
* `/HdiSamples/HdiSamples/WebsiteLogSampleData/SampleLog/`es la ubicación de hello del archivo de ejemplo de Hola que utilizó en la consulta de Hola.

### <a name="run-a-hive-query-against-data-in-a-data-lake-store-as-additional-storage"></a>Ejecución de una consulta de Hive en datos de Data Lake Store (como almacenamiento adicional)

Si clúster Hola que ha creado usa almacenamiento de blobs como almacenamiento de forma predeterminada, los datos de ejemplo de Hola no está contenidos en hello cuenta de almacén de Data Lake de Azure que se usa como almacenamiento adicional. En este caso, primero transferir datos de Hola de toohello de almacenamiento de blobs almacén de Data Lake y, a continuación, ejecutar consultas de hello tal y como se muestra en el anterior ejemplo de Hola.

Para obtener información sobre cómo toocopy desde almacenamiento de blobs tooa Data Lake almacén de datos, vea Hola siguientes artículos:

* [Usar datos de toocopy Distcp entre blobs de almacenamiento de Azure y almacén de Data Lake](data-lake-store-copy-data-wasb-distcp.md)
* [TooData Lake almacén de blobs de datos de uso AdlCopy toocopy desde el almacenamiento de Azure](data-lake-store-copy-data-azure-storage-blob.md)

### <a name="use-data-lake-store-with-a-spark-cluster"></a>Uso de Data Lake Store con un clúster de Spark
Puede usar otra Spark clúster toorun Spark de trabajos en los datos que se almacenan en un almacén de Data Lake. Para obtener más información, consulte [datos de uso HDInsight Spark clúster tooanalyze en almacén de Data Lake](../hdinsight/hdinsight-apache-spark-use-with-data-lake-store.md).


### <a name="use-data-lake-store-in-a-storm-topology"></a>Usar el Almacén de Data Lake en una topología de Storm
Puede usar datos de toowrite de almacén de Data Lake de saludo de una topología de Storm. Para obtener instrucciones sobre cómo tooachieve este escenario, vea [almacén de uso Azure Data Lake con Apache Storm con HDInsight](../hdinsight/hdinsight-storm-write-data-lake-store.md).

## <a name="see-also"></a>Otras referencias
* [PowerShell: Crear un toouse de clúster de HDInsight almacén de Data Lake](data-lake-store-hdinsight-hadoop-use-powershell.md)

[makecert]: https://msdn.microsoft.com/library/windows/desktop/ff548309(v=vs.85).aspx
[pvk2pfx]: https://msdn.microsoft.com/library/windows/desktop/ff550672(v=vs.85).aspx
