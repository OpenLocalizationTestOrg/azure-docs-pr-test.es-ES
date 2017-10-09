---
title: "aaaSet una página de inicio personalizada para las aplicaciones publicadas mediante el uso de Proxy de aplicación de Azure AD | Documentos de Microsoft"
description: "Abarca conceptos básicos de hello acerca de los conectores de Proxy de aplicación de Azure AD"
services: active-directory
documentationcenter: 
author: kgremban
manager: femila
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/17/2017
ms.author: kgremban
ms.reviewer: harshja
ms.custom: it-pro
ms.openlocfilehash: 5bb695e904d285c3b440520f107c7bf63ba5cac9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="set-a-custom-home-page-for-published-apps-by-using-azure-ad-application-proxy"></a><span data-ttu-id="9c61d-103">Establecimiento de una página principal personalizada para aplicaciones publicadas mediante el Proxy de aplicación de Azure AD</span><span class="sxs-lookup"><span data-stu-id="9c61d-103">Set a custom home page for published apps by using Azure AD Application Proxy</span></span>

<span data-ttu-id="9c61d-104">Este artículo se describe cómo tooconfigure aplicaciones toodirect usuarios tooa página principal personalizada.</span><span class="sxs-lookup"><span data-stu-id="9c61d-104">This article discusses how tooconfigure apps toodirect users tooa custom home page.</span></span> <span data-ttu-id="9c61d-105">Al publicar una aplicación con el Proxy de aplicación, establecer una dirección URL interna pero a veces no es página Hola que los usuarios deben ver en primer lugar.</span><span class="sxs-lookup"><span data-stu-id="9c61d-105">When you publish an application with Application Proxy, you set an internal URL but sometimes that's not hello page your users should see first.</span></span> <span data-ttu-id="9c61d-106">Establecer una página principal personalizada para que los usuarios entren página derecha toohello cuando tienen acceso a aplicaciones de Hola de Hola Panel de acceso de Azure Active Directory o iniciador de aplicaciones de Office 365 Hola.</span><span class="sxs-lookup"><span data-stu-id="9c61d-106">Set a custom home page so that your users go toohello right page when they access hello apps from hello Azure Active Directory Access Panel or hello Office 365 app launcher.</span></span>

<span data-ttu-id="9c61d-107">Cuando los usuarios inicien la aplicación hello, se le dirige por predeterminada toohello raíz dirección URL del dominio de aplicación publicados de hello.</span><span class="sxs-lookup"><span data-stu-id="9c61d-107">When users launch hello app, they're directed by default toohello root domain URL for hello published app.</span></span> <span data-ttu-id="9c61d-108">página de aterrizaje de Hello normalmente se establece como dirección URL de página principal de Hola.</span><span class="sxs-lookup"><span data-stu-id="9c61d-108">hello landing page is typically set as hello home page URL.</span></span> <span data-ttu-id="9c61d-109">Utilice direcciones URL de página principal personalizada de hello Azure AD PowerShell módulo toodefine cuando desee tooland de los usuarios de aplicación en una página específica dentro de la aplicación hello.</span><span class="sxs-lookup"><span data-stu-id="9c61d-109">Use hello Azure AD PowerShell module toodefine custom home page URLs when you want app users tooland on a specific page within hello app.</span></span> 

