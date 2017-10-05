---
title: "Inicio de sesión único en aplicaciones mediante el proxy de aplicación de Azure AD | Microsoft Docs"
description: "Active el inicio de sesión único para sus aplicaciones locales publicadas mediante el proxy de aplicación de Azure AD en Azure Portal."
services: active-directory
documentationcenter: 
author: kgremban
manager: femila
ms.assetid: d94ac3f4-cd33-4c51-9d19-544a528637d4
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/20/2017
ms.author: kgremban
ms.reviewer: harshja
ms.custom: it-pro
ms.openlocfilehash: 9ddc0c1bd5f2cbb24f6761cfd041b820ee6464b8
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/03/2017
---
# <a name="password-vaulting-for-single-sign-on-with-application-proxy"></a><span data-ttu-id="ccf93-103">Almacén de contraseñas para el inicio de sesión único con el proxy de aplicación</span><span class="sxs-lookup"><span data-stu-id="ccf93-103">Password vaulting for single sign-on with Application Proxy</span></span>

<span data-ttu-id="ccf93-104">El proxy de aplicación de Azure Active Directory le ayuda a mejorar la productividad mediante la publicación de aplicaciones locales de manera que los empleados remotos puedan tener acceso seguro a estas.</span><span class="sxs-lookup"><span data-stu-id="ccf93-104">Azure Active Directory Application Proxy helps you improve productivity by publishing on-premises applications so that remote employees can securely access them, too.</span></span> <span data-ttu-id="ccf93-105">En Azure Portal, puede configurar también el inicio de sesión único (SSO) para estas aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="ccf93-105">In the Azure portal, you can also set up single sign-on (SSO) to these apps.</span></span> <span data-ttu-id="ccf93-106">Los usuarios solo necesitan autenticarse con Azure AD y podrán acceder a la aplicación de empresa sin necesidad de volver a iniciar sesión.</span><span class="sxs-lookup"><span data-stu-id="ccf93-106">Your users only need to authenticate with Azure AD, and they can access your enterprise application without having to sign in again.</span></span>

<span data-ttu-id="ccf93-107">El proxy de aplicación admite varios [modos de inicio de sesión único](application-proxy-sso-overview.md).</span><span class="sxs-lookup"><span data-stu-id="ccf93-107">Application Proxy supports several [single sign-on modes](application-proxy-sso-overview.md).</span></span> <span data-ttu-id="ccf93-108">El inicio de sesión basado en contraseña se ha creado para aplicaciones que usan una combinación de nombre de usuario/contraseña para la autenticación.</span><span class="sxs-lookup"><span data-stu-id="ccf93-108">Password-based sign-on is intended for applications that use a username/password combination for authentication.</span></span> <span data-ttu-id="ccf93-109">Al configurar el inicio de sesión basado en contraseña para su aplicación, los usuarios tendrán que iniciar sesión en la aplicación local una vez.</span><span class="sxs-lookup"><span data-stu-id="ccf93-109">When you configure password-based sign-on for your application, your users have to sign in to the on-premises application once.</span></span> <span data-ttu-id="ccf93-110">Después de eso, Azure Active Directory almacena la información de inicio de sesión y la proporciona automáticamente a la aplicación cuando los usuarios acceden a ella de forma remota.</span><span class="sxs-lookup"><span data-stu-id="ccf93-110">After that, Azure Active Directory stores the sign-in information and automatically provides it to the application when your users access it remotely.</span></span> 

<span data-ttu-id="ccf93-111">Debe haber publicado y probado ya la aplicación con el proxy de aplicación.</span><span class="sxs-lookup"><span data-stu-id="ccf93-111">You should already have published and tested your app with Application Proxy.</span></span> <span data-ttu-id="ccf93-112">Si no es así, siga los pasos de [Publish applications using Azure AD Application Proxy](application-proxy-publish-azure-portal.md) (Publicación de aplicaciones mediante el proxy de aplicación de Azure AD) y luego vuelva a este punto.</span><span class="sxs-lookup"><span data-stu-id="ccf93-112">If not, follow the steps in [Publish applications using Azure AD Application Proxy](application-proxy-publish-azure-portal.md) then come back here.</span></span> 

## <a name="set-up-password-vaulting-for-your-application"></a><span data-ttu-id="ccf93-113">Configuración del almacenamiento de contraseñas para la aplicación</span><span class="sxs-lookup"><span data-stu-id="ccf93-113">Set up password vaulting for your application</span></span>

