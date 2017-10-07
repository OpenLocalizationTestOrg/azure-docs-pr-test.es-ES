---
title: "Tutorial: Integración de Azure Active Directory con Boomi | Microsoft Docs"
description: "Obtenga información acerca de cómo tooconfigure inicio de sesión único entre Azure Active Directory y Boomi."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 8e05afa9-2eda-4975-a0cc-6d408065860f
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/30/2017
ms.author: jeedes
ms.openlocfilehash: ce64a4561697d311a8c7b1b244315bb552c5cfb7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-boomi"></a><span data-ttu-id="11a1f-103">Tutorial: Integración de Azure Active Directory con Boomi</span><span class="sxs-lookup"><span data-stu-id="11a1f-103">Tutorial: Azure Active Directory integration with Boomi</span></span>

<span data-ttu-id="11a1f-104">En este tutorial, aprenderá cómo toointegrate Boomi con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="11a1f-104">In this tutorial, you learn how toointegrate Boomi with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="11a1f-105">Integración de Boomi con Azure AD proporciona Hola siguientes ventajas:</span><span class="sxs-lookup"><span data-stu-id="11a1f-105">Integrating Boomi with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="11a1f-106">Puede controlar en Azure AD que tenga acceso tooBoomi</span><span class="sxs-lookup"><span data-stu-id="11a1f-106">You can control in Azure AD who has access tooBoomi</span></span>
- <span data-ttu-id="11a1f-107">Puede habilitar los usuarios tooautomatically get ha iniciado sesión tooBoomi (Single Sign-On) con sus cuentas de Azure AD</span><span class="sxs-lookup"><span data-stu-id="11a1f-107">You can enable your users tooautomatically get signed-on tooBoomi (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="11a1f-108">Puede administrar las cuentas en una ubicación central: Hola portal de Azure</span><span class="sxs-lookup"><span data-stu-id="11a1f-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="11a1f-109">Si desea obtener más información acerca de la integración de aplicaciones de SaaS con Azure AD tooknow, consulte [¿qué es acceso a la aplicación y el inicio de sesión único con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="11a1f-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="11a1f-110">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="11a1f-110">Prerequisites</span></span>

<span data-ttu-id="11a1f-111">integración de Azure AD con Boomi tooconfigure, necesita Hola siguientes elementos:</span><span class="sxs-lookup"><span data-stu-id="11a1f-111">tooconfigure Azure AD integration with Boomi, you need hello following items:</span></span>

- <span data-ttu-id="11a1f-112">Una suscripción de Azure AD</span><span class="sxs-lookup"><span data-stu-id="11a1f-112">An Azure AD subscription</span></span>
- <span data-ttu-id="11a1f-113">Una suscripción habilitada para inicio de sesión único en Boomi</span><span class="sxs-lookup"><span data-stu-id="11a1f-113">A Boomi single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="11a1f-114">Hola tootest los pasos de este tutorial, no se recomienda usar un entorno de producción.</span><span class="sxs-lookup"><span data-stu-id="11a1f-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="11a1f-115">pasos de hello tootest en este tutorial, debe seguir estas recomendaciones:</span><span class="sxs-lookup"><span data-stu-id="11a1f-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="11a1f-116">No use el entorno de producción, salvo que sea necesario.</span><span class="sxs-lookup"><span data-stu-id="11a1f-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="11a1f-117">Si no dispone de un entorno de prueba de Azure AD, puede obtener una versión de prueba de un mes [aquí](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="11a1f-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="11a1f-118">Descripción del escenario</span><span class="sxs-lookup"><span data-stu-id="11a1f-118">Scenario description</span></span>
<span data-ttu-id="11a1f-119">En este tutorial, puede probar el inicio de sesión único de Azure AD en un entorno de prueba.</span><span class="sxs-lookup"><span data-stu-id="11a1f-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="11a1f-120">escenario de Hello descrito en este tutorial consta de dos bloques principales:</span><span class="sxs-lookup"><span data-stu-id="11a1f-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="11a1f-121">Adición de Boomi de galería de Hola</span><span class="sxs-lookup"><span data-stu-id="11a1f-121">Adding Boomi from hello gallery</span></span>
2. <span data-ttu-id="11a1f-122">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="11a1f-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-boomi-from-hello-gallery"></a><span data-ttu-id="11a1f-123">Adición de Boomi de galería de Hola</span><span class="sxs-lookup"><span data-stu-id="11a1f-123">Adding Boomi from hello gallery</span></span>
<span data-ttu-id="11a1f-124">integración de hello tooconfigure de Boomi en Azure AD, deberá tooadd Boomi de lista de tooyour Hola Galería de aplicaciones administradas de SaaS.</span><span class="sxs-lookup"><span data-stu-id="11a1f-124">tooconfigure hello integration of Boomi into Azure AD, you need tooadd Boomi from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="11a1f-125">**tooadd Boomi de galería de hello, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="11a1f-125">**tooadd Boomi from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="11a1f-126">Hola  **[portal de Azure](https://portal.azure.com)**, en el panel de navegación izquierdo de Hola, haga clic en **Azure Active Directory** icono.</span><span class="sxs-lookup"><span data-stu-id="11a1f-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="11a1f-128">Navegue demasiado**aplicaciones empresariales**.</span><span class="sxs-lookup"><span data-stu-id="11a1f-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="11a1f-129">A continuación, vaya demasiado**todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="11a1f-129">Then go too**All applications**.</span></span>

    ![Aplicaciones][2]
    
3. <span data-ttu-id="11a1f-131">tooadd nueva aplicación, haga clic en **nueva aplicación** botón en la parte superior de saludo del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="11a1f-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Aplicaciones][3]

4. <span data-ttu-id="11a1f-133">En el cuadro de búsqueda de hello, escriba **Boomi**.</span><span class="sxs-lookup"><span data-stu-id="11a1f-133">In hello search box, type **Boomi**.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-boomi-tutorial/tutorial_boomi_search.png)

5. <span data-ttu-id="11a1f-135">En el panel de resultados de hello, seleccione **Boomi**y, a continuación, haga clic en **agregar** botón aplicación hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="11a1f-135">In hello results panel, select **Boomi**, and then click **Add** button tooadd hello application.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-boomi-tutorial/tutorial_boomi_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="11a1f-137">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="11a1f-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="11a1f-138">En esta sección, podrá configurar y probar el inicio de sesión único de Azure AD con Boomi con un usuario de prueba llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="11a1f-138">In this section, you configure and test Azure AD single sign-on with Boomi based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="11a1f-139">Para toowork de inicio de sesión único, Azure AD necesita tooknow qué usuario equivalente de hello en Boomi es tooa usuario en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="11a1f-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Boomi is tooa user in Azure AD.</span></span> <span data-ttu-id="11a1f-140">En otras palabras, una relación de vínculo entre un usuario de Azure AD y el usuario relacionado de hello en Boomi debe toobe establecido.</span><span class="sxs-lookup"><span data-stu-id="11a1f-140">In other words, a link relationship between an Azure AD user and hello related user in Boomi needs toobe established.</span></span>

<span data-ttu-id="11a1f-141">En Boomi, asigne el valor de Hola de hello **nombre de usuario** en Azure AD como valor de Hola de hello **nombre de usuario** tooestablish la relación de vínculo de Hola.</span><span class="sxs-lookup"><span data-stu-id="11a1f-141">In Boomi, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="11a1f-142">tooconfigure y prueba de inicio de sesión único en Azure AD con Boomi, deberá hello toocomplete después de bloques de creación:</span><span class="sxs-lookup"><span data-stu-id="11a1f-142">tooconfigure and test Azure AD single sign-on with Boomi, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="11a1f-143">**[Configuración de Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable la toouse usuarios esta característica.</span><span class="sxs-lookup"><span data-stu-id="11a1f-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="11a1f-144">**[Crear un usuario de prueba de Azure AD](#creating-an-azure-ad-test-user)**  -inicio de sesión único en Azure AD tootest con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="11a1f-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="11a1f-145">**[Crear un usuario de prueba de Boomi](#creating-a-boomi-test-user)**  -toohave un equivalente de Britta Simon en Boomi que es la representación toohello vinculado Azure AD del usuario.</span><span class="sxs-lookup"><span data-stu-id="11a1f-145">**[Creating a Boomi test user](#creating-a-boomi-test-user)** - toohave a counterpart of Britta Simon in Boomi that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="11a1f-146">**[Asignar usuario de prueba de hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="11a1f-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="11a1f-147">**[Pruebas de Single Sign-On](#testing-single-sign-on)**  -tooverify Hola si funciona la configuración.</span><span class="sxs-lookup"><span data-stu-id="11a1f-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="11a1f-148">Configuración del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="11a1f-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="11a1f-149">En esta sección, habilitar inicio de sesión único en Azure AD en hello portal de Azure y configurar el inicio de sesión único en la aplicación de Boomi.</span><span class="sxs-lookup"><span data-stu-id="11a1f-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Boomi application.</span></span>

<span data-ttu-id="11a1f-150">**inicio de sesión único en Azure AD tooconfigure con Boomi, siga Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="11a1f-150">**tooconfigure Azure AD single sign-on with Boomi, perform hello following steps:**</span></span>

1. <span data-ttu-id="11a1f-151">En el portal de Azure, en Hola Hola **Boomi** página de integración de aplicaciones, haga clic en **inicio de sesión único**.</span><span class="sxs-lookup"><span data-stu-id="11a1f-151">In hello Azure portal, on hello **Boomi** application integration page, click **Single sign-on**.</span></span>

    ![Configurar inicio de sesión único][4]

2. <span data-ttu-id="11a1f-153">En hello **inicio de sesión único** cuadro de diálogo, seleccione **modo** como **sesión basado en SAML** tooenable inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="11a1f-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurar inicio de sesión único](./media/active-directory-saas-boomi-tutorial/tutorial_boomi_samlbase.png)

3. <span data-ttu-id="11a1f-155">En hello **Boomi dominio y las direcciones URL** sección, lleve a cabo Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="11a1f-155">On hello **Boomi Domain and URLs** section, perform hello following steps:</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-boomi-tutorial/tutorial_boomi_url.png)

    <span data-ttu-id="11a1f-157">a.</span><span class="sxs-lookup"><span data-stu-id="11a1f-157">a.</span></span> <span data-ttu-id="11a1f-158">Hola **identificador** cuadro de texto, escriba una dirección URL usando Hola siguiente patrón:`https://platform.boomi.com/sso/<accountname>/saml`</span><span class="sxs-lookup"><span data-stu-id="11a1f-158">In hello **Identifier** textbox, type a URL using hello following pattern: `https://platform.boomi.com/sso/<accountname>/saml`</span></span>

    <span data-ttu-id="11a1f-159">b.</span><span class="sxs-lookup"><span data-stu-id="11a1f-159">b.</span></span> <span data-ttu-id="11a1f-160">Hola **dirección URL de respuesta** cuadro de texto, escriba una dirección URL usando Hola siguiente patrón:`https://platform.boomi.com/sso/<accountname>/saml`</span><span class="sxs-lookup"><span data-stu-id="11a1f-160">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://platform.boomi.com/sso/<accountname>/saml`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="11a1f-161">Estos valores no son reales.</span><span class="sxs-lookup"><span data-stu-id="11a1f-161">These values are not real.</span></span> <span data-ttu-id="11a1f-162">Actualizar estos valores con hello URL de identificador y la respuesta real.</span><span class="sxs-lookup"><span data-stu-id="11a1f-162">Update these values with hello actual Identifier and Reply URL.</span></span> <span data-ttu-id="11a1f-163">Póngase en contacto con [equipo de soporte técnico de Boomi](https://boomi.com/company/contact/) tooget estos valores.</span><span class="sxs-lookup"><span data-stu-id="11a1f-163">Contact [Boomi support team](https://boomi.com/company/contact/) tooget these values.</span></span>

4. <span data-ttu-id="11a1f-164">En hello **el certificado de firma de SAML** sección, haga clic en **Certificate(Base64)** y, a continuación, guarde el archivo de certificado de hello en el equipo.</span><span class="sxs-lookup"><span data-stu-id="11a1f-164">On hello **SAML Signing Certificate** section, click **Certificate(Base64)** and then save hello certificate file on your computer.</span></span>
    
    ![Configurar inicio de sesión único](./media/active-directory-saas-boomi-tutorial/tutorial_boomi_certificate.png)

4. <span data-ttu-id="11a1f-166">Aplicación de Boomi espera las aserciones de SAML de hello en un formato concreto.</span><span class="sxs-lookup"><span data-stu-id="11a1f-166">Boomi application expects hello SAML assertions in a specific format.</span></span> <span data-ttu-id="11a1f-167">Configure Hola después de notificaciones para esta aplicación.</span><span class="sxs-lookup"><span data-stu-id="11a1f-167">Please configure hello following claims for this application.</span></span> <span data-ttu-id="11a1f-168">Puede administrar valores de hello de estos atributos de Hola "**atributos de usuario**" sección en la página de integración de aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="11a1f-168">You can manage hello values of these attributes from hello "**User Attributes**" section on application integration page.</span></span> <span data-ttu-id="11a1f-169">Hola siguiente captura de pantalla muestra un ejemplo de esto.</span><span class="sxs-lookup"><span data-stu-id="11a1f-169">hello following screenshot shows an example for this.</span></span>
    
    ![Configurar inicio de sesión único](./media/active-directory-saas-boomi-tutorial/tutorial_attribute.png)

5. <span data-ttu-id="11a1f-171">Hola **atributos de usuario** sección en hello **inicio de sesión único** cuadro de diálogo, para cada fila se muestra en la tabla de Hola a continuación, realizar Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="11a1f-171">In hello **User Attributes** section on hello **Single sign-on** dialog, for each row shown in hello table below, perform hello following steps:</span></span>

    | <span data-ttu-id="11a1f-172">Nombre del atributo</span><span class="sxs-lookup"><span data-stu-id="11a1f-172">Attribute Name</span></span> | <span data-ttu-id="11a1f-173">Valor de atributo</span><span class="sxs-lookup"><span data-stu-id="11a1f-173">Attribute Value</span></span> |
    | -------------- | --------------- |
    | <span data-ttu-id="11a1f-174">FEDERATION_ID</span><span class="sxs-lookup"><span data-stu-id="11a1f-174">FEDERATION_ID</span></span> | <span data-ttu-id="11a1f-175">user.mail</span><span class="sxs-lookup"><span data-stu-id="11a1f-175">user.mail</span></span> |
    
    <span data-ttu-id="11a1f-176">a.</span><span class="sxs-lookup"><span data-stu-id="11a1f-176">a.</span></span> <span data-ttu-id="11a1f-177">Haga clic en **Agregar atributo** tooopen hello **Agregar atributo** cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="11a1f-177">Click **Add attribute** tooopen hello **Add Attribute** dialog.</span></span>
    
    ![Configurar inicio de sesión único](./media/active-directory-saas-boomi-tutorial/tutorial_attribute_04.png)
    
    ![Configurar inicio de sesión único](./media/active-directory-saas-boomi-tutorial/tutorial_attribute_05.png)
    
    <span data-ttu-id="11a1f-180">b.</span><span class="sxs-lookup"><span data-stu-id="11a1f-180">b.</span></span> <span data-ttu-id="11a1f-181">Hola **nombre** cuadro de texto, nombre de atributo de tipo hello se muestra para esa fila.</span><span class="sxs-lookup"><span data-stu-id="11a1f-181">In hello **Name** textbox, type hello attribute name shown for that row.</span></span>
    
    <span data-ttu-id="11a1f-182">c.</span><span class="sxs-lookup"><span data-stu-id="11a1f-182">c.</span></span> <span data-ttu-id="11a1f-183">De hello **valor** lista, el valor de atributo de tipo hello se muestra para esa fila.</span><span class="sxs-lookup"><span data-stu-id="11a1f-183">From hello **Value** list, type hello attribute value shown for that row.</span></span>
    
    <span data-ttu-id="11a1f-184">d.</span><span class="sxs-lookup"><span data-stu-id="11a1f-184">d.</span></span> <span data-ttu-id="11a1f-185">Haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="11a1f-185">Click **Ok**.</span></span>

6. <span data-ttu-id="11a1f-186">Haga clic en el botón **Guardar** .</span><span class="sxs-lookup"><span data-stu-id="11a1f-186">Click **Save** button.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-boomi-tutorial/tutorial_general_400.png)

7. <span data-ttu-id="11a1f-188">En hello **configuración de Boomi** sección, haga clic en **configurar Boomi** tooopen **configurar inicio de sesión** ventana.</span><span class="sxs-lookup"><span data-stu-id="11a1f-188">On hello **Boomi Configuration** section, click **Configure Boomi** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="11a1f-189">Hola copia **SAML Single Sign-On dirección URL del servicio** de hello **sección de referencia rápida.**</span><span class="sxs-lookup"><span data-stu-id="11a1f-189">Copy hello **SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-boomi-tutorial/tutorial_boomi_configure.png) 

