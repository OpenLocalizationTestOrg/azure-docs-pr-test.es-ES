---
title: "Tutorial: Integración de Azure Active Directory con LinkedIn Lookup | Microsoft Docs"
description: "Obtenga información acerca de cómo tooconfigure inicio de sesión único entre Azure Active Directory y búsqueda de LinkedIn."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: a2757a39-1ead-4a3e-91e4-270be3055683
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/14/2017
ms.author: jeedes
ms.openlocfilehash: d79c34baa676391699e4b49806f16422fcfe73e1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-linkedin-lookup"></a><span data-ttu-id="e2901-103">Tutorial: Integración de Azure Active Directory con LinkedIn Lookup</span><span class="sxs-lookup"><span data-stu-id="e2901-103">Tutorial: Azure Active Directory integration with LinkedIn Lookup</span></span>

<span data-ttu-id="e2901-104">En este tutorial, aprenderá cómo toointegrate búsqueda LinkedIn con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="e2901-104">In this tutorial, you learn how toointegrate LinkedIn Lookup with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="e2901-105">Integración de búsqueda de LinkedIn con Azure AD proporciona Hola siguientes ventajas:</span><span class="sxs-lookup"><span data-stu-id="e2901-105">Integrating LinkedIn Lookup with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="e2901-106">Puede controlar en Azure AD que tenga acceso tooLinkedIn búsqueda</span><span class="sxs-lookup"><span data-stu-id="e2901-106">You can control in Azure AD who has access tooLinkedIn Lookup</span></span>
- <span data-ttu-id="e2901-107">Puede habilitar los usuarios tooautomatically get ha iniciado sesión tooLinkedIn búsqueda (Single Sign-On) con sus cuentas de Azure AD</span><span class="sxs-lookup"><span data-stu-id="e2901-107">You can enable your users tooautomatically get signed-on tooLinkedIn Lookup (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="e2901-108">Puede administrar las cuentas en una ubicación central: Hola portal de Azure</span><span class="sxs-lookup"><span data-stu-id="e2901-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="e2901-109">Si desea obtener más información acerca de la integración de aplicaciones de SaaS con Azure AD tooknow, consulte [¿qué es acceso a la aplicación y el inicio de sesión único con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="e2901-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="e2901-110">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="e2901-110">Prerequisites</span></span>

<span data-ttu-id="e2901-111">tooconfigure integración de Azure AD con búsqueda de LinkedIn, necesita Hola siguientes elementos:</span><span class="sxs-lookup"><span data-stu-id="e2901-111">tooconfigure Azure AD integration with LinkedIn Lookup, you need hello following items:</span></span>

- <span data-ttu-id="e2901-112">Una suscripción de Azure AD</span><span class="sxs-lookup"><span data-stu-id="e2901-112">An Azure AD subscription</span></span>
- <span data-ttu-id="e2901-113">Una suscripción habilitada para el inicio de sesión único en LinkedIn Lookup</span><span class="sxs-lookup"><span data-stu-id="e2901-113">An LinkedIn Lookup single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="e2901-114">Hola tootest los pasos de este tutorial, no se recomienda usar un entorno de producción.</span><span class="sxs-lookup"><span data-stu-id="e2901-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="e2901-115">pasos de hello tootest en este tutorial, debe seguir estas recomendaciones:</span><span class="sxs-lookup"><span data-stu-id="e2901-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="e2901-116">No use el entorno de producción, salvo que sea necesario.</span><span class="sxs-lookup"><span data-stu-id="e2901-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="e2901-117">Si no dispone de un entorno de prueba de Azure AD, puede obtener una versión de prueba de un mes [aquí](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="e2901-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="e2901-118">Descripción del escenario</span><span class="sxs-lookup"><span data-stu-id="e2901-118">Scenario description</span></span>
<span data-ttu-id="e2901-119">En este tutorial, puede probar el inicio de sesión único de Azure AD en un entorno de prueba.</span><span class="sxs-lookup"><span data-stu-id="e2901-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="e2901-120">escenario de Hello descrito en este tutorial consta de dos bloques principales:</span><span class="sxs-lookup"><span data-stu-id="e2901-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="e2901-121">Agregar LinkedIn búsqueda desde la Galería de Hola</span><span class="sxs-lookup"><span data-stu-id="e2901-121">Adding LinkedIn Lookup from hello gallery</span></span>
2. <span data-ttu-id="e2901-122">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="e2901-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-linkedin-lookup-from-hello-gallery"></a><span data-ttu-id="e2901-123">Agregar LinkedIn búsqueda desde la Galería de Hola</span><span class="sxs-lookup"><span data-stu-id="e2901-123">Adding LinkedIn Lookup from hello gallery</span></span>
<span data-ttu-id="e2901-124">integración de hello tooconfigure de búsqueda de LinkedIn en Azure AD, deberá tooadd LinkedIn búsqueda de lista de tooyour Hola Galería de aplicaciones administradas de SaaS.</span><span class="sxs-lookup"><span data-stu-id="e2901-124">tooconfigure hello integration of LinkedIn Lookup into Azure AD, you need tooadd LinkedIn Lookup from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="e2901-125">**tooadd LinkedIn búsqueda desde la Galería de hello, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="e2901-125">**tooadd LinkedIn Lookup from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="e2901-126">Hola  **[portal de Azure](https://portal.azure.com)**, en el panel de navegación izquierdo de Hola, haga clic en **Azure Active Directory** icono.</span><span class="sxs-lookup"><span data-stu-id="e2901-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="e2901-128">Navegue demasiado**aplicaciones empresariales**.</span><span class="sxs-lookup"><span data-stu-id="e2901-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="e2901-129">A continuación, vaya demasiado**todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="e2901-129">Then go too**All applications**.</span></span>

    ![Aplicaciones][2]
    
3. <span data-ttu-id="e2901-131">Haga clic en **nueva aplicación** botón en la parte superior de Hola de nueva aplicación de hello diálogo tooadd.</span><span class="sxs-lookup"><span data-stu-id="e2901-131">Click **New application** button on hello top of hello dialog tooadd new application.</span></span>

    ![Aplicaciones][3]

4. <span data-ttu-id="e2901-133">En el cuadro de búsqueda de hello, escriba **LinkedIn búsqueda**.</span><span class="sxs-lookup"><span data-stu-id="e2901-133">In hello search box, type **LinkedIn Lookup**.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-LinkedInlookup-tutorial/tutorial_linkedInlookup_search.png)

5. <span data-ttu-id="e2901-135">En el panel de resultados de hello, seleccione **LinkedIn búsqueda**y, a continuación, haga clic en **agregar** botón aplicación hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="e2901-135">In hello results panel, select **LinkedIn Lookup**, and then click **Add** button tooadd hello application.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-LinkedInlookup-tutorial/tutorial_linkedInlookup_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="e2901-137">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="e2901-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="e2901-138">En esta sección, configurará y probará el inicio de sesión único de Azure AD con LinkedIn Lookup utilizando un usuario de prueba llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="e2901-138">In this section, you configure and test Azure AD single sign-on with LinkedIn Lookup based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="e2901-139">Para toowork de inicio de sesión único, Azure AD necesita tooknow qué usuario equivalente de hello en búsqueda de LinkedIn es tooa usuario en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="e2901-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in LinkedIn Lookup is tooa user in Azure AD.</span></span> <span data-ttu-id="e2901-140">En otras palabras, una relación de vínculo entre un usuario de Azure AD y el usuario relacionado de hello en búsqueda de LinkedIn debe toobe establecido.</span><span class="sxs-lookup"><span data-stu-id="e2901-140">In other words, a link relationship between an Azure AD user and hello related user in LinkedIn Lookup needs toobe established.</span></span>

<span data-ttu-id="e2901-141">Esta relación de vínculo se establece mediante la asignación de valor de Hola de hello **nombre de usuario** en Azure AD como valor de Hola de hello **nombre de usuario** en búsqueda de LinkedIn.</span><span class="sxs-lookup"><span data-stu-id="e2901-141">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in LinkedIn Lookup.</span></span>

<span data-ttu-id="e2901-142">tooconfigure y prueba de inicio de sesión único en Azure AD con búsqueda de LinkedIn, deberá hello toocomplete después de bloques de creación:</span><span class="sxs-lookup"><span data-stu-id="e2901-142">tooconfigure and test Azure AD single sign-on with LinkedIn Lookup, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="e2901-143">**[Configuración de Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable la toouse usuarios esta característica.</span><span class="sxs-lookup"><span data-stu-id="e2901-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="e2901-144">**[Crear un usuario de prueba de Azure AD](#creating-an-azure-ad-test-user)**  -inicio de sesión único en Azure AD tootest con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="e2901-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="e2901-145">**[Creación de un usuario de prueba de búsqueda de LinkedIn](#creating-an-linkedin-lookup-test-user)**  -toohave un equivalente de Britta Simon en búsqueda de LinkedIn es representación toohello vinculado Azure AD.</span><span class="sxs-lookup"><span data-stu-id="e2901-145">**[Creating an LinkedIn Lookup test user](#creating-an-linkedin-lookup-test-user)** - toohave a counterpart of Britta Simon in LinkedIn Lookup that is linked toohello Azure AD representation.</span></span>
4. <span data-ttu-id="e2901-146">**[Asignar usuario de prueba de hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="e2901-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="e2901-147">**[Pruebas de Single Sign-On](#testing-single-sign-on)**  -tooverify Hola si funciona la configuración.</span><span class="sxs-lookup"><span data-stu-id="e2901-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="e2901-148">Configuración del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="e2901-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="e2901-149">En esta sección, habilitar inicio de sesión único en Azure AD en hello portal de Azure y configurar el inicio de sesión único en la aplicación de búsqueda de LinkedIn.</span><span class="sxs-lookup"><span data-stu-id="e2901-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your LinkedIn Lookup application.</span></span>

<span data-ttu-id="e2901-150">**inicio de sesión único en Azure AD tooconfigure con búsqueda de LinkedIn, realizar Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="e2901-150">**tooconfigure Azure AD single sign-on with LinkedIn Lookup, perform hello following steps:**</span></span>

1. <span data-ttu-id="e2901-151">En el portal de Azure, en Hola Hola **LinkedIn búsqueda** página de integración de aplicaciones, haga clic en **inicio de sesión único**.</span><span class="sxs-lookup"><span data-stu-id="e2901-151">In hello Azure portal, on hello **LinkedIn Lookup** application integration page, click **Single sign-on**.</span></span>

    ![Configurar inicio de sesión único][4]

2. <span data-ttu-id="e2901-153">En hello **inicio de sesión único** cuadro de diálogo, en **modo** seleccione **sesión basado en SAML** tooenable inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="e2901-153">On hello **Single sign-on** dialog, in **Mode** select **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurar inicio de sesión único](./media/active-directory-saas-LinkedInlookup-tutorial/tutorial_linkedInlookup_samlbase.png)

3. <span data-ttu-id="e2901-155">En una ventana del explorador web diferente, inicio de sesión tooyour **LinkedIn búsqueda** sitio Web como administrador.</span><span class="sxs-lookup"><span data-stu-id="e2901-155">In a different web browser window, sign-on tooyour **LinkedIn Lookup** website as an administrator.</span></span>

4. <span data-ttu-id="e2901-156">En **Account Center** (Centro de cuentas), haga clic en **Global Settings** (Configuración global) en **Settings** (Configuración).</span><span class="sxs-lookup"><span data-stu-id="e2901-156">In **Account Center**, click **Global Settings** under **Settings**.</span></span> <span data-ttu-id="e2901-157">Además, seleccione **búsqueda** de lista desplegable de Hola.</span><span class="sxs-lookup"><span data-stu-id="e2901-157">Also, select **Lookup** from hello dropdown list.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-LinkedInlookup-tutorial/tutorial_LinkedIn_admin_011.png)

5. <span data-ttu-id="e2901-159">Haga clic en **o haga clic aquí tooload y copie los campos individuales de formulario de hello** y copie **Id. de entidad** y **dirección Url de acceso de consumidor de aserción (ACS)**</span><span class="sxs-lookup"><span data-stu-id="e2901-159">Click **OR Click Here tooload and copy individual fields from hello form** and copy **Entity Id** and **Assertion Consumer Access (ACS) Url**</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-LinkedInlookup-tutorial/tutorial_LinkedIn_admin_032.png)

6. <span data-ttu-id="e2901-161">En el portal de Azure, en **LinkedIn búsqueda dominio y las direcciones URL** sección, lleve a cabo Hola siguientes pasos si desea tooconfigure aplicación de hello en **IDP** modo iniciado:</span><span class="sxs-lookup"><span data-stu-id="e2901-161">On Azure portal, under **LinkedIn Lookup Domain and URLs** section, perform hello following steps if you wish tooconfigure hello application in **IDP** initiated mode:</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-LinkedInlookup-tutorial/tutorial_linkedInlookup_url.png)

    <span data-ttu-id="e2901-163">a.</span><span class="sxs-lookup"><span data-stu-id="e2901-163">a.</span></span> <span data-ttu-id="e2901-164">Hola **identificador** cuadro de texto, escriba Hola **Id. de entidad** copiados desde el LinkedIn Portal</span><span class="sxs-lookup"><span data-stu-id="e2901-164">In hello **Identifier** textbox, enter hello **Entity ID** copied from LinkedIn Portal</span></span> 

    <span data-ttu-id="e2901-165">b.</span><span class="sxs-lookup"><span data-stu-id="e2901-165">b.</span></span> <span data-ttu-id="e2901-166">Hola **dirección URL de respuesta** cuadro de texto, escriba Hola **dirección Url de acceso de consumidor de aserción (ACS)** copiados desde el LinkedIn Portal</span><span class="sxs-lookup"><span data-stu-id="e2901-166">In hello **Reply URL** textbox, enter hello **Assertion Consumer Access (ACS) Url** copied from LinkedIn Portal</span></span>

