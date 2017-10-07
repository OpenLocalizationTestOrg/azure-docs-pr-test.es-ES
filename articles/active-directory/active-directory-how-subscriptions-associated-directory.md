---
title: "aaaHow Azure suscripciones están asociadas con Azure Active Directory | Documentos de Microsoft"
description: "Iniciar sesión en Azure tooMicrosoft y relacionados con problemas, como la relación de hello entre una suscripción de Azure y Azure Active Directory."
services: active-directory
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: bc4773c2-bc4a-4d21-9264-2267065f0aea
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 08/24/2017
ms.author: curtand
ms.reviewer: jeffsta
ms.custom: oldportal;it-pro;
ms.openlocfilehash: 4f831cfb972efec57083fcaa63adb43fde7b2faf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="how-azure-subscriptions-are-associated-with-azure-active-directory"></a><span data-ttu-id="8fc2c-103">Asociación de las suscripciones de Azure con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="8fc2c-103">How Azure subscriptions are associated with Azure Active Directory</span></span>
<span data-ttu-id="8fc2c-104">Este artículo contiene información acerca de la relación de hello entre una suscripción de Azure y Azure Active Directory (Azure AD) y cómo tooadd un directorio de Azure AD tooyour suscripción existente.</span><span class="sxs-lookup"><span data-stu-id="8fc2c-104">This article covers information about hello relationship between an Azure subscription and Azure Active Directory (Azure AD), and how tooadd an existing subscription tooyour Azure AD directory.</span></span>

## <a name="your-azure-subscriptions-relationship-tooazure-ad"></a><span data-ttu-id="8fc2c-105">TooAzure de relación de su suscripción a Azure AD</span><span class="sxs-lookup"><span data-stu-id="8fc2c-105">Your Azure subscription's relationship tooAzure AD</span></span>
<span data-ttu-id="8fc2c-106">Su suscripción de Azure tiene una relación de confianza con Azure AD, lo que significa que confía en los dispositivos, servicios y usuarios de hello directory tooauthenticate.</span><span class="sxs-lookup"><span data-stu-id="8fc2c-106">Your Azure subscription has a trust relationship with Azure AD, which means that it trusts hello directory tooauthenticate users, services, and devices.</span></span> <span data-ttu-id="8fc2c-107">Varias suscripciones pueden confiar Hola mismo directorio, pero cada suscripción confía en un único directorio.</span><span class="sxs-lookup"><span data-stu-id="8fc2c-107">Multiple subscriptions can trust hello same directory, but each subscription trusts only one directory.</span></span> 

<span data-ttu-id="8fc2c-108">relación de confianza de Hola que tiene una suscripción con un directorio es distinto de la relación de Hola que tiene con otros recursos de Azure (sitios Web, bases de datos y así sucesivamente).</span><span class="sxs-lookup"><span data-stu-id="8fc2c-108">hello trust relationship that a subscription has with a directory is unlike hello relationship that it has with other resources in Azure (websites, databases, and so on).</span></span> <span data-ttu-id="8fc2c-109">Si caduca una suscripción, tener acceso a toohello otros recursos asociados a la suscripción de hello también se detiene.</span><span class="sxs-lookup"><span data-stu-id="8fc2c-109">If a subscription expires, access toohello other resources associated with hello subscription also stops.</span></span> <span data-ttu-id="8fc2c-110">Pero sigue siendo un directorio de Azure AD en Azure, y puede asociar otra suscripción a ese directorio y administrar el directorio Hola usando Hola nueva suscripción.</span><span class="sxs-lookup"><span data-stu-id="8fc2c-110">But an Azure AD directory remains in Azure, and you can associate a different subscription with that directory and manage hello directory using hello new subscription.</span></span>

![Diagrama de asociación de suscripciones](./media/active-directory-how-subscriptions-associated-directory/WAAD_OrgAccountSubscription.png)

<span data-ttu-id="8fc2c-112">Todos los usuarios tienen un único directorio de inicio que los autentica, pero también pueden ser invitados en otros directorios.</span><span class="sxs-lookup"><span data-stu-id="8fc2c-112">All users have a single home directory that authenticates them, but they can also be guests in other directories.</span></span> <span data-ttu-id="8fc2c-113">En Azure AD, puede ver los directorios de Hola de que su cuenta de usuario es un miembro o invitado.</span><span class="sxs-lookup"><span data-stu-id="8fc2c-113">In Azure AD, you can see hello directories of which your user account is a member or guest.</span></span>

