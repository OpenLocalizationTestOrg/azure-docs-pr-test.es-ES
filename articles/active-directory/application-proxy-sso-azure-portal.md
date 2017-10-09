---
title: "aaaSingle inicio de sesión tooapps con el Proxy de aplicación de Azure AD | Documentos de Microsoft"
description: "Activar inicio de sesión único para las aplicaciones locales publicadas con Proxy de aplicación de Azure AD en hello portal de Azure."
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
ms.openlocfilehash: 5ff288d36163b74215677d9e34c93c985ac33d54
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="password-vaulting-for-single-sign-on-with-application-proxy"></a><span data-ttu-id="1ee0a-103">Almacén de contraseñas para el inicio de sesión único con el proxy de aplicación</span><span class="sxs-lookup"><span data-stu-id="1ee0a-103">Password vaulting for single sign-on with Application Proxy</span></span>

<span data-ttu-id="1ee0a-104">El proxy de aplicación de Azure Active Directory le ayuda a mejorar la productividad mediante la publicación de aplicaciones locales de manera que los empleados remotos puedan tener acceso seguro a estas.</span><span class="sxs-lookup"><span data-stu-id="1ee0a-104">Azure Active Directory Application Proxy helps you improve productivity by publishing on-premises applications so that remote employees can securely access them, too.</span></span> <span data-ttu-id="1ee0a-105">Hola portal de Azure, también puede configurar single sign-on (SSO) toothese aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="1ee0a-105">In hello Azure portal, you can also set up single sign-on (SSO) toothese apps.</span></span> <span data-ttu-id="1ee0a-106">Los usuarios solo necesitan tooauthenticate con Azure AD y puede acceder a la aplicación empresarial sin necesidad de toosign nuevo.</span><span class="sxs-lookup"><span data-stu-id="1ee0a-106">Your users only need tooauthenticate with Azure AD, and they can access your enterprise application without having toosign in again.</span></span>

<span data-ttu-id="1ee0a-107">El proxy de aplicación admite varios [modos de inicio de sesión único](application-proxy-sso-overview.md).</span><span class="sxs-lookup"><span data-stu-id="1ee0a-107">Application Proxy supports several [single sign-on modes](application-proxy-sso-overview.md).</span></span> <span data-ttu-id="1ee0a-108">El inicio de sesión basado en contraseña se ha creado para aplicaciones que usan una combinación de nombre de usuario/contraseña para la autenticación.</span><span class="sxs-lookup"><span data-stu-id="1ee0a-108">Password-based sign-on is intended for applications that use a username/password combination for authentication.</span></span> <span data-ttu-id="1ee0a-109">Al configurar sesión basado en contraseña para la aplicación, los usuarios tendrán toosign en la aplicación una vez de toohello local.</span><span class="sxs-lookup"><span data-stu-id="1ee0a-109">When you configure password-based sign-on for your application, your users have toosign in toohello on-premises application once.</span></span> <span data-ttu-id="1ee0a-110">Después de eso, Azure Active Directory almacena la información de inicio de sesión de Hola y proporciona automáticamente lo toohello aplicación cuando los usuarios tener acceso remoto.</span><span class="sxs-lookup"><span data-stu-id="1ee0a-110">After that, Azure Active Directory stores hello sign-in information and automatically provides it toohello application when your users access it remotely.</span></span> 

<span data-ttu-id="1ee0a-111">Debe haber publicado y probado ya la aplicación con el proxy de aplicación.</span><span class="sxs-lookup"><span data-stu-id="1ee0a-111">You should already have published and tested your app with Application Proxy.</span></span> <span data-ttu-id="1ee0a-112">Si no es así, siga los pasos de hello en [publicar aplicaciones mediante el Proxy de aplicación de Azure AD](application-proxy-publish-azure-portal.md) , a continuación, vuelve aquí proceden.</span><span class="sxs-lookup"><span data-stu-id="1ee0a-112">If not, follow hello steps in [Publish applications using Azure AD Application Proxy](application-proxy-publish-azure-portal.md) then come back here.</span></span> 

## <a name="set-up-password-vaulting-for-your-application"></a><span data-ttu-id="1ee0a-113">Configuración del almacenamiento de contraseñas para la aplicación</span><span class="sxs-lookup"><span data-stu-id="1ee0a-113">Set up password vaulting for your application</span></span>

