---
title: "aaaCreate una aplicación de la función de hello Portal de Azure | Documentos de Microsoft"
description: "Crear una nueva aplicación de función en el servicio de aplicación de Azure desde el portal de Hola."
services: functions
documentationcenter: na
author: ggailey777
manager: erikre
editor: 
tags: 
ms.assetid: 
ms.service: functions
ms.devlang: multiple
ms.topic: quickstart
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 04/11/2017
ms.author: glenga
ms.custom: mvc
ms.openlocfilehash: c531fc71c798edf22e25a5f4b79c15413809dc86
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-function-app-from-hello-azure-portal"></a><span data-ttu-id="96579-103">Crear una aplicación de la función de hello portal de Azure</span><span class="sxs-lookup"><span data-stu-id="96579-103">Create a function app from hello Azure portal</span></span>

<span data-ttu-id="96579-104">Las aplicaciones de Azure función usa la infraestructura de servicio de aplicaciones de Azure de Hola.</span><span class="sxs-lookup"><span data-stu-id="96579-104">Azure Function Apps uses hello Azure App Service infrastructure.</span></span> <span data-ttu-id="96579-105">Este tema muestra cómo toocreate una aplicación de la función en hello portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="96579-105">This topic shows you how toocreate a function app in hello Azure portal.</span></span> <span data-ttu-id="96579-106">Una aplicación de la función es contenedor de Hola que hospeda la ejecución de Hola de las funciones individuales.</span><span class="sxs-lookup"><span data-stu-id="96579-106">A function app is hello container that hosts hello execution of individual functions.</span></span> <span data-ttu-id="96579-107">Cuando se crea una aplicación de la función en hello plan de hospedaje de servicio de aplicaciones, la aplicación de la función puede usar todas las características de Hola de servicio de aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="96579-107">When you create a function app in hello App Service hosting plan, your function app can use all hello features of App Service.</span></span>

## <a name="create-a-function-app"></a><span data-ttu-id="96579-108">Creación de una aplicación de función</span><span class="sxs-lookup"><span data-stu-id="96579-108">Create a function app</span></span>

[!INCLUDE [functions-create-function-app-portal](../../includes/functions-create-function-app-portal.md)]

<span data-ttu-id="96579-109">Cuando cree una instancia de Function App, brinde un **nombre de aplicación** válido, que solo puede incluir letras, números y guiones.</span><span class="sxs-lookup"><span data-stu-id="96579-109">When you create a function app, supply a valid **App name**, which can contain only letters, numbers, and hyphens.</span></span> <span data-ttu-id="96579-110">El carácter de subrayado (**_**) no se permite.</span><span class="sxs-lookup"><span data-stu-id="96579-110">Underscore (**_**) is not an allowed character.</span></span>

<span data-ttu-id="96579-111">Los nombres de cuentas de almacenamiento deben tener entre 3 y 24 caracteres, y solo pueden contener números y letras minúsculas.</span><span class="sxs-lookup"><span data-stu-id="96579-111">Storage account names must be between 3 and 24 characters in length and may contain numbers and lowercase letters only.</span></span> <span data-ttu-id="96579-112">El nombre de la cuenta de almacenamiento debe ser único dentro de Azure.</span><span class="sxs-lookup"><span data-stu-id="96579-112">Your storage account name must be unique within Azure.</span></span> 

