---
title: "Tutorial: Integración de Azure Active Directory con LinkedIn Learning | Microsoft Docs"
description: "Obtenga información acerca de cómo tooconfigure inicio de sesión único entre Azure Active Directory y aprendizaje de LinkedIn."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: d5857070-bf79-4bd3-9a2a-4c1919a74946
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/15/2017
ms.author: jeedes
ms.openlocfilehash: 14610a25132ed0ccf5892cad6ccc4e1ef03ff280
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-linkedin-learning"></a><span data-ttu-id="c325e-103">Tutorial: Integración de Azure Active Directory con LinkedIn Learning</span><span class="sxs-lookup"><span data-stu-id="c325e-103">Tutorial: Azure Active Directory integration with LinkedIn Learning</span></span>

<span data-ttu-id="c325e-104">En este tutorial, aprenderá cómo toointegrate aprendizaje de LinkedIn con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="c325e-104">In this tutorial, you learn how toointegrate LinkedIn Learning with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="c325e-105">Integración de aprendizaje de LinkedIn con Azure AD proporciona Hola siguientes ventajas:</span><span class="sxs-lookup"><span data-stu-id="c325e-105">Integrating LinkedIn Learning with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="c325e-106">Puede controlar en Azure AD que tenga acceso tooLinkedIn de aprendizaje</span><span class="sxs-lookup"><span data-stu-id="c325e-106">You can control in Azure AD who has access tooLinkedIn Learning</span></span>
- <span data-ttu-id="c325e-107">Puede habilitar los usuarios tooautomatically get ha iniciado sesión tooLinkedIn aprendizaje (Single Sign-On) con sus cuentas de Azure AD</span><span class="sxs-lookup"><span data-stu-id="c325e-107">You can enable your users tooautomatically get signed-on tooLinkedIn Learning (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="c325e-108">Puede administrar las cuentas en una ubicación central: Hola portal de Azure</span><span class="sxs-lookup"><span data-stu-id="c325e-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="c325e-109">Si desea obtener más información acerca de la integración de aplicaciones de SaaS con Azure AD tooknow, consulte [¿qué es acceso a la aplicación y el inicio de sesión único con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="c325e-109">If you want tooknow more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="c325e-110">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="c325e-110">Prerequisites</span></span>

<span data-ttu-id="c325e-111">tooconfigure integración de Azure AD con el aprendizaje de LinkedIn, necesita Hola siguientes elementos:</span><span class="sxs-lookup"><span data-stu-id="c325e-111">tooconfigure Azure AD integration with LinkedIn Learning, you need hello following items:</span></span>

- <span data-ttu-id="c325e-112">Una suscripción de Azure AD</span><span class="sxs-lookup"><span data-stu-id="c325e-112">An Azure AD subscription</span></span>
- <span data-ttu-id="c325e-113">Una suscripción habilitada para el inicio de sesión único en LinkedIn Learning</span><span class="sxs-lookup"><span data-stu-id="c325e-113">A LinkedIn Learning single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="c325e-114">Hola tootest los pasos de este tutorial, no se recomienda usar un entorno de producción.</span><span class="sxs-lookup"><span data-stu-id="c325e-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="c325e-115">pasos de hello tootest en este tutorial, debe seguir estas recomendaciones:</span><span class="sxs-lookup"><span data-stu-id="c325e-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="c325e-116">No use el entorno de producción, salvo que sea necesario.</span><span class="sxs-lookup"><span data-stu-id="c325e-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="c325e-117">Si no dispone de un entorno de prueba de Azure AD, puede obtener una versión de prueba de un mes [aquí](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="c325e-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="c325e-118">Descripción del escenario</span><span class="sxs-lookup"><span data-stu-id="c325e-118">Scenario description</span></span>
<span data-ttu-id="c325e-119">En este tutorial, puede probar el inicio de sesión único de Azure AD en un entorno de prueba.</span><span class="sxs-lookup"><span data-stu-id="c325e-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="c325e-120">escenario de Hello descrito en este tutorial consta de dos bloques principales:</span><span class="sxs-lookup"><span data-stu-id="c325e-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="c325e-121">Agregar LinkedIn aprendizaje desde la Galería de Hola</span><span class="sxs-lookup"><span data-stu-id="c325e-121">Adding LinkedIn Learning from hello gallery</span></span>
2. <span data-ttu-id="c325e-122">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="c325e-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-linkedin-learning-from-hello-gallery"></a><span data-ttu-id="c325e-123">Agregar LinkedIn aprendizaje desde la Galería de Hola</span><span class="sxs-lookup"><span data-stu-id="c325e-123">Adding LinkedIn Learning from hello gallery</span></span>
<span data-ttu-id="c325e-124">integración de hello tooconfigure de aprendizaje de LinkedIn en Azure AD, deberá tooadd LinkedIn aprendizaje de lista de tooyour Hola Galería de aplicaciones administradas de SaaS.</span><span class="sxs-lookup"><span data-stu-id="c325e-124">tooconfigure hello integration of LinkedIn Learning into Azure AD, you need tooadd LinkedIn Learning from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="c325e-125">**tooadd LinkedIn aprendizaje de galería de hello, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="c325e-125">**tooadd LinkedIn Learning from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="c325e-126">Hola  **[portal de Azure](https://portal.azure.com)**, en el panel de navegación izquierdo de Hola, haga clic en **Azure Active Directory** icono.</span><span class="sxs-lookup"><span data-stu-id="c325e-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="c325e-128">Navegue demasiado**aplicaciones empresariales**.</span><span class="sxs-lookup"><span data-stu-id="c325e-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="c325e-129">A continuación, vaya demasiado**todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="c325e-129">Then go too**All applications**.</span></span>

    ![Aplicaciones][2]
    
3. <span data-ttu-id="c325e-131">Haga clic en **agregar** botón en la parte superior de saludo del cuadro de diálogo de Hola.</span><span class="sxs-lookup"><span data-stu-id="c325e-131">Click **Add** button on hello top of hello dialog.</span></span>

    ![Aplicaciones][3]

4. <span data-ttu-id="c325e-133">En el cuadro de búsqueda de hello, escriba **LinkedIn aprendizaje**.</span><span class="sxs-lookup"><span data-stu-id="c325e-133">In hello search box, type **LinkedIn Learning**.</span></span> <span data-ttu-id="c325e-134">En el panel de resultados, haga clic en **LinkedIn aprendizaje** aplicación de hello tooadd.</span><span class="sxs-lookup"><span data-stu-id="c325e-134">From results panel, click **LinkedIn Learning** tooadd hello application.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-linkedinlearning-tutorial/tutorial-linkedinlearning_000.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="c325e-136">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="c325e-136">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="c325e-137">En esta sección, configurará y probará el inicio de sesión único de Azure AD con LinkedIn Learning utilizando usuario de prueba llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="c325e-137">In this section, you configure and test Azure AD single sign-on with LinkedIn Learning based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="c325e-138">Para toowork de inicio de sesión único, Azure AD necesita tooknow qué usuario equivalente de hello en el aprendizaje de LinkedIn es tooa usuario en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="c325e-138">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in LinkedIn Learning is tooa user in Azure AD.</span></span> <span data-ttu-id="c325e-139">En otras palabras, una relación de vínculo entre un usuario de Azure AD y el usuario relacionado de hello en el aprendizaje de LinkedIn debe toobe establecido.</span><span class="sxs-lookup"><span data-stu-id="c325e-139">In other words, a link relationship between an Azure AD user and hello related user in LinkedIn Learning needs toobe established.</span></span>

<span data-ttu-id="c325e-140">Esta relación de vínculo se establece mediante la asignación de valor de Hola de hello **nombre de usuario** en Azure AD como valor de Hola de hello **nombre de usuario** en el aprendizaje de LinkedIn.</span><span class="sxs-lookup"><span data-stu-id="c325e-140">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in LinkedIn Learning.</span></span>

<span data-ttu-id="c325e-141">tooconfigure y prueba de inicio de sesión único en Azure AD con aprendizaje LinkedIn, deberá hello toocomplete después de bloques de creación:</span><span class="sxs-lookup"><span data-stu-id="c325e-141">tooconfigure and test Azure AD single sign-on with LinkedIn Learning, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="c325e-142">**[Configuración de Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable la toouse usuarios esta característica.</span><span class="sxs-lookup"><span data-stu-id="c325e-142">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="c325e-143">**[Crear un usuario de prueba de Azure AD](#creating-an-azure-ad-test-user)**  -inicio de sesión único en Azure AD tootest con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="c325e-143">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="c325e-144">**[Crear un usuario de prueba de aprendizaje de LinkedIn](#creating-a-linkedin-learning-test-user)**  -inicio de sesión único en Azure AD tootest con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="c325e-144">**[Creating a LinkedIn Learning test user](#creating-a-linkedin-learning-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
4. <span data-ttu-id="c325e-145">**[Asignar usuario de prueba de hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="c325e-145">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="c325e-146">**[Pruebas de Single Sign-On](#testing-single-sign-on)**  -tooverify Hola si funciona la configuración.</span><span class="sxs-lookup"><span data-stu-id="c325e-146">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="c325e-147">Configuración del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="c325e-147">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="c325e-148">En esta sección, habilitar inicio de sesión único en Azure AD en hello portal de Azure y configurar el inicio de sesión único en la aplicación de aprendizaje de LinkedIn.</span><span class="sxs-lookup"><span data-stu-id="c325e-148">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your LinkedIn Learning application.</span></span>

<span data-ttu-id="c325e-149">**inicio de sesión único en tooconfigure Azure AD con el aprendizaje de LinkedIn, realizar Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="c325e-149">**tooconfigure Azure AD single sign-on with LinkedIn Learning, perform hello following steps:**</span></span>

1. <span data-ttu-id="c325e-150">En el portal de Azure, en Hola Hola **LinkedIn aprendizaje** página de integración de aplicaciones, haga clic en **inicio de sesión único**.</span><span class="sxs-lookup"><span data-stu-id="c325e-150">In hello Azure portal, on hello **LinkedIn Learning** application integration page, click **Single sign-on**.</span></span>

    ![Configurar inicio de sesión único][4]

2. <span data-ttu-id="c325e-152">En hello **inicio de sesión único** cuadro de diálogo, seleccione **modo** como **sesión basado en SAML** tooenable inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="c325e-152">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurar inicio de sesión único](./media/active-directory-saas-linkedinlearning-tutorial/tutorial-linkedin_01.png)

3. <span data-ttu-id="c325e-154">En una ventana del explorador web diferente, inquilino de aprendizaje de LinkedIn tooyour inicio de sesión como administrador.</span><span class="sxs-lookup"><span data-stu-id="c325e-154">In a different web browser window, sign-on tooyour LinkedIn Learning tenant as an administrator.</span></span>

4. <span data-ttu-id="c325e-155">En **Account Center** (Centro de cuentas), haga clic en **Global Settings** (Configuración global) en **Settings** (Configuración).</span><span class="sxs-lookup"><span data-stu-id="c325e-155">In **Account Center**, click **Global Settings** under **Settings**.</span></span> <span data-ttu-id="c325e-156">Además, seleccione **aprendizaje - predeterminado** en lista de desplegable Hola.</span><span class="sxs-lookup"><span data-stu-id="c325e-156">Also, select **Learning - Default** from hello dropdown list.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-linkedinlearning-tutorial/tutorial_linkedin_admin_01.png)

5. <span data-ttu-id="c325e-158">Haga clic en **o haga clic aquí tooload y copie los campos individuales de formulario de hello** y copie **Id. de entidad** y **dirección Url de acceso de consumidor de aserción (ACS)**</span><span class="sxs-lookup"><span data-stu-id="c325e-158">Click **OR Click Here tooload and copy individual fields from hello form** and copy **Entity Id** and **Assertion Consumer Access (ACS) Url**</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-linkedinlearning-tutorial/tutorial_linkedin_admin_03.png)

6. <span data-ttu-id="c325e-160">En el portal de Azure, en **LinkedIn aprendizaje dominio y las direcciones URL**, realizar Hola siguientes pasos si desea tooconfigure SSO en **iniciado por IdP** modo</span><span class="sxs-lookup"><span data-stu-id="c325e-160">On Azure portal, under **LinkedIn Learning Domain and URLs**, perform hello following steps if you want tooconfigure SSO in **IdP Initiated** mode</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-linkedinlearning-tutorial/tutorial_linkedin_signon_01.png)

    <span data-ttu-id="c325e-162">a.</span><span class="sxs-lookup"><span data-stu-id="c325e-162">a.</span></span> <span data-ttu-id="c325e-163">Hola **identificador** cuadro de texto, escriba Hola **Id. de entidad** copiados desde el LinkedIn Portal</span><span class="sxs-lookup"><span data-stu-id="c325e-163">In hello **Identifier** textbox, enter hello **Entity ID** copied from LinkedIn Portal</span></span> 

    <span data-ttu-id="c325e-164">b.</span><span class="sxs-lookup"><span data-stu-id="c325e-164">b.</span></span> <span data-ttu-id="c325e-165">Hola **dirección URL de respuesta** cuadro de texto, escriba Hola **dirección Url de acceso de consumidor de aserción (ACS)** copiados desde el LinkedIn Portal</span><span class="sxs-lookup"><span data-stu-id="c325e-165">In hello **Reply URL** textbox, enter hello **Assertion Consumer Access (ACS) Url** copied from LinkedIn Portal</span></span>

7. <span data-ttu-id="c325e-166">Si desea que tooconfigure SSO en **iniciado en SP**, a continuación, haga clic en la opción Mostrar URL avanzada en la sección de configuración de Hola y configurar dirección URL de inicio de sesión de hello con hello siguiente patrón:</span><span class="sxs-lookup"><span data-stu-id="c325e-166">If you want tooconfigure SSO in **SP Initiated**, then click Show Advanced URL setting option in hello configuration section and configure hello sign-on URL with hello following pattern:</span></span>

    `https://www.linkedin.com/checkpoint/enterprise/login/<AccountId>?application=learning&applicationInstanceId=<InstanceId>`

    ![Configurar inicio de sesión único](./media/active-directory-saas-linkedinlearning-tutorial/tutorial_linkedin_signon_02.png)   
    
8. <span data-ttu-id="c325e-168">La aplicación de aprendizaje de LinkedIn espera las aserciones de SAML de hello en un formato específico, lo que requiere tooadd atributo personalizado tooyour SAML atributos de token configuración de asignaciones.</span><span class="sxs-lookup"><span data-stu-id="c325e-168">Your LinkedIn Learning application expects hello SAML assertions in a specific format, which requires you tooadd custom attribute mappings tooyour SAML token attributes configuration.</span></span> <span data-ttu-id="c325e-169">Hola siguiente captura de pantalla muestra un ejemplo de esto.</span><span class="sxs-lookup"><span data-stu-id="c325e-169">hello following screenshot shows an example for this.</span></span> <span data-ttu-id="c325e-170">Hola valor predeterminado de **identificador de usuario** es **user.userprincipalname** pero LinkedIn aprendizaje espera este toobe asignado con la dirección de correo electrónico del usuario de Hola.</span><span class="sxs-lookup"><span data-stu-id="c325e-170">hello default value of **User Identifier** is **user.userprincipalname** but LinkedIn Learning expects this toobe mapped with hello user's email address.</span></span> <span data-ttu-id="c325e-171">Para que puede usar **user.mail** de atributo de la lista de Hola o usar el valor de atributo apropiado de hello según la configuración de la organización.</span><span class="sxs-lookup"><span data-stu-id="c325e-171">For that you can use **user.mail** attribute from hello list or use hello appropriate attribute value based on your organization configuration.</span></span> 

    ![Configurar inicio de sesión único](./media/active-directory-saas-linkedinlearning-tutorial/updateusermail.png)
    
9. <span data-ttu-id="c325e-173">En **atributos de usuario** sección, haga clic en **ver y editar todos los demás atributos de usuario** y establezca los atributos de Hola.</span><span class="sxs-lookup"><span data-stu-id="c325e-173">In **User Attributes** section, click **View and edit all other user attributes** and set hello attributes.</span></span> <span data-ttu-id="c325e-174">usuario de Hello necesita cuatro notificaciones tooadd denominados **correo electrónico**, **departamento**, **firstname**, y **lastname** y valor de hello es toobe asignado con **user.mail**, **user.department**, **user.givenname**, y **user.surname** respectivamente</span><span class="sxs-lookup"><span data-stu-id="c325e-174">hello user needs tooadd four claims named **email**, **department**, **firstname**, and **lastname** and hello value is toobe mapped with **user.mail**, **user.department**, **user.givenname**, and **user.surname** respectively</span></span>

    | <span data-ttu-id="c325e-175">Nombre del atributo</span><span class="sxs-lookup"><span data-stu-id="c325e-175">Attribute Name</span></span> | <span data-ttu-id="c325e-176">Valor de atributo</span><span class="sxs-lookup"><span data-stu-id="c325e-176">Attribute Value</span></span> |
    | --- | --- |
    | <span data-ttu-id="c325e-177">email</span><span class="sxs-lookup"><span data-stu-id="c325e-177">email</span></span>| <span data-ttu-id="c325e-178">user.mail</span><span class="sxs-lookup"><span data-stu-id="c325e-178">user.mail</span></span> |    
    | <span data-ttu-id="c325e-179">department</span><span class="sxs-lookup"><span data-stu-id="c325e-179">department</span></span>| <span data-ttu-id="c325e-180">user.department</span><span class="sxs-lookup"><span data-stu-id="c325e-180">user.department</span></span> |
    | <span data-ttu-id="c325e-181">firstname</span><span class="sxs-lookup"><span data-stu-id="c325e-181">firstname</span></span>| <span data-ttu-id="c325e-182">user.givenname</span><span class="sxs-lookup"><span data-stu-id="c325e-182">user.givenname</span></span> |
    | <span data-ttu-id="c325e-183">lastname</span><span class="sxs-lookup"><span data-stu-id="c325e-183">lastname</span></span>| <span data-ttu-id="c325e-184">user.surname</span><span class="sxs-lookup"><span data-stu-id="c325e-184">user.surname</span></span> |
    
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-linkedinlearning-tutorial/userattribute.png)
    
    <span data-ttu-id="c325e-186">a.</span><span class="sxs-lookup"><span data-stu-id="c325e-186">a.</span></span> <span data-ttu-id="c325e-187">Haga clic en **Agregar atributo** el cuadro de diálogo de tooopen Hola atributo.</span><span class="sxs-lookup"><span data-stu-id="c325e-187">Click **Add Attribute** tooopen hello attribute dialog.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-linkedinLearning-tutorial/tutorial_attribute_04.png)

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-linkedinLearning-tutorial/tutorial_attribute_05.png)
    
    <span data-ttu-id="c325e-190">b.</span><span class="sxs-lookup"><span data-stu-id="c325e-190">b.</span></span> <span data-ttu-id="c325e-191">Hola **nombre** cuadro de texto, nombre de atributo de tipo hello se muestra para esa fila.</span><span class="sxs-lookup"><span data-stu-id="c325e-191">In hello **Name** textbox, type hello attribute name shown for that row.</span></span>
    
    <span data-ttu-id="c325e-192">c.</span><span class="sxs-lookup"><span data-stu-id="c325e-192">c.</span></span> <span data-ttu-id="c325e-193">De hello **valor** lista, el valor de atributo de tipo hello se muestra para esa fila.</span><span class="sxs-lookup"><span data-stu-id="c325e-193">From hello **Value** list, type hello attribute value shown for that row.</span></span>
    
    <span data-ttu-id="c325e-194">d.</span><span class="sxs-lookup"><span data-stu-id="c325e-194">d.</span></span> <span data-ttu-id="c325e-195">Haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="c325e-195">Click **Ok**</span></span>