8. <span data-ttu-id="11a1f-191">En otra ventana del explorador web, inicie sesión como administrador en el sitio de la compañía de Boomi.</span><span class="sxs-lookup"><span data-stu-id="11a1f-191">In a different web browser window, log into your Boomi company site as an administrator.</span></span> 

9. <span data-ttu-id="11a1f-192">Navegue demasiado**nombre de la compañía** y vaya demasiado**configurar**.</span><span class="sxs-lookup"><span data-stu-id="11a1f-192">Navigate too**Company Name** and go too**Set up**.</span></span>

10. <span data-ttu-id="11a1f-193">Haga clic en hello **opciones SSO** ficha y realice los pasos siguientes.</span><span class="sxs-lookup"><span data-stu-id="11a1f-193">Click hello **SSO Options** tab and perform below steps.</span></span>

    ![Configuración del inicio de sesión único en la aplicación](./media/active-directory-saas-boomi-tutorial/tutorial_boomi_11.png)

    <span data-ttu-id="11a1f-195">a.</span><span class="sxs-lookup"><span data-stu-id="11a1f-195">a.</span></span> <span data-ttu-id="11a1f-196">Marque la casilla **Enable SAML Single Sign-On** (Habilitar el inicio de sesión único de SAML).</span><span class="sxs-lookup"><span data-stu-id="11a1f-196">Check **Enable SAML Single Sign-On** checkbox.</span></span>

    <span data-ttu-id="11a1f-197">b.</span><span class="sxs-lookup"><span data-stu-id="11a1f-197">b.</span></span> <span data-ttu-id="11a1f-198">Haga clic en **importación** hello tooupload descarga certificado de Azure AD demasiado**certificado del proveedor de identidad**.</span><span class="sxs-lookup"><span data-stu-id="11a1f-198">Click **Import** tooupload hello downloaded certificate from Azure AD too**Identity Provider Certificate**.</span></span>
    
    <span data-ttu-id="11a1f-199">c.</span><span class="sxs-lookup"><span data-stu-id="11a1f-199">c.</span></span> <span data-ttu-id="11a1f-200">Hola **URL de inicio de sesión del proveedor de identidades** cuadro de texto, coloque valor Hola de **SAML Single Sign-On dirección URL del servicio** desde la ventana de configuración de aplicación de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="11a1f-200">In hello **Identity Provider Login URL** textbox, put hello value of **SAML Single Sign-On Service URL** from Azure AD application configuration window.</span></span>

    <span data-ttu-id="11a1f-201">d.</span><span class="sxs-lookup"><span data-stu-id="11a1f-201">d.</span></span> <span data-ttu-id="11a1f-202">Como **ubicación del identificador de federación**, seleccione el botón de radio **Federation Id is in FEDERATION_ID Attribute element** (El id. de federación está en el elemento de atributo FEDERATION_ID).</span><span class="sxs-lookup"><span data-stu-id="11a1f-202">As **Federation Id Location**, select **Federation Id is in FEDERATION_ID Attribute element** radio button.</span></span> 

    <span data-ttu-id="11a1f-203">e.</span><span class="sxs-lookup"><span data-stu-id="11a1f-203">e.</span></span> <span data-ttu-id="11a1f-204">Haga clic en el botón **Guardar** .</span><span class="sxs-lookup"><span data-stu-id="11a1f-204">Click **Save** button.</span></span>

