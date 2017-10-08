---
title: "Azure Active Directory B2C: configuración de Facebook | Microsoft Docs"
description: "Proporcionar tooconsumers registrarse e iniciar sesión con cuentas de Facebook en las aplicaciones que están protegidas por Azure Active Directory B2C."
services: active-directory-b2c
documentationcenter: 
author: sromeroz
manager: krassk
editor: sromeroz
ms.assetid: b875f235-a1d2-4abb-b9f0-b89beac38a32
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 8/7/2017
ms.author: sromeroz
ms.openlocfilehash: 4c3b79c7248bd1e789bf33fc467abb27d0170edd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-b2c-provide-sign-up-and-sign-in-tooconsumers-with-facebook-accounts"></a><span data-ttu-id="094c6-103">Azure B2C Directory Active: Proporcionar tooconsumers registrarse e iniciar sesión con cuentas de Facebook</span><span class="sxs-lookup"><span data-stu-id="094c6-103">Azure Active Directory B2C: Provide sign-up and sign-in tooconsumers with Facebook accounts</span></span>
## <a name="create-a-facebook-application"></a><span data-ttu-id="094c6-104">Creación de una aplicación de Facebook</span><span class="sxs-lookup"><span data-stu-id="094c6-104">Create a Facebook application</span></span>
<span data-ttu-id="094c6-105">toouse Facebook como proveedor de identidades en Azure Active Directory (Azure AD) B2C, necesita toocreate una aplicación de Facebook y proporcionarle los parámetros correctos de Hola.</span><span class="sxs-lookup"><span data-stu-id="094c6-105">toouse Facebook as an identity provider in Azure Active Directory (Azure AD) B2C, you need toocreate a Facebook application and supply it with hello right parameters.</span></span> <span data-ttu-id="094c6-106">Se necesita un toodo de cuenta de Facebook.</span><span class="sxs-lookup"><span data-stu-id="094c6-106">You need a Facebook account toodo this.</span></span> <span data-ttu-id="094c6-107">Si no tiene una, puede obtenerla en [https://www.facebook.com/](https://www.facebook.com/).</span><span class="sxs-lookup"><span data-stu-id="094c6-107">If you don’t have one, you can get it at [https://www.facebook.com/](https://www.facebook.com/).</span></span>

1. <span data-ttu-id="094c6-108">Vaya toohello [Facebook para los desarrolladores](https://developers.facebook.com/) credenciales de cuenta de sitio Web e inicie sesión con su Facebook.</span><span class="sxs-lookup"><span data-stu-id="094c6-108">Go toohello [Facebook for developers](https://developers.facebook.com/) website and sign in with your Facebook account credentials.</span></span>
2. <span data-ttu-id="094c6-109">Si no lo ha hecho ya, deberá tooregister como un programador de Facebook.</span><span class="sxs-lookup"><span data-stu-id="094c6-109">If you have not already done so, you need tooregister as a Facebook developer.</span></span> <span data-ttu-id="094c6-110">toodo, haga clic en **registrar** (en la esquina de superior derecha de Hola de página hello), acepte las directivas de Facebook y completar los pasos de registro de hello.</span><span class="sxs-lookup"><span data-stu-id="094c6-110">toodo this, click **Register** (on hello upper-right corner of hello page), accept Facebook's policies, and complete hello registration steps.</span></span>
3. <span data-ttu-id="094c6-111">Haga clic en **Mis aplicaciones** y luego en **Agregar una nueva aplicación**.</span><span class="sxs-lookup"><span data-stu-id="094c6-111">Click **My Apps** and then click **Add a New App**.</span></span> 
4. <span data-ttu-id="094c6-112">En el formulario de hello, proporcionar un **nombre para mostrar** y válido **correo electrónico de contacto**.</span><span class="sxs-lookup"><span data-stu-id="094c6-112">In hello form, provide a **Display Name** and a valid **Contact Email**.</span></span>
5. <span data-ttu-id="094c6-113">Haga clic en **Create App ID** (Crear id. de aplicación).</span><span class="sxs-lookup"><span data-stu-id="094c6-113">Click **Create App ID**.</span></span> <span data-ttu-id="094c6-114">Esto puede requieren directivas de plataforma Facebook tooaccept y completar una comprobación de seguridad en línea.</span><span class="sxs-lookup"><span data-stu-id="094c6-114">This may require you tooaccept Facebook platform policies and complete an online security check.</span></span>
6. <span data-ttu-id="094c6-115">En la columna izquierda de hello, haga clic en **configuración** y, a continuación, seleccione **básica** si no ha seleccionado ya.</span><span class="sxs-lookup"><span data-stu-id="094c6-115">In hello left column, click **Settings** and then select **Basic** if not selected already.</span></span>
7. <span data-ttu-id="094c6-116">Seleccione un valor de **Categoría**.</span><span class="sxs-lookup"><span data-stu-id="094c6-116">Select a **Category**.</span></span> 
8. <span data-ttu-id="094c6-117">Haga clic en **+Add Platform** (+Agregar plataforma) y seleccione **Sitio web**.</span><span class="sxs-lookup"><span data-stu-id="094c6-117">Click **+ Add Platform** and select **Website**.</span></span>
   
    ![Facebook - Configuración](./media/active-directory-b2c-setup-fb-app/fb-settings.png)
   
    ![Facebook - Configuración - Sitio web](./media/active-directory-b2c-setup-fb-app/fb-website.png)
9. <span data-ttu-id="094c6-120">Escriba `https://login.microsoftonline.com/` en hello **dirección URL del sitio** campo y, a continuación, haga clic en **guardar cambios** final Hola de página Hola.</span><span class="sxs-lookup"><span data-stu-id="094c6-120">Enter `https://login.microsoftonline.com/` in hello **Site URL** field and then click **Save Changes** at hello bottom of hello page.</span></span>
   
    ![Facebook - Dirección URL del sitio](./media/active-directory-b2c-setup-fb-app/fb-site-url.png)

10. <span data-ttu-id="094c6-122">Copiar valor de Hola de **identificador de la aplicación**.</span><span class="sxs-lookup"><span data-stu-id="094c6-122">Copy hello value of **App ID**.</span></span> <span data-ttu-id="094c6-123">Haga clic en **mostrar** y copie el valor de Hola de **secreto de la aplicación**.</span><span class="sxs-lookup"><span data-stu-id="094c6-123">Click **Show** and copy hello value of **App Secret**.</span></span> <span data-ttu-id="094c6-124">Necesitará ambos tooconfigure Facebook como proveedor de identidades en su inquilino.</span><span class="sxs-lookup"><span data-stu-id="094c6-124">You will need both of them tooconfigure Facebook as an identity provider in your tenant.</span></span> <span data-ttu-id="094c6-125">El **secreto de la aplicación** es una credencial de seguridad importante.</span><span class="sxs-lookup"><span data-stu-id="094c6-125">**App Secret** is an important security credential.</span></span>
   
    ![Facebook - Id. de aplicación y el secreto de la aplicación](./media/active-directory-b2c-setup-fb-app/fb-app-id-app-secret.png)
11. <span data-ttu-id="094c6-127">Haga clic en **+ agregar producto** Hola de navegación izquierdo y, a continuación, Hola **Set Up** botón **inicio de sesión de Facebook**.</span><span class="sxs-lookup"><span data-stu-id="094c6-127">Click **+ Add Product** on hello left navigation and then hello **Set Up** button for **Facebook Login**.</span></span>
   
    ![Facebook - Inicio de sesión de Facebook](./media/active-directory-b2c-setup-fb-app/fb-login.png)
12. <span data-ttu-id="094c6-129">Haga clic en **configuración** en hello nav derecha bajo **inicio de sesión de Facebook**</span><span class="sxs-lookup"><span data-stu-id="094c6-129">Click **Settings** on hello right nav under **Facebook Login**</span></span>

    ![Facebook - Configuración de inicio de sesión de Facebook](./media/active-directory-b2c-setup-fb-app/fb-login-settings.png)
13. <span data-ttu-id="094c6-131">Escriba `https://login.microsoftonline.com/te/{tenant}/oauth2/authresp` en hello **URI de redireccionamiento válido OAuth** campo hello **configuración de cliente OAuth** sección.</span><span class="sxs-lookup"><span data-stu-id="094c6-131">Enter `https://login.microsoftonline.com/te/{tenant}/oauth2/authresp` in hello **Valid OAuth redirect URIs** field in hello **Client OAuth Settings** section.</span></span> <span data-ttu-id="094c6-132">Reemplace **{tenant}** por el nombre de su inquilino (por ejemplo, contosob2c.onmicrosoft.com).</span><span class="sxs-lookup"><span data-stu-id="094c6-132">Replace **{tenant}** with your tenant's name (for example, contosob2c.onmicrosoft.com).</span></span> <span data-ttu-id="094c6-133">Haga clic en **guardar cambios** final Hola de página Hola.</span><span class="sxs-lookup"><span data-stu-id="094c6-133">Click **Save Changes** at hello bottom of hello page.</span></span>
    
    ![Facebook - URI de redireccionamiento de OAuth](./media/active-directory-b2c-setup-fb-app/fb-oauth-redirect-uri.png)
14. <span data-ttu-id="094c6-135">toomake su aplicación de Facebook utilizable por Azure AD B2C, necesita toomake estén disponibles públicamente.</span><span class="sxs-lookup"><span data-stu-id="094c6-135">toomake your Facebook application usable by Azure AD B2C, you need toomake it publicly available.</span></span> <span data-ttu-id="094c6-136">Para ello, haga clic en **revisión de aplicación** en la barra de navegación izquierda de Hola y Hola activar cambiar al principio de Hola de página de hello demasiado**Sí** y haga clic en **confirmar**.</span><span class="sxs-lookup"><span data-stu-id="094c6-136">You can do this by clicking **App Review** on hello left navigation and by turning hello switch at hello top of hello page too**YES** and clicking **Confirm**.</span></span>
    
    ![Facebook - Público de la aplicación](./media/active-directory-b2c-setup-fb-app/fb-app-public.png)

## <a name="configure-facebook-as-an-identity-provider-in-your-tenant"></a><span data-ttu-id="094c6-138">Configuración de Facebook como proveedor de identidades del inquilino</span><span class="sxs-lookup"><span data-stu-id="094c6-138">Configure Facebook as an identity provider in your tenant</span></span>
1. <span data-ttu-id="094c6-139">Siga estos pasos demasiado[navegue hoja de características toohello B2C](active-directory-b2c-app-registration.md#navigate-to-b2c-settings) en hello portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="094c6-139">Follow these steps too[navigate toohello B2C features blade](active-directory-b2c-app-registration.md#navigate-to-b2c-settings) on hello Azure portal.</span></span>
2. <span data-ttu-id="094c6-140">En la hoja de características de hello B2C, haga clic en **proveedores de identidades**.</span><span class="sxs-lookup"><span data-stu-id="094c6-140">On hello B2C features blade, click **Identity providers**.</span></span>
3. <span data-ttu-id="094c6-141">Haga clic en **+ agregar** princip Hola de hoja de Hola.</span><span class="sxs-lookup"><span data-stu-id="094c6-141">Click **+Add** at hello top of hello blade.</span></span>
4. <span data-ttu-id="094c6-142">Proporcionar descriptivo **nombre** para la configuración del proveedor de identidades Hola.</span><span class="sxs-lookup"><span data-stu-id="094c6-142">Provide a friendly **Name** for hello identity provider configuration.</span></span> <span data-ttu-id="094c6-143">Por ejemplo, escriba "Facebook".</span><span class="sxs-lookup"><span data-stu-id="094c6-143">For example, enter "Facebook".</span></span>
5. <span data-ttu-id="094c6-144">Haga clic en **Identity provider type** (Tipo de proveedor de identidades), seleccione **Facebook** y haga clic en **OK** (Aceptar).</span><span class="sxs-lookup"><span data-stu-id="094c6-144">Click **Identity provider type**, select **Facebook**, and click **OK**.</span></span>
6. <span data-ttu-id="094c6-145">Haga clic en **configurar este proveedor de identidades** y escriba Hola Id. y aplicación secreto de la aplicación (de Hola aplicación de Facebook que creó anteriormente) en hello **Id. de cliente** y **secreto del cliente**campos respectivamente.</span><span class="sxs-lookup"><span data-stu-id="094c6-145">Click **Set up this identity provider** and enter hello app ID and app secret (of hello Facebook application that you created earlier) in hello **Client ID** and **Client secret** fields respectively.</span></span>
7. <span data-ttu-id="094c6-146">Haga clic en **Aceptar**y, a continuación, haga clic en **crear** toosave la configuración de Facebook.</span><span class="sxs-lookup"><span data-stu-id="094c6-146">Click **OK**, and then click **Create** toosave your Facebook configuration.</span></span>

> [!NOTE]
> <span data-ttu-id="094c6-147">Agregar un **proveedor de identidades** tooyour inquilino no modifica las directivas existentes.</span><span class="sxs-lookup"><span data-stu-id="094c6-147">Adding an **Identity provider** tooyour tenant does not modify your existing policies.</span></span> <span data-ttu-id="094c6-148">Recuerde tooupdate las directivas mediante la inclusión de proveedor de identidades de Hola que acaba de crear.</span><span class="sxs-lookup"><span data-stu-id="094c6-148">Remember tooupdate your policies by including hello identity provider you just created.</span></span>
>