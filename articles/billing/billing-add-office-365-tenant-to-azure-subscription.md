---
title: "inquilino aaaUse Office 365 con una suscripción de Azure | Documentos de Microsoft"
description: "Obtenga información acerca de cómo tooadd Office 365 directorio (inquilino) tooan suscripción de Azure."
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
ms.openlocfilehash: e560370417bd074a7e37ceb7c60da45dbbbcf775
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="associate-an-office-365-tenant-tooan-azure-subscription"></a><span data-ttu-id="1b585-103">Asociar un tooan del inquilino de Office 365 suscripción de Azure</span><span class="sxs-lookup"><span data-stu-id="1b585-103">Associate an Office 365 tenant tooan Azure subscription</span></span>
<span data-ttu-id="1b585-104">Vincular las suscripciones de Azure y Office 365 independientes para que pueda acceder el inquilino de hello Office 365 de su suscripción de Azure.</span><span class="sxs-lookup"><span data-stu-id="1b585-104">Link your separate Azure and Office 365 subscriptions so that you can access hello Office 365 tenant from your Azure subscription.</span></span> <span data-ttu-id="1b585-105">toolink sus suscripciones, inicie sesión en tooAzure con hello cuenta de administrador del servicio de Azure, agregue un directorio y agregue el inquilino de Azure Active Directory de toohello de cuentas organizativas Hola Office 365.</span><span class="sxs-lookup"><span data-stu-id="1b585-105">toolink your subscriptions, sign in tooAzure with hello Azure service administrator account, add a directory, and add hello Office 365 organizational accounts toohello Azure Active Directory tenant.</span></span>

<span data-ttu-id="1b585-106">Si desea una suscripción de Office 365 para los usuarios de la instancia de Azure Active Directory o tiene una cuenta de Office 365, pero no una cuenta de Azure, consulte [Uso de una cuenta de Office 365 con la suscripción de Azure y viceversa](billing-use-existing-office-365-account-azure-subscription.md).</span><span class="sxs-lookup"><span data-stu-id="1b585-106">If you want an Office 365 subscription for users in your Azure Active Directory instance or you have an Office 365 account but not an Azure account, see [Sign up for Azure with Office 365 account](billing-use-existing-office-365-account-azure-subscription.md).</span></span> 

