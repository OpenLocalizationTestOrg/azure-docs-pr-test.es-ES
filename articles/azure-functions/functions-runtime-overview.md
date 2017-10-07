---
title: "información general de las funciones en tiempo de ejecución aaaAzure | Documentos de Microsoft"
description: "Información general de hello vista previa en tiempo de ejecución de funciones de Azure"
services: functions
documentationcenter: 
author: apwestgarth
manager: stefsch
editor: 
ms.assetid: 
ms.service: functions
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: multiple
ms.topic: article
ms.date: 05/08/2017
ms.author: anwestg
ms.openlocfilehash: 8ce3e5037731d499c330b395c89c90109d18d65b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="azure-functions-runtime-overview"></a><span data-ttu-id="24e62-103">Introducción al Sistema en ejecución de Azure Functions</span><span class="sxs-lookup"><span data-stu-id="24e62-103">Azure Functions Runtime Overview</span></span>

<span data-ttu-id="24e62-104">Hola en tiempo de ejecución de funciones de Azure proporciona una nueva forma para tootake aprovechar simplicidad de Hola y la flexibilidad de las funciones de Azure de hello en local de modelo de programación.</span><span class="sxs-lookup"><span data-stu-id="24e62-104">hello Azure Functions Runtime provides a new way for you tootake advantage of hello simplicity and flexibility of hello Azure Functions programming model on-premises.</span></span> <span data-ttu-id="24e62-105">Basado en hello mismo abra raíces de origen como funciones de Azure, en tiempo de ejecución de funciones de Azure es tooprovide implementado de forma local un desarrollo casi idéntico experiencia como servicio en la nube Hola.</span><span class="sxs-lookup"><span data-stu-id="24e62-105">Built on hello same open source roots as Azure Functions, Azure Functions Runtime is deployed on-premises tooprovide a nearly identical development experience as hello cloud service.</span></span>

![Portal del Sistema en ejecución de Azure Functions (versión preliminar)][1]

<span data-ttu-id="24e62-107">Hola en tiempo de ejecución de funciones de Azure proporciona una manera para que las funciones de Azure tooexperience antes de confirmar toohello en la nube.</span><span class="sxs-lookup"><span data-stu-id="24e62-107">hello Azure Functions Runtime provides a way for you tooexperience Azure Functions before committing toohello cloud.</span></span> <span data-ttu-id="24e62-108">De esta manera, recursos de código de hello que compilar, a continuación, pueden considerarse con se toohello en la nube cuando se migra.</span><span class="sxs-lookup"><span data-stu-id="24e62-108">In this way, hello code assets you build can then be taken with you toohello cloud when you migrate.</span></span>  <span data-ttu-id="24e62-109">en tiempo de ejecución de Hello también abre nuevas opciones para usted, como el uso de capacidad de proceso de reserva de Hola de los procesos de lote de toorun de equipos local durante la noche.</span><span class="sxs-lookup"><span data-stu-id="24e62-109">hello runtime also opens up new options for you, such as using hello spare compute power of your on-premises computers toorun batch processes overnight.</span></span> <span data-ttu-id="24e62-110">También puede usar dispositivos dentro de sus organización tooconditionally envío datos tooother los sistemas, tanto de forma local y en la nube de Hola.</span><span class="sxs-lookup"><span data-stu-id="24e62-110">You can also use devices within your organization tooconditionally send data tooother systems, both on-premises and in hello cloud.</span></span>

<span data-ttu-id="24e62-111">Hola en tiempo de ejecución de funciones de Azure consta de dos partes:</span><span class="sxs-lookup"><span data-stu-id="24e62-111">hello Azure Functions Runtime consists of two pieces:</span></span>
* <span data-ttu-id="24e62-112">Rol de administración del Sistema en ejecución de Azure Functions</span><span class="sxs-lookup"><span data-stu-id="24e62-112">Azure Functions Runtime Management Role</span></span>
* <span data-ttu-id="24e62-113">Rol de trabajo del Sistema en ejecución de Azure Functions</span><span class="sxs-lookup"><span data-stu-id="24e62-113">Azure Functions Runtime Worker Role</span></span>

