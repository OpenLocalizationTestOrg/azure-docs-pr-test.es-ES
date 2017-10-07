---
title: "Tutorial: Integración de Azure Active Directory con Sciforma | Microsoft Docs"
description: "Obtenga información acerca de cómo tooconfigure inicio de sesión único entre Azure Active Directory y Sciforma."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: abbfb5ac-7687-4153-b263-8090102dae37
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/09/2017
ms.author: jeedes
ms.openlocfilehash: fca6237196061355e38d431e958964a45246f965
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-sciforma"></a><span data-ttu-id="f8239-103">Tutorial: Integración de Azure Active Directory con Sciforma</span><span class="sxs-lookup"><span data-stu-id="f8239-103">Tutorial: Azure Active Directory integration with Sciforma</span></span>

<span data-ttu-id="f8239-104">En este tutorial, aprenderá cómo toointegrate Sciforma con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="f8239-104">In this tutorial, you learn how toointegrate Sciforma with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="f8239-105">Integración Sciforma con Azure AD proporciona Hola siguientes ventajas:</span><span class="sxs-lookup"><span data-stu-id="f8239-105">Integrating Sciforma with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="f8239-106">Puede controlar en Azure AD que tenga acceso tooSciforma</span><span class="sxs-lookup"><span data-stu-id="f8239-106">You can control in Azure AD who has access tooSciforma</span></span>
- <span data-ttu-id="f8239-107">Puede habilitar los usuarios tooautomatically get ha iniciado sesión tooSciforma (Single Sign-On) con sus cuentas de Azure AD</span><span class="sxs-lookup"><span data-stu-id="f8239-107">You can enable your users tooautomatically get signed-on tooSciforma (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="f8239-108">Puede administrar las cuentas en una ubicación central: Hola portal de Azure</span><span class="sxs-lookup"><span data-stu-id="f8239-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="f8239-109">Si desea obtener más información acerca de la integración de aplicaciones de SaaS con Azure AD tooknow, consulte [¿qué es acceso a la aplicación y el inicio de sesión único con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="f8239-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="f8239-110">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="f8239-110">Prerequisites</span></span>

<span data-ttu-id="f8239-111">integración de Azure AD con Sciforma tooconfigure, necesita Hola siguientes elementos:</span><span class="sxs-lookup"><span data-stu-id="f8239-111">tooconfigure Azure AD integration with Sciforma, you need hello following items:</span></span>

- <span data-ttu-id="f8239-112">Una suscripción de Azure AD</span><span class="sxs-lookup"><span data-stu-id="f8239-112">An Azure AD subscription</span></span>
- <span data-ttu-id="f8239-113">Una suscripción habilitada para el inicio de sesión único en Sciforma</span><span class="sxs-lookup"><span data-stu-id="f8239-113">A Sciforma single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="f8239-114">Hola tootest los pasos de este tutorial, no se recomienda usar un entorno de producción.</span><span class="sxs-lookup"><span data-stu-id="f8239-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="f8239-115">pasos de hello tootest en este tutorial, debe seguir estas recomendaciones:</span><span class="sxs-lookup"><span data-stu-id="f8239-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="f8239-116">No use el entorno de producción, salvo que sea necesario.</span><span class="sxs-lookup"><span data-stu-id="f8239-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="f8239-117">Si no dispone de un entorno de prueba de Azure AD, puede obtener una versión de prueba de un mes [aquí](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="f8239-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="f8239-118">Descripción del escenario</span><span class="sxs-lookup"><span data-stu-id="f8239-118">Scenario description</span></span>
<span data-ttu-id="f8239-119">En este tutorial, puede probar el inicio de sesión único de Azure AD en un entorno de prueba.</span><span class="sxs-lookup"><span data-stu-id="f8239-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="f8239-120">escenario de Hello descrito en este tutorial consta de dos bloques principales:</span><span class="sxs-lookup"><span data-stu-id="f8239-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="f8239-121">Agregar Sciforma desde la Galería de Hola</span><span class="sxs-lookup"><span data-stu-id="f8239-121">Adding Sciforma from hello gallery</span></span>
2. <span data-ttu-id="f8239-122">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="f8239-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-sciforma-from-hello-gallery"></a><span data-ttu-id="f8239-123">Agregar Sciforma desde la Galería de Hola</span><span class="sxs-lookup"><span data-stu-id="f8239-123">Adding Sciforma from hello gallery</span></span>
<span data-ttu-id="f8239-124">integración de hello tooconfigure de Sciforma en Azure AD, deberá tooadd Sciforma de lista de tooyour Hola Galería de aplicaciones administradas de SaaS.</span><span class="sxs-lookup"><span data-stu-id="f8239-124">tooconfigure hello integration of Sciforma into Azure AD, you need tooadd Sciforma from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="f8239-125">**tooadd Sciforma de galería de hello, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="f8239-125">**tooadd Sciforma from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="f8239-126">Hola ** [portal de Azure](https://portal.azure.com)**, en el panel de navegación izquierdo de Hola, haga clic en **Azure Active Directory** icono.</span><span class="sxs-lookup"><span data-stu-id="f8239-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="f8239-128">Navegue demasiado**aplicaciones empresariales**.</span><span class="sxs-lookup"><span data-stu-id="f8239-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="f8239-129">A continuación, vaya demasiado**todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="f8239-129">Then go too**All applications**.</span></span>

    ![Aplicaciones][2]
    
3. <span data-ttu-id="f8239-131">tooadd nueva aplicación, haga clic en **nueva aplicación** botón en la parte superior de saludo del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="f8239-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Aplicaciones][3]

4. <span data-ttu-id="f8239-133">En el cuadro de búsqueda de hello, escriba **Sciforma**.</span><span class="sxs-lookup"><span data-stu-id="f8239-133">In hello search box, type **Sciforma**.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-sciforma-tutorial/tutorial_sciforma_search.png)

5. <span data-ttu-id="f8239-135">En el panel de resultados de hello, seleccione **Sciforma**y, a continuación, haga clic en **agregar** botón aplicación hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="f8239-135">In hello results panel, select **Sciforma**, and then click **Add** button tooadd hello application.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-sciforma-tutorial/tutorial_sciforma_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="f8239-137">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="f8239-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="f8239-138">En esta sección, podrá configurar y probar el inicio de sesión único de Azure AD con Sciforma con un usuario de prueba llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="f8239-138">In this section, you configure and test Azure AD single sign-on with Sciforma based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="f8239-139">Para toowork de inicio de sesión único, Azure AD necesita tooknow qué usuario equivalente de hello en Sciforma es tooa usuario en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="f8239-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Sciforma is tooa user in Azure AD.</span></span> <span data-ttu-id="f8239-140">En otras palabras, una relación de vínculo entre un usuario de Azure AD y el usuario relacionado de hello en Sciforma debe toobe establecido.</span><span class="sxs-lookup"><span data-stu-id="f8239-140">In other words, a link relationship between an Azure AD user and hello related user in Sciforma needs toobe established.</span></span>

<span data-ttu-id="f8239-141">En Sciforma, asigne el valor de Hola de hello **nombre de usuario** en Azure AD como valor de Hola de hello **nombre de usuario** tooestablish la relación de vínculo de Hola.</span><span class="sxs-lookup"><span data-stu-id="f8239-141">In Sciforma, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="f8239-142">tooconfigure y prueba de inicio de sesión único en Azure AD con Sciforma, deberá hello toocomplete después de bloques de creación:</span><span class="sxs-lookup"><span data-stu-id="f8239-142">tooconfigure and test Azure AD single sign-on with Sciforma, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="f8239-143">**[Configuración de Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on) ** -tooenable la toouse usuarios esta característica.</span><span class="sxs-lookup"><span data-stu-id="f8239-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="f8239-144">**[Crear un usuario de prueba de Azure AD](#creating-an-azure-ad-test-user) ** -inicio de sesión único en Azure AD tootest con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="f8239-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="f8239-145">**[Crear un usuario de prueba de Sciforma](#creating-a-sciforma-test-user) ** -toohave un equivalente de Britta Simon en Sciforma que es la representación toohello vinculado Azure AD del usuario.</span><span class="sxs-lookup"><span data-stu-id="f8239-145">**[Creating a Sciforma test user](#creating-a-sciforma-test-user)** - toohave a counterpart of Britta Simon in Sciforma that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="f8239-146">**[Asignar usuario de prueba de hello Azure AD](#assigning-the-azure-ad-test-user) ** -tooenable Britta Simon toouse Azure AD inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="f8239-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="f8239-147">**[Pruebas de Single Sign-On](#testing-single-sign-on) ** -tooverify Hola si funciona la configuración.</span><span class="sxs-lookup"><span data-stu-id="f8239-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="f8239-148">Configuración del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="f8239-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="f8239-149">En esta sección, habilitar inicio de sesión único en Azure AD en hello portal de Azure y configurar el inicio de sesión único en la aplicación de Sciforma.</span><span class="sxs-lookup"><span data-stu-id="f8239-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Sciforma application.</span></span>

<span data-ttu-id="f8239-150">**inicio de sesión único en tooconfigure Azure AD con Sciforma, siga Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="f8239-150">**tooconfigure Azure AD single sign-on with Sciforma, perform hello following steps:**</span></span>

1. <span data-ttu-id="f8239-151">En el portal de Azure, en Hola Hola **Sciforma** página de integración de aplicaciones, haga clic en **inicio de sesión único**.</span><span class="sxs-lookup"><span data-stu-id="f8239-151">In hello Azure portal, on hello **Sciforma** application integration page, click **Single sign-on**.</span></span>

    ![Configurar inicio de sesión único][4]

2. <span data-ttu-id="f8239-153">En hello **inicio de sesión único** cuadro de diálogo, seleccione **modo** como **sesión basado en SAML** tooenable inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="f8239-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurar inicio de sesión único](./media/active-directory-saas-sciforma-tutorial/tutorial_sciforma_samlbase.png)

3. <span data-ttu-id="f8239-155">En hello **Sciforma dominio y las direcciones URL** sección, lleve a cabo Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="f8239-155">On hello **Sciforma Domain and URLs** section, perform hello following steps:</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-sciforma-tutorial/tutorial_sciforma_url.png)

    <span data-ttu-id="f8239-157">a.</span><span class="sxs-lookup"><span data-stu-id="f8239-157">a.</span></span> <span data-ttu-id="f8239-158">Hola **dirección URL de inicio de sesión** cuadro de texto, escriba una dirección URL usando Hola siguiente patrón:`https://<subdomain>.sciforma.net/sciforma/main.html`</span><span class="sxs-lookup"><span data-stu-id="f8239-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<subdomain>.sciforma.net/sciforma/main.html`</span></span>

    <span data-ttu-id="f8239-159">b.</span><span class="sxs-lookup"><span data-stu-id="f8239-159">b.</span></span> <span data-ttu-id="f8239-160">Hola **identificador** cuadro de texto, escriba una dirección URL usando Hola siguiente patrón:`https://<subdomain>.sciforma.net/sciforma/saml`</span><span class="sxs-lookup"><span data-stu-id="f8239-160">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<subdomain>.sciforma.net/sciforma/saml`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="f8239-161">Estos valores no son reales.</span><span class="sxs-lookup"><span data-stu-id="f8239-161">These values are not real.</span></span> <span data-ttu-id="f8239-162">Actualizar estos valores con hello real de dirección URL de inicio de sesión y el identificador.</span><span class="sxs-lookup"><span data-stu-id="f8239-162">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="f8239-163">Póngase en contacto con [equipo de soporte técnico de Sciforma cliente](http://www.sciforma.com/company/contact_us) tooget estos valores.</span><span class="sxs-lookup"><span data-stu-id="f8239-163">Contact [Sciforma Client support team](http://www.sciforma.com/company/contact_us) tooget these values.</span></span> 
 


4. <span data-ttu-id="f8239-164">En hello **el certificado de firma de SAML** sección, haga clic en **Metadata XML** y, a continuación, guarde el archivo de metadatos de hello en el equipo.</span><span class="sxs-lookup"><span data-stu-id="f8239-164">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-sciforma-tutorial/tutorial_sciforma_certificate.png) 

5. <span data-ttu-id="f8239-166">Haga clic en el botón **Guardar** .</span><span class="sxs-lookup"><span data-stu-id="f8239-166">Click **Save** button.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-sciforma-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="f8239-168">inicio de sesión único en tooconfigure en **Sciforma** lado, necesita hello toosend descargado **Metadata XML** demasiado[equipo de soporte técnico de Sciforma](http://www.sciforma.com/company/contact_us).</span><span class="sxs-lookup"><span data-stu-id="f8239-168">tooconfigure single sign-on on **Sciforma** side, you need toosend hello downloaded **Metadata XML** too[Sciforma support team](http://www.sciforma.com/company/contact_us).</span></span>

> [!TIP]
> <span data-ttu-id="f8239-169">Ahora puede leer una versión concisa de estas instrucciones dentro de hello [portal de Azure](https://portal.azure.com), mientras que está configurando la aplicación hello!</span><span class="sxs-lookup"><span data-stu-id="f8239-169">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="f8239-170">Después de agregar esta aplicación de hello **Active Directory > aplicaciones empresariales** sección, simplemente haga clic en hello **Single Sign-On** Hola de pestaña y acceso incrustado documentación a través de hello ** Configuración** sección final Hola.</span><span class="sxs-lookup"><span data-stu-id="f8239-170">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="f8239-171">Puede leer más acerca de características de documentación de embedded Hola aquí: [Azure AD incrustado documentación]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="f8239-171">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="f8239-172">Creación de un usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="f8239-172">Creating an Azure AD test user</span></span>
<span data-ttu-id="f8239-173">objetivo de Hola de esta sección es un usuario de prueba en hello Azure portal llamado a Britta Simon toocreate.</span><span class="sxs-lookup"><span data-stu-id="f8239-173">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Creación de un usuario de Azure AD][100]

<span data-ttu-id="f8239-175">**toocreate un usuario de prueba en Azure AD, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="f8239-175">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="f8239-176">Hola **portal de Azure**, en Hola panel de navegación izquierdo, haga clic en **Azure Active Directory** icono.</span><span class="sxs-lookup"><span data-stu-id="f8239-176">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-sciforma-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="f8239-178">lista de hello toodisplay de usuarios, vaya demasiado**usuarios y grupos** y haga clic en **todos los usuarios**.</span><span class="sxs-lookup"><span data-stu-id="f8239-178">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-sciforma-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="f8239-180">Hola tooopen **usuario** cuadro de diálogo, haga clic en **agregar** en la parte superior de saludo del cuadro de diálogo de Hola.</span><span class="sxs-lookup"><span data-stu-id="f8239-180">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-sciforma-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="f8239-182">En hello **usuario** cuadro de diálogo, siga los pasos de hello:</span><span class="sxs-lookup"><span data-stu-id="f8239-182">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-sciforma-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="f8239-184">a.</span><span class="sxs-lookup"><span data-stu-id="f8239-184">a.</span></span> <span data-ttu-id="f8239-185">Hola **nombre** cuadro de texto, tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="f8239-185">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="f8239-186">b.</span><span class="sxs-lookup"><span data-stu-id="f8239-186">b.</span></span> <span data-ttu-id="f8239-187">Hola **nombre de usuario** cuadro de texto, hello tipo **dirección de correo electrónico** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="f8239-187">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="f8239-188">c.</span><span class="sxs-lookup"><span data-stu-id="f8239-188">c.</span></span> <span data-ttu-id="f8239-189">Seleccione **Mostrar contraseña** y anote el valor de Hola de hello **contraseña**.</span><span class="sxs-lookup"><span data-stu-id="f8239-189">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="f8239-190">d.</span><span class="sxs-lookup"><span data-stu-id="f8239-190">d.</span></span> <span data-ttu-id="f8239-191">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="f8239-191">Click **Create**.</span></span>
 
### <a name="creating-a-sciforma-test-user"></a><span data-ttu-id="f8239-192">Creación de un usuario de prueba de Sciforma</span><span class="sxs-lookup"><span data-stu-id="f8239-192">Creating a Sciforma test user</span></span>

<span data-ttu-id="f8239-193">No hay ningún elemento de acción tooconfigure de aprovisionamiento de usuarios tooSciforma.</span><span class="sxs-lookup"><span data-stu-id="f8239-193">There is no action item for you tooconfigure user provisioning tooSciforma.</span></span> <span data-ttu-id="f8239-194">Cuando un usuario asignado intenta toolog en tooSciforma mediante el panel de acceso de hello, Sciforma comprueba si existe el usuario de Hola.</span><span class="sxs-lookup"><span data-stu-id="f8239-194">When an assigned user tries toolog in tooSciforma using hello access panel, Sciforma checks whether hello user exists.</span></span>  

* <span data-ttu-id="f8239-195">Si no hay cuentas de usuario disponibles todavía, Sciforma crea una automáticamente.</span><span class="sxs-lookup"><span data-stu-id="f8239-195">If there is no user account available yet, it is automatically created by Sciforma.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="f8239-196">Asignación de usuario de prueba de hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="f8239-196">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="f8239-197">En esta sección, se habilita Britta Simon toouse un inicio de sesión único Azure concediendo acceso tooSciforma.</span><span class="sxs-lookup"><span data-stu-id="f8239-197">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooSciforma.</span></span>

![Asignar usuario][200] 

<span data-ttu-id="f8239-199">**tooassign Britta Simon tooSciforma, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="f8239-199">**tooassign Britta Simon tooSciforma, perform hello following steps:**</span></span>

1. <span data-ttu-id="f8239-200">Hola portal de Azure, abra la vista de aplicaciones de hello y, a continuación, navegue a vista de directorio toohello y vaya demasiado**aplicaciones empresariales** , a continuación, haga clic en **todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="f8239-200">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Asignar usuario][201] 

2. <span data-ttu-id="f8239-202">En la lista de aplicaciones de hello, seleccione **Sciforma**.</span><span class="sxs-lookup"><span data-stu-id="f8239-202">In hello applications list, select **Sciforma**.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-sciforma-tutorial/tutorial_sciforma_app.png) 

3. <span data-ttu-id="f8239-204">En el menú de Hola Hola izquierda, haga clic en **usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="f8239-204">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Asignar usuario][202] 

4. <span data-ttu-id="f8239-206">Haga clic en el botón **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="f8239-206">Click **Add** button.</span></span> <span data-ttu-id="f8239-207">Después, seleccione **Usuarios y grupos** en el cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="f8239-207">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Asignar usuario][203]

5. <span data-ttu-id="f8239-209">En **usuarios y grupos** cuadro de diálogo, seleccione **Britta Simon** en la lista de usuarios de Hola.</span><span class="sxs-lookup"><span data-stu-id="f8239-209">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="f8239-210">Haga clic en el botón **Seleccionar** del cuadro de diálogo **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="f8239-210">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="f8239-211">Haga clic en el botón **Asignar** del cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="f8239-211">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="f8239-212">Prueba del inicio de sesión único </span><span class="sxs-lookup"><span data-stu-id="f8239-212">Testing single sign-on</span></span>

<span data-ttu-id="f8239-213">Si desea tootest las opciones de inicio de sesión único, abra Hola Panel de acceso.</span><span class="sxs-lookup"><span data-stu-id="f8239-213">If you want tootest your single sign-on settings, open hello Access Panel.</span></span> <span data-ttu-id="f8239-214">Para obtener más información acerca de hello Panel de acceso, consulte [Introducción toohello Panel de acceso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="f8239-214">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="f8239-215">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="f8239-215">Additional resources</span></span>

* [<span data-ttu-id="f8239-216">Lista de tutoriales sobre cómo tooIntegrate aplicaciones de SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="f8239-216">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="f8239-217">¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="f8239-217">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-sciforma-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-sciforma-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-sciforma-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-sciforma-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-sciforma-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-sciforma-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-sciforma-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-sciforma-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-sciforma-tutorial/tutorial_general_203.png

