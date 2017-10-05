---
title: "Solución de errores de los paquetes de contenido de los registros de actividad de Azure Active Directory | Microsoft Docs"
description: Proporciona una lista de mensajes de error del paquete de contenido de la actividad de Azure Active Directory y los pasos para corregirlos.
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
editor: 
ms.assetid: ffce7eb1-99da-4ea7-9c4d-2322b755c8ce
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/15/2017
ms.author: markvi
ms.reviewer: dhanyahk
ms.openlocfilehash: c880e9eb6d48bd1e38075fbd867d3906ec67b547
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/03/2017
---
# <a name="troubleshooting-azure-active-directory-activity-logs-content-pack-errors"></a><span data-ttu-id="998ea-103">Solución de errores de los paquetes de contenido de los registros de actividad de Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="998ea-103">Troubleshooting Azure Active Directory Activity logs content pack errors</span></span> 


<span data-ttu-id="998ea-104">Cuando se trabaja con el paquete de contenido de Power BI para la versión preliminar de Azure Active Directory, es posible que se encuentre con los siguientes errores:</span><span class="sxs-lookup"><span data-stu-id="998ea-104">When working with the Power BI Content Pack for Azure Active Directory Preview, it is possible that you run into the following errors:</span></span> 

- [<span data-ttu-id="998ea-105">Error al actualizar</span><span class="sxs-lookup"><span data-stu-id="998ea-105">Refresh failed</span></span>](active-directory-reporting-troubleshoot-content-pack.md#refresh-failed) 
- [<span data-ttu-id="998ea-106">Error al actualizar las credenciales del origen de datos </span><span class="sxs-lookup"><span data-stu-id="998ea-106">Failed to update data source credentials</span></span>](active-directory-reporting-troubleshoot-content-pack.md#failed-to-update-data-source-credentials) 
- [<span data-ttu-id="998ea-107">La importación de datos tarda demasiado</span><span class="sxs-lookup"><span data-stu-id="998ea-107">Importing of data is taking too long</span></span>](active-directory-reporting-troubleshoot-content-pack.md#importing-of-data-is-taking-too-long) 
 
<span data-ttu-id="998ea-108">Este tema proporciona información sobre las posibles causas y cómo corregir estos errores.</span><span class="sxs-lookup"><span data-stu-id="998ea-108">This topic provides you with information about the possible causes and how to fix these errors.</span></span>
 
## <a name="refresh-failed"></a><span data-ttu-id="998ea-109">Error al actualizar</span><span class="sxs-lookup"><span data-stu-id="998ea-109">Refresh failed</span></span> 
 
<span data-ttu-id="998ea-110">**¿Cómo aparece este error**: correo electrónico desde Power BI o estado de error en el historial de actualización.</span><span class="sxs-lookup"><span data-stu-id="998ea-110">**How this error is surfaced**: Email from Power BI or failed status in the refresh history.</span></span> 


| <span data-ttu-id="998ea-111">Causa</span><span class="sxs-lookup"><span data-stu-id="998ea-111">Cause</span></span> | <span data-ttu-id="998ea-112">Solución</span><span class="sxs-lookup"><span data-stu-id="998ea-112">How to fix</span></span> |
| ---   | ---        |
| <span data-ttu-id="998ea-113">Los errores de actualización pueden producirse cuando se han restablecido las credenciales de los usuarios que se conectan al paquete de contenido, pero no se actualizan en la configuración de conexión del paquete de contenido.</span><span class="sxs-lookup"><span data-stu-id="998ea-113">Refresh failure errors can be caused when the credentials of the users connecting to the content pack have been reset but not updated in the connection settings of the of the content pack.</span></span> | <span data-ttu-id="998ea-114">En Power BI, busque el conjunto de datos correspondiente en el panel de registros de actividad de Azure Active Directory, elija programar la actualización y, a continuación, escriba sus credenciales de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="998ea-114">In Power BI, locate the dataset corresponding to the Azure Active Directory Activity logs dashboard (Azure Active Directory Activity logs), choose schedule refresh, and then enter your Azure AD credentials.</span></span> |
| <span data-ttu-id="998ea-115">Una actualización puede producir un error debido a problemas de datos en el paquete de contenido subyacente.</span><span class="sxs-lookup"><span data-stu-id="998ea-115">A refresh can fail due to data issues in the underlying content pack.</span></span> | <span data-ttu-id="998ea-116">Abra una incidencia de soporte técnico.</span><span class="sxs-lookup"><span data-stu-id="998ea-116">File a support ticket.</span></span> <span data-ttu-id="998ea-117">Para más detalles, consulte [Obtención de soporte técnico para Azure Active Directory](active-directory-troubleshooting-support-howto.md).</span><span class="sxs-lookup"><span data-stu-id="998ea-117">For more details, see [How to get support for Azure Active Directory](active-directory-troubleshooting-support-howto.md).</span></span>|
 
 
## <a name="failed-to-update-data-source-credentials"></a><span data-ttu-id="998ea-118">Error al actualizar las credenciales del origen de datos</span><span class="sxs-lookup"><span data-stu-id="998ea-118">Failed to update data source credentials</span></span> 
 
<span data-ttu-id="998ea-119">**¿Cómo aparece este error**: en Power BI, cuando se conecta al paquete de contenido de registros de actividad (versión preliminar) de Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="998ea-119">**How this error is surfaced**: In Power BI, when you are connecting to the Azure Active Directory Activity logs (preview) content pack.</span></span> 

| <span data-ttu-id="998ea-120">Causa</span><span class="sxs-lookup"><span data-stu-id="998ea-120">Cause</span></span> | <span data-ttu-id="998ea-121">Solución</span><span class="sxs-lookup"><span data-stu-id="998ea-121">How to fix</span></span> |
| ---   | ---        |
| <span data-ttu-id="998ea-122">El usuario que se conecta no es un administrador global, un lector de seguridad ni un administrador de seguridad.</span><span class="sxs-lookup"><span data-stu-id="998ea-122">The connecting user is neither a global admin nor a security reader or a security admin.</span></span> | <span data-ttu-id="998ea-123">Utilice una cuenta que sea administrador global, lector de seguridad o administrador de seguridad para tener acceso a los paquetes de contenido.</span><span class="sxs-lookup"><span data-stu-id="998ea-123">Use an account that is either a global admin or a security reader or a security admin to access the content packs.</span></span> |
| <span data-ttu-id="998ea-124">El inquilino no es Premium o no tiene al menos un usuario con un archivo de licencia Premium.</span><span class="sxs-lookup"><span data-stu-id="998ea-124">Your tenant is not a Premium tenant or doesn't have at least one user with Premium license File.</span></span> | <span data-ttu-id="998ea-125">Abra una incidencia de soporte técnico.</span><span class="sxs-lookup"><span data-stu-id="998ea-125">File a support ticket.</span></span> <span data-ttu-id="998ea-126">Para más detalles, consulte [Obtención de soporte técnico para Azure Active Directory](active-directory-troubleshooting-support-howto.md).</span><span class="sxs-lookup"><span data-stu-id="998ea-126">For more details, see [How to get support for Azure Active Directory](active-directory-troubleshooting-support-howto.md).</span></span>|
 

 

## <a name="importing-of-data-is-taking-too-long"></a><span data-ttu-id="998ea-127">La importación de datos tarda demasiado</span><span class="sxs-lookup"><span data-stu-id="998ea-127">Importing of data is taking too long</span></span> 
 
<span data-ttu-id="998ea-128">**¿Cómo aparece este error**: en Power BI, una vez que se ha conectado el paquete de contenido, el proceso de importación de datos comienza a preparar su panel para el registro de actividad de Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="998ea-128">**How this error is surfaced**: In Power BI, once you have connected your content pack, the data import process starts to prepare your dashboard for Azure Active Directory Activity log.</span></span> <span data-ttu-id="998ea-129">Verá el mensaje: "*Importando datos...* ”</span><span class="sxs-lookup"><span data-stu-id="998ea-129">You see the message: “*Importing data...*”</span></span>  

| <span data-ttu-id="998ea-130">Causa</span><span class="sxs-lookup"><span data-stu-id="998ea-130">Cause</span></span> | <span data-ttu-id="998ea-131">Solución</span><span class="sxs-lookup"><span data-stu-id="998ea-131">How to fix</span></span> |
| ---   | ---        |
| <span data-ttu-id="998ea-132">Según el tamaño de su inquilino, este paso puede tardar desde algunos minutos hasta media hora.</span><span class="sxs-lookup"><span data-stu-id="998ea-132">Depending on the size of your tenant, this step could take anywhere from a few mins to 30 minutes.</span></span> | <span data-ttu-id="998ea-133">Tenga paciencia.</span><span class="sxs-lookup"><span data-stu-id="998ea-133">Just be patient.</span></span> <span data-ttu-id="998ea-134">Si el mensaje no cambia para mostrar el panel dentro de una hora, registre una incidencia de soporte técnico.</span><span class="sxs-lookup"><span data-stu-id="998ea-134">If the message does not change to showing your dashboard within an hour, please file a support ticket.</span></span> <span data-ttu-id="998ea-135">Para más detalles, consulte [Obtención de soporte técnico para Azure Active Directory](active-directory-troubleshooting-support-howto.md).</span><span class="sxs-lookup"><span data-stu-id="998ea-135">For more details, see [How to get support for Azure Active Directory](active-directory-troubleshooting-support-howto.md).</span></span>|

## <a name="next-steps"></a><span data-ttu-id="998ea-136">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="998ea-136">Next steps</span></span>

<span data-ttu-id="998ea-137">Para instalar el paquete de contenido de Power BI para Azure Active Directory (versión preliminar), haga clic [aquí](https://powerbi.microsoft.com/en-us/blog/azure-active-directory-meets-power-bi/).</span><span class="sxs-lookup"><span data-stu-id="998ea-137">To install the Power BI Content Pack for Azure Active Directory Preview, click [here](https://powerbi.microsoft.com/en-us/blog/azure-active-directory-meets-power-bi/).</span></span>


