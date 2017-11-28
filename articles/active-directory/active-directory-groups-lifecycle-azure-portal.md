---
title: "aaaPreview Office 365 agrupa expiración en Azure Active Directory | Documentos de Microsoft"
description: "Cómo agrupa tooset la expiración para Office 365 en Azure Active Directory (versión preliminar)"
services: active-directory
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/09/2017
ms.author: curtand
ms.reviewer: kairaz.contractor
ms.custom: it-pro
ms.openlocfilehash: a8c99961cff3aad3f4d8b0cc1b2eb8e8a4c9ba95
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="configure-office-365-groups-expiration-preview"></a><span data-ttu-id="5b1bc-103">Configuración de la expiración de grupos de Office 365 (versión preliminar)</span><span class="sxs-lookup"><span data-stu-id="5b1bc-103">Configure Office 365 groups expiration (preview)</span></span>

<span data-ttu-id="5b1bc-104">Ahora puede administrar el ciclo de vida de Hola de grupos de Office 365 estableciendo la expiración de los grupos de Office 365 que seleccione.</span><span class="sxs-lookup"><span data-stu-id="5b1bc-104">You can now manage hello lifecycle of Office 365 groups by setting expiration for any Office 365 groups that you select.</span></span> <span data-ttu-id="5b1bc-105">Una vez establecida esta expiración, los propietarios de los grupos son más frecuentes toorenew sus grupos si es necesario grupos Hola.</span><span class="sxs-lookup"><span data-stu-id="5b1bc-105">Once this expiration is set, owners of those groups are asked toorenew their groups if they still need hello groups.</span></span> <span data-ttu-id="5b1bc-106">Los grupos de Office 365 que no se renueven se eliminarán.</span><span class="sxs-lookup"><span data-stu-id="5b1bc-106">Any Office 365 group that is not renewed will be deleted.</span></span> <span data-ttu-id="5b1bc-107">Cualquier grupo de Office 365 que se ha eliminado se puede restaurar durante los 30 días propietarios del grupo de Hola o un administrador de Hola.</span><span class="sxs-lookup"><span data-stu-id="5b1bc-107">Any Office 365 group that was deleted can be restored within 30 days by hello group owners or hello administrator.</span></span>  


> [!NOTE]
> <span data-ttu-id="5b1bc-108">Solo puede establecer la expiración de grupos de Office 365.</span><span class="sxs-lookup"><span data-stu-id="5b1bc-108">You can set expiration for only Office 365 groups.</span></span>
>
> <span data-ttu-id="5b1bc-109">El establecimiento de la expiración de grupos de O365 requiere que se asigne una licencia de Azure AD Premium a:</span><span class="sxs-lookup"><span data-stu-id="5b1bc-109">Setting expiration for O365 groups requires that an Azure AD Premium license is assigned to</span></span>
>   - <span data-ttu-id="5b1bc-110">Administrador de Hola que configura la configuración de inquilino de Hola Hola expiración</span><span class="sxs-lookup"><span data-stu-id="5b1bc-110">hello administrator who configures hello expiration settings for hello tenant</span></span>
>   - <span data-ttu-id="5b1bc-111">Todos los miembros de grupos de hello seleccionados para esta configuración</span><span class="sxs-lookup"><span data-stu-id="5b1bc-111">All members of hello groups selected for this setting</span></span>

## <a name="set-office-365-groups-expiration"></a><span data-ttu-id="5b1bc-112">Establecimiento de la expiración de grupos de Office 365</span><span class="sxs-lookup"><span data-stu-id="5b1bc-112">Set Office 365 groups expiration</span></span>

