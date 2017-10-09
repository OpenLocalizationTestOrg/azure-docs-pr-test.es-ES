---
title: "aaaManage tooAzure de acceso mediante roles de facturación | Documentos de Microsoft"
description: 
services: 
documentationcenter: 
author: vikramdesai01
manager: vikdesai
editor: 
tags: billing
ms.assetid: e4c4d136-2826-4938-868f-a7e67ff6b025
ms.service: billing
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/22/2017
ms.author: vikdesai
ms.openlocfilehash: 5937fac5ffa5ca204eb03a1dcbc5e800b3d5eb74
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="manage-access-toobilling-information-for-azure-using-role-based-access-control"></a><span data-ttu-id="dc4ec-102">Administrar la información de toobilling de acceso de Azure mediante control de acceso basado en roles</span><span class="sxs-lookup"><span data-stu-id="dc4ec-102">Manage access toobilling information for Azure using role-based access control</span></span>

<span data-ttu-id="dc4ec-103">Puede conceder acceso a Azure toomembers de información de facturación de su equipo mediante la asignación de uno de hello después de suscripción de tooyour de roles de usuario: cuenta de administrador, Administrador de servicios, Coadministrador, propietario, Colaborador, lector y lector de facturación.</span><span class="sxs-lookup"><span data-stu-id="dc4ec-103">You can grant access for Azure billing information toomembers of your team by assigning one of hello following user roles tooyour subscription: Account Administrator, Service Administrator, Co-administrator, Owner, Contributor, Reader, and Billing Reader.</span></span> <span data-ttu-id="dc4ec-104">Tendrían acceso toobilling información en hello [portal de Azure](https://portal.azure.com/), y pueden utilizar hello [API facturación](billing-usage-rate-card-overview.md) tooprogrammatically obtener facturas (una vez elegido-in) y obtener detalles de uso.</span><span class="sxs-lookup"><span data-stu-id="dc4ec-104">They would have access toobilling information in hello [Azure portal](https://portal.azure.com/), and they can use hello [Billing APIs](billing-usage-rate-card-overview.md) tooprogrammatically get invoices (once opted-in) and usage details.</span></span> <span data-ttu-id="dc4ec-105">Para más información sobre quién puede conceder roles y qué puede hacer cada rol, vea [Roles en Azure RBAC](../active-directory/role-based-access-built-in-roles.md).</span><span class="sxs-lookup"><span data-stu-id="dc4ec-105">For more information about who can grant roles, and which roles can do what, see [Roles in Azure RBAC](../active-directory/role-based-access-built-in-roles.md).</span></span>

## <span data-ttu-id="dc4ec-106"><a name="opt-in"></a>Permitir que otros usuarios tooaccess facturas</span><span class="sxs-lookup"><span data-stu-id="dc4ec-106"><a name="opt-in"></a> Allowing additional users tooaccess invoices</span></span>

<span data-ttu-id="dc4ec-107">Hello Administrador de la cuenta debe elegir utilizando hello [portal de Azure](https://portal.azure.com/) permitir acceso tooinvoices para otros usuarios y a través de API.</span><span class="sxs-lookup"><span data-stu-id="dc4ec-107">hello Account Administrator must opt in using hello [Azure portal](https://portal.azure.com/) allow access tooinvoices for other users and via API.</span></span>

1. <span data-ttu-id="dc4ec-108">Como administrador de la cuenta de hello, seleccione su suscripción de hello [hoja suscripciones](https://portal.azure.com/#blade/Microsoft_Azure_Billing/SubscriptionsBlade) en portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="dc4ec-108">As hello Account Administrator, select your subscription from hello [Subscriptions blade](https://portal.azure.com/#blade/Microsoft_Azure_Billing/SubscriptionsBlade) in Azure portal.</span></span>

1. <span data-ttu-id="dc4ec-109">Seleccione **facturas** y, a continuación, **acceso tooinvoices**.</span><span class="sxs-lookup"><span data-stu-id="dc4ec-109">Select **Invoices** and then **Access tooinvoices**.</span></span>

    ![Captura de pantalla muestra cómo acceder toodelegate a tooinvoices](./media/billing-manage-access/AA-optin.png)

1. <span data-ttu-id="dc4ec-111">Activar **en** acceso Hola seguido de guardar los cambios de hello, los usuarios de tooallow de suscripción roles con ámbito toodownload factura.</span><span class="sxs-lookup"><span data-stu-id="dc4ec-111">Turn **On** hello access followed by saving hello changes, tooallow users in subscription scoped roles toodownload invoice.</span></span>

    ![Captura de pantalla muestra toodelegate desactivar acceso tooinvoice](./media/billing-manage-access/AA-optinAllow.png)

<span data-ttu-id="dc4ec-113">La aceptación de permite el Administrador de servicios, Coadministrador, propietario, Colaborador, lector y lector de facturación en facturas de hello suscripción toodownload PDF en hello portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="dc4ec-113">Opting in allows Service Administrator, Co-administrator, Owner, Contributor, Reader, and Billing Reader on hello subscription toodownload PDF invoices in hello Azure portal.</span></span> <span data-ttu-id="dc4ec-114">Sin embargo, facturas anteriores a de 2016 diciembre son toohello única disponible Administrador de la cuenta por ahora.</span><span class="sxs-lookup"><span data-stu-id="dc4ec-114">However, invoices older than December 2016 are available only toohello Account Administrator for now.</span></span>

<span data-ttu-id="dc4ec-115">Hola, Administrador de la cuenta también puede configurar facturas toohave enviadas a través del correo electrónico.</span><span class="sxs-lookup"><span data-stu-id="dc4ec-115">hello Account Administrator can also configure toohave invoices sent via email.</span></span> <span data-ttu-id="dc4ec-116">más información, consulte toolearn [obtener la factura de correo electrónico](billing-download-azure-invoice-daily-usage-date.md).</span><span class="sxs-lookup"><span data-stu-id="dc4ec-116">toolearn more, see [Get your invoice in email](billing-download-azure-invoice-daily-usage-date.md).</span></span>

## <a name="adding-users-toohello-billing-reader-role"></a><span data-ttu-id="dc4ec-117">Agregar rol de lector de facturación de los usuarios toohello</span><span class="sxs-lookup"><span data-stu-id="dc4ec-117">Adding users toohello Billing Reader role</span></span>

<span data-ttu-id="dc4ec-118">rol de lector de facturación de Hello tiene información de facturación de toosubscription de acceso de solo lectura en el portal de Azure y no tooservices de acceso, como las máquinas virtuales y las cuentas de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="dc4ec-118">hello Billing Reader role has read-only access toosubscription billing information in Azure portal, and no access tooservices such as VMs and storage accounts.</span></span> <span data-ttu-id="dc4ec-119">Asignar toosomeone de rol de lector de facturación Hola que necesita tener acceso a información de facturación de suscripción toohello pero no Hola capacidad toomanage Azure servicios.</span><span class="sxs-lookup"><span data-stu-id="dc4ec-119">Assign hello Billing Reader role toosomeone that needs access toohello subscription billing information but not hello ability toomanage Azure services.</span></span> <span data-ttu-id="dc4ec-120">Este rol es adecuado para los usuarios de una organización que solo realizan la administración financiera y de costos para las suscripciones de Azure.</span><span class="sxs-lookup"><span data-stu-id="dc4ec-120">This role is appropriate for users in an organization who only perform financial and cost management for Azure subscriptions.</span></span>

1. <span data-ttu-id="dc4ec-121">Seleccione la suscripción de hello [hoja suscripciones](https://portal.azure.com/#blade/Microsoft_Azure_Billing/SubscriptionsBlade) en portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="dc4ec-121">Select your subscription from hello [Subscriptions blade](https://portal.azure.com/#blade/Microsoft_Azure_Billing/SubscriptionsBlade) in Azure portal.</span></span>

1. <span data-ttu-id="dc4ec-122">Seleccione **Control de acceso (IAM)** y haga clic en **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="dc4ec-122">Select **Access control (IAM)** and then click **Add**.</span></span>

    ![Captura de pantalla muestra IAM en la hoja de la suscripción de Hola](./media/billing-manage-access/select-iam.PNG)

1. <span data-ttu-id="dc4ec-124">Elija **facturación lector** en hello **seleccione un rol** página.</span><span class="sxs-lookup"><span data-stu-id="dc4ec-124">Choose **Billing Reader** in hello **Select a role** page.</span></span>

    ![Captura de pantalla muestra de facturación lector en la vista de la ventana emergente de Hola](./media/billing-manage-access/select-roles.PNG)

1. <span data-ttu-id="dc4ec-126">Escriba el correo electrónico de hello para el usuario de Hola que desee tooinvite, y después haga clic en **Aceptar** invitación de hello toosend.</span><span class="sxs-lookup"><span data-stu-id="dc4ec-126">Type hello email for hello user you want tooinvite, then click **OK** toosend hello invitation.</span></span>

    ![Captura de pantalla que muestra una persona tooenter tooinvite de correo electrónico](./media/billing-manage-access/add-user.PNG)

1. <span data-ttu-id="dc4ec-128">Siga las instrucciones en toolog de correo electrónico de invitación de hello en como un lector de facturación.</span><span class="sxs-lookup"><span data-stu-id="dc4ec-128">Follow instructions in hello invite email toolog in as a Billing Reader.</span></span>

    ![Captura de pantalla que muestra qué Hola lector de facturación puede ver en el portal de Azure](./media/billing-manage-access/billing-reader-view.png)

> [!NOTE]
> <span data-ttu-id="dc4ec-130">característica de lector de facturación de Hello está en vista previa y aún no admiten suscripciones de enterprise (EA) o nubes no globales.</span><span class="sxs-lookup"><span data-stu-id="dc4ec-130">hello Billing Reader feature is in preview, and does not yet support enterprise (EA) subscriptions or non-global clouds.</span></span>

## <a name="adding-users-tooother-roles"></a><span data-ttu-id="dc4ec-131">Agregar usuarios tooother roles</span><span class="sxs-lookup"><span data-stu-id="dc4ec-131">Adding users tooother roles</span></span>

<span data-ttu-id="dc4ec-132">Los usuarios de otros roles, como Propietario o Colaborador, pueden tener acceso no solo a la información de facturación, sino también a los servicios de Azure.</span><span class="sxs-lookup"><span data-stu-id="dc4ec-132">Users in other roles, such as Owner or Contributor, can access not just billing information, but Azure services as well.</span></span> <span data-ttu-id="dc4ec-133">estos roles, consulte el toomanage [agregar o cambiar roles de administrador de Azure que administran la suscripción de Hola o servicios](billing-add-change-azure-subscription-administrator.md).</span><span class="sxs-lookup"><span data-stu-id="dc4ec-133">toomanage these roles, see [Add or change Azure administrator roles that manage hello subscription or services](billing-add-change-azure-subscription-administrator.md).</span></span>

## <a name="who-can-access-hello-account-centerhttpsaccountwindowsazurecom"></a><span data-ttu-id="dc4ec-134">¿Quién puede acceder a hello [centro de cuentas de](https://account.windowsazure.com)?</span><span class="sxs-lookup"><span data-stu-id="dc4ec-134">Who can access hello [Account Center](https://account.windowsazure.com)?</span></span>

<span data-ttu-id="dc4ec-135">Hola sólo administrador de la cuenta puede iniciar sesión en el centro de cuentas de toohello.</span><span class="sxs-lookup"><span data-stu-id="dc4ec-135">Only hello Account Administrator can log in toohello Account center.</span></span> <span data-ttu-id="dc4ec-136">Hola, Administrador de la cuenta es propietario legal de Hola de suscripción de Hola.</span><span class="sxs-lookup"><span data-stu-id="dc4ec-136">hello Account Administrator is hello legal owner of hello subscription.</span></span> <span data-ttu-id="dc4ec-137">De forma predeterminada, Hola quien inscrito o comprado Hola suscripción de Azure es hello Administrador de cuenta, a menos que hello [propiedad de la suscripción se ha transferido](billing-subscription-transfer.md) toosomebody else.</span><span class="sxs-lookup"><span data-stu-id="dc4ec-137">By default, hello person who signed up for or bought hello Azure subscription is hello Account Administrator, unless hello [subscription ownership was transferred](billing-subscription-transfer.md) toosomebody else.</span></span> <span data-ttu-id="dc4ec-138">Hola, Administrador de la cuenta puede crear suscripciones, cancelar suscripciones, cambiar dirección de facturación de Hola para una suscripción y administrar las directivas de acceso para la suscripción de Hola.</span><span class="sxs-lookup"><span data-stu-id="dc4ec-138">hello Account Administrator can create subscriptions, cancel subscriptions, change hello billing address for a subscription, and manage access policies for hello subscription.</span></span>

## <a name="need-help-contact-support"></a><span data-ttu-id="dc4ec-139">¿Necesita ayuda?</span><span class="sxs-lookup"><span data-stu-id="dc4ec-139">Need help?</span></span> <span data-ttu-id="dc4ec-140">Póngase en contacto con el servicio de soporte técnico.</span><span class="sxs-lookup"><span data-stu-id="dc4ec-140">Contact support.</span></span>

<span data-ttu-id="dc4ec-141">Si tienes más preguntas, [póngase en contacto con soporte técnico](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) tooget rápidamente para solucionar el problema.</span><span class="sxs-lookup"><span data-stu-id="dc4ec-141">If you still have further questions, [contact support](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) tooget your issue resolved quickly.</span></span>
