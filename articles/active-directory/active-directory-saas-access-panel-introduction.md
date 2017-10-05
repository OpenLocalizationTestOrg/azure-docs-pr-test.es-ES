---
title: "¿Qué es el panel de acceso de Azure Active Directory? | Microsoft Docs"
description: "Aprenda a usar las variaciones del panel de acceso (explorador web, aplicación Android, y aplicación iPhone y iPad) para tener acceso a las aplicaciones SaaS."
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
ms.assetid: c0252d01-7e6e-4f79-a70e-600479577dfd
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/31/2017
ms.author: markvi
ms.reviewer: asteen
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: bd9066c251188c0f18fe1a9403baa2beaeeb987c
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/03/2017
---
# <a name="what-is-the-access-panel"></a><span data-ttu-id="d7e28-104">¿Qué es el panel de acceso?</span><span class="sxs-lookup"><span data-stu-id="d7e28-104">What is the access panel?</span></span>

<span data-ttu-id="d7e28-105">El panel de acceso es un portal web.</span><span class="sxs-lookup"><span data-stu-id="d7e28-105">The access panel is a web-based portal.</span></span> <span data-ttu-id="d7e28-106">Permite que un usuario con una cuenta profesional o educativa en Azure Active Directory (Azure AD) vea e inicie aplicaciones basadas en la nube a las que el administrador de Azure AD le concedió acceso.</span><span class="sxs-lookup"><span data-stu-id="d7e28-106">It enables a user with a work or school account in Azure Active Directory to view and start cloud-based applications an Azure AD administrator has granted them access to.</span></span> <span data-ttu-id="d7e28-107">También se pueden usar las funcionalidades de administración de grupos de autoservicio y aplicaciones a través del panel de acceso.</span><span class="sxs-lookup"><span data-stu-id="d7e28-107">You can also use self-service group and app management capabilities through the access panel.</span></span>

<span data-ttu-id="d7e28-108">El panel de acceso es independiente de Azure Portal y no requiere que los usuarios tengan una suscripción de Azure.</span><span class="sxs-lookup"><span data-stu-id="d7e28-108">The access panel is separate from the Azure portal and does not you to have an Azure subscription.</span></span>

![Panel de acceso][1]

<span data-ttu-id="d7e28-110">El panel de acceso permite que los usuarios editen parte de la configuración de su perfil, por ejemplo, para lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="d7e28-110">The access panel enables you to edit some of your profile settings, including the ability to:</span></span>

- <span data-ttu-id="d7e28-111">Cambiar la contraseña asociada a una cuenta profesional o educativa.</span><span class="sxs-lookup"><span data-stu-id="d7e28-111">Change the password associated with a work or school account</span></span>

- <span data-ttu-id="d7e28-112">Editar configuración de restablecimiento de contraseña</span><span class="sxs-lookup"><span data-stu-id="d7e28-112">Edit password reset settings</span></span>

- <span data-ttu-id="d7e28-113">Editar la configuración de contacto y preferencias relacionada con la autenticación multifactor (en el caso de las cuentas para las que un administrador requirió su uso)</span><span class="sxs-lookup"><span data-stu-id="d7e28-113">Edit contact and preference settings related to multi-factor authentication (for accounts that have been required to use it by an administrator)</span></span>

- <span data-ttu-id="d7e28-114">Ver detalles de la cuenta, como el identificador de usuario, el correo electrónico alternativo, y los números de teléfono móvil y del trabajo.</span><span class="sxs-lookup"><span data-stu-id="d7e28-114">View account details, such as user ID, alternate email, and mobile and office phone numbers, and devices</span></span>

- <span data-ttu-id="d7e28-115">Ver e iniciar aplicaciones basadas en la nube a las que el administrador de Azure AD les concedió acceso.</span><span class="sxs-lookup"><span data-stu-id="d7e28-115">View and start cloud-based applications that the Azure AD administrator has granted them access to.</span></span> <span data-ttu-id="d7e28-116">Para obtener más información sobre el panel de acceso desde la perspectiva de los usuarios, consulte Utilización del panel de acceso.</span><span class="sxs-lookup"><span data-stu-id="d7e28-116">For more information about the access panel from the users’ perspective, see Using the access panel.</span></span> 

