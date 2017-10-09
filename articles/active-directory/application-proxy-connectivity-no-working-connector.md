---
title: "grupo de conectores de trabajo aaaNo encontró para una aplicación de Proxy de aplicación | Documentos de Microsoft"
description: "Solucionar problemas que pueden surgir cuando no hay ningún trabajo conector en un grupo de conectores para su aplicación con hello Proxy de aplicación de Azure AD"
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
ms.openlocfilehash: 4c4baf296b316db131929c9a7c618fb9960713e6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="no-working-connector-group-found-for-an-application-proxy-application"></a><span data-ttu-id="8e5bf-103">No se encontró ningún grupo de conectores en funcionamiento para una aplicación de proxy de aplicación</span><span class="sxs-lookup"><span data-stu-id="8e5bf-103">No working connector group found for an Application Proxy application</span></span>

<span data-ttu-id="8e5bf-104">La Ayuda de este artículo se problemas comunes de hello tooresolve enfrentados cuando no hay un conector detectado para una aplicación de Proxy de aplicación integrada con Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="8e5bf-104">This article help you tooresolve hello common issues faced when there is not a connector detected for an Application Proxy application integrated with Azure Active Directory.</span></span>

## <a name="overview-of-steps"></a><span data-ttu-id="8e5bf-105">Introducción a los pasos</span><span class="sxs-lookup"><span data-stu-id="8e5bf-105">Overview of steps</span></span>
<span data-ttu-id="8e5bf-106">Si no hay ningún trabajo conector en un grupo de conectores para la aplicación, hay algunos problemas de Hola de tooresolve maneras:</span><span class="sxs-lookup"><span data-stu-id="8e5bf-106">If there is no working Connector in a Connector Group for your application, there are a few ways tooresolve hello problem:</span></span>

-   <span data-ttu-id="8e5bf-107">Si no tiene ningún conector de grupo de hello, hacer lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="8e5bf-107">If you have no connectors in hello group, you can:</span></span>

    -   <span data-ttu-id="8e5bf-108">Descargar un nuevo conector en servidor de derecho local de Hola y asignar toothis grupo</span><span class="sxs-lookup"><span data-stu-id="8e5bf-108">Download a new Connector on hello right on-prem server, and assign it toothis group</span></span>

    -   <span data-ttu-id="8e5bf-109">Mover un conector active Hola grupo</span><span class="sxs-lookup"><span data-stu-id="8e5bf-109">Move an active Connector into hello group</span></span>

-   <span data-ttu-id="8e5bf-110">Si no tiene ningún conector de active en grupo de hello, puede:</span><span class="sxs-lookup"><span data-stu-id="8e5bf-110">If you have no active connectors in hello group, you can:</span></span>

    -   <span data-ttu-id="8e5bf-111">Identificar el motivo de hello que el conector está inactivo y resolver</span><span class="sxs-lookup"><span data-stu-id="8e5bf-111">Identify hello reason your Connector is inactive and resolve</span></span>

    -   <span data-ttu-id="8e5bf-112">Mover un conector active Hola grupo</span><span class="sxs-lookup"><span data-stu-id="8e5bf-112">Move an active Connector into hello group</span></span>

<span data-ttu-id="8e5bf-113">tooknow cuál de estos es problema de hello, abra el menú de "Proxy de aplicación" hello en la aplicación y mire el mensaje de advertencia de grupo de conectores de Hola.</span><span class="sxs-lookup"><span data-stu-id="8e5bf-113">tooknow which of these is hello issue, open hello “Application Proxy” menu in your Application, and look at hello Connector Group warning message.</span></span> <span data-ttu-id="8e5bf-114">Especifique ese grupo de hello necesita al menos un conector (no hay ninguno en el grupo de hello) o que no tiene ningún conector de active (aunque es probable que tenga conectores inactivos).</span><span class="sxs-lookup"><span data-stu-id="8e5bf-114">It specify either that hello group needs at least one Connector (you have none in hello group) or that it has no active Connectors (though you likely have inactive Connectors).</span></span>

   ![Selección de grupos de conectores en Azure Portal](./media/application-proxy-connectivity-no-working-connector/no-active-connector.png)

<span data-ttu-id="8e5bf-116">Para obtener detalles sobre cada una de estas opciones, vea Hola correspondiente sección.</span><span class="sxs-lookup"><span data-stu-id="8e5bf-116">For details on each of these options, see hello corresponding section below.</span></span> <span data-ttu-id="8e5bf-117">Cada una de ellas se da por supuesto que se inicia desde la página de administración del conector de Hola.</span><span class="sxs-lookup"><span data-stu-id="8e5bf-117">Each of these assumes that you are starting from hello Connector management page.</span></span> <span data-ttu-id="8e5bf-118">Si se trata de mensaje de error de saludo anterior, puede ir toothis página haciendo clic en el mensaje de advertencia de saludo.</span><span class="sxs-lookup"><span data-stu-id="8e5bf-118">If you are looking at hello error message above, you can go toothis page by clicking on hello warning message.</span></span> <span data-ttu-id="8e5bf-119">En caso contrario, se puede encontrar yendo demasiado**Azure Active Directory**, haga clic en **aplicaciones empresariales**, a continuación, **Proxy de aplicación.**</span><span class="sxs-lookup"><span data-stu-id="8e5bf-119">Otherwise this can be found by going too**Azure Active Directory**, clicking on **Enterprise Applications**, then **Application Proxy.**</span></span>

   ![Administración de grupos de conectores en Azure Portal](./media/application-proxy-connectivity-no-working-connector/app-proxy.png)

