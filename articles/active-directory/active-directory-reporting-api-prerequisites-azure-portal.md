---
title: "Requisitos previos para acceder a la API de generación de informes de Azure AD | Microsoft Docs"
description: "Conozca los requisitos previos para acceder a la API de generación de informes de Azure AD."
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
ms.openlocfilehash: 5fafd83c337e3c73260d89cdad7409a01ce5855b
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/18/2017
---
# <a name="prerequisites-to-access-the-azure-ad-reporting-api"></a><span data-ttu-id="4898c-103">Requisitos previos para acceder a la API de generación de informes de Azure AD</span><span class="sxs-lookup"><span data-stu-id="4898c-103">Prerequisites to access the Azure AD reporting API</span></span>

<span data-ttu-id="4898c-104">Las [API de generación de informes de Azure AD](https://msdn.microsoft.com/library/azure/ad/graph/howto/azure-ad-reports-and-events-preview) proporcionan acceso mediante programación a los datos a través de un conjunto de API de REST.</span><span class="sxs-lookup"><span data-stu-id="4898c-104">The [Azure AD reporting APIs](https://msdn.microsoft.com/library/azure/ad/graph/howto/azure-ad-reports-and-events-preview) provide you with programmatic access to the data through a set of REST-based APIs.</span></span> <span data-ttu-id="4898c-105">Estas API pueden llamarse desde una variedad de lenguajes de programación y herramientas.</span><span class="sxs-lookup"><span data-stu-id="4898c-105">You can call these APIs from a variety of programming languages and tools.</span></span>

<span data-ttu-id="4898c-106">La API de generación de informes utiliza [OAuth](https://msdn.microsoft.com/library/azure/dn645545.aspx) para autorizar el acceso a las API web.</span><span class="sxs-lookup"><span data-stu-id="4898c-106">The reporting API uses [OAuth](https://msdn.microsoft.com/library/azure/dn645545.aspx) to authorize access to the web APIs.</span></span> 

<span data-ttu-id="4898c-107">Para acceder a los datos de informes a través de la API, debe tener asignado uno de los siguientes roles:</span><span class="sxs-lookup"><span data-stu-id="4898c-107">To get access to the reporting data through the API, you need to have one of the following roles assigned:</span></span>

- <span data-ttu-id="4898c-108">Lector de seguridad</span><span class="sxs-lookup"><span data-stu-id="4898c-108">Security Reader</span></span>
- <span data-ttu-id="4898c-109">Administrador de seguridad</span><span class="sxs-lookup"><span data-stu-id="4898c-109">Security Admin</span></span>
- <span data-ttu-id="4898c-110">Administrador global</span><span class="sxs-lookup"><span data-stu-id="4898c-110">Global Admin</span></span>


<span data-ttu-id="4898c-111">Para preparar el acceso a la API de generación de informes, debe hacer lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="4898c-111">To prepare your access to the reporting API, you must:</span></span>

1. <span data-ttu-id="4898c-112">Registro de una aplicación</span><span class="sxs-lookup"><span data-stu-id="4898c-112">Register an application</span></span> 
2. <span data-ttu-id="4898c-113">Concesión de permisos</span><span class="sxs-lookup"><span data-stu-id="4898c-113">Grant permissions</span></span> 
3. <span data-ttu-id="4898c-114">Recopilación de configuraciones</span><span class="sxs-lookup"><span data-stu-id="4898c-114">Gather configuration settings</span></span> 

<span data-ttu-id="4898c-115">Si tiene preguntas, problemas o comentarios, [abra una incidencia de soporte técnico](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-troubleshooting-support-howto).</span><span class="sxs-lookup"><span data-stu-id="4898c-115">For questions, issues or feedback, please [file a support ticket](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-troubleshooting-support-howto).</span></span>

## <a name="register-an-azure-active-directory-application"></a><span data-ttu-id="4898c-116">Registro de una aplicación de Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="4898c-116">Register an Azure Active Directory application</span></span>

<span data-ttu-id="4898c-117">Debe registrar una aplicación incluso si accede a la API de generación de informes mediante un script.</span><span class="sxs-lookup"><span data-stu-id="4898c-117">You need to register an app even if you are accessing the reporting API using a script.</span></span> <span data-ttu-id="4898c-118">Así se le proporciona un **id. de la aplicación**, que es necesario para una llamada de autorización y hace posible que el código reciba tokens.</span><span class="sxs-lookup"><span data-stu-id="4898c-118">This gives you an **Application ID**, which is required for an authorization call and it enables your code to receive tokens.</span></span>

<span data-ttu-id="4898c-119">Si quiere configurar el directorio para que acceda a la API de generación de informes de Azure AD, debe iniciar sesión en Azure Portal con una cuenta de administrador de Azure que también sea miembro del rol de directorio **Administrador global** en su inquilino de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="4898c-119">To configure your directory to access the Azure AD reporting API, you must sign in to the Azure portal with an Azure administrator account that is also a member of the **Global Administrator** directory role in your Azure AD tenant.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="4898c-120">Las aplicaciones que se ejecutan con credenciales con privilegios administrativos como este pueden ser muy avanzadas, así que asegúrese de mantener seguras las credenciales del secreto o el identificador de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="4898c-120">Applications running under credentials with "admin" privileges like this can be very powerful, so please be sure to keep the application's ID/secret credentials secure.</span></span>
> 


<span data-ttu-id="4898c-121">**Para registrar una aplicación de Azure Active Directory:**</span><span class="sxs-lookup"><span data-stu-id="4898c-121">**To register an Azure Active Directory application:**</span></span>

1. <span data-ttu-id="4898c-122">En [Azure Portal](https://portal.azure.com), en el panel de navegación izquierdo, haga clic en **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="4898c-122">In the [Azure portal](https://portal.azure.com), on the left navigation pane, click **Active Directory**.</span></span>
   
    ![Registre la aplicación](./media/active-directory-reporting-api-prerequisites-azure-portal/01.png) 

2. <span data-ttu-id="4898c-124">En la hoja **Azure Active Directory**, haga clic en **Registros de aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="4898c-124">On the **Azure Active Directory** blade, click **App registrations**.</span></span>

    ![Registre la aplicación](./media/active-directory-reporting-api-prerequisites-azure-portal/02.png) 

3. <span data-ttu-id="4898c-126">En la hoja **Registros de aplicaciones**, en la barra de herramientas de la parte superior, haga clic en **Nuevo registro de aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="4898c-126">On the **App registrations** blade, in the toolbar on the top, click **New application registration**.</span></span>

    ![Registre la aplicación](./media/active-directory-reporting-api-prerequisites-azure-portal/03.png)

4. <span data-ttu-id="4898c-128">En la hoja **Crear**, siga estos pasos:</span><span class="sxs-lookup"><span data-stu-id="4898c-128">On the **Create** blade, perform the following steps:</span></span>

    ![Registre la aplicación](./media/active-directory-reporting-api-prerequisites-azure-portal/04.png)

    <span data-ttu-id="4898c-130">a.</span><span class="sxs-lookup"><span data-stu-id="4898c-130">a.</span></span> <span data-ttu-id="4898c-131">En el cuadro de texto **Nombre**, escriba `Reporting API application`.</span><span class="sxs-lookup"><span data-stu-id="4898c-131">In the **Name** textbox, type `Reporting API application`.</span></span>

    <span data-ttu-id="4898c-132">b.</span><span class="sxs-lookup"><span data-stu-id="4898c-132">b.</span></span> <span data-ttu-id="4898c-133">Seleccione **Aplicación web o API** como **Tipo de aplicación**.</span><span class="sxs-lookup"><span data-stu-id="4898c-133">As **Application type**, select **Web app / API**.</span></span>

    <span data-ttu-id="4898c-134">c.</span><span class="sxs-lookup"><span data-stu-id="4898c-134">c.</span></span> <span data-ttu-id="4898c-135">En el cuadro de texto **URL de inicio de sesión**, escriba `https://localhost`.</span><span class="sxs-lookup"><span data-stu-id="4898c-135">In the **Sign-on URL** textbox, type `https://localhost`.</span></span>

    <span data-ttu-id="4898c-136">d.</span><span class="sxs-lookup"><span data-stu-id="4898c-136">d.</span></span> <span data-ttu-id="4898c-137">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="4898c-137">Click **Create**.</span></span> 


## <a name="grant-permissions"></a><span data-ttu-id="4898c-138">Concesión de permisos</span><span class="sxs-lookup"><span data-stu-id="4898c-138">Grant permissions</span></span> 

<span data-ttu-id="4898c-139">El objetivo de este paso es conceder a la aplicación permisos **Leer datos de directorio** para la API de **Microsoft Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="4898c-139">The objective of this step is to grant your application **Read directory data** permissions to the **Windows Azure Active Directory** API.</span></span>

![Registre la aplicación](./media/active-directory-reporting-api-prerequisites-azure-portal/16.png)
 

<span data-ttu-id="4898c-141">**Para conceder a la aplicación permiso para usar la API:**</span><span class="sxs-lookup"><span data-stu-id="4898c-141">**To grant your application permission to use the API:**</span></span>

1. <span data-ttu-id="4898c-142">En la hoja **Registros de aplicaciones**, en la lista de aplicaciones, haga clic en **Reporting API application** (Aplicación de la API de generación de informes).</span><span class="sxs-lookup"><span data-stu-id="4898c-142">On the **App registrations** blade, in the apps list, click **Reporting API application**.</span></span>

2. <span data-ttu-id="4898c-143">En la hoja **Reporting API application** (Aplicación de la API de generación de informes), en la barra de herramientas de la parte superior, haga clic en **Configuración**.</span><span class="sxs-lookup"><span data-stu-id="4898c-143">On the **Reporting API application** blade, in the toolbar on the top, click **Settings**.</span></span> 

    ![Registre la aplicación](./media/active-directory-reporting-api-prerequisites-azure-portal/05.png)

3. <span data-ttu-id="4898c-145">En la hoja **Configuración**, haga clic en **Permisos necesarios**.</span><span class="sxs-lookup"><span data-stu-id="4898c-145">On the **Settings** blade, click **Required permissions**.</span></span> 

    ![Registre la aplicación](./media/active-directory-reporting-api-prerequisites-azure-portal/06.png)

4. <span data-ttu-id="4898c-147">En la hoja **Permisos necesarios**, en la lista **API**, haga clic en **Microsoft Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="4898c-147">On the **Required permissions** blade, in the **API** list, click **Windows Azure Active Directory**.</span></span> 

    ![Registre la aplicación](./media/active-directory-reporting-api-prerequisites-azure-portal/07.png)

5. <span data-ttu-id="4898c-149">En la hoja **Habilitar acceso**, seleccione **Leer datos de directorio**.</span><span class="sxs-lookup"><span data-stu-id="4898c-149">On the **Enable Access** blade, select **Read directory data**.</span></span> 

    ![Registre la aplicación](./media/active-directory-reporting-api-prerequisites-azure-portal/08.png)

6. <span data-ttu-id="4898c-151">En la barra de herramientas de la parte superior, haga clic en **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="4898c-151">In the toolbar on the top, click **Save**.</span></span>

    ![Registre la aplicación](./media/active-directory-reporting-api-prerequisites-azure-portal/15.png)

## <a name="gather-configuration-settings"></a><span data-ttu-id="4898c-153">Recopilación de configuraciones</span><span class="sxs-lookup"><span data-stu-id="4898c-153">Gather configuration settings</span></span> 
<span data-ttu-id="4898c-154">En esta sección se muestra cómo obtener la siguiente configuración del directorio:</span><span class="sxs-lookup"><span data-stu-id="4898c-154">This section shows you how to get the following settings from your directory:</span></span>

* <span data-ttu-id="4898c-155">Nombre de dominio</span><span class="sxs-lookup"><span data-stu-id="4898c-155">Domain name</span></span>
* <span data-ttu-id="4898c-156">id. de cliente</span><span class="sxs-lookup"><span data-stu-id="4898c-156">Client ID</span></span>
* <span data-ttu-id="4898c-157">Secreto del cliente</span><span class="sxs-lookup"><span data-stu-id="4898c-157">Client secret</span></span>

<span data-ttu-id="4898c-158">Necesitará estos valores al configurar llamadas a la API de generación de informes.</span><span class="sxs-lookup"><span data-stu-id="4898c-158">You need these values when configuring calls to the reporting API.</span></span> 

### <a name="get-your-domain-name"></a><span data-ttu-id="4898c-159">Obtención del nombre de dominio</span><span class="sxs-lookup"><span data-stu-id="4898c-159">Get your domain name</span></span>

<span data-ttu-id="4898c-160">**Para obtener el nombre del dominio:**</span><span class="sxs-lookup"><span data-stu-id="4898c-160">**To get your domain name:**</span></span>

1. <span data-ttu-id="4898c-161">En [Azure Portal](https://portal.azure.com), en el panel de navegación izquierdo, haga clic en **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="4898c-161">In the [Azure portal](https://portal.azure.com), on the left navigation pane, click **Active Directory**.</span></span>
   
    ![Registre la aplicación](./media/active-directory-reporting-api-prerequisites-azure-portal/01.png) 

2. <span data-ttu-id="4898c-163">En la hoja **Azure Active Directory**, haga clic en **Nombres de dominio**.</span><span class="sxs-lookup"><span data-stu-id="4898c-163">On the **Azure Active Directory** blade, click **Domain names**.</span></span>

    ![Registre la aplicación](./media/active-directory-reporting-api-prerequisites-azure-portal/09.png) 

3. <span data-ttu-id="4898c-165">Copie el nombre del dominio en la lista de dominios.</span><span class="sxs-lookup"><span data-stu-id="4898c-165">Copy your domain name from the list of domains.</span></span>


### <a name="get-your-applications-client-id"></a><span data-ttu-id="4898c-166">Obtención del id. de cliente de la aplicación</span><span class="sxs-lookup"><span data-stu-id="4898c-166">Get your application's client ID</span></span>

<span data-ttu-id="4898c-167">**Para obtener el id. de cliente de la aplicación:**</span><span class="sxs-lookup"><span data-stu-id="4898c-167">**To get your application's client ID:**</span></span>

1. <span data-ttu-id="4898c-168">En [Azure Portal](https://portal.azure.com), en el panel de navegación izquierdo, haga clic en **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="4898c-168">In the [Azure portal](https://portal.azure.com), on the left navigation pane, click **Active Directory**.</span></span>
   
    ![Registre la aplicación](./media/active-directory-reporting-api-prerequisites-azure-portal/01.png) 

2. <span data-ttu-id="4898c-170">En la hoja **Registros de aplicaciones**, en la lista de aplicaciones, haga clic en **Reporting API application** (Aplicación de la API de generación de informes).</span><span class="sxs-lookup"><span data-stu-id="4898c-170">On the **App registrations** blade, in the apps list, click **Reporting API application**.</span></span>

3. <span data-ttu-id="4898c-171">En la hoja **Reporting API application** (Aplicación de la API de generación de informes), en **Id. de la aplicación**, haga clic en **Haga clic para copiar**.</span><span class="sxs-lookup"><span data-stu-id="4898c-171">On the **Reporting API application** blade, at the **Application ID**, click **Click to copy**.</span></span>

    ![Registre la aplicación](./media/active-directory-reporting-api-prerequisites-azure-portal/11.png) 



### <a name="get-your-applications-client-secret"></a><span data-ttu-id="4898c-173">Obtención del secreto de cliente de la aplicación</span><span class="sxs-lookup"><span data-stu-id="4898c-173">Get your application's client secret</span></span>
<span data-ttu-id="4898c-174">Para obtener el secreto de cliente de la aplicación, debe crear una nueva clave y guardar su valor después, ya que no es posible recuperarla más tarde.</span><span class="sxs-lookup"><span data-stu-id="4898c-174">To get your application's client secret, you need to create a new key and save its value upon saving the new key because it is not possible to retrieve this value later anymore.</span></span>

<span data-ttu-id="4898c-175">**Para obtener el secreto de cliente de la aplicación:**</span><span class="sxs-lookup"><span data-stu-id="4898c-175">**To get your application's client secret:**</span></span>

1. <span data-ttu-id="4898c-176">En [Azure Portal](https://portal.azure.com), en el panel de navegación izquierdo, haga clic en **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="4898c-176">In the [Azure portal](https://portal.azure.com), on the left navigation pane, click **Active Directory**.</span></span>
   
    ![Registre la aplicación](./media/active-directory-reporting-api-prerequisites-azure-portal/01.png) 

2. <span data-ttu-id="4898c-178">En la hoja **Registros de aplicaciones**, en la lista de aplicaciones, haga clic en **Reporting API application** (Aplicación de la API de generación de informes).</span><span class="sxs-lookup"><span data-stu-id="4898c-178">On the **App registrations** blade, in the apps list, click **Reporting API application**.</span></span>


3. <span data-ttu-id="4898c-179">En la hoja **Reporting API application** (Aplicación de la API de generación de informes), en la barra de herramientas de la parte superior, haga clic en **Configuración**.</span><span class="sxs-lookup"><span data-stu-id="4898c-179">On the **Reporting API application** blade, in the toolbar on the top, click **Settings**.</span></span> 

    ![Registre la aplicación](./media/active-directory-reporting-api-prerequisites-azure-portal/05.png)

4. <span data-ttu-id="4898c-181">En la hoja **Configuración**, en la sección **Acceso de API**, haga clic en **Claves**.</span><span class="sxs-lookup"><span data-stu-id="4898c-181">On the **Settings** blade, in the **APIR Access** section, click **Keys**.</span></span> 

    ![Registre la aplicación](./media/active-directory-reporting-api-prerequisites-azure-portal/12.png)


5. <span data-ttu-id="4898c-183">En la hoja **Claves**, siga estos pasos:</span><span class="sxs-lookup"><span data-stu-id="4898c-183">On the **Keys** blade, perform the following steps:</span></span>

    ![Registre la aplicación](./media/active-directory-reporting-api-prerequisites-azure-portal/14.png)

    <span data-ttu-id="4898c-185">a.</span><span class="sxs-lookup"><span data-stu-id="4898c-185">a.</span></span> <span data-ttu-id="4898c-186">En el cuadro de texto **Descripción**, escriba `Reporting API`.</span><span class="sxs-lookup"><span data-stu-id="4898c-186">In the **Description** textbox, type `Reporting API`.</span></span>

    <span data-ttu-id="4898c-187">b.</span><span class="sxs-lookup"><span data-stu-id="4898c-187">b.</span></span> <span data-ttu-id="4898c-188">En **Expiración**, seleccione **En 2 años**.</span><span class="sxs-lookup"><span data-stu-id="4898c-188">As **Expires**, select **In 2 years**.</span></span>

    <span data-ttu-id="4898c-189">c.</span><span class="sxs-lookup"><span data-stu-id="4898c-189">c.</span></span> <span data-ttu-id="4898c-190">Haga clic en **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="4898c-190">Click **Save**.</span></span>

    <span data-ttu-id="4898c-191">d.</span><span class="sxs-lookup"><span data-stu-id="4898c-191">d.</span></span> <span data-ttu-id="4898c-192">Copie el valor de la clave.</span><span class="sxs-lookup"><span data-stu-id="4898c-192">Copy the key value.</span></span>


## <a name="next-steps"></a><span data-ttu-id="4898c-193">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="4898c-193">Next Steps</span></span>
* <span data-ttu-id="4898c-194">¿Quiere obtener acceso mediante programación a los datos de la API de generación de informes de Azure AD?</span><span class="sxs-lookup"><span data-stu-id="4898c-194">Would you like to access the data from the Azure AD reporting API in a programmatic manner?</span></span> <span data-ttu-id="4898c-195">Consulte [Introducción a la API de informes de Azure Active Directory](active-directory-reporting-api-getting-started.md).</span><span class="sxs-lookup"><span data-stu-id="4898c-195">Check out [Getting started with the Azure Active Directory Reporting API](active-directory-reporting-api-getting-started.md).</span></span>
* <span data-ttu-id="4898c-196">Si quiere obtener más información sobre informes de Azure Active Directory, consulte la [guía de generación de informes de Azure Active Directory](active-directory-reporting-guide.md).</span><span class="sxs-lookup"><span data-stu-id="4898c-196">If you would like to find out more about Azure Active Directory reporting, see the [Azure Active Directory Reporting Guide](active-directory-reporting-guide.md).</span></span>  