## <a name="azure-ad-and-cloud-service-subscriptions"></a><span data-ttu-id="8fc2c-114">Azure AD y suscripciones de servicios en la nube</span><span class="sxs-lookup"><span data-stu-id="8fc2c-114">Azure AD and cloud service subscriptions</span></span>
<span data-ttu-id="8fc2c-115">Azure AD proporciona identidad y directorio principal de hello capacidades de administración detrás de la mayoría de servicios de nube de Microsoft, incluidos:</span><span class="sxs-lookup"><span data-stu-id="8fc2c-115">Azure AD provides hello core directory and identity management capabilities behind most of Microsoft’s cloud services, including:</span></span>

* <span data-ttu-id="8fc2c-116">Azure</span><span class="sxs-lookup"><span data-stu-id="8fc2c-116">Azure</span></span>
* <span data-ttu-id="8fc2c-117">Microsoft Office 365</span><span class="sxs-lookup"><span data-stu-id="8fc2c-117">Microsoft Office 365</span></span>
* <span data-ttu-id="8fc2c-118">Microsoft Dynamics CRM Online</span><span class="sxs-lookup"><span data-stu-id="8fc2c-118">Microsoft Dynamics CRM Online</span></span>
* <span data-ttu-id="8fc2c-119">Microsoft Intune</span><span class="sxs-lookup"><span data-stu-id="8fc2c-119">Microsoft Intune</span></span>

<span data-ttu-id="8fc2c-120">Obtener Hola libre de servicio de Azure AD al suscribirse para cualquiera de estos servicios de nube de Microsoft.</span><span class="sxs-lookup"><span data-stu-id="8fc2c-120">You get hello Azure AD service free when you sign up for any of these Microsoft cloud services.</span></span> <span data-ttu-id="8fc2c-121">Si desea tooadd un directorio de suscripción de Azure adicionales tooan Azure AD, debe iniciar sesión con una cuenta de Microsoft.</span><span class="sxs-lookup"><span data-stu-id="8fc2c-121">If you want tooadd an additional Azure subscription tooan Azure AD directory, you must be signed in with a Microsoft account.</span></span> <span data-ttu-id="8fc2c-122">Si iniciar sesión en tooAzure con un trabajo o escuela cuenta, no se puede agregar un directorio existente de suscripción de Azure tooan porque no se puede autenticar su cuenta profesional o educativa directamente en Azure.</span><span class="sxs-lookup"><span data-stu-id="8fc2c-122">If you sign in tooAzure with a work or school account, you can't add an Azure subscription tooan existing directory because your work or school account can't be authenticated directly by Azure.</span></span> 

## <a name="tooadd-an-existing-subscription-tooyour-azure-ad-directory"></a><span data-ttu-id="8fc2c-123">tooadd un directorio de Azure AD tooyour suscripción existente</span><span class="sxs-lookup"><span data-stu-id="8fc2c-123">tooadd an existing subscription tooyour Azure AD directory</span></span>
<span data-ttu-id="8fc2c-124">Debe iniciar sesión con una cuenta que existe en ambas directorio actual Hola con qué hello suscripción está asociada y en el directorio de hello desea tooadd a.</span><span class="sxs-lookup"><span data-stu-id="8fc2c-124">You must sign in with an account that exists in both hello current directory with which hello subscription is associated and in hello directory you want tooadd it to.</span></span> 

