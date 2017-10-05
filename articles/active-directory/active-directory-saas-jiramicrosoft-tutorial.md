---
title: "Tutorial: Integración de Azure Active Directory con JIRA SAML SSO by Microsoft | Microsoft Docs"
description: "Obtenga información sobre cómo configurar el inicio de sesión único entre Azure Active Directory y JIRA SAML SSO by Microsoft."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 0dc847b9-eec4-4c31-845e-0144ddedc4a7
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/19/2017
ms.author: jeedes
ms.openlocfilehash: b5f7813c8244d2964b6894ae49cd64e0ee71b704
ms.sourcegitcommit: 422efcbac5b6b68295064bd545132fcc98349d01
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/29/2017
---
# <a name="tutorial-azure-active-directory-integration-with-jira-saml-sso-by-microsoft"></a><span data-ttu-id="3df09-103">Tutorial: Integración de Azure Active Directory con JIRA SAML SSO by Microsoft</span><span class="sxs-lookup"><span data-stu-id="3df09-103">Tutorial: Azure Active Directory integration with JIRA SAML SSO by Microsoft</span></span>

<span data-ttu-id="3df09-104">En este tutorial, obtendrá información sobre cómo integrar JIRA SAML SSO by Microsoft con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="3df09-104">In this tutorial, you learn how to integrate JIRA SAML SSO by Microsoft with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="3df09-105">La integración de JIRA SAML SSO by Microsoft con Azure AD le proporciona las siguientes ventajas:</span><span class="sxs-lookup"><span data-stu-id="3df09-105">Integrating JIRA SAML SSO by Microsoft with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="3df09-106">Puede controlar en Azure AD quién tiene acceso a JIRA SAML SSO by Microsoft.</span><span class="sxs-lookup"><span data-stu-id="3df09-106">You can control in Azure AD who has access to JIRA SAML SSO by Microsoft</span></span>
- <span data-ttu-id="3df09-107">Puede permitir que los usuarios inicien sesión automáticamente en JIRA SAML SSO by Microsoft (inicio de sesión único) con sus cuentas de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="3df09-107">You can enable your users to automatically get signed-on to JIRA SAML SSO by Microsoft (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="3df09-108">Puede administrar sus cuentas en una ubicación central: el nuevo Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="3df09-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="3df09-109">Si desea saber más sobre la integración de aplicaciones SaaS con Azure AD, consulte [¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="3df09-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="3df09-110">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="3df09-110">Prerequisites</span></span>

<span data-ttu-id="3df09-111">Para configurar la integración de Azure AD con JIRA SAML SSO by Microsoft, se necesitan los siguientes elementos:</span><span class="sxs-lookup"><span data-stu-id="3df09-111">To configure Azure AD integration with JIRA SAML SSO by Microsoft, you need the following items:</span></span>

- <span data-ttu-id="3df09-112">Una suscripción de Azure AD</span><span class="sxs-lookup"><span data-stu-id="3df09-112">An Azure AD subscription</span></span>
- <span data-ttu-id="3df09-113">Aplicación de servidor JIRA instalada en un servidor Windows de 64 bits (de manera local o en la infraestructura de IaaS en la nube)</span><span class="sxs-lookup"><span data-stu-id="3df09-113">JIRA server application installed on a Windows 64-bit server (on premise or on the cloud IaaS infrastructure)</span></span>
- <span data-ttu-id="3df09-114">El servidor JIRA es compatible con HTTPS</span><span class="sxs-lookup"><span data-stu-id="3df09-114">JIRA server is HTTPS enabled</span></span>
- <span data-ttu-id="3df09-115">Tenga en cuenta que las versiones admitidas para el complemento JIRA se mencionan en la sección siguiente.</span><span class="sxs-lookup"><span data-stu-id="3df09-115">Note the supported versions for JIRA Plugin are mentioned in below section.</span></span>
- <span data-ttu-id="3df09-116">El servidor JIRA es accesible en Internet, especialmente a la página de inicio de sesión de Azure AD para la autenticación y debe poder recibir el token de Azure AD</span><span class="sxs-lookup"><span data-stu-id="3df09-116">JIRA server is reachable on internet particularly to Azure AD Login page for authentication and should able to receive the token from Azure AD</span></span>
- <span data-ttu-id="3df09-117">Las credenciales de administrador se configuran en JIRA</span><span class="sxs-lookup"><span data-stu-id="3df09-117">Admin credentials are set up in JIRA</span></span>
- <span data-ttu-id="3df09-118">WebSudo está deshabilitado en JIRA</span><span class="sxs-lookup"><span data-stu-id="3df09-118">WebSudo is disabled in JIRA</span></span>
- <span data-ttu-id="3df09-119">Usuario de prueba creado en la aplicación de servidor JIRA</span><span class="sxs-lookup"><span data-stu-id="3df09-119">Test user created in the JIRA server application</span></span>

> [!NOTE]
> <span data-ttu-id="3df09-120">Para probar los pasos de este tutorial, no se recomienda el uso de un entorno de producción de JIRA.</span><span class="sxs-lookup"><span data-stu-id="3df09-120">To test the steps in this tutorial, we do not recommend using a production environment of JIRA.</span></span> <span data-ttu-id="3df09-121">Pruebe primero la integración en el entorno de desarrollo o de ensayo de la aplicación y, después, use el entorno de producción.</span><span class="sxs-lookup"><span data-stu-id="3df09-121">Test the integration first in development or staging environment of the application and then use the production environment.</span></span>

<span data-ttu-id="3df09-122">Para probar los pasos de este tutorial, debe seguir estas recomendaciones:</span><span class="sxs-lookup"><span data-stu-id="3df09-122">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="3df09-123">No use el entorno de producción, salvo que sea necesario.</span><span class="sxs-lookup"><span data-stu-id="3df09-123">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="3df09-124">Si no dispone de un entorno de prueba de Azure AD, aquí puede obtener una versión de prueba de un mes: [oferta de versión de prueba](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="3df09-124">If you don't have an Azure AD trial environment, you can get a one-month trial here: [Trial offer](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="supported-versions-of-jira"></a><span data-ttu-id="3df09-125">Versiones compatibles de JIRA</span><span class="sxs-lookup"><span data-stu-id="3df09-125">Supported versions of JIRA</span></span> 

<span data-ttu-id="3df09-126">En la actualidad, se admiten las siguientes versiones de JIRA:</span><span class="sxs-lookup"><span data-stu-id="3df09-126">As of now, following versions of JIRA are supported:</span></span>

- <span data-ttu-id="3df09-127">Núcleo y software de JIRA: de la 6.0 a la 7.2.0</span><span class="sxs-lookup"><span data-stu-id="3df09-127">JIRA Core and Software: 6.0 to 7.2.0</span></span>
- <span data-ttu-id="3df09-128">Departamento de servicios de JIRA: de la 3.0 a la 3.2</span><span class="sxs-lookup"><span data-stu-id="3df09-128">JIRA Service Desk: 3.0 to 3.2</span></span>

## <a name="scenario-description"></a><span data-ttu-id="3df09-129">Descripción del escenario</span><span class="sxs-lookup"><span data-stu-id="3df09-129">Scenario description</span></span>
<span data-ttu-id="3df09-130">En este tutorial, puede probar el inicio de sesión único de Azure AD en un entorno de prueba.</span><span class="sxs-lookup"><span data-stu-id="3df09-130">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="3df09-131">La situación descrita en este tutorial consta de dos bloques de creación principales:</span><span class="sxs-lookup"><span data-stu-id="3df09-131">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="3df09-132">Agregar JIRA SAML SSO by Microsoft desde la galería</span><span class="sxs-lookup"><span data-stu-id="3df09-132">Adding JIRA SAML SSO by Microsoft from the gallery</span></span>
2. <span data-ttu-id="3df09-133">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="3df09-133">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-jira-saml-sso-by-microsoft-from-the-gallery"></a><span data-ttu-id="3df09-134">Agregar JIRA SAML SSO by Microsoft desde la galería</span><span class="sxs-lookup"><span data-stu-id="3df09-134">Adding JIRA SAML SSO by Microsoft from the gallery</span></span>
<span data-ttu-id="3df09-135">Para configurar la integración de JIRA SAML SSO by Microsoft en Azure AD, deberá agregar JIRA SAML SSO by Microsoft desde la galería a la lista de aplicaciones SaaS administradas.</span><span class="sxs-lookup"><span data-stu-id="3df09-135">To configure the integration of JIRA SAML SSO by Microsoft into Azure AD, you need to add JIRA SAML SSO by Microsoft from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="3df09-136">**Para agregar JIRA SAML SSO by Microsoft desde la galería, siga estos pasos:**</span><span class="sxs-lookup"><span data-stu-id="3df09-136">**To add JIRA SAML SSO by Microsoft from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="3df09-137">En el panel de navegación izquierdo de **[Azure Portal](https://portal.azure.com)**, haga clic en el icono de **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="3df09-137">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="3df09-139">Vaya a **Aplicaciones empresariales**.</span><span class="sxs-lookup"><span data-stu-id="3df09-139">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="3df09-140">A continuación, vaya a **Todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="3df09-140">Then go to **All applications**.</span></span>

    ![Aplicaciones][2]
    
3. <span data-ttu-id="3df09-142">Para agregar una nueva aplicación, haga clic en el botón **Nueva aplicación** de la parte superior del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="3df09-142">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Aplicaciones][3]

4. <span data-ttu-id="3df09-144">En el cuadro de búsqueda, escriba **JIRA SAML SSO by Microsoft**.</span><span class="sxs-lookup"><span data-stu-id="3df09-144">In the search box, type **JIRA SAML SSO by Microsoft**.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-jiramicrosoft-tutorial/tutorial_jiramicrosoft_search.png)

5. <span data-ttu-id="3df09-146">En el panel de resultados, seleccione **JIRA SAML SSO by Microsoft** y luego haga clic en el botón **Agregar** para agregar la aplicación.</span><span class="sxs-lookup"><span data-stu-id="3df09-146">In the results panel, select **JIRA SAML SSO by Microsoft**, and then click **Add** button to add the application.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-jiramicrosoft-tutorial/tutorial_jiramicrosoft_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="3df09-148">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="3df09-148">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="3df09-149">En esta sección, va a configurar y probar el inicio de sesión único de Azure AD con JIRA SAML SSO by Microsoft con un usuario de prueba llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="3df09-149">In this section, you configure and test Azure AD single sign-on with JIRA SAML SSO by Microsoft based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="3df09-150">Para que el inicio de sesión único funcione, Azure AD debe saber cuál es el usuario homólogo de JIRA SAML SSO by Microsoft para un usuario de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="3df09-150">For single sign-on to work, Azure AD needs to know what the counterpart user in JIRA SAML SSO by Microsoft is to a user in Azure AD.</span></span> <span data-ttu-id="3df09-151">Es decir, es necesario establecer una relación de vínculo entre un usuario de Azure AD y el usuario correspondiente de JIRA SAML SSO by Microsoft.</span><span class="sxs-lookup"><span data-stu-id="3df09-151">In other words, a link relationship between an Azure AD user and the related user in JIRA SAML SSO by Microsoft needs to be established.</span></span>

<span data-ttu-id="3df09-152">Para establecer la relación de vínculo, en JIRA SAML SSO by Microsoft, asigne el valor de **nombre de usuario** de Azure AD como valor de **nombre de usuario**.</span><span class="sxs-lookup"><span data-stu-id="3df09-152">In JIRA SAML SSO by Microsoft, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="3df09-153">Para configurar y probar el inicio de sesión único de Azure AD con JIRA SAML SSO by Microsoft, es necesario completar los siguientes bloques de creación:</span><span class="sxs-lookup"><span data-stu-id="3df09-153">To configure and test Azure AD single sign-on with JIRA SAML SSO by Microsoft, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="3df09-154">**[Configuración del inicio de sesión único de Azure AD](#configuring-azure-ad-single-sign-on)** : para permitir a los usuarios usar esta característica.</span><span class="sxs-lookup"><span data-stu-id="3df09-154">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="3df09-155">**[Creación de un usuario de prueba de Azure AD](#creating-an-azure-ad-test-user)** : para probar el inicio de sesión único de Azure AD con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="3df09-155">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="3df09-156">**[Creación de un usuario de prueba de JIRA SAML SSO by Microsoft](#creating-a-jira-saml-sso-by-microsoft-test-user)**: Para tener un homólogo de Britta Simon en JIRA SAML SSO by Microsoft que esté vinculado a la representación del usuario en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="3df09-156">**[Creating a JIRA SAML SSO by Microsoft test user](#creating-a-jira-saml-sso-by-microsoft-test-user)** - to have a counterpart of Britta Simon in JIRA SAML SSO by Microsoft that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="3df09-157">**[Asignación del usuario de prueba de Azure AD](#assigning-the-azure-ad-test-user)** : para permitir que Britta Simon use el inicio de sesión único de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="3df09-157">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="3df09-158">**[Testing Single Sign-On](#testing-single-sign-on)** : para comprobar si funciona la configuración.</span><span class="sxs-lookup"><span data-stu-id="3df09-158">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="3df09-159">Configuración del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="3df09-159">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="3df09-160">En esta sección habilitará el inicio de sesión único de Azure AD en Azure Portal y configurará el inicio de sesión único en la aplicación JIRA SAML SSO by Microsoft.</span><span class="sxs-lookup"><span data-stu-id="3df09-160">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your JIRA SAML SSO by Microsoft application.</span></span>

<span data-ttu-id="3df09-161">**Para configurar el inicio de sesión único de Azure AD con JIRA SAML SSO by Microsoft, siga estos pasos:**</span><span class="sxs-lookup"><span data-stu-id="3df09-161">**To configure Azure AD single sign-on with JIRA SAML SSO by Microsoft, perform the following steps:**</span></span>

1. <span data-ttu-id="3df09-162">En Azure Portal, en la página de integración de la aplicación **JIRA SAML SSO by Microsoft**, haga clic en **Inicio de sesión único**.</span><span class="sxs-lookup"><span data-stu-id="3df09-162">In the Azure portal, on the **JIRA SAML SSO by Microsoft** application integration page, click **Single sign-on**.</span></span>

    ![Configurar inicio de sesión único][4]

2. <span data-ttu-id="3df09-164">En el cuadro de diálogo **Inicio de sesión único**, en **Modo** seleccione **Inicio de sesión basado en SAML** para habilitar el inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="3df09-164">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configurar inicio de sesión único](./media/active-directory-saas-jiramicrosoft-tutorial/tutorial_jiramicrosoft_samlbase.png)

3. <span data-ttu-id="3df09-166">En la sección **Dominio y direcciones URL de JIRA SAML SSO by Microsoft**, siga estos pasos:</span><span class="sxs-lookup"><span data-stu-id="3df09-166">On the **JIRA SAML SSO by Microsoft Domain and URLs** section, perform the following steps:</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-jiramicrosoft-tutorial/tutorial_jiramicrosoft_url.png)

    <span data-ttu-id="3df09-168">a.</span><span class="sxs-lookup"><span data-stu-id="3df09-168">a.</span></span> <span data-ttu-id="3df09-169">En el cuadro de texto **URL de inicio de sesión**, escriba una dirección URL con el siguiente patrón: `https://<domain:port>/plugins/servlet/saml/auth`.</span><span class="sxs-lookup"><span data-stu-id="3df09-169">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<domain:port>/plugins/servlet/saml/auth`</span></span>

    <span data-ttu-id="3df09-170">b.</span><span class="sxs-lookup"><span data-stu-id="3df09-170">b.</span></span> <span data-ttu-id="3df09-171">En el cuadro de texto **Identificador**, escriba una dirección URL con el siguiente patrón: `https://<domain:port>/`</span><span class="sxs-lookup"><span data-stu-id="3df09-171">In the **Identifier** textbox, type a URL using the following pattern: `https://<domain:port>/`</span></span>

    <span data-ttu-id="3df09-172">c.</span><span class="sxs-lookup"><span data-stu-id="3df09-172">c.</span></span> <span data-ttu-id="3df09-173">En el cuadro de texto **URL de respuesta**, escriba una dirección URL con el siguiente patrón: `https://<domain:port>/plugins/servlet/saml/auth`.</span><span class="sxs-lookup"><span data-stu-id="3df09-173">In the **Reply URL** textbox, type a URL using the following pattern: `https://<domain:port>/plugins/servlet/saml/auth`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="3df09-174">Estos valores no son reales.</span><span class="sxs-lookup"><span data-stu-id="3df09-174">These values are not real.</span></span> <span data-ttu-id="3df09-175">Actualice estos valores con los valores reales de Identificador, URL de respuesta y URL de inicio de sesión.</span><span class="sxs-lookup"><span data-stu-id="3df09-175">Update these values with the actual Identifier, Reply URL, and Sign-On URL.</span></span> <span data-ttu-id="3df09-176">En caso de que sea una dirección URL con nombre, el puerto es opcional.</span><span class="sxs-lookup"><span data-stu-id="3df09-176">Port is optional in case it’s a named URL.</span></span> <span data-ttu-id="3df09-177">Estos valores se reciben durante la configuración del complemento de Jira, que se explica más adelante en el tutorial.</span><span class="sxs-lookup"><span data-stu-id="3df09-177">These values are received during the configuration of Jira plugin, which is explained later in the tutorial.</span></span>
 
