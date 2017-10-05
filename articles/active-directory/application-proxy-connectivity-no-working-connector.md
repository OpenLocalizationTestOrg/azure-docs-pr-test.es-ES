---
title: "No se encontró ningún grupo de conectores en funcionamiento para una aplicación de proxy de aplicación | Microsoft Docs"
description: "Solucione los problemas que puedan surgir cuando no haya ningún conector en funcionamiento en un grupo de conectores para su aplicación con el proxy de aplicación de Azure AD"
services: active-directory
documentationcenter: 
author: ajamess
manager: femila
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/11/2017
ms.author: asteen
ms.openlocfilehash: 4945958deedc8a1d9989ff901192c03a5363b4dc
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/03/2017
---
# <a name="no-working-connector-group-found-for-an-application-proxy-application"></a><span data-ttu-id="ca4e9-103">No se encontró ningún grupo de conectores en funcionamiento para una aplicación de proxy de aplicación</span><span class="sxs-lookup"><span data-stu-id="ca4e9-103">No working connector group found for an Application Proxy application</span></span>

<span data-ttu-id="ca4e9-104">Este artículo lo ayuda a solucionar problemas habituales que surgen cuando no se detecta ningún conector para una aplicación de proxy de aplicación integrada con Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="ca4e9-104">This article help you to resolve the common issues faced when there is not a connector detected for an Application Proxy application integrated with Azure Active Directory.</span></span>

## <a name="overview-of-steps"></a><span data-ttu-id="ca4e9-105">Introducción a los pasos</span><span class="sxs-lookup"><span data-stu-id="ca4e9-105">Overview of steps</span></span>
<span data-ttu-id="ca4e9-106">Si no hay ningún conector en funcionamiento en un grupo de conectores para la aplicación, hay varias maneras de resolver el problema:</span><span class="sxs-lookup"><span data-stu-id="ca4e9-106">If there is no working Connector in a Connector Group for your application, there are a few ways to resolve the problem:</span></span>

-   <span data-ttu-id="ca4e9-107">Si no tiene ningún conector en el grupo, puede hacer lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="ca4e9-107">If you have no connectors in the group, you can:</span></span>

    -   <span data-ttu-id="ca4e9-108">Descargue un nuevo conector en el servidor local correcto y asígnelo a este grupo.</span><span class="sxs-lookup"><span data-stu-id="ca4e9-108">Download a new Connector on the right on-prem server, and assign it to this group</span></span>

    -   <span data-ttu-id="ca4e9-109">Mueva un conector activo al grupo.</span><span class="sxs-lookup"><span data-stu-id="ca4e9-109">Move an active Connector into the group</span></span>

-   <span data-ttu-id="ca4e9-110">Si no tiene ningún conector activo en el grupo, puede hacer lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="ca4e9-110">If you have no active connectors in the group, you can:</span></span>

    -   <span data-ttu-id="ca4e9-111">Identifique el motivo por el que el conector está inactivo y resuélvalo.</span><span class="sxs-lookup"><span data-stu-id="ca4e9-111">Identify the reason your Connector is inactive and resolve</span></span>

    -   <span data-ttu-id="ca4e9-112">Mueva un conector activo al grupo.</span><span class="sxs-lookup"><span data-stu-id="ca4e9-112">Move an active Connector into the group</span></span>

<span data-ttu-id="ca4e9-113">Para saber cuál de estos es el problema, abra el menú "Proxy de la aplicación" en la aplicación y vea el mensaje de advertencia del grupo de conectores.</span><span class="sxs-lookup"><span data-stu-id="ca4e9-113">To know which of these is the issue, open the “Application Proxy” menu in your Application, and look at the Connector Group warning message.</span></span> <span data-ttu-id="ca4e9-114">Especifica si el grupo necesita al menos un conector (no hay ninguno en el grupo) o si no tiene ninguno activo (es probable que tenga conectores inactivos).</span><span class="sxs-lookup"><span data-stu-id="ca4e9-114">It specify either that the group needs at least one Connector (you have none in the group) or that it has no active Connectors (though you likely have inactive Connectors).</span></span>

   ![Selección de grupos de conectores en Azure Portal](./media/application-proxy-connectivity-no-working-connector/no-active-connector.png)

