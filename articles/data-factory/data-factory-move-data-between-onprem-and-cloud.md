---
title: datos de aaaMove - Data Management Gateway | Documentos de Microsoft
description: Configurar una puerta de enlace de datos toomove datos entre hello y local en la nube. Utilice Data Management Gateway en toomove Data Factory de Azure los datos.
keywords: "puerta de enlace de datos, integración de datos, mover datos, credenciales de puerta de enlace"
services: data-factory
documentationcenter: 
author: nabhishek
manager: jhubbard
editor: monicar
ms.assetid: 7bf6d8fd-04b5-499d-bd19-eff217aa4a9c
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/27/2017
ms.author: abnarain
ms.openlocfilehash: 314341c142d5260c785b7e82081774f044450e81
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="move-data-between-on-premises-sources-and-hello-cloud-with-data-management-gateway"></a>Mover datos entre orígenes locales y en la nube Hola con Data Management Gateway
Este artículo proporciona información general sobre la integración de los almacenes de datos locales y los almacenes de datos en la nube mediante Data Factory. Se basa en hello [las actividades de movimiento de datos](data-factory-data-movement-activities.md) artículo y otros artículos de conceptos de núcleo de generador de datos: [conjuntos de datos](data-factory-create-datasets.md) y [canalizaciones](data-factory-create-pipelines.md).

## <a name="data-management-gateway"></a>Data Management Gateway
Debe instalar Data Management Gateway en su tooenable de máquina local mover datos desde un almacén de datos local. puerta de enlace de Hello puede instalarse en hello que mismo equipo como almacén de datos de Hola o en un equipo diferente como puerta de enlace de hello puede conectar el almacén de datos de toohello.

> [!IMPORTANT]
> Consulte el artículo [Data Management Gateway](data-factory-data-management-gateway.md) para más detalles sobre Data Management Gateway. 

Hello en el tutorial siguiente muestra cómo una factoría de datos con una canalización que mueve los datos de una implementación local de toocreate **SQL Server** tooan almacenamiento de blobs de Azure de la base de datos. Como parte del tutorial de hello, instalar y configurar Hola Data Management Gateway en su equipo.

## <a name="walkthrough-copy-on-premises-data-toocloud"></a>Tutorial: copiar toocloud de datos local
En este tutorial Hola lo siguiente: 

1. Creación de una factoría de datos.
2. Creación de una instancia de Data Management Gateway. 
3. Creación de servicios vinculados para los almacenes de datos de origen y receptor.
4. Creación de conjuntos de datos toorepresent entrada y salida de datos.
5. Crear una canalización con una copia actividad toomove Hola de datos.

## <a name="prerequisites-for-hello-tutorial"></a>Requisitos previos para el tutorial de Hola
Antes de comenzar este tutorial, debe tener Hola siguiendo los requisitos previos:

