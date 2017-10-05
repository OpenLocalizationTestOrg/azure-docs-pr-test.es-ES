---
title: "Administración de nombres de dominio personalizados en Azure Active Directory | Microsoft Docs"
description: "Conceptos y procedimientos de administración de un dominio personalizado en Azure Active Directory"
services: active-directory
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: cf3523bd-9ee0-439e-963d-ccea038867b9
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/26/2017
ms.author: curtand
ms.custom: oldportal;it-pro;
robots: NOINDEX
ms.openlocfilehash: 5ae19bb370064de96cf466ca09b13d02563d65a4
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/03/2017
---
# <a name="managing-custom-domain-names-in-your-azure-active-directory"></a><span data-ttu-id="fc2a7-103">Administración de los nombres de dominio personalizados en Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="fc2a7-103">Managing custom domain names in your Azure Active Directory</span></span>
<span data-ttu-id="fc2a7-104">Un nombre de dominio puede ser un identificador importante para muchos recursos de directorio, como parte de:</span><span class="sxs-lookup"><span data-stu-id="fc2a7-104">A domain name can be an important identifier for many directory resources, as part of:</span></span>

* <span data-ttu-id="fc2a7-105">Un nombre de usuario o una dirección de correo electrónico de un usuario</span><span class="sxs-lookup"><span data-stu-id="fc2a7-105">A user name or email address for a user</span></span>
* <span data-ttu-id="fc2a7-106">La dirección de un grupo</span><span class="sxs-lookup"><span data-stu-id="fc2a7-106">The address for a group</span></span>
* <span data-ttu-id="fc2a7-107">El identificador URI del id. de aplicación para una aplicación</span><span class="sxs-lookup"><span data-stu-id="fc2a7-107">The app ID URI for an application</span></span>

