---
title: "Uso de un inquilino de Office 365 con una suscripción de Azure | Microsoft Docs"
description: "Aprenda cómo agregar un directorio de Office 365 (inquilino) a una suscripción de Azure."
services: 
documentationcenter: 
author: JiangChen79
manager: jlian
editor: 
tags: billing,top-support-issue
ms.assetid: cc9c57c6-7bfd-4dea-9027-c75ef3737589
ms.service: billing
ms.workload: na
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 06/13/2017
ms.author: cjiang
ms.openlocfilehash: 7affb4a83cdb8ababef60e786a3c824e7477ed68
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="associate-an-office-365-tenant-to-an-azure-subscription"></a><span data-ttu-id="beca4-103">Asociación de un inquilino de Office 365 a una suscripción de Azure</span><span class="sxs-lookup"><span data-stu-id="beca4-103">Associate an Office 365 tenant to an Azure subscription</span></span>
<span data-ttu-id="beca4-104">Vincule las suscripciones independientes de Azure y Office 365 para poder acceder al inquilino de Office 365 desde su suscripción de Azure.</span><span class="sxs-lookup"><span data-stu-id="beca4-104">Link your separate Azure and Office 365 subscriptions so that you can access the Office 365 tenant from your Azure subscription.</span></span> <span data-ttu-id="beca4-105">Para vincular sus suscripciones, inicie sesión en Azure con la cuenta de administrador de servicio de Azure, agregue un directorio y agregue las cuentas de organización de Office 365 al inquilino de Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="beca4-105">To link your subscriptions, sign in to Azure with the Azure service administrator account, add a directory, and add the Office 365 organizational accounts to the Azure Active Directory tenant.</span></span>

<span data-ttu-id="beca4-106">Si desea una suscripción de Office 365 para los usuarios de la instancia de Azure Active Directory o tiene una cuenta de Office 365, pero no una cuenta de Azure, consulte [Uso de una cuenta de Office 365 con la suscripción de Azure y viceversa](billing-use-existing-office-365-account-azure-subscription.md).</span><span class="sxs-lookup"><span data-stu-id="beca4-106">If you want an Office 365 subscription for users in your Azure Active Directory instance or you have an Office 365 account but not an Azure account, see [Sign up for Azure with Office 365 account](billing-use-existing-office-365-account-azure-subscription.md).</span></span> 

