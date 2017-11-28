---
title: "Tutorial: Integración de Azure Active Directory con LinkedIn Sales Navigator | Microsoft Docs"
description: "Obtenga información acerca de cómo tooconfigure inicio de sesión único entre Azure Active Directory y LinkedInSalesNavigator."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 7a9fa8f3-d611-4ffe-8d50-04e9586b24da
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/14/2017
ms.author: jeedes
ms.openlocfilehash: 443d302d40d7af16aba5114e00963f23ea8d12d6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-linkedin-sales-navigator"></a><span data-ttu-id="1120d-103">Tutorial: Integración de Azure Active Directory con LinkedIn Sales Navigator</span><span class="sxs-lookup"><span data-stu-id="1120d-103">Tutorial: Azure Active Directory integration with LinkedIn Sales Navigator</span></span>

<span data-ttu-id="1120d-104">En este tutorial, aprenderá cómo toointegrate navegador de ventas de LinkedIn con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="1120d-104">In this tutorial, you learn how toointegrate LinkedIn Sales Navigator with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="1120d-105">Integración de navegador de ventas de LinkedIn con Azure AD proporciona Hola siguientes ventajas:</span><span class="sxs-lookup"><span data-stu-id="1120d-105">Integrating LinkedIn Sales Navigator with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="1120d-106">Puede controlar en Azure AD que tenga acceso tooLinkedIn navegador de ventas</span><span class="sxs-lookup"><span data-stu-id="1120d-106">You can control in Azure AD who has access tooLinkedIn Sales Navigator</span></span>
- <span data-ttu-id="1120d-107">Puede habilitar los usuarios tooautomatically get ha iniciado sesión tooLinkedIn navegador de ventas (Single Sign-On) con sus cuentas de Azure AD</span><span class="sxs-lookup"><span data-stu-id="1120d-107">You can enable your users tooautomatically get signed-on tooLinkedIn Sales Navigator (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="1120d-108">Puede administrar las cuentas en una ubicación central: Hola portal de Azure</span><span class="sxs-lookup"><span data-stu-id="1120d-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="1120d-109">Si desea obtener más información acerca de la integración de aplicaciones de SaaS con Azure AD tooknow, examinar [¿qué es acceso a la aplicación y el inicio de sesión único con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="1120d-109">If you want tooknow more details about SaaS app integration with Azure AD, browse [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="1120d-110">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="1120d-110">Prerequisites</span></span>

<span data-ttu-id="1120d-111">tooconfigure integración de Azure AD con navegador de ventas de LinkedIn, necesita Hola siguientes elementos:</span><span class="sxs-lookup"><span data-stu-id="1120d-111">tooconfigure Azure AD integration with LinkedIn Sales Navigator, you need hello following items:</span></span>

- <span data-ttu-id="1120d-112">Una suscripción de Azure AD</span><span class="sxs-lookup"><span data-stu-id="1120d-112">An Azure AD subscription</span></span>
- <span data-ttu-id="1120d-113">Una suscripción habilitada para el inicio de sesión único en LinkedIn Sales Navigator</span><span class="sxs-lookup"><span data-stu-id="1120d-113">A LinkedIn Sales Navigator single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="1120d-114">Hola tootest los pasos de este tutorial, no se recomienda usar un entorno de producción.</span><span class="sxs-lookup"><span data-stu-id="1120d-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="1120d-115">pasos de hello tootest en este tutorial, debe seguir estas recomendaciones:</span><span class="sxs-lookup"><span data-stu-id="1120d-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="1120d-116">No use el entorno de producción, salvo que sea necesario.</span><span class="sxs-lookup"><span data-stu-id="1120d-116">Avoid using your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="1120d-117">Si no dispone de un entorno de prueba de Azure AD, puede obtener una versión de prueba de un mes [aquí](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="1120d-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="1120d-118">Descripción del escenario</span><span class="sxs-lookup"><span data-stu-id="1120d-118">Scenario description</span></span>
<span data-ttu-id="1120d-119">En este tutorial, puede probar el inicio de sesión único de Azure AD en un entorno de prueba.</span><span class="sxs-lookup"><span data-stu-id="1120d-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="1120d-120">escenario de Hello descrito en este tutorial consta de dos bloques principales:</span><span class="sxs-lookup"><span data-stu-id="1120d-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="1120d-121">Agregar LinkedIn ventas navegador de galería de Hola</span><span class="sxs-lookup"><span data-stu-id="1120d-121">Adding LinkedIn Sales Navigator from hello gallery</span></span>
2. <span data-ttu-id="1120d-122">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="1120d-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-linkedin-sales-navigator-from-hello-gallery"></a><span data-ttu-id="1120d-123">Agregar LinkedIn ventas navegador de galería de Hola</span><span class="sxs-lookup"><span data-stu-id="1120d-123">Adding LinkedIn Sales Navigator from hello gallery</span></span>
<span data-ttu-id="1120d-124">integración de hello tooconfigure de navegador de ventas de LinkedIn en Azure AD, deberá tooadd LinkedIn ventas navegador de lista de tooyour Hola Galería de aplicaciones administradas de SaaS.</span><span class="sxs-lookup"><span data-stu-id="1120d-124">tooconfigure hello integration of LinkedIn Sales Navigator into Azure AD, you need tooadd LinkedIn Sales Navigator from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="1120d-125">**tooadd LinkedIn ventas navegador de galería de hello, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="1120d-125">**tooadd LinkedIn Sales Navigator from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="1120d-126">Hola  **[portal de Azure](https://portal.azure.com)**, en el panel de navegación izquierdo de Hola, haga clic en **Azure Active Directory** icono.</span><span class="sxs-lookup"><span data-stu-id="1120d-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="1120d-128">Navegue demasiado**aplicaciones empresariales**.</span><span class="sxs-lookup"><span data-stu-id="1120d-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="1120d-129">A continuación, vaya demasiado**todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="1120d-129">Then go too**All applications**.</span></span>

    ![Aplicaciones][2]
    
3. <span data-ttu-id="1120d-131">Haga clic en **nueva aplicación** botón en la parte superior de saludo del cuadro de diálogo de Hola.</span><span class="sxs-lookup"><span data-stu-id="1120d-131">Click **New application** button on hello top of hello dialog.</span></span>

    ![Aplicaciones][3]

4. <span data-ttu-id="1120d-133">En el cuadro de búsqueda de hello, escriba **LinkedIn ventas navegador**.</span><span class="sxs-lookup"><span data-stu-id="1120d-133">In hello search box, type **LinkedIn Sales Navigator**.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-linkedinsalesnavigator-tutorial/tutorial_linkedinsalesnavigator_search.png)

5. <span data-ttu-id="1120d-135">En el panel de resultados de hello, seleccione **LinkedIn ventas navegador**y, a continuación, haga clic en **agregar** botón aplicación hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="1120d-135">In hello results panel, select **LinkedIn Sales Navigator**, and then click **Add** button tooadd hello application.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-linkedinsalesnavigator-tutorial/tutorial_linkedinsalesnavigator_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="1120d-137">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="1120d-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="1120d-138">En esta sección, configurará y probará el inicio de sesión único de Azure AD con LinkedIn Sales Navigator con un usuario de prueba llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="1120d-138">In this section, you configure and test Azure AD single sign-on with LinkedIn Sales Navigator based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="1120d-139">Para toowork de inicio de sesión único, Azure AD necesita tooknow qué usuario equivalente de hello en el navegador de ventas de LinkedIn es tooa usuario en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="1120d-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in LinkedIn Sales Navigator is tooa user in Azure AD.</span></span> <span data-ttu-id="1120d-140">En otras palabras, una relación de vínculo entre un usuario de Azure AD y el usuario relacionado de hello en el navegador de ventas de LinkedIn debe toobe establecido.</span><span class="sxs-lookup"><span data-stu-id="1120d-140">In other words, a link relationship between an Azure AD user and hello related user in LinkedIn Sales Navigator needs toobe established.</span></span>

<span data-ttu-id="1120d-141">Esta relación de vínculo se establece mediante la asignación de valor de Hola de hello **nombre de usuario** en Azure AD como valor de Hola de hello **nombre de usuario** en el navegador de ventas de LinkedIn.</span><span class="sxs-lookup"><span data-stu-id="1120d-141">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in LinkedIn Sales Navigator.</span></span>

<span data-ttu-id="1120d-142">tooconfigure y prueba de inicio de sesión único en Azure AD con navegador de ventas de LinkedIn, deberá hello toocomplete después de bloques de creación:</span><span class="sxs-lookup"><span data-stu-id="1120d-142">tooconfigure and test Azure AD single sign-on with LinkedIn Sales Navigator, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="1120d-143">**[Configuración de Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable la toouse usuarios esta característica.</span><span class="sxs-lookup"><span data-stu-id="1120d-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="1120d-144">**[Crear un usuario de prueba de Azure AD](#creating-an-azure-ad-test-user)**  -inicio de sesión único en Azure AD tootest con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="1120d-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="1120d-145">**[Crear un usuario de prueba de navegador de ventas de LinkedIn](#creating-a-linkedin-sales-navigator-test-user)**  -toohave un equivalente de Britta Simon en el navegador de ventas de LinkedIn es representación toohello vinculado Azure AD del usuario de Hola.</span><span class="sxs-lookup"><span data-stu-id="1120d-145">**[Creating a LinkedIn Sales Navigator test user](#creating-a-linkedin-sales-navigator-test-user)** - toohave a counterpart of Britta Simon in LinkedIn Sales Navigator that is linked toohello Azure AD representation of hello user.</span></span>
4. <span data-ttu-id="1120d-146">**[Asignar usuario de prueba de hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="1120d-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="1120d-147">**[Pruebas de Single Sign-On](#testing-single-sign-on)**  -tooverify Hola si funciona la configuración.</span><span class="sxs-lookup"><span data-stu-id="1120d-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="1120d-148">Configuración del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="1120d-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="1120d-149">En esta sección, habilitar inicio de sesión único en Azure AD en hello portal de Azure y configurar el inicio de sesión único en la aplicación de navegador de ventas de LinkedIn.</span><span class="sxs-lookup"><span data-stu-id="1120d-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your LinkedIn Sales Navigator application.</span></span>

<span data-ttu-id="1120d-150">**tooconfigure inicio de sesión único en Azure AD con navegador de ventas de LinkedIn, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="1120d-150">**tooconfigure Azure AD single sign-on with LinkedIn Sales Navigator, perform hello following steps:**</span></span>

1. <span data-ttu-id="1120d-151">En el portal de Azure, en Hola Hola **LinkedIn ventas navegador** página de integración de aplicaciones, haga clic en **inicio de sesión único**.</span><span class="sxs-lookup"><span data-stu-id="1120d-151">In hello Azure portal, on hello **LinkedIn Sales Navigator** application integration page, click **Single sign-on**.</span></span>

    ![Configurar inicio de sesión único][4]

2. <span data-ttu-id="1120d-153">En hello **inicio de sesión único** cuadro de diálogo, en **modo** seleccione **sesión basado en SAML** tooenable inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="1120d-153">On hello **Single sign-on** dialog, in **Mode** select **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurar inicio de sesión único](./media/active-directory-saas-linkedinsalesnavigator-tutorial/tutorial_linkedinsalesnavigator_samlbase.png)

3. <span data-ttu-id="1120d-155">En una ventana del explorador web diferente, inicio de sesión tooyour **LinkedIn ventas navegador** sitio Web como administrador.</span><span class="sxs-lookup"><span data-stu-id="1120d-155">In a different web browser window, sign-on tooyour **LinkedIn Sales Navigator** website as an administrator.</span></span>

4. <span data-ttu-id="1120d-156">En **Account Center** (Centro de cuentas), haga clic en **Global Settings** (Configuración global) en **Settings** (Configuración).</span><span class="sxs-lookup"><span data-stu-id="1120d-156">In **Account Center**, click **Global Settings** under **Settings**.</span></span> <span data-ttu-id="1120d-157">Además, seleccione **ventas navegador** en lista de desplegable Hola.</span><span class="sxs-lookup"><span data-stu-id="1120d-157">Also, select **Sales Navigator** from hello dropdown list.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-linkedinsalesnavigator-tutorial/tutorial_linkedin_admin_01.png)

5. <span data-ttu-id="1120d-159">Haga clic en **o haga clic aquí tooload y copie los campos individuales de formulario de hello** y copie **Id. de entidad** y **dirección Url de acceso de consumidor de aserción (ACS)**.</span><span class="sxs-lookup"><span data-stu-id="1120d-159">Click **OR Click Here tooload and copy individual fields from hello form** and copy **Entity Id** and **Assertion Consumer Access (ACS) Url**.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-linkedinsalesnavigator-tutorial/tutorial_linkedin_admin_031.png)

6. <span data-ttu-id="1120d-161">En el portal de Azure, en **LinkedIn ventas navegador del dominio y las direcciones URL** sección, lleve a cabo Hola siguientes pasos si desea tooconfigure aplicación de hello en **IDP** modo iniciado.</span><span class="sxs-lookup"><span data-stu-id="1120d-161">On Azure portal, under **LinkedIn Sales Navigator Domain and URLs** section, perform hello following steps if you wish tooconfigure hello application in **IDP** initiated mode.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-linkedinsalesnavigator-tutorial/tutorial_linkedinsalesnavigator_url1.png)

    <span data-ttu-id="1120d-163">a.</span><span class="sxs-lookup"><span data-stu-id="1120d-163">a.</span></span> <span data-ttu-id="1120d-164">Hola **identificador** cuadro de texto, escriba Hola **Id. de entidad** copiados desde el LinkedIn Portal</span><span class="sxs-lookup"><span data-stu-id="1120d-164">In hello **Identifier** textbox, enter hello **Entity ID** copied from LinkedIn Portal</span></span> 

    <span data-ttu-id="1120d-165">b.</span><span class="sxs-lookup"><span data-stu-id="1120d-165">b.</span></span> <span data-ttu-id="1120d-166">Hola **dirección URL de respuesta** cuadro de texto, escriba Hola **dirección Url de acceso de consumidor de aserción (ACS)** copiados desde el LinkedIn Portal</span><span class="sxs-lookup"><span data-stu-id="1120d-166">In hello **Reply URL** textbox, enter hello **Assertion Consumer Access (ACS) Url** copied from LinkedIn Portal</span></span>

7. <span data-ttu-id="1120d-167">Comprobar **mostrar avanzadas de configuración de direcciones URL**, si lo desea tooconfigure aplicación de hello en **SP** modo iniciado.</span><span class="sxs-lookup"><span data-stu-id="1120d-167">Check **Show advanced URL settings**, if you wish tooconfigure hello application in **SP** initiated mode.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-linkedinsalesnavigator-tutorial/tutorial_linkedinsalesnavigator_url2.png)

    <span data-ttu-id="1120d-169">Hola **dirección URL de inicio de sesión** cuadro de texto, valor de tipo hello mediante Hola sigue el patrón:`https://www.linkedin.com/checkpoint/enterprise/login/<account id>?application=salesNavigator`</span><span class="sxs-lookup"><span data-stu-id="1120d-169">In hello **Sign-on URL** textbox, type hello value using hello following pattern: `https://www.linkedin.com/checkpoint/enterprise/login/<account id>?application=salesNavigator`</span></span>

