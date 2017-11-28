---
title: "Establecimiento de una página principal personalizada para aplicaciones publicadas mediante el Proxy de aplicación de Azure AD | Microsoft Docs"
description: "Se explican los conceptos básicos acerca de los conectores del Proxy de aplicación de Azure AD."
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
ms.openlocfilehash: 9069166259265f5d2b43043b75039e239f397f6c
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/29/2017
---
# <a name="set-a-custom-home-page-for-published-apps-by-using-azure-ad-application-proxy"></a><span data-ttu-id="ec484-103">Establecimiento de una página principal personalizada para aplicaciones publicadas mediante el Proxy de aplicación de Azure AD</span><span class="sxs-lookup"><span data-stu-id="ec484-103">Set a custom home page for published apps by using Azure AD Application Proxy</span></span>

<span data-ttu-id="ec484-104">En este artículo se explica cómo configurar aplicaciones para que dirijan a los usuarios a una página principal personalizada.</span><span class="sxs-lookup"><span data-stu-id="ec484-104">This article discusses how to configure apps to direct users to a custom home page.</span></span> <span data-ttu-id="ec484-105">Al publicar una aplicación con el proxy de la aplicación, se establece una dirección URL interna pero, a veces, esa no es la primera página que deben ver los usuarios.</span><span class="sxs-lookup"><span data-stu-id="ec484-105">When you publish an application with Application Proxy, you set an internal URL but sometimes that's not the page your users should see first.</span></span> <span data-ttu-id="ec484-106">Establezca una página principal personalizada para que los usuarios vayan a la página correcta cuando accedan a las aplicaciones desde el Panel de acceso de Azure Active Directory o desde el iniciador de aplicaciones de Office 365.</span><span class="sxs-lookup"><span data-stu-id="ec484-106">Set a custom home page so that your users go to the right page when they access the apps from the Azure Active Directory Access Panel or the Office 365 app launcher.</span></span>

<span data-ttu-id="ec484-107">Cuando los usuarios inician sus aplicaciones, se les dirige de manera predeterminada a la dirección URL raíz del dominio raíz de la aplicación publicada.</span><span class="sxs-lookup"><span data-stu-id="ec484-107">When users launch the app, they're directed by default to the root domain URL for the published app.</span></span> <span data-ttu-id="ec484-108">La página de aterrizaje normalmente se establece como la dirección URL de la página principal.</span><span class="sxs-lookup"><span data-stu-id="ec484-108">The landing page is typically set as the home page URL.</span></span> <span data-ttu-id="ec484-109">Use el módulo de Azure AD PowerShell para definir las direcciones URL de la página principal personalizada cuando desee que los usuarios de la aplicación lleguen a una página concreta de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="ec484-109">Use the Azure AD PowerShell module to define custom home page URLs when you want app users to land on a specific page within the app.</span></span> 

<span data-ttu-id="ec484-110">Por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="ec484-110">For example:</span></span>
- <span data-ttu-id="ec484-111">En la red de su compañía, los usuarios van a *https://ExpenseApp/login/login.aspx* para iniciar sesión y acceder a su aplicación.</span><span class="sxs-lookup"><span data-stu-id="ec484-111">Inside your corporate network, users go to *https://ExpenseApp/login/login.aspx* to sign in and access your app.</span></span>
- <span data-ttu-id="ec484-112">Dado que tiene otros recursos, como imágenes, que el proxy de la aplicación necesita para acceder al nivel superior de la estructura de carpetas, publica la aplicación con *https://ExpenseApp* como dirección URL interna.</span><span class="sxs-lookup"><span data-stu-id="ec484-112">Because you have other assets like images that Application Proxy needs to access at the top level of the folder structure, you publish the app with *https://ExpenseApp* as the internal URL.</span></span>
- <span data-ttu-id="ec484-113">La dirección URL externa predeterminada es *https://ExpenseApp-contoso.msappproxy.net*, que no lleva a los usuarios a la página de inicio de sesión.</span><span class="sxs-lookup"><span data-stu-id="ec484-113">The default external URL is *https://ExpenseApp-contoso.msappproxy.net*, which doesn't take your users to the sign in page.</span></span>  
- <span data-ttu-id="ec484-114">Establezca *https://ExpenseApp-contoso.msappproxy.net/login/login.aspx* como dirección URL de la página principal para que los usuarios no tengan problemas.</span><span class="sxs-lookup"><span data-stu-id="ec484-114">Set *https://ExpenseApp-contoso.msappproxy.net/login/login.aspx* as the home page URL to give your users a seamless experience.</span></span> 