<span data-ttu-id="9c61d-110">Por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="9c61d-110">For example:</span></span>
- <span data-ttu-id="9c61d-111">Dentro de la red corporativa, los usuarios ir demasiado*https://ExpenseApp/login/login.aspx* toosign en y tener acceso a la aplicación.</span><span class="sxs-lookup"><span data-stu-id="9c61d-111">Inside your corporate network, users go too*https://ExpenseApp/login/login.aspx* toosign in and access your app.</span></span>
- <span data-ttu-id="9c61d-112">Porque tiene otros recursos como imágenes que el Proxy de aplicación necesita tooaccess en nivel superior de Hola de estructura de carpetas de hello, publicar la aplicación hello con *https://ExpenseApp* como Hola URL interna.</span><span class="sxs-lookup"><span data-stu-id="9c61d-112">Because you have other assets like images that Application Proxy needs tooaccess at hello top level of hello folder structure, you publish hello app with *https://ExpenseApp* as hello internal URL.</span></span>
- <span data-ttu-id="9c61d-113">Hola predeterminado es la dirección URL externa *https://ExpenseApp-contoso.msappproxy.net*, que no toma su inicio de sesión de toohello de usuarios en la página.</span><span class="sxs-lookup"><span data-stu-id="9c61d-113">hello default external URL is *https://ExpenseApp-contoso.msappproxy.net*, which doesn't take your users toohello sign in page.</span></span>  
- <span data-ttu-id="9c61d-114">Establecer *https://ExpenseApp-contoso.msappproxy.net/login/login.aspx* como Hola toogive de dirección URL de página principal de los usuarios una experiencia sin problemas.</span><span class="sxs-lookup"><span data-stu-id="9c61d-114">Set *https://ExpenseApp-contoso.msappproxy.net/login/login.aspx* as hello home page URL toogive your users a seamless experience.</span></span> 