8. <span data-ttu-id="1120d-170">Su **LinkedIn ventas navegador** aplicación espera las aserciones de SAML de hello en un formato específico, lo que requiere la configuración de atributos de token de SAML de tooadd atributo personalizado asignaciones tooyour.</span><span class="sxs-lookup"><span data-stu-id="1120d-170">Your **LinkedIn Sales Navigator** application expects hello SAML assertions in a specific format, which requires you tooadd custom attribute mappings tooyour SAML token attributes configuration.</span></span> <span data-ttu-id="1120d-171">Hola siguiente captura de pantalla muestra un ejemplo.</span><span class="sxs-lookup"><span data-stu-id="1120d-171">hello following screenshot shows an example.</span></span> <span data-ttu-id="1120d-172">Hola valor predeterminado de **identificador de usuario** es **user.userprincipalname** pero LinkedIn ventas navegador así lo espere toobe asignado con la dirección de correo electrónico del usuario de Hola.</span><span class="sxs-lookup"><span data-stu-id="1120d-172">hello default value of **User Identifier** is **user.userprincipalname** but LinkedIn Sales Navigator expects it toobe mapped with hello user's email address.</span></span> <span data-ttu-id="1120d-173">Puede usar **user.mail** de atributo de la lista de Hola o usar el valor de atributo apropiado de hello según la configuración de la organización.</span><span class="sxs-lookup"><span data-stu-id="1120d-173">You can use **user.mail** attribute from hello list or use hello appropriate attribute value based on your organization configuration.</span></span> 

    ![Configurar inicio de sesión único](./media/active-directory-saas-linkedinsalesnavigator-tutorial/updateusermail.png)
    
