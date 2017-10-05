---
title: "Introducción a la CLI de Azure para Batch | Microsoft Docs"
description: "Obtenga una introducción rápida a los comandos de Batch en la CLI de Azure para administrar los recursos del servicio Azure Batch"
services: batch
documentationcenter: 
author: tamram
manager: timlt
editor: 
ms.assetid: fcd76587-1827-4bc8-a84d-bba1cd980d85
ms.service: batch
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: multiple
ms.workload: big-compute
ms.date: 07/20/2017
ms.author: tamram
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 9bee0344ba70c50cda36a87ea617906283040ff9
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/03/2017
---
# <a name="manage-batch-resources-with-azure-cli"></a><span data-ttu-id="d4ab3-103">Administración de recursos de Batch con la CLI de Azure</span><span class="sxs-lookup"><span data-stu-id="d4ab3-103">Manage Batch resources with Azure CLI</span></span>

<span data-ttu-id="d4ab3-104">La CLI 2.0 de Azure es la nueva experiencia de línea de comandos de Azure para administrar recursos de Azure.</span><span class="sxs-lookup"><span data-stu-id="d4ab3-104">The Azure CLI 2.0 is Azure's new command-line experience for managing Azure resources.</span></span> <span data-ttu-id="d4ab3-105">Se puede usar en macOS, Linux y Windows.</span><span class="sxs-lookup"><span data-stu-id="d4ab3-105">It can be used on macOS, Linux, and Windows.</span></span> <span data-ttu-id="d4ab3-106">La CLI de Azure 2.0 está optimizada para administrar recursos de Azure desde la línea de comandos.</span><span class="sxs-lookup"><span data-stu-id="d4ab3-106">Azure CLI 2.0 is optimized for managing and administering Azure resources from the command line.</span></span> <span data-ttu-id="d4ab3-107">Puede usarla para administrar cuentas de Azure Batch y administrar recursos, como grupos, trabajos y tareas.</span><span class="sxs-lookup"><span data-stu-id="d4ab3-107">You can use the Azure CLI to manage your Azure Batch accounts and to manage resources such as pools, jobs, and tasks.</span></span> <span data-ttu-id="d4ab3-108">Con la CLI de Azure, puede realizar mediante scripts muchas de las mismas tareas que lleva a cabo con las API de Batch, Azure Portal y los cmdlets PowerShell de Batch.</span><span class="sxs-lookup"><span data-stu-id="d4ab3-108">With the Azure CLI, you can script many of the same tasks you carry out with the Batch APIs, Azure portal, and Batch PowerShell cmdlets.</span></span>

