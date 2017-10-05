---
title: "Autorización de las cuentas de desarrollador mediante Azure Active Directory - Azure API Management | Microsoft Docs"
description: "Obtenga información sobre cómo autorizar a los usuarios para que usen Azure Active Directory en Administración de API."
services: api-management
documentationcenter: API Management
author: steved0x
manager: erikre
editor: 
ms.assetid: 33a69a83-94f2-4e4e-9cef-f2a5af3c9732
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: apimpm
ms.openlocfilehash: 7637e6419d17a2d75904fbe63df5f27d4be4bbe3
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-authorize-developer-accounts-using-azure-active-directory-in-azure-api-management"></a><span data-ttu-id="ec66e-103">Procedimiento para autorizar a las cuentas de desarrollador para que usen Azure Active Directory en Administración de API de Azure</span><span class="sxs-lookup"><span data-stu-id="ec66e-103">How to authorize developer accounts using Azure Active Directory in Azure API Management</span></span>
## <a name="overview"></a><span data-ttu-id="ec66e-104">Información general</span><span class="sxs-lookup"><span data-stu-id="ec66e-104">Overview</span></span>
<span data-ttu-id="ec66e-105">En esta guía se muestra cómo habilitar el acceso al portal para desarrolladores para todos los usuarios desde Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="ec66e-105">This guide shows you how to enable access to the developer portal for users from Azure Active Directory.</span></span> <span data-ttu-id="ec66e-106">También se muestra cómo administrar los grupos de usuarios de Azure Active Directory mediante la adición de grupos externos que contienen los usuarios de un directorio de Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="ec66e-106">This guide also shows you how to manage groups of Azure Active Directory users by adding external groups that contain the users of an Azure Active Directory.</span></span>

> <span data-ttu-id="ec66e-107">Para completar los pasos descritos en esta guía, debe tener un directorio de Azure Active Directory en el que crear una aplicación.</span><span class="sxs-lookup"><span data-stu-id="ec66e-107">To complete the steps in this guide you must first have an Azure Active Directory in which to create an application.</span></span>
> 
> 

## <a name="how-to-authorize-developer-accounts-using-azure-active-directory"></a><span data-ttu-id="ec66e-108">Procedimiento para autorizar a las cuentas de desarrollador para que usen Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="ec66e-108">How to authorize developer accounts using Azure Active Directory</span></span>
<span data-ttu-id="ec66e-109">Para comenzar, haga clic en **Portal para editores** en Azure Portal para el servicio API Management.</span><span class="sxs-lookup"><span data-stu-id="ec66e-109">To get started, click **Publisher portal** in the Azure portal for your API Management service.</span></span> <span data-ttu-id="ec66e-110">De este modo, se abre el portal del publicador de Administración de API.</span><span class="sxs-lookup"><span data-stu-id="ec66e-110">This takes you to the API Management publisher portal.</span></span>

![Portal del publicador][api-management-management-console]

> <span data-ttu-id="ec66e-112">Si aún no ha creado ninguna instancia del servicio de API Management, consulte [Creación de una instancia del servicio API Management][Create an API Management service instance] en el tutorial [Introducción a Azure API Management][Get started with Azure API Management].</span><span class="sxs-lookup"><span data-stu-id="ec66e-112">If you have not yet created an API Management service instance, see [Create an API Management service instance][Create an API Management service instance] in the [Get started with Azure API Management][Get started with Azure API Management] tutorial.</span></span>
> 
> 

<span data-ttu-id="ec66e-113">Haga clic en **Seguridad** en el menú **API Management** de la izquierda y, después, en **Identidades externas**.</span><span class="sxs-lookup"><span data-stu-id="ec66e-113">Click **Security** from the **API Management** menu on the left and click **External Identities**.</span></span>

![Identidades externas][api-management-security-external-identities]

<span data-ttu-id="ec66e-115">Haga clic en **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="ec66e-115">Click **Azure Active Directory**.</span></span> <span data-ttu-id="ec66e-116">Anote la **URL de redireccionamiento** y cambie a Azure Active Directory en el Portal de Azure clásico.</span><span class="sxs-lookup"><span data-stu-id="ec66e-116">Make a note of the **Redirect URL** and switch over to your Azure Active Directory in the Azure Classic Portal.</span></span>

