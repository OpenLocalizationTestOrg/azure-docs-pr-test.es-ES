---
title: "Azure Active Directory B2C: configuración de Facebook | Microsoft Docs"
description: "Proporcione a los consumidores la posibilidad de registro e inicio de sesión con cuentas de Facebook en las aplicaciones protegidas por Azure Active Directory B2C."
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
ms.openlocfilehash: 8c2154fcf33537358b549395d15b4ba937371cd0
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/18/2017
---
# <a name="azure-active-directory-b2c-provide-sign-up-and-sign-in-to-consumers-with-facebook-accounts"></a><span data-ttu-id="9c4ef-103">Azure Active Directory B2C: provisión de registro e inicio de sesión a los consumidores con cuentas de Facebook</span><span class="sxs-lookup"><span data-stu-id="9c4ef-103">Azure Active Directory B2C: Provide sign-up and sign-in to consumers with Facebook accounts</span></span>
## <a name="create-a-facebook-application"></a><span data-ttu-id="9c4ef-104">Creación de una aplicación de Facebook</span><span class="sxs-lookup"><span data-stu-id="9c4ef-104">Create a Facebook application</span></span>
<span data-ttu-id="9c4ef-105">Para usar Facebook como proveedor de identidades en Azure Active Directory (Azure AD) B2C, primero debe crear una aplicación de Facebook y suministrarle los parámetros correctos.</span><span class="sxs-lookup"><span data-stu-id="9c4ef-105">To use Facebook as an identity provider in Azure Active Directory (Azure AD) B2C, you need to create a Facebook application and supply it with the right parameters.</span></span> <span data-ttu-id="9c4ef-106">Necesita una cuenta de Facebook para ello.</span><span class="sxs-lookup"><span data-stu-id="9c4ef-106">You need a Facebook account to do this.</span></span> <span data-ttu-id="9c4ef-107">Si no tiene una, puede obtenerla en [https://www.facebook.com/](https://www.facebook.com/).</span><span class="sxs-lookup"><span data-stu-id="9c4ef-107">If you don’t have one, you can get it at [https://www.facebook.com/](https://www.facebook.com/).</span></span>

1. <span data-ttu-id="9c4ef-108">Vaya al sitio web [Facebook for developers](https://developers.facebook.com/) e inicie sesión con las credenciales de su cuenta de Facebook.</span><span class="sxs-lookup"><span data-stu-id="9c4ef-108">Go to the [Facebook for developers](https://developers.facebook.com/) website and sign in with your Facebook account credentials.</span></span>
2. <span data-ttu-id="9c4ef-109">Si aún no lo ha hecho, debe registrarse como desarrollador de Facebook.</span><span class="sxs-lookup"><span data-stu-id="9c4ef-109">If you have not already done so, you need to register as a Facebook developer.</span></span> <span data-ttu-id="9c4ef-110">Para ello, haga clic en **Register** (Registrarte) (en la esquina superior derecha de la página), acepte las directivas de Facebook y complete los pasos de registro.</span><span class="sxs-lookup"><span data-stu-id="9c4ef-110">To do this, click **Register** (on the upper-right corner of the page), accept Facebook's policies, and complete the registration steps.</span></span>
3. <span data-ttu-id="9c4ef-111">Haga clic en **Mis aplicaciones** y luego en **Agregar una nueva aplicación**.</span><span class="sxs-lookup"><span data-stu-id="9c4ef-111">Click **My Apps** and then click **Add a New App**.</span></span> 
4. <span data-ttu-id="9c4ef-112">En el formulario, proporcione un valor para **Nombre para mostrar** y un valor válido de **Correo electrónico de contacto**.</span><span class="sxs-lookup"><span data-stu-id="9c4ef-112">In the form, provide a **Display Name** and a valid **Contact Email**.</span></span>
5. <span data-ttu-id="9c4ef-113">Haga clic en **Create App ID** (Crear id. de aplicación).</span><span class="sxs-lookup"><span data-stu-id="9c4ef-113">Click **Create App ID**.</span></span> <span data-ttu-id="9c4ef-114">Es posible que deba aceptar las políticas de la plataforma Facebook y realizar una comprobación de seguridad en línea.</span><span class="sxs-lookup"><span data-stu-id="9c4ef-114">This may require you to accept Facebook platform policies and complete an online security check.</span></span>
6. <span data-ttu-id="9c4ef-115">En la columna izquierda, haga clic en **Configuración** y, a continuación, seleccione el valor **Básico** en el caso de que no aparezca seleccionado ya.</span><span class="sxs-lookup"><span data-stu-id="9c4ef-115">In the left column, click **Settings** and then select **Basic** if not selected already.</span></span>
7. <span data-ttu-id="9c4ef-116">Seleccione un valor de **Categoría**.</span><span class="sxs-lookup"><span data-stu-id="9c4ef-116">Select a **Category**.</span></span> 
8. <span data-ttu-id="9c4ef-117">Haga clic en **+Add Platform** (+Agregar plataforma) y seleccione **Sitio web**.</span><span class="sxs-lookup"><span data-stu-id="9c4ef-117">Click **+ Add Platform** and select **Website**.</span></span>
   
    ![Facebook - Configuración](./media/active-directory-b2c-setup-fb-app/fb-settings.png)
   
    ![Facebook - Configuración - Sitio web](./media/active-directory-b2c-setup-fb-app/fb-website.png)
9. <span data-ttu-id="9c4ef-120">Escriba `https://login.microsoftonline.com/` en el campo **Dirección URL del sitio** y, a continuación, haga clic en **Guardar cambios** en la parte inferior de la página.</span><span class="sxs-lookup"><span data-stu-id="9c4ef-120">Enter `https://login.microsoftonline.com/` in the **Site URL** field and then click **Save Changes** at the bottom of the page.</span></span>
   
    ![Facebook - Dirección URL del sitio](./media/active-directory-b2c-setup-fb-app/fb-site-url.png)

10. <span data-ttu-id="9c4ef-122">Copie el valor de **App ID** (Id. de aplicación).</span><span class="sxs-lookup"><span data-stu-id="9c4ef-122">Copy the value of **App ID**.</span></span> <span data-ttu-id="9c4ef-123">Haga clic en **Show** (Mostrar) y copie el valor de **App Secret** (Secreto de la aplicación).</span><span class="sxs-lookup"><span data-stu-id="9c4ef-123">Click **Show** and copy the value of **App Secret**.</span></span> <span data-ttu-id="9c4ef-124">Necesitará ambos para configurar Facebook como proveedor de identidades de su inquilino.</span><span class="sxs-lookup"><span data-stu-id="9c4ef-124">You will need both of them to configure Facebook as an identity provider in your tenant.</span></span> <span data-ttu-id="9c4ef-125">El **secreto de la aplicación** es una credencial de seguridad importante.</span><span class="sxs-lookup"><span data-stu-id="9c4ef-125">**App Secret** is an important security credential.</span></span>
   
    ![Facebook - Id. de aplicación y el secreto de la aplicación](./media/active-directory-b2c-setup-fb-app/fb-app-id-app-secret.png)
11. <span data-ttu-id="9c4ef-127">Haga clic en **+ Add Product** (+ Agregar producto) en la barra de navegación izquierda y, a continuación, en el botón **Set Up** (Instalación) de **Facebook Login** (Inicio de sesión de Facebook).</span><span class="sxs-lookup"><span data-stu-id="9c4ef-127">Click **+ Add Product** on the left navigation and then the **Set Up** button for **Facebook Login**.</span></span>
   
    ![Facebook - Inicio de sesión de Facebook](./media/active-directory-b2c-setup-fb-app/fb-login.png)
12. <span data-ttu-id="9c4ef-129">Haga clic en **Settings** (Configuración) en la barra de navegación derecha **Facebook Login** (Inicio de sesión de Facebook)</span><span class="sxs-lookup"><span data-stu-id="9c4ef-129">Click **Settings** on the right nav under **Facebook Login**</span></span>

    ![Facebook - Configuración de inicio de sesión de Facebook](./media/active-directory-b2c-setup-fb-app/fb-login-settings.png)
13. <span data-ttu-id="9c4ef-131">Escriba `https://login.microsoftonline.com/te/{tenant}/oauth2/authresp` en el campo **Valid OAuth redirect URIs** (URI de redirección de OAuth válido) de la sección **Client OAuth Settings** (Configuración de OAuth de cliente).</span><span class="sxs-lookup"><span data-stu-id="9c4ef-131">Enter `https://login.microsoftonline.com/te/{tenant}/oauth2/authresp` in the **Valid OAuth redirect URIs** field in the **Client OAuth Settings** section.</span></span> <span data-ttu-id="9c4ef-132">Reemplace **{tenant}** por el nombre de su inquilino (por ejemplo, contosob2c.onmicrosoft.com).</span><span class="sxs-lookup"><span data-stu-id="9c4ef-132">Replace **{tenant}** with your tenant's name (for example, contosob2c.onmicrosoft.com).</span></span> <span data-ttu-id="9c4ef-133">Haga clic en **Save Changes** (Guardar cambios) en la parte inferior de la página.</span><span class="sxs-lookup"><span data-stu-id="9c4ef-133">Click **Save Changes** at the bottom of the page.</span></span>
    
    ![Facebook - URI de redireccionamiento de OAuth](./media/active-directory-b2c-setup-fb-app/fb-oauth-redirect-uri.png)
14. <span data-ttu-id="9c4ef-135">Para que la aplicación Facebook se puede usar con Azure AD B2C, es necesario ponerla a disposición del público.</span><span class="sxs-lookup"><span data-stu-id="9c4ef-135">To make your Facebook application usable by Azure AD B2C, you need to make it publicly available.</span></span> <span data-ttu-id="9c4ef-136">Para ello, haga clic en **App Review** (Revisión de la aplicación) en la barra navegación izquierda, mueva el conmutador de la parte superior de la página a **YES** (SÍ) y haga clic en **Confirm** (Confirmar).</span><span class="sxs-lookup"><span data-stu-id="9c4ef-136">You can do this by clicking **App Review** on the left navigation and by turning the switch at the top of the page to **YES** and clicking **Confirm**.</span></span>
    
    ![Facebook - Público de la aplicación](./media/active-directory-b2c-setup-fb-app/fb-app-public.png)

## <a name="configure-facebook-as-an-identity-provider-in-your-tenant"></a><span data-ttu-id="9c4ef-138">Configuración de Facebook como proveedor de identidades del inquilino</span><span class="sxs-lookup"><span data-stu-id="9c4ef-138">Configure Facebook as an identity provider in your tenant</span></span>
1. <span data-ttu-id="9c4ef-139">Siga estos pasos para [ir a la hoja de características de B2C](active-directory-b2c-app-registration.md#navigate-to-b2c-settings) de Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="9c4ef-139">Follow these steps to [navigate to the B2C features blade](active-directory-b2c-app-registration.md#navigate-to-b2c-settings) on the Azure portal.</span></span>
2. <span data-ttu-id="9c4ef-140">En la hoja de características B2C, haga clic en **Proveedores de identidades**.</span><span class="sxs-lookup"><span data-stu-id="9c4ef-140">On the B2C features blade, click **Identity providers**.</span></span>
3. <span data-ttu-id="9c4ef-141">Haga clic en **+Agregar** en la parte superior de la hoja.</span><span class="sxs-lookup"><span data-stu-id="9c4ef-141">Click **+Add** at the top of the blade.</span></span>
4. <span data-ttu-id="9c4ef-142">Proporcione un **Nombre** descriptivo para la configuración del proveedor de identidades.</span><span class="sxs-lookup"><span data-stu-id="9c4ef-142">Provide a friendly **Name** for the identity provider configuration.</span></span> <span data-ttu-id="9c4ef-143">Por ejemplo, escriba "Facebook".</span><span class="sxs-lookup"><span data-stu-id="9c4ef-143">For example, enter "Facebook".</span></span>
5. <span data-ttu-id="9c4ef-144">Haga clic en **Identity provider type** (Tipo de proveedor de identidades), seleccione **Facebook** y haga clic en **OK** (Aceptar).</span><span class="sxs-lookup"><span data-stu-id="9c4ef-144">Click **Identity provider type**, select **Facebook**, and click **OK**.</span></span>
6. <span data-ttu-id="9c4ef-145">Haga clic en **Set up this identity provider** (Configurar este proveedor de identidades), y escriba el id. y el secreto de la aplicación (de la aplicación de Facebook que creó anteriormente) en los campos **Client ID** y **Client secret** respectivamente.</span><span class="sxs-lookup"><span data-stu-id="9c4ef-145">Click **Set up this identity provider** and enter the app ID and app secret (of the Facebook application that you created earlier) in the **Client ID** and **Client secret** fields respectively.</span></span>
7. <span data-ttu-id="9c4ef-146">Haga clic en **OK** (Aceptar) y, luego, en **Create** (Crear) para guardar la configuración de Facebook.</span><span class="sxs-lookup"><span data-stu-id="9c4ef-146">Click **OK**, and then click **Create** to save your Facebook configuration.</span></span>

> [!NOTE]
> <span data-ttu-id="9c4ef-147">Si se agrega un **Proveedor de identidades** a su inquilino, sus directivas existentes no se modificarán.</span><span class="sxs-lookup"><span data-stu-id="9c4ef-147">Adding an **Identity provider** to your tenant does not modify your existing policies.</span></span> <span data-ttu-id="9c4ef-148">Recuerde actualizar sus directivas incluyendo el proveedor de identidades que acaba de crear.</span><span class="sxs-lookup"><span data-stu-id="9c4ef-148">Remember to update your policies by including the identity provider you just created.</span></span>
>