---
title: "Azure Active Directory B2C: configuración de Amazon | Microsoft Docs"
description: "Proporcionar tooconsumers registrarse e iniciar sesión con cuentas de Amazon en las aplicaciones que están protegidas por Azure Active Directory B2C."
services: active-directory-b2c
documentationcenter: 
author: swkrish
manager: mbaldwin
editor: bryanla
ms.assetid: 77c099bb-a005-4d75-87f9-f61e3de48725
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/06/2016
ms.author: swkrish
ms.openlocfilehash: 60d7c4b76d9d3e86ed535765329abed07f1e5996
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-b2c-provide-sign-up-and-sign-in-tooconsumers-with-amazon-accounts"></a><span data-ttu-id="cfcc3-103">Azure B2C Directory Active: Proporcionar tooconsumers registrarse e iniciar sesión con cuentas de Amazon</span><span class="sxs-lookup"><span data-stu-id="cfcc3-103">Azure Active Directory B2C: Provide sign-up and sign-in tooconsumers with Amazon accounts</span></span>
## <a name="create-an-amazon-application"></a><span data-ttu-id="cfcc3-104">Creación de una aplicación de Amazon</span><span class="sxs-lookup"><span data-stu-id="cfcc3-104">Create an Amazon application</span></span>
<span data-ttu-id="cfcc3-105">toouse Amazon como proveedor de identidades en Azure Active Directory (Azure AD) B2C, necesita toocreate una aplicación de Amazon y proporcionarle los parámetros correctos de Hola.</span><span class="sxs-lookup"><span data-stu-id="cfcc3-105">toouse Amazon as an identity provider in Azure Active Directory (Azure AD) B2C, you need toocreate an Amazon application and supply it with hello right parameters.</span></span> <span data-ttu-id="cfcc3-106">Se necesita un toodo de cuenta de Amazon.</span><span class="sxs-lookup"><span data-stu-id="cfcc3-106">You need an Amazon account toodo this.</span></span> <span data-ttu-id="cfcc3-107">Si no tiene una, puede obtenerla en [http://www.amazon.com/](http://www.amazon.com/).</span><span class="sxs-lookup"><span data-stu-id="cfcc3-107">If you don’t have one, you can get it at [http://www.amazon.com/](http://www.amazon.com/).</span></span>

1. <span data-ttu-id="cfcc3-108">Vaya toohello [Centro para desarrolladores de Amazon](https://login.amazon.com/) e inicie sesión con sus credenciales de cuenta de Amazon.</span><span class="sxs-lookup"><span data-stu-id="cfcc3-108">Go toohello [Amazon Developer Center](https://login.amazon.com/) and sign in with your Amazon account credentials.</span></span>
2. <span data-ttu-id="cfcc3-109">Si no lo ha hecho ya, haga clic en **Sign Up**, siga los pasos de registro del desarrollador de Hola y acepte la política de Hola.</span><span class="sxs-lookup"><span data-stu-id="cfcc3-109">If you have not already done so, click **Sign Up**, follow hello developer registration steps, and accept hello policy.</span></span>
3. <span data-ttu-id="cfcc3-110">Haga clic en **Register new application**(Registrar nueva aplicación).</span><span class="sxs-lookup"><span data-stu-id="cfcc3-110">Click **Register new application**.</span></span>
   
    ![Registrar una nueva aplicación en el sitio Web de Amazon Hola](./media/active-directory-b2c-setup-amzn-app/amzn-new-app.png)
4. <span data-ttu-id="cfcc3-112">Especifique la información de la aplicación [**Name** (Nombre), **Description** (Descripción) y **Privacy Notice URL** (Dirección URL de aviso de privacidad)] y haga clic en **Save** (Guardar).</span><span class="sxs-lookup"><span data-stu-id="cfcc3-112">Provide application information (**Name**, **Description**, and **Privacy Notice URL**) and click **Save**.</span></span>
   
    ![Proporcionar información de la aplicación para registrar una nueva aplicación en Amazon](./media/active-directory-b2c-setup-amzn-app/amzn-register-app.png)
5. <span data-ttu-id="cfcc3-114">Hola **configuración Web** sección, copia los valores de hello de **Id. de cliente** y **secreto de cliente**.</span><span class="sxs-lookup"><span data-stu-id="cfcc3-114">In hello **Web Settings** section, copy hello values of **Client ID** and **Client Secret**.</span></span> <span data-ttu-id="cfcc3-115">(Debe hello tooclick **mostrar secreto** botón toosee esto.) Necesita ambos tooconfigure Amazon como proveedor de identidades en su inquilino.</span><span class="sxs-lookup"><span data-stu-id="cfcc3-115">(You need tooclick hello **Show Secret** button toosee this.) You need both of them tooconfigure Amazon as an identity provider in your tenant.</span></span> <span data-ttu-id="cfcc3-116">Haga clic en **editar** final Hola de sección Hola.</span><span class="sxs-lookup"><span data-stu-id="cfcc3-116">Click **Edit** at hello bottom of hello section.</span></span> <span data-ttu-id="cfcc3-117">**secreto de cliente** es una credencial de seguridad importante.</span><span class="sxs-lookup"><span data-stu-id="cfcc3-117">**Client Secret** is an important security credential.</span></span>
   
    ![Proporcionar el identificador de cliente y el secreto de cliente para la nueva aplicación en Amazon](./media/active-directory-b2c-setup-amzn-app/amzn-client-secret.png)
6. <span data-ttu-id="cfcc3-119">Escriba `https://login.microsoftonline.com` en hello **orígenes de JavaScript permite** campo y `https://login.microsoftonline.com/te/{tenant}/oauth2/authresp` en hello **permite direcciones URL de retorno** campo.</span><span class="sxs-lookup"><span data-stu-id="cfcc3-119">Enter `https://login.microsoftonline.com` in hello **Allowed JavaScript Origins** field and `https://login.microsoftonline.com/te/{tenant}/oauth2/authresp` in hello **Allowed Return URLs** field.</span></span> <span data-ttu-id="cfcc3-120">Reemplace **{tenant}** por el nombre de su inquilino (por ejemplo, contoso.onmicrosoft.com).</span><span class="sxs-lookup"><span data-stu-id="cfcc3-120">Replace **{tenant}** with your tenant's name (for example, contoso.onmicrosoft.com).</span></span> <span data-ttu-id="cfcc3-121">Haga clic en **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="cfcc3-121">Click **Save**.</span></span> <span data-ttu-id="cfcc3-122">Hola **{tenant}** valor distingue mayúsculas de minúsculas.</span><span class="sxs-lookup"><span data-stu-id="cfcc3-122">hello **{tenant}** value is case-sensitive.</span></span>
   
    ![Proporcionar orígenes de JavaScript y direcciones URL de retorno para la nueva aplicación en Amazon](./media/active-directory-b2c-setup-amzn-app/amzn-urls.png)

## <a name="configure-amazon-as-an-identity-provider-in-your-tenant"></a><span data-ttu-id="cfcc3-124">Configuración de Amazon como proveedor de identidades del inquilino</span><span class="sxs-lookup"><span data-stu-id="cfcc3-124">Configure Amazon as an identity provider in your tenant</span></span>
1. <span data-ttu-id="cfcc3-125">Siga estos pasos demasiado[navegue hoja de características toohello B2C](active-directory-b2c-app-registration.md#navigate-to-b2c-settings) en hello portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="cfcc3-125">Follow these steps too[navigate toohello B2C features blade](active-directory-b2c-app-registration.md#navigate-to-b2c-settings) on hello Azure portal.</span></span>
2. <span data-ttu-id="cfcc3-126">En la hoja de características de hello B2C, haga clic en **proveedores de identidades**.</span><span class="sxs-lookup"><span data-stu-id="cfcc3-126">On hello B2C features blade, click **Identity providers**.</span></span>
3. <span data-ttu-id="cfcc3-127">Haga clic en **+ agregar** princip Hola de hoja de Hola.</span><span class="sxs-lookup"><span data-stu-id="cfcc3-127">Click **+Add** at hello top of hello blade.</span></span>
4. <span data-ttu-id="cfcc3-128">Proporcionar descriptivo **nombre** para la configuración del proveedor de identidades Hola.</span><span class="sxs-lookup"><span data-stu-id="cfcc3-128">Provide a friendly **Name** for hello identity provider configuration.</span></span> <span data-ttu-id="cfcc3-129">Por ejemplo, "Amzn".</span><span class="sxs-lookup"><span data-stu-id="cfcc3-129">For example, enter "Amzn".</span></span>
5. <span data-ttu-id="cfcc3-130">Haga clic en **Identity provider type** (Tipo de proveedor de identidades), seleccione **Amazon** y haga clic en **OK** (Aceptar).</span><span class="sxs-lookup"><span data-stu-id="cfcc3-130">Click **Identity provider type**, select **Amazon**, and click **OK**.</span></span>
6. <span data-ttu-id="cfcc3-131">Haga clic en **configurar este proveedor de identidades** y escriba el secreto de cliente y el Id. de cliente de Hola de hello aplicaciones de Amazon que creó anteriormente.</span><span class="sxs-lookup"><span data-stu-id="cfcc3-131">Click **Set up this identity provider** and enter hello client ID and client secret of hello Amazon application that you created earlier.</span></span>
7. <span data-ttu-id="cfcc3-132">Haga clic en **Aceptar** y, a continuación, haga clic en **crear** toosave la configuración de Amazon.</span><span class="sxs-lookup"><span data-stu-id="cfcc3-132">Click **OK** and then click **Create** toosave your Amazon configuration.</span></span>

