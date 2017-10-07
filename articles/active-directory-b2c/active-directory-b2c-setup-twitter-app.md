---
title: "Azure Active Directory B2C: configuración de Twitter | Microsoft Docs"
description: "Proporcionar tooconsumers registrarse e iniciar sesión con cuentas de Twitter en las aplicaciones que están protegidas por Azure Active Directory B2C."
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
ms.openlocfilehash: 275c5c73fd5e8e5075e77fee942cbc1b5e1586cf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-b2c-provide-sign-up-and-sign-in-tooconsumers-with-twitter-accounts"></a><span data-ttu-id="a196a-103">Azure B2C Directory Active: Proporcionar tooconsumers registrarse e iniciar sesión con cuentas de Twitter</span><span class="sxs-lookup"><span data-stu-id="a196a-103">Azure Active Directory B2C: Provide sign-up and sign-in tooconsumers with Twitter accounts</span></span>

> [!NOTE]
> <span data-ttu-id="a196a-104">Esta característica se encuentra en su versión preliminar.</span><span class="sxs-lookup"><span data-stu-id="a196a-104">This feature is in preview.</span></span>
> 

## <a name="create-a-twitter-application"></a><span data-ttu-id="a196a-105">Crear una aplicación de Twitter</span><span class="sxs-lookup"><span data-stu-id="a196a-105">Create a Twitter application</span></span>
<span data-ttu-id="a196a-106">toouse Twitter como proveedor de identidades en Azure Active Directory (Azure AD) B2C, necesita una aplicación de Twitter toocreate y proporcionarle los parámetros correctos de Hola.</span><span class="sxs-lookup"><span data-stu-id="a196a-106">toouse Twitter as an identity provider in Azure Active Directory (Azure AD) B2C, you need toocreate a Twitter application and supply it with hello right parameters.</span></span> <span data-ttu-id="a196a-107">Se necesita un toodo de cuenta de desarrollador de Twitter.</span><span class="sxs-lookup"><span data-stu-id="a196a-107">You need a Twitter developer account toodo this.</span></span> <span data-ttu-id="a196a-108">Si no tiene una, puede obtenerla en [https://dev.twitter.com/](https://dev.twitter.com/).</span><span class="sxs-lookup"><span data-stu-id="a196a-108">If you don’t have one, you can get it at [https://dev.twitter.com/](https://dev.twitter.com/).</span></span>

1. <span data-ttu-id="a196a-109">Vaya toohello [sitio Web del desarrollador de Twitter](https://dev.twitter.com/) e inicie sesión con sus credenciales.</span><span class="sxs-lookup"><span data-stu-id="a196a-109">Go toohello [Twitter developer's website](https://dev.twitter.com/) and sign in with your credentials.</span></span>
2. <span data-ttu-id="a196a-110">Haga clic en **Mis aplicaciones** en **Herramientas y soporte técnico** y, después, haga clic en **Crear una aplicación nueva**.</span><span class="sxs-lookup"><span data-stu-id="a196a-110">Click **My apps** under **Tools & Support** and then click **Create New App**.</span></span> 
3. <span data-ttu-id="a196a-111">En el formulario de hello, proporcione un valor para hello **nombre**, **descripción**, y **sitio Web**.</span><span class="sxs-lookup"><span data-stu-id="a196a-111">In hello form, provide a value for hello **Name**, **Description**, and **Website**.</span></span>
4. <span data-ttu-id="a196a-112">Para hello **dirección URL de devolución de llamada**, escriba `https://login.microsoftonline.com/te/{tenant}/oauth2/authresp`.</span><span class="sxs-lookup"><span data-stu-id="a196a-112">For hello **Callback URL**, enter `https://login.microsoftonline.com/te/{tenant}/oauth2/authresp`.</span></span> <span data-ttu-id="a196a-113">Asegúrese de que tooreplace **{tenant}** con el nombre de su inquilino (por ejemplo, contosob2c.onmicrosoft.com).</span><span class="sxs-lookup"><span data-stu-id="a196a-113">Make sure tooreplace **{tenant}** with your tenant's name (for example, contosob2c.onmicrosoft.com).</span></span>
5. <span data-ttu-id="a196a-114">Comprobar Hola cuadro tooagree toohello **acuerdo para desarrolladores de** y haga clic en **crear su aplicación de Twitter**.</span><span class="sxs-lookup"><span data-stu-id="a196a-114">Check hello box tooagree toohello **Developer Agreement** and click **Create your Twitter application**.</span></span>
6. <span data-ttu-id="a196a-115">Una vez creada la aplicación hello, haga clic en **claves y Tokens de acceso**.</span><span class="sxs-lookup"><span data-stu-id="a196a-115">Once hello app is created, click **Keys and Access Tokens**.</span></span>
7. <span data-ttu-id="a196a-116">Copiar valor de Hola de **clave de consumidor** y **secreto de consumidor**.</span><span class="sxs-lookup"><span data-stu-id="a196a-116">Copy hello value of **Consumer Key** and **Consumer Secret**.</span></span> <span data-ttu-id="a196a-117">Necesitará ambos tooconfigure Twitter como proveedor de identidades en su inquilino.</span><span class="sxs-lookup"><span data-stu-id="a196a-117">You will need both of them tooconfigure Twitter as an identity provider in your tenant.</span></span>

## <a name="configure-twitter-as-an-identity-provider-in-your-tenant"></a><span data-ttu-id="a196a-118">Configuración de Twitter como proveedor de identidades del inquilino</span><span class="sxs-lookup"><span data-stu-id="a196a-118">Configure Twitter as an identity provider in your tenant</span></span>
1. <span data-ttu-id="a196a-119">Siga estos pasos demasiado[navegue hoja de características toohello B2C](active-directory-b2c-app-registration.md#navigate-to-b2c-settings) en hello portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="a196a-119">Follow these steps too[navigate toohello B2C features blade](active-directory-b2c-app-registration.md#navigate-to-b2c-settings) on hello Azure portal.</span></span>
2. <span data-ttu-id="a196a-120">En la hoja de características de hello B2C, haga clic en **proveedores de identidades**.</span><span class="sxs-lookup"><span data-stu-id="a196a-120">On hello B2C features blade, click **Identity providers**.</span></span>
3. <span data-ttu-id="a196a-121">Haga clic en **+ agregar** princip Hola de hoja de Hola.</span><span class="sxs-lookup"><span data-stu-id="a196a-121">Click **+Add** at hello top of hello blade.</span></span>
4. <span data-ttu-id="a196a-122">Proporcionar descriptivo **nombre** para la configuración del proveedor de identidades Hola.</span><span class="sxs-lookup"><span data-stu-id="a196a-122">Provide a friendly **Name** for hello identity provider configuration.</span></span> <span data-ttu-id="a196a-123">Por ejemplo, escriba "Twitter".</span><span class="sxs-lookup"><span data-stu-id="a196a-123">For example, enter "Twitter".</span></span>
5. <span data-ttu-id="a196a-124">Haga clic en **Tipo de proveedor de identidades**, seleccione **Twitter** y haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="a196a-124">Click **Identity provider type**, select **Twitter**, and click **OK**.</span></span>
6. <span data-ttu-id="a196a-125">Haga clic en **configurar este proveedor de identidades** y escriba Hola Twitter **clave de consumidor** para hello **Id. de cliente** y Hola Twitter **secreto del consumidor**para hello **secreto de cliente**.</span><span class="sxs-lookup"><span data-stu-id="a196a-125">Click **Set up this identity provider** and enter hello Twitter **Consumer Key** for hello **Client id** and hello Twitter **Consumer Secret** for hello **Client secret**.</span></span>
7. <span data-ttu-id="a196a-126">Haga clic en **Aceptar**y, a continuación, haga clic en **crear** toosave la configuración de Twitter.</span><span class="sxs-lookup"><span data-stu-id="a196a-126">Click **OK**, and then click **Create** toosave your Twitter configuration.</span></span>

