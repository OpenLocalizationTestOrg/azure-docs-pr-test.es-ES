---
title: "Tutorial: Integración de Azure Active Directory con Learningpool Act | Microsoft Docs"
description: "Obtenga información acerca de cómo tooconfigure inicio de sesión único entre Azure Active Directory y actuar de Learningpool."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 51e8695f-31e1-4d09-8eb3-13241999d99f
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/30/2017
ms.author: jeedes
ms.openlocfilehash: f343623f08bb60e143aaff07d93e4ef773232e07
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-learningpool-act"></a><span data-ttu-id="5b85f-103">Tutorial: Integración de Azure Active Directory con Learningpool Act</span><span class="sxs-lookup"><span data-stu-id="5b85f-103">Tutorial: Azure Active Directory integration with Learningpool Act</span></span>

<span data-ttu-id="5b85f-104">En este tutorial, aprenderá cómo toointegrate Learningpool actuar con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="5b85f-104">In this tutorial, you learn how toointegrate Learningpool Act with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="5b85f-105">Integración Learningpool Act con Azure AD proporciona Hola siguientes ventajas:</span><span class="sxs-lookup"><span data-stu-id="5b85f-105">Integrating Learningpool Act with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="5b85f-106">Puede controlar en Azure AD que tenga acceso tooLearningpool Act</span><span class="sxs-lookup"><span data-stu-id="5b85f-106">You can control in Azure AD who has access tooLearningpool Act</span></span>
- <span data-ttu-id="5b85f-107">Puede habilitar los usuarios tooautomatically get ha iniciado sesión tooLearningpool Act (Single Sign-On) con sus cuentas de Azure AD</span><span class="sxs-lookup"><span data-stu-id="5b85f-107">You can enable your users tooautomatically get signed-on tooLearningpool Act (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="5b85f-108">Puede administrar las cuentas en una ubicación central: Hola portal de Azure</span><span class="sxs-lookup"><span data-stu-id="5b85f-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="5b85f-109">Si desea obtener más información acerca de la integración de aplicaciones de SaaS con Azure AD tooknow, consulte [¿qué es acceso a la aplicación y el inicio de sesión único con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="5b85f-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="5b85f-110">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="5b85f-110">Prerequisites</span></span>

<span data-ttu-id="5b85f-111">integración de Azure AD con Learningpool Act tooconfigure, necesita Hola siguientes elementos:</span><span class="sxs-lookup"><span data-stu-id="5b85f-111">tooconfigure Azure AD integration with Learningpool Act, you need hello following items:</span></span>

- <span data-ttu-id="5b85f-112">Una suscripción de Azure AD</span><span class="sxs-lookup"><span data-stu-id="5b85f-112">An Azure AD subscription</span></span>
- <span data-ttu-id="5b85f-113">Una suscripción habilitada para inicio de sesión único en Learningpool Act</span><span class="sxs-lookup"><span data-stu-id="5b85f-113">A Learningpool Act single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="5b85f-114">Hola tootest los pasos de este tutorial, no se recomienda usar un entorno de producción.</span><span class="sxs-lookup"><span data-stu-id="5b85f-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="5b85f-115">pasos de hello tootest en este tutorial, debe seguir estas recomendaciones:</span><span class="sxs-lookup"><span data-stu-id="5b85f-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="5b85f-116">No use el entorno de producción, salvo que sea necesario.</span><span class="sxs-lookup"><span data-stu-id="5b85f-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="5b85f-117">Si no dispone de un entorno de prueba de Azure AD, puede obtener una versión de prueba de un mes [aquí](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="5b85f-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="5b85f-118">Descripción del escenario</span><span class="sxs-lookup"><span data-stu-id="5b85f-118">Scenario description</span></span>
<span data-ttu-id="5b85f-119">En este tutorial, puede probar el inicio de sesión único de Azure AD en un entorno de prueba.</span><span class="sxs-lookup"><span data-stu-id="5b85f-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="5b85f-120">escenario de Hello descrito en este tutorial consta de dos bloques principales:</span><span class="sxs-lookup"><span data-stu-id="5b85f-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="5b85f-121">Agregar acción de Learningpool de galería de Hola</span><span class="sxs-lookup"><span data-stu-id="5b85f-121">Adding Learningpool Act from hello gallery</span></span>
2. <span data-ttu-id="5b85f-122">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="5b85f-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-learningpool-act-from-hello-gallery"></a><span data-ttu-id="5b85f-123">Agregar acción de Learningpool de galería de Hola</span><span class="sxs-lookup"><span data-stu-id="5b85f-123">Adding Learningpool Act from hello gallery</span></span>
<span data-ttu-id="5b85f-124">integración de hello tooconfigure de Learningpool Act en Azure AD, deberá tooadd Learningpool Act de lista de tooyour Hola Galería de aplicaciones administradas de SaaS.</span><span class="sxs-lookup"><span data-stu-id="5b85f-124">tooconfigure hello integration of Learningpool Act into Azure AD, you need tooadd Learningpool Act from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="5b85f-125">**tooadd Learningpool Act de galería de hello, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="5b85f-125">**tooadd Learningpool Act from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="5b85f-126">Hola ** [portal de Azure](https://portal.azure.com)**, en el panel de navegación izquierdo de Hola, haga clic en **Azure Active Directory** icono.</span><span class="sxs-lookup"><span data-stu-id="5b85f-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="5b85f-128">Navegue demasiado**aplicaciones empresariales**.</span><span class="sxs-lookup"><span data-stu-id="5b85f-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="5b85f-129">A continuación, vaya demasiado**todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="5b85f-129">Then go too**All applications**.</span></span>

    ![Aplicaciones][2]
    
3. <span data-ttu-id="5b85f-131">tooadd nueva aplicación, haga clic en **nueva aplicación** botón en la parte superior de saludo del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="5b85f-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Aplicaciones][3]

4. <span data-ttu-id="5b85f-133">En el cuadro de búsqueda de hello, escriba **Learningpool Act**.</span><span class="sxs-lookup"><span data-stu-id="5b85f-133">In hello search box, type **Learningpool Act**.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-Learningpool-tutorial/tutorial_Learningpoolact_search.png)

5. <span data-ttu-id="5b85f-135">En el panel de resultados de hello, seleccione **Learningpool Act**y, a continuación, haga clic en **agregar** botón aplicación hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="5b85f-135">In hello results panel, select **Learningpool Act**, and then click **Add** button tooadd hello application.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-Learningpool-tutorial/tutorial_Learningpoolact_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="5b85f-137">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="5b85f-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="5b85f-138">En esta sección, configurará y probará el inicio de sesión único de Azure AD con Learningpool Act con un usuario de prueba llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="5b85f-138">In this section, you configure and test Azure AD single sign-on with Learningpool Act based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="5b85f-139">Para toowork de inicio de sesión único, Azure AD necesita tooknow qué usuario equivalente de hello en Learningpool Act es tooa usuario en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="5b85f-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Learningpool Act is tooa user in Azure AD.</span></span> <span data-ttu-id="5b85f-140">En otras palabras, una relación de vínculo entre un usuario de Azure AD y el usuario relacionado de hello en Learningpool Act debe toobe establecido.</span><span class="sxs-lookup"><span data-stu-id="5b85f-140">In other words, a link relationship between an Azure AD user and hello related user in Learningpool Act needs toobe established.</span></span>

<span data-ttu-id="5b85f-141">En el acto de Learningpool, asigne el valor de Hola de Hola **nombre de usuario** en Azure AD como valor de Hola de hello **nombre de usuario** tooestablish la relación de vínculo de Hola.</span><span class="sxs-lookup"><span data-stu-id="5b85f-141">In Learningpool Act, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="5b85f-142">tooconfigure y prueba de inicio de sesión único en Azure AD con Learningpool Act, deberá hello toocomplete después de bloques de creación:</span><span class="sxs-lookup"><span data-stu-id="5b85f-142">tooconfigure and test Azure AD single sign-on with Learningpool Act, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="5b85f-143">**[Configuración de Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on) ** -tooenable la toouse usuarios esta característica.</span><span class="sxs-lookup"><span data-stu-id="5b85f-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="5b85f-144">**[Crear un usuario de prueba de Azure AD](#creating-an-azure-ad-test-user) ** -inicio de sesión único en Azure AD tootest con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="5b85f-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="5b85f-145">**[Crear un usuario de prueba de acción de Learningpool](#creating-a-learningpool-act-test-user) ** -toohave un equivalente de Britta Simon en Learningpool Act que es la representación toohello vinculado Azure AD del usuario.</span><span class="sxs-lookup"><span data-stu-id="5b85f-145">**[Creating a Learningpool Act test user](#creating-a-learningpool-act-test-user)** - toohave a counterpart of Britta Simon in Learningpool Act that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="5b85f-146">**[Asignar usuario de prueba de hello Azure AD](#assigning-the-azure-ad-test-user) ** -tooenable Britta Simon toouse Azure AD inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="5b85f-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="5b85f-147">**[Pruebas de Single Sign-On](#testing-single-sign-on) ** -tooverify Hola si funciona la configuración.</span><span class="sxs-lookup"><span data-stu-id="5b85f-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="5b85f-148">Configuración del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="5b85f-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="5b85f-149">En esta sección, habilitar inicio de sesión único en Azure AD en hello portal de Azure y configurar el inicio de sesión único en la aplicación de Learningpool Act.</span><span class="sxs-lookup"><span data-stu-id="5b85f-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Learningpool Act application.</span></span>

<span data-ttu-id="5b85f-150">**inicio de sesión único en tooconfigure Azure AD con Learningpool Act, realizar Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="5b85f-150">**tooconfigure Azure AD single sign-on with Learningpool Act, perform hello following steps:**</span></span>

1. <span data-ttu-id="5b85f-151">En el portal de Azure, en Hola Hola **Learningpool Act** página de integración de aplicaciones, haga clic en **inicio de sesión único**.</span><span class="sxs-lookup"><span data-stu-id="5b85f-151">In hello Azure portal, on hello **Learningpool Act** application integration page, click **Single sign-on**.</span></span>

    ![Configurar inicio de sesión único][4]

2. <span data-ttu-id="5b85f-153">En hello **inicio de sesión único** cuadro de diálogo, seleccione **modo** como **sesión basado en SAML** tooenable inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="5b85f-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurar inicio de sesión único](./media/active-directory-saas-Learningpool-tutorial/tutorial_Learningpoolact_samlbase.png)

3. <span data-ttu-id="5b85f-155">En hello **Learningpool Act dominio y las direcciones URL** sección, lleve a cabo Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="5b85f-155">On hello **Learningpool Act Domain and URLs** section, perform hello following steps:</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-Learningpool-tutorial/tutorial_Learningpoolact_url.png)

    <span data-ttu-id="5b85f-157">a.</span><span class="sxs-lookup"><span data-stu-id="5b85f-157">a.</span></span> <span data-ttu-id="5b85f-158">Hola **dirección URL de inicio de sesión** cuadro de texto, escriba la dirección URL hello:`https://parliament.preview.Learningpool.com/auth/shibboleth/index.php`</span><span class="sxs-lookup"><span data-stu-id="5b85f-158">In hello **Sign-on URL** textbox, type hello URL: `https://parliament.preview.Learningpool.com/auth/shibboleth/index.php`</span></span>

    <span data-ttu-id="5b85f-159">b.</span><span class="sxs-lookup"><span data-stu-id="5b85f-159">b.</span></span> <span data-ttu-id="5b85f-160">Hola **identificador** cuadro de texto, escriba una dirección URL usando Hola siguiente patrón:</span><span class="sxs-lookup"><span data-stu-id="5b85f-160">In hello **Identifier** textbox, type a URL using hello following pattern:</span></span>
    | |
    |--|
    | `https://<subdomain>.Learningpool.com/shibboleth` |
    | `https://<subdomain>.preview.Learningpool.com/shibboleth` |

    > [!NOTE] 
    > <span data-ttu-id="5b85f-161">Estos valores no son reales.</span><span class="sxs-lookup"><span data-stu-id="5b85f-161">These values are not real.</span></span> <span data-ttu-id="5b85f-162">Actualizar estos valores con hello real de dirección URL de inicio de sesión y el identificador.</span><span class="sxs-lookup"><span data-stu-id="5b85f-162">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="5b85f-163">Póngase en contacto con [equipo de soporte técnico de Learningpool Act cliente](https://www.Learningpool.com/support) tooget estos valores.</span><span class="sxs-lookup"><span data-stu-id="5b85f-163">Contact [Learningpool Act Client support team](https://www.Learningpool.com/support) tooget these values.</span></span> 
 
4. <span data-ttu-id="5b85f-164">En hello **el certificado de firma de SAML** sección, haga clic en **Metadata XML** y, a continuación, guarde el archivo de metadatos de hello en el equipo.</span><span class="sxs-lookup"><span data-stu-id="5b85f-164">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-Learningpool-tutorial/tutorial_Learningpoolact_certificate.png) 

5. <span data-ttu-id="5b85f-166">Aplicación de Learningpool Act espera las aserciones de SAML de hello en un formato concreto.</span><span class="sxs-lookup"><span data-stu-id="5b85f-166">Learningpool Act application expects hello SAML assertions in a specific format.</span></span> <span data-ttu-id="5b85f-167">Configure Hola después de notificaciones para esta aplicación.</span><span class="sxs-lookup"><span data-stu-id="5b85f-167">Please configure hello following claims for this application.</span></span> <span data-ttu-id="5b85f-168">Puede administrar valores de hello de estos atributos de hello **"Atrribute"** pestaña de aplicación hello.</span><span class="sxs-lookup"><span data-stu-id="5b85f-168">You can manage hello values of these attributes from hello **"Atrribute"** tab of hello application.</span></span> <span data-ttu-id="5b85f-169">Hola siguiente captura de pantalla muestra un ejemplo de esto.</span><span class="sxs-lookup"><span data-stu-id="5b85f-169">hello following screenshot shows an example for this.</span></span> 

    ![Configurar inicio de sesión único](./media/active-directory-saas-Learningpool-tutorial/tutorial_Learningpoolact_attribute.png) 

6. <span data-ttu-id="5b85f-171">Hola **atributos de usuario** sección en hello **inicio de sesión único** cuadro de diálogo, configurar atributos de token de SAML como se muestra en la imagen de Hola y realizar Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="5b85f-171">In hello **User Attributes** section on hello **Single sign-on** dialog, configure SAML token attribute as shown in hello image and perform hello following steps:</span></span>
    
    | <span data-ttu-id="5b85f-172">Nombre del atributo</span><span class="sxs-lookup"><span data-stu-id="5b85f-172">Attribute Name</span></span> | <span data-ttu-id="5b85f-173">Valor de atributo</span><span class="sxs-lookup"><span data-stu-id="5b85f-173">Attribute Value</span></span> |
    | ------------------- | -------------------- |
    | <span data-ttu-id="5b85f-174">urn:oid:1.2.840.113556.1.4.221</span><span class="sxs-lookup"><span data-stu-id="5b85f-174">urn:oid:1.2.840.113556.1.4.221</span></span> | <span data-ttu-id="5b85f-175">user.userprincipalname</span><span class="sxs-lookup"><span data-stu-id="5b85f-175">user.userprincipalname</span></span> |
    | <span data-ttu-id="5b85f-176">urn:oid:2.5.4.42</span><span class="sxs-lookup"><span data-stu-id="5b85f-176">urn:oid:2.5.4.42</span></span> | <span data-ttu-id="5b85f-177">user.givenname</span><span class="sxs-lookup"><span data-stu-id="5b85f-177">user.givenname</span></span> |
    | <span data-ttu-id="5b85f-178">urn:oid:0.9.2342.19200300.100.1.3</span><span class="sxs-lookup"><span data-stu-id="5b85f-178">urn:oid:0.9.2342.19200300.100.1.3</span></span> | <span data-ttu-id="5b85f-179">user.mail</span><span class="sxs-lookup"><span data-stu-id="5b85f-179">user.mail</span></span> |    
    | <span data-ttu-id="5b85f-180">urn:oid:2.5.4.4</span><span class="sxs-lookup"><span data-stu-id="5b85f-180">urn:oid:2.5.4.4</span></span> | <span data-ttu-id="5b85f-181">user.surname</span><span class="sxs-lookup"><span data-stu-id="5b85f-181">user.surname</span></span> |
    
    <span data-ttu-id="5b85f-182">a.</span><span class="sxs-lookup"><span data-stu-id="5b85f-182">a.</span></span> <span data-ttu-id="5b85f-183">Haga clic en **Agregar atributo** tooopen hello **Agregar atributo** cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="5b85f-183">Click **Add attribute** tooopen hello **Add Attribute** dialog.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-Learningpool-tutorial/tutorial_attribute_04.png)

    ![Configurar inicio de sesión único](./media/active-directory-saas-Learningpool-tutorial/tutorial_attribute_05.png)

    <span data-ttu-id="5b85f-186">b.</span><span class="sxs-lookup"><span data-stu-id="5b85f-186">b.</span></span> <span data-ttu-id="5b85f-187">Hola **nombre** cuadro de texto, nombre de atributo de tipo hello se muestra para esa fila.</span><span class="sxs-lookup"><span data-stu-id="5b85f-187">In hello **Name** textbox, type hello attribute name shown for that row.</span></span>

    <span data-ttu-id="5b85f-188">c.</span><span class="sxs-lookup"><span data-stu-id="5b85f-188">c.</span></span> <span data-ttu-id="5b85f-189">De hello **valor** lista, el valor de atributo de tipo hello se muestra para esa fila.</span><span class="sxs-lookup"><span data-stu-id="5b85f-189">From hello **Value** list, type hello attribute value shown for that row.</span></span>

    <span data-ttu-id="5b85f-190">d.</span><span class="sxs-lookup"><span data-stu-id="5b85f-190">d.</span></span> <span data-ttu-id="5b85f-191">Deje hello **Namespace** en blanco.</span><span class="sxs-lookup"><span data-stu-id="5b85f-191">Leave hello **Namespace** blank.</span></span>
    
    <span data-ttu-id="5b85f-192">e.</span><span class="sxs-lookup"><span data-stu-id="5b85f-192">e.</span></span> <span data-ttu-id="5b85f-193">Haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="5b85f-193">Click **Ok**.</span></span>

