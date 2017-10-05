---
title: "Azure Active Directory B2C: configuración de Google+ | Microsoft Docs"
description: "Proporcione funciones de registro e inicio de sesión a los consumidores con cuentas de Google+ en las aplicaciones protegidas por Azure Active Directory B2C."
services: active-directory-b2c
documentationcenter: 
author: swkrish
manager: mbaldwin
editor: bryanla
ms.assetid: 4dcca66f-29e4-4b4d-8840-50baad736bd7
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/06/2016
ms.author: swkrish
ms.openlocfilehash: 6ab73e5c79742ab548733f5712dee1e28461db9f
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/18/2017
---
# <a name="azure-active-directory-b2c-provide-sign-up-and-sign-in-to-consumers-with-google-accounts"></a><span data-ttu-id="0ec57-103">Azure Active Directory B2C: provisión de registro e inicio de sesión a los usuarios con cuentas de Google+</span><span class="sxs-lookup"><span data-stu-id="0ec57-103">Azure Active Directory B2C: Provide sign-up and sign-in to consumers with Google+ accounts</span></span>
## <a name="create-a-google-application"></a><span data-ttu-id="0ec57-104">Creación de una aplicación de Google+</span><span class="sxs-lookup"><span data-stu-id="0ec57-104">Create a Google+ application</span></span>
<span data-ttu-id="0ec57-105">Para usar Google+ como proveedor de identidades en Azure Active Directory (Azure AD) B2C, debe crear una aplicación de Google+ y suministrarle los parámetros correctos.</span><span class="sxs-lookup"><span data-stu-id="0ec57-105">To use Google+ as an identity provider in Azure Active Directory (Azure AD) B2C, you need to create a Google+ application and supply it with the right parameters.</span></span> <span data-ttu-id="0ec57-106">Necesita una cuenta de Google+ para hacerlo.</span><span class="sxs-lookup"><span data-stu-id="0ec57-106">You need a Google+ account to do this.</span></span> <span data-ttu-id="0ec57-107">Si no tiene una, puede obtenerla en [https://accounts.google.com/SignUp](https://accounts.google.com/SignUp).</span><span class="sxs-lookup"><span data-stu-id="0ec57-107">If you don’t have one, you can get it at [https://accounts.google.com/SignUp](https://accounts.google.com/SignUp).</span></span>

1. <span data-ttu-id="0ec57-108">Vaya a [Google Developers Console](https://console.developers.google.com/) e inicie sesión con las credenciales de su cuenta de Google+.</span><span class="sxs-lookup"><span data-stu-id="0ec57-108">Go to the [Google Developers Console](https://console.developers.google.com/) and sign in with your Google+ account credentials.</span></span>
2. <span data-ttu-id="0ec57-109">Haga clic en **Create project** (Crear proyecto), escriba un nombre de proyecto en **Project name** y haga clic en **Create** (Crear).</span><span class="sxs-lookup"><span data-stu-id="0ec57-109">Click **Create project**, enter a **Project name**, and then click **Create**.</span></span>
   
    ![Google+: introducción](./media/active-directory-b2c-setup-goog-app/google-get-started.png)
   
    ![Google+: nuevo proyecto](./media/active-directory-b2c-setup-goog-app/google-new-project.png)
3. <span data-ttu-id="0ec57-112">En el panel de navegación izquierdo, haga clic en **API Manager** (Administrador de API) y, luego, en **Credentials** (Credenciales).</span><span class="sxs-lookup"><span data-stu-id="0ec57-112">Click **API Manager** and then click **Credentials** in the left navigation.</span></span>
4. <span data-ttu-id="0ec57-113">Haga clic en la **pantalla de autorización de OAuth** en la parte superior.</span><span class="sxs-lookup"><span data-stu-id="0ec57-113">Click the **OAuth consent screen** tab at the top.</span></span>
   
    ![Google+: credenciales](./media/active-directory-b2c-setup-goog-app/google-add-cred.png)
5. <span data-ttu-id="0ec57-115">Seleccione o especifique una dirección de correo electrónico válida en **Email address**, especifique un nombre de producto en **Product name** y haga clic en **Save** (Guardar).</span><span class="sxs-lookup"><span data-stu-id="0ec57-115">Select or specify a valid **Email address**, provide a **Product name**, and click **Save**.</span></span>
   
    ![Google+: pantalla de consentimiento de OAuth](./media/active-directory-b2c-setup-goog-app/google-consent-screen.png)
6. <span data-ttu-id="0ec57-117">Haga clic en **New credentials** (Nuevas credenciales) y, luego, elija **OAuth client ID** (Id. de cliente de OAuth).</span><span class="sxs-lookup"><span data-stu-id="0ec57-117">Click **New credentials** and then choose **OAuth client ID**.</span></span>
   
    ![Google+: pantalla de consentimiento de OAuth](./media/active-directory-b2c-setup-goog-app/google-add-oauth2-client-id.png)
7. <span data-ttu-id="0ec57-119">En **Application type** (Tipo de aplicación), seleccione **Web application** (Aplicación web).</span><span class="sxs-lookup"><span data-stu-id="0ec57-119">Under **Application type**, select **Web application**.</span></span>
   
    ![Google+: pantalla de consentimiento de OAuth](./media/active-directory-b2c-setup-goog-app/google-web-app.png)
8. <span data-ttu-id="0ec57-121">Especifique un **nombre** para la aplicación, escriba `https://login.microsoftonline.com` en el campo **Authorized JavaScript origins** (Orígenes de JavaScript autorizados) y `https://login.microsoftonline.com/te/{tenant}/oauth2/authresp` en el campo **Authorized redirect URIs** (URI de redirección autorizados).</span><span class="sxs-lookup"><span data-stu-id="0ec57-121">Provide a **Name** for your application, enter `https://login.microsoftonline.com` in the **Authorized JavaScript origins** field, and `https://login.microsoftonline.com/te/{tenant}/oauth2/authresp` in the **Authorized redirect URIs** field.</span></span> <span data-ttu-id="0ec57-122">Reemplace **{tenant}** por el nombre de su inquilino (por ejemplo, contosob2c.onmicrosoft.com).</span><span class="sxs-lookup"><span data-stu-id="0ec57-122">Replace **{tenant}** with your tenant's name (for example, contosob2c.onmicrosoft.com).</span></span> <span data-ttu-id="0ec57-123">El valor de **{tenant}** distingue mayúsculas de minúsculas.</span><span class="sxs-lookup"><span data-stu-id="0ec57-123">The **{tenant}** value is case-sensitive.</span></span> <span data-ttu-id="0ec57-124">Haga clic en **Create**(Crear).</span><span class="sxs-lookup"><span data-stu-id="0ec57-124">Click **Create**.</span></span>
   
    ![Google+: creación del identificador de cliente](./media/active-directory-b2c-setup-goog-app/google-create-client-id.png)
9. <span data-ttu-id="0ec57-126">Copie los valores de **Client ID** y **Client Secret**.</span><span class="sxs-lookup"><span data-stu-id="0ec57-126">Copy the values of **Client ID** and **Client secret**.</span></span> <span data-ttu-id="0ec57-127">Necesitará ambos para configurar Google+ como proveedor de identidades de su inquilino.</span><span class="sxs-lookup"><span data-stu-id="0ec57-127">You will need both of them to configure Google+ as an identity provider in your tenant.</span></span> <span data-ttu-id="0ec57-128">**Secreto del cliente** es una credencial de seguridad importante.</span><span class="sxs-lookup"><span data-stu-id="0ec57-128">**Client secret** is an important security credential.</span></span>
   
    ![Google+: secreto de cliente](./media/active-directory-b2c-setup-goog-app/google-client-secret.png)

## <a name="configure-google-as-an-identity-provider-in-your-tenant"></a><span data-ttu-id="0ec57-130">Configuración de Google+ como proveedor de identidades del inquilino</span><span class="sxs-lookup"><span data-stu-id="0ec57-130">Configure Google+ as an identity provider in your tenant</span></span>
1. <span data-ttu-id="0ec57-131">Siga estos pasos para [ir a la hoja de características de B2C](active-directory-b2c-app-registration.md#navigate-to-b2c-settings) del Portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="0ec57-131">Follow these steps to [navigate to the B2C features blade](active-directory-b2c-app-registration.md#navigate-to-b2c-settings) on the Azure portal.</span></span>
2. <span data-ttu-id="0ec57-132">En la hoja de características B2C, haga clic en **Proveedores de identidades**.</span><span class="sxs-lookup"><span data-stu-id="0ec57-132">On the B2C features blade, click **Identity providers**.</span></span>
3. <span data-ttu-id="0ec57-133">Haga clic en **+Agregar** en la parte superior de la hoja.</span><span class="sxs-lookup"><span data-stu-id="0ec57-133">Click **+Add** at the top of the blade.</span></span>
4. <span data-ttu-id="0ec57-134">Proporcione un **Nombre** descriptivo para la configuración del proveedor de identidades.</span><span class="sxs-lookup"><span data-stu-id="0ec57-134">Provide a friendly **Name** for the identity provider configuration.</span></span> <span data-ttu-id="0ec57-135">Por ejemplo, "G+".</span><span class="sxs-lookup"><span data-stu-id="0ec57-135">For example, enter "G+".</span></span>
5. <span data-ttu-id="0ec57-136">Haga clic en **Identity provider type** (Tipo de proveedor de identidades), seleccione **Google** y haga clic en **OK** (Aceptar).</span><span class="sxs-lookup"><span data-stu-id="0ec57-136">Click **Identity provider type**, select **Google**, and click **OK**.</span></span>
6. <span data-ttu-id="0ec57-137">Haga clic en **Set up this identity provider** (Configurar este proveedor de identidades) y escriba el identificador de cliente y el secreto de cliente de la aplicación de Google+ que creó anteriormente.</span><span class="sxs-lookup"><span data-stu-id="0ec57-137">Click **Set up this identity provider** and enter the client ID and client secret of the Google+ application that you created earlier.</span></span>
7. <span data-ttu-id="0ec57-138">Haga clic en **OK** (Aceptar) y, luego, en **Create** (Crear) para guardar la configuración de Google+.</span><span class="sxs-lookup"><span data-stu-id="0ec57-138">Click **OK** and then click **Create** to save your Google+ configuration.</span></span>

