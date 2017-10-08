---
title: "Tutorial: Integración de Azure Active Directory con Workday | Microsoft Docs"
description: "Obtenga información acerca de cómo tooconfigure inicio de sesión único entre Azure Active Directory y los días laborables."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: e9da692e-4a65-4231-8ab3-bc9a87b10bca
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: jeedes
ms.openlocfilehash: aaa41e372e45f464c4540a70fc79c98dbc06d6b4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-workday"></a><span data-ttu-id="cc0ab-103">Tutorial: Integración de Azure Active Directory con Workday</span><span class="sxs-lookup"><span data-stu-id="cc0ab-103">Tutorial: Azure Active Directory integration with Workday</span></span>

<span data-ttu-id="cc0ab-104">En este tutorial, aprenderá cómo toointegrate Workday con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="cc0ab-104">In this tutorial, you learn how toointegrate Workday with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="cc0ab-105">Integración de Workday con Azure AD proporciona Hola siguientes ventajas:</span><span class="sxs-lookup"><span data-stu-id="cc0ab-105">Integrating Workday with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="cc0ab-106">Puede controlar en Azure AD que tenga acceso tooWorkday</span><span class="sxs-lookup"><span data-stu-id="cc0ab-106">You can control in Azure AD who has access tooWorkday</span></span>
- <span data-ttu-id="cc0ab-107">Puede habilitar los usuarios tooautomatically get ha iniciado sesión tooWorkday (Single Sign-On) con sus cuentas de Azure AD</span><span class="sxs-lookup"><span data-stu-id="cc0ab-107">You can enable your users tooautomatically get signed-on tooWorkday (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="cc0ab-108">Puede administrar las cuentas en una ubicación central: Hola portal de Azure</span><span class="sxs-lookup"><span data-stu-id="cc0ab-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="cc0ab-109">Si desea obtener más información acerca de la integración de aplicaciones de SaaS con Azure AD tooknow, consulte [¿qué es acceso a la aplicación y el inicio de sesión único con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="cc0ab-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="cc0ab-110">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="cc0ab-110">Prerequisites</span></span>

<span data-ttu-id="cc0ab-111">integración de Azure AD con Workday tooconfigure, necesita Hola siguientes elementos:</span><span class="sxs-lookup"><span data-stu-id="cc0ab-111">tooconfigure Azure AD integration with Workday, you need hello following items:</span></span>

- <span data-ttu-id="cc0ab-112">Una suscripción de Azure AD</span><span class="sxs-lookup"><span data-stu-id="cc0ab-112">An Azure AD subscription</span></span>
- <span data-ttu-id="cc0ab-113">Una suscripción habilitada para el inicio de sesión único en Workday</span><span class="sxs-lookup"><span data-stu-id="cc0ab-113">A Workday single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="cc0ab-114">Hola tootest los pasos de este tutorial, no se recomienda usar un entorno de producción.</span><span class="sxs-lookup"><span data-stu-id="cc0ab-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="cc0ab-115">pasos de hello tootest en este tutorial, debe seguir estas recomendaciones:</span><span class="sxs-lookup"><span data-stu-id="cc0ab-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="cc0ab-116">No use el entorno de producción, salvo que sea necesario.</span><span class="sxs-lookup"><span data-stu-id="cc0ab-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="cc0ab-117">Si no dispone de un entorno de prueba de Azure AD, puede obtener una versión de prueba de un mes [aquí](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="cc0ab-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="cc0ab-118">Descripción del escenario</span><span class="sxs-lookup"><span data-stu-id="cc0ab-118">Scenario description</span></span>
<span data-ttu-id="cc0ab-119">En este tutorial, puede probar el inicio de sesión único de Azure AD en un entorno de prueba.</span><span class="sxs-lookup"><span data-stu-id="cc0ab-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="cc0ab-120">escenario de Hello descrito en este tutorial consta de dos bloques principales:</span><span class="sxs-lookup"><span data-stu-id="cc0ab-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="cc0ab-121">Adición de jornada laboral de galería de Hola</span><span class="sxs-lookup"><span data-stu-id="cc0ab-121">Adding Workday from hello gallery</span></span>
2. <span data-ttu-id="cc0ab-122">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="cc0ab-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-workday-from-hello-gallery"></a><span data-ttu-id="cc0ab-123">Adición de jornada laboral de galería de Hola</span><span class="sxs-lookup"><span data-stu-id="cc0ab-123">Adding Workday from hello gallery</span></span>
<span data-ttu-id="cc0ab-124">integración de hello tooconfigure de jornada laboral en Azure AD, deberá tooadd Workday de lista de tooyour Hola Galería de aplicaciones administradas de SaaS.</span><span class="sxs-lookup"><span data-stu-id="cc0ab-124">tooconfigure hello integration of Workday into Azure AD, you need tooadd Workday from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="cc0ab-125">**tooadd Workday de galería de hello, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="cc0ab-125">**tooadd Workday from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="cc0ab-126">Hola  **[portal de Azure](https://portal.azure.com)**, en el panel de navegación izquierdo de Hola, haga clic en **Azure Active Directory** icono.</span><span class="sxs-lookup"><span data-stu-id="cc0ab-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="cc0ab-128">Navegue demasiado**aplicaciones empresariales**.</span><span class="sxs-lookup"><span data-stu-id="cc0ab-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="cc0ab-129">A continuación, vaya demasiado**todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="cc0ab-129">Then go too**All applications**.</span></span>

    ![Aplicaciones][2]
    
3. <span data-ttu-id="cc0ab-131">tooadd nueva aplicación, haga clic en **nueva aplicación** botón en la parte superior de saludo del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="cc0ab-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Aplicaciones][3]

4. <span data-ttu-id="cc0ab-133">En el cuadro de búsqueda de hello, escriba **Workday**.</span><span class="sxs-lookup"><span data-stu-id="cc0ab-133">In hello search box, type **Workday**.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-workday-tutorial/tutorial_workday_search.png)

5. <span data-ttu-id="cc0ab-135">En el panel de resultados de hello, seleccione **Workday**y, a continuación, haga clic en **agregar** botón aplicación hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="cc0ab-135">In hello results panel, select **Workday**, and then click **Add** button tooadd hello application.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-workday-tutorial/tutorial_workday_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="cc0ab-137">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="cc0ab-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="cc0ab-138">En esta sección, puede configurar y probar el inicio de sesión único de Azure AD con Workday con un usuario de prueba llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="cc0ab-138">In this section, you configure and test Azure AD single sign-on with Workday based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="cc0ab-139">Para toowork de inicio de sesión único, Azure AD necesita tooknow qué usuario equivalente de hello en Workday es tooa usuario en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="cc0ab-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Workday is tooa user in Azure AD.</span></span> <span data-ttu-id="cc0ab-140">En otras palabras, una relación de vínculo entre un usuario de Azure AD y el usuario relacionado de hello en Workday debe toobe establecido.</span><span class="sxs-lookup"><span data-stu-id="cc0ab-140">In other words, a link relationship between an Azure AD user and hello related user in Workday needs toobe established.</span></span>

<span data-ttu-id="cc0ab-141">Esta relación de vínculo se establece mediante la asignación de valor de Hola de hello **nombre de usuario** en Azure AD como valor de Hola de hello **nombre de usuario** en jornada laboral.</span><span class="sxs-lookup"><span data-stu-id="cc0ab-141">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in Workday.</span></span>

<span data-ttu-id="cc0ab-142">tooconfigure y prueba de inicio de sesión único en Azure AD con Workday, deberá hello toocomplete después de bloques de creación:</span><span class="sxs-lookup"><span data-stu-id="cc0ab-142">tooconfigure and test Azure AD single sign-on with Workday, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="cc0ab-143">**[Configuración de Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable la toouse usuarios esta característica.</span><span class="sxs-lookup"><span data-stu-id="cc0ab-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="cc0ab-144">**[Crear un usuario de prueba de Azure AD](#creating-an-azure-ad-test-user)**  -inicio de sesión único en Azure AD tootest con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="cc0ab-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="cc0ab-145">**[Crear un usuario de prueba de jornada laboral](#creating-a-workday-test-user)**  -toohave un equivalente de Britta Simon en jornada laboral que es la representación toohello vinculado Azure AD del usuario.</span><span class="sxs-lookup"><span data-stu-id="cc0ab-145">**[Creating a Workday test user](#creating-a-workday-test-user)** - toohave a counterpart of Britta Simon in Workday that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="cc0ab-146">**[Asignar usuario de prueba de hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="cc0ab-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="cc0ab-147">**[Pruebas de Single Sign-On](#testing-single-sign-on)**  -tooverify Hola si funciona la configuración.</span><span class="sxs-lookup"><span data-stu-id="cc0ab-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="cc0ab-148">Configuración del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="cc0ab-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="cc0ab-149">En esta sección, habilitar inicio de sesión único en Azure AD en hello portal de Azure y configurar el inicio de sesión único en la aplicación de jornada laboral.</span><span class="sxs-lookup"><span data-stu-id="cc0ab-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Workday application.</span></span>

<span data-ttu-id="cc0ab-150">**inicio de sesión único en tooconfigure Azure AD con Workday, siga Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="cc0ab-150">**tooconfigure Azure AD single sign-on with Workday, perform hello following steps:**</span></span>

1. <span data-ttu-id="cc0ab-151">En el portal de Azure, en Hola Hola **Workday** página de integración de aplicaciones, haga clic en **inicio de sesión único**.</span><span class="sxs-lookup"><span data-stu-id="cc0ab-151">In hello Azure portal, on hello **Workday** application integration page, click **Single sign-on**.</span></span>

    ![Configurar inicio de sesión único][4]

2. <span data-ttu-id="cc0ab-153">En hello **inicio de sesión único** cuadro de diálogo, seleccione **modo** como **sesión basado en SAML** tooenable inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="cc0ab-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurar inicio de sesión único](./media/active-directory-saas-workday-tutorial/tutorial_workday_samlbase.png)

3. <span data-ttu-id="cc0ab-155">En hello **Workday dominio y las direcciones URL** sección, lleve a cabo Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="cc0ab-155">On hello **Workday Domain and URLs** section, perform hello following steps:</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-workday-tutorial/tutorial_workday_url.png)

    <span data-ttu-id="cc0ab-157">a.</span><span class="sxs-lookup"><span data-stu-id="cc0ab-157">a.</span></span> <span data-ttu-id="cc0ab-158">Hola **dirección URL de inicio de sesión** cuadro de texto, valor de tipo hello como:`https://impl.workday.com/<tenant>/login-saml2.htmld`</span><span class="sxs-lookup"><span data-stu-id="cc0ab-158">In hello **Sign-on URL** textbox, type hello value as: `https://impl.workday.com/<tenant>/login-saml2.htmld`</span></span>

    <span data-ttu-id="cc0ab-159">b.</span><span class="sxs-lookup"><span data-stu-id="cc0ab-159">b.</span></span> <span data-ttu-id="cc0ab-160">Hola **dirección URL de respuesta** cuadro de texto, escriba una dirección URL usando Hola siguiente patrón:`https://impl.workday.com/<tenant>/login-saml.htmld`</span><span class="sxs-lookup"><span data-stu-id="cc0ab-160">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://impl.workday.com/<tenant>/login-saml.htmld`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="cc0ab-161">Estos valores no son Hola real.</span><span class="sxs-lookup"><span data-stu-id="cc0ab-161">These values are not hello real.</span></span> <span data-ttu-id="cc0ab-162">Actualizar estos valores con la URL de inicio de sesión real de Hola y la dirección URL de respuesta.</span><span class="sxs-lookup"><span data-stu-id="cc0ab-162">Update these values with hello actual Sign-on URL and Reply URL.</span></span> <span data-ttu-id="cc0ab-163">La URL de respuesta debe tener un subdominio (por ejemplo, www, wd2, wd3, wd3-impl, wd5 y wd5-impl).</span><span class="sxs-lookup"><span data-stu-id="cc0ab-163">Your reply URL must have a subdomain for example: www, wd2, wd3, wd3-impl, wd5, wd5-impl).</span></span> <span data-ttu-id="cc0ab-164">Usar algo como "*http://www.myworkday.com*" funciona, pero "*http://myworkday.com*" no funciona.</span><span class="sxs-lookup"><span data-stu-id="cc0ab-164">Using something like "*http://www.myworkday.com*" works but "*http://myworkday.com*" does not.</span></span> <span data-ttu-id="cc0ab-165">Póngase en contacto con [equipo de soporte técnico de Workday cliente](https://www.workday.com/en-us/partners-services/services/support.html) tooget estos valores.</span><span class="sxs-lookup"><span data-stu-id="cc0ab-165">Contact [Workday Client support team](https://www.workday.com/en-us/partners-services/services/support.html) tooget these values.</span></span> 
 

4. <span data-ttu-id="cc0ab-166">En hello **el certificado de firma de SAML** sección, haga clic en **certificado (Base64)** y, a continuación, guarde el archivo de certificado de hello en el equipo.</span><span class="sxs-lookup"><span data-stu-id="cc0ab-166">On hello **SAML Signing Certificate** section, click **Certificate (Base64)** and then save hello certificate file on your computer.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-workday-tutorial/tutorial_workday_certificate.png) 

5. <span data-ttu-id="cc0ab-168">Haga clic en el botón **Guardar** .</span><span class="sxs-lookup"><span data-stu-id="cc0ab-168">Click **Save** button.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-workday-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="cc0ab-170">En hello **configuración de Workday** sección, haga clic en **configurar Workday** tooopen **configurar inicio de sesión** ventana.</span><span class="sxs-lookup"><span data-stu-id="cc0ab-170">On hello **Workday Configuration** section, click **Configure Workday** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="cc0ab-171">Hola copia **dirección URL de cierre de sesión, Id. de entidad de SAML y SAML Single Sign-On dirección URL del servicio** de hello **sección de referencia rápida.**</span><span class="sxs-lookup"><span data-stu-id="cc0ab-171">Copy hello **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    <span data-ttu-id="cc0ab-172">![Configuración del inicio de sesión único](./media/active-directory-saas-workday-tutorial/tutorial_workday_configure.png) 
<CS></span><span class="sxs-lookup"><span data-stu-id="cc0ab-172">![Configure Single Sign-On](./media/active-directory-saas-workday-tutorial/tutorial_workday_configure.png) 
<CS></span></span>
7. <span data-ttu-id="cc0ab-173">En una ventana del explorador web diferente, inicie sesión en el sitio de la compañía Workday tooyour como administrador.</span><span class="sxs-lookup"><span data-stu-id="cc0ab-173">In a different web browser window, log in tooyour Workday company site as an administrator.</span></span>

8. <span data-ttu-id="cc0ab-174">Vaya demasiado**menú \> Workbench**.</span><span class="sxs-lookup"><span data-stu-id="cc0ab-174">Go too**Menu \> Workbench**.</span></span>
   
    <span data-ttu-id="cc0ab-175">![Workbench](./media/active-directory-saas-workday-tutorial/IC782923.png "Workbench")</span><span class="sxs-lookup"><span data-stu-id="cc0ab-175">![Workbench](./media/active-directory-saas-workday-tutorial/IC782923.png "Workbench")</span></span>

9. <span data-ttu-id="cc0ab-176">Vaya demasiado**administración de cuentas**.</span><span class="sxs-lookup"><span data-stu-id="cc0ab-176">Go too**Account Administration**.</span></span>
   
    <span data-ttu-id="cc0ab-177">![Administración de cuentas](./media/active-directory-saas-workday-tutorial/IC782924.png "Administración de cuentas")</span><span class="sxs-lookup"><span data-stu-id="cc0ab-177">![Account Administration](./media/active-directory-saas-workday-tutorial/IC782924.png "Account Administration")</span></span>

10. <span data-ttu-id="cc0ab-178">Vaya demasiado**Editar configuración de inquilino – seguridad**.</span><span class="sxs-lookup"><span data-stu-id="cc0ab-178">Go too**Edit Tenant Setup – Security**.</span></span>
   
    <span data-ttu-id="cc0ab-179">![Edición de seguridad del inquilino](./media/active-directory-saas-workday-tutorial/IC782925.png "Edición de seguridad del inquilino")</span><span class="sxs-lookup"><span data-stu-id="cc0ab-179">![Edit Tenant Security](./media/active-directory-saas-workday-tutorial/IC782925.png "Edit Tenant Security")</span></span>

11. <span data-ttu-id="cc0ab-180">Hola **direcciones URL de redirección** sección, lleve a cabo Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="cc0ab-180">In hello **Redirection URLs** section, perform hello following steps:</span></span>
   
    <span data-ttu-id="cc0ab-181">![Direcciones URL de redirección](./media/active-directory-saas-workday-tutorial/IC7829581.png "Direcciones URL de redirección")</span><span class="sxs-lookup"><span data-stu-id="cc0ab-181">![Redirection URLs](./media/active-directory-saas-workday-tutorial/IC7829581.png "Redirection URLs")</span></span>
   
    <span data-ttu-id="cc0ab-182">a.</span><span class="sxs-lookup"><span data-stu-id="cc0ab-182">a.</span></span> <span data-ttu-id="cc0ab-183">Haga clic en **Add Row**(Agregar fila).</span><span class="sxs-lookup"><span data-stu-id="cc0ab-183">Click **Add Row**.</span></span>
   
    <span data-ttu-id="cc0ab-184">b.</span><span class="sxs-lookup"><span data-stu-id="cc0ab-184">b.</span></span> <span data-ttu-id="cc0ab-185">Hola **dirección URL de redireccionamiento de inicio de sesión** cuadro de texto hello y **dirección URL de redireccionamiento de Mobile** cuadro de texto, hello tipo **dirección URL de inicio de sesión** que ha escrito en hello **Workday dominio y Las direcciones URL** sección de hello portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="cc0ab-185">In hello **Login Redirect URL** textbox and hello **Mobile Redirect URL** textbox, type hello **Sign-on URL** you have entered on hello **Workday Domain and URLs** section of hello Azure portal.</span></span>
   
    <span data-ttu-id="cc0ab-186">c.</span><span class="sxs-lookup"><span data-stu-id="cc0ab-186">c.</span></span> <span data-ttu-id="cc0ab-187">En el portal de Azure, en Hola Hola **configurar inicio de sesión** ventana, Hola copia **dirección URL de cierre de sesión**y, a continuación, péguelo en hello **dirección URL de redireccionamiento de cierre de sesión** cuadro de texto.</span><span class="sxs-lookup"><span data-stu-id="cc0ab-187">In hello Azure portal, on hello **Configure sign-on** window, copy hello **Sign-Out URL**, and then paste it into hello **Logout Redirect URL** textbox.</span></span>
   
    <span data-ttu-id="cc0ab-188">d.</span><span class="sxs-lookup"><span data-stu-id="cc0ab-188">d.</span></span>  <span data-ttu-id="cc0ab-189">En **entorno** cuadro de texto, el nombre del entorno de tipo hello.</span><span class="sxs-lookup"><span data-stu-id="cc0ab-189">In **Environment** textbox, type hello environment name.</span></span>  

    >[!NOTE]
    > <span data-ttu-id="cc0ab-190">Hello valor del atributo de entorno Hola está ligado toohello valor de dirección URL del inquilino hello:</span><span class="sxs-lookup"><span data-stu-id="cc0ab-190">hello value of hello Environment attribute is tied toohello value of hello tenant URL:</span></span>  
    ><span data-ttu-id="cc0ab-191">-Si nombre de dominio de Hola de URL de inquilino de Workday Hola comienza con impl por ejemplo: *https://impl.workday.com/\<inquilino\>/login-saml2.htmld*), hello **entorno** debe establecer el atributo tooImplementation.</span><span class="sxs-lookup"><span data-stu-id="cc0ab-191">-If hello domain name of hello Workday tenant URL starts with impl for example: *https://impl.workday.com/\<tenant\>/login-saml2.htmld*), hello **Environment** attribute must be set tooImplementation.</span></span>  
    ><span data-ttu-id="cc0ab-192">-Si el nombre de dominio de hello empieza por algo más, necesita toocontact [equipo de soporte técnico de Workday cliente](https://www.workday.com/en-us/partners-services/services/support.html) tooget Hola coincidencia **entorno** valor.</span><span class="sxs-lookup"><span data-stu-id="cc0ab-192">-If hello domain name starts with something else, you need toocontact [Workday Client support team](https://www.workday.com/en-us/partners-services/services/support.html) tooget hello matching **Environment** value.</span></span>

12. <span data-ttu-id="cc0ab-193">Hola **configuración de SAML** sección, lleve a cabo Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="cc0ab-193">In hello **SAML Setup** section, perform hello following steps:</span></span>
   
    <span data-ttu-id="cc0ab-194">![Configuración de SAML](./media/active-directory-saas-workday-tutorial/IC782926.png "Configuración de SAML")</span><span class="sxs-lookup"><span data-stu-id="cc0ab-194">![SAML Setup](./media/active-directory-saas-workday-tutorial/IC782926.png "SAML Setup")</span></span>
   
    <span data-ttu-id="cc0ab-195">a.</span><span class="sxs-lookup"><span data-stu-id="cc0ab-195">a.</span></span>  <span data-ttu-id="cc0ab-196">Seleccione **Enable SAML Authentication**(Habilitar autenticación SAML).</span><span class="sxs-lookup"><span data-stu-id="cc0ab-196">Select **Enable SAML Authentication**.</span></span>
   
    <span data-ttu-id="cc0ab-197">b.</span><span class="sxs-lookup"><span data-stu-id="cc0ab-197">b.</span></span>  <span data-ttu-id="cc0ab-198">Haga clic en **Add Row**(Agregar fila).</span><span class="sxs-lookup"><span data-stu-id="cc0ab-198">Click **Add Row**.</span></span>

13. <span data-ttu-id="cc0ab-199">Hola sección proveedores de identidades SAML, siga Hola siguiendo los pasos:</span><span class="sxs-lookup"><span data-stu-id="cc0ab-199">In hello SAML Identity Providers section, perform hello following steps:</span></span>
   
    <span data-ttu-id="cc0ab-200">![Proveedores de identidades SAML](./media/active-directory-saas-workday-tutorial/IC7829271.png "Proveedores de identidades SAML")</span><span class="sxs-lookup"><span data-stu-id="cc0ab-200">![SAML Identity Providers](./media/active-directory-saas-workday-tutorial/IC7829271.png "SAML Identity Providers")</span></span>
   
    <span data-ttu-id="cc0ab-201">a.</span><span class="sxs-lookup"><span data-stu-id="cc0ab-201">a.</span></span> <span data-ttu-id="cc0ab-202">En el cuadro de texto de nombre de proveedor de identidad de hello, escriba un nombre de proveedor (por ejemplo: *SPInitiatedSSO*).</span><span class="sxs-lookup"><span data-stu-id="cc0ab-202">In hello Identity Provider Name textbox, type a provider name (for example: *SPInitiatedSSO*).</span></span>
   
    <span data-ttu-id="cc0ab-203">b.</span><span class="sxs-lookup"><span data-stu-id="cc0ab-203">b.</span></span> <span data-ttu-id="cc0ab-204">En el portal de Azure, en Hola Hola **configurar inicio de sesión** ventana, Hola copia **Id. de entidad SAML** valor y, a continuación, péguelo en hello **emisor** cuadro de texto.</span><span class="sxs-lookup"><span data-stu-id="cc0ab-204">In hello Azure portal, on hello **Configure sign-on** window, copy hello **SAML Entity ID** value, and then paste it into hello **Issuer** textbox.</span></span>
   
    <span data-ttu-id="cc0ab-205">c.</span><span class="sxs-lookup"><span data-stu-id="cc0ab-205">c.</span></span> <span data-ttu-id="cc0ab-206">Seleccione **Enable Workday Initiated Logout** (Habilitar el cierre de sesión iniciado de Workday).</span><span class="sxs-lookup"><span data-stu-id="cc0ab-206">Select **Enable Workday Initiated Logout**.</span></span>
   
    <span data-ttu-id="cc0ab-207">d.</span><span class="sxs-lookup"><span data-stu-id="cc0ab-207">d.</span></span> <span data-ttu-id="cc0ab-208">En el portal de Azure, en Hola Hola **configurar inicio de sesión** ventana, Hola copia **dirección URL de cierre de sesión** valor y, a continuación, péguelo en hello **URL de solicitud de cierre de sesión** cuadro de texto.</span><span class="sxs-lookup"><span data-stu-id="cc0ab-208">In hello Azure portal, on hello **Configure sign-on** window, copy hello **Sign-Out URL** value, and then paste it into hello **Logout Request URL** textbox.</span></span>

    <span data-ttu-id="cc0ab-209">e.</span><span class="sxs-lookup"><span data-stu-id="cc0ab-209">e.</span></span> <span data-ttu-id="cc0ab-210">Haga clic en **Identity Provider Public Key Certificate** (Certificado de clave pública de proveedor de identidades) y, después, en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="cc0ab-210">Click **Identity Provider Public Key Certificate**, and then click **Create**.</span></span> 

    <span data-ttu-id="cc0ab-211">![Crear](./media/active-directory-saas-workday-tutorial/IC782928.png "Crear")</span><span class="sxs-lookup"><span data-stu-id="cc0ab-211">![Create](./media/active-directory-saas-workday-tutorial/IC782928.png "Create")</span></span>

    <span data-ttu-id="cc0ab-212">f.</span><span class="sxs-lookup"><span data-stu-id="cc0ab-212">f.</span></span> <span data-ttu-id="cc0ab-213">Haga clic en **Create x509 Public Key**(Crear clave pública x509).</span><span class="sxs-lookup"><span data-stu-id="cc0ab-213">Click **Create x509 Public Key**.</span></span> 

    <span data-ttu-id="cc0ab-214">![Crear](./media/active-directory-saas-workday-tutorial/IC782929.png "Crear")</span><span class="sxs-lookup"><span data-stu-id="cc0ab-214">![Create](./media/active-directory-saas-workday-tutorial/IC782929.png "Create")</span></span>


14. <span data-ttu-id="cc0ab-215">Hola **x509 ver clave pública** sección, lleve a cabo Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="cc0ab-215">In hello **View x509 Public Key** section, perform hello following steps:</span></span> 
   
    <span data-ttu-id="cc0ab-216">![Visualización de clave pública x509](./media/active-directory-saas-workday-tutorial/IC782930.png "Visualización de clave pública x509")</span><span class="sxs-lookup"><span data-stu-id="cc0ab-216">![View x509 Public Key](./media/active-directory-saas-workday-tutorial/IC782930.png "View x509 Public Key")</span></span> 
   
    <span data-ttu-id="cc0ab-217">a.</span><span class="sxs-lookup"><span data-stu-id="cc0ab-217">a.</span></span> <span data-ttu-id="cc0ab-218">Hola **nombre** cuadro de texto, escriba un nombre para el certificado (por ejemplo: *PPE\_SP*).</span><span class="sxs-lookup"><span data-stu-id="cc0ab-218">In hello **Name** textbox, type a name for your certificate (for example: *PPE\_SP*).</span></span>
   
    <span data-ttu-id="cc0ab-219">b.</span><span class="sxs-lookup"><span data-stu-id="cc0ab-219">b.</span></span> <span data-ttu-id="cc0ab-220">Hola **válido desde** cuadro de texto, hello de tipo válido de valor de atributo de su certificado.</span><span class="sxs-lookup"><span data-stu-id="cc0ab-220">In hello **Valid From** textbox, type hello valid from attribute value of your certificate.</span></span>
   
    <span data-ttu-id="cc0ab-221">c.</span><span class="sxs-lookup"><span data-stu-id="cc0ab-221">c.</span></span>  <span data-ttu-id="cc0ab-222">Hola **válido hasta** cuadro de texto, valor de tipo hello tooattribute válida de su certificado.</span><span class="sxs-lookup"><span data-stu-id="cc0ab-222">In hello **Valid To** textbox, type hello valid tooattribute value of your certificate.</span></span>
   
    > [!NOTE]
    > <span data-ttu-id="cc0ab-223">Puede obtener Hola válido de fecha y Hola toodate válida de hello Descargar certificado haciendo doble clic en él.</span><span class="sxs-lookup"><span data-stu-id="cc0ab-223">You can get hello valid from date and hello valid toodate from hello downloaded certificate by double-clicking it.</span></span>  <span data-ttu-id="cc0ab-224">aparecen las fechas de Hello en hello **detalles** ficha.</span><span class="sxs-lookup"><span data-stu-id="cc0ab-224">hello dates are listed under hello **Details** tab.</span></span>
    > 
    >
   
    <span data-ttu-id="cc0ab-225">d.</span><span class="sxs-lookup"><span data-stu-id="cc0ab-225">d.</span></span>  <span data-ttu-id="cc0ab-226">Abra el certificado codificado en base 64 en el Bloc de notas y, a continuación, Hola copia contenido del mismo.</span><span class="sxs-lookup"><span data-stu-id="cc0ab-226">Open your base-64 encoded certificate in notepad, and then copy hello content of it.</span></span>
   
    <span data-ttu-id="cc0ab-227">e.</span><span class="sxs-lookup"><span data-stu-id="cc0ab-227">e.</span></span>  <span data-ttu-id="cc0ab-228">Hola **certificado** cuadro de texto, contenido de hello Pegar del Portapapeles.</span><span class="sxs-lookup"><span data-stu-id="cc0ab-228">In hello **Certificate** textbox, paste hello content of your clipboard.</span></span>
   
    <span data-ttu-id="cc0ab-229">f.</span><span class="sxs-lookup"><span data-stu-id="cc0ab-229">f.</span></span>  <span data-ttu-id="cc0ab-230">Haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="cc0ab-230">Click **OK**.</span></span>

15. <span data-ttu-id="cc0ab-231">Lleve a cabo Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="cc0ab-231">Perform hello following steps:</span></span> 
   
    <span data-ttu-id="cc0ab-232">![Configuración de SSO](./media/active-directory-saas-workday-tutorial/WorkdaySSOConfiguratio.png "Configuración de SSO")</span><span class="sxs-lookup"><span data-stu-id="cc0ab-232">![SSO configuration](./media/active-directory-saas-workday-tutorial/WorkdaySSOConfiguratio.png "SSO configuration")</span></span>
   
    <span data-ttu-id="cc0ab-233">a.</span><span class="sxs-lookup"><span data-stu-id="cc0ab-233">a.</span></span>  <span data-ttu-id="cc0ab-234">Habilitar hello **x509 par de claves privada**.</span><span class="sxs-lookup"><span data-stu-id="cc0ab-234">Enable hello **x509 Private Key Pair**.</span></span>
   
    <span data-ttu-id="cc0ab-235">b.</span><span class="sxs-lookup"><span data-stu-id="cc0ab-235">b.</span></span>  <span data-ttu-id="cc0ab-236">Hola **Id. de proveedor de servicio** cuadro de texto, tipo **http://www.workday.com**.</span><span class="sxs-lookup"><span data-stu-id="cc0ab-236">In hello **Service Provider ID** textbox, type **http://www.workday.com**.</span></span>
   
    <span data-ttu-id="cc0ab-237">c.</span><span class="sxs-lookup"><span data-stu-id="cc0ab-237">c.</span></span>  <span data-ttu-id="cc0ab-238">Seleccione **Habilitar autenticación SAML iniciada por el proveedor de servicios**.</span><span class="sxs-lookup"><span data-stu-id="cc0ab-238">Select **Enable SP Initiated SAML Authentication**.</span></span>
   
    <span data-ttu-id="cc0ab-239">d.</span><span class="sxs-lookup"><span data-stu-id="cc0ab-239">d.</span></span>  <span data-ttu-id="cc0ab-240">En el portal de Azure, en Hola Hola **configurar inicio de sesión** ventana, Hola copia **SAML Single Sign-On dirección URL del servicio** valor y, a continuación, péguelo en hello **dirección URL de servicio de SSO IdP** cuadro de texto.</span><span class="sxs-lookup"><span data-stu-id="cc0ab-240">In hello Azure portal, on hello **Configure sign-on** window, copy hello **SAML Single Sign-On Service URL** value, and then paste it into hello **IdP SSO Service URL** textbox.</span></span>
   
    <span data-ttu-id="cc0ab-241">e.</span><span class="sxs-lookup"><span data-stu-id="cc0ab-241">e.</span></span> <span data-ttu-id="cc0ab-242">Seleccione **No desinflar la solicitud de autenticación iniciada por el SP**.</span><span class="sxs-lookup"><span data-stu-id="cc0ab-242">Select **Do Not Deflate SP-initiated Authentication Request**.</span></span>
   
    <span data-ttu-id="cc0ab-243">f.</span><span class="sxs-lookup"><span data-stu-id="cc0ab-243">f.</span></span> <span data-ttu-id="cc0ab-244">Como **Método de firma de solicitud de autenticación**, seleccione **SHA256**.</span><span class="sxs-lookup"><span data-stu-id="cc0ab-244">As **Authentication Request Signature Method**, select **SHA256**.</span></span> 
   
    <span data-ttu-id="cc0ab-245">![Método de firma de solicitud de autenticación](./media/active-directory-saas-workday-tutorial/WorkdaySSOConfiguration.png "Método de firma de solicitud de autenticación")</span><span class="sxs-lookup"><span data-stu-id="cc0ab-245">![Authentication Request Signature Method](./media/active-directory-saas-workday-tutorial/WorkdaySSOConfiguration.png "Authentication Request Signature Method")</span></span> 
   
    <span data-ttu-id="cc0ab-246">g.</span><span class="sxs-lookup"><span data-stu-id="cc0ab-246">g.</span></span> <span data-ttu-id="cc0ab-247">Haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="cc0ab-247">Click **OK**.</span></span> 
   
    <span data-ttu-id="cc0ab-248">![ACEPTAR](./media/active-directory-saas-workday-tutorial/IC782933.png "OK")
<CE></span><span class="sxs-lookup"><span data-stu-id="cc0ab-248">![OK](./media/active-directory-saas-workday-tutorial/IC782933.png "OK")
<CE></span></span>

> [!TIP]
> <span data-ttu-id="cc0ab-249">Ahora puede leer una versión concisa de estas instrucciones dentro de hello [portal de Azure](https://portal.azure.com), mientras que está configurando la aplicación hello!</span><span class="sxs-lookup"><span data-stu-id="cc0ab-249">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="cc0ab-250">Después de agregar esta aplicación de hello **Active Directory > aplicaciones empresariales** sección, simplemente haga clic en hello **Single Sign-On** Hola de pestaña y acceso incrustado documentación a través de hello  **Configuración** sección final Hola.</span><span class="sxs-lookup"><span data-stu-id="cc0ab-250">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="cc0ab-251">Puede leer más acerca de características de documentación de embedded Hola aquí: [Azure AD incrustado documentación]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="cc0ab-251">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="cc0ab-252">Creación de un usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="cc0ab-252">Creating an Azure AD test user</span></span>
<span data-ttu-id="cc0ab-253">objetivo de Hola de esta sección es un usuario de prueba en hello Azure portal llamado a Britta Simon toocreate.</span><span class="sxs-lookup"><span data-stu-id="cc0ab-253">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Creación de un usuario de Azure AD][100]

<span data-ttu-id="cc0ab-255">**toocreate un usuario de prueba en Azure AD, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="cc0ab-255">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="cc0ab-256">Hola **portal de Azure**, en Hola panel de navegación izquierdo, haga clic en **Azure Active Directory** icono.</span><span class="sxs-lookup"><span data-stu-id="cc0ab-256">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-workday-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="cc0ab-258">lista de hello toodisplay de usuarios, vaya demasiado**usuarios y grupos** y haga clic en **todos los usuarios**.</span><span class="sxs-lookup"><span data-stu-id="cc0ab-258">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-workday-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="cc0ab-260">Hola tooopen **usuario** cuadro de diálogo, haga clic en **agregar** en la parte superior de saludo del cuadro de diálogo de Hola.</span><span class="sxs-lookup"><span data-stu-id="cc0ab-260">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-workday-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="cc0ab-262">En hello **usuario** cuadro de diálogo, siga los pasos de hello:</span><span class="sxs-lookup"><span data-stu-id="cc0ab-262">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-workday-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="cc0ab-264">a.</span><span class="sxs-lookup"><span data-stu-id="cc0ab-264">a.</span></span> <span data-ttu-id="cc0ab-265">Hola **nombre** cuadro de texto, tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="cc0ab-265">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="cc0ab-266">b.</span><span class="sxs-lookup"><span data-stu-id="cc0ab-266">b.</span></span> <span data-ttu-id="cc0ab-267">Hola **nombre de usuario** cuadro de texto, hello tipo **dirección de correo electrónico** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="cc0ab-267">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="cc0ab-268">c.</span><span class="sxs-lookup"><span data-stu-id="cc0ab-268">c.</span></span> <span data-ttu-id="cc0ab-269">Seleccione **Mostrar contraseña** y anote el valor de Hola de hello **contraseña**.</span><span class="sxs-lookup"><span data-stu-id="cc0ab-269">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="cc0ab-270">d.</span><span class="sxs-lookup"><span data-stu-id="cc0ab-270">d.</span></span> <span data-ttu-id="cc0ab-271">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="cc0ab-271">Click **Create**.</span></span>
 
### <a name="creating-a-workday-test-user"></a><span data-ttu-id="cc0ab-272">Creación de un usuario de prueba de Workday</span><span class="sxs-lookup"><span data-stu-id="cc0ab-272">Creating a Workday test user</span></span>

<span data-ttu-id="cc0ab-273">tooget un usuario de prueba aprovisionado en Workday, deberá hello toocontact [equipo de soporte técnico de Workday cliente](https://www.workday.com/en-us/partners-services/services/support.html).</span><span class="sxs-lookup"><span data-stu-id="cc0ab-273">tooget a test user provisioned into Workday, you need toocontact hello [Workday Client support team](https://www.workday.com/en-us/partners-services/services/support.html).</span></span>
<span data-ttu-id="cc0ab-274">Hola [equipo de soporte técnico de Workday cliente](https://www.workday.com/en-us/partners-services/services/support.html) crea usuario Hola para usted.</span><span class="sxs-lookup"><span data-stu-id="cc0ab-274">hello [Workday Client support team](https://www.workday.com/en-us/partners-services/services/support.html) creates hello user for you.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="cc0ab-275">Asignación de usuario de prueba de hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="cc0ab-275">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="cc0ab-276">En esta sección, se habilita Britta Simon toouse un inicio de sesión único Azure concediendo acceso tooWorkday.</span><span class="sxs-lookup"><span data-stu-id="cc0ab-276">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooWorkday.</span></span>

![Asignar usuario][200] 

<span data-ttu-id="cc0ab-278">**tooassign Britta Simon tooWorkday, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="cc0ab-278">**tooassign Britta Simon tooWorkday, perform hello following steps:**</span></span>

1. <span data-ttu-id="cc0ab-279">Hola portal de Azure, abra la vista de aplicaciones de hello y, a continuación, navegue a vista de directorio toohello y vaya demasiado**aplicaciones empresariales** , a continuación, haga clic en **todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="cc0ab-279">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Asignar usuario][201] 

2. <span data-ttu-id="cc0ab-281">En la lista de aplicaciones de hello, seleccione **Workday**.</span><span class="sxs-lookup"><span data-stu-id="cc0ab-281">In hello applications list, select **Workday**.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-workday-tutorial/tutorial_workday_app.png) 

3. <span data-ttu-id="cc0ab-283">En el menú de Hola Hola izquierda, haga clic en **usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="cc0ab-283">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Asignar usuario][202] 

4. <span data-ttu-id="cc0ab-285">Haga clic en el botón **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="cc0ab-285">Click **Add** button.</span></span> <span data-ttu-id="cc0ab-286">Después, seleccione **Usuarios y grupos** en el cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="cc0ab-286">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Asignar usuario][203]

