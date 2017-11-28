---
title: "Tutorial: Integración de Azure Active Directory con Novatus | Microsoft Docs"
description: "Obtenga información acerca de cómo tooconfigure inicio de sesión único entre Azure Active Directory y Novatus."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: d2f13779-bdb7-4408-9738-be67ed3de4e5
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/02/2017
ms.author: jeedes
ms.openlocfilehash: 7ff13f56f0f47d0c2667c9ca555801a7a06a2fa7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-novatus"></a><span data-ttu-id="94aad-103">Tutorial: integración de Azure Active Directory con Novatus</span><span class="sxs-lookup"><span data-stu-id="94aad-103">Tutorial: Azure Active Directory integration with Novatus</span></span>

<span data-ttu-id="94aad-104">En este tutorial, aprenderá cómo toointegrate Novatus con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="94aad-104">In this tutorial, you learn how toointegrate Novatus with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="94aad-105">Integración Novatus con Azure AD proporciona Hola siguientes ventajas:</span><span class="sxs-lookup"><span data-stu-id="94aad-105">Integrating Novatus with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="94aad-106">Puede controlar en Azure AD que tenga acceso tooNovatus</span><span class="sxs-lookup"><span data-stu-id="94aad-106">You can control in Azure AD who has access tooNovatus</span></span>
- <span data-ttu-id="94aad-107">Puede habilitar los usuarios tooautomatically get ha iniciado sesión tooNovatus (Single Sign-On) con sus cuentas de Azure AD</span><span class="sxs-lookup"><span data-stu-id="94aad-107">You can enable your users tooautomatically get signed-on tooNovatus (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="94aad-108">Puede administrar las cuentas en una ubicación central: Hola portal de Azure</span><span class="sxs-lookup"><span data-stu-id="94aad-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="94aad-109">Si desea obtener más información acerca de la integración de aplicaciones de SaaS con Azure AD tooknow, consulte [¿qué es acceso a la aplicación y el inicio de sesión único con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="94aad-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="94aad-110">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="94aad-110">Prerequisites</span></span>

<span data-ttu-id="94aad-111">integración de Azure AD con Novatus tooconfigure, necesita Hola siguientes elementos:</span><span class="sxs-lookup"><span data-stu-id="94aad-111">tooconfigure Azure AD integration with Novatus, you need hello following items:</span></span>

- <span data-ttu-id="94aad-112">Una suscripción de Azure AD</span><span class="sxs-lookup"><span data-stu-id="94aad-112">An Azure AD subscription</span></span>
- <span data-ttu-id="94aad-113">Una suscripción habilitada para el inicio de sesión único en Novatus</span><span class="sxs-lookup"><span data-stu-id="94aad-113">A Novatus single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="94aad-114">Hola tootest los pasos de este tutorial, no se recomienda usar un entorno de producción.</span><span class="sxs-lookup"><span data-stu-id="94aad-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="94aad-115">pasos de hello tootest en este tutorial, debe seguir estas recomendaciones:</span><span class="sxs-lookup"><span data-stu-id="94aad-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="94aad-116">No use el entorno de producción, salvo que sea necesario.</span><span class="sxs-lookup"><span data-stu-id="94aad-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="94aad-117">Si no dispone de un entorno de prueba de Azure AD, puede obtener una versión de prueba de un mes [aquí](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="94aad-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="94aad-118">Descripción del escenario</span><span class="sxs-lookup"><span data-stu-id="94aad-118">Scenario description</span></span>
<span data-ttu-id="94aad-119">En este tutorial, puede probar el inicio de sesión único de Azure AD en un entorno de prueba.</span><span class="sxs-lookup"><span data-stu-id="94aad-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="94aad-120">escenario de Hello descrito en este tutorial consta de dos bloques principales:</span><span class="sxs-lookup"><span data-stu-id="94aad-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="94aad-121">Agregar Novatus desde la Galería de Hola</span><span class="sxs-lookup"><span data-stu-id="94aad-121">Adding Novatus from hello gallery</span></span>
2. <span data-ttu-id="94aad-122">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="94aad-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-novatus-from-hello-gallery"></a><span data-ttu-id="94aad-123">Agregar Novatus desde la Galería de Hola</span><span class="sxs-lookup"><span data-stu-id="94aad-123">Adding Novatus from hello gallery</span></span>
<span data-ttu-id="94aad-124">integración de hello tooconfigure de Novatus en Azure AD, deberá tooadd Novatus de lista de tooyour Hola Galería de aplicaciones administradas de SaaS.</span><span class="sxs-lookup"><span data-stu-id="94aad-124">tooconfigure hello integration of Novatus into Azure AD, you need tooadd Novatus from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="94aad-125">**tooadd Novatus de galería de hello, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="94aad-125">**tooadd Novatus from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="94aad-126">Hola  **[portal de Azure](https://portal.azure.com)**, en el panel de navegación izquierdo de Hola, haga clic en **Azure Active Directory** icono.</span><span class="sxs-lookup"><span data-stu-id="94aad-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="94aad-128">Navegue demasiado**aplicaciones empresariales**.</span><span class="sxs-lookup"><span data-stu-id="94aad-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="94aad-129">A continuación, vaya demasiado**todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="94aad-129">Then go too**All applications**.</span></span>

    ![Aplicaciones][2]
    
3. <span data-ttu-id="94aad-131">tooadd nueva aplicación, haga clic en **nueva aplicación** botón en la parte superior de saludo del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="94aad-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Aplicaciones][3]

4. <span data-ttu-id="94aad-133">En el cuadro de búsqueda de hello, escriba **Novatus**.</span><span class="sxs-lookup"><span data-stu-id="94aad-133">In hello search box, type **Novatus**.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-novatus-tutorial/tutorial_novatus_search.png)

5. <span data-ttu-id="94aad-135">En el panel de resultados de hello, seleccione **Novatus**y, a continuación, haga clic en **agregar** botón aplicación hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="94aad-135">In hello results panel, select **Novatus**, and then click **Add** button tooadd hello application.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-novatus-tutorial/tutorial_novatus_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="94aad-137">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="94aad-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="94aad-138">En esta sección, configurará y probará el inicio de sesión único de Azure AD con Novatus con un usuario de prueba llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="94aad-138">In this section, you configure and test Azure AD single sign-on with Novatus based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="94aad-139">Para toowork de inicio de sesión único, Azure AD necesita tooknow qué usuario equivalente de hello en Novatus es tooa usuario en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="94aad-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Novatus is tooa user in Azure AD.</span></span> <span data-ttu-id="94aad-140">En otras palabras, una relación de vínculo entre un usuario de Azure AD y el usuario relacionado de hello en Novatus debe toobe establecido.</span><span class="sxs-lookup"><span data-stu-id="94aad-140">In other words, a link relationship between an Azure AD user and hello related user in Novatus needs toobe established.</span></span>

<span data-ttu-id="94aad-141">En Novatus, asigne el valor de Hola de hello **nombre de usuario** en Azure AD como valor de Hola de hello **nombre de usuario** tooestablish la relación de vínculo de Hola.</span><span class="sxs-lookup"><span data-stu-id="94aad-141">In Novatus, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="94aad-142">tooconfigure y prueba de inicio de sesión único en Azure AD con Novatus, deberá hello toocomplete después de bloques de creación:</span><span class="sxs-lookup"><span data-stu-id="94aad-142">tooconfigure and test Azure AD single sign-on with Novatus, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="94aad-143">**[Configuración de Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable la toouse usuarios esta característica.</span><span class="sxs-lookup"><span data-stu-id="94aad-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="94aad-144">**[Crear un usuario de prueba de Azure AD](#creating-an-azure-ad-test-user)**  -inicio de sesión único en Azure AD tootest con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="94aad-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="94aad-145">**[Crear un usuario de prueba Novatus](#creating-a-novatus-test-user)**  -toohave un equivalente de Britta Simon en Novatus que es la representación toohello vinculado Azure AD del usuario.</span><span class="sxs-lookup"><span data-stu-id="94aad-145">**[Creating a Novatus test user](#creating-a-novatus-test-user)** - toohave a counterpart of Britta Simon in Novatus that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="94aad-146">**[Asignar usuario de prueba de hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="94aad-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="94aad-147">**[Pruebas de Single Sign-On](#testing-single-sign-on)**  -tooverify Hola si funciona la configuración.</span><span class="sxs-lookup"><span data-stu-id="94aad-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="94aad-148">Configuración del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="94aad-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="94aad-149">En esta sección, habilitar inicio de sesión único en Azure AD en hello portal de Azure y configurar el inicio de sesión único en la aplicación Novatus.</span><span class="sxs-lookup"><span data-stu-id="94aad-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Novatus application.</span></span>

<span data-ttu-id="94aad-150">**inicio de sesión único en Azure AD tooconfigure con Novatus, realizar Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="94aad-150">**tooconfigure Azure AD single sign-on with Novatus, perform hello following steps:**</span></span>

1. <span data-ttu-id="94aad-151">En el portal de Azure, en Hola Hola **Novatus** página de integración de aplicaciones, haga clic en **inicio de sesión único**.</span><span class="sxs-lookup"><span data-stu-id="94aad-151">In hello Azure portal, on hello **Novatus** application integration page, click **Single sign-on**.</span></span>

    ![Configurar inicio de sesión único][4]

2. <span data-ttu-id="94aad-153">En hello **inicio de sesión único** cuadro de diálogo, seleccione **modo** como **sesión basado en SAML** tooenable inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="94aad-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurar inicio de sesión único](./media/active-directory-saas-novatus-tutorial/tutorial_novatus_samlbase.png)

3. <span data-ttu-id="94aad-155">En hello **Novatus dominio y las direcciones URL** sección, lleve a cabo Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="94aad-155">On hello **Novatus Domain and URLs** section, perform hello following steps:</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-novatus-tutorial/tutorial_novatus_url.png)

     <span data-ttu-id="94aad-157">Hola **dirección URL de inicio de sesión** cuadro de texto, escriba una dirección URL usando Hola siguiente patrón:`https://sso.novatuscontracts.com/<companyname>`</span><span class="sxs-lookup"><span data-stu-id="94aad-157">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://sso.novatuscontracts.com/<companyname>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="94aad-158">Este valor no es real.</span><span class="sxs-lookup"><span data-stu-id="94aad-158">This value is not real.</span></span> <span data-ttu-id="94aad-159">Actualice este valor con hello dirección URL de inicio de sesión real.</span><span class="sxs-lookup"><span data-stu-id="94aad-159">Update this value with hello actual Sign-On URL.</span></span> <span data-ttu-id="94aad-160">Póngase en contacto con [equipo de soporte técnico de cliente de Novatus](mailto:jvinci@novatusinc.com) tooget este valor.</span><span class="sxs-lookup"><span data-stu-id="94aad-160">Contact [Novatus Client support team](mailto:jvinci@novatusinc.com) tooget this value.</span></span> 
 


4. <span data-ttu-id="94aad-161">En hello **el certificado de firma de SAML** sección, haga clic en **Certificate(Base64)** y, a continuación, guarde el archivo de certificado de hello en el equipo.</span><span class="sxs-lookup"><span data-stu-id="94aad-161">On hello **SAML Signing Certificate** section, click **Certificate(Base64)** and then save hello certificate file on your computer.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-novatus-tutorial/tutorial_novatus_certificate.png) 

5. <span data-ttu-id="94aad-163">Haga clic en el botón **Guardar** .</span><span class="sxs-lookup"><span data-stu-id="94aad-163">Click **Save** button.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-novatus-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="94aad-165">En hello **Novatus configuración** sección, haga clic en **configurar Novatus** tooopen **configurar inicio de sesión** ventana.</span><span class="sxs-lookup"><span data-stu-id="94aad-165">On hello **Novatus Configuration** section, click **Configure Novatus** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="94aad-166">Hola copia **dirección URL de cierre de sesión, Id. de entidad de SAML y SAML Single Sign-On dirección URL del servicio** de hello **sección de referencia rápida.**</span><span class="sxs-lookup"><span data-stu-id="94aad-166">Copy hello **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-novatus-tutorial/tutorial_novatus_configure.png) 