> [!TIP]
> <span data-ttu-id="11a1f-205">Ahora puede leer una versión concisa de estas instrucciones dentro de hello [portal de Azure](https://portal.azure.com), mientras que está configurando la aplicación hello!</span><span class="sxs-lookup"><span data-stu-id="11a1f-205">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="11a1f-206">Después de agregar esta aplicación de hello **Active Directory > aplicaciones empresariales** sección, simplemente haga clic en hello **Single Sign-On** Hola de pestaña y acceso incrustado documentación a través de hello  **Configuración** sección final Hola.</span><span class="sxs-lookup"><span data-stu-id="11a1f-206">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="11a1f-207">Puede leer más acerca de características de documentación de embedded Hola aquí: [Azure AD incrustado documentación]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="11a1f-207">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="11a1f-208">Creación de un usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="11a1f-208">Creating an Azure AD test user</span></span>
<span data-ttu-id="11a1f-209">objetivo de Hola de esta sección es un usuario de prueba en hello Azure portal llamado a Britta Simon toocreate.</span><span class="sxs-lookup"><span data-stu-id="11a1f-209">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Creación de un usuario de Azure AD][100]

<span data-ttu-id="11a1f-211">**toocreate un usuario de prueba en Azure AD, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="11a1f-211">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="11a1f-212">Hola **portal de Azure**, en Hola panel de navegación izquierdo, haga clic en **Azure Active Directory** icono.</span><span class="sxs-lookup"><span data-stu-id="11a1f-212">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-boomi-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="11a1f-214">lista de hello toodisplay de usuarios, vaya demasiado**usuarios y grupos** y haga clic en **todos los usuarios**.</span><span class="sxs-lookup"><span data-stu-id="11a1f-214">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-boomi-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="11a1f-216">Hola tooopen **usuario** cuadro de diálogo, haga clic en **agregar** en la parte superior de saludo del cuadro de diálogo de Hola.</span><span class="sxs-lookup"><span data-stu-id="11a1f-216">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-boomi-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="11a1f-218">En hello **usuario** cuadro de diálogo, siga los pasos de hello:</span><span class="sxs-lookup"><span data-stu-id="11a1f-218">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-boomi-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="11a1f-220">a.</span><span class="sxs-lookup"><span data-stu-id="11a1f-220">a.</span></span> <span data-ttu-id="11a1f-221">Hola **nombre** cuadro de texto, tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="11a1f-221">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="11a1f-222">b.</span><span class="sxs-lookup"><span data-stu-id="11a1f-222">b.</span></span> <span data-ttu-id="11a1f-223">Hola **nombre de usuario** cuadro de texto, hello tipo **dirección de correo electrónico** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="11a1f-223">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="11a1f-224">c.</span><span class="sxs-lookup"><span data-stu-id="11a1f-224">c.</span></span> <span data-ttu-id="11a1f-225">Seleccione **Mostrar contraseña** y anote el valor de Hola de hello **contraseña**.</span><span class="sxs-lookup"><span data-stu-id="11a1f-225">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="11a1f-226">d.</span><span class="sxs-lookup"><span data-stu-id="11a1f-226">d.</span></span> <span data-ttu-id="11a1f-227">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="11a1f-227">Click **Create**.</span></span>
 