>[!NOTE]
><span data-ttu-id="ec484-115">Al proporcionar a los usuarios acceso a las aplicaciones publicadas, estas aparecen en el [panel de acceso de Azure AD](active-directory-saas-access-panel-introduction.md) y el [iniciador de aplicaciones de Office 365](https://blogs.office.com/2016/09/27/introducing-the-new-office-365-app-launcher).</span><span class="sxs-lookup"><span data-stu-id="ec484-115">When you give users access to published apps, the apps are displayed in the [Azure AD Access Panel](active-directory-saas-access-panel-introduction.md) and the [Office 365 app launcher](https://blogs.office.com/2016/09/27/introducing-the-new-office-365-app-launcher).</span></span>

## <a name="before-you-start"></a><span data-ttu-id="ec484-116">Antes de comenzar</span><span class="sxs-lookup"><span data-stu-id="ec484-116">Before you start</span></span>

<span data-ttu-id="ec484-117">Antes de establecer la dirección URL de la página principal tenga en cuenta los siguientes requisitos:</span><span class="sxs-lookup"><span data-stu-id="ec484-117">Before you set the home page URL, keep in mind the following requirements:</span></span>

* <span data-ttu-id="ec484-118">Asegúrese de que la ruta de acceso especificada sea una ruta de acceso de subdominio de la dirección URL raíz del dominio.</span><span class="sxs-lookup"><span data-stu-id="ec484-118">Ensure that the path you specify is a subdomain path of the root domain URL.</span></span>

  <span data-ttu-id="ec484-119">Si la dirección URL raíz del dominio es, por ejemplo, https://apps.contoso.com/app1/, la dirección URL de la página principal que configure debe empezar por https://apps.contoso.com/app1/.</span><span class="sxs-lookup"><span data-stu-id="ec484-119">If the root-domain URL is, for example, https://apps.contoso.com/app1/, the home page URL that you configure must start with https://apps.contoso.com/app1/.</span></span>

* <span data-ttu-id="ec484-120">Si realiza un cambio en la aplicación publicada, este podría restablecer el valor de la dirección URL de la página principal.</span><span class="sxs-lookup"><span data-stu-id="ec484-120">If you make a change to the published app, the change might reset the value of the home page URL.</span></span> <span data-ttu-id="ec484-121">Si actualiza la aplicación en el futuro, debe volver a comprobar y, si es necesario, actualizar la dirección URL de la página principal.</span><span class="sxs-lookup"><span data-stu-id="ec484-121">When you update the app in the future, you should recheck and, if necessary, update the home page URL.</span></span>

## <a name="change-the-home-page-in-the-azure-portal"></a><span data-ttu-id="ec484-122">Vaya a la página principal de Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="ec484-122">Change the home page in the Azure portal</span></span>

1. <span data-ttu-id="ec484-123">Inicie sesión en [Azure Portal](https://portal.azure.com) como administrador.</span><span class="sxs-lookup"><span data-stu-id="ec484-123">Sign in to the [Azure portal](https://portal.azure.com) as an administrator.</span></span>
2. <span data-ttu-id="ec484-124">Vaya a **Azure Active Directory** > **Registros de aplicación** y elija la aplicación de la lista.</span><span class="sxs-lookup"><span data-stu-id="ec484-124">Navigate to **Azure Active Directory** > **App registrations** and choose your application from the list.</span></span> 
3. <span data-ttu-id="ec484-125">Seleccione **Propiedades** en las opciones.</span><span class="sxs-lookup"><span data-stu-id="ec484-125">Select **Properties** from the settings.</span></span>
4. <span data-ttu-id="ec484-126">Actualice el campo **URL de página principal** con la nueva ruta de acceso.</span><span class="sxs-lookup"><span data-stu-id="ec484-126">Update the **Home page URL** field with your new path.</span></span> 

   ![Especifique la nueva dirección URL de la página principal](./media/application-proxy-office365-app-launcher/homepage.png)

5. <span data-ttu-id="ec484-128">Seleccione **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="ec484-128">Select **Save**</span></span>

## <a name="change-the-home-page-with-powershell"></a><span data-ttu-id="ec484-129">Cambio de la página principal con PowerShell</span><span class="sxs-lookup"><span data-stu-id="ec484-129">Change the home page with PowerShell</span></span>

### <a name="install-the-azure-ad-powershell-module"></a><span data-ttu-id="ec484-130">Instalación del módulo de PowerShell de Azure AD</span><span class="sxs-lookup"><span data-stu-id="ec484-130">Install the Azure AD PowerShell module</span></span>

<span data-ttu-id="ec484-131">Para poder definir la dirección URL de la página principal personalizada mediante PowerShell, instale el módulo de Azure AD PowerShell.</span><span class="sxs-lookup"><span data-stu-id="ec484-131">Before you define a custom home page URL by using PowerShell, install the Azure AD PowerShell module.</span></span> <span data-ttu-id="ec484-132">Puede descargar este paquete desde la [Galería de PowerShell](https://www.powershellgallery.com/packages/AzureAD/2.0.0.131), que utiliza el punto de conexión de API Graph.</span><span class="sxs-lookup"><span data-stu-id="ec484-132">You can download the package from the [PowerShell Gallery](https://www.powershellgallery.com/packages/AzureAD/2.0.0.131), which uses the Graph API endpoint.</span></span> 

<span data-ttu-id="ec484-133">Para instalar el paquete, siga estos pasos:</span><span class="sxs-lookup"><span data-stu-id="ec484-133">To install the package, follow these steps:</span></span>

1. <span data-ttu-id="ec484-134">Abra una ventana de PowerShell estándar y luego ejecute el siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="ec484-134">Open a standard PowerShell window, and then run the following command:</span></span>

    ```
     Install-Module -Name AzureAD
    ```
    <span data-ttu-id="ec484-135">Si está ejecutando el comando como no administrador, use la opción `-scope currentuser`.</span><span class="sxs-lookup"><span data-stu-id="ec484-135">If you're running the command as a non-admin, use the `-scope currentuser` option.</span></span>
2. <span data-ttu-id="ec484-136">Durante la instalación, seleccione **Y** para instalar dos paquetes de Nuget.org. Se requieren ambos paquetes.</span><span class="sxs-lookup"><span data-stu-id="ec484-136">During the installation, select **Y** to install two packages from Nuget.org. Both packages are required.</span></span> 

### <a name="find-the-objectid-of-the-app"></a><span data-ttu-id="ec484-137">Busque el valor ObjectID de la aplicación</span><span class="sxs-lookup"><span data-stu-id="ec484-137">Find the ObjectID of the app</span></span>

<span data-ttu-id="ec484-138">Obtenga el ObjectID de la aplicación y, a continuación, busque la aplicación por su página principal.</span><span class="sxs-lookup"><span data-stu-id="ec484-138">Obtain the ObjectID of the app, and then search for the app by its home page.</span></span>

1. <span data-ttu-id="ec484-139">Abra PowerShell e importe el módulo de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="ec484-139">Open PowerShell and import the Azure AD module.</span></span>

    ```
    Import-Module AzureAD
    ```

2. <span data-ttu-id="ec484-140">Inicie sesión como administrador de inquilinos en el módulo de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="ec484-140">Sign in to the Azure AD module as the tenant administrator.</span></span>

    ```
    Connect-AzureAD
    ```
3. <span data-ttu-id="ec484-141">Busque la aplicación en función de su dirección URL de página principal.</span><span class="sxs-lookup"><span data-stu-id="ec484-141">Find the app based on its home page URL.</span></span> <span data-ttu-id="ec484-142">Puede ver la dirección URL en el portal si va a **Azure Active Directory** > **Aplicaciones empresariales** > **Todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="ec484-142">You can find the URL in the portal by going to **Azure Active Directory** > **Enterprise applications** > **All applications**.</span></span> <span data-ttu-id="ec484-143">Este ejemplo usa *sharepoint-iddemo*.</span><span class="sxs-lookup"><span data-stu-id="ec484-143">This example uses *sharepoint-iddemo*.</span></span>

    ```
    Get-AzureADApplication | where { $_.Homepage -like “sharepoint-iddemo” } | fl DisplayName, Homepage, ObjectID
    ```
4. <span data-ttu-id="ec484-144">Debe obtener un resultado similar al que se muestra aquí.</span><span class="sxs-lookup"><span data-stu-id="ec484-144">You should get a result that's similar to the one shown here.</span></span> <span data-ttu-id="ec484-145">Copie el GUID de ObjectID para usarlo en la siguiente sección.</span><span class="sxs-lookup"><span data-stu-id="ec484-145">Copy the ObjectID GUID to use in the next section.</span></span>

    ```
    DisplayName : SharePoint
    Homepage    : https://sharepoint-iddemo.msappproxy.net/
    ObjectId    : 8af89bfa-eac6-40b0-8a13-c2c4e3ee22a4
    ```

### <a name="update-the-home-page-url"></a><span data-ttu-id="ec484-146">Actualización de la dirección URL de la página principal</span><span class="sxs-lookup"><span data-stu-id="ec484-146">Update the home page URL</span></span>

<span data-ttu-id="ec484-147">En el mismo módulo de PowerShell que ha usado para el paso 1, siga estos pasos:</span><span class="sxs-lookup"><span data-stu-id="ec484-147">In the same PowerShell module that you used for step 1, perform the following steps:</span></span>

1. <span data-ttu-id="ec484-148">Confirme que tiene la aplicación correcta y reemplace *8af89bfa-eac6-40b0-8a13-c2c4e3ee22a4* por el ObjectID que copió en el paso anterior.</span><span class="sxs-lookup"><span data-stu-id="ec484-148">Confirm that you have the correct app, and replace *8af89bfa-eac6-40b0-8a13-c2c4e3ee22a4* with the ObjectID that you copied in the preceding step.</span></span>

    ```
    Get-AzureADApplication -ObjectId 8af89bfa-eac6-40b0-8a13-c2c4e3ee22a4.
    ```

 <span data-ttu-id="ec484-149">Ahora que ha confirmado la aplicación, está preparado para actualizar la página principal como se indica a continuación.</span><span class="sxs-lookup"><span data-stu-id="ec484-149">Now that you've confirmed the app, you're ready to update the home page, as follows.</span></span>

2. <span data-ttu-id="ec484-150">Cree un objeto de aplicación en blanco para que contenga los cambios que desea realizar.</span><span class="sxs-lookup"><span data-stu-id="ec484-150">Create a blank application object to hold the changes that you want to make.</span></span> <span data-ttu-id="ec484-151">Esta variable contiene los valores que desea actualizar.</span><span class="sxs-lookup"><span data-stu-id="ec484-151">This variable holds the values that you want to update.</span></span> <span data-ttu-id="ec484-152">En este paso no se crea nada.</span><span class="sxs-lookup"><span data-stu-id="ec484-152">Nothing is created in this step.</span></span>

    ```
    $appnew = New-Object “Microsoft.Open.AzureAD.Model.Application”
    ```

3. <span data-ttu-id="ec484-153">Establezca la dirección URL de la página principal en el valor que quiera.</span><span class="sxs-lookup"><span data-stu-id="ec484-153">Set the home page URL to the value that you want.</span></span> <span data-ttu-id="ec484-154">El valor debe ser una ruta de acceso de subdominio de la aplicación publicada.</span><span class="sxs-lookup"><span data-stu-id="ec484-154">The value must be a subdomain path of the published app.</span></span> <span data-ttu-id="ec484-155">Por ejemplo, si cambia la dirección URL de la página principal de *https://sharepoint-iddemo.msappproxy.net/* a *https://sharepoint-iddemo.msappproxy.net/hybrid/*, los usuarios de la aplicación van directamente a la página principal personalizada.</span><span class="sxs-lookup"><span data-stu-id="ec484-155">For example, if you change the home page URL from *https://sharepoint-iddemo.msappproxy.net/* to *https://sharepoint-iddemo.msappproxy.net/hybrid/*, app users go directly to the custom home page.</span></span>

    ```
    $homepage = “https://sharepoint-iddemo.msappproxy.net/hybrid/”
    ```
4. <span data-ttu-id="ec484-156">Realice la actualización mediante el GUID (ObjectID) que copió en el "Paso 1: busque el ObjectID de la aplicación".</span><span class="sxs-lookup"><span data-stu-id="ec484-156">Make the update by using the GUID (ObjectID) that you copied in "Step 1: Find the ObjectID of the app."</span></span>

    ```
    Set-AzureADApplication -ObjectId 8af89bfa-eac6-40b0-8a13-c2c4e3ee22a4 -Homepage $homepage
    ```
5. <span data-ttu-id="ec484-157">Para confirmar que el cambio fue correcto, reinicie la aplicación.</span><span class="sxs-lookup"><span data-stu-id="ec484-157">To confirm that the change was successful, restart the app.</span></span>

    ```
    Get-AzureADApplication -ObjectId 8af89bfa-eac6-40b0-8a13-c2c4e3ee22a4
    ```

>[!NOTE]
><span data-ttu-id="ec484-158">Los cambios realizados en la aplicación pueden restablecer la dirección URL de la página principal.</span><span class="sxs-lookup"><span data-stu-id="ec484-158">Any changes that you make to the app might reset the home page URL.</span></span> <span data-ttu-id="ec484-159">Si se restablecer la dirección URL de la página principal, repita el paso 2.</span><span class="sxs-lookup"><span data-stu-id="ec484-159">If your home page URL resets, repeat step 2.</span></span>

## <a name="next-steps"></a><span data-ttu-id="ec484-160">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="ec484-160">Next steps</span></span>

- [<span data-ttu-id="ec484-161">Habilitar el acceso remoto a SharePoint con el Proxy de aplicación de Azure AD</span><span class="sxs-lookup"><span data-stu-id="ec484-161">Enable remote access to SharePoint with Azure AD Application Proxy</span></span>](application-proxy-enable-remote-access-sharepoint.md)
- [<span data-ttu-id="ec484-162">Habilitación del proxy de aplicación en Azure Portal</span><span class="sxs-lookup"><span data-stu-id="ec484-162">Enable Application Proxy in the Azure portal</span></span>](active-directory-application-proxy-enable.md)
