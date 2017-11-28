---
title: "API de generación de informes de aaaPrerequisites tooaccess hello Azure AD. | Microsoft Docs"
description: "Aprender sobre la API de generación de informes de hello requisitos previos tooaccess hello Azure AD"
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
ms.openlocfilehash: e9d7ceaedb07d18fbd75b70d68b5cfbebc756c36
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="prerequisites-tooaccess-hello-azure-ad-reporting-api"></a><span data-ttu-id="2ea08-104">API de generación de informes de requisitos previos tooaccess hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="2ea08-104">Prerequisites tooaccess hello Azure AD reporting API</span></span>
<span data-ttu-id="2ea08-105">Hola [Azure AD reporting API](https://msdn.microsoft.com/library/azure/ad/graph/howto/azure-ad-reports-and-events-preview) proporcionan datos de toohello de acceso mediante programación a través de un conjunto de API basadas en REST.</span><span class="sxs-lookup"><span data-stu-id="2ea08-105">hello [Azure AD reporting APIs](https://msdn.microsoft.com/library/azure/ad/graph/howto/azure-ad-reports-and-events-preview) provide you with programmatic access toohello data through a set of REST-based APIs.</span></span> <span data-ttu-id="2ea08-106">Estas API pueden llamarse desde una variedad de lenguajes de programación y herramientas.</span><span class="sxs-lookup"><span data-stu-id="2ea08-106">You can call these APIs from a variety of programming languages and tools.</span></span>

<span data-ttu-id="2ea08-107">Hola reporting utiliza API [OAuth](https://msdn.microsoft.com/library/azure/dn645545.aspx) toohello web API de tooauthorize acceso.</span><span class="sxs-lookup"><span data-stu-id="2ea08-107">hello reporting API uses [OAuth](https://msdn.microsoft.com/library/azure/dn645545.aspx) tooauthorize access toohello web APIs.</span></span> 

<span data-ttu-id="2ea08-108">tooprepare su toohello acceso a API de informes, debe:</span><span class="sxs-lookup"><span data-stu-id="2ea08-108">tooprepare your access toohello reporting API, you must:</span></span>

1. <span data-ttu-id="2ea08-109">Crear una aplicación en el inquilino de Azure AD</span><span class="sxs-lookup"><span data-stu-id="2ea08-109">Create an application in your Azure AD tenant</span></span> 
2. <span data-ttu-id="2ea08-110">Tooaccess de los permisos adecuados de concesión Hola aplicación Hola datos de Azure AD</span><span class="sxs-lookup"><span data-stu-id="2ea08-110">Grant hello application appropriate permissions tooaccess hello Azure AD data</span></span>
3. <span data-ttu-id="2ea08-111">Recopilar los valores de configuración del directorio</span><span class="sxs-lookup"><span data-stu-id="2ea08-111">Gather configuration settings from your directory</span></span>

<span data-ttu-id="2ea08-112">Para ver preguntas, problemas o comentarios, póngase en contacto con el equipo de [ayuda de informes de AAD](mailto:aadreportinghelp@microsoft.com).</span><span class="sxs-lookup"><span data-stu-id="2ea08-112">For questions, issues or feedback, please contact [AAD Reporting Help](mailto:aadreportinghelp@microsoft.com).</span></span>

## <a name="create-an-azure-ad-application"></a><span data-ttu-id="2ea08-113">Creación de una aplicación de Azure AD</span><span class="sxs-lookup"><span data-stu-id="2ea08-113">Create an Azure AD application</span></span>
<span data-ttu-id="2ea08-114">tooconfigure su API directory tooaccess hello Azure AD informes, debe iniciar sesión en toohello portal de Azure clásico con una cuenta de administrador de suscripción de Azure que también es un miembro del rol de directorio de administrador Global de hello en el inquilino de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="2ea08-114">tooconfigure your directory tooaccess hello Azure AD reporting API, you must sign in toohello Azure classic portal with an Azure subscription administrator account that is also a member of hello Global Administrator directory role in your Azure AD tenant.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="2ea08-115">Aplicaciones que se ejecutan bajo las credenciales con privilegios de "admin" similar al siguiente pueden ser muy eficaces, por lo que Ten credenciales de Id. / secreto de la aplicación de seguro tookeep Hola segura.</span><span class="sxs-lookup"><span data-stu-id="2ea08-115">Applications running under credentials with "admin" privileges like this can be very powerful, so please be sure tookeep hello application's ID/secret credentials secure.</span></span>
> 
> 

1. <span data-ttu-id="2ea08-116">Hola [portal de Azure clásico](https://manage.windowsazure.com), en Hola panel de navegación izquierdo, haga clic en **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="2ea08-116">In hello [Azure classic portal](https://manage.windowsazure.com), on hello left navigation pane, click **Active Directory**.</span></span>
   
    ![Registre la aplicación](./media/active-directory-reporting-api-prerequisites/01.png) 
2. <span data-ttu-id="2ea08-118">De hello **active directory** lista, seleccione el directorio.</span><span class="sxs-lookup"><span data-stu-id="2ea08-118">From hello **active directory** list, select your directory.</span></span>
3. <span data-ttu-id="2ea08-119">En el menú de hello en la parte superior de hello, haga clic en **aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="2ea08-119">In hello menu on hello top, click **Applications**.</span></span>
   
    ![Registre la aplicación](./media/active-directory-reporting-api-prerequisites/02.png) 
4. <span data-ttu-id="2ea08-121">En la barra de la parte inferior de hello, haga clic en **agregar**.</span><span class="sxs-lookup"><span data-stu-id="2ea08-121">On hello bottom bar, click **Add**.</span></span>
   
    ![Registre la aplicación](./media/active-directory-reporting-api-prerequisites/03.png) 
5. <span data-ttu-id="2ea08-123">En hello **especifique qué desea toodo?** cuadro de diálogo, haga clic en **agregar una aplicación que mi organización está desarrollando**.</span><span class="sxs-lookup"><span data-stu-id="2ea08-123">On hello **What do you want toodo?** dialog, click **Add an application my organization is developing**.</span></span> 
   
    ![Registre la aplicación](./media/active-directory-reporting-api-prerequisites/04.png) 
6. <span data-ttu-id="2ea08-125">En hello **envíenos comentarios acerca de la aplicación** cuadro de diálogo, realizar Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="2ea08-125">On hello **Tell us about your application** dialog, perform hello following steps:</span></span> 
   
    ![Registre la aplicación](./media/active-directory-reporting-api-prerequisites/05.png) 
   
    <span data-ttu-id="2ea08-127">a.</span><span class="sxs-lookup"><span data-stu-id="2ea08-127">a.</span></span> <span data-ttu-id="2ea08-128">Hola **nombre** cuadro de texto, escriba un nombre (p. ej.: aplicación de API de informes).</span><span class="sxs-lookup"><span data-stu-id="2ea08-128">In hello **Name** textbox, type a name (e.g.: Reporting API Application).</span></span>
   
    <span data-ttu-id="2ea08-129">b.</span><span class="sxs-lookup"><span data-stu-id="2ea08-129">b.</span></span> <span data-ttu-id="2ea08-130">Seleccione **Aplicación web y/o API web**.</span><span class="sxs-lookup"><span data-stu-id="2ea08-130">Select **Web application and/or web API**.</span></span>
   
    <span data-ttu-id="2ea08-131">c.</span><span class="sxs-lookup"><span data-stu-id="2ea08-131">c.</span></span> <span data-ttu-id="2ea08-132">Haga clic en **Siguiente**.</span><span class="sxs-lookup"><span data-stu-id="2ea08-132">Click **Next**.</span></span>
7. <span data-ttu-id="2ea08-133">En hello **propiedades de la aplicación** cuadro de diálogo, realizar Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="2ea08-133">On hello **App properties** dialog, perform hello following steps:</span></span> 
   
    ![Registre la aplicación](./media/active-directory-reporting-api-prerequisites/06.png) 
   
    <span data-ttu-id="2ea08-135">a.</span><span class="sxs-lookup"><span data-stu-id="2ea08-135">a.</span></span> <span data-ttu-id="2ea08-136">Hola **dirección URL de inicio de sesión** cuadro de texto, tipo `https://localhost`.</span><span class="sxs-lookup"><span data-stu-id="2ea08-136">In hello **Sign-on URL** textbox, type `https://localhost`.</span></span>
   
    <span data-ttu-id="2ea08-137">b.</span><span class="sxs-lookup"><span data-stu-id="2ea08-137">b.</span></span> <span data-ttu-id="2ea08-138">Hola **App ID URI** cuadro de texto, tipo ```https://localhost/ReportingApiApp```.</span><span class="sxs-lookup"><span data-stu-id="2ea08-138">In hello **App ID URI** textbox, type ```https://localhost/ReportingApiApp```.</span></span>
   
    <span data-ttu-id="2ea08-139">c.</span><span class="sxs-lookup"><span data-stu-id="2ea08-139">c.</span></span> <span data-ttu-id="2ea08-140">Haga clic en **Completo**.</span><span class="sxs-lookup"><span data-stu-id="2ea08-140">Click **Complete**.</span></span>

## <a name="grant-your-application-permission-toouse-hello-api"></a><span data-ttu-id="2ea08-141">Conceder su hello toouse de permiso de aplicación API</span><span class="sxs-lookup"><span data-stu-id="2ea08-141">Grant your application permission toouse hello API</span></span>
1. <span data-ttu-id="2ea08-142">Hola [portal de Azure clásico](https://manage.windowsazure.com/), en Hola panel de navegación izquierdo, haga clic en **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="2ea08-142">In hello [Azure classic portal](https://manage.windowsazure.com/), on hello left navigation pane, click **Active Directory**.</span></span>
   
    ![Registre la aplicación](./media/active-directory-reporting-api-prerequisites/01.png) 
2. <span data-ttu-id="2ea08-144">De hello **active directory** lista, seleccione el directorio.</span><span class="sxs-lookup"><span data-stu-id="2ea08-144">From hello **active directory** list, select your directory.</span></span>
3. <span data-ttu-id="2ea08-145">En el menú de hello en la parte superior de hello, haga clic en **aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="2ea08-145">In hello menu on hello top, click **Applications**.</span></span>
   
    ![Registre la aplicación](./media/active-directory-reporting-api-prerequisites/02.png)
4. <span data-ttu-id="2ea08-147">En la lista de aplicaciones de hello, seleccione la aplicación recién creada.</span><span class="sxs-lookup"><span data-stu-id="2ea08-147">In hello applications list, select your newly created application.</span></span>
   
    ![Registre la aplicación](./media/active-directory-reporting-api-prerequisites/07.png)
5. <span data-ttu-id="2ea08-149">En el menú de hello en la parte superior de hello, haga clic en **configurar**.</span><span class="sxs-lookup"><span data-stu-id="2ea08-149">In hello menu on hello top, click **Configure**.</span></span>
   
    ![Registre la aplicación](./media/active-directory-reporting-api-prerequisites/08.png)
6. <span data-ttu-id="2ea08-151">Hola **permisos tooother aplicaciones** sección para hello **Azure Active Directory** recursos, haga clic en hello **permisos de aplicación** la lista desplegable y, a continuación, Seleccione **leer datos de directorio**.</span><span class="sxs-lookup"><span data-stu-id="2ea08-151">In hello **Permissions tooother applications** section, for hello **Azure Active Directory** resource, click hello **Application Permissions** drop-down list, and then select **Read directory data**.</span></span>
   
    ![Registre la aplicación](./media/active-directory-reporting-api-prerequisites/09.png)
7. <span data-ttu-id="2ea08-153">En la barra de la parte inferior de hello, haga clic en **guardar**.</span><span class="sxs-lookup"><span data-stu-id="2ea08-153">On hello bottom bar, click **Save**.</span></span>
   
    ![Registre la aplicación](./media/active-directory-reporting-api-prerequisites/10.png)

## <a name="gather-configuration-settings-from-your-directory"></a><span data-ttu-id="2ea08-155">Recopilar los valores de configuración del directorio</span><span class="sxs-lookup"><span data-stu-id="2ea08-155">Gather configuration settings from your directory</span></span>
<span data-ttu-id="2ea08-156">Esta sección muestra cómo hello tooget siguiendo la configuración de su directorio:</span><span class="sxs-lookup"><span data-stu-id="2ea08-156">This section shows you how tooget hello following settings from your directory:</span></span>

* <span data-ttu-id="2ea08-157">Nombre de dominio</span><span class="sxs-lookup"><span data-stu-id="2ea08-157">Domain name</span></span>
* <span data-ttu-id="2ea08-158">id. de cliente</span><span class="sxs-lookup"><span data-stu-id="2ea08-158">Client ID</span></span>
* <span data-ttu-id="2ea08-159">Secreto del cliente</span><span class="sxs-lookup"><span data-stu-id="2ea08-159">Client secret</span></span>

<span data-ttu-id="2ea08-160">Necesitará estos valores al configurar la API de generación de informes de toohello de llamadas.</span><span class="sxs-lookup"><span data-stu-id="2ea08-160">You need these values when configuring calls toohello reporting API.</span></span> 

### <a name="get-your-domain-name"></a><span data-ttu-id="2ea08-161">Obtención del nombre de dominio</span><span class="sxs-lookup"><span data-stu-id="2ea08-161">Get your domain name</span></span>
1. <span data-ttu-id="2ea08-162">Hola [portal de Azure clásico](https://manage.windowsazure.com), en Hola panel de navegación izquierdo, haga clic en **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="2ea08-162">In hello [Azure classic portal](https://manage.windowsazure.com), on hello left navigation pane, click **Active Directory**.</span></span>
   
    ![Registre la aplicación](./media/active-directory-reporting-api-prerequisites/01.png) 
2. <span data-ttu-id="2ea08-164">De hello **active directory** lista, seleccione el directorio.</span><span class="sxs-lookup"><span data-stu-id="2ea08-164">From hello **active directory** list, select your directory.</span></span>
3. <span data-ttu-id="2ea08-165">En el menú de hello en la parte superior de hello, haga clic en **dominios**.</span><span class="sxs-lookup"><span data-stu-id="2ea08-165">In hello menu on hello top, click **Domains**.</span></span>
   
    ![Registre la aplicación](./media/active-directory-reporting-api-prerequisites/11.png) 
4. <span data-ttu-id="2ea08-167">Hola **nombre de dominio** columna, copie el nombre de dominio.</span><span class="sxs-lookup"><span data-stu-id="2ea08-167">In hello **Domain Name** column, copy your domain name.</span></span>
   
    ![Registre la aplicación](./media/active-directory-reporting-api-prerequisites/12.png) 

### <a name="get-hello-applications-client-id"></a><span data-ttu-id="2ea08-169">Obtener Id. de cliente de la aplicación hello</span><span class="sxs-lookup"><span data-stu-id="2ea08-169">Get hello application's client ID</span></span>
1. <span data-ttu-id="2ea08-170">Hola [portal de Azure clásico](https://manage.windowsazure.com), en Hola panel de navegación izquierdo, haga clic en **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="2ea08-170">In hello [Azure classic portal](https://manage.windowsazure.com), on hello left navigation pane, click **Active Directory**.</span></span>
   
    ![Registre la aplicación](./media/active-directory-reporting-api-prerequisites/01.png) 
2. <span data-ttu-id="2ea08-172">De hello **active directory** lista, seleccione el directorio.</span><span class="sxs-lookup"><span data-stu-id="2ea08-172">From hello **active directory** list, select your directory.</span></span>
3. <span data-ttu-id="2ea08-173">En el menú de hello en la parte superior de hello, haga clic en **aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="2ea08-173">In hello menu on hello top, click **Applications**.</span></span>
   
    ![Registre la aplicación](./media/active-directory-reporting-api-prerequisites/02.png) 
4. <span data-ttu-id="2ea08-175">En la lista de aplicaciones de hello, seleccione la aplicación recién creada.</span><span class="sxs-lookup"><span data-stu-id="2ea08-175">In hello applications list, select your newly created application.</span></span>
   
    ![Registre la aplicación](./media/active-directory-reporting-api-prerequisites/07.png)
5. <span data-ttu-id="2ea08-177">En el menú de hello en la parte superior de hello, haga clic en **configurar**.</span><span class="sxs-lookup"><span data-stu-id="2ea08-177">In hello menu on hello top, click **Configure**.</span></span>
   
    ![Registre la aplicación](./media/active-directory-reporting-api-prerequisites/08.png)
6. <span data-ttu-id="2ea08-179">Copie el **id. de cliente**.</span><span class="sxs-lookup"><span data-stu-id="2ea08-179">Copy your **Client ID**.</span></span>
   
    ![Registre la aplicación](./media/active-directory-reporting-api-prerequisites/13.png)

### <a name="get-hello-applications-client-secret"></a><span data-ttu-id="2ea08-181">Obtener el secreto de cliente de la aplicación hello</span><span class="sxs-lookup"><span data-stu-id="2ea08-181">Get hello application's client secret</span></span>
<span data-ttu-id="2ea08-182">tooget cliente de su aplicación secreta, que necesita toocreate una nueva clave y guardar su valor al guardar la nueva clave de hello porque no es posible tooretrieve este valor más tarde ya.</span><span class="sxs-lookup"><span data-stu-id="2ea08-182">tooget your application's client secret, you need toocreate a new key and save its value upon saving hello new key because it is not possible tooretrieve this value later anymore.</span></span>

1. <span data-ttu-id="2ea08-183">Hola [portal de Azure clásico](https://manage.windowsazure.com), en Hola panel de navegación izquierdo, haga clic en **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="2ea08-183">In hello [Azure classic portal](https://manage.windowsazure.com), on hello left navigation pane, click **Active Directory**.</span></span>
   
    ![Registre la aplicación](./media/active-directory-reporting-api-prerequisites/01.png) 
2. <span data-ttu-id="2ea08-185">De hello **active directory** lista, seleccione el directorio.</span><span class="sxs-lookup"><span data-stu-id="2ea08-185">From hello **active directory** list, select your directory.</span></span>
3. <span data-ttu-id="2ea08-186">En el menú de hello en la parte superior de hello, haga clic en **aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="2ea08-186">In hello menu on hello top, click **Applications**.</span></span>
   
    ![Registre la aplicación](./media/active-directory-reporting-api-prerequisites/02.png) 
4. <span data-ttu-id="2ea08-188">En la lista de aplicaciones de hello, seleccione la aplicación recién creada.</span><span class="sxs-lookup"><span data-stu-id="2ea08-188">In hello applications list, select your newly created application.</span></span>
   
    ![Registre la aplicación](./media/active-directory-reporting-api-prerequisites/07.png)
5. <span data-ttu-id="2ea08-190">En el menú de hello en la parte superior de hello, haga clic en **configurar**.</span><span class="sxs-lookup"><span data-stu-id="2ea08-190">In hello menu on hello top, click **Configure**.</span></span>
   
    ![Registre la aplicación](./media/active-directory-reporting-api-prerequisites/08.png)
6. <span data-ttu-id="2ea08-192">Hola **claves** sección, lleve a cabo Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="2ea08-192">In hello **Keys** section, perform hello following steps:</span></span> 
   
    ![Registre la aplicación](./media/active-directory-reporting-api-prerequisites/14.png)
   
    <span data-ttu-id="2ea08-194">a.</span><span class="sxs-lookup"><span data-stu-id="2ea08-194">a.</span></span> <span data-ttu-id="2ea08-195">En lista de duración de hello, seleccione una duración</span><span class="sxs-lookup"><span data-stu-id="2ea08-195">From hello duration list, select a duration</span></span>
   
    <span data-ttu-id="2ea08-196">b.</span><span class="sxs-lookup"><span data-stu-id="2ea08-196">b.</span></span> <span data-ttu-id="2ea08-197">En la barra de la parte inferior de hello, haga clic en **guardar**.</span><span class="sxs-lookup"><span data-stu-id="2ea08-197">On hello bottom bar, click **Save**.</span></span>
   
    ![Registre la aplicación](./media/active-directory-reporting-api-prerequisites/10.png)
   
    <span data-ttu-id="2ea08-199">c.</span><span class="sxs-lookup"><span data-stu-id="2ea08-199">c.</span></span> <span data-ttu-id="2ea08-200">Copie el valor de clave de Hola.</span><span class="sxs-lookup"><span data-stu-id="2ea08-200">Copy hello key value.</span></span>

## <a name="next-steps"></a><span data-ttu-id="2ea08-201">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="2ea08-201">Next Steps</span></span>
* <span data-ttu-id="2ea08-202">¿Se como tooaccess Hola datos de hello Azure AD API de informes de una manera mediante programación?</span><span class="sxs-lookup"><span data-stu-id="2ea08-202">Would you like tooaccess hello data from hello Azure AD reporting API in a programmatic manner?</span></span> <span data-ttu-id="2ea08-203">Extraer del repositorio [Introducción a Azure Active Directory Reporting API hello](active-directory-reporting-api-getting-started.md).</span><span class="sxs-lookup"><span data-stu-id="2ea08-203">Check out [Getting started with hello Azure Active Directory Reporting API](active-directory-reporting-api-getting-started.md).</span></span>
* <span data-ttu-id="2ea08-204">Si desea que toofind más acerca de los informes de Azure Active Directory, vea hello [Azure Active Directory Reporting guía](active-directory-reporting-guide.md).</span><span class="sxs-lookup"><span data-stu-id="2ea08-204">If you would like toofind out more about Azure Active Directory reporting, see hello [Azure Active Directory Reporting Guide](active-directory-reporting-guide.md).</span></span>  