- <span data-ttu-id="d7e28-117">Autoadministrar grupos.</span><span class="sxs-lookup"><span data-stu-id="d7e28-117">Self-manage groups.</span></span> <span data-ttu-id="d7e28-118">Más concretamente, el administrador puede crear y administrar grupos de seguridad y solicitar pertenencias a grupos de seguridad en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="d7e28-118">More specifically, the administrator can create and manage security groups and request security group memberships in Azure AD.</span></span> <span data-ttu-id="d7e28-119">Para más información, consulte [Configuración de Azure Active Directory para la administración de grupos de autoservicio](active-directory-accessmanagement-self-service-group-management.md) y [Administración del acceso a los recursos con grupos de Azure Active Directory](active-directory-manage-groups.md).</span><span class="sxs-lookup"><span data-stu-id="d7e28-119">For more information, see [Self-service group management for users in Azure AD](active-directory-accessmanagement-self-service-group-management.md) and [Manage your groups](active-directory-manage-groups.md).</span></span>




## <a name="accessing-the-access-panel"></a><span data-ttu-id="d7e28-120">Acceso al panel de acceso</span><span class="sxs-lookup"><span data-stu-id="d7e28-120">Accessing the access panel</span></span>

<span data-ttu-id="d7e28-121">Los usuarios pueden acceder al panel de acceso visitando la siguiente dirección URL en un explorador web: `http://myapps.microsoft.com`.</span><span class="sxs-lookup"><span data-stu-id="d7e28-121">You can access the access panel by visiting the following URL in a web browser: `http://myapps.microsoft.com`</span></span>

<span data-ttu-id="d7e28-122">Con la configuración de marca personalizada en la página de inicio de sesión, se puede cargar esta personalización de marca de forma predeterminada anexando el dominio de su organización al final de la dirección URL: `http://myapps.microsoft.com/<your domain>.com`.</span><span class="sxs-lookup"><span data-stu-id="d7e28-122">If you have custom branding configured for your sign-in page, you can load this branding by appending your organization’s domain to the end of the URL: `http://myapps.microsoft.com/<your domain>.com`</span></span>

<span data-ttu-id="d7e28-123">En este caso, se puede utilizar cualquier nombre de dominio activo o comprobado que se haya configurado en Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="d7e28-123">In this case, you can use any active or verified domain name that has been configured in your Azure portal.</span></span>

![Nombre de dominio de Wingtip Toys][2]  

<span data-ttu-id="d7e28-125">La dirección URL se debe distribuir a todos los usuarios que iniciarán sesión en las aplicaciones integradas con Azure AD.</span><span class="sxs-lookup"><span data-stu-id="d7e28-125">You need to distribute the URL to all users who will sign in to applications that are integrated with Azure AD.</span></span>

## <a name="authentication"></a><span data-ttu-id="d7e28-126">Autenticación</span><span class="sxs-lookup"><span data-stu-id="d7e28-126">Authentication</span></span>

<span data-ttu-id="d7e28-127">Para llegar al panel de acceso, hay que autenticarse con una cuenta profesional o educativa en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="d7e28-127">To reach the access panel, you must be authenticated through a work or school account in Azure AD.</span></span> <span data-ttu-id="d7e28-128">Un usuario se puede autenticar en Azure AD directamente.</span><span class="sxs-lookup"><span data-stu-id="d7e28-128">You can be authenticated to Azure AD directly.</span></span> <span data-ttu-id="d7e28-129">Además, si una organización configuró la federación mediante Servicios de federación de Active Directory (AD FS) u otras tecnologías, Windows Server Active Directory puede autenticar a los usuarios.</span><span class="sxs-lookup"><span data-stu-id="d7e28-129">Alternatively, if an organization has configured federation by using Active Directory Federation Services (AD FS) or other technologies, you can be authenticated by Windows Server Active Directory.</span></span>