9. <span data-ttu-id="1120d-175">En **atributos de usuario** sección, haga clic en **ver y editar todos los demás atributos de usuario** y establezca los atributos de Hola.</span><span class="sxs-lookup"><span data-stu-id="1120d-175">In **User Attributes** section, click **View and edit all other user attributes** and set hello attributes.</span></span> <span data-ttu-id="1120d-176">usuario de Hello necesita cuatro notificaciones tooadd denominados **correo electrónico**, **departamento**, **firstname**, y **lastname** y valor de hello es toobe asignado con **user.mail**, **user.department**, **user.givenname**, y **user.surname** respectivamente</span><span class="sxs-lookup"><span data-stu-id="1120d-176">hello user needs tooadd four claims named **email**, **department**, **firstname**, and **lastname** and hello value is toobe mapped with **user.mail**, **user.department**, **user.givenname**, and **user.surname** respectively</span></span>

    | <span data-ttu-id="1120d-177">Nombre del atributo</span><span class="sxs-lookup"><span data-stu-id="1120d-177">Attribute Name</span></span> | <span data-ttu-id="1120d-178">Valor de atributo</span><span class="sxs-lookup"><span data-stu-id="1120d-178">Attribute Value</span></span> |
    | --- | --- |    
    | <span data-ttu-id="1120d-179">email</span><span class="sxs-lookup"><span data-stu-id="1120d-179">email</span></span>| <span data-ttu-id="1120d-180">user.mail</span><span class="sxs-lookup"><span data-stu-id="1120d-180">user.mail</span></span> |
    | <span data-ttu-id="1120d-181">department</span><span class="sxs-lookup"><span data-stu-id="1120d-181">department</span></span>| <span data-ttu-id="1120d-182">user.department</span><span class="sxs-lookup"><span data-stu-id="1120d-182">user.department</span></span> |
    | <span data-ttu-id="1120d-183">firstname</span><span class="sxs-lookup"><span data-stu-id="1120d-183">firstname</span></span>| <span data-ttu-id="1120d-184">user.givenname</span><span class="sxs-lookup"><span data-stu-id="1120d-184">user.givenname</span></span> |
    | <span data-ttu-id="1120d-185">lastname</span><span class="sxs-lookup"><span data-stu-id="1120d-185">lastname</span></span>| <span data-ttu-id="1120d-186">user.surname</span><span class="sxs-lookup"><span data-stu-id="1120d-186">user.surname</span></span> |
    
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-linkedinsalesnavigator-tutorial/userattribute.png)
    
    <span data-ttu-id="1120d-188">a.</span><span class="sxs-lookup"><span data-stu-id="1120d-188">a.</span></span> <span data-ttu-id="1120d-189">Haga clic en **Agregar atributo** el cuadro de diálogo de tooopen Hola atributo.</span><span class="sxs-lookup"><span data-stu-id="1120d-189">Click on **Add Attribute** tooopen hello attribute dialog.</span></span>
    
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-linkedinsalesnavigator-tutorial/tutorial_attribute_04.png)
    
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-linkedinsalesnavigator-tutorial/tutorial_attribute_05.png)
   
    <span data-ttu-id="1120d-192">b.</span><span class="sxs-lookup"><span data-stu-id="1120d-192">b.</span></span> <span data-ttu-id="1120d-193">Hola **nombre** cuadro de texto, nombre de atributo de tipo hello se muestra para esa fila.</span><span class="sxs-lookup"><span data-stu-id="1120d-193">In hello **Name** textbox, type hello attribute name shown for that row.</span></span>
    
    <span data-ttu-id="1120d-194">c.</span><span class="sxs-lookup"><span data-stu-id="1120d-194">c.</span></span> <span data-ttu-id="1120d-195">De hello **valor** lista, el valor de atributo de tipo hello se muestra para esa fila.</span><span class="sxs-lookup"><span data-stu-id="1120d-195">From hello **Value** list, type hello attribute value shown for that row.</span></span>
    
    <span data-ttu-id="1120d-196">d.</span><span class="sxs-lookup"><span data-stu-id="1120d-196">d.</span></span> <span data-ttu-id="1120d-197">Haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="1120d-197">Click **Ok**</span></span>