7. <span data-ttu-id="94aad-168">tooget SSO configurado para la aplicación, póngase en contacto con su [equipo de soporte técnico Novatus](mailto:jvinci@novatusinc.com).</span><span class="sxs-lookup"><span data-stu-id="94aad-168">tooget SSO configured for your application, contact your [Novatus support team](mailto:jvinci@novatusinc.com).</span></span> <span data-ttu-id="94aad-169">Adjuntar hello **descargado certificado** Hola de correo electrónico y el recurso compartido de archivo tooyour **direcciones URL de metadatos** (**dirección URL de cierre de sesión, Id. de entidad de SAML y SAML Single Sign-On dirección URL del servicio**) con Equipo de Novatus tooset de SSO en uno de su lados.</span><span class="sxs-lookup"><span data-stu-id="94aad-169">Attach hello **downloaded certificate** file tooyour mail and share hello **metadata urls** (**Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL**) with Novatus team tooset up SSO on their side.</span></span>

> [!TIP]
> <span data-ttu-id="94aad-170">Ahora puede leer una versión concisa de estas instrucciones dentro de hello [portal de Azure](https://portal.azure.com), mientras que está configurando la aplicación hello!</span><span class="sxs-lookup"><span data-stu-id="94aad-170">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="94aad-171">Después de agregar esta aplicación de hello **Active Directory > aplicaciones empresariales** sección, simplemente haga clic en hello **Single Sign-On** Hola de pestaña y acceso incrustado documentación a través de hello  **Configuración** sección final Hola.</span><span class="sxs-lookup"><span data-stu-id="94aad-171">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="94aad-172">Puede leer más acerca de características de documentación de embedded Hola aquí: [Azure AD incrustado documentación]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="94aad-172">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="94aad-173">Creación de un usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="94aad-173">Creating an Azure AD test user</span></span>
<span data-ttu-id="94aad-174">objetivo de Hola de esta sección es un usuario de prueba en hello Azure portal llamado a Britta Simon toocreate.</span><span class="sxs-lookup"><span data-stu-id="94aad-174">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Creación de un usuario de Azure AD][100]

