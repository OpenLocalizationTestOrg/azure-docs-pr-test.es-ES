---
title: Hola aaaUsing 2.0 de CLI de Azure con el almacenamiento de Azure | Documentos de Microsoft
description: "Obtenga información acerca de cómo toouse Hola interfaz de línea de comandos de Azure (CLI de Azure) 2.0 con toocreate de almacenamiento de Azure y administrar cuentas de almacenamiento y trabajar con blobs de Azure y archivos. Hola CLI de Azure 2.0 es una herramienta de multiplataforma escrita en Python."
services: storage
documentationcenter: na
author: mmacy
manager: timlt
editor: tysonn
ms.assetid: 
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: azurecli
ms.topic: article
ms.date: 06/02/2017
ms.author: marsma
ms.openlocfilehash: 38402373dcd87f1ef05471a02353c77d58f1a9fe
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="using-hello-azure-cli-20-with-azure-storage"></a><span data-ttu-id="22b93-104">Uso de hello Azure CLI 2.0 con el almacenamiento de Azure</span><span class="sxs-lookup"><span data-stu-id="22b93-104">Using hello Azure CLI 2.0 with Azure Storage</span></span>

<span data-ttu-id="22b93-105">Hola código abierto, multiplataforma Azure CLI 2.0 proporciona un conjunto de comandos para trabajar con hello plataforma Windows Azure.</span><span class="sxs-lookup"><span data-stu-id="22b93-105">hello open-source, cross-platform Azure CLI 2.0 provides a set of commands for working with hello Azure platform.</span></span> <span data-ttu-id="22b93-106">Proporciona gran parte de la misma funcionalidad que se encuentra en Hola de Hola [portal de Azure](https://portal.azure.com), incluido el acceso de datos enriquecidos.</span><span class="sxs-lookup"><span data-stu-id="22b93-106">It provides much of hello same functionality found in hello [Azure portal](https://portal.azure.com), including rich data access.</span></span>

<span data-ttu-id="22b93-107">En esta guía, le mostramos cómo hello toouse [CLI de Azure 2.0](https://docs.microsoft.com/cli/azure/get-started-with-az-cli2) tooperform varias tareas trabajar con recursos de la cuenta de almacenamiento de Azure.</span><span class="sxs-lookup"><span data-stu-id="22b93-107">In this guide, we show you how toouse hello [Azure CLI 2.0](https://docs.microsoft.com/cli/azure/get-started-with-az-cli2) tooperform several tasks working with resources in your Azure Storage account.</span></span> <span data-ttu-id="22b93-108">Se recomienda descargar e instalar o actualizar toohello la versión más reciente de hello CLI 2.0 antes de utilizar a esta guía.</span><span class="sxs-lookup"><span data-stu-id="22b93-108">We recommend that you download and install or upgrade toohello latest version of hello CLI 2.0 before using this guide.</span></span>

<span data-ttu-id="22b93-109">ejemplos de Hello de guía de hello suponen el uso de Hola de hello shell de Bash en Ubuntu, pero otras plataformas deben realizar de forma similar.</span><span class="sxs-lookup"><span data-stu-id="22b93-109">hello examples in hello guide assume hello use of hello Bash shell on Ubuntu, but other platforms should perform similarly.</span></span> 

[!INCLUDE [storage-cli-versions](../../includes/storage-cli-versions.md)]

## <a name="prerequisites"></a><span data-ttu-id="22b93-110">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="22b93-110">Prerequisites</span></span>
<span data-ttu-id="22b93-111">Esta guía se da por supuesto que comprende los conceptos básicos de hello del almacenamiento de Azure.</span><span class="sxs-lookup"><span data-stu-id="22b93-111">This guide assumes that you understand hello basic concepts of Azure Storage.</span></span> <span data-ttu-id="22b93-112">También se da por supuesto que es capaz de toosatisfy Hola creación requisitos de las cuentas que se especifican a continuación para Azure y Hola servicio de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="22b93-112">It also assumes that you're able toosatisfy hello account creation requirements that are specified below for Azure and hello Storage service.</span></span>

### <a name="accounts"></a><span data-ttu-id="22b93-113">Cuentas</span><span class="sxs-lookup"><span data-stu-id="22b93-113">Accounts</span></span>
* <span data-ttu-id="22b93-114">**Cuenta de Azure**: si aún no tiene ninguna suscripción a Azure, [cree una cuenta gratuita de Azure](https://azure.microsoft.com/free/).</span><span class="sxs-lookup"><span data-stu-id="22b93-114">**Azure account**: If you don't already have an Azure subscription, [create a free Azure account](https://azure.microsoft.com/free/).</span></span>
* <span data-ttu-id="22b93-115">**Cuenta de almacenamiento**: consulte la sección [Crear una cuenta de almacenamiento](../storage/storage-create-storage-account.md#create-a-storage-account) del artículo [Acerca de las cuentas de almacenamiento de Azure](../storage/storage-create-storage-account.md).</span><span class="sxs-lookup"><span data-stu-id="22b93-115">**Storage account**: See [Create a storage account](../storage/storage-create-storage-account.md#create-a-storage-account) in [About Azure storage accounts](../storage/storage-create-storage-account.md).</span></span>

### <a name="install-hello-azure-cli-20"></a><span data-ttu-id="22b93-116">Instalar Hola 2.0 de CLI de Azure</span><span class="sxs-lookup"><span data-stu-id="22b93-116">Install hello Azure CLI 2.0</span></span>

<span data-ttu-id="22b93-117">Descargue e instale Hola 2.0 de CLI de Azure siguiendo las instrucciones de Hola que se describen en [instalar Azure CLI 2.0](/cli/azure/install-az-cli2).</span><span class="sxs-lookup"><span data-stu-id="22b93-117">Download and install hello Azure CLI 2.0 by following hello instructions outlined in [Install Azure CLI 2.0](/cli/azure/install-az-cli2).</span></span>

> [!TIP]
> <span data-ttu-id="22b93-118">Si tiene problemas con la instalación de hello, desproteger hello [solución de problemas de instalación](/cli/azure/install-az-cli2#installation-troubleshooting) sección del artículo de Hola y Hola [solución de problemas de instalación](https://github.com/Azure/azure-cli/blob/master/doc/install_troubleshooting.md) guía en GitHub.</span><span class="sxs-lookup"><span data-stu-id="22b93-118">If you have trouble with hello installation, check out hello [Installation Troubleshooting](/cli/azure/install-az-cli2#installation-troubleshooting) section of hello article, and hello [Install Troubleshooting](https://github.com/Azure/azure-cli/blob/master/doc/install_troubleshooting.md) guide on GitHub.</span></span>
>

## <a name="working-with-hello-cli"></a><span data-ttu-id="22b93-119">Trabajar con hello CLI</span><span class="sxs-lookup"><span data-stu-id="22b93-119">Working with hello CLI</span></span>

<span data-ttu-id="22b93-120">Una vez haya instalado Hola CLI, puede usar hello `az` comando en los comandos de CLI de Azure de interfaz de línea de comandos (intensiva de errores, Terminal, símbolo del sistema) tooaccess Hola.</span><span class="sxs-lookup"><span data-stu-id="22b93-120">Once you've installed hello CLI, you can use hello `az` command in your command-line interface (Bash, Terminal, Command Prompt) tooaccess hello Azure CLI commands.</span></span> <span data-ttu-id="22b93-121">Hola de tipo `az` comando toosee una lista completa de comandos de base de hello (se ha truncado la siguiente salida de ejemplo de Hola):</span><span class="sxs-lookup"><span data-stu-id="22b93-121">Type hello `az` command toosee a full list of hello base commands (hello following example output has been truncated):</span></span>

```
     /\
    /  \    _____   _ _ __ ___
   / /\ \  |_  / | | | \'__/ _ \
  / ____ \  / /| |_| | | |  __/
 /_/    \_\/___|\__,_|_|  \___|


Welcome toohello cool new Azure CLI!

Here are hello base commands:

    account          : Manage subscriptions.
    acr              : Manage Azure container registries.
    acs              : Manage Azure Container Services.
    ad               : Synchronize on-premises directories and manage Azure Active Directory
                       resources.
    ...
```

<span data-ttu-id="22b93-122">En la interfaz de línea de comandos, ejecute el comando de hello `az storage --help` hello toolist `storage` comando subgrupos.</span><span class="sxs-lookup"><span data-stu-id="22b93-122">In your command-line interface, execute hello command `az storage --help` toolist hello `storage` command subgroups.</span></span> <span data-ttu-id="22b93-123">las descripciones de Hola de subgrupos de hello proporcionan una visión general de Hola Hola de funcionalidad que CLI de Azure proporciona para trabajar con los recursos de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="22b93-123">hello descriptions of hello subgroups provide an overview of hello functionality hello Azure CLI provides for working with your storage resources.</span></span>

```
Group
    az storage: Durable, highly available, and massively scalable cloud storage.

Subgroups:
    account  : Manage storage accounts.
    blob     : Object storage for unstructured data.
    container: Manage blob storage containers.
    cors     : Manage Storage service Cross-Origin Resource Sharing (CORS).
    directory: Manage file storage directories.
    entity   : Manage table storage entities.
    file     : File shares that use hello standard SMB 3.0 protocol.
    logging  : Manage Storage service logging information.
    message  : Manage queue storage messages.
    metrics  : Manage Storage service metrics.
    queue    : Use queues tooeffectively scale applications according tootraffic.
    share    : Manage file shares.
    table    : NoSQL key-value storage using semi-structured datasets.
```

## <a name="connect-hello-cli-tooyour-azure-subscription"></a><span data-ttu-id="22b93-124">Conectar Hola CLI tooyour suscripción de Azure</span><span class="sxs-lookup"><span data-stu-id="22b93-124">Connect hello CLI tooyour Azure subscription</span></span>

<span data-ttu-id="22b93-125">toowork con recursos de hello en su suscripción de Azure, primero debe iniciar sesión en tooyour cuenta de Azure con `az login`.</span><span class="sxs-lookup"><span data-stu-id="22b93-125">toowork with hello resources in your Azure subscription, you must first log in tooyour Azure account with `az login`.</span></span> <span data-ttu-id="22b93-126">Hay varias formas de iniciar sesión:</span><span class="sxs-lookup"><span data-stu-id="22b93-126">There are several ways you can log in:</span></span>

* <span data-ttu-id="22b93-127">**Inicio de sesión interactivo**: `az login`</span><span class="sxs-lookup"><span data-stu-id="22b93-127">**Interactive login**: `az login`</span></span>
* <span data-ttu-id="22b93-128">**Inicio de sesión con nombre de usuario y contraseña**: `az login -u johndoe@contoso.com -p VerySecret`</span><span class="sxs-lookup"><span data-stu-id="22b93-128">**Log in with user name and password**: `az login -u johndoe@contoso.com -p VerySecret`</span></span>
  * <span data-ttu-id="22b93-129">Esta opción no es compatible con cuentas de Microsoft o cuentas que usan autenticación multifactor.</span><span class="sxs-lookup"><span data-stu-id="22b93-129">This doesn't work with Microsoft accounts or accounts that use multi-factor authentication.</span></span>
* <span data-ttu-id="22b93-130">**Inicio de sesión con una entidad de servicio**: `az login --service-principal -u http://azure-cli-2016-08-05-14-31-15 -p VerySecret --tenant contoso.onmicrosoft.com`</span><span class="sxs-lookup"><span data-stu-id="22b93-130">**Log in with a service principal**: `az login --service-principal -u http://azure-cli-2016-08-05-14-31-15 -p VerySecret --tenant contoso.onmicrosoft.com`</span></span>

## <a name="azure-cli-20-sample-script"></a><span data-ttu-id="22b93-131">Script de ejemplo de CLI de Azure 2.0</span><span class="sxs-lookup"><span data-stu-id="22b93-131">Azure CLI 2.0 sample script</span></span>

<span data-ttu-id="22b93-132">A continuación, vamos a trabajar con una secuencia de comandos de shell pequeño que emite unos toointeract de comandos de CLI de Azure 2.0 básica con los recursos de almacenamiento de Azure.</span><span class="sxs-lookup"><span data-stu-id="22b93-132">Next, we'll work with a small shell script that issues a few basic Azure CLI 2.0 commands toointeract with Azure Storage resources.</span></span> <span data-ttu-id="22b93-133">script de Hola primero crea un nuevo contenedor en la cuenta de almacenamiento, a continuación, carga un contenedor de toothat de archivo (como un blob) existente.</span><span class="sxs-lookup"><span data-stu-id="22b93-133">hello script first creates a new container in your storage account, then uploads an existing file (as a blob) toothat container.</span></span> <span data-ttu-id="22b93-134">A continuación, enumera todos los blobs Hola contenedor y por último, descarga tooa destino de archivo de hello en el equipo local que especifique.</span><span class="sxs-lookup"><span data-stu-id="22b93-134">It then lists all blobs in hello container, and finally, downloads hello file tooa destination on your local computer that you specify.</span></span>

```bash
#!/bin/bash
# A simple Azure Storage example script

export AZURE_STORAGE_ACCOUNT=<storage_account_name>
export AZURE_STORAGE_ACCESS_KEY=<storage_account_key>

export container_name=<container_name>
export blob_name=<blob_name>
export file_to_upload=<file_to_upload>
export destination_file=<destination_file>

echo "Creating hello container..."
az storage container create --name $container_name

echo "Uploading hello file..."
az storage blob upload --container-name $container_name --file $file_to_upload --name $blob_name

echo "Listing hello blobs..."
az storage blob list --container-name $container_name --output table

echo "Downloading hello file..."
az storage blob download --container-name $container_name --name $blob_name --file $destination_file --output table

echo "Done"
```

<span data-ttu-id="22b93-135">**Configurar y ejecutar el script de Hola**</span><span class="sxs-lookup"><span data-stu-id="22b93-135">**Configure and run hello script**</span></span>

1. <span data-ttu-id="22b93-136">Abra el editor de texto, a continuación, copie y pegue Hola anteponer la secuencia de comandos en el editor de Hola.</span><span class="sxs-lookup"><span data-stu-id="22b93-136">Open your favorite text editor, then copy and paste hello preceding script into hello editor.</span></span>

2. <span data-ttu-id="22b93-137">A continuación, actualizar tooreflect de variables del script de Hola las opciones de configuración.</span><span class="sxs-lookup"><span data-stu-id="22b93-137">Next, update hello script's variables tooreflect your configuration settings.</span></span> <span data-ttu-id="22b93-138">Reemplace Hola siguientes valores tal como se especifica:</span><span class="sxs-lookup"><span data-stu-id="22b93-138">Replace hello following values as specified:</span></span>

   * <span data-ttu-id="22b93-139">**\<storage_account_name\>**  nombre hello de la cuenta de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="22b93-139">**\<storage_account_name\>** hello name of your storage account.</span></span>
   * <span data-ttu-id="22b93-140">**\<storage_account_key\>**  clave de acceso principal o secundaria de hello para la cuenta de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="22b93-140">**\<storage_account_key\>** hello primary or secondary access key for your storage account.</span></span>
   * <span data-ttu-id="22b93-141">**\<container_name\>**  nuevas toocreate de contenedor, por ejemplo, "azure-cli-ejemplo-container" Hola a un nombre.</span><span class="sxs-lookup"><span data-stu-id="22b93-141">**\<container_name\>** A name hello new container toocreate, such as "azure-cli-sample-container".</span></span>
   * <span data-ttu-id="22b93-142">**\<blob_name\>**  un nombre para el blob de destino de hello en el contenedor de Hola.</span><span class="sxs-lookup"><span data-stu-id="22b93-142">**\<blob_name\>** A name for hello destination blob in hello container.</span></span>
   * <span data-ttu-id="22b93-143">**\<file_to_upload\>**  Hola archivo toosmall de ruta de acceso en el equipo local, como "~ / images/HelloWorld.png".</span><span class="sxs-lookup"><span data-stu-id="22b93-143">**\<file_to_upload\>** hello path toosmall file on your local computer, such as "~/images/HelloWorld.png".</span></span>
   * <span data-ttu-id="22b93-144">**\<destination_file\>**  Hola ruta de acceso de archivo de destino, como "~ / downloadedImage.png".</span><span class="sxs-lookup"><span data-stu-id="22b93-144">**\<destination_file\>** hello destination file path, such as "~/downloadedImage.png".</span></span>

3. <span data-ttu-id="22b93-145">Después de actualizar las variables necesarias de hello, Guardar script de Hola y salir del editor.</span><span class="sxs-lookup"><span data-stu-id="22b93-145">After you've updated hello necessary variables, save hello script and exit your editor.</span></span> <span data-ttu-id="22b93-146">Hola siguiente da por sentado ha denominado el script **my_storage_sample.sh**.</span><span class="sxs-lookup"><span data-stu-id="22b93-146">hello next steps assume you've named your script **my_storage_sample.sh**.</span></span>

4. <span data-ttu-id="22b93-147">Marcar el script de Hola como archivo ejecutable, si es necesario:`chmod +x my_storage_sample.sh`</span><span class="sxs-lookup"><span data-stu-id="22b93-147">Mark hello script as executable, if necessary: `chmod +x my_storage_sample.sh`</span></span>

5. <span data-ttu-id="22b93-148">Ejecutar script de Hola.</span><span class="sxs-lookup"><span data-stu-id="22b93-148">Execute hello script.</span></span> <span data-ttu-id="22b93-149">Por ejemplo, en Bash: `./my_storage_sample.sh`</span><span class="sxs-lookup"><span data-stu-id="22b93-149">For example, in Bash: `./my_storage_sample.sh`</span></span>

<span data-ttu-id="22b93-150">Debe ver salida similares toohello siguiente y Hola  **\<destination_file\>**  especificado en hello script debe aparecer en el equipo local.</span><span class="sxs-lookup"><span data-stu-id="22b93-150">You should see output similar toohello following, and hello **\<destination_file\>** you specified in hello script should appear on your local computer.</span></span>

```
Creating hello container...
{
  "created": true
}
Uploading hello file...
Percent complete: %100.0
Listing hello blobs...
Name       Blob Type      Length  Content Type              Last Modified
---------  -----------  --------  ------------------------  -------------------------
README.md  BlockBlob        6700  application/octet-stream  2017-05-12T20:54:59+00:00
Downloading hello file...
Name
---------
README.md
Done
```

> [!TIP]
> <span data-ttu-id="22b93-151">Hello salida anterior está en **tabla** formato.</span><span class="sxs-lookup"><span data-stu-id="22b93-151">hello preceding output is in **table** format.</span></span> <span data-ttu-id="22b93-152">Puede especificar qué salida toouse formato especificando hello `--output` argumento en los comandos de CLI, o establecer globalmente mediante `az configure`.</span><span class="sxs-lookup"><span data-stu-id="22b93-152">You can specify which output format toouse by specifying hello `--output` argument in your CLI commands, or set it globally using `az configure`.</span></span>
>

## <a name="manage-storage-accounts"></a><span data-ttu-id="22b93-153">Administrar cuentas de almacenamiento</span><span class="sxs-lookup"><span data-stu-id="22b93-153">Manage storage accounts</span></span>

### <a name="create-a-new-storage-account"></a><span data-ttu-id="22b93-154">Creación de una cuenta de almacenamiento nueva</span><span class="sxs-lookup"><span data-stu-id="22b93-154">Create a new storage account</span></span>
<span data-ttu-id="22b93-155">toouse almacenamiento de Azure, necesita una cuenta de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="22b93-155">toouse Azure Storage, you need a storage account.</span></span> <span data-ttu-id="22b93-156">Puede crear una nueva cuenta de almacenamiento de Azure después de haber configurado el equipo demasiado[conectar tooyour suscripción](#connect-to-your-azure-subscription).</span><span class="sxs-lookup"><span data-stu-id="22b93-156">You can create a new Azure Storage account after you've configured your computer too[connect tooyour subscription](#connect-to-your-azure-subscription).</span></span>

```azurecli
az storage account create \
    --location <location> \
    --name <account_name> \
    --resource-group <resource_group> \
    --sku <account_sku>
```

* <span data-ttu-id="22b93-157">`--location` [Requerido]: Ubicación.</span><span class="sxs-lookup"><span data-stu-id="22b93-157">`--location` [Required]: Location.</span></span> <span data-ttu-id="22b93-158">Por ejemplo, "Oeste de EE. UU.".</span><span class="sxs-lookup"><span data-stu-id="22b93-158">For example, "West US".</span></span>
* <span data-ttu-id="22b93-159">`--name`[Required]: nombre de cuenta de almacenamiento de Hola.</span><span class="sxs-lookup"><span data-stu-id="22b93-159">`--name` [Required]: hello storage account name.</span></span> <span data-ttu-id="22b93-160">nombre de Hello debe tener 3 caracteres too24 y use solo caracteres alfanuméricos en minúsculas.</span><span class="sxs-lookup"><span data-stu-id="22b93-160">hello name must be 3 too24 characters in length, and use only lowercase alphanumeric characters.</span></span>
* <span data-ttu-id="22b93-161">`--resource-group`[Required]: Nombre del grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="22b93-161">`--resource-group` [Required]: Name of resource group.</span></span>
* <span data-ttu-id="22b93-162">`--sku`[Required]: Hola SKU de cuenta de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="22b93-162">`--sku` [Required]: hello storage account SKU.</span></span> <span data-ttu-id="22b93-163">Valores permitidos:</span><span class="sxs-lookup"><span data-stu-id="22b93-163">Allowed values:</span></span>
  * `Premium_LRS`
  * `Standard_GRS`
  * `Standard_LRS`
  * `Standard_RAGRS`
  * `Standard_ZRS`

### <a name="set-default-azure-storage-account-environment-variables"></a><span data-ttu-id="22b93-164">Establecimiento variables de entorno para una cuenta de almacenamiento de Azure predeterminada</span><span class="sxs-lookup"><span data-stu-id="22b93-164">Set default Azure storage account environment variables</span></span>
<span data-ttu-id="22b93-165">Puede tener varias cuentas de almacenamiento en su suscripción a Azure.</span><span class="sxs-lookup"><span data-stu-id="22b93-165">You can have multiple storage accounts in your Azure subscription.</span></span> <span data-ttu-id="22b93-166">tooselect uno de ellos toouse para todo el almacenamiento de posterior comandos, puede establecer estas variables de entorno:</span><span class="sxs-lookup"><span data-stu-id="22b93-166">tooselect one of them toouse for all subsequent storage commands, you can set these environment variables:</span></span>

```azurecli
export AZURE_STORAGE_ACCOUNT=<account_name>
export AZURE_STORAGE_ACCESS_KEY=<key>
```

<span data-ttu-id="22b93-167">Otra manera tooset una cuenta de almacenamiento predeterminada consiste en usar una cadena de conexión.</span><span class="sxs-lookup"><span data-stu-id="22b93-167">Another way tooset a default storage account is by using a connection string.</span></span> <span data-ttu-id="22b93-168">En primer lugar, obtener la cadena de conexión de hello con hello `show-connection-string` comando:</span><span class="sxs-lookup"><span data-stu-id="22b93-168">First, get hello connection string with hello `show-connection-string` command:</span></span>

```azurecli
az storage account show-connection-string \
    --name <account_name> \
    --resource-group <resource_group>
```

<span data-ttu-id="22b93-169">A continuación, Hola copia cadena de conexión de salida y establecer hello `AZURE_STORAGE_CONNECTION_STRING` variable de entorno (tal vez tenga la cadena de conexión de hello tooenclose entre comillas):</span><span class="sxs-lookup"><span data-stu-id="22b93-169">Then copy hello output connection string and set hello `AZURE_STORAGE_CONNECTION_STRING` environment variable (you might need tooenclose hello connection string in quotes):</span></span>

```azurecli
export AZURE_STORAGE_CONNECTION_STRING="<connection_string>"
```

> [!NOTE]
> <span data-ttu-id="22b93-170">Todos los ejemplos de hello siguientes secciones de este artículo se supone que ha establecido hello `AZURE_STORAGE_ACCOUNT` y `AZURE_STORAGE_ACCESS_KEY` las variables de entorno.</span><span class="sxs-lookup"><span data-stu-id="22b93-170">All examples in hello following sections of this article assume that you've set hello `AZURE_STORAGE_ACCOUNT` and `AZURE_STORAGE_ACCESS_KEY` environment variables.</span></span>
>

## <a name="create-and-manage-blobs"></a><span data-ttu-id="22b93-171">Creación y administración de blobs</span><span class="sxs-lookup"><span data-stu-id="22b93-171">Create and manage blobs</span></span>
<span data-ttu-id="22b93-172">Almacenamiento de blobs de Azure es un servicio para almacenar grandes cantidades de datos no estructurados, como texto o binario, que puede tener acceso desde cualquier lugar Hola mundo a través de HTTP o HTTPS.</span><span class="sxs-lookup"><span data-stu-id="22b93-172">Azure Blob storage is a service for storing large amounts of unstructured data, such as text or binary data, that can be accessed from anywhere in hello world via HTTP or HTTPS.</span></span> <span data-ttu-id="22b93-173">En esta sección se supone que ya está familiarizado con los conceptos del almacenamiento de Azure Blob Storage.</span><span class="sxs-lookup"><span data-stu-id="22b93-173">This section assumes that you are already familiar with Azure Blob storage concepts.</span></span> <span data-ttu-id="22b93-174">Para más información, consulte [Introducción a Azure Blob Storage mediante .NET](storage-dotnet-how-to-use-blobs.md) y [Conceptos de Blob service](/rest/api/storageservices/blob-service-concepts).</span><span class="sxs-lookup"><span data-stu-id="22b93-174">For detailed information, see [Get started with Azure Blob storage using .NET](storage-dotnet-how-to-use-blobs.md) and [Blob Service Concepts](/rest/api/storageservices/blob-service-concepts).</span></span>

### <a name="create-a-container"></a><span data-ttu-id="22b93-175">Crear un contenedor</span><span class="sxs-lookup"><span data-stu-id="22b93-175">Create a container</span></span>
<span data-ttu-id="22b93-176">Todos los blobs del almacenamiento de Azure han de estar en un contenedor.</span><span class="sxs-lookup"><span data-stu-id="22b93-176">Every blob in Azure storage must be in a container.</span></span> <span data-ttu-id="22b93-177">Puede crear un contenedor mediante hello `az storage container create` comando:</span><span class="sxs-lookup"><span data-stu-id="22b93-177">You can create a container by using hello `az storage container create` command:</span></span>

```azurecli
az storage container create --name <container_name>
```

<span data-ttu-id="22b93-178">Puede establecer uno de tres niveles de acceso de lectura para un nuevo contenedor mediante la especificación de hello opcional `--public-access` argumento:</span><span class="sxs-lookup"><span data-stu-id="22b93-178">You can set one of three levels of read access for a new container by specifying hello optional  `--public-access` argument:</span></span>

* <span data-ttu-id="22b93-179">`off`(valor predeterminado): datos del contenedor están el propietario de la cuenta de toohello privada.</span><span class="sxs-lookup"><span data-stu-id="22b93-179">`off` (default): Container data is private toohello account owner.</span></span>
* <span data-ttu-id="22b93-180">`blob`: acceso de lectura público solo para blobs.</span><span class="sxs-lookup"><span data-stu-id="22b93-180">`blob`: Public read access for blobs.</span></span>
* <span data-ttu-id="22b93-181">`container`: Leer y mostrar acceso toohello todo contenedor público.</span><span class="sxs-lookup"><span data-stu-id="22b93-181">`container`: Public read and list access toohello entire container.</span></span>

<span data-ttu-id="22b93-182">Para obtener más información, consulte [administrar toocontainers de acceso de lectura anónimo y los blobs](storage-manage-access-to-resources.md).</span><span class="sxs-lookup"><span data-stu-id="22b93-182">For more information, see [Manage anonymous read access toocontainers and blobs](storage-manage-access-to-resources.md).</span></span>

### <a name="upload-a-blob-tooa-container"></a><span data-ttu-id="22b93-183">Cargar un contenedor de blob tooa</span><span class="sxs-lookup"><span data-stu-id="22b93-183">Upload a blob tooa container</span></span>
<span data-ttu-id="22b93-184">Azure Blob Storage admite blobs de bloque, anexados y en páginas.</span><span class="sxs-lookup"><span data-stu-id="22b93-184">Azure Blob storage supports block, append, and page blobs.</span></span> <span data-ttu-id="22b93-185">Cargar blobs tooa contenedor mediante el uso de hello `blob upload` comando:</span><span class="sxs-lookup"><span data-stu-id="22b93-185">Upload blobs tooa container by using hello `blob upload` command:</span></span>

```azurecli
az storage blob upload \
    --file <local_file_path> \
    --container-name <container_name> \
    --name <blob_name>
```

 <span data-ttu-id="22b93-186">De forma predeterminada, Hola `blob upload` comando carga los blobs de *.vhd archivos toopage o blobs en bloques en caso contrario.</span><span class="sxs-lookup"><span data-stu-id="22b93-186">By default, hello `blob upload` command uploads *.vhd files toopage blobs, or block blobs otherwise.</span></span> <span data-ttu-id="22b93-187">toospecify otro cuando escriba cargar un blob, puede usar hello `--type` argumento--valores permitido son `append`, `block`, y `page`.</span><span class="sxs-lookup"><span data-stu-id="22b93-187">toospecify another type when you upload a blob, you can use hello `--type` argument--allowed values are `append`, `block`, and `page`.</span></span>

 <span data-ttu-id="22b93-188">Para obtener más información sobre tipos de blob distinto de hello, consulte [descripción Blobs en bloques, anexar Blobs y Blobs en páginas](/rest/api/storageservices/Understanding-Block-Blobs--Append-Blobs--and-Page-Blobs).</span><span class="sxs-lookup"><span data-stu-id="22b93-188">For more information on hello different blob types, see [Understanding Block Blobs, Append Blobs, and Page Blobs](/rest/api/storageservices/Understanding-Block-Blobs--Append-Blobs--and-Page-Blobs).</span></span>


### <a name="download-a-blob-from-a-container"></a><span data-ttu-id="22b93-189">Descarga de un blob de un contenedor</span><span class="sxs-lookup"><span data-stu-id="22b93-189">Download a blob from a container</span></span>
<span data-ttu-id="22b93-190">Este ejemplo se muestra cómo toodownload un blob de un contenedor:</span><span class="sxs-lookup"><span data-stu-id="22b93-190">This example demonstrates how toodownload a blob from a container:</span></span>

```azurecli
az storage blob download \
    --container-name mycontainer \
    --name myblob.png \
    --file ~/mydownloadedblob.png
```

### <a name="list-hello-blobs-in-a-container"></a><span data-ttu-id="22b93-191">Lista de blobs de hello en un contenedor</span><span class="sxs-lookup"><span data-stu-id="22b93-191">List hello blobs in a container</span></span>

<span data-ttu-id="22b93-192">Lista de blobs de hello en un contenedor con hello [lista de blobs de almacenamiento az](/cli/azure/storage/blob#list) comando.</span><span class="sxs-lookup"><span data-stu-id="22b93-192">List hello blobs in a container with hello [az storage blob list](/cli/azure/storage/blob#list) command.</span></span>

```azurecli
az storage blob list \
    --container-name mycontainer \
    --output table
```

### <a name="copy-blobs"></a><span data-ttu-id="22b93-193">Copia de blobs</span><span class="sxs-lookup"><span data-stu-id="22b93-193">Copy blobs</span></span>
<span data-ttu-id="22b93-194">Los blobs se pueden copiar dentro de las cuentas de almacenamiento y regiones, o entre ellas, de forma asincrónica.</span><span class="sxs-lookup"><span data-stu-id="22b93-194">You can copy blobs within or across storage accounts and regions asynchronously.</span></span>

<span data-ttu-id="22b93-195">Hello en el ejemplo siguiente se muestra cómo toocopy blobs desde el almacenamiento de una cuenta tooanother.</span><span class="sxs-lookup"><span data-stu-id="22b93-195">hello following example demonstrates how toocopy blobs from one storage account tooanother.</span></span> <span data-ttu-id="22b93-196">Primero creamos un contenedor en la cuenta de almacenamiento de origen de hello, especifica el acceso de lectura público para sus blobs.</span><span class="sxs-lookup"><span data-stu-id="22b93-196">We first create a container in hello source storage account, specifying public read-access for its blobs.</span></span> <span data-ttu-id="22b93-197">A continuación, se carga un contenedor de toohello de archivo y, finalmente, copia de blob de Hola desde ese contenedor en un contenedor en la cuenta de almacenamiento de destino de Hola.</span><span class="sxs-lookup"><span data-stu-id="22b93-197">Next, we upload a file toohello container, and finally, copy hello blob from that container into a container in hello destination storage account.</span></span>

```azurecli
# Create container in source account
az storage container create \
    --account-name sourceaccountname \
    --account-key sourceaccountkey \
    --name sourcecontainer \
    --public-access blob

# Upload blob toocontainer in source account
az storage blob upload \
    --account-name sourceaccountname \
    --account-key sourceaccountkey \
    --container-name sourcecontainer \
    --file ~/Pictures/sourcefile.png \
    --name sourcefile.png

# Copy blob from source account toodestination account (destcontainer must exist)
az storage blob copy start \
    --account-name destaccountname \
    --account-key destaccountkey \
    --destination-blob destfile.png \
    --destination-container destcontainer \
    --source-uri https://sourceaccountname.blob.core.windows.net/sourcecontainer/sourcefile.png
```

<span data-ttu-id="22b93-198">Hola ejemplo anterior, contenedor de destino de hello ya debe existir en la cuenta de almacenamiento de destino de Hola para toosucceed de operación de copia de Hola.</span><span class="sxs-lookup"><span data-stu-id="22b93-198">In hello above example, hello destination container must already exist in hello destination storage account for hello copy operation toosucceed.</span></span> <span data-ttu-id="22b93-199">Además, Hola blob de origen especificada en hello `--source-uri` argumento debe incluir un token de firma (SAS) de acceso compartido, o ser accesibles públicamente, como en este ejemplo.</span><span class="sxs-lookup"><span data-stu-id="22b93-199">Additionally, hello source blob specified in hello `--source-uri` argument must either include a shared access signature (SAS) token, or be publicly accessible, as in this example.</span></span>

### <a name="delete-a-blob"></a><span data-ttu-id="22b93-200">Eliminar un blob</span><span class="sxs-lookup"><span data-stu-id="22b93-200">Delete a blob</span></span>
<span data-ttu-id="22b93-201">toodelete un blob, use hello `blob delete` comando:</span><span class="sxs-lookup"><span data-stu-id="22b93-201">toodelete a blob, use hello `blob delete` command:</span></span>

```azurecli
az storage blob delete --container-name <container_name> --name <blob_name>
```

## <a name="create-and-manage-file-shares"></a><span data-ttu-id="22b93-202">Creación y administración de recursos compartidos de archivos</span><span class="sxs-lookup"><span data-stu-id="22b93-202">Create and manage file shares</span></span>
<span data-ttu-id="22b93-203">Almacenamiento de archivos de Azure ofrece almacenamiento compartido para las aplicaciones que usan el protocolo de bloque de mensajes del servidor (SMB) Hola.</span><span class="sxs-lookup"><span data-stu-id="22b93-203">Azure File storage offers shared storage for applications using hello Server Message Block (SMB) protocol.</span></span> <span data-ttu-id="22b93-204">Los servicios en la nube y las máquinas virtuales de Microsoft Azure, así como las aplicaciones locales, pueden compartir datos de archivos a través de recursos compartidos montados.</span><span class="sxs-lookup"><span data-stu-id="22b93-204">Microsoft Azure virtual machines and cloud services, as well as on-premises applications, can share file data via mounted shares.</span></span> <span data-ttu-id="22b93-205">Puede administrar recursos compartidos de archivos y datos de archivos a través de hello CLI de Azure.</span><span class="sxs-lookup"><span data-stu-id="22b93-205">You can manage file shares and file data via hello Azure CLI.</span></span> <span data-ttu-id="22b93-206">Para obtener más información sobre el almacenamiento de archivos de Azure, consulte [Introducción al almacenamiento de archivos de Azure en Windows](storage-dotnet-how-to-use-files.md) o [cómo toouse almacenamiento de archivos de Azure con Linux](storage-how-to-use-files-linux.md).</span><span class="sxs-lookup"><span data-stu-id="22b93-206">For more information on Azure File storage, see [Get started with Azure File storage on Windows](storage-dotnet-how-to-use-files.md) or [How toouse Azure File storage with Linux](storage-how-to-use-files-linux.md).</span></span>

### <a name="create-a-file-share"></a><span data-ttu-id="22b93-207">Creación de un recurso compartido de archivos</span><span class="sxs-lookup"><span data-stu-id="22b93-207">Create a file share</span></span>
<span data-ttu-id="22b93-208">Un recurso compartido de archivos de Azure es un recurso compartido de archivos de SMB en Azure.</span><span class="sxs-lookup"><span data-stu-id="22b93-208">An Azure File share is an SMB file share in Azure.</span></span> <span data-ttu-id="22b93-209">Todos los directorios y archivos se deben crear en un recurso compartido de archivos.</span><span class="sxs-lookup"><span data-stu-id="22b93-209">All directories and files must be created in a file share.</span></span> <span data-ttu-id="22b93-210">Una cuenta puede contener un número ilimitado de recursos compartidos y un recurso compartido puede almacenar un número ilimitado de archivos, los límites de capacidad de toohello de cuenta de almacenamiento de Hola.</span><span class="sxs-lookup"><span data-stu-id="22b93-210">An account can contain an unlimited number of shares, and a share can store an unlimited number of files, up toohello capacity limits of hello storage account.</span></span> <span data-ttu-id="22b93-211">Hello en el ejemplo siguiente se crea un recurso compartido de archivos denominado **MiRecursoCompartido**.</span><span class="sxs-lookup"><span data-stu-id="22b93-211">hello following example creates a file share named **myshare**.</span></span>

```azurecli
az storage share create --name myshare
```

### <a name="create-a-directory"></a><span data-ttu-id="22b93-212">Creación de directorios</span><span class="sxs-lookup"><span data-stu-id="22b93-212">Create a directory</span></span>
<span data-ttu-id="22b93-213">Un directorio proporciona una estructura jerárquica para los recursos compartidos de archivos de Azure.</span><span class="sxs-lookup"><span data-stu-id="22b93-213">A directory provides a hierarchical structure in an Azure file share.</span></span> <span data-ttu-id="22b93-214">Hello en el ejemplo siguiente se crea un directorio denominado **myDir** en el recurso compartido de archivos de Hola.</span><span class="sxs-lookup"><span data-stu-id="22b93-214">hello following example creates a directory named **myDir** in hello file share.</span></span>

```azurecli
az storage directory create --name myDir --share-name myshare
```

<span data-ttu-id="22b93-215">La ruta de acceso al directorio puede incluir varios niveles, por ejemplo, **dir1/dir2**.</span><span class="sxs-lookup"><span data-stu-id="22b93-215">A directory path can include multiple levels, for example **dir1/dir2**.</span></span> <span data-ttu-id="22b93-216">Pero debe asegurarse de que existen todos los directorios principales antes de crear un subdirectorio.</span><span class="sxs-lookup"><span data-stu-id="22b93-216">However, you must ensure that all parent directories exist before creating a subdirectory.</span></span> <span data-ttu-id="22b93-217">Por ejemplo, para la ruta de acceso **dir1/dir2**, primero se debe crear el directorio **dir1** y luego el directorio **dir2**.</span><span class="sxs-lookup"><span data-stu-id="22b93-217">For example, for path **dir1/dir2**, you must first create directory **dir1**, then create directory **dir2**.</span></span>

### <a name="upload-a-local-file-tooa-share"></a><span data-ttu-id="22b93-218">Cargar un recurso compartido tooa de archivos local</span><span class="sxs-lookup"><span data-stu-id="22b93-218">Upload a local file tooa share</span></span>
<span data-ttu-id="22b93-219">Hello en el ejemplo siguiente se carga un archivo de **~/temp/samplefile.txt** tooroot de hello **MiRecursoCompartido** recurso compartido de archivos.</span><span class="sxs-lookup"><span data-stu-id="22b93-219">hello following example uploads a file from **~/temp/samplefile.txt** tooroot of hello **myshare** file share.</span></span> <span data-ttu-id="22b93-220">Hola `--source` tooupload de archivo local existente de Hola que especifica el argumento.</span><span class="sxs-lookup"><span data-stu-id="22b93-220">hello `--source` argument specifies hello existing local file tooupload.</span></span>

```azurecli
az storage file upload --share-name myshare --source ~/temp/samplefile.txt
```

<span data-ttu-id="22b93-221">Al igual que con la creación del directorio, puede especificar una ruta de acceso de directorio dentro de hello tooupload Hola archivo tooan existente directorio compartido en el recurso compartido de hello:</span><span class="sxs-lookup"><span data-stu-id="22b93-221">As with directory creation, you can specify a directory path within hello share tooupload hello file tooan existing directory within hello share:</span></span>

```azurecli
az storage file upload --share-name myshare/myDir --source ~/temp/samplefile.txt
```

<span data-ttu-id="22b93-222">Puede ser un archivo en el recurso compartido de hello hasta too1 TB de tamaño.</span><span class="sxs-lookup"><span data-stu-id="22b93-222">A file in hello share can be up too1 TB in size.</span></span>

### <a name="list-hello-files-in-a-share"></a><span data-ttu-id="22b93-223">Enumerar archivos de hello en un recurso compartido</span><span class="sxs-lookup"><span data-stu-id="22b93-223">List hello files in a share</span></span>
<span data-ttu-id="22b93-224">Puede enumerar archivos y directorios en un recurso compartido mediante hello `az storage file list` comando:</span><span class="sxs-lookup"><span data-stu-id="22b93-224">You can list files and directories in a share by using hello `az storage file list` command:</span></span>

```azurecli
# List hello files in hello root of a share
az storage file list --share-name myshare --output table

# List hello files in a directory within a share
az storage file list --share-name myshare/myDir --output table

# List hello files in a path within a share
az storage file list --share-name myshare --path myDir/mySubDir/MySubDir2 --output table
```

### <a name="copy-files"></a><span data-ttu-id="22b93-225">Copiar archivos</span><span class="sxs-lookup"><span data-stu-id="22b93-225">Copy files</span></span>      
<span data-ttu-id="22b93-226">Puede copiar un archivo de tooanother, un blob de tooa de archivo o un archivo de tooa de blob.</span><span class="sxs-lookup"><span data-stu-id="22b93-226">You can copy a file tooanother file, a file tooa blob, or a blob tooa file.</span></span> <span data-ttu-id="22b93-227">Por ejemplo, toocopy un archivo tooa directorio en otro recurso compartido:</span><span class="sxs-lookup"><span data-stu-id="22b93-227">For example, toocopy a file tooa directory in a different share:</span></span>        
        
```azurecli
az storage file copy start \
--source-share share1 --source-path dir1/file.txt \
--destination-share share2 --destination-path dir2/file.txt     
```

## <a name="next-steps"></a><span data-ttu-id="22b93-228">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="22b93-228">Next steps</span></span>
<span data-ttu-id="22b93-229">Aquí tiene algunos recursos adicionales para aprender más acerca de cómo trabajar con hello 2.0 de CLI de Azure.</span><span class="sxs-lookup"><span data-stu-id="22b93-229">Here are some additional resources for learning more about working with hello Azure CLI 2.0.</span></span>

* [<span data-ttu-id="22b93-230">Introducción a la CLI de Azure 2.0</span><span class="sxs-lookup"><span data-stu-id="22b93-230">Get started with Azure CLI 2.0</span></span>](https://docs.microsoft.com/cli/azure/get-started-with-az-cli2)
* [<span data-ttu-id="22b93-231">Referencia de comandos de la CLI de Azure 2.0</span><span class="sxs-lookup"><span data-stu-id="22b93-231">Azure CLI 2.0 command reference</span></span>](/cli/azure)
* [<span data-ttu-id="22b93-232">CLI de Azure 2.0 en GitHub</span><span class="sxs-lookup"><span data-stu-id="22b93-232">Azure CLI 2.0 on GitHub</span></span>](https://github.com/Azure/azure-cli)