7. <span data-ttu-id="e2901-167">Comprobar **mostrar avanzadas de configuración de direcciones URL**, si lo desea tooconfigure aplicación de hello en **SP** modo iniciado:</span><span class="sxs-lookup"><span data-stu-id="e2901-167">Check **Show advanced URL settings**, if you wish tooconfigure hello application in **SP** initiated mode:</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-LinkedInlookup-tutorial/tutorial_linkedInlookup_url1.png)

    <span data-ttu-id="e2901-169">Hola **dirección URL de inicio de sesión** cuadro de texto, escriba una dirección URL usando Hola siguiente patrón:`https://www.linkedIn.com/checkpoint/enterprise/login/<AccountId>?application=lookup`</span><span class="sxs-lookup"><span data-stu-id="e2901-169">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://www.linkedIn.com/checkpoint/enterprise/login/<AccountId>?application=lookup`</span></span>
     
    > [!NOTE] 
    > <span data-ttu-id="e2901-170">Este no es un valor real.</span><span class="sxs-lookup"><span data-stu-id="e2901-170">This is not real value.</span></span> <span data-ttu-id="e2901-171">usuario de Hello tiene tooupdate estos valores con hello dirección URL de inicio de sesión real.</span><span class="sxs-lookup"><span data-stu-id="e2901-171">hello user has tooupdate these values with hello actual Sign-On URL.</span></span> <span data-ttu-id="e2901-172">Póngase en contacto con [equipo de soporte técnico de cliente de LinkedIn búsqueda](https://business.LinkedIn.com/lookup) tooget este valor.</span><span class="sxs-lookup"><span data-stu-id="e2901-172">Contact [LinkedIn Lookup Client support team](https://business.LinkedIn.com/lookup) tooget this value.</span></span>

8. <span data-ttu-id="e2901-173">Su **LinkedIn búsqueda** aplicación espera las aserciones de SAML de hello en un formato concreto.</span><span class="sxs-lookup"><span data-stu-id="e2901-173">Your **LinkedIn Lookup** application expects hello SAML assertions in a specific format.</span></span> <span data-ttu-id="e2901-174">usuario de Hello tiene configuración de atributos de token de SAML de tooadd atributo personalizado asignaciones toohello.</span><span class="sxs-lookup"><span data-stu-id="e2901-174">hello user has tooadd custom attribute mappings toohello SAML token attributes configuration.</span></span> <span data-ttu-id="e2901-175">Hola siguiente captura de pantalla muestra un ejemplo.</span><span class="sxs-lookup"><span data-stu-id="e2901-175">hello following screenshot shows an example.</span></span> <span data-ttu-id="e2901-176">Hola valor predeterminado de **identificador de usuario** es **user.userprincipalname** pero LinkedIn búsqueda espera este toobe asignado con la dirección de correo electrónico del usuario de Hola.</span><span class="sxs-lookup"><span data-stu-id="e2901-176">hello default value of **User Identifier** is **user.userprincipalname** but LinkedIn Lookup expects this toobe mapped with hello user's email address.</span></span> <span data-ttu-id="e2901-177">Puede usar **user.mail** de atributo de la lista de Hola o usar el valor de atributo apropiado de hello según la configuración de la organización.</span><span class="sxs-lookup"><span data-stu-id="e2901-177">You can use **user.mail** attribute from hello list or use hello appropriate attribute value based on your organization configuration.</span></span> 

    ![Configurar inicio de sesión único](./media/active-directory-saas-LinkedInlookup-tutorial/updateusermail.png)
    
9. <span data-ttu-id="e2901-179">En **atributos de usuario** sección, haga clic en **ver y editar todos los demás atributos de usuario** y establezca los atributos de Hola.</span><span class="sxs-lookup"><span data-stu-id="e2901-179">In **User Attributes** section, click **View and edit all other user attributes** and set hello attributes.</span></span> <span data-ttu-id="e2901-180">usuario de Hello necesita cuatro notificaciones tooadd denominados **correo electrónico**, **departamento**, **firstname**, y **lastname** y valor de hello es toobe asignado con **user.mail**, **user.department**, **user.givenname**, y **user.surname** respectivamente</span><span class="sxs-lookup"><span data-stu-id="e2901-180">hello user needs tooadd four claims named **email**,  **department**, **firstname**, and **lastname** and hello value is toobe mapped with **user.mail**, **user.department**, **user.givenname**, and **user.surname** respectively</span></span>

    | <span data-ttu-id="e2901-181">Nombre del atributo</span><span class="sxs-lookup"><span data-stu-id="e2901-181">Attribute Name</span></span> | <span data-ttu-id="e2901-182">Valor de atributo</span><span class="sxs-lookup"><span data-stu-id="e2901-182">Attribute Value</span></span> |
    | --- | --- |
    | <span data-ttu-id="e2901-183">email</span><span class="sxs-lookup"><span data-stu-id="e2901-183">email</span></span>| <span data-ttu-id="e2901-184">user.mail</span><span class="sxs-lookup"><span data-stu-id="e2901-184">user.mail</span></span> |    
    | <span data-ttu-id="e2901-185">department</span><span class="sxs-lookup"><span data-stu-id="e2901-185">department</span></span>| <span data-ttu-id="e2901-186">user.department</span><span class="sxs-lookup"><span data-stu-id="e2901-186">user.department</span></span> |
    | <span data-ttu-id="e2901-187">firstname</span><span class="sxs-lookup"><span data-stu-id="e2901-187">firstname</span></span>| <span data-ttu-id="e2901-188">user.givenname</span><span class="sxs-lookup"><span data-stu-id="e2901-188">user.givenname</span></span> |
    | <span data-ttu-id="e2901-189">lastname</span><span class="sxs-lookup"><span data-stu-id="e2901-189">lastname</span></span>| <span data-ttu-id="e2901-190">user.surname</span><span class="sxs-lookup"><span data-stu-id="e2901-190">user.surname</span></span> |

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-LinkedInlookup-tutorial/userattribute.png)

    <span data-ttu-id="e2901-192">a.</span><span class="sxs-lookup"><span data-stu-id="e2901-192">a.</span></span> <span data-ttu-id="e2901-193">Haga clic en **Agregar atributo** tooopen hello **Agregar atributo** cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="e2901-193">Click **Add Attribute** tooopen hello **Add Attribute** dialog.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-LinkedInlookup-tutorial/4.png)
   
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-LinkedInlookup-tutorial/5.png)
   
    <span data-ttu-id="e2901-196">b.</span><span class="sxs-lookup"><span data-stu-id="e2901-196">b.</span></span> <span data-ttu-id="e2901-197">Hola **nombre** cuadro de texto, nombre de atributo de tipo hello se muestra para esa fila.</span><span class="sxs-lookup"><span data-stu-id="e2901-197">In hello **Name** textbox, type hello attribute name shown for that row.</span></span>
    
    <span data-ttu-id="e2901-198">c.</span><span class="sxs-lookup"><span data-stu-id="e2901-198">c.</span></span> <span data-ttu-id="e2901-199">De hello **valor** lista, el valor de atributo de tipo hello se muestra para esa fila.</span><span class="sxs-lookup"><span data-stu-id="e2901-199">From hello **Value** list, type hello attribute value shown for that row.</span></span>
    
    <span data-ttu-id="e2901-200">d.</span><span class="sxs-lookup"><span data-stu-id="e2901-200">d.</span></span> <span data-ttu-id="e2901-201">Haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="e2901-201">Click **Ok**</span></span>

