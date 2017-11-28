---
title: "Tutorial: Integración de Azure Active Directory con Teamwork | Microsoft Docs"
description: "Obtenga información acerca de cómo tooconfigure inicio de sesión único entre Azure Active Directory y el trabajo en equipo."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 03760032-3d76-4b47-ab84-241f72fbd561
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/15/2017
ms.author: jeedes
ms.openlocfilehash: f3a88a146f2a0a70de5ef58abd46f7f26b4104f3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-teamwork"></a><span data-ttu-id="76f2c-103">Tutorial: Integración de Azure Active Directory con Teamwork</span><span class="sxs-lookup"><span data-stu-id="76f2c-103">Tutorial: Azure Active Directory integration with Teamwork</span></span>

<span data-ttu-id="76f2c-104">En este tutorial, aprenderá cómo toointegrate el trabajo en equipo con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="76f2c-104">In this tutorial, you learn how toointegrate Teamwork with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="76f2c-105">Integrar el trabajo en equipo con Azure AD proporciona Hola siguientes ventajas:</span><span class="sxs-lookup"><span data-stu-id="76f2c-105">Integrating Teamwork with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="76f2c-106">Puede controlar en Azure AD que tenga acceso tooTeamwork</span><span class="sxs-lookup"><span data-stu-id="76f2c-106">You can control in Azure AD who has access tooTeamwork</span></span>
- <span data-ttu-id="76f2c-107">Puede habilitar los usuarios tooautomatically get ha iniciado sesión tooTeamwork (Single Sign-On) con sus cuentas de Azure AD</span><span class="sxs-lookup"><span data-stu-id="76f2c-107">You can enable your users tooautomatically get signed-on tooTeamwork (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="76f2c-108">Puede administrar las cuentas en una ubicación central: portal de administración de Azure de Hola</span><span class="sxs-lookup"><span data-stu-id="76f2c-108">You can manage your accounts in one central location - hello Azure Management portal</span></span>

<span data-ttu-id="76f2c-109">Si desea obtener más información acerca de la integración de aplicaciones de SaaS con Azure AD tooknow, consulte [¿qué es acceso a la aplicación y el inicio de sesión único con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="76f2c-109">If you want tooknow more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="76f2c-110">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="76f2c-110">Prerequisites</span></span>

<span data-ttu-id="76f2c-111">tooconfigure integración de Azure AD con el trabajo en equipo, necesita Hola siguientes elementos:</span><span class="sxs-lookup"><span data-stu-id="76f2c-111">tooconfigure Azure AD integration with Teamwork, you need hello following items:</span></span>

- <span data-ttu-id="76f2c-112">Una suscripción de Azure AD</span><span class="sxs-lookup"><span data-stu-id="76f2c-112">An Azure AD subscription</span></span>
- <span data-ttu-id="76f2c-113">Una suscripción habilitada para el inicio de sesión único en Teamwork</span><span class="sxs-lookup"><span data-stu-id="76f2c-113">A Teamwork single-sign on enabled subscription</span></span>


> [!NOTE]
> <span data-ttu-id="76f2c-114">Hola tootest los pasos de este tutorial, no se recomienda usar un entorno de producción.</span><span class="sxs-lookup"><span data-stu-id="76f2c-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>


<span data-ttu-id="76f2c-115">pasos de hello tootest en este tutorial, debe seguir estas recomendaciones:</span><span class="sxs-lookup"><span data-stu-id="76f2c-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="76f2c-116">No debe usar el entorno de producción, a menos que sea necesario.</span><span class="sxs-lookup"><span data-stu-id="76f2c-116">You should not use your production environment, unless this is necessary.</span></span>
- <span data-ttu-id="76f2c-117">Si no dispone de un entorno de prueba de Azure AD, puede obtener una versión de prueba de un mes [aquí](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="76f2c-117">If you don't have an Azure AD trial environment, you can get an one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>


## <a name="scenario-description"></a><span data-ttu-id="76f2c-118">Descripción del escenario</span><span class="sxs-lookup"><span data-stu-id="76f2c-118">Scenario description</span></span>
<span data-ttu-id="76f2c-119">En este tutorial, puede probar el inicio de sesión único de Azure AD en un entorno de prueba.</span><span class="sxs-lookup"><span data-stu-id="76f2c-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="76f2c-120">escenario de Hello descrito en este tutorial consta de dos bloques principales:</span><span class="sxs-lookup"><span data-stu-id="76f2c-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="76f2c-121">Agregar el trabajo en equipo desde la Galería de Hola</span><span class="sxs-lookup"><span data-stu-id="76f2c-121">Adding Teamwork from hello gallery</span></span>
2. <span data-ttu-id="76f2c-122">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="76f2c-122">Configuring and testing Azure AD single sign-on</span></span>


## <a name="adding-teamwork-from-hello-gallery"></a><span data-ttu-id="76f2c-123">Agregar el trabajo en equipo desde la Galería de Hola</span><span class="sxs-lookup"><span data-stu-id="76f2c-123">Adding Teamwork from hello gallery</span></span>
<span data-ttu-id="76f2c-124">integración de hello tooconfigure de trabajo en equipo en Azure AD, deberá tooadd el trabajo en equipo en lista de tooyour Hola Galería de aplicaciones administradas de SaaS.</span><span class="sxs-lookup"><span data-stu-id="76f2c-124">tooconfigure hello integration of Teamwork into Azure AD, you need tooadd Teamwork from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="76f2c-125">**tooadd trabajo en equipo desde la Galería de hello, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="76f2c-125">**tooadd Teamwork from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="76f2c-126">Hola  **[Portal de administración de Azure](https://portal.azure.com)**, en el panel de navegación izquierdo de Hola, haga clic en **Azure Active Directory** icono.</span><span class="sxs-lookup"><span data-stu-id="76f2c-126">In hello **[Azure Management Portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="76f2c-128">Navegue demasiado**aplicaciones empresariales**.</span><span class="sxs-lookup"><span data-stu-id="76f2c-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="76f2c-129">A continuación, vaya demasiado**todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="76f2c-129">Then go too**All applications**.</span></span>

    ![Aplicaciones][2]
    
3. <span data-ttu-id="76f2c-131">Haga clic en **agregar** botón en la parte superior de saludo del cuadro de diálogo de Hola.</span><span class="sxs-lookup"><span data-stu-id="76f2c-131">Click **Add** button on hello top of hello dialog.</span></span>

    ![Aplicaciones][3]

4. <span data-ttu-id="76f2c-133">En el cuadro de búsqueda de hello, escriba **trabajo en equipo**.</span><span class="sxs-lookup"><span data-stu-id="76f2c-133">In hello search box, type **Teamwork**.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-teamwork-tutorial/tutorial_teamwork_001.png)

5. <span data-ttu-id="76f2c-135">En el panel de resultados de hello, seleccione **trabajo en equipo**y, a continuación, haga clic en **agregar** botón aplicación hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="76f2c-135">In hello results panel, select **Teamwork**, and then click **Add** button tooadd hello application.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-teamwork-tutorial/tutorial_teamwork_0001.png)


##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="76f2c-137">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="76f2c-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="76f2c-138">En esta sección, podrá configurar y probar el inicio de sesión único de Azure AD con Teamwork con un usuario de prueba llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="76f2c-138">In this section, you configure and test Azure AD single sign-on with Teamwork based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="76f2c-139">Para toowork de inicio de sesión único, Azure AD necesita tooknow qué usuario equivalente de hello en el trabajo en equipo es tooa usuario en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="76f2c-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Teamwork is tooa user in Azure AD.</span></span> <span data-ttu-id="76f2c-140">En otras palabras, una relación de vínculo entre un usuario de Azure AD y el usuario relacionado de hello en el trabajo en equipo necesita toobe establecido.</span><span class="sxs-lookup"><span data-stu-id="76f2c-140">In other words, a link relationship between an Azure AD user and hello related user in Teamwork needs toobe established.</span></span>

<span data-ttu-id="76f2c-141">Esta relación de vínculo se establece mediante la asignación de valor de Hola de hello **nombre de usuario** en Azure AD como valor de Hola de hello **nombre de usuario** en el trabajo en equipo.</span><span class="sxs-lookup"><span data-stu-id="76f2c-141">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in Teamwork.</span></span>

<span data-ttu-id="76f2c-142">tooconfigure y prueba de inicio de sesión único en Azure AD con el trabajo en equipo, deberá hello toocomplete después de bloques de creación:</span><span class="sxs-lookup"><span data-stu-id="76f2c-142">tooconfigure and test Azure AD single sign-on with Teamwork, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="76f2c-143">**[Configuración de Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable la toouse usuarios esta característica.</span><span class="sxs-lookup"><span data-stu-id="76f2c-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="76f2c-144">**[Crear un usuario de prueba de Azure AD](#creating-an-azure-ad-test-user)**  -inicio de sesión único en Azure AD tootest con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="76f2c-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="76f2c-145">**[Crear un usuario de prueba de trabajo en equipo](#creating-a-teamwork-test-user)**  -toohave un equivalente de Britta Simon en el trabajo en equipo que está vinculado toohello Azure AD representación de ella.</span><span class="sxs-lookup"><span data-stu-id="76f2c-145">**[Creating a Teamwork test user](#creating-a-teamwork-test-user)** - toohave a counterpart of Britta Simon in Teamwork that is linked toohello Azure AD representation of her.</span></span>
4. <span data-ttu-id="76f2c-146">**[Asignar usuario de prueba de hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="76f2c-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="76f2c-147">**[Pruebas de Single Sign-On](#testing-single-sign-on)**  -tooverify Hola si funciona la configuración.</span><span class="sxs-lookup"><span data-stu-id="76f2c-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="76f2c-148">Configuración del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="76f2c-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="76f2c-149">En esta sección, habilitar inicio de sesión único en Azure AD en el portal de administración de Azure de Hola y configurar el inicio de sesión único en la aplicación de trabajo en equipo.</span><span class="sxs-lookup"><span data-stu-id="76f2c-149">In this section, you enable Azure AD single sign-on in hello Azure Management portal and configure single sign-on in your Teamwork application.</span></span>

<span data-ttu-id="76f2c-150">**inicio de sesión único en tooconfigure Azure AD con el trabajo en equipo, realice Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="76f2c-150">**tooconfigure Azure AD single sign-on with Teamwork, perform hello following steps:**</span></span>

1. <span data-ttu-id="76f2c-151">En el portal de administración de Azure de hello, en hello **trabajo en equipo** página de integración de aplicaciones, haga clic en **inicio de sesión único**.</span><span class="sxs-lookup"><span data-stu-id="76f2c-151">In hello Azure Management portal, on hello **Teamwork** application integration page, click **Single sign-on**.</span></span>

    ![Configurar inicio de sesión único][4]

2. <span data-ttu-id="76f2c-153">En hello **inicio de sesión único** cuadro de diálogo, como **modo** seleccione **sesión basado en SAML** tooenable inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="76f2c-153">On hello **Single sign-on** dialog, as **Mode** select **SAML-based Sign-on** tooenable single sign on.</span></span>
 
    ![Configurar inicio de sesión único](./media/active-directory-saas-teamwork-tutorial/tutorial_teamwork_01.png)

3. <span data-ttu-id="76f2c-155">En hello **dominio de trabajo en equipo y las direcciones URL** sección en hello **dirección URL de inicio de sesión** cuadro de texto, escriba una dirección URL usando Hola siguiente patrón:`https://<company name>.teamwork.com`</span><span class="sxs-lookup"><span data-stu-id="76f2c-155">On hello **Teamwork Domain and URLs** section, in hello **Sign On URL** textbox, type a URL using hello following pattern: `https://<company name>.teamwork.com`</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-teamwork-tutorial/tutorial_teamwork_02.png)

    > [!NOTE] 
    > <span data-ttu-id="76f2c-157">Tenga en cuenta que esto no es un valor real Hola.</span><span class="sxs-lookup"><span data-stu-id="76f2c-157">Please note that this is not hello real value.</span></span> <span data-ttu-id="76f2c-158">Tendrá que tooupdate este valor con hello real iniciar sesión en la dirección URL.</span><span class="sxs-lookup"><span data-stu-id="76f2c-158">You have tooupdate this value with hello actual Sign On URL.</span></span> <span data-ttu-id="76f2c-159">Póngase en contacto con [equipo de soporte técnico de trabajo en equipo](mailto:support@teamwork.com) tooget este valor.</span><span class="sxs-lookup"><span data-stu-id="76f2c-159">Contact [Teamwork support team](mailto:support@teamwork.com) tooget this value.</span></span> 

4. <span data-ttu-id="76f2c-160">En hello **el certificado de firma de SAML** sección, haga clic en **crear un nuevo certificado**.</span><span class="sxs-lookup"><span data-stu-id="76f2c-160">On hello **SAML Signing Certificate** section, click **Create new certificate**.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-teamwork-tutorial/tutorial_teamwork_03.png)   

5. <span data-ttu-id="76f2c-162">En hello **crear nuevo certificado** cuadro de diálogo, haga clic en el icono del calendario de Hola y seleccione un **fecha de expiración**.</span><span class="sxs-lookup"><span data-stu-id="76f2c-162">On hello **Create New Certificate** dialog, click hello calendar icon and select an **expiry date**.</span></span> <span data-ttu-id="76f2c-163">Luego haga clic en el botón **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="76f2c-163">Then click **Save** button.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-teamwork-tutorial/tutorial_general_300.png)

6. <span data-ttu-id="76f2c-165">En hello **el certificado de firma de SAML** sección, seleccione **activar el nuevo certificado** y haga clic en **guardar** botón.</span><span class="sxs-lookup"><span data-stu-id="76f2c-165">On hello **SAML Signing Certificate** section, select **Make new certificate active** and click **Save** button.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-teamwork-tutorial/tutorial_teamwork_04.png)

7. <span data-ttu-id="76f2c-167">En la ventana emergente de hello **el certificado de sustitución** ventana, haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="76f2c-167">On hello pop-up **Rollover certificate** window, click **OK**.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-teamwork-tutorial/tutorial_general_400.png)