<span data-ttu-id="94aad-176">**toocreate un usuario de prueba en Azure AD, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="94aad-176">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="94aad-177">Hola **portal de Azure**, en Hola panel de navegación izquierdo, haga clic en **Azure Active Directory** icono.</span><span class="sxs-lookup"><span data-stu-id="94aad-177">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-novatus-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="94aad-179">lista de hello toodisplay de usuarios, vaya demasiado**usuarios y grupos** y haga clic en **todos los usuarios**.</span><span class="sxs-lookup"><span data-stu-id="94aad-179">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-novatus-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="94aad-181">Hola tooopen **usuario** cuadro de diálogo, haga clic en **agregar** en la parte superior de saludo del cuadro de diálogo de Hola.</span><span class="sxs-lookup"><span data-stu-id="94aad-181">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-novatus-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="94aad-183">En hello **usuario** cuadro de diálogo, siga los pasos de hello:</span><span class="sxs-lookup"><span data-stu-id="94aad-183">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-novatus-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="94aad-185">a.</span><span class="sxs-lookup"><span data-stu-id="94aad-185">a.</span></span> <span data-ttu-id="94aad-186">Hola **nombre** cuadro de texto, tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="94aad-186">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="94aad-187">b.</span><span class="sxs-lookup"><span data-stu-id="94aad-187">b.</span></span> <span data-ttu-id="94aad-188">Hola **nombre de usuario** cuadro de texto, hello tipo **dirección de correo electrónico** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="94aad-188">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="94aad-189">c.</span><span class="sxs-lookup"><span data-stu-id="94aad-189">c.</span></span> <span data-ttu-id="94aad-190">Seleccione **Mostrar contraseña** y anote el valor de Hola de hello **contraseña**.</span><span class="sxs-lookup"><span data-stu-id="94aad-190">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="94aad-191">d.</span><span class="sxs-lookup"><span data-stu-id="94aad-191">d.</span></span> <span data-ttu-id="94aad-192">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="94aad-192">Click **Create**.</span></span>
 
