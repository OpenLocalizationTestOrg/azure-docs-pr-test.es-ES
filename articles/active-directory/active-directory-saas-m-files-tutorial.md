---
title: "Tutorial: integración de Azure Active Directory con M-Files | Microsoft Docs"
description: "Obtenga información acerca de cómo tooconfigure inicio de sesión único entre Azure Active Directory y millones de archivos."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 4536fd49-3a65-4cff-9620-860904f726d0
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/28/2017
ms.author: jeedes
ms.openlocfilehash: e1d268da53312b1d2c12e29d66b1a5b66d0cdcce
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-m-files"></a><span data-ttu-id="d75cc-103">Tutorial: integración de Azure Active Directory con M-Files</span><span class="sxs-lookup"><span data-stu-id="d75cc-103">Tutorial: Azure Active Directory integration with M-Files</span></span>

<span data-ttu-id="d75cc-104">En este tutorial, aprenderá cómo toointegrate millones de archivos con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="d75cc-104">In this tutorial, you learn how toointegrate M-Files with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="d75cc-105">Integración de millones de archivos con Azure AD proporciona Hola siguientes ventajas:</span><span class="sxs-lookup"><span data-stu-id="d75cc-105">Integrating M-Files with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="d75cc-106">Puede controlar en Azure AD que tenga acceso tooM-archivos</span><span class="sxs-lookup"><span data-stu-id="d75cc-106">You can control in Azure AD who has access tooM-Files</span></span>
- <span data-ttu-id="d75cc-107">Puede habilitar los usuarios tooautomatically get ha iniciado sesión tooM-archivos (Single Sign-On) con sus cuentas de Azure AD</span><span class="sxs-lookup"><span data-stu-id="d75cc-107">You can enable your users tooautomatically get signed-on tooM-Files (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="d75cc-108">Puede administrar las cuentas en una ubicación central: Hola portal de Azure</span><span class="sxs-lookup"><span data-stu-id="d75cc-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="d75cc-109">Si desea obtener más información acerca de la integración de aplicaciones de SaaS con Azure AD tooknow, consulte [¿qué es acceso a la aplicación y el inicio de sesión único con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="d75cc-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="d75cc-110">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="d75cc-110">Prerequisites</span></span>

<span data-ttu-id="d75cc-111">tooconfigure integración de Azure AD con millones de archivos, deberá Hola siguientes elementos:</span><span class="sxs-lookup"><span data-stu-id="d75cc-111">tooconfigure Azure AD integration with M-Files, you need hello following items:</span></span>

- <span data-ttu-id="d75cc-112">Una suscripción de Azure AD</span><span class="sxs-lookup"><span data-stu-id="d75cc-112">An Azure AD subscription</span></span>
- <span data-ttu-id="d75cc-113">Una suscripción habilitada para el inicio de sesión único en M-Files</span><span class="sxs-lookup"><span data-stu-id="d75cc-113">A M-Files single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="d75cc-114">Hola tootest los pasos de este tutorial, no se recomienda usar un entorno de producción.</span><span class="sxs-lookup"><span data-stu-id="d75cc-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="d75cc-115">pasos de hello tootest en este tutorial, debe seguir estas recomendaciones:</span><span class="sxs-lookup"><span data-stu-id="d75cc-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="d75cc-116">No use el entorno de producción, salvo que sea necesario.</span><span class="sxs-lookup"><span data-stu-id="d75cc-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="d75cc-117">Si no dispone de un entorno de prueba de Azure AD, puede obtener una versión de prueba de un mes [aquí](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="d75cc-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="d75cc-118">Descripción del escenario</span><span class="sxs-lookup"><span data-stu-id="d75cc-118">Scenario description</span></span>
<span data-ttu-id="d75cc-119">En este tutorial, puede probar el inicio de sesión único de Azure AD en un entorno de prueba.</span><span class="sxs-lookup"><span data-stu-id="d75cc-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="d75cc-120">escenario de Hello descrito en este tutorial consta de dos bloques principales:</span><span class="sxs-lookup"><span data-stu-id="d75cc-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="d75cc-121">Agregar archivos de M desde galería Hola</span><span class="sxs-lookup"><span data-stu-id="d75cc-121">Adding M-Files from hello gallery</span></span>
2. <span data-ttu-id="d75cc-122">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="d75cc-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-m-files-from-hello-gallery"></a><span data-ttu-id="d75cc-123">Agregar archivos de M desde galería Hola</span><span class="sxs-lookup"><span data-stu-id="d75cc-123">Adding M-Files from hello gallery</span></span>
<span data-ttu-id="d75cc-124">integración de hello tooconfigure archivos-M en Azure AD, deberá tooadd millones de archivos de lista de tooyour Hola Galería de aplicaciones administradas de SaaS.</span><span class="sxs-lookup"><span data-stu-id="d75cc-124">tooconfigure hello integration of M-Files into Azure AD, you need tooadd M-Files from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="d75cc-125">**tooadd millones de archivos de la Galería de hello, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="d75cc-125">**tooadd M-Files from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="d75cc-126">Hola  **[portal de Azure](https://portal.azure.com)**, en el panel de navegación izquierdo de Hola, haga clic en **Azure Active Directory** icono.</span><span class="sxs-lookup"><span data-stu-id="d75cc-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="d75cc-128">Navegue demasiado**aplicaciones empresariales**.</span><span class="sxs-lookup"><span data-stu-id="d75cc-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="d75cc-129">A continuación, vaya demasiado**todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="d75cc-129">Then go too**All applications**.</span></span>

    ![Aplicaciones][2]
    
3. <span data-ttu-id="d75cc-131">tooadd nueva aplicación, haga clic en **nueva aplicación** botón en la parte superior de saludo del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="d75cc-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Aplicaciones][3]

4. <span data-ttu-id="d75cc-133">En el cuadro de búsqueda de hello, escriba **archivos M**.</span><span class="sxs-lookup"><span data-stu-id="d75cc-133">In hello search box, type **M-Files**.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-m-files-tutorial/tutorial_m-files_search.png)

5. <span data-ttu-id="d75cc-135">En el panel de resultados de hello, seleccione **archivos M**y, a continuación, haga clic en **agregar** botón aplicación hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="d75cc-135">In hello results panel, select **M-Files**, and then click **Add** button tooadd hello application.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-m-files-tutorial/tutorial_m-files_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="d75cc-137">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="d75cc-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="d75cc-138">En esta sección, se configura y prueba el inicio de sesión único de Azure AD con M-Files con un usuario de prueba llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="d75cc-138">In this section, you configure and test Azure AD single sign-on with M-Files based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="d75cc-139">Para toowork de inicio de sesión único, Azure AD necesita tooknow qué usuario equivalente de hello en archivos de M es tooa usuario en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="d75cc-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in M-Files is tooa user in Azure AD.</span></span> <span data-ttu-id="d75cc-140">En otras palabras, una relación de vínculo entre un usuario de Azure AD y el usuario relacionado de hello en archivos de M debe toobe establecido.</span><span class="sxs-lookup"><span data-stu-id="d75cc-140">In other words, a link relationship between an Azure AD user and hello related user in M-Files needs toobe established.</span></span>

<span data-ttu-id="d75cc-141">En archivos de M, asigne el valor de Hola de hello **nombre de usuario** en Azure AD como valor de Hola de hello **nombre de usuario** tooestablish la relación de vínculo de Hola.</span><span class="sxs-lookup"><span data-stu-id="d75cc-141">In M-Files, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="d75cc-142">tooconfigure y prueba de inicio de sesión único en Azure AD con millones de archivos, deberá hello toocomplete después de bloques de creación:</span><span class="sxs-lookup"><span data-stu-id="d75cc-142">tooconfigure and test Azure AD single sign-on with M-Files, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="d75cc-143">**[Configuración de Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable la toouse usuarios esta característica.</span><span class="sxs-lookup"><span data-stu-id="d75cc-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="d75cc-144">**[Crear un usuario de prueba de Azure AD](#creating-an-azure-ad-test-user)**  -inicio de sesión único en Azure AD tootest con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="d75cc-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="d75cc-145">**[Crear un usuario de prueba de millones de archivos](#creating-a-m-files-test-user)**  -toohave un equivalente de Britta Simon en millones de archivos que está vinculado toohello Azure AD representación del usuario.</span><span class="sxs-lookup"><span data-stu-id="d75cc-145">**[Creating a M-Files test user](#creating-a-m-files-test-user)** - toohave a counterpart of Britta Simon in M-Files that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="d75cc-146">**[Asignar usuario de prueba de hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="d75cc-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="d75cc-147">**[Pruebas de Single Sign-On](#testing-single-sign-on)**  -tooverify Hola si funciona la configuración.</span><span class="sxs-lookup"><span data-stu-id="d75cc-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="d75cc-148">Configuración del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="d75cc-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="d75cc-149">En esta sección, habilitar inicio de sesión único en Azure AD en hello portal de Azure y configurar el inicio de sesión único en la aplicación de millones de archivos.</span><span class="sxs-lookup"><span data-stu-id="d75cc-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your M-Files application.</span></span>

<span data-ttu-id="d75cc-150">**inicio de sesión único en tooconfigure Azure AD con archivos de M, realizar Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="d75cc-150">**tooconfigure Azure AD single sign-on with M-Files, perform hello following steps:**</span></span>

1. <span data-ttu-id="d75cc-151">En el portal de Azure, en Hola Hola **archivos M** página de integración de aplicaciones, haga clic en **inicio de sesión único**.</span><span class="sxs-lookup"><span data-stu-id="d75cc-151">In hello Azure portal, on hello **M-Files** application integration page, click **Single sign-on**.</span></span>

    ![Configurar inicio de sesión único][4]

2. <span data-ttu-id="d75cc-153">En hello **inicio de sesión único** cuadro de diálogo, seleccione **modo** como **sesión basado en SAML** tooenable inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="d75cc-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurar inicio de sesión único](./media/active-directory-saas-m-files-tutorial/tutorial_m-files_samlbase.png)

3. <span data-ttu-id="d75cc-155">En hello **dominio millones de archivos y las direcciones URL** sección, lleve a cabo Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="d75cc-155">On hello **M-Files Domain and URLs** section, perform hello following steps:</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-m-files-tutorial/tutorial_m-files_url.png)

    <span data-ttu-id="d75cc-157">a.</span><span class="sxs-lookup"><span data-stu-id="d75cc-157">a.</span></span> <span data-ttu-id="d75cc-158">Hola **dirección URL de inicio de sesión** cuadro de texto, escriba una dirección URL usando Hola siguiente patrón:`https://<tenantname>.cloudvault.m-files.com/authentication/MFiles.AuthenticationProviders.Core/sso`</span><span class="sxs-lookup"><span data-stu-id="d75cc-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<tenantname>.cloudvault.m-files.com/authentication/MFiles.AuthenticationProviders.Core/sso`</span></span>

    <span data-ttu-id="d75cc-159">b.</span><span class="sxs-lookup"><span data-stu-id="d75cc-159">b.</span></span> <span data-ttu-id="d75cc-160">Hola **identificador** cuadro de texto, escriba una dirección URL usando Hola siguiente patrón:`https://<tenantname>.cloudvault.m-files.com`</span><span class="sxs-lookup"><span data-stu-id="d75cc-160">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<tenantname>.cloudvault.m-files.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="d75cc-161">Estos valores no son reales.</span><span class="sxs-lookup"><span data-stu-id="d75cc-161">These values are not real.</span></span> <span data-ttu-id="d75cc-162">Actualizar estos valores con hello real de dirección URL de inicio de sesión y el identificador.</span><span class="sxs-lookup"><span data-stu-id="d75cc-162">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="d75cc-163">Póngase en contacto con [equipo de soporte técnico de cliente de millones de archivos](mailto:support@m-files.com) tooget estos valores.</span><span class="sxs-lookup"><span data-stu-id="d75cc-163">Contact [M-Files Client support team](mailto:support@m-files.com) tooget these values.</span></span> 
 
4. <span data-ttu-id="d75cc-164">En hello **el certificado de firma de SAML** sección, haga clic en **Metadata XML** y, a continuación, guarde el archivo de metadatos de hello en el equipo.</span><span class="sxs-lookup"><span data-stu-id="d75cc-164">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-m-files-tutorial/tutorial_m-files_certificate.png) 

5. <span data-ttu-id="d75cc-166">Haga clic en el botón **Guardar** .</span><span class="sxs-lookup"><span data-stu-id="d75cc-166">Click **Save** button.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-m-files-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="d75cc-168">tooget SSO configurado para la aplicación, póngase en contacto con [equipo de soporte técnico archivos M](mailto:support@m-files.com) y proporcióneles Hola descarga metadatos.</span><span class="sxs-lookup"><span data-stu-id="d75cc-168">tooget SSO configured for your application, contact [M-Files support team](mailto:support@m-files.com) and provide them hello downloaded Metadata.</span></span>
   
    >[!NOTE]
    ><span data-ttu-id="d75cc-169">Siga los pasos de hello si desea tooconfigure SSO para su aplicación de escritorio de M-File.</span><span class="sxs-lookup"><span data-stu-id="d75cc-169">Follow hello next steps if you want tooconfigure SSO for you M-File desktop application.</span></span> <span data-ttu-id="d75cc-170">Ningún paso adicional es necesario si solo desea tooconfigure SSO para la versión de web de millones de archivos.</span><span class="sxs-lookup"><span data-stu-id="d75cc-170">No extra steps are required if you only want tooconfigure SSO for M-Files web version.</span></span>  

7. <span data-ttu-id="d75cc-171">Siga Hola siguiente pasos tooconfigure Hola M archivo aplicación de escritorio tooenable SSO con Azure AD.</span><span class="sxs-lookup"><span data-stu-id="d75cc-171">Follow hello next steps tooconfigure hello M-File desktop application tooenable SSO with Azure AD.</span></span> <span data-ttu-id="d75cc-172">toodownload M-Files, vaya demasiado[descargarán archivos M](https://www.m-files.com/en/download-latest-version) página.</span><span class="sxs-lookup"><span data-stu-id="d75cc-172">toodownload M-Files, go too[M-Files download](https://www.m-files.com/en/download-latest-version) page.</span></span>

8. <span data-ttu-id="d75cc-173">Abra hello **configuración de escritorio de millones de archivos** ventana.</span><span class="sxs-lookup"><span data-stu-id="d75cc-173">Open hello **M-Files Desktop Settings** window.</span></span> <span data-ttu-id="d75cc-174">A continuación, haga clic en **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="d75cc-174">Then, click **Add**.</span></span>
   
    ![Configurar inicio de sesión único](./media/active-directory-saas-m-files-tutorial/tutorial_m_files_10.png)

9. <span data-ttu-id="d75cc-176">En hello **propiedades de conexión de almacén de documento** ventana, realizar Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="d75cc-176">On hello **Document Vault Connection Properties** window, perform hello following steps:</span></span>
   
    ![Configurar inicio de sesión único](./media/active-directory-saas-m-files-tutorial/tutorial_m_files_11.png)  

    <span data-ttu-id="d75cc-178">En hello tipo de sección de servidor, Hola valores como se indica a continuación:</span><span class="sxs-lookup"><span data-stu-id="d75cc-178">Under hello Server section type, hello values as follows:</span></span>  

    <span data-ttu-id="d75cc-179">a.</span><span class="sxs-lookup"><span data-stu-id="d75cc-179">a.</span></span> <span data-ttu-id="d75cc-180">En **Name** (Nombre), escriba `<tenant-name>.cloudvault.m-files.com`.</span><span class="sxs-lookup"><span data-stu-id="d75cc-180">For **Name**, type `<tenant-name>.cloudvault.m-files.com`.</span></span> 
 
    <span data-ttu-id="d75cc-181">b.</span><span class="sxs-lookup"><span data-stu-id="d75cc-181">b.</span></span> <span data-ttu-id="d75cc-182">En **Port Number** (Número de puerto), escriba **4466**.</span><span class="sxs-lookup"><span data-stu-id="d75cc-182">For **Port Number**, type **4466**.</span></span> 

    <span data-ttu-id="d75cc-183">c.</span><span class="sxs-lookup"><span data-stu-id="d75cc-183">c.</span></span> <span data-ttu-id="d75cc-184">En **Protocol** (Protocolo), seleccione **HTTPS**.</span><span class="sxs-lookup"><span data-stu-id="d75cc-184">For **Protocol**, select **HTTPS**.</span></span> 

    <span data-ttu-id="d75cc-185">d.</span><span class="sxs-lookup"><span data-stu-id="d75cc-185">d.</span></span> <span data-ttu-id="d75cc-186">Hola **autenticación** campo, seleccione **usuario específicos de Windows**.</span><span class="sxs-lookup"><span data-stu-id="d75cc-186">In hello **Authentication** field, select **Specific Windows user**.</span></span> <span data-ttu-id="d75cc-187">Luego, se le solicitará una página de inicio de sesión.</span><span class="sxs-lookup"><span data-stu-id="d75cc-187">Then, you are prompted with a signing page.</span></span> <span data-ttu-id="d75cc-188">Escriba sus credenciales de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="d75cc-188">Insert your Azure AD credentials.</span></span> 

    <span data-ttu-id="d75cc-189">e.</span><span class="sxs-lookup"><span data-stu-id="d75cc-189">e.</span></span> <span data-ttu-id="d75cc-190">Para hello **almacén en servidor**, seleccione Hola almacén correspondiente en el servidor.</span><span class="sxs-lookup"><span data-stu-id="d75cc-190">For hello **Vault on Server**,  select hello corresponding vault on server.</span></span>
 
    <span data-ttu-id="d75cc-191">f.</span><span class="sxs-lookup"><span data-stu-id="d75cc-191">f.</span></span> <span data-ttu-id="d75cc-192">Haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="d75cc-192">Click **OK**.</span></span>

> [!TIP]
> <span data-ttu-id="d75cc-193">Ahora puede leer una versión concisa de estas instrucciones dentro de hello [portal de Azure](https://portal.azure.com), mientras que está configurando la aplicación hello!</span><span class="sxs-lookup"><span data-stu-id="d75cc-193">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="d75cc-194">Después de agregar esta aplicación de hello **Active Directory > aplicaciones empresariales** sección, simplemente haga clic en hello **Single Sign-On** Hola de pestaña y acceso incrustado documentación a través de hello  **Configuración** sección final Hola.</span><span class="sxs-lookup"><span data-stu-id="d75cc-194">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="d75cc-195">Puede leer más acerca de características de documentación de embedded Hola aquí: [Azure AD incrustado documentación]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="d75cc-195">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="d75cc-196">Creación de un usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="d75cc-196">Creating an Azure AD test user</span></span>
<span data-ttu-id="d75cc-197">objetivo de Hola de esta sección es un usuario de prueba en hello Azure portal llamado a Britta Simon toocreate.</span><span class="sxs-lookup"><span data-stu-id="d75cc-197">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Creación de un usuario de Azure AD][100]

<span data-ttu-id="d75cc-199">**toocreate un usuario de prueba en Azure AD, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="d75cc-199">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="d75cc-200">Hola **portal de Azure**, en Hola panel de navegación izquierdo, haga clic en **Azure Active Directory** icono.</span><span class="sxs-lookup"><span data-stu-id="d75cc-200">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-m-files-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="d75cc-202">lista de hello toodisplay de usuarios, vaya demasiado**usuarios y grupos** y haga clic en **todos los usuarios**.</span><span class="sxs-lookup"><span data-stu-id="d75cc-202">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-m-files-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="d75cc-204">Hola tooopen **usuario** cuadro de diálogo, haga clic en **agregar** en la parte superior de saludo del cuadro de diálogo de Hola.</span><span class="sxs-lookup"><span data-stu-id="d75cc-204">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-m-files-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="d75cc-206">En hello **usuario** cuadro de diálogo, siga los pasos de hello:</span><span class="sxs-lookup"><span data-stu-id="d75cc-206">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-m-files-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="d75cc-208">a.</span><span class="sxs-lookup"><span data-stu-id="d75cc-208">a.</span></span> <span data-ttu-id="d75cc-209">Hola **nombre** cuadro de texto, tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="d75cc-209">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="d75cc-210">b.</span><span class="sxs-lookup"><span data-stu-id="d75cc-210">b.</span></span> <span data-ttu-id="d75cc-211">Hola **nombre de usuario** cuadro de texto, hello tipo **dirección de correo electrónico** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="d75cc-211">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="d75cc-212">c.</span><span class="sxs-lookup"><span data-stu-id="d75cc-212">c.</span></span> <span data-ttu-id="d75cc-213">Seleccione **Mostrar contraseña** y anote el valor de Hola de hello **contraseña**.</span><span class="sxs-lookup"><span data-stu-id="d75cc-213">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="d75cc-214">d.</span><span class="sxs-lookup"><span data-stu-id="d75cc-214">d.</span></span> <span data-ttu-id="d75cc-215">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="d75cc-215">Click **Create**.</span></span>
 
### <a name="creating-a-m-files-test-user"></a><span data-ttu-id="d75cc-216">Creación de un usuario de prueba en M-Files</span><span class="sxs-lookup"><span data-stu-id="d75cc-216">Creating a M-Files test user</span></span>

<span data-ttu-id="d75cc-217">objetivo de Hola de esta sección es toocreate un usuario llamado a Britta Simon en millones de archivos.</span><span class="sxs-lookup"><span data-stu-id="d75cc-217">hello objective of this section is toocreate a user called Britta Simon in M-Files.</span></span> <span data-ttu-id="d75cc-218">Trabajar con [equipo de soporte técnico archivos M](mailto:support@m-files.com) a los usuarios de tooadd Hola Hola millones de archivos.</span><span class="sxs-lookup"><span data-stu-id="d75cc-218">Work with  [M-Files support team](mailto:support@m-files.com) tooadd hello users in hello M-Files.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="d75cc-219">Asignación de usuario de prueba de hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="d75cc-219">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="d75cc-220">En esta sección, se habilita Britta Simon toouse un inicio de sesión único Azure concediendo acceso tooM-Files.</span><span class="sxs-lookup"><span data-stu-id="d75cc-220">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooM-Files.</span></span>

![Asignar usuario][200] 

<span data-ttu-id="d75cc-222">**tooassign Britta Simon tooM-Files, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="d75cc-222">**tooassign Britta Simon tooM-Files, perform hello following steps:**</span></span>

1. <span data-ttu-id="d75cc-223">Hola portal de Azure, abra la vista de aplicaciones de hello y, a continuación, navegue a vista de directorio toohello y vaya demasiado**aplicaciones empresariales** , a continuación, haga clic en **todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="d75cc-223">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Asignar usuario][201] 

2. <span data-ttu-id="d75cc-225">En la lista de aplicaciones de hello, seleccione **archivos M**.</span><span class="sxs-lookup"><span data-stu-id="d75cc-225">In hello applications list, select **M-Files**.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-m-files-tutorial/tutorial_m-files_app.png) 