8. <span data-ttu-id="76f2c-169">En hello **el certificado de firma de SAML** sección, haga clic en **Metadata XML** y, a continuación, guarde el archivo de metadatos de hello en el equipo.</span><span class="sxs-lookup"><span data-stu-id="76f2c-169">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-teamwork-tutorial/tutorial_teamwork_05.png) 

9. <span data-ttu-id="76f2c-171">tooget SSO configurado para la aplicación, póngase en contacto con [equipo de soporte técnico de trabajo en equipo](mailto:support@teamwork.com) y proporcionarles Hola descargado **metadatos**.</span><span class="sxs-lookup"><span data-stu-id="76f2c-171">tooget SSO configured for your application, contact [Teamwork support team](mailto:support@teamwork.com) and provide them with hello downloaded **metadata**.</span></span>
  

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="76f2c-172">Creación de un usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="76f2c-172">Creating an Azure AD test user</span></span>
<span data-ttu-id="76f2c-173">objetivo de Hola de esta sección es un usuario de prueba en el portal de administración de Azure de hello llamado a Britta Simon toocreate.</span><span class="sxs-lookup"><span data-stu-id="76f2c-173">hello objective of this section is toocreate a test user in hello Azure Management portal called Britta Simon.</span></span>

![Creación de un usuario de Azure AD][100]

