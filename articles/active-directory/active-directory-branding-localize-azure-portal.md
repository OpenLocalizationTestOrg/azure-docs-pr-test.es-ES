---
title: "marcas tooyour página de inicio de sesión en hello Azure Active Directory de empresa de lenguaje específicas de aaaAdd | Documentos de Microsoft"
description: "Obtenga información acerca de cómo tooadd un idioma específico y la compañía fotografías de personalización de marca tooan el inicio de sesión Azure en la página de texto"
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
ms.openlocfilehash: 1e33c31abc242e8455290beb1f03760be7b9ac42
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="add-language-specific-company-branding-tooyour-sign-in-page-in-hello-azure-active-directory"></a><span data-ttu-id="879a7-103">Agregar marcas tooyour página de inicio de sesión en hello Azure Active Directory de empresa específicas de idioma</span><span class="sxs-lookup"><span data-stu-id="879a7-103">Add language-specific company branding tooyour sign-in page in hello Azure Active Directory</span></span>
<span data-ttu-id="879a7-104">tooavoid confusión, muchas compañías desean tooapply una apariencia coherente en todos los sitios Web de Hola y servicios que administran.</span><span class="sxs-lookup"><span data-stu-id="879a7-104">tooavoid confusion, many companies want tooapply a consistent look and feel across all hello websites and services they manage.</span></span> <span data-ttu-id="879a7-105">Azure Active Directory ofrece esta funcionalidad permitiéndole apariencia de hello toocustomize de página de inicio de sesión de hello con el logotipo de la compañía y combinaciones de colores personalizadas.</span><span class="sxs-lookup"><span data-stu-id="879a7-105">Azure Active Directory provides this capability by allowing you toocustomize hello appearance of hello sign-in page with your company logo and custom color schemes.</span></span> <span data-ttu-id="879a7-106">página de inicio de sesión de Hello es la página de Hola que aparece al iniciar sesión en tooOffice 365 u otras aplicaciones basadas en web que usan Azure AD como proveedor de identidades.</span><span class="sxs-lookup"><span data-stu-id="879a7-106">hello sign-in page is hello page that appears when you sign in tooOffice 365 or other web-based applications that are using Azure AD as your identity provider.</span></span> <span data-ttu-id="879a7-107">Interactuar con este tooenter página sus credenciales.</span><span class="sxs-lookup"><span data-stu-id="879a7-107">You interact with this page tooenter your credentials.</span></span>

## <a name="customizing-hello-sign-in-page-for-another-language"></a><span data-ttu-id="879a7-108">Personalizar la página de inicio de sesión de Hola para otro idioma</span><span class="sxs-lookup"><span data-stu-id="879a7-108">Customizing hello sign-in page for another language</span></span>
<span data-ttu-id="879a7-109">Puede agregar elementos específicos del idioma tooyour inicio de sesión página personalizada sólo si ya ha creado una página de inicio de sesión personalizada tal y como se describe en [Agregar página de inicio de sesión tooyour de personalización de marca de empresa](active-directory-branding-custom-signon-azure-portal.md).</span><span class="sxs-lookup"><span data-stu-id="879a7-109">You can add language-specific elements tooyour custom sign-in page only if you have already created a custom sign-in page as described in [Add company branding tooyour sign-in page](active-directory-branding-custom-signon-azure-portal.md).</span></span> <span data-ttu-id="879a7-110">Puede configurar una página de inicio de sesión por directorio con un conjunto predeterminado de elementos personalizables.</span><span class="sxs-lookup"><span data-stu-id="879a7-110">You can configure one sign-in page per directory with a default set of customizable elements.</span></span> <span data-ttu-id="879a7-111">Después de configurar el conjunto de elementos de la página de hello predeterminado, puede configurar más versiones para diferentes configuraciones regionales.</span><span class="sxs-lookup"><span data-stu-id="879a7-111">After you’ve configured hello default set of page elements, you can configure more versions for different locales.</span></span> <span data-ttu-id="879a7-112">También puede mezclar y hacer coincidir varios elementos.</span><span class="sxs-lookup"><span data-stu-id="879a7-112">You can also mix and match various elements.</span></span> <span data-ttu-id="879a7-113">Por ejemplo, podría realizar estas acciones:</span><span class="sxs-lookup"><span data-stu-id="879a7-113">For example, you could:</span></span>

