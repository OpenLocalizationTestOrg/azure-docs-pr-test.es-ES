---
title: "directivas de acceso de aaaData en visión de serie de tiempo de Azure | Documentos de Microsoft"
description: "En este tutorial, aprenderá toomanage las directivas de acceso de datos en información de la serie de tiempo"
keywords: 
services: time-series-insights
documentationcenter: 
author: op-ravi
manager: jhubbard
editor: cgronlun
ms.assetid: 
ms.service: time-series-insights
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 05/01/2017
ms.author: omravi
ms.openlocfilehash: f286d26c8c5c851c523e9384760dc4b10711fa3f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="grant-data-access-tooa-time-series-insights-environment-using-azure-portal"></a><span data-ttu-id="04947-103">Conceder el entorno de visión de la serie de tiempo de datos access tooa mediante el portal de Azure</span><span class="sxs-lookup"><span data-stu-id="04947-103">Grant data access tooa Time Series Insights environment using Azure portal</span></span>

<span data-ttu-id="04947-104">Los entornos de Time Series Insights tienen dos tipos independientes de directivas de acceso:</span><span class="sxs-lookup"><span data-stu-id="04947-104">Time Series Insights environments have two independent types of access policies:</span></span>

* <span data-ttu-id="04947-105">Directivas de acceso de administración</span><span class="sxs-lookup"><span data-stu-id="04947-105">Management access policies</span></span>
* <span data-ttu-id="04947-106">Directivas de acceso a datos</span><span class="sxs-lookup"><span data-stu-id="04947-106">Data access policies</span></span>

<span data-ttu-id="04947-107">Ambas directivas conceden a las entidades de Azure Active Directory (usuarios y aplicaciones) distintos permisos en un entorno concreto.</span><span class="sxs-lookup"><span data-stu-id="04947-107">Both policies grant Azure Active Directory principals (users and apps) various permissions on a particular environment.</span></span> <span data-ttu-id="04947-108">Hello las entidades de seguridad (usuarios y aplicaciones) deben pertenecer toohello active directory (o "Inquilino de Azure") asociado a la suscripción de Hola que contiene el entorno de Hola.</span><span class="sxs-lookup"><span data-stu-id="04947-108">hello principals (users and apps) must belong toohello active directory (or “Azure tenant”) associated with hello subscription containing hello environment.</span></span>

<span data-ttu-id="04947-109">Directivas de administración de acceso conceder toohello relacionadas de la configuración de permisos del entorno de hello, como</span><span class="sxs-lookup"><span data-stu-id="04947-109">Management access policies grant permissions related toohello configuration of hello environment, such as</span></span>
*   <span data-ttu-id="04947-110">Creación y eliminación del entorno de hello, orígenes de eventos, hacer referencia a conjuntos de datos, y</span><span class="sxs-lookup"><span data-stu-id="04947-110">Creation and deletion of hello environment, event sources, reference data sets, and</span></span>
*   <span data-ttu-id="04947-111">Administración de directivas de acceso de datos de Hola.</span><span class="sxs-lookup"><span data-stu-id="04947-111">Management of hello data access policies.</span></span>

<span data-ttu-id="04947-112">Las directivas de acceso de datos conceder permisos en las consultas de datos tooissue, manipulan los datos de referencia de entorno de Hola y compartan las consultas guardadas y perspectivas asociadas con el entorno de Hola.</span><span class="sxs-lookup"><span data-stu-id="04947-112">Data access policies grant permissions tooissue data queries, manipulate reference data in hello environment, and share saved queries and perspectives associated with hello environment.</span></span>

<span data-ttu-id="04947-113">dos tipos de directivas de Hello permiten una separación clara entre administración de toohello de acceso de entorno de Hola y acceder a los datos dentro del entorno de hello toohello.</span><span class="sxs-lookup"><span data-stu-id="04947-113">hello two kinds of policies allow clear separation between access toohello management of hello environment and access toohello data inside hello environment.</span></span> <span data-ttu-id="04947-114">Por ejemplo, es posible toosetup un entorno de forma que Hola propietario/creador del entorno de Hola se quita del acceso a datos de Hola.</span><span class="sxs-lookup"><span data-stu-id="04947-114">For example, it is possible toosetup an environment such that hello owner/creator of hello environment is removed from hello data access.</span></span> <span data-ttu-id="04947-115">Así como a los usuarios y servicios que se permiten tooread datos desde el entorno de hello no pueden concederse ninguna configuración de toohello de acceso de entorno de Hola.</span><span class="sxs-lookup"><span data-stu-id="04947-115">As well as users and services that are allowed tooread data from hello environment may be granted no access toohello configuration of hello environment.</span></span>