<span data-ttu-id="76f2c-175">**toocreate un usuario de prueba en Azure AD, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="76f2c-175">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="76f2c-176">Hola **portal de administración de Azure**, en Hola panel de navegación izquierdo, haga clic en **Azure Active Directory** icono.</span><span class="sxs-lookup"><span data-stu-id="76f2c-176">In hello **Azure Management portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-teamwork-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="76f2c-178">Vaya demasiado**usuarios y grupos** y haga clic en **todos los usuarios** toodisplay lista de Hola de usuarios.</span><span class="sxs-lookup"><span data-stu-id="76f2c-178">Go too**Users and groups** and click **All users** toodisplay hello list of users.</span></span>
    
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-teamwork-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="76f2c-180">En la parte superior de saludo del cuadro de diálogo de hello haga clic en **agregar** tooopen hello **usuario** cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="76f2c-180">At hello top of hello dialog click **Add** tooopen hello **User** dialog.</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-teamwork-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="76f2c-182">En hello **usuario** cuadro de diálogo, siga los pasos de hello:</span><span class="sxs-lookup"><span data-stu-id="76f2c-182">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-teamwork-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="76f2c-184">a.</span><span class="sxs-lookup"><span data-stu-id="76f2c-184">a.</span></span> <span data-ttu-id="76f2c-185">Hola **nombre** cuadro de texto, tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="76f2c-185">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="76f2c-186">b.</span><span class="sxs-lookup"><span data-stu-id="76f2c-186">b.</span></span> <span data-ttu-id="76f2c-187">Hola **nombre de usuario** cuadro de texto, hello tipo **dirección de correo electrónico** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="76f2c-187">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="76f2c-188">c.</span><span class="sxs-lookup"><span data-stu-id="76f2c-188">c.</span></span> <span data-ttu-id="76f2c-189">Seleccione **Mostrar contraseña** y anote el valor de Hola de hello **contraseña**.</span><span class="sxs-lookup"><span data-stu-id="76f2c-189">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="76f2c-190">d.</span><span class="sxs-lookup"><span data-stu-id="76f2c-190">d.</span></span> <span data-ttu-id="76f2c-191">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="76f2c-191">Click **Create**.</span></span> 