## <a name="before-you-begin"></a><span data-ttu-id="beca4-107">Antes de empezar</span><span class="sxs-lookup"><span data-stu-id="beca4-107">Before you begin</span></span>
* <span data-ttu-id="beca4-108">Necesita las credenciales de administrador de servicios de la suscripción de Azure.</span><span class="sxs-lookup"><span data-stu-id="beca4-108">You must have the credentials of the Azure subscription service administrator.</span></span> <span data-ttu-id="beca4-109">Las cuentas de coadministrador no pueden realizar algunos de los pasos de este artículo.</span><span class="sxs-lookup"><span data-stu-id="beca4-109">Co-administrator accounts can't do some of the steps in this article.</span></span> <span data-ttu-id="beca4-110">Para cambiar el administrador del servicio, consulte [Incorporación o cambio de roles de administrador de Azure](billing-add-change-azure-subscription-administrator.md#change-service-administrator-for-a-subscription).</span><span class="sxs-lookup"><span data-stu-id="beca4-110">To change your service administrator, see [How to add or change Azure administrator roles](billing-add-change-azure-subscription-administrator.md#change-service-administrator-for-a-subscription).</span></span>
* <span data-ttu-id="beca4-111">Debe tener las credenciales de administrador global del inquilino de Office 365.</span><span class="sxs-lookup"><span data-stu-id="beca4-111">You must have the credentials of a global administrator of the Office 365 tenant.</span></span>
* <span data-ttu-id="beca4-112">La dirección de correo electrónico del administrador de servicios no debe estar en el inquilino de Office 365.</span><span class="sxs-lookup"><span data-stu-id="beca4-112">The email address of the service administrator must not be in the Office 365 tenant.</span></span>
* <span data-ttu-id="beca4-113">La dirección de correo electrónico del administrador de servicios no debe coincidir con la de ningún administrador global del inquilino de Office 365.</span><span class="sxs-lookup"><span data-stu-id="beca4-113">The email address of the service administrator must not match that of any global administrator of the Office 365 tenant.</span></span>
* <span data-ttu-id="beca4-114">Si utiliza una dirección de correo electrónico que es una cuenta de Microsoft y una cuenta de organización, cambie temporalmente el administrador de servicios de su suscripción de Azure para que use otra cuenta de Microsoft.</span><span class="sxs-lookup"><span data-stu-id="beca4-114">If you use an email address that is both a Microsoft account and an organizational account, temporarily change the service administrator of your Azure subscription to use another Microsoft account.</span></span> <span data-ttu-id="beca4-115">Puede crear una cuenta de Microsoft en la [página de suscripción de una cuenta de Microsoft](https://signup.live.com/).</span><span class="sxs-lookup"><span data-stu-id="beca4-115">You can create a Microsoft account at the [Microsoft account signup page](https://signup.live.com/).</span></span>

## <a name="link-office-365-tenant-to-azure-subscription"></a><span data-ttu-id="beca4-116">Vinculación de un inquilino de Office 365 a una suscripción de Azure</span><span class="sxs-lookup"><span data-stu-id="beca4-116">Link Office 365 tenant to Azure subscription</span></span>
<span data-ttu-id="beca4-117">Para asociar el inquilino de Office 365 con la suscripción de Azure, siga estos pasos:</span><span class="sxs-lookup"><span data-stu-id="beca4-117">To associate the Office 365 tenant to the Azure subscription, follow these steps:</span></span>

### <a name="step-1-add-office-365-tenant-to-your-azure-subscription"></a><span data-ttu-id="beca4-118">Paso 1: agregue el inquilino de Office 365 a su suscripción de Azure.</span><span class="sxs-lookup"><span data-stu-id="beca4-118">Step 1: Add Office 365 tenant to your Azure subscription</span></span>

1. <span data-ttu-id="beca4-119">Inicie sesión en el [Portal de Azure clásico](https://manage.windowsazure.com/) con las credenciales de administrador de servicios.</span><span class="sxs-lookup"><span data-stu-id="beca4-119">Sign in to the [Azure classic portal](https://manage.windowsazure.com/) with the service administrator credentials.</span></span>

    ![Captura de pantalla de inicio de sesión en Azure](./media/billing-add-office-365-tenant-to-azure-subscription/s313_azure-sign-in-service-admin.png)

2. <span data-ttu-id="beca4-121">En el panel izquierdo, seleccione **ACTIVE DIRECTORY**.</span><span class="sxs-lookup"><span data-stu-id="beca4-121">In the left pane, select **ACTIVE DIRECTORY**.</span></span> <span data-ttu-id="beca4-122">No debería ver el inquilino de Office 365.</span><span class="sxs-lookup"><span data-stu-id="beca4-122">You shouldn't see the Office 365 tenant.</span></span> <span data-ttu-id="beca4-123">Si lo ve, vaya al [Paso 2: cambio del directorio asociado a la suscripción de Azure](#Step2).</span><span class="sxs-lookup"><span data-stu-id="beca4-123">If you see it, skip to [Step 2: Change the directory associated with the Azure subscription](#Step2).</span></span>
   
   ![Captura de pantalla de la entrada de Active Directory](./media/billing-add-office-365-tenant-to-azure-subscription/s35-classic-portal-active-directory-entry.png)

3. <span data-ttu-id="beca4-125">Seleccione **NUEVO** > **DIRECTORIO** > **CREACIÓN PERSONALIZADA**.</span><span class="sxs-lookup"><span data-stu-id="beca4-125">Select **NEW** > **DIRECTORY** > **CUSTOM CREATE**.</span></span>
   
    ![Captura de pantalla de la creación personalizada de Azure Active Directory](./media/billing-add-office-365-tenant-to-azure-subscription/s37-aad-custom-create.png)
   
4. <span data-ttu-id="beca4-127">En la página **Agregar directorio**, en **DIRECTORIO**, seleccione **Usar directorio existente**.</span><span class="sxs-lookup"><span data-stu-id="beca4-127">On the **Add directory** page, under **DIRECTORY**, select **Use existing directory**.</span></span> <span data-ttu-id="beca4-128">A continuación, seleccione **Estoy listo para cerrar la sesión ahora** y seleccione **Completar** ![complete-icon](./media/billing-add-office-365-tenant-to-azure-subscription/s38_complete-icon.png).</span><span class="sxs-lookup"><span data-stu-id="beca4-128">Then select **I am ready to be signed out now**, and select **Complete** ![complete-icon](./media/billing-add-office-365-tenant-to-azure-subscription/s38_complete-icon.png).</span></span>
   
    ![Captura de pantalla de "Usar directorio existente"](./media/billing-add-office-365-tenant-to-azure-subscription/s39_add-directory-use-existing.png)
   
5. <span data-ttu-id="beca4-130">Después de cerrar la sesión, inicie sesión con las credenciales de administrador global de su inquilino de Office 365.</span><span class="sxs-lookup"><span data-stu-id="beca4-130">After you are signed out, sign in with the global administrator’s credentials of your Office 365 tenant.</span></span>
   
    ![Captura de pantalla de inicio de sesión del administrador global de Office 365](./media/billing-add-office-365-tenant-to-azure-subscription/s310_sign-in-global-admin-office-365.png)
   
6. <span data-ttu-id="beca4-132">Seleccione **Continuar**.</span><span class="sxs-lookup"><span data-stu-id="beca4-132">Select **Continue**.</span></span>
   
    ![Captura de pantalla de comprobación](./media/billing-add-office-365-tenant-to-azure-subscription/s311_use-contoso-directory-azure-verify.png)
   
7. <span data-ttu-id="beca4-134">Seleccione **Cerrar sesión ahora**.</span><span class="sxs-lookup"><span data-stu-id="beca4-134">Select **Sign out now**.</span></span>
   
    ![Captura de pantalla del cierre de sesión](./media/billing-add-office-365-tenant-to-azure-subscription/s312_use-contoso-directory-azure-confirm-and-sign-out.png)
   
8. <span data-ttu-id="beca4-136">Inicie sesión en el [Portal de Azure clásico](https://manage.windowsazure.com/) con las credenciales de administrador de servicios.</span><span class="sxs-lookup"><span data-stu-id="beca4-136">Sign in to the [Azure classic portal](https://manage.windowsazure.com/) with the service administrator credentials.</span></span>
   
    ![Captura de pantalla de inicio de sesión en Azure](./media/billing-add-office-365-tenant-to-azure-subscription/s313_azure-sign-in-service-admin.png)
   
9. <span data-ttu-id="beca4-138">Debería ver el inquilino de Office 365 en el panel.</span><span class="sxs-lookup"><span data-stu-id="beca4-138">You should see your Office 365 tenant in the dashboard.</span></span>
   
    ![Captura de pantalla del panel](./media/billing-add-office-365-tenant-to-azure-subscription/s314_office-365-tenant-appear-in-azure.png)

### <span data-ttu-id="beca4-140"><a name="Step2"></a>Paso 2: cambio del directorio asociado a la suscripción de Azure.</span><span class="sxs-lookup"><span data-stu-id="beca4-140"><a name="Step2"></a>Step 2: Change the directory associated with the Azure subscription</span></span>
   
1. <span data-ttu-id="beca4-141">Seleccione **Configuración**.</span><span class="sxs-lookup"><span data-stu-id="beca4-141">Select **Settings**.</span></span>
   
    ![Captura de pantalla del icono de configuración del Portal de Azure clásico](./media/billing-add-office-365-tenant-to-azure-subscription/s315_azure-classic-portal-settings-icon.png)
   
2. <span data-ttu-id="beca4-143">Seleccione la suscripción de Azure y, después, **EDITAR DIRECTORIO**.</span><span class="sxs-lookup"><span data-stu-id="beca4-143">Select your Azure subscription, and then select **EDIT DIRECTORY**.</span></span>

    ![Captura de pantalla del directorio de edición de la suscripción de Azure](./media/billing-add-office-365-tenant-to-azure-subscription/s316_azure-subscription-edit-directory.png)
   
3. <span data-ttu-id="beca4-145">Seleccione **Siguiente** ![Siguiente icono](./media/billing-add-office-365-tenant-to-azure-subscription/s317_next-icon.png).</span><span class="sxs-lookup"><span data-stu-id="beca4-145">Select **Next** ![Next icon](./media/billing-add-office-365-tenant-to-azure-subscription/s317_next-icon.png).</span></span>
   
    ![Captura de pantalla de "Cambiar el directorio asociado"](./media/billing-add-office-365-tenant-to-azure-subscription/s318_azure-change-associated-directory.png)
   
4. <span data-ttu-id="beca4-147">Revise las cuentas afectadas.</span><span class="sxs-lookup"><span data-stu-id="beca4-147">Review the affected accounts.</span></span> <span data-ttu-id="beca4-148">Se eliminan todos los coadministradores y usuarios del [control de acceso basado en roles (RBAC)](../active-directory/role-based-access-control-configure.md) con acceso asignado en los grupos de recursos existentes.</span><span class="sxs-lookup"><span data-stu-id="beca4-148">All co-administrators and [Role-Based Access Control (RBAC)](../active-directory/role-based-access-control-configure.md) users with assigned access in the existing resource groups are removed.</span></span> <span data-ttu-id="beca4-149">La advertencia que recibe únicamente menciona la eliminación de los coadministradores.</span><span class="sxs-lookup"><span data-stu-id="beca4-149">The warning you receive only mentions the removal of co-administrators.</span></span>
      
    ![Captura de pantalla que muestra las cuentas de coadministrador que se eliminarán.](./media/billing-add-office-365-tenant-to-azure-subscription/s322_azure-confirm-directory-mapping.png)
   
    ![Captura de pantalla que muestra la cuenta de usuario de ejemplo que se eliminará.](./media/billing-add-office-365-tenant-to-azure-subscription/s325_assigned-users-removed-resource-groups.png)
   
5. <span data-ttu-id="beca4-152">Seleccione **Completar** ![complete-icon](./media/billing-add-office-365-tenant-to-azure-subscription/s38_complete-icon.png).</span><span class="sxs-lookup"><span data-stu-id="beca4-152">Select **Complete** ![complete-icon](./media/billing-add-office-365-tenant-to-azure-subscription/s38_complete-icon.png).</span></span>

### <a name="step-3-add-your-office-365-organizational-accounts-as-co-administrators-to-the-azure-active-directory-tenant"></a><span data-ttu-id="beca4-153">Paso 3: agregue sus cuentas de organización de Office 365 como coadministradores al inquilino de Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="beca4-153">Step 3: Add your Office 365 organizational accounts as co-administrators to the Azure Active Directory tenant</span></span>
   
1. <span data-ttu-id="beca4-154">Seleccione la pestaña **ADMINISTRADORES** y, a continuación, **AGREGAR**.</span><span class="sxs-lookup"><span data-stu-id="beca4-154">Select the **ADMINISTRATORS** tab, and then select **ADD**.</span></span>
   
    ![Captura de pantalla de la pestaña de administradores de la configuración del Portal de Azure clásico](./media/billing-add-office-365-tenant-to-azure-subscription/s319_azure-classic-portal-settings-administrators.png)
   
2. <span data-ttu-id="beca4-156">Escriba una cuenta de la organización de su inquilino de Office 365, seleccione la suscripción de Azure y, a continuación, seleccione **Completar** ![complete-icon](./media/billing-add-office-365-tenant-to-azure-subscription/s38_complete-icon.png).</span><span class="sxs-lookup"><span data-stu-id="beca4-156">Enter an organizational account of your Office 365 tenant, select the Azure subscription, and then select **Complete** ![complete-icon](./media/billing-add-office-365-tenant-to-azure-subscription/s38_complete-icon.png).</span></span>
   
    ![Captura de pantalla del cuadro de diálogo Agregar coadministrador de Azure](./media/billing-add-office-365-tenant-to-azure-subscription/s320_azure-add-co-administrator.png)
   
3. <span data-ttu-id="beca4-158">Vuelva a la pestaña **ADMINISTRADORES**.</span><span class="sxs-lookup"><span data-stu-id="beca4-158">Go back to the **ADMINISTRATORS** tab.</span></span> <span data-ttu-id="beca4-159">Debería ver la cuenta de la organización mostrada como coadministrador.</span><span class="sxs-lookup"><span data-stu-id="beca4-159">You should see the organizational account displayed as co-administrator.</span></span>
   
    ![Captura de pantalla de la pestaña Administradores](./media/billing-add-office-365-tenant-to-azure-subscription/s321_azure-co-administrator-added.png)
4.  <span data-ttu-id="beca4-161">Pruebe el acceso a Azure con la cuenta de coadministrador.</span><span class="sxs-lookup"><span data-stu-id="beca4-161">Test access to Azure with the co-administrator account.</span></span>
   
    <span data-ttu-id="beca4-162">a.</span><span class="sxs-lookup"><span data-stu-id="beca4-162">a.</span></span> <span data-ttu-id="beca4-163">Cierre sesión en el Portal de Azure clásico.</span><span class="sxs-lookup"><span data-stu-id="beca4-163">Sign out of the Azure classic portal.</span></span>
   
    <span data-ttu-id="beca4-164">b.</span><span class="sxs-lookup"><span data-stu-id="beca4-164">b.</span></span> <span data-ttu-id="beca4-165">Abra el [Portal de Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="beca4-165">Open the [Azure portal](https://portal.azure.com/).</span></span>
   
    <span data-ttu-id="beca4-166">c.</span><span class="sxs-lookup"><span data-stu-id="beca4-166">c.</span></span> <span data-ttu-id="beca4-167">Escriba las credenciales del coadministrador y, a continuación, seleccione **Iniciar sesión**.</span><span class="sxs-lookup"><span data-stu-id="beca4-167">Enter the credentials of the co-administrator, and then select **Sign in**.</span></span>
   
    ![Captura de pantalla de la página de inicio de sesión en Azure](./media/billing-add-office-365-tenant-to-azure-subscription/s324_azure-sign-in-with-co-admin.png)

## <a name="need-help-contact-support"></a><span data-ttu-id="beca4-169">¿Necesita ayuda?</span><span class="sxs-lookup"><span data-stu-id="beca4-169">Need help?</span></span> <span data-ttu-id="beca4-170">Póngase en contacto con el servicio de soporte técnico.</span><span class="sxs-lookup"><span data-stu-id="beca4-170">Contact support.</span></span>
<span data-ttu-id="beca4-171">Si sigue necesitando ayuda, [póngase en contacto con el servicio de soporte técnico](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) para resolver el problema rápidamente.</span><span class="sxs-lookup"><span data-stu-id="beca4-171">If you still need help, [contact support](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) to get your issue resolved quickly.</span></span>