4. <span data-ttu-id="3df09-178">Para generar la dirección URL de **Metadatos**, lleve a cabo los pasos siguientes:</span><span class="sxs-lookup"><span data-stu-id="3df09-178">To generate the **Metadata** url, perform the following steps:</span></span>

    <span data-ttu-id="3df09-179">a.</span><span class="sxs-lookup"><span data-stu-id="3df09-179">a.</span></span> <span data-ttu-id="3df09-180">Haga clic en **Registros de aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="3df09-180">Click **App registrations**.</span></span>
    
    ![Configurar inicio de sesión único](./media/active-directory-saas-jiramicrosoft-tutorial/appregistrations.png)
   
    <span data-ttu-id="3df09-182">b.</span><span class="sxs-lookup"><span data-stu-id="3df09-182">b.</span></span> <span data-ttu-id="3df09-183">Haga clic en **Puntos de conexión** para abrir el cuadro de diálogo **Puntos de conexión**.</span><span class="sxs-lookup"><span data-stu-id="3df09-183">Click **Endpoints** to open **Endpoints** dialog box.</span></span>  
    
    ![Configurar inicio de sesión único](./media/active-directory-saas-jiramicrosoft-tutorial/endpointicon.png)

    <span data-ttu-id="3df09-185">c.</span><span class="sxs-lookup"><span data-stu-id="3df09-185">c.</span></span> <span data-ttu-id="3df09-186">Haga clic en el botón Copiar para copiar la dirección URL del **DOCUMENTO DE METADATOS DE FEDERACIÓN** y péguela en el Bloc de notas.</span><span class="sxs-lookup"><span data-stu-id="3df09-186">Click the copy button to copy **FEDERATION METADATA DOCUMENT** url and paste it into notepad.</span></span>
    
    ![Configurar inicio de sesión único](./media/active-directory-saas-jiramicrosoft-tutorial/endpoint.png)
     
    <span data-ttu-id="3df09-188">d.</span><span class="sxs-lookup"><span data-stu-id="3df09-188">d.</span></span> <span data-ttu-id="3df09-189">Ahora, vaya a la página de propiedades de **JIRA SAML SSO by Microsoft** y copie el **Id. de aplicación** con el botón **Copiar** y péguelo en el Bloc de notas.</span><span class="sxs-lookup"><span data-stu-id="3df09-189">Now go to the property page of **JIRA SAML SSO by Microsoft** and copy the **Application Id** using **Copy** button and paste it into notepad.</span></span>
 
    ![Configurar inicio de sesión único](./media/active-directory-saas-jiramicrosoft-tutorial/appid.png)

    <span data-ttu-id="3df09-191">e.</span><span class="sxs-lookup"><span data-stu-id="3df09-191">e.</span></span> <span data-ttu-id="3df09-192">Genere la **dirección URL de metadatos** con el patrón siguiente: `<FEDERATION METADATA DOCUMENT url>?appid=<application id>` y copie este valor en el Bloc de notas, ya que se usará posteriormente para la configuración del complemento.</span><span class="sxs-lookup"><span data-stu-id="3df09-192">Generate the **Metadata URL** using the following pattern: `<FEDERATION METADATA DOCUMENT url>?appid=<application id>` and copy this value in notepad as it is used later for the configuration of the plugin.</span></span>

