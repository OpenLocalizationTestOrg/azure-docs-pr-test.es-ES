---
title: "Azure Active Directory B2C: configuración de Twitter | Microsoft Docs"
description: "Proporcione funciones de registro e inicio de sesión a los consumidores con cuentas de Twitter en las aplicaciones protegidas por Azure Active Directory B2C."
services: active-directory-b2c
documentationcenter: 
author: parakhj
manager: krassk
editor: parakhj
ms.assetid: 579a6841-9329-45b8-a351-da4315a6634e
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 4/06/2017
ms.author: parakhj
ms.openlocfilehash: 82a001dd53cdddcf3b360090f3250af593c96fbb
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/18/2017
---
# <a name="azure-active-directory-b2c-provide-sign-up-and-sign-in-to-consumers-with-twitter-accounts"></a><span data-ttu-id="d367b-103">Azure Active Directory B2C: provisión de registro e inicio de sesión a los usuarios con cuentas de Twitter</span><span class="sxs-lookup"><span data-stu-id="d367b-103">Azure Active Directory B2C: Provide sign-up and sign-in to consumers with Twitter accounts</span></span>

> [!NOTE]
> <span data-ttu-id="d367b-104">Esta característica se encuentra en su versión preliminar.</span><span class="sxs-lookup"><span data-stu-id="d367b-104">This feature is in preview.</span></span>
> 

