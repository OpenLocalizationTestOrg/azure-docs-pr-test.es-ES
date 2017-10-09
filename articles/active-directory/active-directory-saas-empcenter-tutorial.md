---
title: "Tutorial: Integración de Azure Active Directory con EmpCenter | Microsoft Docs"
description: "Obtenga información acerca de cómo tooconfigure inicio de sesión único entre Azure Active Directory y EmpCenter."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: a00ecf6e-917a-4284-b998-41506931585e
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/14/2017
ms.author: jeedes
ms.openlocfilehash: cce5d86db550327eb73660fb78cea7e6d5428890
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-empcenter"></a><span data-ttu-id="eb408-103">Tutorial: integración de Azure Active Directory con EmpCenter</span><span class="sxs-lookup"><span data-stu-id="eb408-103">Tutorial: Azure Active Directory integration with EmpCenter</span></span>

<span data-ttu-id="eb408-104">En este tutorial, aprenderá cómo toointegrate EmpCenter con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="eb408-104">In this tutorial, you learn how toointegrate EmpCenter with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="eb408-105">Integración EmpCenter con Azure AD proporciona Hola siguientes ventajas:</span><span class="sxs-lookup"><span data-stu-id="eb408-105">Integrating EmpCenter with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="eb408-106">Puede controlar en Azure AD que tenga acceso tooEmpCenter</span><span class="sxs-lookup"><span data-stu-id="eb408-106">You can control in Azure AD who has access tooEmpCenter</span></span>
- <span data-ttu-id="eb408-107">Puede habilitar los usuarios tooautomatically get ha iniciado sesión tooEmpCenter (Single Sign-On) con sus cuentas de Azure AD</span><span class="sxs-lookup"><span data-stu-id="eb408-107">You can enable your users tooautomatically get signed-on tooEmpCenter (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="eb408-108">Puede administrar las cuentas en una ubicación central: Hola portal de Azure</span><span class="sxs-lookup"><span data-stu-id="eb408-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="eb408-109">Si desea obtener más información acerca de la integración de aplicaciones de SaaS con Azure AD tooknow, consulte [¿qué es acceso a la aplicación y el inicio de sesión único con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="eb408-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="eb408-110">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="eb408-110">Prerequisites</span></span>

<span data-ttu-id="eb408-111">integración de Azure AD con EmpCenter tooconfigure, necesita Hola siguientes elementos:</span><span class="sxs-lookup"><span data-stu-id="eb408-111">tooconfigure Azure AD integration with EmpCenter, you need hello following items:</span></span>

- <span data-ttu-id="eb408-112">Una suscripción de Azure AD</span><span class="sxs-lookup"><span data-stu-id="eb408-112">An Azure AD subscription</span></span>
- <span data-ttu-id="eb408-113">Una suscripción habilitada para el inicio de sesión único en EmpCenter</span><span class="sxs-lookup"><span data-stu-id="eb408-113">An EmpCenter single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="eb408-114">Hola tootest los pasos de este tutorial, no se recomienda usar un entorno de producción.</span><span class="sxs-lookup"><span data-stu-id="eb408-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="eb408-115">pasos de hello tootest en este tutorial, debe seguir estas recomendaciones:</span><span class="sxs-lookup"><span data-stu-id="eb408-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="eb408-116">No use el entorno de producción, salvo que sea necesario.</span><span class="sxs-lookup"><span data-stu-id="eb408-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="eb408-117">Si no dispone de un entorno de prueba de Azure AD, aquí puede obtener una versión de evaluación de un mes: [Oferta de prueba](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="eb408-117">If you don't have an Azure AD trial environment, you can get a one-month trial here: [Trial offer](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="eb408-118">Descripción del escenario</span><span class="sxs-lookup"><span data-stu-id="eb408-118">Scenario description</span></span>
<span data-ttu-id="eb408-119">En este tutorial, puede probar el inicio de sesión único de Azure AD en un entorno de prueba.</span><span class="sxs-lookup"><span data-stu-id="eb408-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="eb408-120">escenario de Hello descrito en este tutorial consta de dos bloques principales:</span><span class="sxs-lookup"><span data-stu-id="eb408-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="eb408-121">Agregar EmpCenter desde la Galería de Hola</span><span class="sxs-lookup"><span data-stu-id="eb408-121">Adding EmpCenter from hello gallery</span></span>
2. <span data-ttu-id="eb408-122">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="eb408-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-empcenter-from-hello-gallery"></a><span data-ttu-id="eb408-123">Agregar EmpCenter desde la Galería de Hola</span><span class="sxs-lookup"><span data-stu-id="eb408-123">Adding EmpCenter from hello gallery</span></span>
<span data-ttu-id="eb408-124">integración de hello tooconfigure de EmpCenter en Azure AD, deberá tooadd EmpCenter de lista de tooyour Hola Galería de aplicaciones administradas de SaaS.</span><span class="sxs-lookup"><span data-stu-id="eb408-124">tooconfigure hello integration of EmpCenter into Azure AD, you need tooadd EmpCenter from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="eb408-125">**tooadd EmpCenter de galería de hello, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="eb408-125">**tooadd EmpCenter from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="eb408-126">Hola  **[portal de Azure](https://portal.azure.com)**, en el panel de navegación izquierdo de Hola, haga clic en **Azure Active Directory** icono.</span><span class="sxs-lookup"><span data-stu-id="eb408-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="eb408-128">Navegue demasiado**aplicaciones empresariales**.</span><span class="sxs-lookup"><span data-stu-id="eb408-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="eb408-129">A continuación, vaya demasiado**todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="eb408-129">Then go too**All applications**.</span></span>

    ![Aplicaciones][2]
    
3. <span data-ttu-id="eb408-131">tooadd nueva aplicación, haga clic en **nueva aplicación** botón en la parte superior de saludo del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="eb408-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Aplicaciones][3]

4. <span data-ttu-id="eb408-133">En el cuadro de búsqueda de hello, escriba **EmpCenter**.</span><span class="sxs-lookup"><span data-stu-id="eb408-133">In hello search box, type **EmpCenter**.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-EmpCenter-tutorial/tutorial_EmpCenter_search.png)

5. <span data-ttu-id="eb408-135">En el panel de resultados de hello, seleccione **EmpCenter**y, a continuación, haga clic en **agregar** botón aplicación hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="eb408-135">In hello results panel, select **EmpCenter**, and then click **Add** button tooadd hello application.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-EmpCenter-tutorial/tutorial_EmpCenter_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="eb408-137">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="eb408-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="eb408-138">En esta sección, se configura y se prueba el inicio de sesión único de Azure AD con EmpCenter con un usuario de prueba llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="eb408-138">In this section, you configure and test Azure AD single sign-on with EmpCenter based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="eb408-139">Para toowork de inicio de sesión único, Azure AD necesita tooknow qué usuario equivalente de hello en EmpCenter es tooa usuario en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="eb408-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in EmpCenter is tooa user in Azure AD.</span></span> <span data-ttu-id="eb408-140">En otras palabras, una relación de vínculo entre un usuario de Azure AD y el usuario relacionado de hello en EmpCenter debe toobe establecido.</span><span class="sxs-lookup"><span data-stu-id="eb408-140">In other words, a link relationship between an Azure AD user and hello related user in EmpCenter needs toobe established.</span></span>

<span data-ttu-id="eb408-141">En EmpCenter, asigne el valor de Hola de hello **nombre de usuario** en Azure AD como valor de Hola de hello **nombre de usuario** tooestablish la relación de vínculo de Hola.</span><span class="sxs-lookup"><span data-stu-id="eb408-141">In EmpCenter, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="eb408-142">tooconfigure y prueba de inicio de sesión único en Azure AD con EmpCenter, deberá hello toocomplete después de bloques de creación:</span><span class="sxs-lookup"><span data-stu-id="eb408-142">tooconfigure and test Azure AD single sign-on with EmpCenter, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="eb408-143">**[Configuración de Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable la toouse usuarios esta característica.</span><span class="sxs-lookup"><span data-stu-id="eb408-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="eb408-144">**[Crear un usuario de prueba de Azure AD](#creating-an-azure-ad-test-user)**  -inicio de sesión único en Azure AD tootest con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="eb408-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="eb408-145">**[Creación de un usuario de prueba EmpCenter](#creating-an-empcenter-test-user)**  -toohave un equivalente de Britta Simon en EmpCenter que es la representación toohello vinculado Azure AD del usuario.</span><span class="sxs-lookup"><span data-stu-id="eb408-145">**[Creating an EmpCenter test user](#creating-an-empcenter-test-user)** - toohave a counterpart of Britta Simon in EmpCenter that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="eb408-146">**[Asignar usuario de prueba de hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="eb408-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="eb408-147">**[Pruebas de Single Sign-On](#testing-single-sign-on)**  -tooverify Hola si funciona la configuración.</span><span class="sxs-lookup"><span data-stu-id="eb408-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="eb408-148">Configuración del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="eb408-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="eb408-149">En esta sección, habilitar inicio de sesión único en Azure AD en hello portal de Azure y configurar el inicio de sesión único en la aplicación EmpCenter.</span><span class="sxs-lookup"><span data-stu-id="eb408-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your EmpCenter application.</span></span>

<span data-ttu-id="eb408-150">**inicio de sesión único en Azure AD tooconfigure con EmpCenter, realizar Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="eb408-150">**tooconfigure Azure AD single sign-on with EmpCenter, perform hello following steps:**</span></span>

1. <span data-ttu-id="eb408-151">En el portal de Azure, en Hola Hola **EmpCenter** página de integración de aplicaciones, haga clic en **inicio de sesión único**.</span><span class="sxs-lookup"><span data-stu-id="eb408-151">In hello Azure portal, on hello **EmpCenter** application integration page, click **Single sign-on**.</span></span>

    ![Configurar inicio de sesión único][4]

2. <span data-ttu-id="eb408-153">En hello **inicio de sesión único** cuadro de diálogo, seleccione **modo** como **sesión basado en SAML** tooenable inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="eb408-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurar inicio de sesión único](./media/active-directory-saas-EmpCenter-tutorial/tutorial_EmpCenter_samlbase.png)

3. <span data-ttu-id="eb408-155">En hello **EmpCenter dominio y las direcciones URL** sección, lleve a cabo Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="eb408-155">On hello **EmpCenter Domain and URLs** section, perform hello following steps:</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-EmpCenter-tutorial/tutorial_EmpCenter_url.png)

    <span data-ttu-id="eb408-157">Hola **dirección URL de inicio de sesión** cuadro de texto, escriba una dirección URL usando Hola siguiente patrón:</span><span class="sxs-lookup"><span data-stu-id="eb408-157">In hello **Sign-on URL** textbox, type a URL using hello following pattern:</span></span>
    | |
    |--|
    | `https://<subdomain>.EmpCenter.com/<instancename>` |
    | `https://<subdomain>.workforcehosting.com/<instancename>` |

    > [!NOTE] 
    > <span data-ttu-id="eb408-158">valor de Hello no es real.</span><span class="sxs-lookup"><span data-stu-id="eb408-158">hello value is not real.</span></span> <span data-ttu-id="eb408-159">Valor de Hola de actualización con Hola dirección URL de inicio de sesión real.</span><span class="sxs-lookup"><span data-stu-id="eb408-159">Update hello value with hello actual Sign-On URL.</span></span> <span data-ttu-id="eb408-160">Póngase en contacto con [equipo de soporte técnico de EmpCenter cliente](http://www.workforcesoftware.com/services/customer-support/) valor de hello tooget.</span><span class="sxs-lookup"><span data-stu-id="eb408-160">Contact [EmpCenter Client support team](http://www.workforcesoftware.com/services/customer-support/) tooget hello value.</span></span> 
 
4. <span data-ttu-id="eb408-161">En hello **el certificado de firma de SAML** sección, haga clic en **Metadata XML** y, a continuación, guarde el archivo de metadatos de hello en el equipo.</span><span class="sxs-lookup"><span data-stu-id="eb408-161">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-EmpCenter-tutorial/tutorial_EmpCenter_certificate.png) 

5. <span data-ttu-id="eb408-163">Haga clic en el botón **Guardar** .</span><span class="sxs-lookup"><span data-stu-id="eb408-163">Click **Save** button.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-EmpCenter-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="eb408-165">tooconfigure inicio de sesión único en **EmpCenter** lado, necesita hello toosend descargado **Metadata XML** demasiado[equipo de soporte técnico de EmpCenter](http://www.workforcesoftware.com/services/customer-support/).</span><span class="sxs-lookup"><span data-stu-id="eb408-165">tooconfigure single sign-on on **EmpCenter** side, you need toosend hello downloaded **Metadata XML** too[EmpCenter support team](http://www.workforcesoftware.com/services/customer-support/).</span></span> <span data-ttu-id="eb408-166">Establecen esta Hola de toohave configuración configurada correctamente en ambos lados de la conexión de SSO de SAML.</span><span class="sxs-lookup"><span data-stu-id="eb408-166">They set this setting toohave hello SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="eb408-167">Ahora puede leer una versión concisa de estas instrucciones dentro de hello [portal de Azure](https://portal.azure.com), mientras que está configurando la aplicación hello!</span><span class="sxs-lookup"><span data-stu-id="eb408-167">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="eb408-168">Después de agregar esta aplicación de hello **Active Directory > aplicaciones empresariales** sección, simplemente haga clic en hello **Single Sign-On** Hola de pestaña y acceso incrustado documentación a través de hello  **Configuración** sección final Hola.</span><span class="sxs-lookup"><span data-stu-id="eb408-168">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="eb408-169">Puede leer más acerca de características de documentación de embedded Hola aquí: [Azure AD incrustado documentación]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="eb408-169">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="eb408-170">Creación de un usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="eb408-170">Creating an Azure AD test user</span></span>
<span data-ttu-id="eb408-171">objetivo de Hola de esta sección es un usuario de prueba en hello Azure portal llamado a Britta Simon toocreate.</span><span class="sxs-lookup"><span data-stu-id="eb408-171">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Creación de un usuario de Azure AD][100]

<span data-ttu-id="eb408-173">**toocreate un usuario de prueba en Azure AD, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="eb408-173">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="eb408-174">Hola **portal de Azure**, en Hola panel de navegación izquierdo, haga clic en **Azure Active Directory** icono.</span><span class="sxs-lookup"><span data-stu-id="eb408-174">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-EmpCenter-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="eb408-176">lista de hello toodisplay de usuarios, vaya demasiado**usuarios y grupos** y haga clic en **todos los usuarios**.</span><span class="sxs-lookup"><span data-stu-id="eb408-176">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-EmpCenter-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="eb408-178">Hola tooopen **usuario** cuadro de diálogo, haga clic en **agregar** en la parte superior de saludo del cuadro de diálogo de Hola.</span><span class="sxs-lookup"><span data-stu-id="eb408-178">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-EmpCenter-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="eb408-180">En hello **usuario** cuadro de diálogo, siga los pasos de hello:</span><span class="sxs-lookup"><span data-stu-id="eb408-180">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-EmpCenter-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="eb408-182">a.</span><span class="sxs-lookup"><span data-stu-id="eb408-182">a.</span></span> <span data-ttu-id="eb408-183">Hola **nombre** cuadro de texto, tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="eb408-183">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="eb408-184">b.</span><span class="sxs-lookup"><span data-stu-id="eb408-184">b.</span></span> <span data-ttu-id="eb408-185">Hola **nombre de usuario** cuadro de texto, hello tipo **dirección de correo electrónico** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="eb408-185">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="eb408-186">c.</span><span class="sxs-lookup"><span data-stu-id="eb408-186">c.</span></span> <span data-ttu-id="eb408-187">Seleccione **Mostrar contraseña** y anote el valor de Hola de hello **contraseña**.</span><span class="sxs-lookup"><span data-stu-id="eb408-187">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="eb408-188">d.</span><span class="sxs-lookup"><span data-stu-id="eb408-188">d.</span></span> <span data-ttu-id="eb408-189">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="eb408-189">Click **Create**.</span></span>
 
### <a name="creating-an-empcenter-test-user"></a><span data-ttu-id="eb408-190">Creación de un usuario de prueba EmpCenter</span><span class="sxs-lookup"><span data-stu-id="eb408-190">Creating an EmpCenter test user</span></span>

<span data-ttu-id="eb408-191">En orden tooenable toolog de los usuarios de Azure AD en tooEmpCenter, se les deben aprovisionar en EmpCenter.</span><span class="sxs-lookup"><span data-stu-id="eb408-191">In order tooenable Azure AD users toolog in tooEmpCenter, they must be provisioned into EmpCenter.</span></span> <span data-ttu-id="eb408-192">En caso de hello de EmpCenter, cuentas de usuario de hello debe toobe creado por la [equipo de soporte técnico de EmpCenter](http://www.workforcesoftware.com/services/customer-support/).</span><span class="sxs-lookup"><span data-stu-id="eb408-192">In hello case of EmpCenter, hello user accounts need toobe created by your [EmpCenter support team](http://www.workforcesoftware.com/services/customer-support/).</span></span>

> [!NOTE]
> <span data-ttu-id="eb408-193">Puede usar cualquier otra EmpCenter usuario cuenta herramienta de creación o las API proporcionadas por EmpCenter tooprovision Azure Active Directory las cuentas de usuario.</span><span class="sxs-lookup"><span data-stu-id="eb408-193">You can use any other EmpCenter user account creation tools or APIs provided by EmpCenter tooprovision Azure Active Directory user accounts.</span></span>
> 

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="eb408-194">Asignación de usuario de prueba de hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="eb408-194">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="eb408-195">En esta sección, se habilita Britta Simon toouse un inicio de sesión único Azure concediendo acceso tooEmpCenter.</span><span class="sxs-lookup"><span data-stu-id="eb408-195">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooEmpCenter.</span></span>

![Asignar usuario][200] 

<span data-ttu-id="eb408-197">**tooassign Britta Simon tooEmpCenter, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="eb408-197">**tooassign Britta Simon tooEmpCenter, perform hello following steps:**</span></span>

1. <span data-ttu-id="eb408-198">Hola portal de Azure, abra la vista de aplicaciones de hello y, a continuación, navegue a vista de directorio toohello y vaya demasiado**aplicaciones empresariales** , a continuación, haga clic en **todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="eb408-198">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Asignar usuario][201] 

2. <span data-ttu-id="eb408-200">En la lista de aplicaciones de hello, seleccione **EmpCenter**.</span><span class="sxs-lookup"><span data-stu-id="eb408-200">In hello applications list, select **EmpCenter**.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-EmpCenter-tutorial/tutorial_EmpCenter_app.png) 

3. <span data-ttu-id="eb408-202">En el menú de Hola Hola izquierda, haga clic en **usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="eb408-202">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Asignar usuario][202] 

