---
title: "Autenticación de usuario final: Data Lake Store con Azure Active Directory | Microsoft Docs"
description: "Obtenga información acerca de cómo tooachieve la autenticación del usuario final con el almacén de Data Lake con Azure Active Directory"
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
ms.openlocfilehash: fd58f4f2d8fc915b8bc51d9e5b040d2cee34047e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="end-user-authentication-with-data-lake-store-using-azure-active-directory"></a><span data-ttu-id="2cd07-103">Autenticación de usuario final con Data Lake Store mediante Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="2cd07-103">End-user authentication with Data Lake Store using Azure Active Directory</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="2cd07-104">Autenticación entre servicios</span><span class="sxs-lookup"><span data-stu-id="2cd07-104">Service-to-service authentication</span></span>](data-lake-store-authenticate-using-active-directory.md)
> * [<span data-ttu-id="2cd07-105">Autenticación de usuario final</span><span class="sxs-lookup"><span data-stu-id="2cd07-105">End-user authentication</span></span>](data-lake-store-end-user-authenticate-using-active-directory.md)
> 
> 

<span data-ttu-id="2cd07-106">Azure Data Lake Store usa Azure Active Directory para la autenticación.</span><span class="sxs-lookup"><span data-stu-id="2cd07-106">Azure Data Lake Store uses Azure Active Directory for authentication.</span></span> <span data-ttu-id="2cd07-107">Antes de crear una aplicación que funcione con el almacén de Azure Data Lake o análisis de Data Lake de Azure, primero debe decidir cómo desea que tooauthenticate su aplicación con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="2cd07-107">Before authoring an application that works with Azure Data Lake Store or Azure Data Lake Analytics, you must first decide how you would like tooauthenticate your application with Azure Active Directory (Azure AD).</span></span> <span data-ttu-id="2cd07-108">Hola dos opciones principales disponibles son:</span><span class="sxs-lookup"><span data-stu-id="2cd07-108">hello two main options available are:</span></span>

* <span data-ttu-id="2cd07-109">Autenticación de usuario final (este artículo)</span><span class="sxs-lookup"><span data-stu-id="2cd07-109">End-user authentication (this article)</span></span>
* <span data-ttu-id="2cd07-110">Autenticación entre servicios</span><span class="sxs-lookup"><span data-stu-id="2cd07-110">Service-to-service authentication</span></span>

<span data-ttu-id="2cd07-111">Ambas opciones como resultado de la aplicación que se proporciona con un token de OAuth 2.0, que obtiene tooeach adjunto solicitud realizada tooAzure almacén de Data Lake o análisis de Data Lake de Azure.</span><span class="sxs-lookup"><span data-stu-id="2cd07-111">Both these options result in your application being provided with an OAuth 2.0 token, which gets attached tooeach request made tooAzure Data Lake Store or Azure Data Lake Analytics.</span></span>