### <a name="creating-a-boomi-test-user"></a><span data-ttu-id="11a1f-228">Creación de un usuario de prueba de Boomi</span><span class="sxs-lookup"><span data-stu-id="11a1f-228">Creating a Boomi test user</span></span>

<span data-ttu-id="11a1f-229">En orden tooenable toolog de los usuarios de Azure AD en tooBoomi, se les deben aprovisionar en Boomi.</span><span class="sxs-lookup"><span data-stu-id="11a1f-229">In order tooenable Azure AD users toolog in tooBoomi, they must be provisioned into Boomi.</span></span> <span data-ttu-id="11a1f-230">En caso de hello de Boomi, el aprovisionamiento es una tarea manual.</span><span class="sxs-lookup"><span data-stu-id="11a1f-230">In hello case of Boomi, provisioning is a manual task.</span></span>

### <a name="tooprovision-a-user-account-perform-hello-following-steps"></a><span data-ttu-id="11a1f-231">tooprovision una cuenta de usuario, lleve a cabo Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="11a1f-231">tooprovision a user account, perform hello following steps:</span></span>

1. <span data-ttu-id="11a1f-232">Inicie sesión en tooyour sitio Boomi de su compañía como administrador.</span><span class="sxs-lookup"><span data-stu-id="11a1f-232">Log in tooyour Boomi company site as an administrator.</span></span>

