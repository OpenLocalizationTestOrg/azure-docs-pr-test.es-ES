---
title: "Tutorial: Integración de Azure Active Directory con Lecorpio | Microsoft Docs"
description: "Obtenga información acerca de cómo tooconfigure inicio de sesión único entre Azure Active Directory y Lecorpio."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 28acce3e-22a0-4a37-8b66-6e518d777350
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/02/2017
ms.author: jeedes
ms.openlocfilehash: 963eb36678c589f942f63c7ab555161255324717
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-lecorpio"></a><span data-ttu-id="bfb81-103">Tutorial: Integración de Azure Active Directory con Lecorpio</span><span class="sxs-lookup"><span data-stu-id="bfb81-103">Tutorial: Azure Active Directory integration with Lecorpio</span></span>

<span data-ttu-id="bfb81-104">En este tutorial, aprenderá cómo toointegrate Lecorpio con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="bfb81-104">In this tutorial, you learn how toointegrate Lecorpio with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="bfb81-105">Integración Lecorpio con Azure AD proporciona Hola siguientes ventajas:</span><span class="sxs-lookup"><span data-stu-id="bfb81-105">Integrating Lecorpio with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="bfb81-106">Puede controlar en Azure AD que tenga acceso tooLecorpio</span><span class="sxs-lookup"><span data-stu-id="bfb81-106">You can control in Azure AD who has access tooLecorpio</span></span>
- <span data-ttu-id="bfb81-107">Puede habilitar los usuarios tooautomatically get ha iniciado sesión tooLecorpio (Single Sign-On) con sus cuentas de Azure AD</span><span class="sxs-lookup"><span data-stu-id="bfb81-107">You can enable your users tooautomatically get signed-on tooLecorpio (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="bfb81-108">Puede administrar las cuentas en una ubicación central: Hola portal de Azure</span><span class="sxs-lookup"><span data-stu-id="bfb81-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="bfb81-109">Si desea obtener más información acerca de la integración de aplicaciones de SaaS con Azure AD tooknow, consulte [¿qué es acceso a la aplicación y el inicio de sesión único con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="bfb81-109">If you want tooknow more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="bfb81-110">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="bfb81-110">Prerequisites</span></span>

<span data-ttu-id="bfb81-111">integración de Azure AD con Lecorpio tooconfigure, necesita Hola siguientes elementos:</span><span class="sxs-lookup"><span data-stu-id="bfb81-111">tooconfigure Azure AD integration with Lecorpio, you need hello following items:</span></span>

- <span data-ttu-id="bfb81-112">Una suscripción de Azure AD</span><span class="sxs-lookup"><span data-stu-id="bfb81-112">An Azure AD subscription</span></span>
- <span data-ttu-id="bfb81-113">Una suscripción habilitada para inicio de sesión único en Lecorpio.</span><span class="sxs-lookup"><span data-stu-id="bfb81-113">A Lecorpio single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="bfb81-114">Hola tootest los pasos de este tutorial, no se recomienda usar un entorno de producción.</span><span class="sxs-lookup"><span data-stu-id="bfb81-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="bfb81-115">pasos de hello tootest en este tutorial, debe seguir estas recomendaciones:</span><span class="sxs-lookup"><span data-stu-id="bfb81-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="bfb81-116">No use el entorno de producción, salvo que sea necesario.</span><span class="sxs-lookup"><span data-stu-id="bfb81-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="bfb81-117">Si no dispone de un entorno de prueba de Azure AD, puede obtener una versión de prueba de un mes [aquí](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="bfb81-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="bfb81-118">Descripción del escenario</span><span class="sxs-lookup"><span data-stu-id="bfb81-118">Scenario description</span></span>
<span data-ttu-id="bfb81-119">En este tutorial, puede probar el inicio de sesión único de Azure AD en un entorno de prueba.</span><span class="sxs-lookup"><span data-stu-id="bfb81-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="bfb81-120">escenario de Hello descrito en este tutorial consta de dos bloques principales:</span><span class="sxs-lookup"><span data-stu-id="bfb81-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="bfb81-121">Agregar Lecorpio desde la Galería de Hola</span><span class="sxs-lookup"><span data-stu-id="bfb81-121">Adding Lecorpio from hello gallery</span></span>
2. <span data-ttu-id="bfb81-122">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="bfb81-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-lecorpio-from-hello-gallery"></a><span data-ttu-id="bfb81-123">Agregar Lecorpio desde la Galería de Hola</span><span class="sxs-lookup"><span data-stu-id="bfb81-123">Adding Lecorpio from hello gallery</span></span>
<span data-ttu-id="bfb81-124">integración de hello tooconfigure de Lecorpio en Azure AD, deberá tooadd Lecorpio de lista de tooyour Hola Galería de aplicaciones administradas de SaaS.</span><span class="sxs-lookup"><span data-stu-id="bfb81-124">tooconfigure hello integration of Lecorpio into Azure AD, you need tooadd Lecorpio from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="bfb81-125">**tooadd Lecorpio de galería de hello, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="bfb81-125">**tooadd Lecorpio from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="bfb81-126">Hola  **[portal de Azure](https://portal.azure.com)**, en el panel de navegación izquierdo de Hola, haga clic en **Azure Active Directory** icono.</span><span class="sxs-lookup"><span data-stu-id="bfb81-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="bfb81-128">Navegue demasiado**aplicaciones empresariales**.</span><span class="sxs-lookup"><span data-stu-id="bfb81-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="bfb81-129">A continuación, vaya demasiado**todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="bfb81-129">Then go too**All applications**.</span></span>

    ![Aplicaciones][2]
    
3. <span data-ttu-id="bfb81-131">Haga clic en **nueva aplicación** botón en la parte superior de saludo del cuadro de diálogo de Hola.</span><span class="sxs-lookup"><span data-stu-id="bfb81-131">Click **New application** button on hello top of hello dialog.</span></span>

    ![Aplicaciones][3]

4. <span data-ttu-id="bfb81-133">En el cuadro de búsqueda de hello, escriba **Lecorpio**.</span><span class="sxs-lookup"><span data-stu-id="bfb81-133">In hello search box, type **Lecorpio**.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-lecorpio-tutorial/tutorial_lecorpio_search.png)

5. <span data-ttu-id="bfb81-135">En el panel de resultados de hello, seleccione **Lecorpio**y, a continuación, haga clic en **agregar** botón aplicación hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="bfb81-135">In hello results panel, select **Lecorpio**, and then click **Add** button tooadd hello application.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-lecorpio-tutorial/tutorial_lecorpio_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="bfb81-137">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="bfb81-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="bfb81-138">En esta sección, podrá configurar y probar el inicio de sesión único de Azure AD con Lecorpio con un usuario de prueba llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="bfb81-138">In this section, you configure and test Azure AD single sign-on with Lecorpio based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="bfb81-139">Para toowork de inicio de sesión único, Azure AD necesita tooknow qué usuario equivalente de hello en Lecorpio es tooa usuario en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="bfb81-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Lecorpio is tooa user in Azure AD.</span></span> <span data-ttu-id="bfb81-140">En otras palabras, una relación de vínculo entre un usuario de Azure AD y el usuario relacionado de hello en Lecorpio debe toobe establecido.</span><span class="sxs-lookup"><span data-stu-id="bfb81-140">In other words, a link relationship between an Azure AD user and hello related user in Lecorpio needs toobe established.</span></span>

<span data-ttu-id="bfb81-141">Esta relación de vínculo se establece mediante la asignación de valor de Hola de hello **nombre de usuario** en Azure AD como valor de Hola de hello **nombre de usuario** en Lecorpio.</span><span class="sxs-lookup"><span data-stu-id="bfb81-141">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in Lecorpio.</span></span>

<span data-ttu-id="bfb81-142">tooconfigure y prueba de inicio de sesión único en Azure AD con Lecorpio, deberá hello toocomplete después de bloques de creación:</span><span class="sxs-lookup"><span data-stu-id="bfb81-142">tooconfigure and test Azure AD single sign-on with Lecorpio, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="bfb81-143">**[Configuración de Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable la toouse usuarios esta característica.</span><span class="sxs-lookup"><span data-stu-id="bfb81-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="bfb81-144">**[Crear un usuario de prueba de Azure AD](#creating-an-azure-ad-test-user)**  -inicio de sesión único en Azure AD tootest con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="bfb81-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="bfb81-145">**[Crear un usuario de prueba Lecorpio](#creating-a-lecorpio-test-user)**  -toohave un equivalente de Britta Simon en Lecorpio que es la representación toohello vinculado Azure AD del usuario.</span><span class="sxs-lookup"><span data-stu-id="bfb81-145">**[Creating a Lecorpio test user](#creating-a-lecorpio-test-user)** - toohave a counterpart of Britta Simon in Lecorpio that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="bfb81-146">**[Asignar usuario de prueba de hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="bfb81-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="bfb81-147">**[Pruebas de Single Sign-On](#testing-single-sign-on)**  -tooverify Hola si funciona la configuración.</span><span class="sxs-lookup"><span data-stu-id="bfb81-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="bfb81-148">Configuración del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="bfb81-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="bfb81-149">En esta sección, habilitar inicio de sesión único en Azure AD en hello portal de Azure y configurar el inicio de sesión único en la aplicación Lecorpio.</span><span class="sxs-lookup"><span data-stu-id="bfb81-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Lecorpio application.</span></span>

<span data-ttu-id="bfb81-150">**inicio de sesión único en Azure AD tooconfigure con Lecorpio, realizar Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="bfb81-150">**tooconfigure Azure AD single sign-on with Lecorpio, perform hello following steps:**</span></span>

1. <span data-ttu-id="bfb81-151">En el portal de Azure, en Hola Hola **Lecorpio** página de integración de aplicaciones, haga clic en **inicio de sesión único**.</span><span class="sxs-lookup"><span data-stu-id="bfb81-151">In hello Azure portal, on hello **Lecorpio** application integration page, click **Single sign-on**.</span></span>

    ![Configurar inicio de sesión único][4]

2. <span data-ttu-id="bfb81-153">En hello **inicio de sesión único** cuadro de diálogo, seleccione **modo** como **sesión basado en SAML** tooenable inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="bfb81-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurar inicio de sesión único](./media/active-directory-saas-lecorpio-tutorial/tutorial_lecorpio_samlbase.png)

3. <span data-ttu-id="bfb81-155">En hello **Lecorpio dominio y las direcciones URL** sección, lleve a cabo Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="bfb81-155">On hello **Lecorpio Domain and URLs** section, perform hello following steps:</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-lecorpio-tutorial/tutorial_lecorpio_url.png)

    <span data-ttu-id="bfb81-157">a.</span><span class="sxs-lookup"><span data-stu-id="bfb81-157">a.</span></span> <span data-ttu-id="bfb81-158">Hola **dirección URL de inicio de sesión** cuadro de texto, valor de tipo hello mediante Hola sigue el patrón:`https://<instance name>.lecorpio.com/<customer name>`</span><span class="sxs-lookup"><span data-stu-id="bfb81-158">In hello **Sign-on URL** textbox, type hello value using hello following pattern: `https://<instance name>.lecorpio.com/<customer name>`</span></span>

    <span data-ttu-id="bfb81-159">b.</span><span class="sxs-lookup"><span data-stu-id="bfb81-159">b.</span></span> <span data-ttu-id="bfb81-160">Hola **identificador** cuadro de texto, escriba una dirección URL usando Hola siguiente patrón:`https://<instance name>.lecorpio.com/<customer name>`</span><span class="sxs-lookup"><span data-stu-id="bfb81-160">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<instance name>.lecorpio.com/<customer name>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="bfb81-161">Estos valores no son Hola real.</span><span class="sxs-lookup"><span data-stu-id="bfb81-161">These values are not hello real.</span></span> <span data-ttu-id="bfb81-162">Actualizar estos valores con URL de inicio de sesión real de Hola y el identificador.</span><span class="sxs-lookup"><span data-stu-id="bfb81-162">Update these values with hello actual Sign-on URL and Identifier.</span></span> <span data-ttu-id="bfb81-163">Aquí le sugerimos toouse Hola único valor de cadena en hello identificador.</span><span class="sxs-lookup"><span data-stu-id="bfb81-163">Here we suggest you toouse hello unique value of string in hello Identifier.</span></span> <span data-ttu-id="bfb81-164">Póngase en contacto con [equipo de soporte técnico de cliente de Lecorpio](mailto:info@lecorpio.com) tooget estos valores.</span><span class="sxs-lookup"><span data-stu-id="bfb81-164">Contact [Lecorpio Client support team](mailto:info@lecorpio.com) tooget these values.</span></span> 
 
4. <span data-ttu-id="bfb81-165">En hello **el certificado de firma de SAML** sección, haga clic en **Metadata XML** y, a continuación, guarde el archivo de metadatos de hello en el equipo.</span><span class="sxs-lookup"><span data-stu-id="bfb81-165">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-lecorpio-tutorial/tutorial_lecorpio_certificate.png) 

5. <span data-ttu-id="bfb81-167">Haga clic en el botón **Guardar** .</span><span class="sxs-lookup"><span data-stu-id="bfb81-167">Click **Save** button.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-lecorpio-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="bfb81-169">tooconfigure inicio de sesión único en **Lecorpio** lado, necesita hello toosend descargado **Metadata XML** demasiado[equipo de soporte técnico de Lecorpio](mailto:info@lecorpio.com).</span><span class="sxs-lookup"><span data-stu-id="bfb81-169">tooconfigure single sign-on on **Lecorpio** side, you need toosend hello downloaded **Metadata XML** too[Lecorpio support team](mailto:info@lecorpio.com).</span></span>

> [!TIP]
> <span data-ttu-id="bfb81-170">Ahora puede leer una versión concisa de estas instrucciones dentro de hello [portal de Azure](https://portal.azure.com), mientras que está configurando la aplicación hello!</span><span class="sxs-lookup"><span data-stu-id="bfb81-170">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="bfb81-171">Después de agregar esta aplicación de hello **Active Directory > aplicaciones empresariales** sección, simplemente haga clic en hello **Single Sign-On** Hola de pestaña y acceso incrustado documentación a través de hello  **Configuración** sección final Hola.</span><span class="sxs-lookup"><span data-stu-id="bfb81-171">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="bfb81-172">Puede leer más acerca de características de documentación de embedded Hola aquí: [Azure AD incrustado documentación]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="bfb81-172">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="bfb81-173">Creación de un usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="bfb81-173">Creating an Azure AD test user</span></span>
<span data-ttu-id="bfb81-174">objetivo de Hola de esta sección es un usuario de prueba en hello Azure portal llamado a Britta Simon toocreate.</span><span class="sxs-lookup"><span data-stu-id="bfb81-174">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Creación de un usuario de Azure AD][100]

<span data-ttu-id="bfb81-176">**toocreate un usuario de prueba en Azure AD, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="bfb81-176">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="bfb81-177">Hola **portal de Azure**, en Hola panel de navegación izquierdo, haga clic en **Azure Active Directory** icono.</span><span class="sxs-lookup"><span data-stu-id="bfb81-177">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-lecorpio-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="bfb81-179">Vaya demasiado**usuarios y grupos** y haga clic en **todos los usuarios** toodisplay lista de Hola de usuarios.</span><span class="sxs-lookup"><span data-stu-id="bfb81-179">Go too**Users and groups** and click **All users** toodisplay hello list of users.</span></span>
    
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-lecorpio-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="bfb81-181">En la parte superior de saludo del cuadro de diálogo de hello, haga clic en **agregar** tooopen hello **usuario** cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="bfb81-181">At hello top of hello dialog, click **Add** tooopen hello **User** dialog.</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-lecorpio-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="bfb81-183">En hello **usuario** cuadro de diálogo, siga los pasos de hello:</span><span class="sxs-lookup"><span data-stu-id="bfb81-183">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-lecorpio-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="bfb81-185">a.</span><span class="sxs-lookup"><span data-stu-id="bfb81-185">a.</span></span> <span data-ttu-id="bfb81-186">Hola **nombre** cuadro de texto, tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="bfb81-186">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="bfb81-187">b.</span><span class="sxs-lookup"><span data-stu-id="bfb81-187">b.</span></span> <span data-ttu-id="bfb81-188">Hola **nombre de usuario** cuadro de texto, hello tipo **dirección de correo electrónico** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="bfb81-188">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="bfb81-189">c.</span><span class="sxs-lookup"><span data-stu-id="bfb81-189">c.</span></span> <span data-ttu-id="bfb81-190">Seleccione **Mostrar contraseña** y anote el valor de Hola de hello **contraseña**.</span><span class="sxs-lookup"><span data-stu-id="bfb81-190">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="bfb81-191">d.</span><span class="sxs-lookup"><span data-stu-id="bfb81-191">d.</span></span> <span data-ttu-id="bfb81-192">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="bfb81-192">Click **Create**.</span></span>
 
### <a name="creating-a-lecorpio-test-user"></a><span data-ttu-id="bfb81-193">Creación de un usuario de prueba de Lecorpio</span><span class="sxs-lookup"><span data-stu-id="bfb81-193">Creating a Lecorpio test user</span></span>

<span data-ttu-id="bfb81-194">En esta sección, creará un usuario llamado Britta Simon en Lecorpio.</span><span class="sxs-lookup"><span data-stu-id="bfb81-194">In this section, you create a user called Britta Simon in Lecorpio.</span></span> 

<span data-ttu-id="bfb81-195">Póngase en contacto con [equipo de soporte técnico de Lecorpio cliente](mailto:info@lecorpio.com) a los usuarios de tooadd Hola Hola Lecorpio aplicación.</span><span class="sxs-lookup"><span data-stu-id="bfb81-195">Contact [Lecorpio Client support team](mailto:info@lecorpio.com) tooadd hello users in hello Lecorpio application.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="bfb81-196">Asignación de usuario de prueba de hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="bfb81-196">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="bfb81-197">En esta sección, se habilita Britta Simon toouse un inicio de sesión único Azure concediendo acceso tooLecorpio.</span><span class="sxs-lookup"><span data-stu-id="bfb81-197">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooLecorpio.</span></span>

![Asignar usuario][200] 

<span data-ttu-id="bfb81-199">**tooassign Britta Simon tooLecorpio, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="bfb81-199">**tooassign Britta Simon tooLecorpio, perform hello following steps:**</span></span>

1. <span data-ttu-id="bfb81-200">Hola portal de Azure, abra la vista de aplicaciones de hello y, a continuación, navegue a vista de directorio toohello y vaya demasiado**aplicaciones empresariales** , a continuación, haga clic en **todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="bfb81-200">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Asignar usuario][201] 