7. <span data-ttu-id="5b85f-194">Haga clic en el botón **Guardar** .</span><span class="sxs-lookup"><span data-stu-id="5b85f-194">Click **Save** button.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-Learningpool-tutorial/tutorial_general_400.png)

8. <span data-ttu-id="5b85f-196">tooconfigure inicio de sesión único en **Learningpool Act** lado, necesita hello toosend descargado **Metadata XML** demasiado[equipo de soporte técnico de Learningpool Act](https://www.Learningpool.com/support).</span><span class="sxs-lookup"><span data-stu-id="5b85f-196">tooconfigure single sign-on on **Learningpool Act** side, you need toosend hello downloaded **Metadata XML** too[Learningpool Act support team](https://www.Learningpool.com/support).</span></span> <span data-ttu-id="5b85f-197">Establecen esta Hola de toohave configuración configurada correctamente en ambos lados de la conexión de SSO de SAML.</span><span class="sxs-lookup"><span data-stu-id="5b85f-197">They set this setting toohave hello SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="5b85f-198">Ahora puede leer una versión concisa de estas instrucciones dentro de hello [portal de Azure](https://portal.azure.com), mientras que está configurando la aplicación hello!</span><span class="sxs-lookup"><span data-stu-id="5b85f-198">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="5b85f-199">Después de agregar esta aplicación de hello **Active Directory > aplicaciones empresariales** sección, simplemente haga clic en hello **Single Sign-On** Hola de pestaña y acceso incrustado documentación a través de hello ** Configuración** sección final Hola.</span><span class="sxs-lookup"><span data-stu-id="5b85f-199">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="5b85f-200">Puede leer más acerca de características de documentación de embedded Hola aquí: [Azure AD incrustado documentación]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="5b85f-200">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="5b85f-201">Creación de un usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="5b85f-201">Creating an Azure AD test user</span></span>
<span data-ttu-id="5b85f-202">objetivo de Hola de esta sección es un usuario de prueba en hello Azure portal llamado a Britta Simon toocreate.</span><span class="sxs-lookup"><span data-stu-id="5b85f-202">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Creación de un usuario de Azure AD][100]