10. <span data-ttu-id="1120d-198">Realizar Hola seguir pasos de hello **nombre** atributo:</span><span class="sxs-lookup"><span data-stu-id="1120d-198">Perform hello following steps on hello **name** attribute-</span></span>

    <span data-ttu-id="1120d-199">a.</span><span class="sxs-lookup"><span data-stu-id="1120d-199">a.</span></span> <span data-ttu-id="1120d-200">Haga clic en Hola de hello atributo tooopen **Editar atributo** ventana.</span><span class="sxs-lookup"><span data-stu-id="1120d-200">Click on hello attribute tooopen hello **Edit Attribute** window.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-linkedinsalesnavigator-tutorial/url_update.png)

    <span data-ttu-id="1120d-202">b.</span><span class="sxs-lookup"><span data-stu-id="1120d-202">b.</span></span> <span data-ttu-id="1120d-203">Eliminar el valor de dirección URL de Hola de hello **espacio de nombres**.</span><span class="sxs-lookup"><span data-stu-id="1120d-203">Delete hello URL value from hello **namespace**.</span></span>
    
    <span data-ttu-id="1120d-204">c.</span><span class="sxs-lookup"><span data-stu-id="1120d-204">c.</span></span> <span data-ttu-id="1120d-205">Haga clic en **Aceptar** configuración de toosave Hola.</span><span class="sxs-lookup"><span data-stu-id="1120d-205">Click **Ok** toosave hello setting.</span></span>

