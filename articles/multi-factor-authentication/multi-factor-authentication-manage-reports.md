---
title: Informes de acceso y uso para Azure MFA | Microsoft Docs
description: "Aquí se describe cómo utilizar la característica de informes de Azure Multi-Factor Authentication."
services: multi-factor-authentication
documentationcenter: 
author: kgremban
manager: femila
editor: curtand
ms.assetid: 3f6b33c4-04c8-47d4-aecb-aa39a61c4189
ms.service: multi-factor-authentication
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/03/2017
ms.author: kgremban
ms.openlocfilehash: f76e726c6a67de4b0472c0e97f9e72c31c14c4f2
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="reports-in-azure-multi-factor-authentication"></a><span data-ttu-id="67d97-103">Informes en Azure Multi-Factor Authentication</span><span class="sxs-lookup"><span data-stu-id="67d97-103">Reports in Azure Multi-Factor Authentication</span></span>
<span data-ttu-id="67d97-104">Azure Multi-Factor Authentication proporciona varios tipos de informes que usted o su organización pueden usar.</span><span class="sxs-lookup"><span data-stu-id="67d97-104">Azure Multi-Factor Authentication provides several reports that can be used by you and your organization.</span></span> <span data-ttu-id="67d97-105">Estos informes son accesibles a través del Portal de administración de Multi-Factor Authentication.</span><span class="sxs-lookup"><span data-stu-id="67d97-105">These reports can be accessed through the Multi-Factor Authentication Management Portal.</span></span> <span data-ttu-id="67d97-106">La siguiente es una lista de los informes disponibles:</span><span class="sxs-lookup"><span data-stu-id="67d97-106">The following is a list of the available reports:</span></span>

| <span data-ttu-id="67d97-107">Informe</span><span class="sxs-lookup"><span data-stu-id="67d97-107">Report</span></span> | <span data-ttu-id="67d97-108">Descripción</span><span class="sxs-lookup"><span data-stu-id="67d97-108">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="67d97-109">Uso</span><span class="sxs-lookup"><span data-stu-id="67d97-109">Usage</span></span> |<span data-ttu-id="67d97-110">Los informes de uso muestran información sobre el uso general, resúmenes y detalles de usuario.</span><span class="sxs-lookup"><span data-stu-id="67d97-110">The usage reports display information on overall usage, user summary, and user details.</span></span> |
| <span data-ttu-id="67d97-111">Estado del servidor</span><span class="sxs-lookup"><span data-stu-id="67d97-111">Server Status</span></span> |<span data-ttu-id="67d97-112">Este informe muestra el estado de los Servidores Multi-Factor Authentication asociados a su cuenta.</span><span class="sxs-lookup"><span data-stu-id="67d97-112">This report displays the status of Multi-Factor Authentication Servers associated with your account.</span></span> |
| <span data-ttu-id="67d97-113">Historial de usuarios bloqueados</span><span class="sxs-lookup"><span data-stu-id="67d97-113">Blocked User History</span></span> |<span data-ttu-id="67d97-114">Estos informes muestran el historial de solicitudes para bloquear o desbloquear a los usuarios.</span><span class="sxs-lookup"><span data-stu-id="67d97-114">These reports show the history of requests to block or unblock users.</span></span> |
| <span data-ttu-id="67d97-115">Historial de usuarios omitidos</span><span class="sxs-lookup"><span data-stu-id="67d97-115">Bypassed User History</span></span> |<span data-ttu-id="67d97-116">Muestra el historial de solicitudes para omitir Multi-Factor Authentication para el número de teléfono de un usuario.</span><span class="sxs-lookup"><span data-stu-id="67d97-116">Shows the history of requests to bypass Multi-Factor Authentication for a user's phone number.</span></span> |
| <span data-ttu-id="67d97-117">Alerta de fraude</span><span class="sxs-lookup"><span data-stu-id="67d97-117">Fraud Alert</span></span> |<span data-ttu-id="67d97-118">Muestra un historial de las alertas de fraude enviadas durante el intervalo de fechas especificado.</span><span class="sxs-lookup"><span data-stu-id="67d97-118">Shows a history of fraud alerts submitted during the date range you specified.</span></span> |
| <span data-ttu-id="67d97-119">En cola</span><span class="sxs-lookup"><span data-stu-id="67d97-119">Queued</span></span> |<span data-ttu-id="67d97-120">Enumera los informes en cola para su procesamiento y su estado.</span><span class="sxs-lookup"><span data-stu-id="67d97-120">Lists reports queued for processing and their status.</span></span> <span data-ttu-id="67d97-121">Cuando el informe se haya completado, se proporciona un vínculo para descargar o ver el informe.</span><span class="sxs-lookup"><span data-stu-id="67d97-121">A link to download or view the report is provided when the report is complete.</span></span> |

