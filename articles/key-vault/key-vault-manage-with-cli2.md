---
title: "aaaManage con CLI del almacén de claves de Azure | Documentos de Microsoft"
description: "Usar tareas de este tutorial tooautomate en el almacén de claves mediante Hola CLI 2.0"
services: key-vault
documentationcenter: 
author: amitbapat
manager: mbaldwin
tags: azure-resource-manager
ms.assetid: 
ms.service: key-vault
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/08/2017
ms.author: ambapat
ms.openlocfilehash: 76855c0ea09b6b307159468382a6a63627205556
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="manage-key-vault-using-cli-20"></a><span data-ttu-id="a51b5-103">Administración de Key Vault mediante CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="a51b5-103">Manage Key Vault using CLI 2.0</span></span>
<span data-ttu-id="a51b5-104">Almacén de claves de Azure está disponible en la mayoría de las regiones.</span><span class="sxs-lookup"><span data-stu-id="a51b5-104">Azure Key Vault is available in most regions.</span></span> <span data-ttu-id="a51b5-105">Para obtener más información, vea hello [almacén de claves de página de precios](https://azure.microsoft.com/pricing/details/key-vault/).</span><span class="sxs-lookup"><span data-stu-id="a51b5-105">For more information, see hello [Key Vault pricing page](https://azure.microsoft.com/pricing/details/key-vault/).</span></span>

## <a name="introduction"></a><span data-ttu-id="a51b5-106">Introducción</span><span class="sxs-lookup"><span data-stu-id="a51b5-106">Introduction</span></span>
<span data-ttu-id="a51b5-107">Use este tutorial toohelp obtendrá a trabajar con el almacén de claves de Azure toocreate un contenedor reforzado (un almacén) en Azure, toostore y administrar las claves criptográficas y secretos en Azure.</span><span class="sxs-lookup"><span data-stu-id="a51b5-107">Use this tutorial toohelp you get started with Azure Key Vault toocreate a hardened container (a vault) in Azure, toostore and manage cryptographic keys and secrets in Azure.</span></span> <span data-ttu-id="a51b5-108">Le guiará por proceso de Hola de uso de interfaz de línea de comandos entre plataformas de Azure toocreate un almacén que contiene una clave o contraseña que puede utilizar con una aplicación de Azure.</span><span class="sxs-lookup"><span data-stu-id="a51b5-108">It walks you through hello process of using Azure Cross-Platform Command-Line Interface toocreate a vault that contains a key or password that you can then use with an Azure application.</span></span> <span data-ttu-id="a51b5-109">A continuación, se explica cómo utiliza una aplicación esa clave o contraseña.</span><span class="sxs-lookup"><span data-stu-id="a51b5-109">It then shows you how an application can then use that key or password.</span></span>

<span data-ttu-id="a51b5-110">**Estimado toocomplete de tiempo:** 20 minutos</span><span class="sxs-lookup"><span data-stu-id="a51b5-110">**Estimated time toocomplete:** 20 minutes</span></span>

> [!NOTE]
> <span data-ttu-id="a51b5-111">Este tutorial no incluye instrucciones sobre cómo toowrite Hola aplicación de Azure que incluye uno de los pasos de hello, que muestra cómo tooauthorize una toouse una clave de aplicación o un secreto de clave de hello almacén.</span><span class="sxs-lookup"><span data-stu-id="a51b5-111">This tutorial does not include instructions on how toowrite hello Azure application that one of hello steps includes, which shows how tooauthorize an application toouse a key or secret in hello key vault.</span></span>
>
> <span data-ttu-id="a51b5-112">Este tutorial se utiliza Hola 2.0 más reciente de CLI de Azure.</span><span class="sxs-lookup"><span data-stu-id="a51b5-112">This tutorial uses hello latest Azure CLI 2.0.</span></span>
>
>

<span data-ttu-id="a51b5-113">Para obtener información general sobre el Almacén de claves de Azure, consulte [¿Qué es el Almacén de clave de Azure?](key-vault-whatis.md)</span><span class="sxs-lookup"><span data-stu-id="a51b5-113">For overview information about Azure Key Vault, see [What is Azure Key Vault?](key-vault-whatis.md)</span></span>

## <a name="prerequisites"></a><span data-ttu-id="a51b5-114">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="a51b5-114">Prerequisites</span></span>
<span data-ttu-id="a51b5-115">toocomplete este tutorial, debe tener Hola siguientes:</span><span class="sxs-lookup"><span data-stu-id="a51b5-115">toocomplete this tutorial, you must have hello following:</span></span>

* <span data-ttu-id="a51b5-116">Un tooMicrosoft de suscripción de Azure.</span><span class="sxs-lookup"><span data-stu-id="a51b5-116">A subscription tooMicrosoft Azure.</span></span> <span data-ttu-id="a51b5-117">Si no tiene una, puede registrarse para obtener una versión de [evaluación gratuita](https://azure.microsoft.com/pricing/free-trial).</span><span class="sxs-lookup"><span data-stu-id="a51b5-117">If you do not have one, you can sign up for a [free trial](https://azure.microsoft.com/pricing/free-trial).</span></span>
* <span data-ttu-id="a51b5-118">Versión 2.0 de la interfaz de la línea de comandos o posterior.</span><span class="sxs-lookup"><span data-stu-id="a51b5-118">Command-Line Interface version 2.0 or later.</span></span> <span data-ttu-id="a51b5-119">tooinstall Hola versión más reciente y conectar tooyour suscripción de Azure, consulte [instalar y configurar hello Azure 2.0 de interfaz de línea de comandos multiplataforma](/cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="a51b5-119">tooinstall hello latest version and connect tooyour Azure subscription, see [Install and Configure hello Azure Cross-Platform Command-Line Interface 2.0](/cli/azure/install-azure-cli).</span></span>
* <span data-ttu-id="a51b5-120">Una aplicación para que esté configurado toouse clave de Hola o la contraseña que creará en este tutorial.</span><span class="sxs-lookup"><span data-stu-id="a51b5-120">An application that will be configured toouse hello key or password that you create in this tutorial.</span></span> <span data-ttu-id="a51b5-121">Una aplicación de ejemplo está disponible en hello [Microsoft Download Center](http://www.microsoft.com/download/details.aspx?id=45343).</span><span class="sxs-lookup"><span data-stu-id="a51b5-121">A sample application is available from hello [Microsoft Download Center](http://www.microsoft.com/download/details.aspx?id=45343).</span></span> <span data-ttu-id="a51b5-122">Para obtener instrucciones, consulte Hola que acompaña a archivo Léame.</span><span class="sxs-lookup"><span data-stu-id="a51b5-122">For instructions, see hello accompanying Readme file.</span></span>

## <a name="getting-help-with-azure-cross-platform-command-line-interface"></a><span data-ttu-id="a51b5-123">Obtención de ayuda con la interfaz de la línea de comandos entre plataformas de Azure</span><span class="sxs-lookup"><span data-stu-id="a51b5-123">Getting help with Azure Cross-Platform Command-Line Interface</span></span>
<span data-ttu-id="a51b5-124">Este tutorial se da por supuesto que está familiarizado con la interfaz de línea de comandos de hello (intensiva de errores, Terminal, símbolo del sistema)</span><span class="sxs-lookup"><span data-stu-id="a51b5-124">This tutorial assumes that you are familiar with hello command-line interface (Bash, Terminal, Command prompt)</span></span>

<span data-ttu-id="a51b5-125">Hello--ayuda o -h parámetro puede ser utilizados tooview ayuda para comandos específicos.</span><span class="sxs-lookup"><span data-stu-id="a51b5-125">hello --help or -h parameter can be used tooview help for specific commands.</span></span> <span data-ttu-id="a51b5-126">Como alternativa, help hello azure [comando] [opciones] formato también puede ser usado tooreturn Hola misma información.</span><span class="sxs-lookup"><span data-stu-id="a51b5-126">Alternately, hello azure help [command] [options] format can also be used tooreturn hello same information.</span></span> <span data-ttu-id="a51b5-127">Por ejemplo, siguiente Hola comandos devuelven todos los Hola la misma información:</span><span class="sxs-lookup"><span data-stu-id="a51b5-127">For example, hello following commands all return hello same information:</span></span>

```
az account set --help
az account set -h
```

<span data-ttu-id="a51b5-128">En caso de duda acerca de los parámetros de hello necesarios para un comando, consulte usar toohelp--ayuda, -h o az help [comando].</span><span class="sxs-lookup"><span data-stu-id="a51b5-128">When in doubt about hello parameters needed by a command, refer toohelp using --help, -h or az help [command].</span></span>

<span data-ttu-id="a51b5-129">También puede leer Hola después tutoriales tooget familiarizado con Azure Resource Manager en el interfaz de línea de comandos de plataforma cruzada de Azure:</span><span class="sxs-lookup"><span data-stu-id="a51b5-129">You can also read hello following tutorials tooget familiar with Azure Resource Manager in Azure Cross-Platform Command-Line Interface:</span></span>

* [<span data-ttu-id="a51b5-130">Instalación de la CLI de Azure</span><span class="sxs-lookup"><span data-stu-id="a51b5-130">Install Azure CLI</span></span>](/cli/azure/install-azure-cli)
* [<span data-ttu-id="a51b5-131">Introducción a la CLI de Azure 2.0</span><span class="sxs-lookup"><span data-stu-id="a51b5-131">Get started with Azure CLI 2.0</span></span>](/cli/azure/get-started-with-azure-cli)

## <a name="connect-tooyour-subscriptions"></a><span data-ttu-id="a51b5-132">Conectar tooyour suscripciones</span><span class="sxs-lookup"><span data-stu-id="a51b5-132">Connect tooyour subscriptions</span></span>
<span data-ttu-id="a51b5-133">toolog sesión con una cuenta profesional, Hola de uso siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="a51b5-133">toolog in using an organizational account, use hello following command:</span></span>

```
az login -u username@domain.com -p password
```

<span data-ttu-id="a51b5-134">o si desea toolog escribiendo interactivamente</span><span class="sxs-lookup"><span data-stu-id="a51b5-134">or if you want toolog in by typing interactively</span></span>

```
az login
```

<span data-ttu-id="a51b5-135">Si tiene varias suscripciones y desea toospecify un uno toouse específico para el almacén de claves de Azure, escriba Hola siguiendo las suscripciones de hello toosee para su cuenta:</span><span class="sxs-lookup"><span data-stu-id="a51b5-135">If you have multiple subscriptions and want toospecify a specific one toouse for Azure Key Vault, type hello following toosee hello subscriptions for your account:</span></span>

```
az account list
```

<span data-ttu-id="a51b5-136">A continuación, toospecify Hola suscripción toouse, tipo:</span><span class="sxs-lookup"><span data-stu-id="a51b5-136">Then, toospecify hello subscription toouse, type:</span></span>

```
az account set --subscription <subscription name or ID>
```

<span data-ttu-id="a51b5-137">Para más información acerca de cómo configurar la interfaz de la línea de comandos entre plataformas de Azure, consulte el artículo sobre la [instalación de la CLI de Azure](/cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="a51b5-137">For more information about configuring Azure Cross-Platform Command-Line Interface, see [Install Azure CLI](/cli/azure/install-azure-cli).</span></span>

## <a name="create-a-new-resource-group"></a><span data-ttu-id="a51b5-138">Creación de un nuevo grupo de recursos</span><span class="sxs-lookup"><span data-stu-id="a51b5-138">Create a new resource group</span></span>
<span data-ttu-id="a51b5-139">Cuando se utiliza el Administrador de recursos de Azure, todos los recursos relacionados se crean dentro de un grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="a51b5-139">When using Azure Resource Manager, all related resources are created inside a resource group.</span></span> <span data-ttu-id="a51b5-140">Crearemos un nuevo grupo de recursos denominado 'ContosoResourceGroup' para este tutorial.</span><span class="sxs-lookup"><span data-stu-id="a51b5-140">We will create a new resource group 'ContosoResourceGroup' for this tutorial.</span></span>

```
az group create -n 'ContosoResourceGroup' -l 'East Asia'
```

<span data-ttu-id="a51b5-141">Hola primer parámetro es el nombre del grupo de recursos y Hola segundo parámetro es la ubicación de Hola.</span><span class="sxs-lookup"><span data-stu-id="a51b5-141">hello first parameter is resource group name and hello second parameter is hello location.</span></span> <span data-ttu-id="a51b5-142">Para la ubicación, utilice el comando de hello `az account list-locations` tooidentify cómo toospecify una ubicación alternativa toohello uno en este ejemplo.</span><span class="sxs-lookup"><span data-stu-id="a51b5-142">For location, use hello command `az account list-locations` tooidentify how toospecify an alternative location toohello one in this example.</span></span> <span data-ttu-id="a51b5-143">Si necesita más información, escriba: `az account list-locations -h`.</span><span class="sxs-lookup"><span data-stu-id="a51b5-143">If you need more information, type: `az account list-locations -h`.</span></span>

## <a name="register-hello-key-vault-resource-provider"></a><span data-ttu-id="a51b5-144">Registrar el proveedor de recursos de almacén de claves de Hola</span><span class="sxs-lookup"><span data-stu-id="a51b5-144">Register hello Key Vault resource provider</span></span>
<span data-ttu-id="a51b5-145">Asegúrese de que el proveedor de recursos de Almacén de claves está registrado en la suscripción:</span><span class="sxs-lookup"><span data-stu-id="a51b5-145">Make sure that Key Vault resource provider is registered in your subscription:</span></span>

```
az provider register -n Microsoft.KeyVault
```

<span data-ttu-id="a51b5-146">Solo es necesario toobe efectuar una vez por cada suscripción.</span><span class="sxs-lookup"><span data-stu-id="a51b5-146">This only needs toobe done once per subscription.</span></span>

## <a name="create-a-key-vault"></a><span data-ttu-id="a51b5-147">Creación de un Almacén de claves</span><span class="sxs-lookup"><span data-stu-id="a51b5-147">Create a key vault</span></span>
<span data-ttu-id="a51b5-148">Hola de uso `az keyvault create` comando toocreate un almacén de claves.</span><span class="sxs-lookup"><span data-stu-id="a51b5-148">Use hello `az keyvault create` command toocreate a key vault.</span></span> <span data-ttu-id="a51b5-149">Esta secuencia de comandos tiene tres parámetros obligatorios: un nombre de grupo de recursos, un nombre de almacén de claves y la ubicación geográfica de Hola.</span><span class="sxs-lookup"><span data-stu-id="a51b5-149">This script has three mandatory parameters: a resource group name, a key vault name, and hello geographic location.</span></span>

<span data-ttu-id="a51b5-150">Por ejemplo, si utiliza el nombre de almacén de Hola de ContosoKeyVault, nombre de grupo de recursos de Hola de ContosoResourceGroup y la ubicación de Hola de Asia oriental, escriba:</span><span class="sxs-lookup"><span data-stu-id="a51b5-150">For example, if you use hello vault name of ContosoKeyVault, hello resource group name of ContosoResourceGroup, and hello location of East Asia, type:</span></span>
```
az keyvault create --name 'ContosoKeyVault' --resource-group 'ContosoResourceGroup' --location 'East Asia'
```

<span data-ttu-id="a51b5-151">salida de Hello de este comando muestra propiedades del almacén de claves de Hola que acaba de crear.</span><span class="sxs-lookup"><span data-stu-id="a51b5-151">hello output of this command shows properties of hello key vault that you've just created.</span></span> <span data-ttu-id="a51b5-152">propiedades de Hello dos más importantes son:</span><span class="sxs-lookup"><span data-stu-id="a51b5-152">hello two most important properties are:</span></span>

* <span data-ttu-id="a51b5-153">**nombre**: en el ejemplo de Hola es ContosoKeyVault.</span><span class="sxs-lookup"><span data-stu-id="a51b5-153">**name**: In hello example this is ContosoKeyVault.</span></span> <span data-ttu-id="a51b5-154">Utilizará este nombre para otros comandos de Key Vault.</span><span class="sxs-lookup"><span data-stu-id="a51b5-154">You will use this name for other Key Vault commands.</span></span>
* <span data-ttu-id="a51b5-155">**vaultUri**: en el ejemplo de Hola es https://contosokeyvault.vault.azure.net.</span><span class="sxs-lookup"><span data-stu-id="a51b5-155">**vaultUri**: In hello example this is https://contosokeyvault.vault.azure.net.</span></span> <span data-ttu-id="a51b5-156">Las aplicaciones que utilizan el almacén a través de su API de REST deben usar este identificador URI.</span><span class="sxs-lookup"><span data-stu-id="a51b5-156">Applications that use your vault through its REST API must use this URI.</span></span>

<span data-ttu-id="a51b5-157">Su cuenta de Azure es ahora tooperform autorizado cualquier operación en esta clave de seguridad del almacén.</span><span class="sxs-lookup"><span data-stu-id="a51b5-157">Your Azure account is now authorized tooperform any operations on this key vault.</span></span> <span data-ttu-id="a51b5-158">Hasta el momento, nadie más lo está.</span><span class="sxs-lookup"><span data-stu-id="a51b5-158">As yet, nobody else is.</span></span>

## <a name="add-a-key-or-secret-toohello-key-vault"></a><span data-ttu-id="a51b5-159">Agregar una clave o un almacén de claves secretas toohello</span><span class="sxs-lookup"><span data-stu-id="a51b5-159">Add a key or secret toohello key vault</span></span>
<span data-ttu-id="a51b5-160">Si desea que el almacén de claves de Azure toocreate una clave protegida por software automáticamente, use hello `az key create` de comandos y escriba Hola siguiente:</span><span class="sxs-lookup"><span data-stu-id="a51b5-160">If you want Azure Key Vault toocreate a software-protected key for you, use hello `az key create` command, and type hello following:</span></span>
```
az keyvault key create --vault-name 'ContosoKeyVault' --name 'ContosoFirstKey' --protection software
```
<span data-ttu-id="a51b5-161">Sin embargo, si tiene una clave existente en un archivo PEM guardado como archivo local en un archivo denominado softkey.pem que desea tooupload tooAzure el almacén de claves, escriba Hola siguientes clave de hello tooimport de Hola. Archivo PEM, que protege la clave de hello mediante software en hello servicio Almacén de claves:</span><span class="sxs-lookup"><span data-stu-id="a51b5-161">However, if you have an existing key in a .pem file saved as local file in a file named softkey.pem that you want tooupload tooAzure Key Vault, type hello following tooimport hello key from hello .PEM file, which protects hello key by software in hello Key Vault service:</span></span>
```
az keyvault key import --vault-name 'ContosoKeyVault' --name 'ContosoFirstKey' --pem-file './softkey.pem' --pem-password 'PaSSWORD' --protection software
```
<span data-ttu-id="a51b5-162">Ahora puede hacer referencia a clave de Hola que creó o cargó tooAzure el almacén de claves, utilizando su URI.</span><span class="sxs-lookup"><span data-stu-id="a51b5-162">You can now reference hello key that you created or uploaded tooAzure Key Vault, by using its URI.</span></span> <span data-ttu-id="a51b5-163">Usar **https://ContosoKeyVault.vault.azure.net/keys/ContosoFirstKey** tooalways obtener la versión actual de Hola y usar **https://ContosoKeyVault.vault.azure.net/keys/ContosoFirstKey/ cgacf4f763ar42ffb0a1gca546aygd87** tooget esta versión específica.</span><span class="sxs-lookup"><span data-stu-id="a51b5-163">Use  **https://ContosoKeyVault.vault.azure.net/keys/ContosoFirstKey** tooalways get hello current version, and use **https://ContosoKeyVault.vault.azure.net/keys/ContosoFirstKey/cgacf4f763ar42ffb0a1gca546aygd87** tooget this specific version.</span></span>

<span data-ttu-id="a51b5-164">tooadd un almacén toohello secreta, que es una contraseña denominada SQLPassword y no tiene valor de Hola de Pa$ $w0rd tooAzure el almacén de claves, Hola de tipo siguientes:</span><span class="sxs-lookup"><span data-stu-id="a51b5-164">tooadd a secret toohello vault, which is a password named SQLPassword and that has hello value of Pa$$w0rd tooAzure Key Vault, type hello following:</span></span>
```
az keyvault secret set --vault-name 'ContosoKeyVault' --name 'SQLPassword' --value 'Pa$$w0rd'
```
<span data-ttu-id="a51b5-165">Ahora puede hacer referencia a esta contraseña que agregó tooAzure el almacén de claves, mediante el uso de su URI.</span><span class="sxs-lookup"><span data-stu-id="a51b5-165">You can now reference this password that you added tooAzure Key Vault, by using its URI.</span></span> <span data-ttu-id="a51b5-166">Usar **https://ContosoVault.vault.azure.net/secrets/SQLPassword** tooalways obtener la versión actual de Hola y usar **https://ContosoVault.vault.azure.net/secrets/SQLPassword/ 90018dbb96a84117a0d2847ef8e7189d** tooget esta versión específica.</span><span class="sxs-lookup"><span data-stu-id="a51b5-166">Use **https://ContosoVault.vault.azure.net/secrets/SQLPassword** tooalways get hello current version, and use **https://ContosoVault.vault.azure.net/secrets/SQLPassword/90018dbb96a84117a0d2847ef8e7189d** tooget this specific version.</span></span>

<span data-ttu-id="a51b5-167">Vamos a ver clave de Hola o el secreto que acaba de crear:</span><span class="sxs-lookup"><span data-stu-id="a51b5-167">Let's view hello key or secret that you just created:</span></span>

* <span data-ttu-id="a51b5-168">tooview el tipo de clave,:`az keyvault key list --vault-name 'ContosoKeyVault'`</span><span class="sxs-lookup"><span data-stu-id="a51b5-168">tooview your key, type: `az keyvault key list --vault-name 'ContosoKeyVault'`</span></span>
* <span data-ttu-id="a51b5-169">tooview el secreto, tipo:`az keyvault secret list --vault-name 'ContosoKeyVault'`</span><span class="sxs-lookup"><span data-stu-id="a51b5-169">tooview your secret, type: `az keyvault secret list --vault-name 'ContosoKeyVault'`</span></span>

## <a name="register-an-application-with-azure-active-directory"></a><span data-ttu-id="a51b5-170">Registro de una aplicación con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="a51b5-170">Register an application with Azure Active Directory</span></span>
<span data-ttu-id="a51b5-171">Este paso lo haría normalmente un programador en un equipo independiente.</span><span class="sxs-lookup"><span data-stu-id="a51b5-171">This step would usually be done by a developer, on a separate computer.</span></span> <span data-ttu-id="a51b5-172">No es específico tooAzure el almacén de claves, pero se incluye aquí para integridad.</span><span class="sxs-lookup"><span data-stu-id="a51b5-172">It is not specific tooAzure Key Vault but is included here, for completeness.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="a51b5-173">tutorial de hello toocomplete, tu cuenta, el almacén de Hola y aplicación hello que se registren en este paso deben ser Hola mismo directorio de Azure.</span><span class="sxs-lookup"><span data-stu-id="a51b5-173">toocomplete hello tutorial, your account, hello vault, and hello application that you will register in this step must all be in hello same Azure directory.</span></span>
>
>

<span data-ttu-id="a51b5-174">Las aplicaciones que utilizan un Almacén de claves deben autenticarse utilizando un token de Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="a51b5-174">Applications that use a key vault must authenticate by using a token from Azure Active Directory.</span></span> <span data-ttu-id="a51b5-175">toodo, Hola propietario de la aplicación hello en primer lugar debe registrar la aplicación hello en su Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="a51b5-175">toodo this, hello owner of hello application must first register hello application in their Azure Active Directory.</span></span> <span data-ttu-id="a51b5-176">Al final de Hola de registro, propietario de la aplicación hello obtiene Hola siguientes valores:</span><span class="sxs-lookup"><span data-stu-id="a51b5-176">At hello end of registration, hello application owner gets hello following values:</span></span>

* <span data-ttu-id="a51b5-177">Un **Id. de aplicación** (también conocido como un Id. de cliente) y **clave de autenticación** (también conocido como Hola secreto compartido).</span><span class="sxs-lookup"><span data-stu-id="a51b5-177">An **Application ID** (also known as a Client ID) and **authentication key** (also known as hello shared secret).</span></span> <span data-ttu-id="a51b5-178">aplicación Hello debe presentar ambos de estos tooAzure valores tooget un símbolo (token) de Active Directory.</span><span class="sxs-lookup"><span data-stu-id="a51b5-178">hello application must present both of these values tooAzure Active Directory, tooget a token.</span></span> <span data-ttu-id="a51b5-179">Forma de la aplicación hello configurado toodo que esto depende de la aplicación hello.</span><span class="sxs-lookup"><span data-stu-id="a51b5-179">How hello application is configured toodo this depends on hello application.</span></span> <span data-ttu-id="a51b5-180">Para la aplicación de ejemplo de almacén de claves de hello, propietario de la aplicación hello establece estos valores en el archivo app.config de hello.</span><span class="sxs-lookup"><span data-stu-id="a51b5-180">For hello Key Vault sample application, hello application owner sets these values in hello app.config file.</span></span>

<span data-ttu-id="a51b5-181">aplicación de hello tooregister en Azure Active Directory:</span><span class="sxs-lookup"><span data-stu-id="a51b5-181">tooregister hello application in Azure Active Directory:</span></span>

1. <span data-ttu-id="a51b5-182">Inicie sesión en toohello portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="a51b5-182">Sign in toohello Azure portal.</span></span>
2. <span data-ttu-id="a51b5-183">Hola izquierda, haga clic en **Azure Active Directory**y, a continuación, seleccione directorio de hello en el que se vaya a registrar la aplicación.</span><span class="sxs-lookup"><span data-stu-id="a51b5-183">On hello left, click **Azure Active Directory**, and then select hello directory in which you will register your application.</span></span> <br> <br> 

> [!Note] 
> <span data-ttu-id="a51b5-184">Debe seleccionar Hola mismo directorio que contiene Hola suscripción de Azure con la que se creó el almacén de claves.</span><span class="sxs-lookup"><span data-stu-id="a51b5-184">You must select hello same directory that contains hello Azure subscription with which you created your key vault.</span></span> <span data-ttu-id="a51b5-185">Si no sabe qué directorio esto es, haga clic en **configuración**, identificar suscripción Hola con la que se creó el almacén de claves y muestra el nombre de Hola de nota del directorio de hello en la última columna de Hola.</span><span class="sxs-lookup"><span data-stu-id="a51b5-185">If you do not know which directory this is, click **Settings**, identify hello subscription with which you created your key vault, and note hello name of hello directory displayed in hello last column.</span></span>

3. <span data-ttu-id="a51b5-186">Haga clic en **Aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="a51b5-186">Click **APPLICATIONS**.</span></span> <span data-ttu-id="a51b5-187">Si no hay aplicaciones se han agregado tooyour directorio, esta página mostrará solo hello **agregar una aplicación** vínculo.</span><span class="sxs-lookup"><span data-stu-id="a51b5-187">If no apps have been added tooyour directory, this page will show only hello **Add an App** link.</span></span> <span data-ttu-id="a51b5-188">Haga clic en el vínculo de Hola o, como alternativa, puede hacer clic en hello **agregar** en la barra de comandos de Hola.</span><span class="sxs-lookup"><span data-stu-id="a51b5-188">Click hello link, or alternatively, you can click hello **ADD** on hello command bar.</span></span>
4. <span data-ttu-id="a51b5-189">Hola **Agregar aplicación** asistente, en hello **especifique qué desea toodo?** página, haga clic en **agregar una aplicación que mi organización está desarrollando**.</span><span class="sxs-lookup"><span data-stu-id="a51b5-189">In hello **ADD APPLICATION** wizard, on hello **What do you want toodo?** page, click **Add an application my organization is developing**.</span></span>
5. <span data-ttu-id="a51b5-190">En hello **envíenos comentarios acerca de la aplicación** página, especifique un nombre para la aplicación y seleccione **aplicación WEB Y/O API de WEB** (Hola de forma predeterminada).</span><span class="sxs-lookup"><span data-stu-id="a51b5-190">On hello **Tell us about your application** page, specify a name for your application and select **WEB APPLICATION AND/OR WEB API** (hello default).</span></span> <span data-ttu-id="a51b5-191">Haga clic en el icono siguiente Hola.</span><span class="sxs-lookup"><span data-stu-id="a51b5-191">Click hello Next icon.</span></span>
6. <span data-ttu-id="a51b5-192">En hello **propiedades de la aplicación** página, especifique hello **dirección URL de inicio de sesión** y **APP ID URI** para la aplicación web.</span><span class="sxs-lookup"><span data-stu-id="a51b5-192">On hello **App properties** page, specify hello **SIGN-ON URL** and **APP ID URI** for your web application.</span></span> <span data-ttu-id="a51b5-193">Si la aplicación no tiene estos valores, puede inventárselos en este paso (por ejemplo, puede especificar http://test1.contoso.com en ambos cuadros).</span><span class="sxs-lookup"><span data-stu-id="a51b5-193">If your application does not have these values, you can make them up for this step (for example, you could specify http://test1.contoso.com for both boxes).</span></span> <span data-ttu-id="a51b5-194">No importa estos sitios, si existen. lo importante es que esa aplicación hello identificador URI para cada aplicación es diferente para cada aplicación en el directorio.</span><span class="sxs-lookup"><span data-stu-id="a51b5-194">It does not matter if these sites exist; what is important is that hello app ID URI for each application is different for every application in your directory.</span></span> <span data-ttu-id="a51b5-195">directorio de Hello usa este tooidentify de cadena de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="a51b5-195">hello directory uses this string tooidentify your app.</span></span>
7. <span data-ttu-id="a51b5-196">Haga clic en hello icono completa toosave los cambios en el Asistente de Hola.</span><span class="sxs-lookup"><span data-stu-id="a51b5-196">Click hello Complete icon toosave your changes in hello wizard.</span></span>
8. <span data-ttu-id="a51b5-197">En la página de inicio rápido de hello, haga clic en **configurar**.</span><span class="sxs-lookup"><span data-stu-id="a51b5-197">On hello Quick Start page, click **CONFIGURE**.</span></span>
9. <span data-ttu-id="a51b5-198">Desplácese toohello **claves** sección, seleccione la duración de hello y, a continuación, haga clic en **guardar**.</span><span class="sxs-lookup"><span data-stu-id="a51b5-198">Scroll toohello **keys** section, select hello duration, and then click **SAVE**.</span></span> <span data-ttu-id="a51b5-199">página de Hello actualiza y muestra ahora un valor de clave.</span><span class="sxs-lookup"><span data-stu-id="a51b5-199">hello page refreshes and now shows a key value.</span></span> <span data-ttu-id="a51b5-200">Debe configurar la aplicación con este valor de clave y hello **Id. de cliente** valor.</span><span class="sxs-lookup"><span data-stu-id="a51b5-200">You must configure your application with this key value and hello **CLIENT ID** value.</span></span> <span data-ttu-id="a51b5-201">(Las instrucciones para realizar esta configuración serán específicas para la aplicación).</span><span class="sxs-lookup"><span data-stu-id="a51b5-201">(Instructions for this configuration will be application-specific.)</span></span>
10. <span data-ttu-id="a51b5-202">Copie el valor de identificador de cliente de Hola desde esta página, que se usará en el siguiente paso tooset permisos de hello en el almacén.</span><span class="sxs-lookup"><span data-stu-id="a51b5-202">Copy hello client ID value from this page, which you will use in hello next step tooset permissions on your vault.</span></span>

## <a name="authorize-hello-application-toouse-hello-key-or-secret"></a><span data-ttu-id="a51b5-203">Autorizar Hola aplicación toouse Hola clave o el secreto</span><span class="sxs-lookup"><span data-stu-id="a51b5-203">Authorize hello application toouse hello key or secret</span></span>
<span data-ttu-id="a51b5-204">tooauthorize Hola aplicación tooaccess Hola clave o el secreto en el almacén de hello, use hello `az keyvault set-policy` comando.</span><span class="sxs-lookup"><span data-stu-id="a51b5-204">tooauthorize hello application tooaccess hello key or secret in hello vault, use hello `az keyvault set-policy` command.</span></span>

<span data-ttu-id="a51b5-205">Por ejemplo, si el nombre del almacén es aplicación hello y ContosoKeyVault desea tooauthorize tiene un identificador de cliente de 8f8c4bbd 485b 45fd 98f7 ec6300b7b4ed, y desea tooauthorize Hola aplicación toodecrypt e inicie sesión con las claves en el almacén, a continuación, ejecute hello Después de:</span><span class="sxs-lookup"><span data-stu-id="a51b5-205">For example, if your vault name is ContosoKeyVault and hello application you want tooauthorize has a client ID of 8f8c4bbd-485b-45fd-98f7-ec6300b7b4ed, and you want tooauthorize hello application toodecrypt and sign with keys in your vault, then run hello following:</span></span>
```
az keyvault set-policy --name 'ContosoKeyVault' --spn 8f8c4bbd-485b-45fd-98f7-ec6300b7b4ed --key-permissions decrypt sign
```

<span data-ttu-id="a51b5-206">Si desea tooauthorize ese mismo secretos tooread de aplicación en el almacén, ejecute hello siguiente:</span><span class="sxs-lookup"><span data-stu-id="a51b5-206">If you want tooauthorize that same application tooread secrets in your vault, run hello following:</span></span>
```
az keyvault set-policy --name 'ContosoKeyVault' --spn 8f8c4bbd-485b-45fd-98f7-ec6300b7b4ed --secret-permissions get
```
## <a name="if-you-want-toouse-a-hardware-security-module-hsm"></a><span data-ttu-id="a51b5-207">Si desea que toouse un módulo de seguridad de hardware (HSM)</span><span class="sxs-lookup"><span data-stu-id="a51b5-207">If you want toouse a hardware security module (HSM)</span></span>
<span data-ttu-id="a51b5-208">Para mayor seguridad, puede importar o generar claves en módulos de seguridad de hardware (HSM) que no dejan nunca el límite de HSM Hola.</span><span class="sxs-lookup"><span data-stu-id="a51b5-208">For added assurance, you can import or generate keys in hardware security modules (HSMs) that never leave hello HSM boundary.</span></span> <span data-ttu-id="a51b5-209">Hola HSM son FIPS 140-2 nivel 2 validado.</span><span class="sxs-lookup"><span data-stu-id="a51b5-209">hello HSMs are FIPS 140-2 Level 2 validated.</span></span> <span data-ttu-id="a51b5-210">Si este requisito no aplica tooyou, omita esta sección y vaya demasiado[eliminar el almacén de claves de Hola y las claves asociadas y secretos](#delete-the-key-vault-and-associated-keys-and-secrets).</span><span class="sxs-lookup"><span data-stu-id="a51b5-210">If this requirement doesn't apply tooyou, skip this section and go too[Delete hello key vault and associated keys and secrets](#delete-the-key-vault-and-associated-keys-and-secrets).</span></span>

<span data-ttu-id="a51b5-211">toocreate estas claves protegidas con HSM, debe tener una suscripción de almacén que admita claves protegidas con HSM.</span><span class="sxs-lookup"><span data-stu-id="a51b5-211">toocreate these HSM-protected keys, you must have a vault subscription that supports HSM-protected keys.</span></span>

<span data-ttu-id="a51b5-212">Cuando creas hello keyvault, Agregar parámetro de "sku" hello:</span><span class="sxs-lookup"><span data-stu-id="a51b5-212">When you create hello keyvault, add hello 'sku' parameter:</span></span>

```
az keyvault create --name 'ContosoKeyVaultHSM' --resource-group 'ContosoResourceGroup' --location 'East Asia' --sku 'Premium'
```
<span data-ttu-id="a51b5-213">Puede agregar las claves protegidas por software (como se muestra anteriormente) y del almacén de claves protegidas con HSM toothis.</span><span class="sxs-lookup"><span data-stu-id="a51b5-213">You can add software-protected keys (as shown earlier) and HSM-protected keys toothis vault.</span></span> <span data-ttu-id="a51b5-214">toocreate una clave protegida por HSM, too'HSM del parámetro de destino de conjunto hello':</span><span class="sxs-lookup"><span data-stu-id="a51b5-214">toocreate an HSM-protected key, set hello Destination parameter too'HSM':</span></span>

```
az keyvault key create --vault-name 'ContosoKeyVaultHSM' --name 'ContosoFirstHSMKey' --protection 'hsm'
```

<span data-ttu-id="a51b5-215">Puede usar Hola siguientes comando tooimport una clave de un archivo PEM en el equipo.</span><span class="sxs-lookup"><span data-stu-id="a51b5-215">You can use hello following command tooimport a key from a .pem file on your computer.</span></span> <span data-ttu-id="a51b5-216">Este comando importa una clave hello en HSM Hola servicio Almacén de claves:</span><span class="sxs-lookup"><span data-stu-id="a51b5-216">This command imports hello key into HSMs in hello Key Vault service:</span></span>

```
az keyvault key import --vault-name 'ContosoKeyVaultHSM' --name 'ContosoFirstHSMKey' --pem-file '/.softkey.pem' --protection 'hsm' --pem-password 'PaSSWORD'
```
<span data-ttu-id="a51b5-217">comando siguiente de Hello importa una opción "traiga su propia clave" paquete (BYOK).</span><span class="sxs-lookup"><span data-stu-id="a51b5-217">hello next command imports a “bring your own key" (BYOK) package.</span></span> <span data-ttu-id="a51b5-218">Esto le permite generar su clave de HSM local y se transfiere tooHSMs Hola servicio de almacén de claves, sin clave Hola dejando límite de HSM hello:</span><span class="sxs-lookup"><span data-stu-id="a51b5-218">This lets you generate your key in your local HSM, and transfer it tooHSMs in hello Key Vault service, without hello key leaving hello HSM boundary:</span></span>

```
az keyvault key import --vault-name 'ContosoKeyVaultHSM' --name 'ContosoFirstHSMKey' --byok-file './ITByok.byok' --protection 'hsm'
```
<span data-ttu-id="a51b5-219">Para obtener más instrucciones sobre cómo toogenerate este paquete BYOK, vea [cómo toouse HSM-Protected claves al almacén de claves de Azure](key-vault-hsm-protected-keys.md).</span><span class="sxs-lookup"><span data-stu-id="a51b5-219">For more detailed instructions about how toogenerate this BYOK package, see [How toouse HSM-Protected Keys with Azure Key Vault](key-vault-hsm-protected-keys.md).</span></span>

## <a name="delete-hello-key-vault-and-associated-keys-and-secrets"></a><span data-ttu-id="a51b5-220">Eliminar el almacén de claves de Hola y las claves asociadas y secretos</span><span class="sxs-lookup"><span data-stu-id="a51b5-220">Delete hello key vault and associated keys and secrets</span></span>
<span data-ttu-id="a51b5-221">Si ya no necesita el almacén de claves hello y clave de Hola o al secreto que contiene, puede eliminar el almacén de claves hello mediante hello `az keyvault delete` comando:</span><span class="sxs-lookup"><span data-stu-id="a51b5-221">If you no longer need hello key vault and hello key or secret that it contains, you can delete hello key vault by using hello `az keyvault delete` command:</span></span>

```
az keyvault delete --name 'ContosoKeyVault'
```

<span data-ttu-id="a51b5-222">O bien, puede eliminar un grupo de recursos de Azure completo, que incluye el almacén de claves de Hola y otros recursos que incluyen en ese grupo:</span><span class="sxs-lookup"><span data-stu-id="a51b5-222">Or, you can delete an entire Azure resource group, which includes hello key vault and any other resources that you included in that group:</span></span>

```
az group delete --name 'ContosoResourceGroup'
```

## <a name="other-azure-cross-platform-command-line-interface-commands"></a><span data-ttu-id="a51b5-223">Otros comandos de la interfaz de la línea de comandos entre plataformas de Azure</span><span class="sxs-lookup"><span data-stu-id="a51b5-223">Other Azure Cross-Platform Command-line Interface Commands</span></span>
<span data-ttu-id="a51b5-224">Estos son otros comandos que pueden resultar útiles para administrar el Almacén de claves de Azure.</span><span class="sxs-lookup"><span data-stu-id="a51b5-224">Other commands that you might useful for managing Azure Key Vault.</span></span>

<span data-ttu-id="a51b5-225">Este comando ofrece una presentación tabular de todas las claves y las propiedades seleccionadas.</span><span class="sxs-lookup"><span data-stu-id="a51b5-225">This command lists a tabular display of all keys and selected properties:</span></span>

<span data-ttu-id="a51b5-226">az keyvault key list --vault-name 'ContosoKeyVault'</span><span class="sxs-lookup"><span data-stu-id="a51b5-226">az keyvault key list --vault-name 'ContosoKeyVault'</span></span>

<span data-ttu-id="a51b5-227">Este comando muestra una lista completa de propiedades para la clave especificada de hello:</span><span class="sxs-lookup"><span data-stu-id="a51b5-227">This command displays a full list of properties for hello specified key:</span></span>

<span data-ttu-id="a51b5-228">az keyvault key show --vault-name 'ContosoKeyVault' --name 'ContosoFirstKey'</span><span class="sxs-lookup"><span data-stu-id="a51b5-228">az keyvault key show --vault-name 'ContosoKeyVault' --name 'ContosoFirstKey'</span></span>

<span data-ttu-id="a51b5-229">Este comando muestra una presentación tabular de todos nombres de secretos y las propiedades que se elijan.</span><span class="sxs-lookup"><span data-stu-id="a51b5-229">This command lists a tabular display of all secret names and selected properties:</span></span>

<span data-ttu-id="a51b5-230">az keyvault secret list --vault-name 'ContosoKeyVault'</span><span class="sxs-lookup"><span data-stu-id="a51b5-230">az keyvault secret list --vault-name 'ContosoKeyVault'</span></span>

<span data-ttu-id="a51b5-231">Este es un ejemplo de cómo tooremove una clave específica:</span><span class="sxs-lookup"><span data-stu-id="a51b5-231">Here's an example of how tooremove a specific key:</span></span>

<span data-ttu-id="a51b5-232">az keyvault key delete --vault-name 'ContosoKeyVault' --name 'ContosoFirstKey'</span><span class="sxs-lookup"><span data-stu-id="a51b5-232">az keyvault key delete --vault-name 'ContosoKeyVault' --name 'ContosoFirstKey'</span></span>

<span data-ttu-id="a51b5-233">Este es un ejemplo de cómo tooremove un secreto específico:</span><span class="sxs-lookup"><span data-stu-id="a51b5-233">Here's an example of how tooremove a specific secret:</span></span>

<span data-ttu-id="a51b5-234">az keyvault secret delete --vault-name 'ContosoKeyVault' --name 'SQLPassword'</span><span class="sxs-lookup"><span data-stu-id="a51b5-234">az keyvault secret delete --vault-name 'ContosoKeyVault' --name 'SQLPassword'</span></span>


## <a name="next-steps"></a><span data-ttu-id="a51b5-235">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="a51b5-235">Next steps</span></span>
<span data-ttu-id="a51b5-236">Para ver una referencia completa de CLI de Azure para los comandos de Key Vault, consulte la [guía de referencia de la CLI de Key Vault](/cli/azure/keyvault).</span><span class="sxs-lookup"><span data-stu-id="a51b5-236">For complete Azure CLI reference for key vault commands, see [Key Vault CLI reference](/cli/azure/keyvault)</span></span>

<span data-ttu-id="a51b5-237">Para las referencias de programación, vea [Hola Guía del desarrollador de almacén de claves de Azure](key-vault-developers-guide.md).</span><span class="sxs-lookup"><span data-stu-id="a51b5-237">For programming references, see [hello Azure Key Vault developer's guide](key-vault-developers-guide.md).</span></span>