>[!NOTE]
><span data-ttu-id="9c61d-115">Cuando concede a los usuarios acceso toopublished aplicaciones, aplicaciones de Hola se muestran en hello [Panel de acceso de Azure AD](active-directory-saas-access-panel-introduction.md) hello y [iniciador de aplicaciones de Office 365](https://blogs.office.com/2016/09/27/introducing-the-new-office-365-app-launcher).</span><span class="sxs-lookup"><span data-stu-id="9c61d-115">When you give users access toopublished apps, hello apps are displayed in hello [Azure AD Access Panel](active-directory-saas-access-panel-introduction.md) and hello [Office 365 app launcher](https://blogs.office.com/2016/09/27/introducing-the-new-office-365-app-launcher).</span></span>

## <a name="before-you-start"></a><span data-ttu-id="9c61d-116">Antes de comenzar</span><span class="sxs-lookup"><span data-stu-id="9c61d-116">Before you start</span></span>

<span data-ttu-id="9c61d-117">Antes de configurar URL de la página de inicio de hello, tenga en hello cuenta según los requisitos:</span><span class="sxs-lookup"><span data-stu-id="9c61d-117">Before you set hello home page URL, keep in mind hello following requirements:</span></span>

* <span data-ttu-id="9c61d-118">Asegúrese de esa ruta de acceso de hello especificada es una ruta de acceso de subdominio de hello dirección URL raíz del dominio.</span><span class="sxs-lookup"><span data-stu-id="9c61d-118">Ensure that hello path you specify is a subdomain path of hello root domain URL.</span></span>

  <span data-ttu-id="9c61d-119">Si es la dirección URL del dominio raíz de hello, por ejemplo, https://apps.contoso.com/app1/, dirección URL de la página principal de Hola que configure debe empezar por https://apps.contoso.com/app1/.</span><span class="sxs-lookup"><span data-stu-id="9c61d-119">If hello root-domain URL is, for example, https://apps.contoso.com/app1/, hello home page URL that you configure must start with https://apps.contoso.com/app1/.</span></span>

* <span data-ttu-id="9c61d-120">Si realiza un cambio toohello publica la aplicación, cambio Hola puede restablecer el valor de Hola de dirección URL de página principal de Hola.</span><span class="sxs-lookup"><span data-stu-id="9c61d-120">If you make a change toohello published app, hello change might reset hello value of hello home page URL.</span></span> <span data-ttu-id="9c61d-121">Cuando se actualiza la aplicación hello en hello futuras, debe volver a comprobar y, si es necesario, actualice la dirección URL de página principal de Hola.</span><span class="sxs-lookup"><span data-stu-id="9c61d-121">When you update hello app in hello future, you should recheck and, if necessary, update hello home page URL.</span></span>

## <a name="change-hello-home-page-in-hello-azure-portal"></a><span data-ttu-id="9c61d-122">Cambiar la página principal Hola Hola portal de Azure</span><span class="sxs-lookup"><span data-stu-id="9c61d-122">Change hello home page in hello Azure portal</span></span>

1. <span data-ttu-id="9c61d-123">Inicie sesión en toohello [portal de Azure](https://portal.azure.com) como administrador.</span><span class="sxs-lookup"><span data-stu-id="9c61d-123">Sign in toohello [Azure portal](https://portal.azure.com) as an administrator.</span></span>
2. <span data-ttu-id="9c61d-124">Navegue demasiado**Azure Active Directory** > **registros de aplicación** y elija la aplicación de lista de Hola.</span><span class="sxs-lookup"><span data-stu-id="9c61d-124">Navigate too**Azure Active Directory** > **App registrations** and choose your application from hello list.</span></span> 
3. <span data-ttu-id="9c61d-125">Seleccione **propiedades** de configuración de Hola.</span><span class="sxs-lookup"><span data-stu-id="9c61d-125">Select **Properties** from hello settings.</span></span>
4. <span data-ttu-id="9c61d-126">Hola de actualización **URL de la página de inicio** campo con la nueva ruta de acceso.</span><span class="sxs-lookup"><span data-stu-id="9c61d-126">Update hello **Home page URL** field with your new path.</span></span> 

   ![Especifique la nueva dirección URL de la página principal](./media/application-proxy-office365-app-launcher/homepage.png)

5. <span data-ttu-id="9c61d-128">Seleccione **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="9c61d-128">Select **Save**</span></span>

## <a name="change-hello-home-page-with-powershell"></a><span data-ttu-id="9c61d-129">Cambiar la página principal Hola con PowerShell</span><span class="sxs-lookup"><span data-stu-id="9c61d-129">Change hello home page with PowerShell</span></span>

### <a name="install-hello-azure-ad-powershell-module"></a><span data-ttu-id="9c61d-130">Instalar el módulo de PowerShell de Azure AD Hola</span><span class="sxs-lookup"><span data-stu-id="9c61d-130">Install hello Azure AD PowerShell module</span></span>

<span data-ttu-id="9c61d-131">Antes de definir una dirección URL de la página principal personalizada mediante el uso de PowerShell, instale el módulo de PowerShell de Azure AD de Hola.</span><span class="sxs-lookup"><span data-stu-id="9c61d-131">Before you define a custom home page URL by using PowerShell, install hello Azure AD PowerShell module.</span></span> <span data-ttu-id="9c61d-132">Puede descargar paquetes de saludo de hello [Galería de PowerShell](https://www.powershellgallery.com/packages/AzureAD/2.0.0.131), que usa Hola extremo de API Graph.</span><span class="sxs-lookup"><span data-stu-id="9c61d-132">You can download hello package from hello [PowerShell Gallery](https://www.powershellgallery.com/packages/AzureAD/2.0.0.131), which uses hello Graph API endpoint.</span></span> 

<span data-ttu-id="9c61d-133">Hola tooinstall del paquete, siga estos pasos:</span><span class="sxs-lookup"><span data-stu-id="9c61d-133">tooinstall hello package, follow these steps:</span></span>

1. <span data-ttu-id="9c61d-134">Abra una ventana de PowerShell estándar y, a continuación, ejecute el siguiente comando de hello:</span><span class="sxs-lookup"><span data-stu-id="9c61d-134">Open a standard PowerShell window, and then run hello following command:</span></span>

    ```
     Install-Module -Name AzureAD
    ```
    <span data-ttu-id="9c61d-135">Si está ejecutando el comando hello como sin derechos administrativos, utilice hello `-scope currentuser` opción.</span><span class="sxs-lookup"><span data-stu-id="9c61d-135">If you're running hello command as a non-admin, use hello `-scope currentuser` option.</span></span>
2. <span data-ttu-id="9c61d-136">Durante la instalación de hello, seleccione **Y** tooinstall dos paquetes en Nuget.org. Se requieren ambos paquetes.</span><span class="sxs-lookup"><span data-stu-id="9c61d-136">During hello installation, select **Y** tooinstall two packages from Nuget.org. Both packages are required.</span></span> 

### <a name="find-hello-objectid-of-hello-app"></a><span data-ttu-id="9c61d-137">Buscar Hola ObjectID de aplicación hello</span><span class="sxs-lookup"><span data-stu-id="9c61d-137">Find hello ObjectID of hello app</span></span>

<span data-ttu-id="9c61d-138">Obtener Hola ObjectID de aplicación hello y, a continuación, busque aplicación hello por su página de inicio.</span><span class="sxs-lookup"><span data-stu-id="9c61d-138">Obtain hello ObjectID of hello app, and then search for hello app by its home page.</span></span>

1. <span data-ttu-id="9c61d-139">Abrir PowerShell e importe el módulo de hello Azure AD.</span><span class="sxs-lookup"><span data-stu-id="9c61d-139">Open PowerShell and import hello Azure AD module.</span></span>

    ```
    Import-Module AzureAD
    ```

2. <span data-ttu-id="9c61d-140">Inicie sesión en toohello módulo de Azure AD como administrador de inquilinos de Hola.</span><span class="sxs-lookup"><span data-stu-id="9c61d-140">Sign in toohello Azure AD module as hello tenant administrator.</span></span>

    ```
    Connect-AzureAD
    ```
3. <span data-ttu-id="9c61d-141">Buscar la aplicación hello en función de su dirección URL de la página principal.</span><span class="sxs-lookup"><span data-stu-id="9c61d-141">Find hello app based on its home page URL.</span></span> <span data-ttu-id="9c61d-142">Puede encontrar direcciones URL de hello en portal de hello yendo demasiado**Azure Active Directory** > **aplicaciones empresariales** > **todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="9c61d-142">You can find hello URL in hello portal by going too**Azure Active Directory** > **Enterprise applications** > **All applications**.</span></span> <span data-ttu-id="9c61d-143">Este ejemplo usa *sharepoint-iddemo*.</span><span class="sxs-lookup"><span data-stu-id="9c61d-143">This example uses *sharepoint-iddemo*.</span></span>

    ```
    Get-AzureADApplication | where { $_.Homepage -like “sharepoint-iddemo” } | fl DisplayName, Homepage, ObjectID
    ```
4. <span data-ttu-id="9c61d-144">Debería obtener un resultado que es toohello similar que se muestra aquí.</span><span class="sxs-lookup"><span data-stu-id="9c61d-144">You should get a result that's similar toohello one shown here.</span></span> <span data-ttu-id="9c61d-145">Copie hello toouse ObjectID GUID en la sección siguiente Hola.</span><span class="sxs-lookup"><span data-stu-id="9c61d-145">Copy hello ObjectID GUID toouse in hello next section.</span></span>

    ```
    DisplayName : SharePoint
    Homepage    : https://sharepoint-iddemo.msappproxy.net/
    ObjectId    : 8af89bfa-eac6-40b0-8a13-c2c4e3ee22a4
    ```

### <a name="update-hello-home-page-url"></a><span data-ttu-id="9c61d-146">Dirección URL de página principal de actualización Hola</span><span class="sxs-lookup"><span data-stu-id="9c61d-146">Update hello home page URL</span></span>

<span data-ttu-id="9c61d-147">Hola mismo módulo de PowerShell que usó para el paso 1, realizar Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="9c61d-147">In hello same PowerShell module that you used for step 1, perform hello following steps:</span></span>

1. <span data-ttu-id="9c61d-148">Confirme que tiene Hola corregir la aplicación y reemplace *8af89bfa-eac6-40b0-8a13-c2c4e3ee22a4* con hello ObjectID que ha copiado en hello anterior paso.</span><span class="sxs-lookup"><span data-stu-id="9c61d-148">Confirm that you have hello correct app, and replace *8af89bfa-eac6-40b0-8a13-c2c4e3ee22a4* with hello ObjectID that you copied in hello preceding step.</span></span>

    ```
    Get-AzureADApplication -ObjectId 8af89bfa-eac6-40b0-8a13-c2c4e3ee22a4.
    ```

 <span data-ttu-id="9c61d-149">Ahora que ha confirmado la aplicación hello, está listo tooupdate Hola portada, como se indica a continuación.</span><span class="sxs-lookup"><span data-stu-id="9c61d-149">Now that you've confirmed hello app, you're ready tooupdate hello home page, as follows.</span></span>

2. <span data-ttu-id="9c61d-150">Crear un toohold de objeto de aplicación vacía cambios de Hola que desea toomake.</span><span class="sxs-lookup"><span data-stu-id="9c61d-150">Create a blank application object toohold hello changes that you want toomake.</span></span> <span data-ttu-id="9c61d-151">Esta variable contiene valores de hello que desea tooupdate.</span><span class="sxs-lookup"><span data-stu-id="9c61d-151">This variable holds hello values that you want tooupdate.</span></span> <span data-ttu-id="9c61d-152">En este paso no se crea nada.</span><span class="sxs-lookup"><span data-stu-id="9c61d-152">Nothing is created in this step.</span></span>

    ```
    $appnew = New-Object “Microsoft.Open.AzureAD.Model.Application”
    ```

3. <span data-ttu-id="9c61d-153">Establecer el valor de toohello de dirección URL de página principal de Hola que desee.</span><span class="sxs-lookup"><span data-stu-id="9c61d-153">Set hello home page URL toohello value that you want.</span></span> <span data-ttu-id="9c61d-154">valor de Hello debe ser una ruta de acceso de subdominio de la aplicación publicada Hola.</span><span class="sxs-lookup"><span data-stu-id="9c61d-154">hello value must be a subdomain path of hello published app.</span></span> <span data-ttu-id="9c61d-155">Por ejemplo, si cambia Hola URL de la página de inicio de *https://sharepoint-iddemo.msappproxy.net/* demasiado*https://sharepoint-iddemo.msappproxy.net/hybrid/*, los usuarios de la aplicación vaya directamente toohello personalizado página principal.</span><span class="sxs-lookup"><span data-stu-id="9c61d-155">For example, if you change hello home page URL from *https://sharepoint-iddemo.msappproxy.net/* too*https://sharepoint-iddemo.msappproxy.net/hybrid/*, app users go directly toohello custom home page.</span></span>

    ```
    $homepage = “https://sharepoint-iddemo.msappproxy.net/hybrid/”
    ```
4. <span data-ttu-id="9c61d-156">Asegúrese de Hola actualización mediante el uso de hello GUID (ObjectID) que ha copiado en "paso 1: buscar Hola ObjectID de aplicación hello."</span><span class="sxs-lookup"><span data-stu-id="9c61d-156">Make hello update by using hello GUID (ObjectID) that you copied in "Step 1: Find hello ObjectID of hello app."</span></span>

    ```
    Set-AzureADApplication -ObjectId 8af89bfa-eac6-40b0-8a13-c2c4e3ee22a4 -Homepage $homepage
    ```
5. <span data-ttu-id="9c61d-157">tooconfirm que Hola se cambió correctamente, reinicie la aplicación hello.</span><span class="sxs-lookup"><span data-stu-id="9c61d-157">tooconfirm that hello change was successful, restart hello app.</span></span>

    ```
    Get-AzureADApplication -ObjectId 8af89bfa-eac6-40b0-8a13-c2c4e3ee22a4
    ```

>[!NOTE]
><span data-ttu-id="9c61d-158">Los cambios que realice toohello aplicación podrían restablecer URL de la página de inicio de Hola.</span><span class="sxs-lookup"><span data-stu-id="9c61d-158">Any changes that you make toohello app might reset hello home page URL.</span></span> <span data-ttu-id="9c61d-159">Si se restablecer la dirección URL de la página principal, repita el paso 2.</span><span class="sxs-lookup"><span data-stu-id="9c61d-159">If your home page URL resets, repeat step 2.</span></span>

## <a name="next-steps"></a><span data-ttu-id="9c61d-160">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="9c61d-160">Next steps</span></span>

- [<span data-ttu-id="9c61d-161">Habilitar acceso remoto tooSharePoint con el Proxy de aplicación de Azure AD</span><span class="sxs-lookup"><span data-stu-id="9c61d-161">Enable remote access tooSharePoint with Azure AD Application Proxy</span></span>](application-proxy-enable-remote-access-sharepoint.md)
- [<span data-ttu-id="9c61d-162">Habilita el Proxy de aplicación en hello portal de Azure</span><span class="sxs-lookup"><span data-stu-id="9c61d-162">Enable Application Proxy in hello Azure portal</span></span>](active-directory-application-proxy-enable.md)
