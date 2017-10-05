---
title: "Revisión de acceso | Microsoft Docs"
description: "Después de iniciar una revisión de acceso en Privileged Identity Management de Azure AD, aprenda a realizarla y ver los resultados."
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
ms.openlocfilehash: ca2a1c7c287e4cf6b1b50cfb0068861b6f525596
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-complete-an-access-review-in-azure-ad-privileged-identity-management"></a><span data-ttu-id="e7848-103">Revisión de acceso en Privileged Identity Management de Azure AD</span><span class="sxs-lookup"><span data-stu-id="e7848-103">How to complete an access review in Azure AD Privileged Identity Management</span></span>
<span data-ttu-id="e7848-104">Los administradores de roles con privilegios pueden revisar el acceso con privilegios cuando se [ha iniciado una revisión de seguridad](active-directory-privileged-identity-management-how-to-start-security-review.md).</span><span class="sxs-lookup"><span data-stu-id="e7848-104">Privileged role administrators can review privileged access once a [security review has been started](active-directory-privileged-identity-management-how-to-start-security-review.md).</span></span> <span data-ttu-id="e7848-105">Privileged Identity Management (PIM) de Azure AD enviará automáticamente un correo electrónico para pedir a los usuarios que revisen su acceso.</span><span class="sxs-lookup"><span data-stu-id="e7848-105">Azure AD Privileged Identity Management (PIM) will automatically send an email prompting users to review their access.</span></span> <span data-ttu-id="e7848-106">Si un usuario no recibió un correo electrónico, puede enviarle las instrucciones que se indican en [Privileged Identity Management de Azure AD: Realización de una revisión de seguridad](active-directory-privileged-identity-management-how-to-perform-security-review.md).</span><span class="sxs-lookup"><span data-stu-id="e7848-106">If a user did not get an email, you can send them the instructions in [how to perform a security review](active-directory-privileged-identity-management-how-to-perform-security-review.md).</span></span>

<span data-ttu-id="e7848-107">Después de que acabe el período de revisión de seguridad o de que todos los usuarios hayan finalizado su autorrevisión, siga los pasos de este artículo para administrar la revisión y ver los resultados.</span><span class="sxs-lookup"><span data-stu-id="e7848-107">After the security review period is over, or all the users have finished their self-review, follow the steps in this article to manage the review and see the results.</span></span>

