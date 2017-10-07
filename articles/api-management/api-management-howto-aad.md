---
title: "las cuentas de desarrollador aaaAuthorize con Azure Active Directory - administración de API de Azure | Documentos de Microsoft"
description: "Obtenga información acerca de cómo los usuarios de tooauthorize con Azure Active Directory en administración de API."
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
ms.openlocfilehash: ebf5447a509a47df35e4262138bfcf423cb1dd5c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooauthorize-developer-accounts-using-azure-active-directory-in-azure-api-management"></a><span data-ttu-id="aa606-103">Cómo tooauthorize developer cuentas con Azure Active Directory en la administración de API de Azure</span><span class="sxs-lookup"><span data-stu-id="aa606-103">How tooauthorize developer accounts using Azure Active Directory in Azure API Management</span></span>
## <a name="overview"></a><span data-ttu-id="aa606-104">Información general</span><span class="sxs-lookup"><span data-stu-id="aa606-104">Overview</span></span>
<span data-ttu-id="aa606-105">Esta guía le mostrará cómo tooenable tener acceso a portal para desarrolladores de toohello para los usuarios de Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="aa606-105">This guide shows you how tooenable access toohello developer portal for users from Azure Active Directory.</span></span> <span data-ttu-id="aa606-106">Esta guía muestra cómo Hola toomanage grupos de usuarios de Azure Active Directory mediante la adición de grupos externos que contienen a los usuarios de Active Directory de Azure.</span><span class="sxs-lookup"><span data-stu-id="aa606-106">This guide also shows you how toomanage groups of Azure Active Directory users by adding external groups that contain hello users of an Azure Active Directory.</span></span>

> <span data-ttu-id="aa606-107">Hola toocomplete los pasos de esta guía primero debe tener un Azure Active Directory en qué toocreate una aplicación.</span><span class="sxs-lookup"><span data-stu-id="aa606-107">toocomplete hello steps in this guide you must first have an Azure Active Directory in which toocreate an application.</span></span>
> 
> 

## <a name="how-tooauthorize-developer-accounts-using-azure-active-directory"></a><span data-ttu-id="aa606-108">Cómo tooauthorize developer cuentas con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="aa606-108">How tooauthorize developer accounts using Azure Active Directory</span></span>
<span data-ttu-id="aa606-109">tooget iniciado, haga clic en **portal para desarrolladores de** Hola portal de Azure para su servicio de administración de API.</span><span class="sxs-lookup"><span data-stu-id="aa606-109">tooget started, click **Publisher portal** in hello Azure portal for your API Management service.</span></span> <span data-ttu-id="aa606-110">Esto le llevará toohello portal para desarrolladores de administración de API.</span><span class="sxs-lookup"><span data-stu-id="aa606-110">This takes you toohello API Management publisher portal.</span></span>

![Portal del publicador][api-management-management-console]

> <span data-ttu-id="aa606-112">Si aún no ha creado una instancia de servicio de administración de API, consulte [crear una instancia de servicio de administración de API] [ Create an API Management service instance] en hello [Introducción a administración de API de Azure] [ Get started with Azure API Management] tutorial.</span><span class="sxs-lookup"><span data-stu-id="aa606-112">If you have not yet created an API Management service instance, see [Create an API Management service instance][Create an API Management service instance] in hello [Get started with Azure API Management][Get started with Azure API Management] tutorial.</span></span>
> 
> 

<span data-ttu-id="aa606-113">Haga clic en **seguridad** de hello **administración de API** menú Hola izquierda y haga clic en **identidades externas**.</span><span class="sxs-lookup"><span data-stu-id="aa606-113">Click **Security** from hello **API Management** menu on hello left and click **External Identities**.</span></span>

![Identidades externas][api-management-security-external-identities]

<span data-ttu-id="aa606-115">Haga clic en **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="aa606-115">Click **Azure Active Directory**.</span></span> <span data-ttu-id="aa606-116">Tome nota de hello **dirección URL de redireccionamiento** y cambiar tooyour Azure Active Directory en hello Portal clásico de Azure.</span><span class="sxs-lookup"><span data-stu-id="aa606-116">Make a note of hello **Redirect URL** and switch over tooyour Azure Active Directory in hello Azure Classic Portal.</span></span>

![Identidades externas][api-management-security-aad-new]