5. <span data-ttu-id="cc0ab-288">En **usuarios y grupos** cuadro de diálogo, seleccione **Britta Simon** en la lista de usuarios de Hola.</span><span class="sxs-lookup"><span data-stu-id="cc0ab-288">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="cc0ab-289">Haga clic en el botón **Seleccionar** del cuadro de diálogo **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="cc0ab-289">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="cc0ab-290">Haga clic en el botón **Asignar** del cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="cc0ab-290">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="cc0ab-291">Prueba del inicio de sesión único </span><span class="sxs-lookup"><span data-stu-id="cc0ab-291">Testing single sign-on</span></span>

<span data-ttu-id="cc0ab-292">Si desea tootest las opciones de inicio de sesión único, abra Hola Panel de acceso.</span><span class="sxs-lookup"><span data-stu-id="cc0ab-292">If you want tootest your single sign-on settings, open hello Access Panel.</span></span> <span data-ttu-id="cc0ab-293">Para obtener más información acerca de hello Panel de acceso, consulte [Introducción toohello Panel de acceso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="cc0ab-293">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="cc0ab-294">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="cc0ab-294">Additional resources</span></span>

* [<span data-ttu-id="cc0ab-295">Lista de tutoriales sobre cómo tooIntegrate aplicaciones de SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="cc0ab-295">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="cc0ab-296">¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="cc0ab-296">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)
* [<span data-ttu-id="cc0ab-297">Configuración del aprovisionamiento de usuarios</span><span class="sxs-lookup"><span data-stu-id="cc0ab-297">Configure User Provisioning</span></span>](active-directory-saas-workday-inbound-tutorial.md)



<!--Image references-->

[1]: ./media/active-directory-saas-workday-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-workday-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-workday-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-workday-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-workday-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-workday-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-workday-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-workday-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-workday-tutorial/tutorial_general_203.png

