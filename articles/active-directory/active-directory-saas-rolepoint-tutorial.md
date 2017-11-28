---
title: "Tutorial: Integración de Azure Active Directory con RolePoint | Microsoft Docs"
description: "Obtenga información acerca de cómo tooconfigure inicio de sesión único entre Azure Active Directory y RolePoint."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 68d37f40-15da-45f5-a9e1-d53f78e786d1
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/27/2017
ms.author: jeedes
ms.openlocfilehash: 8629dd87c17d44ab89251ebbd19156c6d6cbedc5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-rolepoint"></a><span data-ttu-id="f33bb-103">Tutorial: Integración de Azure Active Directory con RolePoint</span><span class="sxs-lookup"><span data-stu-id="f33bb-103">Tutorial: Azure Active Directory integration with RolePoint</span></span>

<span data-ttu-id="f33bb-104">En este tutorial, aprenderá cómo toointegrate RolePoint con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="f33bb-104">In this tutorial, you learn how toointegrate RolePoint with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="f33bb-105">Integración RolePoint con Azure AD proporciona Hola siguientes ventajas:</span><span class="sxs-lookup"><span data-stu-id="f33bb-105">Integrating RolePoint with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="f33bb-106">Puede controlar en Azure AD que tenga acceso tooRolePoint</span><span class="sxs-lookup"><span data-stu-id="f33bb-106">You can control in Azure AD who has access tooRolePoint</span></span>
- <span data-ttu-id="f33bb-107">Puede habilitar los usuarios tooautomatically get ha iniciado sesión tooRolePoint (Single Sign-On) con sus cuentas de Azure AD</span><span class="sxs-lookup"><span data-stu-id="f33bb-107">You can enable your users tooautomatically get signed-on tooRolePoint (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="f33bb-108">Puede administrar las cuentas en una ubicación central: Hola portal de Azure</span><span class="sxs-lookup"><span data-stu-id="f33bb-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="f33bb-109">Si desea obtener más información acerca de la integración de aplicaciones de SaaS con Azure AD tooknow, consulte [¿qué es acceso a la aplicación y el inicio de sesión único con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="f33bb-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="f33bb-110">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="f33bb-110">Prerequisites</span></span>

<span data-ttu-id="f33bb-111">integración de Azure AD con RolePoint tooconfigure, necesita Hola siguientes elementos:</span><span class="sxs-lookup"><span data-stu-id="f33bb-111">tooconfigure Azure AD integration with RolePoint, you need hello following items:</span></span>

- <span data-ttu-id="f33bb-112">Una suscripción de Azure AD</span><span class="sxs-lookup"><span data-stu-id="f33bb-112">An Azure AD subscription</span></span>
- <span data-ttu-id="f33bb-113">Una suscripción habilitada para el inicio de sesión único en RolePoint.</span><span class="sxs-lookup"><span data-stu-id="f33bb-113">A RolePoint single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="f33bb-114">Hola tootest los pasos de este tutorial, no se recomienda usar un entorno de producción.</span><span class="sxs-lookup"><span data-stu-id="f33bb-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="f33bb-115">pasos de hello tootest en este tutorial, debe seguir estas recomendaciones:</span><span class="sxs-lookup"><span data-stu-id="f33bb-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="f33bb-116">No use el entorno de producción, salvo que sea necesario.</span><span class="sxs-lookup"><span data-stu-id="f33bb-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="f33bb-117">Si no dispone de un entorno de prueba de Azure AD, puede obtener una versión de prueba de un mes [aquí](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="f33bb-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="f33bb-118">Descripción del escenario</span><span class="sxs-lookup"><span data-stu-id="f33bb-118">Scenario description</span></span>
<span data-ttu-id="f33bb-119">En este tutorial, puede probar el inicio de sesión único de Azure AD en un entorno de prueba.</span><span class="sxs-lookup"><span data-stu-id="f33bb-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="f33bb-120">escenario de Hello descrito en este tutorial consta de dos bloques principales:</span><span class="sxs-lookup"><span data-stu-id="f33bb-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="f33bb-121">Agregar RolePoint desde la Galería de Hola</span><span class="sxs-lookup"><span data-stu-id="f33bb-121">Adding RolePoint from hello gallery</span></span>
2. <span data-ttu-id="f33bb-122">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="f33bb-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-rolepoint-from-hello-gallery"></a><span data-ttu-id="f33bb-123">Agregar RolePoint desde la Galería de Hola</span><span class="sxs-lookup"><span data-stu-id="f33bb-123">Adding RolePoint from hello gallery</span></span>
<span data-ttu-id="f33bb-124">integración de hello tooconfigure de RolePoint en Azure AD, deberá tooadd RolePoint de lista de tooyour Hola Galería de aplicaciones administradas de SaaS.</span><span class="sxs-lookup"><span data-stu-id="f33bb-124">tooconfigure hello integration of RolePoint into Azure AD, you need tooadd RolePoint from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="f33bb-125">**tooadd RolePoint de galería de hello, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="f33bb-125">**tooadd RolePoint from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="f33bb-126">Hola  **[portal de Azure](https://portal.azure.com)**, en el panel de navegación izquierdo de Hola, haga clic en **Azure Active Directory** icono.</span><span class="sxs-lookup"><span data-stu-id="f33bb-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="f33bb-128">Navegue demasiado**aplicaciones empresariales**.</span><span class="sxs-lookup"><span data-stu-id="f33bb-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="f33bb-129">A continuación, vaya demasiado**todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="f33bb-129">Then go too**All applications**.</span></span>

    ![Aplicaciones][2]
    
3. <span data-ttu-id="f33bb-131">tooadd nueva aplicación, haga clic en **nueva aplicación** botón en la parte superior de saludo del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="f33bb-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Aplicaciones][3]

4. <span data-ttu-id="f33bb-133">En el cuadro de búsqueda de hello, escriba **RolePoint**.</span><span class="sxs-lookup"><span data-stu-id="f33bb-133">In hello search box, type **RolePoint**.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-rolepoint-tutorial/tutorial_rolepoint_search.png)

5. <span data-ttu-id="f33bb-135">En el panel de resultados de hello, seleccione **RolePoint**y, a continuación, haga clic en **agregar** botón aplicación hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="f33bb-135">In hello results panel, select **RolePoint**, and then click **Add** button tooadd hello application.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-rolepoint-tutorial/tutorial_rolepoint_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="f33bb-137">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="f33bb-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="f33bb-138">En esta sección, configurará y probará el inicio de sesión único de Azure AD con RolePoint con un usuario de prueba llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="f33bb-138">In this section, you configure and test Azure AD single sign-on with RolePoint based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="f33bb-139">Para toowork de inicio de sesión único, Azure AD necesita tooknow qué usuario equivalente de hello en RolePoint es tooa usuario en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="f33bb-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in RolePoint is tooa user in Azure AD.</span></span> <span data-ttu-id="f33bb-140">En otras palabras, una relación de vínculo entre un usuario de Azure AD y el usuario relacionado de hello en RolePoint debe toobe establecido.</span><span class="sxs-lookup"><span data-stu-id="f33bb-140">In other words, a link relationship between an Azure AD user and hello related user in RolePoint needs toobe established.</span></span>

<span data-ttu-id="f33bb-141">Esta relación de vínculo se establece mediante la asignación de valor de Hola de hello **nombre de usuario** en Azure AD como valor de Hola de hello **nombre de usuario** en RolePoint.</span><span class="sxs-lookup"><span data-stu-id="f33bb-141">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in RolePoint.</span></span>

<span data-ttu-id="f33bb-142">tooconfigure y prueba de inicio de sesión único en Azure AD con RolePoint, deberá hello toocomplete después de bloques de creación:</span><span class="sxs-lookup"><span data-stu-id="f33bb-142">tooconfigure and test Azure AD single sign-on with RolePoint, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="f33bb-143">**[Configuración de Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable la toouse usuarios esta característica.</span><span class="sxs-lookup"><span data-stu-id="f33bb-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="f33bb-144">**[Crear un usuario de prueba de Azure AD](#creating-an-azure-ad-test-user)**  -inicio de sesión único en Azure AD tootest con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="f33bb-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="f33bb-145">**[Crear un usuario de prueba RolePoint](#creating-a-rolepoint-test-user)**  -toohave un equivalente de Britta Simon en RolePoint que es la representación toohello vinculado Azure AD del usuario.</span><span class="sxs-lookup"><span data-stu-id="f33bb-145">**[Creating a RolePoint test user](#creating-a-rolepoint-test-user)** - toohave a counterpart of Britta Simon in RolePoint that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="f33bb-146">**[Asignar usuario de prueba de hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="f33bb-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="f33bb-147">**[Pruebas de Single Sign-On](#testing-single-sign-on)**  -tooverify Hola si funciona la configuración.</span><span class="sxs-lookup"><span data-stu-id="f33bb-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="f33bb-148">Configuración del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="f33bb-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="f33bb-149">En esta sección, habilitar inicio de sesión único en Azure AD en hello portal de Azure y configurar el inicio de sesión único en la aplicación RolePoint.</span><span class="sxs-lookup"><span data-stu-id="f33bb-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your RolePoint application.</span></span>

<span data-ttu-id="f33bb-150">**inicio de sesión único en Azure AD tooconfigure con RolePoint, realizar Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="f33bb-150">**tooconfigure Azure AD single sign-on with RolePoint, perform hello following steps:**</span></span>

1. <span data-ttu-id="f33bb-151">En el portal de Azure, en Hola Hola **RolePoint** página de integración de aplicaciones, haga clic en **inicio de sesión único**.</span><span class="sxs-lookup"><span data-stu-id="f33bb-151">In hello Azure portal, on hello **RolePoint** application integration page, click **Single sign-on**.</span></span>

    ![Configurar inicio de sesión único][4]

2. <span data-ttu-id="f33bb-153">En hello **inicio de sesión único** cuadro de diálogo, seleccione **modo** como **sesión basado en SAML** tooenable inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="f33bb-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurar inicio de sesión único](./media/active-directory-saas-rolepoint-tutorial/tutorial_rolepoint_samlbase.png)

3. <span data-ttu-id="f33bb-155">En hello **RolePoint dominio y las direcciones URL** sección, lleve a cabo Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="f33bb-155">On hello **RolePoint Domain and URLs** section, perform hello following steps:</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-rolepoint-tutorial/tutorial_rolepoint_url.png)

    <span data-ttu-id="f33bb-157">a.</span><span class="sxs-lookup"><span data-stu-id="f33bb-157">a.</span></span> <span data-ttu-id="f33bb-158">Hola **dirección URL de inicio de sesión** cuadro de texto, escriba una dirección URL usando Hola siguiente patrón:`https://<subdomain>.rolepoint.com/login`</span><span class="sxs-lookup"><span data-stu-id="f33bb-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<subdomain>.rolepoint.com/login`</span></span>
    
    <span data-ttu-id="f33bb-159">b.</span><span class="sxs-lookup"><span data-stu-id="f33bb-159">b.</span></span> <span data-ttu-id="f33bb-160">Hola **identificador** cuadro de texto, escriba una dirección URL usando Hola siguiente patrón:`https://app.rolepoint.com/<instancename>`</span><span class="sxs-lookup"><span data-stu-id="f33bb-160">In hello **Identifier** textbox, type a URL using hello following pattern: `https://app.rolepoint.com/<instancename>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="f33bb-161">Estos valores no son Hola real.</span><span class="sxs-lookup"><span data-stu-id="f33bb-161">These values are not hello real.</span></span> <span data-ttu-id="f33bb-162">Actualizar estos valores con URL de inicio de sesión real de Hola y el identificador.</span><span class="sxs-lookup"><span data-stu-id="f33bb-162">Update these values with hello actual Sign-on URL and Identifier.</span></span> <span data-ttu-id="f33bb-163">Aquí le sugerimos valor único de hello toouse de cadena en hello Identifier.Contact [equipo de soporte técnico de RolePoint](mailto:info@rolepoint.com) tooget valor de Hola.</span><span class="sxs-lookup"><span data-stu-id="f33bb-163">Here we suggest you toouse hello unique value of string in hello Identifier.Contact [RolePoint support team](mailto:info@rolepoint.com) tooget hello value.</span></span> 
 
4. <span data-ttu-id="f33bb-164">En hello **el certificado de firma de SAML** sección, haga clic en **Metadata XML** y, a continuación, guarde el archivo de metadatos de hello en el equipo.</span><span class="sxs-lookup"><span data-stu-id="f33bb-164">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-rolepoint-tutorial/tutorial_rolepoint_certificate.png) 

5. <span data-ttu-id="f33bb-166">Haga clic en el botón **Guardar** .</span><span class="sxs-lookup"><span data-stu-id="f33bb-166">Click **Save** button.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-rolepoint-tutorial/tutorial_general_400.png)


6. <span data-ttu-id="f33bb-168">tooconfigure inicio de sesión único en **RolePoint** lado, necesita hello toosend descargado **Metadata XML** demasiado[equipo de soporte técnico de RolePoint](mailto:info@rolepoint.com).</span><span class="sxs-lookup"><span data-stu-id="f33bb-168">tooconfigure single sign-on on **RolePoint** side, you need toosend hello downloaded **Metadata XML** too[RolePoint support team](mailto:info@rolepoint.com).</span></span>

> [!TIP]
> <span data-ttu-id="f33bb-169">Ahora puede leer una versión concisa de estas instrucciones dentro de hello [portal de Azure](https://portal.azure.com), mientras que está configurando la aplicación hello!</span><span class="sxs-lookup"><span data-stu-id="f33bb-169">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="f33bb-170">Después de agregar esta aplicación de hello **Active Directory > aplicaciones empresariales** sección, simplemente haga clic en hello **Single Sign-On** Hola de pestaña y acceso incrustado documentación a través de hello  **Configuración** sección final Hola.</span><span class="sxs-lookup"><span data-stu-id="f33bb-170">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="f33bb-171">Puede leer más acerca de características de documentación de embedded Hola aquí: [Azure AD incrustado documentación]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="f33bb-171">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="f33bb-172">Creación de un usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="f33bb-172">Creating an Azure AD test user</span></span>
<span data-ttu-id="f33bb-173">objetivo de Hola de esta sección es un usuario de prueba en hello Azure portal llamado a Britta Simon toocreate.</span><span class="sxs-lookup"><span data-stu-id="f33bb-173">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Creación de un usuario de Azure AD][100]

<span data-ttu-id="f33bb-175">**toocreate un usuario de prueba en Azure AD, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="f33bb-175">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="f33bb-176">Hola **portal de Azure**, en Hola panel de navegación izquierdo, haga clic en **Azure Active Directory** icono.</span><span class="sxs-lookup"><span data-stu-id="f33bb-176">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-rolepoint-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="f33bb-178">lista de hello toodisplay de usuarios, vaya demasiado**usuarios y grupos** y haga clic en **todos los usuarios**.</span><span class="sxs-lookup"><span data-stu-id="f33bb-178">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-rolepoint-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="f33bb-180">Hola tooopen **usuario** cuadro de diálogo, haga clic en **agregar** en la parte superior de saludo del cuadro de diálogo de Hola.</span><span class="sxs-lookup"><span data-stu-id="f33bb-180">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-rolepoint-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="f33bb-182">En hello **usuario** cuadro de diálogo, siga los pasos de hello:</span><span class="sxs-lookup"><span data-stu-id="f33bb-182">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-rolepoint-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="f33bb-184">a.</span><span class="sxs-lookup"><span data-stu-id="f33bb-184">a.</span></span> <span data-ttu-id="f33bb-185">Hola **nombre** cuadro de texto, tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="f33bb-185">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="f33bb-186">b.</span><span class="sxs-lookup"><span data-stu-id="f33bb-186">b.</span></span> <span data-ttu-id="f33bb-187">Hola **nombre de usuario** cuadro de texto, hello tipo **dirección de correo electrónico** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="f33bb-187">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="f33bb-188">c.</span><span class="sxs-lookup"><span data-stu-id="f33bb-188">c.</span></span> <span data-ttu-id="f33bb-189">Seleccione **Mostrar contraseña** y anote el valor de Hola de hello **contraseña**.</span><span class="sxs-lookup"><span data-stu-id="f33bb-189">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="f33bb-190">d.</span><span class="sxs-lookup"><span data-stu-id="f33bb-190">d.</span></span> <span data-ttu-id="f33bb-191">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="f33bb-191">Click **Create**.</span></span>
 
### <a name="creating-a-rolepoint-test-user"></a><span data-ttu-id="f33bb-192">Creación de un usuario de prueba de RolePoint</span><span class="sxs-lookup"><span data-stu-id="f33bb-192">Creating a RolePoint test user</span></span>

<span data-ttu-id="f33bb-193">En esta sección, se crea un usuario denominado Britta Simon en RolePoint.</span><span class="sxs-lookup"><span data-stu-id="f33bb-193">In this section, you create a user called Britta Simon in RolePoint.</span></span> <span data-ttu-id="f33bb-194">Trabajar con [equipo de soporte técnico de RolePoint](mailto:info@rolepoint.com) a los usuarios de tooadd hello en la plataforma de RolePoint Hola.</span><span class="sxs-lookup"><span data-stu-id="f33bb-194">Work with [RolePoint support team](mailto:info@rolepoint.com) tooadd hello users in hello RolePoint platform.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="f33bb-195">Asignación de usuario de prueba de hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="f33bb-195">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="f33bb-196">En esta sección, se habilita Britta Simon toouse un inicio de sesión único Azure concediendo acceso tooRolePoint.</span><span class="sxs-lookup"><span data-stu-id="f33bb-196">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooRolePoint.</span></span>

![Asignar usuario][200] 

<span data-ttu-id="f33bb-198">**tooassign Britta Simon tooRolePoint, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="f33bb-198">**tooassign Britta Simon tooRolePoint, perform hello following steps:**</span></span>

1. <span data-ttu-id="f33bb-199">Hola portal de Azure, abra la vista de aplicaciones de hello y, a continuación, navegue a vista de directorio toohello y vaya demasiado**aplicaciones empresariales** , a continuación, haga clic en **todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="f33bb-199">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Asignar usuario][201] 

2. <span data-ttu-id="f33bb-201">En la lista de aplicaciones de hello, seleccione **RolePoint**.</span><span class="sxs-lookup"><span data-stu-id="f33bb-201">In hello applications list, select **RolePoint**.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-rolepoint-tutorial/tutorial_rolepoint_app.png) 

3. <span data-ttu-id="f33bb-203">En el menú de Hola Hola izquierda, haga clic en **usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="f33bb-203">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Asignar usuario][202] 

4. <span data-ttu-id="f33bb-205">Haga clic en el botón **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="f33bb-205">Click **Add** button.</span></span> <span data-ttu-id="f33bb-206">Después, seleccione **Usuarios y grupos** en el cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="f33bb-206">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Asignar usuario][203]

5. <span data-ttu-id="f33bb-208">En **usuarios y grupos** cuadro de diálogo, seleccione **Britta Simon** en la lista de usuarios de Hola.</span><span class="sxs-lookup"><span data-stu-id="f33bb-208">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="f33bb-209">Haga clic en el botón **Seleccionar** del cuadro de diálogo **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="f33bb-209">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="f33bb-210">Haga clic en el botón **Asignar** del cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="f33bb-210">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="f33bb-211">Prueba del inicio de sesión único </span><span class="sxs-lookup"><span data-stu-id="f33bb-211">Testing single sign-on</span></span>

<span data-ttu-id="f33bb-212">En esta sección, comprobará su único inicio de sesión en configuración de Azure AD con hello Panel de acceso.</span><span class="sxs-lookup"><span data-stu-id="f33bb-212">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="f33bb-213">Al hacer clic en icono de RolePoint Hola Hola Panel de acceso, deberá obtener automáticamente ha iniciado sesión tooyour RolePoint aplicación.</span><span class="sxs-lookup"><span data-stu-id="f33bb-213">When you click hello RolePoint tile in hello Access Panel, you should get automatically signed-on tooyour RolePoint application.</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="f33bb-214">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="f33bb-214">Additional resources</span></span>

* [<span data-ttu-id="f33bb-215">Lista de tutoriales sobre cómo tooIntegrate aplicaciones de SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="f33bb-215">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="f33bb-216">¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="f33bb-216">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-rolepoint-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-rolepoint-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-rolepoint-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-rolepoint-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-rolepoint-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-rolepoint-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-rolepoint-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-rolepoint-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-rolepoint-tutorial/tutorial_general_203.png

