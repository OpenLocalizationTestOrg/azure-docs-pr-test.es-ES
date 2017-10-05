---
title: "Autenticación de usuario final: Data Lake Store con Azure Active Directory | Microsoft Docs"
description: "Aprenda a lograr la autenticación del usuario final con Data Lake Store mediante Azure Active Directory"
services: data-lake-store
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
ms.assetid: ec586ecd-1b42-459e-b600-fadbb7b80a9b
ms.service: data-lake-store
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 04/21/2017
ms.author: nitinme
ms.openlocfilehash: c20f5c39b00992d801909c8e5de292f3c2f12673
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="end-user-authentication-with-data-lake-store-using-azure-active-directory"></a><span data-ttu-id="fe9f0-103">Autenticación de usuario final con Data Lake Store mediante Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="fe9f0-103">End-user authentication with Data Lake Store using Azure Active Directory</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="fe9f0-104">Autenticación entre servicios</span><span class="sxs-lookup"><span data-stu-id="fe9f0-104">Service-to-service authentication</span></span>](data-lake-store-authenticate-using-active-directory.md)
> * [<span data-ttu-id="fe9f0-105">Autenticación de usuario final</span><span class="sxs-lookup"><span data-stu-id="fe9f0-105">End-user authentication</span></span>](data-lake-store-end-user-authenticate-using-active-directory.md)
> 
> 

<span data-ttu-id="fe9f0-106">Azure Data Lake Store usa Azure Active Directory para la autenticación.</span><span class="sxs-lookup"><span data-stu-id="fe9f0-106">Azure Data Lake Store uses Azure Active Directory for authentication.</span></span> <span data-ttu-id="fe9f0-107">Antes de crear una aplicación que funcione con Azure Data Lake Store o Azure Data Lake Analytics, debe determinar cómo desea autenticar la aplicación con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="fe9f0-107">Before authoring an application that works with Azure Data Lake Store or Azure Data Lake Analytics, you must first decide how you would like to authenticate your application with Azure Active Directory (Azure AD).</span></span> <span data-ttu-id="fe9f0-108">Las dos principales opciones disponibles son:</span><span class="sxs-lookup"><span data-stu-id="fe9f0-108">The two main options available are:</span></span>

* <span data-ttu-id="fe9f0-109">Autenticación de usuario final (este artículo)</span><span class="sxs-lookup"><span data-stu-id="fe9f0-109">End-user authentication (this article)</span></span>
* <span data-ttu-id="fe9f0-110">Autenticación entre servicios</span><span class="sxs-lookup"><span data-stu-id="fe9f0-110">Service-to-service authentication</span></span>

<span data-ttu-id="fe9f0-111">Con ambas opciones, la aplicación recibe un token de OAuth 2.0 que se adjunta a cada solicitud realizada a Azure Data Lake Store o Azure Data Lake Analytics.</span><span class="sxs-lookup"><span data-stu-id="fe9f0-111">Both these options result in your application being provided with an OAuth 2.0 token, which gets attached to each request made to Azure Data Lake Store or Azure Data Lake Analytics.</span></span>

