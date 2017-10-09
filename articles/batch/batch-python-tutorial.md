---
title: aaaTutorial - Hola de uso por lotes de Azure SDK para Python | Documentos de Microsoft
description: "Obtenga información acerca de los conceptos básicos de Azure Batch hello y generar una solución simple con Python."
services: batch
documentationcenter: python
author: tamram
manager: timlt
editor: 
ms.assetid: 42cae157-d43d-47f8-88f5-486ccfd334f4
ms.service: batch
ms.devlang: python
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: big-compute
ms.date: 02/27/2017
ms.author: tamram
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: c4d5152aeef31848c50a7f2aae5e7a7e0e1e9535
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-hello-batch-sdk-for-python"></a>Empezar a trabajar con hello lote SDK para Python

> [!div class="op_single_selector"]
> * [.NET](batch-dotnet-get-started.md)
> * [Python](batch-python-tutorial.md)
> * [Node.js](batch-nodejs-get-started.md)
>
>

Obtenga información acerca de los conceptos básicos de Hola de [Azure Batch] [ azure_batch] hello y [lote Python] [ py_azure_sdk] cliente tal y como se describe una aplicación de lote pequeña escrita en Python. Veremos cómo dos muestras las secuencias de comandos use Hola lote servicio tooprocess una carga de trabajo paralelo en máquinas virtuales de Linux en la nube de Hola y cómo interactúan con [el almacenamiento de Azure](../storage/common/storage-introduction.md) para almacenamiento provisional de archivo y la recuperación. Podrá Obtenga información acerca de un flujo de trabajo de aplicación común de lote y obtener una descripción de base de componentes principales Hola de lote como trabajos, tareas, grupos y nodos de ejecución.

![Flujo de trabajo de soluciones de Batch (básico)][11]<br/>

## <a name="prerequisites"></a>Requisitos previos
En este artículo se considera que tiene conocimientos prácticos de Python y está familiarizado con Linux. También se da por supuesto que es capaz de toosatisfy Hola creación requisitos de las cuentas que se especifican a continuación para Azure y Hola por lotes y los servicios de almacenamiento.

