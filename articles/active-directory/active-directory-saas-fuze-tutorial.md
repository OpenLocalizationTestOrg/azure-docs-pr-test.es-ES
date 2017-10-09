---
title: "Tutorial: Integración de Azure Active Directory con Fuze | Microsoft Docs"
description: "Obtenga información acerca de cómo tooconfigure inicio de sesión único entre Azure Active Directory y Fuze."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 9780b4bf-1fd1-48c1-9ceb-f750225ae08a
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/31/2017
ms.author: jeedes
ms.openlocfilehash: d0ea8c6456824e348301ed8bf1f5e00f4bfa8121
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-fuze"></a><span data-ttu-id="ddfe4-103">Tutorial: Integración de Azure Active Directory con Fuze</span><span class="sxs-lookup"><span data-stu-id="ddfe4-103">Tutorial: Azure Active Directory integration with Fuze</span></span>

<span data-ttu-id="ddfe4-104">En este tutorial, aprenderá cómo toointegrate Fuze con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="ddfe4-104">In this tutorial, you learn how toointegrate Fuze with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="ddfe4-105">Integración Fuze con Azure AD proporciona Hola siguientes ventajas:</span><span class="sxs-lookup"><span data-stu-id="ddfe4-105">Integrating Fuze with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="ddfe4-106">Puede controlar en Azure AD que tenga acceso tooFuze</span><span class="sxs-lookup"><span data-stu-id="ddfe4-106">You can control in Azure AD who has access tooFuze</span></span>
- <span data-ttu-id="ddfe4-107">Puede habilitar los usuarios tooautomatically get ha iniciado sesión tooFuze (Single Sign-On) con sus cuentas de Azure AD</span><span class="sxs-lookup"><span data-stu-id="ddfe4-107">You can enable your users tooautomatically get signed-on tooFuze (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="ddfe4-108">Puede administrar las cuentas en una ubicación central: portal de administración de Azure de Hola</span><span class="sxs-lookup"><span data-stu-id="ddfe4-108">You can manage your accounts in one central location - hello Azure Management portal</span></span>

<span data-ttu-id="ddfe4-109">Si desea obtener más información acerca de la integración de aplicaciones de SaaS con Azure AD tooknow, consulte [¿qué es acceso a la aplicación y el inicio de sesión único con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="ddfe4-109">If you want tooknow more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="ddfe4-110">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="ddfe4-110">Prerequisites</span></span>

<span data-ttu-id="ddfe4-111">integración de Azure AD con Fuze tooconfigure, necesita Hola siguientes elementos:</span><span class="sxs-lookup"><span data-stu-id="ddfe4-111">tooconfigure Azure AD integration with Fuze, you need hello following items:</span></span>

- <span data-ttu-id="ddfe4-112">Una suscripción de Azure AD</span><span class="sxs-lookup"><span data-stu-id="ddfe4-112">An Azure AD subscription</span></span>
- <span data-ttu-id="ddfe4-113">Una suscripción habilitada para inicio de sesión único en Fuze</span><span class="sxs-lookup"><span data-stu-id="ddfe4-113">A Fuze single-sign on enabled subscription</span></span>


> [!NOTE]
> <span data-ttu-id="ddfe4-114">Hola tootest los pasos de este tutorial, no se recomienda usar un entorno de producción.</span><span class="sxs-lookup"><span data-stu-id="ddfe4-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>


<span data-ttu-id="ddfe4-115">pasos de hello tootest en este tutorial, debe seguir estas recomendaciones:</span><span class="sxs-lookup"><span data-stu-id="ddfe4-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="ddfe4-116">No debe usar el entorno de producción, a menos que sea necesario.</span><span class="sxs-lookup"><span data-stu-id="ddfe4-116">You should not use your production environment, unless this is necessary.</span></span>
- <span data-ttu-id="ddfe4-117">Si no dispone de un entorno de prueba de Azure AD, puede obtener una versión de prueba de un mes [aquí](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="ddfe4-117">If you don't have an Azure AD trial environment, you can get an one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>


## <a name="scenario-description"></a><span data-ttu-id="ddfe4-118">Descripción del escenario</span><span class="sxs-lookup"><span data-stu-id="ddfe4-118">Scenario description</span></span>
<span data-ttu-id="ddfe4-119">En este tutorial, puede probar el inicio de sesión único de Azure AD en un entorno de prueba.</span><span class="sxs-lookup"><span data-stu-id="ddfe4-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="ddfe4-120">escenario de Hello descrito en este tutorial consta de dos bloques principales:</span><span class="sxs-lookup"><span data-stu-id="ddfe4-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="ddfe4-121">Agregar Fuze desde la Galería de Hola</span><span class="sxs-lookup"><span data-stu-id="ddfe4-121">Adding Fuze from hello gallery</span></span>
2. <span data-ttu-id="ddfe4-122">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="ddfe4-122">Configuring and testing Azure AD single sign-on</span></span>


## <a name="adding-fuze-from-hello-gallery"></a><span data-ttu-id="ddfe4-123">Agregar Fuze desde la Galería de Hola</span><span class="sxs-lookup"><span data-stu-id="ddfe4-123">Adding Fuze from hello gallery</span></span>
<span data-ttu-id="ddfe4-124">integración de hello tooconfigure de Fuze en Azure AD, deberá tooadd Fuze de lista de tooyour Hola Galería de aplicaciones administradas de SaaS.</span><span class="sxs-lookup"><span data-stu-id="ddfe4-124">tooconfigure hello integration of Fuze into Azure AD, you need tooadd Fuze from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="ddfe4-125">**tooadd Fuze de galería de hello, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="ddfe4-125">**tooadd Fuze from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="ddfe4-126">Hola  **[Portal de administración de Azure](https://portal.azure.com)**, en el panel de navegación izquierdo de Hola, haga clic en **Azure Active Directory** icono.</span><span class="sxs-lookup"><span data-stu-id="ddfe4-126">In hello **[Azure Management Portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="ddfe4-128">Navegue demasiado**aplicaciones empresariales**.</span><span class="sxs-lookup"><span data-stu-id="ddfe4-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="ddfe4-129">A continuación, vaya demasiado**todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="ddfe4-129">Then go too**All applications**.</span></span>

    ![Aplicaciones][2]
    
3. <span data-ttu-id="ddfe4-131">Haga clic en **agregar** botón en la parte superior de saludo del cuadro de diálogo de Hola.</span><span class="sxs-lookup"><span data-stu-id="ddfe4-131">Click **Add** button on hello top of hello dialog.</span></span>

    ![Aplicaciones][3]

4. <span data-ttu-id="ddfe4-133">En el cuadro de búsqueda de hello, escriba **Fuze**.</span><span class="sxs-lookup"><span data-stu-id="ddfe4-133">In hello search box, type **Fuze**.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-fuze-tutorial/tutorial_fuze_000.png)

5. <span data-ttu-id="ddfe4-135">En el panel de resultados de hello, seleccione **Fuze**y, a continuación, haga clic en **agregar** botón aplicación hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="ddfe4-135">In hello results panel, select **Fuze**, and then click **Add** button tooadd hello application.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-fuze-tutorial/tutorial_fuze_0001.png)


##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="ddfe4-137">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="ddfe4-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="ddfe4-138">En esta sección, podrá configurar y probar el inicio de sesión único de Azure AD con Fuze con un usuario de prueba llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="ddfe4-138">In this section, you configure and test Azure AD single sign-on with Fuze based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="ddfe4-139">Para toowork de inicio de sesión único, Azure AD necesita tooknow qué usuario equivalente de hello en Fuze es tooa usuario en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="ddfe4-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Fuze is tooa user in Azure AD.</span></span> <span data-ttu-id="ddfe4-140">En otras palabras, una relación de vínculo entre un usuario de Azure AD y el usuario relacionado de hello en Fuze debe toobe establecido.</span><span class="sxs-lookup"><span data-stu-id="ddfe4-140">In other words, a link relationship between an Azure AD user and hello related user in Fuze needs toobe established.</span></span>

<span data-ttu-id="ddfe4-141">Esta relación de vínculo se establece mediante la asignación de valor de Hola de hello **nombre de usuario** en Azure AD como valor de Hola de hello **nombre de usuario** en Fuze.</span><span class="sxs-lookup"><span data-stu-id="ddfe4-141">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in Fuze.</span></span>

<span data-ttu-id="ddfe4-142">tooconfigure y prueba de inicio de sesión único en Azure AD con Fuze, deberá hello toocomplete después de bloques de creación:</span><span class="sxs-lookup"><span data-stu-id="ddfe4-142">tooconfigure and test Azure AD single sign-on with Fuze, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="ddfe4-143">**[Configuración de Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable la toouse usuarios esta característica.</span><span class="sxs-lookup"><span data-stu-id="ddfe4-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="ddfe4-144">**[Crear un usuario de prueba de Azure AD](#creating-an-azure-ad-test-user)**  -inicio de sesión único en Azure AD tootest con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="ddfe4-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="ddfe4-145">**[Crear un usuario de prueba Fuze](#creating-a-fuze-test-user)**  -toohave un equivalente de Britta Simon en Fuze que está vinculado toohello Azure AD representación de ella.</span><span class="sxs-lookup"><span data-stu-id="ddfe4-145">**[Creating a Fuze test user](#creating-a-fuze-test-user)** - toohave a counterpart of Britta Simon in Fuze that is linked toohello Azure AD representation of her.</span></span>
4. <span data-ttu-id="ddfe4-146">**[Asignar usuario de prueba de hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="ddfe4-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="ddfe4-147">**[Pruebas de Single Sign-On](#testing-single-sign-on)**  -tooverify Hola si funciona la configuración.</span><span class="sxs-lookup"><span data-stu-id="ddfe4-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="ddfe4-148">Configuración del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="ddfe4-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="ddfe4-149">En esta sección, habilitar inicio de sesión único en Azure AD en el portal de administración de Azure de Hola y configurar el inicio de sesión único en la aplicación Fuze.</span><span class="sxs-lookup"><span data-stu-id="ddfe4-149">In this section, you enable Azure AD single sign-on in hello Azure Management portal and configure single sign-on in your Fuze application.</span></span>

<span data-ttu-id="ddfe4-150">**inicio de sesión único en Azure AD tooconfigure con Fuze, realizar Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="ddfe4-150">**tooconfigure Azure AD single sign-on with Fuze, perform hello following steps:**</span></span>

1. <span data-ttu-id="ddfe4-151">En el portal de administración de Azure de hello, en hello **Fuze** página de integración de aplicaciones, haga clic en **inicio de sesión único**.</span><span class="sxs-lookup"><span data-stu-id="ddfe4-151">In hello Azure Management portal, on hello **Fuze** application integration page, click **Single sign-on**.</span></span>

    ![Configurar inicio de sesión único][4]

2. <span data-ttu-id="ddfe4-153">En hello **inicio de sesión único** cuadro de diálogo, como **modo** seleccione **sesión basado en SAML** tooenable inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="ddfe4-153">On hello **Single sign-on** dialog, as **Mode** select **SAML-based Sign-on** tooenable single sign on.</span></span>
 
    ![Configurar inicio de sesión único](./media/active-directory-saas-fuze-tutorial/tutorial_fuze_01.png)

3. <span data-ttu-id="ddfe4-155">En hello **Fuze dominio y las direcciones URL** sección, lleve a cabo Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="ddfe4-155">On hello **Fuze Domain and URLs** section, perform hello following steps:</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-fuze-tutorial/tutorial_fuze_020.png)
    
    <span data-ttu-id="ddfe4-157">Hola **dirección URL de inicio de sesión** cuadro de texto, escriba la dirección URL Hola inicio de sesión como:`https://www.thinkingphones.com/jetspeed/portal/`</span><span class="sxs-lookup"><span data-stu-id="ddfe4-157">In hello **Sign on URL** textbox, type hello Sign-on URL as: `https://www.thinkingphones.com/jetspeed/portal/`</span></span>

4.  <span data-ttu-id="ddfe4-158">Haga clic en el botón **Guardar** .</span><span class="sxs-lookup"><span data-stu-id="ddfe4-158">Click **Save** button.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-fuze-tutorial/tutorial_general_400.png)

5. <span data-ttu-id="ddfe4-160">En hello **el certificado de firma de SAML** sección, haga clic en **Metadata XML** y, a continuación, guarde el archivo xml de hello en el equipo.</span><span class="sxs-lookup"><span data-stu-id="ddfe4-160">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello xml file on your computer.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-fuze-tutorial/tutorial_fuze_05.png) 

6. <span data-ttu-id="ddfe4-162">tooconfigure inicio de sesión único en **Fuze** lado, necesita hello toosend descargado **Metadata XML** demasiado[equipo de soporte técnico de Fuze](https://www.fuze.com/support).</span><span class="sxs-lookup"><span data-stu-id="ddfe4-162">tooconfigure single sign-on on **Fuze** side, you need toosend hello downloaded **Metadata XML** too[Fuze support team](https://www.fuze.com/support).</span></span> <span data-ttu-id="ddfe4-163">Configurará esto Hola de toohave orden configurada correctamente en ambos lados de la conexión de SSO de SAML.</span><span class="sxs-lookup"><span data-stu-id="ddfe4-163">They will set this up in order toohave hello SAML SSO connection set properly on both sides.</span></span>


### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="ddfe4-164">Creación de un usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="ddfe4-164">Creating an Azure AD test user</span></span>
<span data-ttu-id="ddfe4-165">objetivo de Hola de esta sección es un usuario de prueba en el portal de administración de Azure de hello llamado a Britta Simon toocreate.</span><span class="sxs-lookup"><span data-stu-id="ddfe4-165">hello objective of this section is toocreate a test user in hello Azure Management portal called Britta Simon.</span></span>

![Creación de un usuario de Azure AD][100]

<span data-ttu-id="ddfe4-167">**toocreate un usuario de prueba en Azure AD, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="ddfe4-167">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="ddfe4-168">Hola **portal de administración de Azure**, en Hola panel de navegación izquierdo, haga clic en **Azure Active Directory** icono.</span><span class="sxs-lookup"><span data-stu-id="ddfe4-168">In hello **Azure Management portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-fuze-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="ddfe4-170">Vaya demasiado**usuarios y grupos** y haga clic en **todos los usuarios** toodisplay lista de Hola de usuarios.</span><span class="sxs-lookup"><span data-stu-id="ddfe4-170">Go too**Users and groups** and click **All users** toodisplay hello list of users.</span></span>
    
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-fuze-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="ddfe4-172">En la parte superior de saludo del cuadro de diálogo de hello haga clic en **agregar** tooopen hello **usuario** cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="ddfe4-172">At hello top of hello dialog click **Add** tooopen hello **User** dialog.</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-fuze-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="ddfe4-174">En hello **usuario** cuadro de diálogo, siga los pasos de hello:</span><span class="sxs-lookup"><span data-stu-id="ddfe4-174">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-fuze-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="ddfe4-176">a.</span><span class="sxs-lookup"><span data-stu-id="ddfe4-176">a.</span></span> <span data-ttu-id="ddfe4-177">Hola **nombre** cuadro de texto, tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="ddfe4-177">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="ddfe4-178">b.</span><span class="sxs-lookup"><span data-stu-id="ddfe4-178">b.</span></span> <span data-ttu-id="ddfe4-179">Hola **nombre de usuario** cuadro de texto, hello tipo **dirección de correo electrónico** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="ddfe4-179">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="ddfe4-180">c.</span><span class="sxs-lookup"><span data-stu-id="ddfe4-180">c.</span></span> <span data-ttu-id="ddfe4-181">Seleccione **Mostrar contraseña** y anote el valor de Hola de hello **contraseña**.</span><span class="sxs-lookup"><span data-stu-id="ddfe4-181">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="ddfe4-182">d.</span><span class="sxs-lookup"><span data-stu-id="ddfe4-182">d.</span></span> <span data-ttu-id="ddfe4-183">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="ddfe4-183">Click **Create**.</span></span> 


### <a name="creating-a-fuze-test-user"></a><span data-ttu-id="ddfe4-184">Creación de un usuario de prueba de Fuze</span><span class="sxs-lookup"><span data-stu-id="ddfe4-184">Creating a Fuze test user</span></span>

<span data-ttu-id="ddfe4-185">Fuze admite aprovisionamiento de usuarios Just-In-Time, por lo que los usuarios se crearán automáticamente al iniciar sesión.</span><span class="sxs-lookup"><span data-stu-id="ddfe4-185">Fuze application supports full Just in time user provision, so users will get created automatically when they sign-in.</span></span> <span data-ttu-id="ddfe4-186">Para cualquier otra aclaración, póngase en contacto con el [equipo de soporte de Fuze](https://www.fuze.com/support).</span><span class="sxs-lookup"><span data-stu-id="ddfe4-186">For any other clarification, please contact Fuze [support](https://www.fuze.com/support).</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="ddfe4-187">Asignación de usuario de prueba de hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="ddfe4-187">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="ddfe4-188">En esta sección, se habilita Britta Simon toouse Azure inicio de sesión único mediante la concesión de su tooFuze de acceso.</span><span class="sxs-lookup"><span data-stu-id="ddfe4-188">In this section, you enable Britta Simon toouse Azure single sign-on by granting her access tooFuze.</span></span>

![Asignar usuario][200] 

<span data-ttu-id="ddfe4-190">**tooassign Britta Simon tooFuze, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="ddfe4-190">**tooassign Britta Simon tooFuze, perform hello following steps:**</span></span>

1. <span data-ttu-id="ddfe4-191">En el portal de administración de Azure de hello, abrir vista de aplicaciones de hello y, a continuación, navegue a vista de directorio toohello y vaya demasiado**aplicaciones empresariales** , a continuación, haga clic en **todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="ddfe4-191">In hello Azure Management portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Asignar usuario][201] 

2. <span data-ttu-id="ddfe4-193">En la lista de aplicaciones de hello, seleccione **Fuze**.</span><span class="sxs-lookup"><span data-stu-id="ddfe4-193">In hello applications list, select **Fuze**.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-fuze-tutorial/tutorial_fuze_50.png) 

3. <span data-ttu-id="ddfe4-195">En el menú de Hola Hola izquierda, haga clic en **usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="ddfe4-195">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Asignar usuario][202] 

4. <span data-ttu-id="ddfe4-197">Haga clic en el botón **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="ddfe4-197">Click **Add** button.</span></span> <span data-ttu-id="ddfe4-198">Después, seleccione **Usuarios y grupos** en el cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="ddfe4-198">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Asignar usuario][203]