### <a name="creating-a-novatus-test-user"></a><span data-ttu-id="94aad-193">Creación de un usuario de prueba de Novatus</span><span class="sxs-lookup"><span data-stu-id="94aad-193">Creating a Novatus test user</span></span>

<span data-ttu-id="94aad-194">objetivo de Hola de esta sección es un usuario llamado a Britta Simon en Novatus toocreate.</span><span class="sxs-lookup"><span data-stu-id="94aad-194">hello objective of this section is toocreate a user called Britta Simon in Novatus.</span></span> <span data-ttu-id="94aad-195">Novatus admite el aprovisionamiento Just-In-Time, que está habilitado de forma predeterminada.</span><span class="sxs-lookup"><span data-stu-id="94aad-195">Novatus supports just-in-time provisioning, which is by default enabled.</span></span>

<span data-ttu-id="94aad-196">No hay ningún elemento de acción para usted en esta sección.</span><span class="sxs-lookup"><span data-stu-id="94aad-196">There is no action item for you in this section.</span></span> <span data-ttu-id="94aad-197">Si no existe todavía, se creará un nuevo usuario durante un tooaccess intento Novatus.</span><span class="sxs-lookup"><span data-stu-id="94aad-197">A new user will be created during an attempt tooaccess Novatus if it doesn't exist yet.</span></span>