<span data-ttu-id="fc2a7-108">Un recurso en Azure Active Directory (Azure AD) puede incluir un nombre de dominio cuya pertenencia al directorio que contiene el recurso ya se haya verificado.</span><span class="sxs-lookup"><span data-stu-id="fc2a7-108">A resource in Azure Active Directory (Azure AD) can include a domain name that is already verified to be owned by the directory that contains the resource.</span></span> <span data-ttu-id="fc2a7-109">Solo los administradores globales pueden realizar tareas de administración de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="fc2a7-109">Only a global administrator can perform domain management tasks in Azure AD.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="fc2a7-110">Microsoft recomienda administrar Azure AD con el [Centro de administración de Azure AD](https://aad.portal.azure.com) en Azure Portal en lugar de usar el portal de Azure clásico al que se hace referencia en este artículo.</span><span class="sxs-lookup"><span data-stu-id="fc2a7-110">Microsoft recommends that you manage Azure AD using the [Azure AD admin center](https://aad.portal.azure.com) in the Azure portal instead of using the Azure classic portal referenced in this article.</span></span> <span data-ttu-id="fc2a7-111">Para saber cómo administrar los nombres de dominio en el centro de administración de Azure AD, consulte [Administración de los nombres de dominio personalizados en Azure Active Directory](active-directory-domains-manage-azure-portal.md).</span><span class="sxs-lookup"><span data-stu-id="fc2a7-111">For how to manage your domain names in the Azure AD admin center, see [Managing custom domain names in your Azure Active Directory](active-directory-domains-manage-azure-portal.md).</span></span>

## <a name="set-the-primary-domain-name-for-your-azure-ad-directory"></a><span data-ttu-id="fc2a7-112">Establecimiento del nombre de dominio principal para su directorio de Azure AD</span><span class="sxs-lookup"><span data-stu-id="fc2a7-112">Set the primary domain name for your Azure AD directory</span></span>
<span data-ttu-id="fc2a7-113">Cuando se crea el directorio, el nombre de dominio inicial, por ejemplo, "contoso.onmicrosoft.com", también es el nombre de dominio principal para el directorio.</span><span class="sxs-lookup"><span data-stu-id="fc2a7-113">When your directory is created, the initial domain name, such as ‘contoso.onmicrosoft.com,’ is also the primary domain name for your directory.</span></span> <span data-ttu-id="fc2a7-114">El dominio principal es el nombre de dominio predeterminado para un nuevo usuario cuando se crea un nuevo usuario en el [Portal de Azure clásico](https://manage.windowsazure.com/)o en otros portales, como el portal de administración de Office 365.</span><span class="sxs-lookup"><span data-stu-id="fc2a7-114">The primary domain is the default domain name for a new user when you create a new user in the [Azure classic portal](https://manage.windowsazure.com/), or other portals such as the Office 365 admin portal.</span></span> <span data-ttu-id="fc2a7-115">Esto simplifica el proceso para que un administrador cree usuarios nuevos en el portal.</span><span class="sxs-lookup"><span data-stu-id="fc2a7-115">This streamlines the process for an administrator to create new users in the portal.</span></span>

<span data-ttu-id="fc2a7-116">Para cambiar el nombre de dominio principal para el directorio:</span><span class="sxs-lookup"><span data-stu-id="fc2a7-116">To change the primary domain name for your directory:</span></span>

1. <span data-ttu-id="fc2a7-117">Inicie sesión en el [Portal de Azure clásico](https://manage.windowsazure.com/) con una cuenta de usuario que sea administrador global de su directorio de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="fc2a7-117">Sign in to the [Azure classic portal](https://manage.windowsazure.com/) with a user account that is a global administrator of your Azure AD directory.</span></span>
2. <span data-ttu-id="fc2a7-118">Seleccione **Active Directory** en la barra de navegación de la izquierda.</span><span class="sxs-lookup"><span data-stu-id="fc2a7-118">Select **Active Directory** on the left navigation bar.</span></span>
3. <span data-ttu-id="fc2a7-119">Abra el directorio.</span><span class="sxs-lookup"><span data-stu-id="fc2a7-119">Open your directory.</span></span>
4. <span data-ttu-id="fc2a7-120">Seleccione la pestaña **Dominios** .</span><span class="sxs-lookup"><span data-stu-id="fc2a7-120">Select the **Domains** tab.</span></span>
5. <span data-ttu-id="fc2a7-121">Seleccione el botón **Cambiar principal** en la barra de comandos.</span><span class="sxs-lookup"><span data-stu-id="fc2a7-121">Select the **Change primary** button on the command bar.</span></span>
6. <span data-ttu-id="fc2a7-122">Seleccione el dominio que desea convertir en el nuevo dominio principal para el directorio.</span><span class="sxs-lookup"><span data-stu-id="fc2a7-122">Select the domain that you want to be the new primary domain for your directory.</span></span>

<span data-ttu-id="fc2a7-123">Puede cambiar el nombre de dominio principal para el directorio de modo que sea cualquier dominio personalizado comprobado que no esté federado.</span><span class="sxs-lookup"><span data-stu-id="fc2a7-123">You can change the primary domain name for your directory to be any verified custom domain that is not federated.</span></span> <span data-ttu-id="fc2a7-124">El hecho de cambiar el dominio principal para el directorio no cambiará los nombres de usuario existentes.</span><span class="sxs-lookup"><span data-stu-id="fc2a7-124">Changing the primary domain for your directory will not change the user names for any existing users.</span></span>

## <a name="add-custom-domain-names-to-your-azure-ad"></a><span data-ttu-id="fc2a7-125">Adición de dominios personalizados a Azure AD</span><span class="sxs-lookup"><span data-stu-id="fc2a7-125">Add custom domain names to your Azure AD</span></span>
<span data-ttu-id="fc2a7-126">Puede agregar hasta 900 nombres de dominio personalizado a cada directorio de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="fc2a7-126">You can add up to 900 custom domain names to each Azure AD directory.</span></span> <span data-ttu-id="fc2a7-127">El proceso de [agregar un nombre de dominio personalizado adicional](active-directory-add-domain.md) es igual para el primer nombre de dominio personalizado.</span><span class="sxs-lookup"><span data-stu-id="fc2a7-127">The process to [add an additional custom domain name](active-directory-add-domain.md) is the same for the first custom domain name.</span></span>

## <a name="add-subdomains-of-a-custom-domain"></a><span data-ttu-id="fc2a7-128">Adición de subdominios de un dominio personalizado</span><span class="sxs-lookup"><span data-stu-id="fc2a7-128">Add subdomains of a custom domain</span></span>
<span data-ttu-id="fc2a7-129">Si desea agregar un nombre de dominio de tercer nivel, como "europe.contoso.com", a su directorio, primero debe agregar y comprobar el dominio de segundo nivel, como contoso.com.</span><span class="sxs-lookup"><span data-stu-id="fc2a7-129">If you want to add a third-level domain name such as ‘europe.contoso.com’ to your directory, you should first add and verify the second-level domain, such as contoso.com.</span></span> <span data-ttu-id="fc2a7-130">Azure AD comprobará automáticamente el subdominio.</span><span class="sxs-lookup"><span data-stu-id="fc2a7-130">The subdomain will be automatically verified by Azure AD.</span></span> <span data-ttu-id="fc2a7-131">Para ver que se ha comprobado el subdominio que acaba de agregar, actualice la página del explorador que muestra los dominios en el directorio.</span><span class="sxs-lookup"><span data-stu-id="fc2a7-131">To see that the subdomain that you just added has been verified, refresh the page in the browser that lists the domains in your directory.</span></span>

## <a name="what-to-do-if-you-change-the-dns-registrar-for-your-custom-domain-name"></a><span data-ttu-id="fc2a7-132">Qué hacer si se cambia el registrador DNS del nombre de dominio personalizado</span><span class="sxs-lookup"><span data-stu-id="fc2a7-132">What to do if you change the DNS registrar for your custom domain name</span></span>
<span data-ttu-id="fc2a7-133">Si solo cambia el registrador DNS para el nombre de dominio personalizado, puede continuar usando el nombre de dominio personalizado con el propio Azure AD sin interrupción y sin tareas de configuración adicionales.</span><span class="sxs-lookup"><span data-stu-id="fc2a7-133">If you change the DNS registrar for your custom domain name, you can continue to use your custom domain name with Azure AD itself without interruption and without additional configuration tasks.</span></span> <span data-ttu-id="fc2a7-134">Si usa el nombre de dominio personalizado con Office 365, Intune u otros servicios que dependan de los nombres de dominio personalizados en Azure AD, consulte la documentación de dichos servicios.</span><span class="sxs-lookup"><span data-stu-id="fc2a7-134">If you use your custom domain name with Office 365, Intune, or other services that rely on custom domain names in Azure AD, refer to the documentation for those services.</span></span>

## <a name="delete-a-custom-domain-name"></a><span data-ttu-id="fc2a7-135">Eliminación de un nombre de dominio personalizado</span><span class="sxs-lookup"><span data-stu-id="fc2a7-135">Delete a custom domain name</span></span>
<span data-ttu-id="fc2a7-136">Puede eliminar un nombre de dominio personalizado de Azure AD si su organización ya no utiliza ese nombre de dominio o si necesita utilizar ese nombre de dominio con otro Azure AD.</span><span class="sxs-lookup"><span data-stu-id="fc2a7-136">You can delete a custom domain name from your Azure AD if your organization no longer uses that domain name, or if you need to use that domain name with another Azure AD.</span></span>

<span data-ttu-id="fc2a7-137">Para eliminar un nombre de dominio personalizado, primero debe asegurarse de que no haya recursos en el directorio que se basen en el nombre de dominio.</span><span class="sxs-lookup"><span data-stu-id="fc2a7-137">To delete a custom domain name, you must first ensure that no resources in your directory rely on the domain name.</span></span> <span data-ttu-id="fc2a7-138">No puede eliminar un nombre de dominio de su directorio si:</span><span class="sxs-lookup"><span data-stu-id="fc2a7-138">You can't delete a domain name from your directory if:</span></span>

* <span data-ttu-id="fc2a7-139">Algún usuario tiene un nombre de usuario, una dirección de correo electrónico o una dirección de proxy que incluyan el nombre de dominio.</span><span class="sxs-lookup"><span data-stu-id="fc2a7-139">Any user has a user name, email address, or proxy address that include the domain name.</span></span>
* <span data-ttu-id="fc2a7-140">Algún grupo tiene una dirección de correo electrónico o una dirección de proxy que incluya el nombre de dominio.</span><span class="sxs-lookup"><span data-stu-id="fc2a7-140">Any group has an email address or proxy address that includes the domain name.</span></span>
* <span data-ttu-id="fc2a7-141">Alguna aplicación en Azure AD tiene un URI de identificador de aplicación que incluya el nombre de dominio.</span><span class="sxs-lookup"><span data-stu-id="fc2a7-141">Any application in your Azure AD has an app ID URI that includes the domain name.</span></span>

<span data-ttu-id="fc2a7-142">Debe cambiar o eliminar dichos recursos en su directorio Azure AD para poder eliminar el nombre de dominio personalizado.</span><span class="sxs-lookup"><span data-stu-id="fc2a7-142">You must change or delete any such resource in your Azure AD directory before you can delete the custom domain name.</span></span>

## <a name="use-powershell-or-graph-api-to-manage-domain-names"></a><span data-ttu-id="fc2a7-143">Utilización de PowerShell o API Graph para administrar nombres de dominio</span><span class="sxs-lookup"><span data-stu-id="fc2a7-143">Use PowerShell or Graph API to manage domain names</span></span>
<span data-ttu-id="fc2a7-144">También se pueden completar la mayoría de las tareas de administración para los nombres de dominio de Azure Active Directory mediante Microsoft PowerShell, o mediante programación utilizando la API de Azure Graph.</span><span class="sxs-lookup"><span data-stu-id="fc2a7-144">Most management tasks for domain names in Azure Active Directory can also be completed using Microsoft PowerShell, or programmatically using Azure AD Graph API.</span></span>

* [<span data-ttu-id="fc2a7-145">Utilización de PowerShell para administrar los nombres de dominio en Azure AD</span><span class="sxs-lookup"><span data-stu-id="fc2a7-145">Using PowerShell to manage domain names in Azure AD</span></span>](https://msdn.microsoft.com/library/azure/e1ef403f-3347-4409-8f46-d72dafa116e0#BKMK_ManageDomains)
* [<span data-ttu-id="fc2a7-146">Using Graph API to manage domain names in Azure AD (Uso de la API Graph para administrar nombres de dominio en Azure AD)</span><span class="sxs-lookup"><span data-stu-id="fc2a7-146">Using Graph API to manage domain names in Azure AD</span></span>](https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/domains-operations)

## <a name="next-steps"></a><span data-ttu-id="fc2a7-147">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="fc2a7-147">Next steps</span></span>
* [<span data-ttu-id="fc2a7-148">Obtenga más información acerca de los nombres de dominio en Azure AD</span><span class="sxs-lookup"><span data-stu-id="fc2a7-148">Learn about domain names in Azure AD</span></span>](active-directory-add-domain-concepts.md)
* [<span data-ttu-id="fc2a7-149">Managing custom domain names (Administración de nombres de dominio).</span><span class="sxs-lookup"><span data-stu-id="fc2a7-149">Manage custom domain names</span></span>](active-directory-add-manage-domain-names.md)

