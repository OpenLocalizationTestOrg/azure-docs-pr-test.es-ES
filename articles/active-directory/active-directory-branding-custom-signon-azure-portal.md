---
title: "Personalización de la página de inicio de sesión de Azure Active Directory | Microsoft Docs"
description: "Aprenda a agregar una personalización de marca de empresa a la página de inicio de sesión de Azure"
services: active-directory
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: f8b932bc-8b4f-42b5-a2d3-f2c076234a78
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/04/2017
ms.author: curtand
ms.openlocfilehash: 27590c018ea55e9793246c7a4cab10f934ea502b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="add-company-branding-to-your-sign-in-page-in-the-azure-active-directory"></a><span data-ttu-id="99e5c-103">Adición de personalización de marca de empresa a la página de inicio de sesión de Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="99e5c-103">Add company branding to your sign-in page in the Azure Active Directory</span></span>
<span data-ttu-id="99e5c-104">Para evitar confusiones, muchas empresas quieren aplicar un aspecto coherente en todos los sitios web y servicios que administran.</span><span class="sxs-lookup"><span data-stu-id="99e5c-104">To avoid confusion, many companies want to apply a consistent look and feel across all the websites and services they manage.</span></span> <span data-ttu-id="99e5c-105">Azure Active Directory ofrece esta funcionalidad, ya que permite personalizar la apariencia de la página de inicio de sesión con esquemas de color personalizados y el logotipo de la empresa.</span><span class="sxs-lookup"><span data-stu-id="99e5c-105">Azure Active Directory provides this capability by allowing you to customize the appearance of the sign-in page with your company logo and custom color schemes.</span></span> <span data-ttu-id="99e5c-106">Se trata de la página que aparece al iniciar sesión en Office 365 u otras aplicaciones web que estén utilizando Azure AD como proveedor de identidades.</span><span class="sxs-lookup"><span data-stu-id="99e5c-106">The sign-in page is the page that appears when you sign in to Office 365 or other web-based applications that are using Azure AD as your identity provider.</span></span> <span data-ttu-id="99e5c-107">Interactuará con esta página para especificar las credenciales.</span><span class="sxs-lookup"><span data-stu-id="99e5c-107">You interact with this page to enter your credentials.</span></span>

<span data-ttu-id="99e5c-108">Si desea mostrar en su página la marca y los colores de su empresa, además de otros elementos personalizables, vea las imágenes siguientes para entender la diferencia entre las dos experiencias.</span><span class="sxs-lookup"><span data-stu-id="99e5c-108">If you want to show your company brand, colors and other customizable elements on this page, see the following images to understand the difference between the two experiences.</span></span>

<span data-ttu-id="99e5c-109">La siguiente captura de pantalla muestra un ejemplo de la página de inicio de sesión de Office 365 en un equipo de escritorio **antes** de una personalización:</span><span class="sxs-lookup"><span data-stu-id="99e5c-109">The following screenshot shows and example for the Office 365 sign-in page on a desktop computer **before** a customization:</span></span>

![Página de inicio de sesión de Office 365 antes de la personalización](./media/active-directory-branding-custom-signon-azure-portal/sign-in-page-before-customization.png)

<span data-ttu-id="99e5c-111">La siguiente captura de pantalla muestra un ejemplo de la página de inicio de sesión de Office 365 en un equipo de escritorio **después** de una personalización:</span><span class="sxs-lookup"><span data-stu-id="99e5c-111">The following screenshot shows and example for the Office 365 sign-in page on a desktop computer **after** a customization:</span></span>

![Página de inicio de sesión de Office 365 después de la personalización](./media/active-directory-branding-custom-signon-azure-portal/sign-in-page-after-customization.png)

## <a name="customizing-the-sign-in-page"></a><span data-ttu-id="99e5c-113">Personalización de la página de inicio de sesión</span><span class="sxs-lookup"><span data-stu-id="99e5c-113">Customizing the sign-in page</span></span>
<span data-ttu-id="99e5c-114">Normalmente, si necesita acceso basado en explorador a las aplicaciones y servicios en la nube a los que está suscrita su organización, utiliza la página de inicio de sesión.</span><span class="sxs-lookup"><span data-stu-id="99e5c-114">Typically, if you need browser-based access to your cloud apps and services that your organization subscribes to, you use the sign-in page.</span></span>