5. <span data-ttu-id="3df09-193">Haga clic en el botón **Guardar** .</span><span class="sxs-lookup"><span data-stu-id="3df09-193">Click **Save** button.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-jiramicrosoft-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="3df09-195">Póngase en contacto con [Microsoft](mailto:waadpartners@microsoft.com) con la siguiente información para el complemento de JIRA.</span><span class="sxs-lookup"><span data-stu-id="3df09-195">Contact [Microsoft](mailto:waadpartners@microsoft.com) with the following information for the JIRA plugin.</span></span>
    
    *   <span data-ttu-id="3df09-196">Nombre del cliente:</span><span class="sxs-lookup"><span data-stu-id="3df09-196">Customer Name:</span></span>
    *   <span data-ttu-id="3df09-197">Nombre del dominio principal:</span><span class="sxs-lookup"><span data-stu-id="3df09-197">Primary domain name:</span></span>
    *   <span data-ttu-id="3df09-198">Azure AD Premium: Sí/No (el complemento estará disponible para todos los clientes Free, Basic y Premium SKU)</span><span class="sxs-lookup"><span data-stu-id="3df09-198">Azure AD Premium: Yes/No (Plugin will be available to all     the customer Free, Basic, and Premium SKU)</span></span>
    *   <span data-ttu-id="3df09-199">Número de usuarios que van a usar esta integración:</span><span class="sxs-lookup"><span data-stu-id="3df09-199">Number of users who will be using this integration:</span></span>
    *   <span data-ttu-id="3df09-200">Versión de JIRA:</span><span class="sxs-lookup"><span data-stu-id="3df09-200">JIRA Version:</span></span>
    *   <span data-ttu-id="3df09-201">Comentarios:</span><span class="sxs-lookup"><span data-stu-id="3df09-201">Comments:</span></span>