### <a name="creating-a-teamwork-test-user"></a><span data-ttu-id="76f2c-192">Creación de un usuario de prueba de Teamwork</span><span class="sxs-lookup"><span data-stu-id="76f2c-192">Creating a Teamwork test user</span></span>

<span data-ttu-id="76f2c-193">En esta sección, creará un usuario llamado Britta Simon en Teamwork.</span><span class="sxs-lookup"><span data-stu-id="76f2c-193">In this section, you create a user called Britta Simon in Teamwork.</span></span> <span data-ttu-id="76f2c-194">Trabaje con [equipo de soporte técnico de trabajo en equipo](mailto:support@teamwork.com) a los usuarios de tooadd hello en la plataforma de trabajo en equipo Hola.</span><span class="sxs-lookup"><span data-stu-id="76f2c-194">Please work with [Teamwork support team](mailto:support@teamwork.com) tooadd hello users in hello Teamwork platform.</span></span>


### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="76f2c-195">Asignación de usuario de prueba de hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="76f2c-195">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="76f2c-196">En esta sección, se habilita Britta Simon toouse Azure inicio de sesión único mediante la concesión de su tooTeamwork de acceso.</span><span class="sxs-lookup"><span data-stu-id="76f2c-196">In this section, you enable Britta Simon toouse Azure single sign-on by granting her access tooTeamwork.</span></span>