10. <span data-ttu-id="e2901-202">Realizar Hola seguir pasos de hello **nombre** atributo:</span><span class="sxs-lookup"><span data-stu-id="e2901-202">Perform hello following steps on hello **name** attribute-</span></span>

    <span data-ttu-id="e2901-203">a.</span><span class="sxs-lookup"><span data-stu-id="e2901-203">a.</span></span> <span data-ttu-id="e2901-204">Haga clic en Hola de hello atributo tooopen **Editar atributo** ventana.</span><span class="sxs-lookup"><span data-stu-id="e2901-204">Click on hello attribute tooopen hello **Edit Attribute** window.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-LinkedInlookup-tutorial/url_update.png)

    <span data-ttu-id="e2901-206">b.</span><span class="sxs-lookup"><span data-stu-id="e2901-206">b.</span></span> <span data-ttu-id="e2901-207">Eliminar el valor de dirección URL de Hola de hello **espacio de nombres**.</span><span class="sxs-lookup"><span data-stu-id="e2901-207">Delete hello URL value from hello **namespace**.</span></span>
    
    <span data-ttu-id="e2901-208">c.</span><span class="sxs-lookup"><span data-stu-id="e2901-208">c.</span></span> <span data-ttu-id="e2901-209">Haga clic en **Aceptar** configuración de toosave Hola.</span><span class="sxs-lookup"><span data-stu-id="e2901-209">Click **Ok** toosave hello setting.</span></span>