10. <span data-ttu-id="c325e-196">Realizar Hola seguir pasos de hello **nombre** atributo:</span><span class="sxs-lookup"><span data-stu-id="c325e-196">Perform hello following steps on hello **name** attribute-</span></span>

    <span data-ttu-id="c325e-197">a.</span><span class="sxs-lookup"><span data-stu-id="c325e-197">a.</span></span> <span data-ttu-id="c325e-198">Haga clic en Hola de hello atributo tooopen **Editar atributo** ventana.</span><span class="sxs-lookup"><span data-stu-id="c325e-198">Click on hello attribute tooopen hello **Edit Attribute** window.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-linkedinLearning-tutorial/url_update.png)

    <span data-ttu-id="c325e-200">b.</span><span class="sxs-lookup"><span data-stu-id="c325e-200">b.</span></span> <span data-ttu-id="c325e-201">Eliminar el valor de dirección URL de Hola de hello **espacio de nombres**.</span><span class="sxs-lookup"><span data-stu-id="c325e-201">Delete hello URL value from hello **namespace**.</span></span>
    
    <span data-ttu-id="c325e-202">c.</span><span class="sxs-lookup"><span data-stu-id="c325e-202">c.</span></span> <span data-ttu-id="c325e-203">Haga clic en **Aceptar** configuración de toosave Hola.</span><span class="sxs-lookup"><span data-stu-id="c325e-203">Click **Ok** toosave hello setting.</span></span>