<span data-ttu-id="2cd07-112">En este artículo se habla de cómo crear una **aplicación nativa de Azure AD para la autenticación de usuario final**.</span><span class="sxs-lookup"><span data-stu-id="2cd07-112">This article talks about how create an **Azure AD native application for end-user authentication**.</span></span> <span data-ttu-id="2cd07-113">Para obtener instrucciones sobre la configuración de la aplicación de Azure AD para la autenticación entre servicios, vea [Service-to-service authentication with Data Lake Store using Azure Active Directory](data-lake-store-authenticate-using-active-directory.md) (Autenticación entre servicios con Data Lake Store mediante Azure Active Directory).</span><span class="sxs-lookup"><span data-stu-id="2cd07-113">For instructions on Azure AD application configuration for service-to-service authentication see [Service-to-service authentication with Data Lake Store using Azure Active Directory](data-lake-store-authenticate-using-active-directory.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="2cd07-114">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="2cd07-114">Prerequisites</span></span>
* <span data-ttu-id="2cd07-115">Una suscripción de Azure.</span><span class="sxs-lookup"><span data-stu-id="2cd07-115">An Azure subscription.</span></span> <span data-ttu-id="2cd07-116">Consulte [How to get Azure Free trial for testing Hadoop in HDInsight (Obtención de una versión de prueba gratuita de Azure para probar Hadoop en HDInsight)](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="2cd07-116">See [Get Azure free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

* <span data-ttu-id="2cd07-117">El identificador de suscripción.</span><span class="sxs-lookup"><span data-stu-id="2cd07-117">Your subscription ID.</span></span> <span data-ttu-id="2cd07-118">Puede recuperarlo desde Hola Portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="2cd07-118">You can retrieve it from hello Azure Portal.</span></span> <span data-ttu-id="2cd07-119">Por ejemplo, está disponible desde la hoja de cuenta de almacén de Data Lake Hola.</span><span class="sxs-lookup"><span data-stu-id="2cd07-119">For example, it is available from hello Data Lake Store account blade.</span></span>
  
    ![Obtener id. de suscripción](./media/data-lake-store-end-user-authenticate-using-active-directory/get-subscription-id.png)

* <span data-ttu-id="2cd07-121">El nombre de dominio de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="2cd07-121">Your Azure AD domain name.</span></span> <span data-ttu-id="2cd07-122">Puede recuperarlo mediante el desplazamiento del mouse de hello en la esquina superior derecha de Hola de hello Portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="2cd07-122">You can retrieve it by hovering hello mouse in hello top-right corner of hello Azure Portal.</span></span> <span data-ttu-id="2cd07-123">En la captura de pantalla de Hola a continuación, nombre de dominio de hello es **contoso.onmicrosoft.com**, y Hola GUID entre corchetes es el identificador del inquilino Hola.</span><span class="sxs-lookup"><span data-stu-id="2cd07-123">From hello screenshot below, hello domain name is **contoso.onmicrosoft.com**, and hello GUID within brackets is hello tenant ID.</span></span> 
  
    ![Obtener dominio de AAD](./media/data-lake-store-end-user-authenticate-using-active-directory/get-aad-domain.png)

## <a name="end-user-authentication"></a><span data-ttu-id="2cd07-125">Autenticación de usuario final</span><span class="sxs-lookup"><span data-stu-id="2cd07-125">End-user authentication</span></span>
<span data-ttu-id="2cd07-126">Se trata de hello enfoque recomendado si desea que un toolog por el usuario final en la aplicación de tooyour a través de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="2cd07-126">This is hello recommended approach if you want an end-user toolog in tooyour application via Azure AD.</span></span> <span data-ttu-id="2cd07-127">La aplicación será capaz de tooaccess recursos de Azure con hello mismo nivel de acceso como usuario final de Hola que ha iniciado sesión.</span><span class="sxs-lookup"><span data-stu-id="2cd07-127">Your application will be able tooaccess Azure resources with hello same level of access as hello end-user that logged in.</span></span> <span data-ttu-id="2cd07-128">El usuario final deberá tooprovide sus credenciales periódicamente en orden para el acceso a la aplicación toomaintain.</span><span class="sxs-lookup"><span data-stu-id="2cd07-128">Your end-user will need tooprovide their credentials periodically in order for your application toomaintain access.</span></span>

<span data-ttu-id="2cd07-129">resultado de Hello de la existencia del usuario final de hello sesión es que la aplicación recibe un token de acceso y un token de actualización.</span><span class="sxs-lookup"><span data-stu-id="2cd07-129">hello result of having hello end-user log in is that your application is given an access token and a refresh token.</span></span> <span data-ttu-id="2cd07-130">token de acceso de Hello obtiene solicitud tooeach adjunto realizado tooData Lake almacén o análisis de Data Lake y tiene una validez de una hora de forma predeterminada.</span><span class="sxs-lookup"><span data-stu-id="2cd07-130">hello access token gets attached tooeach request made tooData Lake Store or Data Lake Analytics, and it is valid for one hour by default.</span></span> <span data-ttu-id="2cd07-131">token de actualización de Hello puede ser usado tooobtain un nuevo token de acceso y es válido para semanas tootwo de forma predeterminada, si se utiliza con regularidad.</span><span class="sxs-lookup"><span data-stu-id="2cd07-131">hello refresh token can be used tooobtain a new access token, and it is valid for up tootwo weeks by default, if used regularly.</span></span> <span data-ttu-id="2cd07-132">Puede usar dos enfoques distintos para el inicio de sesión del usuario final.</span><span class="sxs-lookup"><span data-stu-id="2cd07-132">You can use two different approaches for end-user log in.</span></span>

### <a name="using-hello-oauth-20-pop-up"></a><span data-ttu-id="2cd07-133">Utilizando la ventana emergente de hello OAuth 2.0</span><span class="sxs-lookup"><span data-stu-id="2cd07-133">Using hello OAuth 2.0 pop-up</span></span>
<span data-ttu-id="2cd07-134">La aplicación puede desencadenar un menú emergente de autorización OAuth 2.0, en qué hello para el usuario final puede escribir sus credenciales.</span><span class="sxs-lookup"><span data-stu-id="2cd07-134">Your application can trigger an OAuth 2.0 authorization pop-up, in which hello end-user can enter their credentials.</span></span> <span data-ttu-id="2cd07-135">Este elemento emergente también funciona con el proceso de autenticación en dos fases de Azure AD (2FA) de hello, si es necesario.</span><span class="sxs-lookup"><span data-stu-id="2cd07-135">This pop-up also works with hello Azure AD Two-factor Authentication (2FA) process, if required.</span></span> 

> [!NOTE]
> <span data-ttu-id="2cd07-136">Este método no se admite todavía en hello biblioteca de autenticación de Azure AD (AAL) para Python o Java.</span><span class="sxs-lookup"><span data-stu-id="2cd07-136">This method is not yet supported in hello Azure AD Authentication Library (ADAL) for Python or Java.</span></span>
> 
> 

### <a name="directly-passing-in-user-credentials"></a><span data-ttu-id="2cd07-137">Transmisión directa de credenciales de usuario</span><span class="sxs-lookup"><span data-stu-id="2cd07-137">Directly passing in user credentials</span></span>
<span data-ttu-id="2cd07-138">La aplicación puede proporcionar directamente tooAzure de credenciales de usuario AD.</span><span class="sxs-lookup"><span data-stu-id="2cd07-138">Your application can directly provide user credentials tooAzure AD.</span></span> <span data-ttu-id="2cd07-139">Este método solo funciona con cuentas de usuario con identificador de organización; no es compatible con cuentas de usuario personales de tipo "Live ID", incluidas las que terminan en @outlook.com o @live.com. Además, este método no es compatible con las cuentas de usuario que requieren la autenticación en dos pasos (2FA) de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="2cd07-139">This method only works with organizational ID user accounts; it is not compatible with personal / “live ID” user accounts, including those ending in @outlook.com or @live.com. Furthermore, this method is not compatible with user accounts that require Azure AD Two-factor Authentication (2FA).</span></span>

### <a name="what-do-i-need-toouse-this-approach"></a><span data-ttu-id="2cd07-140">¿Qué necesito toouse este enfoque?</span><span class="sxs-lookup"><span data-stu-id="2cd07-140">What do I need toouse this approach?</span></span>
* <span data-ttu-id="2cd07-141">El nombre de dominio de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="2cd07-141">Azure AD domain name.</span></span> <span data-ttu-id="2cd07-142">Esto ya aparece en el requisito previo de Hola de este artículo.</span><span class="sxs-lookup"><span data-stu-id="2cd07-142">This is already listed in hello prerequisite of this article.</span></span>
* <span data-ttu-id="2cd07-143">**Aplicación nativa** de Azure AD</span><span class="sxs-lookup"><span data-stu-id="2cd07-143">Azure AD **native application**</span></span>
* <span data-ttu-id="2cd07-144">Identificador de la aplicación para aplicación nativa de hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="2cd07-144">Application ID for hello Azure AD native application</span></span>
* <span data-ttu-id="2cd07-145">URI de redirección de hello aplicación nativa de Azure AD</span><span class="sxs-lookup"><span data-stu-id="2cd07-145">Redirect URI for hello Azure AD native application</span></span>
* <span data-ttu-id="2cd07-146">Establecimiento de permisos delegados</span><span class="sxs-lookup"><span data-stu-id="2cd07-146">Set delegated permissions</span></span>


## <a name="step-1-create-an-active-directory-native-application"></a><span data-ttu-id="2cd07-147">Paso 1: Crear una aplicación nativa de Active Directory</span><span class="sxs-lookup"><span data-stu-id="2cd07-147">Step 1: Create an Active Directory native application</span></span>

<span data-ttu-id="2cd07-148">Cree y configure una aplicación nativa de Azure AD para la autenticación de usuario final con Azure Data Lake Store mediante Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="2cd07-148">Create and configure an Azure AD native application for end-user authentication with Azure Data Lake Store using Azure Active Directory.</span></span> <span data-ttu-id="2cd07-149">Para obtener instrucciones, vea cómo [crear una aplicación de Azure AD](../azure-resource-manager/resource-group-create-service-principal-portal.md).</span><span class="sxs-lookup"><span data-stu-id="2cd07-149">For instructions, see [Create an Azure AD application](../azure-resource-manager/resource-group-create-service-principal-portal.md).</span></span>

<span data-ttu-id="2cd07-150">Al seguir las instrucciones de hello en hello por encima del vínculo, asegúrese de seleccionar **nativo** para el tipo de aplicación, como se muestra en la siguiente captura de pantalla de Hola.</span><span class="sxs-lookup"><span data-stu-id="2cd07-150">While following hello instructions at hello above link, make sure you select **Native** for application type, as shown in hello screenshot below.</span></span>

<span data-ttu-id="2cd07-151">![Crear aplicación de web](./media/data-lake-store-end-user-authenticate-using-active-directory/azure-active-directory-create-native-app.png "Crear aplicación nativa")</span><span class="sxs-lookup"><span data-stu-id="2cd07-151">![Create web app](./media/data-lake-store-end-user-authenticate-using-active-directory/azure-active-directory-create-native-app.png "Create native app")</span></span>

## <a name="step-2-get-application-id-and-redirect-uri"></a><span data-ttu-id="2cd07-152">Paso 2: Obtener el identificador de aplicación y el URI de redirección</span><span class="sxs-lookup"><span data-stu-id="2cd07-152">Step 2: Get application id and redirect URI</span></span>

<span data-ttu-id="2cd07-153">Vea [obtener identificador de la aplicación hello](../azure-resource-manager/resource-group-create-service-principal-portal.md#get-application-id-and-authentication-key) tooretrieve Hola Id. de aplicación (también denominado identificador de cliente de hello en hello portal de Azure clásico) de la aplicación nativa de hello Azure AD.</span><span class="sxs-lookup"><span data-stu-id="2cd07-153">See [Get hello application ID](../azure-resource-manager/resource-group-create-service-principal-portal.md#get-application-id-and-authentication-key) tooretrieve hello application id (also called hello client ID in hello Azure classic portal) of hello Azure AD native application.</span></span>

<span data-ttu-id="2cd07-154">Hola tooretrieve URI de redireccionamiento, siga estos pasos Hola.</span><span class="sxs-lookup"><span data-stu-id="2cd07-154">tooretrieve hello redirect URI, follow hello steps below.</span></span>

1. <span data-ttu-id="2cd07-155">En hello Portal de Azure, seleccione **Azure Active Directory**, haga clic en **registros de aplicación**y, a continuación, busque y haga clic en la aplicación nativa de hello Azure AD que acaba de crear.</span><span class="sxs-lookup"><span data-stu-id="2cd07-155">From hello Azure Portal, select **Azure Active Directory**, click **App registrations**, and then find and click hello Azure AD native application that you just created.</span></span>

2. <span data-ttu-id="2cd07-156">De hello **configuración** hoja para la aplicación hello, haga clic en **URI de redireccionamiento**.</span><span class="sxs-lookup"><span data-stu-id="2cd07-156">From hello **Settings** blade for hello application, click **Redirect URIs**.</span></span>

    ![Obtener URI de redirección](./media/data-lake-store-end-user-authenticate-using-active-directory/azure-active-directory-redirect-uri.png)

3. <span data-ttu-id="2cd07-158">Copiar valor de hello mostrado.</span><span class="sxs-lookup"><span data-stu-id="2cd07-158">Copy hello value displayed.</span></span>


## <a name="step-3-set-permissions"></a><span data-ttu-id="2cd07-159">Paso 3: Establecer permisos</span><span class="sxs-lookup"><span data-stu-id="2cd07-159">Step 3: Set permissions</span></span>

1. <span data-ttu-id="2cd07-160">En hello Portal de Azure, seleccione **Azure Active Directory**, haga clic en **registros de aplicación**y, a continuación, busque y haga clic en la aplicación nativa de hello Azure AD que acaba de crear.</span><span class="sxs-lookup"><span data-stu-id="2cd07-160">From hello Azure Portal, select **Azure Active Directory**, click **App registrations**, and then find and click hello Azure AD native application that you just created.</span></span>

2. <span data-ttu-id="2cd07-161">De hello **configuración** hoja para la aplicación hello, haga clic en **los permisos necesarios**y, a continuación, haga clic en **agregar**.</span><span class="sxs-lookup"><span data-stu-id="2cd07-161">From hello **Settings** blade for hello application, click **Required permissions**, and then click **Add**.</span></span>

    ![ID. DE CLIENTE](./media/data-lake-store-end-user-authenticate-using-active-directory/aad-end-user-auth-set-permission-1.png)

3. <span data-ttu-id="2cd07-163">Hola **agregar acceso de API** hoja, haga clic en **seleccionar una API**, haga clic en **Azure Data Lake**y, a continuación, haga clic en **seleccione**.</span><span class="sxs-lookup"><span data-stu-id="2cd07-163">In hello **Add API Access** blade, click **Select an API**, click **Azure Data Lake**, and then click **Select**.</span></span>

    ![ID. DE CLIENTE](./media/data-lake-store-end-user-authenticate-using-active-directory/aad-end-user-auth-set-permission-2.png)
 
4.  <span data-ttu-id="2cd07-165">Hola **agregar acceso de API** hoja, haga clic en **seleccione permisos**, seleccione Hola casilla toogive **acceso total tooData Lake almacén**y, a continuación, haga clic en **seleccionar** .</span><span class="sxs-lookup"><span data-stu-id="2cd07-165">In hello **Add API Access** blade, click **Select permissions**, select hello check box toogive **Full access tooData Lake Store**, and then click **Select**.</span></span>

    ![ID. DE CLIENTE](./media/data-lake-store-end-user-authenticate-using-active-directory/aad-end-user-auth-set-permission-3.png)

    <span data-ttu-id="2cd07-167">Haga clic en **Done**(Listo).</span><span class="sxs-lookup"><span data-stu-id="2cd07-167">Click **Done**.</span></span>

5. <span data-ttu-id="2cd07-168">Hola repetición últimos dos pasos permisos toogrant para **API de administración de servicios de Windows Azure** así.</span><span class="sxs-lookup"><span data-stu-id="2cd07-168">Repeat hello last two steps toogrant permissions for **Windows Azure Service Management API** as well.</span></span>
   
## <a name="next-steps"></a><span data-ttu-id="2cd07-169">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="2cd07-169">Next steps</span></span>
<span data-ttu-id="2cd07-170">En este artículo se crea una aplicación nativa de Azure AD y recopila información de Hola que necesita en las aplicaciones cliente que creas mediante .NET SDK, SDK de Java, API de REST, etcetera. Ahora puede continuar toohello siguientes artículos que hable acerca de cómo se autentican con almacén de Data Lake toofirst de aplicación web de toouse hello Azure AD y, a continuación, realizan otras operaciones en el almacén de Hola.</span><span class="sxs-lookup"><span data-stu-id="2cd07-170">In this article you created an Azure AD native application and gathered hello information you need in your client applications that you author using .NET SDK, Java SDK, REST API, etc. You can now proceed toohello following articles that talk about how toouse hello Azure AD web application toofirst authenticate with Data Lake Store and then perform other operations on hello store.</span></span>

* [<span data-ttu-id="2cd07-171">Introducción al Almacén de Azure Data Lake mediante SDK de .NET</span><span class="sxs-lookup"><span data-stu-id="2cd07-171">Get started with Azure Data Lake Store using .NET SDK</span></span>](data-lake-store-get-started-net-sdk.md)
* [<span data-ttu-id="2cd07-172">Introducción a Azure Data Lake Store con el SDK de Java</span><span class="sxs-lookup"><span data-stu-id="2cd07-172">Get started with Azure Data Lake Store using Java SDK</span></span>](data-lake-store-get-started-java-sdk.md)
* [<span data-ttu-id="2cd07-173">Introducción a Azure Data Lake Store mediante la API de REST</span><span class="sxs-lookup"><span data-stu-id="2cd07-173">Get started with Azure Data Lake Store using REST API</span></span>](data-lake-store-get-started-rest-api.md)