![Asignar usuario][200] 

<span data-ttu-id="76f2c-198">**tooassign Britta Simon tooTeamwork, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="76f2c-198">**tooassign Britta Simon tooTeamwork, perform hello following steps:**</span></span>

1. <span data-ttu-id="76f2c-199">En el portal de administración de Azure de hello, abrir vista de aplicaciones de hello y, a continuación, navegue a vista de directorio toohello y vaya demasiado**aplicaciones empresariales** , a continuación, haga clic en **todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="76f2c-199">In hello Azure Management portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Asignar usuario][201] 

2. <span data-ttu-id="76f2c-201">En la lista de aplicaciones de hello, seleccione **trabajo en equipo**.</span><span class="sxs-lookup"><span data-stu-id="76f2c-201">In hello applications list, select **Teamwork**.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-teamwork-tutorial/tutorial_teamwork_50.png) 

3. <span data-ttu-id="76f2c-203">En el menú de Hola Hola izquierda, haga clic en **usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="76f2c-203">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Asignar usuario][202] 

4. <span data-ttu-id="76f2c-205">Haga clic en el botón **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="76f2c-205">Click **Add** button.</span></span> <span data-ttu-id="76f2c-206">Después, seleccione **Usuarios y grupos** en el cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="76f2c-206">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Asignar usuario][203]

5. <span data-ttu-id="76f2c-208">En **usuarios y grupos** cuadro de diálogo, seleccione **Britta Simon** en la lista de usuarios de Hola.</span><span class="sxs-lookup"><span data-stu-id="76f2c-208">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="76f2c-209">Haga clic en el botón **Seleccionar** del cuadro de diálogo **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="76f2c-209">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="76f2c-210">Haga clic en el botón **Asignar** del cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="76f2c-210">Click **Assign** button on **Add Assignment** dialog.</span></span>
    


### <a name="testing-single-sign-on"></a><span data-ttu-id="76f2c-211">Prueba del inicio de sesión único </span><span class="sxs-lookup"><span data-stu-id="76f2c-211">Testing single sign-on</span></span>

<span data-ttu-id="76f2c-212">En esta sección, comprobará su único inicio de sesión en configuración de Azure AD con hello Panel de acceso.</span><span class="sxs-lookup"><span data-stu-id="76f2c-212">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="76f2c-213">Al hacer clic en icono de trabajo en equipo Hola Hola Panel de acceso, deberá obtener aplicaciones de trabajo en equipo tooyour automáticamente ha iniciado sesión.</span><span class="sxs-lookup"><span data-stu-id="76f2c-213">When you click hello Teamwork tile in hello Access Panel, you should get automatically signed-on tooyour Teamwork application.</span></span>


## <a name="additional-resources"></a><span data-ttu-id="76f2c-214">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="76f2c-214">Additional resources</span></span>

* [<span data-ttu-id="76f2c-215">Lista de tutoriales sobre cómo tooIntegrate aplicaciones de SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="76f2c-215">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="76f2c-216">¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="76f2c-216">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-teamwork-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-teamwork-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-teamwork-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-teamwork-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-teamwork-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-teamwork-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-teamwork-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-teamwork-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-teamwork-tutorial/tutorial_general_203.png