![Identidades externas][api-management-security-aad-new]

<span data-ttu-id="ec66e-118">Haga clic en el botón **Agregar** para crear una nueva aplicación de Azure Active Directory y, a continuación, elija **Agregar una aplicación que mi organización está desarrollando**.</span><span class="sxs-lookup"><span data-stu-id="ec66e-118">Click the **Add** button to create a new Azure Active Directory application, and choose **Add an application my organization is developing**.</span></span>

![Agregar nueva aplicación de Azure Active Directory][api-management-new-aad-application-menu]

<span data-ttu-id="ec66e-120">Escriba un nombre para la aplicación, seleccione **Aplicación web y/o API web**y haga clic en el botón para ir al paso siguiente.</span><span class="sxs-lookup"><span data-stu-id="ec66e-120">Enter a name for the application, select **Web application and/or Web API**, and click the next button.</span></span>

![Nueva aplicación de Azure Active Directory][api-management-new-aad-application-1]

<span data-ttu-id="ec66e-122">Para **URL de inicio de sesión**, escriba la dirección URL de inicio de sesión en el portal para desarrolladores.</span><span class="sxs-lookup"><span data-stu-id="ec66e-122">For **Sign-on URL**, enter the sign-on URL of your developer portal.</span></span> <span data-ttu-id="ec66e-123">En este ejemplo, la **URL de inicio de sesión** es `https://aad03.portal.current.int-azure-api.net/signin`.</span><span class="sxs-lookup"><span data-stu-id="ec66e-123">In this example, the **Sign-on URL** is `https://aad03.portal.current.int-azure-api.net/signin`.</span></span> 

<span data-ttu-id="ec66e-124">Para la **URL de id. de aplicación**, especifique el dominio predeterminado o un dominio personalizado para Azure Active Directory y anexe a este una cadena única.</span><span class="sxs-lookup"><span data-stu-id="ec66e-124">For the **App ID URL**, enter either the default domain or a custom domain for the Azure Active Directory, and append a unique string to it.</span></span> <span data-ttu-id="ec66e-125">En este ejemplo, el dominio predeterminado de **https://contoso5api.onmicrosoft.com** se usa con el sufijo **/api** especificado.</span><span class="sxs-lookup"><span data-stu-id="ec66e-125">In this example, the default domain of **https://contoso5api.onmicrosoft.com** is used with the suffix of **/api** specified.</span></span>

![Propiedades de la nueva aplicación de Azure Active Directory][api-management-new-aad-application-2]

<span data-ttu-id="ec66e-127">Haga clic en el botón de verificación para guardar y crear la nueva aplicación y cambie a la pestaña **Configurar** para configurar la aplicación.</span><span class="sxs-lookup"><span data-stu-id="ec66e-127">Click the check button to save and create the application, and switch to the **Configure** tab to configure the new application.</span></span>

![Nueva aplicación de Azure Active Directory creada][api-management-new-aad-app-created]

<span data-ttu-id="ec66e-129">Si se van a usar varios directorios de Azure Active Directory para la aplicación, haga clic en **Sí** para **La aplicación es multiempresa**.</span><span class="sxs-lookup"><span data-stu-id="ec66e-129">If multiple Azure Active Directories are going to be used for this application, click **Yes** for **Application is multi-tenant**.</span></span> <span data-ttu-id="ec66e-130">El valor predeterminado es **No**.</span><span class="sxs-lookup"><span data-stu-id="ec66e-130">The default is **No**.</span></span>

![La aplicación es multiempresa][api-management-aad-app-multi-tenant]

<span data-ttu-id="ec66e-132">Copie la **URL de redireccionamiento** de la sección **Azure Active Directory** de la pestaña **Identidades externas** del portal del publicador y péguela en el cuadro de texto **URL de respuesta**.</span><span class="sxs-lookup"><span data-stu-id="ec66e-132">Copy the **Redirect URL** from the **Azure Active Directory** section of the **External Identities** tab in the publisher portal and paste it into the **Reply URL** text box.</span></span> 

