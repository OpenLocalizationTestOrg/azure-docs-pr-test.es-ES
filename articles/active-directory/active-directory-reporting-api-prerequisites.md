---
title: "Requisitos previos para acceder a la API de creación de informes de Azure AD | Microsoft Docs"
description: "Conozca los requisitos previos para acceder a la API de generación de informes de Azure AD."
services: active-directory
documentationcenter: 
author: dhanyahk
manager: femila
editor: 
ms.assetid: ada19f69-665c-452a-8452-701029bf4252
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 05/16/2017
ms.author: dhanyahk;markvi
ms.openlocfilehash: 6e409fc56b77f37dac7f37382e664c577666ad4d
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="prerequisites-to-access-the-azure-ad-reporting-api"></a><span data-ttu-id="78fed-104">Requisitos previos para acceder a la API de generación de informes de Azure AD</span><span class="sxs-lookup"><span data-stu-id="78fed-104">Prerequisites to access the Azure AD reporting API</span></span>
<span data-ttu-id="78fed-105">Las [API de generación de informes de Azure AD](https://msdn.microsoft.com/library/azure/ad/graph/howto/azure-ad-reports-and-events-preview) proporcionan acceso mediante programación a los datos a través de un conjunto de API de REST.</span><span class="sxs-lookup"><span data-stu-id="78fed-105">The [Azure AD reporting APIs](https://msdn.microsoft.com/library/azure/ad/graph/howto/azure-ad-reports-and-events-preview) provide you with programmatic access to the data through a set of REST-based APIs.</span></span> <span data-ttu-id="78fed-106">Estas API pueden llamarse desde una variedad de lenguajes de programación y herramientas.</span><span class="sxs-lookup"><span data-stu-id="78fed-106">You can call these APIs from a variety of programming languages and tools.</span></span>

<span data-ttu-id="78fed-107">La API de generación de informes utiliza [OAuth](https://msdn.microsoft.com/library/azure/dn645545.aspx) para autorizar el acceso a las API web.</span><span class="sxs-lookup"><span data-stu-id="78fed-107">The reporting API uses [OAuth](https://msdn.microsoft.com/library/azure/dn645545.aspx) to authorize access to the web APIs.</span></span> 

<span data-ttu-id="78fed-108">Para preparar el acceso a la API de generación de informes, debe hacer lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="78fed-108">To prepare your access to the reporting API, you must:</span></span>

1. <span data-ttu-id="78fed-109">Crear una aplicación en el inquilino de Azure AD</span><span class="sxs-lookup"><span data-stu-id="78fed-109">Create an application in your Azure AD tenant</span></span> 
2. <span data-ttu-id="78fed-110">Conceder los permisos adecuados de aplicación para acceder a los datos de Azure AD</span><span class="sxs-lookup"><span data-stu-id="78fed-110">Grant the application appropriate permissions to access the Azure AD data</span></span>
3. <span data-ttu-id="78fed-111">Recopilar los valores de configuración del directorio</span><span class="sxs-lookup"><span data-stu-id="78fed-111">Gather configuration settings from your directory</span></span>

<span data-ttu-id="78fed-112">Para ver preguntas, problemas o comentarios, póngase en contacto con el equipo de [ayuda de informes de AAD](mailto:aadreportinghelp@microsoft.com).</span><span class="sxs-lookup"><span data-stu-id="78fed-112">For questions, issues or feedback, please contact [AAD Reporting Help](mailto:aadreportinghelp@microsoft.com).</span></span>

## <a name="create-an-azure-ad-application"></a><span data-ttu-id="78fed-113">Creación de una aplicación de Azure AD</span><span class="sxs-lookup"><span data-stu-id="78fed-113">Create an Azure AD application</span></span>
<span data-ttu-id="78fed-114">Si quiere configurar el directorio para que tenga acceso a la API de generación de informes de Azure AD, debe iniciar sesión en el Portal de Azure clásico con una cuenta de administrador de suscripción de Azure que también sea miembro del rol de directorio Administrador global en su inquilino de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="78fed-114">To configure your directory to access the Azure AD reporting API, you must sign in to the Azure classic portal with an Azure subscription administrator account that is also a member of the Global Administrator directory role in your Azure AD tenant.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="78fed-115">Las aplicaciones que se ejecutan con credenciales con privilegios administrativos como este pueden ser muy avanzadas, así que asegúrese de mantener seguras las credenciales del secreto o el identificador de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="78fed-115">Applications running under credentials with "admin" privileges like this can be very powerful, so please be sure to keep the application's ID/secret credentials secure.</span></span>
> 
> 

1. <span data-ttu-id="78fed-116">En el [Portal de Azure clásico](https://manage.windowsazure.com), en el panel de navegación izquierdo, haga clic en **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="78fed-116">In the [Azure classic portal](https://manage.windowsazure.com), on the left navigation pane, click **Active Directory**.</span></span>
   
    ![Registre la aplicación](./media/active-directory-reporting-api-prerequisites/01.png) 
2. <span data-ttu-id="78fed-118">En la lista de **directorios activos** , seleccione el directorio.</span><span class="sxs-lookup"><span data-stu-id="78fed-118">From the **active directory** list, select your directory.</span></span>
3. <span data-ttu-id="78fed-119">En el menú superior, haga clic en **Aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="78fed-119">In the menu on the top, click **Applications**.</span></span>
   
    ![Registre la aplicación](./media/active-directory-reporting-api-prerequisites/02.png) 
4. <span data-ttu-id="78fed-121">En la barra inferior, haga clic en **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="78fed-121">On the bottom bar, click **Add**.</span></span>
   
    ![Registre la aplicación](./media/active-directory-reporting-api-prerequisites/03.png) 
5. <span data-ttu-id="78fed-123">En la página de diálogo **¿Qué desea hacer?**, haga clic en **Agregar una aplicación que mi organización está desarrollando**.</span><span class="sxs-lookup"><span data-stu-id="78fed-123">On the **What do you want to do?** dialog, click **Add an application my organization is developing**.</span></span> 
   
    ![Registre la aplicación](./media/active-directory-reporting-api-prerequisites/04.png) 
6. <span data-ttu-id="78fed-125">En la cuadro de diálogo **Proporcione información sobre este usuario** , realice los pasos siguientes:</span><span class="sxs-lookup"><span data-stu-id="78fed-125">On the **Tell us about your application** dialog, perform the following steps:</span></span> 
   
    ![Registre la aplicación](./media/active-directory-reporting-api-prerequisites/05.png) 
   
    <span data-ttu-id="78fed-127">a.</span><span class="sxs-lookup"><span data-stu-id="78fed-127">a.</span></span> <span data-ttu-id="78fed-128">En el cuadro de texto **Nombre** , escriba un nombre (por ejemplo: aplicación de API de generación de informes).</span><span class="sxs-lookup"><span data-stu-id="78fed-128">In the **Name** textbox, type a name (e.g.: Reporting API Application).</span></span>
   
    <span data-ttu-id="78fed-129">b.</span><span class="sxs-lookup"><span data-stu-id="78fed-129">b.</span></span> <span data-ttu-id="78fed-130">Seleccione **Aplicación web y/o API web**.</span><span class="sxs-lookup"><span data-stu-id="78fed-130">Select **Web application and/or web API**.</span></span>
   
    <span data-ttu-id="78fed-131">c.</span><span class="sxs-lookup"><span data-stu-id="78fed-131">c.</span></span> <span data-ttu-id="78fed-132">Haga clic en **Siguiente**.</span><span class="sxs-lookup"><span data-stu-id="78fed-132">Click **Next**.</span></span>
7. <span data-ttu-id="78fed-133">En el cuadro de diálogo **Agregar propiedades** , realice los pasos siguientes:</span><span class="sxs-lookup"><span data-stu-id="78fed-133">On the **App properties** dialog, perform the following steps:</span></span> 
   
    ![Registre la aplicación](./media/active-directory-reporting-api-prerequisites/06.png) 
   
    <span data-ttu-id="78fed-135">a.</span><span class="sxs-lookup"><span data-stu-id="78fed-135">a.</span></span> <span data-ttu-id="78fed-136">En el cuadro de texto **URL de inicio de sesión**, escriba `https://localhost`.</span><span class="sxs-lookup"><span data-stu-id="78fed-136">In the **Sign-on URL** textbox, type `https://localhost`.</span></span>
   
    <span data-ttu-id="78fed-137">b.</span><span class="sxs-lookup"><span data-stu-id="78fed-137">b.</span></span> <span data-ttu-id="78fed-138">En el cuadro de texto **URI de id. de aplicación**, escriba ```https://localhost/ReportingApiApp```.</span><span class="sxs-lookup"><span data-stu-id="78fed-138">In the **App ID URI** textbox, type ```https://localhost/ReportingApiApp```.</span></span>
   
    <span data-ttu-id="78fed-139">c.</span><span class="sxs-lookup"><span data-stu-id="78fed-139">c.</span></span> <span data-ttu-id="78fed-140">Haga clic en **Complete**.</span><span class="sxs-lookup"><span data-stu-id="78fed-140">Click **Complete**.</span></span>

## <a name="grant-your-application-permission-to-use-the-api"></a><span data-ttu-id="78fed-141">Conceder a la aplicación permiso para usar la API</span><span class="sxs-lookup"><span data-stu-id="78fed-141">Grant your application permission to use the API</span></span>
1. <span data-ttu-id="78fed-142">En el [Portal de Azure clásico](https://manage.windowsazure.com/), en el panel de navegación izquierdo, haga clic en **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="78fed-142">In the [Azure classic portal](https://manage.windowsazure.com/), on the left navigation pane, click **Active Directory**.</span></span>
   
    ![Registre la aplicación](./media/active-directory-reporting-api-prerequisites/01.png) 
2. <span data-ttu-id="78fed-144">En la lista de **directorios activos** , seleccione el directorio.</span><span class="sxs-lookup"><span data-stu-id="78fed-144">From the **active directory** list, select your directory.</span></span>
3. <span data-ttu-id="78fed-145">En el menú superior, haga clic en **Aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="78fed-145">In the menu on the top, click **Applications**.</span></span>
   
    ![Registre la aplicación](./media/active-directory-reporting-api-prerequisites/02.png)
4. <span data-ttu-id="78fed-147">En la lista de aplicaciones, seleccione la aplicación que acaba de crear.</span><span class="sxs-lookup"><span data-stu-id="78fed-147">In the applications list, select your newly created application.</span></span>
   
    ![Registre la aplicación](./media/active-directory-reporting-api-prerequisites/07.png)
5. <span data-ttu-id="78fed-149">En el menú de la parte superior, haga clic en **Configurar**.</span><span class="sxs-lookup"><span data-stu-id="78fed-149">In the menu on the top, click **Configure**.</span></span>
   
    ![Registre la aplicación](./media/active-directory-reporting-api-prerequisites/08.png)
6. <span data-ttu-id="78fed-151">En la sección **Permisos para otras aplicaciones**, en el recurso **Azure Active Directory**, haga clic en la lista desplegable **Permisos de la aplicación** y seleccione **Leer datos de directorio**.</span><span class="sxs-lookup"><span data-stu-id="78fed-151">In the **Permissions to other applications** section, for the **Azure Active Directory** resource, click the **Application Permissions** drop-down list, and then select **Read directory data**.</span></span>
   
    ![Registre la aplicación](./media/active-directory-reporting-api-prerequisites/09.png)
7. <span data-ttu-id="78fed-153">En la barra inferior, haga clic en **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="78fed-153">On the bottom bar, click **Save**.</span></span>
   
    ![Registre la aplicación](./media/active-directory-reporting-api-prerequisites/10.png)

## <a name="gather-configuration-settings-from-your-directory"></a><span data-ttu-id="78fed-155">Recopilar los valores de configuración del directorio</span><span class="sxs-lookup"><span data-stu-id="78fed-155">Gather configuration settings from your directory</span></span>
<span data-ttu-id="78fed-156">En esta sección se muestra cómo obtener la siguiente configuración del directorio:</span><span class="sxs-lookup"><span data-stu-id="78fed-156">This section shows you how to get the following settings from your directory:</span></span>

* <span data-ttu-id="78fed-157">Nombre de dominio</span><span class="sxs-lookup"><span data-stu-id="78fed-157">Domain name</span></span>
* <span data-ttu-id="78fed-158">id. de cliente</span><span class="sxs-lookup"><span data-stu-id="78fed-158">Client ID</span></span>
* <span data-ttu-id="78fed-159">Secreto del cliente</span><span class="sxs-lookup"><span data-stu-id="78fed-159">Client secret</span></span>

<span data-ttu-id="78fed-160">Necesitará estos valores al configurar llamadas a la API de generación de informes.</span><span class="sxs-lookup"><span data-stu-id="78fed-160">You need these values when configuring calls to the reporting API.</span></span> 

### <a name="get-your-domain-name"></a><span data-ttu-id="78fed-161">Obtención del nombre de dominio</span><span class="sxs-lookup"><span data-stu-id="78fed-161">Get your domain name</span></span>
1. <span data-ttu-id="78fed-162">En el [Portal de Azure clásico](https://manage.windowsazure.com), en el panel de navegación izquierdo, haga clic en **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="78fed-162">In the [Azure classic portal](https://manage.windowsazure.com), on the left navigation pane, click **Active Directory**.</span></span>
   
    ![Registre la aplicación](./media/active-directory-reporting-api-prerequisites/01.png) 
2. <span data-ttu-id="78fed-164">En la lista de **directorios activos** , seleccione el directorio.</span><span class="sxs-lookup"><span data-stu-id="78fed-164">From the **active directory** list, select your directory.</span></span>
3. <span data-ttu-id="78fed-165">En el menú de la parte superior, haga clic en **Dominios**.</span><span class="sxs-lookup"><span data-stu-id="78fed-165">In the menu on the top, click **Domains**.</span></span>
   
    ![Registre la aplicación](./media/active-directory-reporting-api-prerequisites/11.png) 
4. <span data-ttu-id="78fed-167">Escriba el nombre del dominio en el campo **Nombre de dominio** .</span><span class="sxs-lookup"><span data-stu-id="78fed-167">In the **Domain Name** column, copy your domain name.</span></span>
   
    ![Registre la aplicación](./media/active-directory-reporting-api-prerequisites/12.png) 

### <a name="get-the-applications-client-id"></a><span data-ttu-id="78fed-169">Obtención del id. de cliente de la aplicación</span><span class="sxs-lookup"><span data-stu-id="78fed-169">Get the application's client ID</span></span>
1. <span data-ttu-id="78fed-170">En el [Portal de Azure clásico](https://manage.windowsazure.com), en el panel de navegación izquierdo, haga clic en **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="78fed-170">In the [Azure classic portal](https://manage.windowsazure.com), on the left navigation pane, click **Active Directory**.</span></span>
   
    ![Registre la aplicación](./media/active-directory-reporting-api-prerequisites/01.png) 
2. <span data-ttu-id="78fed-172">En la lista de **directorios activos** , seleccione el directorio.</span><span class="sxs-lookup"><span data-stu-id="78fed-172">From the **active directory** list, select your directory.</span></span>
3. <span data-ttu-id="78fed-173">En el menú superior, haga clic en **Aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="78fed-173">In the menu on the top, click **Applications**.</span></span>
   
    ![Registre la aplicación](./media/active-directory-reporting-api-prerequisites/02.png) 
4. <span data-ttu-id="78fed-175">En la lista de aplicaciones, seleccione la aplicación que acaba de crear.</span><span class="sxs-lookup"><span data-stu-id="78fed-175">In the applications list, select your newly created application.</span></span>
   
    ![Registre la aplicación](./media/active-directory-reporting-api-prerequisites/07.png)
5. <span data-ttu-id="78fed-177">En el menú de la parte superior, haga clic en **Configurar**.</span><span class="sxs-lookup"><span data-stu-id="78fed-177">In the menu on the top, click **Configure**.</span></span>
   
    ![Registre la aplicación](./media/active-directory-reporting-api-prerequisites/08.png)
6. <span data-ttu-id="78fed-179">Copie el **id. de cliente**.</span><span class="sxs-lookup"><span data-stu-id="78fed-179">Copy your **Client ID**.</span></span>
   
    ![Registre la aplicación](./media/active-directory-reporting-api-prerequisites/13.png)

### <a name="get-the-applications-client-secret"></a><span data-ttu-id="78fed-181">Obtención del secreto de cliente de la aplicación</span><span class="sxs-lookup"><span data-stu-id="78fed-181">Get the application's client secret</span></span>
<span data-ttu-id="78fed-182">Para obtener el secreto de cliente de la aplicación, debe crear una nueva clave y guardar su valor después, ya que no es posible recuperarla más tarde.</span><span class="sxs-lookup"><span data-stu-id="78fed-182">To get your application's client secret, you need to create a new key and save its value upon saving the new key because it is not possible to retrieve this value later anymore.</span></span>

1. <span data-ttu-id="78fed-183">En el [Portal de Azure clásico](https://manage.windowsazure.com), en el panel de navegación izquierdo, haga clic en **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="78fed-183">In the [Azure classic portal](https://manage.windowsazure.com), on the left navigation pane, click **Active Directory**.</span></span>
   
    ![Registre la aplicación](./media/active-directory-reporting-api-prerequisites/01.png) 
2. <span data-ttu-id="78fed-185">En la lista de **directorios activos** , seleccione el directorio.</span><span class="sxs-lookup"><span data-stu-id="78fed-185">From the **active directory** list, select your directory.</span></span>
3. <span data-ttu-id="78fed-186">En el menú superior, haga clic en **Aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="78fed-186">In the menu on the top, click **Applications**.</span></span>
   
    ![Registre la aplicación](./media/active-directory-reporting-api-prerequisites/02.png) 
4. <span data-ttu-id="78fed-188">En la lista de aplicaciones, seleccione la aplicación que acaba de crear.</span><span class="sxs-lookup"><span data-stu-id="78fed-188">In the applications list, select your newly created application.</span></span>
   
    ![Registre la aplicación](./media/active-directory-reporting-api-prerequisites/07.png)
5. <span data-ttu-id="78fed-190">En el menú de la parte superior, haga clic en **Configurar**.</span><span class="sxs-lookup"><span data-stu-id="78fed-190">In the menu on the top, click **Configure**.</span></span>
   
    ![Registre la aplicación](./media/active-directory-reporting-api-prerequisites/08.png)
6. <span data-ttu-id="78fed-192">En la sección **Claves** , realice los siguientes pasos:</span><span class="sxs-lookup"><span data-stu-id="78fed-192">In the **Keys** section, perform the following steps:</span></span> 
   
    ![Registre la aplicación](./media/active-directory-reporting-api-prerequisites/14.png)
   
    <span data-ttu-id="78fed-194">a.</span><span class="sxs-lookup"><span data-stu-id="78fed-194">a.</span></span> <span data-ttu-id="78fed-195">En la lista de duración, seleccione una duración.</span><span class="sxs-lookup"><span data-stu-id="78fed-195">From the duration list, select a duration</span></span>
   
    <span data-ttu-id="78fed-196">b.</span><span class="sxs-lookup"><span data-stu-id="78fed-196">b.</span></span> <span data-ttu-id="78fed-197">En la barra inferior, haga clic en **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="78fed-197">On the bottom bar, click **Save**.</span></span>
   
    ![Registre la aplicación](./media/active-directory-reporting-api-prerequisites/10.png)
   
    <span data-ttu-id="78fed-199">c.</span><span class="sxs-lookup"><span data-stu-id="78fed-199">c.</span></span> <span data-ttu-id="78fed-200">Copie el valor de la clave.</span><span class="sxs-lookup"><span data-stu-id="78fed-200">Copy the key value.</span></span>

## <a name="next-steps"></a><span data-ttu-id="78fed-201">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="78fed-201">Next Steps</span></span>
* <span data-ttu-id="78fed-202">¿Quiere obtener acceso mediante programación a los datos de la API de generación de informes de Azure AD?</span><span class="sxs-lookup"><span data-stu-id="78fed-202">Would you like to access the data from the Azure AD reporting API in a programmatic manner?</span></span> <span data-ttu-id="78fed-203">Consulte [Introducción a la API de informes de Azure Active Directory](active-directory-reporting-api-getting-started.md).</span><span class="sxs-lookup"><span data-stu-id="78fed-203">Check out [Getting started with the Azure Active Directory Reporting API](active-directory-reporting-api-getting-started.md).</span></span>
* <span data-ttu-id="78fed-204">Si quiere obtener más información sobre informes de Azure Active Directory, consulte la [guía de generación de informes de Azure Active Directory](active-directory-reporting-guide.md).</span><span class="sxs-lookup"><span data-stu-id="78fed-204">If you would like to find out more about Azure Active Directory reporting, see the [Azure Active Directory Reporting Guide](active-directory-reporting-guide.md).</span></span>  