## <a name="before-you-begin"></a><span data-ttu-id="1b585-107">Antes de empezar</span><span class="sxs-lookup"><span data-stu-id="1b585-107">Before you begin</span></span>
* <span data-ttu-id="1b585-108">Debe tener credenciales de Hola de administrador de servicios de suscripción de Azure Hola.</span><span class="sxs-lookup"><span data-stu-id="1b585-108">You must have hello credentials of hello Azure subscription service administrator.</span></span> <span data-ttu-id="1b585-109">Las cuentas de administrador no pueden realizar algunos pasos de Hola de este artículo.</span><span class="sxs-lookup"><span data-stu-id="1b585-109">Co-administrator accounts can't do some of hello steps in this article.</span></span> <span data-ttu-id="1b585-110">toochange el administrador del servicio, consulte [cómo tooadd o cambiar roles de administrador de Azure](billing-add-change-azure-subscription-administrator.md#change-service-administrator-for-a-subscription).</span><span class="sxs-lookup"><span data-stu-id="1b585-110">toochange your service administrator, see [How tooadd or change Azure administrator roles](billing-add-change-azure-subscription-administrator.md#change-service-administrator-for-a-subscription).</span></span>
* <span data-ttu-id="1b585-111">Debe tener credenciales de Hola de administrador global del inquilino de Office 365 Hola.</span><span class="sxs-lookup"><span data-stu-id="1b585-111">You must have hello credentials of a global administrator of hello Office 365 tenant.</span></span>
* <span data-ttu-id="1b585-112">dirección de correo electrónico de Hola de administrador de servicios de hello no debe estar en el inquilino de Office 365 Hola.</span><span class="sxs-lookup"><span data-stu-id="1b585-112">hello email address of hello service administrator must not be in hello Office 365 tenant.</span></span>
* <span data-ttu-id="1b585-113">dirección de correo electrónico de Hola de administrador de servicios de hello no debe coincidir con cualquier administrador global del inquilino de hello Office 365.</span><span class="sxs-lookup"><span data-stu-id="1b585-113">hello email address of hello service administrator must not match that of any global administrator of hello Office 365 tenant.</span></span>
* <span data-ttu-id="1b585-114">Si utiliza una dirección de correo electrónico que es una cuenta de Microsoft y una cuenta profesional, cambiar temporalmente Hola Administrador de servicios de su suscripción de Azure toouse otra cuenta de Microsoft.</span><span class="sxs-lookup"><span data-stu-id="1b585-114">If you use an email address that is both a Microsoft account and an organizational account, temporarily change hello service administrator of your Azure subscription toouse another Microsoft account.</span></span> <span data-ttu-id="1b585-115">Puede crear una cuenta de Microsoft en hello [página de suscripción de cuenta de Microsoft](https://signup.live.com/).</span><span class="sxs-lookup"><span data-stu-id="1b585-115">You can create a Microsoft account at hello [Microsoft account signup page](https://signup.live.com/).</span></span>

## <a name="link-office-365-tenant-tooazure-subscription"></a><span data-ttu-id="1b585-116">Vincular la suscripción de tooAzure del inquilino de Office 365</span><span class="sxs-lookup"><span data-stu-id="1b585-116">Link Office 365 tenant tooAzure subscription</span></span>
<span data-ttu-id="1b585-117">tooassociate Hola Office 365 inquilino toohello suscripción de Azure, siga estos pasos:</span><span class="sxs-lookup"><span data-stu-id="1b585-117">tooassociate hello Office 365 tenant toohello Azure subscription, follow these steps:</span></span>

### <a name="step-1-add-office-365-tenant-tooyour-azure-subscription"></a><span data-ttu-id="1b585-118">Paso 1: Agregar Office 365 inquilino tooyour suscripción de Azure</span><span class="sxs-lookup"><span data-stu-id="1b585-118">Step 1: Add Office 365 tenant tooyour Azure subscription</span></span>

1. <span data-ttu-id="1b585-119">Inicie sesión en toohello [portal de Azure clásico](https://manage.windowsazure.com/) con credenciales de administrador de servicios de Hola.</span><span class="sxs-lookup"><span data-stu-id="1b585-119">Sign in toohello [Azure classic portal](https://manage.windowsazure.com/) with hello service administrator credentials.</span></span>

    ![Captura de pantalla de inicio de sesión en Azure](./media/billing-add-office-365-tenant-to-azure-subscription/s313_azure-sign-in-service-admin.png)

2. <span data-ttu-id="1b585-121">En el panel izquierdo de hello, seleccione **ACTIVE DIRECTORY**.</span><span class="sxs-lookup"><span data-stu-id="1b585-121">In hello left pane, select **ACTIVE DIRECTORY**.</span></span> <span data-ttu-id="1b585-122">No debería ver a inquilino Hola Office 365.</span><span class="sxs-lookup"><span data-stu-id="1b585-122">You shouldn't see hello Office 365 tenant.</span></span> <span data-ttu-id="1b585-123">Si lo ve, omitir demasiado[paso 2: cambie el directorio Hola asociado con suscripción de Azure hello](#Step2).</span><span class="sxs-lookup"><span data-stu-id="1b585-123">If you see it, skip too[Step 2: Change hello directory associated with hello Azure subscription](#Step2).</span></span>
   
   ![Captura de pantalla de la entrada de Active Directory](./media/billing-add-office-365-tenant-to-azure-subscription/s35-classic-portal-active-directory-entry.png)

3. <span data-ttu-id="1b585-125">Seleccione **NUEVO** > **DIRECTORIO** > **CREACIÓN PERSONALIZADA**.</span><span class="sxs-lookup"><span data-stu-id="1b585-125">Select **NEW** > **DIRECTORY** > **CUSTOM CREATE**.</span></span>
   
    ![Captura de pantalla de la creación personalizada de Azure Active Directory](./media/billing-add-office-365-tenant-to-azure-subscription/s37-aad-custom-create.png)
   
4. <span data-ttu-id="1b585-127">En hello **Agregar directorio** página, en **directorio**, seleccione **usar directorio existente**.</span><span class="sxs-lookup"><span data-stu-id="1b585-127">On hello **Add directory** page, under **DIRECTORY**, select **Use existing directory**.</span></span> <span data-ttu-id="1b585-128">A continuación, seleccione **estoy listo toobe cerrar la sesión ahora**y seleccione **completar** ![icono completar](./media/billing-add-office-365-tenant-to-azure-subscription/s38_complete-icon.png).</span><span class="sxs-lookup"><span data-stu-id="1b585-128">Then select **I am ready toobe signed out now**, and select **Complete** ![complete-icon](./media/billing-add-office-365-tenant-to-azure-subscription/s38_complete-icon.png).</span></span>
   
    ![Captura de pantalla de "Usar directorio existente"](./media/billing-add-office-365-tenant-to-azure-subscription/s39_add-directory-use-existing.png)
   
5. <span data-ttu-id="1b585-130">Una vez que cierre sesión, inicie sesión con credenciales de administrador global de Hola de su inquilino de Office 365.</span><span class="sxs-lookup"><span data-stu-id="1b585-130">After you are signed out, sign in with hello global administrator’s credentials of your Office 365 tenant.</span></span>
   
    ![Captura de pantalla de inicio de sesión del administrador global de Office 365](./media/billing-add-office-365-tenant-to-azure-subscription/s310_sign-in-global-admin-office-365.png)
   
6. <span data-ttu-id="1b585-132">Seleccione **Continuar**.</span><span class="sxs-lookup"><span data-stu-id="1b585-132">Select **Continue**.</span></span>
   
    ![Captura de pantalla de comprobación](./media/billing-add-office-365-tenant-to-azure-subscription/s311_use-contoso-directory-azure-verify.png)
   
7. <span data-ttu-id="1b585-134">Seleccione **Cerrar sesión ahora**.</span><span class="sxs-lookup"><span data-stu-id="1b585-134">Select **Sign out now**.</span></span>
   
    ![Captura de pantalla del cierre de sesión](./media/billing-add-office-365-tenant-to-azure-subscription/s312_use-contoso-directory-azure-confirm-and-sign-out.png)
   
8. <span data-ttu-id="1b585-136">Inicie sesión en toohello [portal de Azure clásico](https://manage.windowsazure.com/) con credenciales de administrador de servicios de Hola.</span><span class="sxs-lookup"><span data-stu-id="1b585-136">Sign in toohello [Azure classic portal](https://manage.windowsazure.com/) with hello service administrator credentials.</span></span>
   
    ![Captura de pantalla de inicio de sesión en Azure](./media/billing-add-office-365-tenant-to-azure-subscription/s313_azure-sign-in-service-admin.png)
   
9. <span data-ttu-id="1b585-138">Debería ver al inquilino de Office 365 en el panel de Hola.</span><span class="sxs-lookup"><span data-stu-id="1b585-138">You should see your Office 365 tenant in hello dashboard.</span></span>
   
    ![Captura de pantalla del panel](./media/billing-add-office-365-tenant-to-azure-subscription/s314_office-365-tenant-appear-in-azure.png)

### <span data-ttu-id="1b585-140"><a name="Step2"></a>Paso 2: Cambiar el directorio de hello asociado Hola suscripción de Azure</span><span class="sxs-lookup"><span data-stu-id="1b585-140"><a name="Step2"></a>Step 2: Change hello directory associated with hello Azure subscription</span></span>
   
1. <span data-ttu-id="1b585-141">Seleccione **Configuración**.</span><span class="sxs-lookup"><span data-stu-id="1b585-141">Select **Settings**.</span></span>
   
    ![Captura de pantalla del icono de configuración del Portal de Azure clásico](./media/billing-add-office-365-tenant-to-azure-subscription/s315_azure-classic-portal-settings-icon.png)
   
2. <span data-ttu-id="1b585-143">Seleccione la suscripción de Azure y, después, **EDITAR DIRECTORIO**.</span><span class="sxs-lookup"><span data-stu-id="1b585-143">Select your Azure subscription, and then select **EDIT DIRECTORY**.</span></span>

    ![Captura de pantalla del directorio de edición de la suscripción de Azure](./media/billing-add-office-365-tenant-to-azure-subscription/s316_azure-subscription-edit-directory.png)
   
3. <span data-ttu-id="1b585-145">Seleccione **Siguiente** ![Siguiente icono](./media/billing-add-office-365-tenant-to-azure-subscription/s317_next-icon.png).</span><span class="sxs-lookup"><span data-stu-id="1b585-145">Select **Next** ![Next icon](./media/billing-add-office-365-tenant-to-azure-subscription/s317_next-icon.png).</span></span>
   
    ![Captura de pantalla de "Cambio Hola asociados en el directorio"](./media/billing-add-office-365-tenant-to-azure-subscription/s318_azure-change-associated-directory.png)
   
4. <span data-ttu-id="1b585-147">Revise las cuentas de hello afectado.</span><span class="sxs-lookup"><span data-stu-id="1b585-147">Review hello affected accounts.</span></span> <span data-ttu-id="1b585-148">Todos los coadministradores y [Control de acceso basado en roles (RBAC)](../active-directory/role-based-access-control-configure.md) se quitan los usuarios con acceso asignado en grupos de recursos existentes de Hola.</span><span class="sxs-lookup"><span data-stu-id="1b585-148">All co-administrators and [Role-Based Access Control (RBAC)](../active-directory/role-based-access-control-configure.md) users with assigned access in hello existing resource groups are removed.</span></span> <span data-ttu-id="1b585-149">Advertencia de Hello que recibirá solo menciona eliminación Hola de coadministradores.</span><span class="sxs-lookup"><span data-stu-id="1b585-149">hello warning you receive only mentions hello removal of co-administrators.</span></span>
      
    ![Captura de pantalla que muestra hello cuentas de Coadministrador toobe quitado.](./media/billing-add-office-365-tenant-to-azure-subscription/s322_azure-confirm-directory-mapping.png)
   
    ![Captura de pantalla que muestra un toobe de cuenta de usuario en el ejemplo se quitan.](./media/billing-add-office-365-tenant-to-azure-subscription/s325_assigned-users-removed-resource-groups.png)
   
5. <span data-ttu-id="1b585-152">Seleccione **Completar** ![complete-icon](./media/billing-add-office-365-tenant-to-azure-subscription/s38_complete-icon.png).</span><span class="sxs-lookup"><span data-stu-id="1b585-152">Select **Complete** ![complete-icon](./media/billing-add-office-365-tenant-to-azure-subscription/s38_complete-icon.png).</span></span>

### <a name="step-3-add-your-office-365-organizational-accounts-as-co-administrators-toohello-azure-active-directory-tenant"></a><span data-ttu-id="1b585-153">Paso 3: Agregar las cuentas de organización de Office 365 como inquilino de Azure Active Directory toohello coadministradores</span><span class="sxs-lookup"><span data-stu-id="1b585-153">Step 3: Add your Office 365 organizational accounts as co-administrators toohello Azure Active Directory tenant</span></span>
   
1. <span data-ttu-id="1b585-154">Seleccione hello **administradores** pestaña y, a continuación, seleccione **agregar**.</span><span class="sxs-lookup"><span data-stu-id="1b585-154">Select hello **ADMINISTRATORS** tab, and then select **ADD**.</span></span>
   
    ![Captura de pantalla de la pestaña de administradores de la configuración del Portal de Azure clásico](./media/billing-add-office-365-tenant-to-azure-subscription/s319_azure-classic-portal-settings-administrators.png)
   
2. <span data-ttu-id="1b585-156">Especifique una cuenta organizativa de su inquilino de Office 365, seleccione Hola suscripción de Azure y, a continuación, seleccione **completar** ![icono completar](./media/billing-add-office-365-tenant-to-azure-subscription/s38_complete-icon.png).</span><span class="sxs-lookup"><span data-stu-id="1b585-156">Enter an organizational account of your Office 365 tenant, select hello Azure subscription, and then select **Complete** ![complete-icon](./media/billing-add-office-365-tenant-to-azure-subscription/s38_complete-icon.png).</span></span>
   
    ![Captura de pantalla del cuadro de diálogo Agregar coadministrador de Azure](./media/billing-add-office-365-tenant-to-azure-subscription/s320_azure-add-co-administrator.png)
   
3. <span data-ttu-id="1b585-158">Volver atrás toohello **administradores** ficha. Debería ver cuenta profesional hello muestra como Coadministrador.</span><span class="sxs-lookup"><span data-stu-id="1b585-158">Go back toohello **ADMINISTRATORS** tab. You should see hello organizational account displayed as co-administrator.</span></span>
   
    ![Captura de pantalla de la pestaña Administradores](./media/billing-add-office-365-tenant-to-azure-subscription/s321_azure-co-administrator-added.png)
4.  <span data-ttu-id="1b585-160">TooAzure de acceso de prueba con la cuenta de administrador de Hola.</span><span class="sxs-lookup"><span data-stu-id="1b585-160">Test access tooAzure with hello co-administrator account.</span></span>
   
    <span data-ttu-id="1b585-161">a.</span><span class="sxs-lookup"><span data-stu-id="1b585-161">a.</span></span> <span data-ttu-id="1b585-162">Cierre la sesión de hello portal de Azure clásico.</span><span class="sxs-lookup"><span data-stu-id="1b585-162">Sign out of hello Azure classic portal.</span></span>
   
    <span data-ttu-id="1b585-163">b.</span><span class="sxs-lookup"><span data-stu-id="1b585-163">b.</span></span> <span data-ttu-id="1b585-164">Abra hello [portal de Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="1b585-164">Open hello [Azure portal](https://portal.azure.com/).</span></span>
   
    <span data-ttu-id="1b585-165">c.</span><span class="sxs-lookup"><span data-stu-id="1b585-165">c.</span></span> <span data-ttu-id="1b585-166">Escriba las credenciales de Hola de Coadministrador de hello y, a continuación, seleccione **iniciar sesión en**.</span><span class="sxs-lookup"><span data-stu-id="1b585-166">Enter hello credentials of hello co-administrator, and then select **Sign in**.</span></span>
   
    ![Captura de pantalla de la página de inicio de sesión en Azure](./media/billing-add-office-365-tenant-to-azure-subscription/s324_azure-sign-in-with-co-admin.png)

## <a name="need-help-contact-support"></a><span data-ttu-id="1b585-168">¿Necesita ayuda?</span><span class="sxs-lookup"><span data-stu-id="1b585-168">Need help?</span></span> <span data-ttu-id="1b585-169">Póngase en contacto con el servicio de soporte técnico.</span><span class="sxs-lookup"><span data-stu-id="1b585-169">Contact support.</span></span>
<span data-ttu-id="1b585-170">Si aún necesita ayuda, [póngase en contacto con soporte técnico](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) tooget rápidamente para solucionar el problema.</span><span class="sxs-lookup"><span data-stu-id="1b585-170">If you still need help, [contact support](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) tooget your issue resolved quickly.</span></span>