7. <span data-ttu-id="3df09-202">En otra ventana del explorador web, inicie sesión en la instancia de JIRA como administrador.</span><span class="sxs-lookup"><span data-stu-id="3df09-202">In a different web browser window, log in to your JIRA instance as an administrator.</span></span>

8. <span data-ttu-id="3df09-203">Mantenga el mouse encima del icono de engranaje y haga clic en **Complementos**.</span><span class="sxs-lookup"><span data-stu-id="3df09-203">Hover on cog and click the **Add-ons**.</span></span>
    
    ![Configurar inicio de sesión único](./media/active-directory-saas-jiramicrosoft-tutorial/addon1.png)

9. <span data-ttu-id="3df09-205">En la sección de la pestaña Complementos, haga clic en **Administrar complementos**.</span><span class="sxs-lookup"><span data-stu-id="3df09-205">Under Add-ons tab section, click **Manage add-ons**.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-jiramicrosoft-tutorial/addon7.png)

10. <span data-ttu-id="3df09-207">Cargue manualmente el complemento proporcionado por Microsoft.</span><span class="sxs-lookup"><span data-stu-id="3df09-207">Manually upload the plugin provided by Microsoft.</span></span> <span data-ttu-id="3df09-208">Una vez instalado el complemento, aparece en la sección de complementos **Instalados por el usuario** de **Administrar complemento**.</span><span class="sxs-lookup"><span data-stu-id="3df09-208">Once the plugin is installed, it appears in **User Installed** add-ons section of **Manage Add-on** section.</span></span>