<span data-ttu-id="ca4e9-116">Para ver información detallada sobre cada una de estas opciones, consulte la sección correspondiente a continuación.</span><span class="sxs-lookup"><span data-stu-id="ca4e9-116">For details on each of these options, see the corresponding section below.</span></span> <span data-ttu-id="ca4e9-117">En cada una, se da por supuesto que empieza desde la página de administración del conector.</span><span class="sxs-lookup"><span data-stu-id="ca4e9-117">Each of these assumes that you are starting from the Connector management page.</span></span> <span data-ttu-id="ca4e9-118">Si ve el mensaje de error anterior, puede ir a esta página si hace clic en el mensaje de advertencia.</span><span class="sxs-lookup"><span data-stu-id="ca4e9-118">If you are looking at the error message above, you can go to this page by clicking on the warning message.</span></span> <span data-ttu-id="ca4e9-119">De lo contrario, para encontrarlo, vaya a **Azure Active Directory** y haga clic en **Aplicaciones empresariales** y en **Proxy de la aplicación**.</span><span class="sxs-lookup"><span data-stu-id="ca4e9-119">Otherwise this can be found by going to **Azure Active Directory**, clicking on **Enterprise Applications**, then **Application Proxy.**</span></span>

   ![Administración de grupos de conectores en Azure Portal](./media/application-proxy-connectivity-no-working-connector/app-proxy.png)

## <a name="download-a-new-connector"></a><span data-ttu-id="ca4e9-121">Descarga de un nuevo conector</span><span class="sxs-lookup"><span data-stu-id="ca4e9-121">Download a new Connector</span></span>

<span data-ttu-id="ca4e9-122">Para descargar un conector nuevo, use el botón "Descargar conector" en la parte superior de la página.</span><span class="sxs-lookup"><span data-stu-id="ca4e9-122">To download a new Connector, use the “Download Connector” button at the top of the page.</span></span>

<span data-ttu-id="ca4e9-123">Tenga en cuenta que el conector debe instalarse en una máquina con línea de visión directa a la aplicación back-end y se suele colocar en el mismo servidor que la aplicación.</span><span class="sxs-lookup"><span data-stu-id="ca4e9-123">note the Connector needs to be installed on a machine with direct line of sight to the backend application, and is typically placed on the same server as the application.</span></span> <span data-ttu-id="ca4e9-124">Después de la descarga, el conector debería aparecer en este menú.</span><span class="sxs-lookup"><span data-stu-id="ca4e9-124">After downloading, the Connector should appear in this menu.</span></span> <span data-ttu-id="ca4e9-125">Haga clic en el conector y compruebe en la lista desplegable "Grupo de conectores" que pertenece al grupo adecuado.</span><span class="sxs-lookup"><span data-stu-id="ca4e9-125">click the Connector, and use the “Connector Group” drop-down to make sure it belongs to the right group.</span></span> <span data-ttu-id="ca4e9-126">Guarde el cambio.</span><span class="sxs-lookup"><span data-stu-id="ca4e9-126">Save the change.</span></span>

   ![Descarga del conector de Azure Portal](./media/application-proxy-connectivity-no-working-connector/download-connector.png)
   
## <a name="move-an-active-connector"></a><span data-ttu-id="ca4e9-128">Movimiento de un conector activo</span><span class="sxs-lookup"><span data-stu-id="ca4e9-128">Move an Active Connector</span></span>

<span data-ttu-id="ca4e9-129">Si tiene un conector activo que debería pertenecer a este grupo y tiene línea de visión a la aplicación back-end de destino, puede moverlo al grupo asignado.</span><span class="sxs-lookup"><span data-stu-id="ca4e9-129">If you have an active Connector that should belong to the group and has line of sight to the target backend application, you can move the Connector into the assigned group.</span></span> <span data-ttu-id="ca4e9-130">Para ello, haga clic en el conector.</span><span class="sxs-lookup"><span data-stu-id="ca4e9-130">To do so, click the Connector.</span></span> <span data-ttu-id="ca4e9-131">En el campo "Grupo de conectores", seleccione el grupo correcto en la lista desplegable y haga clic en Guardar.</span><span class="sxs-lookup"><span data-stu-id="ca4e9-131">In the “Connector Group” field, use the drop-down to select the correct group, and click Save.</span></span>

## <a name="resolve-an-inactive-connector"></a><span data-ttu-id="ca4e9-132">Resolución de un conector inactivo</span><span class="sxs-lookup"><span data-stu-id="ca4e9-132">Resolve an inactive Connector</span></span>

<span data-ttu-id="ca4e9-133">Si los únicos conectores del grupo están inactivos, es probable que estén en una máquina donde no están desbloqueados todos los puertos necesarios.</span><span class="sxs-lookup"><span data-stu-id="ca4e9-133">If the only Connectors in the group are inactive, they are likely on a machine that does not have all the necessary ports unblocked.</span></span>

<span data-ttu-id="ca4e9-134">Consulte el documento de solución de problemas de puertos para más información sobre cómo investigar este problema.</span><span class="sxs-lookup"><span data-stu-id="ca4e9-134">see the ports Troubleshoot document for details on investigating this problem.</span></span>

## <a name="next-steps"></a><span data-ttu-id="ca4e9-135">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="ca4e9-135">Next steps</span></span>
[<span data-ttu-id="ca4e9-136">Descripción de los conectores del Proxy de aplicación de Azure AD</span><span class="sxs-lookup"><span data-stu-id="ca4e9-136">Understand Azure AD Application Proxy connectors</span></span>](application-proxy-understand-connectors.md)


