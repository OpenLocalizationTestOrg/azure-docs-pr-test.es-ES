---
title: "Tutorial: Integración de Azure Active Directory con Skillport | Microsoft Docs"
description: "Obtenga información acerca de cómo tooconfigure inicio de sesión único entre Azure Active Directory y Skillport."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 4df349b2-a73f-4b88-a077-ec0fbfc26527
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/05/2017
ms.author: jeedes
ms.openlocfilehash: ba504c3cae5f92767eb90d8453887904690fe0c5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-skillport"></a><span data-ttu-id="7a6a9-103">Tutorial: Integración de Azure Active Directory con Skillport</span><span class="sxs-lookup"><span data-stu-id="7a6a9-103">Tutorial: Azure Active Directory integration with Skillport</span></span>

<span data-ttu-id="7a6a9-104">En este tutorial, aprenderá cómo toointegrate Skillport con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="7a6a9-104">In this tutorial, you learn how toointegrate Skillport with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="7a6a9-105">Integración Skillport con Azure AD proporciona Hola siguientes ventajas:</span><span class="sxs-lookup"><span data-stu-id="7a6a9-105">Integrating Skillport with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="7a6a9-106">Puede controlar en Azure AD que tenga acceso tooSkillport</span><span class="sxs-lookup"><span data-stu-id="7a6a9-106">You can control in Azure AD who has access tooSkillport</span></span>
- <span data-ttu-id="7a6a9-107">Puede habilitar los usuarios tooautomatically get ha iniciado sesión tooSkillport (Single Sign-On) con sus cuentas de Azure AD</span><span class="sxs-lookup"><span data-stu-id="7a6a9-107">You can enable your users tooautomatically get signed-on tooSkillport (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="7a6a9-108">Puede administrar las cuentas en una ubicación central: Hola portal de Azure</span><span class="sxs-lookup"><span data-stu-id="7a6a9-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="7a6a9-109">Si desea obtener más información acerca de la integración de aplicaciones de SaaS con Azure AD tooknow, consulte [¿qué es acceso a la aplicación y el inicio de sesión único con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="7a6a9-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="7a6a9-110">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="7a6a9-110">Prerequisites</span></span>

<span data-ttu-id="7a6a9-111">integración de Azure AD con Skillport tooconfigure, necesita Hola siguientes elementos:</span><span class="sxs-lookup"><span data-stu-id="7a6a9-111">tooconfigure Azure AD integration with Skillport, you need hello following items:</span></span>

- <span data-ttu-id="7a6a9-112">Una suscripción de Azure AD</span><span class="sxs-lookup"><span data-stu-id="7a6a9-112">An Azure AD subscription</span></span>
- <span data-ttu-id="7a6a9-113">Una suscripción habilitada para el inicio de sesión único en Skillport</span><span class="sxs-lookup"><span data-stu-id="7a6a9-113">A Skillport single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="7a6a9-114">Hola tootest los pasos de este tutorial, no se recomienda usar un entorno de producción.</span><span class="sxs-lookup"><span data-stu-id="7a6a9-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="7a6a9-115">pasos de hello tootest en este tutorial, debe seguir estas recomendaciones:</span><span class="sxs-lookup"><span data-stu-id="7a6a9-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="7a6a9-116">No use el entorno de producción, salvo que sea necesario.</span><span class="sxs-lookup"><span data-stu-id="7a6a9-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="7a6a9-117">Si no dispone de un entorno de prueba de Azure AD, puede obtener una versión de prueba de un mes [aquí](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="7a6a9-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="7a6a9-118">Descripción del escenario</span><span class="sxs-lookup"><span data-stu-id="7a6a9-118">Scenario description</span></span>
<span data-ttu-id="7a6a9-119">En este tutorial, puede probar el inicio de sesión único de Azure AD en un entorno de prueba.</span><span class="sxs-lookup"><span data-stu-id="7a6a9-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="7a6a9-120">escenario de Hello descrito en este tutorial consta de dos bloques principales:</span><span class="sxs-lookup"><span data-stu-id="7a6a9-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="7a6a9-121">Agregar Skillport desde la Galería de Hola</span><span class="sxs-lookup"><span data-stu-id="7a6a9-121">Adding Skillport from hello gallery</span></span>
2. <span data-ttu-id="7a6a9-122">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="7a6a9-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-skillport-from-hello-gallery"></a><span data-ttu-id="7a6a9-123">Agregar Skillport desde la Galería de Hola</span><span class="sxs-lookup"><span data-stu-id="7a6a9-123">Adding Skillport from hello gallery</span></span>
<span data-ttu-id="7a6a9-124">integración de hello tooconfigure de Skillport en Azure AD, deberá tooadd Skillport de lista de tooyour Hola Galería de aplicaciones administradas de SaaS.</span><span class="sxs-lookup"><span data-stu-id="7a6a9-124">tooconfigure hello integration of Skillport into Azure AD, you need tooadd Skillport from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="7a6a9-125">**tooadd Skillport de galería de hello, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="7a6a9-125">**tooadd Skillport from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="7a6a9-126">Hola  **[portal de Azure](https://portal.azure.com)**, en el panel de navegación izquierdo de Hola, haga clic en **Azure Active Directory** icono.</span><span class="sxs-lookup"><span data-stu-id="7a6a9-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="7a6a9-128">Navegue demasiado**aplicaciones empresariales**.</span><span class="sxs-lookup"><span data-stu-id="7a6a9-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="7a6a9-129">A continuación, vaya demasiado**todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="7a6a9-129">Then go too**All applications**.</span></span>

    ![Aplicaciones][2]
    
3. <span data-ttu-id="7a6a9-131">Haga clic en **nueva aplicación** botón en la parte superior de saludo del cuadro de diálogo de Hola.</span><span class="sxs-lookup"><span data-stu-id="7a6a9-131">Click **New Application** button on hello top of hello dialog.</span></span>

    ![Aplicaciones][3]

4. <span data-ttu-id="7a6a9-133">En el cuadro de búsqueda de hello, escriba **Skillport**.</span><span class="sxs-lookup"><span data-stu-id="7a6a9-133">In hello search box, type **Skillport**.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-skillport-tutorial/tutorial_skillport_search.png)

5. <span data-ttu-id="7a6a9-135">En el panel de resultados de hello, seleccione **Skillport**y, a continuación, haga clic en **agregar** botón aplicación hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="7a6a9-135">In hello results panel, select **Skillport**, and then click **Add** button tooadd hello application.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-skillport-tutorial/tutorial_skillport_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="7a6a9-137">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="7a6a9-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="7a6a9-138">En esta sección, podrá configurar y probar el inicio de sesión único de Azure AD con Skillport con un usuario de prueba llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="7a6a9-138">In this section, you configure and test Azure AD single sign-on with Skillport based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="7a6a9-139">Para toowork de inicio de sesión único, Azure AD necesita tooknow qué usuario equivalente de hello en Skillport es tooa usuario en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="7a6a9-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Skillport is tooa user in Azure AD.</span></span> <span data-ttu-id="7a6a9-140">En otras palabras, una relación de vínculo entre un usuario de Azure AD y el usuario relacionado de hello en Skillport debe toobe establecido.</span><span class="sxs-lookup"><span data-stu-id="7a6a9-140">In other words, a link relationship between an Azure AD user and hello related user in Skillport needs toobe established.</span></span>

<span data-ttu-id="7a6a9-141">Esta relación de vínculo se establece mediante la asignación de valor de Hola de hello **nombre de usuario** en Azure AD como valor de Hola de hello **nombre de usuario** en Skillport.</span><span class="sxs-lookup"><span data-stu-id="7a6a9-141">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in Skillport.</span></span>

<span data-ttu-id="7a6a9-142">tooconfigure y prueba de inicio de sesión único en Azure AD con Skillport, deberá hello toocomplete después de bloques de creación:</span><span class="sxs-lookup"><span data-stu-id="7a6a9-142">tooconfigure and test Azure AD single sign-on with Skillport, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="7a6a9-143">**[Configuración de Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable la toouse usuarios esta característica.</span><span class="sxs-lookup"><span data-stu-id="7a6a9-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="7a6a9-144">**[Crear un usuario de prueba de Azure AD](#creating-an-azure-ad-test-user)**  -inicio de sesión único en Azure AD tootest con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="7a6a9-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="7a6a9-145">**[Crear un usuario de prueba Skillport](#creating-a-skillport-test-user)**  -toohave un equivalente de Britta Simon en Skillport que es la representación toohello vinculado Azure AD del usuario.</span><span class="sxs-lookup"><span data-stu-id="7a6a9-145">**[Creating a Skillport test user](#creating-a-skillport-test-user)** - toohave a counterpart of Britta Simon in Skillport that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="7a6a9-146">**[Asignar usuario de prueba de hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="7a6a9-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="7a6a9-147">**[Pruebas de Single Sign-On](#testing-single-sign-on)**  -tooverify Hola si funciona la configuración.</span><span class="sxs-lookup"><span data-stu-id="7a6a9-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="7a6a9-148">Configuración del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="7a6a9-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="7a6a9-149">En esta sección, habilitar inicio de sesión único en Azure AD en hello portal de Azure y configurar el inicio de sesión único en la aplicación Skillport.</span><span class="sxs-lookup"><span data-stu-id="7a6a9-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Skillport application.</span></span>

<span data-ttu-id="7a6a9-150">**inicio de sesión único en Azure AD tooconfigure con Skillport, realizar Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="7a6a9-150">**tooconfigure Azure AD single sign-on with Skillport, perform hello following steps:**</span></span>

1. <span data-ttu-id="7a6a9-151">En el portal de Azure, en Hola Hola **Skillport** página de integración de aplicaciones, haga clic en **inicio de sesión único**.</span><span class="sxs-lookup"><span data-stu-id="7a6a9-151">In hello Azure  portal, on hello **Skillport** application integration page, click **Single sign-on**.</span></span>

    ![Configurar inicio de sesión único][4]

2. <span data-ttu-id="7a6a9-153">En hello **inicio de sesión único** cuadro de diálogo, seleccione **modo** como **sesión basado en SAML** tooenable inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="7a6a9-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurar inicio de sesión único](./media/active-directory-saas-skillport-tutorial/tutorial_skillport_samlbase.png)

3. <span data-ttu-id="7a6a9-155">En hello **Skillport dominio y las direcciones URL** sección, lleve a cabo Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="7a6a9-155">On hello **Skillport Domain and URLs** section, perform hello following steps:</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-skillport-tutorial/tutorial_skillport_url.png)

    <span data-ttu-id="7a6a9-157">a.</span><span class="sxs-lookup"><span data-stu-id="7a6a9-157">a.</span></span> <span data-ttu-id="7a6a9-158">Hola **dirección URL de inicio de sesión** cuadro de texto, escriba una dirección URL con hello siguiendo patrones:</span><span class="sxs-lookup"><span data-stu-id="7a6a9-158">In hello **Sign-on URL** textbox, type a URL using hello following patterns:</span></span>
      
      <span data-ttu-id="7a6a9-159">Centro de datos de UE: `https://<subdomain>.skillport.eu`</span><span class="sxs-lookup"><span data-stu-id="7a6a9-159">EU Datacenter: `https://<subdomain>.skillport.eu`</span></span>
   
      <span data-ttu-id="7a6a9-160">Centro de datos de EE. UU.: `https://<subdomain>.skillport.com`</span><span class="sxs-lookup"><span data-stu-id="7a6a9-160">US Datacenter: `https://<subdomain>.skillport.com`</span></span>
   
    <span data-ttu-id="7a6a9-161">b.</span><span class="sxs-lookup"><span data-stu-id="7a6a9-161">b.</span></span> <span data-ttu-id="7a6a9-162">Hola **dirección URL de respuesta** cuadro de texto, escriba una dirección URL con hello siguiendo patrones:</span><span class="sxs-lookup"><span data-stu-id="7a6a9-162">In hello **Reply URL** textbox, type a URL using hello following patterns:</span></span>
    
      <span data-ttu-id="7a6a9-163">Centro de datos de UE: `https://<subdomain>.skillport.eu/adfs/ls/`</span><span class="sxs-lookup"><span data-stu-id="7a6a9-163">EU Datacenter: `https://<subdomain>.skillport.eu/adfs/ls/`</span></span>
    
      <span data-ttu-id="7a6a9-164">Centro de datos de EE. UU.: `https://<subdomain>.skillport.com/sp/ACS.saml2`</span><span class="sxs-lookup"><span data-stu-id="7a6a9-164">US Datacenter: `https://<subdomain>.skillport.com/sp/ACS.saml2`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="7a6a9-165">Estos valores no son Hola real.</span><span class="sxs-lookup"><span data-stu-id="7a6a9-165">These values are not hello real.</span></span> <span data-ttu-id="7a6a9-166">Actualizar estos valores con la dirección URL de respuesta real hello y dirección URL de inicio de sesión.</span><span class="sxs-lookup"><span data-stu-id="7a6a9-166">Update these values with hello actual Reply URL and Sign-On URL.</span></span> <span data-ttu-id="7a6a9-167">Póngase en contacto con [equipo de soporte técnico de cliente de Skillport](https://www.skillsoft.com/contact.asp) tooget estos valores.</span><span class="sxs-lookup"><span data-stu-id="7a6a9-167">Contact [Skillport Client support team](https://www.skillsoft.com/contact.asp) tooget these values.</span></span>
 
4. <span data-ttu-id="7a6a9-168">En hello **el certificado de firma de SAML** sección, haga clic en **Metadata XML** y, a continuación, guarde el archivo XML de hello en el equipo.</span><span class="sxs-lookup"><span data-stu-id="7a6a9-168">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello XML file on your computer.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-skillport-tutorial/tutorial_skillport_certificate.png) 

5. <span data-ttu-id="7a6a9-170">Haga clic en el botón **Guardar** .</span><span class="sxs-lookup"><span data-stu-id="7a6a9-170">Click **Save** button.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-skillport-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="7a6a9-172">tooconfigure inicio de sesión único en **Skillport** lado, necesita hello toosend descargado **Metadata XML** demasiado[equipo de soporte técnico de Skillport](https://www.skillsoft.com/contact.asp).</span><span class="sxs-lookup"><span data-stu-id="7a6a9-172">tooconfigure single sign-on on **Skillport** side, you need toosend hello downloaded **Metadata XML** too[Skillport support team](https://www.skillsoft.com/contact.asp).</span></span> <span data-ttu-id="7a6a9-173">Configurará el toohave Hola configurada correctamente en ambos lados de la conexión de SSO de SAML.</span><span class="sxs-lookup"><span data-stu-id="7a6a9-173">They will set it up toohave hello SAML SSO connection set properly on both sides.</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="7a6a9-174">Creación de un usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="7a6a9-174">Creating an Azure AD test user</span></span>
<span data-ttu-id="7a6a9-175">objetivo de Hola de esta sección es un usuario de prueba en hello Azure portal llamado a Britta Simon toocreate.</span><span class="sxs-lookup"><span data-stu-id="7a6a9-175">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Creación de un usuario de Azure AD][100]

<span data-ttu-id="7a6a9-177">**toocreate un usuario de prueba en Azure AD, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="7a6a9-177">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="7a6a9-178">Hola **portal de Azure**, en Hola panel de navegación izquierdo, haga clic en **Azure Active Directory** icono.</span><span class="sxs-lookup"><span data-stu-id="7a6a9-178">In hello **Azure  portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-skillport-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="7a6a9-180">Vaya demasiado**usuarios y grupos** y haga clic en **todos los usuarios** toodisplay lista de Hola de usuarios.</span><span class="sxs-lookup"><span data-stu-id="7a6a9-180">Go too**Users and groups** and click **All users** toodisplay hello list of users.</span></span>
    
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-skillport-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="7a6a9-182">En la parte superior de saludo del cuadro de diálogo de hello, haga clic en **agregar** tooopen hello **usuario** cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="7a6a9-182">At hello top of hello dialog, click **Add** tooopen hello **User** dialog.</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-skillport-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="7a6a9-184">En hello **usuario** cuadro de diálogo, siga los pasos de hello:</span><span class="sxs-lookup"><span data-stu-id="7a6a9-184">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-skillport-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="7a6a9-186">a.</span><span class="sxs-lookup"><span data-stu-id="7a6a9-186">a.</span></span> <span data-ttu-id="7a6a9-187">Hola **nombre** cuadro de texto, tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="7a6a9-187">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="7a6a9-188">b.</span><span class="sxs-lookup"><span data-stu-id="7a6a9-188">b.</span></span> <span data-ttu-id="7a6a9-189">Hola **nombre de usuario** cuadro de texto, hello tipo **dirección de correo electrónico** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="7a6a9-189">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="7a6a9-190">c.</span><span class="sxs-lookup"><span data-stu-id="7a6a9-190">c.</span></span> <span data-ttu-id="7a6a9-191">Seleccione **Mostrar contraseña** y anote el valor de Hola de hello **contraseña**.</span><span class="sxs-lookup"><span data-stu-id="7a6a9-191">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="7a6a9-192">d.</span><span class="sxs-lookup"><span data-stu-id="7a6a9-192">d.</span></span> <span data-ttu-id="7a6a9-193">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="7a6a9-193">Click **Create**.</span></span>
 
### <a name="creating-a-skillport-test-user"></a><span data-ttu-id="7a6a9-194">Creación de un usuario de prueba de Skillport</span><span class="sxs-lookup"><span data-stu-id="7a6a9-194">Creating a Skillport test user</span></span>

<span data-ttu-id="7a6a9-195">En el usuario de prueba de orden toocreate Skillport, necesita toocontact [equipo de soporte técnico de Skillport](https://www.skillsoft.com/contact.asp) porque tienen varios escenarios empresariales según el requisito de toohello del usuario final.</span><span class="sxs-lookup"><span data-stu-id="7a6a9-195">In order toocreate Skillport test user, you need toocontact [Skillport support team](https://www.skillsoft.com/contact.asp) as they have multiple business scenarios according toohello requirement of end user.</span></span> <span data-ttu-id="7a6a9-196">Configurará después hablando con los usuarios de Hola.</span><span class="sxs-lookup"><span data-stu-id="7a6a9-196">They will configure it after discussion with hello users.</span></span>  

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="7a6a9-197">Asignación de usuario de prueba de hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="7a6a9-197">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="7a6a9-198">En esta sección, se habilita Britta Simon toouse un inicio de sesión único Azure concediendo acceso tooSkillport.</span><span class="sxs-lookup"><span data-stu-id="7a6a9-198">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooSkillport.</span></span>

![Asignar usuario][200] 

<span data-ttu-id="7a6a9-200">**tooassign Britta Simon tooSkillport, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="7a6a9-200">**tooassign Britta Simon tooSkillport, perform hello following steps:**</span></span>

1. <span data-ttu-id="7a6a9-201">Hola portal de Azure, abra la vista de aplicaciones de hello y, a continuación, navegue a vista de directorio toohello y vaya demasiado**aplicaciones empresariales** , a continuación, haga clic en **todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="7a6a9-201">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Asignar usuario][201] 

2. <span data-ttu-id="7a6a9-203">En la lista de aplicaciones de hello, seleccione **Skillport**.</span><span class="sxs-lookup"><span data-stu-id="7a6a9-203">In hello applications list, select **Skillport**.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-skillport-tutorial/tutorial_skillport_app.png) 

3. <span data-ttu-id="7a6a9-205">En el menú de Hola Hola izquierda, haga clic en **usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="7a6a9-205">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Asignar usuario][202] 

