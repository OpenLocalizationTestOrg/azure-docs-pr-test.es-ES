---
title: "Creación de una instancia de Function App desde Azure Portal | Microsoft Docs"
description: Cree una nueva instancia de Function App en Azure App Service desde el portal.
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
ms.openlocfilehash: 85a88c537415cd6f2b6bc005cc18e3baaa29e9a4
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/29/2017
---
# <a name="create-a-function-app-from-the-azure-portal"></a><span data-ttu-id="ed45d-103">Creación de una instancia de Function App desde Azure Portal</span><span class="sxs-lookup"><span data-stu-id="ed45d-103">Create a function app from the Azure portal</span></span>

<span data-ttu-id="ed45d-104">Azure Function Apps usa la infraestructura de Azure App Service.</span><span class="sxs-lookup"><span data-stu-id="ed45d-104">Azure Function Apps uses the Azure App Service infrastructure.</span></span> <span data-ttu-id="ed45d-105">En este tema se muestra cómo crear una instancia de Function App en Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="ed45d-105">This topic shows you how to create a function app in the Azure portal.</span></span> <span data-ttu-id="ed45d-106">Una instancia de Function App es el contenedor que hospeda la ejecución de funciones individuales.</span><span class="sxs-lookup"><span data-stu-id="ed45d-106">A function app is the container that hosts the execution of individual functions.</span></span> <span data-ttu-id="ed45d-107">Cuando crea una instancia de Function App en el plan de hospedaje de App Service, esa instancia puede usar todas las características de App Service.</span><span class="sxs-lookup"><span data-stu-id="ed45d-107">When you create a function app in the App Service hosting plan, your function app can use all the features of App Service.</span></span>

## <a name="create-a-function-app"></a><span data-ttu-id="ed45d-108">Creación de una aplicación de función</span><span class="sxs-lookup"><span data-stu-id="ed45d-108">Create a function app</span></span>

[!INCLUDE [functions-create-function-app-portal](../../includes/functions-create-function-app-portal.md)]

<span data-ttu-id="ed45d-109">Cuando cree una instancia de Function App, brinde un **nombre de aplicación** válido, que solo puede incluir letras, números y guiones.</span><span class="sxs-lookup"><span data-stu-id="ed45d-109">When you create a function app, supply a valid **App name**, which can contain only letters, numbers, and hyphens.</span></span> <span data-ttu-id="ed45d-110">El carácter de subrayado (**_**) no se permite.</span><span class="sxs-lookup"><span data-stu-id="ed45d-110">Underscore (**_**) is not an allowed character.</span></span>

<span data-ttu-id="ed45d-111">Los nombres de cuentas de almacenamiento deben tener entre 3 y 24 caracteres, y solo pueden contener números y letras minúsculas.</span><span class="sxs-lookup"><span data-stu-id="ed45d-111">Storage account names must be between 3 and 24 characters in length and may contain numbers and lowercase letters only.</span></span> <span data-ttu-id="ed45d-112">El nombre de la cuenta de almacenamiento debe ser único dentro de Azure.</span><span class="sxs-lookup"><span data-stu-id="ed45d-112">Your storage account name must be unique within Azure.</span></span> 

