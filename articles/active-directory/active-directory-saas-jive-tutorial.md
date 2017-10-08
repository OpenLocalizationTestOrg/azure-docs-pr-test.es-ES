---
title: "Tutorial: Integración de Azure Active Directory con Jive | Microsoft Docs"
description: "Obtenga información acerca de cómo tooconfigure inicio de sesión único entre Active Directory de Azure y Jive."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 9fc5659a-c116-4a1b-a601-333325a26b46
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/19/2017
ms.author: jeedes
ms.openlocfilehash: f22bf78a55e8a4a9ea2f0020ef2f535be88b6302
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-jive"></a><span data-ttu-id="33e8c-103">Tutorial: Integración de Azure Active Directory con Jive</span><span class="sxs-lookup"><span data-stu-id="33e8c-103">Tutorial: Azure Active Directory integration with Jive</span></span>

<span data-ttu-id="33e8c-104">En este tutorial, aprenderá cómo toointegrate Jive con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="33e8c-104">In this tutorial, you learn how toointegrate Jive with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="33e8c-105">Integración Jive con Azure AD proporciona Hola siguientes ventajas:</span><span class="sxs-lookup"><span data-stu-id="33e8c-105">Integrating Jive with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="33e8c-106">Puede controlar en Azure AD que tenga acceso tooJive</span><span class="sxs-lookup"><span data-stu-id="33e8c-106">You can control in Azure AD who has access tooJive</span></span>
- <span data-ttu-id="33e8c-107">Puede habilitar los usuarios tooautomatically get ha iniciado sesión tooJive (Single Sign-On) con sus cuentas de Azure AD</span><span class="sxs-lookup"><span data-stu-id="33e8c-107">You can enable your users tooautomatically get signed-on tooJive (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="33e8c-108">Puede administrar las cuentas en una ubicación central: Hola portal de Azure</span><span class="sxs-lookup"><span data-stu-id="33e8c-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="33e8c-109">Si desea tooknow obtener más información acerca de la integración de aplicaciones de SaaS con Azure AD, consulte [¿qué es acceso a la aplicación y el inicio de sesión único con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="33e8c-109">If you want tooknow more information about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="33e8c-110">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="33e8c-110">Prerequisites</span></span>

<span data-ttu-id="33e8c-111">integración de Azure AD con Jive tooconfigure, necesita Hola siguientes elementos:</span><span class="sxs-lookup"><span data-stu-id="33e8c-111">tooconfigure Azure AD integration with Jive, you need hello following items:</span></span>

- <span data-ttu-id="33e8c-112">Una suscripción de Azure AD</span><span class="sxs-lookup"><span data-stu-id="33e8c-112">An Azure AD subscription</span></span>
- <span data-ttu-id="33e8c-113">Una suscripción habilitada para inicio de sesión único en Jive</span><span class="sxs-lookup"><span data-stu-id="33e8c-113">A Jive single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="33e8c-114">Hola tootest los pasos de este tutorial, no se recomienda usar un entorno de producción.</span><span class="sxs-lookup"><span data-stu-id="33e8c-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="33e8c-115">pasos de hello tootest en este tutorial, debe seguir estas recomendaciones:</span><span class="sxs-lookup"><span data-stu-id="33e8c-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="33e8c-116">No use el entorno de producción, salvo que sea necesario.</span><span class="sxs-lookup"><span data-stu-id="33e8c-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="33e8c-117">Si no dispone de un entorno de prueba de Azure AD, puede obtener una versión de prueba de un mes [aquí](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="33e8c-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="33e8c-118">Descripción del escenario</span><span class="sxs-lookup"><span data-stu-id="33e8c-118">Scenario description</span></span>
<span data-ttu-id="33e8c-119">En este tutorial, puede probar el inicio de sesión único de Azure AD en un entorno de prueba.</span><span class="sxs-lookup"><span data-stu-id="33e8c-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="33e8c-120">escenario de Hello descrito en este tutorial consta de dos bloques principales:</span><span class="sxs-lookup"><span data-stu-id="33e8c-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="33e8c-121">Agregar Jive desde la Galería de Hola</span><span class="sxs-lookup"><span data-stu-id="33e8c-121">Adding Jive from hello gallery</span></span>
2. <span data-ttu-id="33e8c-122">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="33e8c-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-jive-from-hello-gallery"></a><span data-ttu-id="33e8c-123">Agregar Jive desde la Galería de Hola</span><span class="sxs-lookup"><span data-stu-id="33e8c-123">Adding Jive from hello gallery</span></span>
<span data-ttu-id="33e8c-124">integración de hello tooconfigure de Jive en Azure AD, deberá tooadd Jive de lista de tooyour Hola Galería de aplicaciones administradas de SaaS.</span><span class="sxs-lookup"><span data-stu-id="33e8c-124">tooconfigure hello integration of Jive into Azure AD, you need tooadd Jive from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="33e8c-125">**tooadd Jive de galería de hello, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="33e8c-125">**tooadd Jive from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="33e8c-126">Hola  **[portal de Azure](https://portal.azure.com)**, en el panel de navegación izquierdo de Hola, haga clic en **Azure Active Directory** icono.</span><span class="sxs-lookup"><span data-stu-id="33e8c-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="33e8c-128">Navegue demasiado**aplicaciones empresariales**.</span><span class="sxs-lookup"><span data-stu-id="33e8c-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="33e8c-129">A continuación, vaya demasiado**todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="33e8c-129">Then go too**All applications**.</span></span>

    ![Aplicaciones][2]
    
3. <span data-ttu-id="33e8c-131">tooadd nueva aplicación, haga clic en **nueva aplicación** botón en la parte superior de saludo del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="33e8c-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Aplicaciones][3]

4. <span data-ttu-id="33e8c-133">En el cuadro de búsqueda de hello, escriba **Jive**.</span><span class="sxs-lookup"><span data-stu-id="33e8c-133">In hello search box, type **Jive**.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-jive-tutorial/tutorial_jive_search.png)

5. <span data-ttu-id="33e8c-135">En el panel de resultados de hello, seleccione **Jive**y, a continuación, haga clic en **agregar** botón aplicación hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="33e8c-135">In hello results panel, select **Jive**, and then click **Add** button tooadd hello application.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-jive-tutorial/tutorial_jive_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="33e8c-137">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="33e8c-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="33e8c-138">En esta sección, podrá configurar y probar el inicio de sesión único de Azure AD con Jive con un usuario de prueba llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="33e8c-138">In this section, you configure and test Azure AD single sign-on with Jive based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="33e8c-139">Para toowork de inicio de sesión único, Azure AD necesita tooknow qué usuario equivalente de hello en Jive es tooa usuario en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="33e8c-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Jive is tooa user in Azure AD.</span></span> <span data-ttu-id="33e8c-140">En otras palabras, una relación de vínculo entre un usuario de Azure AD y el usuario relacionado de hello en Jive debe toobe establecido.</span><span class="sxs-lookup"><span data-stu-id="33e8c-140">In other words, a link relationship between an Azure AD user and hello related user in Jive needs toobe established.</span></span>

<span data-ttu-id="33e8c-141">Esta relación de vínculo se establece mediante la asignación de valor de Hola de hello **nombre de usuario** en Azure AD como valor de Hola de hello **nombre de usuario** en Jive.</span><span class="sxs-lookup"><span data-stu-id="33e8c-141">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in Jive.</span></span>

<span data-ttu-id="33e8c-142">tooconfigure y prueba de inicio de sesión único en Azure AD con Jive, deberá hello toocomplete después de bloques de creación:</span><span class="sxs-lookup"><span data-stu-id="33e8c-142">tooconfigure and test Azure AD single sign-on with Jive, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="33e8c-143">**[Configuración de Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable la toouse usuarios esta característica.</span><span class="sxs-lookup"><span data-stu-id="33e8c-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="33e8c-144">**[Crear un usuario de prueba de Azure AD](#creating-an-azure-ad-test-user)**  -inicio de sesión único en Azure AD tootest con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="33e8c-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="33e8c-145">**[Crear un usuario de prueba de Jive](#creating-a-jive-test-user)**  -toohave un equivalente de Britta Simon en Jive que es la representación toohello vinculado Azure AD del usuario.</span><span class="sxs-lookup"><span data-stu-id="33e8c-145">**[Creating a Jive test user](#creating-a-jive-test-user)** - toohave a counterpart of Britta Simon in Jive that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="33e8c-146">**[Asignar usuario de prueba de hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="33e8c-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="33e8c-147">**[Pruebas de Single Sign-On](#testing-single-sign-on)**  -tooverify Hola si funciona la configuración.</span><span class="sxs-lookup"><span data-stu-id="33e8c-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="33e8c-148">Configuración del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="33e8c-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="33e8c-149">En esta sección, habilitar inicio de sesión único en Azure AD en hello portal de Azure y configurar el inicio de sesión único en la aplicación de Jive.</span><span class="sxs-lookup"><span data-stu-id="33e8c-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Jive application.</span></span>

<span data-ttu-id="33e8c-150">**tooconfigure inicio de sesión único en Azure AD con Jive, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="33e8c-150">**tooconfigure Azure AD single sign-on with Jive, perform hello following steps:**</span></span>

1. <span data-ttu-id="33e8c-151">En el portal de Azure, en Hola Hola **Jive** página de integración de aplicaciones, haga clic en **inicio de sesión único**.</span><span class="sxs-lookup"><span data-stu-id="33e8c-151">In hello Azure portal, on hello **Jive** application integration page, click **Single sign-on**.</span></span>

    ![Configurar inicio de sesión único][4]

2. <span data-ttu-id="33e8c-153">En hello **inicio de sesión único** cuadro de diálogo, seleccione **modo** como **sesión basado en SAML** tooenable inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="33e8c-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurar inicio de sesión único](./media/active-directory-saas-jive-tutorial/tutorial_jive_samlbase.png)

3. <span data-ttu-id="33e8c-155">En hello **Jive dominio y las direcciones URL** sección, lleve a cabo Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="33e8c-155">On hello **Jive Domain and URLs** section, perform hello following steps:</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-jive-tutorial/tutorial_jive_url.png)

    <span data-ttu-id="33e8c-157">a.</span><span class="sxs-lookup"><span data-stu-id="33e8c-157">a.</span></span> <span data-ttu-id="33e8c-158">Hola **dirección URL de inicio de sesión** cuadro de texto, escriba una dirección URL usando Hola siguiente patrón:`https://<instance name>.jivecustom.com`</span><span class="sxs-lookup"><span data-stu-id="33e8c-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<instance name>.jivecustom.com`</span></span>

    <span data-ttu-id="33e8c-159">b.</span><span class="sxs-lookup"><span data-stu-id="33e8c-159">b.</span></span> <span data-ttu-id="33e8c-160">Hola **identificador** cuadro de texto, escriba una dirección URL usando Hola siguiente patrón:`https://<instance name>.jiveon.com`</span><span class="sxs-lookup"><span data-stu-id="33e8c-160">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<instance name>.jiveon.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="33e8c-161">Estos valores no son Hola real.</span><span class="sxs-lookup"><span data-stu-id="33e8c-161">These values are not hello real.</span></span> <span data-ttu-id="33e8c-162">Actualizar estos valores con URL de inicio de sesión real de Hola y el identificador.</span><span class="sxs-lookup"><span data-stu-id="33e8c-162">Update these values with hello actual Sign-on URL and Identifier.</span></span> <span data-ttu-id="33e8c-163">Póngase en contacto con [equipo de soporte técnico de cliente de Jive](https://www.jivesoftware.com/services-support/) tooget estos valores.</span><span class="sxs-lookup"><span data-stu-id="33e8c-163">Contact [Jive Client support team](https://www.jivesoftware.com/services-support/) tooget these values.</span></span> 
 
4. <span data-ttu-id="33e8c-164">En hello **el certificado de firma de SAML** sección, haga clic en **Metadata XML** y, a continuación, guarde el archivo XML de hello en el equipo.</span><span class="sxs-lookup"><span data-stu-id="33e8c-164">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello XML file on your computer.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-jive-tutorial/tutorial_jive_certificate.png) 

5. <span data-ttu-id="33e8c-166">Haga clic en el botón **Guardar** .</span><span class="sxs-lookup"><span data-stu-id="33e8c-166">Click **Save** button.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-jive-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="33e8c-168">inicio de sesión único en tooconfigure en **Jive** inquilino de Jive tooyour lateral, inicio de sesión como administrador.</span><span class="sxs-lookup"><span data-stu-id="33e8c-168">tooconfigure single sign-on on **Jive** side, sign-on tooyour Jive tenant as an administrator.</span></span>

7. <span data-ttu-id="33e8c-169">En el menú de hello en la parte superior de hello, haga clic en "**Saml**."</span><span class="sxs-lookup"><span data-stu-id="33e8c-169">In hello menu on hello top, Click "**Saml**."</span></span>

    ![Configuración del inicio de sesión único en la aplicación](./media/active-directory-saas-jive-tutorial/tutorial_jive_002.png)

    <span data-ttu-id="33e8c-171">a.</span><span class="sxs-lookup"><span data-stu-id="33e8c-171">a.</span></span> <span data-ttu-id="33e8c-172">Seleccione **habilitado** en hello **General** ficha.</span><span class="sxs-lookup"><span data-stu-id="33e8c-172">Select **Enabled** under hello **General** tab.</span></span>   
    <span data-ttu-id="33e8c-173">b.</span><span class="sxs-lookup"><span data-stu-id="33e8c-173">b.</span></span> <span data-ttu-id="33e8c-174">Haga clic en hello "**guardar toda la configuración de saml**" botón.</span><span class="sxs-lookup"><span data-stu-id="33e8c-174">Click hello "**Save all saml settings**" button.</span></span>

8. <span data-ttu-id="33e8c-175">Navegue toohello "**metadatos de Idp**" pestaña.</span><span class="sxs-lookup"><span data-stu-id="33e8c-175">Navigate toohello "**Idp Metadata**" tab.</span></span>
   
    ![Configuración del inicio de sesión único en la aplicación](./media/active-directory-saas-jive-tutorial/tutorial_jive_003.png)
   
    <span data-ttu-id="33e8c-177">a.</span><span class="sxs-lookup"><span data-stu-id="33e8c-177">a.</span></span> <span data-ttu-id="33e8c-178">Copiar el contenido de Hola de archivo XML de metadatos de hello descargado y, a continuación, péguelo en hello **metadatos del proveedor de identidades (IDP)** cuadro de texto.</span><span class="sxs-lookup"><span data-stu-id="33e8c-178">Copy hello content of hello downloaded metadata XML file, and then paste it into hello **Identity Provider (IDP) Metadata** textbox.</span></span>
    
    <span data-ttu-id="33e8c-179">b.</span><span class="sxs-lookup"><span data-stu-id="33e8c-179">b.</span></span> <span data-ttu-id="33e8c-180">Haga clic en hello "**guardar toda la configuración de saml**" botón.</span><span class="sxs-lookup"><span data-stu-id="33e8c-180">Click hello "**Save all saml settings**" button.</span></span> 

9. <span data-ttu-id="33e8c-181">Vaya toohello "**asignación de atributos de usuario**" pestaña.</span><span class="sxs-lookup"><span data-stu-id="33e8c-181">Go toohello "**User Attribute Mapping**" tab.</span></span>
   
    ![Configuración del inicio de sesión único en la aplicación](./media/active-directory-saas-jive-tutorial/tutorial_jive_004.png)
   
    <span data-ttu-id="33e8c-183">a.</span><span class="sxs-lookup"><span data-stu-id="33e8c-183">a.</span></span> <span data-ttu-id="33e8c-184">Hola **correo electrónico** cuadro de texto, copiar y pegar Hola nombre de atributo **correo** valor.</span><span class="sxs-lookup"><span data-stu-id="33e8c-184">In hello **Email** textbox, copy and paste hello attribute name of **mail** value.</span></span>
   
    <span data-ttu-id="33e8c-185">b.</span><span class="sxs-lookup"><span data-stu-id="33e8c-185">b.</span></span> <span data-ttu-id="33e8c-186">Hola **nombre** cuadro de texto, copiar y pegar Hola nombre de atributo **givenname** valor.</span><span class="sxs-lookup"><span data-stu-id="33e8c-186">In hello **First Name** textbox, copy and paste hello attribute name of **givenname** value.</span></span>
   
    <span data-ttu-id="33e8c-187">c.</span><span class="sxs-lookup"><span data-stu-id="33e8c-187">c.</span></span> <span data-ttu-id="33e8c-188">Hola **Last Name** cuadro de texto, copiar y pegar Hola nombre de atributo **apellido** valor.</span><span class="sxs-lookup"><span data-stu-id="33e8c-188">In hello **Last Name** textbox, copy and paste hello attribute name of **surname** value.</span></span>

> [!TIP]
> <span data-ttu-id="33e8c-189">Ahora puede leer una versión concisa de estas instrucciones dentro de hello [portal de Azure](https://portal.azure.com), mientras que está configurando la aplicación hello!</span><span class="sxs-lookup"><span data-stu-id="33e8c-189">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="33e8c-190">Después de agregar esta aplicación de hello **Active Directory > aplicaciones empresariales** sección, simplemente haga clic en hello **Single Sign-On** Hola de pestaña y acceso incrustado documentación a través de hello  **Configuración** sección final Hola.</span><span class="sxs-lookup"><span data-stu-id="33e8c-190">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="33e8c-191">Puede leer más acerca de características de documentación de embedded Hola aquí: [Azure AD incrustado documentación]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="33e8c-191">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="33e8c-192">Creación de un usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="33e8c-192">Creating an Azure AD test user</span></span>
<span data-ttu-id="33e8c-193">objetivo de Hola de esta sección es un usuario de prueba en hello Azure portal llamado a Britta Simon toocreate.</span><span class="sxs-lookup"><span data-stu-id="33e8c-193">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Creación de un usuario de Azure AD][100]

<span data-ttu-id="33e8c-195">**toocreate un usuario de prueba en Azure AD, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="33e8c-195">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="33e8c-196">Hola **portal de Azure**, en Hola panel de navegación izquierdo, haga clic en **Azure Active Directory** icono.</span><span class="sxs-lookup"><span data-stu-id="33e8c-196">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-jive-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="33e8c-198">lista de hello toodisplay de usuarios, vaya demasiado**usuarios y grupos** y haga clic en **todos los usuarios**.</span><span class="sxs-lookup"><span data-stu-id="33e8c-198">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-jive-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="33e8c-200">Hola tooopen **usuario** cuadro de diálogo, haga clic en **agregar** en la parte superior de saludo del cuadro de diálogo de Hola.</span><span class="sxs-lookup"><span data-stu-id="33e8c-200">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-jive-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="33e8c-202">En hello **usuario** cuadro de diálogo, siga los pasos de hello:</span><span class="sxs-lookup"><span data-stu-id="33e8c-202">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-jive-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="33e8c-204">a.</span><span class="sxs-lookup"><span data-stu-id="33e8c-204">a.</span></span> <span data-ttu-id="33e8c-205">Hola **nombre** cuadro de texto, tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="33e8c-205">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="33e8c-206">b.</span><span class="sxs-lookup"><span data-stu-id="33e8c-206">b.</span></span> <span data-ttu-id="33e8c-207">Hola **nombre de usuario** cuadro de texto, hello tipo **dirección de correo electrónico** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="33e8c-207">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="33e8c-208">c.</span><span class="sxs-lookup"><span data-stu-id="33e8c-208">c.</span></span> <span data-ttu-id="33e8c-209">Seleccione **Mostrar contraseña** y anote el valor de Hola de hello **contraseña**.</span><span class="sxs-lookup"><span data-stu-id="33e8c-209">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="33e8c-210">d.</span><span class="sxs-lookup"><span data-stu-id="33e8c-210">d.</span></span> <span data-ttu-id="33e8c-211">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="33e8c-211">Click **Create**.</span></span>
 
### <a name="creating-a-jive-test-user"></a><span data-ttu-id="33e8c-212">Creación de un usuario de prueba de Jive</span><span class="sxs-lookup"><span data-stu-id="33e8c-212">Creating a Jive test user</span></span>

<span data-ttu-id="33e8c-213">Trabajar con [equipo de soporte técnico de Jive cliente](https://www.jivesoftware.com/services-support/) a los usuarios de tooadd hello en la plataforma de Jive Hola.</span><span class="sxs-lookup"><span data-stu-id="33e8c-213">Work with [Jive Client support team](https://www.jivesoftware.com/services-support/) tooadd hello users in hello Jive platform.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="33e8c-214">Asignación de usuario de prueba de hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="33e8c-214">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="33e8c-215">En esta sección, se habilita Britta Simon toouse un inicio de sesión único Azure concediendo acceso tooJive.</span><span class="sxs-lookup"><span data-stu-id="33e8c-215">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooJive.</span></span>

![Asignar usuario][200] 

<span data-ttu-id="33e8c-217">**tooassign Britta Simon tooJive, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="33e8c-217">**tooassign Britta Simon tooJive, perform hello following steps:**</span></span>

1. <span data-ttu-id="33e8c-218">Hola portal de Azure, abra la vista de aplicaciones de hello y, a continuación, navegue a vista de directorio toohello y vaya demasiado**aplicaciones empresariales** , a continuación, haga clic en **todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="33e8c-218">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Asignar usuario][201] 

2. <span data-ttu-id="33e8c-220">En la lista de aplicaciones de hello, seleccione **Jive**.</span><span class="sxs-lookup"><span data-stu-id="33e8c-220">In hello applications list, select **Jive**.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-jive-tutorial/tutorial_jive_app.png) 

3. <span data-ttu-id="33e8c-222">En el menú de Hola Hola izquierda, haga clic en **usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="33e8c-222">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Asignar usuario][202] 

