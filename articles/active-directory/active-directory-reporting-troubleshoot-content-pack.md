---
title: "Solución de errores de los paquetes de contenido de los registros de actividad de Azure Active Directory | Microsoft Docs"
description: Proporciona una lista de mensajes de error de hello actividad de Azure Active Directory content pack y pasos toofix ellos.
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
ms.openlocfilehash: 325de65ff1572a2f8f8319c0a52350bda03af3de
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting-azure-active-directory-activity-logs-content-pack-errors"></a><span data-ttu-id="d9f9a-103">Solución de errores de los paquetes de contenido de los registros de actividad de Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="d9f9a-103">Troubleshooting Azure Active Directory Activity logs content pack errors</span></span> 


<span data-ttu-id="d9f9a-104">Cuando se trabaja con hello paquete de contenido de Power BI para Azure Active Directory Preview, es posible que ejecute en hello siguientes errores:</span><span class="sxs-lookup"><span data-stu-id="d9f9a-104">When working with hello Power BI Content Pack for Azure Active Directory Preview, it is possible that you run into hello following errors:</span></span> 

- [<span data-ttu-id="d9f9a-105">Error al actualizar</span><span class="sxs-lookup"><span data-stu-id="d9f9a-105">Refresh failed</span></span>](active-directory-reporting-troubleshoot-content-pack.md#refresh-failed) 
- [<span data-ttu-id="d9f9a-106">Credenciales del origen de datos de errores tooupdate</span><span class="sxs-lookup"><span data-stu-id="d9f9a-106">Failed tooupdate data source credentials</span></span>](active-directory-reporting-troubleshoot-content-pack.md#failed-to-update-data-source-credentials) 
- [<span data-ttu-id="d9f9a-107">La importación de datos tarda demasiado</span><span class="sxs-lookup"><span data-stu-id="d9f9a-107">Importing of data is taking too long</span></span>](active-directory-reporting-troubleshoot-content-pack.md#importing-of-data-is-taking-too-long) 
 
<span data-ttu-id="d9f9a-108">Este tema proporciona información acerca de posibles causas de Hola y cómo toofix estos errores.</span><span class="sxs-lookup"><span data-stu-id="d9f9a-108">This topic provides you with information about hello possible causes and how toofix these errors.</span></span>
 
## <a name="refresh-failed"></a><span data-ttu-id="d9f9a-109">Error al actualizar</span><span class="sxs-lookup"><span data-stu-id="d9f9a-109">Refresh failed</span></span> 
 
<span data-ttu-id="d9f9a-110">**¿Cómo aparece este error**: correo electrónico desde Power BI o estado de error en el historial de actualización de Hola.</span><span class="sxs-lookup"><span data-stu-id="d9f9a-110">**How this error is surfaced**: Email from Power BI or failed status in hello refresh history.</span></span> 


| <span data-ttu-id="d9f9a-111">Causa</span><span class="sxs-lookup"><span data-stu-id="d9f9a-111">Cause</span></span> | <span data-ttu-id="d9f9a-112">Cómo toofix</span><span class="sxs-lookup"><span data-stu-id="d9f9a-112">How toofix</span></span> |
| ---   | ---        |
| <span data-ttu-id="d9f9a-113">Actualizar errores pueden deberse al credenciales de Hola de los usuarios de hello conectar el paquete de contenido de toohello restablecer aún no se actualizan en configuración de conexión de Hola Hola de paquete de contenido de Hola de error.</span><span class="sxs-lookup"><span data-stu-id="d9f9a-113">Refresh failure errors can be caused when hello credentials of hello users connecting toohello content pack have been reset but not updated in hello connection settings of hello of hello content pack.</span></span> | <span data-ttu-id="d9f9a-114">En Power BI, busque Hola de conjunto de datos correspondiente toohello panel de registros de actividad de Azure Active Directory (registros de actividad de Azure Active Directory), elegir programar la actualización y, a continuación, escriba sus credenciales de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="d9f9a-114">In Power BI, locate hello dataset corresponding toohello Azure Active Directory Activity logs dashboard (Azure Active Directory Activity logs), choose schedule refresh, and then enter your Azure AD credentials.</span></span> |
| <span data-ttu-id="d9f9a-115">Una actualización puede producir un error debido a problemas de toodata Hola subyacente paquete de contenido.</span><span class="sxs-lookup"><span data-stu-id="d9f9a-115">A refresh can fail due toodata issues in hello underlying content pack.</span></span> | <span data-ttu-id="d9f9a-116">Abra una incidencia de soporte técnico.</span><span class="sxs-lookup"><span data-stu-id="d9f9a-116">File a support ticket.</span></span> <span data-ttu-id="d9f9a-117">Para obtener más información, consulte [cómo son compatibles con tooget para Azure Active Directory](active-directory-troubleshooting-support-howto.md).</span><span class="sxs-lookup"><span data-stu-id="d9f9a-117">For more details, see [How tooget support for Azure Active Directory](active-directory-troubleshooting-support-howto.md).</span></span>|
 
 
## <a name="failed-tooupdate-data-source-credentials"></a><span data-ttu-id="d9f9a-118">Credenciales del origen de datos de errores tooupdate</span><span class="sxs-lookup"><span data-stu-id="d9f9a-118">Failed tooupdate data source credentials</span></span> 
 
<span data-ttu-id="d9f9a-119">**¿Cómo aparece este error**: en Power BI, cuando se conectan toohello paquete de contenido de registros (vista previa) de actividad de Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="d9f9a-119">**How this error is surfaced**: In Power BI, when you are connecting toohello Azure Active Directory Activity logs (preview) content pack.</span></span> 

| <span data-ttu-id="d9f9a-120">Causa</span><span class="sxs-lookup"><span data-stu-id="d9f9a-120">Cause</span></span> | <span data-ttu-id="d9f9a-121">Cómo toofix</span><span class="sxs-lookup"><span data-stu-id="d9f9a-121">How toofix</span></span> |
| ---   | ---        |
| <span data-ttu-id="d9f9a-122">usuario que se conecta Hello es ni un administrador global ni un lector de seguridad o un administrador de seguridad.</span><span class="sxs-lookup"><span data-stu-id="d9f9a-122">hello connecting user is neither a global admin nor a security reader or a security admin.</span></span> | <span data-ttu-id="d9f9a-123">Utilice una cuenta que sea un administrador global o un lector de seguridad o una seguridad admin tooaccess Hola los paquetes de contenido.</span><span class="sxs-lookup"><span data-stu-id="d9f9a-123">Use an account that is either a global admin or a security reader or a security admin tooaccess hello content packs.</span></span> |
| <span data-ttu-id="d9f9a-124">El inquilino no es Premium o no tiene al menos un usuario con un archivo de licencia Premium.</span><span class="sxs-lookup"><span data-stu-id="d9f9a-124">Your tenant is not a Premium tenant or doesn't have at least one user with Premium license File.</span></span> | <span data-ttu-id="d9f9a-125">Abra una incidencia de soporte técnico.</span><span class="sxs-lookup"><span data-stu-id="d9f9a-125">File a support ticket.</span></span> <span data-ttu-id="d9f9a-126">Para obtener más información, consulte [cómo son compatibles con tooget para Azure Active Directory](active-directory-troubleshooting-support-howto.md).</span><span class="sxs-lookup"><span data-stu-id="d9f9a-126">For more details, see [How tooget support for Azure Active Directory](active-directory-troubleshooting-support-howto.md).</span></span>|
 

 

## <a name="importing-of-data-is-taking-too-long"></a><span data-ttu-id="d9f9a-127">La importación de datos tarda demasiado</span><span class="sxs-lookup"><span data-stu-id="d9f9a-127">Importing of data is taking too long</span></span> 
 
<span data-ttu-id="d9f9a-128">**¿Cómo aparece este error**: en Power BI, una vez que se ha conectado el paquete de contenido, proceso de importación de datos de hello inicia tooprepare el panel de registro de actividad de Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="d9f9a-128">**How this error is surfaced**: In Power BI, once you have connected your content pack, hello data import process starts tooprepare your dashboard for Azure Active Directory Activity log.</span></span> <span data-ttu-id="d9f9a-129">Verá un mensaje de bienvenida: "*importar datos...* "</span><span class="sxs-lookup"><span data-stu-id="d9f9a-129">You see hello message: “*Importing data...*”</span></span>  

| <span data-ttu-id="d9f9a-130">Causa</span><span class="sxs-lookup"><span data-stu-id="d9f9a-130">Cause</span></span> | <span data-ttu-id="d9f9a-131">Cómo toofix</span><span class="sxs-lookup"><span data-stu-id="d9f9a-131">How toofix</span></span> |
| ---   | ---        |
| <span data-ttu-id="d9f9a-132">Función tamaño Hola de su inquilino, este paso podría tardar entre unos minutos too30 minutos.</span><span class="sxs-lookup"><span data-stu-id="d9f9a-132">Depending on hello size of your tenant, this step could take anywhere from a few mins too30 minutes.</span></span> | <span data-ttu-id="d9f9a-133">Tenga paciencia.</span><span class="sxs-lookup"><span data-stu-id="d9f9a-133">Just be patient.</span></span> <span data-ttu-id="d9f9a-134">Si mensaje hello no cambia tooshowing panel dentro de una hora, registre una incidencia de soporte técnico.</span><span class="sxs-lookup"><span data-stu-id="d9f9a-134">If hello message does not change tooshowing your dashboard within an hour, please file a support ticket.</span></span> <span data-ttu-id="d9f9a-135">Para obtener más información, consulte [cómo son compatibles con tooget para Azure Active Directory](active-directory-troubleshooting-support-howto.md).</span><span class="sxs-lookup"><span data-stu-id="d9f9a-135">For more details, see [How tooget support for Azure Active Directory](active-directory-troubleshooting-support-howto.md).</span></span>|

## <a name="next-steps"></a><span data-ttu-id="d9f9a-136">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="d9f9a-136">Next steps</span></span>

<span data-ttu-id="d9f9a-137">Hola tooinstall paquete de contenido de Power BI para Azure Active Directory vista previa, haga clic en [aquí](https://powerbi.microsoft.com/en-us/blog/azure-active-directory-meets-power-bi/).</span><span class="sxs-lookup"><span data-stu-id="d9f9a-137">tooinstall hello Power BI Content Pack for Azure Active Directory Preview, click [here](https://powerbi.microsoft.com/en-us/blog/azure-active-directory-meets-power-bi/).</span></span>


