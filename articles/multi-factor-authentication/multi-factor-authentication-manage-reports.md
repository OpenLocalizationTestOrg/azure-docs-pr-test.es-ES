---
title: informes de uso y aaaAccess para MFA de Azure | Documentos de Microsoft
description: "Describe cómo toouse Hola característica de la autenticación multifactor Azure - informes."
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
ms.openlocfilehash: ae7ccceca4968d7ec7cf0cb1cf9e041d9997c840
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="reports-in-azure-multi-factor-authentication"></a><span data-ttu-id="b8ee6-103">Informes en Azure Multi-Factor Authentication</span><span class="sxs-lookup"><span data-stu-id="b8ee6-103">Reports in Azure Multi-Factor Authentication</span></span>
<span data-ttu-id="b8ee6-104">Azure Multi-Factor Authentication proporciona varios tipos de informes que usted o su organización pueden usar.</span><span class="sxs-lookup"><span data-stu-id="b8ee6-104">Azure Multi-Factor Authentication provides several reports that can be used by you and your organization.</span></span> <span data-ttu-id="b8ee6-105">Estos informes pueden obtenerse a través de hello Portal de administración de autenticación multifactor.</span><span class="sxs-lookup"><span data-stu-id="b8ee6-105">These reports can be accessed through hello Multi-Factor Authentication Management Portal.</span></span> <span data-ttu-id="b8ee6-106">Hola mostramos una lista de los informes disponibles de hello:</span><span class="sxs-lookup"><span data-stu-id="b8ee6-106">hello following is a list of hello available reports:</span></span>

| <span data-ttu-id="b8ee6-107">Informe</span><span class="sxs-lookup"><span data-stu-id="b8ee6-107">Report</span></span> | <span data-ttu-id="b8ee6-108">Descripción</span><span class="sxs-lookup"><span data-stu-id="b8ee6-108">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="b8ee6-109">Uso</span><span class="sxs-lookup"><span data-stu-id="b8ee6-109">Usage</span></span> |<span data-ttu-id="b8ee6-110">información de visualización de informes de uso de Hello en los detalles del usuario, el uso general y resumen de usuario.</span><span class="sxs-lookup"><span data-stu-id="b8ee6-110">hello usage reports display information on overall usage, user summary, and user details.</span></span> |
| <span data-ttu-id="b8ee6-111">Estado del servidor</span><span class="sxs-lookup"><span data-stu-id="b8ee6-111">Server Status</span></span> |<span data-ttu-id="b8ee6-112">Este informe muestra el estado de Hola de servidores de autenticación multifactor asociadas a su cuenta.</span><span class="sxs-lookup"><span data-stu-id="b8ee6-112">This report displays hello status of Multi-Factor Authentication Servers associated with your account.</span></span> |
| <span data-ttu-id="b8ee6-113">Historial de usuarios bloqueados</span><span class="sxs-lookup"><span data-stu-id="b8ee6-113">Blocked User History</span></span> |<span data-ttu-id="b8ee6-114">Estos informes muestran Hola historial de solicitudes tooblock o desbloquear usuarios.</span><span class="sxs-lookup"><span data-stu-id="b8ee6-114">These reports show hello history of requests tooblock or unblock users.</span></span> |
| <span data-ttu-id="b8ee6-115">Historial de usuarios omitidos</span><span class="sxs-lookup"><span data-stu-id="b8ee6-115">Bypassed User History</span></span> |<span data-ttu-id="b8ee6-116">Muestra el historial de Hola de solicitudes toobypass la autenticación multifactor para el número de teléfono del usuario.</span><span class="sxs-lookup"><span data-stu-id="b8ee6-116">Shows hello history of requests toobypass Multi-Factor Authentication for a user's phone number.</span></span> |
| <span data-ttu-id="b8ee6-117">Alerta de fraude</span><span class="sxs-lookup"><span data-stu-id="b8ee6-117">Fraud Alert</span></span> |<span data-ttu-id="b8ee6-118">Muestra un historial de alertas de fraude enviadas durante el intervalo de fechas de hello especificado.</span><span class="sxs-lookup"><span data-stu-id="b8ee6-118">Shows a history of fraud alerts submitted during hello date range you specified.</span></span> |
| <span data-ttu-id="b8ee6-119">En cola</span><span class="sxs-lookup"><span data-stu-id="b8ee6-119">Queued</span></span> |<span data-ttu-id="b8ee6-120">Enumera los informes en cola para su procesamiento y su estado.</span><span class="sxs-lookup"><span data-stu-id="b8ee6-120">Lists reports queued for processing and their status.</span></span> <span data-ttu-id="b8ee6-121">Cuando haya terminado el informe de hello, se proporciona un informe de Hola de toodownload o la vista de vínculo.</span><span class="sxs-lookup"><span data-stu-id="b8ee6-121">A link toodownload or view hello report is provided when hello report is complete.</span></span> |