<span data-ttu-id="5b85f-204">**toocreate un usuario de prueba en Azure AD, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="5b85f-204">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="5b85f-205">Hola **portal de Azure**, en Hola panel de navegación izquierdo, haga clic en **Azure Active Directory** icono.</span><span class="sxs-lookup"><span data-stu-id="5b85f-205">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-Learningpool-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="5b85f-207">lista de hello toodisplay de usuarios, vaya demasiado**usuarios y grupos** y haga clic en **todos los usuarios**.</span><span class="sxs-lookup"><span data-stu-id="5b85f-207">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-Learningpool-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="5b85f-209">Hola tooopen **usuario** cuadro de diálogo, haga clic en **agregar** en la parte superior de saludo del cuadro de diálogo de Hola.</span><span class="sxs-lookup"><span data-stu-id="5b85f-209">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-Learningpool-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="5b85f-211">En hello **usuario** cuadro de diálogo, siga los pasos de hello:</span><span class="sxs-lookup"><span data-stu-id="5b85f-211">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-Learningpool-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="5b85f-213">a.</span><span class="sxs-lookup"><span data-stu-id="5b85f-213">a.</span></span> <span data-ttu-id="5b85f-214">Hola **nombre** cuadro de texto, tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="5b85f-214">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="5b85f-215">b.</span><span class="sxs-lookup"><span data-stu-id="5b85f-215">b.</span></span> <span data-ttu-id="5b85f-216">Hola **nombre de usuario** cuadro de texto, hello tipo **dirección de correo electrónico** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="5b85f-216">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="5b85f-217">c.</span><span class="sxs-lookup"><span data-stu-id="5b85f-217">c.</span></span> <span data-ttu-id="5b85f-218">Seleccione **Mostrar contraseña** y anote el valor de Hola de hello **contraseña**.</span><span class="sxs-lookup"><span data-stu-id="5b85f-218">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="5b85f-219">d.</span><span class="sxs-lookup"><span data-stu-id="5b85f-219">d.</span></span> <span data-ttu-id="5b85f-220">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="5b85f-220">Click **Create**.</span></span>
 