<span data-ttu-id="96579-113">Después de crea la aplicación de la función de hello, puede crear funciones individuales en uno o más idiomas diferentes.</span><span class="sxs-lookup"><span data-stu-id="96579-113">After hello function app is created, you can create individual functions in one or more different languages.</span></span> <span data-ttu-id="96579-114">Crear funciones [mediante el portal de hello](functions-create-first-azure-function.md#create-function), [implementación continua](functions-continuous-deployment.md), o por [cargar con FTP](https://github.com/projectkudu/kudu/wiki/Accessing-files-via-ftp).</span><span class="sxs-lookup"><span data-stu-id="96579-114">Create functions [by using hello portal](functions-create-first-azure-function.md#create-function), [continuous deployment](functions-continuous-deployment.md), or by [uploading with FTP](https://github.com/projectkudu/kudu/wiki/Accessing-files-via-ftp).</span></span>

## <a name="service-plans"></a><span data-ttu-id="96579-115">Planes de servicio</span><span class="sxs-lookup"><span data-stu-id="96579-115">Service plans</span></span>

<span data-ttu-id="96579-116">Azure Functions tiene dos planes de servicio diferentes: plan de consumo y plan de App Service.</span><span class="sxs-lookup"><span data-stu-id="96579-116">Azure Functions has two different service plans: Consumption plan and App Service plan.</span></span> <span data-ttu-id="96579-117">plan de consumo de Hello asigna automáticamente la capacidad de proceso cuando se ejecuta el código, escalas horizontal como carga de toohandle es necesario y, a continuación, escalas de cuando no se está ejecutando el código.</span><span class="sxs-lookup"><span data-stu-id="96579-117">hello Consumption plan automatically allocates compute power when your code is running, scales-out as necessary toohandle load, and then scales-in when code is not running.</span></span> <span data-ttu-id="96579-118">Hola plan de servicio de aplicaciones proporciona la función de instalaciones de Hola de tooall de acceso de aplicación de servicio de aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="96579-118">hello App Service plan gives your function app access tooall hello facilities of App Service.</span></span> <span data-ttu-id="96579-119">Debe elegir el plan de servicio cuando crea la instancia de Function App y actualmente no se puede cambiar.</span><span class="sxs-lookup"><span data-stu-id="96579-119">You must choose your service plan when your function app is created, and it cannot currently be changed.</span></span> <span data-ttu-id="96579-120">Para más información, consulte [Elección de un plan de hospedaje de Azure Functions](functions-scale.md).</span><span class="sxs-lookup"><span data-stu-id="96579-120">For more information, see [Choose an Azure Functions hosting plan](functions-scale.md).</span></span>

<span data-ttu-id="96579-121">Si tiene previsto toorun funciones de JavaScript en un plan de servicio de aplicaciones, debe elegir un plan con menos núcleos.</span><span class="sxs-lookup"><span data-stu-id="96579-121">If you are planning toorun JavaScript functions on an App Service plan, you should choose a plan with fewer cores.</span></span> <span data-ttu-id="96579-122">Para obtener más información, vea hello [referencia de JavaScript para funciones](functions-reference-node.md#choose-single-core-app-service-plans).</span><span class="sxs-lookup"><span data-stu-id="96579-122">For more information, see hello [JavaScript reference for Functions](functions-reference-node.md#choose-single-core-app-service-plans).</span></span>

<a name="storage-account-requirements"></a>

## <a name="storage-account-requirements"></a><span data-ttu-id="96579-123">Requisitos de la cuenta de almacenamiento</span><span class="sxs-lookup"><span data-stu-id="96579-123">Storage account requirements</span></span>

<span data-ttu-id="96579-124">Al crear una aplicación de la función en el servicio de aplicaciones, debe crear o vincular la cuenta del almacenamiento de Azure de propósito general tooa que admite el almacenamiento de Blob, cola y tabla.</span><span class="sxs-lookup"><span data-stu-id="96579-124">When creating a function app in App Service, you must create or link tooa general-purpose Azure Storage account that supports Blob, Queue, and Table storage.</span></span> <span data-ttu-id="96579-125">A nivel interno, Functions usa Storage para operaciones como la administración de desencadenadores y las ejecuciones de la función de registro.</span><span class="sxs-lookup"><span data-stu-id="96579-125">Internally, Functions uses Storage for operations such as managing triggers and logging function executions.</span></span> <span data-ttu-id="96579-126">Algunas cuentas de almacenamiento no son compatibles con colas ni tablas, como las cuentas de almacenamiento solo para blob, Almacenamiento Premium de Azure y cuentas de almacenamiento de uso general con replicación ZRS.</span><span class="sxs-lookup"><span data-stu-id="96579-126">Some storage accounts do not support queues and tables, such as blob-only storage accounts, Azure Premium Storage, and general-purpose storage accounts with ZRS replication.</span></span> <span data-ttu-id="96579-127">Estas cuentas se filtran de hoja de la cuenta de almacenamiento de hello al crear una aplicación de la función.</span><span class="sxs-lookup"><span data-stu-id="96579-127">These accounts are filtered out of from hello Storage Account blade when creating a function app.</span></span>

>[!NOTE]
><span data-ttu-id="96579-128">Cuando se usa el plan de hospedaje de consumo de hello, se almacenan los archivos de configuración de código y el enlace de función en el almacenamiento de archivos de Azure en la cuenta de almacenamiento principal de Hola.</span><span class="sxs-lookup"><span data-stu-id="96579-128">When using hello Consumption hosting plan, your function code and binding configuration files are stored in Azure File storage in hello main storage account.</span></span> <span data-ttu-id="96579-129">Cuando se elimina la cuenta de almacenamiento principal de hello, este contenido se elimina y no se puede recuperar.</span><span class="sxs-lookup"><span data-stu-id="96579-129">When you delete hello main storage account, this content is deleted and cannot be recovered.</span></span>

<span data-ttu-id="96579-130">toolearn más información acerca de los tipos de cuenta de almacenamiento, consulte [Introducción a servicios de almacenamiento de Azure de hello](../storage/common/storage-introduction.md#introducing-the-azure-storage-services).</span><span class="sxs-lookup"><span data-stu-id="96579-130">toolearn more about storage account types, see [Introducing hello Azure Storage Services](../storage/common/storage-introduction.md#introducing-the-azure-storage-services).</span></span> 

## <a name="next-steps"></a><span data-ttu-id="96579-131">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="96579-131">Next steps</span></span>

[!INCLUDE [Functions quickstart next steps](../../includes/functions-quickstart-next-steps.md)]



