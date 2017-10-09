---
title: "aaaCustomize el inicio de sesión en la página en hello Azure Active Directory | Documentos de Microsoft"
description: "Obtenga información acerca de cómo tooadd una página de toohello inicio de sesión Azure de personalización de marca de empresa"
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
ms.openlocfilehash: 151521e3b9cbc6a438a589735058fbff78443cf8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="add-company-branding-tooyour-sign-in-page-in-hello-azure-active-directory"></a><span data-ttu-id="f5e9b-103">Agregar marcas tooyour página de inicio de sesión en hello Azure Active Directory de empresa</span><span class="sxs-lookup"><span data-stu-id="f5e9b-103">Add company branding tooyour sign-in page in hello Azure Active Directory</span></span>
<span data-ttu-id="f5e9b-104">tooavoid confusión, muchas compañías desean tooapply una apariencia coherente en todos los sitios Web de Hola y servicios que administran.</span><span class="sxs-lookup"><span data-stu-id="f5e9b-104">tooavoid confusion, many companies want tooapply a consistent look and feel across all hello websites and services they manage.</span></span> <span data-ttu-id="f5e9b-105">Azure Active Directory ofrece esta funcionalidad permitiéndole apariencia de hello toocustomize de página de inicio de sesión de hello con el logotipo de la compañía y combinaciones de colores personalizadas.</span><span class="sxs-lookup"><span data-stu-id="f5e9b-105">Azure Active Directory provides this capability by allowing you toocustomize hello appearance of hello sign-in page with your company logo and custom color schemes.</span></span> <span data-ttu-id="f5e9b-106">página de inicio de sesión de Hello es la página de Hola que aparece al iniciar sesión en tooOffice 365 u otras aplicaciones basadas en web que usan Azure AD como proveedor de identidades.</span><span class="sxs-lookup"><span data-stu-id="f5e9b-106">hello sign-in page is hello page that appears when you sign in tooOffice 365 or other web-based applications that are using Azure AD as your identity provider.</span></span> <span data-ttu-id="f5e9b-107">Interactuar con este tooenter página sus credenciales.</span><span class="sxs-lookup"><span data-stu-id="f5e9b-107">You interact with this page tooenter your credentials.</span></span>

<span data-ttu-id="f5e9b-108">Si desea que tooshow su marca de empresa, colores y otros elementos personalizables en esta página, vea Hola después imágenes toounderstand Hola diferenciar dos experiencias de Hola.</span><span class="sxs-lookup"><span data-stu-id="f5e9b-108">If you want tooshow your company brand, colors and other customizable elements on this page, see hello following images toounderstand hello difference between hello two experiences.</span></span>

<span data-ttu-id="f5e9b-109">Hola siguiente captura de pantalla muestra y ejemplo de página de inicio de sesión de hello Office 365 en un equipo de escritorio **antes de** una personalización:</span><span class="sxs-lookup"><span data-stu-id="f5e9b-109">hello following screenshot shows and example for hello Office 365 sign-in page on a desktop computer **before** a customization:</span></span>

![Página de inicio de sesión de Office 365 antes de la personalización](./media/active-directory-branding-custom-signon-azure-portal/sign-in-page-before-customization.png)

<span data-ttu-id="f5e9b-111">Hola siguiente captura de pantalla muestra y ejemplo de página de inicio de sesión de hello Office 365 en un equipo de escritorio **después** una personalización:</span><span class="sxs-lookup"><span data-stu-id="f5e9b-111">hello following screenshot shows and example for hello Office 365 sign-in page on a desktop computer **after** a customization:</span></span>

![Página de inicio de sesión de Office 365 después de la personalización](./media/active-directory-branding-custom-signon-azure-portal/sign-in-page-after-customization.png)

## <a name="customizing-hello-sign-in-page"></a><span data-ttu-id="f5e9b-113">Personalizar la página de inicio de sesión de Hola</span><span class="sxs-lookup"><span data-stu-id="f5e9b-113">Customizing hello sign-in page</span></span>
<span data-ttu-id="f5e9b-114">Por lo general, si tiene aplicaciones de acceso basado en explorador tooyour en la nube y los servicios que su organización se suscribe a, utilice página de inicio de sesión de Hola.</span><span class="sxs-lookup"><span data-stu-id="f5e9b-114">Typically, if you need browser-based access tooyour cloud apps and services that your organization subscribes to, you use hello sign-in page.</span></span>