2. <span data-ttu-id="11a1f-233">Después de iniciar sesión, navegar demasiado**administración de usuarios** y vaya demasiado**usuarios**.</span><span class="sxs-lookup"><span data-stu-id="11a1f-233">After logging in, navigate too**User Management** and go too**Users**.</span></span>

    <span data-ttu-id="11a1f-234">![Usuarios](./media/active-directory-saas-boomi-tutorial/tutorial_boomi_001.png "Usuarios")</span><span class="sxs-lookup"><span data-stu-id="11a1f-234">![Users](./media/active-directory-saas-boomi-tutorial/tutorial_boomi_001.png "Users")</span></span>

3. <span data-ttu-id="11a1f-235">Haga clic en  **+**  hello e icono **agregar y mantener los Roles de usuario** abre el cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="11a1f-235">Click **+**  icon and hello **Add/Maintain User Roles** dialog opens.</span></span>

    <span data-ttu-id="11a1f-236">![Usuarios](./media/active-directory-saas-boomi-tutorial/tutorial_boomi_002.png "Usuarios")</span><span class="sxs-lookup"><span data-stu-id="11a1f-236">![Users](./media/active-directory-saas-boomi-tutorial/tutorial_boomi_002.png "Users")</span></span>

    <span data-ttu-id="11a1f-237">![Usuarios](./media/active-directory-saas-boomi-tutorial/tutorial_boomi_003.png "Usuarios")</span><span class="sxs-lookup"><span data-stu-id="11a1f-237">![Users](./media/active-directory-saas-boomi-tutorial/tutorial_boomi_003.png "Users")</span></span>

    <span data-ttu-id="11a1f-238">a.</span><span class="sxs-lookup"><span data-stu-id="11a1f-238">a.</span></span> <span data-ttu-id="11a1f-239">Hola **dirección de correo electrónico del usuario** Hola de tipo de correo electrónico del usuario, cuadro de texto, como BrittaSimon@contoso.com.</span><span class="sxs-lookup"><span data-stu-id="11a1f-239">In hello **User e-mail address** textbox, type hello email of user like BrittaSimon@contoso.com.</span></span>
    
    <span data-ttu-id="11a1f-240">b.</span><span class="sxs-lookup"><span data-stu-id="11a1f-240">b.</span></span> <span data-ttu-id="11a1f-241">Hola **nombre** cuadro de texto, tipo hello nombre de usuario como Bárbara.</span><span class="sxs-lookup"><span data-stu-id="11a1f-241">In hello **First name** textbox, type hello First name of user like Britta.</span></span>

    <span data-ttu-id="11a1f-242">c.</span><span class="sxs-lookup"><span data-stu-id="11a1f-242">c.</span></span> <span data-ttu-id="11a1f-243">Hola **apellidos** cuadro de texto, escriba Hola apellidos del usuario como Simon.</span><span class="sxs-lookup"><span data-stu-id="11a1f-243">In hello **Last name** textbox, type hello Last name of user like Simon.</span></span>
    
    <span data-ttu-id="11a1f-244">d.</span><span class="sxs-lookup"><span data-stu-id="11a1f-244">d.</span></span> <span data-ttu-id="11a1f-245">Escriba del usuario de hello **identificador de federación**.</span><span class="sxs-lookup"><span data-stu-id="11a1f-245">Enter hello user's **Federation ID**.</span></span> <span data-ttu-id="11a1f-246">Cada usuario debe tener un identificador de federación que identifica de forma única usuario Hola dentro de la cuenta de hello.</span><span class="sxs-lookup"><span data-stu-id="11a1f-246">Each user must have a Federation ID that uniquely identifies hello user within hello account.</span></span>
    
    <span data-ttu-id="11a1f-247">e.</span><span class="sxs-lookup"><span data-stu-id="11a1f-247">e.</span></span> <span data-ttu-id="11a1f-248">Asignar Hola **usuario estándar** usuario toohello de rol.</span><span class="sxs-lookup"><span data-stu-id="11a1f-248">Assign hello **Standard User** role toohello user.</span></span> <span data-ttu-id="11a1f-249">No se debe asignar el rol de administrador de hello porque dispondría de invertir el acceso normal de ambiente, así como acceso de inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="11a1f-249">Do not assign hello Administrator role because that would give him normal Atmosphere access as well as single sign-on access.</span></span>
    
    <span data-ttu-id="11a1f-250">f.</span><span class="sxs-lookup"><span data-stu-id="11a1f-250">f.</span></span> <span data-ttu-id="11a1f-251">Haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="11a1f-251">Click **OK**.</span></span>
    
    > [!NOTE]
    > <span data-ttu-id="11a1f-252">usuario de Hello no recibirá un correo electrónico de bienvenida de notificación que contiene una contraseña que puede ser utilizado toolog en toohello AtomSphere cuenta porque su contraseña se administra a través del proveedor de identidades de Hola.</span><span class="sxs-lookup"><span data-stu-id="11a1f-252">hello user will not receive a welcome notification email containing a password that can be used toolog in toohello AtomSphere account because his password is managed through hello identity provider.</span></span> <span data-ttu-id="11a1f-253">Puede usar cualquier otra Boomi usuario cuenta herramienta de creación o las API proporcionadas por Boomi tooprovision cuentas de usuario AAD.</span><span class="sxs-lookup"><span data-stu-id="11a1f-253">You may use any other Boomi user account creation tools or APIs provided by Boomi tooprovision AAD user accounts.</span></span> 

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="11a1f-254">Asignación de usuario de prueba de hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="11a1f-254">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="11a1f-255">En esta sección, se habilita Britta Simon toouse un inicio de sesión único Azure concediendo acceso tooBoomi.</span><span class="sxs-lookup"><span data-stu-id="11a1f-255">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooBoomi.</span></span>