1. <span data-ttu-id="5b1bc-113">Abra hello [centro de administración de Azure AD](https://aad.portal.azure.com) con una cuenta que sea un administrador global de inquilino de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="5b1bc-113">Open hello [Azure AD admin center](https://aad.portal.azure.com) with an account that is a global administrator in your Azure AD tenant.</span></span>

2. <span data-ttu-id="5b1bc-114">Abra Azure AD y seleccione **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="5b1bc-114">Open Azure AD, select **Users and groups**.</span></span>

3. <span data-ttu-id="5b1bc-115">Seleccione **configuración de grupo** y, a continuación, seleccione **caducidad** tooopen configuración de la expiración de Hola.</span><span class="sxs-lookup"><span data-stu-id="5b1bc-115">Select **Group settings** and then select **Expiration** tooopen hello expiration settings.</span></span>
  
  ![Hoja Expiración](./media/active-directory-groups-lifecycle-azure-portal/expiration-settings.png)

4. <span data-ttu-id="5b1bc-117">En hello **caducidad** hoja, puede:</span><span class="sxs-lookup"><span data-stu-id="5b1bc-117">On hello **Expiration** blade, you can:</span></span>

  * <span data-ttu-id="5b1bc-118">Establecer la duración del grupo de hello en días.</span><span class="sxs-lookup"><span data-stu-id="5b1bc-118">Set hello group lifetime in days.</span></span> <span data-ttu-id="5b1bc-119">Puede seleccionar uno de hello preestablece valores o un valor personalizado (debe ser 31 días o más).</span><span class="sxs-lookup"><span data-stu-id="5b1bc-119">You could select one of hello preset values, or a custom value (should be 31 days or more).</span></span> 
  * <span data-ttu-id="5b1bc-120">Especifique una dirección de correo electrónico donde se deben enviar notificaciones de caducidad y renovación de hello cuando un grupo no tiene propietario.</span><span class="sxs-lookup"><span data-stu-id="5b1bc-120">Specify an email address where hello renewal and expiration notifications should be sent when a group has no owner.</span></span> 
  * <span data-ttu-id="5b1bc-121">Seleccionar los grupos de Office 365 que expiran.</span><span class="sxs-lookup"><span data-stu-id="5b1bc-121">Select which Office 365 groups expire.</span></span> <span data-ttu-id="5b1bc-122">Puede habilitar la expiración para **todos los** grupos de Office 365, puede seleccionar de entre los grupos de Office 365 Hola o seleccionar **ninguno** para deshabilitar la expiración de todos los grupos.</span><span class="sxs-lookup"><span data-stu-id="5b1bc-122">You can enable expiration for **All** Office 365 groups, you can select from among hello Office 365 groups, or you select **None** to disable expiration for all groups.</span></span>
  * <span data-ttu-id="5b1bc-123">Guardar la configuración cuando haya terminado seleccionando **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="5b1bc-123">Save your settings when you're done by selecting **Save**.</span></span>

<span data-ttu-id="5b1bc-124">Para obtener instrucciones sobre cómo toodownload e instalar Hola tooconfigure caducidad de módulo de PowerShell de Microsoft para los grupos de Office 365 a través de PowerShell, consulte [módulo Azure Active Directory V2 PowerShell - versión de vista previa pública 2.0.0.137](https://www.powershellgallery.com/packages/AzureADPreview/2.0.0.137).</span><span class="sxs-lookup"><span data-stu-id="5b1bc-124">For instructions on how toodownload and install hello Microsoft PowerShell module tooconfigure expiration for Office 365 groups via PowerShell, see [Azure Active Directory V2 PowerShell Module - Public Preview Release 2.0.0.137](https://www.powershellgallery.com/packages/AzureADPreview/2.0.0.137).</span></span>

<span data-ttu-id="5b1bc-125">Se envían notificaciones por correo electrónico como éste propietarios del grupo toohello Office 365 30 días, 15 días y tooexpiration anterior del día 1, del grupo de Hola.</span><span class="sxs-lookup"><span data-stu-id="5b1bc-125">Email notifications such as this one are sent toohello Office 365 group owners 30 days, 15 days, and 1 day prior tooexpiration of hello group.</span></span>

![Notificación por correo electrónico de expiración](./media/active-directory-groups-lifecycle-azure-portal/expiration-notification.png)

<span data-ttu-id="5b1bc-127">propietario del grupo de Hello, a continuación, puede seleccionar **grupo renovar** toorenew Hola grupo de Office 365, o puede seleccionar **vaya toogroup** toosee miembros de Hola y otros detalles acerca de Hola grupo.</span><span class="sxs-lookup"><span data-stu-id="5b1bc-127">hello group owner can then select **Renew group** toorenew hello Office 365 group, or can select **Go toogroup** toosee hello members and other details about hello group.</span></span>

<span data-ttu-id="5b1bc-128">Cuando expira un grupo, el grupo de Hola se elimina un día después de la fecha de expiración de Hola.</span><span class="sxs-lookup"><span data-stu-id="5b1bc-128">When a group expires, hello group is deleted one day after hello expiration date.</span></span> <span data-ttu-id="5b1bc-129">Se envía una notificación de correo electrónico como éste propietarios del grupo toohello Office 365 que les informa acerca de la expiración de Hola y eliminación posterior de su grupo de Office 365.</span><span class="sxs-lookup"><span data-stu-id="5b1bc-129">An email notification such as this one is sent toohello Office 365 group owners informing them about hello expiration and subsequent deletion of their Office 365 group.</span></span>

![Notificación por correo electrónico de eliminación del grupo](./media/active-directory-groups-lifecycle-azure-portal/deletion-notification.png)

<span data-ttu-id="5b1bc-131">grupo de Hello puede restaurarse seleccionando **restauración grupo** o mediante cmdlets de PowerShell, tal y como se describe en [grupo de restauración un eliminado Office 365 en Azure Active Directory] (https://docs.microsoft.com/azure/active-directory/ Active-Directory-Groups-restore-Azure-Portal).</span><span class="sxs-lookup"><span data-stu-id="5b1bc-131">hello group can be restored by selecting **Restore group** or by using PowerShell cmdlets, as described in [Restore a deleted Office 365 group in Azure Active Directory] (https://docs.microsoft.com/azure/active-directory/active-directory-groups-restore-azure-portal).</span></span>
    
<span data-ttu-id="5b1bc-132">Si va a restaurar el grupo de hello contiene documentos, los sitios de SharePoint u otros objetos persistentes, podría tardar hasta too24 horas toofully restauración Hola grupo y su contenido.</span><span class="sxs-lookup"><span data-stu-id="5b1bc-132">If hello group you're restoring contains documents, SharePoint sites, or other persistent objects, it might take up too24 hours toofully restore hello group and its contents.</span></span>

> [!NOTE]
> * <span data-ttu-id="5b1bc-133">Al implementar la configuración de la expiración de hello, podría haber algunos grupos que sean más antiguos que la ventana de expiración de hello.</span><span class="sxs-lookup"><span data-stu-id="5b1bc-133">When deploying hello expiration settings, there might be some groups that are older than hello expiration window.</span></span> <span data-ttu-id="5b1bc-134">Estos grupos no se eliminarán inmediatamente, pero son establecer too30 días hasta la expiración.</span><span class="sxs-lookup"><span data-stu-id="5b1bc-134">These groups are not be immediately deleted, but are set too30 days until expiration.</span></span> <span data-ttu-id="5b1bc-135">correo electrónico de notificación primer de renovación de Hola se envía dentro de un día.</span><span class="sxs-lookup"><span data-stu-id="5b1bc-135">hello first renewal notification email is sent out within a day.</span></span> <span data-ttu-id="5b1bc-136">Por ejemplo, un grupo se creó hace 400 días, y se establece el intervalo de expiración de hello too180 días.</span><span class="sxs-lookup"><span data-stu-id="5b1bc-136">For example, Group A was created 400 days ago, and hello expiration interval is set too180 days.</span></span> <span data-ttu-id="5b1bc-137">Cuando aplica la configuración de expiración, un grupo tiene 30 días antes de eliminarla, a menos que el propietario de Hola renueva.</span><span class="sxs-lookup"><span data-stu-id="5b1bc-137">When you apply expiration settings, Group A has 30 days before it is deleted, unless hello owner renews it.</span></span>
> * <span data-ttu-id="5b1bc-138">Cuando se elimina un grupo dinámico y se restaura, se ve como un nuevo grupo y vuelve a llenar regla toohello correspondiente.</span><span class="sxs-lookup"><span data-stu-id="5b1bc-138">When a dynamic group is deleted and restored, it is seen as a new group and re-populated according toohello rule.</span></span> <span data-ttu-id="5b1bc-139">Este proceso puede tardar horas too24.</span><span class="sxs-lookup"><span data-stu-id="5b1bc-139">This process might take up too24 hours.</span></span>

## <a name="next-steps"></a><span data-ttu-id="5b1bc-140">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="5b1bc-140">Next steps</span></span>
<span data-ttu-id="5b1bc-141">En estos artículos se proporciona información adicional sobre los grupos de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="5b1bc-141">These articles provide additional information on Azure AD groups.</span></span>

* [<span data-ttu-id="5b1bc-142">Consulta de los grupos existentes</span><span class="sxs-lookup"><span data-stu-id="5b1bc-142">See existing groups</span></span>](active-directory-groups-view-azure-portal.md)
* [<span data-ttu-id="5b1bc-143">Administración de la configuración de un grupo</span><span class="sxs-lookup"><span data-stu-id="5b1bc-143">Manage settings of a group</span></span>](active-directory-groups-settings-azure-portal.md)
* [<span data-ttu-id="5b1bc-144">Administrar miembros de un grupo</span><span class="sxs-lookup"><span data-stu-id="5b1bc-144">Manage members of a group</span></span>](active-directory-groups-members-azure-portal.md)
* [<span data-ttu-id="5b1bc-145">Administrar la pertenencia a grupos</span><span class="sxs-lookup"><span data-stu-id="5b1bc-145">Manage memberships of a group</span></span>](active-directory-groups-membership-azure-portal.md)
* [<span data-ttu-id="5b1bc-146">Administrar reglas dinámicas de los usuarios de un grupo</span><span class="sxs-lookup"><span data-stu-id="5b1bc-146">Manage dynamic rules for users in a group</span></span>](active-directory-groups-dynamic-membership-azure-portal.md)