* <span data-ttu-id="879a7-114">Crear una **imagen de página de inicio de sesión** predeterminada que funcione en todas las referencias culturales y, después, crear versiones específicas para inglés y francés.</span><span class="sxs-lookup"><span data-stu-id="879a7-114">Create a default **Sign-in page image** that works for all cultures, then create specific versions for English and French.</span></span> <span data-ttu-id="879a7-115">Cuando se establece su tooone de exploradores de estos dos idiomas, Hola específicos del idioma imagen aparece, mientras ilustración de hello predeterminada aparece para todos los demás lenguajes.</span><span class="sxs-lookup"><span data-stu-id="879a7-115">When you set your browsers tooone of these two languages, hello language-specific image appears, while hello default illustration appears for all other languages.</span></span>
* <span data-ttu-id="879a7-116">Configure logotipos diferentes para su organización (por ejemplo, para las versiones en japonés o hebreo).</span><span class="sxs-lookup"><span data-stu-id="879a7-116">Configure different logos for your organization (for example, Japanese or Hebrew versions).</span></span>

<span data-ttu-id="879a7-117">Se recomienda que mantenga número Hola de las variaciones de lenguajes bajo, por motivos de mantenimiento y rendimiento.</span><span class="sxs-lookup"><span data-stu-id="879a7-117">We recommend that you keep hello number of language variations low, for maintenance and performance reasons.</span></span>

<span data-ttu-id="879a7-118">**tooadd marca tooyour directorio de la empresa:**</span><span class="sxs-lookup"><span data-stu-id="879a7-118">**tooadd company branding tooyour directory:**</span></span>

1. <span data-ttu-id="879a7-119">Inicie sesión en toohello [portal de Azure](https://portal.azure.com) con una cuenta que sea un administrador global para el directorio de Hola.</span><span class="sxs-lookup"><span data-stu-id="879a7-119">Sign in toohello [Azure portal](https://portal.azure.com) with an account that's a global admin for hello directory.</span></span>
2. <span data-ttu-id="879a7-120">Seleccione **más servicios**, escriba **usuarios y grupos** en Hola cuadro de texto y, a continuación, seleccione **ENTRAR**.</span><span class="sxs-lookup"><span data-stu-id="879a7-120">Select **More services**, enter **Users and groups** in hello text box, and then select **Enter**.</span></span>

   ![Apertura de Administración de usuarios](./media/active-directory-branding-localize-azure-portal/user-management.png)
3. <span data-ttu-id="879a7-122">En hello **usuarios y grupos** hoja, seleccione **información de marca**.</span><span class="sxs-lookup"><span data-stu-id="879a7-122">On hello **Users and groups** blade, select **Company branding**.</span></span>
4. <span data-ttu-id="879a7-123">En hello **a los usuarios y grupos: personalización de marca de empresa** hoja, seleccione hello **Agregar idioma** comando.</span><span class="sxs-lookup"><span data-stu-id="879a7-123">On hello **Users and groups - Company branding** blade, select hello **Add language** command.</span></span>

    ![Adición de elementos de personalización de marca específicos del idioma](./media/active-directory-branding-localize-azure-portal/add-language.png)
5. <span data-ttu-id="879a7-125">Modificar elementos de hello desea toocustomize.</span><span class="sxs-lookup"><span data-stu-id="879a7-125">Modify hello elements you want toocustomize.</span></span> <span data-ttu-id="879a7-126">Todos los elementos son opcionales.</span><span class="sxs-lookup"><span data-stu-id="879a7-126">All elements are optional.</span></span>
6. <span data-ttu-id="879a7-127">Haga clic en **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="879a7-127">Click **Save**.</span></span>

<span data-ttu-id="879a7-128">Puede tardar hasta hora tooan para cualquier cambio realizado toohello inicio de sesión página tooappear personalización de marca.</span><span class="sxs-lookup"><span data-stu-id="879a7-128">It can take up tooan hour for any changes you made toohello sign-in page branding tooappear.</span></span>

## <a name="next-steps"></a><span data-ttu-id="879a7-129">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="879a7-129">Next steps</span></span>
[<span data-ttu-id="879a7-130">Agregar marcas tooyour página de inicio de sesión de empresa</span><span class="sxs-lookup"><span data-stu-id="879a7-130">Add company branding tooyour sign-in page</span></span>](active-directory-branding-custom-signon-azure-portal.md)
