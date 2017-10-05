---
title: P+F de Azure Active Directory | Microsoft Docs
description: "Preguntas más frecuentes de Azure Active Directory respuestas a preguntas relativas al acceso a Azure y a Azure Active Directory, administración de contraseñas y acceso a aplicaciones."
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
editor: 
ms.assetid: b8207760-9714-4871-93d5-f9893de31c8f
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 08/16/2017
ms.author: markvi
ms.openlocfilehash: 8d4460b3059558de2253c6f6a2d2fc8e7564d6d9
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/18/2017
---
# <a name="azure-active-directory-faq"></a><span data-ttu-id="17d27-103">P+F de Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="17d27-103">Azure Active Directory FAQ</span></span>
<span data-ttu-id="17d27-104">Azure Active Directory (Azure AD) es una completa solución de identidad como servicio (IDaaS) que abarca todos los aspectos de la identidad, la administración de acceso y la seguridad.</span><span class="sxs-lookup"><span data-stu-id="17d27-104">Azure Active Directory (Azure AD) is a comprehensive identity as a service (IDaaS) solution that spans all aspects of identity, access management, and security.</span></span>

<span data-ttu-id="17d27-105">Para más información, consulte [¿Qué es Azure Active Directory?](active-directory-whatis.md)</span><span class="sxs-lookup"><span data-stu-id="17d27-105">For more information, see [What is Azure Active Directory?](active-directory-whatis.md).</span></span>


## <a name="access-azure-and-azure-active-directory"></a><span data-ttu-id="17d27-106">Acceso a Azure y a Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="17d27-106">Access Azure and Azure Active Directory</span></span>
<span data-ttu-id="17d27-107">**P: ¿Por qué veo "No se encontraron suscripciones" cuando intento acceder a Azure AD en el Portal de Azure clásico?**</span><span class="sxs-lookup"><span data-stu-id="17d27-107">**Q: Why do I get “No subscriptions found” when I try to access Azure AD in the Azure classic portal?**</span></span>