11. <span data-ttu-id="1120d-206">En hello **el certificado de firma de SAML** sección, haga clic en **Metadata XML** y, a continuación, guarde el archivo XML de hello en el equipo.</span><span class="sxs-lookup"><span data-stu-id="1120d-206">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello XML file on your computer.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-linkedinsalesnavigator-tutorial/tutorial_linkedinsalesnavigator_certificate.png) 

12. <span data-ttu-id="1120d-208">Haga clic en el botón **Guardar** .</span><span class="sxs-lookup"><span data-stu-id="1120d-208">Click **Save** button.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-linkedinsalesnavigator-tutorial/tutorial_general_400.png)

13. <span data-ttu-id="1120d-210">Vaya demasiado**configuración de administración de LinkedIn** sección.</span><span class="sxs-lookup"><span data-stu-id="1120d-210">Go too**LinkedIn Admin Settings** section.</span></span> <span data-ttu-id="1120d-211">Haga clic en **archivo cargar XML** hello tooupload archivo Metadata XML que ha descargado desde Hola portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="1120d-211">Click **Upload XML file** tooupload hello Metadata XML file that you have downloaded from hello Azure portal.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-linkedinsalesnavigator-tutorial/tutorial_linkedin_metadata_03.png)

14. <span data-ttu-id="1120d-213">Haga clic en **en** tooenable SSO.</span><span class="sxs-lookup"><span data-stu-id="1120d-213">Click **On** tooenable SSO.</span></span> <span data-ttu-id="1120d-214">Estado SSO cambia de **no conectado** demasiado**conectado**</span><span class="sxs-lookup"><span data-stu-id="1120d-214">SSO status changes from **Not Connected** too**Connected**</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-linkedinsalesnavigator-tutorial/tutorial_linkedin_admin_05.png)