4. <span data-ttu-id="33e8c-224">Haga clic en el botón **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="33e8c-224">Click **Add** button.</span></span> <span data-ttu-id="33e8c-225">Después, seleccione **Usuarios y grupos** en el cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="33e8c-225">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Asignar usuario][203]

5. <span data-ttu-id="33e8c-227">En **usuarios y grupos** cuadro de diálogo, seleccione **Britta Simon** en la lista de usuarios de Hola.</span><span class="sxs-lookup"><span data-stu-id="33e8c-227">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="33e8c-228">Haga clic en el botón **Seleccionar** del cuadro de diálogo **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="33e8c-228">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="33e8c-229">Haga clic en el botón **Asignar** del cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="33e8c-229">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="33e8c-230">Prueba del inicio de sesión único </span><span class="sxs-lookup"><span data-stu-id="33e8c-230">Testing single sign-on</span></span>

<span data-ttu-id="33e8c-231">En esta sección, comprobará su único inicio de sesión en configuración de Azure AD con hello Panel de acceso.</span><span class="sxs-lookup"><span data-stu-id="33e8c-231">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="33e8c-232">Al hacer clic en icono de Jive Hola Hola Panel de acceso, deberá obtener la aplicación de Jive tooyour automáticamente ha iniciado sesión.</span><span class="sxs-lookup"><span data-stu-id="33e8c-232">When you click hello Jive tile in hello Access Panel, you should get automatically signed-on tooyour Jive application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="33e8c-233">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="33e8c-233">Additional resources</span></span>

* [<span data-ttu-id="33e8c-234">Lista de tutoriales sobre cómo tooIntegrate aplicaciones de SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="33e8c-234">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="33e8c-235">¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="33e8c-235">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)
* [<span data-ttu-id="33e8c-236">Configuración del aprovisionamiento de usuarios</span><span class="sxs-lookup"><span data-stu-id="33e8c-236">Configure User Provisioning</span></span>](active-directory-saas-jive-provisioning-tutorial.md)

<!--Image references-->

[1]: ./media/active-directory-saas-jive-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-jive-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-jive-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-jive-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-jive-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-jive-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-jive-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-jive-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-jive-tutorial/tutorial_general_203.png