10. <span data-ttu-id="e2901-210">En hello **el certificado de firma de SAML** sección, haga clic en **Metadata XML** y, a continuación, guarde el archivo XML de hello en el equipo.</span><span class="sxs-lookup"><span data-stu-id="e2901-210">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello XML file on your computer.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-LinkedInlookup-tutorial/tutorial_linkedInlookup_certificate.png) 

11. <span data-ttu-id="e2901-212">Haga clic en el botón **Guardar** .</span><span class="sxs-lookup"><span data-stu-id="e2901-212">Click **Save** button.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-LinkedInlookup-tutorial/tutorial_general_400.png)

12. <span data-ttu-id="e2901-214">Vaya demasiado**configuración de administración de LinkedIn** sección.</span><span class="sxs-lookup"><span data-stu-id="e2901-214">Go too**LinkedIn Admin Settings** section.</span></span> <span data-ttu-id="e2901-215">Archivo XML carga hello que descargó desde Hola portal de Azure, haga clic en hello **archivo cargar XML** opción.</span><span class="sxs-lookup"><span data-stu-id="e2901-215">Upload hello XML file you downloaded from hello Azure portal by clicking hello **Upload XML file** option.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-LinkedInlookup-tutorial/tutorial_linkedIn_metadata_03.png)