### <a name="creating-a-learningpool-act-test-user"></a><span data-ttu-id="5b85f-221">Creación de un usuario de prueba de Learningpool Act</span><span class="sxs-lookup"><span data-stu-id="5b85f-221">Creating a Learningpool Act test user</span></span>

<span data-ttu-id="5b85f-222">toolog de los usuarios de Azure AD tooenable en tooLearningpool Act, se les deben aprovisionar en Learningpool Act.</span><span class="sxs-lookup"><span data-stu-id="5b85f-222">tooenable Azure AD users toolog in tooLearningpool Act, they must be provisioned into Learningpool Act.</span></span>

<span data-ttu-id="5b85f-223">No hay ningún elemento de acción tooconfigure de aprovisionamiento de usuarios tooLearningpool Act.</span><span class="sxs-lookup"><span data-stu-id="5b85f-223">There is no action item for you tooconfigure user provisioning tooLearningpool Act.</span></span>  
<span data-ttu-id="5b85f-224">Los usuarios necesitan toobe creado por la [equipo de soporte técnico de Learningpool Act](https://www.Learningpool.com/support).</span><span class="sxs-lookup"><span data-stu-id="5b85f-224">Users need toobe created by your [Learningpool Act support team](https://www.Learningpool.com/support).</span></span>

>[!NOTE]
><span data-ttu-id="5b85f-225">Puede usar cualquier otra acción de Learningpool usuario cuenta herramienta de creación o las API proporcionadas por Learningpool Act tooprovision cuentas de usuario AAD.</span><span class="sxs-lookup"><span data-stu-id="5b85f-225">You can use any other Learningpool Act user account creation tools or APIs provided by Learningpool Act tooprovision AAD user accounts.</span></span> 

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="5b85f-226">Asignación de usuario de prueba de hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="5b85f-226">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="5b85f-227">En esta sección, se habilita Britta Simon toouse un inicio de sesión único Azure concediendo acceso tooLearningpool Act.</span><span class="sxs-lookup"><span data-stu-id="5b85f-227">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooLearningpool Act.</span></span>

![Asignar usuario][200] 

<span data-ttu-id="5b85f-229">**tooassign Britta Simon tooLearningpool Act, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="5b85f-229">**tooassign Britta Simon tooLearningpool Act, perform hello following steps:**</span></span>

1. <span data-ttu-id="5b85f-230">Hola portal de Azure, abra la vista de aplicaciones de hello y, a continuación, navegue a vista de directorio toohello y vaya demasiado**aplicaciones empresariales** , a continuación, haga clic en **todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="5b85f-230">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Asignar usuario][201] 

