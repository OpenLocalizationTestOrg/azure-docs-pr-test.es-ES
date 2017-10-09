---
title: "aaaAuthenticate con API de REST de Mobile Engagement - configuración manual"
description: "Describe cómo toomanually configurar la autenticación para las API de REST de Mobile Engagement"
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: 2e79f9c9-41e4-45ac-b427-3b8338675163
ms.service: mobile-engagement
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: mobile-multiple
ms.workload: mobile
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: 3884f94afcd6b9a62bfcf498fb6ee84bb6e837b7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="authenticate-with-mobile-engagement-rest-apis---manual-setup"></a><span data-ttu-id="dcbf1-103">Autenticación con las API de REST de Mobile Engagement: configuración manual</span><span class="sxs-lookup"><span data-stu-id="dcbf1-103">Authenticate with Mobile Engagement REST APIs - manual setup</span></span>
<span data-ttu-id="dcbf1-104">Se trata de una documentación de apéndice demasiado[autenticar con las API de REST de Mobile Engagement](mobile-engagement-api-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="dcbf1-104">This is an appendix documentation too[Authenticate with Mobile Engagement REST APIs](mobile-engagement-api-authentication.md).</span></span> <span data-ttu-id="dcbf1-105">Asegúrese de que pueda leerse primer contexto de hello tooget.</span><span class="sxs-lookup"><span data-stu-id="dcbf1-105">Make sure you read it first tooget hello context.</span></span> <span data-ttu-id="dcbf1-106">Describe una instalación única de forma alternativa toodo Hola sobre cómo configurar la autenticación para el uso de las API de REST de Mobile Engagement Hola Hola Portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="dcbf1-106">This describes an alternate way toodo hello One-time setup for setting up your authentication for hello Mobile Engagement REST APIs using hello Azure Portal.</span></span> 

> [!NOTE]
> <span data-ttu-id="dcbf1-107">instrucciones de Hello siguientes se basan en el objeto [Guía de Active Directory](../azure-resource-manager/resource-group-create-service-principal-portal.md) y personalizar para lo que se requiere para la autenticación de las API de Mobile Engagement.</span><span class="sxs-lookup"><span data-stu-id="dcbf1-107">hello instructions below are based on this [Active Directory guide](../azure-resource-manager/resource-group-create-service-principal-portal.md) and customized for what is required for authentication for Mobile Engagement APIs.</span></span> <span data-ttu-id="dcbf1-108">Así que haga referencia tooit si desea toounderstand Hola pasos detalladamente.</span><span class="sxs-lookup"><span data-stu-id="dcbf1-108">So refer tooit if you want toounderstand hello steps below in detail.</span></span> 
> 
> 

1. <span data-ttu-id="dcbf1-109">Inicio de sesión tooyour cuenta de Azure a través de hello [portal clásico](https://manage.windowsazure.com/).</span><span class="sxs-lookup"><span data-stu-id="dcbf1-109">Login tooyour Azure Account through hello [classic portal](https://manage.windowsazure.com/).</span></span>
2. <span data-ttu-id="dcbf1-110">Seleccione **Active Directory** en el panel izquierdo de Hola.</span><span class="sxs-lookup"><span data-stu-id="dcbf1-110">Select **Active Directory** from hello left pane.</span></span>
   
     ![seleccionar Active Directory][1]
3. <span data-ttu-id="dcbf1-112">Elija hello **predeterminada Active Directory** en el portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="dcbf1-112">Choose hello **Default Active Directory** in your Azure portal.</span></span> 
   
     ![elegir directorio][2]
   
   > [!IMPORTANT]
   > <span data-ttu-id="dcbf1-114">Este enfoque funciona sólo cuando está trabajando en su cuenta de Active Directory de forma predeterminada Hola y no funcionará si está realizando en Active Directory que haya creado en su cuenta.</span><span class="sxs-lookup"><span data-stu-id="dcbf1-114">This approach works only when you are working in hello default Active Directory of your account and will not work if you are doing this in an Active Directory that you have created in your account.</span></span> 
   > 
   > 
4. <span data-ttu-id="dcbf1-115">las aplicaciones de hello tooview en el directorio, haga clic en **aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="dcbf1-115">tooview hello applications in your directory, click on **Applications**.</span></span>
   
     ![ver aplicaciones][3]
5. <span data-ttu-id="dcbf1-117">Haga clic en **AGREGAR**.</span><span class="sxs-lookup"><span data-stu-id="dcbf1-117">Click on **ADD**.</span></span> 
   
     ![agregar aplicación][4]
6. <span data-ttu-id="dcbf1-119">Haga clic en **Agregar una aplicación que mi organización está desarrollando**</span><span class="sxs-lookup"><span data-stu-id="dcbf1-119">Click on **Add an application my organization is developing**</span></span>
   
     ![nueva aplicación][5]
7. <span data-ttu-id="dcbf1-121">Rellene el nombre de aplicación hello y tipo de select Hola de aplicación como **aplicación WEB Y/O API de WEB** y haga clic en el botón siguiente Hola.</span><span class="sxs-lookup"><span data-stu-id="dcbf1-121">Fill in name of hello application and select hello type of application as **WEB APPLICATION AND/OR WEB API** and click hello next button.</span></span>
   
     ![aplicación de nombre][6]
8. <span data-ttu-id="dcbf1-123">Puede especificar direcciones URL ficticias en **URL DE INICIO DE SESIÓN** y **URI DE ID. DE APLICACIÓN**.</span><span class="sxs-lookup"><span data-stu-id="dcbf1-123">You can provide any dummy URLs for **SIGN-ON URL** and **APP ID URI**.</span></span> <span data-ttu-id="dcbf1-124">No se usan en nuestro caso y no se validan las direcciones URL de Hola por sí mismos.</span><span class="sxs-lookup"><span data-stu-id="dcbf1-124">They are not used for our scenario and hello URLs themselves are not validated.</span></span>  
   
     ![propiedades de la aplicación][7]
9. <span data-ttu-id="dcbf1-126">Al final de Hola de esto, tendrá una aplicación AAD con el nombre de hello indicadas anteriormente como Hola siguiente.</span><span class="sxs-lookup"><span data-stu-id="dcbf1-126">At hello end of this, you will have an AAD app with hello name you provided previously like hello following.</span></span> <span data-ttu-id="dcbf1-127">Este es el **AD\_APP\_NAME** (anótelo).</span><span class="sxs-lookup"><span data-stu-id="dcbf1-127">This is your **AD\_APP\_NAME** and make a note of it.</span></span>  
   
     ![nombre de la aplicación][8]
10. <span data-ttu-id="dcbf1-129">Haga clic en el nombre de la aplicación hello y haga clic en **configurar**.</span><span class="sxs-lookup"><span data-stu-id="dcbf1-129">Click on hello app name and click on **Configure**.</span></span>
    
      ![configurar aplicación ][9]
11. <span data-ttu-id="dcbf1-131">Tome nota de hello Id. de cliente que se usará como **cliente\_ID** de la API llama.</span><span class="sxs-lookup"><span data-stu-id="dcbf1-131">Make a note of hello CLIENT ID that will be used as **CLIENT\_ID** for your API calls.</span></span> 
    
     ![configurar aplicación ][10]
12. <span data-ttu-id="dcbf1-133">Desplácese hacia abajo toohello **claves** sección, agregue una clave con preferiblemente una duración de 2 años (caducidad) y haga clic en **guardar**.</span><span class="sxs-lookup"><span data-stu-id="dcbf1-133">Scroll down toohello **Keys** section and add a key with preferably 2 years (expiry) duration and click **Save**.</span></span> 
    
     ![configurar aplicación ][11]
13. <span data-ttu-id="dcbf1-135">Copiar inmediatamente valor Hola que se muestra para la clave de hello, ya que solo se muestra ahora y no se almacena por lo que no se mostrarán nunca más.</span><span class="sxs-lookup"><span data-stu-id="dcbf1-135">Immediately copy hello value which is shown for hello key as it is only shown now and is not stored so will not be displayed ever again.</span></span> <span data-ttu-id="dcbf1-136">Si se pierde, tendrá toogenerate una nueva clave.</span><span class="sxs-lookup"><span data-stu-id="dcbf1-136">If you lose it then you will have toogenerate a new key.</span></span> <span data-ttu-id="dcbf1-137">Se trata de hello **CLIENT_SECRET** de la API llama.</span><span class="sxs-lookup"><span data-stu-id="dcbf1-137">This will be hello **CLIENT_SECRET** for your API calls.</span></span> 
    
     ![configurar aplicación ][12]
    
    > [!IMPORTANT]
    > <span data-ttu-id="dcbf1-139">Esta clave expirará final Hola de duración de Hola que especificó así toorenew seguro de Asegúrese de que cuanto tiempo hello en caso contrario, la autenticación de API dejará de funcionar.</span><span class="sxs-lookup"><span data-stu-id="dcbf1-139">This key will expire at hello end of hello duration that you specified so make sure toorenew it when hello time comes otherwise your API authentication will not work anymore.</span></span> <span data-ttu-id="dcbf1-140">También puede eliminar y volver a crear esta clave si cree que se ha visto comprometida.</span><span class="sxs-lookup"><span data-stu-id="dcbf1-140">You can also delete and recreate this key if you think that it has been compromised.</span></span>
    > 
    > 
14. <span data-ttu-id="dcbf1-141">Haga clic en **ver EXTREMOS** botón ahora que abrirían hello **extremos de la aplicación** cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="dcbf1-141">Click on **VIEW ENDPOINTS** button now which will open up hello **App Endpoints** dialog box.</span></span> 
    
    ![][13]
15. <span data-ttu-id="dcbf1-142">Desde el cuadro de diálogo de extremos de la aplicación hello, copie hello **extremo de TOKEN de OAUTH 2.0**.</span><span class="sxs-lookup"><span data-stu-id="dcbf1-142">From hello App Endpoints dialog box, copy hello **OAUTH 2.0 TOKEN ENDPOINT**.</span></span> 
    
    ![][14]
16. <span data-ttu-id="dcbf1-143">Este punto de conexión será en hello siguiente formulario donde hello GUID en la dirección URL de hello es su **TENANT_ID** por lo que tome nota del mismo:</span><span class="sxs-lookup"><span data-stu-id="dcbf1-143">This endpoint will be in hello following form where hello GUID in hello URL is your **TENANT_ID** so make a note of it:</span></span> 
    
        https://login.microsoftonline.com/<GUID>/oauth2/token
17. <span data-ttu-id="dcbf1-144">Ahora se continuará tooconfigure permisos de hello en esta aplicación.</span><span class="sxs-lookup"><span data-stu-id="dcbf1-144">Now we will proceed tooconfigure hello permissions on this app.</span></span> <span data-ttu-id="dcbf1-145">Para que esto tendrá tooopen seguridad hello [portal de Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="dcbf1-145">For this you will have tooopen up hello [Azure portal](https://portal.azure.com).</span></span> 
18. <span data-ttu-id="dcbf1-146">Haga clic en **grupos de recursos** y buscar hello **Mobile Engagement** grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="dcbf1-146">Click on **Resource Groups** and find hello **Mobile Engagement** resource group.</span></span>  
    
    ![][15]
19. <span data-ttu-id="dcbf1-147">Haga clic en hello **Mobile Engagement** recurso de grupo del sistema y desplácese toohello **configuración** hoja aquí.</span><span class="sxs-lookup"><span data-stu-id="dcbf1-147">Click hello **Mobile Engagement** resource group and navigate toohello **Settings** blade here.</span></span> 
    
    ![][16]
20. <span data-ttu-id="dcbf1-148">Haga clic en **usuarios** en Hola hoja de configuración y, a continuación, haga clic en **agregar** tooadd un usuario.</span><span class="sxs-lookup"><span data-stu-id="dcbf1-148">Click on **Users** in hello Settings blade and then click on **Add** tooadd a user.</span></span> 
    
    ![][17]
21. <span data-ttu-id="dcbf1-149">Haga clic en **Seleccionar un rol**</span><span class="sxs-lookup"><span data-stu-id="dcbf1-149">Click on **Select a role**</span></span>
    
    ![][18]
22. <span data-ttu-id="dcbf1-150">Haga clic en **Propietario**</span><span class="sxs-lookup"><span data-stu-id="dcbf1-150">Click on **Owner**</span></span>
    
    ![][19]
23. <span data-ttu-id="dcbf1-151">Búsqueda de nombre de saludo de la aplicación **AD\_aplicación\_nombre** en el cuadro de búsqueda de Hola.</span><span class="sxs-lookup"><span data-stu-id="dcbf1-151">Search for hello name of your application **AD\_APP\_NAME** in hello Search box.</span></span> <span data-ttu-id="dcbf1-152">No verá esto de forma predeterminada aquí.</span><span class="sxs-lookup"><span data-stu-id="dcbf1-152">You will not see this by default here.</span></span> <span data-ttu-id="dcbf1-153">Una vez que encuentra, selecciónelo y haga clic en **seleccione** final Hola de hoja de Hola.</span><span class="sxs-lookup"><span data-stu-id="dcbf1-153">Once you find it, select it and click on **Select** at hello bottom of hello blade.</span></span> 
    
    ![][20]
24. <span data-ttu-id="dcbf1-154">En hello **agregar acceso** hoja, se mostrará como **1 usuario, 0 grupos**.</span><span class="sxs-lookup"><span data-stu-id="dcbf1-154">On hello **Add Access** blade, it will show up as **1 user, 0 groups**.</span></span> <span data-ttu-id="dcbf1-155">Haga clic en **Aceptar** acerca de este cambio de hello tooconfirm de hoja.</span><span class="sxs-lookup"><span data-stu-id="dcbf1-155">Click **OK** on this blade tooconfirm hello change.</span></span> 
    
    ![][21]

<span data-ttu-id="dcbf1-156">Ahora ha completado la configuración de AAD de hello necesario y son Hola de toocall conjunto de todas las API.</span><span class="sxs-lookup"><span data-stu-id="dcbf1-156">You have now completed hello required AAD configuration and you are all set toocall hello APIs.</span></span> 

<!-- Images -->
[1]: ./media/mobile-engagement-api-authentication-manual/active-directory.png
[2]: ./media/mobile-engagement-api-authentication-manual/active-directory-details.png
[3]: ./media/mobile-engagement-api-authentication-manual/view-applications.png
[4]: ./media/mobile-engagement-api-authentication-manual/add-icon.png
[5]: ./media/mobile-engagement-api-authentication-manual/what-do-you-want-to-do.png
[6]: ./media/mobile-engagement-api-authentication-manual/tell-us-about-your-application.png
[7]: ./media/mobile-engagement-api-authentication-manual/app-properties.png
[8]: ./media/mobile-engagement-api-authentication-manual/aad-app.png
[9]: ./media/mobile-engagement-api-authentication-manual/configure-menu.png
[10]: ./media/mobile-engagement-api-authentication-manual/client-id.png
[11]: ./media/mobile-engagement-api-authentication-manual/client_secret.png
[12]: ./media/mobile-engagement-api-authentication-manual/keys.png
[13]: ./media/mobile-engagement-api-authentication-manual/view-endpoints.png
[14]: ./media/mobile-engagement-api-authentication-manual/app-endpoints.png
[15]: ./media/mobile-engagement-api-authentication-manual/resource-groups.png
[16]: ./media/mobile-engagement-api-authentication-manual/resource-groups-settings.png
[17]: ./media/mobile-engagement-api-authentication-manual/add-users.png
[18]: ./media/mobile-engagement-api-authentication-manual/add-role.png
[19]: ./media/mobile-engagement-api-authentication-manual/select-role.png
[20]: ./media/mobile-engagement-api-authentication-manual/add-user-select.png
[21]: ./media/mobile-engagement-api-authentication-manual/add-access-final.png