13. <span data-ttu-id="e2901-217">Haga clic en **en** tooenable SSO.</span><span class="sxs-lookup"><span data-stu-id="e2901-217">Click **On** tooenable SSO.</span></span> <span data-ttu-id="e2901-218">Estado SSO cambia de **no conectado** demasiado**conectado**</span><span class="sxs-lookup"><span data-stu-id="e2901-218">SSO status changes from **Not Connected** too**Connected**</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-LinkedInlookup-tutorial/tutorial_linkedIn_admin_05.png)

> [!TIP]
> <span data-ttu-id="e2901-220">Ahora puede leer una versión concisa de estas instrucciones dentro de hello [portal de Azure](https://portal.azure.com), mientras que está configurando la aplicación hello!</span><span class="sxs-lookup"><span data-stu-id="e2901-220">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="e2901-221">Después de agregar esta aplicación de hello **Active Directory > aplicaciones empresariales** sección, simplemente haga clic en hello **Single Sign-On** Hola de pestaña y acceso incrustado documentación a través de hello  **Configuración** sección final Hola.</span><span class="sxs-lookup"><span data-stu-id="e2901-221">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="e2901-222">Puede leer más acerca de características de documentación de embedded Hola aquí: [Azure AD incrustado documentación]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="e2901-222">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="e2901-223">Creación de un usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="e2901-223">Creating an Azure AD test user</span></span>
<span data-ttu-id="e2901-224">objetivo de Hola de esta sección es un usuario de prueba en hello Azure portal llamado a Britta Simon toocreate.</span><span class="sxs-lookup"><span data-stu-id="e2901-224">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Creación de un usuario de Azure AD][100]

