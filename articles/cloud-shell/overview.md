---
title: "Introducción al Shell de nube (versión preliminar) aaaAzure | Documentos de Microsoft"
description: "Información general de hello Shell en la nube de Azure."
services: 
documentationcenter: 
author: jluk
manager: timlt
tags: azure-resource-manager
ms.assetid: 
ms.service: azure
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 07/10/2017
ms.author: juluk
ms.openlocfilehash: 45c6c85b167a90947a333f44a9186e2c01b4fa7b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="overview-of-azure-cloud-shell-preview"></a><span data-ttu-id="742e9-103">Introducción a Azure Cloud Shell (versión preliminar)</span><span class="sxs-lookup"><span data-stu-id="742e9-103">Overview of Azure Cloud Shell (Preview)</span></span>
<span data-ttu-id="742e9-104">Azure Cloud Shell es un shell interactivo, accesible desde el explorador, para administrar recursos de Azure.</span><span class="sxs-lookup"><span data-stu-id="742e9-104">Azure Cloud Shell is an interactive, browser-accessible shell for managing Azure resources.</span></span>

![](media/overview-pic.png)

## <a name="features"></a><span data-ttu-id="742e9-105">Características</span><span class="sxs-lookup"><span data-stu-id="742e9-105">Features</span></span>
### <a name="browser-based-shell-experience"></a><span data-ttu-id="742e9-106">Experiencia de shell basada en explorador</span><span class="sxs-lookup"><span data-stu-id="742e9-106">Browser-based shell experience</span></span>
<span data-ttu-id="742e9-107">La nube Shell permite acceso tooa basadas en el Explorador de línea de comandos experiencia compilada con tareas de administración de Azure en mente.</span><span class="sxs-lookup"><span data-stu-id="742e9-107">Cloud Shell enables access tooa browser-based command-line experience built with Azure management tasks in mind.</span></span> <span data-ttu-id="742e9-108">Aprovechar toowork de Shell en la nube sin restricción de un equipo local de forma que se puede proporcionar solo en la nube Hola.</span><span class="sxs-lookup"><span data-stu-id="742e9-108">Leverage Cloud Shell toowork untethered from a local machine in a way only hello cloud can provide.</span></span>

### <a name="pre-configured-azure-workstation"></a><span data-ttu-id="742e9-109">Estación de trabajo de Azure configurada previamente</span><span class="sxs-lookup"><span data-stu-id="742e9-109">Pre-configured Azure workstation</span></span>
<span data-ttu-id="742e9-110">Cloud Shell viene preinstalado con conocidas populares herramientas de línea de comandos y compatibilidad de idiomas para que pueda trabajar con mayor rapidez.</span><span class="sxs-lookup"><span data-stu-id="742e9-110">Cloud Shell comes pre-installed with popular command-line tools and language support so you can work faster.</span></span>