> [!TIP]
> <span data-ttu-id="1120d-216">Ahora puede leer una versión concisa de estas instrucciones dentro de hello [portal de Azure](https://portal.azure.com), mientras que está configurando la aplicación hello!</span><span class="sxs-lookup"><span data-stu-id="1120d-216">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="1120d-217">Después de agregar esta aplicación de hello **Active Directory > aplicaciones empresariales** sección, simplemente haga clic en hello **Single Sign-On** Hola de pestaña y acceso incrustado documentación a través de hello  **Configuración** sección final Hola.</span><span class="sxs-lookup"><span data-stu-id="1120d-217">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="1120d-218">Puede leer más acerca de características de documentación de embedded Hola aquí: [Azure AD incrustado documentación]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="1120d-218">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="1120d-219">Creación de un usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="1120d-219">Creating an Azure AD test user</span></span>
<span data-ttu-id="1120d-220">objetivo de Hola de esta sección es un usuario de prueba en hello Azure portal llamado a Britta Simon toocreate.</span><span class="sxs-lookup"><span data-stu-id="1120d-220">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Creación de un usuario de Azure AD][100]

<span data-ttu-id="1120d-222">**toocreate un usuario de prueba en Azure AD, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="1120d-222">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="1120d-223">Hola **portal de Azure**, en Hola panel de navegación izquierdo, haga clic en **Azure Active Directory** icono.</span><span class="sxs-lookup"><span data-stu-id="1120d-223">In hello **Azure  portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-linkedinsalesnavigator-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="1120d-225">Vaya demasiado**usuarios y grupos** y haga clic en **todos los usuarios**.</span><span class="sxs-lookup"><span data-stu-id="1120d-225">Go too**Users and groups** and click **All users**.</span></span>
    
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-linkedinsalesnavigator-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="1120d-227">En la parte superior de saludo del cuadro de diálogo de hello haga clic en **agregar** tooopen hello **usuario** cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="1120d-227">At hello top of hello dialog click **Add** tooopen hello **User** dialog.</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-linkedinsalesnavigator-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="1120d-229">En hello **usuario** cuadro de diálogo, siga los pasos de hello:</span><span class="sxs-lookup"><span data-stu-id="1120d-229">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-linkedinsalesnavigator-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="1120d-231">a.</span><span class="sxs-lookup"><span data-stu-id="1120d-231">a.</span></span> <span data-ttu-id="1120d-232">Hola **nombre** cuadro de texto, tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="1120d-232">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="1120d-233">b.</span><span class="sxs-lookup"><span data-stu-id="1120d-233">b.</span></span> <span data-ttu-id="1120d-234">Hola **nombre de usuario** cuadro de texto, hello tipo **dirección de correo electrónico** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="1120d-234">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="1120d-235">c.</span><span class="sxs-lookup"><span data-stu-id="1120d-235">c.</span></span> <span data-ttu-id="1120d-236">Seleccione **Mostrar contraseña** y anote el valor de Hola de hello **contraseña**.</span><span class="sxs-lookup"><span data-stu-id="1120d-236">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="1120d-237">d.</span><span class="sxs-lookup"><span data-stu-id="1120d-237">d.</span></span> <span data-ttu-id="1120d-238">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="1120d-238">Click **Create**.</span></span>
 