>[!NOTE]
><span data-ttu-id="94aad-198">Si necesita un usuario toocreate manualmente, necesita hello toocontact [equipo de soporte técnico Novatus](mailto:jvinci@novatusinc.com).</span><span class="sxs-lookup"><span data-stu-id="94aad-198">If you need toocreate an user manually, you need toocontact hello [Novatus support team](mailto:jvinci@novatusinc.com).</span></span> 
> 

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="94aad-199">Asignación de usuario de prueba de hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="94aad-199">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="94aad-200">En esta sección, se habilita Britta Simon toouse un inicio de sesión único Azure concediendo acceso tooNovatus.</span><span class="sxs-lookup"><span data-stu-id="94aad-200">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooNovatus.</span></span>

![Asignar usuario][200] 

<span data-ttu-id="94aad-202">**tooassign Britta Simon tooNovatus, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="94aad-202">**tooassign Britta Simon tooNovatus, perform hello following steps:**</span></span>

1. <span data-ttu-id="94aad-203">Hola portal de Azure, abra la vista de aplicaciones de hello y, a continuación, navegue a vista de directorio toohello y vaya demasiado**aplicaciones empresariales** , a continuación, haga clic en **todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="94aad-203">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Asignar usuario][201] 

2. <span data-ttu-id="94aad-205">En la lista de aplicaciones de hello, seleccione **Novatus**.</span><span class="sxs-lookup"><span data-stu-id="94aad-205">In hello applications list, select **Novatus**.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-novatus-tutorial/tutorial_novatus_app.png) 

3. <span data-ttu-id="94aad-207">En el menú de Hola Hola izquierda, haga clic en **usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="94aad-207">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Asignar usuario][202] 

4. <span data-ttu-id="94aad-209">Haga clic en el botón **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="94aad-209">Click **Add** button.</span></span> <span data-ttu-id="94aad-210">Después, seleccione **Usuarios y grupos** en el cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="94aad-210">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Asignar usuario][203]

5. <span data-ttu-id="94aad-212">En **usuarios y grupos** cuadro de diálogo, seleccione **Britta Simon** en la lista de usuarios de Hola.</span><span class="sxs-lookup"><span data-stu-id="94aad-212">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="94aad-213">Haga clic en el botón **Seleccionar** del cuadro de diálogo **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="94aad-213">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="94aad-214">Haga clic en el botón **Asignar** del cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="94aad-214">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="94aad-215">Prueba del inicio de sesión único </span><span class="sxs-lookup"><span data-stu-id="94aad-215">Testing single sign-on</span></span>

<span data-ttu-id="94aad-216">objetivo de Hola de esta sección es tootest su configuración de inicio de sesión único de Azure AD mediante Hola Panel de acceso.</span><span class="sxs-lookup"><span data-stu-id="94aad-216">hello objective of this section is tootest your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="94aad-217">Al hacer clic en hello Novatus el icono Panel de acceso de hello, debería obtener automáticamente ha iniciado sesión tooyour Novatus aplicación.</span><span class="sxs-lookup"><span data-stu-id="94aad-217">When you click hello Novatus tile in hello Access Panel, you should get automatically signed-on tooyour Novatus application.</span></span> <span data-ttu-id="94aad-218">Para obtener más información acerca de hello Panel de acceso, consulte [Introducción toohello Panel de acceso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="94aad-218">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="94aad-219">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="94aad-219">Additional resources</span></span>

* [<span data-ttu-id="94aad-220">Lista de tutoriales sobre cómo tooIntegrate aplicaciones de SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="94aad-220">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="94aad-221">¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="94aad-221">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-novatus-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-novatus-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-novatus-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-novatus-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-novatus-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-novatus-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-novatus-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-novatus-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-novatus-tutorial/tutorial_general_203.png