## <a name="download-a-new-connector"></a><span data-ttu-id="8e5bf-121">Descarga de un nuevo conector</span><span class="sxs-lookup"><span data-stu-id="8e5bf-121">Download a new Connector</span></span>

<span data-ttu-id="8e5bf-122">toodownload un conector nuevo, use el botón de "Descargar el conector" de hello al principio de Hola de página de Hola.</span><span class="sxs-lookup"><span data-stu-id="8e5bf-122">toodownload a new Connector, use hello “Download Connector” button at hello top of hello page.</span></span>

<span data-ttu-id="8e5bf-123">las necesidades de conector de hello Nota toobe instalado en un equipo con aplicaciones de línea de visión directa toohello back-end y se coloca normalmente en Hola mismo servidor que la aplicación hello.</span><span class="sxs-lookup"><span data-stu-id="8e5bf-123">note hello Connector needs toobe installed on a machine with direct line of sight toohello backend application, and is typically placed on hello same server as hello application.</span></span> <span data-ttu-id="8e5bf-124">Después de descargar, Hola conector debe aparecer en este menú.</span><span class="sxs-lookup"><span data-stu-id="8e5bf-124">After downloading, hello Connector should appear in this menu.</span></span> <span data-ttu-id="8e5bf-125">Haga clic en hello conector y usar Hola "Grupo de conectores" desplegable toomake pertenece grupo adecuado toohello seguro.</span><span class="sxs-lookup"><span data-stu-id="8e5bf-125">click hello Connector, and use hello “Connector Group” drop-down toomake sure it belongs toohello right group.</span></span> <span data-ttu-id="8e5bf-126">Guarde el cambio de Hola.</span><span class="sxs-lookup"><span data-stu-id="8e5bf-126">Save hello change.</span></span>

   ![Descargar conector Hola de hello Portal de Azure](./media/application-proxy-connectivity-no-working-connector/download-connector.png)
   
## <a name="move-an-active-connector"></a><span data-ttu-id="8e5bf-128">Movimiento de un conector activo</span><span class="sxs-lookup"><span data-stu-id="8e5bf-128">Move an Active Connector</span></span>

<span data-ttu-id="8e5bf-129">Si tiene un conector activo que debería pertenecer toohello grupo y tiene la aplicación de línea de visión toohello destino back-end, puede mover Hola conector en el grupo de hello asignado.</span><span class="sxs-lookup"><span data-stu-id="8e5bf-129">If you have an active Connector that should belong toohello group and has line of sight toohello target backend application, you can move hello Connector into hello assigned group.</span></span> <span data-ttu-id="8e5bf-130">toodo por lo tanto, haga clic en el conector de Hola.</span><span class="sxs-lookup"><span data-stu-id="8e5bf-130">toodo so, click hello Connector.</span></span> <span data-ttu-id="8e5bf-131">En el campo de "Grupo de conectores" Hola, usar grupo correcto de hello tooselect desplegable hello y haga clic en Guardar.</span><span class="sxs-lookup"><span data-stu-id="8e5bf-131">In hello “Connector Group” field, use hello drop-down tooselect hello correct group, and click Save.</span></span>

## <a name="resolve-an-inactive-connector"></a><span data-ttu-id="8e5bf-132">Resolución de un conector inactivo</span><span class="sxs-lookup"><span data-stu-id="8e5bf-132">Resolve an inactive Connector</span></span>

<span data-ttu-id="8e5bf-133">Si hello solo conectores de grupo de hello están inactivos, es probable que en un equipo que no han desbloqueado todos los puertos necesarios Hola.</span><span class="sxs-lookup"><span data-stu-id="8e5bf-133">If hello only Connectors in hello group are inactive, they are likely on a machine that does not have all hello necessary ports unblocked.</span></span>

<span data-ttu-id="8e5bf-134">Consulte los puertos de hello documento de solución de problemas para obtener más información sobre la investigación de este problema.</span><span class="sxs-lookup"><span data-stu-id="8e5bf-134">see hello ports Troubleshoot document for details on investigating this problem.</span></span>

## <a name="next-steps"></a><span data-ttu-id="8e5bf-135">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="8e5bf-135">Next steps</span></span>
[<span data-ttu-id="8e5bf-136">Descripción de los conectores del Proxy de aplicación de Azure AD</span><span class="sxs-lookup"><span data-stu-id="8e5bf-136">Understand Azure AD Application Proxy connectors</span></span>](application-proxy-understand-connectors.md)