<span data-ttu-id="d4ab3-109">En este artículo se proporciona una introducción al uso de la [CLI de Azure versión 2.0](https://docs.microsoft.com/cli/azure/overview) con Batch.</span><span class="sxs-lookup"><span data-stu-id="d4ab3-109">This article provides an overview of using [Azure CLI version 2.0](https://docs.microsoft.com/cli/azure/overview) with Batch.</span></span> <span data-ttu-id="d4ab3-110">Consulte [Introducción a la CLI de Azure 2.0](https://docs.microsoft.com/cli/azure/get-started-with-azure-cli) para información general sobre el uso de la CLI con Azure.</span><span class="sxs-lookup"><span data-stu-id="d4ab3-110">See [Get started with Azure CLI 2.0](https://docs.microsoft.com/cli/azure/get-started-with-azure-cli) for an overview of using the CLI with Azure.</span></span>

<span data-ttu-id="d4ab3-111">Microsoft recomienda usar la versión más reciente de la CLI de Azure, la versión 2.0.</span><span class="sxs-lookup"><span data-stu-id="d4ab3-111">Microsoft recommends using the latest version of the Azure CLI, version 2.0.</span></span> <span data-ttu-id="d4ab3-112">Para más información acerca de la versión 2.0, consulte [Azure Command Line 2.0 now generally available](https://azure.microsoft.com/blog/announcing-general-availability-of-vm-storage-and-network-azure-cli-2-0/) (La línea de comandos de Azure 2.0 está ahora disponible con carácter general).</span><span class="sxs-lookup"><span data-stu-id="d4ab3-112">For more information about version 2.0, see [Azure Command Line 2.0 now generally available](https://azure.microsoft.com/blog/announcing-general-availability-of-vm-storage-and-network-azure-cli-2-0/).</span></span>

## <a name="set-up-the-azure-cli"></a><span data-ttu-id="d4ab3-113">Configuración de la CLI de Azure</span><span class="sxs-lookup"><span data-stu-id="d4ab3-113">Set up the Azure CLI</span></span>

<span data-ttu-id="d4ab3-114">Para instalar la CLI de Azure, siga los pasos descritos en [Instalación de la CLI de Azure](https://docs.microsoft.com/cli/azure/install-azure-cli.md).</span><span class="sxs-lookup"><span data-stu-id="d4ab3-114">To install the Azure CLI, follow the steps outlined in [Install the Azure CLI](https://docs.microsoft.com/cli/azure/install-azure-cli.md).</span></span>

> [!TIP]
> <span data-ttu-id="d4ab3-115">Se recomienda actualizar su instalación de la CLI de Azure con frecuencia para aprovechar las mejoras y actualizaciones del servicio.</span><span class="sxs-lookup"><span data-stu-id="d4ab3-115">We recommend that you update your Azure CLI installation frequently to take advantage of service updates and enhancements.</span></span>
> 
> 

## <a name="command-help"></a><span data-ttu-id="d4ab3-116">Ayuda de comandos</span><span class="sxs-lookup"><span data-stu-id="d4ab3-116">Command help</span></span>

<span data-ttu-id="d4ab3-117">Para mostrar texto de ayuda para todos los comandos de la CLI de Azure, anexe `-h` al comando.</span><span class="sxs-lookup"><span data-stu-id="d4ab3-117">You can display help text for every command in the Azure CLI by appending `-h` to the command.</span></span> <span data-ttu-id="d4ab3-118">Omita el resto de las opciones.</span><span class="sxs-lookup"><span data-stu-id="d4ab3-118">Omit any other options.</span></span> <span data-ttu-id="d4ab3-119">Por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="d4ab3-119">For example:</span></span>

* <span data-ttu-id="d4ab3-120">Para obtener ayuda sobre el comando `az` escriba: `az -h`</span><span class="sxs-lookup"><span data-stu-id="d4ab3-120">To get help for the `az` command, enter: `az -h`</span></span>
* <span data-ttu-id="d4ab3-121">Para obtener una lista de todos los comandos de Batch en la CLI, utilice: `az batch -h`</span><span class="sxs-lookup"><span data-stu-id="d4ab3-121">To get a list of all Batch commands in the CLI, use: `az batch -h`</span></span>
* <span data-ttu-id="d4ab3-122">Para obtener ayuda acerca de la creación de una cuenta de Batch, escriba: `az batch account create -h`</span><span class="sxs-lookup"><span data-stu-id="d4ab3-122">To get help on creating a Batch account, enter: `az batch account create -h`</span></span>

<span data-ttu-id="d4ab3-123">En caso de duda, utilice la opción de línea de comandos `-h` para obtener ayuda sobre cualquier comando de CLI de Azure.</span><span class="sxs-lookup"><span data-stu-id="d4ab3-123">When in doubt, use the `-h` command-line option to get help on any Azure CLI command.</span></span>

> [!NOTE]
> <span data-ttu-id="d4ab3-124">Las versiones anteriores de la CLI de Azure usaban `azure` delante de un comando de CLI.</span><span class="sxs-lookup"><span data-stu-id="d4ab3-124">Earlier versions of the Azure CLI used `azure` to preface a CLI command.</span></span> <span data-ttu-id="d4ab3-125">En la versión 2.0, todos los comandos van precedidos de `az`.</span><span class="sxs-lookup"><span data-stu-id="d4ab3-125">In version 2.0, all commands are now prefaced with `az`.</span></span> <span data-ttu-id="d4ab3-126">Asegúrese de actualizar los scripts para que usen la nueva sintaxis con la versión 2.0.</span><span class="sxs-lookup"><span data-stu-id="d4ab3-126">Be sure to update your scripts to use the new syntax with version 2.0.</span></span>
>
>  

<span data-ttu-id="d4ab3-127">Además, consulte la documentación de referencia de la CLI de Azure para más información sobre los [comandos de la CLI de Azure para Batch](https://docs.microsoft.com/cli/azure/batch).</span><span class="sxs-lookup"><span data-stu-id="d4ab3-127">Additionally, refer to the Azure CLI reference documentation for details about [Azure CLI commands for Batch](https://docs.microsoft.com/cli/azure/batch).</span></span> 

## <a name="log-in-and-authenticate"></a><span data-ttu-id="d4ab3-128">Inicio de sesión y autenticación</span><span class="sxs-lookup"><span data-stu-id="d4ab3-128">Log in and authenticate</span></span>

<span data-ttu-id="d4ab3-129">Para utilizar la CLI de Azure con Batch, debe iniciar sesión y autenticarse.</span><span class="sxs-lookup"><span data-stu-id="d4ab3-129">To use the Azure CLI with Batch, you need to log in and authenticate.</span></span> <span data-ttu-id="d4ab3-130">Hay dos pasos sencillos que seguir:</span><span class="sxs-lookup"><span data-stu-id="d4ab3-130">There are two simple steps to follow:</span></span>

1. <span data-ttu-id="d4ab3-131">**Inicie sesión en Azure.**</span><span class="sxs-lookup"><span data-stu-id="d4ab3-131">**Log into Azure.**</span></span> <span data-ttu-id="d4ab3-132">Al iniciar sesión en Azure, logra acceso a los comandos de Azure Resource Manager, incluidos los del [servicio de administración de Batch](batch-management-dotnet.md).</span><span class="sxs-lookup"><span data-stu-id="d4ab3-132">Logging into Azure gives you access to Azure Resource Manager commands, including [Batch Management service](batch-management-dotnet.md) commands.</span></span>  
2. <span data-ttu-id="d4ab3-133">**Inicie sesión en su cuenta de Batch.**</span><span class="sxs-lookup"><span data-stu-id="d4ab3-133">**Log into your Batch account.**</span></span> <span data-ttu-id="d4ab3-134">Al iniciar sesión en su cuenta de Batch, logra acceso a los comandos del servicio Batch.</span><span class="sxs-lookup"><span data-stu-id="d4ab3-134">Logging into your Batch account gives you access to Batch service commands.</span></span>   

### <a name="log-in-to-azure"></a><span data-ttu-id="d4ab3-135">Inicie sesión en Azure.</span><span class="sxs-lookup"><span data-stu-id="d4ab3-135">Log in to Azure</span></span>

<span data-ttu-id="d4ab3-136">Hay varias maneras diferentes de iniciar sesión en Azure, las cuales se describen en detalle en [Inicio de sesión con la CLI de Azure 2.0](https://docs.microsoft.com/cli/azure/authenticate-azure-cli):</span><span class="sxs-lookup"><span data-stu-id="d4ab3-136">There are a few different ways to log into Azure, described in detail in [Log in with Azure CLI 2.0](https://docs.microsoft.com/cli/azure/authenticate-azure-cli):</span></span>

1. <span data-ttu-id="d4ab3-137">[Inicie sesión de forma interactiva](https://docs.microsoft.com/cli/azure/authenticate-azure-cli#interactive-log-in).</span><span class="sxs-lookup"><span data-stu-id="d4ab3-137">[Log in interactively](https://docs.microsoft.com/cli/azure/authenticate-azure-cli#interactive-log-in).</span></span> <span data-ttu-id="d4ab3-138">Inicie sesión de forma interactiva cuando ejecute comandos de la CLI de Azure desde la línea de comandos.</span><span class="sxs-lookup"><span data-stu-id="d4ab3-138">Log in interactively when you are running Azure CLI commands yourself from the command line.</span></span>
2. <span data-ttu-id="d4ab3-139">[Inicie sesión con una entidad de servicio](https://docs.microsoft.com/cli/azure/authenticate-azure-cli#logging-in-with-a-service-principal).</span><span class="sxs-lookup"><span data-stu-id="d4ab3-139">[Log in with a service principal](https://docs.microsoft.com/cli/azure/authenticate-azure-cli#logging-in-with-a-service-principal).</span></span> <span data-ttu-id="d4ab3-140">Inicie sesión con una entidad de servicio cuando ejecute comandos de la CLI de Azure desde un script o una aplicación.</span><span class="sxs-lookup"><span data-stu-id="d4ab3-140">Log in with a service principal when you are running Azure CLI commands from a script or an application.</span></span>

<span data-ttu-id="d4ab3-141">Para este artículo, se muestra cómo iniciar sesión de forma interactiva en Azure.</span><span class="sxs-lookup"><span data-stu-id="d4ab3-141">For the purposes of this article, we show how to log into Azure interactively.</span></span> <span data-ttu-id="d4ab3-142">Escriba [az login](https://docs.microsoft.com/cli/azure/#login) en la línea de comandos:</span><span class="sxs-lookup"><span data-stu-id="d4ab3-142">Type [az login](https://docs.microsoft.com/cli/azure/#login) on the command line:</span></span>

```azurecli
# Log in to Azure and authenticate interactively.
az login
```

<span data-ttu-id="d4ab3-143">El comando `az login` devuelve un token que puede usar para autenticarse, como se muestra aquí.</span><span class="sxs-lookup"><span data-stu-id="d4ab3-143">The `az login` command returns a token that you can use to authenticate, as shown here.</span></span> <span data-ttu-id="d4ab3-144">Siga las instrucciones proporcionadas para abrir una página web y enviar el token a Azure:</span><span class="sxs-lookup"><span data-stu-id="d4ab3-144">Follow the instructions provided to open a web page and submit the token to Azure:</span></span>

![Inicie sesión en Azure.](./media/batch-cli-get-started/az-login.png)

<span data-ttu-id="d4ab3-146">Los ejemplos en la sección [Scripts de shell de ejemplo](#sample-shell-scripts) también muestran cómo iniciar la sesión de la CLI de Azure mediante el inicio interactivo en Azure.</span><span class="sxs-lookup"><span data-stu-id="d4ab3-146">The examples listed in the [Sample shell scripts](#sample-shell-scripts) section also show how to start your Azure CLI session by logging into Azure interactively.</span></span> <span data-ttu-id="d4ab3-147">Una vez que haya iniciado sesión, puede llamar a comandos para trabajar con recursos de administración de Batch, incluidas cuentas de Batch, claves, paquetes de aplicación y cuotas.</span><span class="sxs-lookup"><span data-stu-id="d4ab3-147">Once you have logged in, you can call commands to work with Batch Management resources, including Batch accounts, keys, application packages, and quotas.</span></span>  

### <a name="log-in-to-your-batch-account"></a><span data-ttu-id="d4ab3-148">Inicio de sesión en la cuenta de Batch</span><span class="sxs-lookup"><span data-stu-id="d4ab3-148">Log in to your Batch account</span></span>

<span data-ttu-id="d4ab3-149">Para usar la CLI de Azure para administrar recursos de Batch, como grupos, trabajos y tareas, debe iniciar sesión en su cuenta de Batch y autenticarse.</span><span class="sxs-lookup"><span data-stu-id="d4ab3-149">To use the Azure CLI to manage Batch resources, such as pools, jobs, and tasks, you need to log into your Batch account and authenticate.</span></span> <span data-ttu-id="d4ab3-150">Para iniciar sesión en el servicio Batch, use el comando [az batch account login](https://docs.microsoft.com/cli/azure/batch/account#login).</span><span class="sxs-lookup"><span data-stu-id="d4ab3-150">To log in to the Batch service, use the [az batch account login](https://docs.microsoft.com/cli/azure/batch/account#login) command.</span></span> 

<span data-ttu-id="d4ab3-151">Tiene dos opciones para autenticarse en su cuenta de Batch:</span><span class="sxs-lookup"><span data-stu-id="d4ab3-151">You have two options for authenticating against your Batch account:</span></span>

- <span data-ttu-id="d4ab3-152">**Mediante la autenticación de Azure Active Directory (Azure AD).**</span><span class="sxs-lookup"><span data-stu-id="d4ab3-152">**By using Azure Active Directory (Azure AD) authentication.**</span></span> 

    <span data-ttu-id="d4ab3-153">La autenticación con Azure AD es el valor predeterminado cuando se usa la CLI de Azure con Batch y se recomienda para la mayoría de los escenarios.</span><span class="sxs-lookup"><span data-stu-id="d4ab3-153">Authenticating with Azure AD is the default when you use the Azure CLI with Batch, and recommended for most scenarios.</span></span> 
    
    <span data-ttu-id="d4ab3-154">Cuando inicia sesión en Azure de forma interactiva, como se describe en la sección anterior, sus credenciales se almacenan en caché, por lo que la CLI de Azure puede iniciar sesión en su cuenta de Batch con esas mismas credenciales.</span><span class="sxs-lookup"><span data-stu-id="d4ab3-154">When you log in to Azure interactively, as described in the previous section, your credentials are cached, so the Azure CLI can log you in to your Batch account using those same credentials.</span></span> <span data-ttu-id="d4ab3-155">Si inicia sesión Azure con una entidad de servicio, esas credenciales también se usan para iniciar sesión en su cuenta de Batch.</span><span class="sxs-lookup"><span data-stu-id="d4ab3-155">If you log in to Azure using a service principal, those credentials are also used to log in to your Batch account.</span></span>

    <span data-ttu-id="d4ab3-156">Una ventaja de Azure AD es que ofrece control de acceso basado en rol (RBAC).</span><span class="sxs-lookup"><span data-stu-id="d4ab3-156">An advantage of Azure AD is that it offers role-based access control (RBAC).</span></span> <span data-ttu-id="d4ab3-157">Con RBAC, el acceso de un usuario depende de su rol asignado, y no de si posee o no las claves de cuenta.</span><span class="sxs-lookup"><span data-stu-id="d4ab3-157">With RBAC, a user's access depends on their assigned role, rather than whether or not they possess the account keys.</span></span> <span data-ttu-id="d4ab3-158">En lugar de administrar claves de cuenta, puede administrar roles RBAC y dejar que Azure AD se encargue del acceso y la autenticación.</span><span class="sxs-lookup"><span data-stu-id="d4ab3-158">Instead of managing account keys, you can manage RBAC roles, and let Azure AD handle access and authentication.</span></span>  

    <span data-ttu-id="d4ab3-159">Es necesario autenticarse con Azure AD si ha creado su cuenta de Azure Batch con el modo de asignación de grupo establecido en "Suscripción del usuario".</span><span class="sxs-lookup"><span data-stu-id="d4ab3-159">Authenticating with Azure AD is required if you created your Azure Batch account with its pool allocation mode set to 'User Subscription'.</span></span> 

    <span data-ttu-id="d4ab3-160">Para iniciar sesión en su cuenta de Batch con Azure AD, llame al comando [az batch account login](https://docs.microsoft.com/cli/azure/batch/account#login):</span><span class="sxs-lookup"><span data-stu-id="d4ab3-160">To log in to your Batch account using Azure AD, call the [az batch account login](https://docs.microsoft.com/cli/azure/batch/account#login) command:</span></span> 

    ```azurecli
    az batch account login -g myresource group -n mybatchaccount
    ```

- <span data-ttu-id="d4ab3-161">**Mediante la autenticación de clave compartida.**</span><span class="sxs-lookup"><span data-stu-id="d4ab3-161">**By using Shared Key authentication.**</span></span>

    <span data-ttu-id="d4ab3-162">La [autenticación de clave compartida](https://docs.microsoft.com/rest/api/batchservice/authenticate-requests-to-the-azure-batch-service#authentication-via-shared-key) usa las claves de acceso de su cuenta para autenticar comandos de la CLI de Azure para el servicio Batch.</span><span class="sxs-lookup"><span data-stu-id="d4ab3-162">[Shared Key authentication](https://docs.microsoft.com/rest/api/batchservice/authenticate-requests-to-the-azure-batch-service#authentication-via-shared-key) uses your account access keys to authenticate Azure CLI commands for the Batch service.</span></span>

    <span data-ttu-id="d4ab3-163">Si va a crear scripts de la CLI de Azure para automatizar la llamada a comandos de Batch, puede usar la autenticación de clave compartida o una entidad de servicio de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="d4ab3-163">If you are creating Azure CLI scripts to automate calling Batch commands, you can use either Shared Key authentication, or an Azure AD service principal.</span></span> <span data-ttu-id="d4ab3-164">En algunos escenarios, puede resultar más sencillo usar la autenticación de clave compartida que crear una entidad de servicio.</span><span class="sxs-lookup"><span data-stu-id="d4ab3-164">In some scenarios, using Shared Key authentication may be simpler than creating a service principal.</span></span>  

    <span data-ttu-id="d4ab3-165">Para iniciar sesión con autenticación de clave compartida, incluya la opción `--shared-key-auth` en la línea de comandos:</span><span class="sxs-lookup"><span data-stu-id="d4ab3-165">To log in using Shared Key authentication, include the `--shared-key-auth` option on the command line:</span></span>

    ```azurecli
    az batch account login -g myresourcegroup -n mybatchaccount --shared-key-auth
    ```

<span data-ttu-id="d4ab3-166">Los ejemplos en la sección [Scripts de shell de ejemplo](#sample-shell-scripts) muestran cómo iniciar sesión en su cuenta de Batch con la CLI de Azure mediante Azure AD y la clave compartida.</span><span class="sxs-lookup"><span data-stu-id="d4ab3-166">The examples listed in the [Sample shell scripts](#sample-shell-scripts) section show how to log into your Batch account with the Azure CLI using both Azure AD and Shared Key.</span></span>

## <a name="use-azure-batch-cli-templates-and-file-transfer-preview"></a><span data-ttu-id="d4ab3-167">Uso de plantillas y transferencia de archivos de la CLI de Azure Batch (versión preliminar)</span><span class="sxs-lookup"><span data-stu-id="d4ab3-167">Use Azure Batch CLI Templates and File Transfer (Preview)</span></span>

<span data-ttu-id="d4ab3-168">Puede utilizar la CLI de Azure para ejecutar trabajos completos de Batch sin escribir código.</span><span class="sxs-lookup"><span data-stu-id="d4ab3-168">You can use the Azure CLI to run Batch jobs end-to-end without writing code.</span></span> <span data-ttu-id="d4ab3-169">Los archivos de plantilla de Batch admiten la creación de grupos, trabajos y tareas con la CLI de Azure.</span><span class="sxs-lookup"><span data-stu-id="d4ab3-169">Batch template files support creating pools, jobs, and tasks with the Azure CLI.</span></span> <span data-ttu-id="d4ab3-170">También puede utilizar la CLI de Azure para cargar archivos de entrada de trabajos en la cuenta de Azure Storage asociada con la cuenta de Batch y descargar los archivos de salida de trabajos.</span><span class="sxs-lookup"><span data-stu-id="d4ab3-170">You can also use the Azure CLI to upload job input files to the Azure Storage account associated with the Batch account, and download job output files from it.</span></span> <span data-ttu-id="d4ab3-171">Para más información, consulte [Uso de plantillas y transferencia de archivos de la CLI de Azure Batch (versión preliminar)](batch-cli-templates.md).</span><span class="sxs-lookup"><span data-stu-id="d4ab3-171">For more information, see [Use Azure Batch CLI Templates and File Transfer (Preview)](batch-cli-templates.md).</span></span>

## <a name="sample-shell-scripts"></a><span data-ttu-id="d4ab3-172">Scripts de shell de ejemplo</span><span class="sxs-lookup"><span data-stu-id="d4ab3-172">Sample shell scripts</span></span>

<span data-ttu-id="d4ab3-173">Los scripts de ejemplo en la tabla siguiente muestran cómo usar comandos de la CLI de Azure con el servicio Batch y el servicio de administración de Batch para realizar tareas habituales.</span><span class="sxs-lookup"><span data-stu-id="d4ab3-173">The sample scripts listed in the following table show how to use Azure CLI commands with the Batch service and Batch Management service to accomplish common tasks.</span></span> <span data-ttu-id="d4ab3-174">Estos scripts de ejemplo tratan muchos de los comandos disponibles en la CLI de Azure para Batch.</span><span class="sxs-lookup"><span data-stu-id="d4ab3-174">These sample scripts cover many of the commands available in the Azure CLI for Batch.</span></span> 

| <span data-ttu-id="d4ab3-175">Script</span><span class="sxs-lookup"><span data-stu-id="d4ab3-175">Script</span></span> | <span data-ttu-id="d4ab3-176">Notas</span><span class="sxs-lookup"><span data-stu-id="d4ab3-176">Notes</span></span> |
|---|---|
| [<span data-ttu-id="d4ab3-177">Crear una cuenta de Batch</span><span class="sxs-lookup"><span data-stu-id="d4ab3-177">Create a Batch account</span></span>](./scripts/batch-cli-sample-create-account.md) | <span data-ttu-id="d4ab3-178">Crea una cuenta de Batch y la asocia con una cuenta de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="d4ab3-178">Creates a Batch account and associates it with a storage account.</span></span> |
| [<span data-ttu-id="d4ab3-179">Agregar una aplicación</span><span class="sxs-lookup"><span data-stu-id="d4ab3-179">Add an application</span></span>](./scripts/batch-cli-sample-add-application.md) | <span data-ttu-id="d4ab3-180">Agrega una aplicación y carga los paquetes de binarios.</span><span class="sxs-lookup"><span data-stu-id="d4ab3-180">Adds an application and uploads packaged binaries.</span></span>|
| [<span data-ttu-id="d4ab3-181">Administrar grupos de Batch</span><span class="sxs-lookup"><span data-stu-id="d4ab3-181">Manage Batch pools</span></span>](./scripts/batch-cli-sample-manage-pool.md) | <span data-ttu-id="d4ab3-182">Muestra cómo crear grupos, cambiarlos de tamaño y administrarlos.</span><span class="sxs-lookup"><span data-stu-id="d4ab3-182">Demonstrates creating, resizing, and managing pools.</span></span> |
| [<span data-ttu-id="d4ab3-183">Ejecutar un trabajo y tareas con Batch</span><span class="sxs-lookup"><span data-stu-id="d4ab3-183">Run a job and tasks with Batch</span></span>](./scripts/batch-cli-sample-run-job.md) | <span data-ttu-id="d4ab3-184">Muestra cómo ejecutar un trabajo y agregar tareas.</span><span class="sxs-lookup"><span data-stu-id="d4ab3-184">Demonstrates running a job and adding tasks.</span></span> |

## <a name="json-files-for-resource-creation"></a><span data-ttu-id="d4ab3-185">Archivos JSON para la creación de recursos</span><span class="sxs-lookup"><span data-stu-id="d4ab3-185">JSON files for resource creation</span></span>

<span data-ttu-id="d4ab3-186">Al crear recursos de Batch, como grupos y trabajos, puede especificar un archivo JSON que contenga la configuración del recurso nuevo, en lugar de pasar sus parámetros como opciones de la línea de comandos.</span><span class="sxs-lookup"><span data-stu-id="d4ab3-186">When you create Batch resources like pools and jobs, you can specify a JSON file containing the new resource's configuration instead of passing its parameters as command-line options.</span></span> <span data-ttu-id="d4ab3-187">Por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="d4ab3-187">For example:</span></span>

```azurecli
az batch pool create my_batch_pool.json
```

<span data-ttu-id="d4ab3-188">Aunque puede crear la mayoría de los recursos de Batch solo con las opciones de la línea de comandos, algunas características requieren que especifique un archivo con formato JSON que contenga los detalles de los recursos.</span><span class="sxs-lookup"><span data-stu-id="d4ab3-188">While you can create most Batch resources using only command-line options, some features require that you specify a JSON-formatted file containing the resource details.</span></span> <span data-ttu-id="d4ab3-189">Por ejemplo, si desea especificar archivos de recursos para una tarea de inicio, debe utilizar un archivo JSON.</span><span class="sxs-lookup"><span data-stu-id="d4ab3-189">For example, you must use a JSON file if you want to specify resource files for a start task.</span></span>

<span data-ttu-id="d4ab3-190">Para ver la sintaxis JSON necesaria para crear un recurso, consulte la documentación de [referencia de API de REST de Batch][rest_api].</span><span class="sxs-lookup"><span data-stu-id="d4ab3-190">To see the JSON syntax required to create a resource, refer to the [Batch REST API reference][rest_api] documentation.</span></span> <span data-ttu-id="d4ab3-191">Todos los temas sobre la incorporación de *tipos de recurso* en la referencia de API de REST contienen scripts JSON de ejemplo para crear el recurso correspondiente.</span><span class="sxs-lookup"><span data-stu-id="d4ab3-191">Each "Add *resource type*" topic in the REST API reference contains sample JSON scripts for creating that resource.</span></span> <span data-ttu-id="d4ab3-192">Puede usar esos scripts JSON de ejemplo como plantillas para los archivos JSON que se usan con la CLI de Azure.</span><span class="sxs-lookup"><span data-stu-id="d4ab3-192">You can use those sample JSON scripts as templates for JSON files to use with the Azure CLI.</span></span> <span data-ttu-id="d4ab3-193">Por ejemplo, para ver la sintaxis JSON para crear grupos, consulte [Add a pool to an account][rest_add_pool] (Incorporación de un grupo a una cuenta).</span><span class="sxs-lookup"><span data-stu-id="d4ab3-193">For example, to see the JSON syntax for pool creation, refer to [Add a pool to an account][rest_add_pool].</span></span>

<span data-ttu-id="d4ab3-194">Para un script de ejemplo que especifica un archivo JSON, consulte [Ejecutar un trabajo y tareas con Batch](./scripts/batch-cli-sample-run-job.md).</span><span class="sxs-lookup"><span data-stu-id="d4ab3-194">For a sample script that specifies a JSON file, see [Run a job and tasks with Batch](./scripts/batch-cli-sample-run-job.md).</span></span>

> [!NOTE]
> <span data-ttu-id="d4ab3-195">Si especifica un archivo JSON al crear un recurso, se pasan por alto los restantes parámetros que especifique en la línea de comandos de dicho recurso.</span><span class="sxs-lookup"><span data-stu-id="d4ab3-195">If you specify a JSON file when you create a resource, any other parameters that you specify on the command line for that resource are ignored.</span></span>
> 
> 

## <a name="efficient-queries-for-batch-resources"></a><span data-ttu-id="d4ab3-196">Consultas eficaces para recursos de Batch</span><span class="sxs-lookup"><span data-stu-id="d4ab3-196">Efficient queries for Batch resources</span></span>

<span data-ttu-id="d4ab3-197">Cada tipo de recurso de proceso de Batch admite un comando `list` que consulta la cuenta de Batch y enumera los recursos de ese tipo.</span><span class="sxs-lookup"><span data-stu-id="d4ab3-197">Each Batch resource type supports a `list` command that queries your Batch account and lists resources of that type.</span></span> <span data-ttu-id="d4ab3-198">Por ejemplo, puede enumerar los grupos de su cuenta y las tareas de un trabajo:</span><span class="sxs-lookup"><span data-stu-id="d4ab3-198">For example, you can list the pools in your account and the tasks in a job:</span></span>

```azurecli
az batch pool list
az batch task list --job-id job001
```

<span data-ttu-id="d4ab3-199">Cuando consulta el servicio Batch con una operación `list`, puede especificar una cláusula OData para limitar la cantidad de datos devueltos.</span><span class="sxs-lookup"><span data-stu-id="d4ab3-199">When you query the Batch service with a `list` operation, you can specify an OData clause to limit the amount of data returned.</span></span> <span data-ttu-id="d4ab3-200">Dado que todo el filtrado se produce en el lado servidor, solo se devuelven los datos que solicite.</span><span class="sxs-lookup"><span data-stu-id="d4ab3-200">Because all filtering occurs server-side, only the data you request crosses the wire.</span></span> <span data-ttu-id="d4ab3-201">Use estas cláusulas para ahorrar ancho de banda (y, por consiguiente, tiempo) al realizar operaciones de lista.</span><span class="sxs-lookup"><span data-stu-id="d4ab3-201">Use these clauses to save bandwidth (and therefore time) when you perform list operations.</span></span>

<span data-ttu-id="d4ab3-202">En la tabla siguiente se describen las cláusulas OData admitidas por el servicio Batch:</span><span class="sxs-lookup"><span data-stu-id="d4ab3-202">The following table describes the OData clauses supported by the Batch service:</span></span>

| <span data-ttu-id="d4ab3-203">Cláusula</span><span class="sxs-lookup"><span data-stu-id="d4ab3-203">Clause</span></span> | <span data-ttu-id="d4ab3-204">Descripción</span><span class="sxs-lookup"><span data-stu-id="d4ab3-204">Description</span></span> |
|---|---|
| `--select-clause [select-clause]` | <span data-ttu-id="d4ab3-205">Devuelve un subconjunto de propiedades para cada entidad.</span><span class="sxs-lookup"><span data-stu-id="d4ab3-205">Returns a subset of properties for each entity.</span></span> |
| `--filter-clause [filter-clause]` | <span data-ttu-id="d4ab3-206">Devuelve solo las entidades que coincidan con la expresión OData especificada.</span><span class="sxs-lookup"><span data-stu-id="d4ab3-206">Returns only entities that match the specified OData expression.</span></span> |
| `--expand-clause [expand-clause]` | <span data-ttu-id="d4ab3-207">Obtiene la información de la entidad en una única llamada REST subyacente.</span><span class="sxs-lookup"><span data-stu-id="d4ab3-207">Obtains the entity information in a single underlying REST call.</span></span> <span data-ttu-id="d4ab3-208">Actualmente, la cláusula expand solo admite la propiedad `stats`.</span><span class="sxs-lookup"><span data-stu-id="d4ab3-208">The expand clause currently supports only the `stats` property.</span></span> |

<span data-ttu-id="d4ab3-209">Para un script de ejemplo que muestra cómo usar una cláusula OData, consulte [Ejecutar un trabajo y tareas con Batch](./scripts/batch-cli-sample-run-job.md).</span><span class="sxs-lookup"><span data-stu-id="d4ab3-209">For a sample script that shows how to use an OData clause, see [Run a job and tasks with Batch](./scripts/batch-cli-sample-run-job.md).</span></span>

<span data-ttu-id="d4ab3-210">Para más información sobre cómo realizar consultas de lista eficaces con cláusulas OData, consulte [Consulta del servicio Azure Batch con eficacia](batch-efficient-list-queries.md).</span><span class="sxs-lookup"><span data-stu-id="d4ab3-210">For more information on performing efficient list queries with OData clauses, see [Query the Azure Batch service efficiently](batch-efficient-list-queries.md).</span></span>

## <a name="troubleshooting-tips"></a><span data-ttu-id="d4ab3-211">Sugerencias de solución de problemas</span><span class="sxs-lookup"><span data-stu-id="d4ab3-211">Troubleshooting tips</span></span>

<span data-ttu-id="d4ab3-212">Las siguientes sugerencias pueden ayudarle cuando esté solucionando problemas de la CLI de Azure:</span><span class="sxs-lookup"><span data-stu-id="d4ab3-212">The following tips may help when you are troubleshooting Azure CLI issues:</span></span>

* <span data-ttu-id="d4ab3-213">Use `-h` para obtener **texto de ayuda** de cualquier comando de CLI.</span><span class="sxs-lookup"><span data-stu-id="d4ab3-213">Use `-h` to get **help text** for any CLI command</span></span>
* <span data-ttu-id="d4ab3-214">Use `-v` y `-vv` para mostrar la salida **detallada** de comandos.</span><span class="sxs-lookup"><span data-stu-id="d4ab3-214">Use `-v` and `-vv` to display **verbose** command output.</span></span> <span data-ttu-id="d4ab3-215">Cuando se incluye la marca `-vv`, la CLI de Azure muestra las solicitudes y respuestas REST en sí.</span><span class="sxs-lookup"><span data-stu-id="d4ab3-215">When the `-vv` flag is included, the Azure CLI displays the actual REST requests and responses.</span></span> <span data-ttu-id="d4ab3-216">Estos modificadores son útiles para mostrar la salida completa del error.</span><span class="sxs-lookup"><span data-stu-id="d4ab3-216">These switches are handy for displaying full error output.</span></span>
* <span data-ttu-id="d4ab3-217">Puede ver la **salida del comando como JSON** con la opción `--json`.</span><span class="sxs-lookup"><span data-stu-id="d4ab3-217">You can view **command output as JSON** with the `--json` option.</span></span> <span data-ttu-id="d4ab3-218">Por ejemplo, `az batch pool show pool001 --json` muestra las propiedades de pool001 en formato JSON.</span><span class="sxs-lookup"><span data-stu-id="d4ab3-218">For example, `az batch pool show pool001 --json` displays pool001's properties in JSON format.</span></span> <span data-ttu-id="d4ab3-219">Puede copiar y modificar esta salida para usarla en `--json-file` (consulte [Archivos JSON](#json-files) en este mismo artículo).</span><span class="sxs-lookup"><span data-stu-id="d4ab3-219">You can then copy and modify this output to use in a `--json-file` (see [JSON files](#json-files) earlier in this article).</span></span>
<!---Loc Comment: Please, check link [JSON files] since it's not redirecting to any location.--->
* <span data-ttu-id="d4ab3-220">El [foro de Batch][batch_forum] está supervisado por los miembros del equipo de Batch.</span><span class="sxs-lookup"><span data-stu-id="d4ab3-220">The [Batch forum][batch_forum] is monitored by Batch team members.</span></span> <span data-ttu-id="d4ab3-221">Puede publicar en él sus preguntas si experimenta problemas o desea obtener ayuda acerca de una operación concreta.</span><span class="sxs-lookup"><span data-stu-id="d4ab3-221">You can post your questions there if you run into issues or would like help with a specific operation.</span></span>

## <a name="next-steps"></a><span data-ttu-id="d4ab3-222">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="d4ab3-222">Next steps</span></span>

* <span data-ttu-id="d4ab3-223">Para más información sobre la CLI de Azure, consulte la [documentación de la CLI de Azure](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="d4ab3-223">For more information about the Azure CLI, see the [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>
* <span data-ttu-id="d4ab3-224">Para más información sobre los recursos de Batch, consulte [Introducción a Azure Batch para desarrolladores](batch-api-basics.md).</span><span class="sxs-lookup"><span data-stu-id="d4ab3-224">For more information about Batch resources, see [Overview of Azure Batch for developers](batch-api-basics.md).</span></span>
* <span data-ttu-id="d4ab3-225">Para más información sobre el uso de plantillas de Batch para crear grupos, trabajos y tareas sin escribir código, consulte [Uso de plantillas y transferencia de archivos de la CLI de Azure Batch (versión preliminar)](batch-cli-templates.md).</span><span class="sxs-lookup"><span data-stu-id="d4ab3-225">For more information about using Batch templates to create pools, jobs, and tasks without writing code, see [Use Azure Batch CLI Templates and File Transfer (Preview)](batch-cli-templates.md).</span></span>

[batch_forum]: https://social.msdn.microsoft.com/forums/azure/home?forum=azurebatch
[github_readme]: https://github.com/Azure/azure-xplat-cli/blob/dev/README.md
[rest_api]: https://msdn.microsoft.com/library/azure/dn820158.aspx
[rest_add_pool]: https://msdn.microsoft.com/library/azure/dn820174.aspx
