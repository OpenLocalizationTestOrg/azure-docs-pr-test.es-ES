---
title: "Adición de personalización de marca de empresa específica del lenguaje a la página de inicio de sesión en Azure Active Directory | Microsoft Docs"
description: "Sepa cómo agregar imágenes y texto de personalización de marca específicos del idioma a una página de inicio de sesión de Azure."
services: active-directory
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: a0310d6a-aaa7-4ea0-991d-6d3135b4382a
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/04/2017
ms.author: curtand
ms.openlocfilehash: e1fe8d855386ceec39edbc985538cdf32d78a13b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="add-language-specific-company-branding-to-your-sign-in-page-in-the-azure-active-directory"></a><span data-ttu-id="28b28-103">Adición de personalización de marca de empresa específica del lenguaje a la página de inicio de sesión en Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="28b28-103">Add language-specific company branding to your sign-in page in the Azure Active Directory</span></span>
<span data-ttu-id="28b28-104">Para evitar confusiones, muchas empresas quieren aplicar un aspecto coherente en todos los sitios web y servicios que administran.</span><span class="sxs-lookup"><span data-stu-id="28b28-104">To avoid confusion, many companies want to apply a consistent look and feel across all the websites and services they manage.</span></span> <span data-ttu-id="28b28-105">Azure Active Directory ofrece esta funcionalidad, ya que permite personalizar la apariencia de la página de inicio de sesión con esquemas de color personalizados y el logotipo de la empresa.</span><span class="sxs-lookup"><span data-stu-id="28b28-105">Azure Active Directory provides this capability by allowing you to customize the appearance of the sign-in page with your company logo and custom color schemes.</span></span> <span data-ttu-id="28b28-106">Se trata de la página que aparece al iniciar sesión en Office 365 u otras aplicaciones web que estén utilizando Azure AD como proveedor de identidades.</span><span class="sxs-lookup"><span data-stu-id="28b28-106">The sign-in page is the page that appears when you sign in to Office 365 or other web-based applications that are using Azure AD as your identity provider.</span></span> <span data-ttu-id="28b28-107">Interactuará con esta página para especificar las credenciales.</span><span class="sxs-lookup"><span data-stu-id="28b28-107">You interact with this page to enter your credentials.</span></span>

## <a name="customizing-the-sign-in-page-for-another-language"></a><span data-ttu-id="28b28-108">Personalización de la página de inicio de sesión para otro idioma</span><span class="sxs-lookup"><span data-stu-id="28b28-108">Customizing the sign-in page for another language</span></span>
<span data-ttu-id="28b28-109">Solo podrá agregar elementos específicos del idioma a la página de inicio de sesión personalizada si ya ha creado una página de inicio de sesión personalizada tal y como se describe en el artículo sobre cómo [agregar personalización de marca de empresa a la página de inicio de sesión](active-directory-branding-custom-signon-azure-portal.md).</span><span class="sxs-lookup"><span data-stu-id="28b28-109">You can add language-specific elements to your custom sign-in page only if you have already created a custom sign-in page as described in [Add company branding to your sign-in page](active-directory-branding-custom-signon-azure-portal.md).</span></span> <span data-ttu-id="28b28-110">Puede configurar una página de inicio de sesión por directorio con un conjunto predeterminado de elementos personalizables.</span><span class="sxs-lookup"><span data-stu-id="28b28-110">You can configure one sign-in page per directory with a default set of customizable elements.</span></span> <span data-ttu-id="28b28-111">Cuando haya configurado el conjunto predeterminado de elementos de página, podrá ajustar más versiones para las diferentes configuraciones regionales.</span><span class="sxs-lookup"><span data-stu-id="28b28-111">After you’ve configured the default set of page elements, you can configure more versions for different locales.</span></span> <span data-ttu-id="28b28-112">También puede mezclar y hacer coincidir varios elementos.</span><span class="sxs-lookup"><span data-stu-id="28b28-112">You can also mix and match various elements.</span></span> <span data-ttu-id="28b28-113">Por ejemplo, podría realizar estas acciones:</span><span class="sxs-lookup"><span data-stu-id="28b28-113">For example, you could:</span></span>