<span data-ttu-id="e2901-226">**toocreate un usuario de prueba en Azure AD, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="e2901-226">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="e2901-227">Hola **portal de Azure**, en Hola panel de navegación izquierdo, haga clic en **Azure Active Directory** icono.</span><span class="sxs-lookup"><span data-stu-id="e2901-227">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-LinkedInlookup-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="e2901-229">Vaya demasiado**usuarios y grupos** y haga clic en **todos los usuarios**.</span><span class="sxs-lookup"><span data-stu-id="e2901-229">Go too**Users and groups** and click **All users**.</span></span>
    
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-LinkedInlookup-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="e2901-231">Haga clic en **agregar** tooopen hello **usuario** cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="e2901-231">Click **Add** tooopen hello **User** dialog.</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-LinkedInlookup-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="e2901-233">En hello **usuario** cuadro de diálogo, siga los pasos de hello:</span><span class="sxs-lookup"><span data-stu-id="e2901-233">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-LinkedInlookup-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="e2901-235">a.</span><span class="sxs-lookup"><span data-stu-id="e2901-235">a.</span></span> <span data-ttu-id="e2901-236">Hola **nombre** cuadro de texto, tipo **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="e2901-236">In hello **Name** textbox, type **Britta Simon**.</span></span>

    <span data-ttu-id="e2901-237">b.</span><span class="sxs-lookup"><span data-stu-id="e2901-237">b.</span></span> <span data-ttu-id="e2901-238">Hola **nombre de usuario** cuadro de texto, hello tipo **dirección de correo electrónico** de Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="e2901-238">In hello **User name** textbox, type hello **email address** of Britta Simon.</span></span>

    <span data-ttu-id="e2901-239">c.</span><span class="sxs-lookup"><span data-stu-id="e2901-239">c.</span></span> <span data-ttu-id="e2901-240">Seleccione **Mostrar contraseña** y anote el valor de Hola de hello **contraseña**.</span><span class="sxs-lookup"><span data-stu-id="e2901-240">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="e2901-241">d.</span><span class="sxs-lookup"><span data-stu-id="e2901-241">d.</span></span> <span data-ttu-id="e2901-242">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="e2901-242">Click **Create**.</span></span>
 