## <a name="manage-security-reviews"></a><span data-ttu-id="e7848-108">Administración de las revisiones de seguridad</span><span class="sxs-lookup"><span data-stu-id="e7848-108">Manage security reviews</span></span>
1. <span data-ttu-id="e7848-109">Vaya al [Portal de Azure](https://portal.azure.com/) y seleccione la aplicación **Azure AD Privileged Identity Management** en el panel.</span><span class="sxs-lookup"><span data-stu-id="e7848-109">Go to the [Azure portal](https://portal.azure.com/) and select the **Azure AD Privileged Identity Management** application on your dashboard.</span></span>
2. <span data-ttu-id="e7848-110">Seleccione la sección **Revisiones de acceso** del panel.</span><span class="sxs-lookup"><span data-stu-id="e7848-110">Select the **Access reviews** section of the dashboard.</span></span>
3. <span data-ttu-id="e7848-111">Seleccione la revisión de acceso que quiere administrar.</span><span class="sxs-lookup"><span data-stu-id="e7848-111">Select the access review that you want to manage.</span></span>

<span data-ttu-id="e7848-112">En la hoja de detalles de la revisión de acceso, hay un número de opciones para administrar dicha revisión.</span><span class="sxs-lookup"><span data-stu-id="e7848-112">On the access review's detail blade there are a number options for managing that review.</span></span>

![Botones de revisión de acceso de PIM: captura de pantalla][1]

### <a name="remind"></a><span data-ttu-id="e7848-114">Recuerde</span><span class="sxs-lookup"><span data-stu-id="e7848-114">Remind</span></span>
<span data-ttu-id="e7848-115">Si una revisión de acceso está configurada para que los usuarios revisen por sí mismos, el botón **Recordar** envía una notificación.</span><span class="sxs-lookup"><span data-stu-id="e7848-115">If an access review is set up so that the users review themselves, the **Remind** button sends out a notification.</span></span> 

### <a name="stop"></a><span data-ttu-id="e7848-116">Detención</span><span class="sxs-lookup"><span data-stu-id="e7848-116">Stop</span></span>
<span data-ttu-id="e7848-117">Todas las revisiones de acceso tienen una fecha de finalización, pero puede usar el botón **Detener** para terminarlas antes.</span><span class="sxs-lookup"><span data-stu-id="e7848-117">All access reviews have an end date, but you can use the **Stop** button to finish it early.</span></span> <span data-ttu-id="e7848-118">Si para entonces algunos de los usuarios no se han revisado, no podrán hacerlo una vez que se haya detenido la revisión.</span><span class="sxs-lookup"><span data-stu-id="e7848-118">If any users haven't been reviewed by this time, they won't be able to after you stop the review.</span></span> <span data-ttu-id="e7848-119">No se puede reiniciar una revisión después de que se ha detenido.</span><span class="sxs-lookup"><span data-stu-id="e7848-119">You cannot restart a review after it's been stopped.</span></span>

### <a name="apply"></a><span data-ttu-id="e7848-120">Aplicar</span><span class="sxs-lookup"><span data-stu-id="e7848-120">Apply</span></span>
<span data-ttu-id="e7848-121">Después de que finaliza una revisión de acceso, bien porque se ha llegado a la fecha de finalización o porque se ha detenido manualmente, el botón **Aplicar** implementa el resultado de la revisión.</span><span class="sxs-lookup"><span data-stu-id="e7848-121">After an access review is completed, either because you reached the end date or stopped it manually, the **Apply** button implements the outcome of the review.</span></span> <span data-ttu-id="e7848-122">Si se denegó el acceso de un usuario en la revisión, este es el paso que se quitará su asignación de rol.</span><span class="sxs-lookup"><span data-stu-id="e7848-122">If a user's access was denied in the review, this is the step that will remove their role assignment.</span></span>  

### <a name="export"></a><span data-ttu-id="e7848-123">Exportación</span><span class="sxs-lookup"><span data-stu-id="e7848-123">Export</span></span>
<span data-ttu-id="e7848-124">Si quiere aplicar los resultados de la revisión de seguridad manualmente, puede exportar la revisión.</span><span class="sxs-lookup"><span data-stu-id="e7848-124">If you want to apply the results of the security review manually, you can export the review.</span></span> <span data-ttu-id="e7848-125">El botón **Exportar** iniciará la descarga de un archivo CSV.</span><span class="sxs-lookup"><span data-stu-id="e7848-125">The **Export** button will start downloading a CSV file.</span></span> <span data-ttu-id="e7848-126">Puede administrar los resultados en Excel u otros programas que abran archivos CSV.</span><span class="sxs-lookup"><span data-stu-id="e7848-126">You can manage the results in Excel or other programs that open CSV files.</span></span>

### <a name="delete"></a><span data-ttu-id="e7848-127">Eliminar</span><span class="sxs-lookup"><span data-stu-id="e7848-127">Delete</span></span>
<span data-ttu-id="e7848-128">Si ya no le interesa más la revisión, elimínela.</span><span class="sxs-lookup"><span data-stu-id="e7848-128">If you are not interested in the review any further, delete it.</span></span> <span data-ttu-id="e7848-129">El botón **Eliminar** quita la revisión de la aplicación PIM.</span><span class="sxs-lookup"><span data-stu-id="e7848-129">The **Delete** button removes the review from the PIM application.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="e7848-130">No recibirá ninguna advertencia antes de la eliminación, así que asegúrese de que realmente quiere eliminar esa revisión.</span><span class="sxs-lookup"><span data-stu-id="e7848-130">You will not get a warning before deletion occurs, so be sure that you want to delete that review.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="e7848-131">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="e7848-131">Next steps</span></span>
[!INCLUDE [active-directory-privileged-identity-management-toc](../../includes/active-directory-privileged-identity-management-toc.md)]

<!--Image references-->

[1]: ./media/active-directory-privileged-identity-management-how-to-complete-review/PIM_review_buttons.png