11. <span data-ttu-id="3df09-209">Haga clic en **Configurar** para configurar el nuevo complemento.</span><span class="sxs-lookup"><span data-stu-id="3df09-209">Click **Configure** to configure the new plugin.</span></span>

12. <span data-ttu-id="3df09-210">Siga estos pasos en la página de configuración:</span><span class="sxs-lookup"><span data-stu-id="3df09-210">Perform following steps on configuration page:</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-jiramicrosoft-tutorial/addon5.png)
 
    <span data-ttu-id="3df09-212">a.</span><span class="sxs-lookup"><span data-stu-id="3df09-212">a.</span></span> <span data-ttu-id="3df09-213">En **Dirección URL de metadatos** pegue la **dirección URL de metadatos** generada desde Azure AD y haga clic en el botón **Resolver**.</span><span class="sxs-lookup"><span data-stu-id="3df09-213">In **Metadata URL** paste the **Metadata URL** generated from Azure AD and click the **Resolve** button.</span></span> <span data-ttu-id="3df09-214">Se lee la dirección URL de metadatos de IdP y se rellena toda la información de campos.</span><span class="sxs-lookup"><span data-stu-id="3df09-214">It reads the IdP metadata URL and populates all the fields information.</span></span>

    > [!Note]
    > <span data-ttu-id="3df09-215">La ubicación del Id. de usuario de SAML predeterminada es el identificador de nombre.</span><span class="sxs-lookup"><span data-stu-id="3df09-215">Default SAML User ID location is Name Identifier.</span></span> <span data-ttu-id="3df09-216">Puede cambiarlo a una opción de atributo y escribir el nombre de atributo adecuado.</span><span class="sxs-lookup"><span data-stu-id="3df09-216">You can change this to an attribute option and enter the appropriate attribute name.</span></span>

    > [!TIP]
    > <span data-ttu-id="3df09-217">Asegúrese de que hay un solo certificado asignado a la aplicación, de forma que no se produzca ningún error en la resolución de los metadatos.</span><span class="sxs-lookup"><span data-stu-id="3df09-217">Ensure that there is only one certificate mapped against the app so that there is no error in resolving the metadata.</span></span> <span data-ttu-id="3df09-218">Si hay varios certificados, después de resolver los metadatos, el administrador recibe un error.</span><span class="sxs-lookup"><span data-stu-id="3df09-218">If there are multiple certificates, upon resolving the metadata, admin gets an error.</span></span>
    
    <span data-ttu-id="3df09-219">b.</span><span class="sxs-lookup"><span data-stu-id="3df09-219">b.</span></span> <span data-ttu-id="3df09-220">Copie los valores **Identificador, Dirección URL de respuesta y Dirección URL de inicio de sesión**, y péguelos en los cuadros de texto **Identificador, Dirección URL de respuesta y Dirección URL de inicio de sesión** respectivamente en la sección **Dominio y direcciones URL de JIRA SAML SSO by Microsoft** de Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="3df09-220">Copy the **Identifier, Reply URL and Sign on URL** values and paste them in **Identifier, Reply URL and Sign on URL** textboxes respectively in **JIRA SAML SSO by Microsoft Domain and URLs** section on Azure portal.</span></span>

    <span data-ttu-id="3df09-221">c.</span><span class="sxs-lookup"><span data-stu-id="3df09-221">c.</span></span> <span data-ttu-id="3df09-222">En **Nombre del botón de inicio de sesión** escriba el nombre del botón que la organización quiere que los usuarios vean en la pantalla de inicio de sesión.</span><span class="sxs-lookup"><span data-stu-id="3df09-222">In **Login Button Name** type the name of button your organization wants the users to see on login screen.</span></span>

    <span data-ttu-id="3df09-223">d.</span><span class="sxs-lookup"><span data-stu-id="3df09-223">d.</span></span> <span data-ttu-id="3df09-224">En **SAML User ID Locations** (Ubicaciones de Id. de usuario de SAML) seleccione **User ID is in the NameIdentifier element of the Subject statement** (El Id. de usuario está en el elemento NameIdentifier de la instrucción Subject) o **User ID is in an Attribute element** (El Id. de usuario está en un elemento Attribute).</span><span class="sxs-lookup"><span data-stu-id="3df09-224">In **SAML User ID Locations** select either **User ID is in the NameIdentifier element of the Subject statement** or **User ID is in an Attribute element**.</span></span>  <span data-ttu-id="3df09-225">Este identificador debe ser el identificador de usuario de JIRA.</span><span class="sxs-lookup"><span data-stu-id="3df09-225">This ID has to be the JIRA user id.</span></span> <span data-ttu-id="3df09-226">Si el identificador de usuario no coincide, el sistema no permitirá que los usuarios inicien sesión.</span><span class="sxs-lookup"><span data-stu-id="3df09-226">If the user id is not matched, then system will not allow users to log in.</span></span> 
    
    <span data-ttu-id="3df09-227">e.</span><span class="sxs-lookup"><span data-stu-id="3df09-227">e.</span></span> <span data-ttu-id="3df09-228">Si selecciona la opción **User ID is in an Attribute element** (El Id. de usuario está en un elemento Attribute), escriba el nombre del atributo cuando se espera el Id. de usuario en el cuadro de texto **Nombre del atributo**.</span><span class="sxs-lookup"><span data-stu-id="3df09-228">If you select **User ID is in an Attribute element** option, then in **Attribute name** textbox type the name of the attribute where User Id is expected.</span></span> 

    <span data-ttu-id="3df09-229">f.</span><span class="sxs-lookup"><span data-stu-id="3df09-229">f.</span></span> <span data-ttu-id="3df09-230">Si se usa el dominio federado (por ejemplo, ADFS, etc.) con Azure AD, haga clic en la opción **Habilitar detección de dominio principal** y configure el **nombre de dominio**.</span><span class="sxs-lookup"><span data-stu-id="3df09-230">If you are using the federated domain (like ADFS etc.) with Azure AD, then click on the **Enable Home Realm Discovery** option and configure the **Domain Name**.</span></span>
    
    <span data-ttu-id="3df09-231">g.</span><span class="sxs-lookup"><span data-stu-id="3df09-231">g.</span></span> <span data-ttu-id="3df09-232">En **Nombre de dominio**, escriba el nombre del dominio en el caso de inicios de sesión basados en ADFS.</span><span class="sxs-lookup"><span data-stu-id="3df09-232">In **Domain Name** type the domain name here in case of the ADFS-based login.</span></span>

    <span data-ttu-id="3df09-233">h.</span><span class="sxs-lookup"><span data-stu-id="3df09-233">h.</span></span> <span data-ttu-id="3df09-234">Active **Habilitar cierre de sesión único** si quiere que se cierre la sesión de Azure AD cuando un usuario cierra la sesión de JIRA.</span><span class="sxs-lookup"><span data-stu-id="3df09-234">Check **Enable Single Sign out** if you wish to log out from Azure AD when a user logs out from JIRA.</span></span> 

    <span data-ttu-id="3df09-235">i.</span><span class="sxs-lookup"><span data-stu-id="3df09-235">i.</span></span> <span data-ttu-id="3df09-236">Haga clic en el botón **Save** (Guardar) para guardar la configuración.</span><span class="sxs-lookup"><span data-stu-id="3df09-236">Click **Save** button to save the settings.</span></span>

