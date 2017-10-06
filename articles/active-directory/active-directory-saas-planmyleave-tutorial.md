---
title: "Tutorial: integración de Azure Active Directory con PlanMyLeave | Microsoft Docs"
description: "Obtenga información acerca de cómo tooconfigure inicio de sesión único entre Azure Active Directory y PlanMyLeave."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: b0d31cbe-7ae2-488b-9cf3-4927391fa744
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/01/2017
ms.author: jeedes
ms.openlocfilehash: 44a6782e44ef22fc957544960be1742f9eed6e51
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-planmyleave"></a><span data-ttu-id="9111d-103">Tutorial: Integración de Azure Active Directory con PlanMyLeave</span><span class="sxs-lookup"><span data-stu-id="9111d-103">Tutorial: Azure Active Directory integration with PlanMyLeave</span></span>

<span data-ttu-id="9111d-104">En este tutorial, aprenderá cómo toointegrate PlanMyLeave con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="9111d-104">In this tutorial, you learn how toointegrate PlanMyLeave with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="9111d-105">Integración PlanMyLeave con Azure AD proporciona Hola siguientes ventajas:</span><span class="sxs-lookup"><span data-stu-id="9111d-105">Integrating PlanMyLeave with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="9111d-106">Puede controlar en Azure AD que tenga acceso tooPlanMyLeave</span><span class="sxs-lookup"><span data-stu-id="9111d-106">You can control in Azure AD who has access tooPlanMyLeave</span></span>
- <span data-ttu-id="9111d-107">Puede habilitar los usuarios tooautomatically get ha iniciado sesión tooPlanMyLeave (Single Sign-On) con sus cuentas de Azure AD</span><span class="sxs-lookup"><span data-stu-id="9111d-107">You can enable your users tooautomatically get signed-on tooPlanMyLeave (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="9111d-108">Puede administrar las cuentas en una ubicación central: portal de administración de Azure de Hola</span><span class="sxs-lookup"><span data-stu-id="9111d-108">You can manage your accounts in one central location - hello Azure Management portal</span></span>

<span data-ttu-id="9111d-109">Si desea obtener más información acerca de la integración de aplicaciones de SaaS con Azure AD tooknow, consulte [¿qué es acceso a la aplicación y el inicio de sesión único con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="9111d-109">If you want tooknow more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="9111d-110">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="9111d-110">Prerequisites</span></span>

<span data-ttu-id="9111d-111">integración de Azure AD con PlanMyLeave tooconfigure, necesita Hola siguientes elementos:</span><span class="sxs-lookup"><span data-stu-id="9111d-111">tooconfigure Azure AD integration with PlanMyLeave, you need hello following items:</span></span>

- <span data-ttu-id="9111d-112">Una suscripción de Azure AD</span><span class="sxs-lookup"><span data-stu-id="9111d-112">An Azure AD subscription</span></span>
- <span data-ttu-id="9111d-113">Una suscripción habilitada para el inicio de sesión único en PlanMyLeave</span><span class="sxs-lookup"><span data-stu-id="9111d-113">A PlanMyLeave single-sign on enabled subscription</span></span>


> [!NOTE]
> <span data-ttu-id="9111d-114">Hola tootest los pasos de este tutorial, no se recomienda usar un entorno de producción.</span><span class="sxs-lookup"><span data-stu-id="9111d-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>


<span data-ttu-id="9111d-115">pasos de hello tootest en este tutorial, debe seguir estas recomendaciones:</span><span class="sxs-lookup"><span data-stu-id="9111d-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="9111d-116">No debe usar el entorno de producción, a menos que sea necesario.</span><span class="sxs-lookup"><span data-stu-id="9111d-116">You should not use your production environment, unless this is necessary.</span></span>
- <span data-ttu-id="9111d-117">Si no dispone de un entorno de prueba de Azure AD, puede obtener una versión de prueba de un mes [aquí](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="9111d-117">If you don't have an Azure AD trial environment, you can get an one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>


## <a name="scenario-description"></a><span data-ttu-id="9111d-118">Descripción del escenario</span><span class="sxs-lookup"><span data-stu-id="9111d-118">Scenario description</span></span>
<span data-ttu-id="9111d-119">En este tutorial, puede probar el inicio de sesión único de Azure AD en un entorno de prueba.</span><span class="sxs-lookup"><span data-stu-id="9111d-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="9111d-120">escenario de Hello descrito en este tutorial consta de dos bloques principales:</span><span class="sxs-lookup"><span data-stu-id="9111d-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="9111d-121">Agregar PlanMyLeave desde la Galería de Hola</span><span class="sxs-lookup"><span data-stu-id="9111d-121">Adding PlanMyLeave from hello gallery</span></span>
2. <span data-ttu-id="9111d-122">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="9111d-122">Configuring and testing Azure AD single sign-on</span></span>


## <a name="adding-planmyleave-from-hello-gallery"></a><span data-ttu-id="9111d-123">Agregar PlanMyLeave desde la Galería de Hola</span><span class="sxs-lookup"><span data-stu-id="9111d-123">Adding PlanMyLeave from hello gallery</span></span>
<span data-ttu-id="9111d-124">integración de hello tooconfigure de PlanMyLeave en Azure AD, deberá tooadd PlanMyLeave de lista de tooyour Hola Galería de aplicaciones administradas de SaaS.</span><span class="sxs-lookup"><span data-stu-id="9111d-124">tooconfigure hello integration of PlanMyLeave into Azure AD, you need tooadd PlanMyLeave from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="9111d-125">**tooadd PlanMyLeave de galería de hello, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="9111d-125">**tooadd PlanMyLeave from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="9111d-126">Hola  **[Portal de administración de Azure](https://portal.azure.com)**, en el panel de navegación izquierdo de Hola, haga clic en **Azure Active Directory** icono.</span><span class="sxs-lookup"><span data-stu-id="9111d-126">In hello **[Azure Management Portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="9111d-128">Navegue demasiado**aplicaciones empresariales**.</span><span class="sxs-lookup"><span data-stu-id="9111d-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="9111d-129">A continuación, vaya demasiado**todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="9111d-129">Then go too**All applications**.</span></span>

    ![Aplicaciones][2]
    
3. <span data-ttu-id="9111d-131">Haga clic en **agregar** botón en la parte superior de saludo del cuadro de diálogo de Hola.</span><span class="sxs-lookup"><span data-stu-id="9111d-131">Click **Add** button on hello top of hello dialog.</span></span>

    ![Aplicaciones][3]

4. <span data-ttu-id="9111d-133">En el cuadro de búsqueda de hello, escriba **PlanMyLeave**.</span><span class="sxs-lookup"><span data-stu-id="9111d-133">In hello search box, type **PlanMyLeave**.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-planmyleave-tutorial/tutorial_planmyleave_001.png)

5. <span data-ttu-id="9111d-135">En el panel de resultados de hello, seleccione **PlanMyLeave**y, a continuación, haga clic en **agregar** botón aplicación hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="9111d-135">In hello results panel, select **PlanMyLeave**, and then click **Add** button tooadd hello application.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-planmyleave-tutorial/tutorial_planmyleave_0001.png)


##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="9111d-137">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="9111d-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="9111d-138">En esta sección, podrá configurar y probar el inicio de sesión único de Azure AD con PlanMyLeave con un usuario de prueba llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="9111d-138">In this section, you configure and test Azure AD single sign-on with PlanMyLeave based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="9111d-139">Para toowork de inicio de sesión único, Azure AD necesita tooknow qué usuario equivalente de hello en PlanMyLeave es tooa usuario en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="9111d-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in PlanMyLeave is tooa user in Azure AD.</span></span> <span data-ttu-id="9111d-140">En otras palabras, una relación de vínculo entre un usuario de Azure AD y el usuario relacionado de hello en PlanMyLeave debe toobe establecido.</span><span class="sxs-lookup"><span data-stu-id="9111d-140">In other words, a link relationship between an Azure AD user and hello related user in PlanMyLeave needs toobe established.</span></span>

<span data-ttu-id="9111d-141">Esta relación de vínculo se establece mediante la asignación de valor de Hola de hello **nombre de usuario** en Azure AD como valor de Hola de hello **nombre de usuario** en PlanMyLeave.</span><span class="sxs-lookup"><span data-stu-id="9111d-141">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in PlanMyLeave.</span></span>

<span data-ttu-id="9111d-142">tooconfigure y prueba de inicio de sesión único en Azure AD con PlanMyLeave, deberá hello toocomplete después de bloques de creación:</span><span class="sxs-lookup"><span data-stu-id="9111d-142">tooconfigure and test Azure AD single sign-on with PlanMyLeave, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="9111d-143">**[Configuración de Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable la toouse usuarios esta característica.</span><span class="sxs-lookup"><span data-stu-id="9111d-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="9111d-144">**[Crear un usuario de prueba de Azure AD](#creating-an-azure-ad-test-user)**  -inicio de sesión único en Azure AD tootest con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="9111d-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="9111d-145">**[Crear un usuario de prueba PlanMyLeave](#creating-a-planmyleave-test-user)**  -toohave un equivalente de Britta Simon en PlanMyLeave que está vinculado toohello Azure AD representación de ella.</span><span class="sxs-lookup"><span data-stu-id="9111d-145">**[Creating a PlanMyLeave test user](#creating-a-planmyleave-test-user)** - toohave a counterpart of Britta Simon in PlanMyLeave that is linked toohello Azure AD representation of her.</span></span>
4. <span data-ttu-id="9111d-146">**[Asignar usuario de prueba de hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="9111d-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="9111d-147">**[Pruebas de Single Sign-On](#testing-single-sign-on)**  -tooverify Hola si funciona la configuración.</span><span class="sxs-lookup"><span data-stu-id="9111d-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="9111d-148">Configuración del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="9111d-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="9111d-149">En esta sección, habilitar inicio de sesión único en Azure AD en el portal de administración de Azure de Hola y configurar el inicio de sesión único en la aplicación PlanMyLeave.</span><span class="sxs-lookup"><span data-stu-id="9111d-149">In this section, you enable Azure AD single sign-on in hello Azure Management portal and configure single sign-on in your PlanMyLeave application.</span></span>

<span data-ttu-id="9111d-150">**inicio de sesión único en Azure AD tooconfigure con PlanMyLeave, realizar Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="9111d-150">**tooconfigure Azure AD single sign-on with PlanMyLeave, perform hello following steps:**</span></span>

1. <span data-ttu-id="9111d-151">En el portal de administración de Azure de hello, en hello **PlanMyLeave** página de integración de aplicaciones, haga clic en **inicio de sesión único**.</span><span class="sxs-lookup"><span data-stu-id="9111d-151">In hello Azure Management portal, on hello **PlanMyLeave** application integration page, click **Single sign-on**.</span></span>

    ![Configurar inicio de sesión único][4]

2. <span data-ttu-id="9111d-153">En hello **inicio de sesión único** página del cuadro de diálogo, como **modo** seleccione **sesión basado en SAML** tooenable inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="9111d-153">On hello **Single sign-on** dialog page, as **Mode** select **SAML-based Sign-on** tooenable single sign on.</span></span>
 
    ![Configurar inicio de sesión único](./media/active-directory-saas-planmyleave-tutorial/tutorial_planmyleave_01.png)

3. <span data-ttu-id="9111d-155">En hello **PlanMyLeave dominio y las direcciones URL** sección, lleve a cabo Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="9111d-155">On hello **PlanMyLeave Domain and URLs** section, perform hello following steps:</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-planmyleave-tutorial/tutorial_planmyleave_02.png)

    <span data-ttu-id="9111d-157">a.</span><span class="sxs-lookup"><span data-stu-id="9111d-157">a.</span></span> <span data-ttu-id="9111d-158">Hola **dirección URL de inicio de sesión** cuadro de texto, escriba una dirección URL usando Hola siguiente patrón:`https://<company-name>.planmyleave.com/Login.aspx`</span><span class="sxs-lookup"><span data-stu-id="9111d-158">In hello **Sign On URL** textbox, type a URL using hello following pattern: `https://<company-name>.planmyleave.com/Login.aspx`</span></span>
    
    <span data-ttu-id="9111d-159">b.</span><span class="sxs-lookup"><span data-stu-id="9111d-159">b.</span></span> <span data-ttu-id="9111d-160">Hola **identificador** cuadro de texto, escriba una dirección URL usando Hola siguiente patrón:`https://<company-name>.planmyleave.com`</span><span class="sxs-lookup"><span data-stu-id="9111d-160">In hello **Identifer** textbox, type a URL using hello following pattern: `https://<company-name>.planmyleave.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="9111d-161">Tenga en cuenta que estos no son los valores reales de Hola.</span><span class="sxs-lookup"><span data-stu-id="9111d-161">Please note that these are not hello real values.</span></span> <span data-ttu-id="9111d-162">Tendrá que tooupdate estos valores con hello real iniciar sesión en la dirección URL y el identificador.</span><span class="sxs-lookup"><span data-stu-id="9111d-162">You have tooupdate these values with hello actual Sign On URL and Identifier.</span></span> <span data-ttu-id="9111d-163">Póngase en contacto con [equipo de soporte técnico de PlanMyLeave](mailto:support@planmyleave.com) tooget estos valores.</span><span class="sxs-lookup"><span data-stu-id="9111d-163">Contact [PlanMyLeave support team](mailto:support@planmyleave.com) tooget these values.</span></span>

4. <span data-ttu-id="9111d-164">En hello **el certificado de firma de SAML** sección, haga clic en **crear un nuevo certificado**.</span><span class="sxs-lookup"><span data-stu-id="9111d-164">On hello **SAML Signing Certificate** section, click **Create new certificate**.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-planmyleave-tutorial/tutorial_planmyleave_03.png)     

5. <span data-ttu-id="9111d-166">En hello **crear nuevo certificado** cuadro de diálogo, haga clic en el icono del calendario de Hola y seleccione un **fecha de expiración**.</span><span class="sxs-lookup"><span data-stu-id="9111d-166">On hello **Create New Certificate** dialog, click hello calendar icon and select an **expiry date**.</span></span> <span data-ttu-id="9111d-167">Luego haga clic en el botón **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="9111d-167">Then click **Save** button.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-planmyleave-tutorial/tutorial_general_300.png)

6. <span data-ttu-id="9111d-169">En hello **el certificado de firma de SAML** sección, seleccione **activar el nuevo certificado** y haga clic en **guardar** botón.</span><span class="sxs-lookup"><span data-stu-id="9111d-169">On hello **SAML Signing Certificate** section, select **Make new certificate active** and click **Save** button.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-planmyleave-tutorial/tutorial_planmyleave_04.png)

7. <span data-ttu-id="9111d-171">En la ventana emergente de hello **el certificado de sustitución** ventana, haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="9111d-171">On hello pop-up **Rollover certificate** window, click **OK**.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-planmyleave-tutorial/tutorial_general_400.png)

8. <span data-ttu-id="9111d-173">En hello **el certificado de firma de SAML** sección, haga clic en **certificado (base64)** y, a continuación, guarde el archivo de certificado de hello en el equipo.</span><span class="sxs-lookup"><span data-stu-id="9111d-173">On hello **SAML Signing Certificate** section, click **Certificate (base64)** and then save hello certificate file on your computer.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-planmyleave-tutorial/tutorial_planmyleave_05.png) 

9. <span data-ttu-id="9111d-175">En hello **PlanMyLeave configuración** sección, haga clic en **configurar PlanMyLeave** tooopen **configurar inicio de sesión** ventana.</span><span class="sxs-lookup"><span data-stu-id="9111d-175">On hello **PlanMyLeave Configuration** section, click **Configure PlanMyLeave** tooopen **Configure sign-on** window.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-planmyleave-tutorial/tutorial_planmyleave_06.png) 

    ![Configurar inicio de sesión único](./media/active-directory-saas-planmyleave-tutorial/tutorial_planmyleave_07.png)

10. <span data-ttu-id="9111d-178">En otra ventana del explorador web, inicie sesión en como administrador en el inquilino de PlanMyLeave.</span><span class="sxs-lookup"><span data-stu-id="9111d-178">In a different web browser window, log into your PlanMyLeave tenant as an administrator.</span></span>

11. <span data-ttu-id="9111d-179">Vaya demasiado**el programa de instalación de sistema**.</span><span class="sxs-lookup"><span data-stu-id="9111d-179">Go too**System Setup**.</span></span> <span data-ttu-id="9111d-180">A continuación, en hello **administración de seguridad** sección, haga clic **configuración de SAML de la empresa** .</span><span class="sxs-lookup"><span data-stu-id="9111d-180">Then on hello **Security Management** section click **Company SAML settings** .</span></span>

    ![Configuración del inicio de sesión único en la aplicación](./media/active-directory-saas-planmyleave-tutorial/tutorial_planmyleave_002.png) 

12. <span data-ttu-id="9111d-182">En hello **configuración SAML** sección, haga clic en el icono de editor.</span><span class="sxs-lookup"><span data-stu-id="9111d-182">On hello **SAML Settings** section, click editor icon.</span></span>

    ![Configuración del inicio de sesión único en la aplicación](./media/active-directory-saas-planmyleave-tutorial/tutorial_planmyleave_003.png)

13. <span data-ttu-id="9111d-184">En hello **configuración de SAML de actualización** sección, lleve a cabo Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="9111d-184">On hello **Update SAML Settings** section, perform hello following steps:</span></span>

    ![Configuración del inicio de sesión único en la aplicación](./media/active-directory-saas-planmyleave-tutorial/tutorial_planmyleave_004.png)

    <span data-ttu-id="9111d-186">a.</span><span class="sxs-lookup"><span data-stu-id="9111d-186">a.</span></span>  <span data-ttu-id="9111d-187">Hola **dirección URL de inicio de sesión** cuadro de texto, coloque valor Hola de **SAML Single Sign-On dirección URL del servicio** desde la ventana de configuración de aplicación de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="9111d-187">In hello **Login URL** textbox, put hello value of **SAML Single Sign-On Service URL** from Azure AD application configuration window.</span></span>

    <span data-ttu-id="9111d-188">b.</span><span class="sxs-lookup"><span data-stu-id="9111d-188">b.</span></span>  <span data-ttu-id="9111d-189">Abra el archivo de certificado descargado en el Bloc de notas, copie solo Hola contenido entre Hola---Begin Certificate---y---End certificate---del mismo en el Portapapeles y, a continuación, péguelo toohello **certificado** cuadro de texto.</span><span class="sxs-lookup"><span data-stu-id="9111d-189">Open your downloaded certificate file in notepad, copy only hello content between hello ---Begin Certificate--- and ---End certificate---- of it into your clipboard, and then paste it toohello **Certificate** textbox.</span></span>

    <span data-ttu-id="9111d-190">c.</span><span class="sxs-lookup"><span data-stu-id="9111d-190">c.</span></span> <span data-ttu-id="9111d-191">Establecer"**está habilitado**"demasiado"**Sí**".</span><span class="sxs-lookup"><span data-stu-id="9111d-191">Set "**Is Enable**" too"**Yes**".</span></span>

    <span data-ttu-id="9111d-192">d.</span><span class="sxs-lookup"><span data-stu-id="9111d-192">d.</span></span> <span data-ttu-id="9111d-193">Haga clic en **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="9111d-193">Click **Save**.</span></span>



### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="9111d-194">Creación de un usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="9111d-194">Creating an Azure AD test user</span></span>
<span data-ttu-id="9111d-195">objetivo de Hola de esta sección es un usuario de prueba en el portal de administración de Azure de hello llamado a Britta Simon toocreate.</span><span class="sxs-lookup"><span data-stu-id="9111d-195">hello objective of this section is toocreate a test user in hello Azure Management portal called Britta Simon.</span></span>

![Creación de un usuario de Azure AD][100]

<span data-ttu-id="9111d-197">**toocreate un usuario de prueba en Azure AD, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="9111d-197">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="9111d-198">Hola **portal de administración de Azure**, en Hola panel de navegación izquierdo, haga clic en **Azure Active Directory** icono.</span><span class="sxs-lookup"><span data-stu-id="9111d-198">In hello **Azure Management portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-planmyleave-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="9111d-200">Vaya demasiado**usuarios y grupos** y haga clic en **todos los usuarios** toodisplay lista de Hola de usuarios.</span><span class="sxs-lookup"><span data-stu-id="9111d-200">Go too**Users and groups** and click **All users** toodisplay hello list of users.</span></span>
    
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-planmyleave-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="9111d-202">En la parte superior de saludo del cuadro de diálogo de hello haga clic en **agregar** tooopen hello **usuario** cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="9111d-202">At hello top of hello dialog click **Add** tooopen hello **User** dialog.</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-planmyleave-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="9111d-204">En hello **usuario** cuadro de diálogo, siga los pasos de hello:</span><span class="sxs-lookup"><span data-stu-id="9111d-204">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-planmyleave-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="9111d-206">a.</span><span class="sxs-lookup"><span data-stu-id="9111d-206">a.</span></span> <span data-ttu-id="9111d-207">Hola **nombre** cuadro de texto, tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="9111d-207">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="9111d-208">b.</span><span class="sxs-lookup"><span data-stu-id="9111d-208">b.</span></span> <span data-ttu-id="9111d-209">Hola **nombre de usuario** cuadro de texto, hello tipo **dirección de correo electrónico** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="9111d-209">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="9111d-210">c.</span><span class="sxs-lookup"><span data-stu-id="9111d-210">c.</span></span> <span data-ttu-id="9111d-211">Seleccione **Mostrar contraseña** y anote el valor de Hola de hello **contraseña**.</span><span class="sxs-lookup"><span data-stu-id="9111d-211">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="9111d-212">d.</span><span class="sxs-lookup"><span data-stu-id="9111d-212">d.</span></span> <span data-ttu-id="9111d-213">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="9111d-213">Click **Create**.</span></span> 



### <a name="creating-a-planmyleave-test-user"></a><span data-ttu-id="9111d-214">Crear un usuario de prueba de PlanMyLeave</span><span class="sxs-lookup"><span data-stu-id="9111d-214">Creating a PlanMyLeave test user</span></span>

<span data-ttu-id="9111d-215">objetivo de Hola de esta sección es un usuario llamado a Britta Simon en PlanMyLeave toocreate.</span><span class="sxs-lookup"><span data-stu-id="9111d-215">hello objective of this section is toocreate a user called Britta Simon in PlanMyLeave.</span></span> <span data-ttu-id="9111d-216">PlanMyLeave admite el aprovisionamiento Just-In-Time, que está habilitado de forma predeterminada.</span><span class="sxs-lookup"><span data-stu-id="9111d-216">PlanMyLeave supports just-in-time provisioning, which is by default enabled.</span></span>

<span data-ttu-id="9111d-217">No hay ningún elemento de acción para usted en esta sección.</span><span class="sxs-lookup"><span data-stu-id="9111d-217">There is no action item for you in this section.</span></span> <span data-ttu-id="9111d-218">Si no existe todavía, se creará un nuevo usuario durante un tooaccess intento PlanMyLeave.</span><span class="sxs-lookup"><span data-stu-id="9111d-218">A new user will be created during an attempt tooaccess PlanMyLeave if it doesn't exist yet.</span></span>

> [!NOTE]
> <span data-ttu-id="9111d-219">Si necesita un usuario toocreate manualmente, necesita toocontact [equipo de soporte técnico de PlanMyLeave](mailto:support@planmyleave.com).</span><span class="sxs-lookup"><span data-stu-id="9111d-219">If you need toocreate an user manually, you need toocontact [PlanMyLeave support team](mailto:support@planmyleave.com).</span></span>



### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="9111d-220">Asignación de usuario de prueba de hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="9111d-220">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="9111d-221">En esta sección, se habilita Britta Simon toouse Azure inicio de sesión único mediante la concesión de su tooPlanMyLeave de acceso.</span><span class="sxs-lookup"><span data-stu-id="9111d-221">In this section, you enable Britta Simon toouse Azure single sign-on by granting her access tooPlanMyLeave.</span></span>

![Asignar usuario][200] 

<span data-ttu-id="9111d-223">**tooassign Britta Simon tooPlanMyLeave, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="9111d-223">**tooassign Britta Simon tooPlanMyLeave, perform hello following steps:**</span></span>

1. <span data-ttu-id="9111d-224">En el portal de administración de Azure de hello, abrir vista de aplicaciones de hello y, a continuación, navegue a vista de directorio toohello y vaya demasiado**aplicaciones empresariales** , a continuación, haga clic en **todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="9111d-224">In hello Azure Management portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Asignar usuario][201] 

2. <span data-ttu-id="9111d-226">En la lista de aplicaciones de hello, seleccione **PlanMyLeave**.</span><span class="sxs-lookup"><span data-stu-id="9111d-226">In hello applications list, select **PlanMyLeave**.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-planmyleave-tutorial/tutorial_planmyleave_50.png) 

3. <span data-ttu-id="9111d-228">En el menú de Hola Hola izquierda, haga clic en **usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="9111d-228">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Asignar usuario][202] 

4. <span data-ttu-id="9111d-230">Haga clic en el botón **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="9111d-230">Click **Add** button.</span></span> <span data-ttu-id="9111d-231">Después, seleccione **Usuarios y grupos** en el cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="9111d-231">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Asignar usuario][203]

5. <span data-ttu-id="9111d-233">En **usuarios y grupos** cuadro de diálogo, seleccione **Britta Simon** en la lista de usuarios de Hola.</span><span class="sxs-lookup"><span data-stu-id="9111d-233">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="9111d-234">Haga clic en el botón **Seleccionar** del cuadro de diálogo **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="9111d-234">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="9111d-235">Haga clic en el botón **Asignar** del cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="9111d-235">Click **Assign** button on **Add Assignment** dialog.</span></span>
    


### <a name="testing-single-sign-on"></a><span data-ttu-id="9111d-236">Prueba del inicio de sesión único </span><span class="sxs-lookup"><span data-stu-id="9111d-236">Testing single sign-on</span></span>

<span data-ttu-id="9111d-237">En esta sección, comprobará su único inicio de sesión en configuración de Azure AD con hello Panel de acceso.</span><span class="sxs-lookup"><span data-stu-id="9111d-237">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="9111d-238">Al hacer clic en icono de PlanMyLeave Hola Hola Panel de acceso, deberá obtener automáticamente ha iniciado sesión tooyour PlanMyLeave aplicación.</span><span class="sxs-lookup"><span data-stu-id="9111d-238">When you click hello PlanMyLeave tile in hello Access Panel, you should get automatically signed-on tooyour PlanMyLeave application.</span></span>


## <a name="additional-resources"></a><span data-ttu-id="9111d-239">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="9111d-239">Additional resources</span></span>

* [<span data-ttu-id="9111d-240">Lista de tutoriales sobre cómo tooIntegrate aplicaciones de SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="9111d-240">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="9111d-241">¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="9111d-241">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-planmyleave-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-planmyleave-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-planmyleave-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-planmyleave-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-planmyleave-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-planmyleave-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-planmyleave-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-planmyleave-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-planmyleave-tutorial/tutorial_general_203.png