![URL de respuesta][api-management-aad-reply-url]

<span data-ttu-id="ec66e-134">Desplácese a la parte inferior de la pestaña Configurar, seleccione la lista desplegable **Permisos de la aplicación** y active **Leer datos de directorio**.</span><span class="sxs-lookup"><span data-stu-id="ec66e-134">Scroll to the bottom of the configure tab, select the **Application Permissions** drop-down, and check **Read directory data**.</span></span>

![Permisos de la aplicación][api-management-aad-app-permissions]

<span data-ttu-id="ec66e-136">Seleccione la lista desplegable **Permisos delegados** y active **Habilitar inicio de sesión y leer perfiles de usuarios**.</span><span class="sxs-lookup"><span data-stu-id="ec66e-136">Select the **Delegate Permissions** drop-down, and check **Enable sign-on and read users' profiles**.</span></span>

![Permisos delegados][api-management-aad-delegated-permissions]

> <span data-ttu-id="ec66e-138">Para obtener más información sobre la aplicación y los permisos delegados, consulte [Acceso a la API Graph][Accessing the Graph API].</span><span class="sxs-lookup"><span data-stu-id="ec66e-138">For more information about application and delegated permissions, see [Accessing the Graph API][Accessing the Graph API].</span></span>
> 
> 

<span data-ttu-id="ec66e-139">Copie el **Id. de cliente** en el Portapapeles.</span><span class="sxs-lookup"><span data-stu-id="ec66e-139">Copy the **Client Id** to the clipboard.</span></span>

![Id. de cliente][api-management-aad-app-client-id]

<span data-ttu-id="ec66e-141">Vuelva al portal del publicador y pegue el **Id. de cliente** que ha copiado de la configuración de la aplicación de Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="ec66e-141">Switch back to the publisher portal and paste in the **Client Id** copied from the Azure Active Directory application configuration.</span></span>

![Id. de cliente][api-management-client-id]

<span data-ttu-id="ec66e-143">Vuelva a la configuración de Azure Active Directory, haga clic en la lista desplegable **Seleccionar duración** de la sección **Claves** y especifique un intervalo.</span><span class="sxs-lookup"><span data-stu-id="ec66e-143">Switch back to the Azure Active Directory configuration, and click the **Select duration** drop-down in the **Keys** section and specify an interval.</span></span> <span data-ttu-id="ec66e-144">En este ejemplo se usa el **año 1**.</span><span class="sxs-lookup"><span data-stu-id="ec66e-144">In this example, **1 year** is used.</span></span>

![Clave][api-management-aad-key-before-save]

<span data-ttu-id="ec66e-146">Haga clic en **Guardar** para guardar la configuración y mostrar la clave.</span><span class="sxs-lookup"><span data-stu-id="ec66e-146">Click **Save** to save the configuration and display the key.</span></span> <span data-ttu-id="ec66e-147">Copie la clave en el Portapapeles.</span><span class="sxs-lookup"><span data-stu-id="ec66e-147">Copy the key to the clipboard.</span></span>

> <span data-ttu-id="ec66e-148">Anote esta clave.</span><span class="sxs-lookup"><span data-stu-id="ec66e-148">Make a note of this key.</span></span> <span data-ttu-id="ec66e-149">Una vez que se cierre la ventana de configuración de Azure Active Directory, la clave no se puede mostrar de nuevo.</span><span class="sxs-lookup"><span data-stu-id="ec66e-149">Once you close the Azure Active Directory configuration window, the key cannot be displayed again.</span></span>
> 
> 

![Clave][api-management-aad-key-after-save]

<span data-ttu-id="ec66e-151">Vuelva al portal del publicador y pegue la clave en el cuadro de texto **Secreto del cliente** .</span><span class="sxs-lookup"><span data-stu-id="ec66e-151">Switch back to the publisher portal and paste the key into the **Client Secret** text box.</span></span>

![Secreto del cliente][api-management-client-secret]