<span data-ttu-id="aa606-118">Haga clic en hello **agregar** toocreate una nueva aplicación de Azure Active Directory de botón y elija **agregar una aplicación que mi organización está desarrollando**.</span><span class="sxs-lookup"><span data-stu-id="aa606-118">Click hello **Add** button toocreate a new Azure Active Directory application, and choose **Add an application my organization is developing**.</span></span>

![Agregar nueva aplicación de Azure Active Directory][api-management-new-aad-application-menu]

<span data-ttu-id="aa606-120">Escriba un nombre para la aplicación hello, seleccione **Web de aplicación o Web API**y haga clic en el botón siguiente Hola.</span><span class="sxs-lookup"><span data-stu-id="aa606-120">Enter a name for hello application, select **Web application and/or Web API**, and click hello next button.</span></span>

![Nueva aplicación de Azure Active Directory][api-management-new-aad-application-1]

<span data-ttu-id="aa606-122">Para **dirección URL de inicio de sesión**, escriba Hola dirección URL de inicio de sesión de su portal para desarrolladores.</span><span class="sxs-lookup"><span data-stu-id="aa606-122">For **Sign-on URL**, enter hello sign-on URL of your developer portal.</span></span> <span data-ttu-id="aa606-123">En este ejemplo, Hola **dirección URL de inicio de sesión** es `https://aad03.portal.current.int-azure-api.net/signin`.</span><span class="sxs-lookup"><span data-stu-id="aa606-123">In this example, hello **Sign-on URL** is `https://aad03.portal.current.int-azure-api.net/signin`.</span></span> 

<span data-ttu-id="aa606-124">Para hello **URL de Id. de aplicación**, escriba el dominio predeterminado de Hola o un dominio personalizado para hello Azure Active Directory y anexar un tooit de cadena única.</span><span class="sxs-lookup"><span data-stu-id="aa606-124">For hello **App ID URL**, enter either hello default domain or a custom domain for hello Azure Active Directory, and append a unique string tooit.</span></span> <span data-ttu-id="aa606-125">En este ejemplo, Hola dominio predeterminado de **https://contoso5api.onmicrosoft.com** se usa con el sufijo de Hola de **/API** especificado.</span><span class="sxs-lookup"><span data-stu-id="aa606-125">In this example, hello default domain of **https://contoso5api.onmicrosoft.com** is used with hello suffix of **/api** specified.</span></span>

![Propiedades de la nueva aplicación de Azure Active Directory][api-management-new-aad-application-2]

<span data-ttu-id="aa606-127">Haga clic en toosave de botón de comprobación de Hola y crear la aplicación hello y cambiar toohello **configurar** ficha nueva aplicación de tooconfigure Hola.</span><span class="sxs-lookup"><span data-stu-id="aa606-127">Click hello check button toosave and create hello application, and switch toohello **Configure** tab tooconfigure hello new application.</span></span>

![Nueva aplicación de Azure Active Directory creada][api-management-new-aad-app-created]

<span data-ttu-id="aa606-129">Si varios directorios de Azure Active Directory va toobe usada para esta aplicación, haga clic en **Sí** para **aplicación es multiempresa**.</span><span class="sxs-lookup"><span data-stu-id="aa606-129">If multiple Azure Active Directories are going toobe used for this application, click **Yes** for **Application is multi-tenant**.</span></span> <span data-ttu-id="aa606-130">valor predeterminado de Hello es **No**.</span><span class="sxs-lookup"><span data-stu-id="aa606-130">hello default is **No**.</span></span>

![La aplicación es multiempresa][api-management-aad-app-multi-tenant]

<span data-ttu-id="aa606-132">Hola copia **dirección URL de redireccionamiento** de hello **Azure Active Directory** sección de hello **identidades externas** pestaña en el portal para desarrolladores de Hola y pegarlos en hello **Dirección URL de respuesta** cuadro de texto.</span><span class="sxs-lookup"><span data-stu-id="aa606-132">Copy hello **Redirect URL** from hello **Azure Active Directory** section of hello **External Identities** tab in hello publisher portal and paste it into hello **Reply URL** text box.</span></span> 

![URL de respuesta][api-management-aad-reply-url]

<span data-ttu-id="aa606-134">Desplazar hacia abajo de toohello de hello configurar ficha, seleccione hello **permisos de aplicación** lista desplegable y compruebe **leer datos de directorio**.</span><span class="sxs-lookup"><span data-stu-id="aa606-134">Scroll toohello bottom of hello configure tab, select hello **Application Permissions** drop-down, and check **Read directory data**.</span></span>