11. <span data-ttu-id="c325e-204">En hello **el certificado de firma de SAML** sección, haga clic en **Metadata XML** y, a continuación, guarde el archivo XML de hello en el equipo.</span><span class="sxs-lookup"><span data-stu-id="c325e-204">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello XML file on your computer.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-linkedinlearning-tutorial/tutorial-linkedinlearning_certificate.png) 

12. <span data-ttu-id="c325e-206">Haga clic en **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="c325e-206">Click **Save**.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-linkedinlearning-tutorial/tutorial_general_400.png)

13. <span data-ttu-id="c325e-208">Vaya demasiado**configuración de administración de LinkedIn** sección.</span><span class="sxs-lookup"><span data-stu-id="c325e-208">Go too**LinkedIn Admin Settings** section.</span></span> <span data-ttu-id="c325e-209">Archivo XML con carga hello que descargó desde Hola portal de Azure haciendo clic en la opción de archivo de cargar XML de Hola.</span><span class="sxs-lookup"><span data-stu-id="c325e-209">Upload hello XML file you downloaded from hello Azure portal by clicking hello Upload XML file option.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-linkedinlearning-tutorial/tutorial_linkedin_metadata_03.png)

14. <span data-ttu-id="c325e-211">Haga clic en **en** tooenable SSO.</span><span class="sxs-lookup"><span data-stu-id="c325e-211">Click **On** tooenable SSO.</span></span> <span data-ttu-id="c325e-212">Estado SSO cambia de **no conectado** demasiado**conectado**</span><span class="sxs-lookup"><span data-stu-id="c325e-212">SSO status changes from **Not Connected** too**Connected**</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-linkedinlearning-tutorial/tutorial_linkedin_admin_05.png)

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="c325e-214">Creación de un usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="c325e-214">Creating an Azure AD test user</span></span>
<span data-ttu-id="c325e-215">objetivo de Hola de esta sección es un usuario de prueba en hello Azure portal llamado a Britta Simon toocreate.</span><span class="sxs-lookup"><span data-stu-id="c325e-215">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Creación de un usuario de Azure AD][100]