<span data-ttu-id="ec66e-153">**Inquilinos permitidos** especifica los directorios que tienen acceso a las API de la instancia del servicio Administración de API.</span><span class="sxs-lookup"><span data-stu-id="ec66e-153">**Allowed Tenants** specifies which directories have access to the APIs of the API Management service instance.</span></span> <span data-ttu-id="ec66e-154">Especifique los dominios de las instancias de Azure Active Directory a los que desea conceder acceso.</span><span class="sxs-lookup"><span data-stu-id="ec66e-154">Specify the domains of the Azure Active Directory instances to which you want to grant access.</span></span> <span data-ttu-id="ec66e-155">Puede separar varios dominios mediante nuevas líneas, espacios o comas.</span><span class="sxs-lookup"><span data-stu-id="ec66e-155">You can separate multiple domains with newlines, spaces, or commas.</span></span>

![Inquilinos permitidos][api-management-client-allowed-tenants]


<span data-ttu-id="ec66e-157">Una vez especificada la configuración deseada, haga clic en **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="ec66e-157">Once the desired configuration is specified, click **Save**.</span></span>

![Guardar][api-management-client-allowed-tenants-save]

<span data-ttu-id="ec66e-159">Después de guardar los cambios, los usuarios de la instancia de Azure Active Directory especificada pueden iniciar sesión en el portal para desarrolladores mediante los pasos descritos en [Inicio de sesión en el portal para desarrolladores con una cuenta de Azure Active Directory][Log in to the Developer portal using an Azure Active Directory account].</span><span class="sxs-lookup"><span data-stu-id="ec66e-159">Once the changes are saved, the users in the specified Azure Active Directory can sign in to the Developer portal by following the steps in [Log in to the Developer portal using an Azure Active Directory account][Log in to the Developer portal using an Azure Active Directory account].</span></span>