<span data-ttu-id="99e5c-115">Si ha aplicado cambios a la página de inicio de sesión, puede tardar hasta una hora para que aparezcan.</span><span class="sxs-lookup"><span data-stu-id="99e5c-115">If you have applied changes to your sign-in page, it can take up to an hour for the changes to appear.</span></span>

<span data-ttu-id="99e5c-116">Las páginas de inicio de sesión con marca solamente aparecen cuando se visita un servicio con una dirección URL específica del inquilino, como https://outlook.com/**contoso**.com o https://mail.**contoso**.com.</span><span class="sxs-lookup"><span data-stu-id="99e5c-116">A branded sign-in page only appears when you visit a service with a tenant-specific URL such as https://outlook.com/**contoso**.com, or https://mail.**contoso**.com.</span></span>

<span data-ttu-id="99e5c-117">Si visita un servicio con direcciones URL que no son específicas de un inquilino (por ejemplo, https://mail.office365.com), aparece una página de inicio de sesión sin marca.</span><span class="sxs-lookup"><span data-stu-id="99e5c-117">When you visit a service with non-tenant specific URLs (e.g.: https://mail.office365.com), a non-branded sign-in page appears.</span></span> <span data-ttu-id="99e5c-118">En este caso, la marca solamente aparecerá una vez que haya especificado el identificador de usuario o haya seleccionado un icono de usuario.</span><span class="sxs-lookup"><span data-stu-id="99e5c-118">in this case, your branding appears once you have entered your user ID or you have selected a user tile.</span></span>

> [!NOTE]
> * <span data-ttu-id="99e5c-119">El nombre de usuario debe aparecer como "activo" en la parte **Dominios** de Azure Portal donde ha configurado la personalización de marca.</span><span class="sxs-lookup"><span data-stu-id="99e5c-119">Your domain name must appear as “Active" in the **Domains** portion of the Azure portal in which you have configured branding.</span></span> <span data-ttu-id="99e5c-120">Para más información, consulte [cómo agregar nombres de dominio personalizados](active-directory-domains-add-azure-portal.md).</span><span class="sxs-lookup"><span data-stu-id="99e5c-120">For more information, see [Add custom domain names](active-directory-domains-add-azure-portal.md).</span></span>
> * <span data-ttu-id="99e5c-121">La personalización de marca de la página de inicio de sesión no se traslada a la página de inicio de sesión de cliente de Microsoft.</span><span class="sxs-lookup"><span data-stu-id="99e5c-121">Sign-in page branding doesn’t carry over to the consumer sign in page of Microsoft.</span></span> <span data-ttu-id="99e5c-122">Si inicia sesión con una cuenta de Microsoft, puede ver una lista de iconos de usuario con la personalización de marca presentada por Azure AD, pero la personalización de marca de su organización no se aplica a la página de inicio de sesión de la cuenta de Microsoft.</span><span class="sxs-lookup"><span data-stu-id="99e5c-122">If you sign in with a Microsoft account, you may see a branded list of user tiles rendered by Azure AD, but the branding of your organization does not apply to the Microsoft account sign-in page.</span></span>
>
>

<span data-ttu-id="99e5c-123">En la página de inicio de sesión, la casilla **Mantener la sesión iniciada** permite que el usuario se mantenga conectado después de cerrar y abrir de nuevo el explorador.</span><span class="sxs-lookup"><span data-stu-id="99e5c-123">On your sign-in page, the **Keep me signed in** checkbox allows a user to remain signed in when they close and re-open their browser.</span></span>

   ![Mantener la sesión iniciada](./media/active-directory-branding-custom-signon-azure-portal/01.png)

<span data-ttu-id="99e5c-125">No afecta a la duración de la sesión.</span><span class="sxs-lookup"><span data-stu-id="99e5c-125">It does not effect session lifetime.</span></span> <span data-ttu-id="99e5c-126">Puede ocultar la casilla en la página de inicio de sesión de Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="99e5c-126">You can hide the checkbox on the Azure Active Directory sign-in page.</span></span>
<span data-ttu-id="99e5c-127">Puede decidir si se muestra la casilla o no mediante la configuración de **Se deshabilitó la opción Mantener la sesión iniciada**.</span><span class="sxs-lookup"><span data-stu-id="99e5c-127">Whether the checkbox is displayed depends on the setting of **Keep me signed in disabled**.</span></span>

   ![Mantener la sesión iniciada](./media/active-directory-branding-custom-signon-azure-portal/02.png)

<span data-ttu-id="99e5c-129">Para ocultar la casilla, seleccione **Sí** en esta opción.</span><span class="sxs-lookup"><span data-stu-id="99e5c-129">To hide the checkbox, configure this setting to **Yes**.</span></span>

> [!NOTE]
> <span data-ttu-id="99e5c-130">Algunas características de SharePoint Online y Office 2010 dependen de que los usuarios puedan activar esta casilla.</span><span class="sxs-lookup"><span data-stu-id="99e5c-130">Some features of SharePoint Online and Office 2010 depend on users being able to check this box.</span></span> <span data-ttu-id="99e5c-131">Si configura esta opción en oculto, es posible que los usuarios reciban solicitudes adicionales e inesperadas de inicio de sesión.</span><span class="sxs-lookup"><span data-stu-id="99e5c-131">If you configure this setting to hidden, your users may see additional and unexpected prompts to sign-in.</span></span>
>
>

<span data-ttu-id="99e5c-132">**Para agregar la información de marca de empresa a su directorio:**</span><span class="sxs-lookup"><span data-stu-id="99e5c-132">**To add company branding to your directory:**</span></span>

1. <span data-ttu-id="99e5c-133">Inicie sesión en [Azure Portal](https://portal.azure.com) con una cuenta que tenga el rol de administrador global en el directorio.</span><span class="sxs-lookup"><span data-stu-id="99e5c-133">Sign in to the [Azure portal](https://portal.azure.com) with an account that's a global admin for the directory.</span></span>
2. <span data-ttu-id="99e5c-134">Seleccione **Más servicios**, escriba **Usuarios y grupos** en el cuadro de texto y presione **Entrar**.</span><span class="sxs-lookup"><span data-stu-id="99e5c-134">Select **More services**, enter **Users and groups** in the text box, and then select **Enter**.</span></span>

   ![Apertura de Administración de usuarios](./media/active-directory-branding-custom-signon-azure-portal/user-management.png)
3. <span data-ttu-id="99e5c-136">En la hoja **Usuarios y grupos**, seleccione **Personalización de marca de empresa**.</span><span class="sxs-lookup"><span data-stu-id="99e5c-136">On the **Users and groups** blade, select **Company branding**.</span></span>
4. <span data-ttu-id="99e5c-137">En la hoja **Usuarios y grupos - Personalización de marca de empresa**, seleccione el comando **Editar**.</span><span class="sxs-lookup"><span data-stu-id="99e5c-137">On the **Users and groups - Company branding** blade, select the **Edit** command.</span></span>

    ![Edición de la personalización de marca](./media/active-directory-branding-custom-signon-azure-portal/edit-branding.png)
5. <span data-ttu-id="99e5c-139">Modifique los elementos que desea personalizar.</span><span class="sxs-lookup"><span data-stu-id="99e5c-139">Modify the elements you want to customize.</span></span> <span data-ttu-id="99e5c-140">Todos los elementos son opcionales.</span><span class="sxs-lookup"><span data-stu-id="99e5c-140">All elements are optional.</span></span>
6. <span data-ttu-id="99e5c-141">Haga clic en **Save**.</span><span class="sxs-lookup"><span data-stu-id="99e5c-141">Click **Save**.</span></span>

<span data-ttu-id="99e5c-142">Puede transcurrir hasta una hora para que los cambios efectuados se muestren en la personalización de marca de la página de inicio de sesión.</span><span class="sxs-lookup"><span data-stu-id="99e5c-142">It can take up to an hour for any changes you made to the sign-in page branding to appear.</span></span>

## <a name="next-steps"></a><span data-ttu-id="99e5c-143">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="99e5c-143">Next steps</span></span>
[<span data-ttu-id="99e5c-144">Agregar información de marca de empresa específica de un idioma</span><span class="sxs-lookup"><span data-stu-id="99e5c-144">Add language-specific company branding</span></span>](active-directory-branding-localize-azure-portal.md)