<span data-ttu-id="c325e-217">**toocreate un usuario de prueba en Azure AD, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="c325e-217">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="c325e-218">Hola **portal de Azure**, en Hola panel de navegación izquierdo, haga clic en **Azure Active Directory** icono.</span><span class="sxs-lookup"><span data-stu-id="c325e-218">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-linkedinlearning-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="c325e-220">lista de hello toodisplay de usuarios, vaya demasiado**usuarios y grupos** y haga clic en **todos los usuarios**.</span><span class="sxs-lookup"><span data-stu-id="c325e-220">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-linkedinlearning-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="c325e-222">Hola tooopen **usuario** cuadro de diálogo, haga clic en **agregar** en la parte superior de saludo del cuadro de diálogo de Hola.</span><span class="sxs-lookup"><span data-stu-id="c325e-222">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-linkedinlearning-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="c325e-224">En hello **usuario** cuadro de diálogo, siga los pasos de hello:</span><span class="sxs-lookup"><span data-stu-id="c325e-224">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-linkedinlearning-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="c325e-226">a.</span><span class="sxs-lookup"><span data-stu-id="c325e-226">a.</span></span> <span data-ttu-id="c325e-227">Hola **nombre** cuadro de texto, tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="c325e-227">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="c325e-228">b.</span><span class="sxs-lookup"><span data-stu-id="c325e-228">b.</span></span> <span data-ttu-id="c325e-229">Hola **nombre de usuario** cuadro de texto, hello tipo **dirección de correo electrónico** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="c325e-229">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="c325e-230">c.</span><span class="sxs-lookup"><span data-stu-id="c325e-230">c.</span></span> <span data-ttu-id="c325e-231">Seleccione **Mostrar contraseña** y anote el valor de Hola de hello **contraseña**.</span><span class="sxs-lookup"><span data-stu-id="c325e-231">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="c325e-232">d.</span><span class="sxs-lookup"><span data-stu-id="c325e-232">d.</span></span> <span data-ttu-id="c325e-233">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="c325e-233">Click **Create**.</span></span> 

