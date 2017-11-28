---
title: "aaaManage con CLI del almacén de claves de Azure | Documentos de Microsoft"
description: "Usar tareas de este tutorial tooautomate en el almacén de claves mediante Hola CLI"
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
ms.openlocfilehash: 9ef506faa67e1f0db5b9e303300d63b135ddd7b9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="manage-key-vault-using-cli"></a><span data-ttu-id="c023a-103">Administración del Almacén de claves mediante CLI</span><span class="sxs-lookup"><span data-stu-id="c023a-103">Manage Key Vault using CLI</span></span>

<span data-ttu-id="c023a-104">Almacén de claves de Azure está disponible en la mayoría de las regiones.</span><span class="sxs-lookup"><span data-stu-id="c023a-104">Azure Key Vault is available in most regions.</span></span> <span data-ttu-id="c023a-105">Para obtener más información, vea hello [almacén de claves de página de precios](https://azure.microsoft.com/pricing/details/key-vault/).</span><span class="sxs-lookup"><span data-stu-id="c023a-105">For more information, see hello [Key Vault pricing page](https://azure.microsoft.com/pricing/details/key-vault/).</span></span>

## <a name="introduction"></a><span data-ttu-id="c023a-106">Introducción</span><span class="sxs-lookup"><span data-stu-id="c023a-106">Introduction</span></span>

<span data-ttu-id="c023a-107">Use este tutorial toohelp obtendrá a trabajar con el almacén de claves de Azure toocreate un contenedor reforzado (un almacén) en Azure, toostore y administrar las claves criptográficas y secretos en Azure.</span><span class="sxs-lookup"><span data-stu-id="c023a-107">Use this tutorial toohelp you get started with Azure Key Vault toocreate a hardened container (a vault) in Azure, toostore and manage cryptographic keys and secrets in Azure.</span></span> <span data-ttu-id="c023a-108">Le guiará por proceso de Hola de uso de interfaz de línea de comandos entre plataformas de Azure toocreate un almacén que contiene una clave o contraseña que puede utilizar con una aplicación de Azure.</span><span class="sxs-lookup"><span data-stu-id="c023a-108">It walks you through hello process of using Azure Cross-Platform Command-Line Interface toocreate a vault that contains a key or password that you can then use with an Azure application.</span></span> <span data-ttu-id="c023a-109">A continuación, se explica cómo utiliza una aplicación esa clave o contraseña.</span><span class="sxs-lookup"><span data-stu-id="c023a-109">It then shows you how an application can then use that key or password.</span></span>

<span data-ttu-id="c023a-110">**Estimado toocomplete de tiempo:** 20 minutos</span><span class="sxs-lookup"><span data-stu-id="c023a-110">**Estimated time toocomplete:** 20 minutes</span></span>

> [!NOTE]
> <span data-ttu-id="c023a-111">Este tutorial no incluye instrucciones sobre cómo toowrite Hola aplicación de Azure que incluye uno de los pasos de hello, que muestra cómo tooauthorize una toouse una clave de aplicación o un secreto de clave de hello almacén.</span><span class="sxs-lookup"><span data-stu-id="c023a-111">This tutorial does not include instructions on how toowrite hello Azure application that one of hello steps includes, which shows how tooauthorize an application toouse a key or secret in hello key vault.</span></span>
> 
> <span data-ttu-id="c023a-112">Actualmente, no se puede configurar el almacén de claves de Azure en hello portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="c023a-112">Currently, you cannot configure Azure Key Vault in hello Azure portal.</span></span> <span data-ttu-id="c023a-113">En su lugar, use estas instrucciones sobre la interfaz de la línea de comandos multiplataforma.</span><span class="sxs-lookup"><span data-stu-id="c023a-113">Instead, use these Cross-Platform Command-Line Interface  instructions.</span></span> <span data-ttu-id="c023a-114">O bien, para obtener instrucciones de Azure PowerShell, consulte [este tutorial equivalente](key-vault-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="c023a-114">Or, for Azure PowerShell instructions, see [this equivalent tutorial](key-vault-get-started.md).</span></span>
> 
> 

<span data-ttu-id="c023a-115">Para obtener información general sobre el Almacén de claves de Azure, consulte [¿Qué es el Almacén de clave de Azure?](key-vault-whatis.md)</span><span class="sxs-lookup"><span data-stu-id="c023a-115">For overview information about Azure Key Vault, see [What is Azure Key Vault?](key-vault-whatis.md)</span></span>

## <a name="prerequisites"></a><span data-ttu-id="c023a-116">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="c023a-116">Prerequisites</span></span>

<span data-ttu-id="c023a-117">toocomplete este tutorial, debe tener Hola siguientes:</span><span class="sxs-lookup"><span data-stu-id="c023a-117">toocomplete this tutorial, you must have hello following:</span></span>

* <span data-ttu-id="c023a-118">Un tooMicrosoft de suscripción de Azure.</span><span class="sxs-lookup"><span data-stu-id="c023a-118">A subscription tooMicrosoft Azure.</span></span> <span data-ttu-id="c023a-119">Si no tiene una, puede registrarse para obtener una versión de [evaluación gratuita](https://azure.microsoft.com/pricing/free-trial).</span><span class="sxs-lookup"><span data-stu-id="c023a-119">If you do not have one, you can sign up for a [free trial](https://azure.microsoft.com/pricing/free-trial).</span></span>
* <span data-ttu-id="c023a-120">Versión 0.9.1 o una posterior de la interfaz de la línea de comandos.</span><span class="sxs-lookup"><span data-stu-id="c023a-120">Command-Line Interface version 0.9.1 or later.</span></span> <span data-ttu-id="c023a-121">tooinstall Hola versión más reciente y conectar tooyour suscripción de Azure, consulte [instalar y configurar la interfaz de línea de comandos entre plataformas de Azure de Hola](../cli-install-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="c023a-121">tooinstall hello latest version and connect tooyour Azure subscription, see [Install and Configure hello Azure Cross-Platform Command-Line Interface](../cli-install-nodejs.md).</span></span>
* <span data-ttu-id="c023a-122">Una aplicación para que esté configurado toouse clave de Hola o la contraseña que creará en este tutorial.</span><span class="sxs-lookup"><span data-stu-id="c023a-122">An application that will be configured toouse hello key or password that you create in this tutorial.</span></span> <span data-ttu-id="c023a-123">Una aplicación de ejemplo está disponible en hello [Microsoft Download Center](http://www.microsoft.com/download/details.aspx?id=45343).</span><span class="sxs-lookup"><span data-stu-id="c023a-123">A sample application is available from hello [Microsoft Download Center](http://www.microsoft.com/download/details.aspx?id=45343).</span></span> <span data-ttu-id="c023a-124">Para obtener instrucciones, consulte Hola que acompaña a archivo Léame.</span><span class="sxs-lookup"><span data-stu-id="c023a-124">For instructions, see hello accompanying Readme file.</span></span>

## <a name="getting-help-with-azure-cross-platform-command-line-interface"></a><span data-ttu-id="c023a-125">Obtención de ayuda con la interfaz de la línea de comandos entre plataformas de Azure</span><span class="sxs-lookup"><span data-stu-id="c023a-125">Getting help with Azure Cross-Platform Command-Line Interface</span></span>

<span data-ttu-id="c023a-126">Este tutorial se da por supuesto que está familiarizado con la interfaz de línea de comandos de hello (intensiva de errores, Terminal, símbolo del sistema)</span><span class="sxs-lookup"><span data-stu-id="c023a-126">This tutorial assumes that you are familiar with hello command-line interface (Bash, Terminal, Command prompt)</span></span>

<span data-ttu-id="c023a-127">Hello--ayuda o -h parámetro puede ser utilizados tooview ayuda para comandos específicos.</span><span class="sxs-lookup"><span data-stu-id="c023a-127">hello --help or -h parameter can be used tooview help for specific commands.</span></span> <span data-ttu-id="c023a-128">Como alternativa, help hello azure [comando] [opciones] formato también puede ser usado tooreturn Hola misma información.</span><span class="sxs-lookup"><span data-stu-id="c023a-128">Alternately, hello azure help [command] [options] format can also be used tooreturn hello same information.</span></span> <span data-ttu-id="c023a-129">Por ejemplo, siguiente Hola comandos devuelven todos los Hola la misma información:</span><span class="sxs-lookup"><span data-stu-id="c023a-129">For example, hello following commands all return hello same information:</span></span>

    azure account set --help

    azure account set -h

    azure help account set

<span data-ttu-id="c023a-130">En caso de duda acerca de los parámetros de hello necesarios para un comando, consulte usar toohelp--ayuda, -h o azure help [comando].</span><span class="sxs-lookup"><span data-stu-id="c023a-130">When in doubt about hello parameters needed by a command, refer toohelp using --help, -h or azure help [command].</span></span>

<span data-ttu-id="c023a-131">También puede leer Hola después tutoriales tooget familiarizado con Azure Resource Manager en el interfaz de línea de comandos de plataforma cruzada de Azure:</span><span class="sxs-lookup"><span data-stu-id="c023a-131">You can also read hello following tutorials tooget familiar with Azure Resource Manager in Azure Cross-Platform Command-Line Interface:</span></span>

* [<span data-ttu-id="c023a-132">¿Cómo tooinstall y configurar la interfaz de línea de comandos entre plataformas de Azure</span><span class="sxs-lookup"><span data-stu-id="c023a-132">How tooinstall and configure Azure Cross-Platform Command Line Interface</span></span>](../cli-install-nodejs.md)
* [<span data-ttu-id="c023a-133">Uso de la interfaz de la línea de comandos entre plataformas de Azure con el Administrador de recursos de Azure</span><span class="sxs-lookup"><span data-stu-id="c023a-133">Using Azure Cross-Platform Command-Line Interface with Azure Resource Manager</span></span>](../xplat-cli-azure-resource-manager.md)

## <a name="connect-tooyour-subscriptions"></a><span data-ttu-id="c023a-134">Conectar tooyour suscripciones</span><span class="sxs-lookup"><span data-stu-id="c023a-134">Connect tooyour subscriptions</span></span>

<span data-ttu-id="c023a-135">toolog sesión con una cuenta profesional, Hola de uso siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="c023a-135">toolog in using an organizational account, use hello following command:</span></span>

    azure login -u username -p password

<span data-ttu-id="c023a-136">o si desea toolog escribiendo interactivamente</span><span class="sxs-lookup"><span data-stu-id="c023a-136">or if you want toolog in by typing interactively</span></span>

    azure login

> [!NOTE]
> <span data-ttu-id="c023a-137">método de inicio de sesión de Hello solo funciona con la cuenta de la organización.</span><span class="sxs-lookup"><span data-stu-id="c023a-137">hello login method only works with organizational account.</span></span> <span data-ttu-id="c023a-138">Una cuenta profesional es un usuario administrado por su organización y definido en su inquilino de Azure Active Directory de la organización.</span><span class="sxs-lookup"><span data-stu-id="c023a-138">An organizational account is a user that is managed by your organization, and defined in your organization's Azure Active Directory tenant.</span></span>
> 
> 

<span data-ttu-id="c023a-139">Si no tiene actualmente una cuenta profesional y está usando un toolog de cuenta de Microsoft en tooyour suscripción de Azure, puede crear fácilmente uno que use Hola lo siguiente.</span><span class="sxs-lookup"><span data-stu-id="c023a-139">If you do not currently have an organizational account, and are using a Microsoft account toolog in tooyour Azure subscription, you can easily create one using hello following steps.</span></span>

1. <span data-ttu-id="c023a-140">Toohello de inicio de sesión de inicio de sesión toohello [Portal de administración de Azure](https://manage.windowsazure.com/)y haga clic en Active Directory.</span><span class="sxs-lookup"><span data-stu-id="c023a-140">Login toohello Login toohello [Azure Management Portal](https://manage.windowsazure.com/), and click on Active Directory.</span></span>
2. <span data-ttu-id="c023a-141">Si no existe ningún directorio, seleccione crear su directorio y Hola de proporcionar la información solicitada.</span><span class="sxs-lookup"><span data-stu-id="c023a-141">If no directory exists, select Create your directory and provide hello requested information.</span></span>
3. <span data-ttu-id="c023a-142">Seleccione su directorio y agregue un nuevo usuario.</span><span class="sxs-lookup"><span data-stu-id="c023a-142">Select your directory and add a new user.</span></span> <span data-ttu-id="c023a-143">Este nuevo usuario es una cuenta profesional.</span><span class="sxs-lookup"><span data-stu-id="c023a-143">This new user is an organizational account.</span></span> <span data-ttu-id="c023a-144">Durante la creación del usuario de Hola Hola será proporcionado con una dirección de correo electrónico para el usuario de hello y una contraseña temporal.</span><span class="sxs-lookup"><span data-stu-id="c023a-144">During hello creation of hello user, you will be supplied with both an e-mail address for hello user and a temporary password.</span></span> <span data-ttu-id="c023a-145">Guarde esta información para usarla en otro paso.</span><span class="sxs-lookup"><span data-stu-id="c023a-145">Save this information as it is used in another step.</span></span>
4. <span data-ttu-id="c023a-146">En el portal de hello, seleccione Configuración y, a continuación, seleccione los administradores.</span><span class="sxs-lookup"><span data-stu-id="c023a-146">From hello portal, select Settings and then select Administrators.</span></span> <span data-ttu-id="c023a-147">Seleccione Agregar y agregar Hola nuevo usuario como Coadministrador.</span><span class="sxs-lookup"><span data-stu-id="c023a-147">Select Add, and add hello new user as a co-administrator.</span></span> <span data-ttu-id="c023a-148">Esto permite Hola cuenta profesional toomanage su suscripción de Azure.</span><span class="sxs-lookup"><span data-stu-id="c023a-148">This allows hello organizational account toomanage your Azure subscription.</span></span>
5. <span data-ttu-id="c023a-149">Por último, cierre la sesión de hello portal de Azure y, a continuación, volver a iniciar sesión con la nueva cuenta organizativa de Hola.</span><span class="sxs-lookup"><span data-stu-id="c023a-149">Finally, log out of hello Azure portal and then log back in using hello new organizational account.</span></span> <span data-ttu-id="c023a-150">Si ésta es la primera vez que inicia sesión con esta cuenta de hello, será la contraseña de hello toochange solicitadas.</span><span class="sxs-lookup"><span data-stu-id="c023a-150">If this is hello first time logging in with this account, you will be prompted toochange hello password.</span></span>

<span data-ttu-id="c023a-151">Para obtener más información acerca de cómo usar una cuenta profesional con Microsoft Azure, consulte [Inicio de sesión como organización en Microsoft Azure](../active-directory/sign-up-organization.md).</span><span class="sxs-lookup"><span data-stu-id="c023a-151">For more information about using an organizational account with Microsoft Azure, see [Sign up for Microsoft Azure as an Organization](../active-directory/sign-up-organization.md).</span></span>

<span data-ttu-id="c023a-152">Si tiene varias suscripciones y desea toospecify un uno toouse específico para el almacén de claves de Azure, escriba Hola siguiendo las suscripciones de hello toosee para su cuenta:</span><span class="sxs-lookup"><span data-stu-id="c023a-152">If you have multiple subscriptions and want toospecify a specific one toouse for Azure Key Vault, type hello following toosee hello subscriptions for your account:</span></span>

    azure account list

<span data-ttu-id="c023a-153">A continuación, toospecify Hola suscripción toouse, tipo:</span><span class="sxs-lookup"><span data-stu-id="c023a-153">Then, toospecify hello subscription toouse, type:</span></span>

    azure account set <subscription name>

<span data-ttu-id="c023a-154">Para obtener más información acerca de cómo configurar la interfaz de línea de comandos entre plataformas de Azure, consulte [cómo tooInstall y configurar Azure multiplataforma de línea de comandos interfaz](../cli-install-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="c023a-154">For more information about configuring Azure Cross-Platform Command-Line Interface, see [How tooInstall and Configure Azure Cross-Platform Command-Line Interface](../cli-install-nodejs.md).</span></span>

## <a name="switch-toousing-azure-resource-manager"></a><span data-ttu-id="c023a-155">Conmutador toousing Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="c023a-155">Switch toousing Azure Resource Manager</span></span>
<span data-ttu-id="c023a-156">Hola el almacén de claves requiere Azure Resource Manager, así que escriba Hola siguiendo el modo de tooswitch tooAzure Resource Manager:</span><span class="sxs-lookup"><span data-stu-id="c023a-156">hello Key Vault requires Azure Resource Manager, so type hello following tooswitch tooAzure Resource Manager mode:</span></span>

    azure config mode arm

## <a name="create-a-new-resource-group"></a><span data-ttu-id="c023a-157">Creación de un nuevo grupo de recursos</span><span class="sxs-lookup"><span data-stu-id="c023a-157">Create a new resource group</span></span>
<span data-ttu-id="c023a-158">Cuando se utiliza el Administrador de recursos de Azure, todos los recursos relacionados se crean dentro de un grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="c023a-158">When using Azure Resource Manager, all related resources are created inside a resource group.</span></span> <span data-ttu-id="c023a-159">Crearemos un nuevo grupo de recursos denominado 'ContosoResourceGroup' para este tutorial.</span><span class="sxs-lookup"><span data-stu-id="c023a-159">We will create a new resource group 'ContosoResourceGroup' for this tutorial.</span></span>

    azure group create 'ContosoResourceGroup' 'East Asia'

<span data-ttu-id="c023a-160">Hola primer parámetro es el nombre del grupo de recursos y Hola segundo parámetro es la ubicación de Hola.</span><span class="sxs-lookup"><span data-stu-id="c023a-160">hello first parameter is resource group name and hello second parameter is hello location.</span></span> <span data-ttu-id="c023a-161">Para la ubicación, utilice el comando de hello `azure location list` tooidentify cómo toospecify una ubicación alternativa toohello uno en este ejemplo.</span><span class="sxs-lookup"><span data-stu-id="c023a-161">For location, use hello command `azure location list` tooidentify how toospecify an alternative location toohello one in this example.</span></span> <span data-ttu-id="c023a-162">Si necesita más información, escriba: `azure help location`</span><span class="sxs-lookup"><span data-stu-id="c023a-162">If you need more information, type: `azure help location`</span></span>

## <a name="register-hello-key-vault-resource-provider"></a><span data-ttu-id="c023a-163">Registrar el proveedor de recursos de almacén de claves de Hola</span><span class="sxs-lookup"><span data-stu-id="c023a-163">Register hello Key Vault resource provider</span></span>
<span data-ttu-id="c023a-164">Asegúrese de que el proveedor de recursos de Almacén de claves está registrado en la suscripción:</span><span class="sxs-lookup"><span data-stu-id="c023a-164">Make sure that Key Vault resource provider is registered in your subscription:</span></span>

`azure provider register Microsoft.KeyVault`

<span data-ttu-id="c023a-165">Solo es necesario toobe efectuar una vez por cada suscripción.</span><span class="sxs-lookup"><span data-stu-id="c023a-165">This only needs toobe done once per subscription.</span></span>

## <a name="create-a-key-vault"></a><span data-ttu-id="c023a-166">Creación de un Almacén de claves</span><span class="sxs-lookup"><span data-stu-id="c023a-166">Create a key vault</span></span>

<span data-ttu-id="c023a-167">Hola de uso `azure keyvault create` comando toocreate un almacén de claves.</span><span class="sxs-lookup"><span data-stu-id="c023a-167">Use hello `azure keyvault create` command toocreate a key vault.</span></span> <span data-ttu-id="c023a-168">Esta secuencia de comandos tiene tres parámetros obligatorios: un nombre de grupo de recursos, un nombre de almacén de claves y la ubicación geográfica de Hola.</span><span class="sxs-lookup"><span data-stu-id="c023a-168">This script has three mandatory parameters: a resource group name, a key vault name, and hello geographic location.</span></span>

<span data-ttu-id="c023a-169">Por ejemplo, si utiliza el nombre de almacén de Hola de ContosoKeyVault, nombre de grupo de recursos de Hola de ContosoResourceGroup y la ubicación de Hola de Asia oriental, escriba:</span><span class="sxs-lookup"><span data-stu-id="c023a-169">For example, if you use hello vault name of ContosoKeyVault, hello resource group name of ContosoResourceGroup, and hello location of East Asia, type:</span></span>

    azure keyvault create --vault-name 'ContosoKeyVault' --resource-group 'ContosoResourceGroup' --location 'East Asia'

<span data-ttu-id="c023a-170">salida de Hello de este comando muestra propiedades del almacén de claves de Hola que acaba de crear.</span><span class="sxs-lookup"><span data-stu-id="c023a-170">hello output of this command shows properties of hello key vault that you've just created.</span></span> <span data-ttu-id="c023a-171">propiedades de Hello dos más importantes son:</span><span class="sxs-lookup"><span data-stu-id="c023a-171">hello two most important properties are:</span></span>

* <span data-ttu-id="c023a-172">**Nombre**: en el ejemplo de Hola es ContosoKeyVault.</span><span class="sxs-lookup"><span data-stu-id="c023a-172">**Name**: In hello example this is ContosoKeyVault.</span></span> <span data-ttu-id="c023a-173">Utilizará este nombre para otros cmdlets del Almacén de claves.</span><span class="sxs-lookup"><span data-stu-id="c023a-173">You will use this name for other Key Vault cmdlets.</span></span>
* <span data-ttu-id="c023a-174">**vaultUri**: en el ejemplo de Hola es https://contosokeyvault.vault.azure.net.</span><span class="sxs-lookup"><span data-stu-id="c023a-174">**vaultUri**: In hello example this is https://contosokeyvault.vault.azure.net.</span></span> <span data-ttu-id="c023a-175">Las aplicaciones que utilizan el almacén a través de su API de REST deben usar este identificador URI.</span><span class="sxs-lookup"><span data-stu-id="c023a-175">Applications that use your vault through its REST API must use this URI.</span></span>

<span data-ttu-id="c023a-176">Su cuenta de Azure es ahora tooperform autorizado cualquier operación en esta clave de seguridad del almacén.</span><span class="sxs-lookup"><span data-stu-id="c023a-176">Your Azure account is now authorized tooperform any operations on this key vault.</span></span> <span data-ttu-id="c023a-177">Hasta el momento, nadie más lo está.</span><span class="sxs-lookup"><span data-stu-id="c023a-177">As yet, nobody else is.</span></span>

## <a name="add-a-key-or-secret-toohello-key-vault"></a><span data-ttu-id="c023a-178">Agregar una clave o un almacén de claves secretas toohello</span><span class="sxs-lookup"><span data-stu-id="c023a-178">Add a key or secret toohello key vault</span></span>

<span data-ttu-id="c023a-179">Si desea que el almacén de claves de Azure toocreate una clave protegida por software automáticamente, use hello `azure key create` de comandos y escriba Hola siguiente:</span><span class="sxs-lookup"><span data-stu-id="c023a-179">If you want Azure Key Vault toocreate a software-protected key for you, use hello `azure key create` command, and type hello following:</span></span>

    azure keyvault key create --vault-name 'ContosoKeyVault' --key-name 'ContosoFirstKey' --destination software

<span data-ttu-id="c023a-180">Sin embargo, si tiene una clave existente en un archivo PEM guardado como archivo local en un archivo denominado softkey.pem que desea tooupload tooAzure el almacén de claves, escriba Hola siguientes clave de hello tooimport de Hola. Archivo PEM, que protege la clave de hello mediante software en hello servicio Almacén de claves:</span><span class="sxs-lookup"><span data-stu-id="c023a-180">However, if you have an existing key in a .pem file saved as local file in a file named softkey.pem that you want tooupload tooAzure Key Vault, type hello following tooimport hello key from hello .PEM file, which protects hello key by software in hello Key Vault service:</span></span>

    azure keyvault key import --vault-name 'ContosoKeyVault' --key-name 'ContosoFirstKey' --pem-file './softkey.pem' --password 'PaSSWORD' --destination software

<span data-ttu-id="c023a-181">Ahora puede hacer referencia a clave de Hola que creó o cargó tooAzure el almacén de claves, utilizando su URI.</span><span class="sxs-lookup"><span data-stu-id="c023a-181">You can now reference hello key that you created or uploaded tooAzure Key Vault, by using its URI.</span></span> <span data-ttu-id="c023a-182">Usar **https://ContosoKeyVault.vault.azure.net/keys/ContosoFirstKey** tooalways obtener la versión actual de Hola y usar **https://ContosoKeyVault.vault.azure.net/keys/ContosoFirstKey/ cgacf4f763ar42ffb0a1gca546aygd87** tooget esta versión específica.</span><span class="sxs-lookup"><span data-stu-id="c023a-182">Use  **https://ContosoKeyVault.vault.azure.net/keys/ContosoFirstKey** tooalways get hello current version, and use **https://ContosoKeyVault.vault.azure.net/keys/ContosoFirstKey/cgacf4f763ar42ffb0a1gca546aygd87** tooget this specific version.</span></span>

<span data-ttu-id="c023a-183">tooadd un almacén toohello secreta, que es una contraseña denominada SQLPassword y no tiene valor de Hola de Pa$ $w0rd tooAzure el almacén de claves, Hola de tipo siguientes:</span><span class="sxs-lookup"><span data-stu-id="c023a-183">tooadd a secret toohello vault, which is a password named SQLPassword and that has hello value of Pa$$w0rd tooAzure Key Vault, type hello following:</span></span>

    azure keyvault secret set --vault-name 'ContosoKeyVault' --secret-name 'SQLPassword' --value 'Pa$$w0rd'

<span data-ttu-id="c023a-184">Ahora puede hacer referencia a esta contraseña que agregó tooAzure el almacén de claves, mediante el uso de su URI.</span><span class="sxs-lookup"><span data-stu-id="c023a-184">You can now reference this password that you added tooAzure Key Vault, by using its URI.</span></span> <span data-ttu-id="c023a-185">Usar **https://ContosoVault.vault.azure.net/secrets/SQLPassword** tooalways obtener la versión actual de Hola y usar **https://ContosoVault.vault.azure.net/secrets/SQLPassword/ 90018dbb96a84117a0d2847ef8e7189d** tooget esta versión específica.</span><span class="sxs-lookup"><span data-stu-id="c023a-185">Use **https://ContosoVault.vault.azure.net/secrets/SQLPassword** tooalways get hello current version, and use **https://ContosoVault.vault.azure.net/secrets/SQLPassword/90018dbb96a84117a0d2847ef8e7189d** tooget this specific version.</span></span>

<span data-ttu-id="c023a-186">Vamos a ver clave de Hola o el secreto que acaba de crear:</span><span class="sxs-lookup"><span data-stu-id="c023a-186">Let's view hello key or secret that you just created:</span></span>

* <span data-ttu-id="c023a-187">tooview el tipo de clave,:`azure keyvault key list --vault-name 'ContosoKeyVault'`</span><span class="sxs-lookup"><span data-stu-id="c023a-187">tooview your key, type: `azure keyvault key list --vault-name 'ContosoKeyVault'`</span></span>
* <span data-ttu-id="c023a-188">tooview el secreto, tipo:`azure keyvault secret list --vault-name 'ContosoKeyVault'`</span><span class="sxs-lookup"><span data-stu-id="c023a-188">tooview your secret, type: `azure keyvault secret list --vault-name 'ContosoKeyVault'`</span></span>

## <a name="register-an-application-with-azure-active-directory"></a><span data-ttu-id="c023a-189">Registro de una aplicación con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="c023a-189">Register an application with Azure Active Directory</span></span>

<span data-ttu-id="c023a-190">Este paso lo haría normalmente un programador en un equipo independiente.</span><span class="sxs-lookup"><span data-stu-id="c023a-190">This step would usually be done by a developer, on a separate computer.</span></span> <span data-ttu-id="c023a-191">No es específico tooAzure el almacén de claves, pero se incluye aquí para integridad.</span><span class="sxs-lookup"><span data-stu-id="c023a-191">It is not specific tooAzure Key Vault but is included here, for completeness.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="c023a-192">tutorial de hello toocomplete, tu cuenta, el almacén de Hola y aplicación hello que se registren en este paso deben ser Hola mismo directorio de Azure.</span><span class="sxs-lookup"><span data-stu-id="c023a-192">toocomplete hello tutorial, your account, hello vault, and hello application that you will register in this step must all be in hello same Azure directory.</span></span>
> 
> 

<span data-ttu-id="c023a-193">Las aplicaciones que utilizan un Almacén de claves deben autenticarse utilizando un token de Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="c023a-193">Applications that use a key vault must authenticate by using a token from Azure Active Directory.</span></span> <span data-ttu-id="c023a-194">toodo, Hola propietario de la aplicación hello en primer lugar debe registrar la aplicación hello en su Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="c023a-194">toodo this, hello owner of hello application must first register hello application in their Azure Active Directory.</span></span> <span data-ttu-id="c023a-195">Al final de Hola de registro, propietario de la aplicación hello obtiene Hola siguientes valores:</span><span class="sxs-lookup"><span data-stu-id="c023a-195">At hello end of registration, hello application owner gets hello following values:</span></span>

* <span data-ttu-id="c023a-196">Un **Id. de aplicación** (también conocido como un Id. de cliente) y **clave de autenticación** (también conocido como Hola secreto compartido).</span><span class="sxs-lookup"><span data-stu-id="c023a-196">An **Application ID** (also known as a Client ID) and **authentication key** (also known as hello shared secret).</span></span> <span data-ttu-id="c023a-197">aplicación Hello debe presentar ambos de estos tooAzure valores tooget un símbolo (token) de Active Directory.</span><span class="sxs-lookup"><span data-stu-id="c023a-197">hello application must present both of these values tooAzure Active Directory, tooget a token.</span></span> <span data-ttu-id="c023a-198">Forma de la aplicación hello configurado toodo que esto depende de la aplicación hello.</span><span class="sxs-lookup"><span data-stu-id="c023a-198">How hello application is configured toodo this depends on hello application.</span></span> <span data-ttu-id="c023a-199">Para la aplicación de ejemplo de almacén de claves de hello, propietario de la aplicación hello establece estos valores en el archivo app.config de hello.</span><span class="sxs-lookup"><span data-stu-id="c023a-199">For hello Key Vault sample application, hello application owner sets these values in hello app.config file.</span></span>

<span data-ttu-id="c023a-200">aplicación de hello tooregister en Azure Active Directory:</span><span class="sxs-lookup"><span data-stu-id="c023a-200">tooregister hello application in Azure Active Directory:</span></span>

1. <span data-ttu-id="c023a-201">Inicie sesión en toohello portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="c023a-201">Sign in toohello Azure portal.</span></span>
2. <span data-ttu-id="c023a-202">Hola izquierda, haga clic en **Active Directory**y, a continuación, seleccione directorio de hello en el que se vaya a registrar la aplicación.</span><span class="sxs-lookup"><span data-stu-id="c023a-202">On hello left, click **Active Directory**, and then select hello directory in which you will register your application.</span></span> <br> <br> 

>[!NOTE] 
> <span data-ttu-id="c023a-203">Debe seleccionar Hola mismo directorio que contiene Hola suscripción de Azure con la que se creó el almacén de claves.</span><span class="sxs-lookup"><span data-stu-id="c023a-203">You must select hello same directory that contains hello Azure subscription with which you created your key vault.</span></span> <span data-ttu-id="c023a-204">Si no sabe qué directorio esto es, haga clic en **configuración**, identificar suscripción Hola con la que se creó el almacén de claves y muestra el nombre de Hola de nota del directorio de hello en la última columna de Hola.</span><span class="sxs-lookup"><span data-stu-id="c023a-204">If you do not know which directory this is, click **Settings**, identify hello subscription with which you created your key vault, and note hello name of hello directory displayed in hello last column.</span></span>

3. <span data-ttu-id="c023a-205">Haga clic en **Aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="c023a-205">Click **APPLICATIONS**.</span></span> <span data-ttu-id="c023a-206">Si no hay aplicaciones se han agregado tooyour directorio, esta página mostrará solo hello **agregar una aplicación** vínculo.</span><span class="sxs-lookup"><span data-stu-id="c023a-206">If no apps have been added tooyour directory, this page will show only hello **Add an App** link.</span></span> <span data-ttu-id="c023a-207">Haga clic en el vínculo de Hola o, como alternativa, puede hacer clic en hello **agregar** en la barra de comandos de Hola.</span><span class="sxs-lookup"><span data-stu-id="c023a-207">Click hello link, or alternatively, you can click hello **ADD** on hello command bar.</span></span>
4. <span data-ttu-id="c023a-208">Hola **Agregar aplicación** asistente, en hello **especifique qué desea toodo?** página, haga clic en **agregar una aplicación que mi organización está desarrollando**.</span><span class="sxs-lookup"><span data-stu-id="c023a-208">In hello **ADD APPLICATION** wizard, on hello **What do you want toodo?** page, click **Add an application my organization is developing**.</span></span>
5. <span data-ttu-id="c023a-209">En hello **envíenos comentarios acerca de la aplicación** página, especifique un nombre para la aplicación y seleccione **aplicación WEB Y/O API de WEB** (Hola de forma predeterminada).</span><span class="sxs-lookup"><span data-stu-id="c023a-209">On hello **Tell us about your application** page, specify a name for your application and select **WEB APPLICATION AND/OR WEB API** (hello default).</span></span> <span data-ttu-id="c023a-210">Haga clic en el icono siguiente Hola.</span><span class="sxs-lookup"><span data-stu-id="c023a-210">Click hello Next icon.</span></span>
6. <span data-ttu-id="c023a-211">En hello **propiedades de la aplicación** página, especifique hello **dirección URL de inicio de sesión** y **APP ID URI** para la aplicación web.</span><span class="sxs-lookup"><span data-stu-id="c023a-211">On hello **App properties** page, specify hello **SIGN-ON URL** and **APP ID URI** for your web application.</span></span> <span data-ttu-id="c023a-212">Si la aplicación no tiene estos valores, puede inventárselos en este paso (por ejemplo, puede especificar http://test1.contoso.com en ambos cuadros).</span><span class="sxs-lookup"><span data-stu-id="c023a-212">If your application does not have these values, you can make them up for this step (for example, you could specify http://test1.contoso.com for both boxes).</span></span> <span data-ttu-id="c023a-213">No importa estos sitios, si existen. lo importante es que esa aplicación hello identificador URI para cada aplicación es diferente para cada aplicación en el directorio.</span><span class="sxs-lookup"><span data-stu-id="c023a-213">It does not matter if these sites exist; what is important is that hello app ID URI for each application is different for every application in your directory.</span></span> <span data-ttu-id="c023a-214">directorio de Hello usa este tooidentify de cadena de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="c023a-214">hello directory uses this string tooidentify your app.</span></span>
7. <span data-ttu-id="c023a-215">Haga clic en hello icono completa toosave los cambios en el Asistente de Hola.</span><span class="sxs-lookup"><span data-stu-id="c023a-215">Click hello Complete icon toosave your changes in hello wizard.</span></span>
8. <span data-ttu-id="c023a-216">En la página de inicio rápido de hello, haga clic en **configurar**.</span><span class="sxs-lookup"><span data-stu-id="c023a-216">On hello Quick Start page, click **CONFIGURE**.</span></span>
9. <span data-ttu-id="c023a-217">Desplácese toohello **claves** sección, seleccione la duración de hello y, a continuación, haga clic en **guardar**.</span><span class="sxs-lookup"><span data-stu-id="c023a-217">Scroll toohello **keys** section, select hello duration, and then click **SAVE**.</span></span> <span data-ttu-id="c023a-218">página de Hello actualiza y muestra ahora un valor de clave.</span><span class="sxs-lookup"><span data-stu-id="c023a-218">hello page refreshes and now shows a key value.</span></span> <span data-ttu-id="c023a-219">Debe configurar la aplicación con este valor de clave y hello **Id. de cliente** valor.</span><span class="sxs-lookup"><span data-stu-id="c023a-219">You must configure your application with this key value and hello **CLIENT ID** value.</span></span> <span data-ttu-id="c023a-220">(Las instrucciones para realizar esta configuración serán específicas para la aplicación).</span><span class="sxs-lookup"><span data-stu-id="c023a-220">(Instructions for this configuration will be application-specific.)</span></span>
10. <span data-ttu-id="c023a-221">Copie el valor de identificador de cliente de Hola desde esta página, que se usará en el siguiente paso tooset permisos de hello en el almacén.</span><span class="sxs-lookup"><span data-stu-id="c023a-221">Copy hello client ID value from this page, which you will use in hello next step tooset permissions on your vault.</span></span>

## <a name="authorize-hello-application-toouse-hello-key-or-secret"></a><span data-ttu-id="c023a-222">Autorizar Hola aplicación toouse Hola clave o el secreto</span><span class="sxs-lookup"><span data-stu-id="c023a-222">Authorize hello application toouse hello key or secret</span></span>
<span data-ttu-id="c023a-223">tooauthorize Hola aplicación tooaccess Hola clave o el secreto en el almacén de hello, use hello `azure keyvault set-policy` comando.</span><span class="sxs-lookup"><span data-stu-id="c023a-223">tooauthorize hello application tooaccess hello key or secret in hello vault, use hello `azure keyvault set-policy` command.</span></span>

<span data-ttu-id="c023a-224">Por ejemplo, si el nombre del almacén es aplicación hello y ContosoKeyVault desea tooauthorize tiene un identificador de cliente de 8f8c4bbd 485b 45fd 98f7 ec6300b7b4ed, y desea tooauthorize Hola aplicación toodecrypt e inicie sesión con las claves en el almacén, a continuación, ejecute hello Después de:</span><span class="sxs-lookup"><span data-stu-id="c023a-224">For example, if your vault name is ContosoKeyVault and hello application you want tooauthorize has a client ID of 8f8c4bbd-485b-45fd-98f7-ec6300b7b4ed, and you want tooauthorize hello application toodecrypt and sign with keys in your vault, then run hello following:</span></span>

    azure keyvault set-policy --vault-name 'ContosoKeyVault' --spn 8f8c4bbd-485b-45fd-98f7-ec6300b7b4ed --perms-to-keys '[\"decrypt\",\"sign\"]'

> [!NOTE]
> <span data-ttu-id="c023a-225">Si se ejecutan en el símbolo del sistema de Windows, debe reemplazar las comillas simples entre comillas dobles y también de escape las comillas dobles interno Hola.</span><span class="sxs-lookup"><span data-stu-id="c023a-225">If you are running on Windows command prompt, you should replace single quotes with double quotes, and also escape hello internal double quotes.</span></span> <span data-ttu-id="c023a-226">Por ejemplo: "[\"decrypt\",\"sign\"]".</span><span class="sxs-lookup"><span data-stu-id="c023a-226">For example: "[\"decrypt\",\"sign\"]".</span></span>
> 
> 

<span data-ttu-id="c023a-227">Si desea tooauthorize ese mismo secretos tooread de aplicación en el almacén, ejecute hello siguiente:</span><span class="sxs-lookup"><span data-stu-id="c023a-227">If you want tooauthorize that same application tooread secrets in your vault, run hello following:</span></span>

    azure keyvault set-policy --vault-name 'ContosoKeyVault' --spn 8f8c4bbd-485b-45fd-98f7-ec6300b7b4ed --perms-to-secrets '[\"get\"]'

## <a name="if-you-want-toouse-a-hardware-security-module-hsm"></a><span data-ttu-id="c023a-228">Si desea que toouse un módulo de seguridad de hardware (HSM)</span><span class="sxs-lookup"><span data-stu-id="c023a-228">If you want toouse a hardware security module (HSM)</span></span>
<span data-ttu-id="c023a-229">Para mayor seguridad, puede importar o generar claves en módulos de seguridad de hardware (HSM) que no dejan nunca el límite de HSM Hola.</span><span class="sxs-lookup"><span data-stu-id="c023a-229">For added assurance, you can import or generate keys in hardware security modules (HSMs) that never leave hello HSM boundary.</span></span> <span data-ttu-id="c023a-230">Hola HSM son FIPS 140-2 nivel 2 validado.</span><span class="sxs-lookup"><span data-stu-id="c023a-230">hello HSMs are FIPS 140-2 Level 2 validated.</span></span> <span data-ttu-id="c023a-231">Si este requisito no aplica tooyou, omita esta sección y vaya demasiado[eliminar el almacén de claves de Hola y las claves asociadas y secretos](#delete-the-key-vault-and-associated-keys-and-secrets).</span><span class="sxs-lookup"><span data-stu-id="c023a-231">If this requirement doesn't apply tooyou, skip this section and go too[Delete hello key vault and associated keys and secrets](#delete-the-key-vault-and-associated-keys-and-secrets).</span></span>

<span data-ttu-id="c023a-232">toocreate estas claves protegidas con HSM, debe tener una suscripción de almacén que admita claves protegidas con HSM.</span><span class="sxs-lookup"><span data-stu-id="c023a-232">toocreate these HSM-protected keys, you must have a vault subscription that supports HSM-protected keys.</span></span>

<span data-ttu-id="c023a-233">Cuando creas hello keyvault, Agregar parámetro de "sku" hello:</span><span class="sxs-lookup"><span data-stu-id="c023a-233">When you create hello keyvault, add hello 'sku' parameter:</span></span>

    azure azure keyvault create --vault-name 'ContosoKeyVaultHSM' --resource-group 'ContosoResourceGroup' --location 'East Asia' --sku 'Premium'

<span data-ttu-id="c023a-234">Puede agregar las claves protegidas por software (como se muestra anteriormente) y del almacén de claves protegidas con HSM toothis.</span><span class="sxs-lookup"><span data-stu-id="c023a-234">You can add software-protected keys (as shown earlier) and HSM-protected keys toothis vault.</span></span> <span data-ttu-id="c023a-235">toocreate una clave protegida por HSM, too'HSM del parámetro de destino de conjunto hello':</span><span class="sxs-lookup"><span data-stu-id="c023a-235">toocreate an HSM-protected key, set hello Destination parameter too'HSM':</span></span>

    azure keyvault key create --vault-name 'ContosoKeyVaultHSM' --key-name 'ContosoFirstHSMKey' --destination 'HSM'

<span data-ttu-id="c023a-236">Puede usar Hola siguientes comando tooimport una clave de un archivo PEM en el equipo.</span><span class="sxs-lookup"><span data-stu-id="c023a-236">You can use hello following command tooimport a key from a .pem file on your computer.</span></span> <span data-ttu-id="c023a-237">Este comando importa una clave hello en HSM Hola servicio Almacén de claves:</span><span class="sxs-lookup"><span data-stu-id="c023a-237">This command imports hello key into HSMs in hello Key Vault service:</span></span>

    azure keyvault key import --vault-name 'ContosoKeyVaultHSM' --key-name 'ContosoFirstHSMKey' --pem-file '/.softkey.pem' --destination 'HSM' --password 'PaSSWORD'

<span data-ttu-id="c023a-238">comando siguiente de Hello importa una opción "traiga su propia clave" paquete (BYOK).</span><span class="sxs-lookup"><span data-stu-id="c023a-238">hello next command imports a “bring your own key" (BYOK) package.</span></span> <span data-ttu-id="c023a-239">Esto le permite generar su clave de HSM local y se transfiere tooHSMs Hola servicio de almacén de claves, sin clave Hola dejando límite de HSM hello:</span><span class="sxs-lookup"><span data-stu-id="c023a-239">This lets you generate your key in your local HSM, and transfer it tooHSMs in hello Key Vault service, without hello key leaving hello HSM boundary:</span></span>

    azure keyvault key import --vault-name 'ContosoKeyVaultHSM' --key-name 'ContosoFirstHSMKey' --byok-file './ITByok.byok' --destination 'HSM'

<span data-ttu-id="c023a-240">Para obtener más instrucciones sobre cómo toogenerate este paquete BYOK, vea [cómo toouse HSM-Protected claves al almacén de claves de Azure](key-vault-hsm-protected-keys.md).</span><span class="sxs-lookup"><span data-stu-id="c023a-240">For more detailed instructions about how toogenerate this BYOK package, see [How toouse HSM-Protected Keys with Azure Key Vault](key-vault-hsm-protected-keys.md).</span></span>

## <a name="delete-hello-key-vault-and-associated-keys-and-secrets"></a><span data-ttu-id="c023a-241">Eliminar el almacén de claves de Hola y las claves asociadas y secretos</span><span class="sxs-lookup"><span data-stu-id="c023a-241">Delete hello key vault and associated keys and secrets</span></span>
<span data-ttu-id="c023a-242">Si ya no necesita el almacén de claves hello y clave de Hola o al secreto que contiene, puede eliminar el almacén de claves de hello mediante comando de eliminación de keyvault hello azure:</span><span class="sxs-lookup"><span data-stu-id="c023a-242">If you no longer need hello key vault and hello key or secret that it contains, you can delete hello key vault by using hello azure keyvault delete command:</span></span>

    azure keyvault delete --vault-name 'ContosoKeyVault'

<span data-ttu-id="c023a-243">O bien, puede eliminar un grupo de recursos de Azure completo, que incluye el almacén de claves de Hola y otros recursos que incluyen en ese grupo:</span><span class="sxs-lookup"><span data-stu-id="c023a-243">Or, you can delete an entire Azure resource group, which includes hello key vault and any other resources that you included in that group:</span></span>

    azure group delete --name 'ContosoResourceGroup'


## <a name="other-azure-cross-platform-command-line-interface-commands"></a><span data-ttu-id="c023a-244">Otros comandos de la interfaz de la línea de comandos entre plataformas de Azure</span><span class="sxs-lookup"><span data-stu-id="c023a-244">Other Azure Cross-Platform Command-line Interface Commands</span></span>
<span data-ttu-id="c023a-245">Estos son otros comandos que pueden resultar útiles para administrar el Almacén de claves de Azure.</span><span class="sxs-lookup"><span data-stu-id="c023a-245">Other commands that you might useful for managing Azure Key Vault.</span></span>

<span data-ttu-id="c023a-246">Este comando ofrece una presentación tabular de todas las claves y las propiedades seleccionadas.</span><span class="sxs-lookup"><span data-stu-id="c023a-246">This command lists a tabular display of all keys and selected properties:</span></span>

    azure keyvault key list --vault-name 'ContosoKeyVault'

<span data-ttu-id="c023a-247">Este comando muestra una lista completa de propiedades para la clave especificada de hello:</span><span class="sxs-lookup"><span data-stu-id="c023a-247">This command displays a full list of properties for hello specified key:</span></span>

    azure keyvault key show --vault-name 'ContosoKeyVault' --key-name 'ContosoFirstKey'

<span data-ttu-id="c023a-248">Este comando muestra una presentación tabular de todos nombres de secretos y las propiedades que se elijan.</span><span class="sxs-lookup"><span data-stu-id="c023a-248">This command lists a tabular display of all secret names and selected properties:</span></span>

    azure keyvault secret list --vault-name 'ContosoKeyVault'

<span data-ttu-id="c023a-249">Este es un ejemplo de cómo tooremove una clave específica:</span><span class="sxs-lookup"><span data-stu-id="c023a-249">Here's an example of how tooremove a specific key:</span></span>

    azure keyvault key delete --vault-name 'ContosoKeyVault' --key-name 'ContosoFirstKey'

<span data-ttu-id="c023a-250">Este es un ejemplo de cómo tooremove un secreto específico:</span><span class="sxs-lookup"><span data-stu-id="c023a-250">Here's an example of how tooremove a specific secret:</span></span>

    azure keyvault secret delete --vault-name 'ContosoKeyVault' --secret-name 'SQLPassword'


## <a name="next-steps"></a><span data-ttu-id="c023a-251">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="c023a-251">Next steps</span></span>
<span data-ttu-id="c023a-252">Para las referencias de programación, vea [Hola Guía del desarrollador de almacén de claves de Azure](key-vault-developers-guide.md).</span><span class="sxs-lookup"><span data-stu-id="c023a-252">For programming references, see [hello Azure Key Vault developer's guide](key-vault-developers-guide.md).</span></span>

