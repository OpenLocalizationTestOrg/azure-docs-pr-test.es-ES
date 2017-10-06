---
title: "Azure Active Directory B2C: configuración de la cuenta Microsoft | Microsoft Docs"
description: "Proporcionar tooconsumers registrarse e iniciar sesión con cuentas de Microsoft en las aplicaciones que están protegidas por Azure Active Directory B2C."
services: active-directory-b2c
documentationcenter: 
author: swkrish
manager: mbaldwin
editor: bryanla
ms.assetid: 06407322-142c-4cb3-9106-a8d752c4c853
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/06/2016
ms.author: swkrish
ms.openlocfilehash: bec4777f003c459030f68c35b24f0e4bcddf84ae
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-b2c-provide-sign-up-and-sign-in-tooconsumers-with-microsoft-accounts"></a><span data-ttu-id="1a198-103">Azure B2C Directory Active: Proporcionar tooconsumers registrarse e iniciar sesión con cuentas de Microsoft</span><span class="sxs-lookup"><span data-stu-id="1a198-103">Azure Active Directory B2C: Provide sign-up and sign-in tooconsumers with Microsoft accounts</span></span>
## <a name="create-a-microsoft-account-application"></a><span data-ttu-id="1a198-104">Creación de una aplicación de cuenta Microsoft</span><span class="sxs-lookup"><span data-stu-id="1a198-104">Create a Microsoft account application</span></span>
<span data-ttu-id="1a198-105">toouse cuenta de Microsoft como proveedor de identidades en Azure Active Directory (Azure AD) B2C, necesita toocreate una aplicación de la cuenta de Microsoft y suministrarle los parámetros correctos de Hola.</span><span class="sxs-lookup"><span data-stu-id="1a198-105">toouse Microsoft account as an identity provider in Azure Active Directory (Azure AD) B2C, you need toocreate a Microsoft account application and supply it with hello right parameters.</span></span> <span data-ttu-id="1a198-106">Se necesita un toodo de cuenta de Microsoft.</span><span class="sxs-lookup"><span data-stu-id="1a198-106">You need a Microsoft account toodo this.</span></span> <span data-ttu-id="1a198-107">Si no tiene una, puede obtenerla en [https://www.live.com/](https://www.live.com/).</span><span class="sxs-lookup"><span data-stu-id="1a198-107">If you don’t have one, you can get it at [https://www.live.com/](https://www.live.com/).</span></span>

1. <span data-ttu-id="1a198-108">Vaya toohello [Portal de registro de aplicación de Microsoft](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList) e inicie sesión con sus credenciales de cuenta de Microsoft.</span><span class="sxs-lookup"><span data-stu-id="1a198-108">Go toohello [Microsoft Application Registration Portal](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList) and sign in with your Microsoft account credentials.</span></span>
2. <span data-ttu-id="1a198-109">Haga clic en **Agregar una aplicación**.</span><span class="sxs-lookup"><span data-stu-id="1a198-109">Click **Add an app**.</span></span>
   
    ![Cuenta Microsoft: adición de una aplicación nueva](./media/active-directory-b2c-setup-msa-app/msa-add-new-app.png)
3. <span data-ttu-id="1a198-111">Especifique un **nombre** para la aplicación y haga clic en **Crear aplicación**.</span><span class="sxs-lookup"><span data-stu-id="1a198-111">Provide a **Name** for your application and click **Create application**.</span></span>
   
    ![Cuenta Microsoft: nombre de la aplicación](./media/active-directory-b2c-setup-msa-app/msa-app-name.png)
4. <span data-ttu-id="1a198-113">Copiar valor de Hola de **identificador de la aplicación**. Necesitará tooconfigure cuenta de Microsoft como proveedor de identidades en su inquilino.</span><span class="sxs-lookup"><span data-stu-id="1a198-113">Copy hello value of **Application Id**. You will need it tooconfigure Microsoft account as an identity provider in your tenant.</span></span>
   
    ![Cuenta Microsoft: Id. de la aplicación](./media/active-directory-b2c-setup-msa-app/msa-app-id.png)
5. <span data-ttu-id="1a198-115">Haga clic en **Agregar plataforma** y elija **Web**.</span><span class="sxs-lookup"><span data-stu-id="1a198-115">Click on **Add platform** and choose **Web**.</span></span>
   
    ![Cuenta Microsoft: Agregar plataforma](./media/active-directory-b2c-setup-msa-app/msa-add-platform.png)
   
    ![Cuenta Microsoft: Web](./media/active-directory-b2c-setup-msa-app/msa-web.png)
6. <span data-ttu-id="1a198-118">Escriba `https://login.microsoftonline.com/te/{tenant}/oauth2/authresp` en hello **URI de redireccionamiento** campo.</span><span class="sxs-lookup"><span data-stu-id="1a198-118">Enter `https://login.microsoftonline.com/te/{tenant}/oauth2/authresp` in hello **Redirect URIs** field.</span></span> <span data-ttu-id="1a198-119">Reemplace **{tenant}** por el nombre de su inquilino (por ejemplo, contosob2c.onmicrosoft.com).</span><span class="sxs-lookup"><span data-stu-id="1a198-119">Replace **{tenant}** with your tenant's name (for example, contosob2c.onmicrosoft.com).</span></span>
   
    ![Cuenta Microsoft: dirección URL de redireccionamiento](./media/active-directory-b2c-setup-msa-app/msa-redirect-url.png)
7. <span data-ttu-id="1a198-121">Haga clic en **generar nueva contraseña** en hello **aplicación secretos** sección.</span><span class="sxs-lookup"><span data-stu-id="1a198-121">Click on **Generate New Password** under hello **Application Secrets** section.</span></span> <span data-ttu-id="1a198-122">Copiar contraseña nueva hello muestra en pantalla.</span><span class="sxs-lookup"><span data-stu-id="1a198-122">Copy hello new password displayed on screen.</span></span> <span data-ttu-id="1a198-123">Necesitará tooconfigure cuenta de Microsoft como proveedor de identidades en su inquilino.</span><span class="sxs-lookup"><span data-stu-id="1a198-123">You will need it tooconfigure Microsoft account as an identity provider in your tenant.</span></span> <span data-ttu-id="1a198-124">Esta contraseña es una credencial de seguridad importante.</span><span class="sxs-lookup"><span data-stu-id="1a198-124">This password is an important security credential.</span></span>
   
    ![Cuenta Microsoft: Generar nueva contraseña](./media/active-directory-b2c-setup-msa-app/msa-generate-new-password.png)
   
    ![Cuenta Microsoft: Nueva contraseña](./media/active-directory-b2c-setup-msa-app/msa-new-password.png)
8. <span data-ttu-id="1a198-127">Casilla de Hola que dice **soporte técnico del SDK de Live** en hello **opciones avanzadas** sección.</span><span class="sxs-lookup"><span data-stu-id="1a198-127">Check hello box that says **Live SDK support** under hello **Advanced Options** section.</span></span> <span data-ttu-id="1a198-128">Haga clic en **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="1a198-128">Click **Save**.</span></span>
   
    ![Cuenta Microsoft: Soporte técnico de SDK de Live](./media/active-directory-b2c-setup-msa-app/msa-live-sdk-support.png)

## <a name="configure-microsoft-account-as-an-identity-provider-in-your-tenant"></a><span data-ttu-id="1a198-130">Configuración de una cuenta Microsoft como proveedor de identidades de su inquilino</span><span class="sxs-lookup"><span data-stu-id="1a198-130">Configure Microsoft account as an identity provider in your tenant</span></span>
1. <span data-ttu-id="1a198-131">Siga estos pasos demasiado[navegue hoja de características toohello B2C](active-directory-b2c-app-registration.md#navigate-to-b2c-settings) en hello portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="1a198-131">Follow these steps too[navigate toohello B2C features blade](active-directory-b2c-app-registration.md#navigate-to-b2c-settings) on hello Azure portal.</span></span>
2. <span data-ttu-id="1a198-132">En la hoja de características de hello B2C, haga clic en **proveedores de identidades**.</span><span class="sxs-lookup"><span data-stu-id="1a198-132">On hello B2C features blade, click **Identity providers**.</span></span>
3. <span data-ttu-id="1a198-133">Haga clic en **+ agregar** princip Hola de hoja de Hola.</span><span class="sxs-lookup"><span data-stu-id="1a198-133">Click **+Add** at hello top of hello blade.</span></span>
4. <span data-ttu-id="1a198-134">Proporcionar descriptivo **nombre** para la configuración del proveedor de identidades Hola.</span><span class="sxs-lookup"><span data-stu-id="1a198-134">Provide a friendly **Name** for hello identity provider configuration.</span></span> <span data-ttu-id="1a198-135">Por ejemplo, escriba "MSA".</span><span class="sxs-lookup"><span data-stu-id="1a198-135">For example, enter "MSA".</span></span>
5. <span data-ttu-id="1a198-136">Haga clic en **Identity provider type** (Tipo de proveedor de identidades), seleccione **Microsoft account** (Cuenta Microsoft) y haga clic en **OK** (Aceptar).</span><span class="sxs-lookup"><span data-stu-id="1a198-136">Click **Identity provider type**, select **Microsoft account**, and click **OK**.</span></span>
6. <span data-ttu-id="1a198-137">Haga clic en **configurar este proveedor de identidades** y escriba Hola Id. de aplicación y la contraseña de hello aplicación de cuentas de Microsoft que creó anteriormente.</span><span class="sxs-lookup"><span data-stu-id="1a198-137">Click **Set up this identity provider** and enter hello Application Id and password of hello Microsoft account application that you created earlier.</span></span>
7. <span data-ttu-id="1a198-138">Haga clic en **Aceptar** y, a continuación, haga clic en **crear** toosave configuración de la cuenta de Microsoft.</span><span class="sxs-lookup"><span data-stu-id="1a198-138">Click **OK** and then click **Create** toosave your Microsoft account configuration.</span></span>