1. <span data-ttu-id="8fc2c-125">Inicie sesión en toohello [centro de cuentas de Azure](https://account.windowsazure.com/Home/Index) con una cuenta que es Hola el Administrador de la cuenta de suscripción de hello cuya propiedad desea tootransfer.</span><span class="sxs-lookup"><span data-stu-id="8fc2c-125">Sign in toohello [Azure Account Center](https://account.windowsazure.com/Home/Index) with an account that is hello Account Administrator of hello subscription whose ownership you want tootransfer.</span></span>
2. <span data-ttu-id="8fc2c-126">Asegúrese de ese usuario Hola que quieran toobe propietario de la suscripción de Hola se encuentra en el directorio de Hola de destino.</span><span class="sxs-lookup"><span data-stu-id="8fc2c-126">Ensure that hello user who you want toobe hello subscription owner is in hello targeted directory.</span></span>
3. <span data-ttu-id="8fc2c-127">Haga clic en **Transferir suscripción**.</span><span class="sxs-lookup"><span data-stu-id="8fc2c-127">Click **Transfer subscription**.</span></span>
4. <span data-ttu-id="8fc2c-128">Especifica al destinatario de Hola.</span><span class="sxs-lookup"><span data-stu-id="8fc2c-128">Specify hello recipient.</span></span> <span data-ttu-id="8fc2c-129">destinatario de Hello recibe automáticamente un correo electrónico con un vínculo de aceptación.</span><span class="sxs-lookup"><span data-stu-id="8fc2c-129">hello recipient automatically gets an email with an acceptance link.</span></span>
5. <span data-ttu-id="8fc2c-130">destinatario de Hello hace clic en el vínculo de Hola y sigue las instrucciones de hello, incluidos introducir su información de pago.</span><span class="sxs-lookup"><span data-stu-id="8fc2c-130">hello recipient clicks hello link and follows hello instructions, including entering their payment information.</span></span> <span data-ttu-id="8fc2c-131">Cuando el destinatario de Hola se realiza correctamente, se transfiere suscripción Hola.</span><span class="sxs-lookup"><span data-stu-id="8fc2c-131">When hello recipient succeeds, hello subscription is transferred.</span></span> 
6. <span data-ttu-id="8fc2c-132">se cambia el directorio predeterminado de Hola de suscripción de hello toohello el directorio tiene ese usuario Hola.</span><span class="sxs-lookup"><span data-stu-id="8fc2c-132">hello default directory of hello subscription is changed toohello directory that hello user is in.</span></span>


## <a name="suggestions-toomanage-both-a-subscription-and-a-directory"></a><span data-ttu-id="8fc2c-133">Sugerencias toomanage ninguna suscripción y un directorio</span><span class="sxs-lookup"><span data-stu-id="8fc2c-133">Suggestions toomanage both a subscription and a directory</span></span>
<span data-ttu-id="8fc2c-134">roles administrativos de Hola para una suscripción de Azure administran recursos vinculados toohello suscripción de Azure.</span><span class="sxs-lookup"><span data-stu-id="8fc2c-134">hello administrative roles for an Azure subscription manage resources tied toohello Azure subscription.</span></span> <span data-ttu-id="8fc2c-135">En esta sección se explica las diferencias de hello entre administradores de suscripción de Azure y directorio de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="8fc2c-135">This section explains hello differences between Azure subscription admins and Azure AD directory admins.</span></span> <span data-ttu-id="8fc2c-136">Funciones administrativas y otras sugerencias para su uso toomanage su suscripción están cubiertos en [asignar roles de administrador en Azure Active Directory](active-directory-assign-admin-roles.md).</span><span class="sxs-lookup"><span data-stu-id="8fc2c-136">Administrative roles and other suggestions for using them toomanage your subscription are covered at [Assigning administrator roles in Azure Active Directory](active-directory-assign-admin-roles.md).</span></span>

<span data-ttu-id="8fc2c-137">De forma predeterminada, se asignan roles de administrador de servicios de hello al registrarse.</span><span class="sxs-lookup"><span data-stu-id="8fc2c-137">By default, you are assigned hello Service Administrator role when you sign up.</span></span> <span data-ttu-id="8fc2c-138">Si otros usuarios necesita toosign en y acceder a los servicios mediante Hola misma suscripción, puede agregarlas como coadministradores.</span><span class="sxs-lookup"><span data-stu-id="8fc2c-138">If others need toosign in and access services using hello same subscription, you can add them as co-administrators.</span></span> 

<span data-ttu-id="8fc2c-139">Azure AD tiene un conjunto diferente de directorio de hello toomanage funciones administrativas y las características relacionadas con la identidad.</span><span class="sxs-lookup"><span data-stu-id="8fc2c-139">Azure AD has a different set of administrative roles toomanage hello directory and identity-related features.</span></span> <span data-ttu-id="8fc2c-140">Por ejemplo, administrador global de Hola de un directorio puede agregar usuarios y directorios de toohello de grupos o requerir una autenticación multifactor para los usuarios.</span><span class="sxs-lookup"><span data-stu-id="8fc2c-140">For example, hello global administrator of a directory can add users and groups toohello directory, or require multifactor authentication for users.</span></span> <span data-ttu-id="8fc2c-141">Un usuario que crea un directorio se asigna el rol de administrador global de toohello y puede asignar roles administrativos tooother a los usuarios.</span><span class="sxs-lookup"><span data-stu-id="8fc2c-141">A user who creates a directory is assigned toohello global administrator role and they can assign administrative roles tooother users.</span></span> <span data-ttu-id="8fc2c-142">Otros servicios, como Office 365 y Microsoft Intune, también usan los roles administrativos de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="8fc2c-142">Azure AD administrative roles are also used by other services such as Office 365 and Microsoft Intune.</span></span> 

<span data-ttu-id="8fc2c-143">Los administradores de suscripciones de Azure y los administradores de directorios de Azure AD son dos roles diferentes.</span><span class="sxs-lookup"><span data-stu-id="8fc2c-143">Azure subscription admins and Azure AD directory admins are two separate roles.</span></span> 
* <span data-ttu-id="8fc2c-144">Los administradores de suscripciones de Azure pueden administrar recursos en Azure y pueden usar Azure AD en hello portal de Azure (porque Hola propio portal de Azure es un recurso de Azure).</span><span class="sxs-lookup"><span data-stu-id="8fc2c-144">Azure subscription admins can manage resources in Azure and can use Azure AD in hello Azure portal (because hello Azure portal itself is an Azure resource).</span></span> 
* <span data-ttu-id="8fc2c-145">Administradores de directorios pueden administrar las propiedades solo en el directorio de Azure AD Hola.</span><span class="sxs-lookup"><span data-stu-id="8fc2c-145">Directory admins can manage properties only in hello Azure AD directory.</span></span>

<span data-ttu-id="8fc2c-146">Una persona puede tener ambos roles, pero no es obligatorio.</span><span class="sxs-lookup"><span data-stu-id="8fc2c-146">A person can be in both roles but it isn’t required.</span></span> <span data-ttu-id="8fc2c-147">El administrador global de directorios puede no estar asignado como administrador de servicios o coadministrador de una suscripción de Azure, o viceversa.</span><span class="sxs-lookup"><span data-stu-id="8fc2c-147">A directory global administrator might not be assigned as service administrator or co-administrator of an Azure subscription, or vice versa.</span></span> <span data-ttu-id="8fc2c-148">No es un administrador de suscripción de hello, usuario de Hola puede iniciar sesión en toohello portal de Azure, pero no puede administrar los directorios de Hola para esa suscripción en el portal de Hola.</span><span class="sxs-lookup"><span data-stu-id="8fc2c-148">Without being an administrator of hello subscription, hello user can sign in toohello Azure portal, but can't manage hello directories for that subscription in hello portal.</span></span> <span data-ttu-id="8fc2c-149">Sin embargo, este usuario puede administrar los directorios con otras herramientas como PowerShell de Azure AD o hello centro de administración de Office 365.</span><span class="sxs-lookup"><span data-stu-id="8fc2c-149">However, this user can manage directories using other tools such as Azure AD PowerShell or hello Office 365 Admin Center.</span></span>

## <a name="next-steps"></a><span data-ttu-id="8fc2c-150">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="8fc2c-150">Next steps</span></span>
* <span data-ttu-id="8fc2c-151">toolearn Obtenga más información sobre cómo los administradores de toochange para una suscripción de Azure, consulte [transferir la propiedad de una cuenta de tooanother de suscripción de Azure](../billing/billing-subscription-transfer.md)</span><span class="sxs-lookup"><span data-stu-id="8fc2c-151">toolearn more about how toochange administrators for an Azure subscription, see [Transfer ownership of an Azure subscription tooanother account](../billing/billing-subscription-transfer.md)</span></span>
* <span data-ttu-id="8fc2c-152">toolearn más información acerca de cómo se controla el acceso a los recursos en Microsoft Azure, consulte [descripción de acceso a los recursos de Azure](active-directory-understanding-resource-access.md)</span><span class="sxs-lookup"><span data-stu-id="8fc2c-152">toolearn more about how resource access is controlled in Microsoft Azure, see [Understanding resource access in Azure](active-directory-understanding-resource-access.md)</span></span>
* <span data-ttu-id="8fc2c-153">Para obtener más información acerca de cómo las funciones de tooassign en Azure AD, consulte [asignar roles de administrador en Azure Active Directory](active-directory-assign-admin-roles-azure-portal.md)</span><span class="sxs-lookup"><span data-stu-id="8fc2c-153">For more information on how tooassign roles in Azure AD, see [Assigning administrator roles in Azure Active Directory](active-directory-assign-admin-roles-azure-portal.md)</span></span>

<!--Image references-->
[1]: ./media/active-directory-how-subscriptions-associated-directory/WAAD_PassThruAuth.png
[2]: ./media/active-directory-how-subscriptions-associated-directory/WAAD_OrgAccountSubscription.png
[3]: ./media/active-directory-how-subscriptions-associated-directory/WAAD_SignInDisambiguation.PNG