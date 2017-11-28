---
title: "Tutorial: Integración de Azure Active Directory con JobsScore | Microsoft Docs"
description: "Obtenga información acerca de cómo tooconfigure inicio de sesión único entre Azure Active Directory y JobScore."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 30f51b32-e55c-4c66-96e8-50a2f9c2194a
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/22/2017
ms.author: jeedes
ms.openlocfilehash: 6693a5fd96bfd7fbcd7197983b5f04d061970bdd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-jobscore"></a><span data-ttu-id="66ab4-103">Tutorial: Integración de Azure Active Directory con JobScore</span><span class="sxs-lookup"><span data-stu-id="66ab4-103">Tutorial: Azure Active Directory integration with JobScore</span></span>

<span data-ttu-id="66ab4-104">En este tutorial, aprenderá cómo toointegrate JobScore con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="66ab4-104">In this tutorial, you learn how toointegrate JobScore with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="66ab4-105">Integración JobScore con Azure AD proporciona Hola siguientes ventajas:</span><span class="sxs-lookup"><span data-stu-id="66ab4-105">Integrating JobScore with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="66ab4-106">Puede controlar en Azure AD que tenga acceso tooJobScore</span><span class="sxs-lookup"><span data-stu-id="66ab4-106">You can control in Azure AD who has access tooJobScore</span></span>
- <span data-ttu-id="66ab4-107">Puede habilitar los usuarios tooautomatically get ha iniciado sesión tooJobScore (Single Sign-On) con sus cuentas de Azure AD</span><span class="sxs-lookup"><span data-stu-id="66ab4-107">You can enable your users tooautomatically get signed-on tooJobScore (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="66ab4-108">Puede administrar las cuentas en una ubicación central: Hola portal de Azure</span><span class="sxs-lookup"><span data-stu-id="66ab4-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="66ab4-109">Si desea obtener más información acerca de la integración de aplicaciones de SaaS con Azure AD tooknow, consulte [¿qué es acceso a la aplicación y el inicio de sesión único con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="66ab4-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="66ab4-110">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="66ab4-110">Prerequisites</span></span>

<span data-ttu-id="66ab4-111">integración de Azure AD con JobScore tooconfigure, necesita Hola siguientes elementos:</span><span class="sxs-lookup"><span data-stu-id="66ab4-111">tooconfigure Azure AD integration with JobScore, you need hello following items:</span></span>

- <span data-ttu-id="66ab4-112">Una suscripción de Azure AD</span><span class="sxs-lookup"><span data-stu-id="66ab4-112">An Azure AD subscription</span></span>
- <span data-ttu-id="66ab4-113">Una suscripción habilitada para el inicio de sesión único en JobScore.</span><span class="sxs-lookup"><span data-stu-id="66ab4-113">A JobScore single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="66ab4-114">Hola tootest los pasos de este tutorial, no se recomienda usar un entorno de producción.</span><span class="sxs-lookup"><span data-stu-id="66ab4-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="66ab4-115">pasos de hello tootest en este tutorial, debe seguir estas recomendaciones:</span><span class="sxs-lookup"><span data-stu-id="66ab4-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="66ab4-116">No use el entorno de producción, salvo que sea necesario.</span><span class="sxs-lookup"><span data-stu-id="66ab4-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="66ab4-117">Si no dispone de un entorno de prueba de Azure AD, puede obtener una versión de prueba de un mes [aquí](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="66ab4-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="66ab4-118">Descripción del escenario</span><span class="sxs-lookup"><span data-stu-id="66ab4-118">Scenario description</span></span>
<span data-ttu-id="66ab4-119">En este tutorial, puede probar el inicio de sesión único de Azure AD en un entorno de prueba.</span><span class="sxs-lookup"><span data-stu-id="66ab4-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="66ab4-120">escenario de Hello descrito en este tutorial consta de dos bloques principales:</span><span class="sxs-lookup"><span data-stu-id="66ab4-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="66ab4-121">Agregar JobScore desde la Galería de Hola</span><span class="sxs-lookup"><span data-stu-id="66ab4-121">Adding JobScore from hello gallery</span></span>
2. <span data-ttu-id="66ab4-122">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="66ab4-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-jobscore-from-hello-gallery"></a><span data-ttu-id="66ab4-123">Agregar JobScore desde la Galería de Hola</span><span class="sxs-lookup"><span data-stu-id="66ab4-123">Adding JobScore from hello gallery</span></span>
<span data-ttu-id="66ab4-124">integración de hello tooconfigure de JobScore en Azure AD, deberá tooadd JobScore de lista de tooyour Hola Galería de aplicaciones administradas de SaaS.</span><span class="sxs-lookup"><span data-stu-id="66ab4-124">tooconfigure hello integration of JobScore into Azure AD, you need tooadd JobScore from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="66ab4-125">**tooadd JobScore de galería de hello, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="66ab4-125">**tooadd JobScore from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="66ab4-126">Hola  **[portal de Azure](https://portal.azure.com)**, en el panel de navegación izquierdo de Hola, haga clic en **Azure Active Directory** icono.</span><span class="sxs-lookup"><span data-stu-id="66ab4-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="66ab4-128">Navegue demasiado**aplicaciones empresariales**.</span><span class="sxs-lookup"><span data-stu-id="66ab4-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="66ab4-129">A continuación, vaya demasiado**todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="66ab4-129">Then go too**All applications**.</span></span>

    ![Aplicaciones][2]
    
3. <span data-ttu-id="66ab4-131">tooadd nueva aplicación, haga clic en **nueva aplicación** botón en la parte superior de saludo del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="66ab4-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Aplicaciones][3]

4. <span data-ttu-id="66ab4-133">En el cuadro de búsqueda de hello, escriba **JobScore**.</span><span class="sxs-lookup"><span data-stu-id="66ab4-133">In hello search box, type **JobScore**.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-jobscore-tutorial/tutorial_jobscore_search.png)

5. <span data-ttu-id="66ab4-135">En el panel de resultados de hello, seleccione **JobScore**y, a continuación, haga clic en **agregar** botón aplicación hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="66ab4-135">In hello results panel, select **JobScore**, and then click **Add** button tooadd hello application.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-jobscore-tutorial/tutorial_jobscore_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="66ab4-137">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="66ab4-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="66ab4-138">En esta sección, podrá configurar y probar el inicio de sesión único de Azure AD con JobScore con un usuario de prueba llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="66ab4-138">In this section, you configure and test Azure AD single sign-on with JobScore based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="66ab4-139">Para toowork de inicio de sesión único, Azure AD necesita tooknow qué usuario equivalente de hello en JobScore es tooa usuario en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="66ab4-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in JobScore is tooa user in Azure AD.</span></span> <span data-ttu-id="66ab4-140">En otras palabras, una relación de vínculo entre un usuario de Azure AD y el usuario relacionado de hello en JobScore debe toobe establecido.</span><span class="sxs-lookup"><span data-stu-id="66ab4-140">In other words, a link relationship between an Azure AD user and hello related user in JobScore needs toobe established.</span></span>

<span data-ttu-id="66ab4-141">En JobScore, asigne el valor de Hola de hello **nombre de usuario** en Azure AD como valor de Hola de hello **nombre de usuario** tooestablish la relación de vínculo de Hola.</span><span class="sxs-lookup"><span data-stu-id="66ab4-141">In JobScore, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="66ab4-142">tooconfigure y prueba de inicio de sesión único en Azure AD con JobScore, deberá hello toocomplete después de bloques de creación:</span><span class="sxs-lookup"><span data-stu-id="66ab4-142">tooconfigure and test Azure AD single sign-on with JobScore, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="66ab4-143">**[Configuración de Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable la toouse usuarios esta característica.</span><span class="sxs-lookup"><span data-stu-id="66ab4-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="66ab4-144">**[Crear un usuario de prueba de Azure AD](#creating-an-azure-ad-test-user)**  -inicio de sesión único en Azure AD tootest con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="66ab4-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="66ab4-145">**[Crear un usuario de prueba JobScore](#creating-a-jobscore-test-user)**  -toohave un equivalente de Britta Simon en JobScore que es la representación toohello vinculado Azure AD del usuario.</span><span class="sxs-lookup"><span data-stu-id="66ab4-145">**[Creating a JobScore test user](#creating-a-jobscore-test-user)** - toohave a counterpart of Britta Simon in JobScore that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="66ab4-146">**[Asignar usuario de prueba de hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="66ab4-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="66ab4-147">**[Pruebas de Single Sign-On](#testing-single-sign-on)**  -tooverify Hola si funciona la configuración.</span><span class="sxs-lookup"><span data-stu-id="66ab4-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="66ab4-148">Configuración del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="66ab4-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="66ab4-149">En esta sección, habilitar inicio de sesión único en Azure AD en hello portal de Azure y configurar el inicio de sesión único en la aplicación JobScore.</span><span class="sxs-lookup"><span data-stu-id="66ab4-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your JobScore application.</span></span>

<span data-ttu-id="66ab4-150">**inicio de sesión único en Azure AD tooconfigure con JobScore, realizar Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="66ab4-150">**tooconfigure Azure AD single sign-on with JobScore, perform hello following steps:**</span></span>

1. <span data-ttu-id="66ab4-151">En el portal de Azure, en Hola Hola **JobScore** página de integración de aplicaciones, haga clic en **inicio de sesión único**.</span><span class="sxs-lookup"><span data-stu-id="66ab4-151">In hello Azure portal, on hello **JobScore** application integration page, click **Single sign-on**.</span></span>

    ![Configurar inicio de sesión único][4]

2. <span data-ttu-id="66ab4-153">En hello **inicio de sesión único** cuadro de diálogo, seleccione **modo** como **sesión basado en SAML** tooenable inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="66ab4-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurar inicio de sesión único](./media/active-directory-saas-jobscore-tutorial/tutorial_jobscore_samlbase.png)

3. <span data-ttu-id="66ab4-155">En hello **JobScore dominio y las direcciones URL** sección, lleve a cabo Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="66ab4-155">On hello **JobScore Domain and URLs** section, perform hello following steps:</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-jobscore-tutorial/tutorial_jobscore_url.png)

    <span data-ttu-id="66ab4-157">Hola **dirección URL de inicio de sesión** cuadro de texto, escriba una dirección URL usando Hola siguiente patrón:`https://hire.jobscore.com/auth/adfs/<company name>`</span><span class="sxs-lookup"><span data-stu-id="66ab4-157">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://hire.jobscore.com/auth/adfs/<company name>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="66ab4-158">Este valor no es real.</span><span class="sxs-lookup"><span data-stu-id="66ab4-158">This value is not real.</span></span> <span data-ttu-id="66ab4-159">Actualice este valor con hello dirección URL de inicio de sesión real.</span><span class="sxs-lookup"><span data-stu-id="66ab4-159">Update this value with hello actual Sign-On URL.</span></span> <span data-ttu-id="66ab4-160">Póngase en contacto con [equipo de soporte técnico de cliente de JobScore](mailto:support@jobscore.com) tooget este valor.</span><span class="sxs-lookup"><span data-stu-id="66ab4-160">Contact [JobScore Client support team](mailto:support@jobscore.com) tooget this value.</span></span> 
 
4. <span data-ttu-id="66ab4-161">En hello **el certificado de firma de SAML** sección, haga clic en **Metadata XML** y, a continuación, guarde el archivo de metadatos de hello en el equipo.</span><span class="sxs-lookup"><span data-stu-id="66ab4-161">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-jobscore-tutorial/tutorial_jobscore_certificate.png) 

5. <span data-ttu-id="66ab4-163">Haga clic en el botón **Guardar** .</span><span class="sxs-lookup"><span data-stu-id="66ab4-163">Click **Save** button.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-jobscore-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="66ab4-165">tooconfigure inicio de sesión único en **JobScore** lado, necesita hello toosend descargado **Metadata XML** demasiado[equipo de soporte técnico de JobScore](mailto:support@jobscore.com).</span><span class="sxs-lookup"><span data-stu-id="66ab4-165">tooconfigure single sign-on on **JobScore** side, you need toosend hello downloaded **Metadata XML** too[JobScore support team](mailto:support@jobscore.com).</span></span> 

> [!TIP]
> <span data-ttu-id="66ab4-166">Ahora puede leer una versión concisa de estas instrucciones dentro de hello [portal de Azure](https://portal.azure.com), mientras que está configurando la aplicación hello!</span><span class="sxs-lookup"><span data-stu-id="66ab4-166">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="66ab4-167">Después de agregar esta aplicación de hello **Active Directory > aplicaciones empresariales** sección, simplemente haga clic en hello **Single Sign-On** Hola de pestaña y acceso incrustado documentación a través de hello  **Configuración** sección final Hola.</span><span class="sxs-lookup"><span data-stu-id="66ab4-167">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="66ab4-168">Puede leer más acerca de características de documentación de embedded Hola aquí: [Azure AD incrustado documentación]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="66ab4-168">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="66ab4-169">Creación de un usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="66ab4-169">Creating an Azure AD test user</span></span>
<span data-ttu-id="66ab4-170">objetivo de Hola de esta sección es un usuario de prueba en hello Azure portal llamado a Britta Simon toocreate.</span><span class="sxs-lookup"><span data-stu-id="66ab4-170">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Creación de un usuario de Azure AD][100]

<span data-ttu-id="66ab4-172">**toocreate un usuario de prueba en Azure AD, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="66ab4-172">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="66ab4-173">Hola **portal de Azure**, en Hola panel de navegación izquierdo, haga clic en **Azure Active Directory** icono.</span><span class="sxs-lookup"><span data-stu-id="66ab4-173">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-jobscore-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="66ab4-175">lista de hello toodisplay de usuarios, vaya demasiado**usuarios y grupos** y haga clic en **todos los usuarios**.</span><span class="sxs-lookup"><span data-stu-id="66ab4-175">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-jobscore-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="66ab4-177">Hola tooopen **usuario** cuadro de diálogo, haga clic en **agregar** en la parte superior de saludo del cuadro de diálogo de Hola.</span><span class="sxs-lookup"><span data-stu-id="66ab4-177">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-jobscore-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="66ab4-179">En hello **usuario** cuadro de diálogo, siga los pasos de hello:</span><span class="sxs-lookup"><span data-stu-id="66ab4-179">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-jobscore-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="66ab4-181">a.</span><span class="sxs-lookup"><span data-stu-id="66ab4-181">a.</span></span> <span data-ttu-id="66ab4-182">Hola **nombre** cuadro de texto, tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="66ab4-182">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="66ab4-183">b.</span><span class="sxs-lookup"><span data-stu-id="66ab4-183">b.</span></span> <span data-ttu-id="66ab4-184">Hola **nombre de usuario** cuadro de texto, hello tipo **dirección de correo electrónico** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="66ab4-184">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="66ab4-185">c.</span><span class="sxs-lookup"><span data-stu-id="66ab4-185">c.</span></span> <span data-ttu-id="66ab4-186">Seleccione **Mostrar contraseña** y anote el valor de Hola de hello **contraseña**.</span><span class="sxs-lookup"><span data-stu-id="66ab4-186">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="66ab4-187">d.</span><span class="sxs-lookup"><span data-stu-id="66ab4-187">d.</span></span> <span data-ttu-id="66ab4-188">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="66ab4-188">Click **Create**.</span></span>
 
### <a name="creating-a-jobscore-test-user"></a><span data-ttu-id="66ab4-189">Creación de un usuario de prueba de JobScore</span><span class="sxs-lookup"><span data-stu-id="66ab4-189">Creating a JobScore test user</span></span>

<span data-ttu-id="66ab4-190">En esta sección, creará un usuario llamado Britta Simon en JobScore.</span><span class="sxs-lookup"><span data-stu-id="66ab4-190">In this section, you create a user called Britta Simon in JobScore.</span></span> <span data-ttu-id="66ab4-191">Trabajar con [equipo de soporte técnico de JobScore](mailto:support@jobscore.com) a los usuarios de tooadd hello en la plataforma de JobScore Hola.</span><span class="sxs-lookup"><span data-stu-id="66ab4-191">Work with [JobScore support team](mailto:support@jobscore.com) tooadd hello users in hello JobScore platform.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="66ab4-192">Asignación de usuario de prueba de hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="66ab4-192">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="66ab4-193">En esta sección, se habilita Britta Simon toouse un inicio de sesión único Azure concediendo acceso tooJobScore.</span><span class="sxs-lookup"><span data-stu-id="66ab4-193">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooJobScore.</span></span>

![Asignar usuario][200] 

<span data-ttu-id="66ab4-195">**tooassign Britta Simon tooJobScore, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="66ab4-195">**tooassign Britta Simon tooJobScore, perform hello following steps:**</span></span>

1. <span data-ttu-id="66ab4-196">Hola portal de Azure, abra la vista de aplicaciones de hello y, a continuación, navegue a vista de directorio toohello y vaya demasiado**aplicaciones empresariales** , a continuación, haga clic en **todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="66ab4-196">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Asignar usuario][201] 

