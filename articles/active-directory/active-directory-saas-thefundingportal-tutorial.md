---
title: "Tutorial: Hola de integración de Azure Active Directory con financiación Portal | Documentos de Microsoft"
description: "Obtenga información acerca de cómo tooconfigure inicio de sesión único entre Azure Active Directory y Hola financiación Portal."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 4663cc8a-976a-4c6c-b3b4-1e5df9b66744
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/11/2017
ms.author: jeedes
ms.openlocfilehash: 9f4329e02f91eb6d8034f17646ac7d15afe503e8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-hello-funding-portal"></a><span data-ttu-id="63ad7-103">Tutorial: Hola de integración de Azure Active Directory con financiación Portal</span><span class="sxs-lookup"><span data-stu-id="63ad7-103">Tutorial: Azure Active Directory integration with hello Funding Portal</span></span>

<span data-ttu-id="63ad7-104">En este tutorial, aprenderá cómo toointegrate Hola financiación Portal con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="63ad7-104">In this tutorial, you learn how toointegrate hello Funding Portal with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="63ad7-105">Integración de hello financiación Portal con Azure AD proporciona Hola siguientes ventajas:</span><span class="sxs-lookup"><span data-stu-id="63ad7-105">Integrating hello Funding Portal with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="63ad7-106">Puede controlar en Azure AD que tenga acceso toohello financiamiento Portal</span><span class="sxs-lookup"><span data-stu-id="63ad7-106">You can control in Azure AD who has access toohello Funding Portal</span></span>
- <span data-ttu-id="63ad7-107">Puede habilitar los usuarios tooautomatically get ha iniciado sesión toohello Portal financiamiento (Single Sign-On) con sus cuentas de Azure AD</span><span class="sxs-lookup"><span data-stu-id="63ad7-107">You can enable your users tooautomatically get signed-on toohello Funding Portal (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="63ad7-108">Puede administrar las cuentas en una ubicación central: Hola portal de Azure</span><span class="sxs-lookup"><span data-stu-id="63ad7-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="63ad7-109">Si desea obtener más información acerca de la integración de aplicaciones de SaaS con Azure AD tooknow, consulte [¿qué es acceso a la aplicación y el inicio de sesión único con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="63ad7-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="63ad7-110">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="63ad7-110">Prerequisites</span></span>

<span data-ttu-id="63ad7-111">integración de tooconfigure Azure AD con hello financiamiento Portal, deberá Hola siguientes elementos:</span><span class="sxs-lookup"><span data-stu-id="63ad7-111">tooconfigure Azure AD integration with hello Funding Portal, you need hello following items:</span></span>

- <span data-ttu-id="63ad7-112">Una suscripción de Azure AD</span><span class="sxs-lookup"><span data-stu-id="63ad7-112">An Azure AD subscription</span></span>
- <span data-ttu-id="63ad7-113">Suscripción habilitada para un Hola financiación Portal inicio de sesión único</span><span class="sxs-lookup"><span data-stu-id="63ad7-113">A hello Funding Portal single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="63ad7-114">Hola tootest los pasos de este tutorial, no se recomienda usar un entorno de producción.</span><span class="sxs-lookup"><span data-stu-id="63ad7-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="63ad7-115">pasos de hello tootest en este tutorial, debe seguir estas recomendaciones:</span><span class="sxs-lookup"><span data-stu-id="63ad7-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="63ad7-116">No use el entorno de producción, salvo que sea necesario.</span><span class="sxs-lookup"><span data-stu-id="63ad7-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="63ad7-117">Si no dispone de un entorno de prueba de Azure AD, puede obtener una versión de prueba de un mes [aquí](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="63ad7-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="63ad7-118">Descripción del escenario</span><span class="sxs-lookup"><span data-stu-id="63ad7-118">Scenario description</span></span>
<span data-ttu-id="63ad7-119">En este tutorial, puede probar el inicio de sesión único de Azure AD en un entorno de prueba.</span><span class="sxs-lookup"><span data-stu-id="63ad7-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="63ad7-120">escenario de Hello descrito en este tutorial consta de dos bloques principales:</span><span class="sxs-lookup"><span data-stu-id="63ad7-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="63ad7-121">Agregar Hola financiamiento Portal desde la Galería de Hola</span><span class="sxs-lookup"><span data-stu-id="63ad7-121">Adding hello Funding Portal from hello gallery</span></span>
2. <span data-ttu-id="63ad7-122">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="63ad7-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-hello-funding-portal-from-hello-gallery"></a><span data-ttu-id="63ad7-123">Agregar Hola financiamiento Portal desde la Galería de Hola</span><span class="sxs-lookup"><span data-stu-id="63ad7-123">Adding hello Funding Portal from hello gallery</span></span>
<span data-ttu-id="63ad7-124">integración de hello tooconfigure de hello financiamiento Portal en Azure AD, deberá tooadd Hola Portal financiamiento de lista de tooyour Hola Galería de aplicaciones administradas de SaaS.</span><span class="sxs-lookup"><span data-stu-id="63ad7-124">tooconfigure hello integration of hello Funding Portal into Azure AD, you need tooadd hello Funding Portal from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="63ad7-125">**tooadd Hola financiación Portal desde la Galería de hello, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="63ad7-125">**tooadd hello Funding Portal from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="63ad7-126">Hola  **[portal de Azure](https://portal.azure.com)**, en el panel de navegación izquierdo de Hola, haga clic en **Azure Active Directory** icono.</span><span class="sxs-lookup"><span data-stu-id="63ad7-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="63ad7-128">Navegue demasiado**aplicaciones empresariales**.</span><span class="sxs-lookup"><span data-stu-id="63ad7-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="63ad7-129">A continuación, vaya demasiado**todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="63ad7-129">Then go too**All applications**.</span></span>

    ![Aplicaciones][2]
    
3. <span data-ttu-id="63ad7-131">tooadd nueva aplicación, haga clic en **nueva aplicación** botón en la parte superior de saludo del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="63ad7-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Aplicaciones][3]

4. <span data-ttu-id="63ad7-133">En el cuadro de búsqueda de hello, escriba **Hola financiación Portal**.</span><span class="sxs-lookup"><span data-stu-id="63ad7-133">In hello search box, type **hello Funding Portal**.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-thefundingportal-tutorial/tutorial_thefundingportal_search.png)

5. <span data-ttu-id="63ad7-135">En el panel de resultados de hello, seleccione **Hola financiación Portal**y, a continuación, haga clic en **agregar** botón aplicación hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="63ad7-135">In hello results panel, select **hello Funding Portal**, and then click **Add** button tooadd hello application.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-thefundingportal-tutorial/tutorial_thefundingportal_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="63ad7-137">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="63ad7-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="63ad7-138">En esta sección, configurar y probar el inicio de sesión único en Azure AD con hello que financiación Portal basado en un usuario de prueba denominado a "Bárbara Simon".</span><span class="sxs-lookup"><span data-stu-id="63ad7-138">In this section, you configure and test Azure AD single sign-on with hello Funding Portal based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="63ad7-139">Para toowork de inicio de sesión único, Azure AD necesita tooknow qué usuario equivalente de Hola Hola financiación Portal es tooa usuario en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="63ad7-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in hello Funding Portal is tooa user in Azure AD.</span></span> <span data-ttu-id="63ad7-140">En otras palabras, una relación de vínculo entre un usuario de Azure AD y el usuario relacionado de Hola Hola financiación Portal debe toobe establecido.</span><span class="sxs-lookup"><span data-stu-id="63ad7-140">In other words, a link relationship between an Azure AD user and hello related user in hello Funding Portal needs toobe established.</span></span>

<span data-ttu-id="63ad7-141">En el Portal financiación de Hola, asignar un valor de Hola de hello **nombre de usuario** en Azure AD como valor de Hola de hello **nombre de usuario** tooestablish la relación de vínculo de Hola.</span><span class="sxs-lookup"><span data-stu-id="63ad7-141">In hello Funding Portal, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="63ad7-142">tooconfigure y prueba de inicio de sesión único en Azure AD con hello financiamiento Portal, deberá hello toocomplete después de bloques de creación:</span><span class="sxs-lookup"><span data-stu-id="63ad7-142">tooconfigure and test Azure AD single sign-on with hello Funding Portal, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="63ad7-143">**[Configuración de Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable la toouse usuarios esta característica.</span><span class="sxs-lookup"><span data-stu-id="63ad7-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="63ad7-144">**[Crear un usuario de prueba de Azure AD](#creating-an-azure-ad-test-user)**  -inicio de sesión único en Azure AD tootest con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="63ad7-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="63ad7-145">**[Crear usuario de prueba de financiación Portal hello](#creating-the-funding-portal-test-user)**  -toohave un equivalente de Britta Simon Hola Portal financiamiento que es la representación toohello vinculado Azure AD del usuario.</span><span class="sxs-lookup"><span data-stu-id="63ad7-145">**[Creating hello Funding Portal test user](#creating-the-funding-portal-test-user)** - toohave a counterpart of Britta Simon in hello Funding Portal that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="63ad7-146">**[Asignar usuario de prueba de hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="63ad7-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="63ad7-147">**[Pruebas de Single Sign-On](#testing-single-sign-on)**  -tooverify Hola si funciona la configuración.</span><span class="sxs-lookup"><span data-stu-id="63ad7-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="63ad7-148">Configuración del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="63ad7-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="63ad7-149">En esta sección, habilitar inicio de sesión único en Azure AD en hello portal de Azure y configurar el inicio de sesión único en la aplicación de Portal financiación Hola.</span><span class="sxs-lookup"><span data-stu-id="63ad7-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your hello Funding Portal application.</span></span>

<span data-ttu-id="63ad7-150">**tooconfigure Azure AD inicio de sesión único con Hola financiación Portal, realizar Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="63ad7-150">**tooconfigure Azure AD single sign-on with hello Funding Portal, perform hello following steps:**</span></span>

1. <span data-ttu-id="63ad7-151">En el portal de Azure, en Hola Hola **Hola financiación Portal** página de integración de aplicaciones, haga clic en **inicio de sesión único**.</span><span class="sxs-lookup"><span data-stu-id="63ad7-151">In hello Azure portal, on hello **hello Funding Portal** application integration page, click **Single sign-on**.</span></span>

    ![Configurar inicio de sesión único][4]

2. <span data-ttu-id="63ad7-153">En hello **inicio de sesión único** cuadro de diálogo, seleccione **modo** como **sesión basado en SAML** tooenable inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="63ad7-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurar inicio de sesión único](./media/active-directory-saas-thefundingportal-tutorial/tutorial_thefundingportal_samlbase.png)

3. <span data-ttu-id="63ad7-155">En hello **Hola financiación Portal de dominio y las direcciones URL** sección, lleve a cabo Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="63ad7-155">On hello **hello Funding Portal Domain and URLs** section, perform hello following steps:</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-thefundingportal-tutorial/tutorial_thefundingportal_url.png)

    <span data-ttu-id="63ad7-157">a.</span><span class="sxs-lookup"><span data-stu-id="63ad7-157">a.</span></span> <span data-ttu-id="63ad7-158">Hola **dirección URL de inicio de sesión** cuadro de texto, escriba una dirección URL usando Hola siguiente patrón:`https://<subdomain>.regenteducation.net/`</span><span class="sxs-lookup"><span data-stu-id="63ad7-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<subdomain>.regenteducation.net/`</span></span>

    <span data-ttu-id="63ad7-159">b.</span><span class="sxs-lookup"><span data-stu-id="63ad7-159">b.</span></span> <span data-ttu-id="63ad7-160">Hola **identificador** cuadro de texto, escriba una dirección URL usando Hola siguiente patrón:`https://<subdomain>.regenteducation.net`</span><span class="sxs-lookup"><span data-stu-id="63ad7-160">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<subdomain>.regenteducation.net`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="63ad7-161">Estos valores no son reales.</span><span class="sxs-lookup"><span data-stu-id="63ad7-161">These values are not real.</span></span> <span data-ttu-id="63ad7-162">Actualizar estos valores con hello real de dirección URL de inicio de sesión y el identificador.</span><span class="sxs-lookup"><span data-stu-id="63ad7-162">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="63ad7-163">Póngase en contacto con [equipo de soporte técnico de cliente de Portal de financiación de Hola](mailto:info@regenteducation.com) tooget estos valores.</span><span class="sxs-lookup"><span data-stu-id="63ad7-163">Contact [hello Funding Portal Client support team](mailto:info@regenteducation.com) tooget these values.</span></span> 

4. <span data-ttu-id="63ad7-164">Hola la aplicación del Portal financiación espera toocontain de aserciones de SAML de hello un atributo denominado "externalId1".</span><span class="sxs-lookup"><span data-stu-id="63ad7-164">hello Funding Portal application expects hello SAML assertions toocontain an attribute named "externalId1".</span></span> <span data-ttu-id="63ad7-165">valor de Hola de "externalId1" debe ser un studentID reconocido.</span><span class="sxs-lookup"><span data-stu-id="63ad7-165">hello value of "externalId1" should be a recognized studentID.</span></span> <span data-ttu-id="63ad7-166">Configurar notificación de Hola "externalId1" para esta aplicación.</span><span class="sxs-lookup"><span data-stu-id="63ad7-166">Configure hello "externalId1" claim for this application.</span></span> <span data-ttu-id="63ad7-167">Puede administrar valores de hello de estos atributos de hello **atributos de usuario** de aplicación hello.</span><span class="sxs-lookup"><span data-stu-id="63ad7-167">You can manage hello values of these attributes from hello **User Attributes** of hello application.</span></span> <span data-ttu-id="63ad7-168">Hola siguiente captura de pantalla muestra un ejemplo de esto.</span><span class="sxs-lookup"><span data-stu-id="63ad7-168">hello following screenshot shows an example for this.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-thefundingportal-tutorial/tutorial_thefundingportal_attribute.png)

5. <span data-ttu-id="63ad7-170">Hola **atributos de usuario** sección en hello **inicio de sesión único** cuadro de diálogo, configurar atributos de token de SAML como se muestra en la imagen de Hola y realizar Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="63ad7-170">In hello **User Attributes** section on hello **Single sign-on** dialog, configure SAML token attribute as shown in hello image and perform hello following steps:</span></span>

    | <span data-ttu-id="63ad7-171">Nombre del atributo</span><span class="sxs-lookup"><span data-stu-id="63ad7-171">Attribute Name</span></span> | <span data-ttu-id="63ad7-172">Valor de atributo</span><span class="sxs-lookup"><span data-stu-id="63ad7-172">Attribute Value</span></span> |
    | ------------------- | ---------------- |
    | <span data-ttu-id="63ad7-173">externalId1</span><span class="sxs-lookup"><span data-stu-id="63ad7-173">externalId1</span></span> | <span data-ttu-id="63ad7-174">user.extensionattribute1</span><span class="sxs-lookup"><span data-stu-id="63ad7-174">user.extensionattribute1</span></span> |

    <span data-ttu-id="63ad7-175">a.</span><span class="sxs-lookup"><span data-stu-id="63ad7-175">a.</span></span> <span data-ttu-id="63ad7-176">Haga clic en **Agregar atributo** tooopen hello **Agregar atributo** cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="63ad7-176">Click **Add attribute** tooopen hello **Add Attribute** dialog.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-thefundingportal-tutorial/tutorial_attribute_04.png)

    ![Configurar inicio de sesión único](./media/active-directory-saas-thefundingportal-tutorial/tutorial_attribute_05.png)

    <span data-ttu-id="63ad7-179">b.</span><span class="sxs-lookup"><span data-stu-id="63ad7-179">b.</span></span> <span data-ttu-id="63ad7-180">Hola **nombre** cuadro de texto, nombre de atributo de tipo hello se muestra para esa fila.</span><span class="sxs-lookup"><span data-stu-id="63ad7-180">In hello **Name** textbox, type hello attribute name shown for that row.</span></span>

    <span data-ttu-id="63ad7-181">c.</span><span class="sxs-lookup"><span data-stu-id="63ad7-181">c.</span></span> <span data-ttu-id="63ad7-182">De hello **valor del atributo** lista, atributo Hola seleccione desea toouse para su implementación.</span><span class="sxs-lookup"><span data-stu-id="63ad7-182">From hello **Attribute Value** list, select hello attribute you want toouse for your implementation.</span></span> <span data-ttu-id="63ad7-183">Por ejemplo, si ha almacenado Hola StudentID valor Hola Atributodeextensión1, a continuación, seleccione user.extensionattribute1.</span><span class="sxs-lookup"><span data-stu-id="63ad7-183">For example, if you have stored hello StudentID value in hello ExtensionAttribute1, then select user.extensionattribute1.</span></span>
    
    <span data-ttu-id="63ad7-184">d.</span><span class="sxs-lookup"><span data-stu-id="63ad7-184">d.</span></span> <span data-ttu-id="63ad7-185">Haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="63ad7-185">Click **Ok**.</span></span>
 
6. <span data-ttu-id="63ad7-186">En hello **el certificado de firma de SAML** sección, haga clic en **Metadata XML** y, a continuación, guarde el archivo de metadatos de hello en el equipo.</span><span class="sxs-lookup"><span data-stu-id="63ad7-186">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-thefundingportal-tutorial/tutorial_thefundingportal_certificate.png) 

7. <span data-ttu-id="63ad7-188">Haga clic en el botón **Guardar** .</span><span class="sxs-lookup"><span data-stu-id="63ad7-188">Click **Save** button.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-thefundingportal-tutorial/tutorial_general_400.png)

8. <span data-ttu-id="63ad7-190">tooconfigure inicio de sesión único en **Hola financiación Portal** lado, necesita hello toosend descargado **Metadata XML** demasiado[Hola equipo de soporte técnico de financiación Portal](mailto:info@regenteducation.com).</span><span class="sxs-lookup"><span data-stu-id="63ad7-190">tooconfigure single sign-on on **hello Funding Portal** side, you need toosend hello downloaded **Metadata XML** too[hello Funding Portal support team](mailto:info@regenteducation.com).</span></span> <span data-ttu-id="63ad7-191">Establecen esta Hola de toohave configuración configurada correctamente en ambos lados de la conexión de SSO de SAML.</span><span class="sxs-lookup"><span data-stu-id="63ad7-191">They set this setting toohave hello SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="63ad7-192">Ahora puede leer una versión concisa de estas instrucciones dentro de hello [portal de Azure](https://portal.azure.com), mientras que está configurando la aplicación hello!</span><span class="sxs-lookup"><span data-stu-id="63ad7-192">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="63ad7-193">Después de agregar esta aplicación de hello **Active Directory > aplicaciones empresariales** sección, simplemente haga clic en hello **Single Sign-On** Hola de pestaña y acceso incrustado documentación a través de hello  **Configuración** sección final Hola.</span><span class="sxs-lookup"><span data-stu-id="63ad7-193">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="63ad7-194">Puede leer más acerca de características de documentación de embedded Hola aquí: [Azure AD incrustado documentación]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="63ad7-194">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="63ad7-195">Creación de un usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="63ad7-195">Creating an Azure AD test user</span></span>
<span data-ttu-id="63ad7-196">objetivo de Hola de esta sección es un usuario de prueba en hello Azure portal llamado a Britta Simon toocreate.</span><span class="sxs-lookup"><span data-stu-id="63ad7-196">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Creación de un usuario de Azure AD][100]

<span data-ttu-id="63ad7-198">**toocreate un usuario de prueba en Azure AD, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="63ad7-198">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="63ad7-199">Hola **portal de Azure**, en Hola panel de navegación izquierdo, haga clic en **Azure Active Directory** icono.</span><span class="sxs-lookup"><span data-stu-id="63ad7-199">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-thefundingportal-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="63ad7-201">lista de hello toodisplay de usuarios, vaya demasiado**usuarios y grupos** y haga clic en **todos los usuarios**.</span><span class="sxs-lookup"><span data-stu-id="63ad7-201">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-thefundingportal-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="63ad7-203">Hola tooopen **usuario** cuadro de diálogo, haga clic en **agregar** en la parte superior de saludo del cuadro de diálogo de Hola.</span><span class="sxs-lookup"><span data-stu-id="63ad7-203">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-thefundingportal-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="63ad7-205">En hello **usuario** cuadro de diálogo, siga los pasos de hello:</span><span class="sxs-lookup"><span data-stu-id="63ad7-205">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-thefundingportal-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="63ad7-207">a.</span><span class="sxs-lookup"><span data-stu-id="63ad7-207">a.</span></span> <span data-ttu-id="63ad7-208">Hola **nombre** cuadro de texto, tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="63ad7-208">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="63ad7-209">b.</span><span class="sxs-lookup"><span data-stu-id="63ad7-209">b.</span></span> <span data-ttu-id="63ad7-210">Hola **nombre de usuario** cuadro de texto, hello tipo **dirección de correo electrónico** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="63ad7-210">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="63ad7-211">c.</span><span class="sxs-lookup"><span data-stu-id="63ad7-211">c.</span></span> <span data-ttu-id="63ad7-212">Seleccione **Mostrar contraseña** y anote el valor de Hola de hello **contraseña**.</span><span class="sxs-lookup"><span data-stu-id="63ad7-212">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="63ad7-213">d.</span><span class="sxs-lookup"><span data-stu-id="63ad7-213">d.</span></span> <span data-ttu-id="63ad7-214">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="63ad7-214">Click **Create**.</span></span>
 
### <a name="creating-hello-funding-portal-test-user"></a><span data-ttu-id="63ad7-215">Creación de usuario de prueba de hello financiación Portal</span><span class="sxs-lookup"><span data-stu-id="63ad7-215">Creating hello Funding Portal test user</span></span>

<span data-ttu-id="63ad7-216">En esta sección, creará un usuario llamado a Britta Simon Hola financiamiento Portal.</span><span class="sxs-lookup"><span data-stu-id="63ad7-216">In this section, you create a user called Britta Simon in hello Funding Portal.</span></span> <span data-ttu-id="63ad7-217">Trabajar con [Hola equipo de soporte técnico de financiación Portal](mailto:info@regenteducation.com) tooadd Hola usuario de prueba y habilitar el SSO.</span><span class="sxs-lookup"><span data-stu-id="63ad7-217">Work with [hello Funding Portal support team](mailto:info@regenteducation.com) tooadd hello test user and enable SSO.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="63ad7-218">Asignación de usuario de prueba de hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="63ad7-218">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="63ad7-219">En esta sección, se habilita Britta Simon toouse un inicio de sesión único Azure concediendo acceso toohello financiamiento Portal.</span><span class="sxs-lookup"><span data-stu-id="63ad7-219">In this section, you enable Britta Simon toouse Azure single sign-on by granting access toohello Funding Portal.</span></span>

![Asignar usuario][200] 

<span data-ttu-id="63ad7-221">**tooassign Britta Simon toohello financiamiento Portal, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="63ad7-221">**tooassign Britta Simon toohello Funding Portal, perform hello following steps:**</span></span>

1. <span data-ttu-id="63ad7-222">Hola portal de Azure, abra la vista de aplicaciones de hello y, a continuación, navegue a vista de directorio toohello y vaya demasiado**aplicaciones empresariales** , a continuación, haga clic en **todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="63ad7-222">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Asignar usuario][201] 

2. <span data-ttu-id="63ad7-224">En la lista de aplicaciones de hello, seleccione **Hola financiación Portal**.</span><span class="sxs-lookup"><span data-stu-id="63ad7-224">In hello applications list, select **hello Funding Portal**.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-thefundingportal-tutorial/tutorial_thefundingportal_app.png) 

3. <span data-ttu-id="63ad7-226">En el menú de Hola Hola izquierda, haga clic en **usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="63ad7-226">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Asignar usuario][202] 

4. <span data-ttu-id="63ad7-228">Haga clic en el botón **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="63ad7-228">Click **Add** button.</span></span> <span data-ttu-id="63ad7-229">Después, seleccione **Usuarios y grupos** en el cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="63ad7-229">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Asignar usuario][203]

5. <span data-ttu-id="63ad7-231">En **usuarios y grupos** cuadro de diálogo, seleccione **Britta Simon** en la lista de usuarios de Hola.</span><span class="sxs-lookup"><span data-stu-id="63ad7-231">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="63ad7-232">Haga clic en el botón **Seleccionar** del cuadro de diálogo **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="63ad7-232">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="63ad7-233">Haga clic en el botón **Asignar** del cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="63ad7-233">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="63ad7-234">Prueba del inicio de sesión único </span><span class="sxs-lookup"><span data-stu-id="63ad7-234">Testing single sign-on</span></span>

<span data-ttu-id="63ad7-235">objetivo de Hola de esta sección es tootest su configuración de inicio de sesión único de Azure AD mediante Hola Panel de acceso.</span><span class="sxs-lookup"><span data-stu-id="63ad7-235">hello objective of this section is tootest your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="63ad7-236">Al hacer clic en icono de Portal financiación Hola Hola Hola Panel de acceso, deberá obtener la aplicación del Portal de financiación hello tooyour automáticamente ha iniciado sesión.</span><span class="sxs-lookup"><span data-stu-id="63ad7-236">When you click hello hello Funding Portal tile in hello Access Panel, you should get automatically signed-on tooyour hello Funding Portal application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="63ad7-237">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="63ad7-237">Additional resources</span></span>

* [<span data-ttu-id="63ad7-238">Lista de tutoriales sobre cómo tooIntegrate aplicaciones de SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="63ad7-238">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="63ad7-239">¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="63ad7-239">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-thefundingportal-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-thefundingportal-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-thefundingportal-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-thefundingportal-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-thefundingportal-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-thefundingportal-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-thefundingportal-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-thefundingportal-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-thefundingportal-tutorial/tutorial_general_203.png

