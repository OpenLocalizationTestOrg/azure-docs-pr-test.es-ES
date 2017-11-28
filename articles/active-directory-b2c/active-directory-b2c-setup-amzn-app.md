---
title: "Azure Active Directory B2C: configuración de Amazon | Microsoft Docs"
description: "Proporcionar registro e inicio de sesión a los consumidores con cuentas de Amazon en las aplicaciones protegidas por Azure Active Directory B2C"
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
ms.openlocfilehash: dcc97e1b7f6287bd7692c52bf068950065a26572
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/18/2017
---
# <a name="azure-active-directory-b2c-provide-sign-up-and-sign-in-to-consumers-with-amazon-accounts"></a><span data-ttu-id="bd7cf-103">Azure Active Directory B2C: proporcionar a los consumidores registro e inicio de sesión con cuentas de Amazon</span><span class="sxs-lookup"><span data-stu-id="bd7cf-103">Azure Active Directory B2C: Provide sign-up and sign-in to consumers with Amazon accounts</span></span>
## <a name="create-an-amazon-application"></a><span data-ttu-id="bd7cf-104">Creación de una aplicación de Amazon</span><span class="sxs-lookup"><span data-stu-id="bd7cf-104">Create an Amazon application</span></span>
<span data-ttu-id="bd7cf-105">Para usar Amazon como proveedor de identidades en Azure Active Directory (Azure AD) B2C, debe crear una aplicación de Amazon y suministrarle los parámetros correctos.</span><span class="sxs-lookup"><span data-stu-id="bd7cf-105">To use Amazon as an identity provider in Azure Active Directory (Azure AD) B2C, you need to create an Amazon application and supply it with the right parameters.</span></span> <span data-ttu-id="bd7cf-106">Necesita una cuenta de Amazon para ello.</span><span class="sxs-lookup"><span data-stu-id="bd7cf-106">You need an Amazon account to do this.</span></span> <span data-ttu-id="bd7cf-107">Si no tiene una, puede obtenerla en [http://www.amazon.com/](http://www.amazon.com/).</span><span class="sxs-lookup"><span data-stu-id="bd7cf-107">If you don’t have one, you can get it at [http://www.amazon.com/](http://www.amazon.com/).</span></span>

1. <span data-ttu-id="bd7cf-108">Vaya a [Amazon Developer Center](https://login.amazon.com/) e inicie sesión con las credenciales de su cuenta de Amazon.</span><span class="sxs-lookup"><span data-stu-id="bd7cf-108">Go to the [Amazon Developer Center](https://login.amazon.com/) and sign in with your Amazon account credentials.</span></span>
2. <span data-ttu-id="bd7cf-109">Si aún no lo ha hecho, haga clic en **Sign up**(Registro), siga los pasos de registro para desarrolladores y acepte la directiva.</span><span class="sxs-lookup"><span data-stu-id="bd7cf-109">If you have not already done so, click **Sign Up**, follow the developer registration steps, and accept the policy.</span></span>
3. <span data-ttu-id="bd7cf-110">Haga clic en **Register new application**(Registrar nueva aplicación).</span><span class="sxs-lookup"><span data-stu-id="bd7cf-110">Click **Register new application**.</span></span>
   
    ![Registrar una nueva aplicación en el sitio web de Amazon](./media/active-directory-b2c-setup-amzn-app/amzn-new-app.png)
4. <span data-ttu-id="bd7cf-112">Especifique la información de la aplicación [**Name** (Nombre), **Description** (Descripción) y **Privacy Notice URL** (Dirección URL de aviso de privacidad)] y haga clic en **Save** (Guardar).</span><span class="sxs-lookup"><span data-stu-id="bd7cf-112">Provide application information (**Name**, **Description**, and **Privacy Notice URL**) and click **Save**.</span></span>
   
    ![Proporcionar información de la aplicación para registrar una nueva aplicación en Amazon](./media/active-directory-b2c-setup-amzn-app/amzn-register-app.png)
5. <span data-ttu-id="bd7cf-114">En la sección **Web Settings** (Configuración web), copie los valores **Client ID** (Id. de cliente) y **Client Secret** (Secreto de cliente).</span><span class="sxs-lookup"><span data-stu-id="bd7cf-114">In the **Web Settings** section, copy the values of **Client ID** and **Client Secret**.</span></span> <span data-ttu-id="bd7cf-115">[Para verlo, es preciso hacer clic en el botón **Show Secret** (Mostrar secreto)]. Necesitará ambos para configurar Amazon como proveedor de identidades de su inquilino.</span><span class="sxs-lookup"><span data-stu-id="bd7cf-115">(You need to click the **Show Secret** button to see this.) You need both of them to configure Amazon as an identity provider in your tenant.</span></span> <span data-ttu-id="bd7cf-116">Haga clic en **Edit** (Editar) en la parte inferior de la sección.</span><span class="sxs-lookup"><span data-stu-id="bd7cf-116">Click **Edit** at the bottom of the section.</span></span> <span data-ttu-id="bd7cf-117">**secreto de cliente** es una credencial de seguridad importante.</span><span class="sxs-lookup"><span data-stu-id="bd7cf-117">**Client Secret** is an important security credential.</span></span>
   
    ![Proporcionar el identificador de cliente y el secreto de cliente para la nueva aplicación en Amazon](./media/active-directory-b2c-setup-amzn-app/amzn-client-secret.png)
6. <span data-ttu-id="bd7cf-119">Escriba `https://login.microsoftonline.com` en el campo **Allowed JavaScript Origins** (Orígenes de JavaScript permitidos) y `https://login.microsoftonline.com/te/{tenant}/oauth2/authresp` en el campo **Allowed Return URLs** (Direcciones URL de retorno permitidas).</span><span class="sxs-lookup"><span data-stu-id="bd7cf-119">Enter `https://login.microsoftonline.com` in the **Allowed JavaScript Origins** field and `https://login.microsoftonline.com/te/{tenant}/oauth2/authresp` in the **Allowed Return URLs** field.</span></span> <span data-ttu-id="bd7cf-120">Reemplace **{tenant}** por el nombre de su inquilino (por ejemplo, contoso.onmicrosoft.com).</span><span class="sxs-lookup"><span data-stu-id="bd7cf-120">Replace **{tenant}** with your tenant's name (for example, contoso.onmicrosoft.com).</span></span> <span data-ttu-id="bd7cf-121">Haga clic en **Save**.</span><span class="sxs-lookup"><span data-stu-id="bd7cf-121">Click **Save**.</span></span> <span data-ttu-id="bd7cf-122">El valor de **{tenant}** distingue mayúsculas de minúsculas.</span><span class="sxs-lookup"><span data-stu-id="bd7cf-122">The **{tenant}** value is case-sensitive.</span></span>
   
    ![Proporcionar orígenes de JavaScript y direcciones URL de retorno para la nueva aplicación en Amazon](./media/active-directory-b2c-setup-amzn-app/amzn-urls.png)

## <a name="configure-amazon-as-an-identity-provider-in-your-tenant"></a><span data-ttu-id="bd7cf-124">Configuración de Amazon como proveedor de identidades del inquilino</span><span class="sxs-lookup"><span data-stu-id="bd7cf-124">Configure Amazon as an identity provider in your tenant</span></span>
1. <span data-ttu-id="bd7cf-125">Siga estos pasos para [ir a la hoja de características de B2C](active-directory-b2c-app-registration.md#navigate-to-b2c-settings) del Portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="bd7cf-125">Follow these steps to [navigate to the B2C features blade](active-directory-b2c-app-registration.md#navigate-to-b2c-settings) on the Azure portal.</span></span>
2. <span data-ttu-id="bd7cf-126">En la hoja de características B2C, haga clic en **Proveedores de identidades**.</span><span class="sxs-lookup"><span data-stu-id="bd7cf-126">On the B2C features blade, click **Identity providers**.</span></span>
3. <span data-ttu-id="bd7cf-127">Haga clic en **+Agregar** en la parte superior de la hoja.</span><span class="sxs-lookup"><span data-stu-id="bd7cf-127">Click **+Add** at the top of the blade.</span></span>
4. <span data-ttu-id="bd7cf-128">Proporcione un **Nombre** descriptivo para la configuración del proveedor de identidades.</span><span class="sxs-lookup"><span data-stu-id="bd7cf-128">Provide a friendly **Name** for the identity provider configuration.</span></span> <span data-ttu-id="bd7cf-129">Por ejemplo, "Amzn".</span><span class="sxs-lookup"><span data-stu-id="bd7cf-129">For example, enter "Amzn".</span></span>
5. <span data-ttu-id="bd7cf-130">Haga clic en **Identity provider type** (Tipo de proveedor de identidades), seleccione **Amazon** y haga clic en **OK** (Aceptar).</span><span class="sxs-lookup"><span data-stu-id="bd7cf-130">Click **Identity provider type**, select **Amazon**, and click **OK**.</span></span>
6. <span data-ttu-id="bd7cf-131">Haga clic en **Set up this identity provider** (Configurar este proveedor de identidades) y escriba el identificador de cliente y el secreto de cliente de la aplicación de Amazon que creó anteriormente.</span><span class="sxs-lookup"><span data-stu-id="bd7cf-131">Click **Set up this identity provider** and enter the client ID and client secret of the Amazon application that you created earlier.</span></span>
7. <span data-ttu-id="bd7cf-132">Haga clic en **OK** (Aceptar) y, luego, en **Create** (Crear) para guardar la configuración de Amazon.</span><span class="sxs-lookup"><span data-stu-id="bd7cf-132">Click **OK** and then click **Create** to save your Amazon configuration.</span></span>

