---
title: "Azure Active Directory B2C: configuración de LinkedIn | Microsoft Docs"
description: "Proporcionar a los consumidores registro e inicio de sesión con cuentas de LinkedIn en las aplicaciones protegidas por Azure Active Directory B2C"
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
ms.openlocfilehash: 1a6c4b19261aa34e668554ccad2b6340cddf9bf5
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/18/2017
---
# <a name="azure-active-directory-b2c-provide-sign-up-and-sign-in-to-consumers-with-linkedin-accounts"></a><span data-ttu-id="2bbfd-103">Azure Active Directory B2C: provisión de registro e inicio de sesión a los consumidores con cuentas de LinkedIn</span><span class="sxs-lookup"><span data-stu-id="2bbfd-103">Azure Active Directory B2C: Provide sign-up and sign-in to consumers with LinkedIn accounts</span></span>
## <a name="create-a-linkedin-application"></a><span data-ttu-id="2bbfd-104">Creación de una aplicación de LinkedIn</span><span class="sxs-lookup"><span data-stu-id="2bbfd-104">Create a LinkedIn application</span></span>
<span data-ttu-id="2bbfd-105">Para usar LinkedIn como proveedor de identidades en Azure Active Directory (Azure AD) B2C, primero debe crear una aplicación de LinkedIn y suministrarle los parámetros correctos.</span><span class="sxs-lookup"><span data-stu-id="2bbfd-105">To use LinkedIn as an identity provider in Azure Active Directory (Azure AD) B2C, you need to create a LinkedIn application and supply it with the right parameters.</span></span> <span data-ttu-id="2bbfd-106">Necesita una cuenta de LinkedIn para ello.</span><span class="sxs-lookup"><span data-stu-id="2bbfd-106">You need a LinkedIn account to do this.</span></span> <span data-ttu-id="2bbfd-107">Si no tiene una, puede obtenerla en [https://www.linkedin.com/](https://www.linkedin.com/).</span><span class="sxs-lookup"><span data-stu-id="2bbfd-107">If you don’t have one, you can get it at [https://www.linkedin.com/](https://www.linkedin.com/).</span></span>

1. <span data-ttu-id="2bbfd-108">Vaya al [sitio web para desarrolladores de LinkedIn](https://www.developer.linkedin.com/) e inicie sesión con las credenciales de su cuenta de LinkedIn.</span><span class="sxs-lookup"><span data-stu-id="2bbfd-108">Go to the [LinkedIn Developers website](https://www.developer.linkedin.com/) and sign in with your LinkedIn account credentials.</span></span>
2. <span data-ttu-id="2bbfd-109">Haga clic en **My Apps** (Mis aplicaciones) en la barra de menús superior y, luego, en **Create Application** (Crear aplicación).</span><span class="sxs-lookup"><span data-stu-id="2bbfd-109">Click **My Apps** in the top menu bar and then click **Create Application**.</span></span>
   
    ![LinkedIn - nueva aplicación](./media/active-directory-b2c-setup-li-app/linkedin-new-app.png)
3. <span data-ttu-id="2bbfd-111">En el formulario **Create a New Application** (Crea una nueva aplicación), rellene la información relevante (**nombre de la empresa**, **nombre**, **descripción**, **URL del logo de la aplicación**, **uso de la aplicación**, **URL del sitio web**, **correo electrónico de empresa** y **teléfono de empresa**).</span><span class="sxs-lookup"><span data-stu-id="2bbfd-111">In the **Create a New Application** form, fill in the relevant information (**Company Name**, **Name**, **Description**, **Application Logo URL**, **Application Use**, **Website URL**, **Business Email** and **Business Phone**).</span></span>
4. <span data-ttu-id="2bbfd-112">Acepte las **condiciones de uso de API de LinkedIn** y haga clic en **Submit** (Enviar).</span><span class="sxs-lookup"><span data-stu-id="2bbfd-112">Agree to the **LinkedIn API Terms of Use** and click **Submit**.</span></span>
   
    ![LinkedIn - registrar aplicación](./media/active-directory-b2c-setup-li-app/linkedin-register-app.png)
5. <span data-ttu-id="2bbfd-114">Copie los valores de **Client ID** y **Client Secret**.</span><span class="sxs-lookup"><span data-stu-id="2bbfd-114">Copy the values of **Client ID** and **Client Secret**.</span></span> <span data-ttu-id="2bbfd-115">[Los encontrará en **Authentication Keys** (Claves de autenticación)]. Necesitará ambos para configurar LinkedIn como proveedor de identidades de su inquilino.</span><span class="sxs-lookup"><span data-stu-id="2bbfd-115">(You can find them under **Authentication Keys**.) You will need both of them to configure LinkedIn as an identity provider in your tenant.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="2bbfd-116">**secreto de cliente** es una credencial de seguridad importante.</span><span class="sxs-lookup"><span data-stu-id="2bbfd-116">**Client Secret** is an important security credential.</span></span>
   > 
   > 
6. <span data-ttu-id="2bbfd-117">Escriba `https://login.microsoftonline.com/te/{tenant}/oauth2/authresp` en el campo **Authorized Redirect URLs** (Direcciones URL de redirección autorizadas) (en **OAuth 2.0**).</span><span class="sxs-lookup"><span data-stu-id="2bbfd-117">Enter `https://login.microsoftonline.com/te/{tenant}/oauth2/authresp` in the **Authorized Redirect URLs** field (under **OAuth 2.0**).</span></span> <span data-ttu-id="2bbfd-118">Reemplace **{tenant}** por el nombre de su inquilino (por ejemplo, contoso.onmicrosoft.com).</span><span class="sxs-lookup"><span data-stu-id="2bbfd-118">Replace **{tenant}** with your tenant's name (for example, contoso.onmicrosoft.com).</span></span> <span data-ttu-id="2bbfd-119">Haga clic en **Add** (Agregar) y después en **Update** (Actualizar).</span><span class="sxs-lookup"><span data-stu-id="2bbfd-119">Click **Add**, and then click **Update**.</span></span> <span data-ttu-id="2bbfd-120">El valor de **{tenant}** distingue mayúsculas de minúsculas.</span><span class="sxs-lookup"><span data-stu-id="2bbfd-120">The **{tenant}** value is case-sensitive.</span></span>
   
    ![LinkedIn - configurar aplicación](./media/active-directory-b2c-setup-li-app/linkedin-setup.png)

## <a name="configure-linkedin-as-an-identity-provider-in-your-tenant"></a><span data-ttu-id="2bbfd-122">Configuración de LinkedIn como proveedor de identidades del inquilino</span><span class="sxs-lookup"><span data-stu-id="2bbfd-122">Configure LinkedIn as an identity provider in your tenant</span></span>
1. <span data-ttu-id="2bbfd-123">Siga estos pasos para [desplazarse hasta la hoja de características B2C](active-directory-b2c-app-registration.md#navigate-to-b2c-settings) en el Portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="2bbfd-123">Follow these steps to [navigate to the B2C features blade](active-directory-b2c-app-registration.md#navigate-to-b2c-settings) on the Azure portal.</span></span>
2. <span data-ttu-id="2bbfd-124">En la hoja de características B2C, haga clic en **Proveedores de identidades**.</span><span class="sxs-lookup"><span data-stu-id="2bbfd-124">On the B2C features blade, click **Identity providers**.</span></span>
3. <span data-ttu-id="2bbfd-125">Haga clic en **+Agregar** en la parte superior de la hoja.</span><span class="sxs-lookup"><span data-stu-id="2bbfd-125">Click **+Add** at the top of the blade.</span></span>
4. <span data-ttu-id="2bbfd-126">Proporcione un **Nombre** descriptivo para la configuración del proveedor de identidades.</span><span class="sxs-lookup"><span data-stu-id="2bbfd-126">Provide a friendly **Name** for the identity provider configuration.</span></span> <span data-ttu-id="2bbfd-127">Por ejemplo "LI".</span><span class="sxs-lookup"><span data-stu-id="2bbfd-127">For example, enter "LI".</span></span>
5. <span data-ttu-id="2bbfd-128">Haga clic en **Identity provider type** (Tipo de proveedor de identidades), seleccione **LinkedIn** y haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="2bbfd-128">Click **Identity provider type**, select **LinkedIn**, and click **OK**.</span></span>
6. <span data-ttu-id="2bbfd-129">Haga clic en **Set up this identity provider** (Configurar este proveedor de identidades) y escriba el identificador de cliente y el secreto de cliente de la aplicación de LinkedIn que creó anteriormente.</span><span class="sxs-lookup"><span data-stu-id="2bbfd-129">Click **Set up this identity provider** and enter the client ID and client secret of the LinkedIn application that you created earlier.</span></span>
7. <span data-ttu-id="2bbfd-130">Haga clic en **OK** (Aceptar) y en **Create** (Crear) para guardar la configuración de LinkedIn.</span><span class="sxs-lookup"><span data-stu-id="2bbfd-130">Click **OK** and then click **Create** to save your LinkedIn configuration.</span></span>