4. <span data-ttu-id="7a6a9-207">Haga clic en el botón **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="7a6a9-207">Click **Add** button.</span></span> <span data-ttu-id="7a6a9-208">Después, seleccione **Usuarios y grupos** en el cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="7a6a9-208">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Asignar usuario][203]

5. <span data-ttu-id="7a6a9-210">En **usuarios y grupos** cuadro de diálogo, seleccione **Britta Simon** en la lista de usuarios de Hola.</span><span class="sxs-lookup"><span data-stu-id="7a6a9-210">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="7a6a9-211">Haga clic en el botón **Seleccionar** del cuadro de diálogo **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="7a6a9-211">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="7a6a9-212">Haga clic en el botón **Asignar** del cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="7a6a9-212">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="7a6a9-213">Prueba del inicio de sesión único </span><span class="sxs-lookup"><span data-stu-id="7a6a9-213">Testing single sign-on</span></span>

<span data-ttu-id="7a6a9-214">En esta sección, comprobará su único inicio de sesión en configuración de Azure AD con hello Panel de acceso.</span><span class="sxs-lookup"><span data-stu-id="7a6a9-214">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="7a6a9-215">Al hacer clic en icono de Skillport Hola Hola Panel de acceso, deberá obtener automáticamente ha iniciado sesión tooyour Skillport aplicación.</span><span class="sxs-lookup"><span data-stu-id="7a6a9-215">When you click hello Skillport tile in hello Access Panel, you should get automatically signed-on tooyour Skillport application.</span></span>
<span data-ttu-id="7a6a9-216">Para más información sobre el Panel de acceso, consulte [Introducción al Panel de acceso](https://msdn.microsoft.com/library/dn308586).</span><span class="sxs-lookup"><span data-stu-id="7a6a9-216">For more information about the Access Panel, see [Introduction to the Access Panel](https://msdn.microsoft.com/library/dn308586).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="7a6a9-217">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="7a6a9-217">Additional resources</span></span>

* [<span data-ttu-id="7a6a9-218">Lista de tutoriales sobre cómo tooIntegrate aplicaciones de SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="7a6a9-218">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="7a6a9-219">¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="7a6a9-219">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-skillport-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-skillport-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-skillport-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-skillport-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-skillport-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-skillport-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-skillport-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-skillport-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-skillport-tutorial/tutorial_general_203.png