### <a name="creating-a-linkedin-learning-test-user"></a><span data-ttu-id="c325e-234">Creación de un usuario de prueba de LinkedIn Learning</span><span class="sxs-lookup"><span data-stu-id="c325e-234">Creating a LinkedIn Learning test user</span></span>

<span data-ttu-id="c325e-235">La aplicación LinkedIn Learning admite</span><span class="sxs-lookup"><span data-stu-id="c325e-235">Linked Learning Application supports.</span></span> <span data-ttu-id="c325e-236">Justo a tiempo el aprovisionamiento de usuarios y después de la autenticación de usuarios se crean automáticamente en la aplicación hello.</span><span class="sxs-lookup"><span data-stu-id="c325e-236">Just in time user provisioning and after authentication users are created in hello application automatically.</span></span> <span data-ttu-id="c325e-237">Página de configuración de administración de hello en el conmutador de hello voltear portal de aprendizaje de LinkedIn hello **asignar automáticamente licencias** tooactive tooenable sólo en tiempo de aprovisionamiento y esto también asignarán a un usuario de toohello licencia.</span><span class="sxs-lookup"><span data-stu-id="c325e-237">On hello admin settings page on hello LinkedIn Learning portal flip hello switch **Automatically Assign licenses** tooactive tooenable Just in time provisioning and this will also assign a license toohello user.</span></span>
   
   ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-linkedinLearning-tutorial/LinkedinUserprovswitch.png)

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="c325e-239">Asignación de usuario de prueba de hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="c325e-239">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="c325e-240">En esta sección, habilitar Britta Simon toouse un inicio de sesión único Azure concediendo acceso tooLinkedIn de aprendizaje.</span><span class="sxs-lookup"><span data-stu-id="c325e-240">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooLinkedIn Learning.</span></span>