## <a name="create-a-twitter-application"></a><span data-ttu-id="d367b-105">Crear una aplicación de Twitter</span><span class="sxs-lookup"><span data-stu-id="d367b-105">Create a Twitter application</span></span>
<span data-ttu-id="d367b-106">Para usar Twitter como proveedor de identidades en Azure Active Directory (Azure AD) B2C, debe crear una aplicación de Twitter y suministrarle los parámetros correctos.</span><span class="sxs-lookup"><span data-stu-id="d367b-106">To use Twitter as an identity provider in Azure Active Directory (Azure AD) B2C, you need to create a Twitter application and supply it with the right parameters.</span></span> <span data-ttu-id="d367b-107">Necesita una cuenta de desarrollador de Twitter para hacerlo.</span><span class="sxs-lookup"><span data-stu-id="d367b-107">You need a Twitter developer account to do this.</span></span> <span data-ttu-id="d367b-108">Si no tiene una, puede obtenerla en [https://dev.twitter.com/](https://dev.twitter.com/).</span><span class="sxs-lookup"><span data-stu-id="d367b-108">If you don’t have one, you can get it at [https://dev.twitter.com/](https://dev.twitter.com/).</span></span>

1. <span data-ttu-id="d367b-109">Vaya al [sitio web para desarrolladores de Twitter](https://dev.twitter.com/) e inicie sesión con sus credenciales.</span><span class="sxs-lookup"><span data-stu-id="d367b-109">Go to the [Twitter developer's website](https://dev.twitter.com/) and sign in with your credentials.</span></span>
2. <span data-ttu-id="d367b-110">Haga clic en **Mis aplicaciones** en **Herramientas y soporte técnico** y, después, haga clic en **Crear una aplicación nueva**.</span><span class="sxs-lookup"><span data-stu-id="d367b-110">Click **My apps** under **Tools & Support** and then click **Create New App**.</span></span> 
3. <span data-ttu-id="d367b-111">En el formulario, proporcione un valor para **Nombre**, **Descripción** y **Sitio web**.</span><span class="sxs-lookup"><span data-stu-id="d367b-111">In the form, provide a value for the **Name**, **Description**, and **Website**.</span></span>
4. <span data-ttu-id="d367b-112">Para la **URL de devolución de llamada**, escriba `https://login.microsoftonline.com/te/{tenant}/oauth2/authresp`.</span><span class="sxs-lookup"><span data-stu-id="d367b-112">For the **Callback URL**, enter `https://login.microsoftonline.com/te/{tenant}/oauth2/authresp`.</span></span> <span data-ttu-id="d367b-113">Asegúrese de reemplazar **{tenant}** por el nombre de su inquilino (por ejemplo, contosob2c.onmicrosoft.com).</span><span class="sxs-lookup"><span data-stu-id="d367b-113">Make sure to replace **{tenant}** with your tenant's name (for example, contosob2c.onmicrosoft.com).</span></span>
5. <span data-ttu-id="d367b-114">Active la casilla para aceptar el **Acuerdo para desarrolladores** y haga clic en **Crear su aplicación de Twitter**.</span><span class="sxs-lookup"><span data-stu-id="d367b-114">Check the box to agree to the **Developer Agreement** and click **Create your Twitter application**.</span></span>
6. <span data-ttu-id="d367b-115">Una vez creada la aplicación, haga clic en **Claves y tokens de acceso**.</span><span class="sxs-lookup"><span data-stu-id="d367b-115">Once the app is created, click **Keys and Access Tokens**.</span></span>
7. <span data-ttu-id="d367b-116">Copie el valor de **Clave de consumidor** y **Secreto de consumidor**.</span><span class="sxs-lookup"><span data-stu-id="d367b-116">Copy the value of **Consumer Key** and **Consumer Secret**.</span></span> <span data-ttu-id="d367b-117">Necesitará los dos para configurar Twitter como proveedor de identidades de su inquilino.</span><span class="sxs-lookup"><span data-stu-id="d367b-117">You will need both of them to configure Twitter as an identity provider in your tenant.</span></span>

## <a name="configure-twitter-as-an-identity-provider-in-your-tenant"></a><span data-ttu-id="d367b-118">Configuración de Twitter como proveedor de identidades del inquilino</span><span class="sxs-lookup"><span data-stu-id="d367b-118">Configure Twitter as an identity provider in your tenant</span></span>
1. <span data-ttu-id="d367b-119">Siga estos pasos para [ir a la hoja de características de B2C](active-directory-b2c-app-registration.md#navigate-to-b2c-settings) de Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="d367b-119">Follow these steps to [navigate to the B2C features blade](active-directory-b2c-app-registration.md#navigate-to-b2c-settings) on the Azure portal.</span></span>
2. <span data-ttu-id="d367b-120">En la hoja de características B2C, haga clic en **Proveedores de identidades**.</span><span class="sxs-lookup"><span data-stu-id="d367b-120">On the B2C features blade, click **Identity providers**.</span></span>
3. <span data-ttu-id="d367b-121">Haga clic en **+Agregar** en la parte superior de la hoja.</span><span class="sxs-lookup"><span data-stu-id="d367b-121">Click **+Add** at the top of the blade.</span></span>
4. <span data-ttu-id="d367b-122">Proporcione un **Nombre** descriptivo para la configuración del proveedor de identidades.</span><span class="sxs-lookup"><span data-stu-id="d367b-122">Provide a friendly **Name** for the identity provider configuration.</span></span> <span data-ttu-id="d367b-123">Por ejemplo, escriba "Twitter".</span><span class="sxs-lookup"><span data-stu-id="d367b-123">For example, enter "Twitter".</span></span>
5. <span data-ttu-id="d367b-124">Haga clic en **Tipo de proveedor de identidades**, seleccione **Twitter** y haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="d367b-124">Click **Identity provider type**, select **Twitter**, and click **OK**.</span></span>
6. <span data-ttu-id="d367b-125">Haga clic en **Configurar este proveedor de identidades** y escriba la **Clave de consumidor** de Twitter para el **Id. de cliente** y el **Secreto de consumidor** de Twitter para el **Secreto de cliente**.</span><span class="sxs-lookup"><span data-stu-id="d367b-125">Click **Set up this identity provider** and enter the Twitter **Consumer Key** for the **Client id** and the Twitter **Consumer Secret** for the **Client secret**.</span></span>
7. <span data-ttu-id="d367b-126">Haga clic en **Aceptar** y luego en **Crear** para guardar la configuración de Twitter.</span><span class="sxs-lookup"><span data-stu-id="d367b-126">Click **OK**, and then click **Create** to save your Twitter configuration.</span></span>

