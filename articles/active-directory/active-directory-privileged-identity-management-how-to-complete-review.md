---
title: "aaaHow toocomplete una revisión de acceso | Documentos de Microsoft"
description: "Después de que ha iniciado una revisión de acceso en Azure AD Privileged Identity Management, obtenga información acerca de cómo toocomplete y ver resultados de Hola"
services: active-directory
documentationcenter: 
author: billmath
manager: femila
editor: 
ms.assetid: abc2d3dd-afd5-42cf-8a17-6c11f5674c35
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 06/06/2017
ms.author: kgremban
ms.custom: pim
ms.openlocfilehash: f99ddf3ebcf80b51110326064d584f33d8e1679a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="how-toocomplete-an-access-review-in-azure-ad-privileged-identity-management"></a><span data-ttu-id="6d432-103">¿Cómo toocomplete un acceso Revise en Azure AD Privileged Identity Management</span><span class="sxs-lookup"><span data-stu-id="6d432-103">How toocomplete an access review in Azure AD Privileged Identity Management</span></span>
<span data-ttu-id="6d432-104">Los administradores de roles con privilegios pueden revisar el acceso con privilegios cuando se [ha iniciado una revisión de seguridad](active-directory-privileged-identity-management-how-to-start-security-review.md).</span><span class="sxs-lookup"><span data-stu-id="6d432-104">Privileged role administrators can review privileged access once a [security review has been started](active-directory-privileged-identity-management-how-to-start-security-review.md).</span></span> <span data-ttu-id="6d432-105">Azure AD Privileged Identity Management (PIM) enviará automáticamente un correo electrónico preguntar a los usuarios tooreview su acceso.</span><span class="sxs-lookup"><span data-stu-id="6d432-105">Azure AD Privileged Identity Management (PIM) will automatically send an email prompting users tooreview their access.</span></span> <span data-ttu-id="6d432-106">Si un usuario no obtuvo un correo electrónico, se pueden enviar instrucciones de hello [cómo tooperform una revisión de seguridad](active-directory-privileged-identity-management-how-to-perform-security-review.md).</span><span class="sxs-lookup"><span data-stu-id="6d432-106">If a user did not get an email, you can send them hello instructions in [how tooperform a security review](active-directory-privileged-identity-management-how-to-perform-security-review.md).</span></span>

<span data-ttu-id="6d432-107">Después de período de revisión de seguridad de Hola o todos los usuarios de hello han terminado su revisar automáticamente, siga los pasos de hello en esta revisión del artículo toomanage hello y ver resultados de Hola.</span><span class="sxs-lookup"><span data-stu-id="6d432-107">After hello security review period is over, or all hello users have finished their self-review, follow hello steps in this article toomanage hello review and see hello results.</span></span>