* **Suscripción de Azure**.  Si no tiene una suscripción, puede crear una cuenta de prueba gratuita en tan solo un par de minutos. Vea hello [gratuita](http://azure.microsoft.com/pricing/free-trial/) artículo para obtener más información.
* **Cuenta de almacenamiento de Azure**. Usar el almacenamiento de blobs de Hola como un **destino/receptor** almacén de datos en este tutorial. Si no tiene una cuenta de almacenamiento de Azure, vea hello [crear una cuenta de almacenamiento](../storage/common/storage-create-storage-account.md#create-a-storage-account) artículo para toocreate pasos uno.
* **SQL Server**. Use una base de datos de SQL Server local como almacén de datos de **origen** en este tutorial. 

## <a name="create-data-factory"></a>Creación de Data Factory
En este paso, utilice hello Azure toocreate portal una instancia de la factoría de datos de Azure denominada **ADFTutorialOnPremDF**.

1. Inicie sesión en toohello [portal de Azure](https://portal.azure.com).
2. Haga clic en **+ NUEVO**, en **Inteligencia y análisis** y en **Data Factory**.

   ![New->DataFactory](./media/data-factory-move-data-between-onprem-and-cloud/NewDataFactoryMenu.png)  
3. Hola **factoría de datos** escriba **ADFTutorialOnPremDF** para hello nombre.

    ![Agregar tooStartboard](./media/data-factory-move-data-between-onprem-and-cloud/OnPremNewDataFactoryAddToStartboard.png)

   > [!IMPORTANT]
   > nombre de Hola Hola Azure factoría de datos debe ser único globalmente. Si recibe el error hello: **nombre de generador de datos "ADFTutorialOnPremDF" no está disponible**, cambiar nombre de Hola Hola factoría de datos (por ejemplo, yournameADFTutorialOnPremDF) y pruebe a crear de nuevo. Use este nombre en lugar de ADFTutorialFactory al realizar los restantes pasos de este tutorial.
   >
   > nombre de Hola Hola factoría de datos se puede registrar como un **DNS** asigne un nombre en el futuro de hello y, por tanto, se convierten en visible públicamente.
   >
   >
4. Seleccione hello **suscripción de Azure** donde desea Hola datos generador toobe creado.
5. Seleccione un **grupo de recursos** existente o cree uno nuevo. Para ver tutorial Hola, cree un grupo de recursos denominado: **ADFTutorialResourceGroup**.
6. Haga clic en **crear** en hello **factoría de datos** página.

   > [!IMPORTANT]
   > instancias de la factoría de datos de toocreate, debe ser miembro del programa Hola a [colaborador de la factoría de datos](../active-directory/role-based-access-built-in-roles.md#data-factory-contributor) rol en el nivel de grupo de recursos/suscripción Hola.
   >
   >
7. Una vez completada la creación, vea hello **factoría de datos** página como se muestra en hello después de imagen:

   ![Página principal de Factoría de datos](./media/data-factory-move-data-between-onprem-and-cloud/OnPremDataFactoryHomePage.png)

## <a name="create-gateway"></a>Crear puerta de enlace
1. Hola **factoría de datos** página, haga clic en **autor e implementar** icono toolaunch hello **Editor** de factoría de datos de Hola.

    ![Mosaico Crear e implementar](./media/data-factory-move-data-between-onprem-and-cloud/author-deploy-tile.png)
2. Hola Editor de generador de datos, haga clic en **... Más** Hola barra de herramientas y, a continuación, haga clic en **nueva puerta de enlace de datos**. Como alternativa, puede hacer clic **puertas de enlace de datos** en Hola vista de árbol y haga clic en **nueva puerta de enlace de datos**.

   ![Nueva puerta de enlace de datos en la barra de herramientas](./media/data-factory-move-data-between-onprem-and-cloud/NewDataGateway.png)
3. Hola **crear** escriba **adftutorialgateway** para hello **nombre**y haga clic en **Aceptar**.     

    ![Página Crear puerta de enlace](./media/data-factory-move-data-between-onprem-and-cloud/OnPremCreateGatewayBlade.png)

    > [!NOTE]
    > En este tutorial, creará puerta de enlace lógica de hello con un único nodo (máquina de Windows local). Puede escalar horizontalmente una puerta de enlace de administración de datos mediante la asociación de varios máquinas locales con puerta de enlace de Hola. Puede escalar verticalmente aumentando el número de trabajos de movimiento de datos que pueden ejecutarse simultáneamente en un nodo. Esta característica también está disponible para una puerta de enlace lógica con un único nodo. Consulte el artículo [Escalado en Data Management Gateway en Azure Data Factory](data-factory-data-management-gateway-high-availability-scalability.md) para más información.  
4. Hola **configurar** página, haga clic en **instalar directamente en este equipo**. Esta acción descarga el paquete de instalación de Hola de puerta de enlace de hello, instala, configura y registra la puerta de enlace de hello en el equipo de Hola.  

   > [!NOTE]
   > Utilice Internet Explorer o un explorador web compatible con Microsoft ClickOnce.
   >
   > Si usas Chrome, vaya toohello [almacén web de Chrome](https://chrome.google.com/webstore/), buscar con la palabra clave "ClickOnce", elija una de las extensiones de ClickOnce hello e instalarlo.
   >
   > Hola mismo para Firefox (complemento de instalación). Haga clic en **menú Abrir** botón de barra de herramientas de hello (**tres líneas horizontales** en la esquina superior derecha de hello), haga clic en **complementos**, buscar con la palabra clave "ClickOnce", elija uno de Hola Extensiones de ClickOnce e instalarlo.    
   >
   >

    ![Puerta de enlace: página Configurar](./media/data-factory-move-data-between-onprem-and-cloud/OnPremGatewayConfigureBlade.png)

    De este modo es toodownload (un solo clic) de la manera más fácil de hello, instalar, configurar y registrar la puerta de enlace de hello en un solo paso. Puede ver hello **Administrador de configuración de Microsoft Data Management Gateway** aplicación está instalada en el equipo. También puede encontrar Hola ejecutable **ConfigManager.exe** en la carpeta de hello: **C:\Program Files\Microsoft datos administración Gateway\2.0\Shared**.

    También puede descargar e instalar puerta de enlace de manualmente mediante el uso de vínculos de hello en esta página y registrarla mediante la clave de Hola que aparece en hello **nueva clave** cuadro de texto.

    Vea [Data Management Gateway](data-factory-data-management-gateway.md) artículo para todos los detalles acerca de la puerta de enlace de Hola de Hola.

   > [!NOTE]
   > Debe ser un administrador en hello tooinstall de equipo local y configurar correctamente Hola Data Management Gateway. Puede agregar usuarios adicionales toohello **Data Management Gateway Users** grupo local de Windows. los miembros de Hola de este grupo pueden utilizar la puerta de enlace de hello Administrador de configuración de Data Management Gateway herramienta tooconfigure Hola.
   >
   >
5. Espere unos minutos o espere hasta que vea Hola después el mensaje de notificación:

    ![Instalación correcta de la puerta de enlace](./media/data-factory-move-data-between-onprem-and-cloud/gateway-install-success.png)
6. Inicie la aplicación **Administrador de configuración de Data Management Gateway** en el equipo. Hola **búsqueda** ventana, escriba **Data Management Gateway** tooaccess este utilidad. También puede encontrar Hola ejecutable **ConfigManager.exe** en la carpeta de hello: **C:\Program Files\Microsoft datos administración Gateway\2.0\Shared**

    ![Administrador de configuración de puertas de enlace](./media/data-factory-move-data-between-onprem-and-cloud/OnPremDMGConfigurationManager.png)
7. Confirme que ve el mensaje `adftutorialgateway is connected toohello cloud service`. Hola Hola inferior muestra la barra de estado **toohello servicio de nube conectado** junto con un **marca de verificación verde**.

    En hello **inicio** pestaña, también puede hacer Hola realizar las siguientes operaciones:

   * **Registrar** una puerta de enlace con una clave de hello portal de Azure con botón de registro de hello.
   * **Detener** Hola servicio de Host de Data Management Gateway ejecutando en el equipo de puerta de enlace.
   * **Programar actualizaciones** toobe instalado en un momento determinado del día de Hola.
   * Ver si se realizó la puerta de enlace de hello **actualizó por última vez**.
   * Especifique la hora a la que se puede instalar una puerta de enlace de toohello de actualización.
8. Cambiar toohello **configuración** certificado de Hola de ficha especificado en hello **certificado** sección es usado tooencrypt o descifrar credenciales para almacén de datos local de Hola que especifique en el portal de Hola. (opcional) Haga clic en **cambio** toouse su propio certificado en su lugar. De forma predeterminada, puerta de enlace de hello utiliza certificado Hola Hola servicio factoría de datos genera automáticamente.

    ![Configuración del certificado de puerta de enlace](./media/data-factory-move-data-between-onprem-and-cloud/gateway-certificate.png)

    También puede hacer Hola siguientes acciones en hello **configuración** ficha:

   * Ver o exportar el certificado de Hola que se usa la puerta de enlace de Hola.
   * Cambiar el punto de conexión HTTPS de hello usa Hola puerta de enlace.    
   * Establecer un toobe del proxy HTTP utilizado por la puerta de enlace de Hola.     
9. (opcional) Cambiar toohello **diagnósticos** ficha, compruebe hello **habilitar el registro detallado** opción si desea que tooenable el registro que puede usar cualquier problema tootroubleshoot con puerta de enlace de hello detallado. Hello información de registro puede encontrarse en **Visor de eventos** en **registros de aplicaciones y servicios** -> **Data Management Gateway** nodo.

    ![Ficha Diagnóstico](./media/data-factory-move-data-between-onprem-and-cloud/diagnostics-tab.png)

    También puede realizar Hola siguientes acciones en hello **diagnósticos** ficha:

   * Use **Probar conexión** origen de datos local de la sección tooan con puerta de enlace de Hola.
   * Haga clic en **ver registros** toosee Hola Data Management Gateway inicie sesión en una ventana del Visor de eventos.
   * Haga clic en **enviar registros** tooupload un archivo zip con registros de los últimos siete días tooMicrosoft toofacilitate solución de problemas de los problemas.
10. En hello **diagnósticos** ficha Hola **Probar conexión** sección, seleccione **SqlServer** para el tipo de saludo de datos de hello, almacenar, escriba Hola nombre del servidor de base de datos de Hola, nombre del Hola de base de datos, especificar el tipo de autenticación, escriba el nombre de usuario y contraseña y haga clic en **prueba** tootest si la puerta de enlace de hello puede conectarse toohello base de datos.
11. Explorador de web toohello de conmutador y en hello **portal de Azure**, haga clic en **Aceptar** en hello **configurar** página y, a continuación, en hello **nueva puerta de enlace de datos** página.
12. Debería ver **adftutorialgateway** en **puertas de enlace de datos** en vista de árbol de Hola Hola izquierda.  Si hace clic en él, debería ver Hola asociados JSON.

## <a name="create-linked-services"></a>Crear servicios vinculados
En este paso, creará dos servicios vinculados: **AzureStorageLinkedService** y **SqlServerLinkedService**. Hola **SqlServerLinkedService** vincula una base de datos de SQL Server local y hello **AzureStorageLinkedService** servicio vinculado vincula una factoría de datos de toohello de almacén de blobs de Azure. Crear una canalización más adelante en este tutorial que copia datos de almacén de blobs de Azure de hello local SQL Server base de datos toohello.

#### <a name="add-a-linked-service-tooan-on-premises-sql-server-database"></a>Agregar una base de datos de SQL Server de servicio vinculado tooan local
1. Hola **Editor de generador de datos**, haga clic en **nuevo almacén de datos** en la barra de herramientas de Hola y seleccione **SQL Server**.

   ![Nuevo servicio vinculado de SQL Server](./media/data-factory-move-data-between-onprem-and-cloud/NewSQLServer.png)
2. Hola **editor JSON** en Hola derecho Hola lo siguiente:

   1. Para hello **gatewayName**, especifique **adftutorialgateway**.    
   2. Hola **connectionString**, Hola lo siguiente:    

      1. Para **servername**, escriba Hola nombre de hello servidor que hospeda la base de datos de SQL Server de Hola.
      2. Para **databasename**, escriba Hola nombre de base de datos de Hola.
      3. Haga clic en **Encrypt** botón de barra de herramientas de Hola. Consulte aplicación de administrador de credenciales de hello.

         ![Aplicación Administrador de credenciales](./media/data-factory-move-data-between-onprem-and-cloud/credentials-manager-application.png)
      4. Hola **establecer credenciales** cuadro de diálogo, especifique el tipo de autenticación, nombre de usuario y contraseña y haga clic en **Aceptar**. Si Hola conexión es correcta, credenciales de hello cifrado se almacenan en hello JSON y cierra el cuadro de diálogo de Hola.
      5. Cerrar la pestaña de explorador vacía de Hola que inicia el cuadro de diálogo de hello si no se cierra automáticamente y regresar pestaña toohello con hello portal de Azure.

         En la máquina de puerta de enlace de hello, estas credenciales son **cifrados** mediante un certificado que Hola factoría de datos posee el servicio. Si desea toouse Hola certificado asociado con hello Data Management Gateway en su lugar, consulte [establecer las credenciales de forma segura](#set-credentials-and-security).    
   3. Haga clic en **implementar** en toodeploy Hola servicio vinculado de SQL Server de la barra de comandos de Hola. Debería ver Hola vinculado servicio en la vista de árbol de Hola.

      ![Servicio de SQL Server vinculado en la vista de árbol de Hola](./media/data-factory-move-data-between-onprem-and-cloud/sql-linked-service-in-tree-view.png)    

#### <a name="add-a-linked-service-for-an-azure-storage-account"></a>Adición de un servicio vinculado para una cuenta de almacenamiento de Azure
1. Hola **Editor de generador de datos**, haga clic en **nuevo almacén de datos** Hola barra de comandos y haga clic en **almacenamiento de Azure**.
2. Escriba Hola nombre de la cuenta de almacenamiento de Azure para hello **nombre de la cuenta**.
3. Escriba la clave de Hola de su cuenta de almacenamiento de Azure para hello **clave de cuenta**.
4. Haga clic en **implementar** toodeploy hello **AzureStorageLinkedService**.

## <a name="create-datasets"></a>Creación de conjuntos de datos
En este paso, creará entrada y salida conjuntos de datos que representan los datos de entrada y salidas para la operación de copia de hello (base de datos de SQL Server en local = > almacenamiento de blobs de Azure). Antes de crear conjuntos de datos, Hola pasos (los pasos detallados a continuación de lista de hello):

* Crear una tabla denominada **emp** en Hola base de datos de SQL Server agrega como una factoría de datos de servicio vinculado toohello e inserte un par de entradas de ejemplo en la tabla de Hola.
* Crear un contenedor de blobs denominado **adftutorial** en hello Azure blob agrega como una factoría de datos de servicio vinculado toohello de cuenta de almacenamiento.

### <a name="prepare-on-premises-sql-server-for-hello-tutorial"></a>Preparar SQL Server en local para el tutorial de Hola
1. En base de datos de hello especificada para hello SQL Server local servicio vinculado (**SqlServerLinkedService**), usar hello después Hola de toocreate de secuencia de comandos SQL **emp** tabla de base de datos de Hola.

    ```SQL   
    CREATE TABLE dbo.emp
    (
        ID int IDENTITY(1,1) NOT NULL,
        FirstName varchar(50),
        LastName varchar(50),
        CONSTRAINT PK_emp PRIMARY KEY (ID)
    )
    GO
    ```
2. Insertar algunos ejemplos en la tabla de hello:

    ```SQL
    INSERT INTO emp VALUES ('John', 'Doe')
    INSERT INTO emp VALUES ('Jane', 'Doe')
    ```

### <a name="create-input-dataset"></a>Creación de un conjunto de datos de entrada

1. Hola **Editor de generador de datos**, haga clic en **... Más**, haga clic en **nuevo conjunto de datos** Hola barra de comandos y haga clic en **tabla de SQL Server**.
2. Reemplace Hola JSON en el panel derecho de hello con hello siguiente texto:

    ```JSON   
    {        
        "name": "EmpOnPremSQLTable",
        "properties": {
            "type": "SqlServerTable",
            "linkedServiceName": "SqlServerLinkedService",
            "typeProperties": {
                "tableName": "emp"
            },
            "external": true,
            "availability": {
                "frequency": "Hour",
                "interval": 1
            },
            "policy": {
                "externalData": {
                    "retryInterval": "00:01:00",
                    "retryTimeout": "00:10:00",
                    "maximumRetry": 3
                }
            }
        }
    }     
    ```     
   Tenga en cuenta Hola siguientes puntos:

   * **tipo de** se establece demasiado**SqlServerTable**.
   * **tableName** se establece demasiado**emp**.
   * **linkedServiceName** se establece demasiado**SqlServerLinkedService** (este servicio vinculado había creado anteriormente en este tutorial.).
   * Para un conjunto de datos entrada que no se hayan generado por otra canalización de factoría de datos de Azure, debe establecer **externo** demasiado**true**. Indica los datos de entrada de hello están toohello externo producido servicio Data Factory de Azure. Opcionalmente, puede especificar las directivas de datos externos utilizando hello **externalData** elemento Hola **directiva** sección.    

   Para más información acerca de las propiedades de JSON, consulte [Movimiento de datos hacia y desde SQL Server](data-factory-sqlserver-connector.md).
3. Haga clic en **implementar** en el conjunto de datos de toodeploy Hola la barra de comandos de Hola.  

### <a name="create-output-dataset"></a>Creación del conjunto de datos de salida

1. Hola **Editor de generador de datos**, haga clic en **nuevo conjunto de datos** Hola barra de comandos y haga clic en **almacenamiento de blobs de Azure**.
2. Reemplace Hola JSON en el panel derecho de hello con hello siguiente texto:

    ```JSON   
    {
        "name": "OutputBlobTable",
        "properties": {
            "type": "AzureBlob",
            "linkedServiceName": "AzureStorageLinkedService",
            "typeProperties": {
                "folderPath": "adftutorial/outfromonpremdf",
                "format": {
                    "type": "TextFormat",
                    "columnDelimiter": ","
                }
            },
            "availability": {
                "frequency": "Hour",
                "interval": 1
            }
        }
     }
    ```   
   Tenga en cuenta Hola siguientes puntos:

   * **tipo de** se establece demasiado**AzureBlob**.
   * **linkedServiceName** se establece demasiado**AzureStorageLinkedService** (había creado este servicio vinculado en el paso 2).
   * **folderPath** se establece demasiado**adftutorial/outfromonpremdf** donde outfromonpremdf es la carpeta hello en el contenedor de adftutorial Hola. Crear hello **adftutorial** contenedor si aún no existe.
   * Hola **disponibilidad** se establece demasiado**cada hora** (**frecuencia** establecido demasiado**hora** y **intervalo** establecido demasiado **1**).  Hola servicio factoría de datos genera un segmento de datos de salida cada hora en hello **emp** tabla Hola base de datos de SQL Azure.

   Si no se especifica un **fileName** para un **tabla de salida**, archivos de hello generado en hello **folderPath** se denominan en hello siguiendo el formato: datos.<Guid>. txt (por ejemplo:: Data.0a405f8a 93ff 4c6f b3be f69616f1df7a.txt.).

   tooset **folderPath** y **fileName** dinámicamente en función de hello **SliceStart** tiempo, use la propiedad de partitionedBy Hola. En el siguiente ejemplo de Hola folderPath usa año, mes y día de hello SliceStart (hora de inicio del segmento de hello procesando) y nombre de archivo usa hora de hello SliceStart. Por ejemplo, si se está produciendo un segmento para 2014-10-20T08:00:00, Hola nombreDeCarpeta se establece toowikidatagateway/wikisampledataout/2014/10/20 y fileName hello too08.csv.

    ```JSON
    "folderPath": "wikidatagateway/wikisampledataout/{Year}/{Month}/{Day}",
    "fileName": "{Hour}.csv",
    "partitionedBy":
    [

        { "name": "Year", "value": { "type": "DateTime", "date": "SliceStart", "format": "yyyy" } },
        { "name": "Month", "value": { "type": "DateTime", "date": "SliceStart", "format": "MM" } },
        { "name": "Day", "value": { "type": "DateTime", "date": "SliceStart", "format": "dd" } },
        { "name": "Hour", "value": { "type": "DateTime", "date": "SliceStart", "format": "hh" } }
    ],
    ```

    Para más información acerca de las propiedades de JSON, consulte [Movimiento de datos hacia y desde Azure Blob Storage](data-factory-azure-blob-connector.md).
3. Haga clic en **implementar** en el conjunto de datos de toodeploy Hola la barra de comandos de Hola. Confirme que ve los dos conjuntos de datos de hello en la vista de árbol de Hola.  

## <a name="create-pipeline"></a>Creación de una canalización
En este paso, va a crear una **canalización** con una **actividad de copia** que usa **EmpOnPremSQLTable** como entrada y **OutputBlobTable** como salida.

1. En Data Factory Editor, haga clic en **... Más** y, luego, en **Nueva canalización**.
2. Reemplace Hola JSON en el panel derecho de hello con hello siguiente texto:    

    ```JSON   
     {
         "name": "ADFTutorialPipelineOnPrem",
         "properties": {
         "description": "This pipeline has one Copy activity that copies data from an on-prem SQL tooAzure blob",
         "activities": [
           {
             "name": "CopyFromSQLtoBlob",
             "description": "Copy data from on-prem SQL server tooblob",
             "type": "Copy",
             "inputs": [
               {
                 "name": "EmpOnPremSQLTable"
               }
             ],
             "outputs": [
               {
                 "name": "OutputBlobTable"
               }
             ],
             "typeProperties": {
               "source": {
                 "type": "SqlSource",
                 "sqlReaderQuery": "select * from emp"
               },
               "sink": {
                 "type": "BlobSink"
               }
             },
             "Policy": {
               "concurrency": 1,
               "executionPriorityOrder": "NewestFirst",
               "style": "StartOfInterval",
               "retry": 0,
               "timeout": "01:00:00"
             }
           }
         ],
         "start": "2016-07-05T00:00:00Z",
         "end": "2016-07-06T00:00:00Z",
         "isPaused": false
       }
     }
    ```   
   > [!IMPORTANT]
   > Reemplazar el valor de Hola de hello **iniciar** propiedad con hello día actual y **final** valor con hello día siguiente.
   >
   >

   Tenga en cuenta Hola siguientes puntos:

   * En la sección de actividades de hello, hay sólo una actividad cuyo **tipo** se establece demasiado**copia**.
   * **Entrada** de actividad hello se establece demasiado**EmpOnPremSQLTable** y **salida** de actividad hello se establece demasiado**OutputBlobTable**.
   * Hola **typeProperties** sección, **SqlSource** se especifica como hello **tipo de origen de** y ** BlobSink ** se especifica como hello **receptor tipo**.
   * Consulta SQL `select * from emp` se especifica para hello **sqlReaderQuery** propiedad de **SqlSource**.

   Las fechas y horas de inicio y de finalización deben estar en [formato ISO](http://en.wikipedia.org/wiki/ISO_8601). Por ejemplo: 2014-10-14T16:32:41Z. Hola **final** tiempo es opcional, pero se usa en este tutorial.

   Si no especifica el valor de hello **final** propiedad, se calcula como "**inicio + 48 horas**". canalización de hello toorun indefinidamente, especifique **9/9/9999** como valor de Hola de hello **final** propiedad.

   Se está definiendo Hola duración en qué Hola se procesan los segmentos de datos en función de hello **disponibilidad** propiedades que se han definido para cada conjunto de datos de Data Factory de Azure.

   En el ejemplo de Hola, hay 24 segmentos de datos tal y como se produce cada segmento de datos cada hora.        
3. Haga clic en **implementar** en el conjunto de datos de toodeploy Hola la barra de comandos de hello (tabla es un conjunto de datos rectangular). Confirmar esa canalización Hola se muestra en la vista de árbol de hello en **canalizaciones** nodo.  
4. Ahora, haga clic en **X** dos veces tooclose Hola página tooget back-toohello **factoría de datos** página de hello **ADFTutorialOnPremDF**.

**¡Enhorabuena!** Ha creado correctamente una factoría de datos de Azure, servicios vinculados, conjuntos de datos y una canalización y canalización Hola programada.

#### <a name="view-hello-data-factory-in-a-diagram-view"></a>Factoría de datos de vista hello en una vista de diagrama
1. Hola **portal de Azure**, haga clic en **diagrama** de mosaico en la página de inicio de Hola de hello **ADFTutorialOnPremDF** factoría de datos. :

    ![Vínculo de diagrama](./media/data-factory-move-data-between-onprem-and-cloud/OnPremDiagramLink.png)
2. Debería ver Hola diagrama similar toohello después de imagen:

    ![Vista de diagrama](./media/data-factory-move-data-between-onprem-and-cloud/OnPremDiagramView.png)

    Puede acercar, alejar, zoom too100%, toofit de zoom, automáticamente las canalizaciones de posición y conjuntos de datos y mostrar la información de linaje (resalta los elementos que preceden y siguen en la cadena de los elementos seleccionados).  Hacer doble clic en un toosee las propiedades de objeto (conjunto de datos de entrada/salida o canalización) para ella.

## <a name="monitor-pipeline"></a>Supervisión de la canalización
En este paso, utilizará hello toomonitor portal Azure que está sucediendo en una factoría de datos de Azure. También puede utilizar las canalizaciones y conjuntos de datos de toomonitor de cmdlets de PowerShell. Para obtener más información sobre la supervisión, consulte [Supervisión y administración de canalizaciones](data-factory-monitor-manage-pipelines.md).

1. En el diagrama de hello, haga doble clic en **EmpOnPremSQLTable**.  

    ![Segmentos EmpOnPremSQLTable](./media/data-factory-move-data-between-onprem-and-cloud/OnPremSQLTableSlicesBlade.png)
2. Tenga en cuenta que todos los datos de hello divide los están en **listo** estado porque Hola canalización tiempo (hora de tooend de tiempo de inicio) en hello anterior. También es porque ha insertado datos hello en la base de datos de SQL Server de Hola y encuentra todo el tiempo Hola. Confirme que no hay ningún segmento se mostrarán en hello **sectores problema** sección final Hola. tooview todos los sectores de hello, haga clic en ejecutar **vea más** final Hola de lista de Hola de segmentos.
3. Ahora, en hello **conjuntos de datos** página, haga clic en **OutputBlobTable**.

    ![Segmentos OputputBlobTable](./media/data-factory-move-data-between-onprem-and-cloud/OutputBlobTableSlicesBlade.png)
4. Haga clic en cualquier segmento de datos de lista de Hola y debería ver Hola **el segmento de datos** página. Vea la actividad se ejecuta durante el intervalo de Hola. Normalmente solo se ve una ejecución de actividad.  

    ![Hoja Segmento de datos](./media/data-factory-move-data-between-onprem-and-cloud/DataSlice.png)

    Si el segmento de hello no está en hello **listo** estado, puede ver segmentos ascendentes de Hola que no están listos y están bloqueando el intervalo actual de Hola de ejecutarse en hello **segmentos ascendentes que no están listos** lista.
5. Haga clic en hello **actividad ejecutar** de lista de hello en hello inferior toosee **detalles de ejecución de la actividad**.

   ![Página Detalles de ejecución de actividad](./media/data-factory-move-data-between-onprem-and-cloud/ActivityRunDetailsBlade.png)

   Verá información, como el rendimiento, la duración y la puerta de enlace de hello usan datos de hello tootransfer.
6. Haga clic en **X** tooclose todos Hola páginas hasta que
7. regresar toohello portada hello **ADFTutorialOnPremDF**.
8. (Opcional) Haga clic en **Canalizaciones**, elija **ADFTutorialOnPremDF** y obtenga detalles de los conjuntos de datos de entrada (**Consumido**) o los conjuntos de datos de salida (**Producido**).
9. Usar herramientas como [Explorador de almacenamiento de Microsoft](http://storageexplorer.com/) tooverify que se crea un archivo de blob para cada hora.

   ![Explorador de Azure Storage](./media/data-factory-move-data-between-onprem-and-cloud/OnPremAzureStorageExplorer.png)

## <a name="next-steps"></a>Pasos siguientes
* Vea [Data Management Gateway](data-factory-data-management-gateway.md) artículo para todos los detalles acerca de hello Data Management Gateway de Hola.
* Vea [copiar los datos de Blob de Azure tooAzure SQL](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) toolearn acerca de cómo tooa almacén de datos de receptor de almacén de datos de toomove de actividad de copia de toouse desde un origen de datos.