### <a name="accounts"></a>Cuentas
* **Cuenta de Azure**: si aún no tiene ninguna suscripción a Azure, [cree una cuenta gratuita de Azure][azure_free_account].
* **Cuenta de Batch**: una vez que tenga una suscripción a Azure, [cree una cuenta de Azure Batch](batch-account-create-portal.md).
* **Cuenta de almacenamiento**: consulte la sección [Crear una cuenta de almacenamiento](../storage/common/storage-create-storage-account.md#create-a-storage-account) del artículo [Acerca de las cuentas de almacenamiento de Azure](../storage/common/storage-create-storage-account.md).

### <a name="code-sample"></a>Código de ejemplo
tutorial de Python de Hello [código de ejemplo] [ github_article_samples] es uno de los muchos ejemplos de código de proceso por lotes que se encuentran en Hola de hello [ejemplos de lote de azure] [ github_samples] repositorio en GitHub. Puede descargar todos los ejemplos de hello haciendo clic en **clon o una descarga > Download ZIP** en página de inicio del repositorio de hello, o haciendo clic en hello [azure-lote-ejemplos-master.zip] [ github_samples_zip]vínculo de descarga directa. Una vez que haya extraído contenido Hola del archivo ZIP de hello, secuencias de comandos de hello dos para este tutorial se encuentran en hello `article_samples` directorio:

`/azure-batch-samples/Python/Batch/article_samples/python_tutorial_client.py`<br/>
`/azure-batch-samples/Python/Batch/article_samples/python_tutorial_task.py`

### <a name="python-environment"></a>Entorno de Python
Hola toorun *python_tutorial_client.py* secuencia de comandos de ejemplo en la estación de trabajo local, necesita un **intérprete Python** compatible con la versión **2.7** o **3.3 +**. script de Hola se ha probado en Linux y Windows.

### <a name="cryptography-dependencies"></a>Dependencias de cryptography
Debe instalar las dependencias de Hola de hello [criptografía] [ crypto] library, requerida por hello `azure-batch` y `azure-storage` paquetes de Python. Realice uno de hello siguiendo las operaciones adecuadas para su plataforma o consulte toohello [instalación de criptografía] [ crypto_install] detalles para obtener más información:

* Ubuntu

    `apt-get update && apt-get install -y build-essential libssl-dev libffi-dev libpython-dev python-dev`
* CentOS

    `yum update && yum install -y gcc openssl-devel libffi-devel python-devel`
* SLES/OpenSUSE

    `zypper ref && zypper -n in libopenssl-dev libffi48-devel python-devel`
* Windows

    `pip install cryptography`

> [!NOTE]
> Si la instalación de Python 3.3 + en Linux, utilizar los equivalentes de python3 de Hola para las dependencias de Python de Hola. Por ejemplo, en Ubuntu: `apt-get update && apt-get install -y build-essential libssl-dev libffi-dev libpython3-dev python3-dev`
>
>

### <a name="azure-packages"></a>Paquetes de Azure
A continuación, instale hello **Azure Batch** y **el almacenamiento de Azure** paquetes de Python. Puede instalar ambos paquetes mediante **pip** hello y *requirements.txt* encontrar aquí:

`/azure-batch-samples/Python/Batch/requirements.txt`

Problema siguiente **pip** paquetes de lote y el almacenamiento de hello tooinstall de comandos:

`pip install -r requirements.txt`

O bien, puede instalar hello [lote de azure] [ pypi_batch] y [almacenamiento de azure] [ pypi_storage] Python paquetes manualmente:

`pip install azure-batch`<br/>
`pip install azure-storage`

> [!TIP]
> Si usas una cuenta sin privilegios, puede que tenga tooprefix los comandos con `sudo`. Por ejemplo: `sudo pip install -r requirements.txt`. Para más información acerca de cómo instalar los paquetes de Python, consulte [Installing Packages][pypi_install] (Instalación de paquetes) en python.org.
>
>

## <a name="batch-python-tutorial-code-sample"></a>Ejemplo de código del tutorial de Python de Lote
ejemplo de código del tutorial de Python de lote de Hello consta de dos scripts de Python y algunos archivos de datos.

* **python_tutorial_client.py**: interactúa con tooexecute de servicios de almacenamiento y por lotes Hola una carga de trabajo paralelo en nodos de proceso (máquinas virtuales). Hola *python_tutorial_client.py* script se ejecuta en la estación de trabajo local.
* **python_tutorial_task.py**: script de Hola que se ejecuta en nodos de cálculo en trabajo real de Azure tooperform Hola. En el ejemplo de Hola, *python_tutorial_task.py* analiza Hola texto en un archivo descargado desde el almacenamiento de Azure (archivo de entrada de hello). A continuación, genera un archivo de texto (archivo de salida de Hola) que contiene una lista de palabras de tres primeras Hola que aparecen en el archivo de entrada de Hola. Después de crear el archivo de salida de hello, *python_tutorial_task.py* cargas Hola tooAzure almacenamiento de archivo. Estarán disponibles para el script de cliente de descarga toohello ejecutando en la estación de trabajo. Hola *python_tutorial_task.py* script se ejecuta en paralelo en varios nodos de cálculo en hello servicio por lotes.
* **./Data/taskdata\*.txt**: estos archivos de tres texto proporcionan la entrada de Hola para nodos de ejecución de tareas de Hola que se ejecutan en Hola.

Hola siguiente diagrama muestra operaciones principales de hello realizadas por los scripts de cliente y la tarea de Hola. Este flujo de trabajo básico es típico de muchas soluciones de proceso que se crean con Batch. Mientras no muestran todas las características disponibles en hello servicio por lotes, casi cada escenario de lote incluye algunas partes de este flujo de trabajo.

![Flujo de trabajo de ejemplo de Batch][8]<br/>

[**Paso 1.**](#step-1-create-storage-containers) Crear **contenedores** en Azure Blob Storage.<br/>
[**Paso 2.**](#step-2-upload-task-script-and-data-files) Cargar toocontainers de archivos de script y entrada de tarea.<br/>
[**Paso 3.**](#step-3-create-batch-pool) Cree un **grupo** de Batch.<br/>
  &nbsp;&nbsp;&nbsp;&nbsp;**3a.** Hola grupo **StartTask** descargas Hola tarea script (python_tutorial_task.py) toonodes cuando se unen a grupo Hola.<br/>
[**Paso 4.**](#step-4-create-batch-job) Cree un **trabajo** de Batch.<br/>
[**Paso 5.**](#step-5-add-tasks-to-job) Agregar **tareas** toohello trabajo.<br/>
  &nbsp;&nbsp;&nbsp;&nbsp;**5a.** las tareas de Hello son tooexecute programada en nodos.<br/>
    &nbsp;&nbsp;&nbsp;&nbsp;**5b.** Cada tarea descarga sus datos de entrada de Azure Storage y comienza la ejecución.<br/>
[**Paso 6.**](#step-6-monitor-tasks) Supervisar las tareas.<br/>
  &nbsp;&nbsp;&nbsp;&nbsp;**6a.** Tal y como se completan tareas, cargan su tooAzure de datos de salida almacenamiento.<br/>
[**Paso 7.**](#step-7-download-task-output) Descargar el resultado de la tarea de Almacenamiento

Como se ha indicado, no todas las soluciones de Lote realizan estos mismos pasos y se puede haber muchos otros; sin embargo, sin embargo, este ejemplo muestra los procesos comunes que se encuentran en una solución de Lote.

## <a name="prepare-client-script"></a>Preparación del script de cliente
Antes de ejecutar el ejemplo hello, agregue sus credenciales de cuenta de lote y el almacenamiento demasiado*python_tutorial_client.py*. Si aún no lo ha hecho, abra el archivo de hello en los favoritos Hola de editor y actualización siguiendo las líneas con sus credenciales.

```python
# Update hello Batch and Storage account credential strings below with hello values
# unique tooyour accounts. These are used when constructing connection strings
# for hello Batch and Storage client objects.

# Batch account credentials
BATCH_ACCOUNT_NAME = ""
BATCH_ACCOUNT_KEY = ""
BATCH_ACCOUNT_URL = ""

# Storage account credentials
STORAGE_ACCOUNT_NAME = ""
STORAGE_ACCOUNT_KEY = ""
```

Puede encontrar sus credenciales de cuenta de lote y el almacenamiento en la hoja de la cuenta de hello de cada servicio en hello [portal de Azure][azure_portal]:

![Procesar por lotes las credenciales en el portal de hello][9]
![credenciales de almacenamiento en el portal de Hola][10]<br/>

En las secciones siguientes de hello, analizamos pasos Hola utilizado por hello scripts tooprocess una carga de trabajo en hello servicio por lotes. Le recomendamos que toorefer con regularidad toohello scripts en el editor mientras el equipo funcionan su camino a través del resto de Hola de artículo Hola.

Navegue toohello después de la línea en **python_tutorial_client.py** toostart con el paso 1:

```python
if __name__ == '__main__':
```

## <a name="step-1-create-storage-containers"></a>Paso 1: Crear contenedores de Storage
![Crear contenedores en Azure Storage][1]
<br/>

Batch incluye compatibilidad integrada para interactuar con Azure Storage. Contenedores en su cuenta de almacenamiento proporcionará los archivos de hello necesarios para las tareas de Hola que se ejecutan en su cuenta de lote. los contenedores de Hello también proporcionan un colocar toostore Hola salida los datos que producen las tareas de Hola. lo primero que Hola Hola *python_tutorial_client.py* script hace es crear tres contenedores en [almacenamiento de blobs de Azure](../storage/common/storage-introduction.md#blob-storage):

* **aplicación**: este contenedor almacenará script de Python Hola ejecutar las tareas de hello, *python_tutorial_task.py*.
* **entrada**: tareas descargará tooprocess de archivos de datos de Hola de hello *entrada* contenedor.
* **salida**: cuando completen de tareas de procesamiento del archivo de entrada, cargará Hola resultados toohello *salida* contenedor.

En orden toointeract con un almacenamiento de información de la cuenta y crear contenedores, usamos hello [almacenamiento de azure] [ pypi_storage] paquete toocreate una [BlockBlobService] [ py_blockblobservice] objeto: Hola ""blob cliente. A continuación, crearemos tres contenedores en la cuenta de almacenamiento de hello con cliente de blob de Hola.

```python
import azure.storage.blob as azureblob

# Create hello blob client, for use in obtaining references to
# blob storage containers and uploading files toocontainers.
blob_client = azureblob.BlockBlobService(
    account_name=STORAGE_ACCOUNT_NAME,
    account_key=STORAGE_ACCOUNT_KEY)

# Use hello blob client toocreate hello containers in Azure Storage if they
# don't yet exist.
APP_CONTAINER_NAME = 'application'
INPUT_CONTAINER_NAME = 'input'
OUTPUT_CONTAINER_NAME = 'output'
blob_client.create_container(APP_CONTAINER_NAME, fail_on_exist=False)
blob_client.create_container(INPUT_CONTAINER_NAME, fail_on_exist=False)
blob_client.create_container(OUTPUT_CONTAINER_NAME, fail_on_exist=False)
```

Una vez que se han creado los contenedores de hello, aplicación hello ahora puede cargar archivos de Hola que se usará en las tareas de Hola.

> [!TIP]
> [¿Cómo toouse almacenamiento de blobs de Azure de Python](../storage/blobs/storage-python-how-to-use-blob-storage.md) proporciona una buena información general sobre cómo trabajar con contenedores de almacenamiento de Azure y los blobs. Debe ser cerca de la parte superior de saludo de la lista de lectura como comienza a trabajar con el lote.
>
>

## <a name="step-2-upload-task-script-and-data-files"></a>Paso 2: Cargar un script de tarea y archivos de entrada
![Toocontainers de archivos de la tarea de carga de aplicación y entrada (datos)][2]
<br/>

En el archivo hello cargar el operación, *python_tutorial_client.py* define en primer lugar las colecciones de **aplicación** y **entrada** las rutas de acceso de archivo tal como aparecen en la máquina local Hola. A continuación, se cargan estos contenedores de toohello de archivos que creó en el paso anterior de Hola.

```python
# Paths toohello task script. This script will be executed by hello tasks that
# run on hello compute nodes.
application_file_paths = [os.path.realpath('python_tutorial_task.py')]

# hello collection of data files that are toobe processed by hello tasks.
input_file_paths = [os.path.realpath('./data/taskdata1.txt'),
                    os.path.realpath('./data/taskdata2.txt'),
                    os.path.realpath('./data/taskdata3.txt')]

# Upload hello application script tooAzure Storage. This is hello script that
# will process hello data files, and is executed by each of hello tasks on the
# compute nodes.
application_files = [
    upload_file_to_container(blob_client, APP_CONTAINER_NAME, file_path)
    for file_path in application_file_paths]

# Upload hello data files. This is hello data that will be processed by each of
# hello tasks executed on hello compute nodes in hello pool.
input_files = [
    upload_file_to_container(blob_client, INPUT_CONTAINER_NAME, file_path)
    for file_path in input_file_paths]
```

Mediante la comprensión de la lista, Hola `upload_file_to_container` función se llama para cada archivo de colecciones de Hola y dos [ResourceFile] [ py_resource_file] se rellenan las colecciones. Hola `upload_file_to_container` función aparece a continuación:

```python
def upload_file_to_container(block_blob_client, container_name, path):
    """
    Uploads a local file tooan Azure Blob storage container.

    :param block_blob_client: A blob service client.
    :type block_blob_client: `azure.storage.blob.BlockBlobService`
    :param str container_name: hello name of hello Azure Blob storage container.
    :param str file_path: hello local path toohello file.
    :rtype: `azure.batch.models.ResourceFile`
    :return: A ResourceFile initialized with a SAS URL appropriate for Batch
    tasks.
    """

    import datetime
    import azure.storage.blob as azureblob
    import azure.batch.models as batchmodels

    blob_name = os.path.basename(path)

    print('Uploading file {} toocontainer [{}]...'.format(path,
                                                          container_name))

    block_blob_client.create_blob_from_path(container_name,
                                            blob_name,
                                            file_path)

    sas_token = block_blob_client.generate_blob_shared_access_signature(
        container_name,
        blob_name,
        permission=azureblob.BlobPermissions.READ,
        expiry=datetime.datetime.utcnow() + datetime.timedelta(hours=2))

    sas_url = block_blob_client.make_blob_url(container_name,
                                              blob_name,
                                              sas_token=sas_token)

    return batchmodels.ResourceFile(file_path=blob_name,
                                    blob_source=sas_url)
```

### <a name="resourcefiles"></a>ResourceFiles
A [ResourceFile] [ py_resource_file] proporciona el nodo de ejecución de tareas en el lote con el archivo de tooa de dirección URL de hello en el almacenamiento de Azure que está tooa descargado antes de que se ejecuta dicha tarea. Hola [ResourceFile][py_resource_file]. **blob_source** propiedad especifica Hola de dirección URL completa del archivo hello tal como existe en el almacenamiento de Azure. dirección URL de Hello también puede incluir una firma de acceso compartido (SAS) que proporciona un acceso seguro toohello archivo. La mayoría de los tipos de tareas de Lote contienen una propiedad *ResourceFiles* , que incluye:

* [CloudTask][py_task]
* [StartTask][py_starttask]
* [JobPreparationTask][py_jobpreptask]
* [JobReleaseTask][py_jobreltask]

Este ejemplo no utiliza Hola JobPreparationTask o tipos de tareas de JobReleaseTask, pero puede obtener más información acerca de esto en [nodos de ejecución de las tareas de preparación y finalización del trabajo de ejecución en Azure Batch](batch-job-prep-release.md).

### <a name="shared-access-signature-sas"></a>Firma de acceso compartido (SAS)
Firmas de acceso compartido son cadenas que proporcionan un acceso seguro toocontainers y blobs en almacenamiento de Azure. Hola *python_tutorial_client.py* secuencia de comandos utiliza ambos blob y contenedor de firmas de acceso compartido y muestra cómo tooobtain estos compartidos tener acceso a las cadenas de firmas de hello servicio de almacenamiento.

* **Firmas de acceso compartido de BLOB**: usos de StartTask del grupo de Hola firmas de acceso compartido cuando descarga archivos de datos de secuencias de comandos y de entrada para la tarea de Hola desde el almacenamiento de objetos binarios (vea [paso 3](#step-3-create-batch-pool) a continuación). Hola `upload_file_to_container` funcionando en *python_tutorial_client.py* contiene código de hello que obtiene la firma de acceso compartido de cada blob. Lo hace mediante una llamada a [BlockBlobService.make_blob_url] [ py_make_blob_url] en el módulo de almacenamiento de Hola.
* **Firma de acceso compartido del contenedor**: a medida que cada tarea finaliza su trabajo en el nodo de proceso de hello, que se carga su toohello del archivo de salida *salida* contenedor en el almacenamiento de Azure. toodo por lo tanto, *python_tutorial_task.py* utilizan una firma de acceso compartido de contenedor que proporciona acceso de escritura toohello contenedor. Hola `get_container_sas_token` funcionando en *python_tutorial_client.py* Obtiene la firma de acceso compartido del contenedor de hello, que, a continuación, se pasa como una tarea de toohello de argumento de línea de comandos. Paso 5 de #, [trabajo de agregar tareas tooa](#step-5-add-tasks-to-job), se describe el uso de Hola de hello contenedor SAS.

> [!TIP]
> Desprotección serie de dos partes de hello en firmas de acceso compartido, [parte 1: modelo de descripción Hola SAS](../storage/common/storage-dotnet-shared-access-signature-part-1.md) y [parte 2: crear y utilizar una SAS con hello servicio Blob](../storage/blobs/storage-dotnet-shared-access-signature-part-2.md), toolearn más acerca de cómo proporcionar un acceso seguro toodata en su cuenta de almacenamiento.
>
>

## <a name="step-3-create-batch-pool"></a>Paso 3: Crear el grupo de Batch
![Crear un grupo de Batch][3]
<br/>

Un **grupo** de Batch es una colección de nodos de proceso (máquinas virtuales) en los que Batch ejecuta tareas de un trabajo.

Una vez que se carga Hola tarea script y datos de archivos toohello cuenta de almacenamiento, *python_tutorial_client.py* inicia su interacción con el servicio de lote de hello mediante el módulo de Python de lote de Hola. toodo por lo tanto, un [BatchServiceClient] [ py_batchserviceclient] se crea:

```python
# Create a Batch service client. We'll now be interacting with hello Batch
# service in addition tooStorage.
credentials = batchauth.SharedKeyCredentials(BATCH_ACCOUNT_NAME,
                                             BATCH_ACCOUNT_KEY)

batch_client = batch.BatchServiceClient(
    credentials,
    base_url=BATCH_ACCOUNT_URL)
```

A continuación, se crea un grupo de nodos de proceso en la cuenta de lote con una llamada de hello demasiado`create_pool`.

```python
def create_pool(batch_service_client, pool_id,
                resource_files, publisher, offer, sku):
    """
    Creates a pool of compute nodes with hello specified OS settings.

    :param batch_service_client: A Batch service client.
    :type batch_service_client: `azure.batch.BatchServiceClient`
    :param str pool_id: An ID for hello new pool.
    :param list resource_files: A collection of resource files for hello pool's
    start task.
    :param str publisher: Marketplace image publisher
    :param str offer: Marketplace image offer
    :param str sku: Marketplace image sku
    """
    print('Creating pool [{}]...'.format(pool_id))

    # Create a new pool of Linux compute nodes using an Azure Virtual Machines
    # Marketplace image. For more information about creating pools of Linux
    # nodes, see:
    # https://azure.microsoft.com/documentation/articles/batch-linux-nodes/

    # Specify hello commands for hello pool's start task. hello start task is run
    # on each node as it joins hello pool, and when it's rebooted or re-imaged.
    # We use hello start task tooprep hello node for running our task script.
    task_commands = [
        # Copy hello python_tutorial_task.py script toohello "shared" directory
        # that all tasks that run on hello node have access to.
        'cp -r $AZ_BATCH_TASK_WORKING_DIR/* $AZ_BATCH_NODE_SHARED_DIR',
        # Install pip and hello dependencies for cryptography
        'apt-get update',
        'apt-get -y install python-pip',
        'apt-get -y install build-essential libssl-dev libffi-dev python-dev',
        # Install hello azure-storage module so that hello task script can access
        # Azure Blob storage
        'pip install azure-storage']

    # Get hello node agent SKU and image reference for hello virtual machine
    # configuration.
    # For more information about hello virtual machine configuration, see:
    # https://azure.microsoft.com/documentation/articles/batch-linux-nodes/
    sku_to_use, image_ref_to_use = \
        common.helpers.select_latest_verified_vm_image_with_node_agent_sku(
            batch_service_client, publisher, offer, sku)

    new_pool = batch.models.PoolAddParameter(
        id=pool_id,
        virtual_machine_configuration=batchmodels.VirtualMachineConfiguration(
            image_reference=image_ref_to_use,
            node_agent_sku_id=sku_to_use),
        vm_size=_POOL_VM_SIZE,
        target_dedicated=_POOL_NODE_COUNT,
        start_task=batch.models.StartTask(
            command_line=
            common.helpers.wrap_commands_in_shell('linux', task_commands),
            run_elevated=True,
            wait_for_success=True,
            resource_files=resource_files),
        )

    try:
        batch_service_client.pool.add(new_pool)
    except batchmodels.batch_error.BatchErrorException as err:
        print_batch_exception(err)
        raise
```

Cuando se crea un grupo, defina un [PoolAddParameter] [ py_pooladdparam] que especifica varias propiedades para el grupo de hello:

* **Id. de** del grupo de hello (*identificador* : es necesario)<p/>Lo mismo que sucede con la mayoría de las entidades en Lote, el nuevo grupo debe tener un identificador único dentro de la cuenta de Lote. El código hace referencia a un grupo de toothis con su identificador, y sirve para identificar a grupo de hello en hello Azure [portal][azure_portal].
* **Número de nodos de proceso** (*target_dedicated*: necesario)<p/>Esta propiedad especifica el número de máquinas virtuales deben implementarse en el grupo de Hola. Es importante toonote que todas las cuentas de lote tienen el valor predeterminado es **cuota** que límites Hola número de **núcleos** (y por lo tanto, los nodos de ejecución) en una cuenta de lote. Puede encontrar las cuotas predeterminadas de hello e instrucciones sobre cómo demasiado[aumentar una cuota](batch-quota-limit.md#increase-a-quota) (por ejemplo, el número máximo de Hola de núcleos de su cuenta de lote) en [las cuotas y límites de hello servicio Azure Batch](batch-quota-limit.md). Si se pregunta "¿Por qué mi grupo no llega a más de X nodos?", Esta cuota básica puede ser la causa de Hola.
* **Sistema operativo** para los nodos (*virtual_machine_configuration***o***cloud_service_configuration*: necesario)<p/>En *python_tutorial_client.py*, se crea un grupo de nodos de Linux con [VirtualMachineConfiguration][py_vm_config]. Hola `select_latest_verified_vm_image_with_node_agent_sku` funcionando en `common.helpers` simplifica el trabajo con [máquinas virtuales de Azure Marketplace] [ vm_marketplace] imágenes. Para más información acerca del uso de imágenes de Marketplace, consulte [Aprovisionamiento de nodos de proceso de Linux en grupos del servicio Azure Batch](batch-linux-nodes.md) .
* **Tamaño de los nodos de proceso** (*vm_size*: necesario)<p/>Dado que especificamos nodos de Linux para nuestra instancia de [VirtualMachineConfiguration][py_vm_config], especificamos también un tamaño de máquina virtual (`STANDARD_A1` en este ejemplo) de los que aparecen en [Tamaños de las máquinas virtuales Linux en Azure](../virtual-machines/linux/sizes.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json). Para más información, vuelva a consultar [Aprovisionamiento de nodos de proceso de Linux en grupos del servicio Lote de Azure](batch-linux-nodes.md) .
* **Tarea de inicio** (*start_task*: no necesario)<p/>Junto con hello por encima de las propiedades de nodo físico, también puede especificar un [StartTask] [ py_starttask] para grupo de hello (no es necesario). Hola StartTask se ejecuta en cada nodo según ese nodo une a grupo de Hola y cada vez que se reinicie un nodo. Hola StartTask resulta especialmente útil para preparar los nodos de proceso para la ejecución de Hola de tareas, como la instalación de aplicaciones de Hola que se ejecutan las tareas.<p/>En esta aplicación de ejemplo Hola StartTask copia los archivos de Hola que descarga desde el almacenamiento (que se especifican mediante el uso de hello StartTask **resource_files** propiedad) de hello StartTask *deldirectoriodetrabajo* toohello *compartido* directorio que pueden tener acceso todas las tareas que se ejecutan en el nodo de Hola. Básicamente, se copian `python_tutorial_task.py` toohello directorio compartido en cada nodo como nodo de Hola une a grupo de hello, para que las tareas que se ejecutan en el nodo de hello pueden tener acceso a él.

Puede que observe Hola llamada toohello `wrap_commands_in_shell` función auxiliar. Esta función toma una colección de comandos independientes y crea una línea de comandos adecuada para la propiedad de la línea de comandos de la tarea.

También importantes en el fragmento de código de hello anterior es el uso de Hola de dos variables de entorno de hello **command_line** propiedad de hello StartTask: `AZ_BATCH_TASK_WORKING_DIR` y `AZ_BATCH_NODE_SHARED_DIR`. Cada nodo de ejecución dentro de un grupo de proceso por lotes se configura automáticamente con varias variables de entorno que están tooBatch específico. Cualquier proceso que se ejecuta una tarea tiene acceso a variables de entorno de toothese.

> [!TIP]
> toofind más información sobre las variables de entorno de Hola que están disponibles en los nodos de proceso en un grupo de lote, así como información de directorios de trabajo de tarea, consulte **configuración del entorno para tareas** y **archivos y directorios**  en hello [información general de las características de Azure Batch](batch-api-basics.md).
>
>

## <a name="step-4-create-batch-job"></a>Paso 4: Crear el trabajo de Batch
![Crear un trabajo de Batch][4]<br/>

Un **trabajo** de Batch es una colección de tareas y está asociado a un grupo de nodos de proceso. las tareas de Hello en un trabajo que se ejecutan en nodos de proceso del grupo de hello asociado.

Puede usar un trabajo no solo para organizar y seguimiento de las tareas en las cargas de trabajo relacionados, sino también para imponer ciertas restricciones, como el tiempo de ejecución máximo de hello para el trabajo de hello (y por extensión, sus tareas) y prioridad de trabajo en los trabajos de relación tooother en Hola cuenta de lote. Sin embargo, en este ejemplo, el trabajo de Hola se asocia únicamente a grupo Hola que creó en el paso 3 de #. No hay propiedades adicionales configuradas.

Todos los trabajos de Batch están asociados a un grupo específico. Esta asociación indica qué nodos que ejecutan tareas del trabajo de hello en. Especificar el grupo de hello mediante hello [PoolInformation] [ py_poolinfo] propiedad, como se muestra en el siguiente fragmento de código de hello.

```python
def create_job(batch_service_client, job_id, pool_id):
    """
    Creates a job with hello specified ID, associated with hello specified pool.

    :param batch_service_client: A Batch service client.
    :type batch_service_client: `azure.batch.BatchServiceClient`
    :param str job_id: hello ID for hello job.
    :param str pool_id: hello ID for hello pool.
    """
    print('Creating job [{}]...'.format(job_id))

    job = batch.models.JobAddParameter(
        job_id,
        batch.models.PoolInformation(pool_id=pool_id))

    try:
        batch_service_client.job.add(job)
    except batchmodels.batch_error.BatchErrorException as err:
        print_batch_exception(err)
        raise
```

Ahora que se ha creado un trabajo, las tareas se agregan trabajo de hello tooperform.

## <a name="step-5-add-tasks-toojob"></a>Paso 5: Agregar toojob de tareas
![Agregar tareas toojob][5]<br/>
*(1) tareas se agregan toohello trabajo, tareas de hello (2) son toorun programada en nodos y tareas (3) Hola descargar tooprocess de archivos de datos de Hola*

Lote **tareas** son nodos de proceso de hello unidades de trabajo que se ejecutan en Hola. Una tarea tiene una línea de comandos y ejecuta scripts de Hola o archivos ejecutables que especifique en esa línea de comandos.

tooactually realizar el trabajo, se deben agregar tareas tooa trabajo. Cada [CloudTask] [ py_task] se configura con una propiedad de línea de comandos y [ResourceFiles] [ py_resource_file] (al igual que con StartTask del grupo de Hola) que Hola tarea de descarga toohello nodo antes de su línea de comandos se ejecuta automáticamente. En el ejemplo de Hola, cada tarea procesa un solo archivo. Por lo tanto, su colección ResourceFiles contiene un único elemento.

```python
def add_tasks(batch_service_client, job_id, input_files,
              output_container_name, output_container_sas_token):
    """
    Adds a task for each input file in hello collection toohello specified job.

    :param batch_service_client: A Batch service client.
    :type batch_service_client: `azure.batch.BatchServiceClient`
    :param str job_id: hello ID of hello job toowhich tooadd hello tasks.
    :param list input_files: A collection of input files. One task will be
     created for each input file.
    :param output_container_name: hello ID of an Azure Blob storage container to
    which hello tasks will upload their results.
    :param output_container_sas_token: A SAS token granting write access to
    hello specified Azure Blob storage container.
    """

    print('Adding {} tasks toojob [{}]...'.format(len(input_files), job_id))

    tasks = list()

    for input_file in input_files:

        command = ['python $AZ_BATCH_NODE_SHARED_DIR/python_tutorial_task.py '
                   '--filepath {} --numwords {} --storageaccount {} '
                   '--storagecontainer {} --sastoken "{}"'.format(
                    input_file.file_path,
                    '3',
                    _STORAGE_ACCOUNT_NAME,
                    output_container_name,
                    output_container_sas_token)]

        tasks.append(batch.models.TaskAddParameter(
                'topNtask{}'.format(input_files.index(input_file)),
                wrap_commands_in_shell('linux', command),
                resource_files=[input_file]
                )
        )

    batch_service_client.task.add_collection(job_id, tasks)
```

> [!IMPORTANT]
> Cuando tengan acceso a las variables de entorno como `$AZ_BATCH_NODE_SHARED_DIR` o ejecutar una aplicación no se encuentra en el nodo de hello `PATH`, líneas de comandos de la tarea debe invocar Hola shell explícitamente, como con `/bin/sh -c MyTaskApplication $MY_ENV_VAR`. Este requisito no es necesario si las tareas ejecutan una aplicación en el nodo de hello `PATH` y no hacen referencia a las variables de entorno.
>
>

Dentro de hello `for` bucle en el fragmento de código de hello anterior, puede ver que la línea de comandos de hello para la tarea hello se construye con cinco argumentos de línea de comandos que se pasan demasiado*python_tutorial_task.py*:

1. **FilePath**: este es el archivo de toohello de ruta de acceso local de hello tal como existe en el nodo de Hola. Hola al objeto ResourceFile en `upload_file_to_container` se creó en el paso 2 anterior, el nombre de archivo de Hola se usó para esta propiedad (hello `file_path` parámetro hello ResourceFile constructor). Esto indica que ese archivo hello puede encontrarse en hello mismo directorio en el nodo de hello como *python_tutorial_task.py*.
2. **NUMWORDS**: parte superior de hello *N* palabras deberían escribir el archivo de salida de toohello.
3. **storageaccount**: nombre de Hola de hello cuenta de almacenamiento que posee el resultado de la tarea de hello contenedor toowhich Hola se debe cargar.
4. **storagecontainer**: nombre de Hola de Hola Hola de toowhich de contenedor de almacenamiento se deben cargar los archivos de salida.
5. **sastoken**: firma de acceso compartido (SAS) de Hola que proporciona acceso de escritura toohello **salida** contenedor en el almacenamiento de Azure. Hola *python_tutorial_task.py* secuencia de comandos utiliza esta firma de acceso compartido cuando se crea su referencia BlockBlobService. Esto proporciona acceso de escritura toohello contenedor sin necesidad de una clave de acceso para la cuenta de almacenamiento de Hola.

```python
# NOTE: Taken from python_tutorial_task.py

# Create hello blob client using hello container's SAS token.
# This allows us toocreate a client that provides write
# access only toohello container.
blob_client = azureblob.BlockBlobService(account_name=args.storageaccount,
                                         sas_token=args.sastoken)
```

## <a name="step-6-monitor-tasks"></a>Paso 6: Supervisar tareas
![Supervisar tareas][6]<br/>
*Hola crear scripts para tareas hello (1) los monitores de estado de finalización y tareas (2) Hola cargar tooAzure de datos de resultado almacenamiento*

Cuando las tareas se agregan trabajo tooa, están en cola y programadas para ejecutarse en nodos de ejecución dentro del bloque de hello asociado al trabajo de Hola automáticamente. En función de la configuración de Hola que especifique, por lotes controla Queue de todas las tareas, programación, Reintentar y otras tareas de administración de la tarea de.

Existen muchos enfoques de ejecución de la tarea de toomonitoring. Hola `wait_for_tasks_to_complete` funcionando en *python_tutorial_client.py* proporciona un ejemplo sencillo de tareas de supervisión para un estado determinado, en este caso, hello [completado] [ py_taskstate] estado.

```python
def wait_for_tasks_to_complete(batch_service_client, job_id, timeout):
    """
    Returns when all tasks in hello specified job reach hello Completed state.

    :param batch_service_client: A Batch service client.
    :type batch_service_client: `azure.batch.BatchServiceClient`
    :param str job_id: hello id of hello job whose tasks should be toomonitored.
    :param timedelta timeout: hello duration toowait for task completion. If all
    tasks in hello specified job do not reach Completed state within this time
    period, an exception will be raised.
    """
    timeout_expiration = datetime.datetime.now() + timeout

    print("Monitoring all tasks for 'Completed' state, timeout in {}..."
          .format(timeout), end='')

    while datetime.datetime.now() < timeout_expiration:
        print('.', end='')
        sys.stdout.flush()
        tasks = batch_service_client.task.list(job_id)

        incomplete_tasks = [task for task in tasks if
                            task.state != batchmodels.TaskState.completed]
        if not incomplete_tasks:
            print()
            return True
        else:
            time.sleep(1)

    print()
    raise RuntimeError("ERROR: Tasks did not reach 'Completed' state within "
                       "timeout period of " + str(timeout))
```

## <a name="step-7-download-task-output"></a>Paso 7: Descargar el resultado de la tarea
![Descargar el resultado de la tarea de Storage][7]<br/>

Ahora que hello trabajo se completa, resultado de hello de las tareas de hello puede descargarse desde el almacenamiento de Azure. Esto se realiza con una llamada demasiado`download_blobs_from_container` en *python_tutorial_client.py*:

```python
def download_blobs_from_container(block_blob_client,
                                  container_name, directory_path):
    """
    Downloads all blobs from hello specified Azure Blob storage container.

    :param block_blob_client: A blob service client.
    :type block_blob_client: `azure.storage.blob.BlockBlobService`
    :param container_name: hello Azure Blob storage container from which to
     download files.
    :param directory_path: hello local directory toowhich toodownload hello files.
    """
    print('Downloading all files from container [{}]...'.format(
        container_name))

    container_blobs = block_blob_client.list_blobs(container_name)

    for blob in container_blobs.items:
        destination_file_path = os.path.join(directory_path, blob.name)

        block_blob_client.get_blob_to_path(container_name,
                                           blob.name,
                                           destination_file_path)

        print('  Downloaded blob [{}] from container [{}] too{}'.format(
            blob.name,
            container_name,
            destination_file_path))

    print('  Download complete!')
```

> [!NOTE]
> Hola llamada demasiado`download_blobs_from_container` en *python_tutorial_client.py* especifica que los archivos de hello deben ser directorio particular tooyour descargado. Cree toomodify libre esta ubicación de salida.
>
>

## <a name="step-8-delete-containers"></a>Paso 8: Eliminar contenedores
Dado que se le cobrará por datos que residen en el almacenamiento de Azure, siempre es un tooremove buena idea los blobs que no tengan más necesarios para los trabajos por lotes. En *python_tutorial_client.py*, esto se realiza con tres llamadas demasiado[BlockBlobService.delete_container][py_delete_container]:

```python
# Clean up storage resources
print('Deleting containers...')
blob_client.delete_container(app_container_name)
blob_client.delete_container(input_container_name)
blob_client.delete_container(output_container_name)
```

## <a name="step-9-delete-hello-job-and-hello-pool"></a>Paso 9: Eliminar trabajo hello y grupo de Hola
En el paso final de hello, es toodelete solicitadas Hola hello y trabajo de grupo creados por hello *python_tutorial_client.py* secuencia de comandos. Aunque no se cobran los trabajos y tareas, *sí* se cobran los nodos de proceso. Por consiguiente, se recomienda asignar solo los nodos necesarios. La eliminación de los grupos que no se usen puede formar parte del proceso de mantenimiento.

Hola BatchServiceClient [JobOperations] [ py_job] y [PoolOperations] [ py_pool] tienen métodos de eliminación correspondientes, que son se llama si Confirmar eliminación:

```python
# Clean up Batch resources (if hello user so chooses).
if query_yes_no('Delete job?') == 'yes':
    batch_client.job.delete(_JOB_ID)

if query_yes_no('Delete pool?') == 'yes':
    batch_client.pool.delete(_POOL_ID)
```

> [!IMPORTANT]
> Tenga en cuenta que los recursos de proceso se cobran (la eliminación de grupos sin usar reducirá el costo). Además, tenga en cuenta que al eliminar un grupo eliminan todos los nodos de proceso dentro de ese grupo y que todos los datos de los nodos de hello serán irrecuperables después de elimina el grupo de Hola.
>
>

## <a name="run-hello-sample-script"></a>Ejecutar script de ejemplo de Hola
Cuando ejecute hello *python_tutorial_client.py* secuencia de comandos de tutorial de hello [ejemplo de código][github_article_samples], salida de la consola de hello es similar siguiente de toohello. Hay una pausa en `Monitoring all tasks for 'Completed' state, timeout in 0:20:00...` mientras se crean nodos de proceso del grupo de hello, inicia, y se ejecutan comandos de hello en la tarea de inicio del grupo de Hola. Hola de uso [portal de Azure] [ azure_portal] toomonitor su grupo, nodos de proceso, trabajo y las tareas durante y después de la ejecución. Hola de uso [portal de Azure] [ azure_portal] o hello [Microsoft Azure Storage Explorer] [ storage_explorer] tooview los recursos de almacenamiento hello (contenedores y blobs) que se crean por aplicación hello.

> [!TIP]
> Ejecute hello *python_tutorial_client.py* script desde dentro de hello `azure-batch-samples/Python/Batch/article_samples` directory. Utiliza una ruta de acceso relativa para hello `common.helpers` importación del módulo, por lo que es posible que vea `ImportError: No module named 'common'` si no ejecuta el script de Hola desde dentro de este directorio.
>
>

Tiempo de ejecución típica es **aproximadamente 5-7 minutos** al ejecutar el ejemplo hello en su configuración predeterminada.

```
Sample start: 2016-05-20 22:47:10

Uploading file /home/user/py_tutorial/python_tutorial_task.py toocontainer [application]...
Uploading file /home/user/py_tutorial/data/taskdata1.txt toocontainer [input]...
Uploading file /home/user/py_tutorial/data/taskdata2.txt toocontainer [input]...
Uploading file /home/user/py_tutorial/data/taskdata3.txt toocontainer [input]...
Creating pool [PythonTutorialPool]...
Creating job [PythonTutorialJob]...
Adding 3 tasks toojob [PythonTutorialJob]...
Monitoring all tasks for 'Completed' state, timeout in 0:20:00..........................................................................
  Success! All tasks reached hello 'Completed' state within hello specified timeout period.
Downloading all files from container [output]...
  Downloaded blob [taskdata1_OUTPUT.txt] from container [output] too/home/user/taskdata1_OUTPUT.txt
  Downloaded blob [taskdata2_OUTPUT.txt] from container [output] too/home/user/taskdata2_OUTPUT.txt
  Downloaded blob [taskdata3_OUTPUT.txt] from container [output] too/home/user/taskdata3_OUTPUT.txt
  Download complete!
Deleting containers...

Sample end: 2016-05-20 22:53:12
Elapsed time: 0:06:02

Delete job? [Y/n]
Delete pool? [Y/n]

Press ENTER tooexit...
```

## <a name="next-steps"></a>Pasos siguientes
Cree cambios toomake libre demasiado*python_tutorial_client.py* y *python_tutorial_task.py* tooexperiment con diferentes escenarios de proceso. Por ejemplo, intente agregar un retraso de ejecución demasiado*python_tutorial_task.py* toosimulate ejecución prolongada tareas y supervisarlos en el portal de Hola. Intente agregar más tareas o ajustar Hola número de nodos de cálculo. Agregar lógica toocheck para y permitir el uso de Hola de un tiempo de ejecución de toospeed de grupo existente.

Ahora que está familiarizado con un flujo de trabajo básico de Hola de una solución de lote, es hora toodig en toohello características adicionales de hello servicio por lotes.

* Hola de revisión [características de información general de Azure Batch](batch-api-basics.md) artículo, que se recomienda si dispone de un nuevo servicio de toohello.
* Inicio de Hola otros artículos de desarrollo de lote en **desarrollo detallada** en hello [ruta de acceso de aprendizaje por lotes][batch_learning_path].
* Extraer del repositorio una implementación diferente de procesamiento Hola "top N palabras" carga de trabajo con lote hello [TopNWords] [ github_topnwords] ejemplo.

[azure_batch]: https://azure.microsoft.com/services/batch/
[azure_free_account]: https://azure.microsoft.com/free/
[azure_portal]: https://portal.azure.com
[batch_learning_path]: https://azure.microsoft.com/documentation/learning-paths/batch/
[blog_linux]: http://blogs.technet.com/b/windowshpc/archive/2016/03/30/introducing-linux-support-on-azure-batch.aspx
[crypto]: https://cryptography.io/en/latest/
[crypto_install]: https://cryptography.io/en/latest/installation/
[github_samples]: https://github.com/Azure/azure-batch-samples
[github_samples_zip]: https://github.com/Azure/azure-batch-samples/archive/master.zip
[github_topnwords]: https://github.com/Azure/azure-batch-samples/tree/master/CSharp/TopNWords
[github_article_samples]: https://github.com/Azure/azure-batch-samples/tree/master/Python/Batch/article_samples

[nuget_packagemgr]: https://visualstudiogallery.msdn.microsoft.com/27077b70-9dad-4c64-adcf-c7cf6bc9970c
[nuget_restore]: https://docs.nuget.org/consume/package-restore/msbuild-integrated#enabling-package-restore-during-build

[py_account_ops]: http://azure-sdk-for-python.readthedocs.org/en/latest/ref/azure.batch.operations.html#azure.batch.operations.AccountOperations
[py_azure_sdk]: https://pypi.python.org/pypi/azure
[py_batch_docs]: http://azure-sdk-for-python.readthedocs.org/en/latest/ref/azure.batch.html
[py_batch_package]: https://pypi.python.org/pypi/azure-batch
[py_batchserviceclient]: http://azure-sdk-for-python.readthedocs.io/en/latest/ref/azure.batch.html#azure.batch.BatchServiceClient
[py_blockblobservice]: http://azure.github.io/azure-storage-python/ref/azure.storage.blob.blockblobservice.html#azure.storage.blob.blockblobservice.BlockBlobService
[py_cloudtask]: http://azure-sdk-for-python.readthedocs.io/en/latest/ref/azure.batch.models.html#azure.batch.models.CloudTask
[py_computenodeuser]: http://azure-sdk-for-python.readthedocs.org/en/latest/ref/azure.batch.models.html#azure.batch.models.ComputeNodeUser
[py_cs_config]: http://azure-sdk-for-python.readthedocs.io/en/latest/ref/azure.batch.models.html#azure.batch.models.CloudServiceConfiguration
[py_delete_container]: http://azure.github.io/azure-storage-python/ref/azure.storage.blob.baseblobservice.html#azure.storage.blob.baseblobservice.BaseBlobService.delete_container
[py_gen_blob_sas]: http://azure.github.io/azure-storage-python/ref/azure.storage.blob.baseblobservice.html#azure.storage.blob.baseblobservice.BaseBlobService.generate_blob_shared_access_signature
[py_gen_container_sas]: http://azure.github.io/azure-storage-python/ref/azure.storage.blob.baseblobservice.html#azure.storage.blob.baseblobservice.BaseBlobService.generate_container_shared_access_signature
[py_image_ref]: http://azure-sdk-for-python.readthedocs.io/en/latest/ref/azure.batch.models.html#azure.batch.models.ImageReference
[py_imagereference]: http://azure-sdk-for-python.readthedocs.org/en/latest/ref/azure.batch.models.html#azure.batch.models.ImageReference
[py_job]: http://azure-sdk-for-python.readthedocs.io/en/latest/ref/azure.batch.operations.html#azure.batch.operations.JobOperations
[py_jobpreptask]: http://azure-sdk-for-python.readthedocs.io/en/latest/ref/azure.batch.models.html#azure.batch.models.JobPreparationTask
[py_jobreltask]: http://azure-sdk-for-python.readthedocs.io/en/latest/ref/azure.batch.models.html#azure.batch.models.JobReleaseTask
[py_list_skus]: http://azure-sdk-for-python.readthedocs.io/en/latest/ref/azure.batch.operations.html#azure.batch.operations.AccountOperations.list_node_agent_skus
[py_make_blob_url]: http://azure.github.io/azure-storage-python/ref/azure.storage.blob.baseblobservice.html#azure.storage.blob.baseblobservice.BaseBlobService.make_blob_url
[py_pool]: http://azure-sdk-for-python.readthedocs.io/en/latest/ref/azure.batch.operations.html#azure.batch.operations.PoolOperations
[py_pooladdparam]: http://azure-sdk-for-python.readthedocs.io/en/latest/ref/azure.batch.models.html#azure.batch.models.PoolAddParameter
[py_poolinfo]: http://azure-sdk-for-python.readthedocs.io/en/latest/ref/azure.batch.models.html#azure.batch.models.PoolInformation
[py_resource_file]: http://azure-sdk-for-python.readthedocs.io/en/latest/ref/azure.batch.models.html#azure.batch.models.ResourceFile
[py_samples_github]: https://github.com/Azure/azure-batch-samples/tree/master/Python/Batch/
[py_starttask]: http://azure-sdk-for-python.readthedocs.io/en/latest/ref/azure.batch.models.html#azure.batch.models.StartTask
[py_starttask]: http://azure-sdk-for-python.readthedocs.io/en/latest/ref/azure.batch.models.html#azure.batch.models.StartTask
[py_task]: http://azure-sdk-for-python.readthedocs.io/en/latest/ref/azure.batch.models.html#azure.batch.models.CloudTask
[py_taskstate]: http://azure-sdk-for-python.readthedocs.io/en/latest/ref/azure.batch.models.html#azure.batch.models.TaskState
[py_vm_config]: http://azure-sdk-for-python.readthedocs.io/en/latest/ref/azure.batch.models.html#azure.batch.models.VirtualMachineConfiguration
[pypi_batch]: https://pypi.python.org/pypi/azure-batch
[pypi_storage]: https://pypi.python.org/pypi/azure-storage
[pypi_install]: https://packaging.python.org/installing/
[storage_explorer]: http://storageexplorer.com/
[visual_studio]: https://www.visualstudio.com/products/vs-2015-product-editions
[vm_marketplace]: https://azure.microsoft.com/marketplace/virtual-machines/

[1]: ./media/batch-python-tutorial/batch_workflow_01_sm.png "Crear contenedores en Azure Storage"
[2]: ./media/batch-python-tutorial/batch_workflow_02_sm.png "Toocontainers de archivos de la tarea de carga de aplicación y entrada (datos)"
[3]: ./media/batch-python-tutorial/batch_workflow_03_sm.png "Crear el grupo de Batch"
[4]: ./media/batch-python-tutorial/batch_workflow_04_sm.png "Crear trabajo de Batch"
[5]: ./media/batch-python-tutorial/batch_workflow_05_sm.png "Agregar tareas toojob"
[6]: ./media/batch-python-tutorial/batch_workflow_06_sm.png "Supervisar tareas"
[7]: ./media/batch-python-tutorial/batch_workflow_07_sm.png "Descargar el resultado de la tarea de Storage"
[8]: ./media/batch-python-tutorial/batch_workflow_sm.png "Flujo de trabajo de soluciones de Batch (diagrama completo)"
[9]: ./media/batch-python-tutorial/credentials_batch_sm.png "Credenciales de Batch en el portal"
[10]: ./media/batch-python-tutorial/credentials_storage_sm.png "Credenciales de Storage en el portal"
[11]: ./media/batch-python-tutorial/batch_workflow_minimal_sm.png "Flujo de trabajo de soluciones de Batch (diagrama mínimo)"