<span data-ttu-id="fe9f0-112">En este artículo se habla de cómo crear una **aplicación nativa de Azure AD para la autenticación de usuario final**.</span><span class="sxs-lookup"><span data-stu-id="fe9f0-112">This article talks about how create an **Azure AD native application for end-user authentication**.</span></span> <span data-ttu-id="fe9f0-113">Para obtener instrucciones sobre la configuración de la aplicación de Azure AD para la autenticación entre servicios, vea [Service-to-service authentication with Data Lake Store using Azure Active Directory](data-lake-store-authenticate-using-active-directory.md) (Autenticación entre servicios con Data Lake Store mediante Azure Active Directory).</span><span class="sxs-lookup"><span data-stu-id="fe9f0-113">For instructions on Azure AD application configuration for service-to-service authentication see [Service-to-service authentication with Data Lake Store using Azure Active Directory](data-lake-store-authenticate-using-active-directory.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="fe9f0-114">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="fe9f0-114">Prerequisites</span></span>
* <span data-ttu-id="fe9f0-115">Una suscripción de Azure.</span><span class="sxs-lookup"><span data-stu-id="fe9f0-115">An Azure subscription.</span></span> <span data-ttu-id="fe9f0-116">Consulte [How to get Azure Free trial for testing Hadoop in HDInsight (Obtención de una versión de prueba gratuita de Azure para probar Hadoop en HDInsight)](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="fe9f0-116">See [Get Azure free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

* <span data-ttu-id="fe9f0-117">El identificador de suscripción.</span><span class="sxs-lookup"><span data-stu-id="fe9f0-117">Your subscription ID.</span></span> <span data-ttu-id="fe9f0-118">Puede recuperarlo en Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="fe9f0-118">You can retrieve it from the Azure Portal.</span></span> <span data-ttu-id="fe9f0-119">Por ejemplo, está disponible en la hoja de la cuenta de Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="fe9f0-119">For example, it is available from the Data Lake Store account blade.</span></span>
  
    ![Obtener id. de suscripción](./media/data-lake-store-end-user-authenticate-using-active-directory/get-subscription-id.png)

* <span data-ttu-id="fe9f0-121">El nombre de dominio de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="fe9f0-121">Your Azure AD domain name.</span></span> <span data-ttu-id="fe9f0-122">Para recuperarlo, mantenga el puntero del mouse en la esquina superior derecha de Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="fe9f0-122">You can retrieve it by hovering the mouse in the top-right corner of the Azure Portal.</span></span> <span data-ttu-id="fe9f0-123">En la siguiente captura de pantalla, el nombre de dominio es **contoso.onmicrosoft.com** y el GUID entre paréntesis es el identificador del inquilino.</span><span class="sxs-lookup"><span data-stu-id="fe9f0-123">From the screenshot below, the domain name is **contoso.onmicrosoft.com**, and the GUID within brackets is the tenant ID.</span></span> 
  
    ![Obtener dominio de AAD](./media/data-lake-store-end-user-authenticate-using-active-directory/get-aad-domain.png)

## <a name="end-user-authentication"></a><span data-ttu-id="fe9f0-125">Autenticación de usuario final</span><span class="sxs-lookup"><span data-stu-id="fe9f0-125">End-user authentication</span></span>
<span data-ttu-id="fe9f0-126">Es el enfoque recomendado si desea que un usuario final inicie sesión en la aplicación a través de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="fe9f0-126">This is the recommended approach if you want an end-user to log in to your application via Azure AD.</span></span> <span data-ttu-id="fe9f0-127">La aplicación podrá tener acceso a los recursos de Azure con el mismo nivel de acceso que tiene el usuario final que inició sesión.</span><span class="sxs-lookup"><span data-stu-id="fe9f0-127">Your application will be able to access Azure resources with the same level of access as the end-user that logged in.</span></span> <span data-ttu-id="fe9f0-128">El usuario final deberá proporcionar sus credenciales de manera periódica para que la aplicación conserve el acceso.</span><span class="sxs-lookup"><span data-stu-id="fe9f0-128">Your end-user will need to provide their credentials periodically in order for your application to maintain access.</span></span>

<span data-ttu-id="fe9f0-129">El inicio de sesión del usuario final genera que su aplicación reciba un token de acceso y un token de actualización.</span><span class="sxs-lookup"><span data-stu-id="fe9f0-129">The result of having the end-user log in is that your application is given an access token and a refresh token.</span></span> <span data-ttu-id="fe9f0-130">El token de acceso se adjunta a cada solicitud hecha a Data Lake Store o Data Lake Analytics y es válido, de manera predeterminada, durante 1 hora.</span><span class="sxs-lookup"><span data-stu-id="fe9f0-130">The access token gets attached to each request made to Data Lake Store or Data Lake Analytics, and it is valid for one hour by default.</span></span> <span data-ttu-id="fe9f0-131">El token de actualización se puede usar para obtener un nuevo token de acceso y es válido, de manera predeterminada, hasta por dos semanas, si se usa de manera habitual.</span><span class="sxs-lookup"><span data-stu-id="fe9f0-131">The refresh token can be used to obtain a new access token, and it is valid for up to two weeks by default, if used regularly.</span></span> <span data-ttu-id="fe9f0-132">Puede usar dos enfoques distintos para el inicio de sesión del usuario final.</span><span class="sxs-lookup"><span data-stu-id="fe9f0-132">You can use two different approaches for end-user log in.</span></span>

### <a name="using-the-oauth-20-pop-up"></a><span data-ttu-id="fe9f0-133">Uso de la ventana emergente de OAuth 2.0</span><span class="sxs-lookup"><span data-stu-id="fe9f0-133">Using the OAuth 2.0 pop-up</span></span>
<span data-ttu-id="fe9f0-134">La aplicación puede desencadenar una ventana emergente de autorización de OAuth 2.0 en la que el usuario final puede escribir sus credenciales.</span><span class="sxs-lookup"><span data-stu-id="fe9f0-134">Your application can trigger an OAuth 2.0 authorization pop-up, in which the end-user can enter their credentials.</span></span> <span data-ttu-id="fe9f0-135">Esta ventana emergente también funciona con el proceso de autenticación en dos pasos (2FA) de Azure AD, si es necesario.</span><span class="sxs-lookup"><span data-stu-id="fe9f0-135">This pop-up also works with the Azure AD Two-factor Authentication (2FA) process, if required.</span></span> 

> [!NOTE]
> <span data-ttu-id="fe9f0-136">Este método todavía no es compatible con la Biblioteca de autenticación de Active Directory (ADAL) para Python o Java.</span><span class="sxs-lookup"><span data-stu-id="fe9f0-136">This method is not yet supported in the Azure AD Authentication Library (ADAL) for Python or Java.</span></span>
> 
> 

### <a name="directly-passing-in-user-credentials"></a><span data-ttu-id="fe9f0-137">Transmisión directa de credenciales de usuario</span><span class="sxs-lookup"><span data-stu-id="fe9f0-137">Directly passing in user credentials</span></span>
<span data-ttu-id="fe9f0-138">Su aplicación puede proporcionar directamente las credenciales de usuario a Azure AD.</span><span class="sxs-lookup"><span data-stu-id="fe9f0-138">Your application can directly provide user credentials to Azure AD.</span></span> <span data-ttu-id="fe9f0-139">Este método solo funciona con cuentas de usuario con identificador de organización; no es compatible con cuentas de usuario personales de tipo "Live ID", incluidas las que terminan en @outlook.com o @live.com.</span><span class="sxs-lookup"><span data-stu-id="fe9f0-139">This method only works with organizational ID user accounts; it is not compatible with personal / “live ID” user accounts, including those ending in @outlook.com or @live.com.</span></span> <span data-ttu-id="fe9f0-140">Además, este método no es compatible con las cuentas de usuario que requieren la autenticación en dos pasos (2FA) de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="fe9f0-140">Furthermore, this method is not compatible with user accounts that require Azure AD Two-factor Authentication (2FA).</span></span>

### <a name="what-do-i-need-to-use-this-approach"></a><span data-ttu-id="fe9f0-141">¿Qué se necesita para usar este enfoque?</span><span class="sxs-lookup"><span data-stu-id="fe9f0-141">What do I need to use this approach?</span></span>
* <span data-ttu-id="fe9f0-142">El nombre de dominio de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="fe9f0-142">Azure AD domain name.</span></span> <span data-ttu-id="fe9f0-143">Este ya aparece en los requisitos previos de este artículo.</span><span class="sxs-lookup"><span data-stu-id="fe9f0-143">This is already listed in the prerequisite of this article.</span></span>
* <span data-ttu-id="fe9f0-144">**Aplicación nativa** de Azure AD</span><span class="sxs-lookup"><span data-stu-id="fe9f0-144">Azure AD **native application**</span></span>
* <span data-ttu-id="fe9f0-145">Identificador de la aplicación nativa de Azure AD</span><span class="sxs-lookup"><span data-stu-id="fe9f0-145">Application ID for the Azure AD native application</span></span>
* <span data-ttu-id="fe9f0-146">URI de redirección de la aplicación nativa de Azure AD</span><span class="sxs-lookup"><span data-stu-id="fe9f0-146">Redirect URI for the Azure AD native application</span></span>
* <span data-ttu-id="fe9f0-147">Establecimiento de permisos delegados</span><span class="sxs-lookup"><span data-stu-id="fe9f0-147">Set delegated permissions</span></span>


## <a name="step-1-create-an-active-directory-native-application"></a><span data-ttu-id="fe9f0-148">Paso 1: Crear una aplicación nativa de Active Directory</span><span class="sxs-lookup"><span data-stu-id="fe9f0-148">Step 1: Create an Active Directory native application</span></span>

<span data-ttu-id="fe9f0-149">Cree y configure una aplicación nativa de Azure AD para la autenticación de usuario final con Azure Data Lake Store mediante Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="fe9f0-149">Create and configure an Azure AD native application for end-user authentication with Azure Data Lake Store using Azure Active Directory.</span></span> <span data-ttu-id="fe9f0-150">Para obtener instrucciones, vea cómo [crear una aplicación de Azure AD](../azure-resource-manager/resource-group-create-service-principal-portal.md).</span><span class="sxs-lookup"><span data-stu-id="fe9f0-150">For instructions, see [Create an Azure AD application](../azure-resource-manager/resource-group-create-service-principal-portal.md).</span></span>

<span data-ttu-id="fe9f0-151">Al seguir las instrucciones que aparecen en el vínculo anterior, asegúrese de seleccionar **Nativa** para el tipo de aplicación, como se muestra en la captura de pantalla siguiente.</span><span class="sxs-lookup"><span data-stu-id="fe9f0-151">While following the instructions at the above link, make sure you select **Native** for application type, as shown in the screenshot below.</span></span>

<span data-ttu-id="fe9f0-152">![Crear aplicación de web](./media/data-lake-store-end-user-authenticate-using-active-directory/azure-active-directory-create-native-app.png "Crear aplicación nativa")</span><span class="sxs-lookup"><span data-stu-id="fe9f0-152">![Create web app](./media/data-lake-store-end-user-authenticate-using-active-directory/azure-active-directory-create-native-app.png "Create native app")</span></span>

## <a name="step-2-get-application-id-and-redirect-uri"></a><span data-ttu-id="fe9f0-153">Paso 2: Obtener el identificador de aplicación y el URI de redirección</span><span class="sxs-lookup"><span data-stu-id="fe9f0-153">Step 2: Get application id and redirect URI</span></span>

<span data-ttu-id="fe9f0-154">Vea [Get the application ID](../azure-resource-manager/resource-group-create-service-principal-portal.md#get-application-id-and-authentication-key) (Obtener el identificador de la aplicación) para recuperar el identificador de aplicación (también llamado identificador de cliente en el Portal de Azure clásico) de la aplicación nativa de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="fe9f0-154">See [Get the application ID](../azure-resource-manager/resource-group-create-service-principal-portal.md#get-application-id-and-authentication-key) to retrieve the application id (also called the client ID in the Azure classic portal) of the Azure AD native application.</span></span>

<span data-ttu-id="fe9f0-155">Para recuperar el URI de redireccionamiento, siga estos pasos.</span><span class="sxs-lookup"><span data-stu-id="fe9f0-155">To retrieve the redirect URI, follow the steps below.</span></span>

1. <span data-ttu-id="fe9f0-156">En Azure Portal, seleccione **Azure Active Directory**, haga clic en **Registros de aplicaciones**y después busque y haga clic en la aplicación nativa de Azure AD que acaba de crear.</span><span class="sxs-lookup"><span data-stu-id="fe9f0-156">From the Azure Portal, select **Azure Active Directory**, click **App registrations**, and then find and click the Azure AD native application that you just created.</span></span>

2. <span data-ttu-id="fe9f0-157">En la hoja **Configuración** de la aplicación, haga clic en **URI de redirección**.</span><span class="sxs-lookup"><span data-stu-id="fe9f0-157">From the **Settings** blade for the application, click **Redirect URIs**.</span></span>

    ![Obtener URI de redirección](./media/data-lake-store-end-user-authenticate-using-active-directory/azure-active-directory-redirect-uri.png)

3. <span data-ttu-id="fe9f0-159">Copie el valor mostrado.</span><span class="sxs-lookup"><span data-stu-id="fe9f0-159">Copy the value displayed.</span></span>


## <a name="step-3-set-permissions"></a><span data-ttu-id="fe9f0-160">Paso 3: Establecer permisos</span><span class="sxs-lookup"><span data-stu-id="fe9f0-160">Step 3: Set permissions</span></span>

1. <span data-ttu-id="fe9f0-161">En Azure Portal, seleccione **Azure Active Directory**, haga clic en **Registros de aplicaciones**y después busque y haga clic en la aplicación nativa de Azure AD que acaba de crear.</span><span class="sxs-lookup"><span data-stu-id="fe9f0-161">From the Azure Portal, select **Azure Active Directory**, click **App registrations**, and then find and click the Azure AD native application that you just created.</span></span>

2. <span data-ttu-id="fe9f0-162">En la hoja **Configuración** de la aplicación, haga clic en **Permisos necesarios** y después en **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="fe9f0-162">From the **Settings** blade for the application, click **Required permissions**, and then click **Add**.</span></span>

    ![ID. DE CLIENTE](./media/data-lake-store-end-user-authenticate-using-active-directory/aad-end-user-auth-set-permission-1.png)

3. <span data-ttu-id="fe9f0-164">En la hoja **Agregar acceso de API**, haga clic en **Seleccionar una API**, después en **Azure Data Lake** y, por último, en **Seleccionar**.</span><span class="sxs-lookup"><span data-stu-id="fe9f0-164">In the **Add API Access** blade, click **Select an API**, click **Azure Data Lake**, and then click **Select**.</span></span>

    ![ID. DE CLIENTE](./media/data-lake-store-end-user-authenticate-using-active-directory/aad-end-user-auth-set-permission-2.png)
 
4.  <span data-ttu-id="fe9f0-166">En la hoja **Agregar acceso de API**, haga clic en **Seleccionar permisos**, active la casilla de verificación para conceder **acceso total a Data Lake Store** y después haga clic en **Seleccionar**.</span><span class="sxs-lookup"><span data-stu-id="fe9f0-166">In the **Add API Access** blade, click **Select permissions**, select the check box to give **Full access to Data Lake Store**, and then click **Select**.</span></span>

    ![ID. DE CLIENTE](./media/data-lake-store-end-user-authenticate-using-active-directory/aad-end-user-auth-set-permission-3.png)

    <span data-ttu-id="fe9f0-168">Haga clic en **Done**.</span><span class="sxs-lookup"><span data-stu-id="fe9f0-168">Click **Done**.</span></span>

5. <span data-ttu-id="fe9f0-169">Repita los dos últimos pasos para conceder permisos también para **Service Management API de Windows Azure**.</span><span class="sxs-lookup"><span data-stu-id="fe9f0-169">Repeat the last two steps to grant permissions for **Windows Azure Service Management API** as well.</span></span>
   
## <a name="next-steps"></a><span data-ttu-id="fe9f0-170">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="fe9f0-170">Next steps</span></span>
<span data-ttu-id="fe9f0-171">En este artículo se ha creado una aplicación nativa de Azure AD y se ha recopilado la información que necesita en las aplicaciones cliente que cree mediante el SDK de .NET, el SDK de Java, la API de REST, etc. Ahora puede continuar en los artículos siguientes, que hablan de cómo usar la aplicación web de Azure AD para autenticarse primero en Data Lake Store y luego realizar otras operaciones en el almacén.</span><span class="sxs-lookup"><span data-stu-id="fe9f0-171">In this article you created an Azure AD native application and gathered the information you need in your client applications that you author using .NET SDK, Java SDK, REST API, etc. You can now proceed to the following articles that talk about how to use the Azure AD web application to first authenticate with Data Lake Store and then perform other operations on the store.</span></span>

* [<span data-ttu-id="fe9f0-172">Introducción al Almacén de Azure Data Lake mediante SDK de .NET</span><span class="sxs-lookup"><span data-stu-id="fe9f0-172">Get started with Azure Data Lake Store using .NET SDK</span></span>](data-lake-store-get-started-net-sdk.md)
* [<span data-ttu-id="fe9f0-173">Introducción a Azure Data Lake Store con el SDK de Java</span><span class="sxs-lookup"><span data-stu-id="fe9f0-173">Get started with Azure Data Lake Store using Java SDK</span></span>](data-lake-store-get-started-java-sdk.md)
* [<span data-ttu-id="fe9f0-174">Introducción a Azure Data Lake Store mediante la API de REST</span><span class="sxs-lookup"><span data-stu-id="fe9f0-174">Get started with Azure Data Lake Store using REST API</span></span>](data-lake-store-get-started-rest-api.md)