## <a name="azure-functions-management-role"></a><span data-ttu-id="24e62-114">Rol de administración de Azure Functions</span><span class="sxs-lookup"><span data-stu-id="24e62-114">Azure Functions Management Role</span></span>

<span data-ttu-id="24e62-115">Hola rol de administración de funciones de Azure proporciona un host para la administración de Hola de funciones local.</span><span class="sxs-lookup"><span data-stu-id="24e62-115">hello Azure Functions Management Role provides a host for hello management of your Functions on-premises.</span></span> <span data-ttu-id="24e62-116">Esta función realiza Hola siguientes tareas:</span><span class="sxs-lookup"><span data-stu-id="24e62-116">This role performs hello following tasks:</span></span>

* <span data-ttu-id="24e62-117">Hospedaje del Portal de administración de funciones de Azure, que es Hola Hola Hola misma vea Hola [portal de Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="24e62-117">Hosting of hello Azure Functions Management Portal, which is hello hello same one you see in hello [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="24e62-118">Esto permite desarrollar sus funciones en Hola igual manera que lo haría en hello portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="24e62-118">This lets you develop your functions in hello same way as you would in hello Azure portal.</span></span>
* <span data-ttu-id="24e62-119">Distribución de funciones entre varios trabajadores de Functions.</span><span class="sxs-lookup"><span data-stu-id="24e62-119">Distributing functions across multiple Functions workers.</span></span>
* <span data-ttu-id="24e62-120">Proporciona un punto de conexión de publicación para que pueda publicar sus funciones directamente desde Microsoft Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="24e62-120">Providing a publishing endpoint so that you can publish your functions direct from Microsoft Visual Studio.</span></span>

## <a name="azure-functions-worker-role"></a><span data-ttu-id="24e62-121">Rol de trabajo de Azure Functions</span><span class="sxs-lookup"><span data-stu-id="24e62-121">Azure Functions Worker Role</span></span>

<span data-ttu-id="24e62-122">Roles de trabajo de Hello Azure funciones se implementan en los contenedores de Windows y es donde se ejecuta el código de función.</span><span class="sxs-lookup"><span data-stu-id="24e62-122">hello Azure Functions Worker Roles are deployed in Windows Containers and this is where your function code executes.</span></span>  <span data-ttu-id="24e62-123">Puede implementar varios roles de trabajo en toda la organización; se trata de una manera clave en que los clientes pueden hacer uso de la capacidad de proceso que sobra.</span><span class="sxs-lookup"><span data-stu-id="24e62-123">You can deploy multiple Worker Roles throughout your organization and is a key way in which customers can make use of spare compute power.</span></span>

## <a name="minimum-requirements"></a><span data-ttu-id="24e62-124">Requisitos mínimos</span><span class="sxs-lookup"><span data-stu-id="24e62-124">Minimum Requirements</span></span>

<span data-ttu-id="24e62-125">tooget partió hello en tiempo de ejecución las funciones de Azure debe tener una máquina con **Windows Server 2016 o Windows 10 creadores Update** con acceso tooa **SQL Server** instancia.</span><span class="sxs-lookup"><span data-stu-id="24e62-125">tooget started with hello Azure Functions Runtime you must have a machine with **Windows Server 2016 or Windows 10 Creators Update** with access tooa **SQL Server** instance.</span></span>

## <a name="next-steps"></a><span data-ttu-id="24e62-126">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="24e62-126">Next Steps</span></span>

<span data-ttu-id="24e62-127">Instalar hello [vista previa en tiempo de ejecución de funciones de Azure](https://aka.ms/azafr)</span><span class="sxs-lookup"><span data-stu-id="24e62-127">Install hello [Azure Functions Runtime preview](https://aka.ms/azafr)</span></span>

<!--Image references-->
[1]: ./media/functions-runtime-overview/AzureFunctionsRuntime_Portal.png