> [!TIP]
> <span data-ttu-id="3df09-237">Ahora puede leer una versión resumida de estas instrucciones dentro de [Azure Portal](https://portal.azure.com) mientras configura la aplicación.</span><span class="sxs-lookup"><span data-stu-id="3df09-237">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="3df09-238">Después de agregar esta aplicación desde la sección **Active Directory > Aplicaciones empresariales**, simplemente haga clic en la pestaña **Inicio de sesión único** y acceda a la documentación insertada a través de la sección **Configuración** de la parte inferior.</span><span class="sxs-lookup"><span data-stu-id="3df09-238">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="3df09-239">Puede leer más sobre la característica de documentación insertada aquí: [Vista previa: Administración de inicio de sesión único para aplicaciones empresariales en el nuevo Azure Portal]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="3df09-239">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="3df09-240">Creación de un usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="3df09-240">Creating an Azure AD test user</span></span>
<span data-ttu-id="3df09-241">El objetivo de esta sección es crear un usuario de prueba en Azure Portal llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="3df09-241">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Creación de un usuario de Azure AD][100]

<span data-ttu-id="3df09-243">**Siga estos pasos para crear un usuario de prueba en Azure AD:**</span><span class="sxs-lookup"><span data-stu-id="3df09-243">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="3df09-244">En el panel de navegación izquierdo de **Azure Portal**, haga clic en el icono de **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="3df09-244">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-jiramicrosoft-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="3df09-246">Para mostrar la lista de usuarios, vaya a **Usuarios y grupos** y haga clic en **Todos los usuarios**.</span><span class="sxs-lookup"><span data-stu-id="3df09-246">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-jiramicrosoft-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="3df09-248">Para abrir el cuadro de diálogo **Usuario**, haga clic en **Agregar** en la parte superior del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="3df09-248">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-jiramicrosoft-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="3df09-250">En la página de diálogo **Usuario**, realice los siguientes pasos:</span><span class="sxs-lookup"><span data-stu-id="3df09-250">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-jiramicrosoft-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="3df09-252">a.</span><span class="sxs-lookup"><span data-stu-id="3df09-252">a.</span></span> <span data-ttu-id="3df09-253">En el cuadro de texto **Nombre**, escriba **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="3df09-253">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="3df09-254">b.</span><span class="sxs-lookup"><span data-stu-id="3df09-254">b.</span></span> <span data-ttu-id="3df09-255">En el cuadro de texto **Nombre de usuario**, escriba la **dirección de correo electrónico** de Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="3df09-255">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="3df09-256">c.</span><span class="sxs-lookup"><span data-stu-id="3df09-256">c.</span></span> <span data-ttu-id="3df09-257">Seleccione **Mostrar contraseña** y anote el valor del cuadro **Contraseña**.</span><span class="sxs-lookup"><span data-stu-id="3df09-257">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="3df09-258">d.</span><span class="sxs-lookup"><span data-stu-id="3df09-258">d.</span></span> <span data-ttu-id="3df09-259">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="3df09-259">Click **Create**.</span></span>
 
