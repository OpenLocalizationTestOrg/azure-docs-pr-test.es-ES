---
title: "¿Qué es la colaboración B2B de Azure Active Directory? | Microsoft Docs"
description: "La colaboración B2B de Azure Active Directory posibilita las relaciones entre empresas al permitir que los asociados comerciales tengan acceso de forma selectiva a las aplicaciones corporativas."
services: active-directory
documentationcenter: 
author: sasubram
manager: femila
editor: 
tags: 
ms.assetid: 1464387b-ee8b-4c7c-94b3-2c5567224c27
ms.service: active-directory
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: identity
ms.date: 06/27/2017
ms.author: curtand
ms.custom: aaddev
ms.reviewer: sasubram
ms.openlocfilehash: fbc12a52555b190d43b5e953fd4d19923a25b0ed
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="what-is-azure-ad-b2b-collaboration"></a><span data-ttu-id="6771b-104">¿Qué es la colaboración B2B de Azure AD?</span><span class="sxs-lookup"><span data-stu-id="6771b-104">What is Azure AD B2B collaboration?</span></span>

<iframe width="560" height="315" src="https://www.youtube.com/embed/AhwrweCBdsc" frameborder="0" allowfullscreen></iframe>

<span data-ttu-id="6771b-105">Las funcionalidades de colaboración de Azure AD negocio a negocio (B2B) permiten que cualquier organización con Azure AD funcione de forma segura con usuarios de cualquier otra organización, pequeña o grande;</span><span class="sxs-lookup"><span data-stu-id="6771b-105">Azure AD business-to-business (B2B) collaboration capabilities enable any organization using Azure AD to work safely and securely with users from any other organization, small or large.</span></span> <span data-ttu-id="6771b-106">con o sin Azure AD; de hecho, con o sin una organización de TI.</span><span class="sxs-lookup"><span data-stu-id="6771b-106">Those organizations can be with Azure AD or without, or even with an IT organization or without.</span></span> 

<span data-ttu-id="6771b-107">Las organizaciones que usan Azure AD pueden proporcionar acceso a documentos, recursos y aplicaciones a sus asociados, mientras mantienen un control total sobre sus propios datos corporativos.</span><span class="sxs-lookup"><span data-stu-id="6771b-107">Organizations using Azure AD can provide access to documents, resources, and applications to their partners, while maintaining complete control over their own corporate data.</span></span> <span data-ttu-id="6771b-108">Los desarrolladores pueden usar las API de negocio a negocio de Azure AD para escribir aplicaciones que unan a dos organizaciones de una manera más segura.</span><span class="sxs-lookup"><span data-stu-id="6771b-108">Developers can use the Azure AD business-to-business APIs to write applications that bring two organizations together in more securely.</span></span> <span data-ttu-id="6771b-109">Además, la navegación resulta bastante sencilla para los usuarios finales.</span><span class="sxs-lookup"><span data-stu-id="6771b-109">Also, it's pretty easy for end users to navigate.</span></span>

<span data-ttu-id="6771b-110">El 97 % de nuestros clientes nos ha comentado que la colaboración B2B en Azure AD es muy importante para ellos.</span><span class="sxs-lookup"><span data-stu-id="6771b-110">97% of our customers have told us Azure AD B2B collaboration is very important to them.</span></span>

![gráfico circular](media/active-directory-b2b-what-is-azure-ad-b2b/97-percent-support.png)

<span data-ttu-id="6771b-112">Desde comienzos de abril de 2017, aproximadamente 3 millones de usuarios ya usan las funcionalidades de colaboración B2B en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="6771b-112">As of early April 2017, we had about 3 million users already using Azure AD B2B collaboration capabilities.</span></span> <span data-ttu-id="6771b-113">Y más del 23 % de organizaciones de Azure AD que tienen más de 10 usuarios ya se benefician de estas funcionalidades.</span><span class="sxs-lookup"><span data-stu-id="6771b-113">And more than 23% of Azure AD organizations that have more than 10 users are already benefiting from these capabilities.</span></span>

## <a name="the-key-benefits-of-azure-ad-b2b-collaboration-to-your-organization"></a><span data-ttu-id="6771b-114">Entre las principales ventajas de la colaboración B2B de Azure AD para su organización, se encuentran las siguientes:</span><span class="sxs-lookup"><span data-stu-id="6771b-114">The key benefits of Azure AD B2B collaboration to your organization</span></span>

### <a name="work-with-any-user-from-any-partner"></a><span data-ttu-id="6771b-115">Permite trabajar con cualquier usuario de cualquier asociado.</span><span class="sxs-lookup"><span data-stu-id="6771b-115">Work with any user from any partner</span></span>

