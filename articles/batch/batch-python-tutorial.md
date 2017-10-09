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
# <a name="get-started-with-hello-batch-sdk-for-python"></a><span data-ttu-id="b89d0-103">Empezar a trabajar con hello lote SDK para Python</span><span class="sxs-lookup"><span data-stu-id="b89d0-103">Get started with hello Batch SDK for Python</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="b89d0-104">.NET</span><span class="sxs-lookup"><span data-stu-id="b89d0-104">.NET</span></span>](batch-dotnet-get-started.md)
> * [<span data-ttu-id="b89d0-105">Python</span><span class="sxs-lookup"><span data-stu-id="b89d0-105">Python</span></span>](batch-python-tutorial.md)
> * [<span data-ttu-id="b89d0-106">Node.js</span><span class="sxs-lookup"><span data-stu-id="b89d0-106">Node.js</span></span>](batch-nodejs-get-started.md)
>
>

<span data-ttu-id="b89d0-107">Obtenga información acerca de los conceptos básicos de Hola de [Azure Batch] [ azure_batch] hello y [lote Python] [ py_azure_sdk] cliente tal y como se describe una aplicación de lote pequeña escrita en Python.</span><span class="sxs-lookup"><span data-stu-id="b89d0-107">Learn hello basics of [Azure Batch][azure_batch] and hello [Batch Python][py_azure_sdk] client as we discuss a small Batch application written in Python.</span></span> <span data-ttu-id="b89d0-108">Veremos cómo dos muestras las secuencias de comandos use Hola lote servicio tooprocess una carga de trabajo paralelo en máquinas virtuales de Linux en la nube de Hola y cómo interactúan con [el almacenamiento de Azure](../storage/common/storage-introduction.md) para almacenamiento provisional de archivo y la recuperación.</span><span class="sxs-lookup"><span data-stu-id="b89d0-108">We look at how two sample scripts use hello Batch service tooprocess a parallel workload on Linux virtual machines in hello cloud, and how they interact with [Azure Storage](../storage/common/storage-introduction.md) for file staging and retrieval.</span></span> <span data-ttu-id="b89d0-109">Podrá Obtenga información acerca de un flujo de trabajo de aplicación común de lote y obtener una descripción de base de componentes principales Hola de lote como trabajos, tareas, grupos y nodos de ejecución.</span><span class="sxs-lookup"><span data-stu-id="b89d0-109">You'll learn a common Batch application workflow and gain a base understanding of hello major components of Batch such as jobs, tasks, pools, and compute nodes.</span></span>

<span data-ttu-id="b89d0-110">![Flujo de trabajo de soluciones de Batch (básico)][11]</span><span class="sxs-lookup"><span data-stu-id="b89d0-110">![Batch solution workflow (basic)][11]</span></span><br/>

## <a name="prerequisites"></a><span data-ttu-id="b89d0-111">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="b89d0-111">Prerequisites</span></span>
<span data-ttu-id="b89d0-112">En este artículo se considera que tiene conocimientos prácticos de Python y está familiarizado con Linux.</span><span class="sxs-lookup"><span data-stu-id="b89d0-112">This article assumes that you have a working knowledge of Python and familiarity with Linux.</span></span> <span data-ttu-id="b89d0-113">También se da por supuesto que es capaz de toosatisfy Hola creación requisitos de las cuentas que se especifican a continuación para Azure y Hola por lotes y los servicios de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="b89d0-113">It also assumes that you're able toosatisfy hello account creation requirements that are specified below for Azure and hello Batch and Storage services.</span></span>