### <a name="creating-an-linkedin-lookup-test-user"></a><span data-ttu-id="e2901-243">Creación de un usuario de prueba de LinkedIn Lookup</span><span class="sxs-lookup"><span data-stu-id="e2901-243">Creating an LinkedIn Lookup test user</span></span>

<span data-ttu-id="e2901-244">Aplicación de búsqueda vinculado admite sólo de aprovisionamiento de usuarios de Time (JIT) y después de autenticar usuarios se crean automáticamente en la aplicación hello.</span><span class="sxs-lookup"><span data-stu-id="e2901-244">Linked Lookup Application supports Just in Time (JIT) user provisioning and after authentication users are created in hello application automatically.</span></span> <span data-ttu-id="e2901-245">Activar **automáticamente asignar licencias** tooassign un usuario de toohello de licencia.</span><span class="sxs-lookup"><span data-stu-id="e2901-245">Activate **Automatically assign licenses** tooassign a license toohello user.</span></span>
   
   ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-LinkedInlookup-tutorial/tutorial_linkedin_admin_license.png)

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="e2901-247">Asignación de usuario de prueba de hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="e2901-247">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="e2901-248">En esta sección, se habilita Britta Simon toouse un inicio de sesión único Azure concediendo acceso tooLinkedIn búsqueda.</span><span class="sxs-lookup"><span data-stu-id="e2901-248">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooLinkedIn Lookup.</span></span>