<span data-ttu-id="ed45d-113">Después de crear la instancia de Function App, puede crear funciones individuales en uno o más lenguajes distintos.</span><span class="sxs-lookup"><span data-stu-id="ed45d-113">After the function app is created, you can create individual functions in one or more different languages.</span></span> <span data-ttu-id="ed45d-114">Cree funciones [a través del portal](functions-create-first-azure-function.md#create-function), la [implementación continua](functions-continuous-deployment.md) o mediante la [carga con FTP](https://github.com/projectkudu/kudu/wiki/Accessing-files-via-ftp).</span><span class="sxs-lookup"><span data-stu-id="ed45d-114">Create functions [by using the portal](functions-create-first-azure-function.md#create-function), [continuous deployment](functions-continuous-deployment.md), or by [uploading with FTP](https://github.com/projectkudu/kudu/wiki/Accessing-files-via-ftp).</span></span>

## <a name="service-plans"></a><span data-ttu-id="ed45d-115">Planes de servicio</span><span class="sxs-lookup"><span data-stu-id="ed45d-115">Service plans</span></span>

<span data-ttu-id="ed45d-116">Azure Functions tiene dos planes de servicio diferentes: plan de consumo y plan de App Service.</span><span class="sxs-lookup"><span data-stu-id="ed45d-116">Azure Functions has two different service plans: Consumption plan and App Service plan.</span></span> <span data-ttu-id="ed45d-117">El plan de consumo asigna automáticamente potencia de proceso cuando se ejecuta código, se escala horizontalmente cuando es necesario para gestionar la carga y se reduce horizontalmente cuando no se ejecuta código.</span><span class="sxs-lookup"><span data-stu-id="ed45d-117">The Consumption plan automatically allocates compute power when your code is running, scales-out as necessary to handle load, and then scales-in when code is not running.</span></span> <span data-ttu-id="ed45d-118">El plan de App Service da a su instancia de Function App acceso a todas las funciones de App Service.</span><span class="sxs-lookup"><span data-stu-id="ed45d-118">The App Service plan gives your function app access to all the facilities of App Service.</span></span> <span data-ttu-id="ed45d-119">Debe elegir el plan de servicio cuando crea la instancia de Function App y actualmente no se puede cambiar.</span><span class="sxs-lookup"><span data-stu-id="ed45d-119">You must choose your service plan when your function app is created, and it cannot currently be changed.</span></span> <span data-ttu-id="ed45d-120">Para más información, consulte [Elección de un plan de hospedaje de Azure Functions](functions-scale.md).</span><span class="sxs-lookup"><span data-stu-id="ed45d-120">For more information, see [Choose an Azure Functions hosting plan](functions-scale.md).</span></span>

<span data-ttu-id="ed45d-121">Si va a ejecutar funciones de JavaScript en un plan de App Service, debería elegir un plan con menos núcleos.</span><span class="sxs-lookup"><span data-stu-id="ed45d-121">If you are planning to run JavaScript functions on an App Service plan, you should choose a plan with fewer cores.</span></span> <span data-ttu-id="ed45d-122">Para obtener más información, consulte la [referencia de JavaScript relativa a las funciones](functions-reference-node.md#choose-single-core-app-service-plans).</span><span class="sxs-lookup"><span data-stu-id="ed45d-122">For more information, see the [JavaScript reference for Functions](functions-reference-node.md#choose-single-core-app-service-plans).</span></span>

<a name="storage-account-requirements"></a>

## <a name="storage-account-requirements"></a><span data-ttu-id="ed45d-123">Requisitos de la cuenta de almacenamiento</span><span class="sxs-lookup"><span data-stu-id="ed45d-123">Storage account requirements</span></span>

<span data-ttu-id="ed45d-124">Cuando crea una instancia de Function App en App Service, debe crear o vincular una cuenta de Azure Storage de uso general compatible con Blob Storage, Queue Storage y Table Storage.</span><span class="sxs-lookup"><span data-stu-id="ed45d-124">When creating a function app in App Service, you must create or link to a general-purpose Azure Storage account that supports Blob, Queue, and Table storage.</span></span> <span data-ttu-id="ed45d-125">A nivel interno, Functions usa Storage para operaciones como la administración de desencadenadores y las ejecuciones de la función de registro.</span><span class="sxs-lookup"><span data-stu-id="ed45d-125">Internally, Functions uses Storage for operations such as managing triggers and logging function executions.</span></span> <span data-ttu-id="ed45d-126">Algunas cuentas de almacenamiento no son compatibles con colas ni tablas, como las cuentas de almacenamiento solo para blob, Almacenamiento Premium de Azure y cuentas de almacenamiento de uso general con replicación ZRS.</span><span class="sxs-lookup"><span data-stu-id="ed45d-126">Some storage accounts do not support queues and tables, such as blob-only storage accounts, Azure Premium Storage, and general-purpose storage accounts with ZRS replication.</span></span> <span data-ttu-id="ed45d-127">Estas cuentas se filtran en la hoja Cuenta de almacenamiento cuando se crea una instancia de Function App.</span><span class="sxs-lookup"><span data-stu-id="ed45d-127">These accounts are filtered out of from the Storage Account blade when creating a function app.</span></span>

>[!NOTE]
><span data-ttu-id="ed45d-128">Cuando usa el plan de hospedaje de consumo, los archivos de configuración de enlace y el código de la función se almacenan en Azure File Storage en la cuenta de almacenamiento principal.</span><span class="sxs-lookup"><span data-stu-id="ed45d-128">When using the Consumption hosting plan, your function code and binding configuration files are stored in Azure File storage in the main storage account.</span></span> <span data-ttu-id="ed45d-129">Si elimina la cuenta de almacenamiento principal, este contenido se suprimirá y no se podrá recuperar.</span><span class="sxs-lookup"><span data-stu-id="ed45d-129">When you delete the main storage account, this content is deleted and cannot be recovered.</span></span>

<span data-ttu-id="ed45d-130">Para más información sobre los tipos de cuenta de almacenamiento, consulte [Introducción de los servicios Azure Storage](../storage/common/storage-introduction.md#introducing-the-azure-storage-services).</span><span class="sxs-lookup"><span data-stu-id="ed45d-130">To learn more about storage account types, see [Introducing the Azure Storage Services](../storage/common/storage-introduction.md#introducing-the-azure-storage-services).</span></span> 

## <a name="next-steps"></a><span data-ttu-id="ed45d-131">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="ed45d-131">Next steps</span></span>

[!INCLUDE [Functions quickstart next steps](../../includes/functions-quickstart-next-steps.md)]



