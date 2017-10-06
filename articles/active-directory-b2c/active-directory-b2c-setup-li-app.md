---
title: "Azure Active Directory B2C: configuración de LinkedIn | Microsoft Docs"
description: "Proporcionar tooconsumers registrarse e iniciar sesión con cuentas de LinkedIn en las aplicaciones que están protegidas por Azure Active Directory B2C"
services: active-directory-b2c
documentationcenter: 
author: swkrish
manager: mbaldwin
editor: bryanla
ms.assetid: fa51a16b-9ce9-4e27-9eff-0869b4c4f0ef
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/06/2016
ms.author: swkrish
ms.openlocfilehash: 6c5233ef48b24968fd6383f470b5d8a969a78ecf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-b2c-provide-sign-up-and-sign-in-tooconsumers-with-linkedin-accounts"></a><span data-ttu-id="ebdf9-103">Azure B2C Directory Active: Proporcionar tooconsumers registrarse e iniciar sesión con cuentas de LinkedIn</span><span class="sxs-lookup"><span data-stu-id="ebdf9-103">Azure Active Directory B2C: Provide sign-up and sign-in tooconsumers with LinkedIn accounts</span></span>
## <a name="create-a-linkedin-application"></a><span data-ttu-id="ebdf9-104">Creación de una aplicación de LinkedIn</span><span class="sxs-lookup"><span data-stu-id="ebdf9-104">Create a LinkedIn application</span></span>
<span data-ttu-id="ebdf9-105">toouse LinkedIn como proveedor de identidades en Azure Active Directory (Azure AD) B2C, se necesita una aplicación de LinkedIn toocreate y suministrarlo con los parámetros correctos de Hola.</span><span class="sxs-lookup"><span data-stu-id="ebdf9-105">toouse LinkedIn as an identity provider in Azure Active Directory (Azure AD) B2C, you need toocreate a LinkedIn application and supply it with hello right parameters.</span></span> <span data-ttu-id="ebdf9-106">Se necesita un toodo de cuenta de LinkedIn.</span><span class="sxs-lookup"><span data-stu-id="ebdf9-106">You need a LinkedIn account toodo this.</span></span> <span data-ttu-id="ebdf9-107">Si no tiene una, puede obtenerla en [https://www.linkedin.com/](https://www.linkedin.com/).</span><span class="sxs-lookup"><span data-stu-id="ebdf9-107">If you don’t have one, you can get it at [https://www.linkedin.com/](https://www.linkedin.com/).</span></span>

1. <span data-ttu-id="ebdf9-108">Vaya toohello [sitio Web de desarrolladores de LinkedIn](https://www.developer.linkedin.com/) e inicie sesión con sus credenciales de cuenta de LinkedIn.</span><span class="sxs-lookup"><span data-stu-id="ebdf9-108">Go toohello [LinkedIn Developers website](https://www.developer.linkedin.com/) and sign in with your LinkedIn account credentials.</span></span>
2. <span data-ttu-id="ebdf9-109">Haga clic en **mis aplicaciones** en Hola barra de menús superior y, a continuación, haga clic en **crear aplicación**.</span><span class="sxs-lookup"><span data-stu-id="ebdf9-109">Click **My Apps** in hello top menu bar and then click **Create Application**.</span></span>
   
    ![LinkedIn - nueva aplicación](./media/active-directory-b2c-setup-li-app/linkedin-new-app.png)
3. <span data-ttu-id="ebdf9-111">Hola **crear una nueva aplicación** forman, rellene la información pertinente de hello (**nombre de la compañía**, **nombre**, **descripción**, **Dirección URL del logotipo de la aplicación**, **uso de las aplicaciones**, **URL del sitio Web**, **correo electrónico empresarial** y **teléfono del trabajo**).</span><span class="sxs-lookup"><span data-stu-id="ebdf9-111">In hello **Create a New Application** form, fill in hello relevant information (**Company Name**, **Name**, **Description**, **Application Logo URL**, **Application Use**, **Website URL**, **Business Email** and **Business Phone**).</span></span>
4. <span data-ttu-id="ebdf9-112">Acepta toohello **LinkedIn términos de uso de la API** y haga clic en **enviar**.</span><span class="sxs-lookup"><span data-stu-id="ebdf9-112">Agree toohello **LinkedIn API Terms of Use** and click **Submit**.</span></span>
   
    ![LinkedIn - registrar aplicación](./media/active-directory-b2c-setup-li-app/linkedin-register-app.png)
5. <span data-ttu-id="ebdf9-114">Copiar valores de hello de **Id. de cliente** y **secreto de cliente**.</span><span class="sxs-lookup"><span data-stu-id="ebdf9-114">Copy hello values of **Client ID** and **Client Secret**.</span></span> <span data-ttu-id="ebdf9-115">[Los encontrará en **Authentication Keys** (Claves de autenticación)]. Necesitará ambos tooconfigure LinkedIn como proveedor de identidades en su inquilino.</span><span class="sxs-lookup"><span data-stu-id="ebdf9-115">(You can find them under **Authentication Keys**.) You will need both of them tooconfigure LinkedIn as an identity provider in your tenant.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="ebdf9-116">**secreto de cliente** es una credencial de seguridad importante.</span><span class="sxs-lookup"><span data-stu-id="ebdf9-116">**Client Secret** is an important security credential.</span></span>
   > 
   > 
6. <span data-ttu-id="ebdf9-117">Escriba `https://login.microsoftonline.com/te/{tenant}/oauth2/authresp` en hello **autorizado redirigir las direcciones URL** campo (en **OAuth 2.0**).</span><span class="sxs-lookup"><span data-stu-id="ebdf9-117">Enter `https://login.microsoftonline.com/te/{tenant}/oauth2/authresp` in hello **Authorized Redirect URLs** field (under **OAuth 2.0**).</span></span> <span data-ttu-id="ebdf9-118">Reemplace **{tenant}** por el nombre de su inquilino (por ejemplo, contoso.onmicrosoft.com).</span><span class="sxs-lookup"><span data-stu-id="ebdf9-118">Replace **{tenant}** with your tenant's name (for example, contoso.onmicrosoft.com).</span></span> <span data-ttu-id="ebdf9-119">Haga clic en **Add** (Agregar) y después en **Update** (Actualizar).</span><span class="sxs-lookup"><span data-stu-id="ebdf9-119">Click **Add**, and then click **Update**.</span></span> <span data-ttu-id="ebdf9-120">Hola **{tenant}** valor distingue mayúsculas de minúsculas.</span><span class="sxs-lookup"><span data-stu-id="ebdf9-120">hello **{tenant}** value is case-sensitive.</span></span>
   
    ![LinkedIn - configurar aplicación](./media/active-directory-b2c-setup-li-app/linkedin-setup.png)

## <a name="configure-linkedin-as-an-identity-provider-in-your-tenant"></a><span data-ttu-id="ebdf9-122">Configuración de LinkedIn como proveedor de identidades del inquilino</span><span class="sxs-lookup"><span data-stu-id="ebdf9-122">Configure LinkedIn as an identity provider in your tenant</span></span>
1. <span data-ttu-id="ebdf9-123">Siga estos pasos demasiado[navegue hoja de características toohello B2C](active-directory-b2c-app-registration.md#navigate-to-b2c-settings) en hello portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="ebdf9-123">Follow these steps too[navigate toohello B2C features blade](active-directory-b2c-app-registration.md#navigate-to-b2c-settings) on hello Azure portal.</span></span>
2. <span data-ttu-id="ebdf9-124">En la hoja de características de hello B2C, haga clic en **proveedores de identidades**.</span><span class="sxs-lookup"><span data-stu-id="ebdf9-124">On hello B2C features blade, click **Identity providers**.</span></span>
3. <span data-ttu-id="ebdf9-125">Haga clic en **+ agregar** princip Hola de hoja de Hola.</span><span class="sxs-lookup"><span data-stu-id="ebdf9-125">Click **+Add** at hello top of hello blade.</span></span>
4. <span data-ttu-id="ebdf9-126">Proporcionar descriptivo **nombre** para la configuración del proveedor de identidades Hola.</span><span class="sxs-lookup"><span data-stu-id="ebdf9-126">Provide a friendly **Name** for hello identity provider configuration.</span></span> <span data-ttu-id="ebdf9-127">Por ejemplo "LI".</span><span class="sxs-lookup"><span data-stu-id="ebdf9-127">For example, enter "LI".</span></span>
5. <span data-ttu-id="ebdf9-128">Haga clic en **Identity provider type** (Tipo de proveedor de identidades), seleccione **LinkedIn** y haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="ebdf9-128">Click **Identity provider type**, select **LinkedIn**, and click **OK**.</span></span>
6. <span data-ttu-id="ebdf9-129">Haga clic en **configurar este proveedor de identidades** y escriba el secreto de cliente y el Id. de cliente de Hola de hello aplicación LinkedIn que creó anteriormente.</span><span class="sxs-lookup"><span data-stu-id="ebdf9-129">Click **Set up this identity provider** and enter hello client ID and client secret of hello LinkedIn application that you created earlier.</span></span>
7. <span data-ttu-id="ebdf9-130">Haga clic en **Aceptar** y, a continuación, haga clic en **crear** toosave la configuración de LinkedIn.</span><span class="sxs-lookup"><span data-stu-id="ebdf9-130">Click **OK** and then click **Create** toosave your LinkedIn configuration.</span></span>

