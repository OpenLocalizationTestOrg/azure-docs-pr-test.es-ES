---
title: "Tutorial: Integración de Azure Active Directory con Salesforce Sandbox | Microsoft Docs"
description: "Obtenga información acerca de cómo tooconfigure inicio de sesión único entre Azure Active Directory y el espacio aislado de Salesforce."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: ee54c39e-ce20-42a4-8531-da7b5f40f57c
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/19/2017
ms.author: jeedes
ms.openlocfilehash: 7539f08356568a17ebfcee2764bbbefa129b0553
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-salesforce-sandbox"></a><span data-ttu-id="0cc23-103">Tutorial: Integración de Azure Active Directory con Salesforce Sandbox</span><span class="sxs-lookup"><span data-stu-id="0cc23-103">Tutorial: Azure Active Directory integration with Salesforce Sandbox</span></span>

<span data-ttu-id="0cc23-104">En este tutorial, aprenderá cómo toointegrate espacio aislado de Salesforce con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="0cc23-104">In this tutorial, you learn how toointegrate Salesforce Sandbox with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="0cc23-105">Integración de Salesforce Sandbox con Azure AD proporciona Hola siguientes ventajas:</span><span class="sxs-lookup"><span data-stu-id="0cc23-105">Integrating Salesforce Sandbox with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="0cc23-106">Puede controlar en Azure AD que tenga acceso tooSalesforce espacio aislado</span><span class="sxs-lookup"><span data-stu-id="0cc23-106">You can control in Azure AD who has access tooSalesforce Sandbox</span></span>
- <span data-ttu-id="0cc23-107">Puede habilitar los usuarios tooautomatically get ha iniciado sesión tooSalesforce espacio aislado (Single Sign-On) con sus cuentas de Azure AD</span><span class="sxs-lookup"><span data-stu-id="0cc23-107">You can enable your users tooautomatically get signed-on tooSalesforce Sandbox (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="0cc23-108">Puede administrar las cuentas en una ubicación central: Hola portal de Azure</span><span class="sxs-lookup"><span data-stu-id="0cc23-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="0cc23-109">Si desea obtener más información acerca de la integración de aplicaciones de SaaS con Azure AD tooknow, consulte [¿qué es acceso a la aplicación y el inicio de sesión único con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="0cc23-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="0cc23-110">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="0cc23-110">Prerequisites</span></span>

<span data-ttu-id="0cc23-111">integración de Azure AD con Salesforce Sandbox tooconfigure, necesita Hola siguientes elementos:</span><span class="sxs-lookup"><span data-stu-id="0cc23-111">tooconfigure Azure AD integration with Salesforce Sandbox, you need hello following items:</span></span>

- <span data-ttu-id="0cc23-112">Una suscripción de Azure AD</span><span class="sxs-lookup"><span data-stu-id="0cc23-112">An Azure AD subscription</span></span>
- <span data-ttu-id="0cc23-113">Una suscripción habilitada para el inicio de sesión único en Salesforce Sandbox</span><span class="sxs-lookup"><span data-stu-id="0cc23-113">A Salesforce Sandbox single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="0cc23-114">Hola tootest los pasos de este tutorial, no se recomienda usar un entorno de producción.</span><span class="sxs-lookup"><span data-stu-id="0cc23-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="0cc23-115">pasos de hello tootest en este tutorial, debe seguir estas recomendaciones:</span><span class="sxs-lookup"><span data-stu-id="0cc23-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="0cc23-116">No use el entorno de producción, salvo que sea necesario.</span><span class="sxs-lookup"><span data-stu-id="0cc23-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="0cc23-117">Si no dispone de un entorno de prueba de Azure AD, puede obtener una versión de prueba de un mes [aquí](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="0cc23-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="0cc23-118">Descripción del escenario</span><span class="sxs-lookup"><span data-stu-id="0cc23-118">Scenario description</span></span>
<span data-ttu-id="0cc23-119">En este tutorial, puede probar el inicio de sesión único de Azure AD en un entorno de prueba.</span><span class="sxs-lookup"><span data-stu-id="0cc23-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="0cc23-120">escenario de Hello descrito en este tutorial consta de dos bloques principales:</span><span class="sxs-lookup"><span data-stu-id="0cc23-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="0cc23-121">Agregar espacio aislado de Salesforce desde la Galería de Hola</span><span class="sxs-lookup"><span data-stu-id="0cc23-121">Adding Salesforce Sandbox from hello gallery</span></span>
2. <span data-ttu-id="0cc23-122">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="0cc23-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-salesforce-sandbox-from-hello-gallery"></a><span data-ttu-id="0cc23-123">Agregar espacio aislado de Salesforce desde la Galería de Hola</span><span class="sxs-lookup"><span data-stu-id="0cc23-123">Adding Salesforce Sandbox from hello gallery</span></span>
<span data-ttu-id="0cc23-124">integración de hello tooconfigure de espacio aislado de Salesforce en Azure AD, necesita tooadd espacio aislado de Salesforce en lista de tooyour Hola Galería de aplicaciones administradas de SaaS.</span><span class="sxs-lookup"><span data-stu-id="0cc23-124">tooconfigure hello integration of Salesforce Sandbox into Azure AD, you need tooadd Salesforce Sandbox from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="0cc23-125">**tooadd Salesforce Sandbox de galería de hello, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="0cc23-125">**tooadd Salesforce Sandbox from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="0cc23-126">Hola  **[portal de Azure](https://portal.azure.com)**, en el panel de navegación izquierdo de Hola, haga clic en **Azure Active Directory** icono.</span><span class="sxs-lookup"><span data-stu-id="0cc23-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="0cc23-128">Navegue demasiado**aplicaciones empresariales**.</span><span class="sxs-lookup"><span data-stu-id="0cc23-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="0cc23-129">A continuación, vaya demasiado**todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="0cc23-129">Then go too**All applications**.</span></span>

    ![Aplicaciones][2]
    
3. <span data-ttu-id="0cc23-131">Haga clic en **nueva aplicación** botón en la parte superior de saludo del cuadro de diálogo de Hola.</span><span class="sxs-lookup"><span data-stu-id="0cc23-131">Click **New application** button on hello top of hello dialog.</span></span>

    ![Aplicaciones][3]

4. <span data-ttu-id="0cc23-133">En el cuadro de búsqueda de hello, escriba **Salesforce Sandbox**.</span><span class="sxs-lookup"><span data-stu-id="0cc23-133">In hello search box, type **Salesforce Sandbox**.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-salesforcesandbox-tutorial/tutorial_salesforcesandbox_search.png)

5. <span data-ttu-id="0cc23-135">En el panel de resultados de hello, seleccione **Salesforce Sandbox**y, a continuación, haga clic en **agregar** botón aplicación hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="0cc23-135">In hello results panel, select **Salesforce Sandbox**, and then click **Add** button tooadd hello application.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-salesforcesandbox-tutorial/tutorial_salesforcesandbox_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="0cc23-137">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="0cc23-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="0cc23-138">En esta sección, podrá configurar y probar el inicio de sesión único de Azure AD con Salesforce Sandbox con un usuario de prueba llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="0cc23-138">In this section, you configure and test Azure AD single sign-on with Salesforce Sandbox based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="0cc23-139">Para toowork de inicio de sesión único, Azure AD necesita tooknow qué usuario equivalente de hello en espacio aislado de Salesforce es tooa usuario en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="0cc23-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Salesforce Sandbox is tooa user in Azure AD.</span></span> <span data-ttu-id="0cc23-140">En otras palabras, una relación de vínculo entre un usuario de Azure AD y el usuario relacionado de hello en espacio aislado de Salesforce debe toobe establecido.</span><span class="sxs-lookup"><span data-stu-id="0cc23-140">In other words, a link relationship between an Azure AD user and hello related user in Salesforce Sandbox needs toobe established.</span></span>

<span data-ttu-id="0cc23-141">Esta relación de vínculo se establece mediante la asignación de valor de Hola de hello **nombre de usuario** en Azure AD como valor de Hola de hello **nombre de usuario** en espacio aislado de Salesforce.</span><span class="sxs-lookup"><span data-stu-id="0cc23-141">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in Salesforce Sandbox.</span></span>

<span data-ttu-id="0cc23-142">tooconfigure y prueba de inicio de sesión único en Azure AD con Salesforce Sandbox, deberá hello toocomplete después de bloques de creación:</span><span class="sxs-lookup"><span data-stu-id="0cc23-142">tooconfigure and test Azure AD single sign-on with Salesforce Sandbox, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="0cc23-143">**[Configuración de Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable la toouse usuarios esta característica.</span><span class="sxs-lookup"><span data-stu-id="0cc23-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="0cc23-144">**[Crear un usuario de prueba de Azure AD](#creating-an-azure-ad-test-user)**  -inicio de sesión único en Azure AD tootest con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="0cc23-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="0cc23-145">**[Crear un usuario de prueba de Salesforce Sandbox](#creating-a-salesforce-sandbox-test-user)**  -toohave un equivalente de Britta Simon en espacio aislado de Salesforce es representación toohello vinculado Azure AD del usuario.</span><span class="sxs-lookup"><span data-stu-id="0cc23-145">**[Creating a Salesforce Sandbox test user](#creating-a-salesforce-sandbox-test-user)** - toohave a counterpart of Britta Simon in Salesforce Sandbox that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="0cc23-146">**[Asignar usuario de prueba de hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="0cc23-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="0cc23-147">**[Pruebas de Single Sign-On](#testing-single-sign-on)**  -tooverify Hola si funciona la configuración.</span><span class="sxs-lookup"><span data-stu-id="0cc23-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="0cc23-148">Configuración del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="0cc23-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="0cc23-149">En esta sección, habilitar inicio de sesión único en Azure AD en hello portal de Azure y configurar el inicio de sesión único en la aplicación de espacio aislado de Salesforce.</span><span class="sxs-lookup"><span data-stu-id="0cc23-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Salesforce Sandbox application.</span></span>

<span data-ttu-id="0cc23-150">**inicio de sesión único en tooconfigure Azure AD con Salesforce Sandbox, siga Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="0cc23-150">**tooconfigure Azure AD single sign-on with Salesforce Sandbox, perform hello following steps:**</span></span>

1. <span data-ttu-id="0cc23-151">En el portal de Azure, en Hola Hola **Salesforce Sandbox** página de integración de aplicaciones, haga clic en **inicio de sesión único**.</span><span class="sxs-lookup"><span data-stu-id="0cc23-151">In hello Azure portal, on hello **Salesforce Sandbox** application integration page, click **Single sign-on**.</span></span>

    ![Configurar inicio de sesión único][4]

2. <span data-ttu-id="0cc23-153">En hello **inicio de sesión único** cuadro de diálogo, seleccione **modo** como **sesión basado en SAML** tooenable inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="0cc23-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurar inicio de sesión único](./media/active-directory-saas-salesforcesandbox-tutorial/tutorial_salesforcesandbox_samlbase.png)

3. <span data-ttu-id="0cc23-155">En hello **dominio de espacio aislado de Salesforce y las direcciones URL** sección, lleve a cabo Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="0cc23-155">On hello **Salesforce Sandbox Domain and URLs** section, perform hello following steps:</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-salesforcesandbox-tutorial/tutorial_salesforcesandbox_url.png)

     <span data-ttu-id="0cc23-157">Hola **dirección URL de inicio de sesión** cuadro de texto, valor de tipo hello mediante Hola sigue el patrón:`https://<subdomain>.my.salesforce.com`</span><span class="sxs-lookup"><span data-stu-id="0cc23-157">In hello **Sign-on URL** textbox, type hello value using hello following pattern: `https://<subdomain>.my.salesforce.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="0cc23-158">Este valor no es hello real.</span><span class="sxs-lookup"><span data-stu-id="0cc23-158">This value is not hello real.</span></span> <span data-ttu-id="0cc23-159">Actualizar este valor con la URL de inicio de sesión real de Hola. Póngase en contacto con [equipo de soporte técnico de cliente de espacio aislado de Salesforce](https://help.salesforce.com/support) tooget este valor.</span><span class="sxs-lookup"><span data-stu-id="0cc23-159">Update this value with hello actual Sign-on URL.Contact [Salesforce Sandbox Client support team](https://help.salesforce.com/support) tooget this value.</span></span>


4. <span data-ttu-id="0cc23-160">Si ya ha configurado un inicio de sesión único para otra instancia de Salesforce Sandbox de su directorio, también debe configurar hello **identificador** toohave Hola el mismo valor que hello **dirección URL de inicio de sesión**.</span><span class="sxs-lookup"><span data-stu-id="0cc23-160">If you have already configured single sign-on for another Salesforce Sandbox instance in your directory, then you must also configure hello **Identifier** toohave hello same value as hello **Sign on URL**.</span></span> 
    
    >[!Note]
    ><span data-ttu-id="0cc23-161">Hola **identificador** campo puede encontrarse mediante la comprobación de hello **Mostrar configuración avanzada** casilla de verificación de hello **configurar URL de aplicación** página del cuadro de diálogo de Hola</span><span class="sxs-lookup"><span data-stu-id="0cc23-161">hello **Identifier** field can be found by checking hello **Show advanced settings** checkbox on hello **Configure App URL** page of hello dialog</span></span> 


5. <span data-ttu-id="0cc23-162">En hello **el certificado de firma de SAML** sección, haga clic en **certificado** y, a continuación, guarde el archivo de certificado de hello en el equipo.</span><span class="sxs-lookup"><span data-stu-id="0cc23-162">On hello **SAML Signing Certificate** section, click **Certificate** and then save hello certificate file on your computer.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-salesforcesandbox-tutorial/tutorial_salesforcesandbox_certificate.png) 

6. <span data-ttu-id="0cc23-164">Haga clic en el botón **Guardar** .</span><span class="sxs-lookup"><span data-stu-id="0cc23-164">Click **Save** button.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-salesforcesandbox-tutorial/tutorial_general_400.png)

7. <span data-ttu-id="0cc23-166">En hello **configuración de espacio aislado de Salesforce** sección, haga clic en **configurar Salesforce Sandbox** tooopen **configurar inicio de sesión** ventana.</span><span class="sxs-lookup"><span data-stu-id="0cc23-166">On hello **Salesforce Sandbox Configuration** section, click **Configure Salesforce Sandbox** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="0cc23-167">Hola copia **Id. de entidad de SAML y SAML Single Sign-On dirección URL del servicio** de hello **sección de referencia rápida.**</span><span class="sxs-lookup"><span data-stu-id="0cc23-167">Copy hello **SAML Entity ID and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    <span data-ttu-id="0cc23-168">![Configuración del inicio de sesión único](./media/active-directory-saas-salesforcesandbox-tutorial/tutorial_salesforcesandbox_configure.png) 
<CS></span><span class="sxs-lookup"><span data-stu-id="0cc23-168">![Configure Single Sign-On](./media/active-directory-saas-salesforcesandbox-tutorial/tutorial_salesforcesandbox_configure.png) 
<CS></span></span>
8. <span data-ttu-id="0cc23-169">Abra una nueva pestaña en el explorador e inicie sesión tooyour cuenta de administrador de espacio aislado de Salesforce.</span><span class="sxs-lookup"><span data-stu-id="0cc23-169">Open a new tab in your browser and log in tooyour Salesforce Sandbox administrator account.</span></span>

9. <span data-ttu-id="0cc23-170">En el menú de hello en la parte superior de hello, haga clic en **el programa de instalación**.</span><span class="sxs-lookup"><span data-stu-id="0cc23-170">In hello menu on hello top, click **Setup**.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-salesforcesandbox-tutorial/IC781024.png)
10. <span data-ttu-id="0cc23-172">En el panel de navegación de Hola Hola izquierda, haga clic en **controles de seguridad**y, a continuación, haga clic en **configuración de inicio de sesión único**.</span><span class="sxs-lookup"><span data-stu-id="0cc23-172">In hello navigation pane on hello left, click **Security Controls**, and then click **Single Sign-On Settings**.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-salesforcesandbox-tutorial/IC781025.png)
11. <span data-ttu-id="0cc23-174">En la sección de configuración de inicio de sesión único de hello, realizar Hola siguiendo los pasos: ![configurar Single Sign-On](./media/active-directory-saas-salesforcesandbox-tutorial/IC781026.png)</span><span class="sxs-lookup"><span data-stu-id="0cc23-174">On hello Single Sign-On Settings section, perform hello following steps:  ![Configure Single Sign-On](./media/active-directory-saas-salesforcesandbox-tutorial/IC781026.png)</span></span>
     
     <span data-ttu-id="0cc23-175">a.</span><span class="sxs-lookup"><span data-stu-id="0cc23-175">a.</span></span>  <span data-ttu-id="0cc23-176">Seleccione **SAML habilitado**.</span><span class="sxs-lookup"><span data-stu-id="0cc23-176">Select **SAML Enabled**.</span></span> 

     <span data-ttu-id="0cc23-177">b.</span><span class="sxs-lookup"><span data-stu-id="0cc23-177">b.</span></span>  <span data-ttu-id="0cc23-178">Haga clic en **Nuevo**.</span><span class="sxs-lookup"><span data-stu-id="0cc23-178">Click **New**.</span></span>

12. <span data-ttu-id="0cc23-179">En la sección de configuración de inicio de sesión único de SAML de hello, realizar Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="0cc23-179">On hello SAML Single Sign-On Settings section, perform hello following steps:</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-salesforcesandbox-tutorial/IC781027.png)

    <span data-ttu-id="0cc23-181">el cuadro de texto de a.In Hola nombre, escriba un nombre Hola de configuración de hello (p. ej.: *SPSSOWAAD\_prueba*).</span><span class="sxs-lookup"><span data-stu-id="0cc23-181">a.In hello Name textbox, type hello name of hello configuration (e.g.: *SPSSOWAAD\_Test*).</span></span> 

    <span data-ttu-id="0cc23-182">b.</span><span class="sxs-lookup"><span data-stu-id="0cc23-182">b.</span></span> <span data-ttu-id="0cc23-183">Pegar **Id. de entidad Small** valor en hello **emisor** cuadro de texto.</span><span class="sxs-lookup"><span data-stu-id="0cc23-183">Paste **SMAL Entity ID** value into hello **Issuer** textbox.</span></span>

    <span data-ttu-id="0cc23-184">c.</span><span class="sxs-lookup"><span data-stu-id="0cc23-184">c.</span></span> <span data-ttu-id="0cc23-185">Hola **Id. de entidad** cuadro de texto, tipo **https://test.salesforce.com** si es Hola la primera instancia de Salesforce Sandbox que va a Agregar directorio tooyour.</span><span class="sxs-lookup"><span data-stu-id="0cc23-185">In hello **Entity Id** textbox, type **https://test.salesforce.com** if it is hello first Salesforce Sandbox instance that you are adding tooyour directory.</span></span> <span data-ttu-id="0cc23-186">Si ya ha agregado una instancia de Salesforce Sandbox, después de hello **Id. de entidad** tipo Hola **dirección URL de inicio de sesión**, que debe tener este formato:`http://company.my.salesforce.com`</span><span class="sxs-lookup"><span data-stu-id="0cc23-186">If you have already added an instance of Salesforce Sandbox, then for hello **Entity ID** type in hello **Sign On URL**, which should be in this format: `http://company.my.salesforce.com`</span></span>  
 
    <span data-ttu-id="0cc23-187">d.</span><span class="sxs-lookup"><span data-stu-id="0cc23-187">d.</span></span> <span data-ttu-id="0cc23-188">Haga clic en **examinar** hello tooupload descargado el certificado.</span><span class="sxs-lookup"><span data-stu-id="0cc23-188">Click **Browse** tooupload hello downloaded certificate.</span></span>  

    <span data-ttu-id="0cc23-189">e.</span><span class="sxs-lookup"><span data-stu-id="0cc23-189">e.</span></span> <span data-ttu-id="0cc23-190">Como **tipo de identidad SAML**, seleccione **la aserción contiene Hola Id. de federación del objeto de usuario de hello**.</span><span class="sxs-lookup"><span data-stu-id="0cc23-190">As **SAML Identity Type**, select **Assertion contains hello Federation ID from hello User object**.</span></span>
 
    <span data-ttu-id="0cc23-191">f.</span><span class="sxs-lookup"><span data-stu-id="0cc23-191">f.</span></span> <span data-ttu-id="0cc23-192">Como **ubicación de identidad SAML**, seleccione **identidad está en el elemento NameIdentifier de Hola de hello instrucción Subject**.</span><span class="sxs-lookup"><span data-stu-id="0cc23-192">As **SAML Identity Location**, select **Identity is in hello NameIdentifier element of hello Subject statement**.</span></span>

    <span data-ttu-id="0cc23-193">g.</span><span class="sxs-lookup"><span data-stu-id="0cc23-193">g.</span></span> <span data-ttu-id="0cc23-194">Pegar **URL de servicio de inicio de sesión único** en hello **URL de inicio de sesión del proveedor de identidades** cuadro de texto.</span><span class="sxs-lookup"><span data-stu-id="0cc23-194">Paste **Single Sign-On Service URL** into hello **Identity Provider Login URL** textbox.</span></span> 

    <span data-ttu-id="0cc23-195">h.</span><span class="sxs-lookup"><span data-stu-id="0cc23-195">h.</span></span> <span data-ttu-id="0cc23-196">SFDC no admite el cierre de sesión SAML.</span><span class="sxs-lookup"><span data-stu-id="0cc23-196">SFDC does not support SAML logout.</span></span>  <span data-ttu-id="0cc23-197">Como alternativa, pegue 'https://login.microsoftonline.com/common/wsfederation?wa=wsignout1.0' en hello **URL de cierre de sesión del proveedor de identidades** cuadro de texto.</span><span class="sxs-lookup"><span data-stu-id="0cc23-197">As a workaround, paste 'https://login.microsoftonline.com/common/wsfederation?wa=wsignout1.0' it into hello **Identity Provider Logout URL** textbox.</span></span>

    <span data-ttu-id="0cc23-198">i.</span><span class="sxs-lookup"><span data-stu-id="0cc23-198">i.</span></span> <span data-ttu-id="0cc23-199">Para **Service Provider Initiated Request Binding** (Enlace de solicitud iniciada por el proveedor de servicio), seleccione **HTTP POST** (Método HTTP POST).</span><span class="sxs-lookup"><span data-stu-id="0cc23-199">As **Service Provider Initiated Request Binding**, select **HTTP POST**.</span></span> 

    <span data-ttu-id="0cc23-200">j.</span><span class="sxs-lookup"><span data-stu-id="0cc23-200">j.</span></span> <span data-ttu-id="0cc23-201">Haga clic en **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="0cc23-201">Click **Save**.</span></span>

### <a name="enable-your-domain"></a><span data-ttu-id="0cc23-202">Habilitación del dominio</span><span class="sxs-lookup"><span data-stu-id="0cc23-202">Enable your domain</span></span>
<span data-ttu-id="0cc23-203">En esta sección se supone que ya ha creado un dominio.</span><span class="sxs-lookup"><span data-stu-id="0cc23-203">This section assumes that you already have created a domain.</span></span>  <span data-ttu-id="0cc23-204">Para más información, consulte [Defining Your Domain Name](https://help.salesforce.com/HTViewHelpDoc?id=domain_name_define.htm&language=en_US) (Definición del nombre de dominio).</span><span class="sxs-lookup"><span data-stu-id="0cc23-204">For more information, see [Defining Your Domain Name](https://help.salesforce.com/HTViewHelpDoc?id=domain_name_define.htm&language=en_US).</span></span>

<span data-ttu-id="0cc23-205">**tooenable su dominio, realizar Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="0cc23-205">**tooenable your domain, perform hello following steps:**</span></span>

1. <span data-ttu-id="0cc23-206">En el panel de navegación izquierdo de hello, haga clic en **Domain Management**y, a continuación, haga clic en **mi dominio.**</span><span class="sxs-lookup"><span data-stu-id="0cc23-206">In hello left navigation pane, click **Domain Management**, and then click **My Domain.**</span></span>
   
     ![Configurar inicio de sesión único](./media/active-directory-saas-salesforcesandbox-tutorial/IC781029.png)
   
   >[!NOTE]
   ><span data-ttu-id="0cc23-208">Asegúrese de que su dominio se ha configurado correctamente.</span><span class="sxs-lookup"><span data-stu-id="0cc23-208">Please make sure that your domain has been configured correctly.</span></span> 

2. <span data-ttu-id="0cc23-209">Hola **configuración de la página de inicio de sesión** sección, haga clic en **editar**, a continuación, como **servicio de autenticación**, seleccione nombre de Hola de hello configuración de inicio de sesión único de SAML de hello anterior sección y, por último, haga clic en **guardar**.</span><span class="sxs-lookup"><span data-stu-id="0cc23-209">In hello **Login Page Settings** section, click **Edit**, then, as **Authentication Service**, select hello name of hello SAML Single Sign-On Setting from hello previous section, and finally click **Save**.</span></span>
   
   ![Configurar inicio de sesión único](./media/active-directory-saas-salesforcesandbox-tutorial/IC781030.png)

<span data-ttu-id="0cc23-211">Tan pronto como tiene configurado un dominio, los usuarios deben usar toohello Salesforce sandbox de hello dominio URL toologin.</span><span class="sxs-lookup"><span data-stu-id="0cc23-211">As soon as you have a domain configured, your users should use hello domain URL toologin toohello Salesforce sandbox.</span></span>  

<span data-ttu-id="0cc23-212">valor de hello tooget de dirección URL de hello, haga clic en perfil SSO de Hola que haya creado en la sección anterior de Hola.</span><span class="sxs-lookup"><span data-stu-id="0cc23-212">tooget hello value of hello URL, click hello SSO profile you have created in hello previous section.</span></span>    

> [!TIP]
> <span data-ttu-id="0cc23-213">Ahora puede leer una versión concisa de estas instrucciones dentro de hello [portal de Azure](https://portal.azure.com), mientras que está configurando la aplicación hello!</span><span class="sxs-lookup"><span data-stu-id="0cc23-213">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="0cc23-214">Después de agregar esta aplicación de hello **Active Directory > aplicaciones empresariales** sección, simplemente haga clic en hello **Single Sign-On** Hola de pestaña y acceso incrustado documentación a través de hello  **Configuración** sección final Hola.</span><span class="sxs-lookup"><span data-stu-id="0cc23-214">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="0cc23-215">Puede leer más acerca de características de documentación de embedded Hola aquí: [Azure AD incrustado documentación]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="0cc23-215">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>


### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="0cc23-216">Creación de un usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="0cc23-216">Creating an Azure AD test user</span></span>
<span data-ttu-id="0cc23-217">objetivo de Hola de esta sección es un usuario de prueba en hello Azure portal llamado a Britta Simon toocreate.</span><span class="sxs-lookup"><span data-stu-id="0cc23-217">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Creación de un usuario de Azure AD][100]

<span data-ttu-id="0cc23-219">**toocreate un usuario de prueba en Azure AD, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="0cc23-219">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="0cc23-220">Hola **portal de Azure**, en Hola panel de navegación izquierdo, haga clic en **Azure Active Directory** icono.</span><span class="sxs-lookup"><span data-stu-id="0cc23-220">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-salesforcesandbox-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="0cc23-222">lista de hello toodisplay de usuarios vaya demasiado**usuarios y grupos** y haga clic en **todos los usuarios**.</span><span class="sxs-lookup"><span data-stu-id="0cc23-222">toodisplay hello list of users go too**Users and groups** and click **All users**.</span></span>
    
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-salesforcesandbox-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="0cc23-224">En la parte superior de saludo del cuadro de diálogo de hello, haga clic en **agregar** tooopen hello **usuario** cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="0cc23-224">At hello top of hello dialog, click **Add** tooopen hello **User** dialog.</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-salesforcesandbox-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="0cc23-226">En hello **usuario** cuadro de diálogo, siga los pasos de hello:</span><span class="sxs-lookup"><span data-stu-id="0cc23-226">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-salesforcesandbox-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="0cc23-228">a.</span><span class="sxs-lookup"><span data-stu-id="0cc23-228">a.</span></span> <span data-ttu-id="0cc23-229">Hola **nombre** cuadro de texto, tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="0cc23-229">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="0cc23-230">b.</span><span class="sxs-lookup"><span data-stu-id="0cc23-230">b.</span></span> <span data-ttu-id="0cc23-231">Hola **nombre de usuario** cuadro de texto, hello tipo **dirección de correo electrónico** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="0cc23-231">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="0cc23-232">c.</span><span class="sxs-lookup"><span data-stu-id="0cc23-232">c.</span></span> <span data-ttu-id="0cc23-233">Seleccione **Mostrar contraseña** y anote el valor de Hola de hello **contraseña**.</span><span class="sxs-lookup"><span data-stu-id="0cc23-233">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="0cc23-234">d.</span><span class="sxs-lookup"><span data-stu-id="0cc23-234">d.</span></span> <span data-ttu-id="0cc23-235">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="0cc23-235">Click **Create**.</span></span>
 
### <a name="creating-a-salesforce-sandbox-test-user"></a><span data-ttu-id="0cc23-236">Creación de un usuario de prueba de Salesforce Sandbox</span><span class="sxs-lookup"><span data-stu-id="0cc23-236">Creating a Salesforce Sandbox test user</span></span>

<span data-ttu-id="0cc23-237">En esta sección, creará un usuario llamado a Britta Simon en Salesforce Sandbox.</span><span class="sxs-lookup"><span data-stu-id="0cc23-237">In this section, a user called Britta Simon is created in Salesforce Sandbox.</span></span> <span data-ttu-id="0cc23-238">Salesforce Sandbox admite el aprovisionamiento Just-In-Time, que está habilitado de forma predeterminada.</span><span class="sxs-lookup"><span data-stu-id="0cc23-238">Salesforce Sandbox supports just-in-time provisioning, which is enabled by default.</span></span>
<span data-ttu-id="0cc23-239">No hay ningún elemento de acción para usted en esta sección.</span><span class="sxs-lookup"><span data-stu-id="0cc23-239">There is no action item for you in this section.</span></span> <span data-ttu-id="0cc23-240">Si un usuario ya no existe en el espacio aislado de Salesforce, se crea uno nuevo si intentas tooaccess espacio aislado de Salesforce.</span><span class="sxs-lookup"><span data-stu-id="0cc23-240">If a user doesn't already exist in Salesforce Sandbox, a new one is created when you attempt tooaccess Salesforce Sandbox.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="0cc23-241">Asignación de usuario de prueba de hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="0cc23-241">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="0cc23-242">En esta sección, se habilita Britta Simon toouse un inicio de sesión único Azure concediendo acceso tooSalesforce espacio aislado.</span><span class="sxs-lookup"><span data-stu-id="0cc23-242">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooSalesforce Sandbox.</span></span>

![Asignar usuario][200] 

<span data-ttu-id="0cc23-244">**tooassign Britta Simon tooSalesforce de espacio aislado, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="0cc23-244">**tooassign Britta Simon tooSalesforce Sandbox, perform hello following steps:**</span></span>

1. <span data-ttu-id="0cc23-245">Hola portal de Azure, abra la vista de aplicaciones de hello y, a continuación, navegue a vista de directorio toohello y vaya demasiado**aplicaciones empresariales** , a continuación, haga clic en **todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="0cc23-245">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Asignar usuario][201] 

2. <span data-ttu-id="0cc23-247">En la lista de aplicaciones de hello, seleccione **Salesforce Sandbox**.</span><span class="sxs-lookup"><span data-stu-id="0cc23-247">In hello applications list, select **Salesforce Sandbox**.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-salesforcesandbox-tutorial/tutorial_salesforcesandbox_app.png) 

3. <span data-ttu-id="0cc23-249">En el menú de Hola Hola izquierda, haga clic en **usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="0cc23-249">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Asignar usuario][202] 