## <a name="grant-data-access"></a><span data-ttu-id="04947-116">Concesión de acceso a datos</span><span class="sxs-lookup"><span data-stu-id="04947-116">Grant data access</span></span>
<span data-ttu-id="04947-117">Hello pasos siguientes muestran cómo tener acceso datos toogrant para una entidad de seguridad de usuario:</span><span class="sxs-lookup"><span data-stu-id="04947-117">hello following steps show how toogrant data access for a user principal:</span></span>

1.  <span data-ttu-id="04947-118">Inicie sesión en toohello [portal de Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="04947-118">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>
2.  <span data-ttu-id="04947-119">Haga clic en "Todos los recursos" en el menú Hola izquierda Hola de hello portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="04947-119">Click “All resources” in hello menu on hello left side of hello Azure portal.</span></span>
3.  <span data-ttu-id="04947-120">Seleccione el entorno de Time Series Insights.</span><span class="sxs-lookup"><span data-stu-id="04947-120">Select your Time Series Insights environment.</span></span>

  ![Administrar el origen de información de la serie de tiempo de hello: entorno](media/data-access/getstarted-grant-data-access1.png)

4.  <span data-ttu-id="04947-122">Seleccione “Acceso a plano de datos” y haga clic en “Agregar”.</span><span class="sxs-lookup"><span data-stu-id="04947-122">Select “Data Plane Access”, click “Add”</span></span>

  ![Administrar el origen de información de la serie de tiempo de hello: agregar](media/data-access/getstarted-grant-data-access2.png)

5.  <span data-ttu-id="04947-124">Haga clic en "Seleccionar usuario".</span><span class="sxs-lookup"><span data-stu-id="04947-124">Click “Select user”.</span></span>
6.  <span data-ttu-id="04947-125">Busque y seleccione el usuario por correo electrónico de Hola.</span><span class="sxs-lookup"><span data-stu-id="04947-125">Search and select user by hello email.</span></span>
7.  <span data-ttu-id="04947-126">Haga clic en "Seleccionar" en la hoja "Seleccionar usuarios".</span><span class="sxs-lookup"><span data-stu-id="04947-126">Click “Select” in “Select User” blade.</span></span>

  ![Administrar el origen de información de la serie de tiempo de hello: seleccione el usuario](media/data-access/getstarted-grant-data-access3.png)

8.  <span data-ttu-id="04947-128">Haga clic en "Seleccionar rol".</span><span class="sxs-lookup"><span data-stu-id="04947-128">Click “Select role”.</span></span>
9.  <span data-ttu-id="04947-129">Seleccione "Colaborador" Si desea que los datos de referencia de tooallow usuario toochange y compartir las consultas guardadas y las perspectivas con otros usuarios del entorno de Hola.</span><span class="sxs-lookup"><span data-stu-id="04947-129">Select “Contributor” if you want tooallow user toochange reference data and share saved queries and perspectives with other users of hello environment.</span></span> <span data-ttu-id="04947-130">En caso contrario, seleccionar datos de consulta de usuario de "Lectura" tooallow entorno hello y guarde personales consultas (no compartidas) en el entorno de Hola.</span><span class="sxs-lookup"><span data-stu-id="04947-130">Otherwise select “Reader” tooallow user query data in hello environment and save personal (not shared) queries in hello environment.</span></span>
10. <span data-ttu-id="04947-131">Haga clic en "Aceptar" en la hoja de Hola "Seleccionar rol".</span><span class="sxs-lookup"><span data-stu-id="04947-131">Click “Ok” in hello “Select Role” blade.</span></span>

  ![Administrar el origen de información de la serie de tiempo de hello: Seleccionar rol](media/data-access/getstarted-grant-data-access4.png)

11. <span data-ttu-id="04947-133">Haga clic en "Aceptar" en la hoja de Hola "Seleccionar rol de usuario".</span><span class="sxs-lookup"><span data-stu-id="04947-133">Click “Ok” in hello “Select User Role” blade.</span></span>
12. <span data-ttu-id="04947-134">Debería ver lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="04947-134">You should see:</span></span>

  ![Administrar el origen de información de la serie de tiempo de hello: resultados](media/data-access/getstarted-grant-data-access5.png)

## <a name="next-steps"></a><span data-ttu-id="04947-136">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="04947-136">Next steps</span></span>

* [<span data-ttu-id="04947-137">Creación de un origen de eventos</span><span class="sxs-lookup"><span data-stu-id="04947-137">Create an event source</span></span>](time-series-insights-add-event-source.md)
* <span data-ttu-id="04947-138">[Enviar eventos](time-series-insights-send-events.md) toohello origen del evento</span><span class="sxs-lookup"><span data-stu-id="04947-138">[Send events](time-series-insights-send-events.md) toohello event source</span></span>
* <span data-ttu-id="04947-139">Vea el entorno en el [portal de Time Series Insights](https://insights.timeseries.azure.com)</span><span class="sxs-lookup"><span data-stu-id="04947-139">View your environment in [Time Series Insights Portal](https://insights.timeseries.azure.com)</span></span>