![Asignar usuario][200] 

<span data-ttu-id="e2901-250">**tooassign Britta Simon tooLinkedIn búsqueda, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="e2901-250">**tooassign Britta Simon tooLinkedIn Lookup, perform hello following steps:**</span></span>

1. <span data-ttu-id="e2901-251">Hola portal de Azure, abra la vista de aplicaciones de hello y, a continuación, navegue a vista de directorio toohello y vaya demasiado**aplicaciones empresariales** , a continuación, haga clic en **todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="e2901-251">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Asignar usuario][201] 

2. <span data-ttu-id="e2901-253">En la lista de aplicaciones de hello, seleccione **LinkedIn búsqueda**.</span><span class="sxs-lookup"><span data-stu-id="e2901-253">In hello applications list, select **LinkedIn Lookup**.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-LinkedInlookup-tutorial/tutorial_linkedInlookup_app.png) 

3. <span data-ttu-id="e2901-255">En el menú de Hola Hola izquierda, haga clic en **usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="e2901-255">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Asignar usuario][202] 

4. <span data-ttu-id="e2901-257">Haga clic en el botón **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="e2901-257">Click **Add** button.</span></span> <span data-ttu-id="e2901-258">Después, seleccione **Usuarios y grupos** en el cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="e2901-258">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Asignar usuario][203]

5. <span data-ttu-id="e2901-260">En **usuarios y grupos** cuadro de diálogo, seleccione **Britta Simon** en la lista de usuarios de Hola.</span><span class="sxs-lookup"><span data-stu-id="e2901-260">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="e2901-261">Haga clic en el botón **Seleccionar** del cuadro de diálogo **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="e2901-261">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="e2901-262">Haga clic en el botón **Asignar** del cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="e2901-262">Click **Assign** button on **Add Assignment** dialog.</span></span>

    
### <a name="testing-single-sign-on"></a><span data-ttu-id="e2901-263">Prueba del inicio de sesión único </span><span class="sxs-lookup"><span data-stu-id="e2901-263">Testing single sign-on</span></span>

<span data-ttu-id="e2901-264">En esta sección, comprobará su único inicio de sesión en configuración de Azure AD con hello Panel de acceso.</span><span class="sxs-lookup"><span data-stu-id="e2901-264">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="e2901-265">Al hacer clic en hello LinkedIn búsqueda disponer en mosaico en hello Panel de acceso, debe ser página redirigidos tooOrganizational donde haya tooprovide detalles de su cuenta personales de LinkedIn.</span><span class="sxs-lookup"><span data-stu-id="e2901-265">When you click hello LinkedIn Lookup tile in hello Access Panel, you should be redirected tooOrganizational page where you have tooprovide your personal LinkedIn account details.</span></span> <span data-ttu-id="e2901-266">Esta página vincula su cuenta personal con su cuenta empresarial de LinkedIn.</span><span class="sxs-lookup"><span data-stu-id="e2901-266">It links your personal account with your LinkedIn business account.</span></span> 

<span data-ttu-id="e2901-267">Para más información sobre el Panel de acceso, consulte [Introducción al Panel de acceso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="e2901-267">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="e2901-268">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="e2901-268">Additional resources</span></span>

* [<span data-ttu-id="e2901-269">Lista de tutoriales sobre cómo tooIntegrate aplicaciones de SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="e2901-269">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="e2901-270">¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="e2901-270">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-LinkedInlookup-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-LinkedInlookup-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-LinkedInlookup-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-LinkedInlookup-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-LinkedInlookup-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-LinkedInlookup-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-LinkedInlookup-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-LinkedInlookup-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-LinkedInlookup-tutorial/tutorial_general_203.png

