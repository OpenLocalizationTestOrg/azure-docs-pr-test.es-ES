---
title: "Administración de Azure Key Vault mediante CLI | Microsoft Docs"
description: "Use este tutorial para automatizar las tareas comunes en el Almacén de clave mediante el uso de la CLI."
services: key-vault
documentationcenter: 
author: BrucePerlerMS
manager: mbaldwin
tags: azure-resource-manager
ms.assetid: 66be6e44-684a-411b-802e-884628458ae7
ms.service: key-vault
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/08/2017
ms.author: bruceper
ms.openlocfilehash: c2565a742ce4f6ab5f7639a54c4a475f00cbc260
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="manage-key-vault-using-cli"></a><span data-ttu-id="d6427-103">Administración del Almacén de claves mediante CLI</span><span class="sxs-lookup"><span data-stu-id="d6427-103">Manage Key Vault using CLI</span></span>

<span data-ttu-id="d6427-104">Almacén de claves de Azure está disponible en la mayoría de las regiones.</span><span class="sxs-lookup"><span data-stu-id="d6427-104">Azure Key Vault is available in most regions.</span></span> <span data-ttu-id="d6427-105">Para obtener más información, consulte la [página de precios del Almacén de claves](https://azure.microsoft.com/pricing/details/key-vault/).</span><span class="sxs-lookup"><span data-stu-id="d6427-105">For more information, see the [Key Vault pricing page](https://azure.microsoft.com/pricing/details/key-vault/).</span></span>

## <a name="introduction"></a><span data-ttu-id="d6427-106">Introducción</span><span class="sxs-lookup"><span data-stu-id="d6427-106">Introduction</span></span>

<span data-ttu-id="d6427-107">Use este tutorial para empezar a trabajar con el Almacén de claves de Azure para crear un contenedor (un almacén) reforzado en Azure en el que almacenar y administrar las claves criptográficas y los secretos en Azure.</span><span class="sxs-lookup"><span data-stu-id="d6427-107">Use this tutorial to help you get started with Azure Key Vault to create a hardened container (a vault) in Azure, to store and manage cryptographic keys and secrets in Azure.</span></span> <span data-ttu-id="d6427-108">Se describe el proceso para usar la interfaz de la línea de comandos entre plataformas de Azure fin de crear un almacén en el que se guardará una clave o una contraseña para usarla con una aplicación de Azure.</span><span class="sxs-lookup"><span data-stu-id="d6427-108">It walks you through the process of using Azure Cross-Platform Command-Line Interface to create a vault that contains a key or password that you can then use with an Azure application.</span></span> <span data-ttu-id="d6427-109">A continuación, se explica cómo utiliza una aplicación esa clave o contraseña.</span><span class="sxs-lookup"><span data-stu-id="d6427-109">It then shows you how an application can then use that key or password.</span></span>

<span data-ttu-id="d6427-110">**Tiempo estimado para completar el tutorial:** 20 minutos</span><span class="sxs-lookup"><span data-stu-id="d6427-110">**Estimated time to complete:** 20 minutes</span></span>

> [!NOTE]
> <span data-ttu-id="d6427-111">Este tutorial no incluye instrucciones sobre cómo escribir la aplicación de Azure incluida en uno de los pasos, en el que se muestra cómo autorizar a una aplicación para que use una clave o un secreto del Almacén de claves.</span><span class="sxs-lookup"><span data-stu-id="d6427-111">This tutorial does not include instructions on how to write the Azure application that one of the steps includes, which shows how to authorize an application to use a key or secret in the key vault.</span></span>
> 
> <span data-ttu-id="d6427-112">Actualmente, no es posible configurar el Almacén de claves de Azure en el portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="d6427-112">Currently, you cannot configure Azure Key Vault in the Azure portal.</span></span> <span data-ttu-id="d6427-113">En su lugar, use estas instrucciones sobre la interfaz de la línea de comandos multiplataforma.</span><span class="sxs-lookup"><span data-stu-id="d6427-113">Instead, use these Cross-Platform Command-Line Interface  instructions.</span></span> <span data-ttu-id="d6427-114">O bien, para obtener instrucciones de Azure PowerShell, consulte [este tutorial equivalente](key-vault-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="d6427-114">Or, for Azure PowerShell instructions, see [this equivalent tutorial](key-vault-get-started.md).</span></span>
> 
> 

<span data-ttu-id="d6427-115">Para obtener información general sobre el Almacén de claves de Azure, consulte [¿Qué es el Almacén de clave de Azure?](key-vault-whatis.md)</span><span class="sxs-lookup"><span data-stu-id="d6427-115">For overview information about Azure Key Vault, see [What is Azure Key Vault?](key-vault-whatis.md)</span></span>

## <a name="prerequisites"></a><span data-ttu-id="d6427-116">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="d6427-116">Prerequisites</span></span>

<span data-ttu-id="d6427-117">Para realizar este tutorial, necesitará lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="d6427-117">To complete this tutorial, you must have the following:</span></span>

* <span data-ttu-id="d6427-118">Una suscripción a Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="d6427-118">A subscription to Microsoft Azure.</span></span> <span data-ttu-id="d6427-119">Si no tiene una, puede registrarse para obtener una versión de [evaluación gratuita](https://azure.microsoft.com/pricing/free-trial).</span><span class="sxs-lookup"><span data-stu-id="d6427-119">If you do not have one, you can sign up for a [free trial](https://azure.microsoft.com/pricing/free-trial).</span></span>
* <span data-ttu-id="d6427-120">Versión 0.9.1 o una posterior de la interfaz de la línea de comandos.</span><span class="sxs-lookup"><span data-stu-id="d6427-120">Command-Line Interface version 0.9.1 or later.</span></span> <span data-ttu-id="d6427-121">Para instalar la última versión y conectarla a su suscripción de Azure, vea [Instalación y configuración de la interfaz de la línea de comandos entre plataformas de Azure](../cli-install-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="d6427-121">To install the latest version and connect to your Azure subscription, see [Install and Configure the Azure Cross-Platform Command-Line Interface](../cli-install-nodejs.md).</span></span>
* <span data-ttu-id="d6427-122">Una aplicación que se configurará para utilizar la clave o contraseña creada en este tutorial.</span><span class="sxs-lookup"><span data-stu-id="d6427-122">An application that will be configured to use the key or password that you create in this tutorial.</span></span> <span data-ttu-id="d6427-123">Hay una aplicación de ejemplo disponible en el [Centro de descarga de Microsoft](http://www.microsoft.com/download/details.aspx?id=45343).</span><span class="sxs-lookup"><span data-stu-id="d6427-123">A sample application is available from the [Microsoft Download Center](http://www.microsoft.com/download/details.aspx?id=45343).</span></span> <span data-ttu-id="d6427-124">Para obtener instrucciones, consulte el archivo Léame adjunto.</span><span class="sxs-lookup"><span data-stu-id="d6427-124">For instructions, see the accompanying Readme file.</span></span>

## <a name="getting-help-with-azure-cross-platform-command-line-interface"></a><span data-ttu-id="d6427-125">Obtención de ayuda con la interfaz de la línea de comandos entre plataformas de Azure</span><span class="sxs-lookup"><span data-stu-id="d6427-125">Getting help with Azure Cross-Platform Command-Line Interface</span></span>

<span data-ttu-id="d6427-126">Este tutorial asume que está familiarizado con la interfaz de la línea de comandos (Bash, Terminal, símbolo del sistema).</span><span class="sxs-lookup"><span data-stu-id="d6427-126">This tutorial assumes that you are familiar with the command-line interface (Bash, Terminal, Command prompt)</span></span>

<span data-ttu-id="d6427-127">Los parámetros --help o -h se pueden usar para ver la ayuda de comandos específicos.</span><span class="sxs-lookup"><span data-stu-id="d6427-127">The --help or -h parameter can be used to view help for specific commands.</span></span> <span data-ttu-id="d6427-128">También puede usar el formato azure help [command] [options] para devolver la misma información.</span><span class="sxs-lookup"><span data-stu-id="d6427-128">Alternately, The azure help [command] [options] format can also be used to return the same information.</span></span> <span data-ttu-id="d6427-129">Por ejemplo, todos los comandos siguientes devuelven la misma información:</span><span class="sxs-lookup"><span data-stu-id="d6427-129">For example, the following commands all return the same information:</span></span>

    azure account set --help

    azure account set -h

    azure help account set

<span data-ttu-id="d6427-130">Si duda de qué parámetros necesita un comando, consulte la ayuda usando --help, -h o azure help [command].</span><span class="sxs-lookup"><span data-stu-id="d6427-130">When in doubt about the parameters needed by a command, refer to help using --help, -h or azure help [command].</span></span>

<span data-ttu-id="d6427-131">También puede leer los tutoriales siguientes para familiarizarse con el Administrador de recursos de Azure en la interfaz de la línea de comandos entre plataformas de Azure:</span><span class="sxs-lookup"><span data-stu-id="d6427-131">You can also read the following tutorials to get familiar with Azure Resource Manager in Azure Cross-Platform Command-Line Interface:</span></span>

* [<span data-ttu-id="d6427-132">Instalación y configuración de la interfaz de la línea de comandos entre plataformas de Azure.</span><span class="sxs-lookup"><span data-stu-id="d6427-132">How to install and configure Azure Cross-Platform Command Line Interface</span></span>](../cli-install-nodejs.md)
* [<span data-ttu-id="d6427-133">Uso de la interfaz de la línea de comandos entre plataformas de Azure con el Administrador de recursos de Azure</span><span class="sxs-lookup"><span data-stu-id="d6427-133">Using Azure Cross-Platform Command-Line Interface with Azure Resource Manager</span></span>](../xplat-cli-azure-resource-manager.md)

## <a name="connect-to-your-subscriptions"></a><span data-ttu-id="d6427-134">Conectarse a sus suscripciones</span><span class="sxs-lookup"><span data-stu-id="d6427-134">Connect to your subscriptions</span></span>

<span data-ttu-id="d6427-135">Para iniciar sesión usando una cuenta profesional, utilice el comando siguiente:</span><span class="sxs-lookup"><span data-stu-id="d6427-135">To log in using an organizational account, use the following command:</span></span>

    azure login -u username -p password

<span data-ttu-id="d6427-136">o si desea iniciar sesión escribiendo interactivamente</span><span class="sxs-lookup"><span data-stu-id="d6427-136">or if you want to log in by typing interactively</span></span>

    azure login

> [!NOTE]
> <span data-ttu-id="d6427-137">El método de inicio de sesión solo funciona con la cuenta organizativa.</span><span class="sxs-lookup"><span data-stu-id="d6427-137">The login method only works with organizational account.</span></span> <span data-ttu-id="d6427-138">Una cuenta profesional es un usuario administrado por su organización y definido en su inquilino de Azure Active Directory de la organización.</span><span class="sxs-lookup"><span data-stu-id="d6427-138">An organizational account is a user that is managed by your organization, and defined in your organization's Azure Active Directory tenant.</span></span>
> 
> 

<span data-ttu-id="d6427-139">Si actualmente no tiene una cuenta profesional y usa una cuenta Microsoft para iniciar sesión en su suscripción de Azure, puede crear una fácilmente siguiendo los pasos que se indican a continuación.</span><span class="sxs-lookup"><span data-stu-id="d6427-139">If you do not currently have an organizational account, and are using a Microsoft account to log in to your Azure subscription, you can easily create one using the following steps.</span></span>

1. <span data-ttu-id="d6427-140">Inicie sesión en el [Portal de administración de Azure](https://manage.windowsazure.com/)y haga clic en Active Directory.</span><span class="sxs-lookup"><span data-stu-id="d6427-140">Login to the Login to the [Azure Management Portal](https://manage.windowsazure.com/), and click on Active Directory.</span></span>
2. <span data-ttu-id="d6427-141">Si no hay ningún directorio, seleccione Create your directory y proporcione la información que se le pida.</span><span class="sxs-lookup"><span data-stu-id="d6427-141">If no directory exists, select Create your directory and provide the requested information.</span></span>
3. <span data-ttu-id="d6427-142">Seleccione su directorio y agregue un nuevo usuario.</span><span class="sxs-lookup"><span data-stu-id="d6427-142">Select your directory and add a new user.</span></span> <span data-ttu-id="d6427-143">Este nuevo usuario es una cuenta profesional.</span><span class="sxs-lookup"><span data-stu-id="d6427-143">This new user is an organizational account.</span></span> <span data-ttu-id="d6427-144">Durante la creación del usuario, se le proporcionará una dirección de correo electrónico para el usuario y una contraseña temporal.</span><span class="sxs-lookup"><span data-stu-id="d6427-144">During the creation of the user, you will be supplied with both an e-mail address for the user and a temporary password.</span></span> <span data-ttu-id="d6427-145">Guarde esta información para usarla en otro paso.</span><span class="sxs-lookup"><span data-stu-id="d6427-145">Save this information as it is used in another step.</span></span>
4. <span data-ttu-id="d6427-146">En el portal, seleccione Configuración y, a continuación, Administradores.</span><span class="sxs-lookup"><span data-stu-id="d6427-146">From the portal, select Settings and then select Administrators.</span></span> <span data-ttu-id="d6427-147">Seleccione Agregar y agregue el usuario nuevo como coadministrador.</span><span class="sxs-lookup"><span data-stu-id="d6427-147">Select Add, and add the new user as a co-administrator.</span></span> <span data-ttu-id="d6427-148">Así permite a la cuenta profesional administrar su suscripción de Azure.</span><span class="sxs-lookup"><span data-stu-id="d6427-148">This allows the organizational account to manage your Azure subscription.</span></span>
5. <span data-ttu-id="d6427-149">Finalmente, cierre sesión en el portal de Azure y, a continuación, vuelva a iniciarla usando la nueva cuenta profesional.</span><span class="sxs-lookup"><span data-stu-id="d6427-149">Finally, log out of the Azure portal and then log back in using the new organizational account.</span></span> <span data-ttu-id="d6427-150">Si es la primera vez que inicia sesión con esta cuenta, se le pedirá que cambie la contraseña.</span><span class="sxs-lookup"><span data-stu-id="d6427-150">If this is the first time logging in with this account, you will be prompted to change the password.</span></span>

<span data-ttu-id="d6427-151">Para obtener más información acerca de cómo usar una cuenta profesional con Microsoft Azure, consulte [Inicio de sesión como organización en Microsoft Azure](../active-directory/sign-up-organization.md).</span><span class="sxs-lookup"><span data-stu-id="d6427-151">For more information about using an organizational account with Microsoft Azure, see [Sign up for Microsoft Azure as an Organization](../active-directory/sign-up-organization.md).</span></span>

<span data-ttu-id="d6427-152">Si tiene varias suscripciones y desea especificar una en concreto para que use el Almacén de claves de Azure, escriba lo siguiente para ver las suscripciones de su cuenta:</span><span class="sxs-lookup"><span data-stu-id="d6427-152">If you have multiple subscriptions and want to specify a specific one to use for Azure Key Vault, type the following to see the subscriptions for your account:</span></span>

    azure account list

<span data-ttu-id="d6427-153">A continuación, para especificar la suscripción que se debe usar, escriba:</span><span class="sxs-lookup"><span data-stu-id="d6427-153">Then, to specify the subscription to use, type:</span></span>

    azure account set <subscription name>

<span data-ttu-id="d6427-154">Para obtener más información sobre la configuración de la interfaz de la línea de comandos entre plataformas de Azure, vea [Instalación y configuración de la interfaz de la línea de comandos entre plataformas de Azure](../cli-install-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="d6427-154">For more information about configuring Azure Cross-Platform Command-Line Interface, see [How to Install and Configure Azure Cross-Platform Command-Line Interface](../cli-install-nodejs.md).</span></span>

## <a name="switch-to-using-azure-resource-manager"></a><span data-ttu-id="d6427-155">Cambio al Administrador de recursos de Azure</span><span class="sxs-lookup"><span data-stu-id="d6427-155">Switch to using Azure Resource Manager</span></span>
<span data-ttu-id="d6427-156">El Almacén de claves necesita el Administrador de recursos de Azure. Por lo tanto, escriba lo siguiente para cambiar al modo del Administrador de recursos de Azure:</span><span class="sxs-lookup"><span data-stu-id="d6427-156">The Key Vault requires Azure Resource Manager, so type the following to switch to Azure Resource Manager mode:</span></span>

    azure config mode arm

## <a name="create-a-new-resource-group"></a><span data-ttu-id="d6427-157">Creación de un nuevo grupo de recursos</span><span class="sxs-lookup"><span data-stu-id="d6427-157">Create a new resource group</span></span>
<span data-ttu-id="d6427-158">Cuando se utiliza el Administrador de recursos de Azure, todos los recursos relacionados se crean dentro de un grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="d6427-158">When using Azure Resource Manager, all related resources are created inside a resource group.</span></span> <span data-ttu-id="d6427-159">Crearemos un nuevo grupo de recursos denominado 'ContosoResourceGroup' para este tutorial.</span><span class="sxs-lookup"><span data-stu-id="d6427-159">We will create a new resource group 'ContosoResourceGroup' for this tutorial.</span></span>

    azure group create 'ContosoResourceGroup' 'East Asia'

<span data-ttu-id="d6427-160">El primer parámetro es el nombre del grupo de recursos y el segundo parámetro es la ubicación.</span><span class="sxs-lookup"><span data-stu-id="d6427-160">The first parameter is resource group name and the second parameter is the location.</span></span> <span data-ttu-id="d6427-161">Para la ubicación, use el comando `azure location list` para identificar cómo se debe especificar una ubicación alternativa a la usada en este ejemplo.</span><span class="sxs-lookup"><span data-stu-id="d6427-161">For location, use the command `azure location list` to identify how to specify an alternative location to the one in this example.</span></span> <span data-ttu-id="d6427-162">Si necesita más información, escriba: `azure help location`</span><span class="sxs-lookup"><span data-stu-id="d6427-162">If you need more information, type: `azure help location`</span></span>

## <a name="register-the-key-vault-resource-provider"></a><span data-ttu-id="d6427-163">Registro del proveedor de recursos de Almacén de claves</span><span class="sxs-lookup"><span data-stu-id="d6427-163">Register the Key Vault resource provider</span></span>
<span data-ttu-id="d6427-164">Asegúrese de que el proveedor de recursos de Almacén de claves está registrado en la suscripción:</span><span class="sxs-lookup"><span data-stu-id="d6427-164">Make sure that Key Vault resource provider is registered in your subscription:</span></span>

`azure provider register Microsoft.KeyVault`

<span data-ttu-id="d6427-165">Esto solo se debe hacer una vez por suscripción.</span><span class="sxs-lookup"><span data-stu-id="d6427-165">This only needs to be done once per subscription.</span></span>

## <a name="create-a-key-vault"></a><span data-ttu-id="d6427-166">Creación de un Almacén de claves</span><span class="sxs-lookup"><span data-stu-id="d6427-166">Create a key vault</span></span>

<span data-ttu-id="d6427-167">Utilice el comando `azure keyvault create` para crear un Almacén de claves.</span><span class="sxs-lookup"><span data-stu-id="d6427-167">Use the `azure keyvault create` command to create a key vault.</span></span> <span data-ttu-id="d6427-168">Este script tiene tres parámetros obligatorios: el nombre del grupo de recursos, el nombre del Almacén de claves y la ubicación geográfica.</span><span class="sxs-lookup"><span data-stu-id="d6427-168">This script has three mandatory parameters: a resource group name, a key vault name, and the geographic location.</span></span>

<span data-ttu-id="d6427-169">Por ejemplo, si utiliza el nombre del almacén de ContosoKeyVault, el nombre del grupo de recursos ContosoResourceGroup y la ubicación East Asia, deberá escribir:</span><span class="sxs-lookup"><span data-stu-id="d6427-169">For example, if you use the vault name of ContosoKeyVault, the resource group name of ContosoResourceGroup, and the location of East Asia, type:</span></span>

    azure keyvault create --vault-name 'ContosoKeyVault' --resource-group 'ContosoResourceGroup' --location 'East Asia'

<span data-ttu-id="d6427-170">El resultado de este comando muestra las propiedades del Almacén de claves que acaba de crear.</span><span class="sxs-lookup"><span data-stu-id="d6427-170">The output of this command shows properties of the key vault that you've just created.</span></span> <span data-ttu-id="d6427-171">Las dos propiedades más importantes son:</span><span class="sxs-lookup"><span data-stu-id="d6427-171">The two most important properties are:</span></span>

* <span data-ttu-id="d6427-172">**Name**: en este ejemplo, el nombre es ContosoKeyVault.</span><span class="sxs-lookup"><span data-stu-id="d6427-172">**Name**: In the example this is ContosoKeyVault.</span></span> <span data-ttu-id="d6427-173">Utilizará este nombre para otros cmdlets del Almacén de claves.</span><span class="sxs-lookup"><span data-stu-id="d6427-173">You will use this name for other Key Vault cmdlets.</span></span>
* <span data-ttu-id="d6427-174">**vaultUri**: en este ejemplo es https://contosokeyvault.vault.azure.net.</span><span class="sxs-lookup"><span data-stu-id="d6427-174">**vaultUri**: In the example this is https://contosokeyvault.vault.azure.net.</span></span> <span data-ttu-id="d6427-175">Las aplicaciones que utilizan el almacén a través de su API de REST deben usar este identificador URI.</span><span class="sxs-lookup"><span data-stu-id="d6427-175">Applications that use your vault through its REST API must use this URI.</span></span>

<span data-ttu-id="d6427-176">Su cuenta de Azure ahora está autorizada para realizar operaciones en este Almacén de claves.</span><span class="sxs-lookup"><span data-stu-id="d6427-176">Your Azure account is now authorized to perform any operations on this key vault.</span></span> <span data-ttu-id="d6427-177">Hasta el momento, nadie más lo está.</span><span class="sxs-lookup"><span data-stu-id="d6427-177">As yet, nobody else is.</span></span>

## <a name="add-a-key-or-secret-to-the-key-vault"></a><span data-ttu-id="d6427-178">Adición de una clave o un secreto al Almacén de claves</span><span class="sxs-lookup"><span data-stu-id="d6427-178">Add a key or secret to the key vault</span></span>

<span data-ttu-id="d6427-179">Si desea que el Almacén de claves de Azure cree una clave protegida mediante software, utilice el comando `azure key create` y escriba lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="d6427-179">If you want Azure Key Vault to create a software-protected key for you, use the `azure key create` command, and type the following:</span></span>

    azure keyvault key create --vault-name 'ContosoKeyVault' --key-name 'ContosoFirstKey' --destination software

<span data-ttu-id="d6427-180">Sin embargo, si tiene una clave existente en un archivo .pem guardado como archivo local en un archivo denominado softkey.pem que desea cargar en el Almacén de claves de Azure, escriba lo siguiente para importar la clave desde el archivo .PEM, que protege la clave de software en el servicio de Almacén de claves:</span><span class="sxs-lookup"><span data-stu-id="d6427-180">However, if you have an existing key in a .pem file saved as local file in a file named softkey.pem that you want to upload to Azure Key Vault, type the following to import the key from the .PEM file, which protects the key by software in the Key Vault service:</span></span>

    azure keyvault key import --vault-name 'ContosoKeyVault' --key-name 'ContosoFirstKey' --pem-file './softkey.pem' --password 'PaSSWORD' --destination software

<span data-ttu-id="d6427-181">Ahora puede utilizar el URI para hacer referencia a la clave que creó o cargó en el Almacén de claves de Azure.</span><span class="sxs-lookup"><span data-stu-id="d6427-181">You can now reference the key that you created or uploaded to Azure Key Vault, by using its URI.</span></span> <span data-ttu-id="d6427-182">Use **https://ContosoKeyVault.vault.azure.net/keys/ContosoFirstKey** para obtener siempre la versión actual y **https://ContosoKeyVault.vault.azure.net/keys/ContosoFirstKey/cgacf4f763ar42ffb0a1gca546aygd87** para obtener esta versión concreta.</span><span class="sxs-lookup"><span data-stu-id="d6427-182">Use  **https://ContosoKeyVault.vault.azure.net/keys/ContosoFirstKey** to always get the current version, and use **https://ContosoKeyVault.vault.azure.net/keys/ContosoFirstKey/cgacf4f763ar42ffb0a1gca546aygd87** to get this specific version.</span></span>

<span data-ttu-id="d6427-183">Para agregar un secreto, que es una contraseña denominada SQLPassword con el valor Pa$$w0rd, al Almacén de claves de Azure, escriba lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="d6427-183">To add a secret to the vault, which is a password named SQLPassword and that has the value of Pa$$w0rd to Azure Key Vault, type the following:</span></span>

    azure keyvault secret set --vault-name 'ContosoKeyVault' --secret-name 'SQLPassword' --value 'Pa$$w0rd'

<span data-ttu-id="d6427-184">Ahora puede hacer referencia a esta clave que agregó al Almacén de claves de Azure utilizando su URI.</span><span class="sxs-lookup"><span data-stu-id="d6427-184">You can now reference this password that you added to Azure Key Vault, by using its URI.</span></span> <span data-ttu-id="d6427-185">Utilice **https://ContosoVault.vault.azure.net/secrets/SQLPassword** para obtener siempre la versión actual y **https://ContosoVault.vault.azure.net/secrets/SQLPassword/90018dbb96a84117a0d2847ef8e7189d** para obtener esta versión concreta.</span><span class="sxs-lookup"><span data-stu-id="d6427-185">Use **https://ContosoVault.vault.azure.net/secrets/SQLPassword** to always get the current version, and use **https://ContosoVault.vault.azure.net/secrets/SQLPassword/90018dbb96a84117a0d2847ef8e7189d** to get this specific version.</span></span>

<span data-ttu-id="d6427-186">Veamos la clave o el secreto que acaba de crear:</span><span class="sxs-lookup"><span data-stu-id="d6427-186">Let's view the key or secret that you just created:</span></span>

* <span data-ttu-id="d6427-187">Para ver la clave, escriba: `azure keyvault key list --vault-name 'ContosoKeyVault'`</span><span class="sxs-lookup"><span data-stu-id="d6427-187">To view your key, type: `azure keyvault key list --vault-name 'ContosoKeyVault'`</span></span>
* <span data-ttu-id="d6427-188">Para ver el secreto, escriba: `azure keyvault secret list --vault-name 'ContosoKeyVault'`</span><span class="sxs-lookup"><span data-stu-id="d6427-188">To view your secret, type: `azure keyvault secret list --vault-name 'ContosoKeyVault'`</span></span>

## <a name="register-an-application-with-azure-active-directory"></a><span data-ttu-id="d6427-189">Registro de una aplicación con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="d6427-189">Register an application with Azure Active Directory</span></span>

<span data-ttu-id="d6427-190">Este paso lo haría normalmente un programador en un equipo independiente.</span><span class="sxs-lookup"><span data-stu-id="d6427-190">This step would usually be done by a developer, on a separate computer.</span></span> <span data-ttu-id="d6427-191">No es específico del Almacén de claves de Azure, pero se incluye aquí a fin de que la información ofrecida sea lo más completa posible.</span><span class="sxs-lookup"><span data-stu-id="d6427-191">It is not specific to Azure Key Vault but is included here, for completeness.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="d6427-192">Para finalizar el tutorial, la cuenta, el almacén y la aplicación que vaya a registrar en este paso deben estar en el mismo directorio de Azure.</span><span class="sxs-lookup"><span data-stu-id="d6427-192">To complete the tutorial, your account, the vault, and the application that you will register in this step must all be in the same Azure directory.</span></span>
> 
> 

<span data-ttu-id="d6427-193">Las aplicaciones que utilizan un Almacén de claves deben autenticarse utilizando un token de Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="d6427-193">Applications that use a key vault must authenticate by using a token from Azure Active Directory.</span></span> <span data-ttu-id="d6427-194">Para ello, el propietario de la aplicación debe registrarla primero en su Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="d6427-194">To do this, the owner of the application must first register the application in their Azure Active Directory.</span></span> <span data-ttu-id="d6427-195">Al final del registro, el propietario de la aplicación obtiene los valores siguientes:</span><span class="sxs-lookup"><span data-stu-id="d6427-195">At the end of registration, the application owner gets the following values:</span></span>

* <span data-ttu-id="d6427-196">Un **identificador de la aplicación** (también conocido como un identificador de cliente) y una **clave de autenticación** (también conocida como secreto compartido).</span><span class="sxs-lookup"><span data-stu-id="d6427-196">An **Application ID** (also known as a Client ID) and **authentication key** (also known as the shared secret).</span></span> <span data-ttu-id="d6427-197">Para obtener un token, la aplicación debe presentar estos dos valores a Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="d6427-197">The application must present both of these values to Azure Active Directory, to get a token.</span></span> <span data-ttu-id="d6427-198">La forma en que se configura la aplicación para ello depende de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="d6427-198">How the application is configured to do this depends on the application.</span></span> <span data-ttu-id="d6427-199">Para la aplicación de ejemplo del Almacén de claves, el propietario de la aplicación establece estos valores en el archivo app.config.</span><span class="sxs-lookup"><span data-stu-id="d6427-199">For the Key Vault sample application, the application owner sets these values in the app.config file.</span></span>

<span data-ttu-id="d6427-200">Para registrar la aplicación en Azure Active Directory:</span><span class="sxs-lookup"><span data-stu-id="d6427-200">To register the application in Azure Active Directory:</span></span>

1. <span data-ttu-id="d6427-201">Inicie sesión en el Portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="d6427-201">Sign in to the Azure portal.</span></span>
2. <span data-ttu-id="d6427-202">A la izquierda, haga clic en **Active Directory** y, después, seleccione el directorio en el que va a registrar la aplicación.</span><span class="sxs-lookup"><span data-stu-id="d6427-202">On the left, click **Active Directory**, and then select the directory in which you will register your application.</span></span> <br> <br> 

>[!NOTE] 
> <span data-ttu-id="d6427-203">Debe seleccionar el mismo directorio que contiene la suscripción de Azure con la que creó la instancia de Key Vault.</span><span class="sxs-lookup"><span data-stu-id="d6427-203">You must select the same directory that contains the Azure subscription with which you created your key vault.</span></span> <span data-ttu-id="d6427-204">Si no sabe qué directorio es, haga clic en **Configuración**, identifique la suscripción con la que creó la instancia de Key Vault y anote el nombre del directorio que se muestra en la última columna.</span><span class="sxs-lookup"><span data-stu-id="d6427-204">If you do not know which directory this is, click **Settings**, identify the subscription with which you created your key vault, and note the name of the directory displayed in the last column.</span></span>

3. <span data-ttu-id="d6427-205">Haga clic en **Aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="d6427-205">Click **APPLICATIONS**.</span></span> <span data-ttu-id="d6427-206">Si no se han agregado aplicaciones a su directorio, esta página muestra solo el vínculo **Agregar una aplicación** .</span><span class="sxs-lookup"><span data-stu-id="d6427-206">If no apps have been added to your directory, this page will show only the **Add an App** link.</span></span> <span data-ttu-id="d6427-207">Haga clic en el vínculo, o como alternativa, puede hacer clic en **Agregar** en la barra de comandos.</span><span class="sxs-lookup"><span data-stu-id="d6427-207">Click the link, or alternatively, you can click the **ADD** on the command bar.</span></span>
4. <span data-ttu-id="d6427-208">En el Asistente para **agregar aplicaciones**, en la página **¿Qué desea hacer?**, haga clic en **Agregar una aplicación que mi organización está desarrollando**.</span><span class="sxs-lookup"><span data-stu-id="d6427-208">In the **ADD APPLICATION** wizard, on the **What do you want to do?** page, click **Add an application my organization is developing**.</span></span>
5. <span data-ttu-id="d6427-209">En la página **Proporcione información sobre su aplicación**, especifique un nombre para la aplicación y seleccione **Aplicación web y/o API web** (valor predeterminado).</span><span class="sxs-lookup"><span data-stu-id="d6427-209">On the **Tell us about your application** page, specify a name for your application and select **WEB APPLICATION AND/OR WEB API** (the default).</span></span> <span data-ttu-id="d6427-210">Haga clic en el icono Siguiente.</span><span class="sxs-lookup"><span data-stu-id="d6427-210">Click the Next icon.</span></span>
6. <span data-ttu-id="d6427-211">En la página **Agregar propiedades**, especifique los valores de **URL de inicio de sesión** y **URI de id. de aplicación** para la aplicación web.</span><span class="sxs-lookup"><span data-stu-id="d6427-211">On the **App properties** page, specify the **SIGN-ON URL** and **APP ID URI** for your web application.</span></span> <span data-ttu-id="d6427-212">Si la aplicación no tiene estos valores, puede inventárselos en este paso (por ejemplo, puede especificar http://test1.contoso.com en ambos cuadros).</span><span class="sxs-lookup"><span data-stu-id="d6427-212">If your application does not have these values, you can make them up for this step (for example, you could specify http://test1.contoso.com for both boxes).</span></span> <span data-ttu-id="d6427-213">No importa si estos sitios existen; lo importante es que el URI del identificador de la aplicación de cada aplicación sea diferente en cada aplicación del directorio.</span><span class="sxs-lookup"><span data-stu-id="d6427-213">It does not matter if these sites exist; what is important is that the app ID URI for each application is different for every application in your directory.</span></span> <span data-ttu-id="d6427-214">El directorio utiliza esta cadena para identificar la aplicación.</span><span class="sxs-lookup"><span data-stu-id="d6427-214">The directory uses this string to identify your app.</span></span>
7. <span data-ttu-id="d6427-215">Haga clic en el icono Completar para guardar los cambios en el Asistente.</span><span class="sxs-lookup"><span data-stu-id="d6427-215">Click the Complete icon to save your changes in the wizard.</span></span>
8. <span data-ttu-id="d6427-216">En la página de inicio rápido, haga clic en **Configurar**.</span><span class="sxs-lookup"><span data-stu-id="d6427-216">On the Quick Start page, click **CONFIGURE**.</span></span>
9. <span data-ttu-id="d6427-217">Desplácese hasta la sección de **claves**, seleccione la duración y haga clic en **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="d6427-217">Scroll to the **keys** section, select the duration, and then click **SAVE**.</span></span> <span data-ttu-id="d6427-218">La página se actualiza y muestra ahora un valor de clave.</span><span class="sxs-lookup"><span data-stu-id="d6427-218">The page refreshes and now shows a key value.</span></span> <span data-ttu-id="d6427-219">Debe configurar la aplicación con este valor de clave y el valor del **identificador del cliente** .</span><span class="sxs-lookup"><span data-stu-id="d6427-219">You must configure your application with this key value and the **CLIENT ID** value.</span></span> <span data-ttu-id="d6427-220">(Las instrucciones para realizar esta configuración serán específicas para la aplicación).</span><span class="sxs-lookup"><span data-stu-id="d6427-220">(Instructions for this configuration will be application-specific.)</span></span>
10. <span data-ttu-id="d6427-221">Copie el valor del identificador del cliente en esta página. Lo utilizará en el paso siguiente para definir los permisos del almacén.</span><span class="sxs-lookup"><span data-stu-id="d6427-221">Copy the client ID value from this page, which you will use in the next step to set permissions on your vault.</span></span>

## <a name="authorize-the-application-to-use-the-key-or-secret"></a><span data-ttu-id="d6427-222">Autorización de la aplicación para que use la clave o el secreto</span><span class="sxs-lookup"><span data-stu-id="d6427-222">Authorize the application to use the key or secret</span></span>
<span data-ttu-id="d6427-223">Para que la aplicación pueda acceder a la clave o el secreto en el almacén, use el comando `azure keyvault set-policy` .</span><span class="sxs-lookup"><span data-stu-id="d6427-223">To authorize the application to access the key or secret in the vault, use the `azure keyvault set-policy` command.</span></span>

<span data-ttu-id="d6427-224">Por ejemplo, si el nombre del almacén es ContosoKeyVault y la aplicación que desea autorizar tiene el identificador de cliente 8f8c4bbd-485b-45fd-98f7-ec6300b7b4ed y desea que la aplicación tenga autorización para descifrar y firmar con claves en el almacén, ejecute lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="d6427-224">For example, if your vault name is ContosoKeyVault and the application you want to authorize has a client ID of 8f8c4bbd-485b-45fd-98f7-ec6300b7b4ed, and you want to authorize the application to decrypt and sign with keys in your vault, then run the following:</span></span>

    azure keyvault set-policy --vault-name 'ContosoKeyVault' --spn 8f8c4bbd-485b-45fd-98f7-ec6300b7b4ed --perms-to-keys '[\"decrypt\",\"sign\"]'

> [!NOTE]
> <span data-ttu-id="d6427-225">Si se ejecuta en un símbolo del sistema de Windows, debe reemplazar las comillas simples por comillas dobles y, además, insertar un carácter de escape en las comillas dobles internas.</span><span class="sxs-lookup"><span data-stu-id="d6427-225">If you are running on Windows command prompt, you should replace single quotes with double quotes, and also escape the internal double quotes.</span></span> <span data-ttu-id="d6427-226">Por ejemplo: "[\"decrypt\",\"sign\"]".</span><span class="sxs-lookup"><span data-stu-id="d6427-226">For example: "[\"decrypt\",\"sign\"]".</span></span>
> 
> 

<span data-ttu-id="d6427-227">Si desea autorizar a esa misma aplicación para leer los secretos en el almacén, ejecute lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="d6427-227">If you want to authorize that same application to read secrets in your vault, run the following:</span></span>

    azure keyvault set-policy --vault-name 'ContosoKeyVault' --spn 8f8c4bbd-485b-45fd-98f7-ec6300b7b4ed --perms-to-secrets '[\"get\"]'

## <a name="if-you-want-to-use-a-hardware-security-module-hsm"></a><span data-ttu-id="d6427-228">Si desea utilizar un módulo de seguridad de hardware (HSM)</span><span class="sxs-lookup"><span data-stu-id="d6427-228">If you want to use a hardware security module (HSM)</span></span>
<span data-ttu-id="d6427-229">Para obtener seguridad adicional, puede importar o generar claves en módulos de seguridad de hardware (HSM) que no se salen nunca del límite de los HSM.</span><span class="sxs-lookup"><span data-stu-id="d6427-229">For added assurance, you can import or generate keys in hardware security modules (HSMs) that never leave the HSM boundary.</span></span> <span data-ttu-id="d6427-230">Los HSM tienen la validación FIPS 140-2 de nivel 2.</span><span class="sxs-lookup"><span data-stu-id="d6427-230">The HSMs are FIPS 140-2 Level 2 validated.</span></span> <span data-ttu-id="d6427-231">Si este requisito no es relevante para usted, omita esta sección y vaya al paso [Eliminación del Almacén de claves junto con las claves y secretos asociados](#delete-the-key-vault-and-associated-keys-and-secrets).</span><span class="sxs-lookup"><span data-stu-id="d6427-231">If this requirement doesn't apply to you, skip this section and go to [Delete the key vault and associated keys and secrets](#delete-the-key-vault-and-associated-keys-and-secrets).</span></span>

<span data-ttu-id="d6427-232">Para crear estas claves protegidas con HSM, debe contar con una suscripción de almacén que admita claves protegidas mediante HSM.</span><span class="sxs-lookup"><span data-stu-id="d6427-232">To create these HSM-protected keys, you must have a vault subscription that supports HSM-protected keys.</span></span>

<span data-ttu-id="d6427-233">Cuando cree el almacén de claves, agregue el parámetro 'sku':</span><span class="sxs-lookup"><span data-stu-id="d6427-233">When you create the keyvault, add the 'sku' parameter:</span></span>

    azure azure keyvault create --vault-name 'ContosoKeyVaultHSM' --resource-group 'ContosoResourceGroup' --location 'East Asia' --sku 'Premium'

<span data-ttu-id="d6427-234">A este almacén, se pueden agregar claves protegidas mediante software (tal como se ha mostrado anteriormente) y claves protegidas con HSM.</span><span class="sxs-lookup"><span data-stu-id="d6427-234">You can add software-protected keys (as shown earlier) and HSM-protected keys to this vault.</span></span> <span data-ttu-id="d6427-235">Para crear una clave protegida con HSM, establezca el parámetro Destination en 'HSM':</span><span class="sxs-lookup"><span data-stu-id="d6427-235">To create an HSM-protected key, set the Destination parameter to 'HSM':</span></span>

    azure keyvault key create --vault-name 'ContosoKeyVaultHSM' --key-name 'ContosoFirstHSMKey' --destination 'HSM'

<span data-ttu-id="d6427-236">Puede utilizar el siguiente comando para importar una clave desde un archivo .pem a su equipo.</span><span class="sxs-lookup"><span data-stu-id="d6427-236">You can use the following command to import a key from a .pem file on your computer.</span></span> <span data-ttu-id="d6427-237">Este comando importa la clave a HSM en el servicio de Almacén de claves:</span><span class="sxs-lookup"><span data-stu-id="d6427-237">This command imports the key into HSMs in the Key Vault service:</span></span>

    azure keyvault key import --vault-name 'ContosoKeyVaultHSM' --key-name 'ContosoFirstHSMKey' --pem-file '/.softkey.pem' --destination 'HSM' --password 'PaSSWORD'

<span data-ttu-id="d6427-238">El comando siguiente importa un paquete BYOK ("traiga su propia clave").</span><span class="sxs-lookup"><span data-stu-id="d6427-238">The next command imports a “bring your own key" (BYOK) package.</span></span> <span data-ttu-id="d6427-239">Esto permite generar la clave en el HSM local y transferirla al HSM en el servicio del Almacén de claves, sin que la clave salga del límite del HSM:</span><span class="sxs-lookup"><span data-stu-id="d6427-239">This lets you generate your key in your local HSM, and transfer it to HSMs in the Key Vault service, without the key leaving the HSM boundary:</span></span>

    azure keyvault key import --vault-name 'ContosoKeyVaultHSM' --key-name 'ContosoFirstHSMKey' --byok-file './ITByok.byok' --destination 'HSM'

<span data-ttu-id="d6427-240">Para obtener instrucciones detalladas sobre cómo generar este paquete BYOK, consulte [Generación y transferencia de claves protegidas con HSM para el Almacén de claves de Azure](key-vault-hsm-protected-keys.md).</span><span class="sxs-lookup"><span data-stu-id="d6427-240">For more detailed instructions about how to generate this BYOK package, see [How to use HSM-Protected Keys with Azure Key Vault](key-vault-hsm-protected-keys.md).</span></span>

## <a name="delete-the-key-vault-and-associated-keys-and-secrets"></a><span data-ttu-id="d6427-241">Eliminación del Almacén de claves junto con las claves y secretos asociados</span><span class="sxs-lookup"><span data-stu-id="d6427-241">Delete the key vault and associated keys and secrets</span></span>
<span data-ttu-id="d6427-242">Si ya no necesita el Almacén de claves ni la clave o el secreto que contiene, puede eliminar el Almacén de claves utilizando el comando azure keyvault delete:</span><span class="sxs-lookup"><span data-stu-id="d6427-242">If you no longer need the key vault and the key or secret that it contains, you can delete the key vault by using the azure keyvault delete command:</span></span>

    azure keyvault delete --vault-name 'ContosoKeyVault'

<span data-ttu-id="d6427-243">O bien puede eliminar un grupo de recursos de Azure completo, que incluye el Almacén de claves y otros recursos incluidos en dicho grupo:</span><span class="sxs-lookup"><span data-stu-id="d6427-243">Or, you can delete an entire Azure resource group, which includes the key vault and any other resources that you included in that group:</span></span>

    azure group delete --name 'ContosoResourceGroup'


## <a name="other-azure-cross-platform-command-line-interface-commands"></a><span data-ttu-id="d6427-244">Otros comandos de la interfaz de la línea de comandos entre plataformas de Azure</span><span class="sxs-lookup"><span data-stu-id="d6427-244">Other Azure Cross-Platform Command-line Interface Commands</span></span>
<span data-ttu-id="d6427-245">Estos son otros comandos que pueden resultar útiles para administrar el Almacén de claves de Azure.</span><span class="sxs-lookup"><span data-stu-id="d6427-245">Other commands that you might useful for managing Azure Key Vault.</span></span>

<span data-ttu-id="d6427-246">Este comando ofrece una presentación tabular de todas las claves y las propiedades seleccionadas.</span><span class="sxs-lookup"><span data-stu-id="d6427-246">This command lists a tabular display of all keys and selected properties:</span></span>

    azure keyvault key list --vault-name 'ContosoKeyVault'

<span data-ttu-id="d6427-247">Este comando muestra una lista completa de propiedades para la clave especificada.</span><span class="sxs-lookup"><span data-stu-id="d6427-247">This command displays a full list of properties for the specified key:</span></span>

    azure keyvault key show --vault-name 'ContosoKeyVault' --key-name 'ContosoFirstKey'

<span data-ttu-id="d6427-248">Este comando muestra una presentación tabular de todos nombres de secretos y las propiedades que se elijan.</span><span class="sxs-lookup"><span data-stu-id="d6427-248">This command lists a tabular display of all secret names and selected properties:</span></span>

    azure keyvault secret list --vault-name 'ContosoKeyVault'

<span data-ttu-id="d6427-249">Ejemplo de cómo quitar una clave específica:</span><span class="sxs-lookup"><span data-stu-id="d6427-249">Here's an example of how to remove a specific key:</span></span>

    azure keyvault key delete --vault-name 'ContosoKeyVault' --key-name 'ContosoFirstKey'

<span data-ttu-id="d6427-250">Ejemplo de cómo quitar un secreto específico:</span><span class="sxs-lookup"><span data-stu-id="d6427-250">Here's an example of how to remove a specific secret:</span></span>

    azure keyvault secret delete --vault-name 'ContosoKeyVault' --secret-name 'SQLPassword'


## <a name="next-steps"></a><span data-ttu-id="d6427-251">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="d6427-251">Next steps</span></span>
<span data-ttu-id="d6427-252">Para conocer las referencias de programación, consulte la [Guía del desarrollador del Almacén de claves de Azure](key-vault-developers-guide.md).</span><span class="sxs-lookup"><span data-stu-id="d6427-252">For programming references, see [the Azure Key Vault developer's guide](key-vault-developers-guide.md).</span></span>

