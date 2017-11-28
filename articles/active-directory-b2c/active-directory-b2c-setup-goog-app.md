---
title: "Azure Active Directory B2C: configuración de Google+ | Microsoft Docs"
description: "Proporcionar tooconsumers registrarse e iniciar sesión con cuentas de Google + en las aplicaciones que están protegidas por Azure Active Directory B2C."
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
ms.openlocfilehash: 6ef66eb17777acd95b5f4745ed6097c77e37663b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-b2c-provide-sign-up-and-sign-in-tooconsumers-with-google-accounts"></a><span data-ttu-id="d7de0-103">Azure B2C Directory Active: Proporcionar tooconsumers registrarse e iniciar sesión con cuentas de Google +</span><span class="sxs-lookup"><span data-stu-id="d7de0-103">Azure Active Directory B2C: Provide sign-up and sign-in tooconsumers with Google+ accounts</span></span>
## <a name="create-a-google-application"></a><span data-ttu-id="d7de0-104">Creación de una aplicación de Google+</span><span class="sxs-lookup"><span data-stu-id="d7de0-104">Create a Google+ application</span></span>
<span data-ttu-id="d7de0-105">toouse Google + como proveedor de identidades en Azure Active Directory (Azure AD) B2C, necesita una aplicación de Google + toocreate y proporcionarla con los parámetros correctos de Hola.</span><span class="sxs-lookup"><span data-stu-id="d7de0-105">toouse Google+ as an identity provider in Azure Active Directory (Azure AD) B2C, you need toocreate a Google+ application and supply it with hello right parameters.</span></span> <span data-ttu-id="d7de0-106">Se necesita una cuenta de Google + toodo.</span><span class="sxs-lookup"><span data-stu-id="d7de0-106">You need a Google+ account toodo this.</span></span> <span data-ttu-id="d7de0-107">Si no tiene una, puede obtenerla en [https://accounts.google.com/SignUp](https://accounts.google.com/SignUp).</span><span class="sxs-lookup"><span data-stu-id="d7de0-107">If you don’t have one, you can get it at [https://accounts.google.com/SignUp](https://accounts.google.com/SignUp).</span></span>

1. <span data-ttu-id="d7de0-108">Vaya toohello [Google Developers Console](https://console.developers.google.com/) e inicie sesión con sus credenciales de cuenta de Google +.</span><span class="sxs-lookup"><span data-stu-id="d7de0-108">Go toohello [Google Developers Console](https://console.developers.google.com/) and sign in with your Google+ account credentials.</span></span>
2. <span data-ttu-id="d7de0-109">Haga clic en **Create project** (Crear proyecto), escriba un nombre de proyecto en **Project name** y haga clic en **Create** (Crear).</span><span class="sxs-lookup"><span data-stu-id="d7de0-109">Click **Create project**, enter a **Project name**, and then click **Create**.</span></span>
   
    ![Google+: introducción](./media/active-directory-b2c-setup-goog-app/google-get-started.png)
   
    ![Google+: nuevo proyecto](./media/active-directory-b2c-setup-goog-app/google-new-project.png)
3. <span data-ttu-id="d7de0-112">Haga clic en **API Manager** y, a continuación, haga clic en **credenciales** Hola barra de navegación izquierda.</span><span class="sxs-lookup"><span data-stu-id="d7de0-112">Click **API Manager** and then click **Credentials** in hello left navigation.</span></span>
4. <span data-ttu-id="d7de0-113">Haga clic en hello **pantalla de consentimiento de OAuth** ficha situada en la parte superior de Hola.</span><span class="sxs-lookup"><span data-stu-id="d7de0-113">Click hello **OAuth consent screen** tab at hello top.</span></span>
   
    ![Google+: credenciales](./media/active-directory-b2c-setup-goog-app/google-add-cred.png)
5. <span data-ttu-id="d7de0-115">Seleccione o especifique una dirección de correo electrónico válida en **Email address**, especifique un nombre de producto en **Product name** y haga clic en **Save** (Guardar).</span><span class="sxs-lookup"><span data-stu-id="d7de0-115">Select or specify a valid **Email address**, provide a **Product name**, and click **Save**.</span></span>
   
    ![Google+: pantalla de consentimiento de OAuth](./media/active-directory-b2c-setup-goog-app/google-consent-screen.png)
6. <span data-ttu-id="d7de0-117">Haga clic en **New credentials** (Nuevas credenciales) y, luego, elija **OAuth client ID** (Id. de cliente de OAuth).</span><span class="sxs-lookup"><span data-stu-id="d7de0-117">Click **New credentials** and then choose **OAuth client ID**.</span></span>
   
    ![Google+: pantalla de consentimiento de OAuth](./media/active-directory-b2c-setup-goog-app/google-add-oauth2-client-id.png)
7. <span data-ttu-id="d7de0-119">En **Application type** (Tipo de aplicación), seleccione **Web application** (Aplicación web).</span><span class="sxs-lookup"><span data-stu-id="d7de0-119">Under **Application type**, select **Web application**.</span></span>
   
    ![Google+: pantalla de consentimiento de OAuth](./media/active-directory-b2c-setup-goog-app/google-web-app.png)
8. <span data-ttu-id="d7de0-121">Proporcionar un **nombre** para la aplicación, escriba `https://login.microsoftonline.com` en hello **orígenes de JavaScript autorizados** campo, y `https://login.microsoftonline.com/te/{tenant}/oauth2/authresp` en hello **autorizadas redirigir URI**campo.</span><span class="sxs-lookup"><span data-stu-id="d7de0-121">Provide a **Name** for your application, enter `https://login.microsoftonline.com` in hello **Authorized JavaScript origins** field, and `https://login.microsoftonline.com/te/{tenant}/oauth2/authresp` in hello **Authorized redirect URIs** field.</span></span> <span data-ttu-id="d7de0-122">Reemplace **{tenant}** por el nombre de su inquilino (por ejemplo, contosob2c.onmicrosoft.com).</span><span class="sxs-lookup"><span data-stu-id="d7de0-122">Replace **{tenant}** with your tenant's name (for example, contosob2c.onmicrosoft.com).</span></span> <span data-ttu-id="d7de0-123">Hola **{tenant}** valor distingue mayúsculas de minúsculas.</span><span class="sxs-lookup"><span data-stu-id="d7de0-123">hello **{tenant}** value is case-sensitive.</span></span> <span data-ttu-id="d7de0-124">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="d7de0-124">Click **Create**.</span></span>
   
    ![Google+: creación del identificador de cliente](./media/active-directory-b2c-setup-goog-app/google-create-client-id.png)
9. <span data-ttu-id="d7de0-126">Copiar valores de hello de **Id. de cliente** y **secreto de cliente**.</span><span class="sxs-lookup"><span data-stu-id="d7de0-126">Copy hello values of **Client ID** and **Client secret**.</span></span> <span data-ttu-id="d7de0-127">Necesitará ambos tooconfigure Google + como proveedor de identidades en su inquilino.</span><span class="sxs-lookup"><span data-stu-id="d7de0-127">You will need both of them tooconfigure Google+ as an identity provider in your tenant.</span></span> <span data-ttu-id="d7de0-128">**Secreto del cliente** es una credencial de seguridad importante.</span><span class="sxs-lookup"><span data-stu-id="d7de0-128">**Client secret** is an important security credential.</span></span>
   
    ![Google+: secreto de cliente](./media/active-directory-b2c-setup-goog-app/google-client-secret.png)

## <a name="configure-google-as-an-identity-provider-in-your-tenant"></a><span data-ttu-id="d7de0-130">Configuración de Google+ como proveedor de identidades del inquilino</span><span class="sxs-lookup"><span data-stu-id="d7de0-130">Configure Google+ as an identity provider in your tenant</span></span>
1. <span data-ttu-id="d7de0-131">Siga estos pasos demasiado[navegue hoja de características toohello B2C](active-directory-b2c-app-registration.md#navigate-to-b2c-settings) en hello portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="d7de0-131">Follow these steps too[navigate toohello B2C features blade](active-directory-b2c-app-registration.md#navigate-to-b2c-settings) on hello Azure portal.</span></span>
2. <span data-ttu-id="d7de0-132">En la hoja de características de hello B2C, haga clic en **proveedores de identidades**.</span><span class="sxs-lookup"><span data-stu-id="d7de0-132">On hello B2C features blade, click **Identity providers**.</span></span>
3. <span data-ttu-id="d7de0-133">Haga clic en **+ agregar** princip Hola de hoja de Hola.</span><span class="sxs-lookup"><span data-stu-id="d7de0-133">Click **+Add** at hello top of hello blade.</span></span>
4. <span data-ttu-id="d7de0-134">Proporcionar descriptivo **nombre** para la configuración del proveedor de identidades Hola.</span><span class="sxs-lookup"><span data-stu-id="d7de0-134">Provide a friendly **Name** for hello identity provider configuration.</span></span> <span data-ttu-id="d7de0-135">Por ejemplo, "G+".</span><span class="sxs-lookup"><span data-stu-id="d7de0-135">For example, enter "G+".</span></span>
5. <span data-ttu-id="d7de0-136">Haga clic en **Identity provider type** (Tipo de proveedor de identidades), seleccione **Google** y haga clic en **OK** (Aceptar).</span><span class="sxs-lookup"><span data-stu-id="d7de0-136">Click **Identity provider type**, select **Google**, and click **OK**.</span></span>
6. <span data-ttu-id="d7de0-137">Haga clic en **configurar este proveedor de identidades** y escriba el secreto de cliente y el Id. de cliente de Hola de hello aplicación de Google + que creó anteriormente.</span><span class="sxs-lookup"><span data-stu-id="d7de0-137">Click **Set up this identity provider** and enter hello client ID and client secret of hello Google+ application that you created earlier.</span></span>
7. <span data-ttu-id="d7de0-138">Haga clic en **Aceptar** y, a continuación, haga clic en **crear** toosave la configuración de Google +.</span><span class="sxs-lookup"><span data-stu-id="d7de0-138">Click **OK** and then click **Create** toosave your Google+ configuration.</span></span>