### <a name="accounts"></a><span data-ttu-id="b89d0-114">Cuentas</span><span class="sxs-lookup"><span data-stu-id="b89d0-114">Accounts</span></span>
* <span data-ttu-id="b89d0-115">**Cuenta de Azure**: si aún no tiene ninguna suscripción a Azure, [cree una cuenta gratuita de Azure][azure_free_account].</span><span class="sxs-lookup"><span data-stu-id="b89d0-115">**Azure account**: If you don't already have an Azure subscription, [create a free Azure account][azure_free_account].</span></span>
* <span data-ttu-id="b89d0-116">**Cuenta de Batch**: una vez que tenga una suscripción a Azure, [cree una cuenta de Azure Batch](batch-account-create-portal.md).</span><span class="sxs-lookup"><span data-stu-id="b89d0-116">**Batch account**: Once you have an Azure subscription, [create an Azure Batch account](batch-account-create-portal.md).</span></span>
* <span data-ttu-id="b89d0-117">**Cuenta de almacenamiento**: consulte la sección [Crear una cuenta de almacenamiento](../storage/common/storage-create-storage-account.md#create-a-storage-account) del artículo [Acerca de las cuentas de almacenamiento de Azure](../storage/common/storage-create-storage-account.md).</span><span class="sxs-lookup"><span data-stu-id="b89d0-117">**Storage account**: See [Create a storage account](../storage/common/storage-create-storage-account.md#create-a-storage-account) in [About Azure storage accounts](../storage/common/storage-create-storage-account.md).</span></span>

### <a name="code-sample"></a><span data-ttu-id="b89d0-118">Código de ejemplo</span><span class="sxs-lookup"><span data-stu-id="b89d0-118">Code sample</span></span>
<span data-ttu-id="b89d0-119">tutorial de Python de Hello [código de ejemplo] [ github_article_samples] es uno de los muchos ejemplos de código de proceso por lotes que se encuentran en Hola de hello [ejemplos de lote de azure] [ github_samples] repositorio en GitHub.</span><span class="sxs-lookup"><span data-stu-id="b89d0-119">hello Python tutorial [code sample][github_article_samples] is one of hello many Batch code samples found in hello [azure-batch-samples][github_samples] repository on GitHub.</span></span> <span data-ttu-id="b89d0-120">Puede descargar todos los ejemplos de hello haciendo clic en **clon o una descarga > Download ZIP** en página de inicio del repositorio de hello, o haciendo clic en hello [azure-lote-ejemplos-master.zip] [ github_samples_zip]vínculo de descarga directa.</span><span class="sxs-lookup"><span data-stu-id="b89d0-120">You can download all hello samples by clicking **Clone or download > Download ZIP** on hello repository home page, or by clicking hello [azure-batch-samples-master.zip][github_samples_zip] direct download link.</span></span> <span data-ttu-id="b89d0-121">Una vez que haya extraído contenido Hola del archivo ZIP de hello, secuencias de comandos de hello dos para este tutorial se encuentran en hello `article_samples` directorio:</span><span class="sxs-lookup"><span data-stu-id="b89d0-121">Once you've extracted hello contents of hello ZIP file, hello two scripts for this tutorial are found in hello `article_samples` directory:</span></span>

`/azure-batch-samples/Python/Batch/article_samples/python_tutorial_client.py`<br/>
`/azure-batch-samples/Python/Batch/article_samples/python_tutorial_task.py`

### <a name="python-environment"></a><span data-ttu-id="b89d0-122">Entorno de Python</span><span class="sxs-lookup"><span data-stu-id="b89d0-122">Python environment</span></span>
<span data-ttu-id="b89d0-123">Hola toorun *python_tutorial_client.py* secuencia de comandos de ejemplo en la estación de trabajo local, necesita un **intérprete Python** compatible con la versión **2.7** o **3.3 +**.</span><span class="sxs-lookup"><span data-stu-id="b89d0-123">toorun hello *python_tutorial_client.py* sample script on your local workstation, you need a **Python interpreter** compatible with version **2.7** or **3.3+**.</span></span> <span data-ttu-id="b89d0-124">script de Hola se ha probado en Linux y Windows.</span><span class="sxs-lookup"><span data-stu-id="b89d0-124">hello script has been tested on both Linux and Windows.</span></span>

### <a name="cryptography-dependencies"></a><span data-ttu-id="b89d0-125">Dependencias de cryptography</span><span class="sxs-lookup"><span data-stu-id="b89d0-125">cryptography dependencies</span></span>
<span data-ttu-id="b89d0-126">Debe instalar las dependencias de Hola de hello [criptografía] [ crypto] library, requerida por hello `azure-batch` y `azure-storage` paquetes de Python.</span><span class="sxs-lookup"><span data-stu-id="b89d0-126">You must install hello dependencies for hello [cryptography][crypto] library, required by hello `azure-batch` and `azure-storage` Python packages.</span></span> <span data-ttu-id="b89d0-127">Realice uno de hello siguiendo las operaciones adecuadas para su plataforma o consulte toohello [instalación de criptografía] [ crypto_install] detalles para obtener más información:</span><span class="sxs-lookup"><span data-stu-id="b89d0-127">Perform one of hello following operations appropriate for your platform, or refer toohello [cryptography installation][crypto_install] details for more information:</span></span>

* <span data-ttu-id="b89d0-128">Ubuntu</span><span class="sxs-lookup"><span data-stu-id="b89d0-128">Ubuntu</span></span>

    `apt-get update && apt-get install -y build-essential libssl-dev libffi-dev libpython-dev python-dev`
* <span data-ttu-id="b89d0-129">CentOS</span><span class="sxs-lookup"><span data-stu-id="b89d0-129">CentOS</span></span>

    `yum update && yum install -y gcc openssl-devel libffi-devel python-devel`
* <span data-ttu-id="b89d0-130">SLES/OpenSUSE</span><span class="sxs-lookup"><span data-stu-id="b89d0-130">SLES/OpenSUSE</span></span>

    `zypper ref && zypper -n in libopenssl-dev libffi48-devel python-devel`
* <span data-ttu-id="b89d0-131">Windows</span><span class="sxs-lookup"><span data-stu-id="b89d0-131">Windows</span></span>

    `pip install cryptography`

> [!NOTE]
> <span data-ttu-id="b89d0-132">Si la instalación de Python 3.3 + en Linux, utilizar los equivalentes de python3 de Hola para las dependencias de Python de Hola.</span><span class="sxs-lookup"><span data-stu-id="b89d0-132">If installing for Python 3.3+ on Linux, use hello python3 equivalents for hello Python dependencies.</span></span> <span data-ttu-id="b89d0-133">Por ejemplo, en Ubuntu: `apt-get update && apt-get install -y build-essential libssl-dev libffi-dev libpython3-dev python3-dev`</span><span class="sxs-lookup"><span data-stu-id="b89d0-133">For example, on Ubuntu: `apt-get update && apt-get install -y build-essential libssl-dev libffi-dev libpython3-dev python3-dev`</span></span>
>
>

### <a name="azure-packages"></a><span data-ttu-id="b89d0-134">Paquetes de Azure</span><span class="sxs-lookup"><span data-stu-id="b89d0-134">Azure packages</span></span>
<span data-ttu-id="b89d0-135">A continuación, instale hello **Azure Batch** y **el almacenamiento de Azure** paquetes de Python.</span><span class="sxs-lookup"><span data-stu-id="b89d0-135">Next, install hello **Azure Batch** and **Azure Storage** Python packages.</span></span> <span data-ttu-id="b89d0-136">Puede instalar ambos paquetes mediante **pip** hello y *requirements.txt* encontrar aquí:</span><span class="sxs-lookup"><span data-stu-id="b89d0-136">You can install both packages by using **pip** and hello *requirements.txt* found here:</span></span>

`/azure-batch-samples/Python/Batch/requirements.txt`

<span data-ttu-id="b89d0-137">Problema siguiente **pip** paquetes de lote y el almacenamiento de hello tooinstall de comandos:</span><span class="sxs-lookup"><span data-stu-id="b89d0-137">Issue following **pip** command tooinstall hello Batch and Storage packages:</span></span>

`pip install -r requirements.txt`

<span data-ttu-id="b89d0-138">O bien, puede instalar hello [lote de azure] [ pypi_batch] y [almacenamiento de azure] [ pypi_storage] Python paquetes manualmente:</span><span class="sxs-lookup"><span data-stu-id="b89d0-138">Or, you can install hello [azure-batch][pypi_batch] and [azure-storage][pypi_storage] Python packages manually:</span></span>

`pip install azure-batch`<br/>
`pip install azure-storage`

> [!TIP]
> <span data-ttu-id="b89d0-139">Si usas una cuenta sin privilegios, puede que tenga tooprefix los comandos con `sudo`.</span><span class="sxs-lookup"><span data-stu-id="b89d0-139">If you are using an unprivileged account, you may need tooprefix your commands with `sudo`.</span></span> <span data-ttu-id="b89d0-140">Por ejemplo: `sudo pip install -r requirements.txt`.</span><span class="sxs-lookup"><span data-stu-id="b89d0-140">For example, `sudo pip install -r requirements.txt`.</span></span> <span data-ttu-id="b89d0-141">Para más información acerca de cómo instalar los paquetes de Python, consulte [Installing Packages][pypi_install] (Instalación de paquetes) en python.org.</span><span class="sxs-lookup"><span data-stu-id="b89d0-141">For more information on installing Python packages, see [Installing Packages][pypi_install] on python.org.</span></span>
>
>

## <a name="batch-python-tutorial-code-sample"></a><span data-ttu-id="b89d0-142">Ejemplo de código del tutorial de Python de Lote</span><span class="sxs-lookup"><span data-stu-id="b89d0-142">Batch Python tutorial code sample</span></span>
<span data-ttu-id="b89d0-143">ejemplo de código del tutorial de Python de lote de Hello consta de dos scripts de Python y algunos archivos de datos.</span><span class="sxs-lookup"><span data-stu-id="b89d0-143">hello Batch Python tutorial code sample consists of two Python scripts and a few data files.</span></span>

* <span data-ttu-id="b89d0-144">**python_tutorial_client.py**: interactúa con tooexecute de servicios de almacenamiento y por lotes Hola una carga de trabajo paralelo en nodos de proceso (máquinas virtuales).</span><span class="sxs-lookup"><span data-stu-id="b89d0-144">**python_tutorial_client.py**: Interacts with hello Batch and Storage services tooexecute a parallel workload on compute nodes (virtual machines).</span></span> <span data-ttu-id="b89d0-145">Hola *python_tutorial_client.py* script se ejecuta en la estación de trabajo local.</span><span class="sxs-lookup"><span data-stu-id="b89d0-145">hello *python_tutorial_client.py* script runs on your local workstation.</span></span>
* <span data-ttu-id="b89d0-146">**python_tutorial_task.py**: script de Hola que se ejecuta en nodos de cálculo en trabajo real de Azure tooperform Hola.</span><span class="sxs-lookup"><span data-stu-id="b89d0-146">**python_tutorial_task.py**: hello script that runs on compute nodes in Azure tooperform hello actual work.</span></span> <span data-ttu-id="b89d0-147">En el ejemplo de Hola, *python_tutorial_task.py* analiza Hola texto en un archivo descargado desde el almacenamiento de Azure (archivo de entrada de hello).</span><span class="sxs-lookup"><span data-stu-id="b89d0-147">In hello sample, *python_tutorial_task.py* parses hello text in a file downloaded from Azure Storage (hello input file).</span></span> <span data-ttu-id="b89d0-148">A continuación, genera un archivo de texto (archivo de salida de Hola) que contiene una lista de palabras de tres primeras Hola que aparecen en el archivo de entrada de Hola.</span><span class="sxs-lookup"><span data-stu-id="b89d0-148">Then it produces a text file (hello output file) that contains a list of hello top three words that appear in hello input file.</span></span> <span data-ttu-id="b89d0-149">Después de crear el archivo de salida de hello, *python_tutorial_task.py* cargas Hola tooAzure almacenamiento de archivo.</span><span class="sxs-lookup"><span data-stu-id="b89d0-149">After it creates hello output file, *python_tutorial_task.py* uploads hello file tooAzure Storage.</span></span> <span data-ttu-id="b89d0-150">Estarán disponibles para el script de cliente de descarga toohello ejecutando en la estación de trabajo.</span><span class="sxs-lookup"><span data-stu-id="b89d0-150">This makes it available for download toohello client script running on your workstation.</span></span> <span data-ttu-id="b89d0-151">Hola *python_tutorial_task.py* script se ejecuta en paralelo en varios nodos de cálculo en hello servicio por lotes.</span><span class="sxs-lookup"><span data-stu-id="b89d0-151">hello *python_tutorial_task.py* script runs in parallel on multiple compute nodes in hello Batch service.</span></span>
* <span data-ttu-id="b89d0-152">**./Data/taskdata\*.txt**: estos archivos de tres texto proporcionan la entrada de Hola para nodos de ejecución de tareas de Hola que se ejecutan en Hola.</span><span class="sxs-lookup"><span data-stu-id="b89d0-152">**./data/taskdata\*.txt**: These three text files provide hello input for hello tasks that run on hello compute nodes.</span></span>

<span data-ttu-id="b89d0-153">Hola siguiente diagrama muestra operaciones principales de hello realizadas por los scripts de cliente y la tarea de Hola.</span><span class="sxs-lookup"><span data-stu-id="b89d0-153">hello following diagram illustrates hello primary operations that are performed by hello client and task scripts.</span></span> <span data-ttu-id="b89d0-154">Este flujo de trabajo básico es típico de muchas soluciones de proceso que se crean con Batch.</span><span class="sxs-lookup"><span data-stu-id="b89d0-154">This basic workflow is typical of many compute solutions that are created with Batch.</span></span> <span data-ttu-id="b89d0-155">Mientras no muestran todas las características disponibles en hello servicio por lotes, casi cada escenario de lote incluye algunas partes de este flujo de trabajo.</span><span class="sxs-lookup"><span data-stu-id="b89d0-155">While it does not demonstrate every feature available in hello Batch service, nearly every Batch scenario includes portions of this workflow.</span></span>

<span data-ttu-id="b89d0-156">![Flujo de trabajo de ejemplo de Batch][8]</span><span class="sxs-lookup"><span data-stu-id="b89d0-156">![Batch example workflow][8]</span></span><br/>

[<span data-ttu-id="b89d0-157">**Paso 1.**</span><span class="sxs-lookup"><span data-stu-id="b89d0-157">**Step 1.**</span></span>](#step-1-create-storage-containers) <span data-ttu-id="b89d0-158">Crear **contenedores** en Azure Blob Storage.</span><span class="sxs-lookup"><span data-stu-id="b89d0-158">Create **containers** in Azure Blob Storage.</span></span><br/><span data-ttu-id="b89d0-159">
[**Paso 2.**](#step-2-upload-task-script-and-data-files)</span><span class="sxs-lookup"><span data-stu-id="b89d0-159">
[**Step 2.**](#step-2-upload-task-script-and-data-files)</span></span> <span data-ttu-id="b89d0-160">Cargar toocontainers de archivos de script y entrada de tarea.</span><span class="sxs-lookup"><span data-stu-id="b89d0-160">Upload task script and input files toocontainers.</span></span><br/><span data-ttu-id="b89d0-161">
[**Paso 3.**](#step-3-create-batch-pool)</span><span class="sxs-lookup"><span data-stu-id="b89d0-161">
[**Step 3.**](#step-3-create-batch-pool)</span></span> <span data-ttu-id="b89d0-162">Cree un **grupo** de Batch.</span><span class="sxs-lookup"><span data-stu-id="b89d0-162">Create a Batch **pool**.</span></span><br/>
  <span data-ttu-id="b89d0-163">&nbsp;&nbsp;&nbsp;&nbsp;**3a.**</span><span class="sxs-lookup"><span data-stu-id="b89d0-163">&nbsp;&nbsp;&nbsp;&nbsp;**3a.**</span></span> <span data-ttu-id="b89d0-164">Hola grupo **StartTask** descargas Hola tarea script (python_tutorial_task.py) toonodes cuando se unen a grupo Hola.</span><span class="sxs-lookup"><span data-stu-id="b89d0-164">hello pool **StartTask** downloads hello task script (python_tutorial_task.py) toonodes as they join hello pool.</span></span><br/><span data-ttu-id="b89d0-165">
[**Paso 4.**](#step-4-create-batch-job)</span><span class="sxs-lookup"><span data-stu-id="b89d0-165">
[**Step 4.**](#step-4-create-batch-job)</span></span> <span data-ttu-id="b89d0-166">Cree un **trabajo** de Batch.</span><span class="sxs-lookup"><span data-stu-id="b89d0-166">Create a Batch **job**.</span></span><br/><span data-ttu-id="b89d0-167">
[**Paso 5.**](#step-5-add-tasks-to-job)</span><span class="sxs-lookup"><span data-stu-id="b89d0-167">
[**Step 5.**](#step-5-add-tasks-to-job)</span></span> <span data-ttu-id="b89d0-168">Agregar **tareas** toohello trabajo.</span><span class="sxs-lookup"><span data-stu-id="b89d0-168">Add **tasks** toohello job.</span></span><br/>
  <span data-ttu-id="b89d0-169">&nbsp;&nbsp;&nbsp;&nbsp;**5a.**</span><span class="sxs-lookup"><span data-stu-id="b89d0-169">&nbsp;&nbsp;&nbsp;&nbsp;**5a.**</span></span> <span data-ttu-id="b89d0-170">las tareas de Hello son tooexecute programada en nodos.</span><span class="sxs-lookup"><span data-stu-id="b89d0-170">hello tasks are scheduled tooexecute on nodes.</span></span><br/>
    <span data-ttu-id="b89d0-171">&nbsp;&nbsp;&nbsp;&nbsp;**5b.**</span><span class="sxs-lookup"><span data-stu-id="b89d0-171">&nbsp;&nbsp;&nbsp;&nbsp;**5b.**</span></span> <span data-ttu-id="b89d0-172">Cada tarea descarga sus datos de entrada de Azure Storage y comienza la ejecución.</span><span class="sxs-lookup"><span data-stu-id="b89d0-172">Each task downloads its input data from Azure Storage, then begins execution.</span></span><br/><span data-ttu-id="b89d0-173">
[**Paso 6.**](#step-6-monitor-tasks)</span><span class="sxs-lookup"><span data-stu-id="b89d0-173">
[**Step 6.**](#step-6-monitor-tasks)</span></span> <span data-ttu-id="b89d0-174">Supervisar las tareas.</span><span class="sxs-lookup"><span data-stu-id="b89d0-174">Monitor tasks.</span></span><br/>
  <span data-ttu-id="b89d0-175">&nbsp;&nbsp;&nbsp;&nbsp;**6a.**</span><span class="sxs-lookup"><span data-stu-id="b89d0-175">&nbsp;&nbsp;&nbsp;&nbsp;**6a.**</span></span> <span data-ttu-id="b89d0-176">Tal y como se completan tareas, cargan su tooAzure de datos de salida almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="b89d0-176">As tasks are completed, they upload their output data tooAzure Storage.</span></span><br/><span data-ttu-id="b89d0-177">
[**Paso 7.**](#step-7-download-task-output)</span><span class="sxs-lookup"><span data-stu-id="b89d0-177">
[**Step 7.**](#step-7-download-task-output)</span></span> <span data-ttu-id="b89d0-178">Descargar el resultado de la tarea de Almacenamiento</span><span class="sxs-lookup"><span data-stu-id="b89d0-178">Download task output from Storage.</span></span>

<span data-ttu-id="b89d0-179">Como se ha indicado, no todas las soluciones de Lote realizan estos mismos pasos y se puede haber muchos otros; sin embargo, sin embargo, este ejemplo muestra los procesos comunes que se encuentran en una solución de Lote.</span><span class="sxs-lookup"><span data-stu-id="b89d0-179">As mentioned, not every Batch solution performs these exact steps, and may include many more, but this sample demonstrates common processes found in a Batch solution.</span></span>

## <a name="prepare-client-script"></a><span data-ttu-id="b89d0-180">Preparación del script de cliente</span><span class="sxs-lookup"><span data-stu-id="b89d0-180">Prepare client script</span></span>
<span data-ttu-id="b89d0-181">Antes de ejecutar el ejemplo hello, agregue sus credenciales de cuenta de lote y el almacenamiento demasiado*python_tutorial_client.py*.</span><span class="sxs-lookup"><span data-stu-id="b89d0-181">Before you run hello sample, add your Batch and Storage account credentials too*python_tutorial_client.py*.</span></span> <span data-ttu-id="b89d0-182">Si aún no lo ha hecho, abra el archivo de hello en los favoritos Hola de editor y actualización siguiendo las líneas con sus credenciales.</span><span class="sxs-lookup"><span data-stu-id="b89d0-182">If you have not done so already, open hello file in your favorite editor and update hello following lines with your credentials.</span></span>

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

<span data-ttu-id="b89d0-183">Puede encontrar sus credenciales de cuenta de lote y el almacenamiento en la hoja de la cuenta de hello de cada servicio en hello [portal de Azure][azure_portal]:</span><span class="sxs-lookup"><span data-stu-id="b89d0-183">You can find your Batch and Storage account credentials within hello account blade of each service in hello [Azure portal][azure_portal]:</span></span>

<span data-ttu-id="b89d0-184">![Procesar por lotes las credenciales en el portal de hello][9]
![credenciales de almacenamiento en el portal de Hola][10]</span><span class="sxs-lookup"><span data-stu-id="b89d0-184">![Batch credentials in hello portal][9]
![Storage credentials in hello portal][10]</span></span><br/>

<span data-ttu-id="b89d0-185">En las secciones siguientes de hello, analizamos pasos Hola utilizado por hello scripts tooprocess una carga de trabajo en hello servicio por lotes.</span><span class="sxs-lookup"><span data-stu-id="b89d0-185">In hello following sections, we analyze hello steps used by hello scripts tooprocess a workload in hello Batch service.</span></span> <span data-ttu-id="b89d0-186">Le recomendamos que toorefer con regularidad toohello scripts en el editor mientras el equipo funcionan su camino a través del resto de Hola de artículo Hola.</span><span class="sxs-lookup"><span data-stu-id="b89d0-186">We encourage you toorefer regularly toohello scripts in your editor while you work your way through hello rest of hello article.</span></span>

<span data-ttu-id="b89d0-187">Navegue toohello después de la línea en **python_tutorial_client.py** toostart con el paso 1:</span><span class="sxs-lookup"><span data-stu-id="b89d0-187">Navigate toohello following line in **python_tutorial_client.py** toostart with Step 1:</span></span>

```python
if __name__ == '__main__':
```

## <a name="step-1-create-storage-containers"></a><span data-ttu-id="b89d0-188">Paso 1: Crear contenedores de Storage</span><span class="sxs-lookup"><span data-stu-id="b89d0-188">Step 1: Create Storage containers</span></span>
<span data-ttu-id="b89d0-189">![Crear contenedores en Azure Storage][1]
</span><span class="sxs-lookup"><span data-stu-id="b89d0-189">![Create containers in Azure Storage][1]
</span></span><br/>

<span data-ttu-id="b89d0-190">Batch incluye compatibilidad integrada para interactuar con Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="b89d0-190">Batch includes built-in support for interacting with Azure Storage.</span></span> <span data-ttu-id="b89d0-191">Contenedores en su cuenta de almacenamiento proporcionará los archivos de hello necesarios para las tareas de Hola que se ejecutan en su cuenta de lote.</span><span class="sxs-lookup"><span data-stu-id="b89d0-191">Containers in your Storage account will provide hello files needed by hello tasks that run in your Batch account.</span></span> <span data-ttu-id="b89d0-192">los contenedores de Hello también proporcionan un colocar toostore Hola salida los datos que producen las tareas de Hola.</span><span class="sxs-lookup"><span data-stu-id="b89d0-192">hello containers also provide a place toostore hello output data that hello tasks produce.</span></span> <span data-ttu-id="b89d0-193">lo primero que Hola Hola *python_tutorial_client.py* script hace es crear tres contenedores en [almacenamiento de blobs de Azure](../storage/common/storage-introduction.md#blob-storage):</span><span class="sxs-lookup"><span data-stu-id="b89d0-193">hello first thing hello *python_tutorial_client.py* script does is create three containers in [Azure Blob Storage](../storage/common/storage-introduction.md#blob-storage):</span></span>

* <span data-ttu-id="b89d0-194">**aplicación**: este contenedor almacenará script de Python Hola ejecutar las tareas de hello, *python_tutorial_task.py*.</span><span class="sxs-lookup"><span data-stu-id="b89d0-194">**application**: This container will store hello Python script run by hello tasks, *python_tutorial_task.py*.</span></span>
* <span data-ttu-id="b89d0-195">**entrada**: tareas descargará tooprocess de archivos de datos de Hola de hello *entrada* contenedor.</span><span class="sxs-lookup"><span data-stu-id="b89d0-195">**input**: Tasks will download hello data files tooprocess from hello *input* container.</span></span>
* <span data-ttu-id="b89d0-196">**salida**: cuando completen de tareas de procesamiento del archivo de entrada, cargará Hola resultados toohello *salida* contenedor.</span><span class="sxs-lookup"><span data-stu-id="b89d0-196">**output**: When tasks complete input file processing, they will upload hello results toohello *output* container.</span></span>

<span data-ttu-id="b89d0-197">En orden toointeract con un almacenamiento de información de la cuenta y crear contenedores, usamos hello [almacenamiento de azure] [ pypi_storage] paquete toocreate una [BlockBlobService] [ py_blockblobservice] objeto: Hola ""blob cliente.</span><span class="sxs-lookup"><span data-stu-id="b89d0-197">In order toointeract with a Storage account and create containers, we use hello [azure-storage][pypi_storage] package toocreate a [BlockBlobService][py_blockblobservice] object--hello "blob client."</span></span> <span data-ttu-id="b89d0-198">A continuación, crearemos tres contenedores en la cuenta de almacenamiento de hello con cliente de blob de Hola.</span><span class="sxs-lookup"><span data-stu-id="b89d0-198">We then create three containers in hello Storage account using hello blob client.</span></span>

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

<span data-ttu-id="b89d0-199">Una vez que se han creado los contenedores de hello, aplicación hello ahora puede cargar archivos de Hola que se usará en las tareas de Hola.</span><span class="sxs-lookup"><span data-stu-id="b89d0-199">Once hello containers have been created, hello application can now upload hello files that will be used by hello tasks.</span></span>

> [!TIP]
> <span data-ttu-id="b89d0-200">[¿Cómo toouse almacenamiento de blobs de Azure de Python](../storage/blobs/storage-python-how-to-use-blob-storage.md) proporciona una buena información general sobre cómo trabajar con contenedores de almacenamiento de Azure y los blobs.</span><span class="sxs-lookup"><span data-stu-id="b89d0-200">[How toouse Azure Blob storage from Python](../storage/blobs/storage-python-how-to-use-blob-storage.md) provides a good overview of working with Azure Storage containers and blobs.</span></span> <span data-ttu-id="b89d0-201">Debe ser cerca de la parte superior de saludo de la lista de lectura como comienza a trabajar con el lote.</span><span class="sxs-lookup"><span data-stu-id="b89d0-201">It should be near hello top of your reading list as you start working with Batch.</span></span>
>
>

## <a name="step-2-upload-task-script-and-data-files"></a><span data-ttu-id="b89d0-202">Paso 2: Cargar un script de tarea y archivos de entrada</span><span class="sxs-lookup"><span data-stu-id="b89d0-202">Step 2: Upload task script and data files</span></span>
<span data-ttu-id="b89d0-203">![Toocontainers de archivos de la tarea de carga de aplicación y entrada (datos)][2]
</span><span class="sxs-lookup"><span data-stu-id="b89d0-203">![Upload task application and input (data) files toocontainers][2]
</span></span><br/>

<span data-ttu-id="b89d0-204">En el archivo hello cargar el operación, *python_tutorial_client.py* define en primer lugar las colecciones de **aplicación** y **entrada** las rutas de acceso de archivo tal como aparecen en la máquina local Hola.</span><span class="sxs-lookup"><span data-stu-id="b89d0-204">In hello file upload operation, *python_tutorial_client.py* first defines collections of **application** and **input** file paths as they exist on hello local machine.</span></span> <span data-ttu-id="b89d0-205">A continuación, se cargan estos contenedores de toohello de archivos que creó en el paso anterior de Hola.</span><span class="sxs-lookup"><span data-stu-id="b89d0-205">Then it uploads these files toohello containers that you created in hello previous step.</span></span>

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

<span data-ttu-id="b89d0-206">Mediante la comprensión de la lista, Hola `upload_file_to_container` función se llama para cada archivo de colecciones de Hola y dos [ResourceFile] [ py_resource_file] se rellenan las colecciones.</span><span class="sxs-lookup"><span data-stu-id="b89d0-206">Using list comprehension, hello `upload_file_to_container` function is called for each file in hello collections, and two [ResourceFile][py_resource_file] collections are populated.</span></span> <span data-ttu-id="b89d0-207">Hola `upload_file_to_container` función aparece a continuación:</span><span class="sxs-lookup"><span data-stu-id="b89d0-207">hello `upload_file_to_container` function appears below:</span></span>

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

### <a name="resourcefiles"></a><span data-ttu-id="b89d0-208">ResourceFiles</span><span class="sxs-lookup"><span data-stu-id="b89d0-208">ResourceFiles</span></span>
<span data-ttu-id="b89d0-209">A [ResourceFile] [ py_resource_file] proporciona el nodo de ejecución de tareas en el lote con el archivo de tooa de dirección URL de hello en el almacenamiento de Azure que está tooa descargado antes de que se ejecuta dicha tarea.</span><span class="sxs-lookup"><span data-stu-id="b89d0-209">A [ResourceFile][py_resource_file] provides tasks in Batch with hello URL tooa file in Azure Storage that is downloaded tooa compute node before that task is run.</span></span> <span data-ttu-id="b89d0-210">Hola [ResourceFile][py_resource_file]. **blob_source** propiedad especifica Hola de dirección URL completa del archivo hello tal como existe en el almacenamiento de Azure.</span><span class="sxs-lookup"><span data-stu-id="b89d0-210">hello [ResourceFile][py_resource_file].**blob_source** property specifies hello full URL of hello file as it exists in Azure Storage.</span></span> <span data-ttu-id="b89d0-211">dirección URL de Hello también puede incluir una firma de acceso compartido (SAS) que proporciona un acceso seguro toohello archivo.</span><span class="sxs-lookup"><span data-stu-id="b89d0-211">hello URL may also include a shared access signature (SAS) that provides secure access toohello file.</span></span> <span data-ttu-id="b89d0-212">La mayoría de los tipos de tareas de Lote contienen una propiedad *ResourceFiles* , que incluye:</span><span class="sxs-lookup"><span data-stu-id="b89d0-212">Most task types in Batch include a *ResourceFiles* property, including:</span></span>

* <span data-ttu-id="b89d0-213">[CloudTask][py_task]</span><span class="sxs-lookup"><span data-stu-id="b89d0-213">[CloudTask][py_task]</span></span>
* <span data-ttu-id="b89d0-214">[StartTask][py_starttask]</span><span class="sxs-lookup"><span data-stu-id="b89d0-214">[StartTask][py_starttask]</span></span>
* <span data-ttu-id="b89d0-215">[JobPreparationTask][py_jobpreptask]</span><span class="sxs-lookup"><span data-stu-id="b89d0-215">[JobPreparationTask][py_jobpreptask]</span></span>
* <span data-ttu-id="b89d0-216">[JobReleaseTask][py_jobreltask]</span><span class="sxs-lookup"><span data-stu-id="b89d0-216">[JobReleaseTask][py_jobreltask]</span></span>

<span data-ttu-id="b89d0-217">Este ejemplo no utiliza Hola JobPreparationTask o tipos de tareas de JobReleaseTask, pero puede obtener más información acerca de esto en [nodos de ejecución de las tareas de preparación y finalización del trabajo de ejecución en Azure Batch](batch-job-prep-release.md).</span><span class="sxs-lookup"><span data-stu-id="b89d0-217">This sample does not use hello JobPreparationTask or JobReleaseTask task types, but you can read more about them in [Run job preparation and completion tasks on Azure Batch compute nodes](batch-job-prep-release.md).</span></span>

### <a name="shared-access-signature-sas"></a><span data-ttu-id="b89d0-218">Firma de acceso compartido (SAS)</span><span class="sxs-lookup"><span data-stu-id="b89d0-218">Shared access signature (SAS)</span></span>
<span data-ttu-id="b89d0-219">Firmas de acceso compartido son cadenas que proporcionan un acceso seguro toocontainers y blobs en almacenamiento de Azure.</span><span class="sxs-lookup"><span data-stu-id="b89d0-219">Shared access signatures are strings that provide secure access toocontainers and blobs in Azure Storage.</span></span> <span data-ttu-id="b89d0-220">Hola *python_tutorial_client.py* secuencia de comandos utiliza ambos blob y contenedor de firmas de acceso compartido y muestra cómo tooobtain estos compartidos tener acceso a las cadenas de firmas de hello servicio de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="b89d0-220">hello *python_tutorial_client.py* script uses both blob and container shared access signatures, and demonstrates how tooobtain these shared access signature strings from hello Storage service.</span></span>

* <span data-ttu-id="b89d0-221">**Firmas de acceso compartido de BLOB**: usos de StartTask del grupo de Hola firmas de acceso compartido cuando descarga archivos de datos de secuencias de comandos y de entrada para la tarea de Hola desde el almacenamiento de objetos binarios (vea [paso 3](#step-3-create-batch-pool) a continuación).</span><span class="sxs-lookup"><span data-stu-id="b89d0-221">**Blob shared access signatures**: hello pool's StartTask uses blob shared access signatures when it downloads hello task script and input data files from Storage (see [Step #3](#step-3-create-batch-pool) below).</span></span> <span data-ttu-id="b89d0-222">Hola `upload_file_to_container` funcionando en *python_tutorial_client.py* contiene código de hello que obtiene la firma de acceso compartido de cada blob.</span><span class="sxs-lookup"><span data-stu-id="b89d0-222">hello `upload_file_to_container` function in *python_tutorial_client.py* contains hello code that obtains each blob's shared access signature.</span></span> <span data-ttu-id="b89d0-223">Lo hace mediante una llamada a [BlockBlobService.make_blob_url] [ py_make_blob_url] en el módulo de almacenamiento de Hola.</span><span class="sxs-lookup"><span data-stu-id="b89d0-223">It does so by calling [BlockBlobService.make_blob_url][py_make_blob_url] in hello Storage module.</span></span>
* <span data-ttu-id="b89d0-224">**Firma de acceso compartido del contenedor**: a medida que cada tarea finaliza su trabajo en el nodo de proceso de hello, que se carga su toohello del archivo de salida *salida* contenedor en el almacenamiento de Azure.</span><span class="sxs-lookup"><span data-stu-id="b89d0-224">**Container shared access signature**: As each task finishes its work on hello compute node, it uploads its output file toohello *output* container in Azure Storage.</span></span> <span data-ttu-id="b89d0-225">toodo por lo tanto, *python_tutorial_task.py* utilizan una firma de acceso compartido de contenedor que proporciona acceso de escritura toohello contenedor.</span><span class="sxs-lookup"><span data-stu-id="b89d0-225">toodo so, *python_tutorial_task.py* uses a container shared access signature that provides write access toohello container.</span></span> <span data-ttu-id="b89d0-226">Hola `get_container_sas_token` funcionando en *python_tutorial_client.py* Obtiene la firma de acceso compartido del contenedor de hello, que, a continuación, se pasa como una tarea de toohello de argumento de línea de comandos.</span><span class="sxs-lookup"><span data-stu-id="b89d0-226">hello `get_container_sas_token` function in *python_tutorial_client.py* obtains hello container's shared access signature, which is then passed as a command-line argument toohello tasks.</span></span> <span data-ttu-id="b89d0-227">Paso 5 de #, [trabajo de agregar tareas tooa](#step-5-add-tasks-to-job), se describe el uso de Hola de hello contenedor SAS.</span><span class="sxs-lookup"><span data-stu-id="b89d0-227">Step #5, [Add tasks tooa job](#step-5-add-tasks-to-job), discusses hello usage of hello container SAS.</span></span>

> [!TIP]
> <span data-ttu-id="b89d0-228">Desprotección serie de dos partes de hello en firmas de acceso compartido, [parte 1: modelo de descripción Hola SAS](../storage/common/storage-dotnet-shared-access-signature-part-1.md) y [parte 2: crear y utilizar una SAS con hello servicio Blob](../storage/blobs/storage-dotnet-shared-access-signature-part-2.md), toolearn más acerca de cómo proporcionar un acceso seguro toodata en su cuenta de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="b89d0-228">Check out hello two-part series on shared access signatures, [Part 1: Understanding hello SAS model](../storage/common/storage-dotnet-shared-access-signature-part-1.md) and [Part 2: Create and use a SAS with hello Blob service](../storage/blobs/storage-dotnet-shared-access-signature-part-2.md), toolearn more about providing secure access toodata in your Storage account.</span></span>
>
>

## <a name="step-3-create-batch-pool"></a><span data-ttu-id="b89d0-229">Paso 3: Crear el grupo de Batch</span><span class="sxs-lookup"><span data-stu-id="b89d0-229">Step 3: Create Batch pool</span></span>
<span data-ttu-id="b89d0-230">![Crear un grupo de Batch][3]
</span><span class="sxs-lookup"><span data-stu-id="b89d0-230">![Create a Batch pool][3]
</span></span><br/>

<span data-ttu-id="b89d0-231">Un **grupo** de Batch es una colección de nodos de proceso (máquinas virtuales) en los que Batch ejecuta tareas de un trabajo.</span><span class="sxs-lookup"><span data-stu-id="b89d0-231">A Batch **pool** is a collection of compute nodes (virtual machines) on which Batch executes a job's tasks.</span></span>

<span data-ttu-id="b89d0-232">Una vez que se carga Hola tarea script y datos de archivos toohello cuenta de almacenamiento, *python_tutorial_client.py* inicia su interacción con el servicio de lote de hello mediante el módulo de Python de lote de Hola.</span><span class="sxs-lookup"><span data-stu-id="b89d0-232">After it uploads hello task script and data files toohello Storage account, *python_tutorial_client.py* starts its interaction with hello Batch service by using hello Batch Python module.</span></span> <span data-ttu-id="b89d0-233">toodo por lo tanto, un [BatchServiceClient] [ py_batchserviceclient] se crea:</span><span class="sxs-lookup"><span data-stu-id="b89d0-233">toodo so, a [BatchServiceClient][py_batchserviceclient] is created:</span></span>

```python
# Create a Batch service client. We'll now be interacting with hello Batch
# service in addition tooStorage.
credentials = batchauth.SharedKeyCredentials(BATCH_ACCOUNT_NAME,
                                             BATCH_ACCOUNT_KEY)

batch_client = batch.BatchServiceClient(
    credentials,
    base_url=BATCH_ACCOUNT_URL)
```

<span data-ttu-id="b89d0-234">A continuación, se crea un grupo de nodos de proceso en la cuenta de lote con una llamada de hello demasiado`create_pool`.</span><span class="sxs-lookup"><span data-stu-id="b89d0-234">Next, a pool of compute nodes is created in hello Batch account with a call too`create_pool`.</span></span>

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

<span data-ttu-id="b89d0-235">Cuando se crea un grupo, defina un [PoolAddParameter] [ py_pooladdparam] que especifica varias propiedades para el grupo de hello:</span><span class="sxs-lookup"><span data-stu-id="b89d0-235">When you create a pool, you define a [PoolAddParameter][py_pooladdparam] that specifies several properties for hello pool:</span></span>

* <span data-ttu-id="b89d0-236">**Id. de** del grupo de hello (*identificador* : es necesario)</span><span class="sxs-lookup"><span data-stu-id="b89d0-236">**ID** of hello pool (*id* - required)</span></span><p/><span data-ttu-id="b89d0-237">Lo mismo que sucede con la mayoría de las entidades en Lote, el nuevo grupo debe tener un identificador único dentro de la cuenta de Lote.</span><span class="sxs-lookup"><span data-stu-id="b89d0-237">As with most entities in Batch, your new pool must have a unique ID within your Batch account.</span></span> <span data-ttu-id="b89d0-238">El código hace referencia a un grupo de toothis con su identificador, y sirve para identificar a grupo de hello en hello Azure [portal][azure_portal].</span><span class="sxs-lookup"><span data-stu-id="b89d0-238">Your code refers toothis pool using its ID, and it's how you identify hello pool in hello Azure [portal][azure_portal].</span></span>
* <span data-ttu-id="b89d0-239">**Número de nodos de proceso** (*target_dedicated*: necesario)</span><span class="sxs-lookup"><span data-stu-id="b89d0-239">**Number of compute nodes** (*target_dedicated* - required)</span></span><p/><span data-ttu-id="b89d0-240">Esta propiedad especifica el número de máquinas virtuales deben implementarse en el grupo de Hola.</span><span class="sxs-lookup"><span data-stu-id="b89d0-240">This property specifies how many VMs should be deployed in hello pool.</span></span> <span data-ttu-id="b89d0-241">Es importante toonote que todas las cuentas de lote tienen el valor predeterminado es **cuota** que límites Hola número de **núcleos** (y por lo tanto, los nodos de ejecución) en una cuenta de lote.</span><span class="sxs-lookup"><span data-stu-id="b89d0-241">It is important toonote that all Batch accounts have a default **quota** that limits hello number of **cores** (and thus, compute nodes) in a Batch account.</span></span> <span data-ttu-id="b89d0-242">Puede encontrar las cuotas predeterminadas de hello e instrucciones sobre cómo demasiado[aumentar una cuota](batch-quota-limit.md#increase-a-quota) (por ejemplo, el número máximo de Hola de núcleos de su cuenta de lote) en [las cuotas y límites de hello servicio Azure Batch](batch-quota-limit.md).</span><span class="sxs-lookup"><span data-stu-id="b89d0-242">You can find hello default quotas and instructions on how too[increase a quota](batch-quota-limit.md#increase-a-quota) (such as hello maximum number of cores in your Batch account) in [Quotas and limits for hello Azure Batch service](batch-quota-limit.md).</span></span> <span data-ttu-id="b89d0-243">Si se pregunta "¿Por qué mi grupo no llega a más de X nodos?",</span><span class="sxs-lookup"><span data-stu-id="b89d0-243">If you find yourself asking "Why won't my pool reach more than X nodes?"</span></span> <span data-ttu-id="b89d0-244">Esta cuota básica puede ser la causa de Hola.</span><span class="sxs-lookup"><span data-stu-id="b89d0-244">this core quota may be hello cause.</span></span>
* <span data-ttu-id="b89d0-245">**Sistema operativo** para los nodos (*virtual_machine_configuration***o***cloud_service_configuration*: necesario)</span><span class="sxs-lookup"><span data-stu-id="b89d0-245">**Operating system** for nodes (*virtual_machine_configuration* **or** *cloud_service_configuration* - required)</span></span><p/><span data-ttu-id="b89d0-246">En *python_tutorial_client.py*, se crea un grupo de nodos de Linux con [VirtualMachineConfiguration][py_vm_config].</span><span class="sxs-lookup"><span data-stu-id="b89d0-246">In *python_tutorial_client.py*, we create a pool of Linux nodes using a [VirtualMachineConfiguration][py_vm_config].</span></span> <span data-ttu-id="b89d0-247">Hola `select_latest_verified_vm_image_with_node_agent_sku` funcionando en `common.helpers` simplifica el trabajo con [máquinas virtuales de Azure Marketplace] [ vm_marketplace] imágenes.</span><span class="sxs-lookup"><span data-stu-id="b89d0-247">hello `select_latest_verified_vm_image_with_node_agent_sku` function in `common.helpers` simplifies working with [Azure Virtual Machines Marketplace][vm_marketplace] images.</span></span> <span data-ttu-id="b89d0-248">Para más información acerca del uso de imágenes de Marketplace, consulte [Aprovisionamiento de nodos de proceso de Linux en grupos del servicio Azure Batch](batch-linux-nodes.md) .</span><span class="sxs-lookup"><span data-stu-id="b89d0-248">See [Provision Linux compute nodes in Azure Batch pools](batch-linux-nodes.md) for more information about using Marketplace images.</span></span>
* <span data-ttu-id="b89d0-249">**Tamaño de los nodos de proceso** (*vm_size*: necesario)</span><span class="sxs-lookup"><span data-stu-id="b89d0-249">**Size of compute nodes** (*vm_size* - required)</span></span><p/><span data-ttu-id="b89d0-250">Dado que especificamos nodos de Linux para nuestra instancia de [VirtualMachineConfiguration][py_vm_config], especificamos también un tamaño de máquina virtual (`STANDARD_A1` en este ejemplo) de los que aparecen en [Tamaños de las máquinas virtuales Linux en Azure](../virtual-machines/linux/sizes.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="b89d0-250">Since we're specifying Linux nodes for our [VirtualMachineConfiguration][py_vm_config], we specify a VM size (`STANDARD_A1` in this sample) from [Sizes for virtual machines in Azure](../virtual-machines/linux/sizes.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span> <span data-ttu-id="b89d0-251">Para más información, vuelva a consultar [Aprovisionamiento de nodos de proceso de Linux en grupos del servicio Lote de Azure](batch-linux-nodes.md) .</span><span class="sxs-lookup"><span data-stu-id="b89d0-251">Again, see [Provision Linux compute nodes in Azure Batch pools](batch-linux-nodes.md) for more information.</span></span>
* <span data-ttu-id="b89d0-252">**Tarea de inicio** (*start_task*: no necesario)</span><span class="sxs-lookup"><span data-stu-id="b89d0-252">**Start task** (*start_task* - not required)</span></span><p/><span data-ttu-id="b89d0-253">Junto con hello por encima de las propiedades de nodo físico, también puede especificar un [StartTask] [ py_starttask] para grupo de hello (no es necesario).</span><span class="sxs-lookup"><span data-stu-id="b89d0-253">Along with hello above physical node properties, you may also specify a [StartTask][py_starttask] for hello pool (it is not required).</span></span> <span data-ttu-id="b89d0-254">Hola StartTask se ejecuta en cada nodo según ese nodo une a grupo de Hola y cada vez que se reinicie un nodo.</span><span class="sxs-lookup"><span data-stu-id="b89d0-254">hello StartTask executes on each node as that node joins hello pool, and each time a node is restarted.</span></span> <span data-ttu-id="b89d0-255">Hola StartTask resulta especialmente útil para preparar los nodos de proceso para la ejecución de Hola de tareas, como la instalación de aplicaciones de Hola que se ejecutan las tareas.</span><span class="sxs-lookup"><span data-stu-id="b89d0-255">hello StartTask is especially useful for preparing compute nodes for hello execution of tasks, such as installing hello applications that your tasks run.</span></span><p/><span data-ttu-id="b89d0-256">En esta aplicación de ejemplo Hola StartTask copia los archivos de Hola que descarga desde el almacenamiento (que se especifican mediante el uso de hello StartTask **resource_files** propiedad) de hello StartTask *deldirectoriodetrabajo* toohello *compartido* directorio que pueden tener acceso todas las tareas que se ejecutan en el nodo de Hola.</span><span class="sxs-lookup"><span data-stu-id="b89d0-256">In this sample application, hello StartTask copies hello files that it downloads from Storage (which are specified by using hello StartTask's **resource_files** property) from hello StartTask *working directory* toohello *shared* directory that all tasks running on hello node can access.</span></span> <span data-ttu-id="b89d0-257">Básicamente, se copian `python_tutorial_task.py` toohello directorio compartido en cada nodo como nodo de Hola une a grupo de hello, para que las tareas que se ejecutan en el nodo de hello pueden tener acceso a él.</span><span class="sxs-lookup"><span data-stu-id="b89d0-257">Essentially, this copies `python_tutorial_task.py` toohello shared directory on each node as hello node joins hello pool, so that any tasks that run on hello node can access it.</span></span>

<span data-ttu-id="b89d0-258">Puede que observe Hola llamada toohello `wrap_commands_in_shell` función auxiliar.</span><span class="sxs-lookup"><span data-stu-id="b89d0-258">You may notice hello call toohello `wrap_commands_in_shell` helper function.</span></span> <span data-ttu-id="b89d0-259">Esta función toma una colección de comandos independientes y crea una línea de comandos adecuada para la propiedad de la línea de comandos de la tarea.</span><span class="sxs-lookup"><span data-stu-id="b89d0-259">This function takes a collection of separate commands and creates a single command line appropriate for a task's command-line property.</span></span>

<span data-ttu-id="b89d0-260">También importantes en el fragmento de código de hello anterior es el uso de Hola de dos variables de entorno de hello **command_line** propiedad de hello StartTask: `AZ_BATCH_TASK_WORKING_DIR` y `AZ_BATCH_NODE_SHARED_DIR`.</span><span class="sxs-lookup"><span data-stu-id="b89d0-260">Also notable in hello code snippet above is hello use of two environment variables in hello **command_line** property of hello StartTask: `AZ_BATCH_TASK_WORKING_DIR` and `AZ_BATCH_NODE_SHARED_DIR`.</span></span> <span data-ttu-id="b89d0-261">Cada nodo de ejecución dentro de un grupo de proceso por lotes se configura automáticamente con varias variables de entorno que están tooBatch específico.</span><span class="sxs-lookup"><span data-stu-id="b89d0-261">Each compute node within a Batch pool is automatically configured with several environment variables that are specific tooBatch.</span></span> <span data-ttu-id="b89d0-262">Cualquier proceso que se ejecuta una tarea tiene acceso a variables de entorno de toothese.</span><span class="sxs-lookup"><span data-stu-id="b89d0-262">Any process that is executed by a task has access toothese environment variables.</span></span>

> [!TIP]
> <span data-ttu-id="b89d0-263">toofind más información sobre las variables de entorno de Hola que están disponibles en los nodos de proceso en un grupo de lote, así como información de directorios de trabajo de tarea, consulte **configuración del entorno para tareas** y **archivos y directorios**  en hello [información general de las características de Azure Batch](batch-api-basics.md).</span><span class="sxs-lookup"><span data-stu-id="b89d0-263">toofind out more about hello environment variables that are available on compute nodes in a Batch pool, as well as information on task working directories, see **Environment settings for tasks** and **Files and directories** in hello [overview of Azure Batch features](batch-api-basics.md).</span></span>
>
>

## <a name="step-4-create-batch-job"></a><span data-ttu-id="b89d0-264">Paso 4: Crear el trabajo de Batch</span><span class="sxs-lookup"><span data-stu-id="b89d0-264">Step 4: Create Batch job</span></span>
<span data-ttu-id="b89d0-265">![Crear un trabajo de Batch][4]</span><span class="sxs-lookup"><span data-stu-id="b89d0-265">![Create Batch job][4]</span></span><br/>

<span data-ttu-id="b89d0-266">Un **trabajo** de Batch es una colección de tareas y está asociado a un grupo de nodos de proceso.</span><span class="sxs-lookup"><span data-stu-id="b89d0-266">A Batch **job** is a collection of tasks, and is associated with a pool of compute nodes.</span></span> <span data-ttu-id="b89d0-267">las tareas de Hello en un trabajo que se ejecutan en nodos de proceso del grupo de hello asociado.</span><span class="sxs-lookup"><span data-stu-id="b89d0-267">hello tasks in a job execute on hello associated pool's compute nodes.</span></span>

<span data-ttu-id="b89d0-268">Puede usar un trabajo no solo para organizar y seguimiento de las tareas en las cargas de trabajo relacionados, sino también para imponer ciertas restricciones, como el tiempo de ejecución máximo de hello para el trabajo de hello (y por extensión, sus tareas) y prioridad de trabajo en los trabajos de relación tooother en Hola cuenta de lote.</span><span class="sxs-lookup"><span data-stu-id="b89d0-268">You can use a job not only for organizing and tracking tasks in related workloads, but also for imposing certain constraints--such as hello maximum runtime for hello job (and by extension, its tasks) and job priority in relation tooother jobs in hello Batch account.</span></span> <span data-ttu-id="b89d0-269">Sin embargo, en este ejemplo, el trabajo de Hola se asocia únicamente a grupo Hola que creó en el paso 3 de #.</span><span class="sxs-lookup"><span data-stu-id="b89d0-269">In this example, however, hello job is associated only with hello pool that was created in step #3.</span></span> <span data-ttu-id="b89d0-270">No hay propiedades adicionales configuradas.</span><span class="sxs-lookup"><span data-stu-id="b89d0-270">No additional properties are configured.</span></span>

<span data-ttu-id="b89d0-271">Todos los trabajos de Batch están asociados a un grupo específico.</span><span class="sxs-lookup"><span data-stu-id="b89d0-271">All Batch jobs are associated with a specific pool.</span></span> <span data-ttu-id="b89d0-272">Esta asociación indica qué nodos que ejecutan tareas del trabajo de hello en.</span><span class="sxs-lookup"><span data-stu-id="b89d0-272">This association indicates which nodes hello job's tasks execute on.</span></span> <span data-ttu-id="b89d0-273">Especificar el grupo de hello mediante hello [PoolInformation] [ py_poolinfo] propiedad, como se muestra en el siguiente fragmento de código de hello.</span><span class="sxs-lookup"><span data-stu-id="b89d0-273">You specify hello pool by using hello [PoolInformation][py_poolinfo] property, as shown in hello code snippet below.</span></span>

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

<span data-ttu-id="b89d0-274">Ahora que se ha creado un trabajo, las tareas se agregan trabajo de hello tooperform.</span><span class="sxs-lookup"><span data-stu-id="b89d0-274">Now that a job has been created, tasks are added tooperform hello work.</span></span>

## <a name="step-5-add-tasks-toojob"></a><span data-ttu-id="b89d0-275">Paso 5: Agregar toojob de tareas</span><span class="sxs-lookup"><span data-stu-id="b89d0-275">Step 5: Add tasks toojob</span></span>
<span data-ttu-id="b89d0-276">![Agregar tareas toojob][5]</span><span class="sxs-lookup"><span data-stu-id="b89d0-276">![Add tasks toojob][5]</span></span><br/><span data-ttu-id="b89d0-277">
*(1) tareas se agregan toohello trabajo, tareas de hello (2) son toorun programada en nodos y tareas (3) Hola descargar tooprocess de archivos de datos de Hola*</span><span class="sxs-lookup"><span data-stu-id="b89d0-277">
*(1) Tasks are added toohello job, (2) hello tasks are scheduled toorun on nodes, and (3) hello tasks download hello data files tooprocess*</span></span>

<span data-ttu-id="b89d0-278">Lote **tareas** son nodos de proceso de hello unidades de trabajo que se ejecutan en Hola.</span><span class="sxs-lookup"><span data-stu-id="b89d0-278">Batch **tasks** are hello individual units of work that execute on hello compute nodes.</span></span> <span data-ttu-id="b89d0-279">Una tarea tiene una línea de comandos y ejecuta scripts de Hola o archivos ejecutables que especifique en esa línea de comandos.</span><span class="sxs-lookup"><span data-stu-id="b89d0-279">A task has a command line and runs hello scripts or executables that you specify in that command line.</span></span>

<span data-ttu-id="b89d0-280">tooactually realizar el trabajo, se deben agregar tareas tooa trabajo.</span><span class="sxs-lookup"><span data-stu-id="b89d0-280">tooactually perform work, tasks must be added tooa job.</span></span> <span data-ttu-id="b89d0-281">Cada [CloudTask] [ py_task] se configura con una propiedad de línea de comandos y [ResourceFiles] [ py_resource_file] (al igual que con StartTask del grupo de Hola) que Hola tarea de descarga toohello nodo antes de su línea de comandos se ejecuta automáticamente.</span><span class="sxs-lookup"><span data-stu-id="b89d0-281">Each [CloudTask][py_task] is configured with a command-line property and [ResourceFiles][py_resource_file] (as with hello pool's StartTask) that hello task downloads toohello node before its command line is automatically executed.</span></span> <span data-ttu-id="b89d0-282">En el ejemplo de Hola, cada tarea procesa un solo archivo.</span><span class="sxs-lookup"><span data-stu-id="b89d0-282">In hello sample, each task processes only one file.</span></span> <span data-ttu-id="b89d0-283">Por lo tanto, su colección ResourceFiles contiene un único elemento.</span><span class="sxs-lookup"><span data-stu-id="b89d0-283">Thus, its ResourceFiles collection contains a single element.</span></span>

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
> <span data-ttu-id="b89d0-284">Cuando tengan acceso a las variables de entorno como `$AZ_BATCH_NODE_SHARED_DIR` o ejecutar una aplicación no se encuentra en el nodo de hello `PATH`, líneas de comandos de la tarea debe invocar Hola shell explícitamente, como con `/bin/sh -c MyTaskApplication $MY_ENV_VAR`.</span><span class="sxs-lookup"><span data-stu-id="b89d0-284">When they access environment variables such as `$AZ_BATCH_NODE_SHARED_DIR` or execute an application not found in hello node's `PATH`, task command lines must invoke hello shell explicitly, such as with `/bin/sh -c MyTaskApplication $MY_ENV_VAR`.</span></span> <span data-ttu-id="b89d0-285">Este requisito no es necesario si las tareas ejecutan una aplicación en el nodo de hello `PATH` y no hacen referencia a las variables de entorno.</span><span class="sxs-lookup"><span data-stu-id="b89d0-285">This requirement is unnecessary if your tasks execute an application in hello node's `PATH` and do not reference any environment variables.</span></span>
>
>

<span data-ttu-id="b89d0-286">Dentro de hello `for` bucle en el fragmento de código de hello anterior, puede ver que la línea de comandos de hello para la tarea hello se construye con cinco argumentos de línea de comandos que se pasan demasiado*python_tutorial_task.py*:</span><span class="sxs-lookup"><span data-stu-id="b89d0-286">Within hello `for` loop in hello code snippet above, you can see that hello command line for hello task is constructed with five command-line arguments that are passed too*python_tutorial_task.py*:</span></span>

1. <span data-ttu-id="b89d0-287">**FilePath**: este es el archivo de toohello de ruta de acceso local de hello tal como existe en el nodo de Hola.</span><span class="sxs-lookup"><span data-stu-id="b89d0-287">**filepath**: This is hello local path toohello file as it exists on hello node.</span></span> <span data-ttu-id="b89d0-288">Hola al objeto ResourceFile en `upload_file_to_container` se creó en el paso 2 anterior, el nombre de archivo de Hola se usó para esta propiedad (hello `file_path` parámetro hello ResourceFile constructor).</span><span class="sxs-lookup"><span data-stu-id="b89d0-288">When hello ResourceFile object in `upload_file_to_container` was created in Step 2 above, hello file name was used for this property (hello `file_path` parameter in hello ResourceFile constructor).</span></span> <span data-ttu-id="b89d0-289">Esto indica que ese archivo hello puede encontrarse en hello mismo directorio en el nodo de hello como *python_tutorial_task.py*.</span><span class="sxs-lookup"><span data-stu-id="b89d0-289">This indicates that hello file can be found in hello same directory on hello node as *python_tutorial_task.py*.</span></span>
2. <span data-ttu-id="b89d0-290">**NUMWORDS**: parte superior de hello *N* palabras deberían escribir el archivo de salida de toohello.</span><span class="sxs-lookup"><span data-stu-id="b89d0-290">**numwords**: hello top *N* words should be written toohello output file.</span></span>
3. <span data-ttu-id="b89d0-291">**storageaccount**: nombre de Hola de hello cuenta de almacenamiento que posee el resultado de la tarea de hello contenedor toowhich Hola se debe cargar.</span><span class="sxs-lookup"><span data-stu-id="b89d0-291">**storageaccount**: hello name of hello Storage account that owns hello container toowhich hello task output should be uploaded.</span></span>
4. <span data-ttu-id="b89d0-292">**storagecontainer**: nombre de Hola de Hola Hola de toowhich de contenedor de almacenamiento se deben cargar los archivos de salida.</span><span class="sxs-lookup"><span data-stu-id="b89d0-292">**storagecontainer**: hello name of hello Storage container toowhich hello output files should be uploaded.</span></span>
5. <span data-ttu-id="b89d0-293">**sastoken**: firma de acceso compartido (SAS) de Hola que proporciona acceso de escritura toohello **salida** contenedor en el almacenamiento de Azure.</span><span class="sxs-lookup"><span data-stu-id="b89d0-293">**sastoken**: hello shared access signature (SAS) that provides write access toohello **output** container in Azure Storage.</span></span> <span data-ttu-id="b89d0-294">Hola *python_tutorial_task.py* secuencia de comandos utiliza esta firma de acceso compartido cuando se crea su referencia BlockBlobService.</span><span class="sxs-lookup"><span data-stu-id="b89d0-294">hello *python_tutorial_task.py* script uses this shared access signature when creates its BlockBlobService reference.</span></span> <span data-ttu-id="b89d0-295">Esto proporciona acceso de escritura toohello contenedor sin necesidad de una clave de acceso para la cuenta de almacenamiento de Hola.</span><span class="sxs-lookup"><span data-stu-id="b89d0-295">This provides write access toohello container without requiring an access key for hello storage account.</span></span>

```python
# NOTE: Taken from python_tutorial_task.py

# Create hello blob client using hello container's SAS token.
# This allows us toocreate a client that provides write
# access only toohello container.
blob_client = azureblob.BlockBlobService(account_name=args.storageaccount,
                                         sas_token=args.sastoken)
```

## <a name="step-6-monitor-tasks"></a><span data-ttu-id="b89d0-296">Paso 6: Supervisar tareas</span><span class="sxs-lookup"><span data-stu-id="b89d0-296">Step 6: Monitor tasks</span></span>
<span data-ttu-id="b89d0-297">![Supervisar tareas][6]</span><span class="sxs-lookup"><span data-stu-id="b89d0-297">![Monitor tasks][6]</span></span><br/><span data-ttu-id="b89d0-298">
*Hola crear scripts para tareas hello (1) los monitores de estado de finalización y tareas (2) Hola cargar tooAzure de datos de resultado almacenamiento*</span><span class="sxs-lookup"><span data-stu-id="b89d0-298">
*hello script (1) monitors hello tasks for completion status, and (2) hello tasks upload result data tooAzure Storage*</span></span>

<span data-ttu-id="b89d0-299">Cuando las tareas se agregan trabajo tooa, están en cola y programadas para ejecutarse en nodos de ejecución dentro del bloque de hello asociado al trabajo de Hola automáticamente.</span><span class="sxs-lookup"><span data-stu-id="b89d0-299">When tasks are added tooa job, they are automatically queued and scheduled for execution on compute nodes within hello pool associated with hello job.</span></span> <span data-ttu-id="b89d0-300">En función de la configuración de Hola que especifique, por lotes controla Queue de todas las tareas, programación, Reintentar y otras tareas de administración de la tarea de.</span><span class="sxs-lookup"><span data-stu-id="b89d0-300">Based on hello settings you specify, Batch handles all task queuing, scheduling, retrying, and other task administration duties for you.</span></span>

<span data-ttu-id="b89d0-301">Existen muchos enfoques de ejecución de la tarea de toomonitoring.</span><span class="sxs-lookup"><span data-stu-id="b89d0-301">There are many approaches toomonitoring task execution.</span></span> <span data-ttu-id="b89d0-302">Hola `wait_for_tasks_to_complete` funcionando en *python_tutorial_client.py* proporciona un ejemplo sencillo de tareas de supervisión para un estado determinado, en este caso, hello [completado] [ py_taskstate] estado.</span><span class="sxs-lookup"><span data-stu-id="b89d0-302">hello `wait_for_tasks_to_complete` function in *python_tutorial_client.py* provides a simple example of monitoring tasks for a certain state, in this case, hello [completed][py_taskstate] state.</span></span>

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

## <a name="step-7-download-task-output"></a><span data-ttu-id="b89d0-303">Paso 7: Descargar el resultado de la tarea</span><span class="sxs-lookup"><span data-stu-id="b89d0-303">Step 7: Download task output</span></span>
<span data-ttu-id="b89d0-304">![Descargar el resultado de la tarea de Storage][7]</span><span class="sxs-lookup"><span data-stu-id="b89d0-304">![Download task output from Storage][7]</span></span><br/>

<span data-ttu-id="b89d0-305">Ahora que hello trabajo se completa, resultado de hello de las tareas de hello puede descargarse desde el almacenamiento de Azure.</span><span class="sxs-lookup"><span data-stu-id="b89d0-305">Now that hello job is completed, hello output from hello tasks can be downloaded from Azure Storage.</span></span> <span data-ttu-id="b89d0-306">Esto se realiza con una llamada demasiado`download_blobs_from_container` en *python_tutorial_client.py*:</span><span class="sxs-lookup"><span data-stu-id="b89d0-306">This is done with a call too`download_blobs_from_container` in *python_tutorial_client.py*:</span></span>

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
> <span data-ttu-id="b89d0-307">Hola llamada demasiado`download_blobs_from_container` en *python_tutorial_client.py* especifica que los archivos de hello deben ser directorio particular tooyour descargado.</span><span class="sxs-lookup"><span data-stu-id="b89d0-307">hello call too`download_blobs_from_container` in *python_tutorial_client.py* specifies that hello files should be downloaded tooyour home directory.</span></span> <span data-ttu-id="b89d0-308">Cree toomodify libre esta ubicación de salida.</span><span class="sxs-lookup"><span data-stu-id="b89d0-308">Feel free toomodify this output location.</span></span>
>
>

## <a name="step-8-delete-containers"></a><span data-ttu-id="b89d0-309">Paso 8: Eliminar contenedores</span><span class="sxs-lookup"><span data-stu-id="b89d0-309">Step 8: Delete containers</span></span>
<span data-ttu-id="b89d0-310">Dado que se le cobrará por datos que residen en el almacenamiento de Azure, siempre es un tooremove buena idea los blobs que no tengan más necesarios para los trabajos por lotes.</span><span class="sxs-lookup"><span data-stu-id="b89d0-310">Because you are charged for data that resides in Azure Storage, it is always a good idea tooremove any blobs that are no longer needed for your Batch jobs.</span></span> <span data-ttu-id="b89d0-311">En *python_tutorial_client.py*, esto se realiza con tres llamadas demasiado[BlockBlobService.delete_container][py_delete_container]:</span><span class="sxs-lookup"><span data-stu-id="b89d0-311">In *python_tutorial_client.py*, this is done with three calls too[BlockBlobService.delete_container][py_delete_container]:</span></span>

```python
# Clean up storage resources
print('Deleting containers...')
blob_client.delete_container(app_container_name)
blob_client.delete_container(input_container_name)
blob_client.delete_container(output_container_name)
```

## <a name="step-9-delete-hello-job-and-hello-pool"></a><span data-ttu-id="b89d0-312">Paso 9: Eliminar trabajo hello y grupo de Hola</span><span class="sxs-lookup"><span data-stu-id="b89d0-312">Step 9: Delete hello job and hello pool</span></span>
<span data-ttu-id="b89d0-313">En el paso final de hello, es toodelete solicitadas Hola hello y trabajo de grupo creados por hello *python_tutorial_client.py* secuencia de comandos.</span><span class="sxs-lookup"><span data-stu-id="b89d0-313">In hello final step, you are prompted toodelete hello job and hello pool that were created by hello *python_tutorial_client.py* script.</span></span> <span data-ttu-id="b89d0-314">Aunque no se cobran los trabajos y tareas, *sí* se cobran los nodos de proceso.</span><span class="sxs-lookup"><span data-stu-id="b89d0-314">Although you are not charged for jobs and tasks themselves, you *are* charged for compute nodes.</span></span> <span data-ttu-id="b89d0-315">Por consiguiente, se recomienda asignar solo los nodos necesarios.</span><span class="sxs-lookup"><span data-stu-id="b89d0-315">Thus, we recommend that you allocate nodes only as needed.</span></span> <span data-ttu-id="b89d0-316">La eliminación de los grupos que no se usen puede formar parte del proceso de mantenimiento.</span><span class="sxs-lookup"><span data-stu-id="b89d0-316">Deleting unused pools can be part of your maintenance process.</span></span>

<span data-ttu-id="b89d0-317">Hola BatchServiceClient [JobOperations] [ py_job] y [PoolOperations] [ py_pool] tienen métodos de eliminación correspondientes, que son se llama si Confirmar eliminación:</span><span class="sxs-lookup"><span data-stu-id="b89d0-317">hello BatchServiceClient's [JobOperations][py_job] and [PoolOperations][py_pool] both have corresponding deletion methods, which are called if you confirm deletion:</span></span>

```python
# Clean up Batch resources (if hello user so chooses).
if query_yes_no('Delete job?') == 'yes':
    batch_client.job.delete(_JOB_ID)

if query_yes_no('Delete pool?') == 'yes':
    batch_client.pool.delete(_POOL_ID)
```

> [!IMPORTANT]
> <span data-ttu-id="b89d0-318">Tenga en cuenta que los recursos de proceso se cobran (la eliminación de grupos sin usar reducirá el costo).</span><span class="sxs-lookup"><span data-stu-id="b89d0-318">Keep in mind that you are charged for compute resources--deleting unused pools will minimize cost.</span></span> <span data-ttu-id="b89d0-319">Además, tenga en cuenta que al eliminar un grupo eliminan todos los nodos de proceso dentro de ese grupo y que todos los datos de los nodos de hello serán irrecuperables después de elimina el grupo de Hola.</span><span class="sxs-lookup"><span data-stu-id="b89d0-319">Also, be aware that deleting a pool deletes all compute nodes within that pool, and that any data on hello nodes will be unrecoverable after hello pool is deleted.</span></span>
>
>

## <a name="run-hello-sample-script"></a><span data-ttu-id="b89d0-320">Ejecutar script de ejemplo de Hola</span><span class="sxs-lookup"><span data-stu-id="b89d0-320">Run hello sample script</span></span>
<span data-ttu-id="b89d0-321">Cuando ejecute hello *python_tutorial_client.py* secuencia de comandos de tutorial de hello [ejemplo de código][github_article_samples], salida de la consola de hello es similar siguiente de toohello.</span><span class="sxs-lookup"><span data-stu-id="b89d0-321">When you run hello *python_tutorial_client.py* script from hello tutorial [code sample][github_article_samples], hello console output is similar toohello following.</span></span> <span data-ttu-id="b89d0-322">Hay una pausa en `Monitoring all tasks for 'Completed' state, timeout in 0:20:00...` mientras se crean nodos de proceso del grupo de hello, inicia, y se ejecutan comandos de hello en la tarea de inicio del grupo de Hola.</span><span class="sxs-lookup"><span data-stu-id="b89d0-322">There is a pause at `Monitoring all tasks for 'Completed' state, timeout in 0:20:00...` while hello pool's compute nodes are created, started, and hello commands in hello pool's start task are executed.</span></span> <span data-ttu-id="b89d0-323">Hola de uso [portal de Azure] [ azure_portal] toomonitor su grupo, nodos de proceso, trabajo y las tareas durante y después de la ejecución.</span><span class="sxs-lookup"><span data-stu-id="b89d0-323">Use hello [Azure portal][azure_portal] toomonitor your pool, compute nodes, job, and tasks during and after execution.</span></span> <span data-ttu-id="b89d0-324">Hola de uso [portal de Azure] [ azure_portal] o hello [Microsoft Azure Storage Explorer] [ storage_explorer] tooview los recursos de almacenamiento hello (contenedores y blobs) que se crean por aplicación hello.</span><span class="sxs-lookup"><span data-stu-id="b89d0-324">Use hello [Azure portal][azure_portal] or hello [Microsoft Azure Storage Explorer][storage_explorer] tooview hello Storage resources (containers and blobs) that are created by hello application.</span></span>

> [!TIP]
> <span data-ttu-id="b89d0-325">Ejecute hello *python_tutorial_client.py* script desde dentro de hello `azure-batch-samples/Python/Batch/article_samples` directory.</span><span class="sxs-lookup"><span data-stu-id="b89d0-325">Run hello *python_tutorial_client.py* script from within hello `azure-batch-samples/Python/Batch/article_samples` directory.</span></span> <span data-ttu-id="b89d0-326">Utiliza una ruta de acceso relativa para hello `common.helpers` importación del módulo, por lo que es posible que vea `ImportError: No module named 'common'` si no ejecuta el script de Hola desde dentro de este directorio.</span><span class="sxs-lookup"><span data-stu-id="b89d0-326">It uses a relative path for hello `common.helpers` module import, so you might see `ImportError: No module named 'common'` if you don't run hello script from within this directory.</span></span>
>
>

<span data-ttu-id="b89d0-327">Tiempo de ejecución típica es **aproximadamente 5-7 minutos** al ejecutar el ejemplo hello en su configuración predeterminada.</span><span class="sxs-lookup"><span data-stu-id="b89d0-327">Typical execution time is **approximately 5-7 minutes** when you run hello sample in its default configuration.</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="b89d0-328">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="b89d0-328">Next steps</span></span>
<span data-ttu-id="b89d0-329">Cree cambios toomake libre demasiado*python_tutorial_client.py* y *python_tutorial_task.py* tooexperiment con diferentes escenarios de proceso.</span><span class="sxs-lookup"><span data-stu-id="b89d0-329">Feel free toomake changes too*python_tutorial_client.py* and *python_tutorial_task.py* tooexperiment with different compute scenarios.</span></span> <span data-ttu-id="b89d0-330">Por ejemplo, intente agregar un retraso de ejecución demasiado*python_tutorial_task.py* toosimulate ejecución prolongada tareas y supervisarlos en el portal de Hola.</span><span class="sxs-lookup"><span data-stu-id="b89d0-330">For example, try adding an execution delay too*python_tutorial_task.py* toosimulate long-running tasks and monitor them in hello portal.</span></span> <span data-ttu-id="b89d0-331">Intente agregar más tareas o ajustar Hola número de nodos de cálculo.</span><span class="sxs-lookup"><span data-stu-id="b89d0-331">Try adding more tasks or adjusting hello number of compute nodes.</span></span> <span data-ttu-id="b89d0-332">Agregar lógica toocheck para y permitir el uso de Hola de un tiempo de ejecución de toospeed de grupo existente.</span><span class="sxs-lookup"><span data-stu-id="b89d0-332">Add logic toocheck for and allow hello use of an existing pool toospeed execution time.</span></span>

<span data-ttu-id="b89d0-333">Ahora que está familiarizado con un flujo de trabajo básico de Hola de una solución de lote, es hora toodig en toohello características adicionales de hello servicio por lotes.</span><span class="sxs-lookup"><span data-stu-id="b89d0-333">Now that you're familiar with hello basic workflow of a Batch solution, it's time toodig in toohello additional features of hello Batch service.</span></span>

* <span data-ttu-id="b89d0-334">Hola de revisión [características de información general de Azure Batch](batch-api-basics.md) artículo, que se recomienda si dispone de un nuevo servicio de toohello.</span><span class="sxs-lookup"><span data-stu-id="b89d0-334">Review hello [Overview of Azure Batch features](batch-api-basics.md) article, which we recommend if you're new toohello service.</span></span>
* <span data-ttu-id="b89d0-335">Inicio de Hola otros artículos de desarrollo de lote en **desarrollo detallada** en hello [ruta de acceso de aprendizaje por lotes][batch_learning_path].</span><span class="sxs-lookup"><span data-stu-id="b89d0-335">Start on hello other Batch development articles under **Development in-depth** in hello [Batch learning path][batch_learning_path].</span></span>
* <span data-ttu-id="b89d0-336">Extraer del repositorio una implementación diferente de procesamiento Hola "top N palabras" carga de trabajo con lote hello [TopNWords] [ github_topnwords] ejemplo.</span><span class="sxs-lookup"><span data-stu-id="b89d0-336">Check out a different implementation of processing hello "top N words" workload with Batch in hello [TopNWords][github_topnwords] sample.</span></span>

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