* <span data-ttu-id="28b28-114">Crear una **imagen de página de inicio de sesión** predeterminada que funcione en todas las referencias culturales y, después, crear versiones específicas para inglés y francés.</span><span class="sxs-lookup"><span data-stu-id="28b28-114">Create a default **Sign-in page image** that works for all cultures, then create specific versions for English and French.</span></span> <span data-ttu-id="28b28-115">Al establecer los exploradores en uno de estos dos idiomas, aparece la imagen específica del idioma, mientras que la ilustración predeterminada se muestra en los demás idiomas.</span><span class="sxs-lookup"><span data-stu-id="28b28-115">When you set your browsers to one of these two languages, the language-specific image appears, while the default illustration appears for all other languages.</span></span>
* <span data-ttu-id="28b28-116">Configure logotipos diferentes para su organización (por ejemplo, para las versiones en japonés o hebreo).</span><span class="sxs-lookup"><span data-stu-id="28b28-116">Configure different logos for your organization (for example, Japanese or Hebrew versions).</span></span>

<span data-ttu-id="28b28-117">Por motivos de rendimiento y mantenimiento, se recomienda mantener un número de variantes de idioma reducido.</span><span class="sxs-lookup"><span data-stu-id="28b28-117">We recommend that you keep the number of language variations low, for maintenance and performance reasons.</span></span>

<span data-ttu-id="28b28-118">**Para agregar la información de marca de empresa a su directorio:**</span><span class="sxs-lookup"><span data-stu-id="28b28-118">**To add company branding to your directory:**</span></span>

1. <span data-ttu-id="28b28-119">Inicie sesión en [Azure Portal](https://portal.azure.com) con una cuenta que tenga el rol de administrador global en el directorio.</span><span class="sxs-lookup"><span data-stu-id="28b28-119">Sign in to the [Azure portal](https://portal.azure.com) with an account that's a global admin for the directory.</span></span>
2. <span data-ttu-id="28b28-120">Seleccione **Más servicios**, escriba **Usuarios y grupos** en el cuadro de texto y presione **Entrar**.</span><span class="sxs-lookup"><span data-stu-id="28b28-120">Select **More services**, enter **Users and groups** in the text box, and then select **Enter**.</span></span>

   ![Apertura de Administración de usuarios](./media/active-directory-branding-localize-azure-portal/user-management.png)
3. <span data-ttu-id="28b28-122">En la hoja **Usuarios y grupos**, seleccione **Personalización de marca de empresa**.</span><span class="sxs-lookup"><span data-stu-id="28b28-122">On the **Users and groups** blade, select **Company branding**.</span></span>
4. <span data-ttu-id="28b28-123">En la hoja **Usuarios y grupos - Personalización de marca de empresa**, seleccione el comando **Agregar idioma**.</span><span class="sxs-lookup"><span data-stu-id="28b28-123">On the **Users and groups - Company branding** blade, select the **Add language** command.</span></span>

    ![Adición de elementos de personalización de marca específicos del idioma](./media/active-directory-branding-localize-azure-portal/add-language.png)
5. <span data-ttu-id="28b28-125">Modifique los elementos que desea personalizar.</span><span class="sxs-lookup"><span data-stu-id="28b28-125">Modify the elements you want to customize.</span></span> <span data-ttu-id="28b28-126">Todos los elementos son opcionales.</span><span class="sxs-lookup"><span data-stu-id="28b28-126">All elements are optional.</span></span>
6. <span data-ttu-id="28b28-127">Haga clic en **Save**.</span><span class="sxs-lookup"><span data-stu-id="28b28-127">Click **Save**.</span></span>

<span data-ttu-id="28b28-128">Puede transcurrir hasta una hora para que los cambios efectuados se muestren en la personalización de marca de la página de inicio de sesión.</span><span class="sxs-lookup"><span data-stu-id="28b28-128">It can take up to an hour for any changes you made to the sign-in page branding to appear.</span></span>

## <a name="next-steps"></a><span data-ttu-id="28b28-129">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="28b28-129">Next steps</span></span>
[<span data-ttu-id="28b28-130">Agregar personalización de marca a la página de inicio de sesión</span><span class="sxs-lookup"><span data-stu-id="28b28-130">Add company branding to your sign-in page</span></span>](active-directory-branding-custom-signon-azure-portal.md)