2. <span data-ttu-id="5b85f-232">En la lista de aplicaciones de hello, seleccione **Learningpool Act**.</span><span class="sxs-lookup"><span data-stu-id="5b85f-232">In hello applications list, select **Learningpool Act**.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-Learningpool-tutorial/tutorial_Learningpoolact_app.png) 

3. <span data-ttu-id="5b85f-234">En el menú de Hola Hola izquierda, haga clic en **usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="5b85f-234">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Asignar usuario][202] 

4. <span data-ttu-id="5b85f-236">Haga clic en el botón **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="5b85f-236">Click **Add** button.</span></span> <span data-ttu-id="5b85f-237">Después, seleccione **Usuarios y grupos** en el cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="5b85f-237">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Asignar usuario][203]

5. <span data-ttu-id="5b85f-239">En **usuarios y grupos** cuadro de diálogo, seleccione **Britta Simon** en la lista de usuarios de Hola.</span><span class="sxs-lookup"><span data-stu-id="5b85f-239">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="5b85f-240">Haga clic en el botón **Seleccionar** del cuadro de diálogo **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="5b85f-240">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="5b85f-241">Haga clic en el botón **Asignar** del cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="5b85f-241">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="5b85f-242">Prueba del inicio de sesión único </span><span class="sxs-lookup"><span data-stu-id="5b85f-242">Testing single sign-on</span></span>

<span data-ttu-id="5b85f-243">objetivo de Hola de esta sección es tootest su configuración de inicio de sesión único de Azure AD mediante Hola Panel de acceso.</span><span class="sxs-lookup"><span data-stu-id="5b85f-243">hello objective of this section is tootest your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="5b85f-244">Al hacer clic en hello Learningpool Act disponer en mosaico en hello Panel de acceso, deberá obtener automáticamente ha iniciado sesión tooyour aplicación Learningpool Act.</span><span class="sxs-lookup"><span data-stu-id="5b85f-244">When you click hello Learningpool Act tile in hello Access Panel, you should get automatically signed-on tooyour Learningpool Act application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="5b85f-245">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="5b85f-245">Additional resources</span></span>

* [<span data-ttu-id="5b85f-246">Lista de tutoriales sobre cómo tooIntegrate aplicaciones de SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="5b85f-246">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="5b85f-247">¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="5b85f-247">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-Learningpool-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-Learningpool-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-Learningpool-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-Learningpool-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-Learningpool-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-Learningpool-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-Learningpool-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-Learningpool-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-Learningpool-tutorial/tutorial_general_203.png