2. <span data-ttu-id="bfb81-202">En la lista de aplicaciones de hello, seleccione **Lecorpio**.</span><span class="sxs-lookup"><span data-stu-id="bfb81-202">In hello applications list, select **Lecorpio**.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-lecorpio-tutorial/tutorial_lecorpio_app.png) 

3. <span data-ttu-id="bfb81-204">En el menú de Hola Hola izquierda, haga clic en **usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="bfb81-204">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Asignar usuario][202] 

4. <span data-ttu-id="bfb81-206">Haga clic en el botón **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="bfb81-206">Click **Add** button.</span></span> <span data-ttu-id="bfb81-207">Después, seleccione **Usuarios y grupos** en el cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="bfb81-207">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Asignar usuario][203]

5. <span data-ttu-id="bfb81-209">En **usuarios y grupos** cuadro de diálogo, seleccione **Britta Simon** en la lista de usuarios de Hola.</span><span class="sxs-lookup"><span data-stu-id="bfb81-209">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="bfb81-210">Haga clic en el botón **Seleccionar** del cuadro de diálogo **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="bfb81-210">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="bfb81-211">Haga clic en el botón **Asignar** del cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="bfb81-211">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="bfb81-212">Prueba del inicio de sesión único </span><span class="sxs-lookup"><span data-stu-id="bfb81-212">Testing single sign-on</span></span>

<span data-ttu-id="bfb81-213">En esta sección, comprobará su único inicio de sesión en configuración de Azure AD con hello Panel de acceso.</span><span class="sxs-lookup"><span data-stu-id="bfb81-213">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="bfb81-214">Al hacer clic en icono de Lecorpio Hola Hola Panel de acceso, deberá obtener automáticamente ha iniciado sesión tooyour Lecorpio aplicación.</span><span class="sxs-lookup"><span data-stu-id="bfb81-214">When you click hello Lecorpio tile in hello Access Panel, you should get automatically signed-on tooyour Lecorpio application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="bfb81-215">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="bfb81-215">Additional resources</span></span>

* [<span data-ttu-id="bfb81-216">Lista de tutoriales sobre cómo tooIntegrate aplicaciones de SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="bfb81-216">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="bfb81-217">¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="bfb81-217">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-lecorpio-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-lecorpio-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-lecorpio-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-lecorpio-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-lecorpio-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-lecorpio-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-lecorpio-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-lecorpio-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-lecorpio-tutorial/tutorial_general_203.png