## <a name="view-reports"></a><span data-ttu-id="b8ee6-122">Ver informes</span><span class="sxs-lookup"><span data-stu-id="b8ee6-122">View reports</span></span>
1. <span data-ttu-id="b8ee6-123">Inicie sesión en toohello [portal de Azure clásico](https://manage.windowsazure.com).</span><span class="sxs-lookup"><span data-stu-id="b8ee6-123">Sign in toohello [Azure classic portal](https://manage.windowsazure.com).</span></span>
2. <span data-ttu-id="b8ee6-124">Hola izquierda, seleccione Active Directory.</span><span class="sxs-lookup"><span data-stu-id="b8ee6-124">On hello left, select Active Directory.</span></span>
3. <span data-ttu-id="b8ee6-125">Siga una de estas dos opciones, dependiendo de si usa proveedores de autenticación:</span><span class="sxs-lookup"><span data-stu-id="b8ee6-125">Follow one of these two options, depending on whether you use Auth Providers:</span></span>
   * <span data-ttu-id="b8ee6-126">**Opción 1**: haga clic en la ficha de proveedores de autenticación multifactor de Hola. Seleccione el proveedor de MFA y haga clic en hello **administrar** situado en la parte inferior de Hola.</span><span class="sxs-lookup"><span data-stu-id="b8ee6-126">**Option 1**: Click hello Multi-Factor Auth Providers tab. Select your MFA provider and click hello **Manage** button at hello bottom.</span></span>
   * <span data-ttu-id="b8ee6-127">**Opción 2**: seleccione el directorio y vaya toohello **configurar** ficha. En la sección de la autenticación multifactor de hello, seleccione **administrar la configuración del servicio**.</span><span class="sxs-lookup"><span data-stu-id="b8ee6-127">**Option 2**: Select your directory and go toohello **Configure** tab. Under hello multi-factor authentication section, select **Manage service settings**.</span></span> <span data-ttu-id="b8ee6-128">En parte inferior de Hola de página de configuración del servicio de MFA de hello, haga clic en hello Go toohello portal vínculo.</span><span class="sxs-lookup"><span data-stu-id="b8ee6-128">At hello bottom of hello MFA Service Settings page, click hello Go toohello portal link.</span></span>
4. <span data-ttu-id="b8ee6-129">Hola Portal de administración de autenticación multifactor de Azure, seleccione el tipo de Hola de informe que desee en hello **ver un informe** sección Hola barra de navegación izquierda.</span><span class="sxs-lookup"><span data-stu-id="b8ee6-129">In hello Azure Multi-Factor Authentication Management Portal, select hello type of report you want from hello **View a Report** section in hello left navigation.</span></span>

<span data-ttu-id="b8ee6-130"><center>![Nube](./media/multi-factor-authentication-manage-reports/report.png)</center></span><span class="sxs-lookup"><span data-stu-id="b8ee6-130"><center>![Cloud](./media/multi-factor-authentication-manage-reports/report.png)</center></span></span>


<span data-ttu-id="b8ee6-131">**Recursos adicionales**</span><span class="sxs-lookup"><span data-stu-id="b8ee6-131">**Additional Resources**</span></span>

* [<span data-ttu-id="b8ee6-132">Para los usuarios</span><span class="sxs-lookup"><span data-stu-id="b8ee6-132">For Users</span></span>](end-user/multi-factor-authentication-end-user.md)
* [<span data-ttu-id="b8ee6-133">Azure Multi-Factor Authenticaton en MSDN</span><span class="sxs-lookup"><span data-stu-id="b8ee6-133">Azure Multi-Factor Authentication on MSDN</span></span>](https://msdn.microsoft.com/library/azure/dn249471.aspx)