4. <span data-ttu-id="eb408-204">Haga clic en el botón **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="eb408-204">Click **Add** button.</span></span> <span data-ttu-id="eb408-205">Después, seleccione **Usuarios y grupos** en el cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="eb408-205">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Asignar usuario][203]

5. <span data-ttu-id="eb408-207">En **usuarios y grupos** cuadro de diálogo, seleccione **Britta Simon** en la lista de usuarios de Hola.</span><span class="sxs-lookup"><span data-stu-id="eb408-207">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="eb408-208">Haga clic en el botón **Seleccionar** del cuadro de diálogo **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="eb408-208">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="eb408-209">Haga clic en el botón **Asignar** del cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="eb408-209">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="eb408-210">Prueba del inicio de sesión único </span><span class="sxs-lookup"><span data-stu-id="eb408-210">Testing single sign-on</span></span>


<span data-ttu-id="eb408-211">objetivo de Hola de esta sección es tootest su configuración de inicio de sesión único de Azure AD mediante Hola Panel de acceso.</span><span class="sxs-lookup"><span data-stu-id="eb408-211">hello objective of this section is tootest your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="eb408-212">Al hacer clic en icono de EmpCenter Hola Hola Panel de acceso, deberá obtener automáticamente ha iniciado sesión tooyour EmpCenter aplicación.</span><span class="sxs-lookup"><span data-stu-id="eb408-212">When you click hello EmpCenter tile in hello Access Panel, you should get automatically signed-on tooyour EmpCenter application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="eb408-213">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="eb408-213">Additional resources</span></span>

* [<span data-ttu-id="eb408-214">Lista de tutoriales sobre cómo tooIntegrate aplicaciones de SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="eb408-214">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="eb408-215">¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="eb408-215">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-EmpCenter-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-EmpCenter-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-EmpCenter-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-EmpCenter-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-EmpCenter-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-EmpCenter-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-EmpCenter-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-EmpCenter-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-EmpCenter-tutorial/tutorial_general_203.png