## <a name="view-reports"></a><span data-ttu-id="67d97-122">Ver informes</span><span class="sxs-lookup"><span data-stu-id="67d97-122">View reports</span></span>
1. <span data-ttu-id="67d97-123">Inicie sesión en el [Portal de Azure clásico](https://manage.windowsazure.com).</span><span class="sxs-lookup"><span data-stu-id="67d97-123">Sign in to the [Azure classic portal](https://manage.windowsazure.com).</span></span>
2. <span data-ttu-id="67d97-124">En la parte izquierda, seleccione Active Directory.</span><span class="sxs-lookup"><span data-stu-id="67d97-124">On the left, select Active Directory.</span></span>
3. <span data-ttu-id="67d97-125">Siga una de estas dos opciones, dependiendo de si usa proveedores de autenticación:</span><span class="sxs-lookup"><span data-stu-id="67d97-125">Follow one of these two options, depending on whether you use Auth Providers:</span></span>
   * <span data-ttu-id="67d97-126">**Opción 1**: haga clic en la pestaña Proveedores de autenticación multifactor.</span><span class="sxs-lookup"><span data-stu-id="67d97-126">**Option 1**: Click the Multi-Factor Auth Providers tab.</span></span> <span data-ttu-id="67d97-127">Seleccione el proveedor de autenticación multifactor y haga clic en el botón **Administrar** de la parte inferior.</span><span class="sxs-lookup"><span data-stu-id="67d97-127">Select your MFA provider and click the **Manage** button at the bottom.</span></span>
   * <span data-ttu-id="67d97-128">**Opción 2**: seleccione el directorio y haga clic en la pestaña **Configurar**.</span><span class="sxs-lookup"><span data-stu-id="67d97-128">**Option 2**: Select your directory and go to the **Configure** tab.</span></span> <span data-ttu-id="67d97-129">En la sección de autenticación multifactor, seleccione **Administrar configuración del servicio**.</span><span class="sxs-lookup"><span data-stu-id="67d97-129">Under the multi-factor authentication section, select **Manage service settings**.</span></span> <span data-ttu-id="67d97-130">En la parte inferior de la página Configuración del servicio MFA, haga clic en el vínculo Ir al portal.</span><span class="sxs-lookup"><span data-stu-id="67d97-130">At the bottom of the MFA Service Settings page, click the Go to the portal link.</span></span>
4. <span data-ttu-id="67d97-131">En el Portal de administración de Azure Multi-Factor Authentication, seleccione el tipo de informe que desea en la sección **Ver un informe** en el panel de navegación izquierdo.</span><span class="sxs-lookup"><span data-stu-id="67d97-131">In the Azure Multi-Factor Authentication Management Portal, select the type of report you want from the **View a Report** section in the left navigation.</span></span>

<span data-ttu-id="67d97-132"><center>![Nube](./media/multi-factor-authentication-manage-reports/report.png)</center></span><span class="sxs-lookup"><span data-stu-id="67d97-132"><center>![Cloud](./media/multi-factor-authentication-manage-reports/report.png)</center></span></span>


<span data-ttu-id="67d97-133">**Recursos adicionales**</span><span class="sxs-lookup"><span data-stu-id="67d97-133">**Additional Resources**</span></span>

* [<span data-ttu-id="67d97-134">Para los usuarios</span><span class="sxs-lookup"><span data-stu-id="67d97-134">For Users</span></span>](end-user/multi-factor-authentication-end-user.md)
* [<span data-ttu-id="67d97-135">Azure Multi-Factor Authenticaton en MSDN</span><span class="sxs-lookup"><span data-stu-id="67d97-135">Azure Multi-Factor Authentication on MSDN</span></span>](https://msdn.microsoft.com/library/azure/dn249471.aspx)