2. <span data-ttu-id="66ab4-198">En la lista de aplicaciones de hello, seleccione **JobScore**.</span><span class="sxs-lookup"><span data-stu-id="66ab4-198">In hello applications list, select **JobScore**.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-jobscore-tutorial/tutorial_jobscore_app.png) 

3. <span data-ttu-id="66ab4-200">En el menú de Hola Hola izquierda, haga clic en **usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="66ab4-200">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Asignar usuario][202] 

4. <span data-ttu-id="66ab4-202">Haga clic en el botón **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="66ab4-202">Click **Add** button.</span></span> <span data-ttu-id="66ab4-203">Después, seleccione **Usuarios y grupos** en el cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="66ab4-203">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Asignar usuario][203]

5. <span data-ttu-id="66ab4-205">En **usuarios y grupos** cuadro de diálogo, seleccione **Britta Simon** en la lista de usuarios de Hola.</span><span class="sxs-lookup"><span data-stu-id="66ab4-205">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="66ab4-206">Haga clic en el botón **Seleccionar** del cuadro de diálogo **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="66ab4-206">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="66ab4-207">Haga clic en el botón **Asignar** del cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="66ab4-207">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="66ab4-208">Prueba del inicio de sesión único </span><span class="sxs-lookup"><span data-stu-id="66ab4-208">Testing single sign-on</span></span>

<span data-ttu-id="66ab4-209">En esta sección, comprobará su único inicio de sesión en configuración de Azure AD con hello Panel de acceso.</span><span class="sxs-lookup"><span data-stu-id="66ab4-209">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="66ab4-210">Al hacer clic en icono de JobScore Hola Hola Panel de acceso, deberá obtener automáticamente ha iniciado sesión tooyour JobScore aplicación.</span><span class="sxs-lookup"><span data-stu-id="66ab4-210">When you click hello JobScore tile in hello Access Panel, you should get automatically signed-on tooyour JobScore application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="66ab4-211">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="66ab4-211">Additional resources</span></span>

* [<span data-ttu-id="66ab4-212">Lista de tutoriales sobre cómo tooIntegrate aplicaciones de SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="66ab4-212">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="66ab4-213">¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="66ab4-213">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-jobscore-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-jobscore-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-jobscore-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-jobscore-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-jobscore-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-jobscore-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-jobscore-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-jobscore-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-jobscore-tutorial/tutorial_general_203.png