[<span data-ttu-id="742e9-111">Vista Hola herramientas completa lista para el Shell de nube de Azure aquí.</span><span class="sxs-lookup"><span data-stu-id="742e9-111">View hello full tooling list for Azure Cloud Shell here.</span></span>](features.md#tools)

### <a name="automatic-authentication"></a><span data-ttu-id="742e9-112">Autenticación automática</span><span class="sxs-lookup"><span data-stu-id="742e9-112">Automatic authentication</span></span>
<span data-ttu-id="742e9-113">Shell de la nube segura autentica automáticamente en cada sesión en recursos de tooyour de acceso instantáneo a través de hello 2.0 de CLI de Azure.</span><span class="sxs-lookup"><span data-stu-id="742e9-113">Cloud Shell securely authenticates automatically on each session for instant access tooyour resources through hello Azure CLI 2.0.</span></span>

### <a name="connect-your-azure-file-storage"></a><span data-ttu-id="742e9-114">Conexión a Azure File Storage</span><span class="sxs-lookup"><span data-stu-id="742e9-114">Connect your Azure File storage</span></span>
<span data-ttu-id="742e9-115">Máquinas de Shell en la nube son temporales y ello requiere un toobe del recurso compartido de archivos de Azure montado como `clouddrive` toopersist el directorio $Home.</span><span class="sxs-lookup"><span data-stu-id="742e9-115">Cloud Shell machines are temporary and as a result require an Azure file share toobe mounted as `clouddrive` toopersist your $Home directory.</span></span>
<span data-ttu-id="742e9-116">Primer inicio Shell de nube le pedirá toocreate que compartan un grupo de recursos, la cuenta de almacenamiento y el archivo en su nombre.</span><span class="sxs-lookup"><span data-stu-id="742e9-116">On first launch Cloud Shell prompts toocreate a resource group, storage account, and file share on your behalf.</span></span> <span data-ttu-id="742e9-117">Esto es un paso único y se adjuntará automáticamente en todas las sesiones.</span><span class="sxs-lookup"><span data-stu-id="742e9-117">This is a one-time step and will be automatically attached for all sessions.</span></span> 

#### <a name="create-new-storage"></a><span data-ttu-id="742e9-118">creación de nuevo almacenamiento</span><span class="sxs-lookup"><span data-stu-id="742e9-118">Create new storage</span></span>
![](media/basic-storage.png)

<span data-ttu-id="742e9-119">Se crea una cuenta de almacenamiento con redundancia local (LRS) en su nombre con un recurso compartido de archivos de Azure que, de forma predeterminada, contiene una imagen de disco de 5 GB.</span><span class="sxs-lookup"><span data-stu-id="742e9-119">A locally-redundant storage (LRS) account can be created on your behalf with an Azure file share containing a default 5-GB disk image.</span></span> <span data-ttu-id="742e9-120">recurso compartido de archivos de Hello monta como `clouddrive` archivo compartir interacción con la imagen de disco de Hola que se usa toosync y conservar el directorio $Home.</span><span class="sxs-lookup"><span data-stu-id="742e9-120">hello file share mounts as `clouddrive` for file share interaction with hello disk image being used toosync and persist your $Home directory.</span></span> <span data-ttu-id="742e9-121">Se aplican costos por almacenamiento normal.</span><span class="sxs-lookup"><span data-stu-id="742e9-121">Regular storage costs apply.</span></span>

<span data-ttu-id="742e9-122">Se crearán tres recursos en su nombre:</span><span class="sxs-lookup"><span data-stu-id="742e9-122">Three resources will be created on your behalf:</span></span>
1. <span data-ttu-id="742e9-123">Grupo de recursos llamado: `cloud-shell-storage-<region>`</span><span class="sxs-lookup"><span data-stu-id="742e9-123">Resource Group named: `cloud-shell-storage-<region>`</span></span>
2. <span data-ttu-id="742e9-124">Cuenta de almacenamiento llamada: `cs<uniqueGuid>`</span><span class="sxs-lookup"><span data-stu-id="742e9-124">Storage Account named: `cs<uniqueGuid>`</span></span>
3. <span data-ttu-id="742e9-125">Recurso compartido de archivos llamado: `cs-<user>-<domain>-com-uniqueGuid`</span><span class="sxs-lookup"><span data-stu-id="742e9-125">File Share named: `cs-<user>-<domain>-com-uniqueGuid`</span></span>

> [!Note]
> <span data-ttu-id="742e9-126">Todos los archivos en el directorio $Home, como las claves de SSH, se conservan en la imagen de disco de usuario almacenada en el recurso compartido de archivos montado.</span><span class="sxs-lookup"><span data-stu-id="742e9-126">All files in your $Home directory such as SSH keys are persisted in your user disk image stored in your mounted file share.</span></span> <span data-ttu-id="742e9-127">Ponga en práctica los procedimientos recomendados para guardar archivos en el directorio $Home y en el recurso compartido de archivos montado.</span><span class="sxs-lookup"><span data-stu-id="742e9-127">Apply best practices when saving files in your $Home directory and mounted file share.</span></span>

#### <a name="use-existing-resources"></a><span data-ttu-id="742e9-128">Uso de recursos existentes</span><span class="sxs-lookup"><span data-stu-id="742e9-128">Use existing resources</span></span>
![](media/advanced-storage.png)

<span data-ttu-id="742e9-129">Una opción avanzada también se proporciona lo que permite tooassociate existente recursos tooCloud Shell.</span><span class="sxs-lookup"><span data-stu-id="742e9-129">An advanced option is also provided allowing you tooassociate existing resources tooCloud Shell.</span></span> <span data-ttu-id="742e9-130">Cuando aparezca el símbolo del sistema de hello almacenamiento el programa de instalación, haga clic en Opciones adicionales de tooselect "Show advanced settings".</span><span class="sxs-lookup"><span data-stu-id="742e9-130">When presented with hello storage setup prompt, click "Show advanced settings" tooselect additional options.</span></span> <span data-ttu-id="742e9-131">Las listas desplegables se filtran para las cuentas de almacenamiento redundante local o globalmente y para la región asignada de Cloud Shell.</span><span class="sxs-lookup"><span data-stu-id="742e9-131">Dropdowns are filtered for your assigned Cloud Shell region and locally/globally-redundant storage accounts.</span></span>

<span data-ttu-id="742e9-132">[Obtenga más información sobre el almacenamiento de Cloud Shell, la actualización de recursos compartidos de archivos y la carga y descarga de archivos]. (persisting-shell-storage.md)</span><span class="sxs-lookup"><span data-stu-id="742e9-132">[Learn about Cloud Shell storage, updating file shares, and uploading/downloading files.] (persisting-shell-storage.md)</span></span>

## <a name="concepts"></a><span data-ttu-id="742e9-133">Conceptos</span><span class="sxs-lookup"><span data-stu-id="742e9-133">Concepts</span></span>
* <span data-ttu-id="742e9-134">Cloud Shell se ejecuta en un equipo temporal proporcionado en cada sesión y por usuario</span><span class="sxs-lookup"><span data-stu-id="742e9-134">Cloud Shell runs on a temporary machine provided on a per-session, per-user basis</span></span>
* <span data-ttu-id="742e9-135">Cloud Shell agota el tiempo de espera tras 20 minutos sin actividad interactiva.</span><span class="sxs-lookup"><span data-stu-id="742e9-135">Cloud Shell times out after 20 minutes without interactive activity</span></span>
* <span data-ttu-id="742e9-136">Solo se puede acceder a Cloud Shell mediante un recurso compartido de archivo adjuntado.</span><span class="sxs-lookup"><span data-stu-id="742e9-136">Cloud Shell can only be accessed with a file share attached</span></span>
* <span data-ttu-id="742e9-137">Se asigna a Cloud Shell una máquina por cuenta de usuario.</span><span class="sxs-lookup"><span data-stu-id="742e9-137">Cloud Shell is assigned one machine per user account</span></span>
* <span data-ttu-id="742e9-138">Los permisos se establecen como un usuario de Linux regular</span><span class="sxs-lookup"><span data-stu-id="742e9-138">Permissions are set as a regular Linux user</span></span>

[<span data-ttu-id="742e9-139">Más información sobre todas las características de Cloud Shell.</span><span class="sxs-lookup"><span data-stu-id="742e9-139">Learn more about all Cloud Shell features.</span></span>](features.md)

## <a name="examples"></a><span data-ttu-id="742e9-140">Ejemplos</span><span class="sxs-lookup"><span data-stu-id="742e9-140">Examples</span></span>
* <span data-ttu-id="742e9-141">Crear o editar scripts tooautomate administración de Azure</span><span class="sxs-lookup"><span data-stu-id="742e9-141">Create or edit scripts tooautomate Azure management</span></span>
* <span data-ttu-id="742e9-142">Administración simultánea los recursos a través de Azure Portal y la CLI de Azure 2.0</span><span class="sxs-lookup"><span data-stu-id="742e9-142">Simultaneously manage resources via Azure portal and Azure CLI 2.0</span></span>
* <span data-ttu-id="742e9-143">Prueba de la CLI de Azure 2.0</span><span class="sxs-lookup"><span data-stu-id="742e9-143">Test-drive Azure CLI 2.0</span></span>

[<span data-ttu-id="742e9-144">Pruebe todos estos ejemplos en Inicio rápido de nube Shell Hola.</span><span class="sxs-lookup"><span data-stu-id="742e9-144">Try out all these examples at hello Cloud Shell quickstart.</span></span>](quickstart.md)

## <a name="pricing"></a><span data-ttu-id="742e9-145">Precios</span><span class="sxs-lookup"><span data-stu-id="742e9-145">Pricing</span></span>
<span data-ttu-id="742e9-146">máquina de Hello Shell en la nube de hospedaje es gratuito, con un requisito previo de un archivo de Azure montado compartir toopersist el directorio $Home.</span><span class="sxs-lookup"><span data-stu-id="742e9-146">hello machine hosting Cloud Shell is free, with a pre-requisite of a mounted Azure file share toopersist your $Home directory.</span></span> <span data-ttu-id="742e9-147">Se aplican costos por almacenamiento normal.</span><span class="sxs-lookup"><span data-stu-id="742e9-147">Regular storage costs apply.</span></span>

## <a name="supported-browsers"></a><span data-ttu-id="742e9-148">Exploradores compatibles</span><span class="sxs-lookup"><span data-stu-id="742e9-148">Supported browsers</span></span>
<span data-ttu-id="742e9-149">Se recomienda Cloud Shell para Chrome, Edge y Safari.</span><span class="sxs-lookup"><span data-stu-id="742e9-149">Cloud Shell is recommended for Chrome, Edge, and Safari.</span></span> <span data-ttu-id="742e9-150">Aunque se admite el Shell de nube para Chrome, Firefox, Safari, Internet Explorer y borde, Shell en la nube es la configuración del explorador de toospecific de asunto.</span><span class="sxs-lookup"><span data-stu-id="742e9-150">While Cloud Shell is supported for Chrome, Firefox, Safari, IE, and Edge, Cloud Shell is subject toospecific browser settings.</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="742e9-151">Solución de problemas</span><span class="sxs-lookup"><span data-stu-id="742e9-151">Troubleshooting</span></span>
1. <span data-ttu-id="742e9-152">Cuando se utiliza una suscripción de Azure Active Directory, no se puede crear almacenamiento due tooError: 400 DisallowedOperation.</span><span class="sxs-lookup"><span data-stu-id="742e9-152">When using an Azure Active Directory subscription, I cannot create storage due tooError: 400 DisallowedOperation.</span></span> <span data-ttu-id="742e9-153">tooresolve esto, use una suscripción de Azure capaz de crear los recursos de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="742e9-153">tooresolve this, please use an Azure subscription capable of creating storage resources.</span></span> <span data-ttu-id="742e9-154">Las suscripciones de AD es toocreate imposibilidad de recursos de Azure.</span><span class="sxs-lookup"><span data-stu-id="742e9-154">AD subscriptions are not able toocreate Azure resources.</span></span>

<span data-ttu-id="742e9-155">Para conocer las limitaciones conocidas específicas, consulte las [limitaciones de Cloud Shell](limitations.md).</span><span class="sxs-lookup"><span data-stu-id="742e9-155">For specific known limitations, visit [limitations of Cloud Shell](limitations.md).</span></span>