3. <span data-ttu-id="d75cc-227">En el menú de Hola Hola izquierda, haga clic en **usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="d75cc-227">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Asignar usuario][202] 

4. <span data-ttu-id="d75cc-229">Haga clic en el botón **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="d75cc-229">Click **Add** button.</span></span> <span data-ttu-id="d75cc-230">Después, seleccione **Usuarios y grupos** en el cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="d75cc-230">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Asignar usuario][203]

5. <span data-ttu-id="d75cc-232">En **usuarios y grupos** cuadro de diálogo, seleccione **Britta Simon** en la lista de usuarios de Hola.</span><span class="sxs-lookup"><span data-stu-id="d75cc-232">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="d75cc-233">Haga clic en el botón **Seleccionar** del cuadro de diálogo **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="d75cc-233">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="d75cc-234">Haga clic en el botón **Asignar** del cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="d75cc-234">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="d75cc-235">Prueba del inicio de sesión único </span><span class="sxs-lookup"><span data-stu-id="d75cc-235">Testing single sign-on</span></span>

<span data-ttu-id="d75cc-236">objetivo de Hola de esta sección es tootest la configuración de SSO de Azure AD mediante Hola Panel de acceso.</span><span class="sxs-lookup"><span data-stu-id="d75cc-236">hello objective of this section is tootest your Azure AD SSO configuration using hello Access Panel.</span></span>

<span data-ttu-id="d75cc-237">Al hacer clic en hello M archivos disponer en mosaico en hello Panel de acceso, deberá obtener la aplicación automáticamente ha iniciado sesión tooyour millones de archivos.</span><span class="sxs-lookup"><span data-stu-id="d75cc-237">When you click hello M-Files tile in hello Access Panel, you should get automatically signed-on tooyour M-Files application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="d75cc-238">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="d75cc-238">Additional resources</span></span>

* [<span data-ttu-id="d75cc-239">Lista de tutoriales sobre cómo tooIntegrate aplicaciones de SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="d75cc-239">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="d75cc-240">¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="d75cc-240">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-m-files-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-m-files-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-m-files-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-m-files-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-m-files-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-m-files-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-m-files-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-m-files-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-m-files-tutorial/tutorial_general_203.png