5. <span data-ttu-id="ddfe4-200">En **usuarios y grupos** cuadro de diálogo, seleccione **Britta Simon** en la lista de usuarios de Hola.</span><span class="sxs-lookup"><span data-stu-id="ddfe4-200">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="ddfe4-201">Haga clic en el botón **Seleccionar** del cuadro de diálogo **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="ddfe4-201">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="ddfe4-202">Haga clic en el botón **Asignar** del cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="ddfe4-202">Click **Assign** button on **Add Assignment** dialog.</span></span>
    

### <a name="testing-single-sign-on"></a><span data-ttu-id="ddfe4-203">Prueba del inicio de sesión único </span><span class="sxs-lookup"><span data-stu-id="ddfe4-203">Testing single sign-on</span></span>

<span data-ttu-id="ddfe4-204">En esta sección, comprobará su único inicio de sesión en configuración de Azure AD con hello Panel de acceso.</span><span class="sxs-lookup"><span data-stu-id="ddfe4-204">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="ddfe4-205">Al hacer clic en icono de Fuze Hola Hola Panel de acceso, deberá obtener la aplicación de Fuze tooyour automáticamente ha iniciado sesión.</span><span class="sxs-lookup"><span data-stu-id="ddfe4-205">When you click hello Fuze tile in hello Access Panel, you should get automatically signed-on tooyour Fuze application.</span></span>


## <a name="additional-resources"></a><span data-ttu-id="ddfe4-206">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="ddfe4-206">Additional resources</span></span>

* [<span data-ttu-id="ddfe4-207">Lista de tutoriales sobre cómo tooIntegrate aplicaciones de SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="ddfe4-207">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="ddfe4-208">¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="ddfe4-208">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-fuze-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-fuze-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-fuze-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-fuze-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-fuze-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-fuze-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-fuze-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-fuze-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-fuze-tutorial/tutorial_general_203.png