<span data-ttu-id="ec66e-160">En la sección **Inquilinos permitidos** pueden especificarse varios dominios.</span><span class="sxs-lookup"><span data-stu-id="ec66e-160">Multiple domains can be specified in the **Allowed Tenants** section.</span></span> <span data-ttu-id="ec66e-161">Para que un usuario pueda iniciar sesión desde otro dominio distinto al dominio original donde se registró la aplicación, un administrador global de ese otro dominio deberá conceder antes a la aplicación permiso de acceso a los datos del directorio.</span><span class="sxs-lookup"><span data-stu-id="ec66e-161">Before any user can log in from a different domain than the original domain where the application was registered, a global administrator of the different domain must grant permission for the application to access directory data.</span></span> <span data-ttu-id="ec66e-162">Para conceder permiso, el administrador global debe ir a `https://<URL of your developer portal>/aadadminconsent` (por ejemplo, https://contoso.portal.azure-api.net/aadadminconsent), escribir el nombre de dominio del inquilino de Active Directory al que desea conceder acceso y hacer clic en Enviar.</span><span class="sxs-lookup"><span data-stu-id="ec66e-162">To grant permission, the global administrator should go to `https://<URL of your developer portal>/aadadminconsent` (for example, https://contoso.portal.azure-api.net/aadadminconsent), type in the domain name of the Active Directory tenant they want to give access to and click Submit.</span></span> <span data-ttu-id="ec66e-163">En el ejemplo siguiente, un administrador global de `miaoaad.onmicrosoft.com` está intentando conceder permiso a este portal para desarrolladores en particular.</span><span class="sxs-lookup"><span data-stu-id="ec66e-163">In the following example, a global administrator from `miaoaad.onmicrosoft.com` is trying to give permission to this particular developer portal.</span></span> 

![Permisos][api-management-aad-consent]

<span data-ttu-id="ec66e-165">En la siguiente pantalla, se pedirá al administrador global que confirme que proporciona el permiso.</span><span class="sxs-lookup"><span data-stu-id="ec66e-165">In the next screen, the global administrator will be prompted to confirm giving the permission.</span></span> 

![Permisos][api-management-permissions-form]

> <span data-ttu-id="ec66e-167">Si un administrador no global intenta iniciar sesión antes de que un administrador global conceda los permisos correspondientes, el inicio de sesión no se puede realizar y aparece una pantalla de error.</span><span class="sxs-lookup"><span data-stu-id="ec66e-167">If a non-global administrator tries to log in before permissions are granted by a global administrator, the login attempt fails and an error screen is displayed.</span></span>
> 
> 

## <a name="how-to-add-an-external-azure-active-directory-group"></a><span data-ttu-id="ec66e-168">Adición de un grupo externo de Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="ec66e-168">How to add an external Azure Active Directory Group</span></span>
<span data-ttu-id="ec66e-169">Tras habilitar el acceso para usuarios en un directorio de Azure Active Directory, puede agregar grupos de Azure Active Directory a Administración de API para administrar más fácilmente la asociación de los desarrolladores del grupo a los productos deseados.</span><span class="sxs-lookup"><span data-stu-id="ec66e-169">After enabling access for users in an Azure Active Directory, you can add Azure Active Directory groups into API Management to more easily manage the association of the developers in the group with the desired products.</span></span>

> <span data-ttu-id="ec66e-170">Para configurar un grupo externo de Azure Active Directory, antes debe configurarse la instancia de Azure Active Directory en la pestaña de identidades mediante el procedimiento descrito en la sección anterior.</span><span class="sxs-lookup"><span data-stu-id="ec66e-170">To configure an external Azure Active Directory group, the Azure Active Directory must first be configured in the Identities tab by following the procedure in the previous section.</span></span> 
> 
> 

<span data-ttu-id="ec66e-171">Los grupos externos de Azure Active Directory se agregan desde la pestaña **Visibilidad** del producto para el que desea conceder acceso al grupo.</span><span class="sxs-lookup"><span data-stu-id="ec66e-171">External Azure Active Directory groups are added from the **Visibility** tab of the product for which you wish to grant access to the group.</span></span> <span data-ttu-id="ec66e-172">Haga clic en **Productos**y, a continuación, en el nombre del producto deseado.</span><span class="sxs-lookup"><span data-stu-id="ec66e-172">Click **Products**, and then click the name of the desired product.</span></span>

![Configure product][api-management-configure-product]

<span data-ttu-id="ec66e-174">Cambie a la pestaña **Visibilidad** y haga clic en **Agregar grupos de Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="ec66e-174">Switch to the **Visibility** tab, and click **Add Groups from Azure Active Directory**.</span></span>

![Agregar grupos][api-management-add-groups]

<span data-ttu-id="ec66e-176">Seleccione el **Inquilino de Azure Active Directory** en la lista desplegable y, a continuación, escriba el nombre del grupo que desee en el cuadro de texto **Grupos para agregar**.</span><span class="sxs-lookup"><span data-stu-id="ec66e-176">Select the **Azure Active Directory Tenant** from the drop-down list, and then type the name of the desired group in the **Groups** to be added text box.</span></span>

![Seleccionar grupo][api-management-select-group]

<span data-ttu-id="ec66e-178">El nombre del grupo aparecerá en la lista **Grupos** de Azure Active Directory, como se muestra en el ejemplo siguiente.</span><span class="sxs-lookup"><span data-stu-id="ec66e-178">This group name can be found in the **Groups** list for your Azure Active Directory, as shown in the following example.</span></span>

![Lista de grupos de Azure Active Directory][api-management-aad-groups-list]

<span data-ttu-id="ec66e-180">Haga clic en **Agregar** para validar el nombre del grupo y agregar el grupo.</span><span class="sxs-lookup"><span data-stu-id="ec66e-180">Click **Add** to validate the group name and add the group.</span></span> <span data-ttu-id="ec66e-181">En este ejemplo, se agrega el grupo externo **Contoso 5 Developers**.</span><span class="sxs-lookup"><span data-stu-id="ec66e-181">In this example, the **Contoso 5 Developers** external group is added.</span></span> 

![Group added][api-management-aad-group-added]

<span data-ttu-id="ec66e-183">Haga clic en **Guardar** para guardar la nueva selección de grupo.</span><span class="sxs-lookup"><span data-stu-id="ec66e-183">Click **Save** to save the new group selection.</span></span>

<span data-ttu-id="ec66e-184">Una vez configurado un grupo de Azure Active Directory de un producto, este aparecerá en la pestaña **Visibilidad** y podrá activarse para el resto de productos de la instancia del servicio API Management.</span><span class="sxs-lookup"><span data-stu-id="ec66e-184">Once an Azure Active Directory group has been configured from one product, it is available to be checked on the **Visibility** tab for the other products in the API Management service instance.</span></span>

<span data-ttu-id="ec66e-185">Para revisar y configurar las propiedades de los grupos externos una vez que se han agregado, haga clic en el nombre del grupo en la pestaña **Grupos**.</span><span class="sxs-lookup"><span data-stu-id="ec66e-185">To review and configure the properties for external groups once they have been added, click the name of the group from the **Groups** tab.</span></span>

![Administrar grupos][api-management-groups]

<span data-ttu-id="ec66e-187">Desde aquí puede editar el **Nombre** y la **Descripción** del grupo.</span><span class="sxs-lookup"><span data-stu-id="ec66e-187">From here you can edit the **Name** and the **Description** of the group.</span></span>

![Editar grupo][api-management-edit-group]

<span data-ttu-id="ec66e-189">Los usuarios de la instancia de Azure Active Directory configurada pueden iniciar sesión en el portal para desarrolladores y ver y suscribirse a los grupos para los que tienen visibilidad mediante las instrucciones de la sección siguiente.</span><span class="sxs-lookup"><span data-stu-id="ec66e-189">Users from the configured Azure Active Directory can sign in to the Developer portal and view and subscribe to any groups for which they have visibility by following the instructions in the following section.</span></span>

## <a name="how-to-log-in-to-the-developer-portal-using-an-azure-active-directory-account"></a><span data-ttu-id="ec66e-190">Inicio de sesión en el portal para desarrolladores con una cuenta de Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="ec66e-190">How to log in to the Developer portal using an Azure Active Directory account</span></span>
<span data-ttu-id="ec66e-191">Para iniciar sesión en el portal para desarrolladores con la cuenta de Azure Active Directory configurada en las secciones anteriores, abra una nueva ventana del explorador mediante la **URL de inicio de sesión** de la configuración de la aplicación de Active Directory y haga clic en **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="ec66e-191">To log into the Developer portal using an Azure Active Directory account configured in the previous sections, open a new browser window using the **Sign-on URL** from the Active Directory application configuration, and click **Azure Active Directory**.</span></span>

![Portal para desarrolladores][api-management-dev-portal-signin]

<span data-ttu-id="ec66e-193">Escriba las credenciales de uno de los usuarios del directorio de Azure Active Directory y haga clic en **Iniciar sesión**.</span><span class="sxs-lookup"><span data-stu-id="ec66e-193">Enter the credentials of one of the users in your Azure Active Directory, and click **Sign in**.</span></span>

![Iniciar sesión][api-management-aad-signin]

<span data-ttu-id="ec66e-195">En caso de requerirse más información, puede que se le solicite un formulario de registro.</span><span class="sxs-lookup"><span data-stu-id="ec66e-195">You may be prompted with a registration form if any additional information is required.</span></span> <span data-ttu-id="ec66e-196">Complete el formulario de registro y haga clic en **Suscribirse**.</span><span class="sxs-lookup"><span data-stu-id="ec66e-196">Complete the registration form and click **Sign up**.</span></span>

![Registro][api-management-complete-registration]

<span data-ttu-id="ec66e-198">Ahora el usuario ha iniciado sesión en el portal para desarrolladores para la instancia del servicio Administración de API.</span><span class="sxs-lookup"><span data-stu-id="ec66e-198">Your user is now logged into the developer portal for your API Management service instance.</span></span>

![Registro completado][api-management-registration-complete]

[api-management-management-console]: ./media/api-management-howto-aad/api-management-management-console.png
[api-management-security-external-identities]: ./media/api-management-howto-aad/api-management-security-external-identities.png
[api-management-security-aad-new]: ./media/api-management-howto-aad/api-management-security-aad-new.png
[api-management-new-aad-application-menu]: ./media/api-management-howto-aad/api-management-new-aad-application-menu.png
[api-management-new-aad-application-1]: ./media/api-management-howto-aad/api-management-new-aad-application-1.png
[api-management-new-aad-application-2]: ./media/api-management-howto-aad/api-management-new-aad-application-2.png
[api-management-new-aad-app-created]: ./media/api-management-howto-aad/api-management-new-aad-app-created.png
[api-management-aad-app-permissions]: ./media/api-management-howto-aad/api-management-aad-app-permissions.png
[api-management-aad-app-client-id]: ./media/api-management-howto-aad/api-management-aad-app-client-id.png
[api-management-client-id]: ./media/api-management-howto-aad/api-management-client-id.png
[api-management-aad-key-before-save]: ./media/api-management-howto-aad/api-management-aad-key-before-save.png
[api-management-aad-key-after-save]: ./media/api-management-howto-aad/api-management-aad-key-after-save.png
[api-management-client-secret]: ./media/api-management-howto-aad/api-management-client-secret.png
[api-management-client-allowed-tenants]: ./media/api-management-howto-aad/api-management-client-allowed-tenants.png
[api-management-client-allowed-tenants-save]: ./media/api-management-howto-aad/api-management-client-allowed-tenants-save.png
[api-management-aad-delegated-permissions]: ./media/api-management-howto-aad/api-management-aad-delegated-permissions.png
[api-management-dev-portal-signin]: ./media/api-management-howto-aad/api-management-dev-portal-signin.png
[api-management-aad-signin]: ./media/api-management-howto-aad/api-management-aad-signin.png
[api-management-complete-registration]: ./media/api-management-howto-aad/api-management-complete-registration.png
[api-management-registration-complete]: ./media/api-management-howto-aad/api-management-registration-complete.png
[api-management-aad-app-multi-tenant]: ./media/api-management-howto-aad/api-management-aad-app-multi-tenant.png
[api-management-aad-reply-url]: ./media/api-management-howto-aad/api-management-aad-reply-url.png
[api-management-aad-consent]: ./media/api-management-howto-aad/api-management-aad-consent.png
[api-management-permissions-form]: ./media/api-management-howto-aad/api-management-permissions-form.png
[api-management-configure-product]: ./media/api-management-howto-aad/api-management-configure-product.png
[api-management-add-groups]: ./media/api-management-howto-aad/api-management-add-groups.png
[api-management-select-group]: ./media/api-management-howto-aad/api-management-select-group.png
[api-management-aad-groups-list]: ./media/api-management-howto-aad/api-management-aad-groups-list.png
[api-management-aad-group-added]: ./media/api-management-howto-aad/api-management-aad-group-added.png
[api-management-groups]: ./media/api-management-howto-aad/api-management-groups.png
[api-management-edit-group]: ./media/api-management-howto-aad/api-management-edit-group.png

[How to add operations to an API]: api-management-howto-add-operations.md
[How to add and publish a product]: api-management-howto-add-products.md
[Monitoring and analytics]: api-management-monitoring.md
[Add APIs to a product]: api-management-howto-add-products.md#add-apis
[Publish a product]: api-management-howto-add-products.md#publish-product
[Get started with Azure API Management]: api-management-get-started.md
[API Management policy reference]: api-management-policy-reference.md
[Caching policies]: api-management-policy-reference.md#caching-policies
[Create an API Management service instance]: api-management-get-started.md#create-service-instance

[http://oauth.net/2/]: http://oauth.net/2/
[WebApp-GraphAPI-DotNet]: https://github.com/AzureADSamples/WebApp-GraphAPI-DotNet
[Accessing the Graph API]: http://msdn.microsoft.com/library/azure/dn132599.aspx#BKMK_Graph

[Prerequisites]: #prerequisites
[Configure an OAuth 2.0 authorization server in API Management]: #step1
[Configure an API to use OAuth 2.0 user authorization]: #step2
[Test the OAuth 2.0 user authorization in the Developer Portal]: #step3
[Next steps]: #next-steps

[Log in to the Developer portal using an Azure Active Directory account]: #Log-in-to-the-Developer-portal-using-an-Azure-Active-Directory-account