### <a name="creating-a-linkedin-sales-navigator-test-user"></a><span data-ttu-id="1120d-239">Creación de un usuario de prueba de LinkedIn Sales Navigator</span><span class="sxs-lookup"><span data-stu-id="1120d-239">Creating a LinkedIn Sales Navigator test user</span></span>

<span data-ttu-id="1120d-240">Aplicación de navegador de ventas vinculado admite sólo de aprovisionamiento de usuarios de Time (JIT) y después de autenticar usuarios se crean automáticamente en la aplicación hello.</span><span class="sxs-lookup"><span data-stu-id="1120d-240">Linked Sales Navigator Application supports Just in Time (JIT) user provisioning and after authentication users are created in hello application automatically.</span></span> <span data-ttu-id="1120d-241">Activar **automáticamente asignar licencias** tooassign un usuario de toohello de licencia.</span><span class="sxs-lookup"><span data-stu-id="1120d-241">Activate **Automatically assign licenses** tooassign a license toohello user.</span></span>
   
   ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-linkedinsalesnavigator-tutorial/LinkedinUserprovswitch.png)

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="1120d-243">Asignación de usuario de prueba de hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="1120d-243">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="1120d-244">En esta sección, se habilita Britta Simon toouse un inicio de sesión único Azure concediendo acceso tooLinkedIn navegador de ventas.</span><span class="sxs-lookup"><span data-stu-id="1120d-244">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooLinkedIn Sales Navigator.</span></span>

