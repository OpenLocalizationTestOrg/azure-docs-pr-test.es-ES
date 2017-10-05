---
title: "Administración de Azure Key Vault mediante CLI | Microsoft Docs"
description: Use este tutorial para automatizar tareas comunes en Key Vault mediante la CLI 2.0.
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
ms.openlocfilehash: 5da9f5eceda71ac85259193e0f183c72813e1679
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="manage-key-vault-using-cli-20"></a><span data-ttu-id="e1e8c-103">Administración de Key Vault mediante CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="e1e8c-103">Manage Key Vault using CLI 2.0</span></span>
<span data-ttu-id="e1e8c-104">Almacén de claves de Azure está disponible en la mayoría de las regiones.</span><span class="sxs-lookup"><span data-stu-id="e1e8c-104">Azure Key Vault is available in most regions.</span></span> <span data-ttu-id="e1e8c-105">Para obtener más información, consulte la [página de precios del Almacén de claves](https://azure.microsoft.com/pricing/details/key-vault/).</span><span class="sxs-lookup"><span data-stu-id="e1e8c-105">For more information, see the [Key Vault pricing page](https://azure.microsoft.com/pricing/details/key-vault/).</span></span>

## <a name="introduction"></a><span data-ttu-id="e1e8c-106">Introducción</span><span class="sxs-lookup"><span data-stu-id="e1e8c-106">Introduction</span></span>
<span data-ttu-id="e1e8c-107">Use este tutorial para empezar a trabajar con el Almacén de claves de Azure para crear un contenedor (un almacén) reforzado en Azure en el que almacenar y administrar las claves criptográficas y los secretos en Azure.</span><span class="sxs-lookup"><span data-stu-id="e1e8c-107">Use this tutorial to help you get started with Azure Key Vault to create a hardened container (a vault) in Azure, to store and manage cryptographic keys and secrets in Azure.</span></span> <span data-ttu-id="e1e8c-108">Se describe el proceso para usar la interfaz de la línea de comandos entre plataformas de Azure fin de crear un almacén en el que se guardará una clave o una contraseña para usarla con una aplicación de Azure.</span><span class="sxs-lookup"><span data-stu-id="e1e8c-108">It walks you through the process of using Azure Cross-Platform Command-Line Interface to create a vault that contains a key or password that you can then use with an Azure application.</span></span> <span data-ttu-id="e1e8c-109">A continuación, se explica cómo utiliza una aplicación esa clave o contraseña.</span><span class="sxs-lookup"><span data-stu-id="e1e8c-109">It then shows you how an application can then use that key or password.</span></span>

<span data-ttu-id="e1e8c-110">**Tiempo estimado para completar el tutorial:** 20 minutos</span><span class="sxs-lookup"><span data-stu-id="e1e8c-110">**Estimated time to complete:** 20 minutes</span></span>

> [!NOTE]
> <span data-ttu-id="e1e8c-111">Este tutorial no incluye instrucciones sobre cómo escribir la aplicación de Azure incluida en uno de los pasos, en el que se muestra cómo autorizar a una aplicación para que use una clave o un secreto del Almacén de claves.</span><span class="sxs-lookup"><span data-stu-id="e1e8c-111">This tutorial does not include instructions on how to write the Azure application that one of the steps includes, which shows how to authorize an application to use a key or secret in the key vault.</span></span>
>
> <span data-ttu-id="e1e8c-112">Este tutorial usa la CLI 2.0 de Azure más reciente.</span><span class="sxs-lookup"><span data-stu-id="e1e8c-112">This tutorial uses the latest Azure CLI 2.0.</span></span>
>
>

<span data-ttu-id="e1e8c-113">Para obtener información general sobre el Almacén de claves de Azure, consulte [¿Qué es el Almacén de clave de Azure?](key-vault-whatis.md)</span><span class="sxs-lookup"><span data-stu-id="e1e8c-113">For overview information about Azure Key Vault, see [What is Azure Key Vault?](key-vault-whatis.md)</span></span>

## <a name="prerequisites"></a><span data-ttu-id="e1e8c-114">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="e1e8c-114">Prerequisites</span></span>
<span data-ttu-id="e1e8c-115">Para realizar este tutorial, necesitará lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="e1e8c-115">To complete this tutorial, you must have the following:</span></span>

* <span data-ttu-id="e1e8c-116">Una suscripción a Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="e1e8c-116">A subscription to Microsoft Azure.</span></span> <span data-ttu-id="e1e8c-117">Si no tiene una, puede registrarse para obtener una versión de [evaluación gratuita](https://azure.microsoft.com/pricing/free-trial).</span><span class="sxs-lookup"><span data-stu-id="e1e8c-117">If you do not have one, you can sign up for a [free trial](https://azure.microsoft.com/pricing/free-trial).</span></span>
* <span data-ttu-id="e1e8c-118">Versión 2.0 de la interfaz de la línea de comandos o posterior.</span><span class="sxs-lookup"><span data-stu-id="e1e8c-118">Command-Line Interface version 2.0 or later.</span></span> <span data-ttu-id="e1e8c-119">Para instalar la última versión y conectarla a su suscripción de Azure, consulte el artículo sobre la [instalación y configuración de la interfaz de la línea de comandos 2.0 entre plataformas de Azure](/cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="e1e8c-119">To install the latest version and connect to your Azure subscription, see [Install and Configure the Azure Cross-Platform Command-Line Interface 2.0](/cli/azure/install-azure-cli).</span></span>
* <span data-ttu-id="e1e8c-120">Una aplicación que se configurará para utilizar la clave o contraseña creada en este tutorial.</span><span class="sxs-lookup"><span data-stu-id="e1e8c-120">An application that will be configured to use the key or password that you create in this tutorial.</span></span> <span data-ttu-id="e1e8c-121">Hay una aplicación de ejemplo disponible en el [Centro de descarga de Microsoft](http://www.microsoft.com/download/details.aspx?id=45343).</span><span class="sxs-lookup"><span data-stu-id="e1e8c-121">A sample application is available from the [Microsoft Download Center](http://www.microsoft.com/download/details.aspx?id=45343).</span></span> <span data-ttu-id="e1e8c-122">Para obtener instrucciones, consulte el archivo Léame adjunto.</span><span class="sxs-lookup"><span data-stu-id="e1e8c-122">For instructions, see the accompanying Readme file.</span></span>

## <a name="getting-help-with-azure-cross-platform-command-line-interface"></a><span data-ttu-id="e1e8c-123">Obtención de ayuda con la interfaz de la línea de comandos entre plataformas de Azure</span><span class="sxs-lookup"><span data-stu-id="e1e8c-123">Getting help with Azure Cross-Platform Command-Line Interface</span></span>
<span data-ttu-id="e1e8c-124">Este tutorial asume que está familiarizado con la interfaz de la línea de comandos (Bash, Terminal, símbolo del sistema).</span><span class="sxs-lookup"><span data-stu-id="e1e8c-124">This tutorial assumes that you are familiar with the command-line interface (Bash, Terminal, Command prompt)</span></span>

<span data-ttu-id="e1e8c-125">Los parámetros --help o -h se pueden usar para ver la ayuda de comandos específicos.</span><span class="sxs-lookup"><span data-stu-id="e1e8c-125">The --help or -h parameter can be used to view help for specific commands.</span></span> <span data-ttu-id="e1e8c-126">También puede usar el formato azure help [command] [options] para devolver la misma información.</span><span class="sxs-lookup"><span data-stu-id="e1e8c-126">Alternately, The azure help [command] [options] format can also be used to return the same information.</span></span> <span data-ttu-id="e1e8c-127">Por ejemplo, todos los comandos siguientes devuelven la misma información:</span><span class="sxs-lookup"><span data-stu-id="e1e8c-127">For example, the following commands all return the same information:</span></span>

```
az account set --help
az account set -h
```

<span data-ttu-id="e1e8c-128">Si duda sobre los parámetros que necesita un comando, consulte la ayuda usando --help, -h o az help [comando].</span><span class="sxs-lookup"><span data-stu-id="e1e8c-128">When in doubt about the parameters needed by a command, refer to help using --help, -h or az help [command].</span></span>

<span data-ttu-id="e1e8c-129">También puede leer los tutoriales siguientes para familiarizarse con el Administrador de recursos de Azure en la interfaz de la línea de comandos entre plataformas de Azure:</span><span class="sxs-lookup"><span data-stu-id="e1e8c-129">You can also read the following tutorials to get familiar with Azure Resource Manager in Azure Cross-Platform Command-Line Interface:</span></span>

* [<span data-ttu-id="e1e8c-130">Instalación de la CLI de Azure</span><span class="sxs-lookup"><span data-stu-id="e1e8c-130">Install Azure CLI</span></span>](/cli/azure/install-azure-cli)
* [<span data-ttu-id="e1e8c-131">Introducción a la CLI de Azure 2.0</span><span class="sxs-lookup"><span data-stu-id="e1e8c-131">Get started with Azure CLI 2.0</span></span>](/cli/azure/get-started-with-azure-cli)

## <a name="connect-to-your-subscriptions"></a><span data-ttu-id="e1e8c-132">Conectarse a sus suscripciones</span><span class="sxs-lookup"><span data-stu-id="e1e8c-132">Connect to your subscriptions</span></span>
<span data-ttu-id="e1e8c-133">Para iniciar sesión usando una cuenta profesional, utilice el comando siguiente:</span><span class="sxs-lookup"><span data-stu-id="e1e8c-133">To log in using an organizational account, use the following command:</span></span>

```
az login -u username@domain.com -p password
```

<span data-ttu-id="e1e8c-134">o si desea iniciar sesión escribiendo interactivamente</span><span class="sxs-lookup"><span data-stu-id="e1e8c-134">or if you want to log in by typing interactively</span></span>

```
az login
```

<span data-ttu-id="e1e8c-135">Si tiene varias suscripciones y desea especificar una en concreto para que use el Almacén de claves de Azure, escriba lo siguiente para ver las suscripciones de su cuenta:</span><span class="sxs-lookup"><span data-stu-id="e1e8c-135">If you have multiple subscriptions and want to specify a specific one to use for Azure Key Vault, type the following to see the subscriptions for your account:</span></span>

```
az account list
```

<span data-ttu-id="e1e8c-136">A continuación, para especificar la suscripción que se debe usar, escriba:</span><span class="sxs-lookup"><span data-stu-id="e1e8c-136">Then, to specify the subscription to use, type:</span></span>

```
az account set --subscription <subscription name or ID>
```

<span data-ttu-id="e1e8c-137">Para más información acerca de cómo configurar la interfaz de la línea de comandos entre plataformas de Azure, consulte el artículo sobre la [instalación de la CLI de Azure](/cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="e1e8c-137">For more information about configuring Azure Cross-Platform Command-Line Interface, see [Install Azure CLI](/cli/azure/install-azure-cli).</span></span>

## <a name="create-a-new-resource-group"></a><span data-ttu-id="e1e8c-138">Creación de un nuevo grupo de recursos</span><span class="sxs-lookup"><span data-stu-id="e1e8c-138">Create a new resource group</span></span>
<span data-ttu-id="e1e8c-139">Cuando se utiliza el Administrador de recursos de Azure, todos los recursos relacionados se crean dentro de un grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="e1e8c-139">When using Azure Resource Manager, all related resources are created inside a resource group.</span></span> <span data-ttu-id="e1e8c-140">Crearemos un nuevo grupo de recursos denominado 'ContosoResourceGroup' para este tutorial.</span><span class="sxs-lookup"><span data-stu-id="e1e8c-140">We will create a new resource group 'ContosoResourceGroup' for this tutorial.</span></span>

```
az group create -n 'ContosoResourceGroup' -l 'East Asia'
```

<span data-ttu-id="e1e8c-141">El primer parámetro es el nombre del grupo de recursos y el segundo parámetro es la ubicación.</span><span class="sxs-lookup"><span data-stu-id="e1e8c-141">The first parameter is resource group name and the second parameter is the location.</span></span> <span data-ttu-id="e1e8c-142">Para la ubicación, use el comando `az account list-locations` para identificar cómo se debe especificar una ubicación alternativa a la usada en este ejemplo.</span><span class="sxs-lookup"><span data-stu-id="e1e8c-142">For location, use the command `az account list-locations` to identify how to specify an alternative location to the one in this example.</span></span> <span data-ttu-id="e1e8c-143">Si necesita más información, escriba: `az account list-locations -h`.</span><span class="sxs-lookup"><span data-stu-id="e1e8c-143">If you need more information, type: `az account list-locations -h`.</span></span>

## <a name="register-the-key-vault-resource-provider"></a><span data-ttu-id="e1e8c-144">Registro del proveedor de recursos de Almacén de claves</span><span class="sxs-lookup"><span data-stu-id="e1e8c-144">Register the Key Vault resource provider</span></span>
<span data-ttu-id="e1e8c-145">Asegúrese de que el proveedor de recursos de Almacén de claves está registrado en la suscripción:</span><span class="sxs-lookup"><span data-stu-id="e1e8c-145">Make sure that Key Vault resource provider is registered in your subscription:</span></span>

```
az provider register -n Microsoft.KeyVault
```

<span data-ttu-id="e1e8c-146">Esto solo se debe hacer una vez por suscripción.</span><span class="sxs-lookup"><span data-stu-id="e1e8c-146">This only needs to be done once per subscription.</span></span>

## <a name="create-a-key-vault"></a><span data-ttu-id="e1e8c-147">Creación de un Almacén de claves</span><span class="sxs-lookup"><span data-stu-id="e1e8c-147">Create a key vault</span></span>
<span data-ttu-id="e1e8c-148">Utilice el comando `az keyvault create` para crear un Almacén de claves.</span><span class="sxs-lookup"><span data-stu-id="e1e8c-148">Use the `az keyvault create` command to create a key vault.</span></span> <span data-ttu-id="e1e8c-149">Este script tiene tres parámetros obligatorios: el nombre del grupo de recursos, el nombre del Almacén de claves y la ubicación geográfica.</span><span class="sxs-lookup"><span data-stu-id="e1e8c-149">This script has three mandatory parameters: a resource group name, a key vault name, and the geographic location.</span></span>

<span data-ttu-id="e1e8c-150">Por ejemplo, si utiliza el nombre del almacén de ContosoKeyVault, el nombre del grupo de recursos ContosoResourceGroup y la ubicación East Asia, deberá escribir:</span><span class="sxs-lookup"><span data-stu-id="e1e8c-150">For example, if you use the vault name of ContosoKeyVault, the resource group name of ContosoResourceGroup, and the location of East Asia, type:</span></span>
```
az keyvault create --name 'ContosoKeyVault' --resource-group 'ContosoResourceGroup' --location 'East Asia'
```

<span data-ttu-id="e1e8c-151">El resultado de este comando muestra las propiedades del Almacén de claves que acaba de crear.</span><span class="sxs-lookup"><span data-stu-id="e1e8c-151">The output of this command shows properties of the key vault that you've just created.</span></span> <span data-ttu-id="e1e8c-152">Las dos propiedades más importantes son:</span><span class="sxs-lookup"><span data-stu-id="e1e8c-152">The two most important properties are:</span></span>

* <span data-ttu-id="e1e8c-153">**name**: en este ejemplo, el nombre es ContosoKeyVault.</span><span class="sxs-lookup"><span data-stu-id="e1e8c-153">**name**: In the example this is ContosoKeyVault.</span></span> <span data-ttu-id="e1e8c-154">Utilizará este nombre para otros comandos de Key Vault.</span><span class="sxs-lookup"><span data-stu-id="e1e8c-154">You will use this name for other Key Vault commands.</span></span>
* <span data-ttu-id="e1e8c-155">**vaultUri**: en este ejemplo es https://contosokeyvault.vault.azure.net.</span><span class="sxs-lookup"><span data-stu-id="e1e8c-155">**vaultUri**: In the example this is https://contosokeyvault.vault.azure.net.</span></span> <span data-ttu-id="e1e8c-156">Las aplicaciones que utilizan el almacén a través de su API de REST deben usar este identificador URI.</span><span class="sxs-lookup"><span data-stu-id="e1e8c-156">Applications that use your vault through its REST API must use this URI.</span></span>

<span data-ttu-id="e1e8c-157">Su cuenta de Azure ahora está autorizada para realizar operaciones en este Almacén de claves.</span><span class="sxs-lookup"><span data-stu-id="e1e8c-157">Your Azure account is now authorized to perform any operations on this key vault.</span></span> <span data-ttu-id="e1e8c-158">Hasta el momento, nadie más lo está.</span><span class="sxs-lookup"><span data-stu-id="e1e8c-158">As yet, nobody else is.</span></span>

## <a name="add-a-key-or-secret-to-the-key-vault"></a><span data-ttu-id="e1e8c-159">Adición de una clave o un secreto al Almacén de claves</span><span class="sxs-lookup"><span data-stu-id="e1e8c-159">Add a key or secret to the key vault</span></span>
<span data-ttu-id="e1e8c-160">Si desea que el Almacén de claves de Azure cree una clave protegida mediante software, utilice el comando `az key create` y escriba lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="e1e8c-160">If you want Azure Key Vault to create a software-protected key for you, use the `az key create` command, and type the following:</span></span>
```
az keyvault key create --vault-name 'ContosoKeyVault' --name 'ContosoFirstKey' --protection software
```
<span data-ttu-id="e1e8c-161">Sin embargo, si tiene una clave existente en un archivo .pem guardado como archivo local en un archivo denominado softkey.pem que desea cargar en el Almacén de claves de Azure, escriba lo siguiente para importar la clave desde el archivo .PEM, que protege la clave de software en el servicio de Almacén de claves:</span><span class="sxs-lookup"><span data-stu-id="e1e8c-161">However, if you have an existing key in a .pem file saved as local file in a file named softkey.pem that you want to upload to Azure Key Vault, type the following to import the key from the .PEM file, which protects the key by software in the Key Vault service:</span></span>
```
az keyvault key import --vault-name 'ContosoKeyVault' --name 'ContosoFirstKey' --pem-file './softkey.pem' --pem-password 'PaSSWORD' --protection software
```
<span data-ttu-id="e1e8c-162">Ahora puede utilizar el URI para hacer referencia a la clave que creó o cargó en el Almacén de claves de Azure.</span><span class="sxs-lookup"><span data-stu-id="e1e8c-162">You can now reference the key that you created or uploaded to Azure Key Vault, by using its URI.</span></span> <span data-ttu-id="e1e8c-163">Use **https://ContosoKeyVault.vault.azure.net/keys/ContosoFirstKey** para obtener siempre la versión actual y **https://ContosoKeyVault.vault.azure.net/keys/ContosoFirstKey/cgacf4f763ar42ffb0a1gca546aygd87** para obtener esta versión concreta.</span><span class="sxs-lookup"><span data-stu-id="e1e8c-163">Use  **https://ContosoKeyVault.vault.azure.net/keys/ContosoFirstKey** to always get the current version, and use **https://ContosoKeyVault.vault.azure.net/keys/ContosoFirstKey/cgacf4f763ar42ffb0a1gca546aygd87** to get this specific version.</span></span>

<span data-ttu-id="e1e8c-164">Para agregar un secreto, que es una contraseña denominada SQLPassword con el valor Pa$$w0rd, al Almacén de claves de Azure, escriba lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="e1e8c-164">To add a secret to the vault, which is a password named SQLPassword and that has the value of Pa$$w0rd to Azure Key Vault, type the following:</span></span>
```
az keyvault secret set --vault-name 'ContosoKeyVault' --name 'SQLPassword' --value 'Pa$$w0rd'
```
<span data-ttu-id="e1e8c-165">Ahora puede hacer referencia a esta clave que agregó al Almacén de claves de Azure utilizando su URI.</span><span class="sxs-lookup"><span data-stu-id="e1e8c-165">You can now reference this password that you added to Azure Key Vault, by using its URI.</span></span> <span data-ttu-id="e1e8c-166">Utilice **https://ContosoVault.vault.azure.net/secrets/SQLPassword** para obtener siempre la versión actual y **https://ContosoVault.vault.azure.net/secrets/SQLPassword/90018dbb96a84117a0d2847ef8e7189d** para obtener esta versión concreta.</span><span class="sxs-lookup"><span data-stu-id="e1e8c-166">Use **https://ContosoVault.vault.azure.net/secrets/SQLPassword** to always get the current version, and use **https://ContosoVault.vault.azure.net/secrets/SQLPassword/90018dbb96a84117a0d2847ef8e7189d** to get this specific version.</span></span>

<span data-ttu-id="e1e8c-167">Veamos la clave o el secreto que acaba de crear:</span><span class="sxs-lookup"><span data-stu-id="e1e8c-167">Let's view the key or secret that you just created:</span></span>

* <span data-ttu-id="e1e8c-168">Para ver la clave, escriba: `az keyvault key list --vault-name 'ContosoKeyVault'`</span><span class="sxs-lookup"><span data-stu-id="e1e8c-168">To view your key, type: `az keyvault key list --vault-name 'ContosoKeyVault'`</span></span>
* <span data-ttu-id="e1e8c-169">Para ver el secreto, escriba: `az keyvault secret list --vault-name 'ContosoKeyVault'`</span><span class="sxs-lookup"><span data-stu-id="e1e8c-169">To view your secret, type: `az keyvault secret list --vault-name 'ContosoKeyVault'`</span></span>

## <a name="register-an-application-with-azure-active-directory"></a><span data-ttu-id="e1e8c-170">Registro de una aplicación con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="e1e8c-170">Register an application with Azure Active Directory</span></span>
<span data-ttu-id="e1e8c-171">Este paso lo haría normalmente un programador en un equipo independiente.</span><span class="sxs-lookup"><span data-stu-id="e1e8c-171">This step would usually be done by a developer, on a separate computer.</span></span> <span data-ttu-id="e1e8c-172">No es específico del Almacén de claves de Azure, pero se incluye aquí a fin de que la información ofrecida sea lo más completa posible.</span><span class="sxs-lookup"><span data-stu-id="e1e8c-172">It is not specific to Azure Key Vault but is included here, for completeness.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="e1e8c-173">Para finalizar el tutorial, la cuenta, el almacén y la aplicación que vaya a registrar en este paso deben estar en el mismo directorio de Azure.</span><span class="sxs-lookup"><span data-stu-id="e1e8c-173">To complete the tutorial, your account, the vault, and the application that you will register in this step must all be in the same Azure directory.</span></span>
>
>

<span data-ttu-id="e1e8c-174">Las aplicaciones que utilizan un Almacén de claves deben autenticarse utilizando un token de Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="e1e8c-174">Applications that use a key vault must authenticate by using a token from Azure Active Directory.</span></span> <span data-ttu-id="e1e8c-175">Para ello, el propietario de la aplicación debe registrarla primero en su Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="e1e8c-175">To do this, the owner of the application must first register the application in their Azure Active Directory.</span></span> <span data-ttu-id="e1e8c-176">Al final del registro, el propietario de la aplicación obtiene los valores siguientes:</span><span class="sxs-lookup"><span data-stu-id="e1e8c-176">At the end of registration, the application owner gets the following values:</span></span>

* <span data-ttu-id="e1e8c-177">Un **identificador de la aplicación** (también conocido como un identificador de cliente) y una **clave de autenticación** (también conocida como secreto compartido).</span><span class="sxs-lookup"><span data-stu-id="e1e8c-177">An **Application ID** (also known as a Client ID) and **authentication key** (also known as the shared secret).</span></span> <span data-ttu-id="e1e8c-178">Para obtener un token, la aplicación debe presentar estos dos valores a Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="e1e8c-178">The application must present both of these values to Azure Active Directory, to get a token.</span></span> <span data-ttu-id="e1e8c-179">La forma en que se configura la aplicación para ello depende de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="e1e8c-179">How the application is configured to do this depends on the application.</span></span> <span data-ttu-id="e1e8c-180">Para la aplicación de ejemplo del Almacén de claves, el propietario de la aplicación establece estos valores en el archivo app.config.</span><span class="sxs-lookup"><span data-stu-id="e1e8c-180">For the Key Vault sample application, the application owner sets these values in the app.config file.</span></span>

<span data-ttu-id="e1e8c-181">Para registrar la aplicación en Azure Active Directory:</span><span class="sxs-lookup"><span data-stu-id="e1e8c-181">To register the application in Azure Active Directory:</span></span>

1. <span data-ttu-id="e1e8c-182">Inicie sesión en el Portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="e1e8c-182">Sign in to the Azure portal.</span></span>
2. <span data-ttu-id="e1e8c-183">A la izquierda, haga clic en **Azure Active Directory** y seleccione el directorio en el que va a registrar la aplicación.</span><span class="sxs-lookup"><span data-stu-id="e1e8c-183">On the left, click **Azure Active Directory**, and then select the directory in which you will register your application.</span></span> <br> <br> 

> [!Note] 
> <span data-ttu-id="e1e8c-184">Debe seleccionar el mismo directorio que contiene la suscripción de Azure con la que creó la instancia de Key Vault.</span><span class="sxs-lookup"><span data-stu-id="e1e8c-184">You must select the same directory that contains the Azure subscription with which you created your key vault.</span></span> <span data-ttu-id="e1e8c-185">Si no sabe qué directorio es, haga clic en **Configuración**, identifique la suscripción con la que creó la instancia de Key Vault y anote el nombre del directorio que se muestra en la última columna.</span><span class="sxs-lookup"><span data-stu-id="e1e8c-185">If you do not know which directory this is, click **Settings**, identify the subscription with which you created your key vault, and note the name of the directory displayed in the last column.</span></span>

3. <span data-ttu-id="e1e8c-186">Haga clic en **Aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="e1e8c-186">Click **APPLICATIONS**.</span></span> <span data-ttu-id="e1e8c-187">Si no se han agregado aplicaciones a su directorio, esta página muestra solo el vínculo **Agregar una aplicación** .</span><span class="sxs-lookup"><span data-stu-id="e1e8c-187">If no apps have been added to your directory, this page will show only the **Add an App** link.</span></span> <span data-ttu-id="e1e8c-188">Haga clic en el vínculo, o como alternativa, puede hacer clic en **Agregar** en la barra de comandos.</span><span class="sxs-lookup"><span data-stu-id="e1e8c-188">Click the link, or alternatively, you can click the **ADD** on the command bar.</span></span>
4. <span data-ttu-id="e1e8c-189">En el Asistente para **agregar aplicaciones**, en la página **¿Qué desea hacer?**, haga clic en **Agregar una aplicación que mi organización está desarrollando**.</span><span class="sxs-lookup"><span data-stu-id="e1e8c-189">In the **ADD APPLICATION** wizard, on the **What do you want to do?** page, click **Add an application my organization is developing**.</span></span>
5. <span data-ttu-id="e1e8c-190">En la página **Proporcione información sobre su aplicación**, especifique un nombre para la aplicación y seleccione **Aplicación web y/o API web** (valor predeterminado).</span><span class="sxs-lookup"><span data-stu-id="e1e8c-190">On the **Tell us about your application** page, specify a name for your application and select **WEB APPLICATION AND/OR WEB API** (the default).</span></span> <span data-ttu-id="e1e8c-191">Haga clic en el icono Siguiente.</span><span class="sxs-lookup"><span data-stu-id="e1e8c-191">Click the Next icon.</span></span>
6. <span data-ttu-id="e1e8c-192">En la página **Agregar propiedades**, especifique los valores de **URL de inicio de sesión** y **URI de id. de aplicación** para la aplicación web.</span><span class="sxs-lookup"><span data-stu-id="e1e8c-192">On the **App properties** page, specify the **SIGN-ON URL** and **APP ID URI** for your web application.</span></span> <span data-ttu-id="e1e8c-193">Si la aplicación no tiene estos valores, puede inventárselos en este paso (por ejemplo, puede especificar http://test1.contoso.com en ambos cuadros).</span><span class="sxs-lookup"><span data-stu-id="e1e8c-193">If your application does not have these values, you can make them up for this step (for example, you could specify http://test1.contoso.com for both boxes).</span></span> <span data-ttu-id="e1e8c-194">No importa si estos sitios existen; lo importante es que el URI del identificador de la aplicación de cada aplicación sea diferente en cada aplicación del directorio.</span><span class="sxs-lookup"><span data-stu-id="e1e8c-194">It does not matter if these sites exist; what is important is that the app ID URI for each application is different for every application in your directory.</span></span> <span data-ttu-id="e1e8c-195">El directorio utiliza esta cadena para identificar la aplicación.</span><span class="sxs-lookup"><span data-stu-id="e1e8c-195">The directory uses this string to identify your app.</span></span>
7. <span data-ttu-id="e1e8c-196">Haga clic en el icono Completar para guardar los cambios en el Asistente.</span><span class="sxs-lookup"><span data-stu-id="e1e8c-196">Click the Complete icon to save your changes in the wizard.</span></span>
8. <span data-ttu-id="e1e8c-197">En la página de inicio rápido, haga clic en **Configurar**.</span><span class="sxs-lookup"><span data-stu-id="e1e8c-197">On the Quick Start page, click **CONFIGURE**.</span></span>
9. <span data-ttu-id="e1e8c-198">Desplácese hasta la sección de **claves**, seleccione la duración y haga clic en **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="e1e8c-198">Scroll to the **keys** section, select the duration, and then click **SAVE**.</span></span> <span data-ttu-id="e1e8c-199">La página se actualiza y muestra ahora un valor de clave.</span><span class="sxs-lookup"><span data-stu-id="e1e8c-199">The page refreshes and now shows a key value.</span></span> <span data-ttu-id="e1e8c-200">Debe configurar la aplicación con este valor de clave y el valor del **identificador del cliente** .</span><span class="sxs-lookup"><span data-stu-id="e1e8c-200">You must configure your application with this key value and the **CLIENT ID** value.</span></span> <span data-ttu-id="e1e8c-201">(Las instrucciones para realizar esta configuración serán específicas para la aplicación).</span><span class="sxs-lookup"><span data-stu-id="e1e8c-201">(Instructions for this configuration will be application-specific.)</span></span>
10. <span data-ttu-id="e1e8c-202">Copie el valor del identificador del cliente en esta página. Lo utilizará en el paso siguiente para definir los permisos del almacén.</span><span class="sxs-lookup"><span data-stu-id="e1e8c-202">Copy the client ID value from this page, which you will use in the next step to set permissions on your vault.</span></span>

## <a name="authorize-the-application-to-use-the-key-or-secret"></a><span data-ttu-id="e1e8c-203">Autorización de la aplicación para que use la clave o el secreto</span><span class="sxs-lookup"><span data-stu-id="e1e8c-203">Authorize the application to use the key or secret</span></span>
<span data-ttu-id="e1e8c-204">Para que la aplicación pueda acceder a la clave o el secreto en el almacén, use el comando `az keyvault set-policy` .</span><span class="sxs-lookup"><span data-stu-id="e1e8c-204">To authorize the application to access the key or secret in the vault, use the `az keyvault set-policy` command.</span></span>

<span data-ttu-id="e1e8c-205">Por ejemplo, si el nombre del almacén es ContosoKeyVault y la aplicación que desea autorizar tiene el identificador de cliente 8f8c4bbd-485b-45fd-98f7-ec6300b7b4ed y desea que la aplicación tenga autorización para descifrar y firmar con claves en el almacén, ejecute lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="e1e8c-205">For example, if your vault name is ContosoKeyVault and the application you want to authorize has a client ID of 8f8c4bbd-485b-45fd-98f7-ec6300b7b4ed, and you want to authorize the application to decrypt and sign with keys in your vault, then run the following:</span></span>
```
az keyvault set-policy --name 'ContosoKeyVault' --spn 8f8c4bbd-485b-45fd-98f7-ec6300b7b4ed --key-permissions decrypt sign
```

<span data-ttu-id="e1e8c-206">Si desea autorizar a esa misma aplicación para leer los secretos en el almacén, ejecute lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="e1e8c-206">If you want to authorize that same application to read secrets in your vault, run the following:</span></span>
```
az keyvault set-policy --name 'ContosoKeyVault' --spn 8f8c4bbd-485b-45fd-98f7-ec6300b7b4ed --secret-permissions get
```
## <a name="if-you-want-to-use-a-hardware-security-module-hsm"></a><span data-ttu-id="e1e8c-207">Si desea utilizar un módulo de seguridad de hardware (HSM)</span><span class="sxs-lookup"><span data-stu-id="e1e8c-207">If you want to use a hardware security module (HSM)</span></span>
<span data-ttu-id="e1e8c-208">Para obtener seguridad adicional, puede importar o generar claves en módulos de seguridad de hardware (HSM) que no se salen nunca del límite de los HSM.</span><span class="sxs-lookup"><span data-stu-id="e1e8c-208">For added assurance, you can import or generate keys in hardware security modules (HSMs) that never leave the HSM boundary.</span></span> <span data-ttu-id="e1e8c-209">Los HSM tienen la validación FIPS 140-2 de nivel 2.</span><span class="sxs-lookup"><span data-stu-id="e1e8c-209">The HSMs are FIPS 140-2 Level 2 validated.</span></span> <span data-ttu-id="e1e8c-210">Si este requisito no es relevante para usted, omita esta sección y vaya al paso [Eliminación del Almacén de claves junto con las claves y secretos asociados](#delete-the-key-vault-and-associated-keys-and-secrets).</span><span class="sxs-lookup"><span data-stu-id="e1e8c-210">If this requirement doesn't apply to you, skip this section and go to [Delete the key vault and associated keys and secrets](#delete-the-key-vault-and-associated-keys-and-secrets).</span></span>

<span data-ttu-id="e1e8c-211">Para crear estas claves protegidas con HSM, debe contar con una suscripción de almacén que admita claves protegidas mediante HSM.</span><span class="sxs-lookup"><span data-stu-id="e1e8c-211">To create these HSM-protected keys, you must have a vault subscription that supports HSM-protected keys.</span></span>

<span data-ttu-id="e1e8c-212">Cuando cree el almacén de claves, agregue el parámetro 'sku':</span><span class="sxs-lookup"><span data-stu-id="e1e8c-212">When you create the keyvault, add the 'sku' parameter:</span></span>

```
az keyvault create --name 'ContosoKeyVaultHSM' --resource-group 'ContosoResourceGroup' --location 'East Asia' --sku 'Premium'
```
<span data-ttu-id="e1e8c-213">A este almacén, se pueden agregar claves protegidas mediante software (tal como se ha mostrado anteriormente) y claves protegidas con HSM.</span><span class="sxs-lookup"><span data-stu-id="e1e8c-213">You can add software-protected keys (as shown earlier) and HSM-protected keys to this vault.</span></span> <span data-ttu-id="e1e8c-214">Para crear una clave protegida con HSM, establezca el parámetro Destination en 'HSM':</span><span class="sxs-lookup"><span data-stu-id="e1e8c-214">To create an HSM-protected key, set the Destination parameter to 'HSM':</span></span>

```
az keyvault key create --vault-name 'ContosoKeyVaultHSM' --name 'ContosoFirstHSMKey' --protection 'hsm'
```

<span data-ttu-id="e1e8c-215">Puede utilizar el siguiente comando para importar una clave desde un archivo .pem a su equipo.</span><span class="sxs-lookup"><span data-stu-id="e1e8c-215">You can use the following command to import a key from a .pem file on your computer.</span></span> <span data-ttu-id="e1e8c-216">Este comando importa la clave a HSM en el servicio de Almacén de claves:</span><span class="sxs-lookup"><span data-stu-id="e1e8c-216">This command imports the key into HSMs in the Key Vault service:</span></span>

```
az keyvault key import --vault-name 'ContosoKeyVaultHSM' --name 'ContosoFirstHSMKey' --pem-file '/.softkey.pem' --protection 'hsm' --pem-password 'PaSSWORD'
```
<span data-ttu-id="e1e8c-217">El comando siguiente importa un paquete BYOK ("traiga su propia clave").</span><span class="sxs-lookup"><span data-stu-id="e1e8c-217">The next command imports a “bring your own key" (BYOK) package.</span></span> <span data-ttu-id="e1e8c-218">Esto permite generar la clave en el HSM local y transferirla al HSM en el servicio del Almacén de claves, sin que la clave salga del límite del HSM:</span><span class="sxs-lookup"><span data-stu-id="e1e8c-218">This lets you generate your key in your local HSM, and transfer it to HSMs in the Key Vault service, without the key leaving the HSM boundary:</span></span>

```
az keyvault key import --vault-name 'ContosoKeyVaultHSM' --name 'ContosoFirstHSMKey' --byok-file './ITByok.byok' --protection 'hsm'
```
<span data-ttu-id="e1e8c-219">Para obtener instrucciones detalladas sobre cómo generar este paquete BYOK, consulte [Generación y transferencia de claves protegidas con HSM para el Almacén de claves de Azure](key-vault-hsm-protected-keys.md).</span><span class="sxs-lookup"><span data-stu-id="e1e8c-219">For more detailed instructions about how to generate this BYOK package, see [How to use HSM-Protected Keys with Azure Key Vault](key-vault-hsm-protected-keys.md).</span></span>

## <a name="delete-the-key-vault-and-associated-keys-and-secrets"></a><span data-ttu-id="e1e8c-220">Eliminación del Almacén de claves junto con las claves y secretos asociados</span><span class="sxs-lookup"><span data-stu-id="e1e8c-220">Delete the key vault and associated keys and secrets</span></span>
<span data-ttu-id="e1e8c-221">Si ya no necesita la instancia de Key Vault ni la clave o el secreto que contiene, puede eliminarla con el comando `az keyvault delete`:</span><span class="sxs-lookup"><span data-stu-id="e1e8c-221">If you no longer need the key vault and the key or secret that it contains, you can delete the key vault by using the `az keyvault delete` command:</span></span>

```
az keyvault delete --name 'ContosoKeyVault'
```

<span data-ttu-id="e1e8c-222">O bien puede eliminar un grupo de recursos de Azure completo, que incluye el Almacén de claves y otros recursos incluidos en dicho grupo:</span><span class="sxs-lookup"><span data-stu-id="e1e8c-222">Or, you can delete an entire Azure resource group, which includes the key vault and any other resources that you included in that group:</span></span>

```
az group delete --name 'ContosoResourceGroup'
```

## <a name="other-azure-cross-platform-command-line-interface-commands"></a><span data-ttu-id="e1e8c-223">Otros comandos de la interfaz de la línea de comandos entre plataformas de Azure</span><span class="sxs-lookup"><span data-stu-id="e1e8c-223">Other Azure Cross-Platform Command-line Interface Commands</span></span>
<span data-ttu-id="e1e8c-224">Estos son otros comandos que pueden resultar útiles para administrar el Almacén de claves de Azure.</span><span class="sxs-lookup"><span data-stu-id="e1e8c-224">Other commands that you might useful for managing Azure Key Vault.</span></span>

<span data-ttu-id="e1e8c-225">Este comando ofrece una presentación tabular de todas las claves y las propiedades seleccionadas.</span><span class="sxs-lookup"><span data-stu-id="e1e8c-225">This command lists a tabular display of all keys and selected properties:</span></span>

<span data-ttu-id="e1e8c-226">az keyvault key list --vault-name 'ContosoKeyVault'</span><span class="sxs-lookup"><span data-stu-id="e1e8c-226">az keyvault key list --vault-name 'ContosoKeyVault'</span></span>

<span data-ttu-id="e1e8c-227">Este comando muestra una lista completa de propiedades para la clave especificada.</span><span class="sxs-lookup"><span data-stu-id="e1e8c-227">This command displays a full list of properties for the specified key:</span></span>

<span data-ttu-id="e1e8c-228">az keyvault key show --vault-name 'ContosoKeyVault' --name 'ContosoFirstKey'</span><span class="sxs-lookup"><span data-stu-id="e1e8c-228">az keyvault key show --vault-name 'ContosoKeyVault' --name 'ContosoFirstKey'</span></span>

<span data-ttu-id="e1e8c-229">Este comando muestra una presentación tabular de todos nombres de secretos y las propiedades que se elijan.</span><span class="sxs-lookup"><span data-stu-id="e1e8c-229">This command lists a tabular display of all secret names and selected properties:</span></span>

<span data-ttu-id="e1e8c-230">az keyvault secret list --vault-name 'ContosoKeyVault'</span><span class="sxs-lookup"><span data-stu-id="e1e8c-230">az keyvault secret list --vault-name 'ContosoKeyVault'</span></span>

<span data-ttu-id="e1e8c-231">Ejemplo de cómo quitar una clave específica:</span><span class="sxs-lookup"><span data-stu-id="e1e8c-231">Here's an example of how to remove a specific key:</span></span>

<span data-ttu-id="e1e8c-232">az keyvault key delete --vault-name 'ContosoKeyVault' --name 'ContosoFirstKey'</span><span class="sxs-lookup"><span data-stu-id="e1e8c-232">az keyvault key delete --vault-name 'ContosoKeyVault' --name 'ContosoFirstKey'</span></span>

<span data-ttu-id="e1e8c-233">Ejemplo de cómo quitar un secreto específico:</span><span class="sxs-lookup"><span data-stu-id="e1e8c-233">Here's an example of how to remove a specific secret:</span></span>

<span data-ttu-id="e1e8c-234">az keyvault secret delete --vault-name 'ContosoKeyVault' --name 'SQLPassword'</span><span class="sxs-lookup"><span data-stu-id="e1e8c-234">az keyvault secret delete --vault-name 'ContosoKeyVault' --name 'SQLPassword'</span></span>


## <a name="next-steps"></a><span data-ttu-id="e1e8c-235">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="e1e8c-235">Next steps</span></span>
<span data-ttu-id="e1e8c-236">Para ver una referencia completa de CLI de Azure para los comandos de Key Vault, consulte la [guía de referencia de la CLI de Key Vault](/cli/azure/keyvault).</span><span class="sxs-lookup"><span data-stu-id="e1e8c-236">For complete Azure CLI reference for key vault commands, see [Key Vault CLI reference](/cli/azure/keyvault)</span></span>

<span data-ttu-id="e1e8c-237">Para conocer las referencias de programación, consulte la [Guía del desarrollador del Almacén de claves de Azure](key-vault-developers-guide.md).</span><span class="sxs-lookup"><span data-stu-id="e1e8c-237">For programming references, see [the Azure Key Vault developer's guide](key-vault-developers-guide.md).</span></span>