![Permisos de la aplicación][api-management-aad-app-permissions]

<span data-ttu-id="aa606-136">Seleccione hello **delegar permisos** lista desplegable y compruebe **habilitar el inicio de sesión y leer los perfiles de usuarios**.</span><span class="sxs-lookup"><span data-stu-id="aa606-136">Select hello **Delegate Permissions** drop-down, and check **Enable sign-on and read users' profiles**.</span></span>

![Permisos delegados][api-management-aad-delegated-permissions]

> <span data-ttu-id="aa606-138">Para obtener más información acerca de la aplicación y los permisos delegados, vea [Hola al tener acceso a API Graph][Accessing hello Graph API].</span><span class="sxs-lookup"><span data-stu-id="aa606-138">For more information about application and delegated permissions, see [Accessing hello Graph API][Accessing hello Graph API].</span></span>
> 
> 

<span data-ttu-id="aa606-139">Hola copia **Id. de cliente** toohello Portapapeles.</span><span class="sxs-lookup"><span data-stu-id="aa606-139">Copy hello **Client Id** toohello clipboard.</span></span>

![Id. de cliente][api-management-aad-app-client-id]

<span data-ttu-id="aa606-141">Cambie portal para desarrolladores de toohello atrás y pegue en hello **Id. de cliente** copiados de la configuración de la aplicación hello Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="aa606-141">Switch back toohello publisher portal and paste in hello **Client Id** copied from hello Azure Active Directory application configuration.</span></span>

![Id. de cliente][api-management-client-id]

<span data-ttu-id="aa606-143">Cambiar configuración de Azure Active Directory toohello atrás y haga clic en hello **seleccione duración** desplegable Hola **claves** sección y especificar un intervalo.</span><span class="sxs-lookup"><span data-stu-id="aa606-143">Switch back toohello Azure Active Directory configuration, and click hello **Select duration** drop-down in hello **Keys** section and specify an interval.</span></span> <span data-ttu-id="aa606-144">En este ejemplo se usa el **año 1**.</span><span class="sxs-lookup"><span data-stu-id="aa606-144">In this example, **1 year** is used.</span></span>

![Clave][api-management-aad-key-before-save]

<span data-ttu-id="aa606-146">Haga clic en **guardar** toosave Hola configuración y mostrar hello la clave.</span><span class="sxs-lookup"><span data-stu-id="aa606-146">Click **Save** toosave hello configuration and display hello key.</span></span> <span data-ttu-id="aa606-147">Copie el Portapapeles de hello toohello clave.</span><span class="sxs-lookup"><span data-stu-id="aa606-147">Copy hello key toohello clipboard.</span></span>

> <span data-ttu-id="aa606-148">Anote esta clave.</span><span class="sxs-lookup"><span data-stu-id="aa606-148">Make a note of this key.</span></span> <span data-ttu-id="aa606-149">Una vez que cierre la ventana de configuración de Azure Active Directory de hello, no se puede mostrar clave Hola de nuevo.</span><span class="sxs-lookup"><span data-stu-id="aa606-149">Once you close hello Azure Active Directory configuration window, hello key cannot be displayed again.</span></span>
> 
> 

![Clave][api-management-aad-key-after-save]

<span data-ttu-id="aa606-151">Conmutador toohello atrás portal y pegar Hola clave del publicador en hello **secreto de cliente** cuadro de texto.</span><span class="sxs-lookup"><span data-stu-id="aa606-151">Switch back toohello publisher portal and paste hello key into hello **Client Secret** text box.</span></span>

![Secreto del cliente][api-management-client-secret]

<span data-ttu-id="aa606-153">**Permite a los inquilinos** especifica los directorios que tienen acceso toohello API de instancia de servicio de administración de API de Hola.</span><span class="sxs-lookup"><span data-stu-id="aa606-153">**Allowed Tenants** specifies which directories have access toohello APIs of hello API Management service instance.</span></span> <span data-ttu-id="aa606-154">Especifique los dominios de Hola de hello toowhich de instancias de Azure Active Directory que desee toogrant acceso.</span><span class="sxs-lookup"><span data-stu-id="aa606-154">Specify hello domains of hello Azure Active Directory instances toowhich you want toogrant access.</span></span> <span data-ttu-id="aa606-155">Puede separar varios dominios mediante nuevas líneas, espacios o comas.</span><span class="sxs-lookup"><span data-stu-id="aa606-155">You can separate multiple domains with newlines, spaces, or commas.</span></span>