1. <span data-ttu-id="ccf93-114">Inicie sesión en [Azure Portal](https://portal.azure.com) como administrador.</span><span class="sxs-lookup"><span data-stu-id="ccf93-114">Sign in to the [Azure portal](https://portal.azure.com) as an administrator.</span></span>
2. <span data-ttu-id="ccf93-115">Seleccione **Azure Active Directory** > **Aplicaciones empresariales** > **Todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="ccf93-115">Select **Azure Active Directory** > **Enterprise applications** > **All applications**.</span></span>
3. <span data-ttu-id="ccf93-116">En la lista, seleccione la aplicación para la que desea configurar el SSO.</span><span class="sxs-lookup"><span data-stu-id="ccf93-116">From the list, select the app that you want to set up with SSO.</span></span>  
4. <span data-ttu-id="ccf93-117">Seleccione **Inicio de sesión único**.</span><span class="sxs-lookup"><span data-stu-id="ccf93-117">Select **Single sign-on**.</span></span>

   ![Seleccionar inicio de sesión único](./media/application-proxy-sso-azure-portal/select-sso.png)

5. <span data-ttu-id="ccf93-119">Para el modo SSO, elija **Inicio de sesión basado en contraseña**.</span><span class="sxs-lookup"><span data-stu-id="ccf93-119">For the SSO mode, choose **Password-based Sign-on**.</span></span>
6. <span data-ttu-id="ccf93-120">Para la URL de inicio de sesión, escriba la dirección URL de la página donde los usuarios escriben su nombre de usuario y contraseña para iniciar sesión fuera de la red corporativa.</span><span class="sxs-lookup"><span data-stu-id="ccf93-120">For the Sign-on URL, enter the URL for the page where users enter their username and password to sign in to your app outside of the corporate network.</span></span> <span data-ttu-id="ccf93-121">Debe ser la dirección URL externa que creó al publicar la aplicación a través del proxy de aplicación.</span><span class="sxs-lookup"><span data-stu-id="ccf93-121">This may be the External URL that you created when you published the app through Application Proxy.</span></span> 

   ![Elegir inicio de sesión basado en contraseña y escribir la URL](./media/application-proxy-sso-azure-portal/password-sso.png)

7. <span data-ttu-id="ccf93-123">Seleccione **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="ccf93-123">Select **Save**.</span></span>

<!-- Need to repro?
7. The page should tell you that a sign-in form was successfully detected at the provided URL. If it doesn't, select **Configure [your app name] Password Single Sign-on Settings** and choose **Manually detect sign-in fields**. Follow the instructions to point out where the sign-in credentials go. 
-->

## <a name="test-your-app"></a><span data-ttu-id="ccf93-124">Prueba de la aplicación</span><span class="sxs-lookup"><span data-stu-id="ccf93-124">Test your app</span></span>

<span data-ttu-id="ccf93-125">Vaya a la dirección URL externa configurada para obtener acceso remoto a la aplicación.</span><span class="sxs-lookup"><span data-stu-id="ccf93-125">Go to external URL that you configured for remote access to your application.</span></span> <span data-ttu-id="ccf93-126">Inicie sesión con sus credenciales para esa aplicación (o las credenciales para la cuenta de prueba que configuró con acceso).</span><span class="sxs-lookup"><span data-stu-id="ccf93-126">Sign in with your credentials for that app (or the credentials for a test account that you set up with access).</span></span> <span data-ttu-id="ccf93-127">Una vez que inicie sesión correctamente, debería poder salir de la aplicación y volver sin necesidad de volver a especificar sus credenciales.</span><span class="sxs-lookup"><span data-stu-id="ccf93-127">Once you sign in successfully, you should be able to leave the app and come back without entering your credentials again.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="ccf93-128">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="ccf93-128">Next steps</span></span>

- <span data-ttu-id="ccf93-129">Obtenga información sobre otras maneras de implementar el [inicio de sesión único con el proxy de aplicación](application-proxy-sso-overview.md)</span><span class="sxs-lookup"><span data-stu-id="ccf93-129">Read about other ways to implement [Single sign-on with Application Proxy](application-proxy-sso-overview.md)</span></span>
- <span data-ttu-id="ccf93-130">Más información sobre [Consideraciones de seguridad al obtener acceso a aplicaciones de forma remota con el Proxy de aplicación de Azure AD](application-proxy-security-considerations.md)</span><span class="sxs-lookup"><span data-stu-id="ccf93-130">Learn about [Security considerations for accessing apps remotely with Azure AD Application Proxy](application-proxy-security-considerations.md)</span></span>