![Asignar usuario][200] 

<span data-ttu-id="1120d-246">**tooassign Britta Simon tooLinkedIn navegador de ventas, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="1120d-246">**tooassign Britta Simon tooLinkedIn Sales Navigator, perform hello following steps:**</span></span>

1. <span data-ttu-id="1120d-247">Hola portal de Azure, abra la vista de aplicaciones de hello y, a continuación, navegue a vista de directorio toohello y vaya demasiado**aplicaciones empresariales** , a continuación, haga clic en **todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="1120d-247">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Asignar usuario][201] 

2. <span data-ttu-id="1120d-249">En la lista de aplicaciones de hello, seleccione **LinkedIn ventas navegador**.</span><span class="sxs-lookup"><span data-stu-id="1120d-249">In hello applications list, select **LinkedIn Sales Navigator**.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-linkedinsalesnavigator-tutorial/tutorial_linkedinsalesnavigator_app.png) 

3. <span data-ttu-id="1120d-251">En el menú de Hola Hola izquierda, haga clic en **usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="1120d-251">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Asignar usuario][202] 

4. <span data-ttu-id="1120d-253">Haga clic en el botón **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="1120d-253">Click **Add** button.</span></span> <span data-ttu-id="1120d-254">Después, seleccione **Usuarios y grupos** en el cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="1120d-254">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Asignar usuario][203]

5. <span data-ttu-id="1120d-256">En **usuarios y grupos** cuadro de diálogo, seleccione **Britta Simon** en la lista de usuarios de Hola.</span><span class="sxs-lookup"><span data-stu-id="1120d-256">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="1120d-257">Haga clic en el botón **Seleccionar** del cuadro de diálogo **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="1120d-257">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="1120d-258">Haga clic en el botón **Asignar** del cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="1120d-258">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="1120d-259">Prueba del inicio de sesión único </span><span class="sxs-lookup"><span data-stu-id="1120d-259">Testing single sign-on</span></span>

<span data-ttu-id="1120d-260">En esta sección, comprobará su único inicio de sesión en configuración de Azure AD con hello Panel de acceso.</span><span class="sxs-lookup"><span data-stu-id="1120d-260">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="1120d-261">Al hacer clic en icono de navegador de ventas de LinkedIn Hola Hola Panel de acceso, debe ser página redirigidos tooOrganizational donde haya tooprovide detalles de su cuenta personales de LinkedIn.</span><span class="sxs-lookup"><span data-stu-id="1120d-261">When you click hello LinkedIn Sales Navigator tile in hello Access Panel, you should be redirected tooOrganizational page where you have tooprovide your personal LinkedIn account details.</span></span> <span data-ttu-id="1120d-262">Esta página vincula su cuenta personal con su cuenta empresarial de LinkedIn.</span><span class="sxs-lookup"><span data-stu-id="1120d-262">It links your personal account with your LinkedIn business account.</span></span> <span data-ttu-id="1120d-263">Para obtener más información acerca de hello Panel de acceso, consulte [Introducción al Panel de acceso](https://msdn.microsoft.com/library/dn308586).</span><span class="sxs-lookup"><span data-stu-id="1120d-263">For more information about hello Access Panel, see [Introduction to the Access Panel](https://msdn.microsoft.com/library/dn308586).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="1120d-264">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="1120d-264">Additional resources</span></span>

* [<span data-ttu-id="1120d-265">Lista de tutoriales sobre cómo tooIntegrate aplicaciones de SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="1120d-265">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="1120d-266">¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="1120d-266">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-linkedinsalesnavigator-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-linkedinsalesnavigator-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-linkedinsalesnavigator-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-linkedinsalesnavigator-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-linkedinsalesnavigator-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-linkedinsalesnavigator-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-linkedinsalesnavigator-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-linkedinsalesnavigator-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-linkedinsalesnavigator-tutorial/tutorial_general_203.png