* <span data-ttu-id="6771b-116">Los asociados usan sus propias credenciales.</span><span class="sxs-lookup"><span data-stu-id="6771b-116">Partners use their own credentials</span></span>

* <span data-ttu-id="6771b-117">Los asociados no necesitan usar Azure AD.</span><span class="sxs-lookup"><span data-stu-id="6771b-117">No requirement for partners to use Azure AD</span></span>

* <span data-ttu-id="6771b-118">No se necesita ningún directorio externo o instalación compleja.</span><span class="sxs-lookup"><span data-stu-id="6771b-118">No external directories or complex set-up required</span></span>

### <a name="simple-and-secure-collaboration"></a><span data-ttu-id="6771b-119">Colaboración sencilla y segura</span><span class="sxs-lookup"><span data-stu-id="6771b-119">Simple and secure collaboration</span></span>

* <span data-ttu-id="6771b-120">Proporciona acceso a cualquier aplicación o datos corporativos, al aplicar avanzadas directivas de autorización con tecnología de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="6771b-120">Provide access to any corporate app or data, while applying sophisticated, Azure AD-powered authorization policies</span></span>

* <span data-ttu-id="6771b-121">Fácil para los usuarios</span><span class="sxs-lookup"><span data-stu-id="6771b-121">Easy for users</span></span>

* <span data-ttu-id="6771b-122">Seguridad de nivel empresarial para aplicaciones y datos.</span><span class="sxs-lookup"><span data-stu-id="6771b-122">Enterprise-grade security for apps and data</span></span>

### <a name="no-management-overhead"></a><span data-ttu-id="6771b-123">Sin sobrecarga de administración.</span><span class="sxs-lookup"><span data-stu-id="6771b-123">No management overhead</span></span>

* <span data-ttu-id="6771b-124">Sin administración externa de contraseñas o cuentas.</span><span class="sxs-lookup"><span data-stu-id="6771b-124">No external account or password management</span></span>

* <span data-ttu-id="6771b-125">Sin administración del ciclo de vida de cuenta manual o sincronización.</span><span class="sxs-lookup"><span data-stu-id="6771b-125">No sync or manual account lifecycle management</span></span>

* <span data-ttu-id="6771b-126">Sin sobrecarga administrativa externa.</span><span class="sxs-lookup"><span data-stu-id="6771b-126">No external administrative overhead</span></span>

## <a name="you-can-easily-add-b2b-collaboration-users-to-your-organization"></a><span data-ttu-id="6771b-127">Adición fácil de usuarios de colaboración B2B a la organización</span><span class="sxs-lookup"><span data-stu-id="6771b-127">You can easily add B2B collaboration users to your organization</span></span>

