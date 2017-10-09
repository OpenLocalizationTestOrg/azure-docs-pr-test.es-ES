---
title: "API de generación de informes de aaaPrerequisites tooaccess hello Azure AD | Documentos de Microsoft"
description: "Aprender sobre la API de generación de informes de hello requisitos previos tooaccess hello Azure AD"
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
editor: 
ms.assetid: ada19f69-665c-452a-8452-701029bf4252
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/15/2017
ms.author: dhanyahk;markvi
ms.reviewer: dhanyahk
ms.openlocfilehash: ec28a7530f341dda31268a978754b615c727d66f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="prerequisites-tooaccess-hello-azure-ad-reporting-api"></a><span data-ttu-id="b72c9-103">API de generación de informes de requisitos previos tooaccess hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="b72c9-103">Prerequisites tooaccess hello Azure AD reporting API</span></span>

<span data-ttu-id="b72c9-104">Hola [Azure AD reporting API](https://msdn.microsoft.com/library/azure/ad/graph/howto/azure-ad-reports-and-events-preview) proporcionan datos de toohello de acceso mediante programación a través de un conjunto de API basadas en REST.</span><span class="sxs-lookup"><span data-stu-id="b72c9-104">hello [Azure AD reporting APIs](https://msdn.microsoft.com/library/azure/ad/graph/howto/azure-ad-reports-and-events-preview) provide you with programmatic access toohello data through a set of REST-based APIs.</span></span> <span data-ttu-id="b72c9-105">Estas API pueden llamarse desde una variedad de lenguajes de programación y herramientas.</span><span class="sxs-lookup"><span data-stu-id="b72c9-105">You can call these APIs from a variety of programming languages and tools.</span></span>

<span data-ttu-id="b72c9-106">Hola reporting utiliza API [OAuth](https://msdn.microsoft.com/library/azure/dn645545.aspx) toohello web API de tooauthorize acceso.</span><span class="sxs-lookup"><span data-stu-id="b72c9-106">hello reporting API uses [OAuth](https://msdn.microsoft.com/library/azure/dn645545.aspx) tooauthorize access toohello web APIs.</span></span> 

<span data-ttu-id="b72c9-107">tooget tener acceso a los datos de informes de toohello a través de API de hello, deberá toohave uno Hola siguiendo los roles asignados:</span><span class="sxs-lookup"><span data-stu-id="b72c9-107">tooget access toohello reporting data through hello API, you need toohave one of hello following roles assigned:</span></span>

- <span data-ttu-id="b72c9-108">Lector de seguridad</span><span class="sxs-lookup"><span data-stu-id="b72c9-108">Security Reader</span></span>
- <span data-ttu-id="b72c9-109">Administrador de seguridad</span><span class="sxs-lookup"><span data-stu-id="b72c9-109">Security Admin</span></span>
- <span data-ttu-id="b72c9-110">Administrador global</span><span class="sxs-lookup"><span data-stu-id="b72c9-110">Global Admin</span></span>


<span data-ttu-id="b72c9-111">tooprepare su toohello acceso a API de informes, debe:</span><span class="sxs-lookup"><span data-stu-id="b72c9-111">tooprepare your access toohello reporting API, you must:</span></span>

1. <span data-ttu-id="b72c9-112">Registro de una aplicación</span><span class="sxs-lookup"><span data-stu-id="b72c9-112">Register an application</span></span> 
2. <span data-ttu-id="b72c9-113">Concesión de permisos</span><span class="sxs-lookup"><span data-stu-id="b72c9-113">Grant permissions</span></span> 
3. <span data-ttu-id="b72c9-114">Recopilación de configuraciones</span><span class="sxs-lookup"><span data-stu-id="b72c9-114">Gather configuration settings</span></span> 

<span data-ttu-id="b72c9-115">Si tiene preguntas, problemas o comentarios, [abra una incidencia de soporte técnico](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-troubleshooting-support-howto).</span><span class="sxs-lookup"><span data-stu-id="b72c9-115">For questions, issues or feedback, please [file a support ticket](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-troubleshooting-support-howto).</span></span>

## <a name="register-an-azure-active-directory-application"></a><span data-ttu-id="b72c9-116">Registro de una aplicación de Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="b72c9-116">Register an Azure Active Directory application</span></span>

<span data-ttu-id="b72c9-117">Debe tooregister una aplicación incluso si tiene acceso hello mediante un script de API de informes.</span><span class="sxs-lookup"><span data-stu-id="b72c9-117">You need tooregister an app even if you are accessing hello reporting API using a script.</span></span> <span data-ttu-id="b72c9-118">Esto le ofrece un **Id. de aplicación**, lo cual es necesario para una llamada de autorización y permite los tokens de tooreceive de código.</span><span class="sxs-lookup"><span data-stu-id="b72c9-118">This gives you an **Application ID**, which is required for an authorization call and it enables your code tooreceive tokens.</span></span>

<span data-ttu-id="b72c9-119">tooconfigure su API directory tooaccess hello Azure AD informes, debe iniciar sesión en toohello portal de Azure con una cuenta de administrador de Azure que también es un miembro de hello **administrador Global** rol del directorio en el inquilino de Azure AD .</span><span class="sxs-lookup"><span data-stu-id="b72c9-119">tooconfigure your directory tooaccess hello Azure AD reporting API, you must sign in toohello Azure portal with an Azure administrator account that is also a member of hello **Global Administrator** directory role in your Azure AD tenant.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="b72c9-120">Aplicaciones que se ejecutan bajo las credenciales con privilegios de "admin" similar al siguiente pueden ser muy eficaces, por lo que Ten credenciales de Id. / secreto de la aplicación de seguro tookeep Hola segura.</span><span class="sxs-lookup"><span data-stu-id="b72c9-120">Applications running under credentials with "admin" privileges like this can be very powerful, so please be sure tookeep hello application's ID/secret credentials secure.</span></span>
> 


<span data-ttu-id="b72c9-121">**tooregister una aplicación de Azure Active Directory:**</span><span class="sxs-lookup"><span data-stu-id="b72c9-121">**tooregister an Azure Active Directory application:**</span></span>

1. <span data-ttu-id="b72c9-122">Hola [portal de Azure](https://portal.azure.com), en Hola panel de navegación izquierdo, haga clic en **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="b72c9-122">In hello [Azure portal](https://portal.azure.com), on hello left navigation pane, click **Active Directory**.</span></span>
   
    ![Registre la aplicación](./media/active-directory-reporting-api-prerequisites-azure-portal/01.png) 

2. <span data-ttu-id="b72c9-124">En hello **Azure Active Directory** hoja, haga clic en **registros de aplicación**.</span><span class="sxs-lookup"><span data-stu-id="b72c9-124">On hello **Azure Active Directory** blade, click **App registrations**.</span></span>

    ![Registre la aplicación](./media/active-directory-reporting-api-prerequisites-azure-portal/02.png) 

3. <span data-ttu-id="b72c9-126">En hello **registros de aplicaciones** hoja, en la barra de herramientas de hello en la parte superior de hello, haga clic en **nuevo registro de aplicación**.</span><span class="sxs-lookup"><span data-stu-id="b72c9-126">On hello **App registrations** blade, in hello toolbar on hello top, click **New application registration**.</span></span>

    ![Registre la aplicación](./media/active-directory-reporting-api-prerequisites-azure-portal/03.png)

4. <span data-ttu-id="b72c9-128">En hello **crear** hoja, realizar Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="b72c9-128">On hello **Create** blade, perform hello following steps:</span></span>

    ![Registre la aplicación](./media/active-directory-reporting-api-prerequisites-azure-portal/04.png)

    <span data-ttu-id="b72c9-130">a.</span><span class="sxs-lookup"><span data-stu-id="b72c9-130">a.</span></span> <span data-ttu-id="b72c9-131">Hola **nombre** cuadro de texto, tipo `Reporting API application`.</span><span class="sxs-lookup"><span data-stu-id="b72c9-131">In hello **Name** textbox, type `Reporting API application`.</span></span>

    <span data-ttu-id="b72c9-132">b.</span><span class="sxs-lookup"><span data-stu-id="b72c9-132">b.</span></span> <span data-ttu-id="b72c9-133">Seleccione **Aplicación web o API** como **Tipo de aplicación**.</span><span class="sxs-lookup"><span data-stu-id="b72c9-133">As **Application type**, select **Web app / API**.</span></span>

    <span data-ttu-id="b72c9-134">c.</span><span class="sxs-lookup"><span data-stu-id="b72c9-134">c.</span></span> <span data-ttu-id="b72c9-135">Hola **dirección URL de inicio de sesión** cuadro de texto, tipo `https://localhost`.</span><span class="sxs-lookup"><span data-stu-id="b72c9-135">In hello **Sign-on URL** textbox, type `https://localhost`.</span></span>

    <span data-ttu-id="b72c9-136">d.</span><span class="sxs-lookup"><span data-stu-id="b72c9-136">d.</span></span> <span data-ttu-id="b72c9-137">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="b72c9-137">Click **Create**.</span></span> 


## <a name="grant-permissions"></a><span data-ttu-id="b72c9-138">Concesión de permisos</span><span class="sxs-lookup"><span data-stu-id="b72c9-138">Grant permissions</span></span> 

<span data-ttu-id="b72c9-139">objetivo de Hola de este paso es la aplicación de toogrant **leer datos de directorio** permisos toohello **Windows Azure Active Directory** API.</span><span class="sxs-lookup"><span data-stu-id="b72c9-139">hello objective of this step is toogrant your application **Read directory data** permissions toohello **Windows Azure Active Directory** API.</span></span>

![Registre la aplicación](./media/active-directory-reporting-api-prerequisites-azure-portal/16.png)
 

<span data-ttu-id="b72c9-141">**toogrant su hello toouse de permiso de aplicación API:**</span><span class="sxs-lookup"><span data-stu-id="b72c9-141">**toogrant your application permission toouse hello API:**</span></span>

1. <span data-ttu-id="b72c9-142">En hello **registros de aplicaciones** hoja, en la lista de aplicaciones de hello, haga clic en **aplicación de API de Reporting**.</span><span class="sxs-lookup"><span data-stu-id="b72c9-142">On hello **App registrations** blade, in hello apps list, click **Reporting API application**.</span></span>

2. <span data-ttu-id="b72c9-143">En hello **aplicación de API de Reporting** hoja, en la barra de herramientas de hello en la parte superior de hello, haga clic en **configuración**.</span><span class="sxs-lookup"><span data-stu-id="b72c9-143">On hello **Reporting API application** blade, in hello toolbar on hello top, click **Settings**.</span></span> 

    ![Registre la aplicación](./media/active-directory-reporting-api-prerequisites-azure-portal/05.png)

3. <span data-ttu-id="b72c9-145">En hello **configuración** hoja, haga clic en **los permisos necesarios**.</span><span class="sxs-lookup"><span data-stu-id="b72c9-145">On hello **Settings** blade, click **Required permissions**.</span></span> 

    ![Registre la aplicación](./media/active-directory-reporting-api-prerequisites-azure-portal/06.png)

4. <span data-ttu-id="b72c9-147">En hello **los permisos necesarios** hoja en hello **API** lista, haga clic en **Windows Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="b72c9-147">On hello **Required permissions** blade, in hello **API** list, click **Windows Azure Active Directory**.</span></span> 

    ![Registre la aplicación](./media/active-directory-reporting-api-prerequisites-azure-portal/07.png)

5. <span data-ttu-id="b72c9-149">En hello **habilitar acceso** hoja, seleccione **leer datos de directorio**.</span><span class="sxs-lookup"><span data-stu-id="b72c9-149">On hello **Enable Access** blade, select **Read directory data**.</span></span> 

    ![Registre la aplicación](./media/active-directory-reporting-api-prerequisites-azure-portal/08.png)

6. <span data-ttu-id="b72c9-151">En la barra de herramientas de hello en la parte superior de hello, haga clic en **guardar**.</span><span class="sxs-lookup"><span data-stu-id="b72c9-151">In hello toolbar on hello top, click **Save**.</span></span>

    ![Registre la aplicación](./media/active-directory-reporting-api-prerequisites-azure-portal/15.png)

## <a name="gather-configuration-settings"></a><span data-ttu-id="b72c9-153">Recopilación de configuraciones</span><span class="sxs-lookup"><span data-stu-id="b72c9-153">Gather configuration settings</span></span> 
<span data-ttu-id="b72c9-154">Esta sección muestra cómo hello tooget siguiendo la configuración de su directorio:</span><span class="sxs-lookup"><span data-stu-id="b72c9-154">This section shows you how tooget hello following settings from your directory:</span></span>

* <span data-ttu-id="b72c9-155">Nombre de dominio</span><span class="sxs-lookup"><span data-stu-id="b72c9-155">Domain name</span></span>
* <span data-ttu-id="b72c9-156">id. de cliente</span><span class="sxs-lookup"><span data-stu-id="b72c9-156">Client ID</span></span>
* <span data-ttu-id="b72c9-157">Secreto del cliente</span><span class="sxs-lookup"><span data-stu-id="b72c9-157">Client secret</span></span>

<span data-ttu-id="b72c9-158">Necesitará estos valores al configurar la API de generación de informes de toohello de llamadas.</span><span class="sxs-lookup"><span data-stu-id="b72c9-158">You need these values when configuring calls toohello reporting API.</span></span> 

### <a name="get-your-domain-name"></a><span data-ttu-id="b72c9-159">Obtención del nombre de dominio</span><span class="sxs-lookup"><span data-stu-id="b72c9-159">Get your domain name</span></span>

<span data-ttu-id="b72c9-160">**tooget el nombre de dominio:**</span><span class="sxs-lookup"><span data-stu-id="b72c9-160">**tooget your domain name:**</span></span>

1. <span data-ttu-id="b72c9-161">Hola [portal de Azure](https://portal.azure.com), en Hola panel de navegación izquierdo, haga clic en **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="b72c9-161">In hello [Azure portal](https://portal.azure.com), on hello left navigation pane, click **Active Directory**.</span></span>
   
    ![Registre la aplicación](./media/active-directory-reporting-api-prerequisites-azure-portal/01.png) 

2. <span data-ttu-id="b72c9-163">En hello **Azure Active Directory** hoja, haga clic en **nombres de dominio**.</span><span class="sxs-lookup"><span data-stu-id="b72c9-163">On hello **Azure Active Directory** blade, click **Domain names**.</span></span>

    ![Registre la aplicación](./media/active-directory-reporting-api-prerequisites-azure-portal/09.png) 

3. <span data-ttu-id="b72c9-165">Copie el nombre de dominio de lista de Hola de dominios.</span><span class="sxs-lookup"><span data-stu-id="b72c9-165">Copy your domain name from hello list of domains.</span></span>


### <a name="get-your-applications-client-id"></a><span data-ttu-id="b72c9-166">Obtención del id. de cliente de la aplicación</span><span class="sxs-lookup"><span data-stu-id="b72c9-166">Get your application's client ID</span></span>

<span data-ttu-id="b72c9-167">**tooget Id. de cliente de la aplicación:**</span><span class="sxs-lookup"><span data-stu-id="b72c9-167">**tooget your application's client ID:**</span></span>

1. <span data-ttu-id="b72c9-168">Hola [portal de Azure](https://portal.azure.com), en Hola panel de navegación izquierdo, haga clic en **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="b72c9-168">In hello [Azure portal](https://portal.azure.com), on hello left navigation pane, click **Active Directory**.</span></span>
   
    ![Registre la aplicación](./media/active-directory-reporting-api-prerequisites-azure-portal/01.png) 

2. <span data-ttu-id="b72c9-170">En hello **registros de aplicaciones** hoja, en la lista de aplicaciones de hello, haga clic en **aplicación de API de Reporting**.</span><span class="sxs-lookup"><span data-stu-id="b72c9-170">On hello **App registrations** blade, in hello apps list, click **Reporting API application**.</span></span>

3. <span data-ttu-id="b72c9-171">En hello **aplicación de API de Reporting** hoja en hello **Id. de aplicación**, haga clic en **haga clic en toocopy**.</span><span class="sxs-lookup"><span data-stu-id="b72c9-171">On hello **Reporting API application** blade, at hello **Application ID**, click **Click toocopy**.</span></span>

    ![Registre la aplicación](./media/active-directory-reporting-api-prerequisites-azure-portal/11.png) 



### <a name="get-your-applications-client-secret"></a><span data-ttu-id="b72c9-173">Obtención del secreto de cliente de la aplicación</span><span class="sxs-lookup"><span data-stu-id="b72c9-173">Get your application's client secret</span></span>
<span data-ttu-id="b72c9-174">tooget cliente de su aplicación secreta, que necesita toocreate una nueva clave y guardar su valor al guardar la nueva clave de hello porque no es posible tooretrieve este valor más tarde ya.</span><span class="sxs-lookup"><span data-stu-id="b72c9-174">tooget your application's client secret, you need toocreate a new key and save its value upon saving hello new key because it is not possible tooretrieve this value later anymore.</span></span>

<span data-ttu-id="b72c9-175">**tooget secreto del cliente de su aplicación:**</span><span class="sxs-lookup"><span data-stu-id="b72c9-175">**tooget your application's client secret:**</span></span>

1. <span data-ttu-id="b72c9-176">Hola [portal de Azure](https://portal.azure.com), en Hola panel de navegación izquierdo, haga clic en **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="b72c9-176">In hello [Azure portal](https://portal.azure.com), on hello left navigation pane, click **Active Directory**.</span></span>
   
    ![Registre la aplicación](./media/active-directory-reporting-api-prerequisites-azure-portal/01.png) 

2. <span data-ttu-id="b72c9-178">En hello **registros de aplicaciones** hoja, en la lista de aplicaciones de hello, haga clic en **aplicación de API de Reporting**.</span><span class="sxs-lookup"><span data-stu-id="b72c9-178">On hello **App registrations** blade, in hello apps list, click **Reporting API application**.</span></span>


3. <span data-ttu-id="b72c9-179">En hello **aplicación de API de Reporting** hoja, en la barra de herramientas de hello en la parte superior de hello, haga clic en **configuración**.</span><span class="sxs-lookup"><span data-stu-id="b72c9-179">On hello **Reporting API application** blade, in hello toolbar on hello top, click **Settings**.</span></span> 

    ![Registre la aplicación](./media/active-directory-reporting-api-prerequisites-azure-portal/05.png)

4. <span data-ttu-id="b72c9-181">En hello **configuración** hoja en hello **APIR acceso** sección, haga clic en **claves**.</span><span class="sxs-lookup"><span data-stu-id="b72c9-181">On hello **Settings** blade, in hello **APIR Access** section, click **Keys**.</span></span> 

    ![Registre la aplicación](./media/active-directory-reporting-api-prerequisites-azure-portal/12.png)


5. <span data-ttu-id="b72c9-183">En hello **claves** hoja, realizar Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="b72c9-183">On hello **Keys** blade, perform hello following steps:</span></span>

    ![Registre la aplicación](./media/active-directory-reporting-api-prerequisites-azure-portal/14.png)

    <span data-ttu-id="b72c9-185">a.</span><span class="sxs-lookup"><span data-stu-id="b72c9-185">a.</span></span> <span data-ttu-id="b72c9-186">Hola **descripción** cuadro de texto, tipo `Reporting API`.</span><span class="sxs-lookup"><span data-stu-id="b72c9-186">In hello **Description** textbox, type `Reporting API`.</span></span>

    <span data-ttu-id="b72c9-187">b.</span><span class="sxs-lookup"><span data-stu-id="b72c9-187">b.</span></span> <span data-ttu-id="b72c9-188">En **Expiración**, seleccione **En 2 años**.</span><span class="sxs-lookup"><span data-stu-id="b72c9-188">As **Expires**, select **In 2 years**.</span></span>

    <span data-ttu-id="b72c9-189">c.</span><span class="sxs-lookup"><span data-stu-id="b72c9-189">c.</span></span> <span data-ttu-id="b72c9-190">Haga clic en **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="b72c9-190">Click **Save**.</span></span>

    <span data-ttu-id="b72c9-191">d.</span><span class="sxs-lookup"><span data-stu-id="b72c9-191">d.</span></span> <span data-ttu-id="b72c9-192">Copie el valor de clave de Hola.</span><span class="sxs-lookup"><span data-stu-id="b72c9-192">Copy hello key value.</span></span>


## <a name="next-steps"></a><span data-ttu-id="b72c9-193">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="b72c9-193">Next Steps</span></span>
* <span data-ttu-id="b72c9-194">¿Se como tooaccess Hola datos de hello Azure AD API de informes de una manera mediante programación?</span><span class="sxs-lookup"><span data-stu-id="b72c9-194">Would you like tooaccess hello data from hello Azure AD reporting API in a programmatic manner?</span></span> <span data-ttu-id="b72c9-195">Extraer del repositorio [Introducción a Azure Active Directory Reporting API hello](active-directory-reporting-api-getting-started.md).</span><span class="sxs-lookup"><span data-stu-id="b72c9-195">Check out [Getting started with hello Azure Active Directory Reporting API](active-directory-reporting-api-getting-started.md).</span></span>
* <span data-ttu-id="b72c9-196">Si desea que toofind más acerca de los informes de Azure Active Directory, vea hello [Azure Active Directory Reporting guía](active-directory-reporting-guide.md).</span><span class="sxs-lookup"><span data-stu-id="b72c9-196">If you would like toofind out more about Azure Active Directory reporting, see hello [Azure Active Directory Reporting Guide](active-directory-reporting-guide.md).</span></span>  