![Inquilinos permitidos][api-management-client-allowed-tenants]


<span data-ttu-id="aa606-157">Una vez Hola deseado especifica la configuración, haga clic en **guardar**.</span><span class="sxs-lookup"><span data-stu-id="aa606-157">Once hello desired configuration is specified, click **Save**.</span></span>

![Save][api-management-client-allowed-tenants-save]

<span data-ttu-id="aa606-159">Una vez que se guardan los cambios de hello, los usuarios de Hola Hola especificado Azure Active Directory puede iniciar sesión en el portal para desarrolladores de toohello siguiendo los pasos de hello en [inicie sesión en el portal para desarrolladores de toohello con una cuenta de Azure Active Directory] [Log in toohello Developer portal using an Azure Active Directory account].</span><span class="sxs-lookup"><span data-stu-id="aa606-159">Once hello changes are saved, hello users in hello specified Azure Active Directory can sign in toohello Developer portal by following hello steps in [Log in toohello Developer portal using an Azure Active Directory account][Log in toohello Developer portal using an Azure Active Directory account].</span></span>

<span data-ttu-id="aa606-160">Se pueden especificar varios dominios en hello **permitido inquilinos** sección.</span><span class="sxs-lookup"><span data-stu-id="aa606-160">Multiple domains can be specified in hello **Allowed Tenants** section.</span></span> <span data-ttu-id="aa606-161">Antes de que cualquier usuario puede iniciar sesión desde un dominio distinto al dominio original Hola donde se registró la aplicación hello, un administrador global de dominio diferente de hello debe conceder permiso para hello aplicación tooaccess datos de directorio.</span><span class="sxs-lookup"><span data-stu-id="aa606-161">Before any user can log in from a different domain than hello original domain where hello application was registered, a global administrator of hello different domain must grant permission for hello application tooaccess directory data.</span></span> <span data-ttu-id="aa606-162">permiso de toogrant, debería ir administrador global de hello demasiado`https://<URL of your developer portal>/aadadminconsent` (por ejemplo, https://contoso.portal.azure-api.net/aadadminconsent), tipo de nombre de dominio de Hola de Hola desean toogive acceso tooand el inquilino de Active Directory, haga clic en enviar.</span><span class="sxs-lookup"><span data-stu-id="aa606-162">toogrant permission, hello global administrator should go too`https://<URL of your developer portal>/aadadminconsent` (for example, https://contoso.portal.azure-api.net/aadadminconsent), type in hello domain name of hello Active Directory tenant they want toogive access tooand click Submit.</span></span> <span data-ttu-id="aa606-163">En la siguiente Hola ejemplo, un administrador global de `miaoaad.onmicrosoft.com` está tratando de portal para desarrolladores determinado de toogive permiso toothis.</span><span class="sxs-lookup"><span data-stu-id="aa606-163">In hello following example, a global administrator from `miaoaad.onmicrosoft.com` is trying toogive permission toothis particular developer portal.</span></span> 

![Permisos][api-management-aad-consent]

<span data-ttu-id="aa606-165">En la siguiente pantalla de bienvenida, administrador global de hello será solicitada tooconfirm da permiso al Hola.</span><span class="sxs-lookup"><span data-stu-id="aa606-165">In hello next screen, hello global administrator will be prompted tooconfirm giving hello permission.</span></span> 

![Permisos][api-management-permissions-form]

> <span data-ttu-id="aa606-167">Si un administrador no globales intenta toolog en antes de permisos se conceden por un administrador global, se produce un error en el intento de inicio de sesión de Hola y se muestra una pantalla de error.</span><span class="sxs-lookup"><span data-stu-id="aa606-167">If a non-global administrator tries toolog in before permissions are granted by a global administrator, hello login attempt fails and an error screen is displayed.</span></span>
> 
> 

## <a name="how-tooadd-an-external-azure-active-directory-group"></a><span data-ttu-id="aa606-168">¿Cómo tooadd un Azure Active Directory externo de grupo</span><span class="sxs-lookup"><span data-stu-id="aa606-168">How tooadd an external Azure Active Directory Group</span></span>
<span data-ttu-id="aa606-169">Después de habilitar el acceso de usuarios en Azure Active Directory, puede agregar grupos de Azure Active Directory en administración de API toomore administran fácilmente asociación Hola de desarrolladores de hello en el grupo de hello con productos de hello deseado.</span><span class="sxs-lookup"><span data-stu-id="aa606-169">After enabling access for users in an Azure Active Directory, you can add Azure Active Directory groups into API Management toomore easily manage hello association of hello developers in hello group with hello desired products.</span></span>

> <span data-ttu-id="aa606-170">tooconfigure un grupo externo de Azure Active Directory, hello Azure Active Directory debe configurarse primero en la pestaña de identidades de hello siguiendo el procedimiento de hello en la sección anterior de Hola.</span><span class="sxs-lookup"><span data-stu-id="aa606-170">tooconfigure an external Azure Active Directory group, hello Azure Active Directory must first be configured in hello Identities tab by following hello procedure in hello previous section.</span></span> 
> 
> 

<span data-ttu-id="aa606-171">Se agregan grupos externos de Azure Active Directory de hello **visibilidad** ficha de producto de hello para el que desea toohello grupo de acceso de toogrant.</span><span class="sxs-lookup"><span data-stu-id="aa606-171">External Azure Active Directory groups are added from hello **Visibility** tab of hello product for which you wish toogrant access toohello group.</span></span> <span data-ttu-id="aa606-172">Haga clic en **productos**y, a continuación, haga clic en nombre de Hola de producto de su preferencia Hola.</span><span class="sxs-lookup"><span data-stu-id="aa606-172">Click **Products**, and then click hello name of hello desired product.</span></span>

![Configure product][api-management-configure-product]

<span data-ttu-id="aa606-174">Cambiar toohello **visibilidad** ficha y haga clic en **agregar grupos de Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="aa606-174">Switch toohello **Visibility** tab, and click **Add Groups from Azure Active Directory**.</span></span>

![Agregar grupos][api-management-add-groups]

<span data-ttu-id="aa606-176">Seleccione hello **inquilino de Azure Active Directory** desde la lista desplegable de hello y, a continuación, nombre de grupo que quiera hello en Hola Hola de tipo **grupos** toobe Agregar cuadro de texto.</span><span class="sxs-lookup"><span data-stu-id="aa606-176">Select hello **Azure Active Directory Tenant** from hello drop-down list, and then type hello name of hello desired group in hello **Groups** toobe added text box.</span></span>

![Seleccionar grupo][api-management-select-group]

<span data-ttu-id="aa606-178">Este nombre de grupo puede encontrarse en hello **grupos** lista para Azure Active Directory, como se muestra en el siguiente ejemplo de Hola.</span><span class="sxs-lookup"><span data-stu-id="aa606-178">This group name can be found in hello **Groups** list for your Azure Active Directory, as shown in hello following example.</span></span>

![Lista de grupos de Azure Active Directory][api-management-aad-groups-list]

<span data-ttu-id="aa606-180">Haga clic en **agregar** toovalidate Hola nombre de grupo y agregar grupo de Hola.</span><span class="sxs-lookup"><span data-stu-id="aa606-180">Click **Add** toovalidate hello group name and add hello group.</span></span> <span data-ttu-id="aa606-181">En este ejemplo, Hola **a los desarrolladores de Contoso 5** se agrega el grupo externo.</span><span class="sxs-lookup"><span data-stu-id="aa606-181">In this example, hello **Contoso 5 Developers** external group is added.</span></span> 

![Group added][api-management-aad-group-added]

<span data-ttu-id="aa606-183">Haga clic en **guardar** toosave Hola nueva selección de grupo.</span><span class="sxs-lookup"><span data-stu-id="aa606-183">Click **Save** toosave hello new group selection.</span></span>

<span data-ttu-id="aa606-184">Una vez que ha configurado un grupo de Azure Active Directory desde uno de los productos, está disponible toobe comprueba en hello **visibilidad** pestaña Hola otros productos de instancia de servicio de administración de API de Hola.</span><span class="sxs-lookup"><span data-stu-id="aa606-184">Once an Azure Active Directory group has been configured from one product, it is available toobe checked on hello **Visibility** tab for hello other products in hello API Management service instance.</span></span>

<span data-ttu-id="aa606-185">tooreview y configurar las propiedades de Hola para grupos externos una vez que se hayan agregado, haga clic en nombre de hello del grupo de Hola de hello **grupos** ficha.</span><span class="sxs-lookup"><span data-stu-id="aa606-185">tooreview and configure hello properties for external groups once they have been added, click hello name of hello group from hello **Groups** tab.</span></span>

![Administrar grupos][api-management-groups]

<span data-ttu-id="aa606-187">Desde aquí puede editar hello **nombre** hello y **descripción** del grupo de Hola.</span><span class="sxs-lookup"><span data-stu-id="aa606-187">From here you can edit hello **Name** and hello **Description** of hello group.</span></span>

![Editar grupo][api-management-edit-group]

<span data-ttu-id="aa606-189">Los usuarios de hello configurado Azure Active Directory puede iniciar sesión en la vista y el portal para desarrolladores de toohello y suscribirse grupos tooany para los que tienen visibilidad siguiendo las instrucciones de Hola Hola pasos de la sección.</span><span class="sxs-lookup"><span data-stu-id="aa606-189">Users from hello configured Azure Active Directory can sign in toohello Developer portal and view and subscribe tooany groups for which they have visibility by following hello instructions in hello following section.</span></span>

## <a name="how-toolog-in-toohello-developer-portal-using-an-azure-active-directory-account"></a><span data-ttu-id="aa606-190">¿Cómo toolog en el portal para desarrolladores de toohello con una cuenta de Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="aa606-190">How toolog in toohello Developer portal using an Azure Active Directory account</span></span>
<span data-ttu-id="aa606-191">toolog en el portal para desarrolladores de hello con una cuenta de Azure Active Directory configurada en las secciones anteriores hello, abra una nueva ventana del explorador utilizando hello **dirección URL de inicio de sesión** de configuración de aplicación de Active Directory de Hola y haga clic en **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="aa606-191">toolog into hello Developer portal using an Azure Active Directory account configured in hello previous sections, open a new browser window using hello **Sign-on URL** from hello Active Directory application configuration, and click **Azure Active Directory**.</span></span>

![Portal para desarrolladores][api-management-dev-portal-signin]

<span data-ttu-id="aa606-193">Escriba las credenciales de Hola de uno de los usuarios de hello en Azure Active Directory y haga clic en **iniciar sesión en**.</span><span class="sxs-lookup"><span data-stu-id="aa606-193">Enter hello credentials of one of hello users in your Azure Active Directory, and click **Sign in**.</span></span>

![Iniciar sesión][api-management-aad-signin]

<span data-ttu-id="aa606-195">En caso de requerirse más información, puede que se le solicite un formulario de registro.</span><span class="sxs-lookup"><span data-stu-id="aa606-195">You may be prompted with a registration form if any additional information is required.</span></span> <span data-ttu-id="aa606-196">Complete el formulario de registro de hello y haga clic en **registrarse**.</span><span class="sxs-lookup"><span data-stu-id="aa606-196">Complete hello registration form and click **Sign up**.</span></span>

![Registro][api-management-complete-registration]

<span data-ttu-id="aa606-198">Ahora, el usuario se registra en el portal para desarrolladores de hello para la instancia de servicio de administración de API.</span><span class="sxs-lookup"><span data-stu-id="aa606-198">Your user is now logged into hello developer portal for your API Management service instance.</span></span>

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

[How tooadd operations tooan API]: api-management-howto-add-operations.md
[How tooadd and publish a product]: api-management-howto-add-products.md
[Monitoring and analytics]: api-management-monitoring.md
[Add APIs tooa product]: api-management-howto-add-products.md#add-apis
[Publish a product]: api-management-howto-add-products.md#publish-product
[Get started with Azure API Management]: api-management-get-started.md
[API Management policy reference]: api-management-policy-reference.md
[Caching policies]: api-management-policy-reference.md#caching-policies
[Create an API Management service instance]: api-management-get-started.md#create-service-instance

[http://oauth.net/2/]: http://oauth.net/2/
[WebApp-GraphAPI-DotNet]: https://github.com/AzureADSamples/WebApp-GraphAPI-DotNet
[Accessing hello Graph API]: http://msdn.microsoft.com/library/azure/dn132599.aspx#BKMK_Graph

[Prerequisites]: #prerequisites
[Configure an OAuth 2.0 authorization server in API Management]: #step1
[Configure an API toouse OAuth 2.0 user authorization]: #step2
[Test hello OAuth 2.0 user authorization in hello Developer Portal]: #step3
[Next steps]: #next-steps

[Log in toohello Developer portal using an Azure Active Directory account]: #Log-in-to-the-Developer-portal-using-an-Azure-Active-Directory-account