<span data-ttu-id="6771b-128">Los administradores pueden agregar usuarios de colaboración (invitados) de B2B en [Azure Portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="6771b-128">Admins can add B2B collaboration (guest) users in the [Azure portal](https://portal.azure.com).</span></span>

![agregar usuarios invitados](media/active-directory-b2b-what-is-azure-ad-b2b/adding-b2b-users-admin.png)

### <a name="enable-your-collaborators-to-bring-their-own-identity"></a><span data-ttu-id="6771b-130">Permiso a los colaboradores para que traigan su propia identidad</span><span class="sxs-lookup"><span data-stu-id="6771b-130">Enable your collaborators to bring their own identity</span></span>

<span data-ttu-id="6771b-131">Los colaboradores de B2B pueden iniciar sesión con la identidad que elijan.</span><span class="sxs-lookup"><span data-stu-id="6771b-131">B2B collaborators can sign in with an identity of their choice.</span></span> <span data-ttu-id="6771b-132">Si el usuario no tiene una cuenta de Microsoft o de Azure AD, se crea una en su nombre en el momento del canje de la oferta.</span><span class="sxs-lookup"><span data-stu-id="6771b-132">If the user doesn’t have a Microsoft account or an Azure AD account – one is created for them seamlessly at the time for offer redemption.</span></span>

![opción de identidad inicio de sesión](media/active-directory-b2b-what-is-azure-ad-b2b/sign-in-identity-choice.png)

### <a name="delegate-to-application-and-group-owners"></a><span data-ttu-id="6771b-134">Delegación a propietarios de grupos y aplicaciones</span><span class="sxs-lookup"><span data-stu-id="6771b-134">Delegate to application and group owners</span></span> 
<span data-ttu-id="6771b-135">Los propietarios de aplicaciones y grupos pueden agregar usuarios de B2B directamente a cualquier aplicación que les interese, ya sea una aplicación de Microsoft o no.</span><span class="sxs-lookup"><span data-stu-id="6771b-135">Application and group owners can add B2B users directly to any application that you care about, whether it is a Microsoft application or not.</span></span> <span data-ttu-id="6771b-136">Los administradores pueden delegar el permiso para agregar usuarios de B2B a los usuarios no administradores.</span><span class="sxs-lookup"><span data-stu-id="6771b-136">Admins can delegate permission to add B2B users to non-admins.</span></span> <span data-ttu-id="6771b-137">Los usuarios no administradores pueden utilizar el [panel de acceso a la aplicación de Azure AD](https://myapps.microsoft.com) para agregar los usuarios de colaboración B2B a aplicaciones o grupos.</span><span class="sxs-lookup"><span data-stu-id="6771b-137">Non-admins can use the [Azure AD Application Access Panel](https://myapps.microsoft.com) to add B2B collaboration users to applications or groups.</span></span>

![panel de acceso](media/active-directory-b2b-what-is-azure-ad-b2b/access-panel.png)

![agregar miembro](media/active-directory-b2b-what-is-azure-ad-b2b/add-member.png)

### <a name="authorization-policies-protect-your-corporate-content"></a><span data-ttu-id="6771b-140">Protección de las directivas de autorización al contenido corporativo</span><span class="sxs-lookup"><span data-stu-id="6771b-140">Authorization policies protect your corporate content</span></span>

<span data-ttu-id="6771b-141">Las directivas de acceso condicional, como la autenticación multifactor, se pueden aplicar:</span><span class="sxs-lookup"><span data-stu-id="6771b-141">Conditional access policies, such as multi-factor authentication, can be enforced:</span></span>
- <span data-ttu-id="6771b-142">En el nivel de inquilino</span><span class="sxs-lookup"><span data-stu-id="6771b-142">At the tenant level</span></span>
- <span data-ttu-id="6771b-143">En el nivel de aplicación</span><span class="sxs-lookup"><span data-stu-id="6771b-143">At the application level</span></span>
- <span data-ttu-id="6771b-144">A usuarios específicos para proteger los datos y las aplicaciones empresariales.</span><span class="sxs-lookup"><span data-stu-id="6771b-144">For specific users to protect corporate apps and data</span></span>

![agregar miembro](media/active-directory-b2b-what-is-azure-ad-b2b/add-member.png)

### <a name="use-our-apis-and-sample-code-to-easily-build-applications-to-onboard"></a><span data-ttu-id="6771b-146">Uso de nuestras API y código de ejemplo para crear fácilmente aplicaciones para realizar una incorporación</span><span class="sxs-lookup"><span data-stu-id="6771b-146">Use our APIs and sample code to easily build applications to onboard</span></span>
<span data-ttu-id="6771b-147">Incorpore a los asociados externos de manera personalizada según las necesidades de su organización.</span><span class="sxs-lookup"><span data-stu-id="6771b-147">Bring your external partners on board in ways customized to your organization’s needs.</span></span>

<span data-ttu-id="6771b-148">Con las [API de invitación de colaboración B2B](https://developer.microsoft.com/graph/docs/api-reference/v1.0/resources/invitation) puede personalizar sus experiencias de incorporación, incluida la creación de portales de suscripción de autoservicio.</span><span class="sxs-lookup"><span data-stu-id="6771b-148">Using the [B2B collaboration invitation APIs](https://developer.microsoft.com/graph/docs/api-reference/v1.0/resources/invitation), you can customize your onboarding experiences, including creating self-service sign-up portals.</span></span> <span data-ttu-id="6771b-149">Proporcionamos código de ejemplo para un portal de autoservicio [en Github](https://github.com/Azure/active-directory-dotnet-graphapi-b2bportal-web).</span><span class="sxs-lookup"><span data-stu-id="6771b-149">We provide sample code for a self-service portal [on Github](https://github.com/Azure/active-directory-dotnet-graphapi-b2bportal-web).</span></span>

![portal de suscripción](media/active-directory-b2b-what-is-azure-ad-b2b/sign-up-portal.png)

<span data-ttu-id="6771b-151">Con la colaboración B2B de Azure AD, puede obtener toda la funcionalidad de Azure AD para proteger sus relaciones con los asociados de forma que los usuarios finales la encuentren sencilla e intuitiva.</span><span class="sxs-lookup"><span data-stu-id="6771b-151">With Azure AD B2B collaboration, you can get the full power of Azure AD to protect your partner relationships in a way that end users find easy and intuitive.</span></span> <span data-ttu-id="6771b-152">Por tanto, únase a las miles de organizaciones que ya utilizan B2B de Azure AD para facilitar la colaboración externa.</span><span class="sxs-lookup"><span data-stu-id="6771b-152">So go ahead, join the thousands of organizations that are already using Azure AD B2B for their external collaboration!</span></span>

## <a name="next-steps"></a><span data-ttu-id="6771b-153">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="6771b-153">Next steps</span></span>

* <span data-ttu-id="6771b-154">Las experiencias del administrador se encuentran en [Azure Portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="6771b-154">Administrator experiences are found in the [Azure portal](https://portal.azure.com).</span></span>

* <span data-ttu-id="6771b-155">Las experiencias del trabajador de la información están disponibles en el [panel de acceso](https://myapps.microsoft.com).</span><span class="sxs-lookup"><span data-stu-id="6771b-155">Information worker experiences are available in the [Access Panel](https://myapps.microsoft.com).</span></span>

* <span data-ttu-id="6771b-156">Y, como siempre, conéctese con el equipo del producto para obtener comentarios, conversaciones y sugerencias a través de nuestra [Comunidad tecnológica de Microsoft](https://techcommunity.microsoft.com/t5/Azure-Active-Directory-B2B/bd-p/AzureAD_B2b).</span><span class="sxs-lookup"><span data-stu-id="6771b-156">And, as always, connect with the product team for any feedback, discussions, and suggestions through our [Microsoft Tech Community](https://techcommunity.microsoft.com/t5/Azure-Active-Directory-B2B/bd-p/AzureAD_B2b).</span></span>

<span data-ttu-id="6771b-157">Examine nuestros otros artículos sobre la colaboración B2B de Azure AD:</span><span class="sxs-lookup"><span data-stu-id="6771b-157">Browse our other articles on Azure AD B2B collaboration:</span></span>

* [<span data-ttu-id="6771b-158">¿Cómo agregan los administradores de Azure Active Directory usuarios de colaboración B2B?</span><span class="sxs-lookup"><span data-stu-id="6771b-158">How do Azure Active Directory admins add B2B collaboration users?</span></span>](active-directory-b2b-admin-add-users.md)
* [<span data-ttu-id="6771b-159">¿Cómo agregan los trabajadores de la información usuarios de colaboración B2B?</span><span class="sxs-lookup"><span data-stu-id="6771b-159">How do information workers add B2B collaboration users?</span></span>](active-directory-b2b-iw-add-users.md)
* [<span data-ttu-id="6771b-160">Los elementos del correo electrónico de invitación de colaboración B2B</span><span class="sxs-lookup"><span data-stu-id="6771b-160">The elements of the B2B collaboration invitation email</span></span>](active-directory-b2b-invitation-email.md)
* [<span data-ttu-id="6771b-161">Canje de invitación de colaboración B2B</span><span class="sxs-lookup"><span data-stu-id="6771b-161">B2B collaboration invitation redemption</span></span>](active-directory-b2b-redemption-experience.md)
* [<span data-ttu-id="6771b-162">Concesión de licencias de colaboración B2B de Azure AD</span><span class="sxs-lookup"><span data-stu-id="6771b-162">Azure AD B2B collaboration licensing</span></span>](active-directory-b2b-licensing.md)
* [<span data-ttu-id="6771b-163">Solución de problemas de colaboración B2B de Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="6771b-163">Troubleshooting Azure Active Directory B2B collaboration</span></span>](active-directory-b2b-troubleshooting.md)
* [<span data-ttu-id="6771b-164">Preguntas frecuentes sobre la colaboración B2B de Azure Active Directory (P+F)</span><span class="sxs-lookup"><span data-stu-id="6771b-164">Azure Active Directory B2B collaboration frequently asked questions (FAQ)</span></span>](active-directory-b2b-faq.md)
* [<span data-ttu-id="6771b-165">Personalización y API de colaboración B2B de Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="6771b-165">Azure Active Directory B2B collaboration API and customization</span></span>](active-directory-b2b-api.md)
* [<span data-ttu-id="6771b-166">Autenticación multifactor para usuarios de colaboración B2B</span><span class="sxs-lookup"><span data-stu-id="6771b-166">Multi-factor authentication for B2B collaboration users</span></span>](active-directory-b2b-mfa-instructions.md)
* [<span data-ttu-id="6771b-167">Incorporación de usuarios de colaboración B2B sin invitación</span><span class="sxs-lookup"><span data-stu-id="6771b-167">Add B2B collaboration users without an invitation</span></span>](active-directory-b2b-add-user-without-invite.md)
* [<span data-ttu-id="6771b-168">Auditoría y generación de informes de usuarios de colaboración B2B</span><span class="sxs-lookup"><span data-stu-id="6771b-168">B2B collaboration user auditing and reporting</span></span>](active-directory-b2b-auditing-and-reporting.md)
* [<span data-ttu-id="6771b-169">Índice de artículos sobre la administración de aplicaciones en Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="6771b-169">Article Index for Application Management in Azure Active Directory</span></span>](active-directory-apps-index.md)