<span data-ttu-id="f5e9b-115">Si ha aplicado la página de inicio de sesión de tooyour de cambios, puede tardar una hora tooan Hola cambios tooappear.</span><span class="sxs-lookup"><span data-stu-id="f5e9b-115">If you have applied changes tooyour sign-in page, it can take up tooan hour for hello changes tooappear.</span></span>

<span data-ttu-id="f5e9b-116">Las páginas de inicio de sesión con marca solamente aparecen cuando se visita un servicio con una dirección URL específica del inquilino, como https://outlook.com/**contoso**.com o https://mail.**contoso**.com.</span><span class="sxs-lookup"><span data-stu-id="f5e9b-116">A branded sign-in page only appears when you visit a service with a tenant-specific URL such as https://outlook.com/**contoso**.com, or https://mail.**contoso**.com.</span></span>

<span data-ttu-id="f5e9b-117">Si visita un servicio con direcciones URL que no son específicas de un inquilino (por ejemplo, https://mail.office365.com), aparece una página de inicio de sesión sin marca.</span><span class="sxs-lookup"><span data-stu-id="f5e9b-117">When you visit a service with non-tenant specific URLs (e.g.: https://mail.office365.com), a non-branded sign-in page appears.</span></span> <span data-ttu-id="f5e9b-118">En este caso, la marca solamente aparecerá una vez que haya especificado el identificador de usuario o haya seleccionado un icono de usuario.</span><span class="sxs-lookup"><span data-stu-id="f5e9b-118">in this case, your branding appears once you have entered your user ID or you have selected a user tile.</span></span>

> [!NOTE]
> * <span data-ttu-id="f5e9b-119">El nombre de dominio debe aparecer como "Activo" Hola **dominios** parte de Hola portal de Azure en el que se ha configurado la marca.</span><span class="sxs-lookup"><span data-stu-id="f5e9b-119">Your domain name must appear as “Active" in hello **Domains** portion of hello Azure portal in which you have configured branding.</span></span> <span data-ttu-id="f5e9b-120">Para más información, consulte [cómo agregar nombres de dominio personalizados](active-directory-domains-add-azure-portal.md).</span><span class="sxs-lookup"><span data-stu-id="f5e9b-120">For more information, see [Add custom domain names](active-directory-domains-add-azure-portal.md).</span></span>
> * <span data-ttu-id="f5e9b-121">Personalización de la página de inicio de sesión no dirige toohello consumidor inicio de sesión en la página de Microsoft.</span><span class="sxs-lookup"><span data-stu-id="f5e9b-121">Sign-in page branding doesn’t carry over toohello consumer sign in page of Microsoft.</span></span> <span data-ttu-id="f5e9b-122">Si inicia sesión con una cuenta de Microsoft, puede ver una lista con marca de mosaicos de los usuarios presentada por Azure AD, pero Hola la marca de su organización no aplicará toohello página de inicio de sesión de cuenta de Microsoft.</span><span class="sxs-lookup"><span data-stu-id="f5e9b-122">If you sign in with a Microsoft account, you may see a branded list of user tiles rendered by Azure AD, but hello branding of your organization does not apply toohello Microsoft account sign-in page.</span></span>
>
>

<span data-ttu-id="f5e9b-123">En la página de inicio de sesión, Hola **mantener la sesión iniciada** casilla permite un tooremain usuario inicie sesión cuando cierre y vuelva a abre su explorador.</span><span class="sxs-lookup"><span data-stu-id="f5e9b-123">On your sign-in page, hello **Keep me signed in** checkbox allows a user tooremain signed in when they close and re-open their browser.</span></span>

   ![Mantener la sesión iniciada](./media/active-directory-branding-custom-signon-azure-portal/01.png)

<span data-ttu-id="f5e9b-125">No afecta a la duración de la sesión.</span><span class="sxs-lookup"><span data-stu-id="f5e9b-125">It does not effect session lifetime.</span></span> <span data-ttu-id="f5e9b-126">Puede ocultar Hola casilla en la página de inicio de sesión de Azure Active Directory de Hola.</span><span class="sxs-lookup"><span data-stu-id="f5e9b-126">You can hide hello checkbox on hello Azure Active Directory sign-in page.</span></span>
<span data-ttu-id="f5e9b-127">Si se muestra la casilla de verificación de hello depende de la configuración de Hola de **mantener la sesión iniciada en deshabilitado**.</span><span class="sxs-lookup"><span data-stu-id="f5e9b-127">Whether hello checkbox is displayed depends on hello setting of **Keep me signed in disabled**.</span></span>

   ![Mantener la sesión iniciada](./media/active-directory-branding-custom-signon-azure-portal/02.png)

<span data-ttu-id="f5e9b-129">toohide Hola casilla, configure esta opción demasiado**Sí**.</span><span class="sxs-lookup"><span data-stu-id="f5e9b-129">toohide hello checkbox, configure this setting too**Yes**.</span></span>

> [!NOTE]
> <span data-ttu-id="f5e9b-130">Algunas características de SharePoint Online y Office 2010 dependen de los usuarios que están toocheck capaz de este cuadro.</span><span class="sxs-lookup"><span data-stu-id="f5e9b-130">Some features of SharePoint Online and Office 2010 depend on users being able toocheck this box.</span></span> <span data-ttu-id="f5e9b-131">Si configura esta toohidden de configuración, los usuarios pueden ver mensajes adicionales e inesperadas en toosign.</span><span class="sxs-lookup"><span data-stu-id="f5e9b-131">If you configure this setting toohidden, your users may see additional and unexpected prompts toosign-in.</span></span>
>
>

<span data-ttu-id="f5e9b-132">**tooadd marca tooyour directorio de la empresa:**</span><span class="sxs-lookup"><span data-stu-id="f5e9b-132">**tooadd company branding tooyour directory:**</span></span>

1. <span data-ttu-id="f5e9b-133">Inicie sesión en toohello [portal de Azure](https://portal.azure.com) con una cuenta que sea un administrador global para el directorio de Hola.</span><span class="sxs-lookup"><span data-stu-id="f5e9b-133">Sign in toohello [Azure portal](https://portal.azure.com) with an account that's a global admin for hello directory.</span></span>
2. <span data-ttu-id="f5e9b-134">Seleccione **más servicios**, escriba **usuarios y grupos** en Hola cuadro de texto y, a continuación, seleccione **ENTRAR**.</span><span class="sxs-lookup"><span data-stu-id="f5e9b-134">Select **More services**, enter **Users and groups** in hello text box, and then select **Enter**.</span></span>

   ![Apertura de Administración de usuarios](./media/active-directory-branding-custom-signon-azure-portal/user-management.png)
3. <span data-ttu-id="f5e9b-136">En hello **usuarios y grupos** hoja, seleccione **información de marca**.</span><span class="sxs-lookup"><span data-stu-id="f5e9b-136">On hello **Users and groups** blade, select **Company branding**.</span></span>
4. <span data-ttu-id="f5e9b-137">En hello **a los usuarios y grupos: personalización de marca de empresa** hoja, seleccione hello **editar** comando.</span><span class="sxs-lookup"><span data-stu-id="f5e9b-137">On hello **Users and groups - Company branding** blade, select hello **Edit** command.</span></span>

    ![Edición de la personalización de marca](./media/active-directory-branding-custom-signon-azure-portal/edit-branding.png)
5. <span data-ttu-id="f5e9b-139">Modificar elementos de hello desea toocustomize.</span><span class="sxs-lookup"><span data-stu-id="f5e9b-139">Modify hello elements you want toocustomize.</span></span> <span data-ttu-id="f5e9b-140">Todos los elementos son opcionales.</span><span class="sxs-lookup"><span data-stu-id="f5e9b-140">All elements are optional.</span></span>
6. <span data-ttu-id="f5e9b-141">Haga clic en **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="f5e9b-141">Click **Save**.</span></span>

<span data-ttu-id="f5e9b-142">Puede tardar hasta hora tooan para cualquier cambio realizado toohello inicio de sesión página tooappear personalización de marca.</span><span class="sxs-lookup"><span data-stu-id="f5e9b-142">It can take up tooan hour for any changes you made toohello sign-in page branding tooappear.</span></span>

## <a name="next-steps"></a><span data-ttu-id="f5e9b-143">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="f5e9b-143">Next steps</span></span>
[<span data-ttu-id="f5e9b-144">Agregar información de marca de empresa específica de un idioma</span><span class="sxs-lookup"><span data-stu-id="f5e9b-144">Add language-specific company branding</span></span>](active-directory-branding-localize-azure-portal.md)