### <a name="creating-a-jira-saml-sso-by-microsoft-test-user"></a><span data-ttu-id="3df09-260">Creación de un usuario de prueba de JIRA SAML SSO by Microsoft</span><span class="sxs-lookup"><span data-stu-id="3df09-260">Creating a JIRA SAML SSO by Microsoft test user</span></span>

<span data-ttu-id="3df09-261">Para permitir que los usuarios de Azure AD inicien sesión en el servidor local de JIRA, se deben aprovisionar en JIRA SAML SSO by Microsoft.</span><span class="sxs-lookup"><span data-stu-id="3df09-261">To enable Azure AD users to log in to JIRA on-premise server, they must be provisioned into JIRA SAML SSO by Microsoft.</span></span> <span data-ttu-id="3df09-262">Para JIRA SAML SSO by Microsoft, el aprovisionamiento es una tarea manual.</span><span class="sxs-lookup"><span data-stu-id="3df09-262">For JIRA SAML SSO by Microsoft, provisioning is a manual task.</span></span>

<span data-ttu-id="3df09-263">**Para aprovisionar una cuenta de usuario, realice estos pasos:**</span><span class="sxs-lookup"><span data-stu-id="3df09-263">**To provision a user account, perform the following steps:**</span></span>

1. <span data-ttu-id="3df09-264">Inicie sesión como administrador el servidor local de JIRA.</span><span class="sxs-lookup"><span data-stu-id="3df09-264">Log in to your JIRA on-premise server as an administrator.</span></span>

2. <span data-ttu-id="3df09-265">Mantenga el mouse encima del icono de engranaje y haga clic en **Administración de usuarios**.</span><span class="sxs-lookup"><span data-stu-id="3df09-265">Hover on cog and click the **User management**.</span></span>

    ![Agregar empleado](./media/active-directory-saas-jiramicrosoft-tutorial/user1.png) 

3. <span data-ttu-id="3df09-267">Se le redirigirá a la página de acceso de administrador para especificar la **contraseña** y haga clic en el botón **Confirmar**.</span><span class="sxs-lookup"><span data-stu-id="3df09-267">You are redirected to Administrator Access page to enter **Password** and click **Confirm** button.</span></span>

    ![Agregar empleado](./media/active-directory-saas-jiramicrosoft-tutorial/user2.png) 

4. <span data-ttu-id="3df09-269">En la sección de la pestaña **Administración de usuarios**, haga clic en **Crear usuario**.</span><span class="sxs-lookup"><span data-stu-id="3df09-269">Under **User management** tab section, click **create user**.</span></span>

    ![Agregar empleado](./media/active-directory-saas-jiramicrosoft-tutorial/user3.png) 