<span data-ttu-id="17d27-108">**R:** Para acceder al Portal de Azure clásico, los usuarios necesitan permiso con una suscripción de Azure.</span><span class="sxs-lookup"><span data-stu-id="17d27-108">**A:** To access the Azure classic portal, each user needs permissions with an Azure subscription.</span></span> <span data-ttu-id="17d27-109">Si tiene una suscripción de pago a Office 365 o Azure AD, vaya a [http://aka.ms/accessAAD](http://aka.ms/accessAAD) para la activación por única vez.</span><span class="sxs-lookup"><span data-stu-id="17d27-109">If you have a paid Office 365 or Azure AD subscription, go to [http://aka.ms/accessAAD](http://aka.ms/accessAAD) for a one-time activation step.</span></span> <span data-ttu-id="17d27-110">En caso contrario, deberá activar una [cuenta de Azure](https://azure.microsoft.com/pricing/free-trial/) gratis o una suscripción de pago.</span><span class="sxs-lookup"><span data-stu-id="17d27-110">Otherwise, you will need to activate a free [Azure account](https://azure.microsoft.com/pricing/free-trial/) or a paid subscription.</span></span>

<span data-ttu-id="17d27-111">Para más información, consulte:</span><span class="sxs-lookup"><span data-stu-id="17d27-111">For more information, see:</span></span>

* [<span data-ttu-id="17d27-112">Asociación de las suscripciones de Azure con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="17d27-112">How Azure subscriptions are associated with Azure Active Directory</span></span>](active-directory-how-subscriptions-associated-directory.md)
* [<span data-ttu-id="17d27-113">Administración del directorio para la suscripción de Office 365 en Azure</span><span class="sxs-lookup"><span data-stu-id="17d27-113">Manage the directory for your Office 365 subscription in Azure</span></span>](active-directory-manage-o365-subscription.md)

- - -
<span data-ttu-id="17d27-114">**P: ¿Cuál es la relación entre AD de Azure, Office 365 y Azure?**</span><span class="sxs-lookup"><span data-stu-id="17d27-114">**Q: What’s the relationship between Azure AD, Office 365, and Azure?**</span></span>

<span data-ttu-id="17d27-115">**R:** Azure AD ofrece funcionalidades de acceso e identidad comunes a todos los servicios web.</span><span class="sxs-lookup"><span data-stu-id="17d27-115">**A:** Azure AD provides you with common identity and access capabilities to all web services.</span></span> <span data-ttu-id="17d27-116">Tanto si usa Office 365 como Microsoft Azure, Intune u otros servicios, ya está utilizando Azure AD para habilitar el inicio de sesión y la administración del acceso de todos estos servicios.</span><span class="sxs-lookup"><span data-stu-id="17d27-116">Whether you are using Office 365, Microsoft Azure, Intune, or others, you're already using Azure AD to help turn on sign-on and access management for all these services.</span></span>

<span data-ttu-id="17d27-117">Todos los usuarios que están configurados para usar servicios web se definen como cuentas de usuario en una o varias instancias de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="17d27-117">All users who are set up to use web services are defined as user accounts in one or more Azure AD instances.</span></span> <span data-ttu-id="17d27-118">Puede configurar gratis en estas cuentas las funcionalidades de Azure AD, como el acceso a aplicaciones en la nube.</span><span class="sxs-lookup"><span data-stu-id="17d27-118">You can set up these accounts for free Azure AD capabilities like cloud application access.</span></span>

<span data-ttu-id="17d27-119">Los servicios de pago de Azure AD, como Enterprise Mobility + Security, complementan otros servicios web como Office 365 y Microsoft Azure con completas soluciones de administración y seguridad para empresas.</span><span class="sxs-lookup"><span data-stu-id="17d27-119">Azure AD paid services like Enterprise Mobility + Security complement other web services like Office 365 and Microsoft Azure with comprehensive enterprise-scale management and security solutions.</span></span>
- - -
<span data-ttu-id="17d27-120">**P: ¿Por qué puedo iniciar sesión en Azure Portal, pero no el Portal de Azure clásico?**</span><span class="sxs-lookup"><span data-stu-id="17d27-120">**Q:  Why can I sign in to the Azure portal but not the Azure classic portal?**</span></span>

<span data-ttu-id="17d27-121">**R:** Azure Portal no requiere una suscripción válida y el Portal clásico sí la requiere.</span><span class="sxs-lookup"><span data-stu-id="17d27-121">**A:**  The Azure portal does not require a valid subscription, and the classic portal does require a valid subscription.</span></span>  <span data-ttu-id="17d27-122">Si no tiene una suscripción, no podrá iniciar sesión en el Portal clásico.</span><span class="sxs-lookup"><span data-stu-id="17d27-122">If you do not have a subscription, you can't sign in to the classic portal.</span></span>
- - -
<span data-ttu-id="17d27-123">**P: ¿En qué se diferencian los administradores de suscripción de los administradores de directorios?**</span><span class="sxs-lookup"><span data-stu-id="17d27-123">**Q:  What are the differences between Subscription Administrator and Directory Administrator?**</span></span>

<span data-ttu-id="17d27-124">**R:** De forma predeterminada, al suscribirse a Azure se le asigna el rol de administrador de suscripción.</span><span class="sxs-lookup"><span data-stu-id="17d27-124">**A:** By default, you are assigned the Subscription Administrator role when you sign up for Azure.</span></span> <span data-ttu-id="17d27-125">Los administradores de suscripción pueden usar una cuenta de Microsoft o una cuenta profesional o educativa del directorio al que está asociada la suscripción de Azure.</span><span class="sxs-lookup"><span data-stu-id="17d27-125">A subscription admin can use either a Microsoft account or a work or school account from the directory that the Azure subscription is associated with.</span></span>  <span data-ttu-id="17d27-126">Este rol tiene autorización para administrar servicios en Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="17d27-126">This role is authorized to manage services in the Azure portal.</span></span>

<span data-ttu-id="17d27-127">Si otros usuarios necesitan iniciar sesión y acceder a los servicios con la misma suscripción, se pueden agregar como coadministradores.</span><span class="sxs-lookup"><span data-stu-id="17d27-127">If others need to sign in and access services by using the same subscription, you can add them as co-admins.</span></span> <span data-ttu-id="17d27-128">Este rol tiene los mismos privilegios de acceso que el administrador de servicios, pero no puede cambiar la asociación de suscripciones a directorios de Azure.</span><span class="sxs-lookup"><span data-stu-id="17d27-128">This role has the same access privileges as the service admin, but can’t change the association of subscriptions to Azure directories.</span></span>  <span data-ttu-id="17d27-129">Para más información sobre los administradores de suscripción, consulte [How to add or change Azure administrator roles](../billing-add-change-azure-subscription-administrator.md) (Incorporación o cambio de roles de administrador de Azure) y [Asociación de las suscripciones de Azure con Azure Active Directory](active-directory-how-subscriptions-associated-directory.md).</span><span class="sxs-lookup"><span data-stu-id="17d27-129">For additional information on subscription admins, see [How to add or change Azure administrator roles](../billing-add-change-azure-subscription-administrator.md) and [How Azure subscriptions are associated with Azure Active Directory](active-directory-how-subscriptions-associated-directory.md).</span></span>


<span data-ttu-id="17d27-130">Azure AD tiene un conjunto diferente de roles administrativos para administrar las características relacionadas con la identidad y el directorio.</span><span class="sxs-lookup"><span data-stu-id="17d27-130">Azure AD has a different set of admin roles to manage the directory and identity-related features.</span></span>  <span data-ttu-id="17d27-131">Estos administradores accederán a varias características de Azure Portal o del Portal de Azure clásico.</span><span class="sxs-lookup"><span data-stu-id="17d27-131">These admins will have access to various features in the Azure portal or the Azure classic portal.</span></span> <span data-ttu-id="17d27-132">El rol de administrador determina qué puede hacer, como crear o editar usuarios, asignar roles administrativos a otros, restablecer contraseñas de usuario, administrar licencias de usuario o administrar dominios.</span><span class="sxs-lookup"><span data-stu-id="17d27-132">The admin's role determines what they can do, like create or edit users, assign administrative roles to others, reset user passwords, manage user licenses, or manage domains.</span></span>  <span data-ttu-id="17d27-133">Para más información sobre los administración de Azure AD y sus roles, consulte [Asignación de roles de administrador en Azure Active Directory](active-directory-assign-admin-roles.md).</span><span class="sxs-lookup"><span data-stu-id="17d27-133">For additional information on Azure AD directory admins and their roles, see [Assigning administrator roles in Azure Active Directory](active-directory-assign-admin-roles.md).</span></span>

<span data-ttu-id="17d27-134">Además, los servicios de pago de Azure AD, como Enterprise Mobility + Security, complementan otros servicios web como Office 365 y Microsoft Azure con completas soluciones de administración y seguridad para empresas.</span><span class="sxs-lookup"><span data-stu-id="17d27-134">Additionally, Azure AD paid services like Enterprise Mobility + Security complement other web services, such as Office 365 and Microsoft Azure, with comprehensive enterprise-scale management and security solutions.</span></span>

- - -
<span data-ttu-id="17d27-135">**P: ¿Existe un informe que muestra cuándo expirarán mis licencias de usuario de Azure AD?**</span><span class="sxs-lookup"><span data-stu-id="17d27-135">**Q: Is there a report that shows when my Azure AD user licenses will expire?**</span></span>

<span data-ttu-id="17d27-136">**R**: No.</span><span class="sxs-lookup"><span data-stu-id="17d27-136">**A:** No.</span></span>  <span data-ttu-id="17d27-137">No está disponible actualmente.</span><span class="sxs-lookup"><span data-stu-id="17d27-137">This is not currently available.</span></span>

- - -

## <a name="get-started-with-hybrid-azure-ad"></a><span data-ttu-id="17d27-138">Introducción a Azure AD híbrido</span><span class="sxs-lookup"><span data-stu-id="17d27-138">Get started with Hybrid Azure AD</span></span>


<span data-ttu-id="17d27-139">**P: ¿Cómo dejo un inquilino cuando se me ha agregado como colaborador?**</span><span class="sxs-lookup"><span data-stu-id="17d27-139">**Q: How do I leave a tenant when I am added as a collaborator?**</span></span>

<span data-ttu-id="17d27-140">**R:** Cuando se agrega a otro inquilino de la organización como colaborador, puede usar el "cambio de inquilino " de la esquina superior derecha para cambiar entre los inquilinos.</span><span class="sxs-lookup"><span data-stu-id="17d27-140">**A:** When you are added to another organization's tenant as a collaborator, you can use the "tenant switcher" in the upper right to switch between tenants.</span></span>  <span data-ttu-id="17d27-141">Actualmente, no hay forma de abandonar la organización que invita y Microsoft está trabajando para proporcionar esta funcionalidad.</span><span class="sxs-lookup"><span data-stu-id="17d27-141">Currently, there is no way to leave the inviting organization, and Microsoft is working on providing this functionality.</span></span>  <span data-ttu-id="17d27-142">Hasta que esta característica esté disponible, puede pedir a la organización que invita que le quite de su inquilino.</span><span class="sxs-lookup"><span data-stu-id="17d27-142">Until this feature is available, you can ask the inviting organization to remove you from their tenant.</span></span>
- - -
<span data-ttu-id="17d27-143">**P: ¿Cómo conecto mi directorio local a Azure AD?**</span><span class="sxs-lookup"><span data-stu-id="17d27-143">**Q: How can I connect my on-premises directory to Azure AD?**</span></span>

<span data-ttu-id="17d27-144">**R:** Puede conectar su directorio local a Azure AD mediante Azure AD Connect.</span><span class="sxs-lookup"><span data-stu-id="17d27-144">**A:** You can connect your on-premises directory to Azure AD by using Azure AD Connect.</span></span>

<span data-ttu-id="17d27-145">Para más información, consulte [Integración de las identidades locales con Azure Active Directory](active-directory-aadconnect.md).</span><span class="sxs-lookup"><span data-stu-id="17d27-145">For more information, see [Integrating your on-premises identities with Azure Active Directory](active-directory-aadconnect.md).</span></span>

- - -
<span data-ttu-id="17d27-146">**P: ¿Cómo se configura el SSO entre mi directorio local y las aplicaciones de nube?**</span><span class="sxs-lookup"><span data-stu-id="17d27-146">**Q: How do I set up SSO between my on-premises directory and my cloud applications?**</span></span>

<span data-ttu-id="17d27-147">**R:** Solo es preciso configurar el inicio de sesión único (SSO) entre el directorio local y Azure AD.</span><span class="sxs-lookup"><span data-stu-id="17d27-147">**A:** You only need to set up single sign-on (SSO) between your on-premises directory and Azure AD.</span></span> <span data-ttu-id="17d27-148">Mientras tenga acceso a las aplicaciones en la nube mediante Azure AD, el servicio lleva automáticamente a los usuarios a autenticarse correctamente con sus credenciales locales.</span><span class="sxs-lookup"><span data-stu-id="17d27-148">As long as you access your cloud applications through Azure AD, the service automatically drives your users to correctly authenticate with their on-premises credentials.</span></span>

<span data-ttu-id="17d27-149">La implementación del SSO desde el entorno local se puede lograr fácilmente con soluciones de federación como Active Directory Federation Services (AD FS) o configurando la sincronización de la sincronización de hash de contraseña. Puede implementar fácilmente ambas opciones con el Asistente para configuración de Azure AD Connect.</span><span class="sxs-lookup"><span data-stu-id="17d27-149">Implementing SSO from on-premises can be easily achieved with federation solutions such as Active Directory Federation Services (AD FS), or by configuring password hash sync. You can easily deploy both options by using the Azure AD Connect configuration wizard.</span></span>

<span data-ttu-id="17d27-150">Para más información, consulte [Integración de las identidades locales con Azure Active Directory](active-directory-aadconnect.md).</span><span class="sxs-lookup"><span data-stu-id="17d27-150">For more information, see [Integrating your on-premises identities with Azure Active Directory](active-directory-aadconnect.md).</span></span>

- - -
<span data-ttu-id="17d27-151">**P: ¿Proporciona Azure AD un portal de autoservicio para usuarios en mi organización?**</span><span class="sxs-lookup"><span data-stu-id="17d27-151">**Q: Does Azure AD provide a self-service portal for users in my organization?**</span></span>

<span data-ttu-id="17d27-152">**R:** Sí, Azure AD proporciona el [panel de acceso de Azure AD](http://myapps.microsoft.com) para el autoservicio de los usuarios y el acceso a las aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="17d27-152">**A:** Yes, Azure AD provides you with the [Azure AD Access Panel](http://myapps.microsoft.com) for user self-service and application access.</span></span> <span data-ttu-id="17d27-153">Si es cliente de Office 365, encontrará muchas de las mismas funcionalidades en el portal de Office 365.</span><span class="sxs-lookup"><span data-stu-id="17d27-153">If you are an Office 365 customer, you can find many of the same capabilities in the Office 365 portal.</span></span>

<span data-ttu-id="17d27-154">Para más información, consulte [Introducción al Panel de acceso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="17d27-154">For more information, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

- - -
<span data-ttu-id="17d27-155">**P: ¿Me ayuda Azure AD a administrar la infraestructura local?**</span><span class="sxs-lookup"><span data-stu-id="17d27-155">**Q: Does Azure AD help me manage my on-premises infrastructure?**</span></span>

<span data-ttu-id="17d27-156">**R:** Sí.</span><span class="sxs-lookup"><span data-stu-id="17d27-156">**A:** Yes.</span></span> <span data-ttu-id="17d27-157">Azure AD Premium Edition incluye Azure AD Connect Health.</span><span class="sxs-lookup"><span data-stu-id="17d27-157">The Azure AD Premium edition provides you with Azure AD Connect Health.</span></span> <span data-ttu-id="17d27-158">Azure AD Connect Health le ayuda a supervisar y a comprender mejor su infraestructura de identidad local y los servicios de sincronización.</span><span class="sxs-lookup"><span data-stu-id="17d27-158">Azure AD Connect Health helps you monitor and gain insight into your on-premises identity infrastructure and the synchronization services.</span></span>  

<span data-ttu-id="17d27-159">Para más información, consulte [Supervisión de la infraestructura de identidad local y los servicios de sincronización en la nube](active-directory-aadconnect-health.md).</span><span class="sxs-lookup"><span data-stu-id="17d27-159">For more information, see [Monitor your on-premises identity infrastructure and synchronization services in the cloud](active-directory-aadconnect-health.md).</span></span>  

- - -
## <a name="password-management"></a><span data-ttu-id="17d27-160">Administración de contraseñas</span><span class="sxs-lookup"><span data-stu-id="17d27-160">Password management</span></span>
<span data-ttu-id="17d27-161">**P: ¿Puedo usar la escritura diferida de contraseñas de Azure AD sin sincronización de contraseñas? (En este escenario, ¿se puede usar el restablecimiento de contraseña de autoservicio de Azure AD (SSPR) con la escritura diferida de contraseñas y no almacenar las contraseñas en la nube?)**</span><span class="sxs-lookup"><span data-stu-id="17d27-161">**Q: Can I use Azure AD password write-back without password sync? (In this scenario, is it possible to use Azure AD self-service password reset (SSPR) with password write-back and not store passwords in the cloud?)**</span></span>

<span data-ttu-id="17d27-162">**R:** No es necesario sincronizar las contraseñas de Active Directory con Azure AD para habilitar la escritura diferida.</span><span class="sxs-lookup"><span data-stu-id="17d27-162">**A:** You do not need to synchronize your Active Directory passwords to Azure AD to enable write-back.</span></span> <span data-ttu-id="17d27-163">En un entorno federado, el inicio de sesión único (SSO) de Azure AD se basa en el directorio local para autenticar al usuario.</span><span class="sxs-lookup"><span data-stu-id="17d27-163">In a federated environment, Azure AD single sign-on (SSO) relies on the on-premises directory to authenticate the user.</span></span> <span data-ttu-id="17d27-164">En este caso no se necesita la contraseña local para realizar el seguimiento en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="17d27-164">This scenario does not require the on-premises password to be tracked in Azure AD.</span></span>

- - -
<span data-ttu-id="17d27-165">**P: ¿Cuánto se tarda en escribir una contraseña en diferido en Active Directory local?**</span><span class="sxs-lookup"><span data-stu-id="17d27-165">**Q: How long does it take for a password to be written back to Active Directory on-premises?**</span></span>

<span data-ttu-id="17d27-166">**R:** La escritura diferida de contraseñas funciona en tiempo real.</span><span class="sxs-lookup"><span data-stu-id="17d27-166">**A:** Password write-back operates in real time.</span></span>

<span data-ttu-id="17d27-167">Para más información, consulte [Introducción a la administración de contraseñas](active-directory-passwords-getting-started.md).</span><span class="sxs-lookup"><span data-stu-id="17d27-167">For more information, see [Getting started with password management](active-directory-passwords-getting-started.md).</span></span>

- - -
<span data-ttu-id="17d27-168">**P: ¿Puedo usar la escritura diferida de contraseñas con las que administra un administrador?**</span><span class="sxs-lookup"><span data-stu-id="17d27-168">**Q: Can I use password write-back with passwords that are managed by an admin?**</span></span>

<span data-ttu-id="17d27-169">**R:** Sí, si tiene la escritura diferida de contraseñas habilitada, las operaciones de contraseña realizadas por un administrador se escriben de manera diferida en el entorno local.</span><span class="sxs-lookup"><span data-stu-id="17d27-169">**A:** Yes, if you have password write-back enabled, the password operations performed by an admin are written back to your on-premises environment.</span></span>  

<span data-ttu-id="17d27-170">Para ver más respuestas a preguntas relativas a las contraseñas, consulte [Preguntas más frecuentes sobre la administración de contraseñas](active-directory-passwords-faq.md).</span><span class="sxs-lookup"><span data-stu-id="17d27-170">For more answers to password-related questions, see [Password management frequently asked questions](active-directory-passwords-faq.md).</span></span>
- - -
<span data-ttu-id="17d27-171">**P: ¿Qué hago si no recuerdo mi contraseña de Office 365 o Azure AD cuando intento cambiarla?**</span><span class="sxs-lookup"><span data-stu-id="17d27-171">**Q:  What can I do if I can't remember my existing Office 365/Azure AD password while trying to change my password?**</span></span>

<span data-ttu-id="17d27-172">**R:** En este tipo de situaciones, dispone de un par de opciones.</span><span class="sxs-lookup"><span data-stu-id="17d27-172">**A:** For this type of situation, there are a couple of options.</span></span>  <span data-ttu-id="17d27-173">Use el restablecimiento de la contraseña de autoservicio (SSPR), si está disponible.</span><span class="sxs-lookup"><span data-stu-id="17d27-173">Use self-service password reset (SSPR) if it's available.</span></span>  <span data-ttu-id="17d27-174">El funcionamiento de SSPR dependerá de cómo esté configurado.</span><span class="sxs-lookup"><span data-stu-id="17d27-174">Whether SSPR works depends on how it's configured.</span></span>  <span data-ttu-id="17d27-175">Para más información, consulte la sección [¿Cómo funciona el portal de restablecimiento de contraseñas?](active-directory-passwords-best-practices.md)</span><span class="sxs-lookup"><span data-stu-id="17d27-175">For more information, see [How does the password reset portal work](active-directory-passwords-best-practices.md).</span></span>

<span data-ttu-id="17d27-176">Para los usuarios de Office 365, el administrador puede restablecer la contraseña mediante los pasos que se describen en [Administradores: restablecer contraseñas de usuario](https://support.office.com/en-us/article/Admins-Reset-user-passwords-7A5D073B-7FAE-4AA5-8F96-9ECD041ABA9C?ui=en-US&rs=en-US&ad=US).</span><span class="sxs-lookup"><span data-stu-id="17d27-176">For Office 365 users, your admin can reset the password by using the steps outlined in [Reset user passwords](https://support.office.com/en-us/article/Admins-Reset-user-passwords-7A5D073B-7FAE-4AA5-8F96-9ECD041ABA9C?ui=en-US&rs=en-US&ad=US).</span></span>

<span data-ttu-id="17d27-177">Para las cuentas de Azure AD, los administradores pueden restablecer las contraseñas mediante uno de los siguientes procedimientos:</span><span class="sxs-lookup"><span data-stu-id="17d27-177">For Azure AD accounts, admins can reset passwords by using one of the following:</span></span>

- [<span data-ttu-id="17d27-178">Restablecimiento de cuentas en Azure Portal</span><span class="sxs-lookup"><span data-stu-id="17d27-178">Reset accounts in the Azure portal</span></span>](active-directory-users-reset-password-azure-portal.md)
- [<span data-ttu-id="17d27-179">Restablecimiento de cuentas en el portal clásico</span><span class="sxs-lookup"><span data-stu-id="17d27-179">Reset accounts in the classic portal</span></span>](active-directory-create-users-reset-password.md)
- [<span data-ttu-id="17d27-180">Uso de PowerShell</span><span class="sxs-lookup"><span data-stu-id="17d27-180">Using PowerShell</span></span>](/powershell/module/msonline/set-msoluserpassword?view=azureadps-1.0)


- - -
## <a name="security"></a><span data-ttu-id="17d27-181">Seguridad</span><span class="sxs-lookup"><span data-stu-id="17d27-181">Security</span></span>
<span data-ttu-id="17d27-182">**P: ¿Se bloquean las cuentas después de un número determinado de intentos erróneos o se usa una estrategia más sofisticada?**</span><span class="sxs-lookup"><span data-stu-id="17d27-182">**Q: Are accounts locked after a specific number of failed attempts or is there a more sophisticated strategy used?**</span></span></br>
<span data-ttu-id="17d27-183">Usamos una estrategia más sofisticada para bloquear cuentas, que</span><span class="sxs-lookup"><span data-stu-id="17d27-183">We use a more sophisticated strategy to lock accounts.</span></span>  <span data-ttu-id="17d27-184">se basa en la dirección IP de la solicitud y las contraseñas escritas.</span><span class="sxs-lookup"><span data-stu-id="17d27-184">This is based on the IP of the request and the passwords entered.</span></span> <span data-ttu-id="17d27-185">El tiempo que dure el bloqueo también aumenta en función de la probabilidad de que sea un ataque.</span><span class="sxs-lookup"><span data-stu-id="17d27-185">The duration of the lockout also increases based on the likelihood that it is an attack.</span></span>  

<span data-ttu-id="17d27-186">**P: Algunas contraseñas (comunes) se rechazan con mensajes del tipo "esta contraseña se ha usado demasiadas veces". ¿Se refiere esto a las contraseñas usadas en la instancia de Active Directory actual?**</span><span class="sxs-lookup"><span data-stu-id="17d27-186">**Q:  Certain (common) passwords get rejected with the messages ‘this password has been used to many times’, does this refer to passwords used in the current active directory?**</span></span></br>
<span data-ttu-id="17d27-187">Se refiere a las contraseñas que son comunes a nivel global, como las variantes de "Contraseña" y "123456".</span><span class="sxs-lookup"><span data-stu-id="17d27-187">This refers to passwords that are globally common, such as any variants of “Password” and “123456”.</span></span>

<span data-ttu-id="17d27-188">**P: ¿Se bloqueará una solicitud de inicio de sesión de origen dudoso (botnets, punto de conexión Tor) en un inquilino B2C o se requerirá un inquilino de la edición Básica o Premium?**</span><span class="sxs-lookup"><span data-stu-id="17d27-188">**Q: Will a sign-in request from dubious sources (botnets, tor endpoint) be blocked in a B2C tenant or does this require a Basic or Premium edition tenant?**</span></span></br>
<span data-ttu-id="17d27-189">Tenemos una puerta de enlace que filtra las solicitudes y proporciona alguna protección contra los botnets, y se aplica a todos los inquilinos B2C.</span><span class="sxs-lookup"><span data-stu-id="17d27-189">We do have a gateway that filters requests and provides some protection from botnets, and is applied for all B2C tenants.</span></span>

## <a name="application-access"></a><span data-ttu-id="17d27-190">Acceso a las aplicaciones</span><span class="sxs-lookup"><span data-stu-id="17d27-190">Application access</span></span>
<span data-ttu-id="17d27-191">**P: ¿Dónde puedo encontrar una lista de las aplicaciones preintegradas en Azure AD y sus funcionalidades?**</span><span class="sxs-lookup"><span data-stu-id="17d27-191">**Q: Where can I find a list of applications that are pre-integrated with Azure AD and their capabilities?**</span></span>

<span data-ttu-id="17d27-192">**R:** Azure AD cuenta con más de 2 600 aplicaciones preintegradas de Microsoft, proveedores de servicios de aplicaciones y asociados.</span><span class="sxs-lookup"><span data-stu-id="17d27-192">**A:** Azure AD has more than 2,600 pre-integrated applications from Microsoft, application service providers, and partners.</span></span> <span data-ttu-id="17d27-193">Todas las aplicaciones preintegradas deben ser compatibles con el inicio de sesión único (SSO).</span><span class="sxs-lookup"><span data-stu-id="17d27-193">All pre-integrated applications support single sign-on (SSO).</span></span> <span data-ttu-id="17d27-194">El SSO permite utilizar las credenciales de su organización para acceder a las aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="17d27-194">SSO lets you use your organizational credentials to access your apps.</span></span> <span data-ttu-id="17d27-195">Algunas de las aplicaciones también admiten el aprovisionamiento y el desaprovisionamiento automatizados.</span><span class="sxs-lookup"><span data-stu-id="17d27-195">Some of the applications also support automated provisioning and de-provisioning.</span></span>

<span data-ttu-id="17d27-196">Para ver una lista exhaustiva de las aplicaciones preintegradas, consulte [Active Directory Marketplace](https://azure.microsoft.com/marketplace/active-directory/).</span><span class="sxs-lookup"><span data-stu-id="17d27-196">For a complete list of the pre-integrated applications, see the [Active Directory Marketplace](https://azure.microsoft.com/marketplace/active-directory/).</span></span>

- - -
<span data-ttu-id="17d27-197">**P: ¿Qué ocurre si no encuentro la aplicación que necesito en Marketplace de Azure AD?**</span><span class="sxs-lookup"><span data-stu-id="17d27-197">**Q: What if the application I need is not in the Azure AD marketplace?**</span></span>

<span data-ttu-id="17d27-198">**R:** Con Azure AD Premium puede agregar y configurar cualquier aplicación.</span><span class="sxs-lookup"><span data-stu-id="17d27-198">**A:** With Azure AD Premium, you can add and configure any application that you want.</span></span> <span data-ttu-id="17d27-199">Según las funcionalidades de la aplicación y sus preferencias, puede configurar el SSO y el aprovisionamiento automatizado.</span><span class="sxs-lookup"><span data-stu-id="17d27-199">Depending on your application’s capabilities and your preferences, you can configure SSO and automated provisioning.</span></span>  

<span data-ttu-id="17d27-200">Para más información, consulte:</span><span class="sxs-lookup"><span data-stu-id="17d27-200">For more information, see:</span></span>

* [<span data-ttu-id="17d27-201">Configuración del inicio de sesión único en aplicaciones que no están en la Galería de aplicaciones de Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="17d27-201">Configuring single sign-on to applications that are not in the Azure Active Directory application gallery</span></span>](active-directory-saas-custom-apps.md)
* [<span data-ttu-id="17d27-202">Uso de SCIM para habilitar el aprovisionamiento automático de usuarios y grupos de Azure Active Directory a aplicaciones</span><span class="sxs-lookup"><span data-stu-id="17d27-202">Using SCIM to enable automatic provisioning of users and groups from Azure Active Directory to applications</span></span>](active-directory-scim-provisioning.md)

- - -
<span data-ttu-id="17d27-203">**P: ¿Cómo inician los usuarios sesión en aplicaciones con Azure AD?**</span><span class="sxs-lookup"><span data-stu-id="17d27-203">**Q: How do users sign in to applications by using Azure AD?**</span></span>

<span data-ttu-id="17d27-204">**R:** Azure AD proporciona varias formas de que los usuarios vean y accedan a sus aplicaciones, como:</span><span class="sxs-lookup"><span data-stu-id="17d27-204">**A:** Azure AD provides several ways for users to view and access their applications, such as:</span></span>

* <span data-ttu-id="17d27-205">El Panel de acceso de Azure AD</span><span class="sxs-lookup"><span data-stu-id="17d27-205">The Azure AD access panel</span></span>
* <span data-ttu-id="17d27-206">El iniciador de aplicaciones de Office 365</span><span class="sxs-lookup"><span data-stu-id="17d27-206">The Office 365 application launcher</span></span>
* <span data-ttu-id="17d27-207">Inicio de sesión directo en aplicaciones federadas</span><span class="sxs-lookup"><span data-stu-id="17d27-207">Direct sign-in to federated apps</span></span>
* <span data-ttu-id="17d27-208">Vínculos profundos a aplicaciones federadas, con contraseña o existentes</span><span class="sxs-lookup"><span data-stu-id="17d27-208">Deep links to federated, password-based, or existing apps</span></span>

<span data-ttu-id="17d27-209">Para más información, consulte [Implementación de aplicaciones integradas en Azure AD a los usuarios](active-directory-appssoaccess-whatis.md#deploying-azure-ad-integrated-applications-to-users).</span><span class="sxs-lookup"><span data-stu-id="17d27-209">For more information, see [Deploying Azure AD integrated applications to users](active-directory-appssoaccess-whatis.md#deploying-azure-ad-integrated-applications-to-users).</span></span>

- - -
<span data-ttu-id="17d27-210">**P: ¿Cuáles son las distintas formas en que Azure AD permite la autenticación y el inicio de sesión único en aplicaciones?**</span><span class="sxs-lookup"><span data-stu-id="17d27-210">**Q: What are the different ways Azure AD enables authentication and single sign-on to applications?**</span></span>

<span data-ttu-id="17d27-211">**R:** Azure AD admite muchos protocolos estandarizados para la autenticación y la autorización, como SAML 2.0, OpenID Connect, OAuth 2.0 y WS-Federation.</span><span class="sxs-lookup"><span data-stu-id="17d27-211">**A:** Azure AD supports many standardized protocols for authentication and authorization, such as SAML 2.0, OpenID Connect, OAuth 2.0, and WS-Federation.</span></span> <span data-ttu-id="17d27-212">Además, Azure AD admite las funcionalidades de inicio de sesión automatizado y de almacenamiento de contraseñas para las aplicaciones que solo sean compatibles con la autenticación basada en formularios.</span><span class="sxs-lookup"><span data-stu-id="17d27-212">Azure AD also supports password vaulting and automated sign-in capabilities for apps that only support forms-based authentication.</span></span>  

<span data-ttu-id="17d27-213">Para más información, consulte:</span><span class="sxs-lookup"><span data-stu-id="17d27-213">For more information, see:</span></span>

* [<span data-ttu-id="17d27-214">Escenarios de autenticación para Azure AD</span><span class="sxs-lookup"><span data-stu-id="17d27-214">Authentication Scenarios for Azure AD</span></span>](active-directory-authentication-scenarios.md)
* [<span data-ttu-id="17d27-215">Protocolos de autenticación de Active Directory</span><span class="sxs-lookup"><span data-stu-id="17d27-215">Active Directory authentication protocols</span></span>](https://msdn.microsoft.com/library/azure/dn151124.aspx)
* [<span data-ttu-id="17d27-216">¿Cómo funciona el inicio de sesión único con Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="17d27-216">How does single sign-on with Azure Active Directory work?</span></span>](active-directory-appssoaccess-whatis.md#how-does-single-sign-on-with-azure-active-directory-work)

- - -
<span data-ttu-id="17d27-217">**P: ¿Puedo agregar aplicaciones que ejecuto de manera local?**</span><span class="sxs-lookup"><span data-stu-id="17d27-217">**Q: Can I add applications I’m running on-premises?**</span></span>

<span data-ttu-id="17d27-218">**R:** El proxy de aplicación de Azure AD proporciona un acceso fácil y seguro a las aplicaciones web locales que elija.</span><span class="sxs-lookup"><span data-stu-id="17d27-218">**A:** Azure AD Application Proxy provides you with easy and secure access to on-premises web applications that you choose.</span></span> <span data-ttu-id="17d27-219">Puede acceder a estas aplicaciones como si se trataran de sus aplicaciones de software como servicio (SaaS) en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="17d27-219">You can access these applications in the same way that you access your software as a service (SaaS) apps in Azure AD.</span></span> <span data-ttu-id="17d27-220">No se necesita una VPN ni cambiar la infraestructura de red.</span><span class="sxs-lookup"><span data-stu-id="17d27-220">There is no need for a VPN or to change your network infrastructure.</span></span>  

<span data-ttu-id="17d27-221">Para más información, consulte [Provisión de acceso remoto seguro a aplicaciones locales](active-directory-application-proxy-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="17d27-221">For more information, see [How to provide secure remote access to on-premises applications](active-directory-application-proxy-get-started.md).</span></span>

- - -
<span data-ttu-id="17d27-222">**P: ¿Cómo requiero la autenticación multifactor para usuarios con acceso a una aplicación determinada?**</span><span class="sxs-lookup"><span data-stu-id="17d27-222">**Q: How do I require multi-factor authentication for users who access a particular application?**</span></span>

<span data-ttu-id="17d27-223">**R:** Con el acceso condicional de Azure AD, puede asignar una directiva de acceso única a cada aplicación.</span><span class="sxs-lookup"><span data-stu-id="17d27-223">**A:** With Azure AD conditional access, you can assign a unique access policy for each application.</span></span> <span data-ttu-id="17d27-224">En la directiva, puede solicitar la autenticación multifactor siempre o solo cuando los usuarios no estén conectados a la red local.</span><span class="sxs-lookup"><span data-stu-id="17d27-224">In your policy, you can require multi-factor authentication always, or when users are not connected to the local network.</span></span>  

<span data-ttu-id="17d27-225">Para más información, consulte [Protección del acceso a Office 365 y otras aplicaciones conectadas a Azure Active Directory](active-directory-conditional-access.md).</span><span class="sxs-lookup"><span data-stu-id="17d27-225">For more information, see [Securing access to Office 365 and other apps connected to Azure Active Directory](active-directory-conditional-access.md).</span></span>

- - -
<span data-ttu-id="17d27-226">**P: ¿Qué es el aprovisionamiento automático de usuarios para aplicaciones SaaS?**</span><span class="sxs-lookup"><span data-stu-id="17d27-226">**Q: What is automated user provisioning for SaaS apps?**</span></span>

<span data-ttu-id="17d27-227">**R:** Use Azure AD para automatizar la creación, el mantenimiento y la eliminación de identidades de usuario en muchas aplicaciones SaaS en la nube conocidas.</span><span class="sxs-lookup"><span data-stu-id="17d27-227">**A:** Use Azure AD to automate the creation, maintenance, and removal of user identities in many popular cloud SaaS apps.</span></span>

<span data-ttu-id="17d27-228">Para más información, consulte [Automatización del aprovisionamiento y desaprovisionamiento de usuarios para aplicaciones SaaS con Azure Active Directory](active-directory-saas-app-provisioning.md)</span><span class="sxs-lookup"><span data-stu-id="17d27-228">For more information, see [Automate user provisioning and deprovisioning to SaaS applications with Azure Active Directory](active-directory-saas-app-provisioning.md).</span></span>

- - -
<span data-ttu-id="17d27-229">**P: ¿Puedo configurar una conexión LDAP segura con Azure Active Directory?**</span><span class="sxs-lookup"><span data-stu-id="17d27-229">**Q:  Can I set up a secure LDAP connection with Azure AD?**</span></span>

<span data-ttu-id="17d27-230">**R**: No.</span><span class="sxs-lookup"><span data-stu-id="17d27-230">**A:**  No.</span></span> <span data-ttu-id="17d27-231">Azure AD no admite el protocolo LDAP.</span><span class="sxs-lookup"><span data-stu-id="17d27-231">Azure AD does not support the LDAP protocol.</span></span>