![Asignar usuario][200] 

<span data-ttu-id="c325e-242">**tooassign Britta Simon tooLinkedIn aprendizaje, realizar Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="c325e-242">**tooassign Britta Simon tooLinkedIn Learning, perform hello following steps:**</span></span>

1. <span data-ttu-id="c325e-243">Hola portal de Azure, abra la vista de aplicaciones de hello y, a continuación, navegue a vista de directorio toohello y vaya demasiado**aplicaciones empresariales** , a continuación, haga clic en **todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="c325e-243">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Asignar usuario][201] 

2. <span data-ttu-id="c325e-245">En la lista de aplicaciones de hello, seleccione **LinkedIn aprendizaje**.</span><span class="sxs-lookup"><span data-stu-id="c325e-245">In hello applications list, select **LinkedIn Learning**.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-linkedinlearning-tutorial/tutorial-linkedinlearning_0001.png) 

3. <span data-ttu-id="c325e-247">En el menú de Hola Hola izquierda, haga clic en **usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="c325e-247">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Asignar usuario][202] 

4. <span data-ttu-id="c325e-249">Haga clic en el botón **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="c325e-249">Click **Add** button.</span></span> <span data-ttu-id="c325e-250">Después, seleccione **Usuarios y grupos** en el cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="c325e-250">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Asignar usuario][203]