![Asignar usuario][200] 

<span data-ttu-id="11a1f-257">**tooassign Britta Simon tooBoomi, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="11a1f-257">**tooassign Britta Simon tooBoomi, perform hello following steps:**</span></span>

1. <span data-ttu-id="11a1f-258">Hola portal de Azure, abra la vista de aplicaciones de hello y, a continuación, navegue a vista de directorio toohello y vaya demasiado**aplicaciones empresariales** , a continuación, haga clic en **todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="11a1f-258">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Asignar usuario][201] 

2. <span data-ttu-id="11a1f-260">En la lista de aplicaciones de hello, seleccione **Boomi**.</span><span class="sxs-lookup"><span data-stu-id="11a1f-260">In hello applications list, select **Boomi**.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-boomi-tutorial/tutorial_boomi_app.png) 

3. <span data-ttu-id="11a1f-262">En el menú de Hola Hola izquierda, haga clic en **usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="11a1f-262">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Asignar usuario][202] 

4. <span data-ttu-id="11a1f-264">Haga clic en el botón **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="11a1f-264">Click **Add** button.</span></span> <span data-ttu-id="11a1f-265">Después, seleccione **Usuarios y grupos** en el cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="11a1f-265">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Asignar usuario][203]

5. <span data-ttu-id="11a1f-267">En **usuarios y grupos** cuadro de diálogo, seleccione **Britta Simon** en la lista de usuarios de Hola.</span><span class="sxs-lookup"><span data-stu-id="11a1f-267">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="11a1f-268">Haga clic en el botón **Seleccionar** del cuadro de diálogo **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="11a1f-268">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="11a1f-269">Haga clic en el botón **Asignar** del cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="11a1f-269">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="11a1f-270">Prueba del inicio de sesión único </span><span class="sxs-lookup"><span data-stu-id="11a1f-270">Testing single sign-on</span></span>

<span data-ttu-id="11a1f-271">En esta sección, comprobará su único inicio de sesión en configuración de Azure AD con hello Panel de acceso.</span><span class="sxs-lookup"><span data-stu-id="11a1f-271">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="11a1f-272">Al hacer clic en icono de Boomi de Hola Hola Panel de acceso, deberá obtener aplicaciones de Boomi de tooyour automáticamente ha iniciado sesión.</span><span class="sxs-lookup"><span data-stu-id="11a1f-272">When you click hello Boomi tile in hello Access Panel, you should get automatically signed-on tooyour Boomi application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="11a1f-273">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="11a1f-273">Additional resources</span></span>

* [<span data-ttu-id="11a1f-274">Lista de tutoriales sobre cómo tooIntegrate aplicaciones de SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="11a1f-274">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="11a1f-275">¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="11a1f-275">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-boomi-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-boomi-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-boomi-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-boomi-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-boomi-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-boomi-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-boomi-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-boomi-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-boomi-tutorial/tutorial_general_203.png