## <a name="manage-security-reviews"></a><span data-ttu-id="6d432-108">Administración de las revisiones de seguridad</span><span class="sxs-lookup"><span data-stu-id="6d432-108">Manage security reviews</span></span>
1. <span data-ttu-id="6d432-109">Vaya toohello [portal de Azure](https://portal.azure.com/) y seleccione hello **Azure AD Privileged Identity Management** aplicación en el panel.</span><span class="sxs-lookup"><span data-stu-id="6d432-109">Go toohello [Azure portal](https://portal.azure.com/) and select hello **Azure AD Privileged Identity Management** application on your dashboard.</span></span>
2. <span data-ttu-id="6d432-110">Seleccione hello **acceder a las revisiones** sección del panel de Hola.</span><span class="sxs-lookup"><span data-stu-id="6d432-110">Select hello **Access reviews** section of hello dashboard.</span></span>
3. <span data-ttu-id="6d432-111">Seleccione la revisión de acceso de Hola que desea toomanage.</span><span class="sxs-lookup"><span data-stu-id="6d432-111">Select hello access review that you want toomanage.</span></span>

<span data-ttu-id="6d432-112">En la hoja de detalle de revisión de hello acceso hay un número opciones para administrar esa revisión.</span><span class="sxs-lookup"><span data-stu-id="6d432-112">On hello access review's detail blade there are a number options for managing that review.</span></span>

![Botones de revisión de acceso de PIM: captura de pantalla][1]

### <a name="remind"></a><span data-ttu-id="6d432-114">Recuerde</span><span class="sxs-lookup"><span data-stu-id="6d432-114">Remind</span></span>
<span data-ttu-id="6d432-115">Si una revisión de acceso está configurada para que los usuarios de hello revisar por sí mismos, Hola **avisar** botón envía una notificación.</span><span class="sxs-lookup"><span data-stu-id="6d432-115">If an access review is set up so that hello users review themselves, hello **Remind** button sends out a notification.</span></span> 

### <a name="stop"></a><span data-ttu-id="6d432-116">Detención</span><span class="sxs-lookup"><span data-stu-id="6d432-116">Stop</span></span>
<span data-ttu-id="6d432-117">Todas las revisiones de acceso tienen una fecha de finalización, pero puede usar hello **detener** botón toofinish cuanto antes.</span><span class="sxs-lookup"><span data-stu-id="6d432-117">All access reviews have an end date, but you can use hello **Stop** button toofinish it early.</span></span> <span data-ttu-id="6d432-118">Si los usuarios aún no ha revisado Llegados a este punto, no será capaz de tooafter detener revisión Hola.</span><span class="sxs-lookup"><span data-stu-id="6d432-118">If any users haven't been reviewed by this time, they won't be able tooafter you stop hello review.</span></span> <span data-ttu-id="6d432-119">No se puede reiniciar una revisión después de que se ha detenido.</span><span class="sxs-lookup"><span data-stu-id="6d432-119">You cannot restart a review after it's been stopped.</span></span>

### <a name="apply"></a><span data-ttu-id="6d432-120">Aplicar</span><span class="sxs-lookup"><span data-stu-id="6d432-120">Apply</span></span>
<span data-ttu-id="6d432-121">Una vez completada una revisión de acceso, ya sea porque se alcanza la fecha de finalización de Hola o se detuvo manualmente, Hola **aplicar** botón implementa el resultado de hello de revisión de Hola.</span><span class="sxs-lookup"><span data-stu-id="6d432-121">After an access review is completed, either because you reached hello end date or stopped it manually, hello **Apply** button implements hello outcome of hello review.</span></span> <span data-ttu-id="6d432-122">Si se denegó el acceso de un usuario en revisión hello, este es el paso de Hola que se quitará la asignación de rol.</span><span class="sxs-lookup"><span data-stu-id="6d432-122">If a user's access was denied in hello review, this is hello step that will remove their role assignment.</span></span>  

### <a name="export"></a><span data-ttu-id="6d432-123">Exportación</span><span class="sxs-lookup"><span data-stu-id="6d432-123">Export</span></span>
<span data-ttu-id="6d432-124">Si desea tooapply resultados de Hola Hola revisión de seguridad manualmente, puede exportar revisión Hola.</span><span class="sxs-lookup"><span data-stu-id="6d432-124">If you want tooapply hello results of hello security review manually, you can export hello review.</span></span> <span data-ttu-id="6d432-125">Hola **exportar** botón iniciará la descarga de un archivo CSV.</span><span class="sxs-lookup"><span data-stu-id="6d432-125">hello **Export** button will start downloading a CSV file.</span></span> <span data-ttu-id="6d432-126">Puede administrar los resultados de hello en Excel u otros programas que se abren los archivos CSV.</span><span class="sxs-lookup"><span data-stu-id="6d432-126">You can manage hello results in Excel or other programs that open CSV files.</span></span>

### <a name="delete"></a><span data-ttu-id="6d432-127">Eliminar</span><span class="sxs-lookup"><span data-stu-id="6d432-127">Delete</span></span>
<span data-ttu-id="6d432-128">Si no está interesado en hello revisar todas aún más, elimínelo.</span><span class="sxs-lookup"><span data-stu-id="6d432-128">If you are not interested in hello review any further, delete it.</span></span> <span data-ttu-id="6d432-129">Hola **eliminar** botón quita revisión Hola Hola aplicación PIM.</span><span class="sxs-lookup"><span data-stu-id="6d432-129">hello **Delete** button removes hello review from hello PIM application.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="6d432-130">No se recibe una advertencia antes de que se produce una eliminación, por tanto, asegúrese de que desea toodelete que revisar.</span><span class="sxs-lookup"><span data-stu-id="6d432-130">You will not get a warning before deletion occurs, so be sure that you want toodelete that review.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="6d432-131">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="6d432-131">Next steps</span></span>
[!INCLUDE [active-directory-privileged-identity-management-toc](../../includes/active-directory-privileged-identity-management-toc.md)]

<!--Image references-->

[1]: ./media/active-directory-privileged-identity-management-how-to-complete-review/PIM_review_buttons.png