5. <span data-ttu-id="c325e-252">En **usuarios y grupos** cuadro de diálogo, seleccione **Britta Simon** en la lista de usuarios de Hola.</span><span class="sxs-lookup"><span data-stu-id="c325e-252">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="c325e-253">Haga clic en el botón **Seleccionar** del cuadro de diálogo **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="c325e-253">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="c325e-254">Haga clic en el botón **Asignar** del cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="c325e-254">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="c325e-255">Prueba del inicio de sesión único </span><span class="sxs-lookup"><span data-stu-id="c325e-255">Testing single sign-on</span></span>

<span data-ttu-id="c325e-256">En esta sección, comprobará su único inicio de sesión en configuración de Azure AD con hello Panel de acceso.</span><span class="sxs-lookup"><span data-stu-id="c325e-256">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="c325e-257">Al hacer clic en icono de aprendizaje de LinkedIn Hola Hola Panel de acceso, deberá obtener la página de inicio de sesión Azure Hola y de después de la sesión correctamente, deberá obtener en la aplicación de aprendizaje de LinkedIn.</span><span class="sxs-lookup"><span data-stu-id="c325e-257">When you click hello LinkedIn Learning tile in hello Access Panel, you should get hello Azure Sign-on page and on after successful sign-on, you should get into your LinkedIn Learning application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="c325e-258">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="c325e-258">Additional resources</span></span>

* [<span data-ttu-id="c325e-259">Lista de tutoriales sobre cómo tooIntegrate aplicaciones de SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="c325e-259">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="c325e-260">¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="c325e-260">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-linkedinlearning-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-linkedinlearning-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-linkedinlearning-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-linkedinlearning-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-linkedinlearning-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-linkedinlearning-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-linkedinlearning-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-linkedinlearning-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-linkedinlearning-tutorial/tutorial_general_203.png