5. <span data-ttu-id="3df09-271">En la página del cuadro de diálogo **"Create New User"** (Crear nuevo usuario), realice los pasos siguientes:</span><span class="sxs-lookup"><span data-stu-id="3df09-271">On the **“Create new user”** dialog page, perform the following steps:</span></span>

    ![Agregar empleado](./media/active-directory-saas-jiramicrosoft-tutorial/user4.png) 

    <span data-ttu-id="3df09-273">a.</span><span class="sxs-lookup"><span data-stu-id="3df09-273">a.</span></span> <span data-ttu-id="3df09-274">En el cuadro de texto **Dirección de correo electrónico**, escriba la dirección de correo electrónico de un usuario, por ejemplo, Brittasimon@contoso.com.</span><span class="sxs-lookup"><span data-stu-id="3df09-274">In the **Email address** textbox, type the email address of user like Brittasimon@contoso.com.</span></span>

    <span data-ttu-id="3df09-275">b.</span><span class="sxs-lookup"><span data-stu-id="3df09-275">b.</span></span> <span data-ttu-id="3df09-276">En el cuadro de texto **Nombre completo**, escriba el nombre completo de un usuario, por ejemplo, Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="3df09-276">In the **Full Name** textbox, type full name of the user like Britta Simon.</span></span>

    <span data-ttu-id="3df09-277">c.</span><span class="sxs-lookup"><span data-stu-id="3df09-277">c.</span></span> <span data-ttu-id="3df09-278">En el cuadro de texto **Nombre de usuario**, escriba el correo electrónico de un usuario, por ejemplo, Brittasimon@contoso.com.</span><span class="sxs-lookup"><span data-stu-id="3df09-278">In the **Username** textbox, type the email of user like Brittasimon@contoso.com.</span></span>

    <span data-ttu-id="3df09-279">d.</span><span class="sxs-lookup"><span data-stu-id="3df09-279">d.</span></span> <span data-ttu-id="3df09-280">En el cuadro de texto **Contraseña**, escriba la contraseña del usuario.</span><span class="sxs-lookup"><span data-stu-id="3df09-280">In the **Password** textbox, type the password of user.</span></span>

    <span data-ttu-id="3df09-281">e.</span><span class="sxs-lookup"><span data-stu-id="3df09-281">e.</span></span> <span data-ttu-id="3df09-282">Haga clic en **Crear usuario**.</span><span class="sxs-lookup"><span data-stu-id="3df09-282">Click **Create user**.</span></span>   

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="3df09-283">Asignación del usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="3df09-283">Assigning the Azure AD test user</span></span>

<span data-ttu-id="3df09-284">En esta sección, habilitará a Britta Simon para que use el inicio de sesión único de Azure concediéndole acceso a JIRA SAML SSO by Microsoft.</span><span class="sxs-lookup"><span data-stu-id="3df09-284">In this section, you enable Britta Simon to use Azure single sign-on by granting access to JIRA SAML SSO by Microsoft.</span></span>

![Asignar usuario][200] 

<span data-ttu-id="3df09-286">**Para asignar a Britta Simon a JIRA SAML SSO by Microsoft, siga estos pasos:**</span><span class="sxs-lookup"><span data-stu-id="3df09-286">**To assign Britta Simon to JIRA SAML SSO by Microsoft, perform the following steps:**</span></span>

1. <span data-ttu-id="3df09-287">En Azure Portal, abra la vista de aplicaciones, vaya a la vista de directorio y vaya a **Aplicaciones empresariales**. Luego, haga clic en **Todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="3df09-287">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Asignar usuario][201] 

2. <span data-ttu-id="3df09-289">En la lista de aplicaciones, seleccione **JIRA SAML SSO by Microsoft**.</span><span class="sxs-lookup"><span data-stu-id="3df09-289">In the applications list, select **JIRA SAML SSO by Microsoft**.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-jiramicrosoft-tutorial/tutorial_jiramicrosoft_app.png) 

3. <span data-ttu-id="3df09-291">En el menú de la izquierda, haga clic en **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="3df09-291">In the menu on the left, click **Users and groups**.</span></span>

    ![Asignar usuario][202] 

4. <span data-ttu-id="3df09-293">Haga clic en el botón **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="3df09-293">Click **Add** button.</span></span> <span data-ttu-id="3df09-294">Después, seleccione **Usuarios y grupos** en el cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="3df09-294">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Asignar usuario][203]

5. <span data-ttu-id="3df09-296">En el cuadro de diálogo **Usuarios y grupos**, seleccione **Britta Simon** en la lista de usuarios.</span><span class="sxs-lookup"><span data-stu-id="3df09-296">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="3df09-297">Haga clic en el botón **Seleccionar** del cuadro de diálogo **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="3df09-297">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="3df09-298">Haga clic en el botón **Asignar** del cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="3df09-298">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="3df09-299">Prueba del inicio de sesión único </span><span class="sxs-lookup"><span data-stu-id="3df09-299">Testing single sign-on</span></span>

<span data-ttu-id="3df09-300">En esta sección, probará la configuración de inicio de sesión único de Azure AD mediante el Panel de acceso.</span><span class="sxs-lookup"><span data-stu-id="3df09-300">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="3df09-301">Al hacer clic en el icono de JIRA SAML SSO by Microsoft en el Panel de acceso, debería iniciar sesión automáticamente en la aplicación JIRA SAML SSO by Microsoft.</span><span class="sxs-lookup"><span data-stu-id="3df09-301">When you click the JIRA SAML SSO by Microsoft tile in the Access Panel, you should get automatically signed-on to your JIRA SAML SSO by Microsoft application.</span></span>
<span data-ttu-id="3df09-302">Para más información sobre el Panel de acceso, consulte [Introducción al Panel de acceso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="3df09-302">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="3df09-303">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="3df09-303">Additional resources</span></span>

* [<span data-ttu-id="3df09-304">Lista de tutoriales sobre cómo integrar aplicaciones SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="3df09-304">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="3df09-305">¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="3df09-305">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-jiramicrosoft-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-jiramicrosoft-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-jiramicrosoft-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-jiramicrosoft-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-jiramicrosoft-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-jiramicrosoft-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-jiramicrosoft-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-jiramicrosoft-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-jiramicrosoft-tutorial/tutorial_general_203.png