4. <span data-ttu-id="0cc23-251">Haga clic en el botón **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="0cc23-251">Click **Add** button.</span></span> <span data-ttu-id="0cc23-252">Después, seleccione **Usuarios y grupos** en el cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="0cc23-252">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Asignar usuario][203]

5. <span data-ttu-id="0cc23-254">En **usuarios y grupos** cuadro de diálogo, seleccione **Britta Simon** en la lista de usuarios de Hola.</span><span class="sxs-lookup"><span data-stu-id="0cc23-254">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="0cc23-255">Haga clic en el botón **Seleccionar** del cuadro de diálogo **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="0cc23-255">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="0cc23-256">Haga clic en el botón **Asignar** del cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="0cc23-256">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="0cc23-257">Prueba del inicio de sesión único </span><span class="sxs-lookup"><span data-stu-id="0cc23-257">Testing single sign-on</span></span>

<span data-ttu-id="0cc23-258">Si desea tootest la configuración de SSO, abra Hola Panel de acceso.</span><span class="sxs-lookup"><span data-stu-id="0cc23-258">If you want tootest your SSO settings, open hello Access Panel.</span></span> <span data-ttu-id="0cc23-259">Para obtener más información acerca de hello Panel de acceso, consulte [Introducción toohello Panel de acceso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="0cc23-259">For more details about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="0cc23-260">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="0cc23-260">Additional resources</span></span>

* [<span data-ttu-id="0cc23-261">Lista de tutoriales sobre cómo tooIntegrate aplicaciones de SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="0cc23-261">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="0cc23-262">¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="0cc23-262">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)
* [<span data-ttu-id="0cc23-263">Configuración del aprovisionamiento de usuarios</span><span class="sxs-lookup"><span data-stu-id="0cc23-263">Configure User Provisioning</span></span>](active-directory-saas-salesforce-sandbox-provisioning-tutorial.md)



<!--Image references-->

[1]: ./media/active-directory-saas-salesforcesandbox-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-salesforcesandbox-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-salesforcesandbox-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-salesforcesandbox-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-salesforcesandbox-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-salesforcesandbox-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-salesforcesandbox-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-salesforcesandbox-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-salesforcesandbox-tutorial/tutorial_general_203.png