1. <span data-ttu-id="1ee0a-114">Inicie sesión en toohello [portal de Azure](https://portal.azure.com) como administrador.</span><span class="sxs-lookup"><span data-stu-id="1ee0a-114">Sign in toohello [Azure portal](https://portal.azure.com) as an administrator.</span></span>
2. <span data-ttu-id="1ee0a-115">Seleccione **Azure Active Directory** > **Aplicaciones empresariales** > **Todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="1ee0a-115">Select **Azure Active Directory** > **Enterprise applications** > **All applications**.</span></span>
3. <span data-ttu-id="1ee0a-116">En lista de hello, seleccione la aplicación hello que desea tooset seguridad con SSO.</span><span class="sxs-lookup"><span data-stu-id="1ee0a-116">From hello list, select hello app that you want tooset up with SSO.</span></span>  
4. <span data-ttu-id="1ee0a-117">Seleccione **Inicio de sesión único**.</span><span class="sxs-lookup"><span data-stu-id="1ee0a-117">Select **Single sign-on**.</span></span>

   ![Seleccionar inicio de sesión único](./media/application-proxy-sso-azure-portal/select-sso.png)

5. <span data-ttu-id="1ee0a-119">Para el modo SSO de hello, elija **sesión basado en contraseña**.</span><span class="sxs-lookup"><span data-stu-id="1ee0a-119">For hello SSO mode, choose **Password-based Sign-on**.</span></span>
6. <span data-ttu-id="1ee0a-120">Hola inicio de sesión en la dirección URL, escriba la dirección URL de hello para la página de Hola donde los usuarios escribir su nombre de usuario y contraseña toosign en aplicación tooyour fuera de la red corporativa de Hola.</span><span class="sxs-lookup"><span data-stu-id="1ee0a-120">For hello Sign-on URL, enter hello URL for hello page where users enter their username and password toosign in tooyour app outside of hello corporate network.</span></span> <span data-ttu-id="1ee0a-121">Esto puede ser Hola dirección URL externa que creó cuando publicó la aplicación hello a través de Proxy de aplicación.</span><span class="sxs-lookup"><span data-stu-id="1ee0a-121">This may be hello External URL that you created when you published hello app through Application Proxy.</span></span> 

   ![Elegir inicio de sesión basado en contraseña y escribir la URL](./media/application-proxy-sso-azure-portal/password-sso.png)

7. <span data-ttu-id="1ee0a-123">Seleccione **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="1ee0a-123">Select **Save**.</span></span>

<!-- Need toorepro?
7. hello page should tell you that a sign-in form was successfully detected at hello provided URL. If it doesn't, select **Configure [your app name] Password Single Sign-on Settings** and choose **Manually detect sign-in fields**. Follow hello instructions toopoint out where hello sign-in credentials go. 
-->

## <a name="test-your-app"></a><span data-ttu-id="1ee0a-124">Prueba de la aplicación</span><span class="sxs-lookup"><span data-stu-id="1ee0a-124">Test your app</span></span>

<span data-ttu-id="1ee0a-125">Ir a dirección URL de tooexternal que ha configurado para la aplicación de tooyour de acceso remoto.</span><span class="sxs-lookup"><span data-stu-id="1ee0a-125">Go tooexternal URL that you configured for remote access tooyour application.</span></span> <span data-ttu-id="1ee0a-126">Inicie sesión con sus credenciales para esa aplicación (o las credenciales de Hola para una cuenta de prueba que configura con acceso).</span><span class="sxs-lookup"><span data-stu-id="1ee0a-126">Sign in with your credentials for that app (or hello credentials for a test account that you set up with access).</span></span> <span data-ttu-id="1ee0a-127">Cuando inicie sesión correctamente, debe ser capaz de tooleave Hola aplicación y vuelven a estar sin escribir sus credenciales de nuevo.</span><span class="sxs-lookup"><span data-stu-id="1ee0a-127">Once you sign in successfully, you should be able tooleave hello app and come back without entering your credentials again.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="1ee0a-128">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="1ee0a-128">Next steps</span></span>

- <span data-ttu-id="1ee0a-129">Obtenga información sobre otra maneras tooimplement [inicio de sesión único con el Proxy de aplicación](application-proxy-sso-overview.md)</span><span class="sxs-lookup"><span data-stu-id="1ee0a-129">Read about other ways tooimplement [Single sign-on with Application Proxy](application-proxy-sso-overview.md)</span></span>
- <span data-ttu-id="1ee0a-130">Más información sobre [Consideraciones de seguridad al obtener acceso a aplicaciones de forma remota con el Proxy de aplicación de Azure AD](application-proxy-security-considerations.md)</span><span class="sxs-lookup"><span data-stu-id="1ee0a-130">Learn about [Security considerations for accessing apps remotely with Azure AD Application Proxy](application-proxy-security-considerations.md)</span></span>