<span data-ttu-id="d7e28-130">Si un usuario tiene una suscripción para Azure u Office 365 y ha usado Azure Portal o una aplicación de Office 365, verá la lista de aplicaciones sin necesidad de volver a iniciar sesión.</span><span class="sxs-lookup"><span data-stu-id="d7e28-130">If you have a subscription for Azure or Office 365 and you have been using the Azure portal or an Office 365 application, you can see the list of applications without signing-in again.</span></span> <span data-ttu-id="d7e28-131">A los usuarios que no se han autenticado se les solicitará que inicien sesión utilizando el nombre de usuario y la contraseña de su cuenta en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="d7e28-131">If you are are not authenticated you are prompted to sign in by using the username and password for your account in Azure AD.</span></span> <span data-ttu-id="d7e28-132">Si la organización configuró la federación, bastará con escribir el nombre de usuario.</span><span class="sxs-lookup"><span data-stu-id="d7e28-132">If your organization has configured federation, typing the username is sufficient.</span></span>

<span data-ttu-id="d7e28-133">Después de la autenticación, los usuarios pueden interactuar con las aplicaciones que el administrador integró con el directorio.</span><span class="sxs-lookup"><span data-stu-id="d7e28-133">When you are authenticated, you can interact with the applications that your administrator has integrated with the directory.</span></span> <span data-ttu-id="d7e28-134">Para obtener información sobre cómo integrar las aplicaciones con Azure AD, vea [¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?](active-directory-appssoaccess-whatis.md)</span><span class="sxs-lookup"><span data-stu-id="d7e28-134">To learn how to integrate applications with Azure AD, see [What is application access and single sign-on with Azure Active Directory?](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="web-browser-requirements"></a><span data-ttu-id="d7e28-135">Requisitos del explorador web</span><span class="sxs-lookup"><span data-stu-id="d7e28-135">Web browser requirements</span></span>

<span data-ttu-id="d7e28-136">Como mínimo, el panel de acceso requiere un explorador que admita JavaScript y que tenga CSS habilitado.</span><span class="sxs-lookup"><span data-stu-id="d7e28-136">At a minimum, the access panel requires a browser that supports JavaScript and has CSS enabled.</span></span> <span data-ttu-id="d7e28-137">Para que el usuario inicie sesión en aplicaciones mediante el inicio de sesión único (SSO) basado en contraseña, debe instalarse la extensión del panel de acceso en el explorador.</span><span class="sxs-lookup"><span data-stu-id="d7e28-137">For the user to be signed in to applications through password-based single sign-on (SSO), the access panel extension must be installed in your browser.</span></span> <span data-ttu-id="d7e28-138">Esta extensión se descarga automáticamente cuando un usuario selecciona una aplicación que está configurada para SSO basado en contraseña.</span><span class="sxs-lookup"><span data-stu-id="d7e28-138">The extension is downloaded automatically when you select an application that is configured for password-based SSO.</span></span>

<span data-ttu-id="d7e28-139">En estos momentos, la extensión del panel de acceso está disponible para los exploradores Internet Explorer 8 y versiones posteriores, Edge, Chrome y Firefox.</span><span class="sxs-lookup"><span data-stu-id="d7e28-139">The access panel extension is currently available for Internet Explorer 8 and later, Edge, Chrome, and Firefox browsers.</span></span>

## <a name="mobile-app-support"></a><span data-ttu-id="d7e28-140">Compatibilidad para aplicación móvil</span><span class="sxs-lookup"><span data-stu-id="d7e28-140">Mobile app support</span></span>

<span data-ttu-id="d7e28-141">El equipo de Azure Active Directory publica la aplicación móvil Mis aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="d7e28-141">The Azure Active Directory team publishes the my apps mobile app.</span></span> <span data-ttu-id="d7e28-142">Cuando los usuarios instalan esta aplicación, pueden iniciar sesión en aplicaciones SSO basadas en contraseña en dispositivos iOS y Android.</span><span class="sxs-lookup"><span data-stu-id="d7e28-142">When you install the app, you can sign in to password-based SSO applications on iOS and Android devices.</span></span>

> [!NOTE]
> <span data-ttu-id="d7e28-143">Los usuarios pueden iniciar sesión en aplicaciones que admitan la federación con Azure AD (como Salesforce, Google Apps, Dropbox, Box, Concur, Workday, Office 365 y otras 70 más) prácticamente en cualquier explorador web, en cualquier dispositivo, sin necesidad de instalar complementos o una aplicación móvil.</span><span class="sxs-lookup"><span data-stu-id="d7e28-143">You can sign in to applications that support federation with Azure AD (including Salesforce, Google Apps, Dropbox, Box, Concur, Workday, Office 365, and more than 70 others) on virtually any web browser, on any device, without needing a plug-in or mobile app.</span></span> <span data-ttu-id="d7e28-144">Tampoco necesitará usar la aplicación móvil Mis aplicaciones en un dispositivo móvil para disfrutar del resto de la [experiencia del panel de acceso](https://myapps.microsoft.com/).</span><span class="sxs-lookup"><span data-stu-id="d7e28-144">All other [access panel experiences](https://myapps.microsoft.com/) do also not require the my apps mobile app to be used on a mobile device.</span></span>
>
>

### <a name="my-apps-for-android"></a><span data-ttu-id="d7e28-145">Mis aplicaciones para Android</span><span class="sxs-lookup"><span data-stu-id="d7e28-145">My apps for Android</span></span>

<span data-ttu-id="d7e28-146">Mis aplicaciones para Android es compatible con cualquier dispositivo Android que ejecute la versión 4.1 o posterior de Android.</span><span class="sxs-lookup"><span data-stu-id="d7e28-146">My apps for Android is supported on any Android device that is running Android version 4.1 and later.</span></span>  
<span data-ttu-id="d7e28-147">Está disponible actualmente en [Google Play Store](https://play.google.com/store/apps/details?id=com.microsoft.myapps).</span><span class="sxs-lookup"><span data-stu-id="d7e28-147">It is available in the [Google Play store](https://play.google.com/store/apps/details?id=com.microsoft.myapps).</span></span>

![Mis aplicaciones para Android][3]   

### <a name="my-apps-for-iphone-and-ipad"></a><span data-ttu-id="d7e28-149">Mis aplicaciones para iPhone y iPad</span><span class="sxs-lookup"><span data-stu-id="d7e28-149">My apps for iPhone and iPad</span></span>

<span data-ttu-id="d7e28-150">Mis aplicaciones para iOS es compatible con cualquier dispositivo iPhone o iPad que ejecute la versión 7 o posterior de iOS.</span><span class="sxs-lookup"><span data-stu-id="d7e28-150">My apps for iOS is supported on any iPhone or iPad that is running iOS version 7 and later.</span></span>  
<span data-ttu-id="d7e28-151">Está disponible actualmente en el [App Store de Apple](https://itunes.apple.com/us/app/my-apps-azure-active-directory/id824048653?mt=8).</span><span class="sxs-lookup"><span data-stu-id="d7e28-151">It is available in the [Apple App Store](https://itunes.apple.com/us/app/my-apps-azure-active-directory/id824048653?mt=8).</span></span>

![Mis aplicaciones para iOS][4]    



## <a name="managed-browser-for-my-apps"></a><span data-ttu-id="d7e28-153">Explorador administrado para Mis aplicaciones</span><span class="sxs-lookup"><span data-stu-id="d7e28-153">Managed browser for my apps</span></span>

<span data-ttu-id="d7e28-154">Mis aplicaciones también se integra en Intune Managed Browser.</span><span class="sxs-lookup"><span data-stu-id="d7e28-154">My apps is also integrated in the Intune Managed Browser.</span></span> <span data-ttu-id="d7e28-155">La solución Intune Managed Browser para dispositivos iOS y Android desempeña un rol clave a la hora de garantizar que los datos de los dispositivos móviles se mantengan seguros.</span><span class="sxs-lookup"><span data-stu-id="d7e28-155">The Intune Managed Browser for iOS and Android devices plays a key role in ensuring that data on mobile devices stays secure.</span></span> <span data-ttu-id="d7e28-156">Asimismo, permite ver y explorar páginas web que podrían contener información de la compañía, además de proporcionar una experiencia de exploración web segura.</span><span class="sxs-lookup"><span data-stu-id="d7e28-156">It lets you safely view and navigate web pages that might contain company information, and provides a secure web-browsing experience.</span></span>  
<span data-ttu-id="d7e28-157">Puede encontrar un acceso rápido a Mis aplicaciones en la página principal de Managed Browser y en los marcadores; de este modo, llegará más rápido a cualquier aplicación a la que quiera acceder.</span><span class="sxs-lookup"><span data-stu-id="d7e28-157">You find quick access to my apps on your Managed Browser homepage and in your bookmarks, giving you fewer clicks to reach any application you want to access.</span></span>

<span data-ttu-id="d7e28-158">Está disponible en el [App Store de Apple](https://itunes.apple.com/us/app/microsoft-intune-managed-browser/id943264951?mt=8) y en [Google Play Store](https://play.google.com/store/apps/details?id=com.microsoft.intune.mam.managedbrowser&hl=en).</span><span class="sxs-lookup"><span data-stu-id="d7e28-158">It is available in the [Apple App Store](https://itunes.apple.com/us/app/microsoft-intune-managed-browser/id943264951?mt=8) and [Google Play Store](https://play.google.com/store/apps/details?id=com.microsoft.intune.mam.managedbrowser&hl=en).</span></span>

![Explorador administrado para Mis aplicaciones][5]    





## <a name="tips-for-testing-the-user-experience"></a><span data-ttu-id="d7e28-160">Sugerencias para probar la experiencia del usuario</span><span class="sxs-lookup"><span data-stu-id="d7e28-160">Tips for testing the user experience</span></span>

<span data-ttu-id="d7e28-161">Los administradores de Azure que hayan iniciado sesión en Azure Portal con una cuenta en el directorio iniciarán la sesión automáticamente en el panel de acceso con la cuenta de administrador actual.</span><span class="sxs-lookup"><span data-stu-id="d7e28-161">If you are an Azure administrator and you are signed in to the Azure portal by using an account in the directory, you are automatically signed in to the access panel as your current account.</span></span> <span data-ttu-id="d7e28-162">En este caso, puede ver todas las aplicaciones que se han asignado a esta cuenta.</span><span class="sxs-lookup"><span data-stu-id="d7e28-162">In this case, you can see all applications that have been assigned to you.</span></span>

<span data-ttu-id="d7e28-163">**Para probar con *otra* cuenta de usuario, siga estos pasos:**</span><span class="sxs-lookup"><span data-stu-id="d7e28-163">**To test as a *different* user account:**</span></span>

1. <span data-ttu-id="d7e28-164">Haga clic en el menú de usuario de la esquina superior derecha de Azure Portal o del panel de acceso; luego, seleccione **Cerrar sesión**.</span><span class="sxs-lookup"><span data-stu-id="d7e28-164">Click the user menu in the upper-right corner of the Azure portal or the access panel, and then select **Sign Out**.</span></span> 
2. <span data-ttu-id="d7e28-165">Vaya al [panel de acceso](http://myapps.microsoft.com).</span><span class="sxs-lookup"><span data-stu-id="d7e28-165">Go to the [access panel](http://myapps.microsoft.com).</span></span>
3. <span data-ttu-id="d7e28-166">En la página de inicio de sesión, escriba el nombre de usuario y la contraseña de la cuenta del directorio que desea probar.</span><span class="sxs-lookup"><span data-stu-id="d7e28-166">On the sign-in page, type the username and password for the account in your directory you want to test.</span></span>


## <a name="starting-applications"></a><span data-ttu-id="d7e28-167">Inicio de aplicaciones</span><span class="sxs-lookup"><span data-stu-id="d7e28-167">Starting applications</span></span>

<span data-ttu-id="d7e28-168">Pueden aparecer varios tipos de aplicaciones en el panel de acceso.</span><span class="sxs-lookup"><span data-stu-id="d7e28-168">Several types of applications can appear on the access panel.</span></span>

### <a name="office-365-applications"></a><span data-ttu-id="d7e28-169">Aplicaciones de Office 365</span><span class="sxs-lookup"><span data-stu-id="d7e28-169">Office 365 applications</span></span>

<span data-ttu-id="d7e28-170">Si una organización usa aplicaciones de Office 365 y el usuario dispone de licencia para ellas, esas aplicaciones aparecen en el panel de acceso del usuario.</span><span class="sxs-lookup"><span data-stu-id="d7e28-170">If your organization is using Office 365 applications and you are licensed for them, the Office 365 applications appear on your access panel.</span></span>

<span data-ttu-id="d7e28-171">Cuando un usuario hace clic en un icono de una aplicación de Office 365, se redirige a esa aplicación e inicia sesión automáticamente.</span><span class="sxs-lookup"><span data-stu-id="d7e28-171">When you click an application tile for an Office 365 application, you are redirected to the application and automatically signed in.</span></span>

### <a name="microsoft-and-third-party-applications-configured-with-federation-based-sso"></a><span data-ttu-id="d7e28-172">Aplicaciones de Microsoft y de terceros configuradas con SSO basado en federación</span><span class="sxs-lookup"><span data-stu-id="d7e28-172">Microsoft and third-party applications configured with federation-based SSO</span></span>

<span data-ttu-id="d7e28-173">El administrador puede agregar aplicaciones en la sección Active Directory de Azure Portal con el modo de SSO establecido en **Inicio de sesión único de Azure AD**.</span><span class="sxs-lookup"><span data-stu-id="d7e28-173">Your administrator can add applications in the Active Directory section of the Azure portal with the SSO mode set to **Azure AD Single Sign-On**.</span></span> <span data-ttu-id="d7e28-174">Un usuario ve estas aplicaciones solo si el administrador concedió expresamente acceso a las aplicaciones a ese usuario.</span><span class="sxs-lookup"><span data-stu-id="d7e28-174">You can only see these applications if your administrator has explicitly granted you access to the applications.</span></span>

<span data-ttu-id="d7e28-175">Cuando un usuario hace clic en el icono de una de estas aplicaciones, se le redirige a esa aplicación e inicia sesión automáticamente.</span><span class="sxs-lookup"><span data-stu-id="d7e28-175">When you click a tile for one of these applications, you are redirected and automatically signed in to the application.</span></span>

### <a name="password-based-sso-without-identity-provisioning"></a><span data-ttu-id="d7e28-176">SSO basado en contraseña sin aprovisionamiento de identidad</span><span class="sxs-lookup"><span data-stu-id="d7e28-176">Password-based SSO without identity provisioning</span></span>

<span data-ttu-id="d7e28-177">El administrador puede agregar aplicaciones en la sección Active Directory de Azure Portal con el modo de SSO establecido en **Inicio de sesión único basado en contraseña**.</span><span class="sxs-lookup"><span data-stu-id="d7e28-177">Your administrator can add applications in the Active Directory section of the Azure portal with the SSO mode set to **Password-based Single Sign-On**.</span></span> <span data-ttu-id="d7e28-178">Todos los usuarios del directorio ven todas las aplicaciones que se han configurado en este modo.</span><span class="sxs-lookup"><span data-stu-id="d7e28-178">All users in the directory can see all applications that have been configured in this mode.</span></span>

<span data-ttu-id="d7e28-179">La primera vez que un usuario haga clic en el icono de una de estas aplicaciones, se le pedirá que instale el complemento SSO de contraseña para Internet Explorer o Chrome.</span><span class="sxs-lookup"><span data-stu-id="d7e28-179">The first time, you click a tile for one of these applications, you are prompted to install the Password SSO plug-in for Internet Explorer or Chrome.</span></span> <span data-ttu-id="d7e28-180">La instalación podría requerir que el usuario reinicie el explorador web.</span><span class="sxs-lookup"><span data-stu-id="d7e28-180">The installation might require you to restart your web browser.</span></span> <span data-ttu-id="d7e28-181">Cuando el usuario vuelve al panel de acceso y hace clic de nuevo en el icono de la aplicación, se le pide el nombre de usuario y la contraseña de dicha aplicación.</span><span class="sxs-lookup"><span data-stu-id="d7e28-181">When you return to the access panel and click the application tile again, you are prompted for a username and password for the application.</span></span> <span data-ttu-id="d7e28-182">Una vez que escribe el nombre de usuario y la contraseña, estas credenciales se almacenan de forma segura en Azure AD y se vinculan con su cuenta en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="d7e28-182">When you have entered your username and password, these credentials are securely stored and linked to your account in Azure AD.</span></span>

<span data-ttu-id="d7e28-183">La próxima vez que el usuario haga clic en el icono de la aplicación, iniciará sesión automáticamente en la aplicación.</span><span class="sxs-lookup"><span data-stu-id="d7e28-183">The next time you click the application tile, you are automatically signed in to the application.</span></span>  
<span data-ttu-id="d7e28-184">No tendrá que volver a escribir las credenciales ni instalar otra vez el complemento SSO de contraseña.</span><span class="sxs-lookup"><span data-stu-id="d7e28-184">You don't have to enter your credentials again and or install the Password SSO plug-in.</span></span>

<span data-ttu-id="d7e28-185">Si las credenciales de un usuario han cambiado en la aplicación de terceros de destino, el usuario también debe actualizar sus credenciales almacenadas en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="d7e28-185">If your credentials have changed in the target third-party application, you must also update your credentials that are stored in Azure AD.</span></span> 

<span data-ttu-id="d7e28-186">**Para actualizar las credenciales, siga estos pasos:**</span><span class="sxs-lookup"><span data-stu-id="d7e28-186">**To update credentials:**</span></span>

1. <span data-ttu-id="d7e28-187">Seleccione el icono en el icono de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="d7e28-187">Select the icon on the application tile.</span></span>
2. <span data-ttu-id="d7e28-188">Seleccione **Actualizar credenciales** para volver a escribir el nombre de usuario y la contraseña de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="d7e28-188">Select **update credentials** to reenter the username and password for the application.</span></span>


### <a name="password-based-sso-with-identity-provisioning"></a><span data-ttu-id="d7e28-189">SSO basado en contraseña con aprovisionamiento de identidad</span><span class="sxs-lookup"><span data-stu-id="d7e28-189">Password-based SSO with identity provisioning</span></span>

<span data-ttu-id="d7e28-190">El administrador puede agregar aplicaciones en la sección **Active Directory** de Azure Portal con el modo de SSO establecido en **Inicio de sesión único basado en contraseña**, además del aprovisionamiento de identidad.</span><span class="sxs-lookup"><span data-stu-id="d7e28-190">Your administrator can add applications in the **Active Directory** section of the Azure portal with the SSO mode set to **Password-based Single Sign-On**, along with identity provisioning.</span></span>

<span data-ttu-id="d7e28-191">La primera vez que un usuario haga clic en el icono de una de estas aplicaciones, se le pedirá que instale el **complemento SSO de contraseña para Internet Explorer o Chrome**.</span><span class="sxs-lookup"><span data-stu-id="d7e28-191">The first time, you click an application tile for one of these applications, you are prompted to install the **Password SSO plug-in for Internet Explorer or Chrome**.</span></span> <span data-ttu-id="d7e28-192">La instalación podría requerir que el usuario reinicie el explorador web.</span><span class="sxs-lookup"><span data-stu-id="d7e28-192">The installation might require you to restart your web browser.</span></span>  
<span data-ttu-id="d7e28-193">Cuando vuelva al panel de acceso y haga clic otra vez en el icono de la aplicación, iniciará sesión automáticamente en ella.</span><span class="sxs-lookup"><span data-stu-id="d7e28-193">When you return to the access panel and click the application tile again, you are automatically signed in to the application.</span></span>

<span data-ttu-id="d7e28-194">Algunas aplicaciones pueden requerir que el usuario cambie su contraseña en el primer inicio de sesión.</span><span class="sxs-lookup"><span data-stu-id="d7e28-194">Some applications might require you to change your password on the first sign-in.</span></span> <span data-ttu-id="d7e28-195">Si las credenciales de un usuario han cambiado en la aplicación de terceros de destino, este también debe actualizar sus credenciales almacenadas en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="d7e28-195">If your credentials have changed in the target third-party application, you must also update the credentials that are stored in Azure AD.</span></span> 

<span data-ttu-id="d7e28-196">**Para actualizar las credenciales, siga estos pasos:**</span><span class="sxs-lookup"><span data-stu-id="d7e28-196">**To update credentials:**</span></span>

1. <span data-ttu-id="d7e28-197">Seleccione el icono en el icono de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="d7e28-197">Select the icon on the application tile.</span></span>
2. <span data-ttu-id="d7e28-198">Seleccione **Actualizar credenciales** para volver a escribir el nombre de usuario y la contraseña de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="d7e28-198">Select **update credentials** to reenter the username and password for the application.</span></span>


### <a name="application-with-existing-sso-solutions"></a><span data-ttu-id="d7e28-199">Aplicación con soluciones SSO existentes</span><span class="sxs-lookup"><span data-stu-id="d7e28-199">Application with existing SSO solutions</span></span>

<span data-ttu-id="d7e28-200">Para configurar SSO en una aplicación, Azure Portal proporciona una tercera opción: **Inicio de sesión único existente**.</span><span class="sxs-lookup"><span data-stu-id="d7e28-200">To configure SSO for an application, the Azure portal provides a third option called **Existing Single Sign-On**.</span></span> <span data-ttu-id="d7e28-201">Esta opción permite que el administrador cree un vínculo a una aplicación y lo coloque en el panel de acceso de los usuarios seleccionados.</span><span class="sxs-lookup"><span data-stu-id="d7e28-201">This option enables your administrator to create a link to an application and place it on the access panel for selected users.</span></span>

<span data-ttu-id="d7e28-202">Por ejemplo, si hay una aplicación configurada para autenticar usuarios mediante AD FS 2.0, el administrador puede usar la opción **Inicio de sesión único existente** y crearle un vínculo en el panel de acceso.</span><span class="sxs-lookup"><span data-stu-id="d7e28-202">For example, if an application is configured to authenticate users by using AD FS 2.0, your administrator can use the **Existing Single Sign-On** option to create a link to it on the access panel.</span></span> <span data-ttu-id="d7e28-203">Cuando los usuarios tienen acceso al vínculo, se autentican mediante AD FS 2.0 o cualquier solución SSO existente que brinde la aplicación.</span><span class="sxs-lookup"><span data-stu-id="d7e28-203">When you access the link, you are authenticated through AD FS 2.0 or whatever existing SSO solution the application provides.</span></span>


## <a name="next-steps"></a><span data-ttu-id="d7e28-204">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="d7e28-204">Next steps</span></span>

- <span data-ttu-id="d7e28-205">Para ver una lista de todos los temas relacionados con la administración de aplicaciones, consulte [Índice de artículos sobre la administración de aplicaciones en Azure Active Directory](active-directory-apps-index.md).</span><span class="sxs-lookup"><span data-stu-id="d7e28-205">To see a list of all topics that are related to application management, see the [article index for application management in Azure Active Directory](active-directory-apps-index.md).</span></span>
 
- <span data-ttu-id="d7e28-206">Si quiere saber cómo integrar una aplicación SaaS en Azure AD, vea [Lista de tutoriales sobre cómo integrar aplicaciones SaaS](active-directory-saas-tutorial-list.md).</span><span class="sxs-lookup"><span data-stu-id="d7e28-206">To learn how to integrate a SaaS app into Azure AD, see the [list of tutorials on how to integrate SaaS apps](active-directory-saas-tutorial-list.md).</span></span>
 
- <span data-ttu-id="d7e28-207">En el caso de que necesite más detalles sobre cómo administrar aplicaciones con Azure AD, consulte [Introducción al inicio de sesión único y la administración del acceso a las aplicaciones con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="d7e28-207">To learn more about managing apps with Azure AD, see the [introduction to single sign-on and managing app access with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>
 
- <span data-ttu-id="d7e28-208">Para obtener más información sobre el aprovisionamiento de usuarios, vea [Aprovisionamiento y desaprovisionamiento automático de usuarios para aplicaciones SaaS](active-directory-saas-app-provisioning.md).</span><span class="sxs-lookup"><span data-stu-id="d7e28-208">To learn more about user provisioning, see [automate user provisioning and deprovisioning to SaaS applications](active-directory-saas-app-provisioning.md).</span></span>

<!--Image references-->
[1]: ./media/active-directory-saas-access-panel-introduction/01.png
[2]: ./media/active-directory-saas-access-panel-introduction/02.png
[3]: ./media/active-directory-saas-access-panel-introduction/03.png
[4]: ./media/active-directory-saas-access-panel-introduction/04.png
[5]: ./media/active-directory-saas-access-panel-introduction/05.png
